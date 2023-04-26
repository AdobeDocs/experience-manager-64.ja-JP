---
title: WebSphere Application Server に対する SSL の設定
seo-title: Configuring SSL for WebSphere Application Server
description: WebSphere Application Server 用に SSL を設定する方法について説明します。
seo-description: Learn how to configure SSL for WebSphere Application Server.
uuid: f939a806-346e-41e0-b2c0-6d0ba83f8f6f
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_ssl
products: SG_EXPERIENCEMANAGER/6.4/FORMS
discoiquuid: 7c0efcb3-5b07-4090-9119-b7318c8b7980
exl-id: 653daaa4-9e35-40eb-a61e-274109f5f0d2
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '1227'
ht-degree: 18%

---

# WebSphere Application Server に対する SSL の設定 {#configuring-ssl-for-websphere-application-server}

この節では、IBM WebSphere Application Server で SSL を設定する次の手順について説明します。

## WebSphere でのローカルユーザーアカウントの作成 {#creating-a-local-user-account-on-websphere}

SSL を有効にするには、WebSphere は、ローカルの OS ユーザーレジストリ内の、システムを管理する権限を持つユーザーアカウントにアクセスする必要があります。

* (Windows) Administrators グループに属し、オペレーティングシステムの一部として機能する権限を持つ新しい Windows ユーザーを作成します。 ( [WebSphere 用の Windows ユーザーの作成](configuring-ssl-websphere-application-server.md#create-a-windows-user-for-websphere).)
* (Linux、UNIX)root ユーザーまたは root 権限を持つ別のユーザーを指定できます。 WebSphere で SSL を有効にする場合は、このユーザーのサーバー ID とパスワードを使用します。

### WebSphere 用の Linux または UNIX ユーザーの作成 {#create-a-linux-or-unix-user-for-websphere}

1. root ユーザーとしてログインします。
1. コマンドプロンプトで次のコマンドを入力して、ユーザーを作成します。

   * （Linux および Sun Solaris）`useradd`
   * （IBM AIX）`mkuser`

1. コマンドプロンプトで `passwd` と入力して、新しいユーザーのパスワードを設定します。
1. （Linux および Solaris）コマンドプロンプトでパラメーターを付けずに `pwconv` と入力して、シャドーパスワードファイルを作成します。

   >[!NOTE]
   >
   >（Linux および Solaris）WebSphere Application Server のローカル OS セキュリティレジストリが機能するには、シャドーパスワードファイルが存在している必要があります。シャドウパスワードファイルの名前は通常 **/etc/shadow***とは、/etc/passwd ファイルに基づいたものです。 シャドウパスワードファイルが存在しない場合は、グローバルセキュリティを有効にし、ユーザーレジストリをローカル OS として設定した後にエラーが発生します。*

1. /etc ディレクトリにあるグループファイルをテキストエディターで開きます。
1. 手順 2 で作成したユーザーを `root` グループに追加します。
1. ファイルを保存して閉じます。
1. （SSL が有効な UNIX）WebSphere を起動し、ルートユーザーとして停止します。

### WebSphere 用の Windows ユーザーの作成 {#create-a-windows-user-for-websphere}

1. Windows にログインするには、管理者のユーザーアカウントを使用します。
1. **スタート／コントロールパネル／管理ツール／コンピュータ管理／ローカルユーザーとグループ**&#x200B;を選択します。
1. ユーザーを右クリックし、「 」を選択します。 **新しいユーザー**.
1. 該当するボックスにユーザ名とパスワードを入力し、残りのボックスに必要な情報を入力します。
1. 選択を解除 **ユーザーは次回のログイン時にパスワードを変更する必要があります**&#x200B;をクリックし、 **作成**&#x200B;をクリックし、 **閉じる**.
1. クリック **ユーザー**、作成したユーザーを右クリックし、「 」を選択します。 **プロパティ**.
1. 次をクリック： **次のメンバー** タブを押し、 **追加**.
1. 「選択するオブジェクト名を入力」ボックスに `Administrators` と入力し、「名前の確認」をクリックしてグループ名が正しいことを確認します。
1. クリック **OK** 次に、 **OK** 再び
1. 選択 **[ スタート ] > [Campaign コントロールパネル] > [ 管理ツール ] > [ ローカルセキュリティポリシー ] > [ ローカルポリシー ]**.
1. [ ユーザー権限の割り当て ] をクリックし、[ オペレーティングシステムの一部として機能 ] を右クリックして、[ プロパティ ] を選択します。
1. クリック **ユーザーまたはグループを追加**.
1. 「選択するオブジェクト名を入力してください」ボックスに、手順 4 で作成したユーザー名を入力し、 **名前を確認** 名前が正しいことを確認するには、 **OK**.
1. クリック **OK** をクリックして、[ オペレーティングシステムのプロパティ ] ダイアログボックスの一部として機能を閉じます。

### 新しく作成したユーザーを管理者として使用するように WebSphere を設定 {#configure-websphere-to-use-the-newly-created-user-as-administrator}

1. WebSphere が実行中であることを確認します。
1. WebSphere Administrative Console で、 **セキュリティ/グローバルセキュリティ**.
1. 「管理セキュリティ」で、「 **管理ユーザーの役割**.
1. 「追加」をクリックし、以下の手順を実行します。

   1. 検索ボックスに「**&amp;ast;**」と入力し、「検索」をクリックします。
   1. クリック **管理者** 「役割」で、
   1. 新しく作成したユーザーを「Mapped to role」に追加し、管理者にマッピングします。

1. クリック **OK** 変更を保存します。
1. WebSphere プロファイルを再起動します。

## 管理セキュリティの有効化 {#enable-administrative-security}

1. WebSphere Administrative Console で、 **セキュリティ/グローバルセキュリティ**.
1. クリック **セキュリティ構成ウィザード**.
1. 確認 **アプリケーションセキュリティの有効化** チェックボックスが有効になっている。 「**次へ**」をクリックします。
1. 選択 **Federated Repositories** をクリックし、 **次へ**.
1. 設定する資格情報を指定し、「 」をクリックします **次へ**.
1. 「**終了**」をクリックします。
1. WebSphere プロファイルを再起動します。

   WebSphere は、デフォルトのキーストアと信頼ストアを使用して起動します。

## SSL を有効にする（カスタムキーと信頼ストア） {#enable-ssl-custom-key-and-truststore}

信頼ストアとキーストアは ikeyman ユーティリティまたは管理コンソールを使用して作成できます。ikeyman を正しく動作させるには、WebSphere のインストールパスに括弧が含まれていないことを確認します。

1. WebSphere Administrative Console で、 **セキュリティ/SSL 証明書および鍵の管理**.
1. クリック **キーストアと証明書** をクリックします。
1. 内 **キーストアの使用** ドロップダウン、 **SSL キーストア** が選択されている。 「**新規**」をクリックします。
1. 論理名と説明を入力します。
1. キーストアを作成する場所のパスを指定します。ikeyman を使用して既にキーストアを作成している場合は、キーストアファイルのパスを指定します。
1. パスワードを指定して確定します。
1. キーストアタイプを選択し、 **適用**.
1. マスター設定を保存します。
1. クリック **個人の証明書**.
1. ikeyman を使用してキーストアを既に作成している場合は、証明書が表示されます。 それ以外の場合は、次の手順を実行して、新しい自己署名証明書を追加する必要があります。

   1. 選択 **作成/自己署名証明書**.
   1. 証明書フォームで適切な値を指定します。 エイリアスと共通名をマシンの完全修飾ドメイン名として保持してください。
   1. 「**適用**」をクリックします。

1. 手順 2 ～ 10 を繰り返して、トラストストアを作成します。

## カスタムキーストアと信頼ストアをサーバーに適用する {#apply-custom-keystore-and-truststore-to-the-server}

1. WebSphere Administrative Console で、 **セキュリティ/SSL 証明書および鍵の管理**.
1. クリック **エンドポイントセキュリティ設定を管理**. ローカルトポロジマップが開きます。
1. 「Inbound」で、ノードの直接の子を選択します。
1. 「関連アイテム」で、「 **SSL 設定**.
1. 選択 **NodeDefaultSSLSetting**.
1. truststore 名とキーストア名のドロップダウンリストから、作成したカスタムの信頼ストアとキーストアを選択します。
1. 「**適用**」をクリックします。
1. マスター設定を保存します。
1. WebSphere プロファイルを再起動します。

   これで、プロファイルは SSL 設定と証明書の上で実行されます。

## AEM forms ネイティブのサポートの有効化 {#enabling-support-for-aem-forms-natives}

1. WebSphere Administrative Console で、 **セキュリティ/グローバルセキュリティ**.
1. 「認証」セクションで、を展開します。 **RMI/IIOP セキュリティ** をクリックし、 **CSIv2 Inbound Communications**.
1. 以下を確認します。 **SSL 対応** が「トランスポート」ドロップダウンリストで選択されている。
1. WebSphere プロファイルを再起動します。

## https で始まる URL を変換するための WebSphere の設定 {#configuring-websphere-to-convert-urls-that-begins-with-https}

https で始まる URL を変換するには、その URL の署名者証明書を WebSphere サーバーに追加します。

**https 対応サイト用の署名者証明書の作成**

1. WebSphere が実行中であることを確認します。
1. WebSphere Administrative Console で、「Signer certificates」に移動し、「Security/SSL Certificate and Key Management」/「Key Stores and Certificates」/「NodeDefaultTrustStore/Signer Certificates」の順にクリックします。
1. [Retrieve From Port] をクリックし、次のタスクを実行します。

   * 「ホスト」ボックスに URL を入力します。 例えば、`www.paypal.com` と入力します。
   * 「ポート」ボックスに、`443` と入力します。このポートはデフォルトの SSL ポートです。
   * 「エイリアス」ボックスにエイリアスを入力します。

1. 「署名者の情報を取得」をクリックし、情報が取得されることを確認します。
1. 「適用」をクリックし、「保存」をクリックします。

証明書が追加されたサイトからのHTML間PDF変換は、GeneratePDFサービスから機能するようになりました。

>[!NOTE]
>
>アプリケーションが WebSphere 内から SSL サイトに接続するには、署名者証明書が必要です。 SSL ハンドシェイク中に接続のリモート側が送信した証明書を検証するために、Java Secure Socket Extensions(JSSE) で使用されます。

## 動的ポートの設定 {#configuring-dynamic-ports}

IBM WebSphere では、グローバルセキュリティが有効な場合、ORB.init() への複数の呼び出しは許可されません。 永続的な制限については、https://www-01.ibm.com/support/docview.wss?uid=swg1PK58704 を参照してください。

動的なポートを設定し、問題を解決するには、次の手順を実行します。

1. WebSphere Administrative Console で、 **サーバー** > **サーバータイプ** > **WebSphere Application Server**.
1. 「環境設定」セクションで、サーバーを選択します。
1. 内 **設定** タブ、下 **通信** セクション、展開 **ポート**&#x200B;をクリックし、 **詳細**.
1. 次のポート名をクリックし、 **ポート番号** を 0 に設定し、をクリックします。 **OK**.

   * `ORB_LISTENER_ADDRESS`
   * `SAS_SSL_SERVERAUTH_LISTENER_ADDRESS`
   * `CSIV2_SSL_SERVERAUTH_LISTENER_ADDRESS`
   * `CSIV2_SSL_MUTUALAUTH_LISTENER_ADDRESS`

## sling.properties ファイルを設定します。 {#configure-the-sling-properties-file}

1. 開く [aem-forms_root]\crx-repository\launchpad\sling.propertiesファイルを編集します。
1. `sling.bootdelegation.ibm` プロパティを見つけてその値フィールドに `com.ibm.websphere.ssl.*` を追加します。更新されたフィールドは次のようになります。

   ```as3
   sling.bootdelegation.ibm=com.ibm.xml.*, com.ibm.websphere.ssl.*
   ```

1. ファイルを保存し、サーバーを再起動します。
