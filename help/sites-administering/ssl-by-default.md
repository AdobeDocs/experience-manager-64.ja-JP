---
title: デフォルトの SSL
seo-title: SSL By Default
description: AEMでデフォルトで SSL を使用する方法を説明します。
seo-description: Learn how to use SSL by Default in AEM.
uuid: 262474b0-f5fa-4cff-8727-9f39c5b5f760
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: Security
discoiquuid: 3a1817cd-357b-473d-9a09-e18bbfc60dfd
exl-id: 07f89673-125b-4205-bc54-c90287a1e9a5
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '797'
ht-degree: 46%

---

# デフォルトの SSL{#ssl-by-default}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

AEMのセキュリティを継続的に改善するために、Adobeではデフォルトで SSL と呼ばれる機能が導入されました。 この目的は、AEMインスタンスへの接続に HTTPS の使用を推奨することです。

## デフォルトでの SSL の有効化 {#enabling-ssl-by-default}

AEMのホーム画面から関連するインボックスメッセージをクリックして、デフォルトで SSL の設定を開始できます。 インボックスに移動するには、画面の右上隅にあるベルのアイコンを押します。 次に、 **すべて表示**. これにより、リストビューで並べ替えられたすべてのアラートのリストが表示されます。

リストで、を選択してを開きます。 **HTTPS を設定** アラート：

![chlimage_1-341](assets/chlimage_1-341.png)

>[注意!]
>
>**HTTPS を設定**&#x200B;アラートがインボックスに表示されていない場合は、*<http://serveraddress:serverport/libs/granite/security/content/sslConfig.html?item=configuration%2fconfiguressl&_charset_=utf-8>* にアクセスして、直接 HTTPS ウィザードに移動できます。

**ssl-service** というサービスユーザーが、この機能のために作成されています。アラートを開くと、次の設定ウィザードに従って進みます。

1. 最初に、「ストア資格情報」を設定します。これらは、HTTPS リスナーの秘密鍵とトラストストアが格納される、**ssl-service** システムユーザーのキーストアの資格情報です。

   ![chlimage_1-342](assets/chlimage_1-342.png)

