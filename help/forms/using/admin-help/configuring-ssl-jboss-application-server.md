---
title: JBoss Application Server に対する SSL の設定
seo-title: Configuring SSL for JBoss Application Server
description: JBoss Application Server に対する SSL の設定方法について説明します。
seo-description: Learn how to configure SSL for JBoss Application Server.
uuid: 7c13cf00-ea89-4894-a4fc-aaeec7ae9f66
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_ssl
products: SG_EXPERIENCEMANAGER/6.4/FORMS
discoiquuid: c187daa4-41b7-47dc-9669-d7120850cafd
exl-id: 1888b8c7-d077-4e54-b442-5df0ba557513
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '908'
ht-degree: 50%

---

# JBoss Application Server に対する SSL の設定 {#configuring-ssl-for-jboss-application-server}

JBoss Application Server で SSL を設定するには、認証時に SSL 秘密鍵証明書が必要です。秘密鍵証明書は、Java keytool を使用して作成するか、認証局（CA）から要求して読み込むことができます。その後、JBoss で SSL を有効にする必要があります。

1 つのコマンドでキーストアの作成に必要なすべての情報を指定することによって、keytool を実行できます。

ここでの手順では次のように指定します。

* `[appserver root]` は、AEM forms を実行するアプリケーションサーバーのホームディレクトリです。
* `[type]` は、実行したインストールの種類に応じて異なるフォルダ名です。

## SSL 秘密鍵証明書の作成 {#create-an-ssl-credential}

1. コマンドプロンプトで、に移動します。 *[JAVA ホーム]*/bin を開き、次のコマンドを入力して秘密鍵証明書とキーストアを作成します。

   `keytool -genkey -dname "CN=`*ホスト名* `, OU=`*グループ名* `, O=`*会社名* `,L=`*市区町村名* `, S=`*都道府県* `, C=`国コード» `-alias "AEMForms Cert"` `-keyalg RSA -keypass`*key_password* `-keystore`*keystorename* `.keystore`

   >[!NOTE]
   >
   >置換 `[JAVA_HOME]` を JDK がインストールされているディレクトリに置き換え、斜体のテキストを環境に対応する値に置き換えます。 「Host Name」は、アプリケーションサーバーの完全修飾ドメイン名です。

1. 次を入力します。 `keystore_password` パスワードの入力を求められた場合。 キーストアおよびキーのパスワードは、同じである必要があります。

   >[!NOTE]
   >
   >この `keystore_password` *このステップで入力するパスワードは、ステップ 1 で入力したものと同じか、異なる場合があります。*

1. を *keystorename*.keystore を `[appserver root]/server/[type]/conf` 次のいずれかのコマンドを入力してディレクトリに追加します。

   * （Windows シングルサーバ） `copy` `keystorename.keystore[appserver root]\standalone\configuration`
   * （Windows Server クラスタ）コピー `keystorename.keystore[appserver root]\domain\configuration`
   * （Linux シングルサーバ） `cp keystorename.keystore [appserver root]/standalone/configuration`
   * （Linux サーバクラスタ） `cp <em>keystorename</em>.keystore<em>[appserver root]</em>/domain/configuration`


1. 次のコマンドを入力して、証明書ファイルを書き出します。

   * （シングルサーバー） `keytool -export -alias "AEMForms Cert" -file AEMForms_cert.cer -keystore [appserver root]/standalone/configuration/keystorename.keystore`
   * （サーバークラスター） `keytool -export -alias "AEMForms Cert" -file AEMForms_cert.cer -keystore [appserver root]/domain/configuration/keystorename.keystore`

