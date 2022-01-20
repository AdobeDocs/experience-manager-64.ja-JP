---
title: クライアントでのFormsのレンダリング
seo-title: Rendering Forms at the Client
description: AcrobatまたはAdobe Readerのクライアント側レンダリング機能を使用して、PDFコンテンツの配信を最適化し、Formsサービスのネットワーク読み込み処理機能を改善します。
seo-description: Optimize the delivery of PDF content and improve the Forms service’s ability to handle network load by using the client-side rendering capability of Acrobat or Adobe Reader.
uuid: 09bcc23d-28b0-473a-87f1-bc17e87620f4
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: operations
discoiquuid: 08d36e9f-cafc-478e-9781-8fc29ac6262e
role: Developer
exl-id: 641452e6-bf7e-4af4-a4f9-6e5627db9fca
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '1684'
ht-degree: 2%

---

# クライアントでのFormsのレンダリング {#rendering-forms-at-the-client}

## クライアントでのFormsのレンダリング {#rendering-forms-at-the-client-inner}

AcrobatまたはAdobe Readerのクライアント側レンダリング機能を使用すると、PDFコンテンツの配信を最適化し、Formsサービスがネットワーク読み込みを処理する機能を向上できます。 このプロセスは、クライアントでのフォームのレンダリングと呼ばれます。 クライアントでフォームをレンダリングするには、クライアントデバイス（通常は Web ブラウザー）でAcrobat 7.0 またはAdobe Reader 7.0 以降を使用する必要があります。

サーバーサイドスクリプトの実行によって生成されたフォームへの変更は、ルートサブフォームに `restoreState` 属性 `auto`. この属性について詳しくは、 [Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63)

>[!NOTE]
>
>Formsサービスについて詳しくは、 [AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary-of-steps}

クライアントでフォームをレンダリングするには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. Forms Client API オブジェクトを作成します。
1. クライアントレンダリングの実行時オプションを設定します。
1. クライアントでフォームをレンダリングします。
1. フォームをクライアントの Web ブラウザーに書き込みます。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。 Web サービスを使用している場合は、プロキシファイルを必ず含めてください。

**Forms Client API オブジェクトの作成**

Forms Service Client API 操作をプログラムで実行する前に、Formsサービスクライアントを作成する必要があります。 Java API を使用している場合は、 `FormsServiceClient` オブジェクト。 Forms Web サービス API を使用している場合は、 `FormsService` オブジェクト。

**クライアントレンダリングの実行時オプションを設定する**

クライアントでフォームをレンダリングする場合は、クライアントでフォームをレンダリングするために、クライアントレンダリングの実行時オプションを設定する必要があります。その際には、 `RenderAtClient` 実行時のオプション `true`. その結果、フォームはレンダリング先のクライアントデバイスに配信されます。 If `RenderAtClient` が `auto` （デフォルト値）を指定した場合、フォームデザインは、フォームをクライアントでレンダリングするかどうかを決定します。 フォームデザインは、編集可能なレイアウトを含むフォームデザインにする必要があります。

オプションで設定できるランタイムオプションは、 `SeedPDF` オプション。 この `SeedPDF` 「 」オプションは、PDFコンテナ ( シードPDFドキュメント ) とフォームデザインと XML データを組み合わせたものです。 フォームデザインと XML データの両方がAcrobatまたはAdobe Readerに配信され、フォームがレンダリングされます。 この `SeedPDF` オプションは、クライアントコンピューターにフォーム内で使用されるフォントがない場合に使用できます。例えば、エンドユーザーがフォーム所有者が使用するライセンスを持つフォントを使用するライセンスを持っていない場合などです。

Designer を使用して、シードPDFファイルとして使用するシンプルなダイナミックPDFファイルを作成できます。 このタスクを実行するには、次の手順が必要です。

