---
title: 使用権限の割り当て
seo-title: Assigning Usage Rights
description: Acrobat Reader DC Extensions Java Client API と Web Service API を使用して、使用権限をPDFドキュメントに適用したり、ドキュメントから削除したりします。
seo-description: Use the Acrobat Reader DC extensions Java Client API and Web Service API to apply and remove usage rights from PDF documents.
uuid: 8c2020df-ea3c-49fa-916f-38a458f40d2b
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: operations
discoiquuid: 9e8db506-9ace-4e1f-8a7b-c4e9b15dde7e
role: Developer
exl-id: c7805d8a-eb6a-4908-9662-936920ffa67a
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '3912'
ht-degree: 7%

---

# 使用権限の割り当て {#assigning-usage-rights}

## Acrobat Reader DC Extensions Service について {#about-the-acrobat-reader-dc-extensions-service}

Acrobat Reader DC Extensions サービスを使用すると、Adobe Readerの機能を拡張して、組織でインタラクティブなPDFドキュメントを簡単に共有できます。 Acrobat Reader DC Extensions サービスは、PDF1.7 以降を含むすべてのPDFドキュメントを完全にサポートします。Adobe Reader 7.0 以降で機能します。 このサービスは、PDFドキュメントに使用権限を追加し、Adobe Readerを使用してPDFドキュメントを開いた場合は通常使用できない機能をアクティベートします。 サードパーティユーザーは、権限を付与されたドキュメントを使用する際に、追加のソフトウェアやプラグインを必要としません。

Acrobat Reader DC Extensions サービスを使用して、次のタスクを実行できます。

