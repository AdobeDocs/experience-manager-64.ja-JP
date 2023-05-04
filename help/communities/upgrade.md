---
title: AEM 6.4 Communities へのアップグレード
seo-title: Upgrading to AEM 6.4 Communities
description: 以前のバージョンからAEM 6.4 Communities にアップグレードする方法
seo-description: How to upgrade from an earlier version to AEM 6.4 Communities
uuid: c6c2846e-38d4-4e99-9038-bfb486afd8b9
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.4/COMMUNITIES
content-type: reference
topic-tags: deploying
discoiquuid: 7aa28e36-6b31-4447-b800-cab2dc78c93c
exl-id: ef622ac3-d96d-48bf-bfb2-61516d9deb5c
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '700'
ht-degree: 4%

---

# AEM 6.4 Communities へのアップグレード {#upgrading-to-aem-communities}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

各サイトのトポロジと機能に応じて、AEM Communities 6.4 にアップグレードする場合、または最新の機能パックをインストールする場合に、次の操作が必要になる場合があります。

この節は、コミュニティに固有で、 [AEM 6.4 へのアップグレード](../../help/sites-deploying/upgrade.md) （プラットフォーム）を使用します。

## AEM 6.1 以降からのアップグレード {#upgrading-from-aem-or-later}

### Solr のインデックス再作成 {#reindex-solr}

MSRP で設定されたデプロイメントに新しい Communities 機能パックをインストールする場合は、次の操作が必要になります。

1. のインストール [最新の機能パック](deploy-communities.md#latestfeaturepack)
2. のインストール [最新の Solr 設定ファイル](msrp.md#upgrading)
3. MSRP のインデックス再作成

   セクションを参照 [MSRP インデックス再作成ツール](msrp.md#msrp-reindex-tool)

### Enablement 2.0 {#enablement}

AEM 6.3 以降、イネーブルメント機能では MySQL にレポート情報が保存されなくなりました。 MySQL 依存関係は、SCORM コンテンツの追跡にのみ存在します。

お問い合わせください [カスタマーケア](https://helpx.adobe.com/jp/marketing-cloud/contact-support.html) を参照してください。

## AEM 6.0 からのアップグレード {#upgrading-from-aem}

既存の UGC を保持する必要がある場合は、その方法は、デプロイメントが UGC を保存したかどうかによって異なります [オンプレミス](#on-premise-storage) または [Adobe雲](#adobe-cloud-storage).

### Adobeクラウドストレージ {#adobe-cloud-storage}

アップグレードされたサイトがAdobeクラウドストレージを使用するように設定されている場合は、SRP メソッドが既存の UGC を古い場所で見つけられないので、すべての UGC が失われたかのように（間違って）表示されることがあります。

したがって、ASRP に対して、 `AEM 6.0 compatability-mode` をクリックして UGC にアクセスします。

すべてのAEM 6.3 オーサーインスタンスとパブリッシュインスタンスの場合：

1. 管理者権限でログインし、設定します。 [ASRP](asrp.md).
1. 既存の UGC を表示するには、次の手順に従います。

   i.Web コンソールを参照します。 デフォルトの URL は、
   `https://localhost:4502/system/console/configMgr`。

   ii.場所 **[!UICONTROL AEM Communities Utilities]** 設定を選択し、設定パネルを展開します。

   iii.オフ **[!UICONTROL クラウドストレージ]** をクリックし、 **[!UICONTROL 保存]**.

![chlimage_1-126](assets/chlimage_1-126.png)

### オンプレミスストレージ {#on-premise-storage}

アップグレードしたサイトがクラウドストレージを使用しなかった場合は、共通ストアをサポートするために、既存の UGC をAEM 6.1 Communities で導入された新しい構造に合わせて変換する必要があります。

そのために、GitHub でオープンソース移行ツールを利用できます。\
[AEM Communities UGC 移行ツール](https://github.com/Adobe-Marketing-Cloud/communities-ugc-migration)

### Java API {#java-apis}

AEM 6.0 ソーシャルコミュニティからAEM 6.3 Communities にアップグレードする場合は、多くの API が異なるパッケージに再編成されていることに注意してください。 コミュニティ機能のカスタマイズに IDE を使用する場合は、ほとんどを簡単に解決できます。

非推奨（廃止予定）の SocialUtils パッケージについて詳しくは、 [SocialUtils リファクタリング](socialutils.md).

関連トピック [コミュニティでの Maven の使用](maven.md).

### JSP コンポーネントテンプレートなし {#no-jsp-component-templates}

この [ソーシャルコンポーネントフレームワーク](scf.md) (SCF) は、 [HandlebarsJS](https://handlebarsjs.com/) AEM 6.0 より前の Java Server Pages(JSP) の代わりに (HBS) テンプレート言語を使用します。

AEM 6.0 では、JSP コンポーネントは新しい HBS フレームワークコンポーネントと同じ場所に残り、HBS コンポーネントは通常、「hbs」という名前のサブフォルダーに配置されます。

AEM 6.1 以降では、JSP コンポーネントは完全に削除されました。 コミュニティの場合は、JSP コンポーネントのすべての使用を SCF コンポーネントに置き換えることをお勧めします。

## AEM Communities UGC 移行ツール {#aem-communities-ugc-migration-tool}

この [AEM Communities UGC 移行ツール](https://github.com/Adobe-Marketing-Cloud/communities-ugc-migration) は、GitHub で利用可能なオープンソース移行ツールで、AEM social communities の以前のバージョンから UGC を書き出してAEM Communities 6.1 以降に読み込むようにカスタマイズできます。

以前のバージョンから UGC を移動する以外に、このツールを使用して UGC を 1 つから移動することもできます [SRP](working-with-srp.md) を別のもの（MSRP から DSRP へなど）に変更する場合に使用します。

## AEM 5.6.1 以前からのアップグレード {#upgrading-from-aem-or-earlier}

概念上、次の 3 世代のコミュニティコンポーネントが存在します。

**第 1 世代**:約 CQ 5.4 ～ AEM 5.6.0 — これらは、 **collab** プラットフォーム間で UGC を同期する手段としてレプリケーションを使用して、ローカルリポジトリに UGC を保存したコンポーネント。 その他の違いとしては、Java Server Pages(JSP) を使用した実装と、オーサー環境でのみオーサリングで構成されるブログ機能があります。

**第 2 世代**:AEM 5.6.1 からAEM 6.1 まで — これは、次の組み合わせです。 **collab** および **social** コンポーネント。 AEM 6.0 では新しい [ソーシャルコンポーネントフレームワーク](scf.md) (SCF) およびAEM 6.2 では、 [共通 UGC ストア](working-with-srp.md) UGC には、 [ストレージリソースプロバイダー](srp.md) (SRP)。

**第 3 世代**:AEM 6.2 以降では、 **social** SCF で Handlebars(HBS) コンポーネントとして実装され、UGC 用の SRP の選択が必要なコンポーネント。
