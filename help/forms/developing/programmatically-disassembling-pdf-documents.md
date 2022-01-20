---
title: プログラムによるPDFドキュメントの分解
seo-title: Programmatically Disassembling PDF Documents
description: Assembler サービスを使用すると、Java API と Web サービス API を使用して、1 つのPDFドキュメントを複数のPDFドキュメントに分解できます。
seo-description: Use the Assembler service to disassemble a single PDF document into multiple PDF documents using the Java API and the Web Service API.
uuid: d71cc044-e948-4b7a-b598-b041723b69e9
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: operations
discoiquuid: 8e38a597-5d22-4d83-95fe-4494fb04e4a3
role: Developer
exl-id: 3f757392-96a0-4f20-91d0-7fbccb1bf171
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '1747'
ht-degree: 3%

---

# プログラムによるPDFドキュメントの分解 {#programmatically-disassembling-pdf-documents}

Assembler サービスにPDFドキュメントを渡すことで、ドキュメントを分解できます。 通常、このタスクは、ステートメントの集まりなど、PDFドキュメントが多数の個々のドキュメントから最初に作成された場合に役立ちます。 次の図では、DocA は複数の結果ドキュメントに分割されています。ページの第 1 レベル 1 のブックマークで、新しい結果ドキュメントの開始が示されています。

![pd_pd_pdfsfrombookmarks](assets/pd_pd_pdfsfrombookmarks.png)

PDF・ドキュメントを分解するには、 `PDFsFromBookmarks` 要素は DDX ドキュメント内にあります。 この `PDFsFromBookmarks` 要素は結果の要素であり、の子要素のみにすることができます `DDX` 要素。 これには `result` 属性を設定する必要があります。

この `PDFsFromBookmarks` 要素を使用すると、ソースドキュメントのレベル 1 のブックマークごとに 1 つのドキュメントが生成されます。

この説明では、次の DDX ドキュメントが使用されているとします。

```as3
 <?xml version="1.0" encoding="UTF-8"?> 
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/"> 
      <PDFsFromBookmarks prefix="stmt"> 
     <PDF source="AssemblerResultPDF.pdf"/> 
 </PDFsFromBookmarks> 
 </DDX>
```

>[!NOTE]
>
>この節を読む前に、Assembler サービスを使用したPDFドキュメントの組み立てを理解しておくことをお勧めします。 ( [プログラムによるPDF文書の作成](/help/forms/developing/programmatically-assembling-pdf-documents.md).)

>[!NOTE]
>
>単一のPDFドキュメントを Assembler サービスに渡し、単一のドキュメントを取得する場合、 `invokeOneDocument` 操作。 ただし、PDFドキュメントを分解するには `invokeDDX` 操作の理由は、1 つの入力PDFドキュメントが Assembler サービスに渡されるのに対し、Assembler サービスは 1 つ以上のドキュメントを含むコレクションオブジェクトを返すからです。

