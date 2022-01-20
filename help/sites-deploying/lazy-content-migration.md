---
title: 遅延コンテンツ移行
seo-title: Lazy Content Migration
description: AEM 6.4 の遅延コンテンツ移行について説明します。
seo-description: Learn about Lazy Content Migration in AEM 6.4.
uuid: 9c84f7fe-31d3-4b63-8975-9e75a6c44b7d
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.4/SITES
content-type: reference
topic-tags: upgrading
discoiquuid: 282a828a-edb2-4643-9bf7-ec30c29dc6ce
feature: Upgrading
exl-id: 8dc2dfb8-037f-40ae-a962-ced89dd3fdd0
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '668'
ht-degree: 93%

---

# 遅延コンテンツ移行{#lazy-content-migration}

後方互換性のために、AEM 6.3 以降で **/etc** および **/content** に存在するコンテンツおよび設定は、アップグレードですぐに変更または変換されません。これは、これらの構造上にあるお客様のアプリケーションの依存関係が変更されないようにするためにおこなわれます。AEM 6.4 のすぐに使用できるコンテンツが別の場所でホストされていても、これらのコンテンツ構造に関連する機能は同じままです。

これらのすべての場所が自動的に変換されるわけではありませんが、いくつかの遅延した `CodeUpgradeTasks` も遅延コンテンツ移行と見なされます。これにより、お客様は、次のシステムプロパティを使用してインスタンスを再起動することで、これらの自動変換にトリガーを設定できます。

```shell
-Dcom.adobe.upgrade.forcemigration=true
```

これにより、移行中に `CodeUpgradeTasks` が実行されます。

目的は効率的な実行ですが、このアップグレード処理は同期的です。そのため、処理される必要のあるコンテンツの量に応じたダウンタイムを伴います。実稼動システムの前にステージ環境で実行時間を評価して、それに応じたメンテナンスウィンドウを計画することをお勧めします。

通常、これにもアプリケーションの調整が必要となるので、このアクティビティは対応するアプリケーションのデプロイメントと共に実行する必要があります。

次に、6.4 で導入された `CodeUpgradeTasks` の完全なリストを示します。

| **名前** | **関連する AEM バージョン** | **移行のタイプ** | **詳細** |
|---|---|---|---|
| `Cq561ProjectContentUpgrade` | &lt; 5.6.1 | 即時 |  |
| `Cq60MSMContentUpgrade` | &lt; 6.0 | 即時 | 削除された `LiveRelationShips` からすべての `VersionStorage` を検出し、親に実行プロパティを追加します。 |
| `Cq61CloudServicesContentUpgrade` | &lt; 6.1 | 即時 | デフォルトの保護設定でクラウドサービスを再構築します。 |
| `Cq62ConfContentUpgrade` | &lt; 6.2 | 即時 | **/content** から **/conf** へのプロパティベースのリンクを削除し（OSGi メカニズムで置き換え）、対応する OSGi 設定を生成します。 |
| `Cq62FormsContentUpgrade` | &lt; 6.2 | 即時 | merge_preserve 処理が原因で、デフォルトの保護拒否ルールが指定された権限を上書きするので、アップグレード時に並べ替えが必要になります。 |
| `CQ62Html5SmartFileUpgrade` | &lt; 6.2 | 即時 | Html5SmartFile ウィジェットを使用するコンポーネントを検出し、コンテンツ内でのコンポーネントの使用を検索して、実質的にバイナリを下のレベルに移動してコンポーネントレベルに格納しないことで永続性を再構築します。 |
| `Cq62ProjectsCodeUpgrade` | &lt; 6.2 | 即時 | 古いスタイルのプロジェクトを **/etc/projects** から **/content/projects** に移動します。 |
| `Cq62TargetCampaignsContentUpgrade` | &lt; 6.2 | 即時 | 階層（Areas）にコンテナレイヤーを導入し、参照を調整します。 |
| `Cq62TargetContentUpgrade` | &lt; 6.2 | 即時 | 固定された場所名をターゲットコンポーネントに設定します。 |
| `Cq62WorkflowContentUpgrade` | &lt; 6.2 | 即時 | ワークフローの複雑な変換では、6.2 の構造、インスタンス、通知にさかのぼり、**/var/backup** のバックアップの場所から結合し直してモデル化します。 |
| `CQ63AssetsMetadataFormsUpdate` | &lt; 6.3 | 即時 | アセット、カスタムメタデータスキーマおよび処理プロファイルを **/apps** から **/conf** に移動して、メタデータスキーマおよびメタデータプロファイルフォームを coral2 から coral3 に変換します。 |
| `CQ63AssetsSearchFacetsUpdate` | &lt; 6.3 | 即時 | アセットおよびカスタム検索ファセットを **/apps** から **/conf** に移動して、メタデータスキーマおよびメタデータプロファイルフォームを coral2 から coral3 に変換します。 |
| `CQ63InboxItemsUpgrade` | &lt; 6.3 | 即時 | インボックス項目を並べ替えるために InboxItems を更新（効率的な並べ替えのためにメタデータを調整）します。 |
| `CQ63MetadataSchemaConfigUpdate` | &lt; 6.3 | 即時 | 相対パスを **/apps** の代わりに **/conf** に置き換えることで、フォルダーの metadataSchema プロパティを調整します。 |
| `CQ63MobileAppsNavUpgrade` | &lt; 6.3 | 即時 | ナビゲーション構造を調整します。 |
| `CQ63MonitoringDashboardsConfigUpdate` | &lt; 6.3 | 即時 | 監視ダッシュボードのカスタム設定を **/libs** および **/apps** から移動します。 |
| `CQ63ProcessingProfileConfigUpdate` | &lt; 6.3 | 即時 | 6.3 以降の構造に合致させるために、（6.1 まで使用されていた）アセットの processingProfile プロパティを変換します。また、プロファイルの相対パスを **/apps** の代わりに **/conf** に変更します。 |
| `CQ63ToolsMenuEntriesContentUpgrade` | &lt; 6.3 | 即時 | アップグレードの場合に、廃止された CRXDE Lite および Web コンソールのメニューエントリを削除するアップグレードタスク。 |
| `CQ64CommunitiesConfigsCleanupTask` | &lt; 6.3 | 遅延 | SRP クラウド設定、コミュニティウォッチワード設定を移動して、**/etc/social** および **/etc/enablement** をクリーンアップします（遅延移行が実行される際に、参照およびデータを調整する必要があります。アプリケーション部分がこの構造に依存しなくなるようにする必要があります）。 |
| `CQ64LegacyCloudSettingsCleanupTask` | &lt; 6.4 | 遅延 | **/etc/cloudsettings** をクリーンアップします（ContextHub 設定を含む）。最初のアクセス時に設定が自動的に移行されます。アップグレードに伴って遅延コンテンツ移行が開始される場合、**/etc/cloudsettings** にあるこのコンテンツは、アップグレード前にパッケージを介して保持し、暗黙的な変換を開始するために再インストールする必要があります。パッケージは移行の完了後にアンインストールされます。 |
| `CQ64UsersTitleFixTask` | &lt; 6.4 | 遅延 | 従来のタイトル構造をユーザープロファイルノードのタイトルに適合させます。 |
| `CQ64CommerceMigrationTask` | &lt; 6.4 | 遅延 | コマースコンテンツの移行元 **/etc/commerce** から **/var/commerce**. 移行中に、コンテンツが移動され、移動されたコンテンツへの参照が新しい場所を反映するように更新されます。 |
