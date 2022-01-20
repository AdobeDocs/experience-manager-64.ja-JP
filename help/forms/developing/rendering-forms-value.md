---
title: 値別にFormsをレンダリング
seo-title: Rendering Forms By Value
description: Forms API(Java) を使用して、Java API および Web サービス API を使用して値でフォームをレンダリングします。
seo-description: Use the Forms API (Java) to render a form by value using the Java API and Web Service API.
uuid: b932cc54-662f-40ae-94e0-20ac82845f3b
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: operations
discoiquuid: ddbb2b82-4c57-4845-a5be-2435902d312b
role: Developer
exl-id: 50c34781-45e3-4255-a997-44f694527c92
source-git-commit: e608249c3f95f44fdc14b100910fa11ffff5ee32
workflow-type: tm+mt
source-wordcount: '1821'
ht-degree: 3%

---

# 値別にFormsをレンダリング {#rendering-forms-by-value}

通常、Designer で作成されたフォームデザインは、Formsサービスへの参照によって渡されます。 フォームデザインは大きくなる可能性があり、その結果、フォームデザインのバイトを値でマーシャリングする必要がなくなるよう、参照で渡す方がより効率的です。 また、Formsサービスは、キャッシュ時にフォームデザインを継続的に読み取る必要がないように、フォームデザインをキャッシュすることもできます。

フォームデザインに UUID 属性が含まれている場合は、その属性がキャッシュされます。 UUID 値は、すべてのフォームデザインで一意で、フォームを一意に識別するために使用されます。 値でフォームをレンダリングする場合、繰り返し使用する場合にのみフォームをキャッシュする必要があります。 ただし、フォームが繰り返し使用されず、一意である必要がある場合は、AEM Forms API を使用して設定されたキャッシュオプションを使用して、フォームをキャッシュするのを避けることができます。

Formsサービスは、フォームデザイン内のリンクされたコンテンツの場所を解決することもできます。 例えば、フォームデザイン内で参照されるリンク画像は、相対 URL です。 リンクされたコンテンツは、常にフォームデザインの場所を基準とした相対コンテンツと見なされます。 したがって、リンクされたコンテンツを解決するには、フォームデザインの絶対パスを適用して、その場所を決定する必要があります。

参照によってフォームデザインを渡す代わりに、値でフォームデザインを渡すことができます。 フォームデザインを動的に作成する場合、値を指定してフォームデザインを渡すと効率的です。つまり、クライアントアプリケーションが実行時にフォームデザインを作成する XML を生成する場合です。 この場合、フォームデザインはメモリに保存されるので、物理リポジトリに保存されません。 実行時に動的にフォームデザインを作成し、値を指定して渡す場合は、フォームをキャッシュして、Formsサービスのパフォーマンスを向上させることができます。

**値によるフォームの受け渡しの制限**

フォームデザインが値で渡される場合は、次の制限が適用されます。

* フォームデザイン内に相対的にリンクされたコンテンツを含めることはできません。 すべての画像とフラグメントは、フォームデザイン内に埋め込むか、絶対に参照する必要があります。
* フォームのレンダリング後は、サーバー側の計算を実行できません。 フォームがFormsサービスに送り返されると、データが抽出され、サーバー側の計算なしで返されます。
* HTMLは実行時にのみリンク画像を使用できるので、埋め込まれた画像とのHTMLを生成できません。 これは、Formsサービスが参照先のフォームデザインから画像を取得することで、HTML付きの埋め込み画像をサポートするからです。 値で渡されたフォームデザインには参照先がないので、埋め込み画像はHTMLページが表示されているときに抽出できません。 したがって、画像参照は、HTMLでレンダリングする絶対パスにする必要があります。

>[!NOTE]
>
>異なる種類のフォームを値でレンダリングすることもできます ( 例えば、HTMLフォームや、使用権限を含むフォーム ) がありますが、このセクションでは、インタラクティブPDF formsのレンダリングについて説明します。

>[!NOTE]
>
>Formsサービスについて詳しくは、 [AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63).

## 手順の概要 {#summary-of-steps}

値でフォームをレンダリングするには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. Forms Client API オブジェクトを作成します。
1. フォームデザインを参照します。
1. 値でフォームをレンダリングします。
1. フォームデータストリームをクライアントの Web ブラウザーに書き込みます。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。 Web サービスを使用している場合は、プロキシファイルを必ず含めてください。

**Forms Client API オブジェクトの作成**

プログラムによってデータをクライアント API からPDFに読み込む前に、Data Integration Service クライアントを作成する必要があります。 サービスクライアントを作成する場合、サービスを呼び出すために必要な接続設定を定義します。

**フォームデザインの参照**

値でフォームをレンダリングする場合は、 `com.adobe.idp.Document` レンダリングするフォームデザインを含むオブジェクト。 既存の XDP ファイルを参照することも、フォームデザインを動的に作成して `com.adobe.idp.Document` そのデータを使って

