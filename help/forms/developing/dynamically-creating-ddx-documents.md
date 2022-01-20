---
title: DDX ドキュメントの動的な作成
seo-title: Dynamically Creating DDX Documents
description: Java API と Web Service API を使用して DDX ドキュメントを動的に作成します。 DDX ドキュメントを動的に作成すると、実行時に取得された DDX ドキュメント内の値を使用できます。
seo-description: Create a DDX document dynamically using the Java API and Web Service API. Dynamically creating a DDX document enables you to use values in the DDX document that are obtained during run-time.
uuid: b73e8069-6c9f-4517-a0ae-f3d503191d2d
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: operations
discoiquuid: 2ad227de-68a8-446f-8c4f-a33a6f95bec8
role: Developer
exl-id: 883b33c8-50b1-4df2-a762-02be67ce24f1
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '2149'
ht-degree: 4%

---

# DDX ドキュメントの動的な作成 {#dynamically-creating-ddx-documents}

Assembler 操作の実行に使用できる DDX ドキュメントを動的に作成できます。 DDX ドキュメントを動的に作成すると、実行時に取得された DDX ドキュメント内の値を使用できます。 DDX ドキュメントを動的に作成するには、使用しているプログラミング言語に属するクラスを使用します。 例えば、Java を使用してクライアントアプリケーションを開発する場合は、 `org.w3c.dom.*`パッケージ。 同様に、Microsoft .NET を使用している場合は、 `System.Xml` 名前空間。

DDX ドキュメントを Assembler サービスに渡す前に、XML を `org.w3c.dom.Document` インスタンスから `com.adobe.idp.Document` インスタンス。 Web サービスを使用している場合は、XML を作成するために使用されたデータ型から XML を変換します ( 例： `XmlDocument`) から `BLOB` インスタンス。

このディスカッションでは、次の DDX ドキュメントが動的に作成されると仮定します。

```as3
 <?xml version="1.0" encoding="UTF-8"?> 
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/"> 
      <PDFsFromBookmarks prefix="stmt"> 
     <PDF source="AssemblerResultPDF.pdf"/> 
 </PDFsFromBookmarks> 
 </DDX>
```

この DDX ドキュメントは、PDFドキュメントを分解します。 PDF・ドキュメントの分解に関する知識を身に付けることをお勧めします。

