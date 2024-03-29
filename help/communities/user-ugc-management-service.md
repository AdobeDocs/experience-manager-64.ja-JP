---
title: AEM Communities のユーザーおよび UGC 管理サービス
seo-title: User and UGC Management Service in AEM Communities
description: API を使用して、ユーザー生成コンテンツの一括削除および一括書き出し、ユーザーアカウントの無効化をおこないます。
seo-description: Use APIs to bulk delete and bulk export user generated content, and disable user account.
uuid: f4663825-eac8-4ef5-8253-46875e0cd71d
contentOwner: mgulati
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/COMMUNITIES
topic-tags: administering
discoiquuid: f564759f-fb56-4f70-a7b1-286a223755c6
role: Admin
exl-id: f4adc53d-6809-4d89-a3dd-5d783e938a63
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '618'
ht-degree: 9%

---

# AEM Communities のユーザーおよび UGC 管理サービス {#user-and-ugc-management-service-in-aem-communities}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

>[!IMPORTANT]
>
>以下の節では GDPR を例として使用していますが、詳細はすべてのデータ保護およびプライバシー規制（GDPR、CCPA など）に適用できます。

AEM Communitiesでは、ユーザープロファイルの管理やユーザー生成コンテンツ (UGC) の一括管理をおこなうための API を標準で提供しています。 有効にすると、 **UserUgcManagement** サービスを使用すると、権限を持つユーザー（コミュニティ管理者とモデレーター）がユーザープロファイルを無効にしたり、特定のユーザーに対して UGC を一括削除または一括書き出ししたりできます。 また、これらの API を使用すると、顧客データの管理者やプロセッサーが、欧州連合の一般データ保護規則 (GDPR) や、GDPR に基づくその他の GDPR に触発されたプライバシー要件に準拠できます。

詳しくは、 [GDPR ページ (Adobeプライバシーセンター )](https://www.adobe.com/jp/privacy/general-data-protection-regulation.html).

>[!NOTE]
>
>設定済みの場合 [AEM CommunitiesのAdobe Analytics](analytics.md) サイトに保存すると、取得したユーザーデータがAdobe Analyticsサーバーに送信されます。 Adobe Analyticsには、ユーザーデータのアクセス、書き出し、削除を可能にし、GDPR に準拠する API が用意されています。 詳しくは、 [アクセス要求および削除要求の送信](https://experienceleague.adobe.com/docs/analytics/admin/data-governance/gdpr-submit-access-delete.html).

これらの API を使用するには、 `/services/social/ugcmanagement` UserUgcManagement サービスをアクティブ化してエンドポイントを作成します。 このサービスをアクティブ化するには、 [サンプルサーブレット](https://github.com/Adobe-Marketing-Cloud/aem-communities-ugc-migration/tree/main/bundles/communities-ugc-management-servlet) 次で利用可能： [GitHub.com](https://github.com/Adobe-Marketing-Cloud/aem-communities-ugc-migration/tree/main/bundles/communities-ugc-management-servlet). 次に、次のような http リクエストを使用して、適切なパラメーターを指定して、コミュニティサイトのパブリッシュインスタンス上のエンドポイントをヒットします。

`http://localhost:port/services/social/ugcmanagement?user=<authorizable ID>&operation<getUgc>`

ただし、UI（ユーザーインターフェイス）を構築して、システム内のユーザープロファイルとユーザー生成コンテンツを管理することもできます。

これらの API を使用して、次の機能を実行できます。

## ユーザーの UGC の取得 {#retrieve-the-ugc-of-a-user}

`getUserUgc(ResourceResolver resourceResolver, String user, OutputStream outputStream)` は、ユーザーのすべての UGC をシステムから書き出すのに役立ちます。

* **ユーザー**:ユーザーの認証可能 ID。
* **outputStream**:結果は出力ストリームとして返されます。これは、ユーザーが生成したコンテンツ（json ファイル）と添付ファイル（ユーザーがアップロードした画像やビデオを含む）を含む zip ファイルです。

例えば、コミュニティサイトにログインする際に許可可能 ID としてweston.mccall@dodgit.comを使用する Weston McCall という名前のユーザーの UGC を書き出すには、次のような httpGETリクエストを送信します。

`http://localhost:port/services/social/ugcmanagement?user=weston.mccall@dodgit.com&operation=getUgc`

## ユーザーの UGC を削除 {#delete-the-ugc-of-a-user}

**deleteUserUgc(ResourceResolver resourceResolver, String user)** は、ユーザーのすべての UGC をシステムから削除するのに役立ちます。

* **ユーザー**:ユーザーの認証可能 ID。

例えば、許可可能 ID weston.mccall@dodgit.comを持つユーザーの UGC を http-Delect 要求を通じてPOSTするには、次のパラメーターを使用します。

* user=weston.mccall@dodgit.com
* operation= deleteUgc

### Adobe Analyticsから UGC を削除 {#delete-ugc-from-analytics}

Adobe Analyticsからユーザーデータを削除するには、GDPR Analytics ワークフローに従います。の場合、API はAdobe Analyticsからユーザーデータを削除しません。

AEM Communitiesで使用されるAdobe Analytics変数のマッピングについては、次の画像を参照してください。

![Adobe AnalyticsでのAEM communities 変数マッピング](assets/Analytics-Communities-Mapping.png)

## ユーザーアカウントの無効化 {#disable-a-user-account}

**deleteUserAccount(ResourceResolver resourceResolver, String user)** は、ユーザーアカウントを無効にするのに役立ちます。

* **ユーザー**:ユーザーの認証可能 ID。

>[!NOTE]
>
>ユーザーを無効にすると、ユーザーがサーバー上に持っているユーザー生成コンテンツがすべて削除されます。

例えば、許可可能 ID weston.mccall@dodgit.comを持つユーザーのプロファイルを http-unlect 要求を通じてPOSTするには、次のパラメーターを使用します。

* user=weston.mccall@dodgit.com
* operation= deleteUser

>[!NOTE]
>
>deleteUserAccount() API は、システム内のユーザープロファイルを無効にし、UGC を削除するだけです。 ただし、ユーザープロファイルをシステムから削除する場合は、 **CRXDE Lite**: [https://&lt;server>/crx/de](http://localhost:4502/crx/de)の上にマウスポインターを置いて、ユーザーノードを探して削除します。