* 使用権限をPDF・ドキュメントに適用する。 詳しくは、 [使用権限のPDF・ドキュメントへの適用](assigning-usage-rights.md#applying-usage-rights-to-pdf-documents).
* 使用権限をPDF文書から削除 詳しくは、 [使用権限の削除 (PDF・ドキュメント )](assigning-usage-rights.md#removing-usage-rights-from-pdf-documents).
* 資格情報の詳細を取得します。 詳しくは、 [認証情報の取得](assigning-usage-rights.md#retrieving-credential-information).

>[!NOTE]
>
>Acrobat Reader DC Extensions サービスについて詳しくは、 [AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63).

## 使用権限のPDF・ドキュメントへの適用 {#applying-usage-rights-to-pdf-documents}

Acrobat Reader DC拡張機能 Java Client API と Web サービスを使用して、PDFドキュメントに使用権限を適用できます。 使用権限は、Acrobat ではデフォルトで利用できるが Adobe Reader では利用できない機能（フォームにコメントを追加する機能や、フォームフィールドにデータを入力してフォームを保存する機能など）に関連しています。使用権限が与えられた PDF ドキュメントは、使用権限を付与されたドキュメントと呼ばれます。使用権限を付与されたドキュメントを Adobe Reader で開いたユーザーは、そのドキュメントで有効になっている操作を実行できます。

>[!NOTE]
>
>を使用してPDFドキュメントに使用権限を適用する場合 `applyUsageRights` メソッド（Java API の一部）を使用して、 `isModeFinal` のパラメーター `ReaderExtensionsOptionSpec` 対して `false`. その結果、フォーム処理カウンターが更新されず、パフォーマンスが向上します。 フォーム処理カウンターの更新を気にしない場合は、 `isModeFinal` パラメータ `false`.

>[!NOTE]
>
>Acrobat Reader DC Extensions サービスについて詳しくは、 [AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary-of-steps}

使用権限をPDF・ドキュメントに適用するには、次の手順に従います。

1. プロジェクトファイルを含めます。
1. Acrobat Reader DC Extensions クライアントオブジェクトを作成します。
1. PDF文書を取得
1. 適用する使用権限を指定します。
1. 使用権限をPDF文書に適用する。
1. 権限が有効なPDF文書を保存します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。 Web サービスを使用している場合は、プロキシファイルを必ず含めてください。

**Acrobat Reader DC Extensions クライアントオブジェクトの作成**

プログラムによってAcrobat Reader DC拡張機能サービス操作を実行するには、Acrobat Reader DC拡張機能サービスクライアントオブジェクトを作成する必要があります。 Acrobat Reader DC拡張機能 Java API を使用している場合は、 `ReaderExtensionsServiceClient` オブジェクト。 Acrobat Reader DC拡張機能 Web サービス API を使用している場合は、 `ReaderExtensionsServiceService` オブジェクト。

**PDF文書の取得**

使用権限を適用するには、PDFドキュメントを取得する必要があります。 権限が有効なPDFドキュメントには、使用権限ディクショナリが含まれています。 Adobe Readerがそのような辞書を含むドキュメントを開くと、そのドキュメントの辞書で指定された使用権限のみが有効になります。 ドキュメントに使用権限ディクショナリが含まれていない場合、Acrobat Reader DC Extensions サービスは使用権限ディクショナリを作成します。 既に辞書が含まれている場合、Acrobat Reader DC Extensions サービスは、指定した使用権限で既存の使用権限を上書きします。 辞書は、有効にする使用権限を指定します。 ユーザーがAdobe Readerでドキュメントを開くと、辞書で指定されている使用権限のみが許可されます。

**適用する使用権限を指定**

設定できる使用権限は、Adobe Systems Incorporatedで購入した秘密鍵証明書によって決まります。 通常、資格情報には、インタラクティブフォームに関連する使用権限など、関連する使用権限のグループを設定する権限が付与されます。 各秘密鍵証明書には、一定数の権限が付与されたPDF・ドキュメントを作成する権限があります。 評価用の資格情報を使用すると、無制限数のドラフトドキュメントを作成する権限が与えられます。

>[!NOTE]
>
>秘密鍵証明書で許可されていない使用権限を割り当てようとすると、例外が発生します。

**使用権限をPDF文書に適用**

PDFドキュメントに使用権限を適用するには、使用権限の適用に使用する秘密鍵証明書のエイリアスを参照します ( 通常、秘密鍵証明書はAEM Formsのインストール時にインストールされます )。 また、使用権限を適用するPDFドキュメントを指定する必要があります。 秘密鍵証明書の設定について詳しくは、使用しているアプリケーションサーバー向けのインストールおよびデプロイガイドを参照してください。

**権限が有効なPDF文書を保存**

Acrobat Reader DC Extensions サービスがPDFドキュメントに使用権限を適用したら、使用権限を付与されたPDFドキュメントをPDFファイルとして保存できます。

**関連トピック**

[Java API を使用した使用権限の適用](assigning-usage-rights.md#apply-usage-rights-using-the-java-api)

[Web サービス API を使用した使用権限の適用](assigning-usage-rights.md#apply-usage-rights-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Acrobat Reader DC Extensions Service API クイックスタート](/help/forms/developing/acrobat-reader-dc-extensions-service.md#acrobat-reader-dc-extensions-service-java-api-quick-start-soap)

### Java API を使用した使用権限の適用 {#apply-usage-rights-using-the-java-api}

Acrobat Reader DC Extensions API(Java) を使用して、PDFドキュメントに使用権限を適用します。

1. プロジェクトファイルを含める

   Java プロジェクトのクラスパスに、adobe-reader-extensions-client.jar などのクライアント JAR ファイルを含めます。

1. Acrobat Reader DC Extensions クライアントオブジェクトを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用して `ReaderExtensionsServiceClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. PDF文書を取得

   * の作成 `java.io.FileInputStream` コンストラクタを使用し、PDFドキュメントの場所を指定する string 値を渡すことによって、PDFドキュメントを表すオブジェクト。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. 適用する使用権限を指定します。

   * の作成 `UsageRights` コンストラクタを使用して使用権限を表すオブジェクト。
   * 適用する使用権限ごとに、 `UsageRights` オブジェクト。 例えば、 `enableFormFillIn` 使用権限、を呼び出す `UsageRights` オブジェクトの `enableFormFillIn` メソッドとパス `true`. （適用する各使用権限に対して、この手順を繰り返します）。

1. 使用権限をPDF文書に適用する。

   * コンストラクタを使用して `ReaderExtensionsOptionSpec` オブジェクトを作成します。このオブジェクトには、Acrobat Reader DC Extensions サービスで必要な実行時オプションが含まれています。 このコンストラクタを呼び出す場合は、次の値を指定する必要があります。

      * この `UsageRights` ドキュメントに適用する使用権限を含むオブジェクト。
      * Adobe Reader 7.x で権限が付与されたPDFドキュメントを開いたときにユーザーに表示されるメッセージを指定する string 値です。このメッセージは、Adobe Reader 8.0 では表示されません。
   * を呼び出して、使用権限をPDFドキュメントに適用します。 `ReaderExtensionsServiceClient` オブジェクトの `applyUsageRights` メソッドを使用して、次の値を渡します。

      * この `com.adobe.idp.Document` 使用権限が適用されるPDFドキュメントを含むオブジェクト。
      * 使用権限を適用できる秘密鍵証明書のエイリアスを指定する string 値です。
      * 対応するパスワード値を指定する文字列値. ( 現在、このパラメーターは無視されます。 パス `null`.)
   * この `ReaderExtensionsOptionSpec` 実行時オプションを含むオブジェクト。

   この `applyUsageRights` メソッドは、 `com.adobe.idp.Document` 権限が有効なPDF・ドキュメントを含むオブジェクト。

1. 権限が有効なPDF文書を保存します。

   * `java.io.File` オブジェクトを作成し、ファイル拡張子が .pdf であることを確認します。
   * を呼び出す `com.adobe.idp.Document` オブジェクトの `copyToFile` メソッドを使用して、 `com.adobe.idp.Document` オブジェクトをファイルに追加します ( `com.adobe.idp.Document` が返したオブジェクト `applyUsageRights` メソッド )。

**関連トピック**

[使用権限のPDF・ドキュメントへの適用](assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)

[クイックスタート（SOAP モード）:Java API を使用した使用権限の適用](/help/forms/developing/acrobat-reader-dc-extensions-service.md#quick-start-soap-mode-applying-usage-rights-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Web サービス API を使用した使用権限の適用 {#apply-usage-rights-using-the-web-service-api}

Acrobat Reader DC Extensions API（Web サービス）を使用して、PDFドキュメントに使用権限を適用します。

1. プロジェクトファイルを含めます。

   MTOM を使用するMicrosoft .NET プロジェクトを作成します。 次の WSDL 定義を使用していることを確認します。 `http://localhost:8080/soap/services/ReaderExtensionsService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >置換 `localhost` を、AEM Formsをホストするサーバーの IP アドレスに設定します。

1. Acrobat Reader DC Extensions クライアントオブジェクトを作成します。

   * の作成 `ReaderExtensionsServiceClient` オブジェクトのデフォルトのコンストラクタを使用します。
   * の作成 `ReaderExtensionsServiceClient.Endpoint.Address` オブジェクトを `System.ServiceModel.EndpointAddress` コンストラクタ。 WSDL をAEM Formsサービスに渡す文字列値 ( 例： `http://localhost:8080/soap/services/ReaderExtensionsService?blob=mtom`. 次を指定してください。 `?blob=mtom`.)
   * の作成 `System.ServiceModel.BasicHttpBinding` オブジェクトを作成するには、 `ReaderExtensionsServiceClient.Endpoint.Binding` フィールドに入力します。 戻り値を `BasicHttpBinding` にキャストします。
   * を `System.ServiceModel.BasicHttpBinding` オブジェクトの `MessageEncoding` ～に向かって `WSMessageEncoding.Mtom`. この値は、MTOM が確実に使用されるようにします。
   * 次のタスクを実行して、基本的な HTTP 認証を有効にします。

      * フィールドにAEM forms ユーザー名を割り当てます。 `ReaderExtensionsServiceClient.ClientCredentials.UserName.UserName`.
      * 対応するパスワード値をフィールドに割り当てます。 `ReaderExtensionsServiceClient.ClientCredentials.UserName.Password`.
      * 定数値を割り当て `HttpClientCredentialType.Basic` フィールドに `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 定数値を割り当て `BasicHttpSecurityMode.TransportCredentialOnly` フィールドに `BasicHttpBindingSecurity.Security.Mode`.

1. PDF文書を取得

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。この `BLOB` オブジェクトは、使用権限が適用されるPDFドキュメントを保存するために使用されます。
   * の作成 `System.IO.FileStream` オブジェクトを指定します。
   * コンテンツを格納するバイト配列を作成します。 `System.IO.FileStream` オブジェクト。 バイト配列のサイズは、 `System.IO.FileStream` オブジェクトの `Length` プロパティ。
   * を呼び出して、バイト配列にストリームデータを入力します。 `System.IO.FileStream` オブジェクトの `Read` メソッド。 読み取るバイト配列、開始位置、ストリーム長を渡します。
   * 次の項目に `BLOB` オブジェクトを割り当てる `MTOM` プロパティにバイト配列の内容を入力します。

1. 適用する使用権限を指定します。

   * の作成 `UsageRights` コンストラクタを使用して使用権限を表すオブジェクト。
   * 適用する使用権限ごとに、値を割り当てます。 `true` を `UsageRights` オブジェクト。 例えば、 `enableFormFillIn` 使用権限、割り当て `true` から `UsageRights` オブジェクトの `enableFormFillIn` データメンバー。 （適用する各使用権限に対して、この手順を繰り返します）。

1. 使用権限をPDF文書に適用する。

   * コンストラクタを使用して `ReaderExtensionsOptionSpec` オブジェクトを作成します。このオブジェクトには、Acrobat Reader DC Extensions サービスで必要な実行時オプションが含まれています。
   * を `UsageRights` オブジェクトを `ReaderExtensionsOptionSpec` オブジェクトの `usageRights` データメンバー。
   * Adobe Readerで権限を付与されたPDFドキュメントを開いたときにユーザーに表示されるメッセージを、 `ReaderExtensionsOptionSpec` オブジェクトの `message` データメンバー。
   * を呼び出して、使用権限をPDFドキュメントに適用します。 `ReaderExtensionsServiceClient` オブジェクトの `applyUsageRights` メソッドを使用して、次の値を渡します。

      * この `BLOB` 使用権限が適用されるPDFドキュメントを含むオブジェクト。
      * 使用権限を適用できる秘密鍵証明書のエイリアスを指定する string 値です。
      * 対応するパスワード値を指定する文字列値. ( 現在、このパラメーターは無視されます。 パス `null`.)
   * この `ReaderExtensionsOptionSpec` 実行時オプションを含むオブジェクト。

   この `applyUsageRights` メソッドは、 `BLOB` 権限が有効なPDF・ドキュメントを含むオブジェクト。

1. 権限が有効なPDF文書を保存します。

   * の作成 `System.IO.FileStream` オブジェクトを指定します。 権限を持つPDFドキュメントのファイルの場所を表す string 値を渡します。
   * のデータコンテンツを格納するバイト配列を作成します。 `BLOB` が返したオブジェクト `applyUsageRights` メソッド。 バイト配列を生成するには、 `BLOB` オブジェクトの `MTOM` データメンバー。
   * の作成 `System.IO.BinaryWriter` オブジェクトのコンストラクタを呼び出し、 `System.IO.FileStream` オブジェクト。
   * を呼び出して、バイト配列の内容をPDFファイルに書き込みます。 `System.IO.BinaryWriter` オブジェクトの `Write` メソッドを使用してバイト配列を渡す。

**関連トピック**

[使用権限のPDF・ドキュメントへの適用](assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)

[MTOM を使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRef を使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 使用権限の削除 (PDF・ドキュメント ) {#removing-usage-rights-from-pdf-documents}

使用権限を付与されたドキュメントから使用権限を削除できます。 使用権限を有効にしたPDFドキュメントから使用権限を削除して、その他のAEM Forms操作を実行する必要もあります。 例えば、PDF ドキュメントに対する電子署名（または認証）は、使用権限を設定する前に実行する必要があります。したがって、権限を持つドキュメントに対して操作を実行する場合は、PDFドキュメントから使用権限を削除し、ドキュメントの電子署名など他の操作を実行してから、ドキュメントに使用権限を再適用する必要があります。

>[!NOTE]
>
>Acrobat Reader DC Extensions サービスについて詳しくは、 [AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary_of_steps-1}

使用権限を付与されたPDF・ドキュメントから削除するには、次の手順に従います。

1. プロジェクトファイルを含めます。
1. Acrobat Reader DC Extensions クライアントオブジェクトを作成します。
1. 権限が有効なPDF文書の取得
1. 使用権限をPDF文書から削除
1. PDF文書を保存します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。 Web サービスを使用している場合は、プロキシファイルを必ず含めてください。

**Acrobat Reader DC Extensions クライアントオブジェクトの作成**

Acrobat Reader DC Extensions Service の操作をプログラムで実行する前に、Acrobat Reader DC Extensions Service のクライアントオブジェクトを作成する必要があります。 Java API を使用している場合は、 `ReaderExtensionsServiceClient` オブジェクト。 Acrobat Reader DC拡張機能 Web サービス API を使用している場合は、 `ReaderExtensionsServiceService` オブジェクト。

**権限が有効なPDF文書の取得**

使用権限を削除するために、権限が有効なPDFドキュメントを取得します。

**使用権限をPDF文書から削除**

権限が設定されたPDFドキュメントを取得したら、使用権限を削除できます。 使用権限を削除すると、Adobe Reader内でPDFを表示している間、その使用権限ドキュメントに追加の機能が追加されなくなります。

**PDF文書を保存**

usage-rights が含まれなくなったPDFドキュメントをPDFファイルとして保存できます。 PDFドキュメントをPDFファイルとして保存すると、Adobe ReaderまたはAcrobatで表示できます。

**関連トピック**

[Java API を使用して使用権限を削除する](assigning-usage-rights.md#remove-usage-rights-using-the-java-api)

[Web サービス API を使用して使用権限を削除する](assigning-usage-rights.md#remove-usage-rights-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Acrobat Reader DC Extensions Service API クイックスタート](/help/forms/developing/acrobat-reader-dc-extensions-service.md#acrobat-reader-dc-extensions-service-java-api-quick-start-soap)

[使用権限のPDF・ドキュメントへの適用](assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)

### Java API を使用して使用権限を削除する {#remove-usage-rights-using-the-java-api}

Acrobat Reader DC Extensions API(Java) を使用して、権限を持つPDFドキュメントから使用権限を削除します。

1. プロジェクトファイルを含めます。

   Java プロジェクトのクラスパスに、adobe-reader-extensions-client.jar などのクライアント JAR ファイルを含めます。

1. Acrobat Reader DC Extensions クライアントオブジェクトを作成します。

   の作成 `ReaderExtensionsServiceClient` オブジェクトのコンストラクタを使用し、 `ServiceClientFactory` 接続プロパティを含むオブジェクト。

1. PDF文書を取得

   * の作成 `java.io.FileInputStream` コンストラクタを使用し、PDFドキュメントの場所を指定する string 値を渡すことによって、権限を持つPDFドキュメントを表すオブジェクト。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. 使用権限をPDF文書から削除

   を呼び出して、使用権限をPDFドキュメントから削除します。 `ReaderExtensionsServiceClient` オブジェクトの `removeUsageRights` メソッドおよび `com.adobe.idp.Document` 権限が有効なPDF・ドキュメントを含むオブジェクト。 このメソッドは、 `com.adobe.idp.Document` 使用権限のないPDFドキュメントを含むオブジェクト。

1. 使用権限をPDF文書に適用する。

   * の作成 `java.io.File` オブジェクトに置き換え、ファイル拡張子が。PDF。
   * を呼び出す `Document` オブジェクトの `copyToFile` メソッドを使用して、 `Document` オブジェクトをファイルに追加します ( `Document` が返したオブジェクト `removeUsageRights` メソッド )。

**関連トピック**

[使用権限の削除 (PDF・ドキュメント )](assigning-usage-rights.md#removing-usage-rights-from-pdf-documents)

[クイックスタート（SOAP モード）:Java API を使用したPDFドキュメントからの使用権限の削除](/help/forms/developing/acrobat-reader-dc-extensions-service.md#quick-start-soap-mode-removing-usage-rights-from-a-pdf-document-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Web サービス API を使用して使用権限を削除する {#remove-usage-rights-using-the-web-service-api}

Acrobat Reader DC Extensions API（Web サービス）を使用して、権限を付与されたPDFドキュメントから使用権限を削除します。

1. プロジェクトファイルを含めます。

   MTOM を使用するMicrosoft .NET プロジェクトを作成します。 次の WSDL 定義を使用していることを確認します。 `http://localhost:8080/soap/services/ReaderExtensionsService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >置換 `localhost` を、AEM Formsをホストするサーバーの IP アドレスに設定します。

1. Acrobat Reader DC Extensions クライアントオブジェクトを作成します。

   * の作成 `ReaderExtensionsServiceClient` オブジェクトのデフォルトのコンストラクタを使用します。
   * の作成 `ReaderExtensionsServiceClient.Endpoint.Address` オブジェクトを `System.ServiceModel.EndpointAddress` コンストラクタ。 WSDL をAEM Formsサービスに渡す文字列値 ( 例： `http://localhost:8080/soap/services/ReaderExtensionsService?blob=mtom`. 次を指定してください。 `?blob=mtom`.)
   * の作成 `System.ServiceModel.BasicHttpBinding` オブジェクトを作成するには、 `ReaderExtensionsServiceClient.Endpoint.Binding` フィールドに入力します。 戻り値を `BasicHttpBinding` にキャストします。
   * を `System.ServiceModel.BasicHttpBinding` オブジェクトの `MessageEncoding` ～に向かって `WSMessageEncoding.Mtom`. この値は、MTOM が確実に使用されるようにします。
   * 次のタスクを実行して、基本的な HTTP 認証を有効にします。

      * フィールドにAEM forms ユーザー名を割り当てます。 `ReaderExtensionsServiceClient.ClientCredentials.UserName.UserName`.
      * 対応するパスワード値をフィールドに割り当てます。 `ReaderExtensionsServiceClient.ClientCredentials.UserName.Password`.
      * 定数値を割り当て `HttpClientCredentialType.Basic` フィールドに `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 定数値を割り当て `BasicHttpSecurityMode.TransportCredentialOnly` フィールドに `BasicHttpBindingSecurity.Security.Mode`.

1. PDF文書を取得

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。この `BLOB` オブジェクトは、使用権限が削除される権限が有効なPDFドキュメントを保存するために使用されます。
   * の作成 `System.IO.FileStream` オブジェクトを指定します。
   * コンテンツを格納するバイト配列を作成します。 `System.IO.FileStream` オブジェクト。 バイト配列のサイズは、 `System.IO.FileStream` オブジェクトの `Length` プロパティ。
   * を呼び出して、バイト配列にストリームデータを入力します。 `System.IO.FileStream` オブジェクトの `Read` メソッドを使用し、読み込むバイト配列、開始位置、ストリーム長を渡す。
   * 次の項目に `BLOB` オブジェクトを割り当てる `MTOM` プロパティにバイト配列の内容を入力します。

1. 使用権限をPDF文書から削除

   を呼び出して、使用権限をPDFドキュメントから削除します。 `ReaderExtensionsServiceClient` オブジェクトの `removeUsageRights` メソッドおよび `BLOB` 権限が有効なPDF・ドキュメントを含むオブジェクト。 このメソッドは、 `BLOB` 使用権限のないPDFドキュメントを含むオブジェクト。

1. 使用権限をPDF文書に適用する。

   * の作成 `System.IO.FileStream` オブジェクトを作成するには、コンストラクタを呼び出し、PDF・ファイルの場所を表す string 値を渡します。
   * のデータコンテンツを格納するバイト配列を作成します。 `BLOB` が返したオブジェクト `removeUsageRights` メソッド。 バイト配列を生成するには、 `BLOB` オブジェクトの `MTOM` データメンバー。
   * の作成 `System.IO.BinaryWriter` オブジェクトのコンストラクタを呼び出し、 `System.IO.FileStream` オブジェクト。

**関連トピック**

[使用権限の削除 (PDF・ドキュメント )](assigning-usage-rights.md#removing-usage-rights-from-pdf-documents)

[MTOM を使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRef を使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 認証情報の取得 {#retrieving-credential-information}

使用権限を付与された認証ドキュメントに使用権限を適用するために使用されたPDFに関する情報を取得できます。 秘密鍵証明書に関する情報を取得することで、証明書が無効になった日付などの情報を取得できます。

>[!NOTE]
>
>Acrobat Reader DC Extensions サービスについて詳しくは、 [AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary_of_steps-2}

使用権限をPDF・ドキュメントに適用するために使用された秘密鍵証明書に関する情報を取得するには、次の手順に従います。

1. プロジェクトファイルを含めます。
1. Acrobat Reader DC Extensions クライアントオブジェクトを作成します。
1. 権限が有効なPDF文書の取得
1. 秘密鍵証明書に関する情報を取得します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。 Web サービスを使用している場合は、プロキシファイルを必ず含めてください。

**Acrobat Reader DC Extensions クライアントオブジェクトの作成**

Acrobat Reader DC Extensions Service の操作をプログラムで実行する前に、Acrobat Reader DC Extensions Service のクライアントオブジェクトを作成する必要があります。 Java API を使用している場合は、 `ReaderExtensionsServiceClient` オブジェクト。 Acrobat Reader DC拡張機能 Web サービス API を使用している場合は、 `ReaderExtensionsServiceService` オブジェクト。

**権限が有効なPDF文書の取得**

秘密鍵証明書に関する情報を取得するには、権限が有効なPDFドキュメントを取得する必要があります。 エイリアスを指定して、秘密鍵証明書に関する情報を取得することもできます。ただし、使用権限を特定の権限を有効にしたPDFドキュメントに適用するために使用された秘密鍵証明書に関する情報を取得する場合は、ドキュメントを取得する必要があります。

**秘密鍵証明書に関する情報の取得**

権限が有効なPDFドキュメントを取得したら、使用権限を適用するために使用された秘密鍵証明書に関する情報を取得できます。 秘密鍵証明書に関する次の情報を取得できます。

* 権限を付与されたメッセージドキュメントが開かれたときにAdobe Reader内でPDFされるメッセージです。
* 秘密鍵証明書が無効になる日付。
* 秘密鍵証明書が無効な日付です。
* この権限が有効なPDF・ドキュメントに設定された使用権限。
* 秘密鍵証明書が使用された回数。

**関連トピック**

[Java API を使用して使用権限を削除する](assigning-usage-rights.md#remove-usage-rights-using-the-java-api)

[Web サービス API を使用して使用権限を削除する](assigning-usage-rights.md#remove-usage-rights-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Acrobat Reader DC Extensions Service API クイックスタート](/help/forms/developing/acrobat-reader-dc-extensions-service.md#acrobat-reader-dc-extensions-service-java-api-quick-start-soap)

### Java API を使用した資格情報の取得 {#retrieve-credential-information-using-the-java-api}

Acrobat Reader DC Extensions API(Java) を使用して、資格情報を取得します。

1. プロジェクトファイルを含めます。

   Java プロジェクトのクラスパスに、adobe-reader-extensions-client.jar などのクライアント JAR ファイルを含めます。

1. Acrobat Reader DC Extensions クライアントオブジェクトを作成します。

   の作成 `ReaderExtensionsServiceClient` オブジェクトのコンストラクタを使用し、 `ServiceClientFactory` 接続プロパティを含むオブジェクト。

1. PDF文書を取得

   * の作成 `java.io.FileInputStream` コンストラクタを使用し、権限が有効なPDFドキュメントの場所を指定する string 値を渡すことによって、権限が有効なPDFドキュメントを表すオブジェクト。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. 使用権限をPDF文書から削除

   * を呼び出して、使用権限をPDFドキュメントに適用するために使用される秘密鍵証明書に関する情報を取得します。 `ReaderExtensionsServiceClient` オブジェクトの `getDocumentUsageRights` メソッドおよび `com.adobe.idp.Document` 権限が有効なPDF・ドキュメントを含むオブジェクト。 このメソッドは、 `GetUsageRightsResult` 資格情報を含むオブジェクト。
   * を呼び出して、秘密鍵証明書が有効でなくなった日付を取得します。 `GetUsageRightsResult` オブジェクトの `getNotAfter` メソッド。 このメソッドは、 `java.util.Date` 資格情報が有効でなくなる日付を表すオブジェクト。
   * を呼び出して、権限を付与されたPDFドキュメントが開かれたときにAdobe Readerに表示されるメッセージを取得します。 `GetUsageRightsResult` オブジェクトの `getMessage` メソッド。 このメソッドは、メッセージを表す string 値を返します。

**関連トピック**

[認証情報の取得](assigning-usage-rights.md#retrieving-credential-information)

[クイックスタート（SOAP モード）:Java API を使用した資格情報の取得](/help/forms/developing/acrobat-reader-dc-extensions-service.md#quick-start-soap-mode-retrieving-credential-information-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Web サービス API を使用した資格情報の取得 {#retrieve-credential-information-using-the-web-service-api}

Acrobat Reader DC Extensions API（Web サービス）を使用して資格情報を取得します。

1. プロジェクトファイルを含めます。

   MTOM を使用するMicrosoft .NET プロジェクトを作成します。 次の WSDL 定義を使用していることを確認します。 `http://localhost:8080/soap/services/ReaderExtensionsService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >置換 `localhost` を、AEM Formsをホストするサーバーの IP アドレスに設定します。

1. Acrobat Reader DC Extensions クライアントオブジェクトを作成します。

   * の作成 `ReaderExtensionsServiceClient` オブジェクトのデフォルトのコンストラクタを使用します。
   * の作成 `ReaderExtensionsServiceClient.Endpoint.Address` オブジェクトを `System.ServiceModel.EndpointAddress` コンストラクタ。 WSDL をAEM Formsサービスに渡す文字列値 ( 例： `http://localhost:8080/soap/services/ReaderExtensionsService?blob=mtom`. 次を指定してください。 `?blob=mtom`.)
   * の作成 `System.ServiceModel.BasicHttpBinding` オブジェクトを作成するには、 `ReaderExtensionsServiceClient.Endpoint.Binding` フィールドに入力します。 戻り値を `BasicHttpBinding` にキャストします。
   * を `System.ServiceModel.BasicHttpBinding` オブジェクトの `MessageEncoding` ～に向かって `WSMessageEncoding.Mtom`. この値は、MTOM が確実に使用されるようにします。
   * 次のタスクを実行して、基本的な HTTP 認証を有効にします。

      * フィールドにAEM forms ユーザー名を割り当てます。 `ReaderExtensionsServiceClient.ClientCredentials.UserName.UserName`.
      * 対応するパスワード値をフィールドに割り当てます。 `ReaderExtensionsServiceClient.ClientCredentials.UserName.Password`.
      * 定数値を割り当て `HttpClientCredentialType.Basic` フィールドに `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 定数値を割り当て `BasicHttpSecurityMode.TransportCredentialOnly` フィールドに `BasicHttpBindingSecurity.Security.Mode`.

1. PDF文書を取得

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。この `BLOB` オブジェクトは、権限が有効なPDF・ドキュメントの保存に使用されます。
   * の作成 `System.IO.FileStream` オブジェクトを呼び出し、権限を持つPDFドキュメントのファイルの場所と、ファイルを開くモードを表す string 値を渡すことによってオブジェクトを開きます。
   * コンテンツを格納するバイト配列を作成します。 `System.IO.FileStream` オブジェクト。 バイト配列のサイズは、 `System.IO.FileStream` オブジェクトの `Length` プロパティ。
   * を呼び出して、バイト配列にストリームデータを入力します。 `System.IO.FileStream` オブジェクトの `Read` メソッドを使用し、読み込むバイト配列、開始位置、ストリーム長を渡す。
   * 次の項目に `BLOB` オブジェクトを割り当てる `MTOM` プロパティにバイト配列の内容を入力します。

1. 使用権限をPDF文書から削除

   * を呼び出して、使用権限をPDFドキュメントに適用するために使用される秘密鍵証明書に関する情報を取得します。 `ReaderExtensionsServiceClient` オブジェクトの `getDocumentUsageRights` メソッドおよび `com.adobe.idp.Document` 権限が有効なPDF・ドキュメントを含むオブジェクト。 このメソッドは、 `GetUsageRightsResult` 資格情報を含むオブジェクト。
   * 証明書の有効期限が切れた日付を取得するには、 `GetUsageRightsResult` オブジェクトの `notAfter` データメンバー。 このデータメンバーのデータタイプは `System.DateTime`.
   * Adobe Readerで権限が付与されたPDFドキュメントを開いたときに表示されるメッセージを取得するには、 `GetUsageRightsResult` オブジェクトの `message` データメンバー。 このデータメンバーのデータ型は文字列です。
   * 証明書の値を取得して、秘密鍵証明書が使用された回数を取得します。 `GetUsageRightsResult` オブジェクトの `useCount` データメンバー。 このデータメンバーのデータ型は整数です。

**関連トピック**

[認証情報の取得](assigning-usage-rights.md#retrieving-credential-information)

[MTOM を使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRef を使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
