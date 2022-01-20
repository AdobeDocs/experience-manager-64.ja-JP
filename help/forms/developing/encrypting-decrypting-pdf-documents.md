---
title: 暗号化および復号化PDF・ドキュメント
seo-title: Encrypting and Decrypting PDF Documents
description: Encryption サービスを使用して、ドキュメントを暗号化および復号化します。 Encryption サービスタスクは、PDF文書をPDFで暗号化し、証明書で暗号化し、PDF文書からパスワードで暗号化を解除し、PDF文書から証明書で暗号化を解除し、他のサービス操作が可能なPDF文書を解除し、保護されたPDF文書の暗号化の種類を決定する。
seo-description: Use the Encryption service to encrypt and decrypt documents. The Encryption service tasks include encrypting a PDF document with a password, encrypting a PDF document with a certificate, removing password-based encryption from a PDF document, removing certificate-based encryption from a PDF document, unlocking the PDF document so that other service operations can be performed, and determining the encryption type of a secured PDF document.
uuid: 4e4e2716-c21f-4bfe-ae7a-7e91442414ef
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: operations
discoiquuid: 5e4bda3a-5648-4c0f-b2f8-bdbebb88f537
role: Developer
exl-id: 670d9680-6125-4a48-82ef-78f1630d780f
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '8175'
ht-degree: 8%

---

# 暗号化および復号化PDF・ドキュメント {#encrypting-and-decrypting-pdf-documents}

**Encryption サービスについて**

Encryption サービスを使用すると、ドキュメントの暗号化と復号化をおこなえます。 ドキュメントを暗号化すると、その内容は判読できなくなります。許可されたユーザーはドキュメントを復号化して、コンテンツにアクセスできます。PDF ドキュメントがパスワードで暗号化されている場合、ユーザーは開くためのパスワードを指定しないと、Adobe Reader または Adobe Acrobat でドキュメントを表示できません。同じように、PDF ドキュメントが証明書で暗号化されている場合も、ユーザーが PDF ドキュメントを復号化するには、その PDF ドキュメントの暗号化に使用された証明書（秘密鍵）に対応した公開鍵が必要です。

Encryption サービスを使用して、次のタスクを実行できます。

