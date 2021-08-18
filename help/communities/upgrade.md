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
exl-id: ef622ac3-d96d-48bf-bfb2-61516d9deb5c
source-git-commit: a70f874ad7fcae59ee4c6ec20e23ffb2e339590b
workflow-type: tm+mt
source-wordcount: '680'
ht-degree: 62%

---

# AEM 6.4 Communities へのアップグレード {#upgrading-to-aem-communities}

各サイトのトポロジや機能に応じて、AEM Communities 6.4 へのアップグレード時または最新の機能パックのインストール時に次のアクションが必要になる場合があります。

このセクションの内容は Communities に特化しており、[AEM 6.4 へのアップグレード](../../help/sites-deploying/upgrade.md)（プラットフォーム）の説明を補足するものです。

## AEM 6.1 以降のバージョンからのアップグレード {#upgrading-from-aem-or-later}

### Solr のインデックス再作成 {#reindex-solr}

MSRPを使用して設定されたデプロイメントに新しいCommunities機能パックをインストールする場合は、次の操作が必要です。

1. [最新の機能パック](deploy-communities.md#latestfeaturepack)をインストールします。
2. [最新のSolr設定ファイル](msrp.md#upgrading)をインストールします。
3. MSRPの再インデックス

   [MSRPインデックス再作成ツール](msrp.md#msrp-reindex-tool)を参照してください。

### Enablement 2.0 {#enablement}

AEM 6.3 以降、イネーブルメント機能では、MySQL の中にレポート情報が保存されなくなりました。MySQL の依存関係は、SCORM コンテンツの追跡用のみに存在します。

Enablement 1.0 からのコンテンツの移行のサポートについては、[カスタマーケア](https://helpx.adobe.com/jp/marketing-cloud/contact-support.html)にお問い合わせください。

## AEM 6.0 からのアップグレード {#upgrading-from-aem}

既存のUGCを保持する必要がある場合は、デプロイメントがUGC [オンプレミス](#on-premise-storage)と[Adobeクラウド](#adobe-cloud-storage)のどちらに保存したかによって、保存方法が異なります。

### アドビクラウドストレージ {#adobe-cloud-storage}

アップグレードされたサイトがアドビクラウドストレージを使用するように設定された場合、SRP のメソッドは古い場所にある既存の UGC を見つけることができなくなるので、すべての UGC が失われたかのように（誤って）表示される可能性があります。

したがって、ASRPに`AEM 6.0 compatability-mode`を使用してUGCにアクセスするよう指示する機能があります。

AEM 6.3 のすべてのオーサーインスタンスとパブリッシュインスタンスでは、

1. 管理者権限でログイン
2. [ASRP](asrp.md)を設定
3. 既存のUGCを表示するには、次の手順に従います。
i.Webコンソールを参照します（例： ）。
   [https://&lt;host>:&lt;port>/system/console/](http://localhost:4502/system/console/configMgr)
configMgrii**[!UICONTROL AEM Communities Utilities]**設定を見つけます。
三 「 」を選択して設定パネルを展開します。
   * *オフ* **`Cloud Storage`**
   * 「**[!UICONTROL 保存]**」を選択します。

![chlimage_1-126](assets/chlimage_1-126.png)

### オンプレミスストレージ {#on-premise-storage}

アップグレードされたサイトでクラウドストレージを使用しなかった場合、既存の UGC は、共通ストアをサポートするために AEM 6.1 Communities で導入された新しい構造に合わせて変換する必要があります。

この目的で、オープンソース移行ツールをGitHubで使用できます。\
[AEM Communities UGC Migration Tool](https://github.com/Adobe-Marketing-Cloud/communities-ugc-migration)

### Java API {#java-apis}

AEM 6.0 Social Communities から AEM 6.3 Communities にアップグレードするときは、多くの API が異なるパッケージに再編成されていることに注意してください。Communities機能のカスタマイズにIDEを使用する場合は、ほとんどの問題を簡単に解決できます。

廃止された SocialUtils パッケージについて詳しくは、[SocialUtils のリファクタリング](socialutils.md)を参照してください。

また、[コミュニティでの Maven の使用](maven.md)も参照してください。

### JSP コンポーネントテンプレートの廃止 {#no-jsp-component-templates}

[ソーシャルコンポーネントフレームワーク](scf.md)(SCF)は、AEM 6.0より前に使用されていたJava Server Pages(JSP)の代わりに、[HandlebarsJS](https://handlebarsjs.com/)(HBS)テンプレート言語を使用します。

AEM 6.0 では、JSP コンポーネントは新しい HBS フレームワークコンポーネントと同じ場所に残っています（HBS コンポーネントは通常、「hbs」という名前のサブフォルダーに存在します）。

AEM 6.1 以降では JSP コンポーネントは完全に削除されています。コミュニティの場合は、JSPコンポーネントの使用をすべてSCFコンポーネントで置き換えることをお勧めします。

## AEM Communities UGC Migration Tool {#aem-communities-ugc-migration-tool}

[AEM Communities UGC Migration Tool ](https://github.com/Adobe-Marketing-Cloud/communities-ugc-migration)は、GitHub で使用できるオープンソース移行ツールで、以前のバージョンの AEM Social Communities から UGC を書き出して AEM Communities 6.1 以降に読み込むようにカスタマイズできます。

以前のバージョンから UGC を移行するだけでなく、MSRP から DSRP のように [SRP](working-with-srp.md) 間で UGC を移行する際にもこのツールを使用できます。

## AEM 5.6.1 以前のバージョンからのアップグレード {#upgrading-from-aem-or-earlier}

概念的に、コミュニティコンポーネントには 3 つの世代があります。

**第 1 世代**：おおよそ CQ 5.4 から AEM 5.6.0 まで - これらは、プラットフォーム間で UGC を同期する手段としてレプリケーションを使用して UGC をローカルリポジトリに保存した **collab** コンポーネントです。その他の違いは、Java Server Pages(JSP)を使用した実装と、オーサー環境でのみオーサリングで構成されるブログ機能です。

**第 2 世代**：AEM 5.6.1 から AEM 6.1 まで - **collab** コンポーネントと **social** コンポーネントが混在しています。AEM 6.0では新しい[ソーシャルコンポーネントフレームワーク](scf.md)(SCF)が導入され、AEM 6.2では[共通のUGCストア](working-with-srp.md)が導入されました。このストアでは、[ストレージリソースプロバイダー](srp.md)(SRP)を使用してUGCにアクセスします。

**第3世代**:AEM 6.2以降では、SCFにHandlebars(HBS)コンポーネン **** トとして実装され、UGC用のSRPの選択が必要なソーシャルコンポーネントのみが存在します。
