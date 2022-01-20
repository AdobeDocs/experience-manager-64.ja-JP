---
title: DDX ドキュメントの検証
seo-title: Validating DDX Documents
description: Java API と Web Service API を使用して、プログラムによる DDX ドキュメントの検証を行います。
seo-description: Validate a DDX document programmatically using the Java API and the Web Service API.
uuid: da668170-d2e9-4fff-aef5-432a856bd0bd
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: operations
discoiquuid: 693859b0-a0c3-43f1-95c0-be48a90d7d8d
role: Developer
exl-id: 5be91b23-355b-4e50-b1f5-afed248bc8b5
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '1512'
ht-degree: 3%

---

# DDX ドキュメントの検証 {#validating-ddx-documents}

Assembler サービスで使用される DDX ドキュメントをプログラムで検証できます。 つまり、Assembler サービス API を使用して、DDX ドキュメントが有効かどうかを判断できます。 例えば、以前のAEM Formsバージョンからアップグレードした場合に、DDX ドキュメントが有効であることを確認するには、Assembler サービス API を使用してドキュメントを検証します。

>[!NOTE]
>
>Assembler サービスについて詳しくは、 [AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>DDX ドキュメントについて詳しくは、 [Assembler サービスと DDX リファレンス](https://www.adobe.com/go/learn_aemforms_ddx_63).

## 手順の概要 {#summary-of-steps}

DDX ドキュメントを検証するには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. Assembler クライアントを作成します。
1. 既存の DDX ドキュメントを参照します。
1. DDX ドキュメントを検証するための実行時オプションを設定します。
1. 検証を実行します。
1. 検証結果をログファイルに保存します。

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

Assembler 操作をプログラムで実行する前に、Assembler サービスクライアントを作成する必要があります。

**既存の DDX ドキュメントの参照**

DDX ドキュメントを検証するには、既存の DDX ドキュメントを参照する必要があります。

**DDX ドキュメントを検証するための実行時オプションの設定**

DDX ドキュメントを検証する場合は、DDX ドキュメントを実行するのではなく、Assembler サービスに DDX ドキュメントを検証するよう指示する特定の実行時オプションを設定する必要があります。 また、Assembler サービスがログファイルに書き込む情報の量を増やすこともできます。

**検証の実行**

Assembler サービスクライアントを作成し、DDX ドキュメントを参照し、実行時オプションを設定したら、 `invokeDDX` 操作を実行して DDX ドキュメントを検証します。 DDX ドキュメントを検証する際に、 `null` を map パラメーターとして ( 通常、このパラメーターは DDX ドキュメントで指定されたPDFを Assembler が実行するために必要な操作ドキュメントを格納します )。

検証が失敗すると、例外がスローされ、DDX ドキュメントが無効な理由を `OperationException` インスタンス。 基本的な XML 解析とスキーマチェックを過ぎると、DDX 仕様に対する検証が実行されます。 DDX ドキュメントに含まれるすべてのエラーは、ログに記録されます。

**検証結果をログファイルに保存**

Assembler サービスは、XML ログファイルに書き込むことができる検証結果を返します。 Assembler サービスがログファイルに書き込む詳細の量は、設定した実行時オプションによって異なります。

**関連トピック**

[Java API を使用した DDX ドキュメントの検証](#validate-a-ddx-document-using-the-java-api)

[Web サービス API を使用した DDX ドキュメントの検証](#validate-a-ddx-document-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[プログラムによるPDF文書の作成](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Java API を使用した DDX ドキュメントの検証 {#validate-a-ddx-document-using-the-java-api}

Assembler Service API(Java) を使用して DDX ドキュメントを検証します。

1. プロジェクトファイルを含めます。

   Java プロジェクトのクラスパスに、adobe-assembler-client.jar などのクライアント JAR ファイルを含めます。

1. Assembler クライアントをPDFします。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * の作成 `AssemblerServiceClient` オブジェクトのコンストラクタを使用し、 `ServiceClientFactory` オブジェクト。

1. 既存の DDX ドキュメントを参照します。

   * の作成 `java.io.FileInputStream` コンストラクターを使用して DDX ファイルの場所を指定する string 値を渡すことによって DDX ドキュメントを表すオブジェクト。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. DDX ドキュメントを検証するための実行時オプションを設定します。

   * の作成 `AssemblerOptionSpec` コンストラクタを使用して実行時オプションを格納するオブジェクト。
   * Assembler サービスに対して、 `AssemblerOptionSpec` オブジェクトの setValidateOnly メソッドおよび `true`.
   * Assembler サービスがログファイルに書き込む情報量を、 `AssemblerOptionSpec` オブジェクトの `getLogLevel` メソッドを使用し、文字列値を渡すことは、要件を満たします。 DDX ドキュメントを検証する場合、検証プロセスに役立つ詳細情報をログファイルに書き込む必要があります。 その結果、 `FINE` または `FINER`.

1. 検証を実行します。

   を呼び出す `AssemblerServiceClient` オブジェクトの `invokeDDX` メソッドを使用して、次の値を渡します。

   * A `com.adobe.idp.Document` DDX ドキュメントを表すオブジェクト。
   * 値 `null` 通常、PDF・ドキュメントを格納するjava.io.Map オブジェクトの場合。
   * A `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` 実行時オプションを指定するオブジェクト。

   この `invokeDDX` メソッドは、 `AssemblerResult` DDX ドキュメントが有効かどうかを指定する情報が格納されるオブジェクト。

1. 検証結果をログファイルに保存します。

   * の作成 `java.io.File` オブジェクトに置き換え、ファイル名の拡張子が.xml であることを確認します。
   * を呼び出す `AssemblerResult` オブジェクトの `getJobLog` メソッド。 このメソッドは、 `com.adobe.idp.Document` 検証情報を含むインスタンス。
   * を呼び出す `com.adobe.idp.Document` オブジェクトの `copyToFile` メソッドを使用して、 `com.adobe.idp.Document` オブジェクトをファイルに追加します。

   >[!NOTE]
   >
   >DDX ドキュメントが無効な場合、 `OperationException` がスローされます。 catch 文内で、 `OperationException` オブジェクトの `getJobLog` メソッド。

**関連トピック**

[DDX ドキュメントの検証](#validating-ddx-documents)

[クイックスタート（SOAP モード）:Java API を使用した DDX ドキュメントの検証](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-validating-ddx-documents-using-the-java-api) （SOAP モード）

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Web サービス API を使用した DDX ドキュメントの検証 {#validate-a-ddx-document-using-the-web-service-api}

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

[DDX ドキュメントの検証](#validating-ddx-documents)

[MTOM を使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