1. パスワードの入力を求められたら、*keystore_password*&#x200B;を入力します。
1. AEMForms_cert.cer ファイルを *[appserver root] \conf* 次のコマンドを入力してディレクトリに追加します。

   * （Windows シングルサーバ） `copy AEMForms_cert.cer [appserver root]\standalone\configuration`
   * （Windows Server クラスタ） `copy AEMForms_cert.cer [appserver root]\domain\configuration`
   * （Linux シングルサーバ） `cp AEMForms _cert.cer [appserver root]\standalone\configuration`
   * （Linux サーバクラスタ） `cp AEMForms _cert.cer [appserver root]\domain\configuration`

1. 次のコマンドを入力して、証明書の内容を表示します。

   * `keytool -printcert -v -file [appserver root]\standalone\configuration\AEMForms_cert.cer`
   * `keytool -printcert -v -file [appserver root]\domain\configuration\AEMForms_cert.cer`

1. の cacerts ファイルへの書き込みアクセス権を提供するには `[JAVA_HOME]\jre\lib\security`必要に応じて、次のタスクを実行します。

   * （Windows）cacerts ファイルを右クリックして「プロパティ」を選択し、「読み取り専用」属性の選択を解除します。
   * (Linux) タイプ `chmod 777 cacerts`

1. 次のコマンドを入力して、証明書ファイルを読み込みます。

   `keytool -import -alias “AEMForms Cert” -file`*AEMForms_cert* `.cer -keystore`*JAVA_HOME* `\jre\lib\security\cacerts`

1. タイプ `changeit` をパスワードとして設定します。 Java インストールではこれがデフォルトのパスワードですが、システム管理者によって変更されている場合があります。
1. 次を求められた場合： `Trust this certificate? [no]`:、型 `yes`. 「Certificate was added to keystore」という確認メッセージが表示されます。
1. Workbench から SSL 経由で接続している場合は、Workbench コンピューターに証明書をインストールします。
1. テキストエディターで、次のファイルを編集用に開きます。

   * シングルサーバ — `[appserver root]`/standalone/configuration/lc_&lt;dbname turnkey=&quot;&quot;>.xml

   * サーバークラスタ — `[appserver root]`/domain/configuration/host.xml

   * サーバークラスタ — `[appserver root]`/domain/configuration/domain_&lt;dbname>.xml

1. 
   * **シングルサーバーの場合、** lc_&lt;dbaname/tunkey>.xml ファイルの &lt;security-realms> セクションに次のテキストを追加します。

   ```as3
   <security-realm name="SSLRealm">
   <server-identities>
   <ssl>
   <keystore path="C:/Adobe/Adobe_Experience_Manager_Forms/jboss/standalone/configuration/aemformses.keystore" keystore-password="changeit" alias="AEMformsCert" key-password="changeit"/>
   </ssl>
   </server-identities>
   </security-realm>
   ```

   を `<server>` セクションが次のコードの後に存在します。

   `<http-listener name="default" socket-binding="http" redirect-socket="https" max-post-size="104857600"/>`

   上記のコードの後の &lt;server> セクションに次のテキストを追加します。

   ```
   <https-listener name="default-secure" socket-binding="https" security-realm="SSLRealm"/>
   ```

   * **サーバークラスタの場合、** 内 [appserver root]\domain\configuration\host.xmlをすべてのノードで、の後に次を追加します。 &lt;security-realms> セクション：

   ```as3
   <security-realm name="SSLRealm">
   <server-identities>
   <ssl>
   <keystore path="C:/Adobe/Adobe_Experience_Manager_Forms/jboss/standalone/configuration/aemformses.keystore" keystore-password="changeit" alias="AEMForms Cert" key-password="changeit"/>
   </ssl>
   </server-identities>
   </security-realm>
   ```

   サーバークラスタのプライマリノード上の [appserver root]\domain\configuration\domain_&lt;dbname>.xml、 &lt;server> セクションが次のコードの後に存在します。

   `<http-listener name="default" socket-binding="http" redirect-socket="https" max-post-size="104857600"/>`

   上記のコードの後の &lt;server> セクションに次のテキストを追加します。

   ```
   <https-listener name="default-secure" socket-binding="https" security-realm="SSLRealm"/>
   ```

