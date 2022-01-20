---
title: ファイル形式とPDFの変換
seo-title: Converting Between File Formatsand PDF
description: GeneratePDFサービスを使用して、ネイティブファイル形式をPDFに変換します。 また、GeneratePDFサービスは、PDFを他のファイル形式に変換し、PDFドキュメントのサイズを最適化します。
seo-description: Use the Generate PDF service to convert native file formats to PDF. Generate PDF service also converts PDF to other file formats and optimizes the size of PDF documents.
uuid: f72ad603-c996-4d48-9bfc-bed7bf776af6
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: operations
discoiquuid: 180cac3f-6378-42bc-9a47-60f9f08a7103
role: Developer
exl-id: 79091a75-2669-453f-9560-e58bfffa3487
source-git-commit: e608249c3f95f44fdc14b100910fa11ffff5ee32
workflow-type: tm+mt
source-wordcount: '7872'
ht-degree: 4%

---

# ファイル形式とPDFの変換 {#converting-between-file-formatsand-pdf}

**GeneratePDFサービス**

Generate PDF サービスは、ネイティブファイル形式を PDF に変換します。また、PDF を他のファイル形式に変換し、PDF ドキュメントのサイズを最適化します。

Generate PDF サービスは、以下のファイル形式を PDF に変換する際にネイティブアプリケーションを使用します。特に説明がない限り、これらのアプリケーションはドイツ語版、フランス語版、英語版および日本語版のみサポートされています。*Windows のみ* は、Windows Server® 2003 および Windows Server 2008 のみをサポートしています。

* Microsoft Office 2003 および 2007:DOC、DOCX、RTF、TXT、XLS、XLSX、PPT、PPTX、VSD、MPP、MPX、XPS、PUB の変換（Windows のみ）

   >[!NOTE]
   >
   >Acrobat® 9.2 以降は、Microsoft XPS 形式をPDFに変換する場合に必要です。

* DWF、DWG、DXW を変換する Autodesk AutoCAD 2005、2006、2007、2008、2009 （英語のみ）
* WPD、QPW、SHW を変換する Corel WordPerfect 12 および X4（英語のみ）
* ODT、ODS、ODP、ODF、ODF、SXW、SXI、SXC、SXD、DOC、DOCX、RTF、TXT、TXT、XLSX、XLS、PPT、OPT、OPTPPTX、VSD、MPP、MPPX および PUB

   >[!NOTE]
   >
   >GeneratePDFサービスは、64 ビットバージョンの OpenOffice をサポートしていません。

* Adobe Photoshop® CS2 によるPSDの変換（Windows のみ）

   >[!NOTE]
   >
   >Photoshop CS3 および CS4 は、Windows Server 2003 または Windows Server 2008 をサポートしていないので、サポートされていません。

* Adobe FrameMaker® 7.2 および 8:FM の変換（Windows のみ）
* PMD、PM6、P65、PM の変換：Adobe PageMaker® 7.0（Windows のみ）
* サードパーティのアプリケーションによってサポートされているネイティブ形式（アプリケーションに固有のセットアップファイルの開発が必要）（Windows のみ）

Generate PDF サービスでは、次の標準ベースのファイル形式を PDF に変換します。

* ビデオファイル形式：SWF、FLV（Windows のみ）
* 画像ファイル形式：JPEG、JPG、JP2、J2Kí、JPC、J2C、GIF、BMP、TIFF、TIF、PNG、JPF
* HTML (Windows、Sun™ Solaris™および Linux®)

Generate PDF サービスでは、PDF を次のファイル形式に変換します（Windows のみ）：

* EPS（Encapsulated PostScript）
* HTML3.2
* CSS 1.0 を使用した HTML 4.01
* DOC（Microsoft Word format）
* RTF
* テキスト（アクセス可能およびプレーンの両方）
* XML
* PDF/A-1a （DeviceRGB カラースペースのみを使用）
* PDF/A-1b （DeviceRGB カラースペースのみを使用）

Generate PDF サービスを使用するには、以下の管理タスクを実行する必要があります。

* 必要なネイティブアプリケーションを、AEM Forms をホストするコンピューター上にインストールする
* AEM FormsをホストするコンピューターにAdobe Acrobat Professional またはAcrobat Pro Extended 9.2 をインストールする
* インストール後のセットアップタスクを実行する

これらのタスクについては、「 AEM forms の自動インストールおよびデプロイ（JBoss 版）」で説明しています。

Generate タスクサービスを使用して、次のタスクをPDFできます。

* ネイティブファイル形式からPDFに変換。
* HTMLドキュメントをPDFドキュメントに変換します。
* PDFドキュメントをファイル形式に変換します。

>[!NOTE]
>
>Generate Generate サービスについて詳しくは、「PDF」を参照してください。 [AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63).

## Word 文書の変換，PDF文書 {#converting-word-documents-to-pdf-documents}

この節では、PDF生成 API を使用して、Microsoft Word 文書をプログラムでPDF文書に変換する方法について説明します。

