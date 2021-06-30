---
cloud: Experience Cloud
product: adobe experience manager
solution: Experience Manager, Experience Manager Sites, Experience Manager 6.4
audience: end-user
user-guide-title: AEM 6.4 デプロイガイド
breadcrumb-title: デプロイガイド
user-guide-description: Adobe Managed Services クラウドデプロイメントを含む、Adobe Experience Manager 6.4 のインストール、デプロイメント、およびアーキテクチャについて詳しく説明します。
feature: デプロイ
role: Architect
source-git-commit: 1ecb63f849f9f6167dddd4053267ae89577659fc
workflow-type: tm+mt
source-wordcount: '357'
ht-degree: 93%

---


# AEM 6.4デプロイユーザーガイド {#deploying}

+ [デプロイユーザーガイド](home.md)
+ AEM プラットフォームの概要 {#introduction}
   + [AEM プラットフォームの概要](platform.md)
   + [技術要件](technical-requirements.md)
   + [AEM 6.4 のストレージ要素](storage-elements-in-aem-6.md)
   + [MongoDB を備えた AEM](aem-with-mongodb.md)
+ AEM のデプロイ {#deploying}
   + [デプロイとメンテナンス](deploy.md)
   + [推奨されるデプロイメント](recommended-deploys.md)
   + [アプリケーションサーバーのインストール](application-server-install.md)
   + [カスタムスタンドアロンインストール](custom-standalone-install.md)
   + [コマンドラインによる起動と停止](command-line-start-and-stop.md)
   + [AEM 6 でのノードストアとデータストアの設定](data-store-config.md)
   + [リビジョンクリーンアップ](revision-cleanup.md)
   + [TarMK コールドスタンバイによる AEM の実行方法](tarmk-cold-standby.md)
   + [AEM 6.4 の RDBMS サポート](rdbms-support-in-aem.md)
   + [Oak クエリとインデックス作成](queries-and-indexing.md)
   + [Oak-run Jar を使用したインデックス作成](indexing-via-the-oak-run-jar.md)
   + [oak-run.jar でのインデックス作成の使用例](oak-run-indexing-usecases.md)
   + [Oak インデックスのトラブルシューティング](troubleshooting-oak-indexes.md)
   + [集計した使用状況の統計の収集をオプトインする方法](opt-in-aggregated-usage-statistics.md)
   + [トラブルシューティング](troubleshooting.md)
+ AEM の設定 {#configuring}
   + [設定の基本概念](configuring.md)
   + [ログ](configure-logging.md)
   + [OSGi の設定](configuring-osgi.md)
   + [OSGi 設定](osgi-configuration-settings.md)
   + [実行モード](configure-runmodes.md)
   + [Web コンソール](web-console.md)
   + [レプリケーション](replication.md)
   + [相互 SSL を使用したレプリケーション](mssl-replication.md)
   + [レプリケーションのトラブルシューティング](troubleshoot-rep.md)
   + [静的オブジェクトの有効期限](expiration-static-objects.md)
   + [バージョンのパージ](version-purging.md)
   + [AEM インスタンスの監視および保守](monitoring-and-maintaining.md)
   + [ジョブのオフロード](offloading.md)
   + [シングルサインオン](single-sign-on.md)
   + [リソースマッピング](resource-mapping.md)
   + [HTTP over SSL の有効化](https://experienceleague.adobe.com/docs/experience-manager-64/deploying/configuring/ssl-by-default.html)
   + [整合性チェックとトラバーサルチェック](consistency-check.md)
   + [パフォーマンスガイドライン](performance-guidelines.md)
   + [パフォーマンスの最適化](configuring-performance.md)
   + [アセットパフォーマンスガイド](assets-performance-sizing.md)
   + [設定方法に関する記事](ht-deploy.md)
   + [Geometrixx サイトの削除](removing-the-geometrixx-sites.md)
   + [Webコンソールの設定](configuring-web-console.md)
+ AEM 6.4 へのアップグレード {#upgrading}
   + [AEM 6.4 へのアップグレード](upgrade.md)
   + [アップグレードの計画](upgrade-planning.md)
   + [パターン検出を使用したアップグレードの複雑性の評価](pattern-detector.md)
   + [AEM 6.4 における後方互換性](backward-compatibility.md)
   + [アップグレード手順](upgrade-procedure.md)
   + [オフラインでのインデックス再作成を使用したアップグレード中のダウンタイムの削減](upgrade-offline-reindexing.md)
   + [インプレースアップグレードの実行](in-place-upgrade.md)
   + [遅延コンテンツ移行](lazy-content-migration.md)
   + [CRX2Oak 移行ツールの使用](using-crx2oak.md)
   + [アップグレード前のメンテナンスタスク](pre-upgrade-maintenance-tasks.md)
   + [アップグレード後のチェックおよびトラブルシューティング](post-upgrade-checks-and-troubleshooting.md)
   + [カスタム検索フォームのアップグレード](upgrading-custom-search-forms.md)
   + [持続可能なアップグレード](sustainable-upgrades.md)
   + [コードのアップグレードとカスタマイズ](upgrading-code-and-customizations.md)
   + [アプリケーションサーバーのインストール環境のアップグレード手順](app-server-upgrade.md)
   + [アップグレード後にアンインストールされる廃止されたバンドルの一覧](obsolete-bundles.md)
+ リポジトリーの再構築 {#restructuring}
   + [AEM 6.4 におけるリポジトリの再構築](repository-restructuring.md)
   + [AEM 6.4 における共通リポジトリの再構築](all-repository-restructuring-in-aem-6-4.md)
   + [AEM 6.4 における Sites リポジトリの再構築](sites-repository-restructuring-in-aem-6-4.md)
   + [AEM 6.4 における Assets リポジトリの再構築](assets-repository-restructuring-in-aem-6-4.md)
   + [AEM 6.4 での Dynamic Media リポジトリの再構築](dynamicmedia-repository-restructuring-in-aem-6-4.md)
   + [AEM 6.4 における Forms リポジトリの再構築](forms-repository-restructuring-in-aem-6-4.md)
   + [AEM 6.4 における e コマースリポジトリの再構築](ecommerce-repository-restructuring-in-aem-6-4.md)
   + [6.4 における AEM Communities のリポジトリ再構築](communities-repository-restructuring-in-aem-6-4.md)
+ e コマース {#ecommerce}
   + [e コマースの概要](ecommerce.md)
   + [SAP Commerce Cloud](sap-commerce-cloud.md)
   + [Salesforce Commerce Cloud](https://github.com/adobe/commerce-salesforce)
   + [Magento](https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/integrations.html#!AdobeDocs/commerce-cif-documentation/master/integrations/02-AEM-Magento.md)
+ ベストプラクティス {#practices}
   + [デプロイのベストプラクティス](best-practices.md)
   + [パフォーマンスツリー](performance-tree.md)
   + [パフォーマンステストに関するベストプラクティス](best-practices-for-performance-testing.md)
   + [クエリとインデックスに関するベストプラクティス](best-practices-for-queries-and-indexing.md)
   + [顧客向けのユーザーインターフェイスの推奨事項](ui-recommendations.md)
   + [パフォーマンスとスケーラビリティ](performance.md)


<!--

To be removed:
[Quickstart for AEM Screens](setting-up-a-basic-project-screens.md)
[Device Control Center](device-control-center.md)
[repository-restructuring-in-aem64](repository-restructuring-in-aem64.md)
[Web Console] (configuring-web-console.md)
[Configuring and Deploying AEM Screens](configuring-screens-introduction.md)
[Kickstart Guide](kickstart-for-aem-screens.md)
/help/sites/deploying/using/performance-lp.md
/help/sites-deploying/do-not-delete-performance-guidelines-pdf.md
/help/sites-deploying/removing-the-geometrixx-sites.md
/help/sites-deploying/consistency-check.md

Redirects:
[(Enabling HTTP Over SSL)](config-ssl.md) redirect to /content/help/en/experience-manager/6-4/sites-administering/ssl-by-default
-->