1. フォントをシードフォントファイル内に埋め込む必要があるかどうかをPDFします。 シードPDFファイルには、レンダリングされるフォームに必要な追加のフォントが含まれている必要があります。 フォントをシードPDFファイルに埋め込む場合は、フォント使用許諾契約に違反しないようにしてください。 Designer では、フォントを法的に埋め込むことができるかどうかを指定できます。 保存すると、フォームに埋め込むことができないフォントがある場合、Designer は埋め込むことができないフォントの一覧を示すメッセージを表示します。 このメッセージは、静的メッセージドキュメントの場合は Designer にPDFされません。
1. Designer でシードPDFファイルを作成する場合は、少なくともメッセージを含むテキストフィールドを追加することをお勧めします。 このメッセージは、Adobe Readerの以前のバージョンのユーザーに対し、ドキュメントの表示にAcrobat 7.0 以降またはAdobe Reader 7.0 以降が必要であると述べている必要があります。
1. シードPDFファイルを動的PDFファイルとして保存し、PDFファイル名の拡張子を付けます。

>[!NOTE]
>
>クライアント上でフォームをレンダリングする場合、シードPDFの実行時オプションを定義する必要はありません。 シードPDFを指定しない場合、Formsサービスはシェル pdf を作成します。この pdf は、COS オブジェクトは含まれず、実際の XDP コンテンツが埋め込まれたPDFラッパーを含みます。 この節の手順では、シードPDFの実行時オプションは設定しません。 COS オブジェクトの詳細については、『 Adobe PDF Reference 』ガイドを参照してください。

**クライアントでフォームをレンダリング**

クライアントでフォームをレンダリングするには、フォームをレンダリングするクライアントレンダリングの実行時オプションがアプリケーションロジックに含まれていることを確認する必要があります。

**フォームデータストリームをクライアント Web ブラウザーに書き込む**

Formsサービスはフォームデータストリームを作成します。このデータストリームは、クライアントの Web ブラウザーに書き込む必要があります。 クライアント Web ブラウザーに書き込まれると、フォームはAcrobat 7.0 またはAdobe Reader 7.0 以降でレンダリングされ、ユーザーに対して表示されます。

**関連トピック**