>[!NOTE]
>
>Assembler サービスについて詳しくは、 [AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>DDX ドキュメントについて詳しくは、 [Assembler サービスと DDX リファレンス](https://www.adobe.com/go/learn_aemforms_ddx_63).

## 手順の概要 {#summary-of-steps}

動的に作成された DDX ドキュメントを使用してPDFドキュメントをディスアセンブルするには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. Assembler クライアントをPDFします。
1. DDX ドキュメントを作成します。
1. DDX ドキュメントを変換します。
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

**Assembler クライアントのPDF**

Assembler 操作をプログラムで実行する前に、Assembler サービスクライアントを作成します。

**DDX ドキュメントの作成**

使用しているプログラミング言語を使用して DDX ドキュメントを作成します。 PDFドキュメントを分解する DDX ドキュメントを作成するには、ドキュメントに `PDFsFromBookmarks` 要素。 DDX ドキュメントの作成に使用するデータタイプをに変換 `com.adobe.idp.Document` インスタンスを使用します（Java API を使用する場合）。 Web サービスを使用している場合は、データ型を `BLOB` インスタンス。

**DDX ドキュメントの変換**

を使用して作成された DDX ドキュメント `org.w3c.dom` クラスは、 `com.adobe.idp.Document` オブジェクト。 Java API を使用する際にこのタスクを実行するには、Java XML 変換クラスを使用します。 Web サービスを使用している場合は、DDX ドキュメントを `BLOB` オブジェクト。

**ディスアセンブリするPDFドキュメントの参照**

PDF文書を分解するには、分解するPDF文書を表すPDFファイルを参照します。 Assembler サービスに渡されると、ドキュメント内のレベル 1 のブックマークごとに個別のPDFドキュメントが返されます。

**実行時オプションを設定**

ジョブの実行中に Assembler サービスの動作を制御する実行時オプションを設定できます。 例えば、エラーが発生した場合にジョブの処理を続行するよう Assembler サービスに指示するオプションを設定できます。 実行時オプションを設定するには、 `AssemblerOptionSpec` オブジェクト。

**PDF文書の分解**

を呼び出してPDFドキュメントを分解する `invokeDDX` 操作。 動的に作成された DDX ドキュメントを渡します。 Assembler サービスは、コレクションオブジェクト内の分解されたPDFドキュメントを返します。

**分解したPDF文書を保存**

分解されたすべてのPDF・ドキュメントは、コレクション・オブジェクト内で返されます。 コレクションオブジェクトを繰り返し処理し、各PDFドキュメントをPDFファイルとして保存します。

**関連トピック**

[Java API を使用した DDX ドキュメントの動的な作成](/help/forms/developing/dynamically-creating-ddx-documents.md#dynamically-create-a-ddx-document-using-the-java-api)

[Web サービス API を使用した DDX ドキュメントの動的な作成](/help/forms/developing/dynamically-creating-ddx-documents.md#dynamically-create-a-ddx-document-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[プログラムによるPDFドキュメントの分解](/help/forms/developing/programmatically-disassembling-pdf-documents.md#programmatically-disassembling-pdf-documents)

## Java API を使用した DDX ドキュメントの動的な作成 {#dynamically-create-a-ddx-document-using-the-java-api}

Assembler Service API(Java) を使用して、DDX ドキュメントを動的に作成し、PDFドキュメントをディスアセンブルします。

1. プロジェクトファイルを含めます。

   Java プロジェクトのクラスパスに、adobe-assembler-client.jar などのクライアント JAR ファイルを含めます。

1. Assembler クライアントをPDFします。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * の作成 `AssemblerServiceClient` オブジェクトのコンストラクタを使用し、 `ServiceClientFactory` オブジェクト。

1. DDX ドキュメントを作成します。

   * Java の作成 `DocumentBuilderFactory` オブジェクトを `DocumentBuilderFactory` クラス&#39; `newInstance` メソッド。
   * Java の作成 `DocumentBuilder` オブジェクトを `DocumentBuilderFactory` オブジェクトの `newDocumentBuilder` メソッド。
   * を `DocumentBuilder` オブジェクトの `newDocument` メソッドを使用して `org.w3c.dom.Document` オブジェクト。
   * を呼び出して、DDX ドキュメントのルート要素を作成します。 `org.w3c.dom.Document` オブジェクトの `createElement` メソッド。 このメソッドは、 `Element` ルート要素を表すオブジェクト。 要素名を表す文字列値を `createElement` メソッド。 戻り値を `Element` にキャストします。次に、 `setAttribute` メソッド。 最後に、ヘッダー要素の `appendChild` メソッドを使用し、子要素オブジェクトを引数として渡します。 次のコード行は、このアプリケーションロジックを示しています。
      ` Element root = (Element)document.createElement("DDX");  root.setAttribute("xmlns","https://ns.adobe.com/DDX/1.0/");  document.appendChild(root);`

   * を作成します。 `PDFsFromBookmarks` 要素を `Document` オブジェクトの `createElement` メソッド。 要素名を表す文字列値を `createElement` メソッド。 戻り値を `Element` にキャストします。の値を設定 `PDFsFromBookmarks` 要素を `setAttribute` メソッド。 を追加します。 `PDFsFromBookmarks` 要素を `DDX` 要素内で DDX 要素の `appendChild` メソッド。 パス `PDFsFromBookmarks` element オブジェクトを引数として指定します。 次のコード行は、このアプリケーションロジックを示しています。

      ` Element PDFsFromBookmarks = (Element)document.createElement("PDFsFromBookmarks");  PDFsFromBookmarks.setAttribute("prefix","stmt");  root.appendChild(PDFsFromBookmarks);`

   * の作成 `PDF` 要素を `Document` オブジェクトの `createElement` メソッド。 要素名を表す string 値を渡します。 戻り値を `Element` にキャストします。の値を設定 `PDF` 要素を `setAttribute` メソッド。 を追加します。 `PDF` 要素を `PDFsFromBookmarks` 要素を `PDFsFromBookmarks` 要素の `appendChild` メソッド。 パス `PDF` element オブジェクトを引数として指定します。 次のコード行は、このアプリケーションロジックを示しています。

      ` Element PDF = (Element)document.createElement("PDF");  PDF.setAttribute("source","AssemblerResultPDF.pdf");  PDFsFromBookmarks.appendChild(PDF);`

1. DDX ドキュメントを変換します。

   * の作成 `javax.xml.transform.Transformer` を呼び出すことによってオブジェクトを取得 `javax.xml.transform.Transformer` オブジェクトの静的 `newInstance` メソッド。
   * の作成 `Transformer` を呼び出すことによってオブジェクトを取得 `TransformerFactory` オブジェクトの `newTransformer` メソッド。
   * コンストラクタを使用して `ByteArrayOutputStream` オブジェクトを作成します。
   * コンストラクタを使用して `javax.xml.transform.dom.DOMSource` オブジェクトを作成します。パス `org.w3c.dom.Document` DDX ドキュメントを表すオブジェクト。
   * コンストラクタを使用して `javax.xml.transform.dom.DOMSource` オブジェクトを渡すことによって、`ByteArrayOutputStream` オブジェクトを作成します。
   * Java の設定 `ByteArrayOutputStream` を呼び出すことによってオブジェクトを取得 `javax.xml.transform.Transformer` オブジェクトの `transform` メソッド。 パス `javax.xml.transform.dom.DOMSource` そして `javax.xml.transform.stream.StreamResult` オブジェクト。
   * バイト配列を作成し、 `ByteArrayOutputStream` オブジェクトをバイト配列に変換します。
   * を呼び出してバイト配列を生成します。 `ByteArrayOutputStream` オブジェクトの `toByteArray` メソッド。
   * の作成 `com.adobe.idp.Document` オブジェクトの値を指定します。

1. ディスアセンブリするPDFドキュメントを参照します。

   * の作成 `java.util.Map` オブジェクトを使用して入力PDFドキュメントを格納する `HashMap` コンストラクタ。
   * の作成 `java.io.FileInputStream` オブジェクトのコンストラクタを使用し、ディスアセンブリするPDFドキュメントの場所を渡す。
   * の作成 `com.adobe.idp.Document` オブジェクト。 パス `java.io.FileInputStream` ディスアセンブリするPDFドキュメントを含むオブジェクト。
   * エントリを `java.util.Map` オブジェクトを呼び出す `put` メソッドを使用し、次の引数を渡す。

      * キー名を表す string 値です。 この値は、DDX ドキュメントで指定されたPDFソース要素の値と一致する必要があります。 ( 動的に作成される DDX ドキュメントでは、値は `AssemblerResultPDF.pdf`.)
      * A `com.adobe.idp.Document` ディスアセンブリするPDFドキュメントを含むオブジェクト。

1. 実行時オプションを設定します。

   * の作成 `AssemblerOptionSpec` コンストラクタを使用して実行時オプションを格納するオブジェクト。
   * に属するメソッドを呼び出して、ビジネス要件を満たすように実行時オプションを設定する `AssemblerOptionSpec` オブジェクト。 例えば、エラーが発生したときにジョブの処理を続行するように Assembler サービスに指示するには、 `AssemblerOptionSpec` オブジェクトの `setFailOnError` メソッドとパス `false`.

1. PDF文書の分解

   を呼び出す `AssemblerServiceClient` オブジェクトの `invokeDDX` メソッドを使用して、次の値を渡します。

   * A `com.adobe.idp.Document` 動的に作成された DDX ドキュメントを表すオブジェクト
   * A `java.util.Map` 分解するPDF・ドキュメントを含むオブジェクト
   * A `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` デフォルトのフォントやジョブログレベルを含む、実行時のオプションを指定するオブジェクト

   この `invokeDDX` メソッドは、 `com.adobe.livecycle.assembler.client.AssemblerResult` 分解されたPDF文書と発生した例外を含むオブジェクト。

1. 分解したPDF文書を保存します。

   分解されたPDF・ドキュメントを取得するには、次の操作を実行します。

   * を呼び出す `AssemblerResult` オブジェクトの `getDocuments` メソッド。 このメソッドは、 `java.util.Map` オブジェクト。
   * 反復処理 `java.util.Map` 結果が見つかるまでオブジェクトを閉じます。 `com.adobe.idp.Document` オブジェクト。
   * を呼び出す `com.adobe.idp.Document` オブジェクトの `copyToFile` メソッドを使用して、PDFドキュメントを抽出します。

**関連トピック**

[クイックスタート（SOAP モード）:Java API を使用した DDX ドキュメントの動的な作成](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-dynamically-creating-a-ddx-document-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Web サービス API を使用した DDX ドキュメントの動的な作成 {#dynamically-create-a-ddx-document-using-the-web-service-api}

Assembler Service API（Web サービス）を使用して、DDX ドキュメントを動的に作成し、PDFドキュメントをディスアセンブルします。

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

1. DDX ドキュメントを作成します。

   * コンストラクタを使用して `System.Xml.XmlElement` オブジェクトを作成します。
   * を呼び出して、DDX ドキュメントのルート要素を作成します。 `XmlElement` オブジェクトの `CreateElement` メソッド。 このメソッドは、 `Element` ルート要素を表すオブジェクト。 要素名を表す文字列値を `CreateElement` メソッド。 DDX 要素の値を設定するには、 `SetAttribute` メソッド。 最後に、 `XmlElement` オブジェクトの `AppendChild` メソッド。 DDX オブジェクトを引数として渡します。 次のコード行は、このアプリケーションロジックを示しています。

      ` System.Xml.XmlElement root = ddx.CreateElement("DDX");  root.SetAttribute("xmlns", "https://ns.adobe.com/DDX/1.0/");  ddx.AppendChild(root);`

   * DDX ドキュメントの作成 `PDFsFromBookmarks` 要素を `XmlElement` オブジェクトの `CreateElement` メソッド。 要素名を表す文字列値を `CreateElement` メソッド。 次に、 `SetAttribute` メソッド。 を追加します。 `PDFsFromBookmarks` 要素をルート要素に追加するには、 `DDX` 要素の `AppendChild` メソッド。 パス `PDFsFromBookmarks` element オブジェクトを引数として指定します。 次のコード行は、このアプリケーションロジックを示しています。

      ` XmlElement PDFsFromBookmarks = ddx.CreateElement("PDFsFromBookmarks");  PDFsFromBookmarks.SetAttribute("prefix", "stmt");  root.AppendChild(PDFsFromBookmarks);`

   * DDX ドキュメントの作成 `PDF` 要素を `XmlElement` オブジェクトの `CreateElement` メソッド。 要素名を表す文字列値を `CreateElement` メソッド。 次に、 `SetAttribute` メソッド。 を追加します。 `PDF` 要素を `PDFsFromBookmarks` 要素を `PDFsFromBookmarks` 要素の `AppendChild` メソッド。 パス `PDF` element オブジェクトを引数として指定します。 次のコード行は、このアプリケーションロジックを示しています。

      ` XmlElement PDF = ddx.CreateElement("PDF");  PDF.SetAttribute("source", "AssemblerResultPDF.pdf");  PDFsFromBookmarks.AppendChild(PDF);`

1. DDX ドキュメントを変換します。

   * コンストラクタを使用して `System.IO.MemoryStream` オブジェクトを作成します。
   * 次の項目に `MemoryStream` オブジェクトを `XmlElement` DDX ドキュメントを表すオブジェクト。 を呼び出す `XmlElement` オブジェクトの `Save` メソッドを使用して、 `MemoryStream` オブジェクト。
   * バイト配列を作成し、 `MemoryStream` オブジェクト。 次のコードは、このアプリケーションロジックを示しています。

      ` int bufLen = Convert.ToInt32(stream.Length);  byte[] byteArray = new byte[bufLen];  stream.Position = 0;  int count = stream.Read(byteArray, 0, bufLen);`

   * の作成 `BLOB` オブジェクト。 バイト配列を `BLOB` オブジェクトの `MTOM` フィールドに入力します。

1. ディスアセンブリするPDFドキュメントを参照します。

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。この `BLOB` オブジェクトは、入力PDF・ドキュメントを格納するために使用します。 この `BLOB` オブジェクトが `invokeOneDocument` を引数として。
   * の作成 `System.IO.FileStream` オブジェクトを指定します。 入力PDFドキュメントのファイルの場所と、ファイルを開くモードを表す string 値を渡します。
   * コンテンツを格納するバイト配列を作成します。 `System.IO.FileStream` オブジェクト。 バイト配列のサイズは、 `System.IO.FileStream` オブジェクトの `Length` プロパティ。
   * を呼び出して、バイト配列にストリームデータを入力します。 `System.IO.FileStream` オブジェクトの `Read` メソッドを使用し、読み込むバイト配列、開始位置、ストリーム長を渡す。
   * 次の項目に `BLOB` オブジェクトを割り当てる `MTOM` プロパティは、バイト配列の内容を示します。

1. 実行時オプションを設定します。

   * の作成 `AssemblerOptionSpec` コンストラクタを使用して実行時オプションを格納するオブジェクト。
   * に属するデータメンバーに値を割り当てて、ビジネス要件を満たすようにランタイムオプションを設定する `AssemblerOptionSpec` オブジェクト。 例えば、エラーが発生した場合にジョブの処理を続行するように Assembler サービスに指示するには、 `false` から `AssemblerOptionSpec` オブジェクトの `failOnError` データメンバー。

1. PDF文書の分解

   を呼び出す `AssemblerServiceClient` オブジェクトの `invokeDDX` メソッドを使用して、次の値を渡します。

   * A `BLOB` 動的に作成された DDX ドキュメントを表すオブジェクト
   * この `mapItem` 入力PDF文書を含む配列
   * An `AssemblerOptionSpec` 実行時のオプションを指定するオブジェクト

   この `invokeDDX` メソッドは、 `AssemblerResult` ジョブの結果と発生した例外を含むオブジェクト。

1. 分解したPDF文書を保存します。

   新しく作成したPDF・ドキュメントを取得するには、次の操作を実行します。

   * 次にアクセス： `AssemblerResult` オブジェクトの `documents` フィールド ( `Map` 分解されたPDF文書を含むオブジェクト。
   * 反復処理 `Map` オブジェクトを使用して各結果ドキュメントを取得します。 次に、その配列メンバの `value` から `BLOB`.
   * PDFドキュメントを表すバイナリデータを、そのドキュメントにアクセスして抽出します `BLOB` オブジェクトの `MTOM` プロパティ。 これは、バイトの配列を返し、PDF・ファイルに書き出すことができます。

**関連トピック**

[MTOM を使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRef を使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
