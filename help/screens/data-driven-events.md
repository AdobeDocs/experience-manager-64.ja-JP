---
title: データ駆動型イベント
seo-title: データ駆動型イベント
description: 'null'
seo-description: 'null'
page-status-flag: never-activated
uuid: 138ceff2-84a2-47f2-981a-755522502c16
contentOwner: jsyal
discoiquuid: b662831c-8cb0-48d8-9b4b-cc11a573d1b5
translation-type: tm+mt
source-git-commit: c8694726dc29b391a157db3ef230f21517c957bd

---


# データ駆動型イベント{#data-driven-events}

デジタルサイネージでは、データ駆動型イベントは、デジタルメニューおよびビデオウォールをインタラクティブに使用することで、情報をリアルタイムに伝えることができます。データ駆動型イベントでユーザー体験を最大化できます。

## データ駆動型イベントに対する Context Hub の使用 {#using-context-hub-for-data-driven-events}

AEM Screens では、Context Hub を使用してデータ駆動型イベントを実現します。Context Hub ではリアルタイムに使用できます。

### データ駆動型イベントの分類 {#categorizing-data-driven-events}

データ駆動型イベントは、次の 4 つの異なるカテゴリに分類されます。

* Data in Operational
* Data in Presentation
* Data out Actionable
* Data out Presentational

#### Data in Operational {#data-in-operational}

これはさらに Channel Interrupt と Placeholder に分類されます。

#### Data in Presentation {#data-in-presentation}

データは、一時チャネルで実行され、トリガー後、チャネル内のアセットを変更します。

#### Data out Actionable {#data-out-actionable}

コマンドが液晶画面に送信されると、画面のオンおよびオフが切り替わります（例えば、画面の明るさやボリュームなど）。

#### Data out Presentational {#data-out-presentational}

フィードバックループに情報を収集するグラフ。分析に使用され、イベントを評価および通知します。