1. `keystoreFile` 属性および `keystorePass` 属性の値を、キーストアの作成時に指定したキーストアパスワードに変更します。
1. アプリケーションサーバーを再起動します。

   * 自動インストールの場合：

      * Windows のコントロールパネルで、「管理ツール」をクリックして「サービス」をクリックします。
      * JBoss for Adobe Experience Manager forms を選択します。
      * 操作／停止を選択します。
      * サービスのステータスが停止になるまで待機します。
      * 操作／開始を選択します。
   * Adobe により事前設定された、または手動で設定した JBoss インストールの場合：

      * コマンドプロンプトで、に移動します。 *`[appserver root]`*/bin.
      * 次のコマンドを入力して、サーバーを停止します。

         * (Windows) `shutdown.bat -S`
         * (Linux) `./shutdown.sh -S`
      * JBoss プロセスが完全にシャットダウンする（JBoss プロセスが、起動された端末にコントロールを返す）まで待機します。
      * 次のコマンドを入力して、サーバーを起動します。

         * (Windows) `run.bat -c <profile>`
         * (Linux) `./run.sh -c <profile>`



1. SSL を使用して管理コンソールにアクセスするには、「 `https://[host name]:[port]/adminui` web ブラウザーの場合：

   JBoss のデフォルト SSL ポートは 8443 です。以降 AEM Forms にアクセスするときはこのポートを指定します。

## CA からの秘密鍵証明書の要求 {#request-a-credential-from-a-ca}

1. コマンドプロンプトで、に移動します。 *[JAVA ホーム]*/bin を開き、次のコマンドを入力してキーストアとキーを作成します。

   `keytool -genkey -dname "CN=`*ホスト名* `, OU=`*グループ名* `, O=`*会社名* `, L=`*市区町村名* `, S=`*都道府県* `, C=`*国コード*&quot; `-alias "AEMForms Cert"` `-keyalg RSA -keypass`-*key_password* `-keystore`*keystorename* `.keystore`

   >[!NOTE]
   >
   >置換 *`[JAVA_HOME]`* を JDK がインストールされているディレクトリに置き換え、斜体のテキストを環境に対応する値に置き換えます。

1. 次のコマンドを入力して証明書要求を生成し、認証局に送信します

   `keytool -certreq -alias` &quot;AEM Forms 証明書&quot; `-keystore`*keystorename* `.keystore -file`*AEMormscertRequest.csr*

1. 証明書ファイルの要求が完了したら、次の手順を実行します。

## CA から取得した秘密鍵証明書の SSL を有効にするための使用 {#use-a-credential-obtained-from-a-ca-to-enable-ssl}

1. コマンドプロンプトで、に移動します。 *`[JAVA HOME]`*/bin と次のコマンドを入力して、CSR が署名されている CA のルート証明書をインポートします。

   `keytool -import -trustcacerts -file` rootcert.pem -keystore` keystorename.keystore -alias root`

   ルート証明書がブラウザーにない場合は、ブラウザーにも読み込みます。

   >[!NOTE]
   >
   >置換 *`[JAVA_HOME]`を JDK がインストールされているディレクトリに置き換え、斜体のテキストを環境に対応する値に置き換えます。*

1. コマンドプロンプトで、に移動します。 *`[JAVA HOME]`*/bin と次のコマンドを入力して、秘密鍵証明書をキーストアに読み込みます。

   `keytool -import -trustcacerts -file`*CACertificateName* `.crt -keystore`*keystorename* `.keystore`

   >[!NOTE]
   >
   >* 置換 `[JAVA_HOME]` を JDK がインストールされているディレクトリに置き換え、斜体のテキストを環境に対応する値に置き換えます。
   >* 自己署名の公開証明書が存在する場合は、読み込んだ CA 署名付き証明書に置き換えられます。


1. SSL 秘密鍵証明書の作成の手順 13～18 を実行します。
