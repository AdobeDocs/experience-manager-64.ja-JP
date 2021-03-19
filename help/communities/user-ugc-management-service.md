---
title: AEM Communities のユーザーおよび UGC 管理サービス
seo-title: AEM Communities のユーザーおよび UGC 管理サービス
description: 'API を使用すると、ユーザー生成コンテンツの一括削除や一括書き出しをおこなったり、ユーザーアカウントを無効化したりできます。 '
seo-description: 'API を使用すると、ユーザー生成コンテンツの一括削除や一括書き出しをおこなったり、ユーザーアカウントを無効化したりできます。 '
uuid: f4663825-eac8-4ef5-8253-46875e0cd71d
contentOwner: mgulati
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/COMMUNITIES
topic-tags: administering
discoiquuid: f564759f-fb56-4f70-a7b1-286a223755c6
role: Administrator
translation-type: tm+mt
source-git-commit: 75312539136bb53cf1db1de03fc0f9a1dca49791
workflow-type: tm+mt
source-wordcount: '608'
ht-degree: 45%

---


# AEM Communities のユーザーおよび UGC 管理サービス {#user-and-ugc-management-service-in-aem-communities}

>[!IMPORTANT]
>
>以下の節ではGDPRを例に挙げていますが、詳細はデータ保護とプライバシーに関するすべての規制に適用されます。GDPR、CCPAなど

AEM CommunitiesはAPIを標準搭載で公開しており、ユーザープロファイルを管理し、ユーザー生成コンテンツ(UGC)を一括管理できます。 **UserUgcManagement**&#x200B;サービスを有効にすると、管理者ユーザー（コミュニティ管理者とモデレーター）はユーザープロファイルを無効にし、特定のユーザーに対してUGCを一括削除または一括エクスポートできます。 また、これらのAPIを使用すると、顧客データのコントローラとプロセッサが、欧州和集合のGDPR(General Data Protection Regulations)や、他のGDPRに基づくプライバシー要件に準拠できます。

詳しくは、[アドビプライバシーセンターの GDPR ページ](https://www.adobe.com/jp/privacy/general-data-protection-regulation.html)を参照してください。

>[!NOTE]
>
>[AEM Communities 内の Adobe Analytics](analytics.md) サイトを設定している場合は、収集されたユーザーデータが Adobe Analytics サーバーに送信されます。Adobe Analytics は、ユーザーデータのアクセス、書き出し、削除や、GDPR に準拠するための処理をおこなう API を提供しています。詳しくは、[アクセス要求および削除要求の送信](https://docs.adobe.com/content/help/en/analytics/admin/data-governance/gdpr-submit-access-delete.html)を参照してください。

これらのAPIを使用するには、UserUgcManagementサービスをアクティブ化して`/services/social/ugcmanagement`エンドポイントを有効にする必要があります。 このサービスをアクティブ化するには、[GitHub.com](https://github.com/Adobe-Marketing-Cloud/aem-communities-ugc-migration/tree/main/bundles/communities-ugc-management-servlet)で利用可能な[サンプルサーブレット](https://github.com/Adobe-Marketing-Cloud/aem-communities-ugc-migration/tree/main/bundles/communities-ugc-management-servlet)をインストールします。 次に、次のようなhttpリクエストを使用して、適切なパラメーターを指定して、コミュニティサイトの発行インスタンスでエンドポイントに到達します。

`http://localhost:port/services/social/ugcmanagement?user=<authorizable ID>&operation<getUgc>`

ただし、システム内のユーザープロファイルとユーザー生成コンテンツを管理するための UI（ユーザーインターフェイス）を構築することもできます。

これらの API で実行できる機能を以下に示します。

## ユーザーの UGC の取得  {#retrieve-the-ugc-of-a-user}

`getUserUgc(ResourceResolver resourceResolver, String user, OutputStream outputStream)` ユーザーのすべてのUGCをシステムから書き出すのに役立ちます。

* **user**:認証可能なユーザーID。
* **outputStream**：結果は出力ストリームとして返されます。このストリームは、ユーザー生成コンテンツ（JSON ファイル）と（ユーザーがアップロードした画像またはビデオを含む）添付ファイルを含んだ zip ファイルになります。

例えば、コミュニティサイトにログインする際の許可可能 ID として weston.mccall@dodgit.com を使用する、Weston McCall という名前のユーザーの UGC を書き出すには、次のような HTTP GET リクエストを送信します。

`http://localhost:port/services/social/ugcmanagement?user=weston.mccall@dodgit.com&operation=getUgc`

## ユーザーの UGC の削除 {#delete-the-ugc-of-a-user}

**deleteUserUgc(ResourceResolver resourceResolver, String user)** は、ユーザーのすべてのUGCをシステムから削除するのに役立ちます。

* **user**：ユーザーの許可可能 ID。

例えば、認証可能なID weston.mccall@dodgit.comを持つユーザーのUGCをhttpPOSTリクエストで削除するには、次のパラメーターを使用します。

* user= weston.mccall@dodgit.com
* operation= deleteUgc

### UGCをAdobe Analyticsから削除{#delete-ugc-from-analytics}

ユーザーデータをAdobe Analyticsから削除するには、GDPR Analyticsのワークフローに従います。を使用しない場合、APIはAdobe Analyticsからユーザーデータを削除しません。

AEM Communitiesが使用するAdobe Analytics変数マッピングについては、次の図を参照してください。

![AEM communitiesのAdobe Analytics変数マッピング](assets/Analytics-Communities-Mapping.png)

## ユーザーアカウントの無効化 {#disable-a-user-account}

**deleteUserAccount(ResourceResolver resourceResolver, String user)は、ユーザーアカウントを無効にする** のに役立ちます。

* **user**：ユーザーの許可可能 ID。

>[!NOTE]
>
>あるユーザーを無効化すると、そのユーザーがサーバー上で所有しているユーザー生成コンテンツがすべて削除されます。

例えば、httpPOSTリクエストを使用して認証可能なID weston.mccall@dodgit.comを持つユーザーのプロファイルを削除するには、次のパラメーターを使用します。

* user=weston.mccall@dodgit.com
* operation= deleteUser

>[!NOTE]
>
>deleteUserAccount() API では、ユーザープロファイルはシステム内で無効化され、その UGC が削除されるだけです。ただし、ユーザープロファイルをシステムから削除するには、**CRXDE Lite**&#x200B;に移動します。[https://&lt;server>/crx/de](http://localhost:4502/crx/de)を開き、ユーザーノードを探して削除します。