>[!NOTE]
>
>その他のファイル形式について詳しくは、 [追加のネイティブファイル形式のサポートの追加](converting-file-formats-pdf.md#adding-support-for-additional-native-file-formats).

>[!NOTE]
>
>Generate Generate サービスについて詳しくは、「PDF」を参照してください。 [AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary-of-steps}

Microsoft Word 文書をPDF文書に変換するには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. 生成PDFクライアントを作成。
1. 変換ドキュメントに変換するファイルをPDFします。
1. ファイルをPDF文書に変換
1. 結果を取得します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。 Web サービスを使用している場合は、プロキシファイルを必ず含めてください。

**GeneratePDFクライアントの作成**

プログラムによって「PDFを生成」操作を実行する前に、GeneratePDFサービスクライアントを作成します。 Java API を使用している場合は、 `GeneratePdfServiceClient` オブジェクト。 Web サービス API を使用している場合、 `GeneratePDFServiceService` オブジェクト。

**変換ドキュメントに変換するファイルをPDFします**

PDFドキュメントに変換するMicrosoft Word ドキュメントを取得します。

**ファイルをPDF文書に変換**

GeneratePDFサービスクライアントを作成した後、 `createPDF2` メソッド。 このメソッドでは、変換するドキュメントに関する情報（ファイル拡張子を含む）が必要です。

**結果の取得**

ファイルをPDF文書に変換した後、結果を取得できます。 例えば、Word ファイルをPDF文書に変換した後に、そのPDF文書を取得して保存できます。

**関連トピック**

[Java API を使用して Word 文書をPDF文書に変換する](converting-file-formats-pdf.md#convert-word-documents-to-pdf-documents-using-the-java-api)

[Web サービス API を使用して Word ドキュメントをPDFドキュメントに変換する](converting-file-formats-pdf.md#convert-word-documents-to-pdf-documents-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[PDFサービス API のクイックスタートの生成](/help/forms/developing/generate-pdf-service-java-api.md#generate-pdf-service-java-api-quick-start-soap)

### Java API を使用して Word 文書をPDF文書に変換する {#convert-word-documents-to-pdf-documents-using-the-java-api}

生成PDFAPI(Java) を使用して、Microsoft Word 文書をPDF文書に変換します。

1. プロジェクトファイルを含めます。

   Java プロジェクトのクラスパスに、adobe-generatepdf-client.jar などのクライアント JAR ファイルを含めます。

1. 生成PDFクライアントを作成。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用して `GeneratePdfServiceClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. 変換ドキュメントに変換するファイルをPDFします。

   * の作成 `java.io.FileInputStream` コンストラクタを使用して変換する Word ファイルを表すオブジェクト。 ファイルの場所を指定する string 値を渡します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. ファイルをPDF文書に変換

   を呼び出して、ファイルをPDFドキュメントに変換します。 `GeneratePdfServiceClient` オブジェクトの `createPDF2` メソッドを使用して、次の値を渡します。

   * A `com.adobe.idp.Document` 変換するファイルを表すオブジェクト。
   * A `java.lang.String` オブジェクトの拡張子にファイル拡張子を含める。
   * A `java.lang.String` 変換処理で使用されるファイルタイプ設定を含むオブジェクト。 ファイルタイプ設定は、.docや.xls など、様々なファイルタイプの変換設定を提供します。
   * A `java.lang.String` 使用するPDF設定の名前を格納するオブジェクト。 例えば、次の項目を指定できます。 `Standard`.
   * A `java.lang.String` 使用するセキュリティ設定の名前を含むオブジェクト。
   * オプション `com.adobe.idp.Document` オブジェクトドキュメントの生成時に適用されるPDFを含むオブジェクト。
   * オプション `com.adobe.idp.Document` オブジェクトドキュメントに適用するメタデータ情報を含むPDF。

   この `createPDF2` メソッドは、 `CreatePDFResult` 新しいPDF・ドキュメントとログ情報を含むオブジェクト。 通常、ログファイルには、変換リクエストによって生成されるエラーまたは警告メッセージが含まれます。

1. 結果を取得します。

   PDF・ドキュメントを取得するには、次の操作を実行します。

   * を呼び出す `CreatePDFResult` オブジェクトの `getCreatedDocument` メソッド。 `com.adobe.idp.Document` オブジェクト。
   * を呼び出す `com.adobe.idp.Document` オブジェクトの `copyToFile` メソッドを使用して、前の手順で作成したPDFからオブジェクトドキュメントを抽出します。

   次の `createPDF2` メソッドを使用して、ログドキュメントを取得し (HTMLの変換には適用されません )、次の操作を実行します。

   * を呼び出す `CreatePDFResult` オブジェクトの `getLogDocument` メソッド。 これにより、 `com.adobe.idp.Document` オブジェクト。
   * を呼び出す `com.adobe.idp.Document` オブジェクトの `copyToFile` メソッドを使用してログドキュメントを抽出します。


**関連トピック**

[手順の概要](converting-file-formats-pdf.md#summary-of-steps)

[クイックスタート（SOAP モード）:Java API を使用したMicrosoft Word ドキュメントのPDFドキュメントへの変換](/help/forms/developing/generate-pdf-service-java-api.md#quick-start-soap-mode-converting-a-microsoft-word-document-to-a-pdf-document-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Web サービス API を使用して Word ドキュメントをPDFドキュメントに変換する {#convert-word-documents-to-pdf-documents-using-the-web-service-api}

GeneratePDFAPI（Web サービス）を使用して、Microsoft Word ドキュメントをPDFドキュメントに変換します。

1. プロジェクトファイルを含めます。

   MTOM を使用するMicrosoft .NET プロジェクトを作成します。 次の WSDL 定義を使用していることを確認します。 `http://localhost:8080/soap/services/GeneratePDFService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >置換 `localhost` を、AEM Formsをホストするサーバーの IP アドレスに設定します。

1. 生成PDFクライアントを作成。

   * の作成 `GeneratePDFServiceClient` オブジェクトのデフォルトのコンストラクタを使用します。
   * の作成 `GeneratePDFServiceClient.Endpoint.Address` オブジェクトを `System.ServiceModel.EndpointAddress` コンストラクタ。 WSDL をAEM Formsサービスに渡す文字列値 ( 例： `http://localhost:8080/soap/services/GeneratePDFService?blob=mtom`.) を使用する必要はありません。 `lc_version` 属性。 ただし、 `?blob=mtom`.
   * の作成 `System.ServiceModel.BasicHttpBinding` オブジェクトを作成するには、 `GeneratePDFServiceClient.Endpoint.Binding` フィールドに入力します。 戻り値を `BasicHttpBinding` にキャストします。
   * を `System.ServiceModel.BasicHttpBinding` オブジェクトの `MessageEncoding` ～に向かって `WSMessageEncoding.Mtom`. この値は、MTOM が確実に使用されるようにします。
   * 次のタスクを実行して、基本的な HTTP 認証を有効にします。

      * フィールドにAEM forms ユーザー名を割り当てます。 `GeneratePDFServiceClient.ClientCredentials.UserName.UserName`.
      * 対応するパスワード値をフィールドに割り当てます。 `GeneratePDFServiceClient.ClientCredentials.UserName.Password`.
      * 定数値を割り当て `HttpClientCredentialType.Basic` フィールドに `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 定数値を割り当て `BasicHttpSecurityMode.TransportCredentialOnly` フィールドに `BasicHttpBindingSecurity.Security.Mode`.

1. 変換ドキュメントに変換するファイルをPDFします。

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。この `BLOB` オブジェクトは、PDFドキュメントに変換するファイルを保存するために使用されます。
   * の作成 `System.IO.FileStream` オブジェクトを指定します。 変換するファイルの場所と、ファイルを開くモードを表す string 値を渡します。
   * コンテンツを格納するバイト配列を作成します。 `System.IO.FileStream` オブジェクト。 バイト配列のサイズは、 `System.IO.FileStream` オブジェクトの `Length` プロパティ。
   * を呼び出して、バイト配列にストリームデータを入力します。 `System.IO.FileStream` オブジェクトの `Read` メソッドを使用し、読み込むバイト配列、開始位置、ストリーム長を渡す。
   * 次の項目に `BLOB` オブジェクトに割り当てることによって `MTOM` プロパティは、バイト配列の内容を示します。

1. ファイルをPDF文書に変換

   を呼び出して、ファイルをPDFドキュメントに変換します。 `GeneratePDFServiceService` オブジェクトの `CreatePDF2` メソッドを使用して、次の値を渡します。

   * A `BLOB` 変換するファイルを表すオブジェクト。
   * ファイル拡張子を含む文字列。
   * A `java.lang.String` 変換処理で使用されるファイルタイプ設定を含むオブジェクト。 ファイルタイプ設定は、.docや.xls など、様々なファイルタイプの変換設定を提供します。
   * 使用する文字列設定を含むPDF列オブジェクト。 次を指定できます。 `Standard`.
   * 使用するセキュリティ設定を含む string オブジェクト。 次を指定できます。 `No Security`.
   * オプション `BLOB` オブジェクトドキュメントの生成時に適用されるPDFを含むオブジェクト。
   * オプション `BLOB` オブジェクトドキュメントに適用するメタデータ情報を含むPDF。
   * 型の出力パラメーター `BLOB` が `CreatePDF2` メソッド。 この `CreatePDF2` メソッドは、このオブジェクトに変換後のドキュメントを入力します。 （このパラメーター値は、Web サービスの呼び出しにのみ必要です）。
   * 型の出力パラメーター `BLOB` が `CreatePDF2` メソッド。 この `CreatePDF2` メソッドは、このオブジェクトにログドキュメントを入力します。 （このパラメーター値は、Web サービスの呼び出しにのみ必要です）。

1. 結果を取得します。

   * 変換後のPDFドキュメントを取得するには、 `BLOB` オブジェクトの `MTOM` フィールドをバイト配列に変換します。 byte 配列は変換後のPDF文書を表します。 必ず `BLOB` オブジェクトの `createPDF2` メソッド。
   * の作成 `System.IO.FileStream` オブジェクトを指定します。
   * の作成 `System.IO.BinaryWriter` オブジェクトのコンストラクタを呼び出し、 `System.IO.FileStream` オブジェクト。
   * を呼び出して、バイト配列の内容をPDFファイルに書き込みます。 `System.IO.BinaryWriter` オブジェクトの `Write` メソッドを使用してバイト配列を渡す。

**関連トピック**

[手順の概要](converting-file-formats-pdf.md#summary-of-steps)

[MTOM を使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRef を使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## HTML文書をPDF文書に変換 {#converting-html-documents-to-pdf-documents}

この節では、GeneratePDFAPI を使用して、プログラムでドキュメントをHTMLドキュメントに変換する方法について説明します。

>[!NOTE]
>
>Generate Generate サービスについて詳しくは、「PDF」を参照してください。 [AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary_of_steps-1}

HTML・ドキュメントをPDF・ドキュメントに変換するには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. 生成PDFクライアントを作成。
1. HTMLドキュメントに変換するPDFコンテンツを取得します。
1. HTMLの内容をPDF文書に変換する
1. 結果を取得します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。 Web サービスを使用している場合は、プロキシファイルを必ず含めてください。

**GeneratePDFクライアントの作成**

プログラムによって「PDFを生成」操作を実行する前に、GeneratePDFサービスクライアントを作成する必要があります。 Java API を使用している場合は、 `GeneratePdfServiceClient` オブジェクト。 Web サービス API を使用している場合、 `GeneratePDFServiceService`.

**HTMLドキュメントに変換するPDFコンテンツを取得**

HTMLドキュメントに変換するPDFコンテンツを参照します。 HTMLコンテンツ (HTMLファイルや、URL を使用してアクセス可能なHTMLコンテンツなど ) を参照できます。

**HTMLコンテンツをPDF文書に変換**

サービスクライアントを作成した後、適切なPDF作成操作を呼び出すことができます。 この操作では、変換対象のドキュメントのパスを含む、変換するドキュメントに関する情報が必要です。

**結果の取得**

HTMLコンテンツをPDFドキュメントに変換した後、結果を取得してPDFドキュメントを保存できます。

**関連トピック**

[Java API を使用してHTMLコンテンツをPDFドキュメントに変換する](converting-file-formats-pdf.md#convert-html-content-to-a-pdf-document-using-the-java-api)

[Web サービス API を使用して、HTMLコンテンツをPDFドキュメントに変換する](converting-file-formats-pdf.md#convert-html-content-to-a-pdf-document-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[PDFサービス API のクイックスタートの生成](/help/forms/developing/generate-pdf-service-java-api.md#generate-pdf-service-java-api-quick-start-soap)

### Java API を使用してHTMLコンテンツをPDFドキュメントに変換する {#convert-html-content-to-a-pdf-document-using-the-java-api}

GeneratePDFAPI(Java) を使用して、HTMLドキュメントをPDFドキュメントに変換します。

1. プロジェクトファイルを含めます。

   Java プロジェクトのクラスパスに、adobe-generatepdf-client.jar などのクライアント JAR ファイルを含めます。

1. 生成PDFクライアントを作成。

   の作成 `GeneratePdfServiceClient` オブジェクトのコンストラクタを使用し、 `ServiceClientFactory` 接続プロパティを含むオブジェクト。

1. HTMLドキュメントに変換するPDFコンテンツを取得します。

   文字列変数を作成し、HTMLコンテンツを指す URL を割り当てて、HTMLコンテンツを取得します。

1. HTMLの内容をPDF文書に変換する

   を呼び出す `GeneratePdfServiceClient` オブジェクトの `htmlToPDF2` メソッドを使用して、次の値を渡します。

   * A `java.lang.String` 変換するHTMLファイルの URL を含むオブジェクト。
   * A `java.lang.String` 変換処理で使用されるファイルタイプ設定を含むオブジェクト。 ファイルタイプの設定には、スパイダリングレベルを含めることができます。
   * A `java.lang.String` 使用するセキュリティ設定の名前を含むオブジェクト。
   * オプション `com.adobe.idp.Document` オブジェクトドキュメントの生成時に適用されるPDFを含むオブジェクト。 この情報が指定されていない場合、設定は前の 3 つのパラメータに基づいて自動的に選択されます。
   * オプション `com.adobe.idp.Document` オブジェクトドキュメントに適用するメタデータ情報を含むPDF。

1. 結果を取得します。

   この `htmlToPDF2` メソッドは、 `HtmlToPdfResult` 生成された新しいPDFドキュメントを含むオブジェクト。 新しく作成したPDF・ドキュメントを取得するには、次の操作を実行します。

   * を呼び出す `HtmlToPdfResult` オブジェクトの `getCreatedDocument` メソッド。 これにより、 `com.adobe.idp.Document` オブジェクト。
   * を呼び出す `com.adobe.idp.Document` オブジェクトの `copyToFile` メソッドを使用して、前の手順で作成したPDFからオブジェクトドキュメントを抽出します。

**関連トピック**

[HTML文書をPDF文書に変換](converting-file-formats-pdf.md#converting-html-documents-to-pdf-documents)

[クイックスタート（SOAP モード）:Java API を使用したHTMLコンテンツのPDFドキュメントへの変換](/help/forms/developing/generate-pdf-service-java-api.md#quick-start-soap-mode-converting-html-content-to-a-pdf-document-using-the-java-api)

[クイックスタート（SOAP モード）:Java API を使用したHTMLコンテンツのPDFドキュメントへの変換](/help/forms/developing/generate-pdf-service-java-api.md#quick-start-soap-mode-converting-html-content-to-a-pdf-document-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Web サービス API を使用して、HTMLコンテンツをPDFドキュメントに変換する {#convert-html-content-to-a-pdf-document-using-the-web-service-api}

GeneratePDFAPI（Web サービス）を使用して、HTMLのコンテンツをPDFドキュメントに変換します。

1. プロジェクトファイルを含めます。

   MTOM を使用するMicrosoft .NET プロジェクトを作成します。 次の WSDL 定義を使用していることを確認します。 `http://localhost:8080/soap/services/GeneratePDFService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >置換 `localhost` を、AEM Formsをホストするサーバーの IP アドレスに設定します。

1. 生成PDFクライアントを作成。

   * の作成 `GeneratePDFServiceClient` オブジェクトのデフォルトのコンストラクタを使用します。
   * の作成 `GeneratePDFServiceClient.Endpoint.Address` オブジェクトを `System.ServiceModel.EndpointAddress` コンストラクタ。 WSDL をAEM Formsサービスに渡す文字列値 ( 例： `http://localhost:8080/soap/services/GeneratePDFService?blob=mtom`.) を使用する必要はありません。 `lc_version` 属性。 ただし、 `?blob=mtom`.
   * の作成 `System.ServiceModel.BasicHttpBinding` オブジェクトを作成するには、 `GeneratePDFServiceClient.Endpoint.Binding` フィールドに入力します。 戻り値を `BasicHttpBinding` にキャストします。
   * を `System.ServiceModel.BasicHttpBinding` オブジェクトの `MessageEncoding` ～に向かって `WSMessageEncoding.Mtom`. この値は、MTOM が確実に使用されるようにします。
   * 次のタスクを実行して、基本的な HTTP 認証を有効にします。

      * フィールドにAEM forms ユーザー名を割り当てます。 `GeneratePDFServiceClient.ClientCredentials.UserName.UserName`.
      * 対応するパスワード値をフィールドに割り当てます。 `GeneratePDFServiceClient.ClientCredentials.UserName.Password`.
      * 定数値を割り当て `HttpClientCredentialType.Basic` フィールドに `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 定数値を割り当て `BasicHttpSecurityMode.TransportCredentialOnly` フィールドに `BasicHttpBindingSecurity.Security.Mode`.

1. HTMLドキュメントに変換するPDFコンテンツを取得します。

   文字列変数を作成し、HTMLコンテンツを指す URL を割り当てて、HTMLコンテンツを取得します。

1. HTMLの内容をPDF文書に変換する

   を呼び出して、HTMLコンテンツをPDFドキュメントに変換します。 `GeneratePDFServiceService` オブジェクトの `HtmlToPDF2` メソッドを使用して、次の値を渡します。

   * 変換するHTMLコンテンツを含む文字列。
   * A `java.lang.String` 変換処理で使用されるファイルタイプ設定を含むオブジェクト。
   * 使用するセキュリティ設定を含む string オブジェクト。
   * オプション `BLOB` オブジェクトドキュメントの生成時に適用されるPDFを含むオブジェクト。
   * オプション `BLOB` オブジェクトドキュメントに適用するメタデータ情報を含むPDF。
   * 型の出力パラメーター `BLOB` が `CreatePDF2` メソッド。 この `CreatePDF2` メソッドは、このオブジェクトに変換後のドキュメントを入力します。 （このパラメーター値は、Web サービスの呼び出しにのみ必要です）。

1. 結果を取得します。

   * 変換後のPDFドキュメントを取得するには、 `BLOB` オブジェクトの `MTOM` フィールドをバイト配列に変換します。 byte 配列は変換後のPDF文書を表します。 必ず `BLOB` オブジェクトの `HtmlToPDF2` メソッド。
   * の作成 `System.IO.FileStream` オブジェクトを指定します。
   * の作成 `System.IO.BinaryWriter` オブジェクトのコンストラクタを呼び出し、 `System.IO.FileStream` オブジェクト。
   * を呼び出して、バイト配列の内容をPDFファイルに書き込みます。 `System.IO.BinaryWriter` オブジェクトの `Write` メソッドを使用してバイト配列を渡す。

**関連トピック**

[HTML文書をPDF文書に変換](converting-file-formats-pdf.md#converting-html-documents-to-pdf-documents)

[MTOM を使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRef を使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## PDFドキュメントを非画像形式に変換中 {#converting-pdf-documents-to-non-image-formats}

この節では、GeneratePDFJava API と Web サービス API を使用して、PDFドキュメントをプログラムで RTF ファイルに変換する方法について説明します。RTF ファイルは、画像以外の形式の一例です。 その他の画像以外の形式には、HTML、テキスト、DOC、EPSなどがあります。 PDFドキュメントを RTF に変換する場合は、送信ボタンなどのフォーム要素がPDFドキュメントに含まれていないことを確認します。 フォーム要素は変換されません。

>[!NOTE]
>
>Generate Generate サービスについて詳しくは、「PDF」を参照してください。 [AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary_of_steps-2}

PDFドキュメントをサポートされている任意のタイプに変換するには、次の手順に従います。

1. プロジェクトファイルを含めます。
1. 生成PDFクライアントを作成。
1. 変換するPDFドキュメントを取得します。
1. PDF文書を変換
1. 変換したファイルを保存します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。 Web サービスを使用している場合は、プロキシファイルを必ず含めてください。

**GeneratePDFクライアントの作成**

プログラムによって「PDFを生成」操作を実行する前に、GeneratePDFサービスクライアントを作成する必要があります。 Java API を使用している場合は、 `GeneratePdfServiceClient` オブジェクト。 Web サービス API を使用している場合、 `GeneratePDFServiceService` オブジェクト。

**変換するPDFドキュメントを取得**

画像以外のPDF形式に変換する画像ドキュメントを取得します。

**変換ドキュメントのPDF**

サービスクライアントを作成した後で、「PDFのエクスポート」操作を呼び出すことができます。 この操作では、変換対象のドキュメントのパスを含む、変換するドキュメントに関する情報が必要です。

**変換したファイルを保存します。**

変換したファイルを保存します。 例えば、変換ドキュメントを RTF ファイルにPDFする場合、変換後のドキュメントを RTF ファイルに保存します。

**関連トピック**

[Java API を使用してPDFドキュメントを RTF ファイルに変換する](converting-file-formats-pdf.md#convert-a-pdf-document-to-a-rtf-file-using-the-java-api)

[Web サービス API を使用してPDFドキュメントを RTF ファイルに変換する](converting-file-formats-pdf.md#convert-a-pdf-document-to-a-rtf-file-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[PDFサービス API のクイックスタートの生成](/help/forms/developing/generate-pdf-service-java-api.md#generate-pdf-service-java-api-quick-start-soap)

### Java API を使用してPDFドキュメントを RTF ファイルに変換する {#convert-a-pdf-document-to-a-rtf-file-using-the-java-api}

GeneratePDFAPI(Java) を使用して、PDFドキュメントを RTF ファイルに変換します。

1. プロジェクトファイルを含めます。

   Java プロジェクトのクラスパスに、adobe-generatepdf-client.jar などのクライアント JAR ファイルを含めます。

1. 生成PDFクライアントを作成。

   の作成 `GeneratePdfServiceClient` オブジェクトのコンストラクタを使用し、 `ServiceClientFactory` 接続プロパティを含むオブジェクト。

1. 変換するPDFドキュメントを取得します。

   * の作成 `java.io.FileInputStream` コンストラクタを使用して変換するPDFドキュメントを表すオブジェクト。 PDFドキュメントの場所を指定する string 値を渡します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. PDF文書を変換

   を呼び出す `GeneratePdfServiceClient` オブジェクトの `exportPDF2` メソッドを使用して、次の値を渡します。

   * A `com.adobe.idp.Document` 変換するPDFファイルを表すオブジェクト。
   * A `java.lang.String` 変換するファイルの名前を格納するオブジェクト。
   * A `java.lang.String` Adobe PDF設定の名前を格納するオブジェクト。
   * A `ConvertPDFFormatType` 変換対象のファイルの種類を指定するオブジェクト。
   * オプション `com.adobe.idp.Document` オブジェクトドキュメントの生成時に適用されるPDFを含むオブジェクト。

   この `exportPDF2` メソッドは、 `ExportPDFResult` オブジェクトの一部を指定します。

1. PDF文書を変換

   新しく作成されたファイルを取得するには、次の操作を実行します。

   * を呼び出す `ExportPDFResult` オブジェクトの `getConvertedDocument` メソッド。 これにより、 `com.adobe.idp.Document` オブジェクト。
   * を呼び出す `com.adobe.idp.Document` オブジェクトの `copyToFile` メソッドを使用して新しいドキュメントを抽出します。

**関連トピック**

[手順の概要](converting-file-formats-pdf.md#summary-of-steps)

[クイックスタート（SOAP モード）:Java API を使用したHTMLコンテンツのPDFドキュメントへの変換](/help/forms/developing/generate-pdf-service-java-api.md#quick-start-soap-mode-converting-html-content-to-a-pdf-document-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Web サービス API を使用してPDFドキュメントを RTF ファイルに変換する {#convert-a-pdf-document-to-a-rtf-file-using-the-web-service-api}

GeneratePDFAPI（Web サービス）を使用して、PDFドキュメントを RTF ファイルに変換します。

1. プロジェクトファイルを含めます。

   MTOM を使用するMicrosoft .NET プロジェクトを作成します。 次の WSDL 定義を使用していることを確認します。 `http://localhost:8080/soap/services/GeneratePDFService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >置換 `localhost` を、AEM Formsをホストするサーバーの IP アドレスに設定します。

1. Generate PDf クライアントを作成します。

   * の作成 `GeneratePDFServiceClient` オブジェクトのデフォルトのコンストラクタを使用します。
   * の作成 `GeneratePDFServiceClient.Endpoint.Address` オブジェクトを `System.ServiceModel.EndpointAddress` コンストラクタ。 WSDL をAEM Formsサービスに渡す文字列値 ( 例： `http://localhost:8080/soap/services/GeneratePDFService?blob=mtom`.) を使用する必要はありません。 `lc_version` 属性。 ただし、 `?blob=mtom`.
   * の作成 `System.ServiceModel.BasicHttpBinding` オブジェクトを作成するには、 `GeneratePDFServiceClient.Endpoint.Binding` フィールドに入力します。 戻り値を `BasicHttpBinding` にキャストします。
   * を `System.ServiceModel.BasicHttpBinding` オブジェクトの `MessageEncoding` ～に向かって `WSMessageEncoding.Mtom`. この値は、MTOM が確実に使用されるようにします。
   * 次のタスクを実行して、基本的な HTTP 認証を有効にします。

      * フィールドにAEM forms ユーザー名を割り当てます。 `GeneratePDFServiceClient.ClientCredentials.UserName.UserName`.
      * 対応するパスワード値をフィールドに割り当てます。 `GeneratePDFServiceClient.ClientCredentials.UserName.Password`.
      * 定数値を割り当て `HttpClientCredentialType.Basic` フィールドに `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 定数値を割り当て `BasicHttpSecurityMode.TransportCredentialOnly` フィールドに `BasicHttpBindingSecurity.Security.Mode`.

1. 変換するPDFドキュメントを取得します。

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。この `BLOB` オブジェクトは、変換されたPDFドキュメントを保存するために使用されます。
   * の作成 `System.IO.FileStream` オブジェクトを指定します。
   * コンテンツを格納するバイト配列を作成します。 `System.IO.FileStream` オブジェクト。 バイト配列のサイズは、 `System.IO.FileStream` オブジェクトの `Length` プロパティ。
   * を呼び出して、バイト配列にストリームデータを入力します。 `System.IO.FileStream` オブジェクトの `Read` メソッドを使用し、読み込むバイト配列、開始位置、ストリーム長を渡す。
   * 次の項目に `BLOB` オブジェクトに割り当てることによって `MTOM` プロパティは、バイト配列の内容を示します。

1. PDF文書を変換

   を呼び出す `GeneratePDFServiceServiceWse` オブジェクトの `ExportPDF2` メソッドを使用して、次の値を渡します。

   * A `BLOB` 変換するPDFファイルを表すオブジェクト。
   * 変換するファイルのパス名を含む文字列。
   * A `java.lang.String` ファイルの場所を指定するオブジェクト。
   * 変換対象のファイルの種類を指定する string オブジェクト。 以下のように `RTF`.
   * オプション `BLOB` オブジェクトドキュメントの生成時に適用されるPDFを含むオブジェクト。
   * 型の出力パラメーター `BLOB` が `ExportPDF2` メソッド。 この `ExportPDF2` メソッドは、このオブジェクトに変換後のドキュメントを入力します。 （このパラメーター値は、Web サービスの呼び出しにのみ必要です）。

1. 変換したファイルを保存します。

   * 変換後の RTF ドキュメントを取得するには、 `BLOB` オブジェクトの `MTOM` フィールドをバイト配列に変換します。 byte 配列は変換された RTF ドキュメントを表します。 必ず `BLOB` オブジェクトの `ExportPDF2` メソッド。
   * の作成 `System.IO.FileStream` オブジェクトを指定します。 RTF ファイルの場所を表す string 値を渡します。
   * の作成 `System.IO.BinaryWriter` オブジェクトのコンストラクタを呼び出し、 `System.IO.FileStream` オブジェクト。
   * を呼び出して、バイト配列の内容を RTF ファイルに書き込みます。 `System.IO.BinaryWriter` オブジェクトの `Write` メソッドを使用してバイト配列を渡す。

**関連トピック**

[手順の概要](converting-file-formats-pdf.md#summary-of-steps)

[MTOM を使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRef を使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 追加のネイティブファイル形式のサポートの追加 {#adding-support-for-additional-native-file-formats}

この節では、追加のネイティブファイル形式のサポートを追加する方法について説明します。 GeneratePDFサービスと、このサービスがネイティブファイル形式の変換に使用するネイティブアプリケーションとの間のやり取りの概要をPDFに示します。

この節では、次の点についても説明します。

* この製品がネイティブファイル形式をPDFに変換する際に既に使用しているネイティブPDFに対する Generate 形式サービスの応答を変更する方法
* GeneratePDFサービス、GeneratePDFサービスの Application Monitor(AppMon) コンポーネント、およびMicrosoft Word などのネイティブアプリケーション間のインタラクション
* XML の文法がこれらの操作で果たす役割

### コンポーネントの操作 {#component-interactions}

GeneratePDFサービスは、ネイティブファイル形式を変換します。そのファイル形式に関連付けられたアプリケーションを呼び出し、アプリケーションとやり取りして、デフォルトのプリンターを使用してドキュメントを印刷します。 デフォルトのプリンターをAdobe PDFプリンターとして設定する必要があります。

この図は、ネイティブアプリケーションのサポートに関連するコンポーネントとドライバを示しています。 また、インタラクションに影響を与える XML 文法についても言及しています。

ネイティブファイル変換のコンポーネントの操作

このドキュメントでは、 *ネイティブアプリケーション* ：ネイティブファイル形式 (Microsoft Word など ) の生成に使用するアプリケーションを示します。

*AppMon* は、ユーザーがアプリケーションで表示されるダイアログボックス間を移動するのと同じ方法でネイティブアプリケーションとやり取りするエンタープライズコンポーネントです。 AppMon が、Microsoft Word などのアプリケーションに対して、ファイルを開いて印刷するように指示する際に使用する XML 文法には、次の順次タスクが含まれます。

1. ファイル/開くを選択してファイルを開く
1. [ 開く ] ダイアログボックスが表示されていることを確認する。そうでない場合は、エラーの処理
1. 「ファイル名」フィールドにファイル名を入力し、「開く」ボタンをクリックします。
1. ファイルが実際に開くことの確認
1. 「ファイル」>「印刷」を選択して、印刷ダイアログボックスを開きます。
1. [ 印刷 ] ダイアログボックスが表示されることの確認

AppMon は、標準の Win32 API を使用して、キーストロークやマウスクリックなどの UI イベントを転送するために、サードパーティのアプリケーションとやり取りします。これは、これらのアプリケーションを制御してPDFファイルを生成するのに役立ちます。

これらの Win32 API の制限により、AppMon は、TextPad などの一部のアプリケーションで見つかるフローティングメニューバーや、Win32 API を使用してコンテンツを取得できない特定の種類のダイアログなど、特定の種類のウィンドウにこれらの UI イベントをディスパッチできません。

フローティングメニューバーを視覚的に識別するのは簡単です。ただし、特別な種類のダイアログは、目視検査だけでは特定できない場合があります。 Microsoft Spy++(Microsoft Visual C++開発環境の一部 ) や同等の WinID（から無料でダウンロード可能）などのサードパーティアプリケーションが必要になります。 [https://www.dennisbabkin.com/php/download.php?what=WinID](https://www.dennisbabkin.com/php/download.php?what=WinID)) を参照して、AppMon が標準の Win32 API を使用して AppMon とやり取りできるかどうかを判断するためのダイアログを調べます。

WinID がテキスト、サブウィンドウ、ウィンドウクラス ID などのダイアログの内容を抽出できる場合は、AppMon も同じ処理を実行できます。

次の表は、ネイティブファイル形式の印刷で使用される情報の種類を示しています。

<table> 
 <thead> 
  <tr> 
   <th><p>情報タイプ</p></th> 
   <th><p>説明</p></th> 
   <th><p>ネイティブファイルに関連するエントリの変更/作成 </p></th> 
  </tr> 
 </thead> 
 <tbody> 
  <tr> 
   <td><p>管理設定 </p></td> 
   <td><p>PDF設定、セキュリティ設定、およびファイルタイプ設定が含まれます。 </p><p>ファイルタイプ設定は、ファイル名拡張子を対応するネイティブアプリケーションに関連付けます。 ファイルタイプ設定では、ネイティブファイルの印刷に使用するネイティブアプリケーション設定も指定します。 </p></td> 
   <td><p>既にサポートされているネイティブアプリケーションの設定を変更するには、システム管理者が管理コンソールで「ファイルタイプ設定」を設定します。 </p><p>新しいネイティブファイル形式のサポートを追加するには、ファイルを手動で編集する必要があります。 ( <a href="converting-file-formats-pdf.md#adding-or-modifying-support-for-a-native-file-format">ネイティブファイル形式のサポートの追加または変更</a>.) </p></td> 
  </tr> 
  <tr> 
   <td><p>スクリプト </p></td> 
   <td><p>Generate アプリケーションサービスとネイティブPDFの間のやり取りを指定します。 このようなやり取りは、通常、アプリケーションに対して、Adobe PDFドライバーにファイルを印刷するよう指示します。 </p><p>スクリプトには、特定のダイアログボックスを開くようネイティブアプリケーションに指示し、それらのダイアログボックスのフィールドやボタンに対して特定の応答を提供する指示が含まれています。 </p></td> 
   <td><p>Generate Application サービスには、サポートされるすべてのネイティブPDF用のスクリプトファイルが含まれます。 これらのファイルは、XML 編集アプリケーションを使用して変更できます。</p><p>新しいネイティブアプリケーションのサポートを追加するには、新しいスクリプトファイルを作成する必要があります。 ( <a href="converting-file-formats-pdf.md#creating-or-modifying-an-additional-dialog-xml-file-for-a-native-application">ネイティブアプリケーション用の追加のダイアログ XML ファイルの作成または変更</a>.) </p></td> 
  </tr> 
  <tr> 
   <td><p>汎用ダイアログボックスの手順 </p></td> 
   <td><p>複数のアプリケーションに共通のダイアログボックスに対する応答方法を指定します。 このようなダイアログボックスは、オペレーティングシステム、ヘルパーアプリケーション（PDFMaker など）、およびドライバによって生成されます。 </p><p>この情報を含むファイルは、appmon.global.en_US.xml です。</p></td> 
   <td><p>このファイルは変更しないでください。 </p></td> 
  </tr> 
  <tr> 
   <td><p>アプリケーション固有のダイアログボックスの説明</p></td> 
   <td><p>アプリケーション固有のダイアログボックスに対する応答方法を指定します。 </p><p>この情報を含むファイルは appmon です。<i>[appname]</i>.dialog.<i>[locale]</i>.xml （appmon.word.en_US.xml など）</p></td> 
   <td><p>このファイルは変更しないでください。 </p><p>新しいネイティブアプリケーション用のダイアログボックスの手順を追加するには、 <a href="converting-file-formats-pdf.md#creating_or_modifying_an_additional_dialog_xml_file_for_a_native_application">ネイティブアプリケーション用の追加のダイアログ XML ファイルの作成または変更</a>.</p></td> 
  </tr> 
  <tr> 
   <td><p>その他のアプリケーション固有のダイアログボックスの手順 </p></td> 
   <td><p>アプリケーション固有のダイアログボックスの手順に対する上書きと追加を指定します。 この節では、このような情報の例を示します。 </p><p>この情報を含むファイルは appmon です。<i>[appname]</i>.addition.<i>[locale]</i>.xml. 例えば、appmon.addition.en_US.xml などがあります。</p></td> 
   <td><p>このタイプのファイルは、XML 編集アプリケーションを使用して作成および変更できます。 ( <a href="converting-file-formats-pdf.md#creating-or-modifying-an-additional-dialog-xml-file-for-a-native-application">ネイティブアプリケーション用の追加のダイアログ XML ファイルの作成または変更</a>.) </p><p><strong>重要</strong>:サーバーがサポートするネイティブアプリケーションごとに、追加のアプリケーション固有のダイアログボックスの手順を作成する必要があります。 </p></td> 
  </tr> 
 </tbody> 
</table>

### スクリプトとダイアログの XML ファイルについて {#about-the-script-and-dialog-xml-files}

スクリプト XML ファイルは、GeneratePDFサービスに対し、ユーザーがアプリケーションのダイアログボックス間を移動するのと同じ方法で、アプリケーションのダイアログボックス間を移動するよう指示します。 スクリプト XML ファイルは、ボタンの押し下げ、チェックボックスの選択/選択解除、メニュー項目の選択などのアクションを実行することで、GeneratePDFサービスに対してダイアログボックスに応答するよう指示します。

これに対し、ダイアログ XML ファイルは、スクリプト XML ファイルで使用されるのと同じタイプのアクションを持つダイアログボックスに対して応答するだけです。

#### ダイアログボックスとウィンドウ要素の用語 {#dialog-box-and-window-element-terminology}

この節と次の節では、説明するパースペクティブに応じて、ダイアログボックスとそれに含まれるコンポーネントに対して異なる用語を使用します。 ダイアログボックスのコンポーネントは、ボタン、フィールド、コンボボックスなどの項目です。

このセクションと次のセクションで、ユーザーの観点からダイアログボックスとそのコンポーネントを説明する場合、 *ダイアログボックス*, *ボタン*, *フィールド*、および *コンボボックス* が使用されます。

このセクションと次のセクションで、ダイアログボックスとそのコンポーネントを内部表現の観点から説明する場合、 *ウィンドウ要素* が使用されます。 窓要素の内部表現は階層で、各窓要素のインスタンスはラベルで識別されます。 ウィンドウ要素インスタンスは、その物理的な特性と動作も記述します。

ユーザーの視点から見ると、ダイアログボックスとそのコンポーネントは異なる動作を示し、一部のダイアログボックス要素は、アクティブ化されるまで非表示になります。 内部表現の観点からは、そのような行動の問題は存在しません。 例えば、ダイアログボックスの内部表現は、そのダイアログボックスに含まれるコンポーネントの内部表現に似ていますが、コンポーネントがダイアログボックス内にネストされている点が異なります。

この節では、AppMon に手順を提供する XML 要素について説明します。 これらの要素には、 `dialog` 要素と `window` 要素。 このドキュメントでは、XML 要素を区別するために等幅フォントを使用します。 この `*dialog*` element は、XML スクリプトファイルが意図せずに表示される原因となる可能性のあるダイアログボックスを識別します。 この `*window*` element は、ウィンドウ要素（ダイアログボックスまたはダイアログボックスのコンポーネント）を識別します。

#### 階層 {#hierarchy}

次の図は、スクリプトとダイアログの XML の階層を示しています。 スクリプト XML ファイルは、script.xsd スキーマに準拠しており、この script.xsd スキーマには、window.xsd スキーマが（XML の意味で）含まれます。 同様に、ダイアログ XML ファイルは dialogs.xsd スキーマに準拠し、dialogs.xsd スキーマにも window.xsd スキーマが含まれます。

![as_as_xml_hierarchy](assets/as_as_xml_hierarchy.png)

スクリプトとダイアログの XML の階層

#### スクリプト XML ファイル {#script-xml-files}

A *スクリプト XML ファイル* は、特定のウィンドウ要素に移動し、それらの要素に応答を提供するようネイティブアプリケーションに指示する一連の手順を指定します。 ほとんどの応答は、対応するダイアログボックスのフィールド、コンボボックス、またはボタンに対してユーザーが入力した入力に対応するテキストまたはキーストロークです。

GeneratePDFサービスでスクリプト XML ファイルをサポートする目的は、ネイティブアプリケーションにネイティブファイルを印刷するよう指示することです。 ただし、スクリプト XML ファイルを使用して、ネイティブアプリケーションのダイアログボックスとの対話中にユーザーが実行できるタスクを実行できます。

スクリプト XML ファイル内の手順は、分岐の機会がなく、順番に実行されます。 唯一の条件付きテストは、タイムアウト/再試行に対してサポートされます。これにより、特定の期間内および特定の回数の再試行の後にステップが正常に完了しなかった場合に、スクリプトが終了します。

順次的なステップに加えて、ステップ内の命令も順に実行されます。 手順と手順が、ユーザーが同じ手順を実行する順序を反映していることを確認する必要があります。

スクリプト XML ファイルの各ステップは、ステップの指示が正常に実行された場合に表示されるウィンドウ要素を識別します。 スクリプトステップの実行中に予期しないダイアログボックスが表示された場合、次の節で説明するように、GeneratePDFサービスはダイアログ XML ファイルを検索します。

#### ダイアログ XML ファイル {#dialog-xml-files}

ネイティブアプリケーションを実行すると、異なるダイアログボックスが表示されます。これは、ネイティブアプリケーションが表示モードか非表示モードかに関係なく表示されます。 ダイアログボックスは、オペレーティングシステムによって生成することも、アプリケーション自体によって生成することもできます。 ネイティブアプリケーションがPDF生成サービスの制御下で実行されている場合、システムおよびネイティブアプリケーションのダイアログボックスが非表示ウィンドウに表示されます。

A *ダイアログ XML ファイル* 「生成PDFサービス」で、システムまたはネイティブアプリケーションのダイアログボックスに対する応答を指定します。 ダイアログ XML ファイルを使用すると、GeneratePDFサービスは、変換プロセスを容易にする方法で、プロンプトのないダイアログボックスに応答できます。

現在実行中のスクリプト XML ファイルで処理されないダイアログボックスがPDFされた場合、Generate アプリケーションサービスは、一致が見つかると停止し、次の順序でダイアログ XML ファイルを検索します。

* アプリモン&#x200B;*[appname]*.additional.*[ロケール]*.xml
* アプリモン&#x200B;*[appname].[ロケール]*.xml （このファイルは変更しないでください。）
* appmon.global.*[ロケール]*.xml （このファイルは変更しないでください。）

GeneratePDFサービスは、ダイアログボックスに一致するものが見つかった場合、そのダイアログボックスに指定されたキーストロークまたは他の操作を送信することで破棄します。 ダイアログボックスの指示で中止メッセージを指定した場合、GeneratePDFサービスは現在実行中のジョブを終了し、エラーメッセージを生成します。 このような中止メッセージは、 `abortMessage` 要素が XML 文法に従って配置されます。

GeneratePDFサービスで、上記のファイルに記載されていないダイアログボックスが表示された場合、そのダイアログボックスのキャプションが GeneratePDFサービスによってログファイルエントリに組み込まれます。 現在実行中のジョブは最終的にタイムアウトになります。 その後、ログファイル内の情報を使用して、ネイティブアプリケーション用の追加のダイアログ XML ファイルで新しい手順を作成できます。

### ネイティブファイル形式のサポートの追加または変更 {#adding-or-modifying-support-for-a-native-file-format}

このセクションでは、他のネイティブファイル形式をサポートするために実行する必要がある作業、または既にサポートされているネイティブファイル形式のサポートを変更するために実行する必要がある作業について説明します。

サポートを追加または変更する前に、次の作業を行う必要があります。

#### 窓要素を識別するツールの選択 {#choosing-a-tool-for-identifying-window-elements}

ダイアログおよびスクリプトの XML ファイルでは、ダイアログまたはスクリプト要素が応答するウィンドウ要素（ダイアログボックス、フィールド、またはその他のダイアログコンポーネント）を指定する必要があります。 例えば、スクリプトがネイティブ・アプリケーションのメニューを呼び出した後、スクリプトはキー操作またはアクションを適用するメニューのウィンドウ要素を識別する必要があります。

ダイアログボックスは、タイトルバーに表示されるキャプションによって簡単に識別できます。 ただし、下位レベルの窓要素を識別するには、Microsoft Spy++などのツールを使用する必要があります。 下位レベルのウィンドウ要素は、明らかではない様々な属性を使用して識別できます。 さらに、各ネイティブアプリケーションでは、ウィンドウ要素を異なる方法で識別する場合があります。 その結果、ウィンドウ要素を識別する方法は複数あります。 ウィンドウ要素の識別を考慮するための推奨順序を次に示します。

1. 一意の場合はキャプション自体
1. 特定のダイアログボックスに対して一意である場合とそうでない場合があるコントロール ID
1. クラス名（一意である場合とそうでない場合があります）

ウィンドウを識別するために、これら 3 つの属性の 1 つまたは複数の属性の組み合わせを使用できます。

属性でキャプションを識別できない場合は、親に対するインデックスを使用して、ウィンドウ要素を識別できます。 An *index* 兄弟の window 要素を基準とした window 要素の位置を指定します。 多くの場合、コンボボックスを識別するには、インデックスしか使用できません。

次の問題に注意してください。

* Microsoft Spy++は、キャプションのホットキーを識別するためにアンパサンド (&amp;) を使用してキャプションを表示します。 たとえば、Spy++は、1 つの [ 印刷 ] ダイアログボックスのキャプションを `Pri&nt`：ホットキーが *n*. スクリプトおよびダイアログ XML ファイルのキャプションタイトルは、アンパサンドを省略する必要があります。
* 一部のキャプションには改行が含まれています。 GeneratePDFサービスは改行を識別できません。 キャプションに改行が含まれている場合は、他のメニュー項目と区別するのに十分なキャプションを含め、省略された部分に正規表現を使用します。 例えば、( `^Long caption title$`) をクリックします。 ( [キャプション属性での正規表現の使用](converting-file-formats-pdf.md#using-regular-expressions-in-caption-attributes).)
* 予約 XML 文字には、文字エンティティ（エスケープシーケンスとも呼ばれます）を使用します。 例えば、 `&` アンパサンド `<` および `>` 記号より小さく、記号より大きい `&apos;` 使用を終えた後に `&quot;` 引用符の場合は

ダイアログまたはスクリプト XML ファイルを使用する場合は、Microsoft Spy++アプリケーションをインストールする必要があります。

#### ダイアログおよびスクリプトファイルのパッケージ解除 {#unpackaging-the-dialog-and-script-files}

ダイアログファイルとスクリプトファイルは、appmondata.jar ファイルに存在します。 これらのファイルを変更したり、新しいスクリプトまたはダイアログファイルを追加したりする前に、この JAR ファイルのパッケージを解除する必要があります。 例えば、EditPlus アプリケーションのサポートを追加するとします。 appmon.editplus.script.en_US.xml という名前の 2 つの XML ファイルを作成し、appmon.editplus.script.addition.en_US.xml という名前を付けます。 次に示すように、これらの XML スクリプトを adobe-appmondata.jar ファイルの 2 つの場所に追加する必要があります。

* adobe-livecycle-native-jboss-x86_win32.ear > adobe-Native2PDFSvc.war\WEB-INF\lib > adobe-native.jar > Native2PDFSvc-native.jar\bin > adobe-appmondata.jar\com\adobe\appmon adobe-livecycle-native-jboss-x86_win32.ear ファイルは、*の export フォルダーにあります。[AEM forms インストールディレクトリ]\*configurationManager を使用します。 (AEM Formsが別の J2EE アプリケーションサーバーにデプロイされている場合は、adobe-livecycle-native-jboss-x86_win32.ear ファイルを、J2EE アプリケーションサーバーに対応する EAR ファイルに置き換えます )。
* adobe-generatepdf-dsc.jar / adobe-appmondata.jar\com\adobe\appmon （adobe-appmondata.jar ファイルは adobe-generatepdf-dsc.jar ファイル内にあります）。 adobe-generatepdf-dsc.jar ファイルは、 *[AEM forms インストールディレクトリ]*\deploy フォルダー。

これらの XML ファイルを adobe-appmondata.jar ファイルに追加した後、GeneratePDF コンポーネントを再デプロイする必要があります。 adobe-appmondata.jar ファイルにダイアログおよびスクリプト XML ファイルを追加するには、次のタスクを実行します。

1. WinZip や WinRAR などのツールを使用して、adobe-livecycle-native-jboss-x86_win32.earfile / adobe-Native2PDFSvc.war\WEB-INF\lib > adobe-native.jar > Native2PDFSvc-native.jar\bin > adobe-appmondata.jrjar ファイル。
1. appmondata.jar ファイルにダイアログおよびスクリプト XML ファイルを追加するか、このファイル内の既存の XML ファイルを変更します。 ( [ネイティブアプリケーション用のスクリプト XML ファイルの作成または変更](converting-file-formats-pdf.md#creating-or-modifying-a-script-xml-file-for-a-native-application)および [ネイティブアプリケーション用の追加のダイアログ XML ファイルの作成または変更](converting-file-formats-pdf.md#creating-or-modifying-an-additional-dialog-xml-file-for-a-native-application).)
1. WinZip や WinRAR などのツールを使用して、 adobe-generatepdf-dsc.jar / adobe-appmondata.jar を開きます。
1. appmondata.jar ファイルにダイアログおよびスクリプト XML ファイルを追加するか、このファイル内の既存の XML ファイルを変更します。 ( [ネイティブアプリケーション用のスクリプト XML ファイルの作成または変更](converting-file-formats-pdf.md#creating-or-modifying-a-script-xml-file-for-a-native-application)および [ネイティブアプリケーション用の追加のダイアログ XML ファイルの作成または変更](converting-file-formats-pdf.md#creating-or-modifying-an-additional-dialog-xml-file-for-a-native-application).) XML ファイルを adobe-appmondata.jar ファイルに追加した後、新しい adobe-appmondata.jar ファイルを adobe-generatepdf-dsc.jar ファイルに配置します。
1. 追加のネイティブファイル形式のサポートを追加した場合は、アプリケーションのパスを提供するシステム環境変数を作成します ( [ネイティブアプリケーションを見つけるための環境変数の作成](converting-file-formats-pdf.md#creating-an-environment-variable-to-locate-the-native-application).)

**GeneratePDF コンポーネントを再デプロイするには**

1. Workbench にログインします。
1. 選択 **ウィンドウ** > **ビューを表示** > **コンポーネント**. この操作により、コンポーネントビューが Workbench に追加されます。
1. GeneratePDF コンポーネントを右クリックし、「 **コンポーネントを停止**.
1. コンポーネントが停止したら、右クリックして [ コンポーネントのアンインストール ] を選択し、コンポーネントを削除します。
1. を右クリックします。 **コンポーネント** アイコンと選択 **コンポーネントをインストール**.
1. 変更された adobe-generatepdf-dsc.jar ファイルを参照して選択し、「開く」をクリックします。 GeneratePDF コンポーネントの横に赤い四角形が表示されます。
1. GeneratePDF コンポーネントを展開し、「サービス記述子」を選択し、「GeneratePDFService」を右クリックして「サービスをアクティブ化」を選択します。
1. 表示される設定ダイアログボックスで、適切な設定値を入力します。 これらの値を空白のままにした場合、デフォルトの設定値が使用されます。
1. 「PDF を生成」を右クリックし、「コンポーネントを開始」を選択します。
1. [ アクティブなサービス ] を展開します。 サービス名の横に緑色の矢印が表示されます（実行中の場合）。 それ以外の場合、サービスは停止状態になります。
1. サービスが停止状態の場合は、サービス名を右クリックし、「Start Service」を選択します。

### ネイティブアプリケーション用のスクリプト XML ファイルの作成または変更 {#creating-or-modifying-a-script-xml-file-for-a-native-application}

新しいネイティブアプリケーションにファイルをダイレクトする場合は、そのアプリケーション用のスクリプト XML ファイルを作成する必要があります。 GeneratePDFサービスと、既にサポートされているネイティブアプリケーションとのやり取りを変更する場合は、そのアプリケーションのスクリプトを変更する必要があります。

スクリプトには、ネイティブアプリケーションのウィンドウ要素間を移動し、それらの要素に対して特定の応答を提供する手順が含まれています。 この情報を含むファイルは appmon です。*[appname]*.script.*[ロケール]*.xml. 例えば、appmon.notepad.script.en_US.xml などがあります。

#### スクリプトが実行する必要があるステップの識別 {#identifying-steps-the-script-must-execute}

ネイティブアプリケーションを使用して、移動する必要のあるウィンドウ要素と、ドキュメントを印刷するために実行する必要がある各応答を決定します。 任意の応答によって生成されるダイアログボックスに注意してください。 手順は次の手順に似ています。

1. ファイル／開くを選択します。
1. パスを指定し、「開く」をクリックします。
1. メニューバーでファイル/印刷を選択します。
1. プリンタに必要なプロパティを指定します。
1. [ 印刷 ] を選択し、[ 名前を付けて保存 ] ダイアログボックスが表示されるのを待ちます。 Generate Service で Save As ダイアログボックスが必要なのは、PDFファイルの保存先を指定するためです。

#### キャプション属性で指定されたダイアログの識別 {#identifying-the-dialogs-specified-in-caption-attributes}

Microsoft Spy++を使用して、ネイティブアプリケーションの window 要素プロパティの ID を取得します。 スクリプトを記述するには、次の ID が必要です。

#### キャプション属性での正規表現の使用 {#using-regular-expressions-in-caption-attributes}

キャプションの仕様では、正規表現を使用できます。 GeneratePDFサービスでは、 `java.util.regex.Matcher` 正規表現をサポートするクラス。 このユーティリティは、 `java.util.regex.Pattern`.

**メモ帳バナーでメモ帳の前に付けられたファイル名を格納する正規表現**

```as3
 <!-- The regular expression ".*Notepad" means any number of non-terminating characters followed by Notepad. --> 
 <step> 
     <expectedWindow> 
         <window caption=".*Notepad"/> 
     </expectedWindow> 
 </step>
```

**印刷と印刷設定を区別する正規表現**

```as3
 <!-- This regular expression differentiates the Print dialog box from the Print Setup dialog box. The "^" specifies the beginning of the line, and the "$" specifies the end of the line. --> 
 <windowList> 
     <window controlID="0x01" caption="^Print$" action="press"/> 
 </windowList>
```

#### window 要素と windowList 要素の順序付け {#ordering-the-window-and-windowlist-elements}

ご注文ください `window` および `windowList` 要素を次に示します。

* 複数の場合 `window` 要素は `windowList` または `dialog` 要素、並べ替え `window` の長さを持つ降順の要素 `caption` 順序内の位置を示す名前。
* 複数の場合 `windowList` 要素が `window` 要素、並べ替え `windowList` の長さを持つ降順の要素 `caption` 最初の `indexes/`順序内の位置を示す要素。

**ダイアログファイル内のウィンドウ要素の並べ替え**

```as3
 <!-- The caption attribute in the following window element is 40 characters long. It is the longest caption in this example, so its parent window element appears before the others. --> 
 <window caption="Unexpected Failure in DebugActiveProcess"> 
     <…> 
 </window> 
  
 <!-- Caption length is 33 characters. --> 
 <window caption="Adobe Acrobat - License Agreement"> 
     <…> 
 </window> 
  
 <!-- Caption length is 33 characters. --> 
 <window caption="Microsoft Visual.*Runtime Library"> 
     <…> 
 </window> 
  
 <!-- The caption attribute in the following window element is 28 characters long. It is the shortest caption in this example, so its parent window element appears after the others. --> 
 <window caption="Adobe Acrobat - Registration"> 
     <…> 
 </window>
```

**windowList 要素内のウィンドウ要素の順序付け**

```as3
 <!-- The caption attribute in the following indexes element is 56 characters long. It is the longest caption in this example, so its parent window element appears before the others. --> 
 <windowList> 
     <window caption="Can&apos;t exit design mode because.* cannot be created"/> 
     <window className="Button" caption="OK" action="press"/> 
 </windowList> 
 <windowList> 
     <window caption="Do you want to continue loading the project?"/> 
     <window className="Button" caption="No" action="press"/> 
 </windowList> 
 <windowList> 
     <window caption="The macros in this project are disabled"/> 
     <window className="Button" caption="OK" action="press"/> 
 </windowList>
```

### ネイティブアプリケーション用の追加のダイアログ XML ファイルの作成または変更 {#creating-or-modifying-an-additional-dialog-xml-file-for-a-native-application}

以前にサポートされていなかったネイティブアプリケーション用のスクリプトを作成する場合は、そのアプリケーション用の追加のダイアログ XML ファイルも作成する必要があります。 AppMon が使用する各ネイティブアプリケーションには、1 つの追加のダイアログ XML ファイルのみを含める必要があります。 未承諾のダイアログボックスが見つからない場合でも、追加のダイアログ XML ファイルが必要です。 追加のダイアログボックスには、少なくとも 1 つの `window` 要素（その場合でも） `window` 要素はプレースホルダーにすぎません。

>[!NOTE]
>
>この文脈では、「追加」とは、アプリモンの内容を意味します。[applicationname].addition.[ロケール].xml ファイル。 このようなファイルは、ダイアログの XML ファイルの上書きと追加を指定します。

また、次の目的で、ネイティブアプリケーション用の追加のダイアログ XML ファイルを変更することもできます。

* 異なる応答を持つアプリケーションのダイアログ XML ファイルを上書きするには
* そのアプリケーションのダイアログ XML ファイル内で指定されていないダイアログボックスに応答を追加するには

追加の dialogXML ファイルを識別するファイル名は appmon です。*[appname]*.addition.*[ロケール]*.xml. 例えば、appmon.excel.addition.en_US.xml などがあります。

追加のダイアログ XML ファイルの名前は、appmon という形式を使用する必要があります。*[applicationname]*.addition.*[ロケール]*.xml，ここで *applicationname* は、XML 設定ファイルおよびスクリプトで使用されるアプリケーション名と完全に一致する必要があります。

>[!NOTE]
>
>native2pdfconfig.xml 設定ファイルで指定された汎用アプリケーションに、プライマリダイアログ XML ファイルがありません。 セクション [ネイティブファイル形式のサポートの追加または変更](converting-file-formats-pdf.md#adding-or-modifying-support-for-a-native-file-format) では、このような仕様について説明します。

ご注文ください `windowList` の子として表示される要素 `window` 要素。 ( [window 要素と windowList 要素の順序付け](converting-file-formats-pdf.md#ordering-the-window-and-windowlist-elements).)

### 一般ダイアログ XML ファイルの変更 {#modifying-the-general-dialog-xml-file}

一般ダイアログ XML ファイルを変更して、システムで生成されるダイアログボックスに応答したり、複数のアプリケーションに共通するダイアログボックスに応答したりできます。

#### XML 設定ファイルへのファイルタイプエントリの追加 {#adding-a-filetype-entry-in-the-xml-configuration-file}

この手順では、Generate Application サービス設定ファイルを更新して、PDF型をネイティブアプリケーションに関連付ける方法を説明します。 この設定ファイルを更新するには、管理コンソールを使用して設定データをファイルに書き出す必要があります。 設定データのデフォルトのファイル名は native2pdfconfig.xml です。

**生成PDFサービス設定ファイルの更新**

1. 選択 **ホーム** > **サービス** > **Adobe PDF Generator** > **設定ファイル**&#x200B;を選択し、 **設定を書き出し**.
1. を変更します。 `filetype-settings` 要素を必要に応じて native2pdfconfig.xml ファイルに追加します。
1. 選択 **ホーム** > **サービス** > **Adobe PDF Generator** >**設定ファイル**&#x200B;を選択し、 **設定を読み込み**. 設定データが Generate 設定サービスに読み込まれ、以前のPDFに置き換えられます。

>[!NOTE]
>
>アプリケーションの名前は、 `GenericApp` 要素の `name` 属性。 この値は、そのアプリケーション用に開発するスクリプトで指定された、対応する名前と完全に一致する必要があります。 同様に、 `GenericApp` 要素の `displayName` 属性は、対応するスクリプトの `expectedWindow` ウィンドウのキャプション。 このような等価性は、 `displayName` または `caption` 属性。

この例では、GeneratePDFサービスで提供されるデフォルトの設定データを変更し、(Microsoft Word ではなく ) メモ帳を使用して、ファイル名拡張子が.txt のファイルを処理するように指定しました。 この変更を行う前に、Microsoft Word は、このようなファイルを処理するネイティブアプリケーションとして指定されていました。

**テキストファイルをメモ帳に転送するための変更 (native2pdfconfig.xml)**

```as3
 <filetype-settings> 
  
 <!-- Some native app file types were omitted for brevity. --> 
 <!-- The following GenericApp element specifies Notepad as the native application that should be used to process files that have a txt file name extension. --> 
             <GenericApp 
                 extensions="txt" 
                 name="Notepad" displayName=".*Notepad"/> 
             <GenericApp  
                 extensions="wpd"  
                 name="WordPerfect" displayName="Corel WordPerfect"/> 
             <GenericApp extensions="pmd,pm6,p65,pm"  
                 name="PageMaker" displayName="Adobe PageMaker"/> 
             <GenericApp extensions="fm"  
                 name="FrameMaker" displayName="Adobe FrameMaker"/> 
             <GenericApp extensions="psd"  
                 name="Photoshop" displayName="Adobe Photoshop"/> 
         </settings> 
     </filetype-settings>
```

#### ネイティブアプリケーションを見つけるための環境変数の作成 {#creating-an-environment-variable-to-locate-the-native-application}

ネイティブアプリケーション実行可能ファイルの場所を指定する環境変数を作成します。 変数は形式を使用する必要があります *[applicationname]*_PATH，ここで *applicationname* は、XML 設定ファイルおよびスクリプトで使用されるアプリケーション名と完全に一致し、パスには実行可能ファイルへのパスが二重引用符で囲まれている必要があります。 このような環境変数の例を次に示します。 `Photoshop_PATH`.

新しい環境変数を作成した後、Generate 環境サービスがデプロイされているPDFを再起動する必要があります。

**Windows XP 環境でシステム変数を作成する**

1. 選択 **Campaign コントロールパネル/システム**.
1. [ システムのプロパティ ] ダイアログボックスで、 **詳細** タブを押し、 **環境変数**.
1. [ 環境変数 ] ダイアログボックスの [ システム変数 ] で、 **新規**.
1. [ 新しいシステム変数 ] ダイアログボックスで、 **変数名** ボックスに、 *[applicationname]*_PATH.
1. 内 **変数値** ボックスに、アプリケーションの実行可能ファイルのフルパスとファイル名を入力し、 **OK**. 例えば、次のように入力します。 `c:\windows\Notepad.exe`
1. [ 環境変数 ] ダイアログボックスで、 **OK**.

**コマンドラインからシステム変数を作成する**

1. コマンドラインウィンドウで、次の形式で変数定義を入力します。

   ```as3
            [applicationname]_PATH=[Full path name]
   ```

   例えば、次のように入力します。 `NotePad_PATH=C:\WINDOWS\NOTEPAD.EXE`

1. 新しいコマンドラインプロンプトを起動して、システム変数を有効にします。

#### XML ファイル {#xml-files}

AEM Formsには、GeneratePDFサービスで.txt というファイル名拡張子を持つファイルを処理するためのサンプル XML ファイルが含まれています。 このコードはこの節に含まれています。 さらに、この節で説明するその他の変更を行う必要があります。

#### 追加のダイアログ XML ファイル {#additional-dialog-xml-file}

この例では、メモ帳アプリケーション用の追加のダイアログボックスが含まれています。 これらのダイアログボックスは、Generate Dialog サービスで指定されたダイアログボックスに加えてPDFできます。

**メモ帳ダイアログボックス (appmon.notepad.addition.en_US.xml)**

```as3
 <dialogs app="Notepad" locale="en_US" version="7.0" xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="dialogs.xsd"> 
     <window caption="Caption Title"> 
         <windowList> 
             <window className="Button" caption="OK" action="press"/> 
         </windowList> 
     </window> 
 </dialogs>
```

#### スクリプト XML ファイル {#script-xml-file}

次の使用例は、GeneratePDFサービスがメモ帳とやり取りし、Adobe PDFプリンターを使用してファイルを印刷する方法を指定します。

**メモ帳スクリプト XML ファイル (appmon.notepad.script.en_US.xml)**

```as3
<?xml version="1.0" encoding="UTF-8" standalone="yes"?> 
<!-- 
* 
* ADOBE CONFIDENTIAL 
* ___________________ 
* Copyright 2004 - 2005 Adobe Systems Incorporated 
* All Rights Reserved. 
* 
* NOTICE:  All information contained herein is, and remains 
* the property of Adobe Systems Incorporated and its suppliers, 
* if any.  The intellectual and technical concepts contained 
* herein are proprietary to Adobe Systems Incorporated and its 
* suppliers and may be covered by U.S. and Foreign Patents, 
* patents in process, and are protected by trade secret or copyright law. 
* Dissemination of this information or reproduction of this material 
* is strictly forbidden unless prior written permission is obtained 
* from Adobe Systems Incorporated. 
*--> 
 
<!-- This file automates printing of text files via notepad to Adobe PDF printer. In order to see the complete hierarchy we recommend using the Microsoft Spy++ which details the properties of windows necessary to write scripts. In this sample there are total of eight steps--> 
 
<application name="Notepad" version="9.0" locale="en_US" xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="scripts.xsd"> 
 
    <!-- In this step we wait for the application window to appear --> 
    <step> 
        <expectedWindow> 
            <window caption=".*Notepad"/> 
        </expectedWindow> 
    </step> 
     
    <!-- In this step, we acquire the application window and send File->Open menu bar, menu item commands and the expectation is the windows Open dialog-->         
    <step> 
        <acquiredWindow> 
            <window caption=".*Notepad"> 
                <virtualInput> 
                    <menuBar> 
                        <selection> 
                            <name>File</name> 
                        </selection> 
                        <selection> 
                            <name>Open...</name> 
                        </selection> 
                    </menuBar> 
                </virtualInput> 
            </window> 
        </acquiredWindow> 
        <expectedWindow> 
            <window caption="Open"/> 
        </expectedWindow> 
    </step> 
     
    <!-- In this step, we acquire the Open window and then select the 'Edit' widget and input the source path followed by clicking on the 'Open' button . The expectation of this 'action' is that the Open dialog will disappear --> 
    <step> 
        <acquiredWindow> 
            <window caption="Open"> 
                <windowList> 
                    <window className="ComboBoxEx32"> 
                        <windowList> 
                            <window className="ComboBox"> 
                                <windowList> 
                                <window className="Edit" action="inputSourcePath"/> 
                                </windowList> 
                            </window> 
                        </windowList> 
                    </window> 
                </windowList> 
                <windowList> 
                    <window className="Button" caption="Open" action="press"/> 
                </windowList> 
            </window> 
        </acquiredWindow> 
        <expectedWindow> 
            <window caption="Open" action="disappear"/> 
        </expectedWindow> 
        <pause value="30"/> 
    </step> 
     
    <!-- In this step, we acquire the application window and send File->Print menu bar, menu item commands and the expectation is the windows Print dialog--> 
    <step> 
        <acquiredWindow> 
            <window caption=".*Notepad"> 
                <virtualInput> 
                    <menuBar> 
                        <selection> 
                            <name>File</name> 
                        </selection> 
                        <selection> 
                            <name>Print...</name> 
                        </selection> 
                    </menuBar> 
                </virtualInput> 
            </window> 
        </acquiredWindow> 
        <expectedWindow> 
            <window caption="Print"> 
        </window> 
        </expectedWindow> 
    </step> 
     
    <!-- In this step, we acquire the Print dialog and click on the 'Preferences' button and the expected window in this case is the dialog with the caption '"Printing Preferences' --> 
    <step> 
        <acquiredWindow> 
            <window caption="Print"> 
                <windowList> 
                    <window caption="General"> 
                        <windowList> 
                            <window className="Button" caption="Preferences" action="press"/> 
                        </windowList> 
                    </window> 
                </windowList> 
            </window> 
        </acquiredWindow> 
        <expectedWindow> 
            <window caption="Printing Preferences"/> 
        </expectedWindow> 
    </step> 
     
    <!-- In this step, we acquire the dialog "Printing Preferences' and select the combo box which is the 10th child of window with caption '"Adobe PDF Settings' and select the first index. (Note: All indeces start with 0.) Besides this we uncheck the box which  has the caption '"View Adobe PDF results' and we click on the button OK. The expectation is that 'Printing Preferences' dialog disappears. --> 
    <step> 
        <acquiredWindow> 
            <window caption="Printing Preferences"> 
                <windowList> 
                    <window caption="Adobe PDF Settings"> 
                        <windowList> 
                            <window className="Button" caption="View Adobe PDF results" action="uncheck"/> 
                        </windowList> 
                        <windowList> 
                            <window className="Button" caption="Ask to Replace existing PDF file" action="uncheck"/> 
                        </windowList> 
                    </window> 
                </windowList> 
                <windowList> 
                    <window className="Button" caption="OK" action="press"/> 
                </windowList> 
            </window> 
        </acquiredWindow> 
        <expectedWindow> 
            <window caption="Printing Preferences" action="disappear"/> 
        </expectedWindow> 
    </step> 
     
    <!-- In this step, we acquire the 'Print' dialog and click on the Print button. The expectation is that the dialog with caption 'Print' disappears. In this case we use the regular expression '^Print$' for specifying the caption given there could be multiple dialogs with caption that includes the word Print. --> 
    <step> 
        <acquiredWindow> 
            <window caption="Print"> 
                <windowList> 
                    <window caption="General"/> 
                    <window className="Button" caption="^Print$" action="press"/> 
                </windowList> 
            </window> 
        </acquiredWindow> 
        <expectedWindow> 
            <window caption="Print" action="disappear"/> 
        </expectedWindow> 
    </step> 
    <step> 
        <expectedWindow> 
            <window caption="Save PDF File As"/> 
        </expectedWindow> 
    </step> 
    <!-- Finally in this step, we acquire the dialog with caption "Save PDF File As" and in the Edit widget type the destination path for the output PDF file and click on the Save button. The expectation is that the dialog disappears--> 
    <step> 
        <acquiredWindow> 
            <window caption="Save PDF File As"> 
                <windowList> 
                    <window className="Edit" action="inputDestinationPath"/> 
                </windowList> 
                <windowList> 
                    <window className="Button" caption="Save" action="press"/> 
                </windowList> 
            </window> 
        </acquiredWindow> 
        <expectedWindow> 
            <window caption="Save PDF File As" action="disappear"/> 
        </expectedWindow> 
    </step> 
     
    <!-- We can always set a retry count or a maximum time for a step. In case we surpass these limitations, PDF Generator generates this abort message and terminates processing. --> 
    <abortMessage msg="15078"/> 
</application>
```