>[!NOTE]
>
>このセクションと対応するクイックスタートでは、既存の XDP ファイルを参照します。

**値でフォームをレンダリング**

値でフォームをレンダリングするには、 `com.adobe.idp.Document` レンダリングメソッドの `inDataDoc` パラメーター ( `FormsServiceClient` オブジェクトのレンダリングメソッド ( `renderPDFForm`, `(Deprecated) renderHTMLForm`など )。 このパラメーター値は、通常、フォームとマージされるデータ用に予約されます。 同様に、空の文字列値を `formQuery` パラメーター。 通常、このパラメーターにはフォームデザインの名前を指定する文字列値が必要です。

>[!NOTE]
>
>フォーム内にデータを表示する場合は、 `xfa:datasets` 要素。 XFA アーキテクチャについて詳しくは、 [https://www.pdfa.org/norm-refs/XFA-3_3.pdf](https://www.pdfa.org/norm-refs/XFA-3_3.pdf).

**フォームデータストリームをクライアント Web ブラウザーに書き込む**

Formsサービスは、値でフォームをレンダリングする場合、フォームデータストリームを返します。このストリームは、クライアントの Web ブラウザーに書き込む必要があります。 クライアント Web ブラウザーに書き込まれると、フォームはユーザーに対して表示されます。

**関連トピック**

[Java API を使用した値によるフォームのレンダリング](#render-a-form-by-value-using-the-java-api)

[Web サービス API を使用した値によるフォームのレンダリング](#render-a-form-by-value-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Forms Service API クイックスタート](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Forms Service にドキュメントを渡す](/help/forms/developing/passing-documents-forms-service.md)

[Formsをレンダリングする Web アプリケーションの作成](/help/forms/developing/creating-web-applications-renders-forms.md)

## Java API を使用した値によるフォームのレンダリング {#render-a-form-by-value-using-the-java-api}

Forms API(Java) を使用して値でフォームをレンダリングします。

1. プロジェクトファイルを含める

   Java プロジェクトのクラスパスに、adobe-forms-client.jar などのクライアント JAR ファイルを含めます。

1. Forms Client API オブジェクトの作成

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * の作成 `FormsServiceClient` オブジェクトのコンストラクタを使用し、 `ServiceClientFactory` オブジェクト。

1. フォームデザインの参照

   * の作成 `java.io.FileInputStream` オブジェクト。レンダリングするフォームデザインを表します。このオブジェクトのコンストラクターを使用し、XDP ファイルの場所を指定する string 値を渡します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. 値でフォームをレンダリング

   を呼び出す `FormsServiceClient` オブジェクトの `renderPDFForm` メソッドを使用して、次の値を渡します。

   * 空の文字列値。 （通常、このパラメーターにはフォームデザインの名前を指定する文字列値が必要です）。
   * A `com.adobe.idp.Document` フォームデザインを含むオブジェクト。 通常、このパラメーター値はフォームとマージされるデータ用に予約されます。
   * A `PDFFormRenderSpec` 実行時オプションを保存するオブジェクト。 これはオプションのパラメーターで、 `null` 実行時のオプションを指定しない場合。
   * A `URLSpec` Formsサービスで必要な URI 値を格納するオブジェクト。
   * A `java.util.HashMap` 添付ファイルを保存するオブジェクト。 これはオプションのパラメーターで、 `null` フォームにファイルを添付しない場合。

   この `renderPDFForm` メソッドは、 `FormsResult` クライアントの Web ブラウザーに書き込むことができるフォームデータストリームを含むオブジェクト。

1. フォームデータストリームをクライアント Web ブラウザーに書き込む

   * の作成 `com.adobe.idp.Document` を呼び出すことによってオブジェクトを取得 `FormsResult` オブジェクト `getOutputContent` メソッド。
   * のコンテンツタイプを取得する `com.adobe.idp.Document` オブジェクトを呼び出す `getContentType` メソッド。
   * を `javax.servlet.http.HttpServletResponse` を呼び出すことによるオブジェクトのコンテンツタイプ `setContentType` メソッドを使用して、 `com.adobe.idp.Document` オブジェクト。
   * の作成 `javax.servlet.ServletOutputStream` オブジェクトを使用します。オブジェクトは、 `javax.servlet.http.HttpServletResponse` オブジェクトの `getOutputStream` メソッド。
   * の作成 `java.io.InputStream` を呼び出すことによってオブジェクトを取得 `com.adobe.idp.Document` オブジェクトの `getInputStream` メソッド。
   * バイト配列を作成し、 `InputStream` オブジェクト。 を呼び出す `InputStream` オブジェクトの `available` メソッドを使用して `InputStream` オブジェクト。
   * を呼び出して、フォームデータストリームを byte 配列に入力します。 `InputStream` オブジェクトの `read`メソッドを使用し、バイト配列を引数として渡す。
   * を呼び出す `javax.servlet.ServletOutputStream` オブジェクトの `write` メソッドを使用して、フォームデータストリームをクライアント Web ブラウザーに送信します。 バイト配列を `write` メソッド。

**関連トピック**

[値別にFormsをレンダリング](/help/forms/developing/rendering-forms.md)

[クイックスタート（SOAP モード）:Java API を使用した値によるレンダリング](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-by-value-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Web サービス API を使用した値によるフォームのレンダリング {#render-a-form-by-value-using-the-web-service-api}

Forms API（Web サービス）を使用して値でフォームをレンダリングする：

1. プロジェクトファイルを含める

   * Forms Service WSDL を使用する Java プロキシクラスを作成します。
   * Java プロキシクラスをクラスパスに含めます。

1. Forms Client API オブジェクトの作成

   の作成 `FormsService` オブジェクトを選択し、認証値を設定します。

1. フォームデザインの参照

   * コンストラクタを使用して `java.io.FileInputStream` オブジェクトを作成します。XDP ファイルの場所を指定する string 値を渡します。
   * コンストラクタを使用して `BLOB` オブジェクトを作成します。この `BLOB` オブジェクトは、パスワードで暗号化されたPDF・ドキュメントを保存するために使用されます。
   * コンテンツを格納するバイト配列を作成します。 `java.io.FileInputStream` オブジェクト。 バイト配列のサイズは、 `java.io.FileInputStream` オブジェクトのサイズを `available` メソッド。
   * を呼び出して、バイト配列にストリームデータを入力します。 `java.io.FileInputStream` オブジェクトの `read` メソッドを使用してバイト配列を渡す。
   * 次の項目に `BLOB` オブジェクトを呼び出す `setBinaryData` メソッドを使用してバイト配列を渡す。

1. 値でフォームをレンダリング

   を呼び出す `FormsService` オブジェクトの `renderPDFForm` メソッドを使用して、次の値を渡します。

   * 空の文字列値。 （通常、このパラメーターにはフォームデザインの名前を指定する文字列値が必要です）。
   * A `BLOB` フォームデザインを含むオブジェクト。 通常、このパラメーター値はフォームとマージされるデータ用に予約されます。
   * A `PDFFormRenderSpec` 実行時オプションを保存するオブジェクト。 これはオプションのパラメーターで、 `null` 実行時のオプションを指定しない場合。
   * A `URLSpec` Formsサービスで必要な URI 値を格納するオブジェクト。
   * A `java.util.HashMap` 添付ファイルを保存するオブジェクト。 これはオプションのパラメーターで、 `null` フォームにファイルを添付しない場合。
   * 空 `com.adobe.idp.services.holders.BLOBHolder` メソッドによって設定されるオブジェクト。 これは、レンダリングされたPDFフォームを保存するために使用されます。
   * 空 `javax.xml.rpc.holders.LongHolder` メソッドによって設定されるオブジェクト。 （この引数は、フォームのページ数を保存します）。
   * 空 `javax.xml.rpc.holders.StringHolder` メソッドによって設定されるオブジェクト。 （この引数はロケール値を格納します。）
   * 空 `com.adobe.idp.services.holders.FormsResultHolder` この操作の結果を格納するオブジェクト。

   この `renderPDFForm` メソッドによって `com.adobe.idp.services.holders.FormsResultHolder` オブジェクト。クライアント Web ブラウザーに書き込む必要があるフォームデータストリームを含む最後の引数値として渡されます。

1. フォームデータストリームをクライアント Web ブラウザーに書き込む

   * の作成 `FormResult` オブジェクトを作成するには、 `com.adobe.idp.services.holders.FormsResultHolder` オブジェクトの `value` データメンバー。
   * の作成 `BLOB` を呼び出してフォームデータを含むオブジェクト `FormsResult` オブジェクトの `getOutputContent` メソッド。
   * のコンテンツタイプを取得する `BLOB` オブジェクトを呼び出す `getContentType` メソッド。
   * を `javax.servlet.http.HttpServletResponse` を呼び出すことによるオブジェクトのコンテンツタイプ `setContentType` メソッドを使用して、 `BLOB` オブジェクト。
   * の作成 `javax.servlet.ServletOutputStream` オブジェクトを使用します。オブジェクトは、 `javax.servlet.http.HttpServletResponse` オブジェクトの `getOutputStream` メソッド。
   * バイト配列を作成し、 `BLOB` オブジェクトの `getBinaryData` メソッド。 このタスクは、 `FormsResult` オブジェクトをバイト配列に変換します。
   * を呼び出す `javax.servlet.http.HttpServletResponse` オブジェクトの `write` メソッドを使用して、フォームデータストリームをクライアント Web ブラウザーに送信します。 バイト配列を `write` メソッド。

**関連トピック**

[値別にFormsをレンダリング](#rendering-forms-by-value)

[Base64 エンコーディングを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
