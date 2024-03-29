---
title: コミュニティサイト
seo-title: Communities Sites
description: AEM Communitiesドキュメントの概要
seo-description: Overview of the AEM Communities documentation
uuid: 9842ce6c-1af8-4b27-b199-07410e797ab2
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.4/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 8799386a-c3b8-43cf-9f71-580ff2a81abc
role: Admin
exl-id: b5d20819-3a3f-4b9e-99a3-e7ae5ae28baf
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '506'
ht-degree: 10%

---

# コミュニティサイト {#communities-sites}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

この節は、AEM Communitiesを管理し、AEM Communitiesの機能に精通しているユーザー向けです。

## 概要 {#overview}

概要と入門チュートリアルについては、次を参照してください。

* [AEM Communities の概要](overview.md)
* [AEM Communities 使用の手引き](getting-started.md)
* [イネーブルメントのための AEM Communities 使用の手引き](getting-started-enablement.md)

## 管理および設定に関するトピック {#administration-and-configuration-topics}

### コミュニティサイトの作成と管理 {#communities-site-creation-and-management}

* コミュニティ [コンソール](consoles.md)

   * [Sites](sites-console.md)

      * [グループ（サブコミュニティ）](groups.md)
   * [モデレート](moderation.md)
   * [メンバーおよびグループ管理](members.md)
   * [実施可能リソース](resources.md)
   * [レポート](reports.md)


* コミュニティ [*ツール*](tools.md):

   * [サイトテンプレート](sites.md)
   * [グループテンプレート](tools-groups.md)
   * [コミュニティ機能](functions.md)
   * [ストレージ設定](srp-config.md)
   * [コンポーネントガイド](components-guide.md)
   * [バッジ](badges.md)


### ユーザー生成コンテンツ {#user-generated-content}

AEM Communitiesの主な機能は、サインインしたサイト訪問者（メンバー）によるユーザー生成コンテンツ (UGC) の生成です。 UGC の使用に関する詳細は、次のとおりです。

* [共通 UGC ストア](working-with-srp.md):UGC の共有ストレージ用の SRP の選択
* [UGC のモデレート](moderate-ugc.md):信頼できるメンバーは、UGC を一括またはコンテキスト内でモデレートできます
* [UGC のタグ付け](tag-ugc.md):機能は、メンバーがコンテンツにタグを付けるのを許可するように設定できます
* [UGC の翻訳](translate-ugc.md):機能は、すべての UGC を翻訳するように設定したり、メンバーが選択した投稿を翻訳することを許可したりできます
* [Analytics 設定](analytics.md):Adobe Analyticsでのメンバーアクティビティに関する様々な指標のレポート作成

### コミュニティメンバー {#community-members}

* [ユーザーとユーザーグループの管理](users.md):権限を持つメンバーを含む、コミュニティメンバーおよびメンバーグループの詳細
* [貢献度の制限](limits.md):新規メンバーによる投稿を制限する能力
* [トンネルサービス](deploy-communities.md#tunnel-service-on-author):パブリッシュ側のメンバーとメンバーグループにオーサー環境からアクセスすることを許可
* [メンバーコンソールとグループコンソール](members.md):パブリッシュ側のメンバーとメンバーグループをオーサー環境から作成および管理できます。
* [ユーザーの同期](sync.md):複数のパブリッシュインスタンス間でメンバーとメンバーグループを同期する場合
* [facebookとTwitterを使用したソーシャルログイン](social-login.md):サイト訪問者が、FacebookまたはTwitterの資格情報を使用してコミュニティメンバーになれる機能
* [スコアとバッジ](implementing-scoring.md):メンバーの役割を識別するために割り当てられるバッジと、コミュニティに参加してメンバーがバッジを獲得するための能力
* [通知](notifications.md):メンバーがフォローしているアクティビティを通知する機能
* [購読](subscriptions.md):メンバーが外部メールを使用してコミュニティとやり取りする機能
* [メッセージ](messaging.md):メンバーが内部メッセージを使用してコミュニティとやり取りする機能

### イネーブルメント機能 {#enablement-features}

* [有効化の設定](enablement.md):イネーブルメント機能を正しくセットアップするために必要な情報
* [Analytics 設定](analytics.md):Communities 機能に対してAdobe Analyticsを有効にするために必要な情報
* [イネーブルメントリソースのタグ付け](tag-resources.md):イネーブルメントカタログの作成に必要

### デプロイメント {#deployment}

デプロイメントセクションには、AEM Communitiesに固有の情報が含まれています。

コミュニティコンテンツを使用する性質は、デプロイメントの構造に影響します。

* [Communities 用の推奨トポロジ](topologies.md)

AEMプラットフォームに最新の Communities リリースをインストールすることが重要です。

* [最新の Communities 機能パック](deploy-communities.md#latestfeaturepack)

その他の Communities 固有の情報 ( 例： [アップグレード](upgrade.md), [Dispatcher](dispatcher.md) および [レプリケーション](deploy-communities.md#replication-agents-on-author).

## 関連するコミュニティドキュメント {#related-communities-documentation}

* 訪問 [コミュニティのデプロイ](deploy-communities.md) を参照して、推奨されるデプロイメントについて確認してください。

* 訪問 [コミュニティの開発](communities.md) ソーシャルコンポーネントフレームワーク (SCF) と、コミュニティのコンポーネントと機能のカスタマイズについて説明します。

* 訪問 [コミュニティコンポーネントのオーサリング](author-communities.md) コミュニティコンポーネントを使用して作成および設定する方法を学ぶには、以下を参照してください。
