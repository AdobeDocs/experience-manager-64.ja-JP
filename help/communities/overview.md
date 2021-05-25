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
exl-id: 3a8b21f8-75da-4867-9a8a-80fddf7946ed
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '1407'
ht-degree: 41%

---

# AEM Communities の概要 {#aem-communities-overview}

Adobe Experience Manager（AEM）Communities では、高いパフォーマンスと優れたサイト管理機能を持つオンプレミスのコミュニティサイトを素早く作成し、サイト訪問者を価値あるコミュニティメンバーに転換できます。

<!--
Contact your account representative for information regarding licensing of AEM Communities as well as additional licensing for enablement features and Adobe Analytics.
-->

## Communities の機能 {#communities-features}

AEM Communitiesは、ブログ、Q&amp;A、イベントカレンダーを通じて通知するサイト訪問者との関係を構築し、フォーラム、コメント、その他のコミュニティコンテンツ(多くの場合、ユーザー生成コンテンツ(UGC)と呼ばれる)を通じて洞察を得ることができます。

さらに AEM Communities では、パブリッシュ環境での信頼されたメンバーによるモデレートや、Twitter および Facebook のソーシャルログイン、コミュニティコンテンツのインライン翻訳、公開済みコミュニティサイトでのコミュニティグループの作成、バッジ授与のためのスコア付け、ファイル共有、通知およびアクティビティストリームを実現できます。

Communities の機能は、GitHub.com で公開されている [AEM Demo Machine](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki)で試すことができます。また、新しい We.Retail のリファレンス実装内でも試すことができます。

## コミュニティサイト  {#community-sites}

コミュニティサイトは、シンプルなウィザードで作成できる AEM サイトです。作成される Web サイトには、数多くの一般的な機能があらかじめ組み込まれています。

[サイト作成ウィザード](sites-console.md):

