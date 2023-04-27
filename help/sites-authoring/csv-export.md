---
title: CSV ファイルへの書き出し
seo-title: Export to CSV
description: ページに関する情報をローカルシステムの CSV ファイルに書き出す
seo-description: Export information about your pages to a CSV file on your local system
uuid: aa03adac-bbfb-4566-a153-25fe6f6843dd
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: d4473758-674a-42d6-923a-b536f7f9c1f7
exl-id: 52eb9c2f-ce29-4622-8726-802ac40246d4
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 60%

---

# CSV ファイルへの書き出し {#export-to-csv}

**CSV の書き出しファイルを作成** では、ページに関する情報をローカルシステムの CSV ファイルに書き出すことができます。

* ダウンロードしたファイルの名前は `export.csv` になります。
* コンテンツは、選択するプロパティによって異なります。
* 書き出しのパスと深さを定義できます。

>[!NOTE]
>
>ブラウザーのダウンロード機能（およびデフォルトのダウンロード先）が使用されます。

CSV の書き出しファイルを作成ウィザードでは、次の要素を選択できます。

* 書き出すプロパティ

   * メタデータ

      * 変更
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

作成 **CSV の書き出し** オプションは **サイト** コンソール（リスト表示）:これは、 **作成** ドロップダウンメニュー：

![screen_shot_2018-03-21at154719](assets/screen_shot_2018-03-21at154719.png)

CSV の書き出しファイルを作成するには、次の手順を実行します。

1. **サイト**&#x200B;コンソールを開き、必要に応じて必要な場所まで移動します。
1. ツールバーで、「 」を選択します。 **作成** その後 **CSV の書き出し** ウィザードを開くには、次の手順に従います。

   ![screen_shot_2018-03-21at154758](assets/screen_shot_2018-03-21at154758.png)

1. 書き出す必要のあるプロパティを選択します。
1. 「**作成**」を選択します。
