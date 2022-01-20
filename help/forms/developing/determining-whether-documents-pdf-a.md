---
title: ドキュメントがPDF/A に準拠しているかどうかの判断
seo-title: Determining Whether Documents Are PDF/A-Compliant
description: Assembler サービスを使用して、Java API と Web サービス API を使用して、PDFドキュメントがPDF/A に準拠しているかどうかを判断します。
seo-description: Use the Assembler service to determine if a PDF document is PDF/A-compliant using the Java API and Web Service API.
uuid: 4e9d8c8f-2153-411b-9c4b-2d14b3c8f4bb
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: operations
discoiquuid: c429d6e1-7847-43c8-bf75-cb0078dbb9d5
role: Developer
exl-id: fa9d0720-f4bf-4933-ae63-c24bb835cc60
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '2082'
ht-degree: 4%

---

# ドキュメントがPDF/A に準拠しているかどうかの判断 {#determining-whether-documents-are-pdf-a-compliant}

Assembler サービスを使用すると、PDFドキュメントがPDF/A に準拠しているかどうかを確認できます。 PDF/A ドキュメントは、ドキュメントのコンテンツを長期間保存するためのアーカイブ形式として存在します。 フォントはドキュメント内に埋め込まれ、ファイルは圧縮されません。その結果、通常、PDF/A ドキュメントは標準の PDF ドキュメントよりも大きくなります。また、PDF/A ドキュメントには、オーディオおよびビデオコンテンツは含まれません。

PDF/A-1 仕様は、A と B という 2 つの適合レベルで構成されます。2 つのレベルの主な違いは、適合レベル B には必要ない論理構造（アクセシビリティ）のサポートです。適合レベルに関係なく、PDF/A-1 では、生成されたPDF/A 文書にすべてのフォントが埋め込まれます。 現時点では、検証（および変換）ではPDF/A-1b のみがサポートされています。

この説明では、次の DDX ドキュメントが使用されていると仮定します。

```as3
 <?xml version="1.0" encoding="UTF-8"?> 
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/"> 
         <DocumentInformation source="Loan.pdf" result="Loan_result.xml"> 
         <PDFAValidation compliance="PDF/A-1b" resultLevel="Detailed"                       ignoreUnusedResources="true" allowCertificationSignatures="true" /> 
     </DocumentInformation> 
 </DDX>
```

この DDX ドキュメント内で、 `DocumentInformation` element は、入力イベントドキュメントに関する情報を返すように Assembler サービスにPDFします。 内 `DocumentInformation` 要素、 `PDFAValidation` element は、入力PDFドキュメントがPDF/A に準拠しているかどうかを示す Assembler サービスに指示します。

Assembler サービスは、入力PDFドキュメントが、 `PDFAConformance` 要素。 入力PDFドキュメントがPDF/A に準拠している場合、 `PDFAConformance` 要素の `isCompliant` 属性が `true`. PDFドキュメントがPDF/A に準拠していない場合、 `PDFAConformance` 要素の `isCompliant` 属性が `false`.

>[!NOTE]
>
>この節で指定した DDX ドキュメントには `DocumentInformation` 要素の場合、Assembler サービスは XML データを返します。PDFドキュメントは返されません。 つまり、Assembler サービスは、Assembler ドキュメントのアセンブルやディスアセンブルをPDFしません。XML ドキュメント内の入力PDF・ドキュメントに関する情報を返します。

