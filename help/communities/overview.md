---
title: AEM Communities の概要
seo-title: AEM Communities の概要
description: AEM Communities の機能とセットアップの概要
seo-description: AEM Communities の機能とセットアップの概要
uuid: 6e3ac9d2-ca31-40ea-8cab-b8451074c498
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.4/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 418cc919-0ae3-4c6c-8566-7e9a206f02a8
translation-type: tm+mt
source-git-commit: 63001012f0d865c2548703ea387c780679128ee7
workflow-type: tm+mt
source-wordcount: '1429'
ht-degree: 42%

---


# AEM Communities の概要 {#aem-communities-overview}

Adobe Experience Manager（AEM）Communities では、高いパフォーマンスと優れたサイト管理機能を持つオンプレミスのコミュニティサイトを素早く作成し、サイト訪問者を価値あるコミュニティメンバーに転換できます。

AEM Communities のライセンス、イネーブルメント機能の追加ライセンスおよび Adobe Analytics に関する情報については、アカウント担当者にお問い合わせください。

## Communities の機能 {#communities-features}

AEM Communitiesは、ブログ、Q&amp;A、イベントカレンダーを通じて情報を伝えるサイト訪問者との関係を発展させると同時に、フォーラム、コメント、その他のコミュニティコンテンツ(UGC)を通して洞察を得ることができます。

さらに AEM Communities では、パブリッシュ環境での信頼されたメンバーによるモデレートや、Twitter および Facebook のソーシャルログイン、コミュニティコンテンツのインライン翻訳、公開済みコミュニティサイトでのコミュニティグループの作成、バッジ授与のためのスコア付け、ファイル共有、通知およびアクティビティストリームを実現できます。

Communities の機能は、GitHub.com で公開されている [AEM Demo Machine](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki)で試すことができます。また、新しい We.Retail のリファレンス実装内でも試すことができます。

## コミュニティサイト {#community-sites}

コミュニティサイトは、シンプルなウィザードで作成できる AEM サイトです。作成される Web サイトには、数多くの一般的な機能があらかじめ組み込まれています。

The [site creation wizard](sites-console.md):