1. 資格情報を入力したら、「 **次へ** をクリックします。 次に、SSL 接続用に関連付けられた秘密鍵と証明書をアップロードします。

   ![chlimage_1-343](assets/chlimage_1-343.png)

   >[!NOTE]
   >
   >ウィザードで使用する秘密鍵および証明書の生成方法について詳しくは、以下の[この手順](/help/sites-administering/ssl-by-default.md#generating-a-private-key-certificate-pair-to-use-with-the-wizard)を参照してください。

1. 最後に、HTTPS リスナーの HTTPS ホスト名と TCP ポートを指定します。

   ![screen_shot_2018-07-25at31658pm](assets/screen_shot_2018-07-25at31658pm.png)

## デフォルトでの SSL の自動化 {#automating-ssl-by-default}

デフォルトで SSL を自動化する方法は 3 つあります。

### HTTPPOST {#via-http-post}

1 つ目のメソッドでは、設定ウィザードで使用される SSLSetup サーバーに次のようにポストします。

```shell
POST /libs/granite/security/post/sslSetup.html
```

設定を自動化するには、次のペイロードをPOSTで使用します。

```xml
------WebKitFormBoundaryyBO4ArmGlcfdGDbs
Content-Disposition: form-data; name="keystorePassword"
 
test
------WebKitFormBoundaryyBO4ArmGlcfdGDbs
Content-Disposition: form-data; name="keystorePasswordConfirm"
test
------WebKitFormBoundaryyBO4ArmGlcfdGDbs
Content-Disposition: form-data; name="truststorePassword"
test
------WebKitFormBoundaryyBO4ArmGlcfdGDbs
Content-Disposition: form-data; name="truststorePasswordConfirm"
test
------WebKitFormBoundaryyBO4ArmGlcfdGDbs
Content-Disposition: form-data; name="privatekeyFile"; filename="server.der"
Content-Type: application/x-x509-ca-cert
 
------WebKitFormBoundaryyBO4ArmGlcfdGDbs
Content-Disposition: form-data; name="certificateFile"; filename="server.crt"
Content-Type: application/x-x509-ca-cert
 
------WebKitFormBoundaryyBO4ArmGlcfdGDbs
Content-Disposition: form-data; name="httpsPort"
8443
```

このサーブレットは、他の SlingPOSTサーブレットと同様に、200 OK またはエラー HTTP ステータスコードで応答します。 ステータスに関する詳細は、応答のHTML本文で確認できます。

次に、成功応答とエラーの両方の例を示します。

**成功の例**（ステータス = 200）：

```xml
<!DOCTYPE html>
<html lang='en'>
<head>
<title>OK</title>
</head>
<body>
<h1>OK</h1>
<dl>
<dt class='foundation-form-response-status-code'>Status</dt>
<dd>200</dd>
<dt class='foundation-form-response-status-message'>Message</dt>
<dd>SSL successfully configured</dd>
<dt class='foundation-form-response-title'>Title</dt>
<dd>OK</dd>
<dt class='foundation-form-response-description'>Description</dt>
<dd>HTTPS has been configured on port 8443. The private key and
certificate were stored in the key store of the user ssl-service.
Please take note of the key store password you provided. You will need
it for any subsequent updating of the private key or certificate.</dd>
</dl>
<h2>Links</h2>
<ul class='foundation-form-response-links'>
<li><a class='foundation-form-response-redirect' href='/'>Done</a></li>
</ul>
</body>
</html>
```

**エラーの例**（ステータス = 500）：

```xml
<!DOCTYPE html>
<html lang='en'>
<head>
<title>Error</title>
</head>
<body>
<h1>Error</h1>
<dl>
<dt class='foundation-form-response-status-code'>Status</dt>
<dd>500</dd>
<dt class='foundation-form-response-status-message'>Message</dt>
<dd>The provided file is not a valid key, DER format expected</dd>
<dt class='foundation-form-response-title'>Title</dt>
<dd>Error</dd>
</dl>
</body>
</html>
```

### パッケージ経由 {#via-package}

または、次の必須項目が既に含まれているパッケージをアップロードして、SSL 設定を自動化することもできます。

* ssl-service ユーザーのキーストア。 これは、 */home/users/system/security/ssl-service/keystore* リポジトリ内に保存されます。
* `GraniteSslConnectorFactory` 設定

### ウィザードで使用する秘密鍵／証明書ペアの生成 {#generating-a-private-key-certificate-pair-to-use-with-the-wizard}

以下は、SSL ウィザードで使用できる DER 形式の自己署名証明書を作成する例です。

>[!NOTE]
>
>自己署名証明書は例を示すためにのみ使用しており、実稼動では使用しないでください。

1. まず、秘密鍵を作成します。

   ```shell
   openssl genrsa -aes256 -out localhostprivate.key 4096
   openssl rsa -in localhostprivate.key -out localhostprivate.key
   ```

1. 次に、秘密鍵を使用して証明書署名要求（CSR）を生成します。

   ```shell
   openssl req -sha256 -new -key localhostprivate.key -out localhost.csr -subj '/CN=localhost'
   ```

1. SSL 証明書を生成し、秘密鍵で署名します。 この例では、は今から 1 年後に期限切れになります。

   ```shell
   openssl x509 -req -days 365 -in localhost.csr -signkey localhostprivate.key -out localhost.crt
   ```

秘密鍵を DER 形式に変換します。 これは、SSL ウィザードでは DER 形式のキーが必要だからです。

```shell
openssl pkcs8 -topk8 -inform PEM -outform DER -in localhostprivate.key -out localhostprivate.der -nocrypt
```

最後に、 **localhostprivate.der** 秘密鍵として、および **localhost.crt** を、このページの最初で説明したグラフィカルな SSL ウィザードの手順 2 の SSL 証明書として使用します。

### cURL を使用した SSL 設定の更新 {#updating-the-ssl-configuration-via-curl}

>[!NOTE]
>
>AEM で利用できる cURL コマンドをまとめたリストについては、[AEM での cURL の使用](https://helpx.adobe.com/jp/experience-manager/6-4/sites/administering/using/curl.html)を参照してください。

また、cURL ツールを使用して SSL 設定を自動化することもできます。 これをおこなうには、設定パラメーターをこの URL に投稿します。

*https://&lt;serveraddress>:&lt;serverport>/libs/granite/security/post/sslSetup.html*

以下は、設定ウィザードの様々な設定を変更するために使用できるパラメーターです。

* `-F "keystorePassword=password"` - キーストアのパスワード。

* `-F "keystorePasswordConfirm=password"` - キーストアのパスワードを確認します。

* `-F "truststorePassword=password"` - トラストストアのパスワード。

* `-F "truststorePasswordConfirm=password"` - トラストストアのパスワードを確認します。

* `-F "privatekeyFile=@localhostprivate.der"` - 秘密鍵を指定します。

* `-F "certificateFile=@localhost.crt"` - 証明書を指定します。

* `-F "httpsHostname=host.example.com"` - ホスト名を指定します。
* `-F "httpsPort=8443"` - HTTPS リスナーが動作するポート。

>[!NOTE]
>
>SSL 設定を自動化するための cURL は、DER および CRT ファイルが存在するフォルダーから実行すると最も速く実行されます。または、`privatekeyFile` および certificateFile 引数でフルパスを指定できます。
>
>また、更新の実行には認証が必要なため、cURL コマンドに `-u user:passeword` パラメーターを付加します。
>
>正しい cURL POST コマンドは、次のようになります。

```shell
curl -u user:password -F "keystorePassword=password" -F "keystorePasswordConfirm=password" -F "truststorePassword=password" -F "truststorePasswordConfirm=password" -F "privatekeyFile=@localhostprivate.der" -F "certificateFile=@localhost.crt" -F "httpsHostname=host.example.com" -F "httpsPort=8443" https://host:port/libs/granite/security/post/sslSetup.html
```

#### cURL を使用する複数の証明書 {#multiple-certificates-using-curl}

次のように certificateFile パラメーターを繰り返すことで、サーブレットに証明書のチェーンを送信できます。

`-F "certificateFile=@root.crt" -F "certificateFile=@localhost.crt"..`

コマンドを実行したら、すべての証明書がキーストアに送信されたことを確認します。キーストアの確認元：\
[http://localhost:4502/libs/granite/security/content/userEditor.html/home/users/system/security/ssl-service](http://localhost:4502/libs/granite/security/content/userEditor.html/home/users/system/security/ssl-service)
