---
title: カスタム CSS ファイルを使用したHTMLFormsのレンダリング
seo-title: Rendering HTML Forms Using Custom CSS Files
description: Formsサービスを使用して、Web ブラウザーからの HTTP 要求に応じてHTMLフォームをレンダリングするカスタム CSS ファイルを参照します。 Java API および WebHTMLAPI を使用して、CSS ファイルを使用するサービスフォームをレンダリングできます。
seo-description: Use the Forms service to refer to custom CSS files to render HTML forms in response to an HTTP request from a web browser. You can render an HTML form that uses a CSS file using the Java API and Web Service API.
uuid: a44e96f1-001d-48a2-8c96-15cb9d0c71b3
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: operations
discoiquuid: 8fe7c072-7df0-44b7-92d0-bf39dc1e688a
role: Developer
exl-id: d10cbb97-1cec-4b1b-9104-48063e75a2cd
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '1674'
ht-degree: 2%

---

# カスタム CSS ファイルを使用したHTMLFormsのレンダリング {#rendering-html-forms-using-custom-css-files}

The Forms service renders HTML forms in response to an HTTP request from a web browser. Formsサービスは、HTMLフォームのレンダリング時にカスタム CSS ファイルを参照できます。 You can create a custom CSS file to meet your business requirements and reference that CSS file when using the Forms service to render HTML forms.

Formsサービスは、カスタム CSS ファイルをサイレントで解析します。 That is, the Forms service does not report errors that may be encountered if the custom CSS file does not comply with CSS standards. この場合、Formsサービスはスタイルを無視し、CSS ファイルに残っているスタイルを使用し続けます。

次のリストでは、カスタム CSS ファイルでサポートされるスタイルを指定します。

* **クラスレベルのセレクタースタイルのペア**:カスタム CSS ファイルに存在する場合は、クラススタイルとしてHTMLフォームで使用されるセレクターが使用されます。 未使用のクラススタイルは無視されます。
* **識別子レベルのセレクタースタイルのペア**:識別子のスタイルが識別子フォームで使用される場合は、すべてのHTMLスタイルが使用されます。
* **要素レベルのセレクタースタイルのペア**:要素スタイルが要素フォームで使用される場合は、すべてのHTMLスタイルを使用します。
* **スタイルの優先度**:スタイルの優先度（重要な場合と同様）はサポートされ、カスタム CSS ファイルで使用できます。
* **メディアタイプ**:1 つ以上のセレクタースタイルのペアを@mediaスタイルでラップして、メディアタイプを定義できます。 Formsサービスは、指定されたメディアタイプがサポートされているかどうかを確認しません。 カスタム CSS ファイルで指定されたメディアタイプが、メディアフォームにHTMLされます。

FormsIVS アプリケーションを使用して、サンプルの CSS ファイルを取得できます。 フォームをアップロードし、「フォームデザインをテスト」ページでフォームを選択して、「CSS を生成」をクリックします。 ボタンをクリックする前に、HTML変換タイプを設定する必要はありません。 次に「保存」を選択します。 この CSS ファイルは、ビジネス要件に合わせて編集できます。

>[!NOTE]
>
>カスタム CSS ファイルを使用するHTMLフォームをレンダリングする前に、HTMLフォームのレンダリングについて十分に理解しておくことが重要です。 ( [FormsをHTMLとしてレンダリング](/help/forms/developing/rendering-forms-html.md).)

>[!NOTE]
>
>Formsサービスについて詳しくは、 [AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63).

## 手順の概要 {#summary-of-steps}

CSS ファイルを使用するHTMLフォームをレンダリングするには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. Forms Java API オブジェクトを作成します。
1. CSS ファイルを参照します。
1. HTMLフォームをレンダリング
1. フォームデータストリームをクライアントの Web ブラウザーに書き込みます。

**プロジェクトファイルを含める**

開発プロジェクトに必要なファイルを含めます。 Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。 Web サービスを使用している場合は、プロキシファイルを必ず含めてください。

**Forms Java API オブジェクトの作成**

Formsサービスでサポートされている操作をプログラムで実行する前に、Formsクライアントオブジェクトを作成する必要があります。

**CSS ファイルの参照**

カスタム CSS ファイルを使用するHTMLフォームをレンダリングするには、必ず既存の CSS ファイルを参照するようにしてください。

**HTMLフォームをレンダリング**

HTMLフォームをレンダリングするには、Designer で作成し、XDP ファイルとして保存したフォームデザインを指定する必要があります。 You must also select an HTML transformation type. 例えば、Internet Explorer 5.0 以降の動的HTMLをレンダリングするHTML変換の種類を指定できます。

HTMLフォームのレンダリングには、他のフォームタイプのレンダリングに必要な URI 値などの値も必要です。

**フォームデータストリームをクライアント Web ブラウザーに書き込む**