[Java API を使用してクライアントでフォームをレンダリングする](#render-a-form-at-the-client-using-the-java-api)

[Web サービス API を使用してクライアントでフォームをレンダリングする](#render-a-form-at-the-client-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Forms Service API クイックスタート](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Forms Service にドキュメントを渡す](/help/forms/developing/passing-documents-forms-service.md)

[Formsをレンダリングする Web アプリケーションの作成](/help/forms/developing/creating-web-applications-renders-forms.md)

### Java API を使用してクライアントでフォームをレンダリングする {#render-a-form-at-the-client-using-the-java-api}

Forms API(Java) を使用して、クライアントでフォームをレンダリングします。

1. プロジェクトファイルを含める

   Java プロジェクトのクラスパスに、adobe-forms-client.jar などのクライアント JAR ファイルを含めます。

1. Forms Client API オブジェクトの作成

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * の作成 `FormsServiceClient` オブジェクトのコンストラクタを使用し、 `ServiceClientFactory` オブジェクト。

1. クライアントレンダリングの実行時オプションを設定する

   * コンストラクタを使用して `PDFFormRenderSpec` オブジェクトを作成します。
   * を `RenderAtClient` を呼び出すことによる実行時オプション `PDFFormRenderSpec` オブジェクトの `setRenderAtClient` メソッドを使用して enum 値を渡す `RenderAtClient.Yes`.

1. クライアントでフォームをレンダリング

   を呼び出す `FormsServiceClient` オブジェクトの `renderPDFForm` メソッドを使用して、次の値を渡します。

   * ファイル名拡張子を含むフォームデザイン名を指定する string 値。 AEM Formsアプリケーションの一部であるフォームデザインを参照する場合は、必ず次のような完全なパスを指定してください。 `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * A `com.adobe.idp.Document` フォームに結合するデータを含むオブジェクト。 データを結合しない場合は、空の `com.adobe.idp.Document` オブジェクト。
   * A `PDFFormRenderSpec` クライアントでフォームをレンダリングするために必要な実行時のオプションを格納するオブジェクト。
   * A `URLSpec` フォームをレンダリングするためにFormsサービスで必要な URI 値を含むオブジェクト。
   * A `java.util.HashMap` 添付ファイルを保存するオブジェクト。 これはオプションのパラメーターで、 `null` フォームにファイルを添付しない場合。

   この `renderPDFForm` メソッドは、 `FormsResult` クライアントの Web ブラウザーに書き込む必要があるフォームデータストリームを含むオブジェクト。

1. フォームデータストリームをクライアント Web ブラウザーに書き込む

   * の作成 `com.adobe.idp.Document` を呼び出すことによってオブジェクトを取得 `FormsResult` オブジェクト `getOutputContent` メソッド。
   * のコンテンツタイプを取得する `com.adobe.idp.Document` オブジェクトを呼び出す `getContentType` メソッド。
   * を `javax.servlet.http.HttpServletResponse` を呼び出すことによるオブジェクトのコンテンツタイプ `setContentType` メソッドを使用して、 `com.adobe.idp.Document` オブジェクト。
   * の作成 `javax.servlet.ServletOutputStream` オブジェクトを使用します。オブジェクトは、 `javax.servlet.http.HttpServletResponse` オブジェクトの `getOutputStream` メソッド。
   * の作成 `java.io.InputStream` を呼び出すことによってオブジェクトを取得 `com.adobe.idp.Document` オブジェクトの `getInputStream` メソッド。
   * バイト配列を作成し、 `InputStream` オブジェクトの `read` メソッドを使用し、バイト配列を引数として渡す。
   * を呼び出す `javax.servlet.ServletOutputStream` オブジェクトの `write` メソッドを使用して、フォームデータストリームをクライアント Web ブラウザーに送信します。 バイト配列を `write` メソッド。

**関連トピック**

[クイックスタート（SOAP モード）:Java API を使用してクライアントでフォームをレンダリングする](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-a-form-at-the-client-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Web サービス API を使用してクライアントでフォームをレンダリングする {#render-a-form-at-the-client-using-the-web-service-api}

Forms API（Web サービス）を使用して、クライアントでフォームをレンダリングします。

1. プロジェクトファイルを含める

   * Forms Service WSDL を使用する Java プロキシクラスを作成します。
   * Java プロキシクラスをクラスパスに含めます。

1. Forms Client API オブジェクトの作成

   の作成 `FormsService` オブジェクトを選択し、認証値を設定します。

1. クライアントレンダリングの実行時オプションを設定する

   * コンストラクタを使用して `PDFFormRenderSpec` オブジェクトを作成します。
   * を `RenderAtClient` を呼び出すことによる実行時オプション `PDFFormRenderSpec` オブジェクトの `setRenderAtClient` メソッドと文字列値を渡す `RenderAtClient.Yes`.

1. クライアントでフォームをレンダリング

   を呼び出す `FormsService` オブジェクトの `renderPDFForm` メソッドを使用して、次の値を渡します。

   * ファイル名拡張子を含むフォームデザイン名を指定する string 値。 Formsアプリケーションの一部であるフォームデザインを参照する場合は、必ず次のような完全なパスを指定してください。 `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * A `BLOB` フォームに結合するデータを含むオブジェクト。 データを結合しない場合は、 `null`. ( [編集可能なレイアウトを使用したFormsの事前入力](/help/forms/developing/prepopulating-forms-flowable-layouts.md).)
   * A `PDFFormRenderSpec` クライアントでフォームをレンダリングするために必要な実行時のオプションを格納するオブジェクト。
   * A `URLSpec` Formsサービスで必要な URI 値を格納するオブジェクト。
   * A `java.util.HashMap` 添付ファイルを保存するオブジェクト。 これはオプションのパラメーターで、 `null` フォームにファイルを添付しない場合。
   * 空 `com.adobe.idp.services.holders.BLOBHolder` メソッドによって設定されるオブジェクト。 このパラメーターは、レンダリングされたPDFフォームを保存するために使用されます。
   * 空 `javax.xml.rpc.holders.LongHolder` メソッドによって設定されるオブジェクト。 （この引数は、フォームのページ数を保存します）。
   * 空 `javax.xml.rpc.holders.StringHolder` メソッドによって設定されるオブジェクト。 （この引数はロケール値を格納します）。
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

[クライアントでのFormsのレンダリング](#rendering-forms-at-the-client)

[Base64 エンコーディングを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
