---
title: プログラムによるPDF文書の作成
seo-title: Programmatically Assembling PDF Documents
description: Assembler サービス API を使用して、Java API と Web サービス API を使用して、複数のPDFドキュメントを 1 つのPDFドキュメントにアセンブリします。
seo-description: Use the Assembler service API to assemble multiple PDF documents into a single PDF document using the Java API and the Web Service API.
uuid: aa3f8f39-1fbc-48d0-82ff-6caaadf125fc
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: operations
discoiquuid: ebe8136b-2a79-4035-b9d5-aa70a5bbd4af
role: Developer
exl-id: be09271b-3004-4866-b43b-fb03c91305ec
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '2110'
ht-degree: 2%

---

# プログラムによるPDF文書の作成 {#programmatically-assembling-pdf-documents}

Assembler サービス API を使用して、複数のPDFドキュメントを 1 つのPDFドキュメントに組み合わせます。 次の図は、3 つのPDFドキュメントを 1 つのPDFドキュメントに結合する様子を示しています。

![pa_pa_document_assembly](assets/pa_pa_document_assembly.png)

2 つ以上のPDFドキュメントを 1 つのPDFドキュメントにアセンブリするには、DDX ドキュメントが必要です。 DDX ドキュメントは、Assembler サービスが生成するPDFドキュメントを記述します。 つまり、DDX ドキュメントは Assembler サービスに対して、実行するアクションを指示します。

この説明では、次の DDX ドキュメントが使用されていると仮定します。

```as3
 <?xml version="1.0" encoding="UTF-8"?> 
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/"> 
     <PDF result="out.pdf"> 
         <PDF source="map.pdf" /> 
         <PDF source="directions.pdf" /> 
     </PDF> 
 </DDX>
```

この DDX ドキュメントは、名前が付いた 2 つのPDFドキュメントを結合します *map.pdf* および *directions.pdf* を単一のPDF文書に

