---
title: Web サービス API を使用したPDFドキュメントの分解
seo-title: Disassemble a PDF document usingthe web service API
description: Assembler サービス API を使用したPDFドキュメントの分解
seo-description: Disassemble a PDF document using the Assembler Service API
uuid: d6283dc5-e333-49d0-abde-1d390662f4fe
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/programmatically_disassembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.4/FORMS
discoiquuid: 49584fb4-8c3a-4d73-acd6-0879a67f6093
role: Developer
exl-id: ea6a05ff-d8d8-4a4f-b1aa-e09670e40ba7
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '704'
ht-degree: 2%

---

# Web サービス API を使用したPDFドキュメントのディスアセンブリ {#disassemble-a-pdf-document-usingthe-web-service-api}

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

[プログラムによるPDFドキュメントの分解](/help/forms/developing/programmatically-disassembling-pdf-documents.md#programmatically-disassembling-pdf-documents)

[MTOM を使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
