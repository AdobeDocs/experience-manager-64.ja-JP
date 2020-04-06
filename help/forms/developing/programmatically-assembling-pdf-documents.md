---
title: プログラムによるPDFドキュメント
seo-title: プログラムによるPDFドキュメント
description: 'null'
seo-description: 'null'
uuid: aa3f8f39-1fbc-48d0-82ff-6caaadf125fc
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: operations
discoiquuid: ebe8136b-2a79-4035-b9d5-aa70a5bbd4af
translation-type: tm+mt
source-git-commit: 5a185a50dc9e413953be91444d5c8e76bdae0a69

---


# プログラムによるPDFドキュメント {#programmatically-assembling-pdf-documents}

Assembler Service APIを使用して、複数のPDFドキュメントを1つのPDFドキュメントにアセンブルできます。 次の図に、3つのPDFドキュメントを単一のPDFドキュメントに結合する例を示します。

![pa_pa_ドキュメント_アセンブリ](assets/pa_pa_document_assembly.png)

複数のPDFドキュメントを1つのPDFドキュメントにアセンブリするには、DDXドキュメントが必要です。 DDXドキュメントは、Assemblerサービスによって生成されるPDFドキュメントを記述します。 つまり、DDXドキュメントは、実行するアクションをAssemblerサービスに指示します。

この説明の目的で、次のDDXドキュメントを使用します。

```as3
 <?xml version="1.0" encoding="UTF-8"?> 
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/"> 
     <PDF result="out.pdf"> 
         <PDF source="map.pdf" /> 
         <PDF source="directions.pdf" /> 
     </PDF> 
 </DDX>
```

このDDXドキュメントは、 *map.pdfとdirections.pdfという2つのPDFドキュメントを*** 1つのPDFドキュメントにマージします。

