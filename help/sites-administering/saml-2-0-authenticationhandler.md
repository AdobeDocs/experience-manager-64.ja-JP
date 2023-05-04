---
title: SAML 2.0 認証ハンドラー
seo-title: SAML 2.0 Authentication Handler
description: AEMの SAML 2.0 認証ハンドラーについて説明します。
seo-description: Learn about the SAML 2.0 Authentication Handler in AEM.
uuid: 51f97315-350a-42a4-af2c-2de87307c6ad
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: Security
content-type: reference
discoiquuid: 6ed09b5d-5089-43d2-b9d5-e7db57be5c02
exl-id: 4868daad-0f3e-48cb-9b20-08dee270e74e
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '878'
ht-degree: 72%

---

# SAML 2.0 認証ハンドラー {#saml-authentication-handler}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

AEM には、[SAML](http://saml.xml.org/saml-specifications) 認証ハンドラーが付属しています。このハンドラーによって、`HTTP POST` バインディングを使用した [SAML](http://saml.xml.org/saml-specifications) 2.0 認証要求プロトコル（Web-SSO プロファイル）のサポートが提供されます。

次の機能をサポートします。

* メッセージの署名と暗号化
* ユーザーの自動作成
* AEM でグループを既存のグループに同期させる
* サービスプロバイダーと ID プロバイダーで開始される認証

このハンドラーは、暗号化された SAML 応答メッセージをユーザーノード（`usernode/samlResponse`）に格納して、サードパーティのサービスプロバイダーとの通信を容易にします。

>[!NOTE]
>
>[AEM と SAML の統合のデモンストレーション](https://helpx.adobe.com/experience-manager/kb/simple-saml-demo.html)を参照してください。
>
>エンドツーエンドのコミュニティ記事を読むには、以下をクリックします。 [SAML とAdobe Experience Managerの統合](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/saml-2-0-authenticationhandler.html?lang=ja).

## SAML 2.0 認証ハンドラーの設定 {#configuring-the-saml-authentication-handler}

[Web コンソール](/help/sites-deploying/configuring-osgi.md)を使用すると、[SAML](http://saml.xml.org/saml-specifications) 2.0 認証ハンドラーの設定（**Adobe Granite SAML 2.0 Authentication Handler**）にアクセスできます。設定可能なプロパティを以下に示します。

>[!NOTE]
>
>SAML 2.0 認証ハンドラーはデフォルトで無効になっています。 ハンドラーを有効にするには、次のプロパティを少なくとも 1 つ設定する必要があります。
>
>* ID プロバイダーの POST の URL
>* サービスプロバイダーのエンティティ ID
>


>[!NOTE]
>
>SAML アサーションは署名され、オプションで暗号化できます。 そのためには、少なくとも ID プロバイダーの公開証明書を TrustStore に指定する必要があります。詳しくは、[TrustStore への IdP 証明書の追加](/help/sites-administering/saml-2-0-authenticationhandler.md#add-the-idp-certificate-to-the-aem-truststore)のセクションを参照してください。

**パス** この認証ハンドラーが Sling によって使用される場合のリポジトリのパスです。このプロパティが空の場合は、認証ハンドラーが無効になります。

**サービスランキング** このサービスを呼び出す順序を示す OSGi フレームワークサービスランキングの値です。これは整数値で、値が大きいほど優先順位が高くなります。

**IDP 証明書エイリアス** グローバル TrustStore における IdP の証明書のエイリアスです。このプロパティが空の場合は、認証ハンドラーが無効になります。設定方法については、以下の「AEM TrustStore への IdP 証明書の追加」の章を参照してください。

**ID プロバイダーの URL** SAML 認証要求を送信する必要のある IDP の URL です。このプロパティが空の場合は、認証ハンドラーが無効になります。

>[!CAUTION]
>
>ID プロバイダーのホスト名は **Apache Sling Referrer Filter** の OSGi 設定に追加する必要があります。詳しくは、[web コンソール](/help/sites-deploying/configuring-osgi.md)に関するセクションを参照してください。

**サービスプロバイダーのエンティティ ID** このサービスプロバイダーを ID プロバイダーとして一意に識別する ID です。このプロパティが空の場合は、認証ハンドラーが無効になります。

**デフォルトのリダイレクト** 認証が成功した後のデフォルトのリダイレクト先です。

>[!NOTE]
>
>この場所は、`request-path` の Cookie が設定されていない場合にのみ使用されます。有効なログイントークンを使用せずに、設定済みのパスの下にあるページを要求すると、要求されたパスは Cookie に格納され、\
>認証が成功した後にブラウザーは再びこの場所にリダイレクトされます。

**ユーザー ID 属性** CRX リポジトリでのユーザーの認証および作成に使用されるユーザー ID を格納する属性の名前です。

>[!NOTE]
>
>ユーザー ID は SAML アサーションの `saml:Subject` ノードではなく、この `saml:Attribute` から取得されます。

**暗号化を使用** この認証ハンドラーが暗号化された SAML アサーションを使用するかどうかを示します。

**CRX ユーザーを自動作成** 認証が成功した後に、リポジトリで既存のユーザー以外のユーザーを自動的に作成するかどうかを示します。

>[!CAUTION]
>
>CRX ユーザーの自動作成が無効な場合は、ユーザーを手動で作成する必要があります。

**グループに追加** 認証が成功した後に、CRX グループにユーザーを自動的に追加する必要があるかどうかを示します。

**グループメンバーシップ** このユーザが追加されるべき CRX グループのリストを含む saml:Attribute の名前です。

## IdP 証明書をAEM TrustStore に追加する {#add-the-idp-certificate-to-the-aem-truststore}

SAML アサーションは署名され、オプションで暗号化できます。 この機能を使用するには、リポジトリ内の IdP の公開証明書を少なくとも指定する必要があります。 これをおこなうには、次の手順を実行する必要があります。

1. *http:/serveraddress:serverport/libs/granite/security/content/truststore.html* に移動します。
1. **[!UICONTROL TrustStore リンクを作成]** を押します。
1. TrustStore のパスワードを入力し、 **[!UICONTROL 保存]**.
1. クリック **[!UICONTROL TrustStore を管理]**.
1. IdP 証明書をアップロードします。
1. 証明書のエイリアスをメモします。 エイリアスはです。 **[!UICONTROL admin#1436172864930]** を次の例に示します。

   ![chlimage_1-372](assets/chlimage_1-372.png)

## AEM キーストアへのサービスプロバイダーキーと証明書チェーンを追加 {#add-the-service-provider-key-and-certificate-chain-to-the-aem-keystore}

>[!NOTE]
>
>以下のステップは必須です。実行しないと、次の例外が発生します。`com.adobe.granite.keystore.KeyStoreNotInitialisedException: Uninitialised system trust store`

1. [http://localhost:4502/libs/granite/security/content/useradmin.html](http://localhost:4502/libs/granite/security/content/useradmin.html) に移動します。
1. `authentication-service` ユーザーを編集します。
1. **アカウント設定** の **キーストアを作成** をクリックしてキーストアを作成します。

>[!NOTE]
>
>以下のステップは、ハンドラーが署名またはメッセージを複合化できるようにする必要がある場合にのみ必須です。

1. **秘密鍵ファイルを選択** をクリックして秘密鍵ファイルをアップロードします。この鍵は PKCS#8 形式で、エンコードが DER である必要があります。
1. 「 **証明書チェーンファイルを選択**.
1. 次に示すように、エイリアスを割り当てます。

   ![chlimage_1-373](assets/chlimage_1-373.png)

## SAML 用のロガーの設定 {#configure-a-logger-for-saml}

SAML の設定ミスに起因する問題をデバッグするために、ロガーを設定できます。 手順は次のとおりです。

1. Web コンソール（*http://localhost:4502/system/console/configMgr*）に移動
1. **Apache Sling Logging Logger Configuration** という名前のエントリを検索してクリックします。
1. 次の設定でロガーを作成します。

   * **ログレベル：** デバッグ
   * **ログファイル：** logs/saml.log
   * **ロガー：** com.adobe.granite.auth.saml
