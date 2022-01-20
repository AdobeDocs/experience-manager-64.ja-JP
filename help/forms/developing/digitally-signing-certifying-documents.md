---
title: ドキュメントのデジタル署名と認証
seo-title: Digitally Signing and Certifying Documents
description: Signature サービスを使用して、PDFドキュメントに対する電子署名フィールドの追加と削除、PDFドキュメント内の署名フィールドの名前の取得、署名フィールドの変更、電子署名ドキュメントの認証、PDFドキュメント内の電子署名の検証、署名フィールドからの電子署名の削除を行います。
seo-description: Use the Signature service to add and delete digital signature fields to a PDF document, retrieve the names of signature fields located in a PDF document, modify signature fields, digitally sign PDF documents, certify PDF documents, validate digital signatures located in a PDF document, validate all digital signatures located in a PDF document, and remove a digital signature from a signature field.
uuid: 6331de8a-2a9c-45bf-89d2-29f1ad5cc856
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: operations
discoiquuid: 42de04bf-25e4-4478-a411-38671ed871ae
role: Developer
exl-id: b8488a39-44dd-4e6c-b3f0-857d67c79385
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '17032'
ht-degree: 8%

---

# ドキュメントのデジタル署名と認証 {#digitally-signing-and-certifying-documents}

**Signature サービスについて**

Signature サービスを使用すると、組織は配信および受信するAdobe PDFドキュメントのセキュリティとプライバシーを保護できます。 このサービスでは、電子署名と証明書を使用して、意図された受信者のみがドキュメントを変更できるようにします。 セキュリティ機能がドキュメント自体に適用されるので、ドキュメントは安全で、ライフサイクル全体にわたって制御されます。 ドキュメントは、ファイアウォールの外部、オフラインでダウンロードされた場合、および組織に送り返される場合に、保護された状態のままになります。

>[!NOTE]
>
>PDFドキュメントへの署名など、特定の操作の呼び出し時に呼び出される Signature サービス用のカスタム署名ハンドラーを作成できます。

**署名フィールド名**

一部の Signature サービス操作では、操作を実行する Signature フィールドの名前を指定する必要があります。 例えば、署名ドキュメントにPDFを行う場合、署名する署名フィールドの名前を指定します。 署名フィールドの完全名が `form1[0].Form1[0].SignatureField1[0]`. 次を指定できます。 `SignatureField1[0]` の代わりに `form1[0].Form1[0].SignatureField1[0]`.

競合が原因で、Signature サービスが誤ったフィールドに署名する（または、署名フィールド名を必要とする別の操作を実行する）ことがあります。 この競合は名前の結果です `SignatureField1[0]` 同じPDF文書内の 2 つ以上の場所に表示される 例えば、PDFドキュメントに、 `form1[0].Form1[0].SignatureField1[0]` および `form1[0].Form1[0].SubForm1[0].SignatureField1[0]` と入力し、 `SignatureField1[0]`. この場合、Signature サービスは、ドキュメント内のすべての署名フィールドを繰り返し処理する際に検出された最初の署名フィールドに署名します。

1 つの署名ドキュメント内に複数のPDFフィールドがある場合は、署名フィールドの完全名を指定することをお勧めします。 つまり、 `form1[0].Form1[0].SignatureField1[0]`の代わりに `SignatureField1[0]`.

Signature サービスを使用して、次のタスクを実行できます。