* パスワードでPDFドキュメントを暗号化します。 ( [パスワードを使用したPDFドキュメントの暗号化](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password).)
* 証明書でPDFドキュメントを暗号化します。 ( [証明書を使用したPDFドキュメントの暗号化](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-certificates).)
* パスワードドキュメントからパスワードベースの暗号化をPDFします。 ( [パスワード暗号化の削除](encrypting-decrypting-pdf-documents.md#removing-password-encryption).)
* 証明書ドキュメントから証明書ベースの暗号化をPDFします。 ( [証明書ベースの暗号化の削除](encrypting-decrypting-pdf-documents.md#removing-certificate-based-encryption).)
* 他のサービスPDFを実行できるように、操作ドキュメントのロックを解除します。 例えば、パスワードで暗号化されたPDFドキュメントのロックが解除された後に、電子署名を適用できます。 ( [暗号化されたPDF文書のロック解除](encrypting-decrypting-pdf-documents.md#unlocking-encrypted-pdf-documents).)
* 保護された暗号化ドキュメントの暗号化の種類をPDFします。 ( [暗号化タイプの決定](encrypting-decrypting-pdf-documents.md#determining-encryption-type).)

   >[!NOTE]
   >
   >Encryption サービスの詳細については、 [AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63).

## パスワードを使用したPDFドキュメントの暗号化 {#encrypting-pdf-documents-with-a-password}

PDF ドキュメントをパスワードで暗号化する場合、ユーザーは Adobe Reader または Acrobat で PDF ドキュメントを開くためのパスワードを指定する必要があります。また、PDFドキュメントへのデジタル署名など、別のAEM Forms操作をドキュメントで実行する前に、パスワードで暗号化されたPDFドキュメントのロックを解除する必要があります。

>[!NOTE]
>
>暗号化されたPDFドキュメントをAEM Formsリポジトリにアップロードすると、PDFドキュメントを復号化して XDP コンテンツを抽出することはできません。 ドキュメントをAEM Formsリポジトリにアップロードする前に、ドキュメントを暗号化しないことをお勧めします。 ( [リソースの書き込み](/help/forms/developing/aem-forms-repository.md#writing-resources).)

>[!NOTE]
>
>Encryption サービスの詳細については、 [AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary-of-steps}

パスワードを使用してPDF・ドキュメントを暗号化するには、次の手順に従います。

1. プロジェクトファイルを含めます。
1. 暗号化クライアント API オブジェクトを作成します。
1. 暗号化するPDFドキュメントを取得します。
1. 暗号化の実行時オプションを設定します。
1. パスワードを追加します。
1. 暗号化されたPDFドキュメントをPDFファイルとして保存します。

**プロジェクトファイルを含める**

開発プロジェクトに必要なファイルを含めます。 Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。 Web サービスを使用している場合は、プロキシファイルを必ず含めてください。

次の JAR ファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encryption-client.jar
* adobe-utilities.jar(AEM Formsを JBoss にデプロイする場合に必要 )
* jbossall-client.jar(AEM Formsが JBoss にデプロイされている場合に必要 )

**暗号化クライアント API オブジェクトの作成**

プログラムによって Encryption サービスの操作を実行するには、Encryption サービスクライアントを作成する必要があります。

**暗号化するPDFドキュメントを取得する**

パスワードを使用してドキュメントを暗号化するには、暗号化されていないPDFドキュメントを取得する必要があります。 既に暗号化されているPDF・ドキュメントを保護しようとすると、例外が発生します。

**暗号化の実行時オプションを設定する**

パスワードを使用してPDFドキュメントを暗号化するには、2 つのパスワード値を含む 4 つの値を指定します。 最初のパスワード値は、PDFドキュメントの暗号化に使用され、パスワードドキュメントを開く際に指定する必要があります。PDF 2 つ目のパスワード値は、master password 値と呼ばれ、パスワードドキュメントから暗号化を削除するためにPDFされます。 パスワード値では大文字と小文字が区別され、これら 2 つのパスワード値を同じ値にすることはできません。

暗号化するPDFドキュメントリソースを指定する必要があります。 PDFドキュメント全体、ドキュメントのメタデータ以外のすべて、またはドキュメントの添付ファイルのみを暗号化できます。 ドキュメントの添付ファイルのみを暗号化する場合、添付ファイルにアクセスしようとすると、ユーザーにパスワードの入力を求められます。

暗号化ドキュメントをPDFする際に、保護されたドキュメントに関連付けられた権限を指定できます。 権限を指定すると、パスワードで暗号化されたPDF・ドキュメントを開いたユーザーが実行できるアクションを制御できます。 例えば、フォームデータを正常に抽出するには、次の権限を設定する必要があります。

* PASSWORD_EDIT_ADD
* PASSWORD_EDIT_MODIFY

>[!NOTE]
>
>権限は次のように指定します。 `PasswordEncryptionPermission` 列挙値。

**パスワードを追加**

保護されていないPDFドキュメントを取得し、暗号化の実行時の値を設定した後、パスワードをPDFドキュメントに追加できます。

**暗号化されたPDFドキュメントをPDFファイルとして保存**

パスワードで暗号化されたPDF・ドキュメントは、PDF・ファイルとして保存できます。

**関連トピック**

[Java API を使用したPDFドキュメントの暗号化](encrypting-decrypting-pdf-documents.md#encrypt-a-pdf-document-using-the-java-api)

[Web サービス API を使用したPDFドキュメントの暗号化](encrypting-decrypting-pdf-documents.md#encrypting-a-pdf-document-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Encryption サービス API のクイックスタート](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

[証明書を使用したPDFドキュメントの暗号化](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-certificates)

### Java API を使用したPDFドキュメントの暗号化 {#encrypt-a-pdf-document-using-the-java-api}

暗号化 API(Java) を使用して、PDFドキュメントをパスワードで暗号化します。

1. プロジェクトファイルを含めます。

   Java プロジェクトのクラスパスに、adobe-encryption-client.jar などのクライアント JAR ファイルを含めます。

1. 暗号化クライアント API を作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * の作成 `EncryptionServiceClient` オブジェクトのコンストラクタを使用し、 `ServiceClientFactory` オブジェクト。

1. 暗号化するPDFドキュメントを取得します。

   * の作成 `java.io.FileInputStream` 暗号化するPDF・ドキュメントを表すオブジェクト。コンストラクタを使用し、PDF・ドキュメントの場所を指定する string 値を渡します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. 暗号化の実行時オプションを設定します。

   * の作成 `PasswordEncryptionOptionSpec` オブジェクトを指定します。
   * を呼び出して、暗号化するPDFドキュメントリソースを指定します。 `PasswordEncryptionOptionSpec` オブジェクトの `setEncryptOption` メソッドと `PasswordEncryptionOption` 暗号化するドキュメントリソースを指定する列挙値。 例えば、メタデータと添付ファイルを含むPDFドキュメント全体を暗号化するには、次のように指定します。 `PasswordEncryptionOption.ALL`.
   * の作成 `java.util.List` を使用して暗号化権限を保存するオブジェクト `ArrayList` コンストラクタ。
   * を呼び出して権限を指定 `java.util.List` オブジェクト `add` メソッドを使用し、設定する権限に対応する列挙値を渡すことができます。 例えば、ユーザーがPDF・ドキュメント内のデータをコピーできる権限を設定するには、次のように指定します。 `PasswordEncryptionPermission.PASSWORD_EDIT_COPY`. （設定する権限ごとに、この手順を繰り返します）。
   * を呼び出して、Acrobatの互換性オプションを指定します。 `PasswordEncryptionOptionSpec` オブジェクトの `setCompatability` メソッドを使用し、Acrobatの互換性レベルを指定する列挙値を渡す 例えば、次の項目を指定できます。 `PasswordEncryptionCompatability.ACRO_7`.
   * パスワードの値を指定します。この値を使用すると、暗号化されたPDFドキュメントを `PasswordEncryptionOptionSpec` オブジェクトの `setDocumentOpenPassword` メソッドを使用し、オープンパスワードを表す string 値を渡す方法と方法を指定します。
   * ユーザーが `PasswordEncryptionOptionSpec` オブジェクトの `setPermissionPassword` メソッドを使用して、マスターパスワードを表す string 値を渡す方法と値を指定します。

1. パスワードを追加します。

   を呼び出してPDFドキュメントを暗号化する `EncryptionServiceClient` オブジェクトの `encryptPDFUsingPassword` メソッドを使用して、次の値を渡します。

   * この `com.adobe.idp.Document` パスワードで暗号化するPDF・ドキュメントを含むオブジェクト。
   * この `PasswordEncryptionOptionSpec` 暗号化の実行時オプションを含むオブジェクト。

   この `encryptPDFUsingPassword` メソッドは、 `com.adobe.idp.Document` パスワードで暗号化されたPDF・ドキュメントを含むオブジェクト。

1. 暗号化されたPDFドキュメントをPDFファイルとして保存します。

   * `java.io.File` オブジェクトを作成し、ファイル拡張子が .pdf であることを確認します。
   * を呼び出す `com.adobe.idp.Document` オブジェクトの `copyToFile` メソッドを使用して、 `com.adobe.idp.Document` オブジェクトをファイルに追加します。 `com.adobe.idp.Document` メソッドから返された `encryptPDFUsingPassword` オブジェクトを必ず使用してください。

**関連トピック**

[手順の概要](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[クイックスタート（SOAP モード）:Java API を使用したPDFドキュメントの暗号化](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-encrypting-a-pdf-document-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Web サービス API を使用したPDFドキュメントの暗号化 {#encrypting-a-pdf-document-using-the-web-service-api}

Encryption API（Web サービス）を使用して、PDFドキュメントをパスワードで暗号化します。

1. プロジェクトファイルを含めます。

   MTOM を使用するMicrosoft .NET プロジェクトを作成します。 次の WSDL 定義を使用していることを確認します。 `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >置換 `localhost` を、AEM Formsをホストするサーバーの IP アドレスに設定します。

1. 暗号化クライアント API オブジェクトを作成します。

   * の作成 `EncryptionServiceClient` オブジェクトのデフォルトのコンストラクタを使用します。
   * の作成 `EncryptionServiceClient.Endpoint.Address` オブジェクトを `System.ServiceModel.EndpointAddress` コンストラクタ。 WSDL をAEM Formsサービスに渡す文字列値 ( 例： `http://localhost:8080/soap/services/EncryptionService?WSDL`.) を使用する必要はありません。 `lc_version` 属性。 この属性は、サービス参照を作成する際に使用されます )。
   * の作成 `System.ServiceModel.BasicHttpBinding` オブジェクトを作成するには、 `EncryptionServiceClient.Endpoint.Binding` フィールドに入力します。 戻り値を `BasicHttpBinding` にキャストします。
   * を `System.ServiceModel.BasicHttpBinding` オブジェクトの `MessageEncoding` ～に向かって `WSMessageEncoding.Mtom`. この値は、MTOM が確実に使用されるようにします。
   * 次のタスクを実行して、基本的な HTTP 認証を有効にします。

      * フィールドにAEM forms ユーザー名を割り当てます。 `EncryptionServiceClient.ClientCredentials.UserName.UserName`.
      * 対応するパスワード値をフィールドに割り当てます。 `EncryptionServiceClient.ClientCredentials.UserName.Password`.
      * 定数値を割り当て `HttpClientCredentialType.Basic` フィールドに `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 定数値を割り当て `BasicHttpSecurityMode.TransportCredentialOnly` フィールドに `BasicHttpBindingSecurity.Security.Mode`.

1. 暗号化するPDFドキュメントを取得します。

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。この `BLOB` オブジェクトは、パスワードで暗号化されたPDF・ドキュメントを保存するために使用されます。
   * の作成 `System.IO.FileStream` オブジェクトを呼び出し、暗号化するPDFドキュメントのファイルの場所と、ファイルを開くモードを表す string 値を渡すことによって、オブジェクトを指定します。
   * コンテンツを格納するバイト配列を作成します。 `System.IO.FileStream` オブジェクト。 バイト配列のサイズは、 `System.IO.FileStream` オブジェクトの `Length` プロパティ。
   * を呼び出して、バイト配列にストリームデータを入力します。 `System.IO.FileStream` オブジェクトの `Read` メソッドを使用し、読み込むバイト配列、開始位置、ストリーム長を渡す。
   * 次の項目に `BLOB` オブジェクトを作成するには、バイト配列の内容を `BLOB` オブジェクトの `MTOM` データメンバー。

1. 暗号化の実行時オプションを設定します。

   * コンストラクタを使用して `PasswordEncryptionOptionSpec` オブジェクトを作成します。
   * 暗号化するPDFドキュメントリソースを指定します。割り当てるには、 `PasswordEncryptionOption` 列挙値を `PasswordEncryptionOptionSpec` オブジェクトの `encryptOption` データメンバー。 メタデータと添付ファイルを含むPDF全体を暗号化するには、 `PasswordEncryptionOption.ALL` をこのデータメンバーに追加します。
   * Acrobatの互換性オプションを指定するには、 `PasswordEncryptionCompatability` 列挙値を `PasswordEncryptionOptionSpec` オブジェクトの `compatability` データメンバー。 例：assign `PasswordEncryptionCompatability.ACRO_7` をこのデータメンバーに追加します。
   * ユーザーが暗号化されたPDFドキュメントを開くための password 値を指定します。この値を指定するには、オープンパスワードを表す string 値を `PasswordEncryptionOptionSpec` オブジェクトの `documentOpenPassword` データメンバー。
   * ユーザーがPDF・ドキュメントの暗号化を解除できるようにするパスワード値を指定します。その際、マスター・パスワードを表す文字列値を `PasswordEncryptionOptionSpec` オブジェクトの `permissionPassword` データメンバー。

1. パスワードを追加します。

   を呼び出してPDFドキュメントを暗号化する `EncryptionServiceClient` オブジェクトの `encryptPDFUsingPassword` メソッドを使用して、次の値を渡します。

   * この `BLOB` パスワードで暗号化するPDF・ドキュメントを含むオブジェクト。
   * この `PasswordEncryptionOptionSpec` 暗号化の実行時オプションを含むオブジェクト。

   この `encryptPDFUsingPassword` メソッドは、 `BLOB` パスワードで暗号化されたPDF・ドキュメントを含むオブジェクト。

1. 暗号化されたPDFドキュメントをPDFファイルとして保存します。

   * の作成 `System.IO.FileStream` オブジェクトを指定します。
   * のデータコンテンツを格納するバイト配列を作成します。 `BLOB` が返したオブジェクト `encryptPDFUsingPassword` メソッド。 バイト配列を生成するには、 `BLOB` オブジェクトの `MTOM` データメンバー。
   * の作成 `System.IO.BinaryWriter` オブジェクトのコンストラクタを呼び出し、 `System.IO.FileStream` オブジェクト。
   * を呼び出して、バイト配列の内容をPDFファイルに書き込みます。 `System.IO.BinaryWriter` オブジェクトの `Write` メソッドを使用してバイト配列を渡す。

**関連トピック**

[手順の概要](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[MTOM を使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRef を使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 証明書を使用したPDFドキュメントの暗号化 {#encrypting-pdf-documents-with-certificates}

証明書ベースの暗号化では、公開鍵によって特定の受信者のドキュメントを暗号化できます。 それぞれの受信者に、異なる権限を与えることができます。公開鍵によって、さまざまな暗号化を行うことができます。アルゴリズムを使用して、大きな数を 2 つ生成します。 *キー*&#x200B;を作成し、次のプロパティを持つ

* 鍵のうち 1 つは、一連のデータを暗号化するために使用されます。その後、他のキーのみを使用してデータを復号化できます。
* 1 つの鍵を、もう片方の鍵と区別することは不可能です。

キーの 1 つが、ユーザーの秘密鍵として機能します。 そのユーザーのみがこの鍵にアクセスできることが重要です。もう 1 つのキーはユーザーの公開鍵で、他のユーザーと共有できます。

公開鍵証明書には、ユーザーの公開鍵と識別情報が含まれます。 証明書の保存には、X.509 形式が使用されます。通常、証明書は認証局（CA）で発行および電子署名されます。CA は、証明書の有効性における信頼度を提供する、承認されたエンティティです。証明書には有効期限があり、この期限を過ぎると無効になります。また、証明書の失効リスト（CRL）には、有効期限よりも前に失効した証明書に関する情報が示されます。CRL は認証局によって定期的に発行されます。証明書の失効ステータスは、ネットワークを通じてオンライン証明書ステータスプロトコル（OCSP）から取得することもできます。

>[!NOTE]
>
>暗号化されたPDFドキュメントをAEM Formsリポジトリにアップロードすると、PDFドキュメントを復号化して XDP コンテンツを抽出することはできません。 ドキュメントをAEM Formsリポジトリにアップロードする前に、ドキュメントを暗号化しないことをお勧めします。 ( [リソースの書き込み](/help/forms/developing/aem-forms-repository.md#writing-resources).)

>[!NOTE]
>
>証明書を使用してPDFドキュメントを暗号化する前に、証明書がAEM Formsに追加されていることを確認する必要があります。 証明書は、管理コンソールを使用して、または Trust Manager API を使用してプログラムで追加されます。 ( [Trust Manager API を使用した資格情報の読み込み](/help/forms/developing/credentials.md#importing-credentials-by-using-the-trust-manager-api).)

>[!NOTE]
>
>Encryption サービスの詳細については、 [AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary_of_steps-1}

証明書を使用してPDFドキュメントを暗号化するには、次の手順に従います。

1. プロジェクトファイルを含めます。
1. 暗号化クライアント API オブジェクトを作成します。
1. 暗号化するPDFドキュメントを取得します。
1. 証明書を参照します。
1. 暗号化の実行時オプションを設定します。
1. 証明書で暗号化されたPDFドキュメントを作成します。
1. 暗号化されたPDFドキュメントをPDFファイルとして保存します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。 Web サービスを使用している場合は、プロキシファイルを必ず含めてください。

次の JAR ファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encryption-client.jar
* adobe-utilities.jar(AEM Formsが JBoss Application Server にデプロイされている場合に必要 )
* jbossall-client.jar(AEM Formsが JBoss Application Server にデプロイされている場合に必要 )

**暗号化クライアント API オブジェクトの作成**

プログラムによって Encryption サービスの操作を実行するには、Encryption サービスクライアントを作成する必要があります。 Java Encryption Service API を使用している場合は、 `EncrytionServiceClient` オブジェクト。 Web サービス Encryption Service API を使用する場合は、 `EncryptionServiceService` オブジェクト。

**暗号化するPDFドキュメントを取得する**

暗号化する暗号化されていないPDFドキュメントを取得する必要があります。 既に暗号化されているPDF・ドキュメントを保護しようとすると、例外が発生します。

**証明書の参照**

PDFドキュメントを証明書で暗号化するには、暗号化ドキュメントの暗号化に使用する証明書をPDFします。 証明書は.cer ファイル、.crt ファイル、.pem ファイルのいずれかです。 PKCS#12 ファイルは、対応する証明書を持つ秘密鍵を保存するために使用されます。

証明書を使用してPDFドキュメントを暗号化する場合は、保護されたドキュメントに関連付けられている権限を指定します。 権限を指定すると、証明書で暗号化されたPDFドキュメントを開いたユーザーが実行できるアクションを制御できます。

**暗号化の実行時オプションを設定する**

暗号化するPDFドキュメントリソースを指定します。 PDFドキュメント全体、ドキュメントのメタデータを除くすべて、またはドキュメントの添付ファイルのみを暗号化できます。

**証明書で暗号化されたPDFドキュメントの作成**

セキュリティで保護されていないPDFドキュメントを取得し、証明書を参照し、実行時オプションを設定したら、証明書で暗号化されたPDFドキュメントを作成できます。 PDFドキュメントが暗号化された後、対応する公開鍵で復号化する必要があります。

**暗号化されたPDFドキュメントをPDFファイルとして保存**

暗号化されたPDFドキュメントは、PDFファイルとして保存できます。

**関連トピック**

[Java API を使用したPDFドキュメントの証明書での暗号化](encrypting-decrypting-pdf-documents.md#encrypt-a-pdf-document-with-a-certificate-using-the-java-api)

[Web サービス API を使用してPDFドキュメントを証明書で暗号化する](encrypting-decrypting-pdf-documents.md#encrypt-a-pdf-document-with-a-certificate-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Encryption サービス API のクイックスタート](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

[パスワードを使用したPDFドキュメントの暗号化](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)

### Java API を使用したPDFドキュメントの証明書での暗号化 {#encrypt-a-pdf-document-with-a-certificate-using-the-java-api}

暗号化 API(Java) を使用して、PDFドキュメントを証明書で暗号化します。

1. プロジェクトファイルを含めます。

   Java プロジェクトのクラスパスに、adobe-encryption-client.jar などのクライアント JAR ファイルを含めます。

1. 暗号化クライアント API オブジェクトを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * の作成 `EncryptionServiceClient` オブジェクトのコンストラクタを使用し、 `ServiceClientFactory` オブジェクト。

1. 暗号化するPDFドキュメントを取得します。

   * の作成 `java.io.FileInputStream` 暗号化するPDF・ドキュメントを表すオブジェクト。コンストラクタを使用し、PDF・ドキュメントの場所を指定する string 値を渡します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. 証明書を参照します。

   * の作成 `java.util.List` コンストラクタを使用して権限情報を格納するオブジェクト。
   * を呼び出して、暗号化されたドキュメントに関連付けられた権限を指定します。 `java.util.List` オブジェクトの `add` メソッドと `CertificateEncryptionPermissions` 保護されたPDFドキュメントを開くユーザーに付与される権限を表す列挙値です。 例えば、すべての権限を指定するには、 `CertificateEncryptionPermissions.PKI_ALL_PERM`.
   * コンストラクタを使用して `Recipient` オブジェクトを作成します。
   * の作成 `java.io.FileInputStream` PDFドキュメントのコンストラクターを使用し、証明書の場所を指定する string 値を渡すことで、証明書ドキュメントの暗号化に使用される証明書を表すオブジェクト。
   * の作成 `com.adobe.idp.Document` オブジェクトのコンストラクタを使用し、 `java.io.FileInputStream` 証明書を表すオブジェクト。
   * を呼び出す `Recipient` オブジェクトの `setX509Cert` メソッドを使用して、 `com.adobe.idp.Document` 証明書を含むオブジェクト。 ( また、 `Recipient`オブジェクトには、Truststore 証明書エイリアスまたは LDAP URL を証明書ソースとして含めることができます )。
   * の作成 `CertificateEncryptionIdentity` コンストラクタを使用して、権限と証明書の情報を格納するオブジェクト。
   * を呼び出す `CertificateEncryptionIdentity` オブジェクトの `setPerms` メソッドを使用して、 `java.util.List` 権限情報を格納するオブジェクト。
   * を呼び出す `CertificateEncryptionIdentity` オブジェクトの `setRecipient` メソッドを使用して、 `Recipient` 証明書情報を格納するオブジェクト。
   * の作成 `java.util.List` コンストラクタを使用して証明書情報を格納するオブジェクト。
   * を呼び出す `java.util.List` オブジェクトの add メソッドを使用して、 `CertificateEncryptionIdentity` オブジェクト。 ( この `java.util.List` オブジェクトが `encryptPDFUsingCertificates` メソッド )

1. 暗号化の実行時オプションを設定します。

   * の作成 `CertificateEncryptionOptionSpec` オブジェクトを指定します。
   * を呼び出して、暗号化するPDFドキュメントリソースを指定します。 `CertificateEncryptionOptionSpec` オブジェクトの `setOption` メソッドと `CertificateEncryptionOption` 暗号化するドキュメントリソースを指定する列挙値。 例えば、メタデータと添付ファイルを含むPDFドキュメント全体を暗号化するには、次のように指定します。 `CertificateEncryptionOption.ALL`.
   * を呼び出して、Acrobatの互換性オプションを指定します。 `CertificateEncryptionOptionSpec` オブジェクトの `setCompat` メソッドと `CertificateEncryptionCompatibility` Acrobatの互換性レベルを指定する列挙値。 例えば、次の項目を指定できます。 `CertificateEncryptionCompatibility.ACRO_7`.

1. 証明書で暗号化されたPDFドキュメントを作成します。

   を呼び出して、PDFドキュメントを証明書で暗号化します。 `EncryptionServiceClient` オブジェクトの `encryptPDFUsingCertificates` メソッドを使用して、次の値を渡します。

   * この `com.adobe.idp.Document` 暗号化するPDF・ドキュメントを含むオブジェクト。
   * この `java.util.List` 証明書情報を格納するオブジェクト。
   * この `CertificateEncryptionOptionSpec` 暗号化の実行時オプションを含むオブジェクト。

   この `encryptPDFUsingCertificates` メソッドは、 `com.adobe.idp.Document` 証明書で暗号化されたPDF・ドキュメントが格納される。

1. 暗号化されたPDFドキュメントをPDFファイルとして保存します。

   * の作成 `java.io.File` オブジェクトにマッピングされ、ファイル名の拡張子が.pdf であることを確認します。
   * を呼び出す `com.adobe.idp.Document` オブジェクトの `copyToFile` メソッドを使用して、 `com.adobe.idp.Document` オブジェクトをファイルに追加します。 `com.adobe.idp.Document` メソッドから返された `encryptPDFUsingCertificates` オブジェクトを必ず使用してください。

**関連トピック**

[手順の概要](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[クイックスタート（SOAP モード）:Java API を使用したPDFドキュメントの証明書での暗号化](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-encrypting-a-pdf-document-with-a-certificate-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Web サービス API を使用してPDFドキュメントを証明書で暗号化する {#encrypt-a-pdf-document-with-a-certificate-using-the-web-service-api}

Encryption API（Web サービス）を使用して、PDFドキュメントを証明書で暗号化します。

1. プロジェクトファイルを含めます。

   MTOM を使用するMicrosoft .NET プロジェクトを作成します。 次の WSDL 定義を使用していることを確認します。 `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >置換 `localhost` を、AEM Formsをホストするサーバーの IP アドレスに設定します。

1. 暗号化クライアント API オブジェクトを作成します。

   * の作成 `EncryptionServiceClient` オブジェクトのデフォルトのコンストラクタを使用します。
   * の作成 `EncryptionServiceClient.Endpoint.Address` オブジェクトを `System.ServiceModel.EndpointAddress` コンストラクタ。 WSDL をAEM Formsサービスに渡す文字列値 ( 例： `http://localhost:8080/soap/services/EncryptionService?WSDL`.) を使用する必要はありません。 `lc_version` 属性。 この属性は、サービス参照を作成する際に使用されます )。
   * の作成 `System.ServiceModel.BasicHttpBinding` オブジェクトを作成するには、 `EncryptionServiceClient.Endpoint.Binding` フィールドに入力します。 戻り値を `BasicHttpBinding` にキャストします。
   * を `System.ServiceModel.BasicHttpBinding` オブジェクトの `MessageEncoding` ～に向かって `WSMessageEncoding.Mtom`. この値は、MTOM が確実に使用されるようにします。
   * 次のタスクを実行して、基本的な HTTP 認証を有効にします。

      * フィールドにAEM forms ユーザー名を割り当てます。 `EncryptionServiceClient.ClientCredentials.UserName.UserName`.
      * 対応するパスワード値をフィールドに割り当てます。 `EncryptionServiceClient.ClientCredentials.UserName.Password`.
      * 定数値を割り当て `HttpClientCredentialType.Basic` フィールドに `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 定数値を割り当て `BasicHttpSecurityMode.TransportCredentialOnly` フィールドに `BasicHttpBindingSecurity.Security.Mode`.

1. 暗号化するPDFドキュメントを取得します。

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。この `BLOB` オブジェクトは、証明書で暗号化されたPDFドキュメントを保存するために使用されます。
   * の作成 `System.IO.FileStream` オブジェクトを呼び出し、暗号化するPDFドキュメントのファイルの場所と、ファイルを開くモードを表す string 値を渡すことによって、オブジェクトを指定します。
   * コンテンツを格納するバイト配列を作成します。 `System.IO.FileStream` オブジェクト。 バイト配列のサイズは、 `System.IO.FileStream` オブジェクトの `Length` プロパティ。
   * を呼び出して、バイト配列にストリームデータを入力します。 `System.IO.FileStream` オブジェクトの `Read` メソッドを使用し、読み込むバイト配列、開始位置、ストリーム長を渡す。
   * 次の項目に `BLOB` オブジェクトを割り当てる `MTOM` プロパティにバイト配列の内容を入力します。

1. 証明書を参照します。

   * コンストラクタを使用して `Recipient` オブジェクトを作成します。このオブジェクトは、証明書情報を格納します。
   * コンストラクタを使用して `BLOB` オブジェクトを作成します。この `BLOB` オブジェクトには、証明書ドキュメントを暗号化するPDFが格納されます。
   * の作成 `System.IO.FileStream` オブジェクトを呼び出し、証明書のファイルの場所とファイルを開くモードを表す string 値を渡すことによって、オブジェクトを開きます。
   * コンテンツを格納するバイト配列を作成します。 `System.IO.FileStream` オブジェクト。 バイト配列のサイズは、 `System.IO.FileStream` オブジェクトの `Length` プロパティ。
   * を呼び出して、バイト配列にストリームデータを入力します。 `System.IO.FileStream` オブジェクトの `Read` メソッドを使用し、読み込むバイト配列、開始位置、ストリーム長を渡す。
   * 次の項目に `BLOB` オブジェクトを作成するには、バイト配列の内容を `BLOB` オブジェクトの `MTOM` データメンバー。
   * を `BLOB` 証明書を `Recipient` オブジェクトの `x509Cert` データメンバー。
   * の作成 `CertificateEncryptionIdentity` コンストラクタを使用して証明書情報を格納するオブジェクト。
   * を `Recipient` 証明書を `CertificateEncryptionIdentity`オブジェクトの受信者データメンバー。
   * の作成 `Object` 配列と割り当て `CertificateEncryptionIdentity` オブジェクトを `Object` 配列。 この `Object` 配列が `encryptPDFUsingCertificates` メソッド。

1. 暗号化の実行時オプションを設定します。

   * コンストラクタを使用して `CertificateEncryptionOptionSpec` オブジェクトを作成します。
   * 暗号化するPDFドキュメントリソースを指定します。割り当てるには、 `CertificateEncryptionOption` 列挙値を `CertificateEncryptionOptionSpec` オブジェクトの `option` データメンバー。 メタデータと添付ファイルを含むPDFドキュメント全体を暗号化するには、 `CertificateEncryptionOption.ALL` をこのデータメンバーに追加します。
   * Acrobatの互換性オプションを指定するには、 `CertificateEncryptionCompatibility` 列挙値を `CertificateEncryptionOptionSpec` オブジェクトの `compat` データメンバー。 例：assign `CertificateEncryptionCompatibility.ACRO_7` をこのデータメンバーに追加します。

1. 証明書で暗号化されたPDFドキュメントを作成します。

   を呼び出して、PDFドキュメントを証明書で暗号化します。 `EncryptionServiceService` オブジェクトの `encryptPDFUsingCertificates` メソッドを使用して、次の値を渡します。

   * この `BLOB` 暗号化するPDF・ドキュメントを含むオブジェクト。
   * この `Object` 証明書情報を格納する配列。
   * この `CertificateEncryptionOptionSpec` 暗号化の実行時オプションを含むオブジェクト。

   この `encryptPDFUsingCertificates` メソッドは、 `BLOB` 証明書で暗号化されたPDF・ドキュメントが格納される。

1. 暗号化されたPDFドキュメントをPDFファイルとして保存します。

   * の作成 `System.IO.FileStream` オブジェクトを指定します。
   * のデータコンテンツを格納するバイト配列を作成します。 `BLOB` が返したオブジェクト `encryptPDFUsingCertificates` メソッド。 バイト配列を生成するには、 `BLOB` オブジェクトの `binaryData` データメンバー。
   * の作成 `System.IO.BinaryWriter` オブジェクトのコンストラクタを呼び出し、 `System.IO.FileStream` オブジェクト。
   * を呼び出して、バイト配列の内容をPDFファイルに書き込みます。 `System.IO.BinaryWriter` オブジェクトの `Write` メソッドを使用してバイト配列を渡す。

**関連トピック**

[手順の概要](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[MTOM を使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRef を使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 証明書ベースの暗号化の削除 {#removing-certificate-based-encryption}

証明書ベースの暗号化をPDFドキュメントから削除して、ユーザーがAdobe ReaderまたはAcrobatでPDFドキュメントを開けるようにすることができます。 証明書で暗号化されているPDFドキュメントから暗号化を削除するには、公開鍵を参照する必要があります。 暗号化ドキュメントから暗号化を削除すると、PDFドキュメントは保護されなくなります。

>[!NOTE]
>
>Encryption サービスの詳細については、 [AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary_of_steps-2}

証明書ベースの暗号化をPDF・ドキュメントから削除するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. 暗号化サービスクライアントを作成します。
1. 暗号化されたPDF文書を取得します。
1. 暗号化を削除します。
1. PDF・ドキュメントをPDF・ファイルとして保存します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。 Web サービスを使用している場合は、プロキシファイルを必ず含めてください。

次の JAR ファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encryption-client.jar
* adobe-utilities.jar(AEM Formsが JBoss Application Server にデプロイされている場合に必要 )
* jbossall-client.jar(AEM Formsが JBoss Application Server にデプロイされている場合に必要 )

**暗号化サービスクライアントの作成**

プログラムによって Encryption サービスの操作を実行するには、Encryption サービスクライアントを作成する必要があります。 Java Encryption Service API を使用している場合は、 `EncrytionServiceClient` オブジェクト。 Web サービス Encryption Service API を使用する場合は、 `EncryptionServiceService` オブジェクト。

**暗号化されたPDF文書を取得**

証明書ベースの暗号化を削除するには、暗号化されたPDFドキュメントを取得する必要があります。 暗号化されていないPDF・ドキュメントから暗号化を削除しようとすると、例外がスローされます。 同様に、パスワードで暗号化されたドキュメントから証明書ベースの暗号化を削除しようとすると、例外がスローされます。

**暗号化を削除**

暗号化されたPDFドキュメントから証明書ベースの暗号化を削除するには、暗号化されたPDFドキュメントと、PDFドキュメントの暗号化に使用されたキーに対応する秘密鍵の両方が必要です。 秘密鍵のエイリアス値は、暗号化された暗号化ドキュメントから証明書ベースの暗号化を削除する際に指定されるPDFです。 公開鍵について詳しくは、 [証明書を使用したPDFドキュメントの暗号化](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-certificates).

>[!NOTE]
>
>秘密鍵はAEM Forms Trust Store に保存されます。 証明書が配置されると、エイリアス値が指定されます。

**PDF文書を保存**

暗号化されたPDFドキュメントから証明書ベースの暗号化を削除した後、PDFドキュメントをPDFファイルとして保存できます。 ユーザーは、Adobe ReaderまたはAcrobatでPDFドキュメントを開くことができます。

**関連トピック**

[Java API を使用した証明書ベースの暗号化の削除](encrypting-decrypting-pdf-documents.md#remove-certificate-based-encryption-using-the-java-api)

[Web サービス API を使用して証明書ベースの暗号化を削除する](encrypting-decrypting-pdf-documents.md#remove-certificate-based-encryption-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Encryption サービス API のクイックスタート](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

### Java API を使用した証明書ベースの暗号化の削除 {#remove-certificate-based-encryption-using-the-java-api}

Encryption API(Java) を使用して、PDFドキュメントから証明書ベースの暗号化を削除します。

1. プロジェクトファイルを含めます。

   Java プロジェクトのクラスパスに、adobe-encryption-client.jar などのクライアント JAR ファイルを含めます。

1. 暗号化サービスクライアントを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * の作成 `EncryptionServiceClient` オブジェクトのコンストラクタを使用し、 `ServiceClientFactory` オブジェクト。

1. 暗号化されたPDF文書を取得します。

   * の作成 `java.io.FileInputStream` コンストラクタを使用し、暗号化されたPDF・ドキュメントの場所を指定する string 値を渡すことによって、暗号化されたPDF・ドキュメントを表すオブジェクト。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. 暗号化を削除します。

   を呼び出して、証明書ベースの暗号化をPDFドキュメントから削除する `EncryptionServiceClient` オブジェクトの `removePDFCertificateSecurity` メソッドを使用して、次の値を渡します。

   * この `com.adobe.idp.Document` 暗号化されたPDF・ドキュメントを含むオブジェクト。
   * PDf ドキュメントの暗号化に使用されたキーに対応する秘密鍵のエイリアス名を指定する string 値です。

   この `removePDFCertificateSecurity` メソッドは、 `com.adobe.idp.Document` 保護されていないPDFドキュメントを含むオブジェクト。

1. PDF文書を保存します。

   * `java.io.File` オブジェクトを作成し、ファイル拡張子が .pdf であることを確認します。
   * を呼び出す `com.adobe.idp.Document` オブジェクトの `copyToFile` メソッドを使用して、 `Document` オブジェクトをファイルに追加します。 `com.adobe.idp.Document` メソッドから返された `removePDFCredentialSecurity` オブジェクトを必ず使用してください。

**関連トピック**

[手順の概要](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[クイックスタート（SOAP モード）:Java API を使用した証明書ベースの暗号化の削除](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-removing-certificate-based-encryption-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Web サービス API を使用して証明書ベースの暗号化を削除する {#remove-certificate-based-encryption-using-the-web-service-api}

Encryption API（Web サービス）を使用して、証明書ベースの暗号化を削除します。

1. プロジェクトファイルを含めます。

   MTOM を使用するMicrosoft .NET プロジェクトを作成します。 次の WSDL 定義を使用していることを確認します。 `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >置換 `localhost` を、AEM Formsをホストするサーバーの IP アドレスに設定します。

1. 暗号化サービスクライアントを作成します。

   * の作成 `EncryptionServiceClient` オブジェクトのデフォルトのコンストラクタを使用します。
   * の作成 `EncryptionServiceClient.Endpoint.Address` オブジェクトを `System.ServiceModel.EndpointAddress` コンストラクタ。 WSDL をAEM Formsサービスに渡す文字列値 ( 例： `http://localhost:8080/soap/services/EncryptionService?WSDL`.) を使用する必要はありません。 `lc_version` 属性。 この属性は、サービス参照を作成する際に使用されます )。
   * の作成 `System.ServiceModel.BasicHttpBinding` オブジェクトを作成するには、 `EncryptionServiceClient.Endpoint.Binding` フィールドに入力します。 戻り値を `BasicHttpBinding` にキャストします。
   * を `System.ServiceModel.BasicHttpBinding` オブジェクトの `MessageEncoding` ～に向かって `WSMessageEncoding.Mtom`. この値は、MTOM が確実に使用されるようにします。
   * 次のタスクを実行して、基本的な HTTP 認証を有効にします。

      * フィールドにAEM forms ユーザー名を割り当てます。 `EncryptionServiceClient.ClientCredentials.UserName.UserName`.
      * 対応するパスワード値をフィールドに割り当てます。 `EncryptionServiceClient.ClientCredentials.UserName.Password`.
      * 定数値を割り当て `HttpClientCredentialType.Basic` フィールドに `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 定数値を割り当て `BasicHttpSecurityMode.TransportCredentialOnly` フィールドに `BasicHttpBindingSecurity.Security.Mode`.

1. 暗号化されたPDF文書を取得します。

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。この `BLOB` オブジェクトは、暗号化されたPDF・ドキュメントを保存するために使用されます。
   * の作成 `System.IO.FileStream` オブジェクトを呼び出し、暗号化されたPDFドキュメントのファイルの場所と、ファイルを開くモードを表す string 値を渡すことによって、オブジェクトを指定します。
   * コンテンツを格納するバイト配列を作成します。 `System.IO.FileStream` オブジェクト。 バイト配列のサイズは、 `System.IO.FileStream` オブジェクトの `Length` プロパティ。
   * を呼び出して、バイト配列にストリームデータを入力します。 `System.IO.FileStream` オブジェクトの `Read` メソッドを使用し、読み込むバイト配列、開始位置、ストリーム長を渡す。
   * 次の項目に `BLOB` オブジェクトを作成するには、バイト配列の内容を `BLOB` オブジェクトの `MTOM` データメンバー。

1. 暗号化を削除します。

   を呼び出す `EncryptionServiceClient` オブジェクトの `removePDFCertificateSecurity` メソッドを使用して、次の値を渡します。

   * この `BLOB` 暗号化されたPDF・ドキュメントを表すファイル・ストリーム・データを格納するオブジェクト。
   * PDf ドキュメントの暗号化に使用された秘密鍵に対応する公開鍵のエイリアス名を指定する string 値です。

   この `removePDFCredentialSecurity` メソッドは、 `BLOB` 保護されていないPDFドキュメントを含むオブジェクト。

1. PDF文書を保存します。

   * の作成 `System.IO.FileStream` オブジェクトを指定します。
   * コンテンツを格納するバイト配列を作成します。 `BLOB` が返したオブジェクト `removePDFPasswordSecurity` メソッド。 バイト配列を生成するには、 `BLOB` オブジェクトの `MTOM` データメンバー。
   * の作成 `System.IO.BinaryWriter` オブジェクトのコンストラクタを呼び出し、 `System.IO.FileStream` オブジェクト。
   * を呼び出して、バイト配列の内容をPDFファイルに書き込みます。 `System.IO.BinaryWriter` オブジェクトの `Write` メソッドを使用してバイト配列を渡す。

**関連トピック**

[手順の概要](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[MTOM を使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRef を使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## パスワード暗号化の削除 {#removing-password-encryption}

PDFベースの暗号化をPDFドキュメントから削除して、ユーザーがパスワードを指定しなくてもAdobe ReaderまたはAcrobatでパスワードドキュメントを開けるようにすることができます。 パスワードベースの暗号化をPDFドキュメントから削除すると、ドキュメントのセキュリティは失われます。

>[!NOTE]
>
>Encryption サービスの詳細については、 [AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary_of_steps-3}

パスワード・ドキュメントからPDF・ベースの暗号化を削除するには、次の手順に従います。

1. プロジェクトファイルを含める
1. 暗号化サービスクライアントを作成します。
1. 暗号化されたPDF文書を取得します。
1. パスワードを削除します。
1. PDF・ドキュメントをPDF・ファイルとして保存します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。 Web サービスを使用している場合は、必ずプロキシファイルを含めてください。

次の JAR ファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encryption-client.jar
* adobe-utilities.jar(AEM Formsを JBoss にデプロイする場合に必要 )
* jbossall-client.jar(AEM Formsが JBoss にデプロイされている場合に必要 )

**暗号化サービスクライアントの作成**

プログラムによって Encryption サービスの操作を実行するには、Encryption サービスクライアントを作成する必要があります。 Java Encryption Service API を使用している場合は、 `EncrytionServiceClient` オブジェクト。 Web サービス Encryption Service API を使用する場合は、 `EncryptionServiceService` オブジェクト。

**暗号化されたPDF文書を取得**

パスワードベースの暗号化を削除するには、暗号化されたPDFドキュメントを取得する必要があります。 暗号化されていないPDF・ドキュメントから暗号化を削除しようとすると、例外がスローされます。

**パスワードを削除**

暗号化されたPDF文書からPDFベースの暗号化を削除するには、暗号化されたPDF文書と、パスワード文書から暗号化を削除するために使用されるマスターパスワード値の両方が必要です。 パスワードで暗号化されたパスワードドキュメントを開くために使用されるPDFは、暗号化を削除するために使用できません。 パスワードで暗号化する際に、マスタPDFを指定する。 ( [パスワードを使用したPDFドキュメントの暗号化](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password).)

**PDF文書を保存**

Encryption サービスがPDF・ドキュメントからパスワード・ベースの暗号化を削除した後、そのPDF・ドキュメントをPDF・ファイルとして保存できます。 ユーザーは、PDFを指定せずに、Adobe ReaderまたはAcrobatでパスワードドキュメントを開くことができます。

**関連トピック**

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Encryption サービス API のクイックスタート](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

[パスワードを使用したPDFドキュメントの暗号化](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)

### Java API を使用したパスワードベースの暗号化の削除 {#remove-password-based-encryption-using-the-java-api}

Encryption API(Java) を使用して、PDFドキュメントからパスワードベースの暗号化を削除します。

1. プロジェクトファイルを含めます。

   Java プロジェクトのクラスパスに、adobe-encryption-client.jar などのクライアント JAR ファイルを含めます。

1. 暗号化サービスクライアントを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * の作成 `EncryptionServiceClient` オブジェクトのコンストラクタを使用し、 `ServiceClientFactory` オブジェクト。

1. 暗号化されたPDF文書を取得します。

   * の作成 `java.io.FileInputStream` コンストラクタを使用し、PDFドキュメントの場所を指定する string 値を渡すことによって、暗号化されたPDFドキュメントを表すオブジェクト。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. パスワードを削除します。

   を呼び出して、パスワードベースの暗号化をPDFドキュメントから削除します。 `EncryptionServiceClient` オブジェクトの `removePDFPasswordSecurity` メソッドを使用して、次の値を渡します。

   * A `com.adobe.idp.Document` 暗号化されたPDF・ドキュメントを含むオブジェクト。
   * 暗号化ドキュメントから暗号化を削除するために使用されるマスターPDF値を指定する string 値。

   この `removePDFPasswordSecurity` メソッドは、 `com.adobe.idp.Document` 保護されていないPDFドキュメントを含むオブジェクト。

1. PDF文書を保存します。

   * の作成 `java.io.File` オブジェクトにマッピングされ、ファイル名の拡張子が.pdf であることを確認します。
   * を呼び出す `com.adobe.idp.Document` オブジェクトの `copyToFile` メソッドを使用して、 `Document` オブジェクトをファイルに追加します。 `Document` メソッドから返された `removePDFPasswordSecurity` オブジェクトを必ず使用してください。

**関連トピック**

[クイックスタート（SOAP モード）:Java API を使用したパスワードベースの暗号化の削除](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-removing-password-based-encryption-using-the-java-api)

### Web サービス API を使用したパスワードベースの暗号化の削除 {#remove-password-based-encryption-using-the-web-service-api}

Encryption API（Web サービス）を使用して、パスワードベースの暗号化を削除します。

1. プロジェクトファイルを含めます。

   MTOM を使用するMicrosoft .NET プロジェクトを作成します。 次の WSDL 定義を使用していることを確認します。 `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >置換 `localhost` を、AEM Formsをホストするサーバーの IP アドレスに設定します。

1. 暗号化サービスクライアントを作成します。

   * の作成 `EncryptionServiceClient` オブジェクトのデフォルトのコンストラクタを使用します。
   * の作成 `EncryptionServiceClient.Endpoint.Address` オブジェクトを `System.ServiceModel.EndpointAddress` コンストラクタ。 WSDL をAEM Formsサービスに渡す文字列値 ( 例： `http://localhost:8080/soap/services/EncryptionService?WSDL`.) を使用する必要はありません。 `lc_version` 属性。 この属性は、サービス参照を作成する際に使用されます )。
   * の作成 `System.ServiceModel.BasicHttpBinding` オブジェクトを作成するには、 `EncryptionServiceClient.Endpoint.Binding` フィールドに入力します。 戻り値を `BasicHttpBinding` にキャストします。
   * を `System.ServiceModel.BasicHttpBinding` オブジェクトの `MessageEncoding` ～に向かって `WSMessageEncoding.Mtom`. この値は、MTOM が確実に使用されるようにします。
   * 次のタスクを実行して、基本的な HTTP 認証を有効にします。

      * フィールドにAEM forms ユーザー名を割り当てます。 `EncryptionServiceClient.ClientCredentials.UserName.UserName`.
      * 対応するパスワード値をフィールドに割り当てます。 `EncryptionServiceClient.ClientCredentials.UserName.Password`.
      * 定数値を割り当て `HttpClientCredentialType.Basic` フィールドに `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 定数値を割り当て `BasicHttpSecurityMode.TransportCredentialOnly` フィールドに `BasicHttpBindingSecurity.Security.Mode`.

1. 暗号化されたPDF文書を取得します。

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。この `BLOB` オブジェクトは、パスワードで暗号化されたPDF・ドキュメントを保存するために使用します。
   * の作成 `System.IO.FileStream` オブジェクトを呼び出し、暗号化されたPDFドキュメントのファイルの場所と、ファイルを開くモードを表す string 値を渡すことによって、オブジェクトを指定します。
   * コンテンツを格納するバイト配列を作成します。 `System.IO.FileStream` オブジェクト。 バイト配列のサイズは、 `System.IO.FileStream` オブジェクトの `Length` プロパティ。
   * を呼び出して、バイト配列にストリームデータを入力します。 `System.IO.FileStream` オブジェクトの `Read` メソッドを使用し、読み込むバイト配列、開始位置、ストリーム長を渡す。
   * 次の項目に `BLOB` オブジェクトを作成するには、バイト配列の内容を `BLOB` オブジェクトの `MTOM` データメンバー。

1. パスワードを削除します。

   を呼び出す `EncryptionServiceService` オブジェクトの `removePDFPasswordSecurity` メソッドを使用して、次の値を渡します。

   * この `BLOB` 暗号化されたPDF・ドキュメントを表すファイル・ストリーム・データを格納するオブジェクト。
   * 暗号化ドキュメントから暗号化を削除するために使用されるPDF値を指定する string 値。 この値は、パスワードでPDFドキュメントを暗号化する際に指定します。

   この `removePDFPasswordSecurity` メソッドは、 `BLOB` 保護されていないPDFドキュメントを含むオブジェクト。

1. PDF文書を保存します。

   * の作成 `System.IO.FileStream` オブジェクトを指定します。
   * コンテンツを格納するバイト配列を作成します。 `BLOB` が返したオブジェクト `removePDFPasswordSecurity` メソッド。 バイト配列を生成するには、 `BLOB` オブジェクトの `MTOM` データメンバー。
   * の作成 `System.IO.BinaryWriter` オブジェクトのコンストラクタを呼び出し、 `System.IO.FileStream` オブジェクト。
   * を呼び出して、バイト配列の内容をPDFファイルに書き込みます。 `System.IO.BinaryWriter` オブジェクトの `Write` メソッドを使用してバイト配列を渡す。

**関連トピック**

[MTOM を使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRef を使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 暗号化されたPDF文書のロック解除 {#unlocking-encrypted-pdf-documents}

パスワードで暗号化または証明書で暗号化されたPDFドキュメントは、別のAEM Forms操作を実行する前に、ロックを解除する必要があります。 暗号化されたPDFドキュメントに対して操作を実行しようとすると、例外が生成されます。 暗号化されたPDFドキュメントのロックを解除した後、そのドキュメントに対して 1 つ以上の操作を実行できます。 これらの操作は、Acrobat Reader DC Extensions Service などの他のサービスに属することができます。

>[!NOTE]
>
>Encryption サービスの詳細については、 [AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary_of_steps-4}

暗号化されたPDF・ドキュメントのロックを解除するには、次の手順に従います。

1. プロジェクトファイルを含めます。
1. 暗号化サービスクライアントを作成します。
1. 暗号化されたPDF文書を取得します。
1. ドキュメントのロックを解除します。
1. AEM Forms操作を実行します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。 Web サービスを使用している場合は、必ずプロキシファイルを含めてください。

次の JAR ファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encryption-client.jar
* adobe-utilities.jar(AEM Formsが JBoss Application Server にデプロイされている場合に必要 )
* jbossall-client.jar(AEM Formsが JBoss Application Server にデプロイされている場合に必要 )

**暗号化サービスクライアントの作成**

プログラムによって Encryption サービスの操作を実行するには、Encryption サービスクライアントを作成する必要があります。 Java Encryption Service API を使用している場合は、 `EncrytionServiceClient` オブジェクト。 Web サービス Encryption Service API を使用する場合は、 `EncryptionServiceService` オブジェクト。

**暗号化されたPDF文書を取得**

ロックを解除するには、暗号化されたPDFドキュメントを取得する必要があります。 暗号化されていないPDF・ドキュメントのロックを解除しようとすると、例外が発生します。

**ドキュメントのロックを解除**

パスワードで暗号化されたPDF・ドキュメントのロックを解除するには、暗号化されたPDF・ドキュメントと、パスワードで暗号化されたPDF・ドキュメントを開くために使用されるパスワード値の両方が必要です。 この値は、パスワードでPDFドキュメントを暗号化する際に指定します。 ( [パスワードを使用したPDFドキュメントの暗号化](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password).)

証明書で暗号化されたPDFドキュメントのロックを解除するには、暗号化されたPDFドキュメントと、PDFドキュメントの暗号化に使用された秘密鍵に対応する公開鍵のエイリアス値の両方が必要です。

**AEM Forms操作の実行**

暗号化されたPDFドキュメントのロックが解除された後は、そのドキュメントに対して別のサービス操作（使用権限の適用など）を実行できます。 この操作は、Acrobat Reader DC Extensions サービスに属しています。

**関連トピック**

[Java API を使用した暗号化されたPDFドキュメントのロック解除](encrypting-decrypting-pdf-documents.md#unlock-an-encrypted-pdf-document-using-the-java-api)

[Web サービス API を使用して暗号化されたPDFドキュメントをロック解除する](encrypting-decrypting-pdf-documents.md#unlock-an-encrypted-pdf-document-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Encryption サービス API のクイックスタート](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

### Java API を使用した暗号化されたPDFドキュメントのロック解除 {#unlock-an-encrypted-pdf-document-using-the-java-api}

暗号化 API(Java) を使用して、暗号化されたPDFドキュメントのロックを解除します。

1. プロジェクトファイルを含めます。

   Java プロジェクトのクラスパスに、adobe-encryption-client.jar などのクライアント JAR ファイルを含めます。

1. 暗号化サービスクライアントを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * の作成 `EncryptionServiceClient` オブジェクトのコンストラクタを使用し、 `ServiceClientFactory` オブジェクト。

1. 暗号化されたPDF文書を取得します。

   * の作成 `java.io.FileInputStream` コンストラクタを使用し、暗号化されたPDF・ドキュメントの場所を指定する string 値を渡すことによって、暗号化されたPDF・ドキュメントを表すオブジェクト。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. ドキュメントのロックを解除します。

   を呼び出して、暗号化されたPDFドキュメントをロック解除します。 `EncryptionServiceClient` オブジェクトの `unlockPDFUsingPassword` または `unlockPDFUsingCredential` メソッド。

   パスワードで暗号化されたPDFドキュメントのロックを解除するには、 `unlockPDFUsingPassword` メソッドを使用して、次の値を渡します。

   * A `com.adobe.idp.Document` パスワードで暗号化されたPDF・ドキュメントを格納するオブジェクト。
   * パスワードで暗号化されたパスワードドキュメントを開くために使用されるPDF値を指定する string 値です。 この値は、パスワードでPDFドキュメントを暗号化する際に指定します。

   証明書で暗号化されているPDFドキュメントのロックを解除するには、 `unlockPDFUsingCredential` メソッドを使用して、次の値を渡します。

   * A `com.adobe.idp.Document` 証明書で暗号化されたPDF・ドキュメントを格納するオブジェクト。
   * PDFドキュメントの暗号化に使用された秘密鍵に対応する公開鍵のエイリアス名を指定する string 値です。

   この `unlockPDFUsingPassword` および `unlockPDFUsingCredential` メソッドは両方とも `com.adobe.idp.Document` 別のAEM Forms Java メソッドに渡して操作を実行するオブジェクト。

1. AEM Forms操作を実行します。

   ロックが解除されたPDFドキュメントに対してAEM Forms操作を実行し、ビジネス要件を満たします。 例えば、使用権限をロック解除されたPDFドキュメントに適用する場合、 `com.adobe.idp.Document` 次のいずれかによって返されたオブジェクト `unlockPDFUsingPassword` または `unlockPDFUsingCredential` メソッドから `ReaderExtensionsServiceClient` オブジェクトの `applyUsageRights` メソッド。

**関連トピック**

[手順の概要](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[クイックスタート（SOAP モード）:Java API を使用した暗号化されたPDFドキュメントのロック解除](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-unlocking-an-encrypted-pdf-document-using-the-java-api) （SOAP モード）

[使用権限のPDF・ドキュメントへの適用](/help/forms/developing/assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Web サービス API を使用して暗号化されたPDFドキュメントをロック解除する {#unlock-an-encrypted-pdf-document-using-the-web-service-api}

Encryption API（Web サービス）を使用して、暗号化されたPDFドキュメントのロックを解除します。

1. プロジェクトファイルを含めます。

   MTOM を使用するMicrosoft .NET プロジェクトを作成します。 次の WSDL 定義を使用していることを確認します。 `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >置換 `localhost` を、AEM Formsをホストするサーバーの IP アドレスに設定します。

1. 暗号化サービスクライアントを作成します。

   * の作成 `EncryptionServiceClient` オブジェクトのデフォルトのコンストラクタを使用します。
   * の作成 `EncryptionServiceClient.Endpoint.Address` オブジェクトを `System.ServiceModel.EndpointAddress` コンストラクタ。 WSDL をAEM Formsサービスに渡す文字列値 ( 例： `http://localhost:8080/soap/services/EncryptionService?WSDL`.) を使用する必要はありません。 `lc_version` 属性。 この属性は、サービス参照を作成する際に使用されます )。
   * の作成 `System.ServiceModel.BasicHttpBinding` オブジェクトを作成するには、 `EncryptionServiceClient.Endpoint.Binding` フィールドに入力します。 戻り値を `BasicHttpBinding` にキャストします。
   * を `System.ServiceModel.BasicHttpBinding` オブジェクトの `MessageEncoding` ～に向かって `WSMessageEncoding.Mtom`. この値は、MTOM が確実に使用されるようにします。
   * 次のタスクを実行して、基本的な HTTP 認証を有効にします。

      * フィールドにAEM forms ユーザー名を割り当てます。 `EncryptionServiceClient.ClientCredentials.UserName.UserName`.
      * 対応するパスワード値をフィールドに割り当てます。 `EncryptionServiceClient.ClientCredentials.UserName.Password`.
      * 定数値を割り当て `HttpClientCredentialType.Basic` フィールドに `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 定数値を割り当て `BasicHttpSecurityMode.TransportCredentialOnly` フィールドに `BasicHttpBindingSecurity.Security.Mode`.

1. 暗号化されたPDF文書を取得します。

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。
   * の作成 `System.IO.FileStream` オブジェクトを呼び出し、暗号化されたPDFドキュメントのファイルの場所と、ファイルを開くモードを表す string 値を渡すことによって、オブジェクトを指定します。
   * コンテンツを格納するバイト配列を作成します。 `System.IO.FileStream` オブジェクト。 バイト配列のサイズは、 `System.IO.FileStream` オブジェクトの `Length` プロパティ。
   * を呼び出して、バイト配列にストリームデータを入力します。 `System.IO.FileStream` オブジェクトの `Read` メソッドを使用し、読み込むバイト配列、開始位置、ストリーム長を渡す。
   * 次の項目に `BLOB` オブジェクトを作成するには、バイト配列の内容を `BLOB` オブジェクトの `MTOM` データメンバー。

1. ドキュメントのロックを解除します。

   を呼び出して、暗号化されたPDFドキュメントをロック解除します。 `EncryptionServiceClient` オブジェクトの `unlockPDFUsingPassword` または `unlockPDFUsingCredential` メソッド。

   パスワードで暗号化されたPDFドキュメントのロックを解除するには、 `unlockPDFUsingPassword` メソッドを使用して、次の値を渡します。

   * A `BLOB` パスワードで暗号化されたPDF・ドキュメントを格納するオブジェクト。
   * パスワードで暗号化されたパスワードドキュメントを開くために使用されるPDF値を指定する string 値です。 この値は、パスワードでPDFドキュメントを暗号化する際に指定します。

   証明書で暗号化されているPDFドキュメントのロックを解除するには、 `unlockPDFUsingCredential` メソッドを使用して、次の値を渡します。

   * A `BLOB` 証明書で暗号化されたPDF・ドキュメントを格納するオブジェクト。
   * PDf ドキュメントの暗号化に使用された秘密鍵に対応する公開鍵のエイリアス名を指定する string 値です。

   この `unlockPDFUsingPassword` および `unlockPDFUsingCredential` メソッドは両方とも `com.adobe.idp.Document` 別のAEM Formsメソッドに渡して操作を実行するオブジェクト。

1. AEM Forms操作を実行します。

   ロックが解除されたPDFドキュメントに対してAEM Forms操作を実行し、ビジネス要件を満たします。 例えば、使用権限をロック解除されたPDFドキュメントに適用する場合、 `BLOB` 次のいずれかによって返されたオブジェクト `unlockPDFUsingPassword` または `unlockPDFUsingCredential` メソッドから `ReaderExtensionsServiceClient` オブジェクトの `applyUsageRights` メソッド。

**関連トピック**

[手順の概要](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[MTOM を使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRef を使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 暗号化タイプの決定 {#determining-encryption-type}

Java Encryption Service API または Web サービス Encryption Service API を使用して、PDFドキュメントを保護する暗号化の種類をプログラムで判断できます。 PDF・ドキュメントが暗号化されているかどうか、および暗号化されている場合は暗号化タイプを動的に判断する必要が生じる場合があります。 例えば、パスワードベースの暗号化とPDFポリシーのどちらで保護されているかを指定できます。

PDFドキュメントは、次の暗号化タイプで保護できます。

* パスワードベースの暗号化
* 証明書ベースの暗号化
* ポリシーサービスによって作成されるRights Management
* 別のタイプの暗号化

>[!NOTE]
>
>Encryption サービスの詳細については、 [AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary_of_steps-5}

PDF・ドキュメントを保護する暗号化の種類を判断するには、次の手順に従います。

1. プロジェクトファイルを含めます。
1. 暗号化サービスクライアントを作成します。
1. 暗号化されたPDF文書を取得します。
1. 暗号化の種類を決定します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。 Web サービスを使用している場合は、プロキシファイルを必ず含めてください。

次の JAR ファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encryption-client.jar
* adobe-utilities.jar(AEM Formsが JBoss Application Server にデプロイされている場合に必要 )
* jbossall-client.jar(AEM Formsが JBoss Application Server にデプロイされている場合に必要 )

**サービスクライアントの作成**

プログラムによって Encryption サービスの操作を実行するには、Encryption サービスクライアントを作成する必要があります。 Java Encryption Service API を使用している場合は、 `EncrytionServiceClient` オブジェクト。 Web サービス Encryption Service API を使用する場合は、 `EncryptionServiceService` オブジェクト。

**暗号化されたPDF文書を取得**

保護する暗号化の種類を判断するには、PDF・ドキュメントを入手する必要があります。

**暗号化タイプの決定**

暗号化ドキュメントを保護する暗号化の種類をPDFできます。 PDFドキュメントが保護されていない場合、Encryption サービスは、PDFドキュメントが保護されていないことを通知します。

**関連トピック**

[Java API を使用した暗号化タイプの決定](encrypting-decrypting-pdf-documents.md#determine-the-encryption-type-using-the-java-api)

[Web サービス API を使用した暗号化の種類の決定](encrypting-decrypting-pdf-documents.md#determine-the-encryption-type-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Encryption サービス API のクイックスタート](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

[ポリシーを使用したドキュメントの保護](/help/forms/developing/protecting-documents-policies.md#protecting-documents-with-policies)

### Java API を使用した暗号化タイプの決定 {#determine-the-encryption-type-using-the-java-api}

Encryption API(Java) を使用して、PDF・ドキュメントを保護する暗号化の種類を決定します。

1. プロジェクトファイルを含めます。

   Java プロジェクトのクラスパスに、adobe-encryption-client.jar などのクライアント JAR ファイルを含めます。

1. サービスクライアントを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * の作成 `EncryptionServiceClient` オブジェクトのコンストラクタを使用し、 `ServiceClientFactory` オブジェクト。

1. 暗号化されたPDF文書を取得します。

   * の作成 `java.io.FileInputStream` コンストラクタを使用し、PDFドキュメントの場所を指定する string 値を渡すことによって、PDFドキュメントを表すオブジェクト。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. 暗号化の種類を決定します。

   * を呼び出して暗号化タイプを決定します。 `EncryptionServiceClient` オブジェクトの `getPDFEncryption` メソッドおよび `com.adobe.idp.Document` オブジェクトドキュメントを含むPDF。 このメソッドは、 `EncryptionTypeResult` オブジェクト。
   * を呼び出す `EncryptionTypeResult` オブジェクトの `getEncryptionType` メソッド。 このメソッドは、 `EncryptionType` 暗号化タイプを指定する enum 値。 例えば、パスワードベースの暗号化でPDFドキュメントが保護されている場合、このメソッドは `EncryptionType.PASSWORD`.

**関連トピック**

[手順の概要](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[クイックスタート（SOAP モード）:Java API を使用した暗号化タイプの決定](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-determining-encryption-type-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Web サービス API を使用した暗号化の種類の決定 {#determine-the-encryption-type-using-the-web-service-api}

Encryption API（Web サービス）を使用して、PDF・ドキュメントを保護する暗号化の種類を決定します。

1. プロジェクトファイルを含めます。

   MTOM を使用するMicrosoft .NET プロジェクトを作成します。 次の WSDL 定義を使用していることを確認します。 `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >置換 `localhost` を、AEM Formsをホストするサーバーの IP アドレスに設定します。

1. サービスクライアントを作成します。

   * の作成 `EncryptionServiceClient` オブジェクトのデフォルトのコンストラクタを使用します。
   * の作成 `EncryptionServiceClient.Endpoint.Address` オブジェクトを `System.ServiceModel.EndpointAddress` コンストラクタ。 WSDL をAEM Formsサービスに渡す文字列値 ( 例： `http://localhost:8080/soap/services/EncryptionService?WSDL`.) を使用する必要はありません。 `lc_version` 属性。 この属性は、サービス参照を作成する際に使用されます )。
   * の作成 `System.ServiceModel.BasicHttpBinding` オブジェクトを作成するには、 `EncryptionServiceClient.Endpoint.Binding` フィールドに入力します。 戻り値を `BasicHttpBinding` にキャストします。
   * を `System.ServiceModel.BasicHttpBinding` オブジェクトの `MessageEncoding` ～に向かって `WSMessageEncoding.Mtom`. この値は、MTOM が確実に使用されるようにします。
   * 次のタスクを実行して、基本的な HTTP 認証を有効にします。

      * フィールドにAEM forms ユーザー名を割り当てます。 `EncryptionServiceClient.ClientCredentials.UserName.UserName`.
      * 対応するパスワード値をフィールドに割り当てます。 `EncryptionServiceClient.ClientCredentials.UserName.Password`.
      * 定数値を割り当て `HttpClientCredentialType.Basic` フィールドに `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 定数値を割り当て `BasicHttpSecurityMode.TransportCredentialOnly` フィールドに `BasicHttpBindingSecurity.Security.Mode`.

1. 暗号化されたPDF文書を取得します。

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。
   * の作成 `System.IO.FileStream` オブジェクトを呼び出し、暗号化されたPDFドキュメントのファイルの場所と、ファイルを開くモードを表す string 値を渡すことによって、オブジェクトを指定します。
   * コンテンツを格納するバイト配列を作成します。 `System.IO.FileStream` オブジェクト。 バイト配列のサイズは、 `System.IO.FileStream` オブジェクトの `Length` プロパティ。
   * を呼び出して、バイト配列にストリームデータを入力します。 `System.IO.FileStream` オブジェクトの `Read` メソッドを使用し、読み込むバイト配列、開始位置、ストリーム長を渡す。
   * 次の項目に `BLOB` オブジェクトを作成するには、バイト配列の内容を `BLOB` オブジェクトの `MTOM` データメンバー。

1. 暗号化の種類を決定します。

   * を呼び出す `EncryptionServiceClient` オブジェクトの `getPDFEncryption` メソッドを使用して、 `BLOB` オブジェクトドキュメントを含むPDF。 このメソッドは、 `EncryptionTypeResult` オブジェクト。
   * の値を取得する `EncryptionTypeResult` オブジェクトの `encryptionType` データメソッド。 例えば、PDF・ドキュメントがパスワード・ベースの暗号化で保護されている場合、このデータ・メンバーの値は次のようになります。 `EncryptionType.PASSWORD`.

**関連トピック**

[手順の概要](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[MTOM を使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRef を使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