>[!NOTE]
>
>PDFドキュメントをディスアセンブリするDDXドキュメントを確認するには、「PDFアセンブリのプログラムによ [るディスアセンブリ」を参照してくださ](/help/forms/developing/programmatically-disassembling-pdf-documents.md#programmatically-disassembling-pdf-documents)い。

>[!NOTE]
>
>For more information about the Assembler service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>DDXドキュメントについて詳しくは、 [Assembler Service and DDX Referenceを参照してください](https://www.adobe.com/go/learn_aemforms_ddx_63)。

## Webサービスを使用してAssemblerサービスを呼び出す場合の考慮事項 {#considerations-when-invoking-assembler-service-using-web-services}

大きなドキュメントのアセンブリ中にヘッダーとフッターを追加すると、エラーが発生し、フ `OutOfMemory` ァイルがアセンブリされない場合があります。 この問題が発生する可能性を減らすには、次の例に示すよ `DDXProcessorSetting` うに、DDXドキュメントに要素を追加します。

`<DDXProcessorSetting name="checkpoint" value="2000" />`

この要素は、要素の子または要素の子と `DDX` して追加することができ `PDF result` ます。 この設定のデフォルト値は0（ゼロ）で、チェックポイントがオフになり、DDXは要素が存在しない場合と同じよ `DDXProcessorSetting` うに動作します。 エラーが発生した場 `OutOfMemory` 合は、値を整数（通常は500 ～ 5000）に設定する必要があります。 チェックポイントの値が小さいと、チェックポイントの頻度が高くなります。

## 手順の概要 {#summary-of-steps}

複数のPDFドキュメントから単一のPDFドキュメントをアセンブリするには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. PDFアセンブラクライアントを作成します。
1. 既存のDDXドキュメントの参照
1. 参照入力PDFドキュメント。
1. 実行時オプションを設定します。
1. 入力PDFアセンブリをドキュメントします。
1. 結果を抽出します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、必ずプロキシファイルを含めてください。

次のJARファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar（AEM FormsがJBossにデプロイされている場合に必要）
* jbossall-client.jar（AEM FormsがJBossにデプロイされている場合に必要）

aem FormsがJBoss以外のサポート対象のJ2EEアプリケーションサーバーにデプロイされている場合は、adobe-utilities.jarファイルとjbossall-client.jarファイルを、AEM FormsがデプロイされているJ2EEアプリケーションサーバーに固有のJARファイルに置き換える必要があります。

**PDFアセンブラクライアントの作成**

プログラムによってAssembler操作を実行する前に、Assemblerクライアントを作成する必要があります。

**既存のDDXの参照ドキュメント**

PDFドキュメントをアセンブリするには、DDXアセンブリを参照する必要があります。ドキュメント 例えば、この節で紹介したDDXドキュメントについて考えてみましょう。 このDDXドキュメントは、2つのPDFドキュメントを1つのPDFドキュメントに結合するようにAssemblerサービスに指示します。

**参照入力PDFドキュメント**

Assemblerサービスに渡す入力PDFドキュメントを参照します。 例えば、MapとDirectionsという名前の2つの入力PDFドキュメントを渡す場合は、対応するPDFファイルを渡す必要があります。

map.pdfファイルとdirections.pdfファイルは、両方ともコレクションオブジェクトに配置する必要があります。 キーの名前は、DDXドキュメントのPDF source属性の値と一致する必要があります。 DDXドキュメントのキーとsource属性が一致した場合、PDFファイルの名前は関係ありません。

>[!NOTE]
>
>操作を `*AssemblerResult*` 呼び出すと、コレクションオブジェクトを含むオブジェクトが返さ `*invokeDDX*` れます。 この操作は、複数の入力PDF操作をAssemblerサービスに渡す場合にドキュメントされます。 ただし、Assemblerサービスに入力PDFを1つだけ渡し、1つの戻りドキュメントのみが必要な場合は、操作を呼び出 `*invokeOneDocument*` します。 この操作を呼び出すと、1つのドキュメントが返されます。 この操作の使用について詳しくは、暗号化されたPDF [ドキュメントの集成](/help/forms/developing/assembling-encrypted-pdf-documents.md#assembling-encrypted-pdf-documents)。

**実行時オプションの設定**

ジョブの実行中にAssemblerサービスの動作を制御する実行時オプションを設定できます。 例えば、エラーが発生した場合にジョブの処理を続行するようにAssemblerサービスに指示するオプションを設定できます。 設定できる実行時オプションについて詳しくは、『 `AssemblerOptionSpec` AEM Forms APIリファレンス』のクラス [参照を参照し](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)てください。

**入力PDFのアセンブリドキュメント**

サービスクライアントを作成し、DDXファイルを参照し、入力PDFドキュメントを格納するコレクションオブジェクトを作成し、実行時オプションを設定したら、DDX操作を呼び出すことができます。 この節で指定するDDXドキュメントを使用する場合、map.pdfファイルとdirection.pdfファイルが1つのPDFドキュメントに結合されます。

**結果の抽出**

Assemblerサービスは、オブジェ `java.util.Map` クトから取得でき、操作結果を含 `AssemblerResult` むオブジェクトを返します。 返されるオブジ `java.util.Map` ェクトには、結果のドキュメントと例外が含まれます。

次の表に、返されるオブジェクト内に配置できるキー値とオブジェクトタイプの一部を示し `java.util.Map` ます。

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
   <td><p>DDX結果ドキュメントで指定された結果要素が含まれます</p></td> 
  </tr> 
  <tr> 
   <td><p><code><i>documentName</i></code></p></td> 
   <td><p><code>Exception</code></p></td> 
   <td><p>例外を含みます。ドキュメント</p></td> 
  </tr> 
  <tr> 
   <td><p><code>OutputMapConstants.LOG_NAME</code></p></td> 
   <td><p><code>com.adobe.idp.Documen</code></p></td> 
   <td><p>ジョブログが含まれます</p></td> 
  </tr> 
 </tbody> 
</table>

**関連トピック**

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[プログラムによるPDFドキュメントの分解](/help/forms/developing/programmatically-disassembling-pdf-documents.md#programmatically-disassembling-pdf-documents)

## Java APIを使用したPDFドキュメントのアセンブリ {#assemble-pdf-documents-using-the-java-api}

Assembler Service API(Java)を使用してPDFドキュメントをアセンブリします。

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-assembler-client.jarなどのクライアントJARファイルを含めます。

1. PDFアセンブラクライアントを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * Create an `AssemblerServiceClient` object by using its constructor and passing the `ServiceClientFactory` object.

1. 既存のDDXドキュメントの参照

   * コンストラ `java.io.FileInputStream` クターを使用し、DDXファイルの場所を指定するstring値を渡して、DDXドキュメントを表すオブジェクトを作成します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. 参照入力PDFドキュメント。

   * コンストラク `java.util.Map` ターを使用して、入力PDFドキュメントの保存に使用するオブジェクトを作成 `HashMap` します。
   * 各入力PDFドキュメントに対して、コンストラク `java.io.FileInputStream` ターを使用し、入力PDFドキュメントの場所を渡して、オブジェクトを作成します。
   * 各入力PDFドキュメントに対して、オブジェクトを作成 `com.adobe.idp.Document` し、PDFドキュメントを含むオ `java.io.FileInputStream` ブジェクトを渡します。
   * 各入力ドキュメントに対して、そのメソッドを呼び出し、 `java.util.Map` 次の引数を渡して、オ `put` ブジェクトにエントリを追加します。

      * キー名を表すstring値です。 この値は、DDX要素で指定されたPDFソース要素の値と一致する必要があります。ドキュメント
      * ソースPDF `com.adobe.idp.Document` ドキュメントを含むオ `java.util.List` ブジェクト(または複数のドキュメントを指定するオブジェクト)です。

1. 実行時オプションを設定します。

   * コンストラクタ `AssemblerOptionSpec` ーを使用して、実行時のオプションを格納するオブジェクトを作成します。
   * オブジェクトに属するメソッドを呼び出して、ビジネス要件に合わせて実行時のオプションを設定 `AssemblerOptionSpec` します。 例えば、エラーが発生した場合にジョブの処理を続行するようにAssemblerサービスに指示するには、オブジェクトのメ `AssemblerOptionSpec` ソッドを呼び出し `setFailOnError` て渡してくださ `false`い。

1. 入力PDFアセンブリをドキュメントします。

   オブジェクト `AssemblerServiceClient` のメソッドを `invokeDDX` 呼び出し、次の必要な値を渡します。

   * 使用 `com.adobe.idp.Document` するDDXドキュメントを表すオブジェクト
   * アセンブリ `java.util.Map` 対象の入力PDFファイルを含むオブジェクトです。
   * デフォ `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` ルトのフォントやジョブログレベルを含む、実行時のオプションを指定するオブジェクト。
   このメ `invokeDDX` ソッドは、ジ `com.adobe.livecycle.assembler.client.AssemblerResult` ョブの結果と発生した例外を含むオブジェクトを返します。

1. 結果を抽出します。

   新しく作成されたPDFアクションを取得するには、次のドキュメントを実行します。

   * オブジェクトの `AssemblerResult` メソッドを呼び出 `getDocuments` します。 オブジェクトを返 `java.util.Map` します。
   * 結果のオブジェクト `java.util.Map` が見つかるまで、オブジェクトを繰り返 `com.adobe.idp.Document` します。 (DDX要素で指定されたPDF結果ドキュメントを使用して、要素を取得できます)。
   * オブジェクト `com.adobe.idp.Document` のメソッドを呼 `copyToFile` び出して、PDFドキュメントを抽出します。
   >[!NOTE]
   >
   >を設 `*LOG_LEVEL*` 定してログを生成した場合は、オブジェクトのメソッドを使用してロ `*AssemblerResult*` グを抽出でき `*getJobLog*` ます。

**関連トピック**

[クイック開始（SOAPモード）:Java APIを使用したPDFドキュメントのアセンブリ](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-a-pdf-document-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## WebサービスAPIを使用したPDFドキュメントのアセンブリ {#assemble-pdf-documents-using-the-web-service-api}

Assembler Service API（Webサービス）を使用してPDFドキュメントをアセンブリします。

1. プロジェクトファイルを含めます。

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。 `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >AEM Formsをホ `localhost` ストするサーバーのIPアドレスで置き換えます。

1. PDFアセンブラクライアントを作成します。

   * デフォルトのコンス `AssemblerServiceClient` トラクターを使用して、オブジェクトを作成します。
   * コンストラクタ `AssemblerServiceClient.Endpoint.Address` ーを使用してオブジェクトを作 `System.ServiceModel.EndpointAddress` 成します。 WSDLを指定するstring値をAEM Formsサービス(例えば、 `http://localhost:8080/soap/services/AssemblerService?blob=mtom`)に渡します。 属性を使用する必要はありま `lc_version` せん。 この属性は、サービス参照を作成する際に使用されます。
   * フィールド `System.ServiceModel.BasicHttpBinding` の値を取得して、オブジェクトを作成 `AssemblerServiceClient.Endpoint.Binding` します。 戻り値を `BasicHttpBinding` にキャストします。
   * オブジェクト `System.ServiceModel.BasicHttpBinding` のフィールドをに `MessageEncoding` 設定しま `WSMessageEncoding.Mtom`す。 この値により、MTOMが使用されます。
   * 次のオプションを実行して、基本的なHTTP認証を有効にします。タスク

      * AEM formsのユーザー名をフィールドに割り当てま `AssemblerServiceClient.ClientCredentials.UserName.UserName`す。
      * 対応するパスワード値をフィールドに割り当てま `AssemblerServiceClient.ClientCredentials.UserName.Password`す。
      * 定数値をフィールドに `HttpClientCredentialType.Basic` 割り当てま `BasicHttpBindingSecurity.Transport.ClientCredentialType`す。
      * 定数値をフィールドに `BasicHttpSecurityMode.TransportCredentialOnly` 割り当てま `BasicHttpBindingSecurity.Security.Mode`す。

1. 既存のDDXドキュメントの参照

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。このオブ `BLOB` ジェクトは、DDXドキュメントの保存。
   * オブジェク `System.IO.FileStream` トを作成するには、コンストラクターを呼び出し、DDXドキュメントーのファイルの場所とファイルを開くモードを表すstring値を渡します。
   * オブジェクトの内容を格納するバイト配列を作成 `System.IO.FileStream` します。 バイト配列のサイズは、オブジェクトのプロパティを取得す `System.IO.FileStream` ることで指定で `Length` きます。
   * オブジェクトのメソッドを呼び出し、読み取るバイ `System.IO.FileStream` ト配列、開始位 `Read` 置およびストリームの長さを渡すことで、バイト配列にストリームデータを入力します。
   * オブジェクト `BLOB` にバイト配列の内容を割り `MTOM` 当てて、オブジェクトを設定します。

1. 参照入力PDFドキュメント。

   * 各入力PDFドキュメントに対して、コンストラクタ `BLOB` ーを使用してオブジェクトを作成します。 このオ `BLOB` ブジェクトは、入力PDFの保存に使用されるドキュメントです。
   * オブジェクト `System.IO.FileStream` を作成するには、コンストラクターを呼び出し、入力PDFドキュメントーのファイルの場所とファイルを開くモードを表すstring値を渡します。
   * オブジェクトの内容を格納するバイト配列を作成 `System.IO.FileStream` します。 バイト配列のサイズは、オブジェクトのプロパティを取得す `System.IO.FileStream` ることで指定で `Length` きます。
   * オブジェクトのメソッドを呼び出して、バイト配列にストリ `System.IO.FileStream` ームデータを入力 `Read` します。 読み取るバイト配列、開始位置およびストリーム長を渡します。
   * バイト配列の `BLOB` 内容をフィールドに割り `MTOM` 当てて、オブジェクトを入力します。
   * Create a `MyMapOf_xsd_string_To_xsd_anyType` object. このコレクションオブジェクトは、入力PDFコレクションの保存に使用されるドキュメントです。
   * 各入力PDFドキュメントに対して、オブジェクトを作成 `MyMapOf_xsd_string_To_xsd_anyType_Item` します。 例えば、2つの入力PDFドキュメントを使用する場合は、2つのオブジェクトを作成 `MyMapOf_xsd_string_To_xsd_anyType_Item` します。
   * キー名を表すstring値をオブジェクトのフィールド `MyMapOf_xsd_string_To_xsd_anyType_Item` に割り当て `key` ます。 この値は、DDX要素で指定されたPDFソース要素の値と一致する必要があります。ドキュメント (このタスクは、入力PDFのドキュメントごとに実行)
   * PDFドキュメントを保 `BLOB` 存するオブジェクトをオブジェク `MyMapOf_xsd_string_To_xsd_anyType_Item` トのフィールドに割り当 `value` てます。 (このタスクは、入力PDFのドキュメントごとに実行)
   * オ追加ブジェクト `MyMapOf_xsd_string_To_xsd_anyType_Item``MyMapOf_xsd_string_To_xsd_anyType` 。 Invoke the `MyMapOf_xsd_string_To_xsd_anyType` object&#39;s `Add` method and pass the `MyMapOf_xsd_string_To_xsd_anyType` object. (このタスクは、入力PDFのドキュメントごとに実行)

1. 実行時オプションを設定します。

   * コンストラクタ `AssemblerOptionSpec` ーを使用して、実行時のオプションを格納するオブジェクトを作成します。
   * オブジェクトに属するデータメンバーに値を割り当てて、ビジネス要件に合わせて実行時オプションを設定 `AssemblerOptionSpec` します。 例えば、エラーが発生した場合にジョブの処理を続行するようにAssemblerサービスに指示するには、オブジェクトの `false` データメ `AssemblerOptionSpec` ンバーに割り当 `failOnError` てます。

1. 入力PDFアセンブリをドキュメントします。

   オブジェクト `AssemblerServiceClient` のメソッドを `invoke` 呼び出し、次の値を渡します。

   * DDX `BLOB` ドキュメント
   * 入力PDF `mapItem` ドキュメントを含む配列。 そのキーはPDFソースファイルの名前と一致し、その値はそれらのファイルに対応するオブジ `BLOB` ェクトである必要があります。
   * 実行時 `AssemblerOptionSpec` のオプションを指定するオブジェクトです。
   このメ `invoke` ソッドは、ジ `AssemblerResult` ョブの結果と発生した可能性のある例外を含むオブジェクトを返します。

1. 結果を抽出します。

   新しく作成されたPDFアクションを取得するには、次のドキュメントを実行します。

   * 結果のPDF `AssemblerResult` ドキュメントを `documents` 含むオブジェクト `Map` のフィールドにアクセスします。
   * 結果のオブジェ `Map` クトの名前と一致するキーが見つかるまで、オブジェクトを繰り返し処理します。ドキュメント 次に、その配列メンバーのをにキャ `value` ストしま `BLOB`す。
   * オブジェクトのプロパティにアクセスして、PDFドキュメントを表すバイナリ `BLOB` データを抽出 `MTOM` します。 PDFファイルに書き出すことのできるバイトの配列を返します。
   >[!NOTE]
   >
   >ログを `LOG_LEVEL` 生成するように設定した場合は、オブジェクトのデータメンバの値を取得してログ `AssemblerResult` を抽出で `jobLog` きます。

**関連トピック**

[MTOMを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
