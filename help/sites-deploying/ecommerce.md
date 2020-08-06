---
title: e コマースの概要
seo-title: e コマースの概要
description: 'AEM の汎用 e コマースは、標準インストールの一部として提供され、e コマースフレームワークのすべての機能を含みます。  '
seo-description: 'AEM の汎用 e コマースは、標準インストールの一部として提供され、e コマースフレームワークのすべての機能を含みます。  '
uuid: 7be42b1e-f1d6-4891-96f8-0133b3a299a1
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: e-commerce
content-type: reference
discoiquuid: cb043066-aefc-4b68-b302-2b5dd710a786
translation-type: tm+mt
source-git-commit: 0a7f40dd692985890c0c51c54a153135d39c7bd8
workflow-type: tm+mt
source-wordcount: '290'
ht-degree: 61%

---


# e コマースの概要{#ecommerce-overview}

AEM の汎用 e コマースは、標準インストールの一部として提供され、e コマースフレームワークのすべての機能を含みます。

アドビでは、2 つのバージョンの Commerce 統合フレームワークを提供しています。

|  | CIF オンプレミス | CIF クラウド |
|-------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------|
| サポートされている AEM バージョン | AEM オンプレミスまたは AMS 6.x | AEM AMS 6.4 および 6.5 |
| バックエンド | - AEM、Java <br> - Monolisic統合、ビルド前のマッピング（テンプレート）<br> - JCRリポジトリ | -Magento <br>- JavaおよびJavaScript <br>- JCRリポジトリにコマースデータが保存されていない |
| フロントエンド | AEM サーバー側によってページをレンダリング | 混在型ページアプリケーション（ハイブリッドレンダリング） |
| 製品カタログ |  — 製品インポーター、エディター、AEMでのキャッシュ <br>-AEMまたはプロキシページを含む通常のカタログ |  — 製品のインポートなし — 汎用テンプレ <br>ート <br>— コネクタを介したオンデマンドデータ |
| スケーラビリティ |  — 数百万個までの製品をサポート可能（使用事例によって異なります） <br> — ディスパッチャーでのキャッシュ |  — ボリュームに制限 <br>なし — ディスパッチャーまたはCDNでのキャッシュ |
| 標準化されたデータモデル | 不可 | あり。Magento GraphQL スキーマ |
| 入手方法 | はい：<br> - SAPCommerce Cloud(AEM 6.4とHybris 5 （デフォルト）をサポートするように更新)、Hybris 4 <br>- SalesforceCommerce Cloud(サポートAEM 6.4をオープンソースにするコネクタ)との互換性を維持 | あり。GitHub 経由のオープンソース。<br>Magento Commerce（Magento 2.3.2（デフォルト）をサポート、Magento 2.3.1 と互換性あり） |
| 用途 | 限定的な使用例： 小さい静的なカタログの読み込みが必要な場合 | ほとんどの使用例で好ましいソリューション |


## その他の実装のデプロイ {#deploying-other-implementations}

* [SAP Commerce Cloud](/help/sites-deploying/sap-commerce-cloud.md)
* [Salesforce Commerce Cloud](https://github.com/adobe/commerce-salesforce)
* [Magento](https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/integrations.html#!AdobeDocs/commerce-cif-documentation/master/integrations/02-AEM-Magento.md)

>[!NOTE]
>
>e コマースの実装の概念および管理について詳しくは、[e コマースの管理](/help/sites-administering/ecommerce.md)を参照してください。
>
>For information about extending eCommerce capabilities, see [Developing eCommerce](/help/sites-developing/ecommerce.md).

