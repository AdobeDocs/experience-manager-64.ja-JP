---
title: Adobe Experience Manager 6.4 の一般リリースノート
seo-title: Release Notes
description: Adobe Experience Manager 6.4 のノートでは、リリース情報、新機能、インストール方法および詳細な変更リストの概要を説明しています。
seo-description: Adobe Experience Manager 6.4 notes outlining the release information, what's new, how to install and detailed change lists.
uuid: 5a220301-2727-4078-ba19-4a2dbf9657f4
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.4
topic-tags: release-notes
content-type: reference
discoiquuid: 2be468e7-2b4e-4e04-881b-b9bdd1f55e57
exl-id: ee034595-2d2a-4887-86c4-6bf0770da6a2
source-git-commit: 0f4f8c2640629f751337e8611a2c8f32f21bcb6d
workflow-type: tm+mt
source-wordcount: '2729'
ht-degree: 21%

---

# Adobe Experience Manager 6.4 の一般リリースノート {#general-release-notes-for-adobe-experience-manager}

## リリース情報 {#release-information}

| 製品 | Adobe Experience Manager |
|---|---|
| バージョン | 6.4 |
| 種類 | メジャーリリース |
| 一般公開日 | 2018年4月04日（PT） |
| 推奨される更新 | 詳しくは、 [AEMのリリースと更新](https://helpx.adobe.com/jp/experience-manager/aem-releases-updates.html) |

### 参考情報 {#trivia}

このバージョンのAdobe Experience Managerのリリースサイクルは 2017 年 4 月 27 日に開始され、22 回の品質保証とバグ修正を繰り返し、2018 年 3 月 22 日に終了しました。 このリリースで修正された、機能強化と新機能を含むお客様関連の問題の総数は 704 件です。   

Adobe Experience Manager 6.4 は、2018 年 4 月 4 日以降、一般に利用可能です。

>[!NOTE]
>
>Adobeは最新のサービスパックをインストールすることをお勧めします。新機能パックはすべて、 [サービスパック](https://helpx.adobe.com/jp/experience-manager/maintenance-releases-roadmap.html).

## 新機能 {#what-s-new}

Adobe Experience Manager 6.4 は、Adobe Experience Manager 6.3 コードベースのアップグレードリリースです。新機能と強化された機能、お客様向けの重要な修正、お客様向けの優先順位の高い機能強化、製品の安定性向上のための全般的なバグ修正が加えられています。また、すべてのAdobe Experience Manager 6.3 機能パック、ホットフィックス、サービスパックリリースの大部分も含まれています。

次のリストはその概要です。詳細については以降のページを参照してください。

### Experience Manager基盤 {#experience-manager-foundation}

の変更の完全なリスト [AEM Foundation](wcm-platform.md).

Adobe Experience Manager 6.4 のプラットフォームは、OSGi ベースのフレームワーク（Apache Sling および Apache Felix）の更新バージョンと Java コンテンツリポジトリの上に構築されています。Apache Jackrabbit Oak 1.8.2.

Quickstart は、サーブレットエンジンとして Eclipse Jetty 9.3.22 を使用します。

#### ユーザーインターフェイス {#user-interface}

UI に様々な機能強化が加えられ、生産性が向上し、使いやすくなりました。

* [新しいコンテンツツリーレール](/help/sites-authoring/basic-handling.md#content-tree) をクリックして、階層をすばやく移動します。 リストビューと組み合わせて、クラシック UI のインタラクションモデルが復元されます。
* 大きなフォルダーのカード表示とリスト表示でのスクロール操作を改善しました。
* [検索結果とのやり取りの改善](/help/sites-authoring/search.md) - 「戻る」ボタンをクリックすると、前の検索結果が復元されます。
* [その他のキーボードショートカット](/help/sites-authoring/keyboard-shortcuts.md)を使用するのは、特定のパネルを開く、項目を編集、移動および削除する、プロパティを開くなどの、ほとんどのアクションです。
* [キーボードショートカットを無効にする機能](/help/sites-authoring/user-properties.md) （環境設定で有効/無効を切り替えます）。
* [すべての UI でタイムスタンプの表示を停止](/help/sites-authoring/user-properties.md) 7 日後の相対（環境設定でデフォルトを設定）

詳しくは、 [オーサリングドキュメント](/help/sites-authoring/home.md) を参照してください。

>[!CAUTION]
>
>Adobeは、クラシック UI をさらに強化する予定はありません。 AEM 6.4 にはクラシック UI が含まれており、以前のリリースからアップグレードするお客様はクラシック UI をそのまま使用できます。 クラシック UI は非推奨になっても引き続き完全にサポートされます。[詳細情報](/help/sites-deploying/ui-recommendations.md)。

#### コンテンツリポジトリ {#content-repository}

* オンラインでのリビジョンクリーンアップによるコンパクションの高速化と効率化。 内部テストでは、新しいテールコンパクションが最大 10 倍高速で、AEM 6.3 に比べて IOPS の少ないディスク領域を再利用できることが示されています。この結果、オンラインリビジョンクリーンアップの実行中は、パフォーマンスに対する影響が少なくなります。 詳しくは、 [ドキュメントページ](/help/sites-deploying/revision-cleanup.md#full-and-tail-compaction-modes).

* MongoMK の継続的なリビジョンクリーンアップは、定期的なクリーンアップメンテナンスに代わるものです
* ドキュメントノードストアでのリビジョンクリーンアップの効率が向上しました。

#### 検索とインデックス作成 {#search-indexing}

* oak-run(CLI) を使用したインデックス作成操作のサポートが強化されました。

   * インデックスの整合性チェック
   * インデックス作成統計
   * インデックス設定の読み込みまたは書き出し
   * インデックス再作成

* Lucene 関連のリポジトリの増加が減少し、システム全体のパフォーマンスが向上

詳しくは、 [このドキュメントページ](/help/sites-deploying/indexing-via-the-oak-run-jar.md).

#### モニタリング {#monitoring}

* 新しい [システム概要](/help/sites-administering/operations-dashboard.md#system-overview) は、パフォーマンス関連のすべてのシステムステータスとアクティビティのスナップショットビューを提供します。
* 新しい [ヘルスチェック](/help/sites-administering/operations-dashboard.md#health-checks) インデックス作成、クエリ、メンテナンスに関する

#### プロジェクトとワークフロー {#projects-and-workflows}

* 新規 [ワークフローモデルを作成および編集するためのワークフローエディター](/help/sites-developing/workflows-models.md).

![screen_shot_2018-04-04at71143am](assets/screen_shot_2018-04-04at71143am.png)

#### 以前のバージョンからのアップグレード {#upgrade-from-earlier-version}

* [後方互換性](/help/sites-deploying/backward-compatibility.md):6.4 の後方互換性のある機能により、ほとんどの場合、カスタムコードの互換性を維持し、アップグレードの作業を軽減できます。
* [アップグレードの複雑性評価](/help/sites-deploying/pattern-detector.md):アップグレードの複雑さを評価する新しいパターン検出ツールが追加されました。
* [リポジトリの再構築](/help/sites-deploying/repository-restructuring.md):大幅な再構築（主に/etc）により、アップグレードが容易になり、実装のベストプラクティスが促進されます。
* アップグレードに関する一般的な情報については、 [このページ](/help/sites-deploying/upgrade.md) を参照してください。

### Experience Manager Sites {#experience-manager-sites}

の変更の完全なリスト [AEM Sitesとアドオン](sites.md).

#### 流動的なエクスペリエンス {#fluid-experiences}

2017 年の初めに、コンテンツフラグメント、エクスペリエンスフラグメント、コンテンツサービスをベースにした流動的なエクスペリエンスの導入が、マルチチャネルファーストのコンテンツ管理への発展の始まりでした。 AEM 6.4 は、以下の各領域を大幅に拡張しています。

**[コンテンツフラグメント](/help/assets/content-fragments.md)**

6.4 の新機能は視覚的です。 [コンテンツモデル](/help/assets/content-fragments-models.md) 編集者と [設定可能なコンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/content-fragment-component.html?lang=ja) 柔軟なHTML出力と JSON をコンテンツサービスに含めることができるようにする。

**エクスペリエンスフラグメント**

構築ブロック機能により、同じコンテンツで異なるレイアウトのフラグメント内でバリエーションを作成する方が効率的になりました。 エクスペリエンスフラグメントをFacebookとPinterestに送信する以外に、オファーとしてAdobe Targetに送信できるようになりました。

**コンテンツサービス**

Sling Model Exporter とコアコンポーネントに対する様々な機能強化が含まれ、シングルページアプリで作成されたモバイルアプリやエクスペリエンスにコンテンツを埋め込むための堅牢な JSON 出力を提供します。

#### サイトの迅速な構築 {#gettings-sites-built-quicker}

AEM 6.4 は、次世代のコンポーネントモデルへの変換を完了します。 AEM 6.3 で導入され、スタイルシステムによって追加されたコアコンポーネントの概念は、新しいサイトを構築し、既存のサイトを拡張する効率的な方法を提供します。

新しいコンポーネントモデルの最適な活用方法を学ぶために推奨されるチュートリアルです。 [AEM Sites使用の手引き — WKND チュートリアル](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=ja)

#### Screens アドオン {#screens-add-on}

デジタルサイネージやキオスクネットワークを含む、すべてのマーケティングチャネルにわたって一貫したメッセージを配信することは、AEM Screensの略です。 AEM 6.4 では、Microsoft Windows およびGoogle Chrome OS ハードウェアでの Signage Player の実行のサポートが追加されました。 さらに、リモートデバイスの管理とスケジュール（チャネルのグループ）の機能強化も利用できます。

Screens のアップデートについて詳しくは、 [AEM Screens User Guide](https://experienceleague.adobe.com/docs/experience-manager-screens/user-guide/aem-screens-introduction.html?lang=ja).

### Experience Managerコミュニティ {#experience-manager-communities}

AEM 6.4 では、Communities に多くの新機能と機能強化が追加されています。 変更の完全なリストは、 [AEM Communities](communities-release-notes.md). このリリースの主な機能は次のとおりです。

#### モデレートの機能強化 {#enhancements-to-moderation}

**自動スパム検出**

コミュニティサイトやグループでユーザーが生成した不要なコンテンツを除外する新しいスパム検出エンジンが提供されました。 system/console/configMgr から有効にすると、事前に定義された一連のスパムワードに基づいて、ユーザーが生成したコンテンツの一部がスパムとしてマークされます。 スパム検出エンジンについて詳しくは、 [コンテンツを生成するコミュニティユーザーの自動化](/help/communities/moderate-ugc.md#spam-detection).

![スパム検出](assets/spamdetection.png)

**Q&amp;A 用の新しいフィルター**

「回答済み」および「未回答」という新しいフィルターが一括モデレートコンソールに追加され、Q&amp;A の質問にフィルターを適用できるようになりました。 回答済みおよび未回答のステータスフィルターの仕組みについては、 [ユーザー生成コンテンツの一括モデレート](/help/communities/moderation.md#main-pars-note-521961797).

**ブックマークモデレートフィルター**

モデレートコンソールで事前定義されたモデレートフィルターをブックマークする機能が提供されました。 これらのフィルターは URL 文字列の末尾に追加されるので、後で共有、再利用、再訪問できます。 でフィルターをブックマークする方法について説明します。 [一括モデレートコンソール](/help/communities/moderation.md#main-pars-note-429176623).

#### UGC とユーザープロファイルの削除 {#delete-ugc-and-user-profiles}

AEM 6.4 Communities で公開されている [標準搭載の API](/help/communities/user-ugc-management-service.md) およびサンプル [servlet](https://github.com/Adobe-Marketing-Cloud/aem-communities-ugc-migration/tree/master/bundles/communities-ugc-management-servlet) エンドユーザーがデータを制御できるようにする。 また、これらの API を使用すると、データ処理やデータ管理組織が EU の GDPR コンプライアンス要求に対応できるようになります。

#### サイトおよびグループ管理の機能強化 {#enhancements-to-site-and-group-management}

**1 つの手順で複数ロケールのグループを作成**

1 回の操作で複数言語グループを作成する機能が提供されました。 このようなグループを作成するには、サイトコンソールから目的のコミュニティサイトのグループコレクションに移動します。 グループを作成し、コミュニティグループテンプレートページで目的の言語を指定します。 この機能について詳しくは、 [コミュニティグループコンソール](/help/communities/groups.md).

![多言語群](assets/multilingualgroup.png)

**[1 回のクリックでコミュニティサイトとグループを削除](/help/communities/groups.md)**

グローバルナビゲーションから移動する際に、それぞれのサイトおよびグループで削除アイコンを使用できるようになりました。 このアイコンを使用すると、サイトまたはグループに関連付けられているすべての項目とコンテンツが削除され、ユーザーの関連付けがすべて削除されます。 この機能について詳しくは、 [コミュニティサイトの管理](/help/communities/create-site.md#main-pars-text-fe17) および [コミュニティグループの管理](/help/communities/groups.md#main-pars-text-5e8c).

#### イネーブルメントの機能強化 {#enhancements-to-enablement}

割り当て機能とカタログ機能がグループ内で使用できるようになりました。 これにより、ターゲットとなる特定のコミュニティメンバー向けに学習コンテンツを作成、管理、公開できます。 コミュニティグループの有効化について詳しくは、 [イネーブルメントリソースの管理](/help/communities/resource.md).

![assignmentcatalog](assets/assignmentcatalog.png)

### Experience Manager Assets {#experience-manager-assets}

AEM 6.4 では、新機能、強化された CreativeCloud 統合、主な人工知能イノベーション、改善されたメタデータ管理、レポート機能の強化、全体的なユーザーエクスペリエンスの改善など、アセットに関する新機能と機能強化が導入されています。 以下で利用できる変更の完全なリスト： [AEM Assets](assets.md). このリリースの主な特徴は次のとおりです。

**Adobe Asset Link**

Adobe向けCreative Cloudの Asset Link を使用すると、コンテンツ作成プロセスでのクリエイティブ担当者とマーケターのコラボレーションを合理化できます。 これは、Photoshop、Illustrator、InDesignをAEMに接続する企業向けの新しいネイティブ機能で、クリエイティブチームがツールを選択したままで済みます。

この機能、前提条件およびアクセス方法について詳しくは、 [Adobeアセットリンク](https://www.adobe.com/jp/creativecloud/business/enterprise/adobe-asset-link.html).

![adobe_asset_link](assets/adobe_asset_link.png)

**AEM デスクトップアプリケーション**

AEMデスクトップアプリケーションが、AEM 6.4 と互換性のあるバージョン 1.8 に更新されました。AEMデスクトップアプリケーションの変更の完全なリストは、専用の [AEM desktop app リリースノート](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/release-notes.html?lang=ja) 文書。

AEM 6.3 リリース以降に導入された改善点には、バックグラウンドで階層フォルダーをアップロードする機能、アセットのバックグラウンド操作を監視する新しい UI、キャッシングの強化、ネットワークとログインの機能、全体的な安定性の向上が含まれます。 このドキュメントには、 [ベストプラクティスガイド](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html?lang=ja).

**Adobe Sensei Services**

新機能には、顧客のビジネス上の分類を学ぶ機能と共に、デジタルアセットに顧客固有のタグを自動的に付ける機能や、スマート翻訳検索が含まれます。これにより、検索用語をその場で翻訳し、複数言語での検索性が向上します。 この機能の詳細については、 [拡張スマートタグ](/help/assets/enhanced-smart-tags.md).

![enhanced_smart_tags2](assets/enhanced_smart_tags2.png)

**メタデータ**

多数のアセットのメタデータを同時に読み込みおよび書き出しする機能や、次のような高度なメタデータ構成など、様々な機能強化がおこなわれました。 [カスケードメタデータ](/help/assets/cascading-metadata.md).

**レポート**

アセットレポートは、新しいレポートフレームワーク、ユーザーエクスペリエンス、お客様の使用例に関するより多くの OOTB レポートを使用して、AEM 6.4 で大きな見直しがおこなわれました。 様々なレポートの生成方法について詳しくは、 [アセットレポート](/help/assets/asset-reports.md).

**ユーザーエクスペリエンス**

スクロールエクスペリエンス、検索戻るボタン、検索フィルターの改善など、Assets ユーザーの参照、検索、管理操作を改善する複数の機能強化。 完全なリストは、 [AEM Assets](assets.md).

**Brand Portal**

アセット配布のためのメタデータ、レポート、デジタル著作権、ログイン操作、公開パフォーマンスの各領域での機能強化。 新しい機能強化については、 [AEM Assets Brand Portalの新機能](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/introduction/whats-new.html?lang=ja).

#### Dynamic Media Add-on {#dynamic-media-add-on}

AEM 6.4 には、Dynamic Mediaの多くの新機能と機能強化が含まれています。 完全なリストは、 [AEM Assets](assets.md). 主な主な特徴は次のとおりです。

**スマート切り抜き**

Adobe Senseiを活用したスマート切り抜きでは、画像の非破壊切り抜きが自動的に提供され、レスポンシブデザインの目標点が維持されます。 切り抜かれた画像の候補をプレビューし、必要に応じて手動で調整することができます。 また、この機能により、製品画像のスウォッチを自動的に生成することもできます。

詳しくは、 [イメージプロファイル](/help/assets/image-profiles.md) スマート切り抜きの使用に関する詳細は、ドキュメントを参照してください。

詳しくは、 [ページへのDynamic Media Assets の追加](/help/assets/adding-dynamic-media-assets-to-pages.md) を参照して、Dynamic Mediaコンポーネントでのスマート切り抜きの操作について確認してください。

**スマートイメージング**

スマートイメージングでは、各ユーザーに固有の閲覧特性を利用して、ユーザーのエクスペリエンス用に最適化された画像を自動的に提供するので、パフォーマンスとエンゲージメントが向上します。

詳しくは、 [スマートイメージング](/help/assets/imaging-faq.md) ドキュメントを参照してください。

![smart_crop](assets/smart_crop.png)

**新しいメディアおよびビューアの機能強化**

パノラマおよび VR を含む新しいビューアを使用すると、より没入感のあるエクスペリエンスを提供できます。

詳しくは、 [パノラマ画像](/help/assets/panoramic-images.md) ドキュメントを参照してください。

### Experience Manager Forms {#experience-manager-forms}

AEM 6.4 Formsでは、いくつかの新機能および機能強化が導入されています。 主なものは次のとおりです。

* マルチチャネルインタラクティブ通信
* ビジネスアプリケーションからのインタラクティブ通信の事前入力
* ワークフローの最新化とモバイルワーカーのサポート
* フラグメントの遅延読み込み
* LiveCycleからExperience Manager Forms 6.4 へのシングルホップアップグレード

詳細は次のとおりです。 [AEM Forms](forms.md) リリースノートページ また、 [AEM 6.4 Formsの新機能および機能強化の概要](/help/forms/using/whats-new.md) を参照してください。

### Experience Manager Livefyre {#experience-manager-livefyre}

使用している AEM 6.4 インスタンスを Livefyre と統合できます。Livefyre とAEMを統合する方法については、次の URL を参照してください。

* [Livefyre との統合](https://experienceleague.adobe.com/docs/experience-manager-64/administering/integration/livefyre.html?lang=ja-JP)

### 顧客中心の開発を活用 {#leverage-customer-focused-development}

Adobeは、お客様が仕様、開発およびテスト中に開発プロセスのすべての段階に貢献できる、お客様中心の開発モデルを使用しています。 このプロセスで貢献しているすべてのお客様およびパートナーに感謝します。

アドビでは、お客様志向のバグ修正と機能強化リクエストの開発に関する、情報収集、優先順位付け、追跡のための手順とプロセスを整備しています。この [Adobe Marketing Cloud Support Portal](https://helpx.adobe.com/jp/contact/enterprise-support.ec.html) は、Adobe機能強化および欠陥追跡システムと統合されています。 お客様の質問は、可能な限りカスタマーケアによって特定および解決されます。 研究開発部門にエスカレートされた場合は、お客様の情報をすべて収集して、優先順位付けとレポートに使用します。有料のサポートと保証に関する問題と有料のお客様向けの機能強化に関する優先事項が開発時に与えられます。

この優先順位付けのプロセスにより、AEM 6.4 では 500 件を超えるお客様中心の変更がおこなわれました。

## リリースに含まれるファイルのリスト {#list-of-files-that-are-part-of-the-release}

**基盤**

* スタンドアロンのクイックスタート：cq-quickstart-6.4.0.jar
* アプリケーションサーバーのクイックスタート：cq-quickstart-6.4.0.war
* 様々な Web サーバーおよびプラットフォーム向けの Dispatcher 4.3.1 以降。 詳しくは、 [ダウンロードリンク](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/getting-started/release-notes.html?lang=ja-JP).
* Eclipse IDE 用プラグイン。 [詳細を表示およびダウンロード](/help/sites-developing/aem-eclipse.md).

* Brackets Code Editor の拡張機能。 [詳細を表示およびダウンロード](/help/sites-developing/aem-brackets.md).
* Maven/Gradle の依存関係。 詳しくは、 [ダウンロードリンク](https://repo.adobe.com/nexus/content/repositories/releases/com/adobe/aem/uber-jar/6.1.0/).

**Sites**

* コアコンポーネント ([GitHub プロジェクト](https://github.com/Adobe-Marketing-Cloud/aem-core-wcm-components))
* We.Retail 参照実装 ([詳細を表示](/help/sites-developing/we-retail.md))
* プロジェクトのブループリントアーキタイプ ([GitHub プロジェクト](https://github.com/Adobe-Marketing-Cloud/aem-project-archetype))
* 様々なプラットフォーム向けの AEM Screens Players（[ダウンロード](https://download.macromedia.com/screens/)）
* スマートコンテンツの言語モデル。英語が事前にインストールされています。より多くの言語をダウンロードできます。

   * [ドイツ語](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-de)
   * [スペイン語](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-es)
   * [イタリア語](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-it)
   * [フランス語](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-fr)

* [AEM Modernization Tools](/help/sites-developing/modernization-tools.md) クラシック UI コンポーネントを Coral 3 に移行するには

**Assets**

* Adobe Experience Managerデスクトップアプリ ([詳細を表示](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html?lang=ja) および [ダウンロード](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/release-notes.html?lang=ja))

* 拡張ラスタライザを追加するPDF([詳細を表示](/help/assets/aem-pdf-rasterizer.md) および [ダウンロード](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq640/product/assets/aem-assets-pdf-rasterizer-pkg))

* 拡張 RAW 画像サポートを追加するパッケージ ([詳細を表示](/help/assets/camera-raw.md))

**Forms**

* AEM Forms機能用パッケージ：

   * [adobe-aemfd-aix-pkg](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=ja)
   * [adobe-aemfd-linux-pkg](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=ja)
   * [adobe-aemfd-solaris-pkg](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=ja)
   * [adobe-aemfd-win-pkg](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=ja)
   * [adobe-aemfd-osx-pkg](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=ja)

## 言語 {#languages}

 ユーザーインターフェイスは次の言語で使用できます。

* 英語
* ドイツ語
* フランス語
* スペイン語
* イタリア語
* ポルトガル語（ブラジル）
* 日本語
* 簡体字中国語
* 繁体字中国語（限定的なサポート）
* 韓国語

Experience Manager6.4 は、中国語エンコーディング規格の使用に関するGB18030-2005 CITS の認定を受けています。

## インストールと更新 {#install-update}

詳しくは、 [インストール手順](/help/sites-deploying/custom-standalone-install.md) を参照してください。

詳しくは、 [アップグレードドキュメント](/help/sites-deploying/upgrade.md) を参照してください。

## サポートされているプラットフォーム {#supported-platforms}

サポートされているプラットフォーム ( サポートレベル： [AEM 6.4 技術要件](/help/sites-deploying/technical-requirements.md).

>[!NOTE]
>
>Oracle は Oracle Java SE 製品の「長期サポート」（LTS）モデルに移行しました。Java 9 と 10 は非 LTS リリースで、Oracle別 ( [OracleJava SE サポート・ロードマップ](https://www.oracle.com/jp/technetwork/java/eol-135779.html)) をクリックします。 Adobeでは、AEMを実稼動環境で実行するための Java の LTS リリースのみをサポートします。 したがって、AEM 6.4 で使用する場合は、Java 8 をお勧めします。

## 廃止される機能および削除された機能 {#deprecated-and-removed-features}

Adobeは、製品の機能を絶えず評価し、長期的な計画に沿って、機能をより強力なバージョンに置き換えるか、将来の期待や拡張に備えて選択したパーツを再実装することを決定します。

Adobe Experience Manager 6.4 の場合、 [非推奨（廃止予定）および削除された機能のリストを読む](deprecated-removed-features.md). このページには、2019 年の変更に関する事前発表と、以前のリリースから更新するお客様向けの重要なお知らせも含まれています。

## 詳細な変更リスト {#detailed-changes-lists}

[AEM Sites](sites.md)

[AEM Assets](assets.md)

[AEM Communities](communities-release-notes.md)

[AEM Forms](forms.md)

[AEM の基盤](wcm-platform.md)

## 既知の問題 {#known-issues}

[既知の問題のリスト](known-issues.md)

### 製品のダウンロードとサポート（制限付きサイト） {#product-download-and-support-restricted-sites}

以下のサイトは既存ユーザーのみが参照できます。のお客様で、アクセス権が必要な場合は、担当のAdobeアカウントマネージャーにお問い合わせください。

* [licensing.adobe.com での製品のダウンロード](https://licensing.adobe.com/)。
* 製品の追加機能に関する[ソフトウェア配布](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)上のアップデート、パッチ、パッケージ。
* [Admin Console 経由でのカスタマーサポート](https://adminconsole.adobe.com/)。詳しくは、[新しいアドビカスタマーサポートエクスペリエンス](https://experienceleague.adobe.com/docs/customer-one/using/home.html?lang=ja)を参照してください。