* Assembles features of the site, based on the selected [community site template](sites.md) which is
   * Built from [community functions](#community-functions)
   * Optional [community groups](#communitygroups) feature
* 次の設定を行います。
   * モデレート
   * ログイン
   * 翻訳
* 重要な機能を提供します。
   * Responsive design: Uses [Twitter Bootstrap themes](https://getbootstrap.com)
   * Login: Self-registration, [social login](social-login.md), user profiles
   * 通知： 会員は、会員に関連のあるイベントを見る
   * メッセージ： コミュニティサイト内のメンバーは、メッセージを送信または受信できます。
   * 検索： コミュニティサイト内の検索機能
   * Language switching: Ability to select a language for a [multillingual site](../../help/sites-administering/translation.md)
   * 管理： コミュニティサイト内のユーザーのモデレートと管理を許可されたメンバーが行うアクセス
* ページレベルのオーサリング手順を多数排除します。
   * ブランディング： コミュニティサイトのすべてのページに表示するバナー画像のアップロード（オプション）
   * ナビゲーションメニュー： コミュニティサイトテンプレートに含まれる機能に対しては、ナビゲーションリンクが提供されます。

To experience the ease of quickly creating a new community site, visit [Getting Started with AEM Communities](getting-started.md).

## コミュニティコンテンツの永続性 {#community-content-persistence}

AEM Communities でコミュニティコンテンツのパフォーマンスと同期を改善するには、ユーザー生成コンテンツ（UGC）専用の共通ストアを用意し、それをすべての AEM インスタンス（オーサーおよびパブリッシュ）で共有することが必要です。

コミュニティコンテンツは、ストレージリソースプロバイダー（SRP）を介して簡単にアクセスできます。SRP はアクセスを基本トポロジから切り離すレイヤーを提供し、UGC の共通ストアをサポートします。

コミュニティコンテンツの永続性と推奨されるデプロイメントについて詳しくは、次のページを参照してください。

* [コミュニティコンテンツのストレージ](working-with-srp.md)：UGC のために利用できる SRP ストレージオプションについて説明します。
* [推奨トポロジ](topologies.md)：ユースケースと SRP の選択に応じたトポロジについて説明します。
* [AEM Communities 6.3 へのアップグレード](upgrade.md)：AEM 6.3 に移行する際に役立つ UGC に関する情報を示します。

## コミュニティコンソール {#communities-consoles}

In the author environment, the global navigation console provides access to the [Communities console](consoles.md), which contains:

* [サイト](sites-console.md)コンソール

   * サイトの作成
   * サイトの編集
   * サイト管理
   * [コミュニティグループ](groups.md)コンソール

* [モデレート](moderation.md)コンソール

   * 作成者および発行環境向けの共通一括モデレートUI
   * 新しいフィルター条件

* [メンバーおよびグループ](members.md)管理コンソール

   * 作成者環境から発行側ユーザー（メンバー）を作成および管理する機能を提供します。
   * メンバーの禁止機能を提供
   * 作成者環境から、発行側のユーザーグループ（メンバーグループ）を作成および管理できます。

* [レポート](reports.md)コンソール

   * 割り当て、投稿、表示に関するレポートを生成できます。

* [リソース](resources.md)コンソール

   * イネーブルメントリソースと学習パスの作成機能を提供
   * 有効化リソースと学習パスに関するレポートにアクセスできます。

グローバルツールコンソールから次のコミュニティツールにアクセスできます。

* [サイトテンプレート](tools.md#sitetemplatesconsole)コンソール

   * コミュニティサイトテンプレートの作成と管理

* [グループテンプレート](tools.md#grouptemplatesconsole)コンソール

   * コミュニティグループテンプレートの作成と管理

* [コミュニティ機能](tools.md#communityfunctionsconsole)コンソール

   * コミュニティ機能の作成と管理

* [ストレージ設定](tools.md#storageconfiguratonconsole)コンソール

   * Select and configure the [common store](working-with-srp.md) for the site

* [コンポーネントガイド](components-guide.md)

   * A sample site, [Community Components](http://localhost:4502/editor.html/content/community-components/en.html), that provides a sample of all Communities components with their default configuration and the ability to experiment with them

## コミュニティサイトテンプレート {#community-site-templates}

コミュニティサイトの作成は、どのサンプルサイトにも依存しないコミュニティサイトを迅速に設定するために、コミュニティサイトテンプレートの選択に基づいて行われます。

コミュニティ機能とコミュニティグループテンプレートで構成されるコミュニティサイトテンプレートは、ログイン、ユーザプロファイル、メッセージング、サイトメニュー、検索、テーマ設定、ブランディング機能など、コミュニティサイトの構造を提供します。

[サイトテンプレートコンソール](sites.md)を参照してください。

## コミュニティ機能 {#community-functions}

コミュニティに必要とされる機能はだいたい決まっています。AEM Communities では、こうした機能が基本要素として用意されており、「コミュニティ機能」と呼ばれています。

コミュニティ機能とは、様々なコンポーネントを組み合わせて 1 つの機能にまとめ、コミュニティサイトテンプレートに簡単に組み込める形にした通常の AEM ページです。

[コミュニティ機能コンソール](functions.md)を参照してください。

## コミュニティグループとグループテンプレート {#community-groups-and-group-templates}

コミュニティグループ機能は、サブコミュニティを作成者と発行環境の両方から許可されたユーザーおよびコミュニティメンバーがコミュニティサイト内で動的に作成する機能です。

From the author environment, community groups (sub-communities) may be created within an existing community site or nested within an existing group, when the structure of the template contains the [Groups function](functions.md#groups-function).

コミュニティグループを作成するには、コミュニティグループページのデザインを提供するコミュニティグループテンプレートを選択する必要があります。 テンプレート構造にGroups機能を追加すると、1つのグループテンプレートを指定するか、新しいコミュニティグループを作成する際に選択したテンプレートを指定するように設定されます。

関連トピック：

* [サイトグループコンソール](groups.md) — 作成者環境でのサブコミュニティの作成
* [グループテンプレートコンソール](tools-groups.md) — グループのサイト構造の作成
* [はじめに —AEM Communities](getting-started.md) — ネストグループを含むコミュニティサイトをすばやく作成するためのチュートリアル

## コミュニティコンポーネント {#community-components}

コミュニティサイトの構成要素である[コミュニティコンポーネント](author-communities.md)は、AEM サイトに Communities 機能を追加するために使用します。

[コミュニティコンポーネントガイド](components-guide.md)では、これらのコンポーネントをインタラクティブに検討できます。

## コミュニティのタイプ {#types-of-communities}

### Engagement Community {#engagement-community}

エンゲージメントコミュニティは、コミュニティのメンバーとしての顧客の情報提供、フィードバックの要請、顧客の対話を可能にする顧客の関与に重点を置いたコミュニティサイトです。

エンゲージメントコミュニティの機能には次のものがあります。

* ログイン
* メッセージ
* フォーラム
* コメント
* レビュー
* 評価
* 投票
* ブログ
* グループ
* カレンダー
* 翻訳
* モデレート
* 通知
* スコアリングとバッジ
* 解析レポート

To experience the ease of quickly creating a new engagement community, visit [Getting Started with AEM Communities](getting-started.md).

### イネーブルメントコミュニティ {#enablement-community}

イネーブルメントコミュニティは、オンライン学習機能を用意したコミュニティサイトです。

有効化コミュニティの機能には、次のものがあります。

* All the features of an [engagement community](#engagement-community)
* メンバーおよびメンバーグループにコンテンツおよび学習リソースを割り当てる機能
* クイズやテストなど、SCORMコンテンツをサポート
* 割り当て完了の追跡
* レポートと解析へのアクセス
* フォーラム、メッセージ、コメントおよび評価を通じて、学習リソースに関する会話を行う機能

An enablement community may be created when the [Enablement add-on is configured](enablement.md), which requires additional licensing for use in a production environment. An enablement community site will include the [assignments function](#community-functions).

To experience the ease of creating a new enablement community, visit [Getting Started with AEM Communities for Enablement](getting-started-enablement.md).

## AEM Demo Machine {#aem-demo-machine}

[AEM Demo Machineは、AEM](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine) Sites [, Assets](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Sites), Communities [, Communities, Communities Apps, Communities Apps, Apps Apps, Apps Appsは、QuickStartインスタンスを起動するよりもセットアップが必要な場合が多い、Forms Sites](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Assets)[](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Communities)[](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Apps)[](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Forms)Assets, Cosets, Com, Com, Comm, Cos, Com, Dens, Dededen, Dedens, Den, Dens, Dededo, Demo, Demo, Demo, Des, Dedos, Demo, Des, Des, Des, Des, Demos, Demos, Des, Des, Des, Des, The AEM Demo Machine will setup additional [infrastructure](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Infrastructure) such as MongoDB, Solr, MySQL, FFmpeg and email servers.

AEM Demo Machine は次の要素から構成されています。

* A [graphical user interface](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/User%20Interface)
* Apache ANT scripts with configurable [properties](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Properties) and [targets](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Command%20Line)
* インストールするパッケージAEM Demo Machineは、Windows、MacOS、およびLinuxでCQ 5.5、CQ 5.6.1、AEM 6.0、AEM 6.1、AEM 6.2、AEM 6.3で正常にテストされました。

AEM Demo Machineには有効なAEMライセンスが必要です。

>[!NOTE]
>
>AEM Demo Machine の[紹介ビデオ](https://www.youtube.com/watch?v=zEE_zkR9fVQ&amp;feature=youtu.be)を参照してください（13:26）。

## AEM Communities ドキュメント {#aem-communities-documentation}

* Visit [Deploying Communities](deploy-communities.md) to learn about recommended deployments.

* コミュニティサイトの作成、コミュニティグループの追加、コミュニティサイトテンプレートの設定、コミュニティコンテンツのモデレート、メンバーの管理、タグ付け、通知、スコアおよびバッジについては、[コミュニティサイトの管理](administer-landing.md)を参照してください。

* Visit [Developing Communities](communities.md) to learn about the social component framework (SCF) and customizing Communities components and features.

* Visit [Authoring Communities Components](author-communities.md) to learn how to author with and configure Communities components.

