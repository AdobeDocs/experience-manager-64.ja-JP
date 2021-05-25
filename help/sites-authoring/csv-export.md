---
title: CSV ファイルへの書き出し
seo-title: CSV ファイルへの書き出し
description: ページの情報をローカルシステムの CSV ファイルに書き出します
seo-description: ページの情報をローカルシステムの CSV ファイルに書き出します
uuid: aa03adac-bbfb-4566-a153-25fe6f6843dd
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: d4473758-674a-42d6-923a-b536f7f9c1f7
exl-id: 52eb9c2f-ce29-4622-8726-802ac40246d4
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 79%

---

# CSV ファイルへの書き出し{#export-to-csv}

**CSV レポートの作成**&#x200B;では、ページの情報をローカルシステムの CSV ファイルに書き出すことができます。

* ダウンロードしたファイルの名前は `export.csv` になります。
* コンテンツは、選択するプロパティによって異なります。
* 書き出しのパスと深さを定義できます。

>[!NOTE]
>
>ブラウザーのダウンロード機能（およびデフォルトのダウンロード先）が使用されます。

CSV の書き出しファイルを作成ウィザードでは、次の要素を選択できます。

* 書き出すプロパティ

   * メタデータ

      * 変更済み
      * 公開済み
   * 分析

      * ページ表示
      * 個別訪問者数
      * ページ滞在時間


* 深さ

   * 親パス
   * 直属の子要素のみ
   * 追加の子のレベル
   * レベル

生成された `export.csv` ファイルは、Excel（または互換性のあるその他のアプリケーション）で開くことができます。

![chlimage_1-58](assets/chlimage_1-58.png)

**CSVの書き出し**&#x200B;を作成オプションは、（リスト表示で）**サイト**&#x200B;コンソールを参照する際に使用できます。これは、**作成**&#x200B;ドロップダウンメニューのオプションです。

![screen_shot_2018-03-21at154719](assets/screen_shot_2018-03-21at154719.png)

CSV の書き出しファイルを作成するには、次の手順を実行します。

1. **サイト**&#x200B;コンソールを開き、必要に応じて必要な場所まで移動します。
1. ツールバーの「**作成** 」を選択し、「**CSVの書き出し**」を選択してウィザードを開きます。

   ![screen_shot_2018-03-21at154758](assets/screen_shot_2018-03-21at154758.png)

1. 書き出す必要があるプロパティを選択します。
1. 「**作成**」を選択します。