>[!NOTE]
>
>Assembler サービスについて詳しくは、 [AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>DDX ドキュメントについて詳しくは、 [Assembler サービスと DDX リファレンス](https://www.adobe.com/go/learn_aemforms_ddx_63).

## 手順の概要 {#summary-of-steps}

PDF・ドキュメントがPDF/A に準拠しているかどうかを判断するには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. Assembler クライアントをPDFします。
1. 既存の DDX ドキュメントを参照します。
1. PDF/A の準拠を判断するために使用されるPDFドキュメントを参照します。
1. 実行時オプションを設定します。
1. PDF・ドキュメントに関する情報を取得します。
1. 返された XML ドキュメントを保存します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。 Web サービスを使用している場合は、プロキシファイルを必ず含めてください。

次の JAR ファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar(AEM Formsを JBoss にデプロイする場合に必要 )
* jbossall-client.jar(AEM Formsが JBoss にデプロイされている場合に必要 )

AEM Formsが JBoss 以外のサポート対象の J2EE アプリケーションサーバーにデプロイされている場合は、adobe-utilities.jar ファイルと jbossall-client.jar ファイルを、AEM Formsがデプロイされている J2EE アプリケーションサーバーに固有の JAR ファイルに置き換える必要があります。 すべてのAEM Forms JAR ファイルの場所について詳しくは、 [AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Assembler クライアントのPDF**

Assembler 操作をプログラムで実行する前に、Assembler サービスクライアントを作成する必要があります。

**既存の DDX ドキュメントの参照**

Assembler サービス操作を実行するには、DDX ドキュメントを参照する必要があります。 入力PDFドキュメントがPDF/A に準拠しているかどうかを判断するには、DDX ドキュメントに `PDFAValidation` 要素内の `DocumentInformation` 要素。 この `PDFAValidation` element は、入力PDFドキュメントがPDF/A に準拠しているかどうかを指定する XML ドキュメントを返すように Assembler サービスに指示します。

**PDF/A 準拠の判断に使用するPDFドキュメントを参照します**

PDFドキュメントがPDF/A に準拠しているかどうかを判断するには、PDFドキュメントを参照して Assembler サービスに渡す必要があります。

**実行時オプションを設定**

ジョブの実行中に Assembler サービスの動作を制御する実行時オプションを設定できます。 例えば、エラーが発生した場合にジョブの処理を続行するよう Assembler サービスに指示するオプションを設定できます。 設定できる実行時オプションについて詳しくは、 `AssemblerOptionSpec` のクラス参照 [AEM Forms API リファレンス](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**PDF文書に関する情報を取得**

Assembler サービスクライアントを作成し、DDX ドキュメントを参照し、インタラクティブPDFドキュメントを参照し、実行時オプションを設定したら、 `invokeDDX` 操作。 DDX ドキュメントに `DocumentInformation` 要素の場合、Assembler サービスは XML データを返します。PDFドキュメントは返されません。

**返された XML ドキュメントを保存**

Assembler サービスが返す XML ドキュメントは、入力PDFドキュメントがPDF/A に準拠しているかどうかを指定します。 例えば、入力PDFドキュメントがPDF/A に準拠していない場合、Assembler サービスは次の要素を含む XML ドキュメントを返します。

```as3
 <PDFAConformance isCompliant="false" compliance="PDF/A-1b" resultLevel="Detailed" ignoreUnusedResources="true" allowCertificationSignatures="true">
```

XML ドキュメントを XML ファイルとして保存し、ファイルを開いて結果を表示できるようにします。

**関連トピック**

[Java API を使用して、ドキュメントがPDF/A に準拠しているかどうかを判断する](/help/forms/developing/determining-whether-documents-pdf-a.md#determine-whether-a-document-is-pdf-a-compliant-using-the-java-api)

[Web サービス API を使用して、ドキュメントがPDF/A に準拠しているかどうかを確認します](/help/forms/developing/determining-whether-documents-pdf-a.md#determine-whether-a-document-is-pdf-a-compliant-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[プログラムによるPDF文書の作成](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Java API を使用して、ドキュメントがPDF/A に準拠しているかどうかを判断する {#determine-whether-a-document-is-pdf-a-compliant-using-the-java-api}

Assembler Service API(Java) を使用して、PDFドキュメントがPDF/A に準拠しているかどうかを判断します。

1. プロジェクトファイルを含めます。

   Java プロジェクトのクラスパスに、adobe-assembler-client.jar などのクライアント JAR ファイルを含めます。

1. Assembler クライアントをPDFします。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * の作成 `AssemblerServiceClient` オブジェクトのコンストラクタを使用し、 `ServiceClientFactory` オブジェクト。

1. 既存の DDX ドキュメントを参照します。

   * の作成 `java.io.FileInputStream` コンストラクターを使用して DDX ファイルの場所を指定する string 値を渡すことによって DDX ドキュメントを表すオブジェクト。 PDFドキュメントがPDF/A に準拠しているかどうかを判断するには、DDX ドキュメントに `PDFAValidation` 内に含まれる要素 `DocumentInformation` 要素。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. PDF/A の準拠を判断するために使用されるPDFドキュメントを参照します。

   * の作成 `java.io.FileInputStream` オブジェクトのコンストラクタを使用し、PDF/A の準拠性を判断するために使用されるPDFドキュメントの場所を渡すことによって、オブジェクトを取得します。
   * の作成 `com.adobe.idp.Document` オブジェクトのコンストラクタを使用し、 `java.io.FileInputStream` オブジェクトドキュメントを含むPDF。
   * の作成 `java.util.Map` オブジェクトを指定し、 `HashMap` コンストラクタ。
   * エントリを `java.util.Map` オブジェクトを呼び出す `put` メソッドを使用し、次の引数を渡す。

      * キー名を表す string 値です。 この値は、DDX ドキュメントで指定されたソース要素の値と一致する必要があります。 例えば、この節で紹介する DDX ドキュメント内のソース要素の値は Loan.pdf です。
      * A `com.adobe.idp.Document` 入力PDF・ドキュメントを格納するオブジェクト。

1. 実行時オプションを設定します。

   * の作成 `AssemblerOptionSpec` コンストラクタを使用して実行時オプションを格納するオブジェクト。
   * に属するメソッドを呼び出して、ビジネス要件を満たすように実行時オプションを設定する `AssemblerOptionSpec` オブジェクト。 例えば、エラーが発生したときにジョブの処理を続行するように Assembler サービスに指示するには、 `AssemblerOptionSpec` オブジェクトの `setFailOnError` メソッドとパス `false`.

1. PDF・ドキュメントに関する情報を取得します。

   を呼び出す `AssemblerServiceClient` オブジェクトの `invokeDDX` メソッドを使用して、以下の必須値を渡します。

   * A `com.adobe.idp.Document` 使用する DDX ドキュメントを表すオブジェクト
   * A `java.util.Map` PDF/A 準拠の判断に使用される入力PDFファイルを含むオブジェクト
   * A `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` 実行時オプションを指定するオブジェクト

   この `invokeDDX` メソッドは、 `com.adobe.livecycle.assembler.client.AssemblerResult` 入力データドキュメントがPDF/A に準拠しているかどうかを指定する XMLPDFを含むオブジェクト。

1. 返された XML ドキュメントを保存します。

   入力PDFドキュメントがPDF/A ドキュメントであるかどうかを指定する XML データを取得するには、次の操作を実行します。

   * を呼び出す `AssemblerResult` オブジェクトの `getDocuments` メソッド。 これにより、 `java.util.Map` オブジェクト。
   * 反復処理 `java.util.Map` 結果が見つかるまでオブジェクトを閉じます。 `com.adobe.idp.Document` オブジェクト。
   * を呼び出す `com.adobe.idp.Document` オブジェクトの `copyToFile` メソッドを使用して XML ドキュメントを抽出します。 XML データは XML ファイルとして保存してください。

**関連トピック**

[クイックスタート（SOAP モード）:Java API を使用したドキュメントのPDF/A 準拠の確認](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-determining-whether-a-document-is-pdf-a-compliant-using-the-java-api) （SOAP モード）

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Web サービス API を使用して、ドキュメントがPDF/A に準拠しているかどうかを確認します {#determine-whether-a-document-is-pdf-a-compliant-using-the-web-service-api}

Assembler Service API（Web サービス）を使用して、PDFドキュメントがPDF/A に準拠しているかどうかを判断します。

1. プロジェクトファイルを含めます。

   MTOM を使用するMicrosoft .NET プロジェクトを作成します。 次の WSDL 定義を使用していることを確認します。 `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >置換 `localhost` を、AEM Formsをホストするサーバーの IP アドレスに設定します。

1. Assembler クライアントをPDFします。

   * の作成 `AssemblerServiceClient` オブジェクトのデフォルトのコンストラクタを使用します。
   * の作成 `AssemblerServiceClient.Endpoint.Address` オブジェクトを `System.ServiceModel.EndpointAddress` コンストラクタ。 WSDL をAEM Formsサービスに渡す文字列値 ( 例： `http://localhost:8080/soap/services/AssemblerService?blob=mtom`) をクリックします。 を使用する必要はありません。 `lc_version` 属性。 この属性は、サービス参照を作成する際に使用されます )。
   * の作成 `System.ServiceModel.BasicHttpBinding` オブジェクトを作成するには、 `AssemblerServiceClient.Endpoint.Binding` フィールドに入力します。 戻り値を `BasicHttpBinding` にキャストします。
   * を `System.ServiceModel.BasicHttpBinding` オブジェクトの `MessageEncoding` ～に向かって `WSMessageEncoding.Mtom`. この値は、MTOM が確実に使用されるようにします。
   * 次のタスクを実行して、基本的な HTTP 認証を有効にします。

      * フィールドにAEM forms ユーザー名を割り当てます。 `AssemblerServiceClient.ClientCredentials.UserName.UserName`.
      * 対応するパスワード値をフィールドに割り当てます。 `AssemblerServiceClient.ClientCredentials.UserName.Password`.
      * 定数値を割り当て `HttpClientCredentialType.Basic` フィールドに `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 定数値を割り当て `BasicHttpSecurityMode.TransportCredentialOnly` フィールドに `BasicHttpBindingSecurity.Security.Mode`.

1. 既存の DDX ドキュメントを参照します。

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。この `BLOB` オブジェクトは、DDX ドキュメントを保存するために使用されます。
   * の作成 `System.IO.FileStream` オブジェクトを作成するには、コンストラクターを呼び出し、DDX ドキュメントのファイルの場所とファイルを開くモードを表す string 値を渡します。
   * コンテンツを格納するバイト配列を作成します。 `System.IO.FileStream` オブジェクト。 バイト配列のサイズは、 `System.IO.FileStream` オブジェクトの `Length` プロパティ。
   * を呼び出して、バイト配列にストリームデータを入力します。 `System.IO.FileStream` オブジェクトの `Read` メソッドを使用し、読み込むバイト配列、開始位置、ストリーム長を渡す。
   * 次の項目に `BLOB` オブジェクトを割り当てる `MTOM` フィールドにバイト配列の内容を入力します。

1. PDF/A の準拠を判断するために使用されるPDFドキュメントを参照します。

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。この `BLOB` オブジェクトは、入力PDF・ドキュメントを格納するために使用します。
   * の作成 `System.IO.FileStream` オブジェクトを指定します。
   * コンテンツを格納するバイト配列を作成します。 `System.IO.FileStream` オブジェクト。 バイト配列のサイズは、 `System.IO.FileStream` オブジェクトの `Length` プロパティ。
   * を呼び出して、バイト配列にストリームデータを入力します。 `System.IO.FileStream` オブジェクトの `Read` メソッドを使用し、読み込むバイト配列、開始位置、ストリーム長を渡す。
   * 次の項目に `BLOB` オブジェクトを割り当てる `MTOM` プロパティにバイト配列の内容を入力します。
   * の作成 `MyMapOf_xsd_string_To_xsd_anyType` オブジェクト。 このコレクションオブジェクトは、コレクションドキュメントのPDFに使用されます。
   * の作成 `MyMapOf_xsd_string_To_xsd_anyType_Item` オブジェクト。
   * キー名を表す string 値を `MyMapOf_xsd_string_To_xsd_anyType_Item` オブジェクトの `key` フィールドに入力します。 この値は、DDX ドキュメントで指定されたPDFソース要素の値と一致する必要があります。
   * を `BLOB` オブジェクトを指定し、PDFドキュメントを `MyMapOf_xsd_string_To_xsd_anyType_Item` オブジェクトの `value` フィールドに入力します。
   * を `MyMapOf_xsd_string_To_xsd_anyType_Item` オブジェクトを `MyMapOf_xsd_string_To_xsd_anyType` オブジェクト。 を呼び出す `MyMapOf_xsd_string_To_xsd_anyType` オブジェクト&#39; `Add` メソッドを使用して、 `MyMapOf_xsd_string_To_xsd_anyType` オブジェクト。

1. 実行時オプションを設定します。

   * の作成 `AssemblerOptionSpec` コンストラクタを使用して実行時オプションを格納するオブジェクト。
   * に属するデータメンバーに値を割り当てて、ビジネス要件を満たすようにランタイムオプションを設定する `AssemblerOptionSpec` オブジェクト。 例えば、エラーが発生した場合にジョブの処理を続行するように Assembler サービスに指示するには、 `false` から `AssemblerOptionSpec` オブジェクトの `failOnError` データメンバー。

1. PDF・ドキュメントに関する情報を取得します。

   を呼び出す `AssemblerServiceService` オブジェクトの `invoke` メソッドを使用して、次の値を渡します。

   * A `BLOB` DDX ドキュメントを表すオブジェクト。
   * この `MyMapOf_xsd_string_To_xsd_anyType` 入力PDF・ドキュメントを格納するオブジェクト。 キーはPDFソースファイルの名前と一致する必要があり、値は `BLOB` オブジェクトを返します。
   * An `AssemblerOptionSpec` 実行時オプションを指定するオブジェクト。

   この `invoke` メソッドは、 `AssemblerResult` 入力PDF・ドキュメントがPDF/A ドキュメントかどうかを指定する XML データを含むオブジェクト。

1. 返された XML ドキュメントを保存します。

   入力PDFドキュメントがPDF/A ドキュメントであるかどうかを指定する XML データを取得するには、次の操作を実行します。

   * 次にアクセス： `AssemblerResult` オブジェクトの `documents` フィールド ( `Map` 入力PDFドキュメントがPDF/A ドキュメントかどうかを指定する XML データを含むオブジェクト。
   * 反復処理 `Map` オブジェクトを使用して各結果ドキュメントを取得します。 次に、その配列メンバーの値を `BLOB`.
   * XML データを表すバイナリデータを、そのデータにアクセスして抽出します `BLOB` オブジェクトの `MTOM` フィールドに入力します。 このフィールドには、XML ファイルとして書き出すことができるバイトの配列が格納されます。

**関連トピック**

[MTOM を使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
