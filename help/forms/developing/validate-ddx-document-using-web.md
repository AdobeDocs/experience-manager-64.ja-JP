---
title: Web サービス API を使用した DDX ドキュメントの検証
seo-title: Validate a DDX document using theweb service API
description: DDX ドキュメントを検証するには、Assembler Service API を使用します。
seo-description: Use the Assembler Service API to validate a DDX document.
uuid: f6125746-6138-4e46-a1c4-fb24fd7399c5
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/validating_ddx_documents
products: SG_EXPERIENCEMANAGER/6.4/FORMS
discoiquuid: a6fe91ab-3aa0-4b3d-87c0-6cf69a2c4cc4
role: Developer
exl-id: da303186-8f36-4fc8-a2db-b38a0b200c39
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '626'
ht-degree: 2%

---

# Web サービス API を使用した DDX ドキュメントの検証 {#validate-a-ddx-document-using-theweb-service-api}

Assembler Service API（Web サービス）を使用して DDX ドキュメントを検証します。

1. プロジェクトファイルを含めます。

   MTOM を使用するMicrosoft .NET プロジェクトを作成します。 次の WSDL 定義を使用していることを確認します。 `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >localhost を forms サーバーの IP アドレスに置き換えます。

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
   * の作成 `System.IO.FileStream` オブジェクトを作成するには、コンストラクターを呼び出し、DDX ドキュメントのファイルの場所とファイルを開くモードを表す string 値を渡します。
   * コンテンツを格納するバイト配列を作成します。 `System.IO.FileStream` オブジェクト。 バイト配列のサイズは、 `System.IO.FileStream` オブジェクトの `Length` プロパティ。
   * を呼び出して、バイト配列にストリームデータを入力します。 `System.IO.FileStream` オブジェクトの `Read` メソッドを使用し、読み込むバイト配列、開始位置、ストリーム長を渡す。
   * 次の項目に `BLOB` オブジェクトを割り当てる `MTOM` プロパティにバイト配列の内容を入力します。

1. DDX ドキュメントを検証するための実行時オプションを設定します。

   * の作成 `AssemblerOptionSpec` コンストラクタを使用して実行時オプションを格納するオブジェクト。
   * DDX ドキュメントを検証するように Assembler サービスに指示する実行時オプションを設定します。このオプションは、 `AssemblerOptionSpec` オブジェクトの `validateOnly` データメンバー。
   * Assembler サービスがログファイルに書き込む情報の量を設定するには、 `AssemblerOptionSpec` オブジェクトの `logLevel` データメンバー。 メソッドを使用して DDX ドキュメントを検証する場合、検証プロセスに役立つ詳細情報をログファイルに書き込みます。 その結果、 `FINE` または `FINER`. 設定できる実行時オプションについて詳しくは、 `AssemblerOptionSpec` のクラス参照 [AEM Forms API リファレンス](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

1. 検証を実行します。

   を呼び出す `AssemblerServiceClient` オブジェクトの `invokeDDX` メソッドを使用して、次の値を渡します。

   * A `BLOB` DDX ドキュメントを表すオブジェクト。
   * 値 `null` の `Map` オブジェクトを指定します。通常はPDF・ドキュメントを格納します。
   * An `AssemblerOptionSpec` 実行時オプションを指定するオブジェクト。

   この `invokeDDX` メソッドは、 `AssemblerResult` DDX ドキュメントが有効かどうかを指定する情報が格納されるオブジェクト。

1. 検証結果をログファイルに保存します。

   * の作成 `System.IO.FileStream` オブジェクトを作成します。 ファイル名の拡張子が.xml であることを確認します。
   * の作成 `BLOB` の値を取得してログ情報を保存するオブジェクト `AssemblerResult` オブジェクトの `jobLog` データメンバー。
   * コンテンツを格納するバイト配列を作成します。 `BLOB` オブジェクト。 バイト配列を生成するには、 `BLOB` オブジェクトの `MTOM` フィールドに入力します。
   * の作成 `System.IO.BinaryWriter` オブジェクトのコンストラクタを呼び出し、 `System.IO.FileStream` オブジェクト。
   * を呼び出して、バイト配列の内容をPDFファイルに書き込みます。 `System.IO.BinaryWriter` オブジェクトの `Write` メソッドを使用してバイト配列を渡す。

   >[!NOTE]
   >
   >DDX ドキュメントが無効な場合、 `OperationException` がスローされます。 catch 文内で、 `OperationException` オブジェクトの `jobLog` メンバー。

**関連トピック**

[DDX ドキュメントの検証](/help/forms/developing/validating-ddx-documents.md#validating-ddx-documents)

[MTOM を使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