FormsサービスがHTMLフォームをレンダリングすると、フォームデータストリームが返されます。このストリームをクライアント Web ブラウザーに書き込み、HTMLフォームをユーザーに表示させる必要があります。

**関連トピック**

[Java API を使用して、CSS ファイルを使用するHTMLフォームをレンダリングする](#render-an-html-form-that-uses-a-css-file-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Forms Service API クイックスタート](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[インタラクティブPDF formsのレンダリング](/help/forms/developing/rendering-interactive-pdf-forms.md)

[FormsをHTMLとしてレンダリング](/help/forms/developing/rendering-forms-html.md)

[Formsをレンダリングする Web アプリケーションの作成](/help/forms/developing/creating-web-applications-renders-forms.md)

## Java API を使用して、CSS ファイルを使用するHTMLフォームをレンダリングする {#render-an-html-form-that-uses-a-css-file-using-the-java-api}

Forms API(Java) を使用して、カスタム CSS ファイルを使用するHTMLフォームをレンダリングします。

1. Include project files

   Java プロジェクトのクラスパスに、adobe-forms-client.jar などのクライアント JAR ファイルを含めます。

1. Forms Java API オブジェクトの作成

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用して `FormsServiceClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. CSS ファイルの参照

   * の作成 `HTMLRenderSpec` オブジェクトを指定します。
   * カスタム CSS ファイルを使用するHTMLフォームをレンダリングするには、 `HTMLRenderSpec` オブジェクトの `setCustomCSSURI` メソッドを使用して、CSS ファイルの場所と名前を指定する string 値を渡します。

1. Render an HTML form

   を呼び出す `FormsServiceClient` オブジェクトの `(Deprecated) (Deprecated) renderHTMLForm` メソッドを使用して、次の値を渡します。

   * ファイル名拡張子を含むフォームデザイン名を指定する string 値。 Formsアプリケーションの一部であるフォームデザインを参照する場合は、必ず次のような完全なパスを指定してください。 `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * A `TransformTo` HTMLの環境設定タイプを指定する enum 値。 例えば、Internet Explorer 5.0 以降の動的HTMLと互換性のあるHTMLフォームをレンダリングするには、次のように指定します。 `TransformTo.MSDHTML`.
   * A `com.adobe.idp.Document` フォームに結合するデータを含むオブジェクト。 データを結合しない場合は、空の `com.adobe.idp.Document` オブジェクト。
   * この `HTMLRenderSpec` オブジェクトを指定します。HTMLの実行時オプションが格納されます。
   * 次を指定する string 値 `HTTP_USER_AGENT` ヘッダー値（例： ） `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`.
   * A `URLSpec` object that stores URI values required to render an HTML form.
   * A `java.util.HashMap` 添付ファイルを保存するオブジェクト。 This is an optional parameter, and you can specify `null` if you do not want to attach files to the form.

   この `(Deprecated) renderHTMLForm` メソッドは、 `FormsResult` クライアントの Web ブラウザーに書き込む必要があるフォームデータストリームを含むオブジェクト。

1. フォームデータストリームをクライアント Web ブラウザーに書き込む

   * の作成 `com.adobe.idp.Document` を呼び出すことによってオブジェクトを取得 `FormsResult` オブジェクト `getOutputContent` メソッド。
   * のコンテンツタイプを取得する `com.adobe.idp.Document` オブジェクトを呼び出す `getContentType` メソッド。
   * を `javax.servlet.http.HttpServletResponse` を呼び出すことによるオブジェクトのコンテンツタイプ `setContentType` メソッドを使用して、 `com.adobe.idp.Document` オブジェクト。
   * の作成 `javax.servlet.ServletOutputStream` オブジェクトを使用します。オブジェクトは、 `javax.servlet.h\ttp.HttpServletResponse` オブジェクトの `getOutputStream` メソッド。
   * の作成 `java.io.InputStream` を呼び出すことによってオブジェクトを取得 `com.adobe.idp.Document` オブジェクトの `getInputStream` メソッド。
   * バイト配列を作成し、 `InputStream` オブジェクトの `read` メソッドを使用し、バイト配列を引数として渡す。
   * を呼び出す `javax.servlet.ServletOutputStream` オブジェクトの `write` メソッドを使用して、フォームデータストリームをクライアント Web ブラウザーに送信します。 バイト配列を `write` メソッド。

**関連トピック**

[カスタム CSS ファイルを使用したHTMLFormsのレンダリング](#rendering-html-forms-using-custom-css-files)

[クイックスタート（SOAP モード）:Java API を使用した CSS ファイルを使用するHTMLフォームのレンダリング](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-an-html-form-that-uses-a-css-file-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Web サービス API を使用して、CSS ファイルを使用するHTMLフォームをレンダリングする {#render-an-html-form-that-uses-a-css-file-using-the-web-service-api}

Forms API（Web サービス）を使用して、カスタム CSS ファイルを使用するHTMLフォームをレンダリングします。

1. プロジェクトファイルを含める

   * Forms Service WSDL を使用する Java プロキシクラスを作成します。
   * クラスパスに Java プロキシクラスを含めます。

1. Forms Java API オブジェクトの作成

   の作成 `FormsService` オブジェクトを選択し、認証値を設定します。

1. CSS ファイルの参照

   * の作成 `HTMLRenderSpec` オブジェクトを指定します。
   * カスタム CSS ファイルを使用するHTMLフォームをレンダリングするには、 `HTMLRenderSpec` オブジェクトの `setCustomCSSURI` メソッドを使用して、CSS ファイルの場所と名前を指定する string 値を渡します。

1. HTMLフォームをレンダリング

   Invoke the `FormsService` object’s `(Deprecated) renderHTMLForm` method and pass the following values:

   * ファイル名拡張子を含むフォームデザイン名を指定する string 値。 Formsアプリケーションの一部であるフォームデザインを参照する場合は、必ず次のような完全なパスを指定してください。 `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * A `TransformTo` HTMLの環境設定タイプを指定する enum 値。 例えば、Internet Explorer 5.0 以降の動的HTMLと互換性のあるHTMLフォームをレンダリングするには、次のように指定します。 `TransformTo.MSDHTML`.
   * A `BLOB` フォームに結合するデータを含むオブジェクト。 データを結合しない場合は、 `null`. ( [編集可能なレイアウトを使用したFormsの事前入力](/help/forms/developing/prepopulating-forms-flowable-layouts.md).)
   * この `HTMLRenderSpec` オブジェクトを指定します。HTMLの実行時オプションが格納されます。
   * 次を指定する string 値 `HTTP_USER_AGENT` ヘッダー値（例： ） `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`. この値を設定しない場合は、空の文字列を渡すことができます。
   * A `URLSpec` オブジェクトフォームのレンダリングに必要な URI 値をHTMLするオブジェクト。
   * A `java.util.HashMap` 添付ファイルを保存するオブジェクト。 これはオプションのパラメーターで、 `null` フォームにファイルを添付しない場合。
   * 空 `com.adobe.idp.services.holders.BLOBHolder` オブジェクト `(Deprecated) renderHTMLForm` メソッド。 このパラメーター値は、レンダリングされたフォームを保存します。
   * 空 `com.adobe.idp.services.holders.BLOBHolder` オブジェクト `(Deprecated) renderHTMLForm` メソッド。 このパラメーターは、出力 XML データを格納します。
   * 空 `javax.xml.rpc.holders.LongHolder` オブジェクト `(Deprecated) renderHTMLForm` メソッド。 This argument stores the number of pages in the form.
   * 空 `javax.xml.rpc.holders.StringHolder` オブジェクト `(Deprecated) renderHTMLForm` メソッド。 この引数はロケール値を格納します。
   * An empty `javax.xml.rpc.holders.StringHolder` object that is populated by the `(Deprecated) renderHTMLForm` method. この引数は、使用されるHTMLレンダリング値を格納します。
   * 空 `com.adobe.idp.services.holders.FormsResultHolder` この操作の結果を格納するオブジェクト。

   この `(Deprecated) renderHTMLForm` メソッドによって `com.adobe.idp.services.holders.FormsResultHolder` オブジェクト。クライアント Web ブラウザーに書き込む必要があるフォームデータストリームを含む最後の引数値として渡されます。

1. フォームデータストリームをクライアント Web ブラウザーに書き込む

   * の作成 `FormResult` オブジェクトを作成するには、 `com.adobe.idp.services.holders.FormsResultHolder` オブジェクトの `value` データメンバー。
   * の作成 `BLOB` を呼び出してフォームデータを含むオブジェクト `FormsResult` オブジェクトの `getOutputContent` メソッド。
   * のコンテンツタイプを取得する `BLOB` オブジェクトを呼び出す `getContentType` メソッド。
   * Set the `javax.servlet.http.HttpServletResponse` object’s content type by invoking its `setContentType` method and passing the content type of the `BLOB` object.
   * Create a `javax.servlet.ServletOutputStream` object used to write the form data stream to the client web browser by invoking the `javax.servlet.http.HttpServletResponse` object’s `getOutputStream` method.
   * バイト配列を作成し、 `BLOB` オブジェクトの `getBinaryData` メソッド。 このタスクは、 `FormsResult` オブジェクトをバイト配列に変換します。
   * を呼び出す `javax.servlet.http.HttpServletResponse` オブジェクトの `write` メソッドを使用して、フォームデータストリームをクライアント Web ブラウザーに送信します。 バイト配列を `write` メソッド。

**関連トピック**

[カスタム CSS ファイルを使用したHTMLFormsのレンダリング](#rendering-html-forms-using-custom-css-files)

[Invoking AEM Forms using Base64 encoding](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
