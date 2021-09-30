---
title: AEM 6.4 Communities へのアップグレード
seo-title: Upgrading to AEM 6.4 Communities
description: 以前のバージョンから AEM 6.4 Communities へアップグレードする方法
seo-description: How to upgrade from an earlier version to AEM 6.4 Communities
uuid: c6c2846e-38d4-4e99-9038-bfb486afd8b9
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.4/COMMUNITIES
content-type: reference
topic-tags: deploying
discoiquuid: 7aa28e36-6b31-4447-b800-cab2dc78c93c
exl-id: ef622ac3-d96d-48bf-bfb2-61516d9deb5c
source-git-commit: 0f82e82cf6e09a2734893a98d67ed1a84b1fec5e
workflow-type: tm+mt
source-wordcount: '664'
ht-degree: 62%

---

# AEM 6.4 Communities へのアップグレード {#upgrading-to-aem-communities}

各サイトのトポロジや機能に応じて、AEM Communities 6.4 へのアップグレード時または最新の機能パックのインストール時に次のアクションが必要になる場合があります。

このセクションの内容は Communities に特化しており、[AEM 6.4 へのアップグレード](../../help/sites-deploying/upgrade.md)（プラットフォーム）の説明を補足するものです。

## AEM 6.1 以降のバージョンからのアップグレード {#upgrading-from-aem-or-later}

### Solr のインデックス再作成 {#reindex-solr}

MSRP を使用して設定したデプロイメントに新しい Communities 機能パックをインストールする場合は、次の操作が必要です。

1. [ 最新の機能パック ](deploy-communities.md#latestfeaturepack) をインストールします。
2. [ 最新の Solr 設定ファイル ](msrp.md#upgrading) をインストールします。
3. MSRP のインデックス再作成

   [MSRP インデックス再作成ツール ](msrp.md#msrp-reindex-tool) を参照してください。

### Enablement 2.0 {#enablement}

AEM 6.3 以降、イネーブルメント機能では、MySQL の中にレポート情報が保存されなくなりました。MySQL の依存関係は、SCORM コンテンツの追跡用のみに存在します。

Enablement 1.0 からのコンテンツの移行のサポートについては、[カスタマーケア](https://helpx.adobe.com/jp/marketing-cloud/contact-support.html)にお問い合わせください。

## AEM 6.0 からのアップグレード {#upgrading-from-aem}

既存の UGC を保持する必要がある場合は、UGC [ オンプレミス ](#on-premise-storage) と [Adobeクラウド ](#adobe-cloud-storage) のどちらにデプロイメントが保存されているかによって、保存方法が異なります。

### アドビクラウドストレージ {#adobe-cloud-storage}

アップグレードされたサイトがアドビクラウドストレージを使用するように設定された場合、SRP のメソッドは古い場所にある既存の UGC を見つけることができなくなるので、すべての UGC が失われたかのように（誤って）表示される可能性があります。

したがって、ASRP に `AEM 6.0 compatability-mode` を使用して UGC にアクセスするように指示する機能があります。

AEM 6.3 のすべてのオーサーインスタンスとパブリッシュインスタンスについて:

1. 管理者権限でログインし、[ASRP](asrp.md) を設定します。
1. 次の手順に従って、既存の UGC を表示します。

   i.Web コンソールを参照します。 デフォルトの URL は、
   `https://localhost:4502/system/console/configMgr`。

   ii.**[!UICONTROL AEM Communities Utilities]** 設定を探し、を選択して設定パネルを展開します。

   iii.「**[!UICONTROL クラウドストレージ]**」をオフにし、「**[!UICONTROL 保存]**」をクリックします。

![chlimage_1-126](assets/chlimage_1-126.png)

### オンプレミスストレージ {#on-premise-storage}

アップグレードされたサイトでクラウドストレージを使用しなかった場合、既存の UGC は、共通ストアをサポートするために AEM 6.1 Communities で導入された新しい構造に合わせて変換する必要があります。

そのために、GitHub でオープンソース移行ツールを利用できます。\
[AEM Communities UGC Migration Tool](https://github.com/Adobe-Marketing-Cloud/communities-ugc-migration)

### Java API {#java-apis}

AEM 6.0 Social Communities から AEM 6.3 Communities にアップグレードするときは、多くの API が異なるパッケージに再編成されていることに注意してください。IDE を使用して Communities 機能をカスタマイズする場合は、ほとんどを簡単に解決できます。

廃止された SocialUtils パッケージについて詳しくは、[SocialUtils のリファクタリング](socialutils.md)を参照してください。

また、[コミュニティでの Maven の使用](maven.md)も参照してください。

### JSP コンポーネントテンプレートの廃止 {#no-jsp-component-templates}

[ ソーシャルコンポーネントフレームワーク ](scf.md)(SCF) は、AEM 6.0 より前の Java Server Pages(JSP) の代わりに、[HandlebarsJS](https://handlebarsjs.com/)(HBS) テンプレート言語を使用します。

AEM 6.0 では、JSP コンポーネントは新しい HBS フレームワークコンポーネントと同じ場所に残っています（HBS コンポーネントは通常、「hbs」という名前のサブフォルダーに存在します）。

AEM 6.1 以降では JSP コンポーネントは完全に削除されています。Communities の場合は、JSP コンポーネントの使用をすべて SCF コンポーネントで置き換えることをお勧めします。

## AEM Communities UGC Migration Tool {#aem-communities-ugc-migration-tool}

[AEM Communities UGC Migration Tool ](https://github.com/Adobe-Marketing-Cloud/communities-ugc-migration)は、GitHub で使用できるオープンソース移行ツールで、以前のバージョンの AEM Social Communities から UGC を書き出して AEM Communities 6.1 以降に読み込むようにカスタマイズできます。

以前のバージョンから UGC を移行するだけでなく、MSRP から DSRP のように [SRP](working-with-srp.md) 間で UGC を移行する際にもこのツールを使用できます。

## AEM 5.6.1 以前のバージョンからのアップグレード {#upgrading-from-aem-or-earlier}

概念的に、コミュニティコンポーネントには 3 つの世代があります。

**第 1 世代**：おおよそ CQ 5.4 から AEM 5.6.0 まで - これらは、プラットフォーム間で UGC を同期する手段としてレプリケーションを使用して UGC をローカルリポジトリに保存した **collab** コンポーネントです。その他の違いとしては、Java Server Pages(JSP) を使用した実装と、オーサー環境でのみオーサリングで構成されるブログ機能があります。

**第 2 世代**：AEM 5.6.1 から AEM 6.1 まで - **collab** コンポーネントと **social** コンポーネントが混在しています。AEM 6.0 では新しい [ ソーシャルコンポーネントフレームワーク ](scf.md)(SCF) が導入され、AEM 6.2 では [ 共通の UGC ストア ](working-with-srp.md) が導入されました。ここでは、[ ストレージリソースプロバイダー ](srp.md)(SRP) を使用して UGC にアクセスします。

**第 3 世代**:AEM 6.2 以降では、SCF に Handlebars(HBS) コンポーネントとして実装さ **** れ、UGC 用の SRP の選択が必要な socialcomponents のみが存在します。
