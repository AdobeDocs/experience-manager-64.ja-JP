---
title: ページ分析データの表示
seo-title: Seeing Page Analytics Data
description: ページ分析データを使用すると、ページコンテンツの効果を測定できます。
seo-description: Use page analytics data to gauge the effectiveness of their page content
uuid: 8dda89be-13e3-4a13-9a44-0213ca66ed9c
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.4/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 42d2195a-1327-45c0-a14c-1cf5ca196cfc
exl-id: 6509c0ce-fc3a-4248-8dc7-db10602c30d6
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '441'
ht-degree: 91%

---

# ページ分析データの表示{#seeing-page-analytics-data}

ページ分析データを使用すると、ページコンテンツの効果を測定できます。

## コンソールに表示できる分析結果 {#analytics-visible-from-the-console}

![aa-10](assets/aa-10.png)

ページ分析データはサイトコンソールの[リスト表示](/help/sites-authoring/basic-handling.md#list-view)に表示されます。ページがリスト形式で表示されているとき、デフォルトでは次の列が表示されます。

* ページ表示
* 個別訪問者数
* ページ滞在時間

各列には現在のレポート期間の値が表示され、前回のレポート期間と比較して値が増加したか減少したかも示されます。表示されるデータは 12 時間ごとに更新されます。

>[!NOTE]
>
>更新期間を変更するには、[読み込み間隔を設定](/help/sites-administering/adobeanalytics-connect.md#configuring-the-import-interval)します。

1. **サイト**&#x200B;コンソールを開きます（例：[http://localhost:4502/sites.html/content](http://localhost:4502/sites.html/content)）。
1. ツールバーの右端（右上隅）で、アイコンをクリックまたはタップして、「**リスト表示**」（表示されるアイコンは、[現在の表示](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources)によって異なる）を選択します。

1. もう一度、ツールバーの右端（右上隅）で、アイコンをクリックまたはタップして、「**設定を表示**」を選択します。**列を構成**&#x200B;ダイアログが開きます。必要な変更を加えて、「**更新**」で確定します。

   ![aa-04](assets/aa-04.png)

### レポート期間の選択 {#selecting-the-reporting-period}

サイトコンソールに表示される分析データのレポート期間を次の中から選択します。

* 過去 30 日間 データ
* 過去 90 日間のデータ
* 今年のデータ

現在のレポート期間がサイトコンソールのツールバー（上部のツールバーの右側）に表示されます。ドロップダウンを使用して、必要なレポート期間を選択します。\
![aa-05](assets/aa-05.png)

### 利用できるデータ列の設定 {#configuring-available-data-columns}

analytics-administrators ユーザーグループのメンバーは、作成者が追加の分析列を確認できるようにサイトコンソールを設定できます。

>[!NOTE]
>
>ページのツリーに異なる Adobe Analytics のクラウド設定に関連付けられている子ページがある場合は、そのページで利用できるデータ列を設定できません。

1. リスト表示で、表示セレクター（ツールバーの右側）を使用し、**表示設定**&#x200B;を選択して「**カスタム分析データを追加**」をクリックします。

   ![aa-15](assets/aa-15.png)

1. サイトコンソールで作成者に表示する指標を選択し、「**追加**」をクリックします。

   表示される列は、Adobe Analyticsから取得されます。

   ![aa-16](assets/aa-16.png)

### サイトからコンテンツインサイトを開く {#opening-content-insights-from-sites}

開く [コンテンツインサイト](/help/sites-authoring/content-insights.md) サイトコンソールから、ページの効果をさらに調べます。

1. サイトコンソールで、コンテンツインサイトを表示するページを選択します。
1. ツールバーで、分析と推奨表示アイコンをクリックします。

   ![](do-not-localize/chlimage_1-16.png)

## ページエディターに表示できる分析結果（Activity Map） {#analytics-visible-from-the-page-editor-activity-map}

>[!CAUTION]
>
>Adobe Analytics API 内のセキュリティ変更により、AEM に含まれているバージョンの Activity Map は使用できなくなりました。
>
>この [Adobe Analyticsが提供する ActivityMap プラグイン](https://docs.adobe.com/content/help/ja/analytics/analyze/activity-map/getting-started/get-started-users/activitymap-install.translate.html) 現在はを使用する必要があります。