* 選択した[コミュニティサイトテンプレート](sites.md)に基づいて、サイトの機能を構築します。
   * [コミュニティ関数](#community-functions)から構築
   * オプションの[コミュニティグループ](#communitygroups)機能
* 設定を使用して、次の設定をおこないます。
   * モデレート
   * ログイン
   * 翻訳
* 基本的な機能を提供します。
   * レスポンシブデザイン：[TwitterBootstrapテーマ](https://getbootstrap.com)を使用
   * ログイン：自己登録、[ソーシャルログイン](social-login.md)、ユーザープロファイル
   * 通知：メンバーは、自分に関連するイベントを確認する
   * メッセージ：メンバーはコミュニティサイト内でメッセージの送受信を行うことができます
   * 検索：コミュニティサイト内での検索機能
   * 言語の切り替え：[多言語サイト](../../help/sites-administering/translation.md)の言語を選択できる
   * 管理：コミュニティサイト内のユーザーをモデレートおよび管理する権限を持つメンバー
* ページレベルのオーサリング手順が多くなりません。
   * ブランディング：コミュニティサイトのすべてのページに表示するバナー画像のオプションアップロード
   * ナビゲーションメニュー：コミュニティサイトテンプレートに含まれる機能のナビゲーションリンクが提供されます。

新しいコミュニティサイトを簡単に作成するには、[AEM Communitiesの概要](getting-started.md)を参照してください。

## コミュニティコンテンツの永続性 {#community-content-persistence}

AEM Communities でコミュニティコンテンツのパフォーマンスと同期を改善するには、ユーザー生成コンテンツ（UGC）専用の共通ストアを用意し、それをすべての AEM インスタンス（オーサーおよびパブリッシュ）で共有することが必要です。

コミュニティコンテンツは、ストレージリソースプロバイダー（SRP）を介して簡単にアクセスできます。SRP はアクセスを基本トポロジから切り離すレイヤーを提供し、UGC の共通ストアをサポートします。

コミュニティコンテンツの永続性と推奨されるデプロイメントについて詳しくは、次のページを参照してください。

* [コミュニティコンテンツのストレージ](working-with-srp.md)：UGC のために利用できる SRP ストレージオプションについて説明します。
* [推奨トポロジ](topologies.md)：ユースケースと SRP の選択に応じたトポロジについて説明します。
* [AEM Communities 6.3 へのアップグレード](upgrade.md)：AEM 6.3 に移行する際に役立つ UGC に関する情報を示します。

## コミュニティコンソール {#communities-consoles}

オーサー環境では、グローバルナビゲーションコンソールから[コミュニティコンソール](consoles.md)にアクセスできます。このコンソールには、次のものが含まれます。

* [サイト](sites-console.md)コンソール

   * サイトの作成
   * サイト編集
   * サイト管理
   * [コミュニティグループ](groups.md)コンソール

* [モデレート](moderation.md)コンソール

   * オーサー環境とパブリッシュ環境向けの一般的な一括モデレートUI
   * 新しいフィルター条件

* [メンバーおよびグループ](members.md)管理コンソール

   * オーサー環境からパブリッシュ側のユーザー（メンバー）を作成および管理する機能を提供します。
   * メンバーを禁止する機能を提供
   * オーサー環境からパブリッシュ側のユーザーグループ（メンバーグループ）を作成および管理する機能を提供します

* [レポート](reports.md)コンソール

   * 割り当て、投稿および表示に関するレポートを生成できます。

* [リソース](resources.md)コンソール

   * イネーブルメントリソースと学習パスを作成する機能を提供します。
   * イネーブルメントリソースと学習パスに関するレポートにアクセスできます。

グローバルツールコンソールから次のコミュニティツールにアクセスできます。

* [サイトテンプレート](tools.md#sitetemplatesconsole)コンソール

   * コミュニティサイトテンプレートの作成と管理

* [グループテンプレート](tools.md#grouptemplatesconsole)コンソール

   * コミュニティグループテンプレートの作成と管理

* [コミュニティ機能](tools.md#communityfunctionsconsole)コンソール

   * コミュニティ機能の作成と管理

* [ストレージ設定](tools.md#storageconfiguratonconsole)コンソール

   * サイトの[共通ストア](working-with-srp.md)を選択して設定します。

* [コンポーネントガイド](components-guide.md)

   * すべてのコミュニティコンポーネントのサンプルをデフォルト設定で提供し、それらを試す機能を提供するサンプルサイト、[コミュニティコンポーネント](http://localhost:4502/editor.html/content/community-components/en.html)

## コミュニティサイトテンプレート {#community-site-templates}

コミュニティサイトの作成は、任意のサンプルサイトとは独立したコミュニティサイトをすばやく設定するために、コミュニティサイトテンプレートの選択に基づいておこなわれます。

コミュニティ機能とコミュニティグループテンプレートで構成されるコミュニティサイトテンプレートは、ログイン、ユーザープロファイル、メッセージング、サイトメニュー、検索、テーマ、ブランディング機能など、コミュニティサイトの構造を提供します。

[サイトテンプレートコンソール](sites.md)を参照してください。

## コミュニティ機能  {#community-functions}

コミュニティに必要とされる機能はだいたい決まっています。AEM Communities では、こうした機能が基本要素として用意されており、「コミュニティ機能」と呼ばれています。

コミュニティ機能とは、様々なコンポーネントを組み合わせて 1 つの機能にまとめ、コミュニティサイトテンプレートに簡単に組み込める形にした通常の AEM ページです。

[コミュニティ機能コンソール](functions.md)を参照してください。

## コミュニティグループとグループテンプレート  {#community-groups-and-group-templates}

コミュニティグループ機能を使用すると、許可されたユーザーとコミュニティメンバーが、オーサー環境とパブリッシュ環境の両方からコミュニティサイト内にサブコミュニティを動的に作成できます。

テンプレートの構造に[グループ機能](functions.md#groups-function)が含まれる場合は、オーサー環境から、コミュニティグループ（サブコミュニティ）を既存のコミュニティサイト内に作成したり、既存のグループ内にネストしたりできます。

コミュニティグループを作成するには、コミュニティグループページのデザインを提供するコミュニティグループテンプレートを選択する必要があります。 グループ機能をテンプレート構造に追加すると、1つのグループテンプレートを指定するか、新しいコミュニティグループの作成時にテンプレートの選択肢を提供するように設定されます。

関連トピック：

* [サイトグループコンソール](groups.md)  — オーサー環境でのサブコミュニティの作成
* [グループテンプレートコンソール](tools-groups.md)  — グループ用のサイト構造の作成
* [AEM Communities使用の手引き](getting-started.md)  — ネストされたグループを含むコミュニティサイトをすばやく作成するためのチュートリアル

## コミュニティコンポーネント {#community-components}

コミュニティサイトの構成要素である[コミュニティコンポーネント](author-communities.md)は、AEM サイトに Communities 機能を追加するために使用します。

[コミュニティコンポーネントガイド](components-guide.md)では、これらのコンポーネントをインタラクティブに検討できます。

## コミュニティのタイプ  {#types-of-communities}

### Engagement Community {#engagement-community}

エンゲージメントコミュニティは、顧客の情報提供、フィードバックの要請、コミュニティメンバーとしての顧客のインタラクションを可能にする、ユーザーの関心を集めたコミュニティサイトです。

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
* スコアとバッジ
* Analyticsレポート

新しいエンゲージメントコミュニティをすばやく簡単に作成するには、[AEM Communitiesの概要](getting-started.md)を参照してください。

### イネーブルメントコミュニティ {#enablement-community}

イネーブルメントコミュニティは、オンライン学習機能を用意したコミュニティサイトです。

イネーブルメントコミュニティの機能には、次のものが含まれます。

* [エンゲージメントコミュニティ](#engagement-community)のすべての機能
* メンバーおよびメンバーグループにコンテンツおよび学習リソースを割り当てる機能
* クイズやテストなど、SCORMコンテンツをサポート
* 割り当て完了の追跡
* Reports &amp; Analyticsへのアクセス
* フォーラム、メッセージング、コメントおよび評価を通じて学習リソースに関する会話を行う機能

イネーブルメントコミュニティは、[イネーブルメントアドオンが設定されると作成される場合があります。](enablement.md)には、実稼動環境で使用する追加のライセンスが必要です。 イネーブルメントコミュニティサイトには、[割り当て機能](#community-functions)が含まれます。

新しいイネーブルメントコミュニティを簡単に作成するには、[AEM Communitiesを使い始める](getting-started-enablement.md)を参照してください。

## AEM Demo Machine {#aem-demo-machine}

[AEM Demo Machine](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine)は、AEM [Sites](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Sites)、[Assets](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Assets)、[Communities](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Communities)、[Apps](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Apps)および[Forms](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Forms)のデモを管理および実行します。クイックスタートインスタンスを起動するだけで済みます。 AEM Demo Machineは、MongoDB、Solr、MySQL、FFmpeg、電子メールサーバーなど、追加の[インフラストラクチャ](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Infrastructure)を設定します。

AEM Demo Machine は次の要素から構成されています。

* [グラフィカルユーザーインターフェイス](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/User%20Interface)
* 設定可能な[プロパティ](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Properties)と[ターゲット](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Command%20Line)を持つApache ANTスクリプト
* インストールするパッケージ
AEM Demo Machineは、Windows、MacOSおよびLinux上でCQ 5.5、CQ 5.6.1、AEM 6.0、AEM 6.1、AEM 6.2、AEM 6.3で正常にテストされました。

AEM Demo Machineには、有効なAEMライセンスが必要です。

>[!NOTE]
>
>AEM Demo Machine の[紹介ビデオ](https://www.youtube.com/watch?v=zEE_zkR9fVQ&amp;feature=youtu.be)を参照してください（13:26）。

## AEM Communities ドキュメント  {#aem-communities-documentation}

* 推奨されるデプロイメントについては、[Communitiesのデプロイ](deploy-communities.md)を参照してください。

* コミュニティサイトの作成、コミュニティグループの追加、コミュニティサイトテンプレートの設定、コミュニティコンテンツのモデレート、メンバーの管理、タグ付け、通知、スコアおよびバッジについては、[コミュニティサイトの管理](administer-landing.md)を参照してください。

* ソーシャルコンポーネントフレームワーク(SCF)とコミュニティのコンポーネントと機能のカスタマイズについては、 [コミュニティの開発](communities.md)を参照してください。

* コミュニティコンポーネントを使用してオーサリングおよび設定する方法については、 [コミュニティコンポーネントのオーサリング](author-communities.md)を参照してください。
