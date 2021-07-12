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
role: Admin
exl-id: f4adc53d-6809-4d89-a3dd-5d783e938a63
source-git-commit: 3c050c33a384d586d74bd641f7622989dc1d6b22
workflow-type: tm+mt
source-wordcount: '607'
ht-degree: 45%

---

# AEM Communities のユーザーおよび UGC 管理サービス {#user-and-ugc-management-service-in-aem-communities}

>[!IMPORTANT]
>
>以下の節ではGDPRを例として使用しますが、ここで説明する詳細は、すべてのデータ保護およびプライバシー規制に適用されます。（GDPR、CCPAなど）

AEM Communitiesでは、ユーザープロファイルの管理やユーザー生成コンテンツ(UGC)の一括管理をおこなうためのAPIが標準で提供されています。 **UserUgcManagement**&#x200B;サービスを有効にすると、権限を持つユーザー（コミュニティ管理者とモデレーター）は、ユーザープロファイルを無効にし、特定のユーザーに対してUGCを一括削除または一括書き出しできます。 また、これらのAPIを使用すると、顧客データのコントローラーおよびプロセッサーが、欧州連合の一般データ保護規則(GDPR)や、その他のGDPRに触発されたプライバシー要件に準拠できます。

詳しくは、[アドビプライバシーセンターの GDPR ページ](https://www.adobe.com/jp/privacy/general-data-protection-regulation.html)を参照してください。

>[!NOTE]
>
>[AEM Communities 内の Adobe Analytics](analytics.md) サイトを設定している場合は、収集されたユーザーデータが Adobe Analytics サーバーに送信されます。Adobe Analytics は、ユーザーデータのアクセス、書き出し、削除や、GDPR に準拠するための処理をおこなう API を提供しています。詳しくは、[アクセス要求および削除要求の送信](https://docs.adobe.com/content/help/en/analytics/admin/data-governance/gdpr-submit-access-delete.html)を参照してください。

これらのAPIを使用するには、UserUgcManagementサービスをアクティブ化して`/services/social/ugcmanagement`エンドポイントを有効にする必要があります。 このサービスをアクティブ化するには、[GitHub.com](https://github.com/Adobe-Marketing-Cloud/aem-communities-ugc-migration/tree/main/bundles/communities-ugc-management-servlet)で入手可能な[サンプルサーブレット](https://github.com/Adobe-Marketing-Cloud/aem-communities-ugc-migration/tree/main/bundles/communities-ugc-management-servlet)をインストールします。 次に、次のようなHTTPリクエストを使用して、適切なパラメーターを指定して、コミュニティサイトのパブリッシュインスタンスでエンドポイントをヒットします。

`http://localhost:port/services/social/ugcmanagement?user=<authorizable ID>&operation<getUgc>`

ただし、システム内のユーザープロファイルとユーザー生成コンテンツを管理するための UI（ユーザーインターフェイス）を構築することもできます。

これらの API で実行できる機能を以下に示します。

## ユーザーの UGC の取得 {#retrieve-the-ugc-of-a-user}

`getUserUgc(ResourceResolver resourceResolver, String user, OutputStream outputStream)` は、ユーザーのすべてのUGCをシステムから書き出すのに役立ちます。

* **ユーザー**:ユーザーの認証可能ID。
* **outputStream**：結果は出力ストリームとして返されます。このストリームは、ユーザー生成コンテンツ（JSON ファイル）と（ユーザーがアップロードした画像またはビデオを含む）添付ファイルを含んだ zip ファイルになります。

例えば、コミュニティサイトにログインする際の許可可能 ID として weston.mccall@dodgit.com を使用する、Weston McCall という名前のユーザーの UGC を書き出すには、次のような HTTP GET リクエストを送信します。

`http://localhost:port/services/social/ugcmanagement?user=weston.mccall@dodgit.com&operation=getUgc`

## ユーザーの UGC の削除 {#delete-the-ugc-of-a-user}

**deleteUserUgc(ResourceResolver resourceResolver, String user)** は、ユーザーのすべてのUGCをシステムから削除するのに役立ちます。

* **user**：ユーザーの許可可能 ID。

例えば、認証可能ID weston.mccall@dodgit.comを持つユーザーのUGCをHTTPPOST要求を通じて削除するには、次のパラメーターを使用します。

* user= weston.mccall@dodgit.com
* operation= deleteUgc

### Adobe AnalyticsからのUGCの削除 {#delete-ugc-from-analytics}

Adobe Analyticsからユーザーデータを削除するには、GDPR Analyticsのワークフローに従います。の代わりに、APIはAdobe Analyticsからユーザーデータを削除しません。

AEM Communitiesで使用されるAdobe Analytics変数のマッピングについては、次の画像を参照してください。

![Adobe AnalyticsのAEM communities変数マッピング](assets/Analytics-Communities-Mapping.png)

## ユーザーアカウントの無効化 {#disable-a-user-account}

**deleteUserAccount(ResourceResolver resourceResolver, String user)** は、ユーザーアカウントを無効にするのに役立ちます。

* **user**：ユーザーの許可可能 ID。

>[!NOTE]
>
>あるユーザーを無効化すると、そのユーザーがサーバー上で所有しているユーザー生成コンテンツがすべて削除されます。

例えば、認証可能ID weston.mccall@dodgit.comを持つユーザーのプロファイルをHTTPPOST要求を通じて削除するには、次のパラメーターを使用します。

* user=weston.mccall@dodgit.com
* operation= deleteUser

>[!NOTE]
>
>deleteUserAccount() API では、ユーザープロファイルはシステム内で無効化され、その UGC が削除されるだけです。ただし、システムからユーザープロファイルを削除するには、**CRXDE Lite**&#x200B;に移動します。[https://&lt;server>/crx/de](http://localhost:4502/crx/de)で、ユーザーノードを探して削除します。