* 署名ドキュメントへの電子署名フィールドの追加およびPDF削除を行います。 ( [署名フィールドの追加](digitally-signing-certifying-documents.md#adding-signature-fields).)
* 署名ドキュメント内の署名フィールドの名前をPDFします。 ( [署名フィールド名の取得](digitally-signing-certifying-documents.md#retrieving-signature-field-names).)
* 署名フィールドを変更します。 ( [署名フィールドの変更](digitally-signing-certifying-documents.md#modifying-signature-fields).)
* デジタル署名PDFドキュメント。 ( [デジタル署名PDF文書](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents).)
* PDF文書を認証します。 ( [認証PDF書](digitally-signing-certifying-documents.md#certifying-pdf-documents).)
* 署名ドキュメント内の電子署名をPDFします。 ( [電子署名の検証](#unresolvedlink-lc-si).)
* PDF・ドキュメント内のすべての電子署名を検証します。 ( [複数のデジタル署名の検証](#unresolvedlink-lc-si).)
* 署名フィールドから電子署名を削除します。 ( [電子署名の削除](digitally-signing-certifying-documents.md#removing-digital-signatures).)

>[!NOTE]
>
>Signature サービスについて詳しくは、 [AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63).

## 署名フィールドの追加 {#adding-signature-fields}

電子署名は、署名のグラフィック表現を含むフォームフィールドである署名フィールドに表示されます。 署名フィールドは、表示または非表示に設定することができます。署名者は、既存の署名フィールドを使用することも、プログラムによって署名フィールドを追加することもできます。 どちらの場合においても、PDF ドキュメントに署名できるようにするには、署名フィールドが存在している必要があります。

プログラムによって署名フィールドを追加するには、Signature サービス Java API や 署名 Web サービス API を使用します。署名ドキュメントには、複数の署名フィールドをPDFできます。ただし、各署名フィールド名は一意である必要があります。

>[!NOTE]
>
>一部のPDFドキュメントタイプでは、プログラムによって署名フィールドを追加できません。 Signature サービスと署名フィールドの追加について詳しくは、 [AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary-of-steps}

署名ドキュメントに署名フィールドをPDFするには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. Signature クライアントを作成します。
1. 署名フィールドが追加されたPDFドキュメントを取得します。
1. 署名フィールドを追加します。
1. PDF・ドキュメントをPDF・ファイルとして保存します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。 Web サービスを使用している場合は、プロキシファイルを必ず含めてください。

次の JAR ファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar(AEM Formsを JBoss にデプロイする場合に必要 )
* jbossall-client.jar(AEM Formsが JBoss にデプロイされている場合に必要 )

**署名クライアントの作成**

Signature サービスの操作をプログラムで実行する前に、Signature サービスクライアントを作成する必要があります。

**署名フィールドが追加されたPDFドキュメントを取得する**

署名フィールドを追加したPDFドキュメントを取得する必要があります。

**署名フィールドの追加**

署名フィールドをPDFドキュメントに正常に追加するには、署名フィールドの場所を識別する座標値を指定します。 （非表示の署名フィールドを追加する場合、これらの値は不要です）。 また、署名が署名フィールドに適用された後にロックされるPDFドキュメント内のフィールドを指定することもできます。

**PDFドキュメントをPDFファイルとして保存**

Signature サービスがPDFドキュメントに署名フィールドを追加した後、そのドキュメントをPDFファイルとして保存し、AcrobatまたはAdobe Readerで開くことができます。

**関連トピック**

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[デジタル署名PDF文書](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)

### Java API を使用した署名フィールドの追加 {#add-signature-fields-using-the-java-api}

署名 API(Java) を使用して署名フィールドを追加します。

1. プロジェクトファイルを含める

   Java プロジェクトのクラスパスに、adobe-signatures-client.jar などのクライアント JAR ファイルを含めます。

1. 署名クライアントの作成

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用して `SignatureServiceClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. 署名フィールドが追加されたPDFドキュメントを取得する

   * の作成 `java.io.FileInputStream` PDFフィールドが追加される署名ドキュメントを表すオブジェクト。PDFドキュメントの場所を指定する string 値を渡すコンストラクターを使用します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. 署名フィールドの追加

   * の作成 `PositionRectangle` コンストラクタを使用して署名フィールドの場所を指定するオブジェクト。 コンストラクタ内で、座標値を指定します。
   * 必要に応じて、 `FieldMDPOptions` 電子署名が署名フィールドに適用されたときにロックされるフィールドを指定するオブジェクトです。
   * を呼び出して、PDFドキュメントに署名フィールドを追加する `SignatureServiceClient` オブジェクトの `addSignatureField` メソッドを使用して、次の値を渡します。

      * A `com.adobe.idp`. `Document` 署名フィールドを追加するPDFドキュメントを表すオブジェクト。
      * 署名フィールドの名前を指定する string 値です。
      * A `java.lang.Integer` 署名フィールドを追加するページ番号を表す値です。
      * A `PositionRectangle` 署名フィールドの場所を指定するオブジェクト。
      * A `FieldMDPOptions` 電子署名がPDFフィールドに適用された後にロックされる署名ドキュメント内のフィールドを指定するオブジェクト。 このパラメータ値はオプションで、 `null`.
   * A `PDFSeedValueOptions` 様々な実行時の値を指定するオブジェクト。 このパラメータ値はオプションで、 `null`.

      この `addSignatureField` メソッドは、 `com.adobe.idp`. `Document` 署名フィールドを含むPDFドキュメントを表すオブジェクト。
   >[!NOTE]
   >
   >を呼び出すことができます。 `SignatureServiceClient` オブジェクトの `addInvisibleSignatureField` メソッドを使用して、非表示の署名フィールドを追加します。

1. PDFドキュメントをPDFファイルとして保存

   * `java.io.File` オブジェクトを作成し、ファイル拡張子が .pdf であることを確認します。
   * を呼び出す `com.adobe.idp`. `Document` オブジェクトの `copyToFile` メソッドを使用して、 `Document` オブジェクトをファイルに追加します。 必ず `com.adobe.idp`. `Document` が返したオブジェクト `addSignatureField` メソッド。

**関連トピック**

[Signature Service API クイックスタート](/help/forms/developing/signature-service-java-api-quick.md#signature-service-java-api-quick-start-soap)

### Web サービス API を使用した署名フィールドの追加 {#add-signature-fields-using-the-web-service-api}

Signature API（Web サービス）を使用して署名フィールドを追加するには：

1. プロジェクトファイルを含める

   MTOM を使用するMicrosoft .NET プロジェクトを作成します。 次の WSDL 定義を使用していることを確認します。 `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >置換 `localhost` を、AEM Formsをホストするサーバーの IP アドレスに設定します。

1. 署名クライアントの作成

   * の作成 `SignatureServiceClient` オブジェクトのデフォルトのコンストラクタを使用します。
   * の作成 `SignatureServiceClient.Endpoint.Address` オブジェクトを `System.ServiceModel.EndpointAddress` コンストラクタ。 WSDL をAEM Formsサービスに渡す文字列値 ( 例： `http://localhost:8080/soap/services/SignatureService?WSDL`) をクリックします。 を使用する必要はありません。 `lc_version` 属性。 この属性は、サービス参照を作成する際に使用されます )。
   * の作成 `System.ServiceModel.BasicHttpBinding` オブジェクトを作成するには、 `SignatureServiceClient.Endpoint.Binding` フィールドに入力します。 戻り値を `BasicHttpBinding` にキャストします。
   * を `System.ServiceModel.BasicHttpBinding` オブジェクトの `MessageEncoding` ～に向かって `WSMessageEncoding.Mtom`. この値は、MTOM が確実に使用されるようにします。
   * 次のタスクを実行して、基本的な HTTP 認証を有効にします。

      * フィールドにAEM forms ユーザー名を割り当てます。 `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * 対応するパスワード値をフィールドに割り当てます。 `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * 定数値を割り当て `HttpClientCredentialType.Basic` フィールドに `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 定数値を割り当て `BasicHttpSecurityMode.TransportCredentialOnly` フィールドに `BasicHttpBindingSecurity.Security.Mode`.

1. 署名フィールドが追加されたPDFドキュメントを取得する

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。この `BLOB` オブジェクトは、署名フィールドを含むPDFドキュメントを保存するために使用されます。
   * の作成 `System.IO.FileStream` オブジェクトを指定します。
   * コンテンツを格納するバイト配列を作成します。 `System.IO.FileStream` オブジェクト。 バイト配列のサイズは、 `System.IO.FileStream` オブジェクトの `Length` プロパティ。
   * を呼び出して、バイト配列にストリームデータを入力します。 `System.IO.FileStream` オブジェクトの `Read` メソッドを使用し、読み込むバイト配列、開始位置、ストリーム長を渡す。
   * 次の項目に `BLOB` オブジェクトを割り当てる `MTOM` プロパティにバイト配列の内容を入力します。

1. 署名フィールドの追加

   を呼び出して、PDFドキュメントに署名フィールドを追加する `SignatureServiceClient` オブジェクトの `addSignatureField` メソッドを使用して、次の値を渡します。

   * A `BLOB` 署名フィールドを追加するPDFドキュメントを表すオブジェクト。
   * 署名フィールド名を指定する string 値です。
   * 署名フィールドを追加するページ番号を表す integer 値です。
   * A `PositionRect` 署名フィールドの場所を指定するオブジェクト。
   * A `FieldMDPOptions` 電子署名がPDFフィールドに適用された後にロックされる署名ドキュメント内のフィールドを指定するオブジェクト。 このパラメータ値はオプションで、 `null`.
   * A `PDFSeedValueOptions` 様々な実行時の値を指定するオブジェクト。 このパラメータ値はオプションで、 `null`.

   この `addSignatureField` メソッドは、 `BLOB` 署名フィールドを含むPDFドキュメントを表すオブジェクト。

1. PDFドキュメントをPDFファイルとして保存

   * の作成 `System.IO.FileStream` オブジェクトを呼び出し、PDFフィールドを含む署名ドキュメントのファイルの場所と、ファイルを開くモードを表す string 値を渡すことによって、オブジェクトを指定します。
   * コンテンツを格納するバイト配列を作成します。 `BLOB` が返したオブジェクト `addSignatureField` メソッド。 バイト配列を生成するには、 `BLOB` オブジェクトの `binaryData` データメンバー。
   * の作成 `System.IO.BinaryWriter` オブジェクトのコンストラクタを呼び出し、 `System.IO.FileStream` オブジェクト。
   * を呼び出して、バイト配列の内容をPDFファイルに書き込みます。 `System.IO.BinaryWriter` オブジェクトの `Write` メソッドを使用してバイト配列を渡す。

**関連トピック**

[MTOM を使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRef を使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 署名フィールド名の取得 {#retrieving-signature-field-names}

署名または認証する PDF ドキュメント内のすべての署名フィールドの名前を取得できます。PDF ドキュメント内の署名フィールド名が分からない場合や、名前を検証したい場合に、プログラムによって名前を取得することができます。Signature サービスは、次のような署名フィールドの完全修飾名を返します。 `form1[0].grantApplication[0].page1[0].SignatureField1[0]`.

>[!NOTE]
>
>Signature サービスについて詳しくは、 [AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)

### 手順の概要 {#summary_of_steps-1}

署名フィールド名を取得するには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. Signature クライアントを作成します。
1. 署名フィールドを含むPDFドキュメントを取得します。
1. 署名フィールド名を取得します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。 Web サービスを使用している場合は、プロキシファイルを必ず含めてください。

次の JAR ファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar(AEM Formsを JBoss にデプロイする場合に必要 )
* jbossall-client.jar(AEM Formsが JBoss にデプロイされている場合に必要 )

これらの JAR ファイルの場所について詳しくは、 [AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**署名クライアントの作成**

Signature サービスの操作をプログラムで実行する前に、Signature サービスクライアントを作成する必要があります。

**署名フィールドを含むPDFドキュメントを取得する**

署名フィールドを含むPDFドキュメントを取得します。

**署名フィールド名の取得**

1 つ以上の署名フィールドを含むPDFドキュメントを取得した後で、署名フィールド名を取得できます。

**関連トピック**

[Java API を使用した署名フィールド名の取得](digitally-signing-certifying-documents.md#retrieve-signature-field-names-using-the-java-api)

[Web サービス API を使用した署名フィールドの取得](digitally-signing-certifying-documents.md#retrieve-signature-field-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[署名フィールドの追加](digitally-signing-certifying-documents.md#adding-signature-fields)

### Java API を使用した署名フィールド名の取得 {#retrieve-signature-field-names-using-the-java-api}

Signature API(Java) を使用して署名フィールド名を取得します。

1. プロジェクトファイルを含める

   Java プロジェクトのクラスパスに、 adobe-signatures-client.jar などのクライアント JAR ファイルを含めます。

1. 署名クライアントの作成

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用して `SignatureServiceClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. 署名フィールドを含むPDFドキュメントを取得する

   * の作成 `java.io.FileInputStream` コンストラクタを使用し、PDFドキュメントの場所を指定する string 値を渡すことによって、PDFフィールドを含む署名ドキュメントを表すオブジェクト。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. 署名フィールド名の取得

   * を呼び出して、署名フィールド名を取得します。 `SignatureServiceClient` オブジェクトの `getSignatureFieldList` メソッドおよび `com.adobe.idp.Document` 署名フィールドを含むPDFドキュメントを格納するオブジェクト。 このメソッドは、 `java.util.List` 各要素に `PDFSignatureField` オブジェクト。 このオブジェクトを使用すると、署名フィールドが表示されているかどうかなど、署名フィールドに関する追加情報を取得できます。
   * 反復処理 `java.util.List` オブジェクトを使用して、署名フィールド名があるかどうかを確認します。 PDFドキュメントの各署名フィールドに対して、 `PDFSignatureField` オブジェクト。 署名フィールドの名前を取得するには、 `PDFSignatureField` オブジェクトの `getName` メソッド。 このメソッドは、署名フィールド名を指定する文字列値を返します。

**関連トピック**

[署名フィールド名の取得](digitally-signing-certifying-documents.md#retrieving-signature-field-names)

[クイックスタート（SOAP モード）:Java API を使用した署名フィールド名の取得](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-retrieving-signature-field-names-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Web サービス API を使用した署名フィールドの取得 {#retrieve-signature-field-using-the-web-service-api}

Signature API（Web サービス）を使用して署名フィールド名を取得します。

1. プロジェクトファイルを含める

   MTOM を使用するMicrosoft .NET プロジェクトを作成します。 次の WSDL 定義を使用していることを確認します。 `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >置換 `localhost` を、AEM Formsをホストするサーバーの IP アドレスに設定します。

1. 署名クライアントの作成

   * の作成 `SignatureServiceClient` オブジェクトのデフォルトのコンストラクタを使用します。
   * の作成 `SignatureServiceClient.Endpoint.Address` オブジェクトを `System.ServiceModel.EndpointAddress` コンストラクタ。 WSDL をAEM Formsサービスに渡す文字列値 ( 例： `http://localhost:8080/soap/services/SignatureService?WSDL`) をクリックします。 を使用する必要はありません。 `lc_version` 属性。 この属性は、サービス参照を作成する際に使用されます )。
   * の作成 `System.ServiceModel.BasicHttpBinding` オブジェクトを作成するには、 `SignatureServiceClient.Endpoint.Binding` フィールドに入力します。 戻り値を `BasicHttpBinding` にキャストします。
   * を `System.ServiceModel.BasicHttpBinding` オブジェクトの `MessageEncoding` ～に向かって `WSMessageEncoding.Mtom`. この値は、MTOM が確実に使用されるようにします。
   * 次のタスクを実行して、基本的な HTTP 認証を有効にします。

      * フィールドにAEM forms ユーザー名を割り当てます。 `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * 対応するパスワード値をフィールドに割り当てます。 `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * 定数値を割り当て `HttpClientCredentialType.Basic` フィールドに `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 定数値を割り当て `BasicHttpSecurityMode.TransportCredentialOnly` フィールドに `BasicHttpBindingSecurity.Security.Mode`.

1. 署名フィールドを含むPDFドキュメントを取得する

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。この `BLOB` オブジェクトは、署名フィールドを含むPDFドキュメントを保存するために使用されます。
   * の作成 `System.IO.FileStream` オブジェクトを指定します。
   * コンテンツを格納するバイト配列を作成します。 `System.IO.FileStream` オブジェクト。 バイト配列のサイズは、 `System.IO.FileStream` オブジェクトの `Length` プロパティ。
   * を呼び出して、バイト配列にストリームデータを入力します。 `System.IO.FileStream` オブジェクトの `Read` メソッドを使用し、読み込むバイト配列、開始位置、ストリーム長を渡す。
   * 次の項目に `BLOB` オブジェクトを割り当てる `MTOM` フィールドにバイト配列の内容を入力します。

1. 署名フィールド名の取得

   * を呼び出して署名フィールド名を取得する `SignatureServiceClient` オブジェクトの `getSignatureFieldList` メソッドおよび `BLOB` 署名フィールドを含むPDFドキュメントを格納するオブジェクト。 このメソッドは、 `MyArrayOfPDFSignatureField` 各要素に `PDFSignatureField` オブジェクト。
   * 反復処理 `MyArrayOfPDFSignatureField` オブジェクトを使用して、署名フィールド名があるかどうかを確認します。 PDFドキュメントの各署名フィールドについて、 `PDFSignatureField` オブジェクト。 署名フィールドの名前を取得するには、 `PDFSignatureField` オブジェクトの `getName` メソッド。 このメソッドは、署名フィールド名を指定する文字列値を返します。

**関連トピック**

[署名フィールド名の取得](digitally-signing-certifying-documents.md#retrieving-signature-field-names)

[MTOM を使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRef を使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 署名フィールドの変更 {#modifying-signature-fields}

Java API と Web サービス API を使用して、PDFドキュメント内の署名フィールドを変更できます。 署名フィールドの署名フィールドロックディクショナリまたはシード値ディクショナリの値を操作することで署名フィールドを変更します。

A *フィールドロック辞書* 署名フィールドが署名されたときにロックされるフィールドのリストを指定します。 フィールドがロックされると、ユーザーはフィールドを変更できません。A *シード値ディクショナリ* には、署名の適用時に使用される制約情報が含まれます。 例えば、署名を無効にすることなく実行できるアクションを制御する権限設定を変更することができます。

既存の署名フィールドを変更すると、ビジネス要件の変更を反映するようにPDFドキュメントを変更できます。 例えば、新しいビジネス要件では、ドキュメントの署名後にすべてのドキュメントフィールドをロックする必要が生じる場合があります。

この節では、フィールドロックディクショナリとシード値ディクショナリの値の両方を変更して署名フィールドを変更する方法について説明します。 署名フィールドロックディクショナリに変更を加えると、PDFドキュメント内のすべてのフィールドが、署名フィールドに署名する際にロックされます。 シード値ディクショナリを変更すると、ドキュメントに対する特定の種類の変更が禁止されます。

>[!NOTE]
>
>Signature サービスと署名フィールドの変更について詳しくは、 [AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary_of_steps-2}

署名ドキュメント内の署名フィールドを変更するには、次のPDFを実行します。

1. プロジェクトファイルを含めます。
1. Signature クライアントを作成します。
1. 変更するPDFフィールドを含む署名ドキュメントを取得します。
1. 辞書の値を設定します。
1. 署名フィールドを変更します。
1. PDF・ドキュメントをPDF・ファイルとして保存します。

**プロジェクトファイルを含める**

開発プロジェクトに必要なファイルを含めます。 Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。 Web サービスを使用している場合は、プロキシファイルを必ず含めてください。

次の JAR ファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar(AEM Formsを JBoss にデプロイする場合に必要 )
* jbossall-client.jar(AEM Formsが JBoss にデプロイされている場合に必要 )

これらの JAR ファイルの場所について詳しくは、 [LiveCycleJava ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**署名クライアントの作成**

Signature サービスの操作をプログラムで実行する前に、Signature サービスクライアントを作成する必要があります。

**変更するPDFフィールドを含む署名ドキュメントを取得します**

変更するPDFフィールドを含む署名ドキュメントを取得します。

**辞書の値を設定**

署名フィールドを変更するには、そのフィールドロックディクショナリまたはシード値ディクショナリに値を割り当てます。 署名フィールドのロックディクショナリ値を指定するには、PDFフィールドが署名されたときにロックされる署名ドキュメントフィールドを指定する必要があります。 （このセクションでは、すべてのフィールドをロックする方法について説明します）。

次のシード値ディクショナリ値を設定できます。

* **リビジョンの確認**:署名フィールドに署名が適用された場合に失効確認を実行するかどうかを指定します。
* **証明書オプション**:証明書のシード値ディクショナリに値を割り当てます。 証明書のオプションを指定する前に、証明書のシード値ディクショナリに慣れておくことをお勧めします。 ( [PDF参照](https://www.adobe.com/devnet/acrobat/pdfs/pdf_reference_1-7.pdf).)
* **ダイジェストオプション**:署名に使用するダイジェストアルゴリズムを割り当てます。 有効な値は、SHA1、SHA256、SHA384、SHA512、RIPEMD160 です。
* **フィルター**:署名フィールドで使用するフィルタを指定します。 例えば、Adobe.PPKLite フィルターを使用できます。 ( [PDF参照](https://www.adobe.com/devnet/acrobat/pdfs/pdf_reference_1-7.pdf).)
* **フラグオプション**:この署名フィールドに関連付けられているフラグ値を指定します。 値が 1 の場合、署名者は指定された値のみをエントリに使用する必要があります。 値 0 は、他の値が許可されることを意味します。 ビット位置は次のとおりです。

   * **1（フィルター）:** 署名フィールドへの署名に使用する署名ハンドラー
   * **2 （サブフィルタ）:** 署名時に使用する有効なエンコードを示す名前の配列
   * **3 (V)**:署名フィールドへの署名に使用する署名ハンドラーの必要最小限のバージョン番号です
   * **4 （理由）:** ドキュメントに署名する理由を指定する文字列の配列
   * **5 (PDFLegalWarnings):** 可能な法的証明を指定する文字列の配列

* **法的証明**:ドキュメントを認証すると、ドキュメントの表示内容をあいまいにしたり誤解を招く可能性のある特定の種類のコンテンツが自動的にスキャンされます。 例えば、注釈を使用すると、認証対象を理解する上で重要なテキストが難読化される場合があります。 スキャン処理によって、このタイプのコンテンツの存在を示す警告が生成されます。 また、警告が発生した可能性のあるコンテンツに関する追加の説明も提供されます。
* **権限**:署名を無効にせずに、署名ドキュメントでPDFできる権限を指定します。
* **理由**:このドキュメントに署名する必要がある理由を指定します。
* **タイムスタンプ**:タイムスタンプオプションを指定します。 例えば、使用するタイムスタンプサーバーの URL を設定できます。
* **バージョン**:署名フィールドへの署名に使用する署名ハンドラーの最小バージョン番号を指定します。

**署名フィールドの変更**

Signature サービスクライアントを作成し、変更するPDFフィールドが含まれている署名ドキュメントを取得して、辞書の値を設定した後、Signature サービスに対して、署名フィールドを変更するように指示できます。 次に、Signature サービスは、変更されたPDFフィールドを含む署名ドキュメントを返します。 元のPDFドキュメントは影響を受けません。

**PDFドキュメントをPDFファイルとして保存**

変更されたPDFフィールドを含む署名ドキュメントをPDFファイルとして保存し、AcrobatまたはAdobe Readerで開けるようにします。

**関連トピック**

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Signature Service API クイックスタート](/help/forms/developing/signature-service-java-api-quick.md#signature-service-java-api-quick-start-soap)

[デジタル署名PDF文書](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)

### Java API を使用した署名フィールドの変更 {#modify-signature-fields-using-the-java-api}

署名 API(Java) を使用して署名フィールドを変更します。

1. プロジェクトファイルを含める

   Java プロジェクトのクラスパスに、adobe-signatures-client.jar などのクライアント JAR ファイルを含めます。

1. 署名クライアントの作成

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用して `SignatureServiceClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. 変更するPDFフィールドを含む署名ドキュメントを取得します

   * の作成 `java.io.FileInputStream` コンストラクタを使用し、PDFドキュメントの場所を指定する string 値を渡すことで、変更するPDFフィールドを含む署名ドキュメントを表すオブジェクト。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. 辞書の値を設定

   * コンストラクタを使用して `PDFSignatureFieldProperties` オブジェクトを作成します。A `PDFSignatureFieldProperties` オブジェクトは、署名フィールドロックディクショナリとシード値ディクショナリ情報を格納します。
   * コンストラクタを使用して `PDFSeedValueOptionSpec` オブジェクトを作成します。このオブジェクトを使用すると、シード値ディクショナリの値を設定できます。
   * を呼び出して、PDFドキュメントの変更を許可しない `PDFSeedValueOptionSpec` オブジェクトの `setMdpValue` メソッドおよび `MDPPermissions.NoChanges` 列挙値。
   * コンストラクタを使用して `FieldMDPOptionSpec` オブジェクトを作成します。このオブジェクトを使用すると、署名フィールドのロックディクショナリ値を設定できます。
   * を呼び出して、PDFドキュメント内のすべてのフィールドをロックする `FieldMDPOptionSpec` オブジェクトの `setMdpValue` メソッドおよび `FieldMDPAction.ALL` 列挙値。
   * を呼び出して、シード値のディクショナリ情報を設定します。 `PDFSignatureFieldProperties` オブジェクトの `setSeedValue` メソッドおよび `PDFSeedValueOptionSpec` オブジェクト。
   * を呼び出して、署名フィールドロック辞書情報を設定します。 `PDFSignatureFieldProperties`オブジェクトの `setFieldMDP` メソッドおよび `FieldMDPOptionSpec` オブジェクト。

   >[!NOTE]
   >
   >設定可能なすべてのシード値ディクショナリの値を確認するには、 `PDFSeedValueOptionSpec` クラス参照。 ( [AEM Forms API リファレンス](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).)

1. 署名フィールドの変更

   を呼び出して署名フィールドを変更する `SignatureServiceClient` オブジェクトの `modifySignatureField` メソッドを使用して、次の値を渡します。

   * この `com.adobe.idp.Document` 変更するPDFフィールドを含む署名ドキュメントを格納するオブジェクト
   * 署名フィールドの名前を指定する string 値です
   * この `PDFSignatureFieldProperties` 署名フィールドロックディクショナリとシード値ディクショナリ情報を格納するオブジェクト

   この `modifySignatureField` メソッドは、 `com.adobe.idp.Document` 変更されたPDFフィールドを含む署名ドキュメントを保存するオブジェクト。

1. PDFドキュメントをPDFファイルとして保存

   * の作成 `java.io.File` オブジェクトにマッピングされ、ファイル名の拡張子が.pdf であることを確認します。
   * を呼び出す `com.adobe.idp.Document` オブジェクトの `copyToFile` メソッドを使用して、 `com.adobe.idp.Document` オブジェクトをファイルに追加します。 必ず `com.adobe.idp.Document` オブジェクト `modifySignatureField` メソッドが返されました。

### Web サービス API を使用した署名フィールドの変更 {#modify-signature-fields-using-the-web-service-api}

Signature API（Web サービス）を使用して署名フィールドを変更します。

1. プロジェクトファイルを含める

   MTOM を使用するMicrosoft .NET プロジェクトを作成します。 次の WSDL 定義を使用していることを確認します。 `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >置換 `localhost` を、AEM Formsをホストするサーバーの IP アドレスに設定します。

1. 署名クライアントの作成

   * の作成 `SignatureServiceClient` オブジェクトのデフォルトのコンストラクタを使用します。
   * の作成 `SignatureServiceClient.Endpoint.Address` オブジェクトを `System.ServiceModel.EndpointAddress` コンストラクタ。 WSDL をAEM Formsサービスに渡す文字列値 ( 例： `http://localhost:8080/soap/services/SignatureService?WSDL`) をクリックします。 を使用する必要はありません。 `lc_version` 属性。 この属性は、サービス参照を作成する際に使用されます )。
   * の作成 `System.ServiceModel.BasicHttpBinding` オブジェクトを作成するには、 `SignatureServiceClient.Endpoint.Binding` フィールドに入力します。 戻り値を `BasicHttpBinding` にキャストします。
   * を `System.ServiceModel.BasicHttpBinding` オブジェクトの `MessageEncoding` ～に向かって `WSMessageEncoding.Mtom`. この値は、MTOM が確実に使用されるようにします。
   * 次のタスクを実行して、基本的な HTTP 認証を有効にします。

      * フィールドにAEM forms ユーザー名を割り当てます。 `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * 対応するパスワード値をフィールドに割り当てます。 `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * 定数値を割り当て `HttpClientCredentialType.Basic` フィールドに `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 定数値を割り当て `BasicHttpSecurityMode.TransportCredentialOnly` フィールドに `BasicHttpBindingSecurity.Security.Mode`.

1. 変更するPDFフィールドを含む署名ドキュメントを取得します

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。この `BLOB` オブジェクトは、変更する署名フィールドを含むPDFドキュメントを保存するために使用されます。
   * の作成 `System.IO.FileStream` オブジェクトを指定します。
   * コンテンツを格納するバイト配列を作成します。 `System.IO.FileStream` オブジェクト。 バイト配列のサイズは、 `System.IO.FileStream` オブジェクトの `Length` プロパティ。
   * を呼び出して、バイト配列にストリームデータを入力します。 `System.IO.FileStream` オブジェクトの `Read` メソッドを使用し、読み込むバイト配列、開始位置、ストリーム長を渡す。
   * 次の項目に `BLOB` オブジェクトを割り当てる `MTOM` プロパティは、バイト配列の内容を示します。

1. 辞書の値を設定

   * コンストラクタを使用して `PDFSignatureFieldProperties` オブジェクトを作成します。このオブジェクトは、署名フィールドロックディクショナリとシード値ディクショナリ情報を格納します。
   * コンストラクタを使用して `PDFSeedValueOptionSpec` オブジェクトを作成します。このオブジェクトを使用すると、シード値ディクショナリの値を設定できます。
   * 割り当てによってPDFドキュメントに変更を許可しない `MDPPermissions.NoChanges` 列挙値を `PDFSeedValueOptionSpec` オブジェクトの `mdpValue` データメンバー。
   * コンストラクタを使用して `FieldMDPOptionSpec` オブジェクトを作成します。このオブジェクトを使用すると、署名フィールドのロックディクショナリ値を設定できます。
   * 割り当てによってPDFドキュメント内のすべてのフィールドをロックする `FieldMDPAction.ALL` 列挙値を `FieldMDPOptionSpec` オブジェクトの `mdpValue` データメンバー。
   * シード値ディクショナリ情報を設定するには、 `PDFSeedValueOptionSpec` オブジェクトを `PDFSignatureFieldProperties` オブジェクトの `seedValue` データメンバー。
   * 署名フィールドロック辞書情報を設定するには、 `FieldMDPOptionSpec` オブジェクトを `PDFSignatureFieldProperties` オブジェクトの `fieldMDP` データメンバー。

   >[!NOTE]
   >
   >設定可能なすべてのシード値ディクショナリの値を確認するには、 `PDFSeedValueOptionSpec` クラス参照。 ( [AEM Forms API リファレンス](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)) をクリックします。

1. 署名フィールドの変更

   を呼び出して署名フィールドを変更する `SignatureServiceClient` オブジェクトの `modifySignatureField` メソッドを使用して、次の値を渡します。

   * この `BLOB` 変更するPDFフィールドを含む署名ドキュメントを格納するオブジェクト
   * 署名フィールドの名前を指定する string 値です
   * この `PDFSignatureFieldProperties` 署名フィールドロックディクショナリとシード値ディクショナリ情報を格納するオブジェクト

   この `modifySignatureField` メソッドは、 `BLOB` 変更されたPDFフィールドを含む署名ドキュメントを保存するオブジェクト。

1. PDFドキュメントをPDFファイルとして保存

   * の作成 `System.IO.FileStream` オブジェクトを呼び出し、PDFフィールドを含む署名ドキュメントのファイルの場所と、ファイルを開くモードを表す string 値を渡すことによって、オブジェクトを指定します。
   * コンテンツを格納するバイト配列を作成します。 `BLOB` オブジェクト `addSignatureField` メソッドはを返します。 バイト配列を生成するには、 `BLOB` オブジェクトの `MTOM` データメンバー。
   * の作成 `System.IO.BinaryWriter` オブジェクトのコンストラクタを呼び出し、 `System.IO.FileStream` オブジェクト。
   * を呼び出して、バイト配列の内容をPDFファイルに書き込みます。 `System.IO.BinaryWriter` オブジェクトの `Write` メソッドを使用してバイト配列を渡す。

**関連トピック**

[MTOM を使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRef を使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## デジタル署名PDF文書 {#digitally-signing-pdf-documents}

セキュリティレベルの提供のため、PDF に電子署名を適用することができます。手書き署名のような電子署名は、署名者を識別したり、ドキュメントに関するステートメントを作成する手段として使用できます。ドキュメントの電子署名に使用されている技術は、署名者と受信者の両方が、何に署名されているのかを明確にし、その署名によりドキュメントに変更がないことを確認するのに役立ちます。

PDF ドキュメントは、公開鍵を用いて署名されます。署名者は公開鍵と秘密鍵の 2 つの鍵を持っています。秘密鍵は、署名時に使用可能である必要があるユーザーの資格情報に保存されます。 公開鍵はユーザーの証明書に保存されます。この証明書は、受信者が署名を検証するために使用できる必要があります。 失効した証明書に関する情報は、認証機関から配布される証明書失効リスト（CRL）およびオンライン証明書ステータスプロトコル（OCSP）応答内にあります。署名が行われた時間は、タイムスタンプ局として知られる信頼できるソースから取得されます。

>[!NOTE]
>
>PDFドキュメントに電子署名する前に、証明書がAEM Formsに追加されていることを確認する必要があります。 証明書は、管理コンソールを使用して、または Trust Manager API を使用してプログラムで追加されます。 ( [Trust Manager API を使用した資格情報の読み込み](/help/forms/developing/credentials.md#importing-credentials-by-using-the-trust-manager-api).)

プログラムによるPDF文書への電子署名が可能です。 PDFドキュメントに電子署名する場合は、AEM Formsに存在するセキュリティ証明書を参照する必要があります。 証明書は署名に使用する秘密鍵となります。

Signature サービスは、署名ドキュメントが署名される際に、次のPDFを実行します。

1. Signature サービスは、要求で指定されたエイリアスを渡すことで、Truststore から秘密鍵証明書を取得します。
1. Truststore は指定した秘密鍵証明書を検索します。
1. 秘密鍵証明書が Signature サービスに返され、ドキュメントへの署名に使用されます。 また、証明書は、以降の要求でエイリアスに対してキャッシュされます。

セキュリティ証明書の処理について詳しくは、使用しているアプリケーションサーバー版の『AEM Forms*のインストールとデプロイ』ガイドを参照してください。

>[!NOTE]
>
>ドキュメントの署名と認証には違いがあります。 ( [認証PDF書](digitally-signing-certifying-documents.md#certifying-pdf-documents).)

>[!NOTE]
>
>署名をサポートしていないPDFドキュメントもあります。 Signature サービスとドキュメントへの電子署名について詳しくは、 [AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Signature サービスは、ドキュメントの認証など、操作への入力としてPDFデータが埋め込まれた XDP ファイルをサポートしていません。 このアクションを実行すると、Signature サービスで `PDFOperationException`. この問題を解決するには、PDFUtilities サービスを使用して XDP ファイルをPDFファイルに変換し、変換後のPDFファイルを Signature サービス操作に渡します。 ( [PDF・ユーティリティの操作](/help/forms/developing/pdf-utilities.md#working-with-pdf-utilities).)

**nCipher nShield HSM 秘密鍵証明書**

PDFドキュメントの署名や証明に nCipher nShield HSM 秘密鍵証明書を使用する場合、AEM Formsがデプロイされている J2EE アプリケーションサーバーが再起動されるまで、新しい秘密鍵証明書は使用できません。 ただし、設定値を設定すると、J2EE アプリケーションサーバーを再起動しなくても、署名や認証の処理が機能します。

次の設定値を cknfastrc ファイルに追加できます。cknfastrc ファイルは/opt/nfast/cknfastrc( またはc:\nfast\cknfastrc) にあります。

```as3
 CKNFAST_ASSUME_SINGLE_PROCESS=0
```

この設定値を cknfastrc ファイルに追加すると、J2EE アプリケーションサーバーを再起動しなくても、新しい秘密鍵証明書を使用できます。

**署名は信頼されていません**

同じPDFドキュメントの認証と署名を行う際に、認証PDFが信頼されていない場合、AcrobatまたはAdobe Readerで署名ドキュメントを開くと、最初の署名に対して黄色い三角形が表示されます。 この状況を避けるには、認証用署名を信頼する必要があります。

**XFA ベースのフォームでドキュメントに署名する**

Signature service API を使用して XFA ベースのフォームに署名しようとすると、データが `View` `Signed` `Version` Acrobatにあります。 例えば、次のワークフローについて考えてみましょう。

* Designer を使用して作成された XDP ファイルを使用して、署名フィールドを含むフォームデザインと、フォームデータを含む XML データを結合します。 Formsサービスを使用して、インタラクティブPDFドキュメントを生成します。
* Signature サービス API を使用してPDFドキュメントに署名します。

### 手順の概要 {#summary_of_steps-3}

PDF文書に電子署名を行うには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. Signature サービスクライアントを作成します。
1. 署名するPDFドキュメントを取得します。
1. PDF文書に署名する。
1. 署名済みPDFドキュメントをPDFファイルとして保存します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。 Web サービスを使用している場合は、プロキシファイルを必ず含めてください。

次の JAR ファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar(AEM Formsを JBoss にデプロイする場合に必要 )
* jbossall-client.jar(AEM Formsが JBoss にデプロイされている場合に必要 )

**Signatures クライアントの作成**

Signature サービスの操作をプログラムで実行する前に、Signature サービスクライアントを作成する必要があります。

**署名するPDFドキュメントを取得**

PDFドキュメントに署名するには、署名フィールドを含むPDFドキュメントを取得する必要があります。 PDFドキュメントに署名フィールドが含まれていない場合、署名できません。 署名フィールドは、Designer を使用して追加することも、プログラムを使用して追加することもできます。

**PDF文書に署名**

PDFドキュメントに署名する際に、Signature サービスで使用する実行時オプションを設定できます。 以下のオプションを設定できます。

* 外観オプション
* 失効確認
* タイムスタンプ値

外観のオプションを設定するには、 `PDFSignatureAppearanceOptionSpec` オブジェクト。 例えば、 `PDFSignatureAppearanceOptionSpec` オブジェクトの `setShowDate` メソッドとパス `true`.

また、PDFドキュメントへのデジタル署名に使用された証明書が失効したかどうかを判断する失効確認を実行するかどうかを指定することもできます。 失効確認を実行するには、次のいずれかの値を指定します。

* **NoCheck**:失効確認を実行しない。
* **BestEffort**:常に、チェーン内のすべての証明書の失効を確認しようとします。 チェック中に問題が発生した場合、失効は有効と見なされます。 エラーが発生した場合は、証明書が失効していないと仮定します。
* **CheckIfAvailable:** 失効情報が利用できる場合は、チェーン内のすべての証明書の失効を確認します。 チェック中に問題が発生した場合、失効は無効と見なされます。 エラーが発生した場合は、証明書が失効し、無効であると仮定します。 （これはデフォルト値です）。
* **AlwaysCheck**:チェーン内のすべての証明書の失効を確認します。 どの証明書にも失効情報が存在しない場合、失効は無効と見なされます。

証明書に対して失効確認を実行するには、証明書失効リスト (CRL) サーバーへの URL を、 `CRLOptionSpec` オブジェクト。 ただし、失効確認を実行し、CRL サーバーへの URL を指定しない場合、Signature サービスは証明書から URL を取得します。

失効確認を実行する際には、CRL サーバーを使用する代わりに、オンライン証明書ステータスプロトコル (OCSP) サーバーを使用できます。 通常、CRL サーバーとは異なり OCSP サーバーを使用する場合は、失効確認の実行が高速になります。 (「オンライン証明書ステータスプロトコル」( [https://tools.ietf.org/html/rfc2560](https://tools.ietf.org/html/rfc2560).)

Signature サービスが Applications and Services を使用して使用する CRL および OCSPAdobeの順序を設定できます。 例えば、OCSP サーバーが最初にAdobeのアプリケーションおよびサービスで設定されている場合、OCSP サーバーがチェックされ、次に CRL サーバーがチェックされます。 （AAC ヘルプの「Trust Store を使用した証明書と秘密鍵証明書の管理」を参照）。

失効確認を実行しないように指定した場合、Signature サービスは、ドキュメントの署名または認証に使用された証明書が失効したかどうかを確認しません。 つまり、CRL および OCSP サーバー情報は無視されます。

>[!NOTE]
>
>証明書に CRL または OCSP サーバーを指定することもできますが、証明書で指定された URL を上書きするには、 `CRLOptionSpec` および `OCSPOptionSpec` オブジェクト。 例えば、CRL サーバーを上書きする場合は、 `CRLOptionSpec` オブジェクトの `setLocalURI` メソッド。

タイムスタンプとは、署名済みまたは認証済みのドキュメントが変更された時間を追跡するプロセスを指します。 ドキュメントの署名後は、ドキュメントの所有者でもドキュメントを変更しないでください。 タイムスタンプを使用すると、署名済みまたは認証済みのドキュメントの有効性を強制することができます。 タイムスタンプオプションは、 `TSPOptionSpec` オブジェクト。 例えば、タイムスタンププロバイダー (TSP) サーバーの URL を指定できます。

>[!NOTE]
>
>Java および Web サービスの各セクションおよび対応するクイックスタートでは、失効確認が使用されます。 CRL または OCSP サーバー情報が指定されていないので、サーバードキュメントへのデジタル署名に使用される証明書からPDF情報が取得されます。

PDFドキュメントに正常に署名するには、次のような電子署名を含む署名フィールドの完全修飾名を指定します。 `form1[0].#subform[1].SignatureField3[3]`. XFA フォームフィールドを使用する場合、署名フィールドの名前の一部を使用することもできます。 `SignatureField3[3]`.

また、セキュリティドキュメントに電子署名を行うには、セキュリティ証明書も参照する必要があります。PDFドキュメントに電子署名を行うには、 セキュリティ証明書を参照するには、エイリアスを指定します。 エイリアスは、PKCS#12 ファイル（.pfx 拡張子付き）またはハードウェアセキュリティモジュール (HSM) に存在する実際の秘密鍵証明書への参照です。 セキュリティ証明書について詳しくは、使用しているアプリケーションサーバー版の『AEM Forms*のインストールとデプロイ』ガイドを参照してください。

**署名済みPDF文書を保存**

Signature サービスがPDFドキュメントに電子署名を行った後、そのドキュメントをPDFファイルとして保存し、AcrobatまたはAdobe Readerで開くことができます。

**関連トピック**

[Java API を使用したPDFドキュメントのデジタル署名](digitally-signing-certifying-documents.md#digitally-sign-pdf-documents-using-the-java-api)

[Web サービス API を使用したPDFドキュメントのデジタル署名](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[署名フィールドの追加](digitally-signing-certifying-documents.md#adding-signature-fields)

[署名フィールド名の取得](digitally-signing-certifying-documents.md#retrieving-signature-field-names)

### Java API を使用したPDFドキュメントのデジタル署名 {#digitally-sign-pdf-documents-using-the-java-api}

署名 API(Java) を使用してPDFドキュメントに電子署名を行う：

1. プロジェクトファイルを含める

   Java プロジェクトのクラスパスに、adobe-signatures-client.jar などのクライアント JAR ファイルを含めます。

1. Signatures クライアントの作成

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用して `SignatureServiceClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. 署名するPDFドキュメントを取得

   * の作成 `java.io.FileInputStream` コンストラクタを使用し、PDFドキュメントの場所を指定する string 値を渡すことによって、デジタル署名を行うPDFドキュメントを表すオブジェクト。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. PDF文書に署名

   を呼び出してPDFドキュメントに署名する `SignatureServiceClient` オブジェクトの `sign` メソッドを使用して、次の値を渡します。

   * A `com.adobe.idp.Document` 署名するPDF文書を表すオブジェクト。
   * 電子署名を格納する署名フィールドの名前を表す string 値です。
   * A `Credential` オブジェクトドキュメントへの電子署名に使用される秘密鍵証明書を表すPDF。 の作成 `Credential` を呼び出すことによってオブジェクトを取得 `Credential` オブジェクトの静的 `getInstance` メソッドを使用し、セキュリティ秘密鍵証明書に対応するエイリアス値を指定する string 値を渡す。
   * A `HashAlgorithm` オブジェクトドキュメントのダイジェストに使用するハッシュアルゴリズムを表す静的データPDFを指定するオブジェクト。 例えば、次の項目を指定できます。 `HashAlgorithm.SHA1` を使用して、SHA1 アルゴリズムを使用します。
   * PDFドキュメントがデジタル署名された理由を表す string 値です。
   * 署名者の連絡先情報を表す string 値です。
   * A `PDFSignatureAppearanceOptions` 電子署名の外観を制御するオブジェクト。 例えば、このオブジェクトを使用して、電子署名にカスタムロゴを追加できます。
   * A `java.lang.Boolean` 署名者の証明書に対して失効確認を実行するかどうかを指定するオブジェクト。
   * An `OCSPOptionSpec` オンライン証明書ステータスプロトコル (OCSP) サポートの環境設定を格納するオブジェクト。 失効確認が実行されない場合、このパラメーターは使用されず、次の項目を指定できます `null`.
   * A `CRLPreferences` 証明書失効リスト (CRL) の環境設定を保存するオブジェクト。 失効確認が実行されない場合、このパラメーターは使用されず、次の項目を指定できます `null`.
   * A `TSPPreferences` タイムスタンププロバイダー (TSP) がサポートする環境設定を保存するオブジェクト。 このパラメーターはオプションで、 `null`. 詳しくは、 [AEM Forms API リファレンス](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

   この `sign` メソッドは、 `com.adobe.idp.Document` 署名済みPDF文書を表すオブジェクト。

1. 署名済みPDF文書を保存

   * `java.io.File` オブジェクトを作成し、ファイル拡張子が .pdf であることを確認します。
   * を呼び出す `com.adobe.idp.Document` オブジェクトの `copyToFile` メソッドとパス `java.io.File`内容をコピーする `Document` オブジェクトをファイルに追加します。 `com.adobe.idp.Document` メソッドから返された `sign` オブジェクトを必ず使用してください。

**関連トピック**

[デジタル署名PDF文書](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)

[クイックスタート（SOAP モード）:Java API を使用したPDFドキュメントのデジタル署名](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-digitally-signing-a-pdf-document-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Web サービス API を使用したPDFドキュメントのデジタル署名 {#digitally-signing-pdf-documents-using-the-web-service-api}

Signature API（Web サービス）を使用してPDFドキュメントに電子署名するには：

1. プロジェクトファイルを含める

   MTOM を使用するMicrosoft .NET プロジェクトを作成します。 次の WSDL 定義を使用していることを確認します。 `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >置換 `localhost` を、AEM Formsをホストするサーバーの IP アドレスに設定します。

1. Signatures クライアントの作成

   * の作成 `SignatureServiceClient` オブジェクトのデフォルトのコンストラクタを使用します。
   * の作成 `SignatureServiceClient.Endpoint.Address` オブジェクトを `System.ServiceModel.EndpointAddress` コンストラクタ。 WSDL をAEM Formsサービスに渡す文字列値 ( 例： `http://localhost:8080/soap/services/SignatureService?WSDL`) をクリックします。 を使用する必要はありません。 `lc_version` 属性。 この属性は、サービス参照を作成する際に使用されます )。
   * の作成 `System.ServiceModel.BasicHttpBinding` オブジェクトを作成するには、 `SignatureServiceClient.Endpoint.Binding` フィールドに入力します。 戻り値を `BasicHttpBinding` にキャストします。
   * を `System.ServiceModel.BasicHttpBinding` オブジェクトの `MessageEncoding` ～に向かって `WSMessageEncoding.Mtom`. この値は、MTOM が確実に使用されるようにします。
   * 次のタスクを実行して、基本的な HTTP 認証を有効にします。

      * フィールドにAEM forms ユーザー名を割り当てます。 `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * 対応するパスワード値をフィールドに割り当てます。 `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * 定数値を割り当て `HttpClientCredentialType.Basic` フィールドに `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 定数値を割り当て `BasicHttpSecurityMode.TransportCredentialOnly` フィールドに `BasicHttpBindingSecurity.Security.Mode`.

1. 署名するPDFドキュメントを取得

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。この `BLOB` オブジェクトは、署名されたPDFドキュメントを保存するために使用されます。
   * の作成 `System.IO.FileStream` オブジェクトを呼び出し、署名するPDFドキュメントのファイルの場所と、ファイルを開くモードを表す string 値を渡すことによって、オブジェクトを指定します。
   * コンテンツを格納するバイト配列を作成します。 `System.IO.FileStream` オブジェクト。 バイト配列のサイズは、 `System.IO.FileStream` オブジェクトの `Length` プロパティ。
   * を呼び出して、バイト配列にストリームデータを入力します。 `System.IO.FileStream` オブジェクトの `Read` メソッドを使用し、読み込むバイト配列、開始位置、ストリーム長を渡す。
   * 次の項目に `BLOB` オブジェクトを割り当てる `MTOM` プロパティは、バイト配列の内容を示します。

1. PDF文書に署名

   を呼び出してPDFドキュメントに署名する `SignatureServiceClient` オブジェクトの `sign` メソッドを使用して、次の値を渡します。

   * A `BLOB` 署名するPDF文書を表すオブジェクト。
   * 電子署名を格納する署名フィールドの名前を表す string 値です。
   * A `Credential` オブジェクトドキュメントへの電子署名に使用される秘密鍵証明書を表すPDF。 の作成 `Credential` オブジェクトを指定するには、コンストラクタを使用し、 `Credential` オブジェクトの `alias` プロパティ。
   * A `HashAlgorithm` オブジェクトドキュメントのダイジェストに使用するハッシュアルゴリズムを表す静的データPDFを指定するオブジェクト。 例えば、次の項目を指定できます。 `HashAlgorithm.SHA1` を使用して、SHA1 アルゴリズムを使用します。
   * ハッシュアルゴリズムを使用するかどうかを指定するブール値です。
   * PDFドキュメントがデジタル署名された理由を表す string 値です。
   * 署名者の場所を表す string 値です。
   * 署名者の連絡先情報を表す string 値です。
   * A `PDFSignatureAppearanceOptions` 電子署名の外観を制御するオブジェクト。 例えば、このオブジェクトを使用して、電子署名にカスタムロゴを追加できます。
   * A `System.Boolean` 署名者の証明書に対して失効確認を実行するかどうかを指定するオブジェクト。 この失効確認が完了すると、署名に埋め込まれます。 デフォルトは、`false` です。
   * An `OCSPOptionSpec` オンライン証明書ステータスプロトコル (OCSP) サポートの環境設定を格納するオブジェクト。 失効確認が実行されない場合、このパラメーターは使用されず、次の項目を指定できます `null`. このオブジェクトについて詳しくは、 [AEM Forms API リファレンス](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).
   * A `CRLPreferences` 証明書失効リスト (CRL) の環境設定を保存するオブジェクト。 失効確認が実行されない場合、このパラメーターは使用されず、次の項目を指定できます `null`.
   * A `TSPPreferences` タイムスタンププロバイダー (TSP) がサポートする環境設定を保存するオブジェクト。 このパラメーターはオプションで、 `null`.

   この `sign` メソッドは、 `BLOB` 署名済みPDF文書を表すオブジェクト。

1. 署名済みPDF文書を保存

   * の作成 `System.IO.FileStream` オブジェクトを指定します。 署名済みPDFドキュメントのファイルの場所と、ファイルを開くモードを表す string 値を渡します。
   * コンテンツを格納するバイト配列を作成します。 `BLOB` が返したオブジェクト `sign` メソッド。 バイト配列を生成するには、 `BLOB` オブジェクトの `MTOM` データメンバー。
   * の作成 `System.IO.BinaryWriter` オブジェクトのコンストラクタを呼び出し、 `System.IO.FileStream` オブジェクト。
   * を呼び出して、バイト配列の内容をPDFファイルに書き込みます。 `System.IO.BinaryWriter` オブジェクトの `Write` メソッドを使用してバイト配列を渡す。

**関連トピック**

[デジタル署名PDF文書](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)

[MTOM を使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRef を使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## インタラクティブFormsのデジタル署名 {#digitally-signing-interactive-forms}

Formsサービスで作成されるインタラクティブフォームに署名することができます。 例えば、次のワークフローについて考えてみましょう。

* Formsサービスを使用して、Designer を使用して作成した XFA ベースのPDFフォームと、XML ドキュメント内のフォームデータを結合します。 Formsサーバーはインタラクティブフォームをレンダリングします。
* Signature service API を使用してインタラクティブフォームに署名します。

その結果、デジタル署名されたインタラクティブPDFフォームが生成されます。 XFA フォームに基づくPDFフォームに署名する場合は、PDFファイルをAdobeの静的PDFフォームとして保存してください。 「動的PDF」フォームとして保存されたAdobeフォームにPDFしようとすると、例外が発生します。 Formsサービスから返されるフォームに署名するので、フォームに署名フィールドが含まれていることを確認してください。

>[!NOTE]
>
>インタラクティブフォームに電子署名する前に、証明書をAEM Formsに追加する必要があります。 証明書は、管理コンソールを使用して、または Trust Manager API を使用してプログラムで追加されます。 ( [Trust Manager API を使用した資格情報の読み込み](/help/forms/developing/credentials.md#importing-credentials-by-using-the-trust-manager-api).)

Forms Service API を使用する場合、 `GenerateServerAppearance` 実行時のオプション `true`. この実行時オプションを使用すると、サーバー上で生成されたフォームの外観をAcrobatまたはAdobe Readerで開いたときにも、その外観が有効なままになります。 Forms API を使用して署名するインタラクティブフォームを生成する場合は、このランタイムオプションを設定することをお勧めします。

>[!NOTE]
>
>インタラクティブFormsのデジタル署名を読む前に、PDFドキュメントへの署名に関する詳細を理解しておくことをお勧めします。 ( [デジタル署名PDF文書](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents).)

### 手順の概要 {#summary_of_steps-4}

Formsサービスが返すインタラクティブフォームに電子署名するには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. Formsおよび Signatures クライアントを作成します。
1. Formsサービスを使用してインタラクティブフォームを取得します。
1. インタラクティブフォームに署名します。
1. 署名済みPDFドキュメントをPDFファイルとして保存します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。 Web サービスを使用している場合は、プロキシファイルを必ず含めてください。

次の JAR ファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-forms-client.jar
* adobe-utilities.jar(AEM Formsを JBoss にデプロイする場合に必要 )
* jbossall-client.jar(AEM Formsが JBoss にデプロイされている場合に必要 )

これらの JAR ファイルの場所について詳しくは、 [AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Formsおよび Signatures クライアントの作成**

このワークフローはFormsと Signature サービスの両方を呼び出すので、Formsサービスクライアントと Signature サービスクライアントの両方を作成します。

**Formsサービスを使用したインタラクティブフォームの取得**

Formsサービスを使用して、署名するインタラクティブPDFフォームを取得できます。 AEM Forms以降、 `com.adobe.idp.Document` オブジェクトを、レンダリングするフォームを含むFormsサービスに追加します。 このメソッドの名前はです。 `renderPDFForm2`. このメソッドは、 `com.adobe.idp.Document` 署名するフォームを含むオブジェクト。 これは `com.adobe.idp.Document` インスタンスを Signature サービスに追加します。

同様に、Web サービスを使用している場合、 `BLOB` Formsサービスが Signature サービスに返すインスタンス。

>[!NOTE]
>
>「インタラクティブなFormsのデジタル署名」セクションに関連付けられたクイックスタートは、 `renderPDFForm2` メソッド。

**インタラクティブフォームに署名する**

PDFドキュメントに署名する際に、Signature サービスが使用する実行時オプションを設定できます。 以下のオプションを設定できます。

* 外観オプション
* 失効確認
* タイムスタンプ値

外観のオプションを設定するには、 `PDFSignatureAppearanceOptionSpec` オブジェクト。 例えば、 `PDFSignatureAppearanceOptionSpec` オブジェクトの `setShowDate` メソッドとパス `true`.

**署名済みPDF文書を保存**

Signature サービスがPDFドキュメントに電子署名を行った後、そのドキュメントをPDFファイルとして保存できます。 PDFファイルは、AcrobatまたはAdobe Readerで開くことができます。

**関連トピック**

[Java API を使用したインタラクティブフォームのデジタル署名](digitally-signing-certifying-documents.md#digitally-sign-an-interactive-form-using-the-java-api)

[Web サービス API を使用してインタラクティブフォームにデジタル署名する](digitally-signing-certifying-documents.md#digitally-sign-an-interactive-form-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[デジタル署名PDF文書](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)

[インタラクティブPDF formsのレンダリング](/help/forms/developing/rendering-forms.md#rendering-interactive-pdf-forms)

### Java API を使用したインタラクティブフォームのデジタル署名 {#digitally-sign-an-interactive-form-using-the-java-api}

Formsと署名 API(Java) を使用してインタラクティブフォームに電子署名するには、次の手順を実行します。

1. プロジェクトファイルを含める

   Java プロジェクトのクラスパスに、adobe-signatures-client.jar や adobe-forms-client.jar などのクライアント JAR ファイルを含めます。

1. Formsおよび Signatures クライアントの作成

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用して `SignatureServiceClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用して `FormsServiceClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. Formsサービスを使用したインタラクティブフォームの取得

   * の作成 `java.io.FileInputStream` コンストラクターを使用してPDFサービスに渡すFormsドキュメントを表すオブジェクト。 Pass a string value that specifies the location of the PDF document.
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。
   * の作成 `java.io.FileInputStream` コンストラクタを使用してFormsサービスに渡すフォームデータが格納されている XML ドキュメントを表すオブジェクト。 XML ファイルの場所を指定する string 値を渡します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。
   * の作成 `PDFFormRenderSpec` オブジェクトを返します。 を呼び出す `PDFFormRenderSpec` オブジェクトの `setGenerateServerAppearance` メソッドとパス `true`.
   * を呼び出す `FormsServiceClient` オブジェクトの `renderPDFForm2` メソッドを使用して、次の値を渡します。

      * A `com.adobe.idp.Document` レンダリングするPDFフォームを含むオブジェクト。
      * A `com.adobe.idp.Document` フォームに結合するデータを含むオブジェクト。
      * A `PDFFormRenderSpec` 実行時オプションを保存するオブジェクト。
      * A `URLSpec` Formsサービスで必要な URI 値を格納するオブジェクト。 次を指定できます。 `null` を参照してください。
      * A `java.util.HashMap` 添付ファイルを保存するオブジェクト。 これはオプションのパラメーターで、 `null` フォームにファイルを添付しない場合。

      この `renderPDFForm2` メソッドは、 `FormsResult` フォームデータストリームを含むオブジェクト

   * を呼び出してPDFフォームを取得する `FormsResult` オブジェクトの `getOutputContent` メソッド。 このメソッドは、 `com.adobe.idp.Document` インタラクティブフォームを表すオブジェクト。


1. インタラクティブフォームに署名する

   を呼び出してPDFドキュメントに署名する `SignatureServiceClient` オブジェクトの `sign` メソッドを使用して、次の値を渡します。

   * A `com.adobe.idp.Document` 署名するPDF文書を表すオブジェクト。 このオブジェクトが `com.adobe.idp.Document` オブジェクトはFormsサービスから取得されます。
   * 署名された署名フィールドの名前を表す string 値です。
   * A `Credential` オブジェクトドキュメントへの電子署名に使用される秘密鍵証明書を表すPDF。 の作成 `Credential` を呼び出すことによってオブジェクトを取得 `Credential` オブジェクトの静的 `getInstance` メソッド。 セキュリティ秘密鍵証明書に対応するエイリアス値を指定する string 値を渡します。
   * A `HashAlgorithm` オブジェクトドキュメントのダイジェストに使用するハッシュアルゴリズムを表す静的データPDFを指定するオブジェクト。 例えば、次の項目を指定できます。 `HashAlgorithm.SHA1` を使用して、SHA1 アルゴリズムを使用します。
   * PDFドキュメントがデジタル署名された理由を表す string 値です。
   * 署名者の連絡先情報を表す string 値です。
   * A `PDFSignatureAppearanceOptions` 電子署名の外観を制御するオブジェクト。 例えば、このオブジェクトを使用して、電子署名にカスタムロゴを追加できます。
   * A `java.lang.Boolean` 署名者の証明書に対して失効確認を実行するかどうかを指定するオブジェクト。
   * An `OCSPPreferences` オンライン証明書ステータスプロトコル (OCSP) サポートの環境設定を格納するオブジェクト。 失効確認が実行されない場合、このパラメーターは使用されず、次の項目を指定できます `null`.
   * A `CRLPreferences` 証明書失効リスト (CRL) の環境設定を保存するオブジェクト。 失効確認が実行されない場合、このパラメーターは使用されず、次の項目を指定できます `null`.
   * A `TSPPreferences` タイムスタンププロバイダー (TSP) がサポートする環境設定を保存するオブジェクト。 このパラメーターはオプションで、 `null`.

   この `sign` メソッドは、 `com.adobe.idp.Document` 署名済みPDF文書を表すオブジェクト。

1. 署名済みPDF文書を保存

   * の作成 `java.io.File` オブジェクトに置き換え、ファイル名の拡張子が.pdf であることを確認します。
   * を呼び出す `com.adobe.idp.Document` オブジェクトの `copyToFile` メソッドとパス `java.io.File`内容をコピーする `Document` オブジェクトをファイルに追加します。 必ず `com.adobe.idp.Document` オブジェクト `sign` メソッドが返されました。

**関連トピック**

[インタラクティブFormsのデジタル署名](digitally-signing-certifying-documents.md#digitally-signing-interactive-forms)

[クイックスタート（SOAP モード）:Java API を使用したPDFドキュメントのデジタル署名](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-digitally-signing-a-pdf-document-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Web サービス API を使用してインタラクティブフォームにデジタル署名する {#digitally-sign-an-interactive-form-using-the-web-service-api}

Formsと署名 API（Web サービス）を使用して、インタラクティブフォームに電子署名します。

1. プロジェクトファイルを含める

   MTOM を使用するMicrosoft .NET プロジェクトを作成します。 このクライアントアプリケーションは 2 つのAEM Formsサービスを呼び出すので、2 つのサービス参照を作成します。 Signature サービスに関連付けられたサービス参照に、次の WSDL 定義を使用します。 `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   Formsサービスに関連付けられたサービス参照に、次の WSDL 定義を使用します。 `http://localhost:8080/soap/services/FormsService?WSDL&lc_version=9.0.1`.

   これは、 `BLOB` データタイプは、両方のサービス参照に共通で、完全に修飾されます `BLOB` データタイプを使用する場合。 対応する Web サービスのクイックスタートで、 `BLOB` インスタンスは完全に選定されています。

   >[!NOTE]
   >
   >置換 `localhost` を、AEM Formsをホストするサーバーの IP アドレスに設定します。

1. Formsおよび Signatures クライアントの作成

   * の作成 `SignatureServiceClient` オブジェクトのデフォルトのコンストラクタを使用します。
   * の作成 `SignatureServiceClient.Endpoint.Address` オブジェクトを `System.ServiceModel.EndpointAddress` コンストラクタ。 WSDL をAEM Formsサービスに渡す文字列値 ( 例： `http://localhost:8080/soap/services/SignatureService?WSDL`) をクリックします。 を使用する必要はありません。 `lc_version` 属性。 この属性は、サービス参照を作成する際に使用されます )。
   * の作成 `System.ServiceModel.BasicHttpBinding` オブジェクトを作成するには、 `SignatureServiceClient.Endpoint.Binding` フィールドに入力します。 戻り値を `BasicHttpBinding` にキャストします。
   * を `System.ServiceModel.BasicHttpBinding` オブジェクトの `MessageEncoding` ～に向かって `WSMessageEncoding.Mtom`. この値は、MTOM が確実に使用されるようにします。
   * 次のタスクを実行して、基本的な HTTP 認証を有効にします。

      * フィールドにAEM forms ユーザー名を割り当てます。 `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * 対応するパスワード値をフィールドに割り当てます。 `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * 定数値を割り当て `HttpClientCredentialType.Basic` フィールドに `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * 定数値を割り当て `BasicHttpSecurityMode.TransportCredentialOnly` フィールドに `BasicHttpBindingSecurity.Security.Mode`.

   >[!NOTE]
   >
   >Formsサービスクライアントに対して、これらの手順を繰り返します。

1. Formsサービスを使用したインタラクティブフォームの取得

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。この `BLOB` オブジェクトは、署名されたPDFドキュメントを保存するために使用されます。
   * の作成 `System.IO.FileStream` オブジェクトを呼び出し、署名するPDFドキュメントのファイルの場所と、ファイルを開くモードを表す string 値を渡すことによって、オブジェクトを指定します。
   * コンテンツを格納するバイト配列を作成します。 `System.IO.FileStream` オブジェクト。 バイト配列のサイズは、 `System.IO.FileStream` オブジェクトの `Length` プロパティ。
   * を呼び出して、バイト配列にストリームデータを入力します。 `System.IO.FileStream` オブジェクトの `Read` メソッドを使用し、読み込むバイト配列、開始位置、ストリーム長を渡す。
   * 次の項目に `BLOB` オブジェクトを割り当てる `MTOM` プロパティは、バイト配列の内容を示します。
   * コンストラクタを使用して `BLOB` オブジェクトを作成します。この `BLOB` オブジェクトは、フォームデータの保存に使用されます。
   * の作成 `System.IO.FileStream` オブジェクトを呼び出し、フォームデータを含む XML ファイルのファイルの場所と、ファイルを開くモードを表す string 値を渡すことによってオブジェクトを指定します。
   * コンテンツを格納するバイト配列を作成します。 `System.IO.FileStream` オブジェクト。 バイト配列のサイズは、 `System.IO.FileStream` オブジェクトの `Length` プロパティ。
   * を呼び出して、バイト配列にストリームデータを入力します。 `System.IO.FileStream` オブジェクトの `Read` メソッドを使用し、読み込むバイト配列、開始位置、ストリーム長を渡す。
   * 次の項目に `BLOB` オブジェクトを割り当てる `MTOM` プロパティは、バイト配列の内容を示します。
   * の作成 `PDFFormRenderSpec` オブジェクトを返します。 値を割り当て `true` から `PDFFormRenderSpec` オブジェクトの `generateServerAppearance` フィールドに入力します。
   * を呼び出す `FormsServiceClient` オブジェクトの `renderPDFForm2` メソッドを使用して、次の値を渡します。

      * A `BLOB` レンダリングするPDFフォームを含むオブジェクト。
      * A `BLOB` フォームに結合するデータを含むオブジェクト。
      * A `PDFFormRenderSpec` 実行時オプションを保存するオブジェクト。
      * A `URLSpec` Formsサービスで必要な URI 値を格納するオブジェクト。 次を指定できます。 `null` を参照してください。
      * A `java.util.HashMap` 添付ファイルを保存するオブジェクト。 これはオプションのパラメーターで、 `null` フォームにファイルを添付しない場合。
      * フォームのページ数を保存するために使用される長い出力パラメーターです。
      * ロケール値に使用される文字列出力パラメーターです。
      * A `FormResult` インタラクティブフォームの保存に使用される出力パラメーターの値です。
   * を呼び出してPDFフォームを取得します。 `FormsResult` オブジェクトの `outputContent` フィールドに入力します。 このフィールドには `BLOB` インタラクティブフォームを表すオブジェクト。


1. インタラクティブフォームに署名する

   を呼び出してPDFドキュメントに署名する `SignatureServiceClient` オブジェクトの `sign` メソッドを使用して、次の値を渡します。

   * A `BLOB` 署名するPDF文書を表すオブジェクト。 以下を使用： `BLOB` Formsサービスによって返されたインスタンス。
   * 署名された署名フィールドの名前を表す string 値です。
   * A `Credential` オブジェクトドキュメントへの電子署名に使用される秘密鍵証明書を表すPDF。 の作成 `Credential` オブジェクトを指定するには、コンストラクタを使用し、 `Credential` オブジェクトの `alias` プロパティ。
   * A `HashAlgorithm` オブジェクトドキュメントのダイジェストに使用するハッシュアルゴリズムを表す静的データPDFを指定するオブジェクト。 例えば、次の項目を指定できます。 `HashAlgorithm.SHA1` を使用して、SHA1 アルゴリズムを使用します。
   * ハッシュアルゴリズムを使用するかどうかを指定するブール値です。
   * PDFドキュメントがデジタル署名された理由を表す string 値です。
   * 署名者の場所を表す string 値です。
   * 署名者の連絡先情報を表す string 値です。
   * A `PDFSignatureAppearanceOptions` 電子署名の外観を制御するオブジェクト。 例えば、このオブジェクトを使用して、電子署名にカスタムロゴを追加できます。
   * A `System.Boolean` 署名者の証明書に対して失効確認を実行するかどうかを指定するオブジェクト。 この失効確認が完了すると、署名に埋め込まれます。 デフォルトは、`false` です。
   * An `OCSPPreferences` オンライン証明書ステータスプロトコル (OCSP) サポートの環境設定を格納するオブジェクト。 失効確認が実行されない場合、このパラメーターは使用されず、次の項目を指定できます `null`. このオブジェクトについて詳しくは、 [AEM Forms API リファレンス](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).
   * A `CRLPreferences` 証明書失効リスト (CRL) の環境設定を保存するオブジェクト。 失効確認が実行されない場合、このパラメーターは使用されず、次の項目を指定できます `null`.
   * A `TSPPreferences` タイムスタンププロバイダー (TSP) がサポートする環境設定を保存するオブジェクト。 このパラメーターはオプションで、 `null`.

   この `sign` メソッドは、 `BLOB` 署名済みPDF文書を表すオブジェクト。

1. 署名済みPDF文書を保存

   * の作成 `System.IO.FileStream` オブジェクトを指定します。 署名済みPDFドキュメントのファイルの場所と、ファイルを開くモードを表す string 値を渡します。
   * コンテンツを格納するバイト配列を作成します。 `BLOB` が返したオブジェクト `sign` メソッド。 バイト配列を生成するには、 `BLOB` オブジェクトの `MTOM` データメンバー。
   * の作成 `System.IO.BinaryWriter` オブジェクトのコンストラクタを呼び出し、 `System.IO.FileStream` オブジェクト。
   * を呼び出して、バイト配列の内容をPDFファイルに書き込みます。 `System.IO.BinaryWriter` オブジェクトの `Write` メソッドを使用してバイト配列を渡す。

**関連トピック**

[インタラクティブFormsのデジタル署名](digitally-signing-certifying-documents.md#digitally-signing-interactive-forms)

[MTOM を使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

## PDF ドキュメントの認証 {#certifying-pdf-documents}

認証署名と呼ばれる特定のタイプの署名によって PDF ドキュメントを認証することで、PDF ドキュメントを保護することができます。認証署名は、以下の方法で電子署名と区別されます。

* 認証署名は PDF ドキュメントに適用される最初の署名です。つまり、認証署名が適用されるときは、ドキュメント内の他の署名フィールドは未署名でなければいけません。認証署名は 1 つの PDF ドキュメントにつき 1 つです。PDF ドキュメントを署名および認証するには、署名の前に認証を行う必要があります。PDF ドキュメントの認証後、他の署名フィールドに電子署名を行うことができます。
* ドキュメントの作成者または発信者は、認証署名を無効にすることなく、特定の方法でドキュメントの変更が可能になるように指定することができます。例えば、フォームへの入力やコメント入力を許可するドキュメントなどがあります。作成者が特定の変更を許可しないように設定を行った場合は、Acrobat はユーザーのその方法によるドキュメントの変更を制限します。別のアプリケーションを使用するなどしてそのような変更が行われた場合は、認証署名は無効となり、Acrobat はユーザーがドキュメントを開いた際に警告を発します。（未認証の署名では、変更を防ぐことはできません。また、通常の編集操作では元の署名は無効になりません。）
* 署名時に、ドキュメントのコンテンツにあいまいさや誤解をもたらす可能性のある、特定の種類のコンテンツをスキャンします。例えば、注釈により、認証される対象を把握するために重要なページ上のテキストが隠れてしまう場合があります。そのようなコンテンツに関する、説明（法的証明）を提供することができます。

Signature service Java API または Signature Web サービス API を使用して、PDFドキュメントをプログラムで認証できます。 PDFドキュメントを認証する際は、Credential サービスに存在するセキュリティ証明書を参照する必要があります。 セキュリティ証明書について詳しくは、 *AEM Formsのインストールとデプロイ* アプリケーションサーバーのガイドです。

>[!NOTE]
>
>同じPDFドキュメントを認証および署名する際に、証明書のPDFが信頼されていない場合、AcrobatまたはAdobe Readerで署名ドキュメントを開くと、最初の署名の横に黄色い三角形が表示されます。 この状況を避けるには、認証用署名を信頼する必要があります。

>[!NOTE]
>
>PDFドキュメントの署名や証明に nCipher nShield HSM 秘密鍵証明書を使用する場合、AEM Formsがデプロイされている J2EE アプリケーションサーバーが再起動されるまで、新しい秘密鍵証明書は使用できません。 ただし、設定値を設定すると、J2EE アプリケーションサーバーを再起動しなくても、署名や認証の処理が機能します。

次の設定値を cknfastrc ファイルに追加できます。cknfastrc ファイルは/opt/nfast/cknfastrc( またはc:\nfast\cknfastrc) にあります。

```as3
             CKNFAST_ASSUME_SINGLE_PROCESS=0
```

この設定値を cknfastrc ファイルに追加すると、J2EE アプリケーションサーバーを再起動しなくても、新しい秘密鍵証明書を使用できます。

>[!NOTE]
>
>Signature サービスとドキュメントの認証について詳しくは、 [AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary_of_steps-5}

PDF・ドキュメントを認証するには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. Signature クライアントを作成します。
1. 認証するPDFドキュメントを取得します。
1. PDF文書を認証する。
1. 認証済みPDFドキュメントをPDFファイルとして保存します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。 Web サービスを使用している場合は、プロキシファイルを必ず含めてください。

次の JAR ファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar(AEM Formsを JBoss にデプロイする場合に必要 )
* jbossall-client.jar(AEM Formsが JBoss にデプロイされている場合に必要 )

これらの JAR ファイルの場所について詳しくは、 [AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**署名クライアントの作成**

Signature 操作をプログラムで実行する前に、Signature クライアントを作成する必要があります。

**認証するPDFドキュメントを取得**

PDFドキュメントを認証するには、PDFフィールドを含む署名ドキュメントを取得する必要があります。 PDFドキュメントに署名フィールドが含まれていない場合は、認証できません。 署名フィールドは、Designer を使用して追加することも、プログラムを使用して追加することもできます。 プログラムによる署名フィールドの追加について詳しくは、 [署名フィールドの追加](digitally-signing-certifying-documents.md#adding-signature-fields).

**PDF文書を認証**

PDFドキュメントを正しく認証するには、Signature サービスでPDFドキュメントの認証に使用される次の入力値が必要です。

* **PDF文書**:PDFフィールドを含む署名ドキュメント。署名フィールドは、認証済みの署名のグラフィック表現を含むフォームフィールドです。 PDFドキュメントを認証する前に、署名フィールドを含める必要があります。 署名フィールドは、Designer を使用して追加することも、プログラムを使用して追加することもできます。 ( [署名フィールドの追加](digitally-signing-certifying-documents.md#adding-signature-fields).)
* **署名フィールド名**:認証される署名フィールドの完全修飾名です。 次の値は例です。 `form1[0].#subform[1].SignatureField3[3]`. XFA フォームフィールドを使用する場合、署名フィールドの名前の一部を使用することもできます。 `SignatureField3[3]`. フィールド名に null 値が渡されると、非表示の署名フィールドが動的に作成され、認証されます。
* **セキュリティ証明書**:証明書ドキュメントの認証に使用されるPDF。 このセキュリティ証明書には、パスワードとエイリアスが含まれます。このエイリアスは、Credential サービス内にある資格情報に表示されるエイリアスと一致する必要があります。 エイリアスは、PKCS#12 ファイル（.pfx 拡張子付き）またはハードウェアセキュリティモジュール (HSM) に存在する実際の秘密鍵証明書への参照です。
* **ハッシュアルゴリズム**:ハッシュドキュメントのダイジェストに使用するPDFアルゴリズムです。
* **署名の理由**:PDFドキュメントが認証された理由を他のユーザーが知るためにAcrobatまたはAdobe Readerに表示される値です。
* **署名者の場所**:秘密鍵証明書で指定された署名者の場所です。
* **連絡先情報**:署名者の住所や電話番号などの連絡先情報。
* **権限情報**:証明された署名を無効にすることなく、エンドユーザーがドキュメントに対して実行できるアクションを制御する権限です。 例えば、権限を設定して、認証ドキュメントに変更を加えると、認証済みのPDFが無効になるようにすることができます。
* **法的説明**:ドキュメントを認証すると、ドキュメントのコンテンツがあいまいになったり誤解を招く可能性のある特定の種類のコンテンツが自動的にスキャンされます。 例えば、注釈により、認証される対象を把握するために重要なページ上のテキストが隠れてしまう場合があります。スキャン処理では、これらのタイプのコンテンツに関する警告が生成されます。 この値は、警告が生成された可能性のあるコンテンツの追加の説明を提供します。
* **外観オプション**:認証済みの署名の外観を制御するオプションです。 例えば、認証署名に日付情報を表示することができます。
* **失効確認**:この値は、署名者の証明書に対して失効確認を行うかどうかを指定します。 のデフォルト設定 `false` は、失効確認がおこなわれていないことを意味します。
* **OCSP 設定**:オンライン証明書ステータスプロトコル (OCSP) サポートの設定です。この設定は、PDFドキュメントの認証に使用される秘密鍵証明書の状態に関する情報を提供します。 例えば、PDFドキュメントへのサインオンに使用する秘密鍵証明書に関する情報を提供するサーバーの URL を指定できます。
* **CRL 設定**:失効確認が行われた場合の、証明書失効リスト (CRL) 環境設定の設定です。 例えば、証明書が失効したかどうかを常に確認するように指定できます。
* **タイムスタンプ**:認証署名に適用されるタイムスタンプ情報を定義する設定です。 タイムスタンプは、特定のデータが特定の時間の前に確立されたことを示します。 この知識は、署名者と検証者の間に信頼関係を構築するのに役立ちます。

**認証済みPDFドキュメントをPDFファイルとして保存**

Signature サービスがPDFドキュメントを認証したら、PDFファイルとして保存して、AcrobatまたはAdobe Readerで開くことができます。

**関連トピック**

[Java API を使用したPDFドキュメントの認証](digitally-signing-certifying-documents.md#certify-pdf-documents-using-the-java-api)

[Web サービス API を使用したPDFドキュメントの認証](digitally-signing-certifying-documents.md#certify-pdf-documents-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[署名フィールドの追加](digitally-signing-certifying-documents.md#adding-signature-fields)

### Java API を使用したPDFドキュメントの認証 {#certify-pdf-documents-using-the-java-api}

PDFAPI(Java) を使用して署名ドキュメントを認証します。

1. プロジェクトファイルを含める

   Java プロジェクトのクラスパスに、adobe-signatures-client.jar などのクライアント JAR ファイルを含めます。

1. 署名クライアントの作成

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用して `SignatureServiceClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. 認証するPDFドキュメントを取得

   * の作成 `java.io.FileInputStream` コンストラクタを使用し、PDFドキュメントの場所を指定する string 値を渡すことで、認証するPDFドキュメントを表すオブジェクト。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. PDF文書を認証

   を呼び出してPDFドキュメントを認証する `SignatureServiceClient` オブジェクトの `certify` メソッドを使用して、次の値を渡します。

   * この `com.adobe.idp.Document` 認証するPDFドキュメントを表すオブジェクト。
   * 署名を含む署名フィールドの名前を表す string 値です。
   * A `Credential` オブジェクトのドキュメントの認証に使用されるPDFを表すオブジェクト。 の作成 `Credential` を呼び出すことによってオブジェクトを取得 `Credential` オブジェクトの静的 `getInstance` メソッドを使用し、セキュリティ秘密鍵証明書に対応するエイリアス値を指定する string 値を渡す。
   * A `HashAlgorithm` オブジェクトドキュメントのダイジェストに使用するハッシュアルゴリズムを表す静的データPDFを指定するオブジェクト。 例えば、次の項目を指定できます。 `HashAlgorithm.SHA1` を使用して、SHA1 アルゴリズムを使用します。
   * PDFドキュメントが認証された理由を表す string 値です。
   * 署名者の連絡先情報を表す string 値です。
   * A `MDPPermissions` 署名を無効にするアクションドキュメントに対してPDFを実行できるアクションを指定するオブジェクト。
   * A `PDFSignatureAppearanceOptions` 認証済みの署名の外観を制御するオブジェクト。 必要に応じて、次のようなメソッドを呼び出して、署名の外観を変更します。 `setShowDate`.
   * 署名を無効にするアクションの説明を提供する string 値です。
   * A `java.lang.Boolean` 署名者の証明書に対して失効確認を実行するかどうかを指定するオブジェクト。 この失効確認が完了すると、署名に埋め込まれます。 デフォルトは、`false` です。
   * A `java.lang.Boolean` 認証される署名フィールドがロックされているかどうかを指定するオブジェクト。 このフィールドがロックされている場合、署名フィールドは読み取り専用としてマークされ、プロパティは変更できません。また、必要な権限を持たないユーザーはこのフィールドをクリアできません。 デフォルトは、`false` です。
   * An `OCSPPreferences` オンライン証明書ステータスプロトコル (OCSP) サポートの環境設定を格納するオブジェクト。 失効確認が実行されない場合、このパラメーターは使用されず、次の項目を指定できます `null`. このオブジェクトについて詳しくは、 [AEM Forms API リファレンス](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).
   * A `CRLPreferences` 証明書失効リスト (CRL) の環境設定を保存するオブジェクト。 失効確認が実行されない場合、このパラメーターは使用されず、次の項目を指定できます `null`.
   * A `TSPPreferences` タイムスタンププロバイダー (TSP) がサポートする環境設定を保存するオブジェクト。 例えば、 `TSPPreferences` オブジェクトを使用する場合は、 `TSPPreferences` オブジェクトの `setTspServerURL` メソッド。 このパラメーターはオプションで、 `null`. 詳しくは、 [AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63).

   この `certify` メソッドは、 `com.adobe.idp.Document` 認証済みPDF文書を表すオブジェクト。

1. 認証済みPDFドキュメントをPDFファイルとして保存

   * `java.io.File` オブジェクトを作成し、ファイル拡張子が .pdf であることを確認します。
   * を呼び出す `com.adobe.idp.Document` オブジェクトの `copyToFile` メソッドを使用して、 `com.adobe.idp.Document` オブジェクトをファイルに追加します。

**関連トピック**

[PDF ドキュメントの認証](digitally-signing-certifying-documents.md#certifying-pdf-documents)

[クイックスタート（SOAP モード）:Java API を使用したPDFドキュメントの認証](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-certifying-a-pdf-document-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Web サービス API を使用したPDFドキュメントの認証 {#certify-pdf-documents-using-the-web-service-api}

Signature API（Web サービス）を使用してPDFドキュメントを認証します。

1. プロジェクトファイルを含める

   MTOM を使用するMicrosoft .NET プロジェクトを作成します。 次の WSDL 定義を使用していることを確認します。 `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >置換 `localhost` を、AEM Formsをホストするサーバーの IP アドレスに設定します。

1. 署名クライアントの作成

   * の作成 `SignatureServiceClient` オブジェクトのデフォルトのコンストラクタを使用します。
   * の作成 `SignatureServiceClient.Endpoint.Address` オブジェクトを `System.ServiceModel.EndpointAddress` コンストラクタ。 WSDL をAEM Formsサービスに渡す文字列値 ( 例： `http://localhost:8080/soap/services/SignatureService?WSDL`) をクリックします。 を使用する必要はありません。 `lc_version` 属性。 この属性は、サービス参照を作成する際に使用されます )。
   * の作成 `System.ServiceModel.BasicHttpBinding` オブジェクトを作成するには、 `SignatureServiceClient.Endpoint.Binding` フィールドに入力します。 戻り値を `BasicHttpBinding` にキャストします。
   * を `System.ServiceModel.BasicHttpBinding` オブジェクトの `MessageEncoding` ～に向かって `WSMessageEncoding.Mtom`. この値は、MTOM が確実に使用されるようにします。
   * 次のタスクを実行して、基本的な HTTP 認証を有効にします。

      * フィールドにAEM forms ユーザー名を割り当てます。 `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * 対応するパスワード値をフィールドに割り当てます。 `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * 定数値を割り当て `HttpClientCredentialType.Basic` フィールドに `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 定数値を割り当て `BasicHttpSecurityMode.TransportCredentialOnly` フィールドに `BasicHttpBindingSecurity.Security.Mode`.

1. 認証するPDFドキュメントを取得

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。この `BLOB` オブジェクトは、認証済みのPDFドキュメントを保存するために使用されます。
   * の作成 `System.IO.FileStream` オブジェクトを指定するには、コンストラクタを呼び出し、認証するPDFドキュメントのファイルの場所と、ファイルを開くモードを表す string 値を渡します。
   * コンテンツを格納するバイト配列を作成します。 `System.IO.FileStream` オブジェクト。 バイト配列のサイズは、 `System.IO.FileStream` オブジェクトの `Length` プロパティ。
   * を呼び出して、バイト配列にストリームデータを入力します。 `System.IO.FileStream` オブジェクトの `Read` メソッドを使用し、読み込むバイト配列、開始位置、ストリーム長を渡す。
   * 次の項目に `BLOB` オブジェクトを割り当てる `MTOM` data メンバは、バイト配列の内容を表します。

1. PDF文書を認証

   を呼び出してPDFドキュメントを認証する `SignatureServiceClient` オブジェクトの `certify` メソッドを使用して、次の値を渡します。

   * この `BLOB` 認証するPDFドキュメントを表すオブジェクト。
   * 署名を含む署名フィールドの名前を表す string 値です。
   * A `Credential` オブジェクトのドキュメントの認証に使用されるPDFを表すオブジェクト。 の作成 `Credential` オブジェクトを指定するには、コンストラクタを使用し、 `Credential` オブジェクトの `alias` プロパティ。
   * A `HashAlgorithm` オブジェクトドキュメントのダイジェストに使用するハッシュアルゴリズムを表す静的データPDFを指定するオブジェクト。 例えば、次の項目を指定できます。 `HashAlgorithm.SHA1` を使用して、SHA1 アルゴリズムを使用します。
   * ハッシュアルゴリズムを使用するかどうかを指定するブール値です。
   * PDFドキュメントが認証された理由を表す string 値です。
   * 署名者の場所を表す string 値です。
   * 署名者の連絡先情報を表す string 値です。
   * An `MDPPermissions` 署名を無効にする署名ドキュメントで実行できるアクションを指定する、PDFの静的なデータメンバーです。
   * 次を使用するかどうかを指定する Boolean 値 `MDPPermissions` 前のパラメーター値として渡されたオブジェクト。
   * 署名を無効にするアクションを説明する string 値です。
   * A `PDFSignatureAppearanceOptions` 認証済みの署名の外観を制御するオブジェクト。 コンストラクタを使用して `PDFSignatureAppearanceOptions` オブジェクトを作成します。署名のデータメンバーの 1 つを設定することで、署名の外観を変更できます。
   * A `System.Boolean` 署名者の証明書に対して失効確認を実行するかどうかを指定するオブジェクト。 この失効確認が完了すると、署名に埋め込まれます。 デフォルトは、`false` です。
   * A `System.Boolean` 認証される署名フィールドがロックされているかどうかを指定するオブジェクト。 このフィールドがロックされている場合、署名フィールドは読み取り専用としてマークされ、プロパティは変更できません。また、必要な権限を持たないユーザーはこのフィールドをクリアできません。 デフォルトは、`false` です。
   * A `System.Boolean` 署名フィールドをロックするかどうかを指定するオブジェクト。 つまり、 `true` を前のパラメーターに設定してから、 `true` をこのパラメーターに追加します。
   * An `OCSPPreferences` オブジェクトは、オンライン証明書ステータスプロトコル (OCSP) のサポートの環境設定を格納します。このオブジェクトは、PDFドキュメントの認証に使用される資格情報の状態に関する情報を提供します。 失効確認が実行されない場合、このパラメーターは使用されず、次の項目を指定できます `null`.
   * A `CRLPreferences` 証明書失効リスト (CRL) の環境設定を保存するオブジェクト。 失効確認が実行されない場合、このパラメーターは使用されず、次の項目を指定できます `null`.
   * A `TSPPreferences` タイムスタンププロバイダー (TSP) がサポートする環境設定を保存するオブジェクト。 例えば、 `TSPPreferences` オブジェクトの場合は、 `TSPPreferences` オブジェクトの `tspServerURL` データメンバー。 このパラメーターはオプションで、 `null`.

   この `certify` メソッドは、 `BLOB` 認証済みPDF文書を表すオブジェクト。

1. 認証済みPDFドキュメントをPDFファイルとして保存

   * の作成 `System.IO.FileStream` オブジェクトを呼び出し、認証済みPDFドキュメントを含むPDFドキュメントのファイルの場所と、ファイルを開くモードを表す string 値を渡すことによって、オブジェクトを取得します。
   * コンテンツを格納するバイト配列を作成します。 `BLOB` が返したオブジェクト `certify` メソッド。 バイト配列を生成するには、 `BLOB` オブジェクトの `binaryData` データメンバー。
   * の作成 `System.IO.BinaryWriter` オブジェクトのコンストラクタを呼び出し、 `System.IO.FileStream` オブジェクト。
   * を呼び出して、バイト配列の内容をPDFファイルに書き込みます。 `System.IO.BinaryWriter` オブジェクトの `Write` メソッドを使用してバイト配列を渡す。

**関連トピック**

[PDF ドキュメントの認証](digitally-signing-certifying-documents.md#certifying-pdf-documents)

[MTOM を使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRef を使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 電子署名の検証 {#verifying-digital-signatures}

電子署名を検証することで、署名された PDF ドキュメントに変更がなく、電子署名が有効であることを確認することができます。電子署名を検証する際に、署名のステータスや、署名者の ID などの署名のプロパティを確認できます。 電子署名を信用する前に、検証することをおすすめします。電子署名を検証する際、電子署名を含む PDF ドキュメントを参照します。

署名者の ID が不明であるとします。 AcrobatでPDFドキュメントを開くと、次の図に示すように、署名者の ID が不明であることを示す警告メッセージが表示されます。

![vd_vd_verifysig](assets/vd_vd_verifysig.png)

同様に、プログラムによって電子署名を検証する場合、署名者の ID のステータスを判断できます。 For example, if you verify the digital signature in the document shown in the previous illustration, the result would be that the signer’s identity is unknown.

>[!NOTE]
>
>Signature サービスと電子署名の検証について詳しくは、 [AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary_of_steps-6}

電子署名を検証するには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. Signature クライアントを作成します。
1. 検証するPDFが含まれている署名ドキュメントを取得します。
1. PKI の実行時オプションを設定します。
1. 電子署名を検証します。
1. 署名のステータスを決定します。
1. 署名者の ID を指定します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。 Web サービスを使用している場合は、プロキシファイルを含めます。

次の JAR ファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar(AEM Formsを JBoss にデプロイする場合に必要 )
* jbossall-client.jar(AEM Formsが JBoss にデプロイされている場合に必要 )

これらの JAR ファイルの場所について詳しくは、 [AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**署名クライアントの作成**

Signature サービスの操作をプログラムで実行する前に、Signature サービスクライアントを作成します。

**検証するPDFを含む署名ドキュメントを取得します**

署名ドキュメントのデジタル署名や認証に使用されるPDFを検証するには、署名を含むPDFドキュメントを取得します。

**PKI ランタイムオプションを設定**

Signature ドキュメント内の署名を検証する際に Signature サービスが使用する、次の PKI ランタイムPDFを設定します。

* 検証時間
* 失効確認
* タイムスタンプ値

これらのオプションを設定する際に、検証時間を指定できます。 例えば、現在の時刻（バリデーターのコンピューター上の時刻）を選択し、現在の時刻を使用するように指定できます。 様々な時間値について詳しくは、 `VerificationTime` の列挙値 [AEM Forms API リファレンス](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

また、検証プロセスの一環として失効確認を実行するかどうかを指定することもできます。 例えば、失効確認を実行して、証明書が失効しているかどうかを判断できます。 失効確認オプションについて詳しくは、 `RevocationCheckStyle` の列挙値 [AEM Forms API リファレンス](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

証明書に対して失効確認を実行するには、 `CRLOptionSpec` オブジェクト。 ただし、CRL サーバーへの URL を指定しない場合、Signature サービスは証明書から URL を取得します。

失効確認を実行する際には、CRL サーバーを使用する代わりに、オンライン証明書ステータスプロトコル (OCSP) サーバーを使用できます。 通常、CRL サーバーとは異なり OCSP サーバーを使用する場合は、失効確認の実行が高速になります。 ( [オンライン証明書ステータスプロトコル](https://tools.ietf.org/html/rfc2560).)

Signature サービスが使用する CRL および OCSP サーバーの順序は、Applications and ServicesAdobeを使用して設定できます。 例えば、OCSP サーバーが最初にAdobeのアプリケーションおよびサービスで設定されている場合、OCSP サーバーがチェックされ、次に CRL サーバーがチェックされます。

失効確認を実行しない場合、Signature サービスは証明書が失効しているかどうかを確認しません。 つまり、CRL および OCSP サーバー情報は無視されます。

>[!NOTE]
>
>証明書で指定された URL を上書きするには、 `CRLOptionSpec` および `OCSPOptionSpec` オブジェクト。 例えば、CRL サーバーを上書きする場合は、 `CRLOptionSpec` オブジェクトの `setLocalURI` メソッド。

タイムスタンプとは、署名済みまたは認証済みのドキュメントが変更された時間を追跡するプロセスです。 ドキュメントが署名された後は、誰もドキュメントを変更できません。 タイムスタンプを使用すると、署名済みまたは認証済みのドキュメントの有効性を強制することができます。 タイムスタンプオプションは、 `TSPOptionSpec` オブジェクト。 例えば、タイムスタンププロバイダー (TSP) サーバーの URL を指定できます。

>[!NOTE]
>
>Java および Web サービスのクイックスタートでは、検証時間が `VerificationTime.CURRENT_TIME` 失効確認は `RevocationCheckStyle.BestEffort`. CRL または OCSP サーバー情報が指定されていないので、サーバー情報は証明書から取得されます。

**電子署名の検証**

署名を正しく検証するには、署名が含まれている署名フィールドの完全修飾名を指定します（例： ）。 `form1[0].#subform[1].SignatureField3[3]`. XFA フォームフィールドを使用する場合、署名フィールドの名前の一部を使用することもできます。 `SignatureField3`.

デフォルトでは、Signature サービスは、検証時間の経過後にドキュメントに署名できる時間を 65 分に制限しています。 ユーザーが現在の時刻に署名を検証しようとして、署名時刻が現在の時刻より後で 65 分以内の場合、Signature サービスは検証エラーを作成しません。

>[!NOTE]
>
>署名の検証時に必要なその他の値については、 [AEM Forms API リファレンス](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**署名のステータスの決定**

電子署名の検証の一環として、署名のステータスを確認できます。

**署名者の ID を決定**

署名者の ID を決定できます。次の値のいずれかを指定できます。

* **不明**:署名者の検証を実行できないため、この署名者は不明です。
* **信頼済み**:この署名者は信頼されています。
* **信頼されていません**:この署名者は信頼されていません。

**関連トピック**

[Java API を使用した電子署名の検証](#unresolvedlink-lc-si)

[Web サービス API を使用した電子署名の検証](#unresolvedlink-lc-si)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Java API を使用した電子署名の検証 {#verify-digital-signatures-using-the-java-api}

Signature Service API(Java) を使用した電子署名の検証：

1. プロジェクトファイルを含める

   Java プロジェクトのクラスパスに、adobe-signatures-client.jar などのクライアント JAR ファイルを含めます。

1. [署名クライアントの作成](#unresolvedlink-lc-si)

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用して `SignatureServiceClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. 検証するPDFを含む署名ドキュメントを取得します

   * の作成 `java.io.FileInputStream` コンストラクタを使用してPDFする署名が含まれる検証ドキュメントを表すオブジェクト。 PDFドキュメントの場所を指定する string 値を渡します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. PKI ランタイムオプションを設定

   * コンストラクタを使用して `PKIOptions` オブジェクトを作成します。
   * を呼び出して検証時間を設定 `PKIOptions` オブジェクトの `setVerificationTime` メソッドと `VerificationTime` 検証時間を指定する列挙値。
   * を呼び出して失効確認オプションを設定します。 `PKIOptions` オブジェクトの `setRevocationCheckStyle` メソッドと `RevocationCheckStyle` 失効確認を実行するかどうかを指定する列挙値。

1. 電子署名の検証

   を呼び出して、署名を検証します。 `SignatureServiceClient` オブジェクトの `verify2` メソッドを使用して、次の値を渡します。

   * A `com.adobe.idp.Document` デジタル署名された、または認証されたPDFドキュメントを含むオブジェクト。
   * 検証する署名が含まれている署名フィールド名を表す string 値です。
   * A `PKIOptions` PKI ランタイムオプションを含むオブジェクト。
   * A `VerifySPIOptions` SPI 情報を含むインスタンス。 次を指定できます。 `null` を参照してください。

   この `verify2` メソッドは、 `PDFSignatureVerificationInfo` デジタル署名の検証に使用できる情報を含むオブジェクト。

1. 署名のステータスの決定

   * を呼び出して、署名のステータスを判断します。 `PDFSignatureVerificationInfo` オブジェクトの `getStatus` メソッド。 このメソッドは、 `SignatureStatus` 署名ステータスを指定するオブジェクト。 例えば、署名済みのPDF文書が変更されていない場合、このメソッドは `SignatureStatus.DocumentSigNoChanges`.

1. 署名者の ID を決定

   * を呼び出して、署名者の ID を特定します。 `PDFSignatureVerificationInfo` オブジェクトの `getSigner` メソッド。 このメソッドは、 `IdentityInformation` オブジェクト。
   * を呼び出す `IdentityInformation` オブジェクトの `getStatus` 署名者の id を決定する方法です。 このメソッドは、 `IdentityStatus` id を指定する列挙値。 例えば、署名者が信頼されている場合、このメソッドは `IdentityStatus.TRUSTED`.

**関連トピック**

[電子署名の検証](#unresolvedlink-lc-si)

[クイックスタート（SOAP モード）:Java API を使用したデジタル署名の検証](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-verifying-a-digital-signature-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Web サービス API を使用した電子署名の検証 {#verify-digital-signatures-using-the-web-service-api}

Signature Service API（Web サービス）を使用して電子署名を検証します。

1. プロジェクトファイルを含める

   MTOM を使用するMicrosoft .NET プロジェクトを作成します。 次の WSDL 定義を使用していることを確認します。 `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >置換 `localhost` を、AEM Formsをホストするサーバーの IP アドレスに設定します。

1. 署名クライアントの作成

   * の作成 `SignatureServiceClient` オブジェクトのデフォルトのコンストラクタを使用します。
   * の作成 `SignatureServiceClient.Endpoint.Address` オブジェクトを `System.ServiceModel.EndpointAddress` コンストラクタ。 WSDL をAEM Formsサービスに渡す文字列値 ( 例： `http://localhost:8080/soap/services/SignatureService?WSDL`) をクリックします。 を使用する必要はありません。 `lc_version` 属性。 この属性は、サービス参照を作成する際に使用されます )。
   * の作成 `System.ServiceModel.BasicHttpBinding` オブジェクトを作成するには、 `SignatureServiceClient.Endpoint.Binding` フィールドに入力します。 戻り値を `BasicHttpBinding` にキャストします。
   * を `System.ServiceModel.BasicHttpBinding` オブジェクトの `MessageEncoding` ～に向かって `WSMessageEncoding.Mtom`. この値は、MTOM が確実に使用されるようにします。
   * 次のタスクを実行して、基本的な HTTP 認証を有効にします。

      * フィールドにAEM forms ユーザー名を割り当てます。 `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * 対応するパスワード値をフィールドに割り当てます。 `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * 定数値を割り当て `HttpClientCredentialType.Basic` フィールドに `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 定数値を割り当て `BasicHttpSecurityMode.TransportCredentialOnly` フィールドに `BasicHttpBindingSecurity.Security.Mode`.

1. 検証するPDFを含む署名ドキュメントを取得します

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。この `BLOB` オブジェクトは、検証するデジタルPDFまたは認証署名が含まれる署名ドキュメントを保存するために使用されます。
   * の作成 `System.IO.FileStream` オブジェクトを指定します。 署名済みPDFドキュメントのファイルの場所と、ファイルを開くモードを表す string 値を渡します。
   * コンテンツを格納するバイト配列を作成します。 `System.IO.FileStream` オブジェクト。 バイト配列のサイズは、 `System.IO.FileStream` オブジェクトの `Length` プロパティ。
   * を呼び出して、バイト配列にストリームデータを入力します。 `System.IO.FileStream` オブジェクトの `Read` メソッド。 読み取るバイト配列、開始位置、ストリーム長を渡します。
   * 次の項目に `BLOB` オブジェクトを割り当てる `MTOM` プロパティは、バイト配列の内容を示します。

1. PKI ランタイムオプションを設定

   * コンストラクタを使用して `PKIOptions` オブジェクトを作成します。
   * 検証時間を設定するには、 `PKIOptions` オブジェクトの `verificationTime` データメンバー a `VerificationTime` 検証時間を指定する列挙値。
   * 失効確認オプションを設定するには、 `PKIOptions` オブジェクトの `revocationCheckStyle` データメンバー a `RevocationCheckStyle` 失効確認を実行するかどうかを指定する列挙値。

1. 電子署名の検証

   を呼び出して、署名を検証します。 `SignatureServiceClient` オブジェクトの `verify2` メソッドを使用して、次の値を渡します。

   * この `BLOB` デジタル署名された、または認証されたPDFドキュメントを含むオブジェクト。
   * 検証する署名が含まれている署名フィールド名を表す string 値です。
   * A `PKIOptions` PKI ランタイムオプションを含むオブジェクト。
   * A `VerifySPIOptions` SPI 情報を含むインスタンス。 次を指定できます。 `null` を参照してください。

   この `verify2` メソッドは、 `PDFSignatureVerificationInfo` デジタル署名の検証に使用できる情報を含むオブジェクト。

1. 署名のステータスの決定

   署名のステータスを決定するには、 `PDFSignatureVerificationInfo` オブジェクトの `status` データメンバー。 このデータメンバーは、 `SignatureStatus` 署名のステータスを指定するオブジェクト。 例えば、署名済みのPDFドキュメントを変更する場合、 `status` データメンバーが値を保存 `SignatureStatus.DocumentSigNoChanges`.

1. 署名者の ID を決定

   * 署名者の ID を確認するには、 `PDFSignatureVerificationInfo` オブジェクトの `signer` データメンバー。 このメンバーは `IdentityInformation` オブジェクト。
   * の取得 `IdentityInformation` オブジェクトの `status` 署名者の ID を決定するデータメンバー。 このデータメンバは、 `IdentityStatus` id を指定する列挙値。 例えば、署名者が信頼されている場合、このメンバーは `IdentityStatus.TRUSTED`.

**関連トピック**

[電子署名の検証](#unresolvedlink-lc-si)

[MTOM を使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRef を使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 複数のデジタル署名の検証 {#verifying-multiple-digital-signatures}

AEM Formsは、PDFドキュメント内のすべての電子署名を検証する手段を提供します。 複数の署名者からのPDFを必要とするビジネスプロセスの結果、署名ドキュメントに複数の電子署名が含まれているとします。 例えば、融資担当者の署名と管理者の署名の両方を必要とする金融取引を考えてみましょう。 Signature service Java API または Web サービス API を使用して、署名ドキュメント内のすべてのPDFを検証できます。 複数の署名を検証する際は、それぞれの署名のステータスやプロパティを確認できます。電子署名を信頼する前に、確認することをお勧めします。 単一のデジタル署名の検証に精通していることをお勧めします。

>[!NOTE]
>
>Signature サービスと電子署名の検証について詳しくは、 [AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary_of_steps-7}

複数の電子署名を検証するには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. Signature クライアントを作成します。
1. 検証するPDFが含まれている署名ドキュメントを取得します。
1. PKI の実行時オプションを設定します。
1. すべての電子署名を取得します。
1. すべての署名を繰り返し処理します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。 Web サービスを使用している場合は、プロキシファイルを含めます。

次の JAR ファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar(AEM Formsを JBoss にデプロイする場合に必要 )
* jbossall-client.jar(AEM Formsが JBoss にデプロイされている場合に必要 )

これらの JAR ファイルの場所について詳しくは、 [AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**署名クライアントの作成**

Signature サービスの操作をプログラムで実行する前に、Signature サービスクライアントを作成します。

**検証するPDFが含まれている署名ドキュメントを取得します**

署名ドキュメントのデジタル署名や認証に使用されるPDFを検証するには、署名を含むPDFドキュメントを取得します。

**PKI ランタイムオプションを設定**

Signature ドキュメント内のすべての署名を検証する際に Signature サービスが使用する、次の PKI ランタイムPDFを設定します。

* 検証時間
* 失効確認
* タイムスタンプ値

これらのオプションを設定する際に、検証時間を指定できます。 例えば、現在の時刻（バリデーターのコンピューター上の時刻）を選択し、現在の時刻を使用するように指定できます。 様々な時間値について詳しくは、 `VerificationTime` の列挙値 [AEM Forms API リファレンス](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

また、検証プロセスの一環として失効確認を実行するかどうかを指定することもできます。 例えば、失効確認を実行して、証明書が失効しているかどうかを判断できます。 失効確認オプションについて詳しくは、 `RevocationCheckStyle` の列挙値 [AEM Forms API リファレンス](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

証明書に対して失効確認を実行するには、 `CRLOptionSpec` オブジェクト。 ただし、CRL サーバーへの URL を指定しない場合、Signature サービスは証明書から URL を取得します。

失効確認を実行する際には、CRL サーバーを使用する代わりに、オンライン証明書ステータスプロトコル (OCSP) サーバーを使用できます。 通常、CRL サーバーではなく OCSP サーバーを使用する場合は、失効確認の実行が高速になります。 ( [オンライン証明書ステータスプロトコル](https://tools.ietf.org/html/rfc2560).)

Signature サービスが使用する CRL および OCSP サーバーの順序は、Applications and ServicesAdobeを使用して設定できます。 例えば、Adobeのアプリケーションとサービスで OCSP サーバーを最初に設定した場合、OCSP サーバーがチェックされ、その後に CRL サーバーがチェックされます。

失効確認を実行しない場合、Signature サービスは証明書が失効しているかどうかを確認しません。 つまり、CRL および OCSP サーバー情報は無視されます。

>[!NOTE]
>
>証明書で指定された URL を上書きするには、 `CRLOptionSpec` および `OCSPOptionSpec` オブジェクト。 例えば、CRL サーバーを上書きする場合は、 `CRLOptionSpec` オブジェクトの `setLocalURI` メソッド。

タイムスタンプとは、署名済みまたは認証済みのドキュメントが変更された時間を追跡するプロセスです。 ドキュメントが署名された後は、誰もドキュメントを変更できません。 タイムスタンプを使用すると、署名済みまたは認証済みのドキュメントの有効性を強制することができます。 タイムスタンプオプションは、 `TSPOptionSpec` オブジェクト。 例えば、タイムスタンププロバイダー (TSP) サーバーの URL を指定できます。

>[!NOTE]
>
>Java および Web サービスのクイックスタートでは、検証時間が `VerificationTime.CURRENT_TIME` 失効確認は `RevocationCheckStyle.BestEffort`. CRL または OCSP サーバー情報が指定されていないので、サーバー情報は証明書から取得されます。

**すべての電子署名を取得する**

PDFドキュメント内のすべての電子署名を検証するには、PDFドキュメントから電子署名を取得します。 すべての署名がリストで返されます。 電子署名の検証の一環として、署名のステータスを確認します。

>[!NOTE]
>
>単一の電子署名を検証する場合とは異なり、複数の署名を検証する場合は、署名フィールド名を指定する必要はありません。

**すべての署名を繰り返し処理**

各署名を繰り返し処理します。 つまり、署名ごとに電子署名を検証し、署名者の ID と各署名のステータスを確認します。 ( [電子署名の検証](#unresolvedlink-lc-si).)

>[!NOTE]
>
>ドキュメント全体が要件の場合は、すべての署名を繰り返し処理する必要はありません。

**関連トピック**

[Java API を使用した複数の電子署名の検証](#unresolvedlink-lc-si)

[Web サービス API を使用した複数の電子署名の検証](#unresolvedlink-lc-si)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Java API を使用した複数の電子署名の検証 {#verify-multiple-digital-signatures-using-the-java-api}

Signature Service API(Java) を使用して、複数の電子署名を検証します。

1. プロジェクトファイルを含める

   Java プロジェクトのクラスパスに、adobe-signatures-client.jar などのクライアント JAR ファイルを含めます。

1. 署名クライアントの作成

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用して `SignatureServiceClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. 検証するPDFが含まれている署名ドキュメントを取得します

   * の作成 `java.io.FileInputStream` コンストラクタを使用してPDFする複数の電子署名が含まれる検証ドキュメントを表すオブジェクト。 PDFドキュメントの場所を指定する string 値を渡します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. PKI ランタイムオプションを設定

   * コンストラクタを使用して `PKIOptions` オブジェクトを作成します。
   * を呼び出して検証時間を設定 `PKIOptions` オブジェクトの `setVerificationTime` メソッドと `VerificationTime` 検証時間を指定する列挙値。
   * を呼び出して、失効確認オプションを設定します。 `PKIOptions` オブジェクトの `setRevocationCheckStyle` メソッドと `RevocationCheckStyle` 失効確認を実行するかどうかを指定する列挙値。

1. すべての電子署名を取得する

   を呼び出す `SignatureServiceClient` オブジェクトの `verifyPDFDocument` メソッドを使用して、次の値を渡します。

   * A `com.adobe.idp.Document` 複数の電子署名を含むPDFドキュメントを含むオブジェクト。
   * A `PKIOptions` PKI ランタイムオプションを含むオブジェクト。
   * A `VerifySPIOptions` SPI 情報を含むインスタンス。 次を指定できます。 `null` を参照してください。

   この `verifyPDFDocument` メソッドは、 `PDFDocumentVerificationInfo` オブジェクトドキュメント内のすべての電子署名に関する情報を含むPDF。

1. すべての署名を繰り返し処理

   * を呼び出すことで、すべての署名を繰り返し処理します。 `PDFDocumentVerificationInfo` オブジェクトの `getVerificationInfos` メソッド。 このメソッドは、 `java.util.List` 各要素が `PDFSignatureVerificationInfo` オブジェクト。 の使用 `java.util.Iterator` オブジェクトを使用して、署名のリストを反復処理します。
   * の使用 `PDFSignatureVerificationInfo` オブジェクトを使用すると、 `PDFSignatureVerificationInfo` オブジェクトの `getStatus` メソッド。 このメソッドは、 `SignatureStatus` 静的データメンバーが署名のステータスを通知するオブジェクト。 例えば、署名が不明な場合、このメソッドは `SignatureStatus.DocumentSignatureUnknown`.

**関連トピック**

[複数のデジタル署名の検証](#unresolvedlink-lc-si)

[クイックスタート（SOAP モード）:Java API を使用した複数の電子署名の検証](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-verifying-multiple-digital-signatures-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[電子署名の検証](#unresolvedlink-lc-si)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Web サービス API を使用した複数の電子署名の検証 {#verifying-multiple-digital-signatures-using-the-web-service-api}

Signature Service API（Web サービス）を使用して、複数の電子署名を検証します。

1. プロジェクトファイルを含める

   MTOM を使用するMicrosoft .NET プロジェクトを作成します。 次の WSDL 定義を使用していることを確認します。 `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >置換 `localhost` を、AEM Formsをホストするサーバーの IP アドレスに設定します。

1. 署名クライアントの作成

   * の作成 `SignatureServiceClient` オブジェクトのデフォルトのコンストラクタを使用します。
   * の作成 `SignatureServiceClient.Endpoint.Address` オブジェクトを `System.ServiceModel.EndpointAddress` コンストラクタ。 WSDL をAEM Formsサービスに渡す文字列値 ( 例： `http://localhost:8080/soap/services/SignatureService?WSDL`) をクリックします。 を使用する必要はありません。 `lc_version` 属性。 この属性は、サービス参照を作成する際に使用されます )。
   * の作成 `System.ServiceModel.BasicHttpBinding` オブジェクトを作成するには、 `SignatureServiceClient.Endpoint.Binding` フィールドに入力します。 戻り値を `BasicHttpBinding` にキャストします。
   * を `System.ServiceModel.BasicHttpBinding` オブジェクトの `MessageEncoding` ～に向かって `WSMessageEncoding.Mtom`. この値は、MTOM が確実に使用されるようにします。
   * 次のタスクを実行して、基本的な HTTP 認証を有効にします。

      * フィールドにAEM forms ユーザー名を割り当てます。 `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * 対応するパスワード値をフィールドに割り当てます。 `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * 定数値を割り当て `HttpClientCredentialType.Basic` フィールドに `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 定数値を割り当て `BasicHttpSecurityMode.TransportCredentialOnly` フィールドに `BasicHttpBindingSecurity.Security.Mode`.

1. 検証するPDFが含まれている署名ドキュメントを取得します

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。この `BLOB` オブジェクトは、検証する複数のPDFを含む署名ドキュメントを格納します。
   * の作成 `System.IO.FileStream` オブジェクトを指定します。 PDFドキュメントのファイルの場所と、ファイルを開くモードを表す string 値を渡します。
   * コンテンツを格納するバイト配列を作成します。 `System.IO.FileStream` オブジェクト。 バイト配列のサイズは、 `System.IO.FileStream` オブジェクトの `Length` プロパティ。
   * を呼び出して、バイト配列にストリームデータを入力します。 `System.IO.FileStream` オブジェクトの `Read` メソッド。 読み取るバイト配列、開始位置、ストリーム長を渡します。
   * 次の項目に `BLOB` オブジェクトを割り当てる `MTOM` プロパティは、バイト配列の内容を示します。

1. PKI ランタイムオプションを設定

   * コンストラクタを使用して `PKIOptions` オブジェクトを作成します。
   * 検証時間を設定するには、 `PKIOptions` オブジェクトの `verificationTime` データメンバー a `VerificationTime` 検証時間を指定する列挙値。
   * 失効確認オプションを設定するには、 `PKIOptions` オブジェクトの `revocationCheckStyle` データメンバー a `RevocationCheckStyle` 失効確認を実行するかどうかを指定する列挙値。

1. すべての電子署名を取得する

   を呼び出す `SignatureServiceClient` オブジェクトの `verifyPDFDocument` メソッドを使用して、次の値を渡します。

   * A `BLOB` 複数の電子署名を含むPDFドキュメントを含むオブジェクト。
   * A `PKIOptions` PKI ランタイムオプションを含むオブジェクト。
   * A `VerifySPIOptions` SPI 情報を含むインスタンス。 このパラメーターには null を指定できます。

   この `verifyPDFDocument` メソッドは、 `PDFDocumentVerificationInfo` オブジェクトドキュメント内のすべての電子署名に関する情報を含むPDF。

1. すべての署名を繰り返し処理

   * すべての署名を繰り返し処理し、 `PDFDocumentVerificationInfo` オブジェクトの `verificationInfos` データメンバー。 このデータメンバは、 `Object` 各要素が `PDFSignatureVerificationInfo` オブジェクト。
   * の使用 `PDFSignatureVerificationInfo` オブジェクトを使用すると、署名のステータスを確認するタスクなどを実行できます。その場合、 `PDFSignatureVerificationInfo` オブジェクトの `status` データメンバー。 このデータメンバは、 `SignatureStatus` 静的データメンバーが署名のステータスを通知するオブジェクト。 例えば、署名が不明な場合、このメソッドは `SignatureStatus.DocumentSignatureUnknown`.

**関連トピック**

[複数のデジタル署名の検証](#unresolvedlink-lc-si)

[MTOM を使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRef を使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 電子署名の削除 {#removing-digital-signatures}

新しい電子署名を適用する前に、電子署名を署名フィールドから削除する必要があります。 電子署名は上書きできません。 署名が含まれる署名フィールドに電子署名を適用しようとすると、例外が発生します。

>[!NOTE]
>
>Signature サービスについて詳しくは、 [AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary_of_steps-8}

署名フィールドから電子署名を削除するには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. Signature クライアントを作成します。
1. 削除するPDFを含む署名ドキュメントを取得します。
1. 署名フィールドから電子署名を削除します。
1. PDF・ドキュメントをPDF・ファイルとして保存します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。 Web サービスを使用している場合は、プロキシファイルを必ず含めてください。

次の JAR ファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar(AEM Formsを JBoss にデプロイする場合に必要 )
* jbossall-client.jar(AEM Formsが JBoss にデプロイされている場合に必要 )

これらの JAR ファイルの場所について詳しくは、 [AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**署名クライアントの作成**

Signature サービスの操作をプログラムで実行する前に、Signature サービスクライアントを作成する必要があります。

**削除するPDFを含む署名ドキュメントを取得します**

署名ドキュメントからPDFを削除するには、署名が含まれるPDFドキュメントを取得する必要があります。

**署名フィールドから電子署名を削除します**

PDFドキュメントから電子署名を正しく削除するには、電子署名が含まれている署名フィールドの名前を指定する必要があります。 また、電子署名を削除する権限が必要です。そうしないと、例外が発生します。

**PDFドキュメントをPDFファイルとして保存**

Signature サービスでPDFフィールドから電子署名が削除されたら、署名ドキュメントをPDFファイルとして保存し、AcrobatまたはAdobe Readerで開くことができます。

**関連トピック**

[Java API を使用した電子署名の削除](digitally-signing-certifying-documents.md#remove-digital-signatures-using-the-java-api)

[Web サービス API を使用して電子署名を削除する](digitally-signing-certifying-documents.md#remove-digital-signatures-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[署名フィールドの追加](digitally-signing-certifying-documents.md#adding-signature-fields)

### Java API を使用した電子署名の削除 {#remove-digital-signatures-using-the-java-api}

署名 API(Java) を使用して電子署名を削除するには、次の手順を実行します。

1. プロジェクトファイルを含める

   Java プロジェクトのクラスパスに、adobe-signatures-client.jar などのクライアント JAR ファイルを含めます。

1. Signature クライアントを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用して `SignatureServiceClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. 削除するPDFを含む署名ドキュメントを取得します

   * の作成 `java.io.FileInputStream` 削除するPDFが含まれる署名ドキュメントを表すオブジェクト。このオブジェクトのコンストラクタを使用し、PDFドキュメントの場所を指定する string 値を渡します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. 署名フィールドから電子署名を削除します

   を呼び出して、署名フィールドから電子署名を削除する `SignatureServiceClient` オブジェクトの `clearSignatureField` メソッドを使用して、次の値を渡します。

   * A `com.adobe.idp.Document` 削除する署名が含まれるPDFドキュメントを表すオブジェクト。
   * 電子署名が含まれる署名フィールドの名前を指定する string 値です。

   この `clearSignatureField` メソッドは、 `com.adobe.idp.Document` 電子署名が削除されたPDFドキュメントを表すオブジェクト。

1. PDFドキュメントをPDFファイルとして保存

   * `java.io.File` オブジェクトを作成し、ファイル拡張子が .pdf であることを確認します。
   * を呼び出す `com.adobe.idp.Document` オブジェクトの `copyToFile` メソッド。 パス `java.io.File` オブジェクトを使用して、 `com.adobe.idp.Document` オブジェクトをファイルに追加します。 `Document` メソッドから返された `clearSignatureField` オブジェクトを必ず使用してください。

**関連トピック**

[電子署名の削除](digitally-signing-certifying-documents.md#removing-digital-signatures)

[クイックスタート（SOAP モード）:Java API を使用した電子署名の削除](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-removing-a-digital-signature-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Web サービス API を使用して電子署名を削除する {#remove-digital-signatures-using-the-web-service-api}

Signature API（Web サービス）を使用して電子署名を削除します。

1. プロジェクトファイルを含める

   MTOM を使用するMicrosoft .NET プロジェクトを作成します。 次の WSDL 定義を使用していることを確認します。 `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >置換 `localhost` を、AEM Formsをホストするサーバーの IP アドレスに設定します。

1. 署名クライアントの作成

   * の作成 `SignatureServiceClient` オブジェクトのデフォルトのコンストラクタを使用します。
   * の作成 `SignatureServiceClient.Endpoint.Address` オブジェクトを `System.ServiceModel.EndpointAddress` コンストラクタ。 WSDL をAEM Formsサービスに渡す文字列値 ( 例： `http://localhost:8080/soap/services/SignatureService?WSDL`) をクリックします。 を使用する必要はありません。 `lc_version` 属性。 この属性は、サービス参照を作成する際に使用されます )。
   * の作成 `System.ServiceModel.BasicHttpBinding` オブジェクトを作成するには、 `SignatureServiceClient.Endpoint.Binding` フィールドに入力します。 戻り値を `BasicHttpBinding` にキャストします。
   * を `System.ServiceModel.BasicHttpBinding` オブジェクトの `MessageEncoding` ～に向かって `WSMessageEncoding.Mtom`. この値は、MTOM が確実に使用されるようにします。
   * 次のタスクを実行して、基本的な HTTP 認証を有効にします。

      * フィールドにAEM forms ユーザー名を割り当てます。 `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * 対応するパスワード値をフィールドに割り当てます。 `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * 定数値を割り当て `HttpClientCredentialType.Basic` フィールドに `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 定数値を割り当て `BasicHttpSecurityMode.TransportCredentialOnly` フィールドに `BasicHttpBindingSecurity.Security.Mode`.

1. 削除するPDFを含む署名ドキュメントを取得します

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。この `BLOB` オブジェクトは、削除する電子PDFが含まれる署名ドキュメントを保存するために使用されます。
   * の作成 `System.IO.FileStream` オブジェクトを呼び出し、署名付きPDFドキュメントのファイルの場所と、ファイルを開くモードを表す string 値を渡すことによってオブジェクトを指定します。
   * コンテンツを格納するバイト配列を作成します。 `System.IO.FileStream` オブジェクト。 バイト配列のサイズは、 `System.IO.FileStream` オブジェクトの `Length` プロパティ。
   * を呼び出して、バイト配列にストリームデータを入力します。 `System.IO.FileStream` オブジェクトの `Read` メソッド。 読み取るバイト配列、開始位置、ストリーム長を渡します。
   * 次の項目に `BLOB` オブジェクトを割り当てる `MTOM` プロパティにバイト配列の内容を入力します。

1. 署名フィールドから電子署名を削除します

   を呼び出して電子署名を削除する `SignatureServiceClient` オブジェクトの `clearSignatureField` メソッドを使用して、次の値を渡します。

   * A `BLOB` 署名済みPDF文書を含むオブジェクト。
   * 削除する電子署名が含まれる署名フィールドの名前を表す string 値です。

   この `clearSignatureField` メソッドは、 `BLOB` 電子署名が削除されたPDFドキュメントを表すオブジェクト。

1. PDFドキュメントをPDFファイルとして保存

   * の作成 `System.IO.FileStream` オブジェクトを呼び出し、空のPDFフィールドとファイルを開くモードを含む署名ドキュメントのファイルの場所を表す string 値を渡すことによってオブジェクトを取得します。
   * コンテンツを格納するバイト配列を作成します。 `BLOB` が返したオブジェクト `sign` メソッド。 バイト配列を生成するには、 `BLOB` オブジェクトの `MTOM` データメンバー。
   * の作成 `System.IO.BinaryWriter` オブジェクトのコンストラクタを呼び出し、 `System.IO.FileStream` オブジェクト。
   * を呼び出して、バイト配列の内容をPDFファイルに書き込みます。 `System.IO.BinaryWriter` オブジェクトの `Write` メソッドを使用してバイト配列を渡す。

**関連トピック**

[電子署名の削除](digitally-signing-certifying-documents.md#removing-digital-signatures)

[MTOM を使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRef を使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
