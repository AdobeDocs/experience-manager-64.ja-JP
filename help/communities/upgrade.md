---
title: AEM 6.4 Communities へのアップグレード
seo-title: AEM 6.4 Communities へのアップグレード
description: 以前のバージョンから AEM 6.4 Communities へアップグレードする方法
seo-description: 以前のバージョンから AEM 6.4 Communities へアップグレードする方法
uuid: c6c2846e-38d4-4e99-9038-bfb486afd8b9
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.4/COMMUNITIES
content-type: reference
topic-tags: deploying
discoiquuid: 7aa28e36-6b31-4447-b800-cab2dc78c93c
translation-type: tm+mt
source-git-commit: 3d2b91565e14e85e9e701663c8d0ded03e5b430c
workflow-type: tm+mt
source-wordcount: '680'
ht-degree: 62%

---


# AEM 6.4 Communities へのアップグレード {#upgrading-to-aem-communities}

各サイトのトポロジや機能に応じて、AEM Communities 6.4 へのアップグレード時または最新の機能パックのインストール時に次のアクションが必要になる場合があります。

このセクションの内容は Communities に特化しており、[AEM 6.4 へのアップグレード](../../help/sites-deploying/upgrade.md)（プラットフォーム）の説明を補足するものです。

## AEM 6.1 以降のバージョンからのアップグレード {#upgrading-from-aem-or-later}

### Solr のインデックス再作成 {#reindex-solr}

MSRPで設定された配置に新しいCommunities機能パックをインストールする場合、次の操作が必要になります。

1. Install the [latest feature pack](deploy-communities.md#latestfeaturepack)
2. Install the [latest Solr config files](msrp.md#upgrading)
3. MSRPの再インデックス

   「 [MSRP再インデックスツール」を参照](msrp.md#msrp-reindex-tool)

### Enablement 2.0 {#enablement}

AEM 6.3 以降、イネーブルメント機能では、MySQL の中にレポート情報が保存されなくなりました。MySQL の依存関係は、SCORM コンテンツの追跡用のみに存在します。

Enablement 1.0 からのコンテンツの移行のサポートについては、[カスタマーケア](https://helpx.adobe.com/jp/marketing-cloud/contact-support.html)にお問い合わせください。

## AEM 6.0 からのアップグレード {#upgrading-from-aem}

If pre-existing UGC needs to be retained, then the means to do so depends on whether the deployment stored UGC [on-premise](#on-premise-storage) or in the [Adobe cloud](#adobe-cloud-storage).

### アドビクラウドストレージ {#adobe-cloud-storage}

アップグレードされたサイトがアドビクラウドストレージを使用するように設定された場合、SRP のメソッドは古い場所にある既存の UGC を見つけることができなくなるので、すべての UGC が失われたかのように（誤って）表示される可能性があります。

Thus, there is the ability to instruct ASRP to use `AEM 6.0 compatability-mode` to access UGC.

AEM 6.3 のすべてのオーサーインスタンスとパブリッシュインスタンスでは、

1. 管理者権限でサインインする
2. Configure [ASRP](asrp.md)
3. 既存のUGCを表示するには、次の手順に従います。
i. 例えば、Webコンソールを参照します。
   [https://&lt;host>:&lt;port>/system/console/configMgr](http://localhost:4502/system/console/configMgr)ii. Locate **[!UICONTROL AEM Communities Utilities]** configuration
iii. 選択して設定パネルを展開します
   * *オフ* **`Cloud Storage`**
   * Select **[!UICONTROL Save]**

![chlimage_1-126](assets/chlimage_1-126.png)

### オンプレミスストレージ {#on-premise-storage}

アップグレードされたサイトでクラウドストレージを使用しなかった場合、既存の UGC は、共通ストアをサポートするために AEM 6.1 Communities で導入された新しい構造に合わせて変換する必要があります。

この目的で、GitHubでオープンソース移行ツールを使用できます。\
[AEM Communities UGC Migration Tool](https://github.com/Adobe-Marketing-Cloud/communities-ugc-migration)

### Java API {#java-apis}

AEM 6.0 Social Communities から AEM 6.3 Communities にアップグレードするときは、多くの API が異なるパッケージに再編成されていることに注意してください。IDEを使用してCommunities機能をカスタマイズする場合、ほとんどの問題を簡単に解決できます。

廃止された SocialUtils パッケージについて詳しくは、[SocialUtils のリファクタリング](socialutils.md)を参照してください。

また、[コミュニティでの Maven の使用](maven.md)も参照してください。

### JSP コンポーネントテンプレートの廃止 {#no-jsp-component-templates}

[ソーシャルコンポーネントフレームワーク](scf.md) (SCF)は、AEM 6.0より前のバージョンで使用されていたJava Server Pages(JSP)の代わりに、 [HandlebarsJS](https://www.handlebarsjs.com/) (HBS)テンプレート言語を使用します。

AEM 6.0 では、JSP コンポーネントは新しい HBS フレームワークコンポーネントと同じ場所に残っています（HBS コンポーネントは通常、「hbs」という名前のサブフォルダーに存在します）。

AEM 6.1 以降では JSP コンポーネントは完全に削除されています。Communitiesの場合、JSPコンポーネントの使用をすべてSCFコンポーネントで置き換えることをお勧めします。

## AEM Communities UGC Migration Tool {#aem-communities-ugc-migration-tool}

[AEM Communities UGC Migration Tool ](https://github.com/Adobe-Marketing-Cloud/communities-ugc-migration)は、GitHub で使用できるオープンソース移行ツールで、以前のバージョンの AEM Social Communities から UGC を書き出して AEM Communities 6.1 以降に読み込むようにカスタマイズできます。

以前のバージョンから UGC を移行するだけでなく、MSRP から DSRP のように [SRP](working-with-srp.md) 間で UGC を移行する際にもこのツールを使用できます。

## AEM 5.6.1 以前のバージョンからのアップグレード {#upgrading-from-aem-or-earlier}

概念的に、コミュニティコンポーネントには 3 つの世代があります。

**第 1 世代**：おおよそ CQ 5.4 から AEM 5.6.0 まで - これらは、プラットフォーム間で UGC を同期する手段としてレプリケーションを使用して UGC をローカルリポジトリに保存した **collab** コンポーネントです。その他の違いとしては、Java Server Pages(JSP)を使用した実装と、作成者環境でのみ作成されるブログ機能があります。

**第 2 世代**：AEM 5.6.1 から AEM 6.1 まで - **collab** コンポーネントと **social** コンポーネントが混在しています。AEM 6.0 introduced the new [social component framework](scf.md) (SCF) and AEM 6.2 introduced a [common UGC store](working-with-srp.md) where UGC is accessed using a [storage resource provider](srp.md) (SRP).

**第3世代**: AEM 6.2以降では、SCFにHandlebars(HBS)コンポーネントとして実装される **social** コンポーネントのみが存在し、UGC用のSRPを選択する必要があります。