>[!NOTE]
>
>PDFドキュメントを分解する DDX ドキュメントを確認するには、 [プログラムによるPDFドキュメントの分解](/help/forms/developing/programmatically-disassembling-pdf-documents.md#programmatically-disassembling-pdf-documents).

>[!NOTE]
>
>Assembler サービスについて詳しくは、 [AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>DDX ドキュメントについて詳しくは、 [Assembler サービスと DDX リファレンス](https://www.adobe.com/go/learn_aemforms_ddx_63).

## Web サービスを使用して Assembler サービスを呼び出す際の考慮事項 {#considerations-when-invoking-assembler-service-using-web-services}

大きなドキュメントのアセンブリ中にヘッダーとフッターを追加すると、 `OutOfMemory` エラーが発生し、ファイルがアセンブルされません。 この問題が発生する可能性を減らすには、 `DDXProcessorSetting` 要素を DDX ドキュメントに追加します（以下の例を参照）。

`<DDXProcessorSetting name="checkpoint" value="2000" />`

この要素を `DDX` 要素またはの子として `PDF result` 要素。 この設定のデフォルト値は 0 （ゼロ）で、チェックポイントをオフにし、DDX は `DDXProcessorSetting` 要素が存在しません。 もし `OutOfMemory` エラーが発生した場合は、値を整数（通常は 500 ～ 5000）に設定する必要がある場合があります。 チェックポイントの値が小さいと、チェックポイントが頻繁に行われます。

## 手順の概要 {#summary-of-steps}

複数のPDF・ドキュメントから 1 つのPDF・ドキュメントをアセンブリするには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. Assembler クライアントをPDFします。
1. 既存の DDX ドキュメントを参照します。
1. 参照入力PDF文書。
1. 実行時オプションを設定します。
1. 入力アセンブリドキュメントをPDFします。
1. 結果を抽出します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。 Web サービスを使用している場合は、プロキシファイルを必ず含めてください。

次の JAR ファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar(AEM Formsを JBoss にデプロイする場合に必要 )
* jbossall-client.jar(AEM Formsが JBoss にデプロイされている場合に必要 )

AEM Formsが JBoss 以外のサポート対象の J2EE アプリケーションサーバーにデプロイされている場合は、adobe-utilities.jar ファイルと jbossall-client.jar ファイルを、AEM Formsがデプロイされている J2EE アプリケーションサーバーに固有の JAR ファイルに置き換える必要があります。

**Assembler クライアントのPDF**

Assembler 操作をプログラムで実行する前に、Assembler クライアントを作成する必要があります。

**既存の DDX ドキュメントの参照**

DDX ドキュメントを参照して、アセンブリドキュメントをPDFする必要があります。 例えば、この節で紹介した DDX ドキュメントについて考えてみましょう。 この DDX ドキュメントは、2 つのPDFドキュメントを 1 つのマージドキュメントに結合するよう Assembler サービスにPDFします。

**参照入力PDFドキュメント**

Assembler サービスに渡す入力PDFドキュメントを参照します。 たとえば、Map と Directions という名前の 2 つの入力PDFドキュメントを渡す場合は、対応するPDFファイルを渡す必要があります。

map.pdf ファイルと dorictions.pdf ファイルの両方をコレクションオブジェクトに配置する必要があります。 キーの名前は、DDX ドキュメントのPDFソース属性の値と一致する必要があります。 DDX ドキュメント内のキーと source 属性が一致する場合、PDFファイルの名前は関係ありません。

>[!NOTE]
>
>An `*AssemblerResult*` コレクションオブジェクトを含むオブジェクトは、 `*invokeDDX*` 操作。 この操作は、2 つ以上の入力PDFドキュメントを Assembler サービスに渡す場合に使用されます。 ただし、Assembler サービスに 1 つの入力PDFのみを渡し、1 つの戻り文書のみを渡す場合は、 `*invokeOneDocument*` 操作。 この操作を呼び出すと、1 つのドキュメントが返されます。 この操作の使用方法については、 [暗号化されたPDF文書の作成](/help/forms/developing/assembling-encrypted-pdf-documents.md#assembling-encrypted-pdf-documents).

**実行時オプションを設定**

ジョブの実行中に Assembler サービスの動作を制御する実行時オプションを設定できます。 例えば、エラーが発生した場合にジョブの処理を続行するよう Assembler サービスに指示するオプションを設定できます。 設定できる実行時オプションについて詳しくは、 `AssemblerOptionSpec` のクラス参照 [AEM Forms API リファレンス](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**入力アセンブリドキュメントのPDF**

サービスクライアントを作成し、DDX ファイルを参照し、入力PDFドキュメントを格納するコレクションオブジェクトを作成して、実行時オプションを設定したら、DDX 操作を呼び出すことができます。 この節で指定した DDX ドキュメントを使用する場合、 map.pdf ファイルと direction.pdf ファイルが 1 つのPDFドキュメントに結合されます。

**結果を抽出**

Assembler サービスが `java.util.Map` オブジェクト。 `AssemblerResult` オブジェクト、および操作結果を含む 返された `java.util.Map` オブジェクトには、結果のドキュメントと例外が含まれます。

次の表は、返される `java.util.Map` オブジェクト。

<table> 
 <thead> 
  <tr> 
   <th><p>キー値</p></th> 
   <th><p>オブジェクトタイプ</p></th> 
   <th><p>説明</p></th> 
  </tr> 
 </thead> 
 <tbody>
  <tr> 
   <td><p><code><i>documentName</i></code></p></td> 
   <td><p><code>com.adobe.idp.Document</code></p></td> 
   <td><p>DDX 結果要素で指定された結果のドキュメントを含めます</p></td> 
  </tr> 
  <tr> 
   <td><p><code><i>documentName</i></code></p></td> 
   <td><p><code>Exception</code></p></td> 
   <td><p>ドキュメントの例外を含みます</p></td> 
  </tr> 
  <tr> 
   <td><p><code>OutputMapConstants.LOG_NAME</code></p></td> 
   <td><p><code>com.adobe.idp.Documen</code></p></td> 
   <td><p>ジョブログを含む</p></td> 
  </tr> 
 </tbody> 
</table>

**関連トピック**

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[プログラムによるPDFドキュメントの分解](/help/forms/developing/programmatically-disassembling-pdf-documents.md#programmatically-disassembling-pdf-documents)

## Java API を使用したPDFドキュメントのアセンブリ {#assemble-pdf-documents-using-the-java-api}

Assembler Service API(Java) を使用してPDFドキュメントをアセンブリします。

1. プロジェクトファイルを含めます。

   Java プロジェクトのクラスパスに、adobe-assembler-client.jar などのクライアント JAR ファイルを含めます。

1. Assembler クライアントをPDFします。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * の作成 `AssemblerServiceClient` オブジェクトのコンストラクタを使用し、 `ServiceClientFactory` オブジェクト。

1. 既存の DDX ドキュメントを参照します。

   * の作成 `java.io.FileInputStream` コンストラクターを使用して DDX ファイルの場所を指定する string 値を渡すことによって DDX ドキュメントを表すオブジェクト。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. 参照入力PDF文書。

   * の作成 `java.util.Map` オブジェクトを使用して入力PDFドキュメントを格納する `HashMap` コンストラクタ。
   * 入力PDFドキュメントごとに、 `java.io.FileInputStream` オブジェクトのコンストラクタを使用し、入力PDF・ドキュメントの場所を渡す。
   * 入力PDFドキュメントごとに、 `com.adobe.idp.Document` オブジェクトを選択し、 `java.io.FileInputStream` オブジェクトドキュメントを含むPDF。
   * 入力ドキュメントごとに、 `java.util.Map` オブジェクトを呼び出す `put` メソッドを使用し、次の引数を渡す。

      * キー名を表す string 値です。 この値は、DDX ドキュメントで指定されたPDFソース要素の値と一致する必要があります。
      * A `com.adobe.idp.Document` オブジェクト ( または `java.util.List` ソースドキュメントドキュメントを含む、複数のドキュメントを指定するPDF)。

1. 実行時オプションを設定します。

   * の作成 `AssemblerOptionSpec` コンストラクタを使用して実行時オプションを格納するオブジェクト。
   * に属するメソッドを呼び出して、ビジネス要件を満たすように実行時オプションを設定する `AssemblerOptionSpec` オブジェクト。 例えば、エラーが発生したときにジョブの処理を続行するように Assembler サービスに指示するには、 `AssemblerOptionSpec` オブジェクトの `setFailOnError` メソッドとパス `false`.

1. 入力アセンブリドキュメントをPDFします。

   を呼び出す `AssemblerServiceClient` オブジェクトの `invokeDDX` メソッドを使用して、以下の必須値を渡します。

   * A `com.adobe.idp.Document` 使用する DDX ドキュメントを表すオブジェクト
   * A `java.util.Map` アセンブリ対象の入力PDF・ファイルを含むオブジェクト
   * A `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` デフォルトのフォントやジョブログレベルを含む、実行時のオプションを指定するオブジェクト

   この `invokeDDX` メソッドは、 `com.adobe.livecycle.assembler.client.AssemblerResult` ジョブの結果と発生した例外を含むオブジェクト。

1. 結果を抽出します。

   新しく作成したPDF・ドキュメントを取得するには、次の操作を実行します。

   * を呼び出す `AssemblerResult` オブジェクトの `getDocuments` メソッド。 これにより、 `java.util.Map` オブジェクト。
   * 反復処理 `java.util.Map` 結果が見つかるまでオブジェクトを閉じます。 `com.adobe.idp.Document` オブジェクト。 (DDX ドキュメントで指定されたPDF結果エレメントを使用して、ドキュメントを取得できます )。
   * を呼び出す `com.adobe.idp.Document` オブジェクトの `copyToFile` メソッドを使用して、PDFドキュメントを抽出します。

   >[!NOTE]
   >
   >If `*LOG_LEVEL*` がログを生成するように設定されている場合は、 `*AssemblerResult*` オブジェクトの `*getJobLog*` メソッド。

**関連トピック**

[クイックスタート（SOAP モード）:Java API を使用したPDFドキュメントのアセンブリ](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-a-pdf-document-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Web サービス API を使用したPDFドキュメントのアセンブリ {#assemble-pdf-documents-using-the-web-service-api}

Assembler Service API（Web サービス）を使用してPDFドキュメントをアセンブリします。

1. プロジェクトファイルを含めます。

   MTOM を使用するMicrosoft .NET プロジェクトを作成します。 次の WSDL 定義を使用していることを確認します。 `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

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
   * の作成 `System.IO.FileStream` オブジェクトを開くには、コンストラクターを呼び出し、DDX ドキュメントのファイルの場所とファイルを開くモードを表す string 値を渡します。
   * コンテンツを格納するバイト配列を作成します。 `System.IO.FileStream` オブジェクト。 バイト配列のサイズは、 `System.IO.FileStream` オブジェクトの `Length` プロパティ。
   * を呼び出して、バイト配列にストリームデータを入力します。 `System.IO.FileStream` オブジェクトの `Read` メソッドを使用し、読み込むバイト配列、開始位置、ストリーム長を渡す。
   * 次の項目に `BLOB` オブジェクトを割り当てる `MTOM` プロパティにバイト配列の内容を入力します。

1. 参照入力PDF文書。

   * 入力PDFドキュメントごとに、 `BLOB` オブジェクトを指定します。 この `BLOB` オブジェクトは、入力PDF・ドキュメントを格納するために使用します。
   * の作成 `System.IO.FileStream` オブジェクトを指定します。
   * コンテンツを格納するバイト配列を作成します。 `System.IO.FileStream` オブジェクト。 バイト配列のサイズは、 `System.IO.FileStream` オブジェクトの `Length` プロパティ。
   * を呼び出して、バイト配列にストリームデータを入力します。 `System.IO.FileStream` オブジェクトの `Read` メソッド。 読み取るバイト配列、開始位置、ストリーム長を渡します。
   * 次の項目に `BLOB` オブジェクトを割り当てる `MTOM` フィールドにバイト配列の内容を入力します。
   * の作成 `MyMapOf_xsd_string_To_xsd_anyType` オブジェクト。 このコレクションオブジェクトは、入力コレクションドキュメントをPDFするために使用されます。
   * 入力PDFドキュメントごとに、 `MyMapOf_xsd_string_To_xsd_anyType_Item` オブジェクト。 例えば、2 つの入力PDFドキュメントを使用する場合、 `MyMapOf_xsd_string_To_xsd_anyType_Item` オブジェクト。
   * キー名を表す string 値を `MyMapOf_xsd_string_To_xsd_anyType_Item` オブジェクトの `key` フィールドに入力します。 この値は、DDX ドキュメントで指定されたPDFソース要素の値と一致する必要があります。 ( このタスクは、入力タスクドキュメントごとにPDFします )。
   * を `BLOB` オブジェクトを指定し、PDFドキュメントを `MyMapOf_xsd_string_To_xsd_anyType_Item` オブジェクトの `value` フィールドに入力します。 ( このタスクは、入力タスクドキュメントごとにPDFします )。
   * を `MyMapOf_xsd_string_To_xsd_anyType_Item` オブジェクトを `MyMapOf_xsd_string_To_xsd_anyType` オブジェクト。 を呼び出す `MyMapOf_xsd_string_To_xsd_anyType` オブジェクトの `Add` メソッドを使用して、 `MyMapOf_xsd_string_To_xsd_anyType` オブジェクト。 ( このタスクは、入力タスクドキュメントごとにPDFします )。

1. 実行時オプションを設定します。

   * の作成 `AssemblerOptionSpec` コンストラクタを使用して実行時オプションを格納するオブジェクト。
   * に属するデータメンバーに値を割り当てて、ビジネス要件を満たすようにランタイムオプションを設定する `AssemblerOptionSpec` オブジェクト。 例えば、エラーが発生した場合にジョブの処理を続行するように Assembler サービスに指示するには、 `false` から `AssemblerOptionSpec` オブジェクトの `failOnError` データメンバー。

1. 入力アセンブリドキュメントをPDFします。

   を呼び出す `AssemblerServiceClient` オブジェクトの `invoke` メソッドを使用して、次の値を渡します。

   * A `BLOB` DDX ドキュメントを表すオブジェクト。
   * この `mapItem` 入力PDF・ドキュメントを格納する配列。 キーはPDFソースファイルの名前と一致する必要があり、値は `BLOB` オブジェクトが含まれます。
   * An `AssemblerOptionSpec` 実行時オプションを指定するオブジェクト。

   この `invoke` メソッドは、 `AssemblerResult` ジョブの結果と発生した可能性のある例外を含むオブジェクト。

1. 結果を抽出します。

   新しく作成したPDF・ドキュメントを取得するには、次の操作を実行します。

   * 次にアクセス： `AssemblerResult` オブジェクトの `documents` フィールド ( `Map` 結果PDF文書を含むオブジェクト。
   * 反復処理 `Map` オブジェクトを閉じます。 次に、その配列メンバの `value` から `BLOB`.
   * PDFドキュメントを表すバイナリデータを、そのドキュメントにアクセスして抽出します `BLOB` オブジェクトの `MTOM` プロパティ。 これは、バイトの配列を返し、PDF・ファイルに書き出すことができます。

   >[!NOTE]
   >
   >If `LOG_LEVEL` がログを生成するように設定されている場合、 `AssemblerResult` オブジェクトの `jobLog` データメンバー。

**関連トピック**

[MTOM を使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
