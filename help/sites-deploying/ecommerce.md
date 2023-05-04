---
title: e コマースの概要
seo-title: eCommerce Overview
description: AEMの汎用 e コマースは、標準インストールの一部として使用でき、e コマースフレームワークの全機能を提供します。
seo-description: AEM generic eCommerce is available as part of the standard installation and provides you with the full functionality of the eCommerce framework.
uuid: 7be42b1e-f1d6-4891-96f8-0133b3a299a1
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: e-commerce
content-type: reference
discoiquuid: cb043066-aefc-4b68-b302-2b5dd710a786
feature: Commerce Integration Framework
exl-id: d84cd0ec-4586-45c1-a07a-a4d50fcbb629
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '302'
ht-degree: 63%

---

# e コマースの概要 {#ecommerce-overview}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

AEMの汎用 e コマースは、標準インストールの一部として使用でき、e コマースフレームワークの全機能を提供します。

アドビでは、2 つのバージョンの Commerce 統合フレームワークを提供しています。

|  | CIF オンプレミス | CIF クラウド |
|-------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------|
| サポートされている AEM バージョン | AEMオンプレミスまたは AMS 6.x | AEM AMS 6.4 および 6.5 |
| バックエンド | - AEM、Java <br> - モノリシック統合、ビルド前のマッピング（テンプレート）<br> - JCR リポジトリ | - Magento <br>- Java と JavaScript <br>- JCR リポジトリにはコマースデータは保存されません |
| フロントエンド | AEMサーバーサイドでレンダリングされたページ | 混在ページアプリケーション（ハイブリッドレンダリング） |
| 製品カタログ | - AEMでの製品インポーター、エディター、キャッシュ <br>- AEM またはプロキシページを含む通常のカタログ | - 製品のインポートなし <br>- 汎用テンプレート <br> - コネクタを介したオンデマンドデータ |
| スケーラビリティ | - 数億個までの製品をサポート可能（ユースケースによって異なる） <br> - Dispatcher でのキャッシュ | - ボリューム制限なし <br>- Dispatcher または CDN でのキャッシュ |
| 標準化されたデータモデル | 不可 | はい、MagentoGraphQLスキーマ |
| 入手方法 | 可：<br> - SAP Commerce Cloud（AEM 6.4 と Hybris 5（デフォルト）をサポートし、Hybris 4 との互換性を維持するように更新された拡張機能）<br>- Salesforce Commerce Cloud（AEM 6.4 をサポートする オープンソースコネクタ） | GitHub を通じてオープンソースで使用可能。<br>Magento Commerce（Magento 2.3.2（デフォルト）をサポート、Magento 2.3.1 と互換性あり） |
| 用途 | 限定的なユースケース：小規模で静的なカタログのインポートが必要なシナリオの場合 | ほとんどの使用例で推奨されるソリューション |


## 他の実装のデプロイ {#deploying-other-implementations}

* [SAP Commerce Cloud ](/help/sites-deploying/sap-commerce-cloud.md)
* [Salesforce Commerce Cloud](https://github.com/adobe/commerce-salesforce)
* [Magento](https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/integrations.html#!AdobeDocs/commerce-cif-documentation/master/integrations/02-AEM-Magento.md)

>[!NOTE]
>
>e コマースの実装の概念および管理について詳しくは、[e コマースの管理](/help/sites-administering/ecommerce.md)を参照してください。
>
>e コマース機能の拡張について詳しくは、[e コマースの開発](/help/sites-developing/ecommerce.md)を参照してください。