>[!NOTE]
>
>Assembler サービスについて詳しくは、 [AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>DDX ドキュメントについて詳しくは、 [Assembler サービスと DDX リファレンス](https://www.adobe.com/go/learn_aemforms_ddx_63).

## 手順の概要 {#summary-of-steps}

PDF・ドキュメントを分解するには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. Assembler クライアントをPDFします。
1. 既存の DDX ドキュメントを参照します。
1. ディスアセンブリするPDFドキュメントを参照します。
1. 実行時オプションを設定します。
1. PDF文書の分解
1. 分解したPDF文書を保存します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。 Web サービスを使用している場合は、プロキシファイルを必ず含めてください。

次の JAR ファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar(AEM Formsを JBoss にデプロイする場合に必要 )
* jbossall-client.jar(AEM Formsが JBoss にデプロイされている場合に必要 )

JBoss 以外のサポート対象の J2EE アプリケーションサーバーにAEM Formsがデプロイされている場合は、adobe-utilities.jar と jbossall-client.jar を、AEM Formsがデプロイされている J2EE アプリケーションサーバーに固有の JAR ファイルに置き換える必要があります。

**Assembler クライアントのPDF**

Assembler 操作をプログラムで実行する前に、Assembler サービスクライアントを作成する必要があります。

**既存の DDX ドキュメントの参照**

DDX ドキュメントをディスアセンブリするには、DDX ドキュメントを参照する必要がありますPDFドキュメント。 この DDX ドキュメントには `PDFsFromBookmarks` 要素。

**ディスアセンブリするPDFドキュメントの参照**

PDF文書を分解するには、分解するPDF文書を表すPDFファイルを参照します。 Assembler サービスに渡されると、ドキュメント内のレベル 1 のブックマークごとに個別のPDFドキュメントが返されます。

**実行時オプションを設定**

ジョブの実行中に Assembler サービスの動作を制御する実行時オプションを設定できます。 例えば、エラーが発生した場合にジョブの処理を続行するよう Assembler サービスに指示するオプションを設定できます。

**PDF文書の分解**

Assembler サービスクライアントを作成し、DDX ドキュメントを参照し、PDFドキュメントを参照してアセンブルを解除し、実行時オプションを設定したら、次を呼び出すことで、PDFドキュメントをディスアセンブルできます。 `invokeDDX` メソッド。 DDX ドキュメントにPDFドキュメントの分解手順が含まれている場合、Assembler サービスはコレクションオブジェクト内の分解されたPDFドキュメントを返します。

**分解したPDF文書を保存**

分解されたすべてのPDF・ドキュメントは、コレクション・オブジェクト内で返されます。 コレクションオブジェクトを繰り返し処理し、各PDFドキュメントをPDFファイルとして保存します。

**関連トピック**

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[プログラムによるPDF文書の作成](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Java API を使用したPDFドキュメントのディスアセンブリ {#disassemble-a-pdf-document-using-the-java-api}

Assembler Service API(Java) を使用してPDFドキュメントを分解します。

1. プロジェクトファイルを含めます。

   Java プロジェクトのクラスパスに、adobe-assembler-client.jar などのクライアント JAR ファイルを含めます。

1. Assembler クライアントをPDFします。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * の作成 `AssemblerServiceClient` オブジェクトのコンストラクタを使用し、 `ServiceClientFactory` オブジェクト。

1. 既存の DDX ドキュメントを参照します。

   * の作成 `java.io.FileInputStream` コンストラクターを使用して DDX ファイルの場所を指定する string 値を渡すことによって DDX ドキュメントを表すオブジェクト。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. ディスアセンブリするPDFドキュメントを参照します。

   * の作成 `java.util.Map` オブジェクトを使用して入力PDFドキュメントを格納する `HashMap` コンストラクタ。
   * の作成 `java.io.FileInputStream` オブジェクトのコンストラクタを使用し、ディスアセンブリするPDFドキュメントの場所を渡す。
   * の作成 `com.adobe.idp.Document` オブジェクトを選択し、 `java.io.FileInputStream` ディスアセンブリするPDFドキュメントを含むオブジェクト。
   * エントリを `java.util.Map` オブジェクトを呼び出す `put` メソッドを使用し、次の引数を渡す。

      * キー名を表す string 値です。 この値は、DDX ドキュメントで指定されたPDFソース要素の値と一致する必要があります。
      * A `com.adobe.idp.Document` ディスアセンブリするPDFドキュメントを含むオブジェクト。

1. 実行時オプションを設定します。

   * の作成 `AssemblerOptionSpec` コンストラクタを使用して実行時オプションを格納するオブジェクト。
   * に属するメソッドを呼び出して、ビジネス要件を満たすように実行時オプションを設定する `AssemblerOptionSpec` オブジェクト。 例えば、エラーが発生したときにジョブの処理を続行するように Assembler サービスに指示するには、 `AssemblerOptionSpec` オブジェクトの `setFailOnError` メソッドとパス `false`.

1. PDF文書の分解

   を呼び出す `AssemblerServiceClient` オブジェクトの `invokeDDX` メソッドを使用して、以下の必須値を渡します。

   * A `com.adobe.idp.Document` 使用する DDX ドキュメントを表すオブジェクト
   * A `java.util.Map` 分解するPDF・ドキュメントを含むオブジェクト
   * A `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` デフォルトのフォントやジョブログレベルを含む、実行時のオプションを指定するオブジェクト

   この `invokeDDX` メソッドは、 `com.adobe.livecycle.assembler.client.AssemblerResult` 分解されたPDF文書と発生した例外を含むオブジェクト。

1. 分解したPDF文書を保存します。

   分解されたPDF・ドキュメントを取得するには、次の操作を実行します。

   * を呼び出す `AssemblerResult` オブジェクトの `getDocuments` メソッド。 これにより、 `java.util.Map` オブジェクト。
   * 反復処理 `java.util.Map` 結果が見つかるまでオブジェクトを閉じます。 `com.adobe.idp.Document` オブジェクト。
   * を呼び出す `com.adobe.idp.Document` オブジェクトの `copyToFile` メソッドを使用して、PDFドキュメントを抽出します。

**関連トピック**

[プログラムによるPDFドキュメントの分解](#programmatically-disassembling-pdf-documents)

[クイックスタート（SOAP モード）:Java API を使用したPDFドキュメントの分解](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-disassembling-a-pdf-document-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Web サービス API を使用したPDFドキュメントのディスアセンブリ {#disassemble-a-pdf-document-using-the-web-service-api}

Assembler Service API（Web サービス）を使用してPDFドキュメントを分解します。

1. プロジェクトファイルを含めます。

   MTOM を使用するMicrosoft .NET プロジェクトを作成します。 サービス参照を設定する際は、次の WSDL 定義を必ず使用してください。 `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >置換 `localhost` を、AEM Formsをホストするサーバーの IP アドレスに設定します。

1. Assembler クライアントをPDFします。

   * の作成 `AssemblerServiceClient` オブジェクトのデフォルトのコンストラクタを使用します。
   * の作成 `AssemblerServiceClient.Endpoint.Address` オブジェクトを `System.ServiceModel.EndpointAddress` コンストラクタ。 WSDL をAEM Formsサービスに渡す文字列値 ( 例： `http://localhost:8080/soap/services/AssemblerService?blob=mtom`) をクリックします。 を使用する必要はありません。 `lc_version` 属性。 この属性は、サービス参照を作成する際に使用されます。
   * の作成 `System.ServiceModel.BasicHttpBinding` オブジェクトを作成するには、 `AssemblerServiceClient.Endpoint.Binding` フィールドに入力します。 戻り値を `BasicHttpBinding` にキャストします。
   * を `System.ServiceModel.BasicHttpBinding` オブジェクトの `MessageEncoding` ～に向かって `WSMessageEncoding.Mtom`. この値は、MTOM が確実に使用されるようにします。
   * 次のタスクを実行して、基本的な HTTP 認証を有効にします。

      * フィールドにAEM forms ユーザー名を割り当てます。 `AssemblerServiceClient.ClientCredentials.UserName.UserName`.
      * 対応するパスワード値をフィールドに割り当てます。 `AssemblerServiceClient.ClientCredentials.UserName.Password`.
      * 定数値を割り当て `HttpClientCredentialType.Basic` フィールドに `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 定数値を割り当て `BasicHttpSecurityMode.TransportCredentialOnly` フィールドに `BasicHttpBindingSecurity.Security.Mode`.

1. 既存の DDX ドキュメントを参照します。

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。この `BLOB` オブジェクトは、DDX ドキュメントを保存するために使用されます。
   * の作成 `System.IO.FileStream` オブジェクトを指定します。 DDX ドキュメントのファイルの場所と、ファイルを開くモードを表す string 値を渡します。
   * コンテンツを格納するバイト配列を作成します。 `System.IO.FileStream` オブジェクト。 バイト配列のサイズは、 `System.IO.FileStream` オブジェクトの `Length` プロパティ。
   * を呼び出して、バイト配列にストリームデータを入力します。 `System.IO.FileStream` オブジェクトの `Read` メソッドを使用し、読み込むバイト配列、開始位置、ストリーム長を渡す。
   * 次の項目に `BLOB` オブジェクトを割り当てる `MTOM` プロパティにバイト配列の内容を入力します。

1. ディスアセンブリするPDFドキュメントを参照します。

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。この `BLOB` オブジェクトは、入力PDF・ドキュメントを格納するために使用します。 この `BLOB` オブジェクトが `invokeOneDocument` を引数として。
   * の作成 `System.IO.FileStream` オブジェクトを指定します。
   * コンテンツを格納するバイト配列を作成します。 `System.IO.FileStream` オブジェクト。 バイト配列のサイズは、 `System.IO.FileStream` オブジェクトの `Length` プロパティ。
   * を呼び出して、バイト配列にストリームデータを入力します。 `System.IO.FileStream` オブジェクトの `Read` メソッドを使用し、読み込むバイト配列、開始位置、ストリーム長を渡す。
   * 次の項目に `BLOB` オブジェクトを割り当てる `MTOM` フィールドはバイト配列の内容です。
   * の作成 `MyMapOf_xsd_string_To_xsd_anyType` オブジェクト。 このコレクションオブジェクトは、ディスアセンブリするPDFを保存するために使用されます。
   * の作成 `MyMapOf_xsd_string_To_xsd_anyType_Item` オブジェクト。
   * キー名を表す string 値を `MyMapOf_xsd_string_To_xsd_anyType_Item` オブジェクトの `key` フィールドに入力します。 この値は、DDX ドキュメントで指定されたPDFソース要素の値と一致する必要があります。
   * を `BLOB` オブジェクトを指定し、PDFドキュメントを `MyMapOf_xsd_string_To_xsd_anyType_Item` オブジェクトの `value` フィールドに入力します。
   * を `MyMapOf_xsd_string_To_xsd_anyType_Item` オブジェクトを `MyMapOf_xsd_string_To_xsd_anyType` オブジェクト。 を呼び出す `MyMapOf_xsd_string_To_xsd_anyType` オブジェクト&#39; `Add` メソッドを使用して、 `MyMapOf_xsd_string_To_xsd_anyType` オブジェクト。

1. 実行時オプションを設定します。

   * の作成 `AssemblerOptionSpec` コンストラクタを使用して実行時オプションを格納するオブジェクト。
   * に属するデータメンバーに値を割り当てて、ビジネス要件を満たすようにランタイムオプションを設定する `AssemblerOptionSpec` オブジェクト。 例えば、エラーが発生した場合にジョブの処理を続行するように Assembler サービスに指示するには、 `false` から `AssemblerOptionSpec` オブジェクトの `failOnError` フィールドに入力します。

1. PDF文書の分解

   を呼び出す `AssemblerServiceClient` オブジェクトの `invokeDDX` メソッドを使用して、次の値を渡します。

   * A `BLOB` オブジェクトドキュメントを分解する DDX ドキュメントを表すPDF
   * この `MyMapOf_xsd_string_To_xsd_anyType` 分解するPDF・ドキュメントを含むオブジェクト
   * An `AssemblerOptionSpec` 実行時のオプションを指定するオブジェクト

   この `invokeDDX` メソッドは、 `AssemblerResult` ジョブの結果と発生した例外を含むオブジェクト。

1. 分解したPDF文書を保存します。

   新しく作成したPDF・ドキュメントを取得するには、次の操作を実行します。

   * 次にアクセス： `AssemblerResult` オブジェクトの `documents` フィールド ( `Map` 分解されたPDF文書を含むオブジェクト。
   * 反復処理 `Map` オブジェクトを使用して各結果ドキュメントを取得します。 次に、その配列メンバの `value` から `BLOB`.
   * PDFドキュメントを表すバイナリデータを、そのドキュメントにアクセスして抽出します `BLOB` オブジェクトの `MTOM` プロパティ。 これは、バイトの配列を返し、PDF・ファイルに書き出すことができます。

**関連トピック**

[プログラムによるPDFドキュメントの分解](#programmatically-disassembling-pdf-documents)

[MTOM を使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
