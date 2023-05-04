---
title: 遅延コンテンツ移行
seo-title: Lazy Content Migration
description: AEM 6.4 での遅延コンテンツ移行について説明します。
seo-description: Learn about Lazy Content Migration in AEM 6.4.
uuid: 9c84f7fe-31d3-4b63-8975-9e75a6c44b7d
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.4/SITES
content-type: reference
topic-tags: upgrading
discoiquuid: 282a828a-edb2-4643-9bf7-ec30c29dc6ce
feature: Upgrading
exl-id: 8dc2dfb8-037f-40ae-a962-ced89dd3fdd0
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '704'
ht-degree: 23%

---

# 遅延コンテンツ移行{#lazy-content-migration}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

下位互換性を保つため、のコンテンツと設定 **/etc** および **/content** AEM 6.3 以降は、アップグレードの際に変更や変換が即座におこなわれることはありません。 これは、これらの構造に対する顧客アプリケーションの依存関係を確実に維持するためにおこなわれます。 標準搭載のAEM 6.4 内のコンテンツが別の場所でホストされている場合でも、これらのコンテンツ構造に関連する機能は同じです。

これらのすべての場所が自動的に変換されるわけではありませんが、遅延がいくつかあります `CodeUpgradeTasks` は、遅延コンテンツ移行とも呼ばれます。 これを使用すると、次のシステムプロパティを設定してインスタンスを再起動することで、これらの自動変換をトリガーできます。

```shell
-Dcom.adobe.upgrade.forcemigration=true
```

これにより、移行中に `CodeUpgradeTasks` が実行されます。

目的は効率的な実行ですが、このアップグレードプロセスは同期的なので、処理が必要なコンテンツの量に応じてダウンタイムが発生します。 実稼動システムの前にステージ環境での実行時間を評価して、対応するメンテナンスウィンドウを計画することをお勧めします。

これは通常、アプリケーションの調整も必要なので、このアクティビティは、対応するアプリケーションのデプロイメントと共に実行する必要があります。

次に、6.4 で導入された `CodeUpgradeTasks` の完全なリストを示します。

| **名前** | **以前のAEMバージョンに関連** | **移行タイプ** | **詳細** |
|---|---|---|---|
| `Cq561ProjectContentUpgrade` | &lt; 5.6.1 | 即時 |  |
| `Cq60MSMContentUpgrade` | &lt; 6.0 | 即時 | 削除された `LiveRelationShips` からすべての `VersionStorage` を検出し、親に実行プロパティを追加します。 |
| `Cq61CloudServicesContentUpgrade` | &lt; 6.1 | 即時 | デフォルト設定でセキュリティで保護されたクラウドサービスを再構築 |
| `Cq62ConfContentUpgrade` | &lt; 6.2 | 即時 | 次の場所にあるプロパティベースのリンクを削除 **/content** から **/conf** （OSGi メカニズムに置き換え）、対応する OSGi 設定を生成します。 |
| `Cq62FormsContentUpgrade` | &lt; 6.2 | 即時 | merge_preserve の処理により、デフォルトでは保護された拒否ルールが与えられた権限を上書きするので、アップグレード時に並べ替えを行う必要が生じます |
| `CQ62Html5SmartFileUpgrade` | &lt; 6.2 | 即時 | Html5SmartFile ウィジェットを使用するコンポーネントを検出し、コンテンツ内でのコンポーネントの使用を検索し、永続性を再構築し、バイナリを下のレベルに効果的に移動し、コンポーネントレベルに保存しません。 |
| `Cq62ProjectsCodeUpgrade` | &lt; 6.2 | 即時 | 次の場所から古いスタイルのプロジェクトを移動します： **/etc/projects** から **/content/projects** |
| `Cq62TargetCampaignsContentUpgrade` | &lt; 6.2 | 即時 | コンテナレイヤを階層 (Areas) に導入し、参照を調整します。 |
| `Cq62TargetContentUpgrade` | &lt; 6.2 | 即時 | 固定位置名をターゲットコンポーネントに設定します。 |
| `Cq62WorkflowContentUpgrade` | &lt; 6.2 | 即時 | ワークフローの複雑な変換では、6.2 の構造、インスタンス、通知にさかのぼり、**/var/backup** のバックアップの場所から結合し直してモデル化します。 |
| `CQ63AssetsMetadataFormsUpdate` | &lt; 6.3 | 即時 | アセット、カスタムメタデータスキーマ、処理プロファイルを **/apps** から **/conf** およびは、メタデータスキーマおよびメタデータプロファイルフォームを coral2 から coral3 に変換します。 |
| `CQ63AssetsSearchFacetsUpdate` | &lt; 6.3 | 即時 | アセットおよびカスタム検索ファセットを次の場所に移動： **/apps** から **/conf** およびは、メタデータスキーマおよびメタデータプロファイルフォームを coral2 から coral3 に変換します。 |
| `CQ63InboxItemsUpgrade` | &lt; 6.3 | 即時 | インボックス項目を並べ替えるための InboxItems を更新しました（効率的な並べ替えのためのメタデータの調整） |
| `CQ63MetadataSchemaConfigUpdate` | &lt; 6.3 | 即時 | 相対パスを **/conf** 代わりに **/apps** |
| `CQ63MobileAppsNavUpgrade` | &lt; 6.3 | 即時 | ナビゲーション構造の調整 |
| `CQ63MonitoringDashboardsConfigUpdate` | &lt; 6.3 | 即時 | 監視ダッシュボードのカスタム設定を次の場所に移動します： **/libs** および **/apps** |
| `CQ63ProcessingProfileConfigUpdate` | &lt; 6.3 | 即時 | 6.3 以降の構造と一致するように、Assets の processingProfile プロパティ（6.1 まで使用）を変換します。 また、プロファイルの相対パスを **/apps** の代わりに **/conf** に変更します。 |
| `CQ63ToolsMenuEntriesContentUpgrade` | &lt; 6.3 | 即時 | アップグレード時に古いCRXDE Liteと Web コンソールのメニューエントリを削除するアップグレードタスク。 |
| `CQ64CommunitiesConfigsCleanupTask` | &lt; 6.3 | 遅延 | SRP クラウド設定の移行、コミュニティウォッチワード設定、クリーンアップ **/etc/social** および **/etc/enablement** （遅延移行を実行する際は、参照とデータを調整する必要があります。アプリケーション部分は、この構造に依存しなくなりました）。 |
| `CQ64LegacyCloudSettingsCleanupTask` | &lt; 6.4 | 遅延 | クリーンアップ **/etc/cloudsettings** （ContextHub 設定を含む） 最初のアクセス時に設定が自動的に移行されます。 遅延コンテンツ移行を開始し、このコンテンツを **/etc/cloudsettings** アップグレードの前にパッケージで保持し、暗黙的な変換が開始されるように再インストールする必要があります。また、完了後にパッケージを以降にアンインストールする必要もあります。 |
| `CQ64UsersTitleFixTask` | &lt; 6.4 | 遅延 | 従来のタイトル構造をユーザープロファイルノードのタイトルに調整します。 |
| `CQ64CommerceMigrationTask` | &lt; 6.4 | 遅延 | コマースコンテンツを **/etc/commerce** から **/var/commerce** に移行します。移行中にコンテンツが移動され、移動されたコンテンツへの参照が更新されて、新しい場所が反映されます。 |
