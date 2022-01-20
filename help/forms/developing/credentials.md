---
title: 資格情報の操作
seo-title: Working with Credentials
description: Trust Manager API と Java API を使用して、資格情報をAEM Formsに読み込みます。 さらに、Trust Manager API と Java API を使用して資格情報を削除する方法についても説明します。
seo-description: Import credentials into AEM Forms using the Trust Manager API and Java API. In addition, learn how to delete credentials using the Trust Manager API and Java API.
uuid: b794428f-49bf-4a91-bc5f-d855881f4f38
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: operations
discoiquuid: bc06d9bd-af6c-47b1-b46f-aab990ef5816
role: Developer
exl-id: 7dcfcee1-998e-41d8-badc-3106055e6ba7
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '1071'
ht-degree: 12%

---

# 資格情報の操作 {#working-with-credentials}

**資格情報サービスについて**

秘密鍵証明書には、ドキュメントへの署名や識別に必要な秘密鍵情報が格納されています。証明書は、信頼のために設定する公開鍵情報です。AEM Formsは、いくつかの目的で証明書と資格情報を使用します。

* Acrobat Reader DC Extensions では、秘密鍵証明書を使用して、PDF ドキュメントで Adobe Reader の使用権限を有効にします。( [使用権限のPDF・ドキュメントへの適用](/help/forms/developing/assigning-usage-rights.md#applying-usage-rights-to-pdf-documents).)
* Signature サービスは、証明書ドキュメントへの電子署名などの操作を実行しながら、証明書と資格情報にPDFします。 ( [デジタル署名PDF文書](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-pdf-documents).)

Trust Manager Java API を使用して、プログラムによる資格情報サービスの操作を行うことができます。 次のタスクを実行できます。

* [Trust Manager API を使用した資格情報の読み込み](credentials.md#importing-credentials-by-using-the-trust-manager-api)
* [Trust Manager API を使用した資格情報の削除](credentials.md#deleting-credentials-by-using-the-trust-manager-api)

>[!NOTE]
>
>管理コンソールを使用して証明書を読み込んだり、削除したりすることもできます。 ( [管理ヘルプ。](https://www.adobe.com/go/learn_aemforms_admin_63))

## Trust Manager API を使用した資格情報の読み込み {#importing-credentials-by-using-the-trust-manager-api}

Trust Manager API を使用して、プログラムによって秘密鍵証明書をAEM Formsに読み込むことができます。 例えば、証明書ドキュメントへの署名に使用する秘密鍵証明書をPDFできます。 ( [デジタル署名PDF文書](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)) をクリックします。

秘密鍵証明書を読み込む際は、秘密鍵証明書のエイリアスを指定します。 エイリアスは、秘密鍵証明書を必要とするForms操作を実行する際に使用されます。 次の図に示すように、読み込んだ秘密鍵証明書は管理コンソールで表示できます。 秘密鍵証明書のエイリアスが *セキュア*.

![ww_ww_truststore](assets/ww_ww_truststore.png)

>[!NOTE]
>
>Web サービスを使用してAEM Formsに秘密鍵証明書を読み込むことはできません。

### 手順の概要 {#summary-of-steps}

秘密鍵証明書をAEM Formsに読み込むには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. 資格情報サービスクライアントを作成します。
1. 秘密鍵証明書を参照します。
1. インポート操作を実行します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。 Web サービスを使用している場合は、プロキシファイルを必ず含めてください。

次の JAR ファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-truststore-client.jar
* adobe-utilities.jar(AEM Formsを JBoss にデプロイする場合に必須 )
* jbossall-client.jar(AEM Formsが JBoss にデプロイされている場合に必須 )

これらの JAR ファイルの場所について詳しくは、 [AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**資格情報サービスクライアントの作成**

プログラムによって秘密鍵証明書をAEM Formsに読み込む前に、秘密鍵証明書サービスクライアントを作成します。 詳しくは、 [接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).

**秘密鍵証明書の参照**

AEM Formsに読み込む秘密鍵証明書を参照します。 このセクションに関連するクイックスタートは、ファイルシステム内の P12 ファイルを参照します。

**インポート操作の実行**

秘密鍵証明書を参照した後、秘密鍵証明書をAEM Formsに読み込みます。 秘密鍵証明書が正常に読み込まれない場合は、例外がスローされます。 秘密鍵証明書を読み込む際は、秘密鍵証明書のエイリアスを指定します。

**関連トピック**

[Java API を使用した資格情報の読み込み](credentials.md#import-credentials-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[資格情報サービス API のクイックスタート](/help/forms/developing/credential-service-java-api-quick.md#credential-service-java-api-quick-start-soap)

[Trust Manager API を使用した資格情報の削除](credentials.md#deleting-credentials-by-using-the-trust-manager-api)

### Java API を使用した資格情報の読み込み {#import-credentials-using-the-java-api}

Trust Manager API(Java) を使用して、秘密鍵証明書をAEM Formsに読み込みます。

1. プロジェクトファイルを含める

   Java プロジェクトのクラスパスに、adobe-truststore-client.jar などのクライアント JAR ファイルを含めます。

1. 資格情報サービスクライアントの作成

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用して `CredentialServiceClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. 秘密鍵証明書の参照

   * コンストラクタを使用して `java.io.FileInputStream` オブジェクトを作成します。秘密鍵証明書の場所を指定する string 値を渡します。
   * の作成 `com.adobe.idp.Document` を使用して秘密鍵証明書を保存するオブジェクト `com.adobe.idp.Document` コンストラクタ。 パス `java.io.FileInputStream` コンストラクタに対する資格情報を含むオブジェクト。

1. インポート操作の実行

   * 1 つの要素を保持する文字列配列を作成します。 値を割り当て `truststore.usage.type.sign` を要素に追加します。
   * を呼び出す `CredentialServiceClient` オブジェクトの `importCredential` メソッドを使用して、次の値を渡します。

      * 秘密鍵証明書のエイリアス値を指定する string 値です。
      * この `com.adobe.idp.Document` 秘密鍵証明書を保存するインスタンス。
      * 秘密鍵証明書に関連付けられているパスワードを指定する string 値です。
      * usage 値を含む文字列配列。 例えば、次の値を指定できます。 `truststore.usage.type.sign`. Reader拡張機能の秘密鍵証明書を読み込むには、 `truststore.usage.type.lcre`.

**関連トピック**

[Trust Manager API を使用した資格情報の読み込み](credentials.md#importing-credentials-by-using-the-trust-manager-api)

[クイックスタート（SOAP モード）:Java API を使用した資格情報の読み込み](/help/forms/developing/credential-service-java-api-quick.md#quick-start-soap-mode-importing-credentials-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Trust Manager API を使用した資格情報の削除 {#deleting-credentials-by-using-the-trust-manager-api}

Trust Manager API を使用して、プログラムによって秘密鍵証明書を削除できます。 秘密鍵証明書を削除する際には、秘密鍵証明書に対応するエイリアスを指定します。 削除した後は、秘密鍵証明書を使用して操作を実行できません。

>[!NOTE]
>
>Web サービスを使用してAEM Formsに秘密鍵証明書を削除することはできません。

### 手順の概要 {#summary_of_steps-1}

秘密鍵証明書を削除するには、次の手順に従います。

1. プロジェクトファイルを含めます。
1. 資格情報サービスクライアントを作成します。
1. 削除操作を実行します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。 次の JAR ファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-truststore-client.jar
* adobe-utilities.jar(AEM Formsを JBoss にデプロイする場合に必須 )
* jbossall-client.jar(AEM Formsが JBoss にデプロイされている場合に必須 )

これらの JAR ファイルの場所について詳しくは、 [AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**資格情報サービスクライアントの作成**

プログラムによって秘密鍵証明書を削除する前に、Data Integration Service クライアントを作成します。 サービスクライアントを作成する場合、サービスを呼び出すために必要な接続設定を定義します。 詳しくは、 [接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).

**削除操作の実行**

秘密鍵証明書を削除するには、秘密鍵証明書に対応するエイリアスを指定します。 存在しないエイリアスを指定すると、例外が発生します。

**関連トピック**

[Java API を使用した資格情報の読み込み](credentials.md#import-credentials-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Java API を使用した資格情報の読み込み](credentials.md#import-credentials-using-the-java-api)

### Java API を使用した資格情報の削除 {#deleting-credentials-using-the-java-api}

Trust Manager API(Java) を使用して、AEM Formsから秘密鍵証明書を削除します。

1. プロジェクトファイルを含める

   Java プロジェクトのクラスパスに、adobe-truststore-client.jar などのクライアント JAR ファイルを含めます。

1. 資格情報サービスクライアントの作成

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用して `CredentialServiceClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. 削除操作の実行

   を呼び出す `CredentialServiceClient` オブジェクトの `deleteCredential` メソッドを使用してエイリアス値を指定する string 値を渡します。

**関連トピック**

[Trust Manager API を使用した資格情報の削除](credentials.md#deleting-credentials-by-using-the-trust-manager-api)

[クイックスタート（SOAP モード）:Java API を使用した資格情報の削除](/help/forms/developing/credential-service-java-api-quick.md#quick-start-soap-mode-deleting-credentials-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)
