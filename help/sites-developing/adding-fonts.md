---
title: グラフィックレンダリング用のフォントの追加
seo-title: Adding Fonts for Graphic-Rendering
description: AEM では、コンテンツから動的に取得したテキストを取り込んだグラフィックを生成できます
seo-description: AEM allows you to generate graphics incorporating text dynamically taken from your content
uuid: 67d9b10f-e986-4d29-bde2-10e08075fe17
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: platform
content-type: reference
discoiquuid: 6af48ef5-75e6-4b66-bc0d-ecf254b1c4ef
exl-id: f29868e3-d05c-4898-94d1-0c77ab6b72eb
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '183'
ht-degree: 61%

---

# グラフィックレンダリング用のフォントの追加{#adding-fonts-for-graphic-rendering}

AEM では、コンテンツから動的に取得したテキストを取り込んだグラフィックを生成できます。

その際に、独自のフォントを読み込んで使用することもできます。

現時点で、Java プラットフォームのすべての実装で [TrueType](https://en.wikipedia.org/wiki/Truetype) フォントがサポートされています。

1. CRXDE Liteを開き、プロジェクトアプリケーションフォルダーに移動します。

   `/apps/<your-project>/`

1. の下 `/apps/<your-project>/` 新しいノードを作成します。

   * **名前**：`fonts`
   * **型**：`sling:Folder`

   すべての変更を保存します。

1. WebDAV などを使用して、フォントファイルをこのフォルダー内にコピーします。

   >[!NOTE]
   >
   >リポジトリ内のフォントファイルにはサフィックスが必要です `*.ttf` または `*.TTF`.

1. を更新します。 [OSGi 設定](/help/sites-deploying/configuring-osgi.md) / [Day Commons GFX Font Helper](/help/sites-deploying/osgi-configuration-settings.md).フォントフォルダーにパスを追加します。例： `/apps/<your-project>/fonts`.

1. CRXDE Lite に戻ります。これで、 `.fontlist` 読み込んだフォントの名前を含むフォルダー内のノード。

   これらのフォントは、今後 Java API で使用できます。

Java API でのフォントの使用方法について詳しくは、[Java API の Font クラスに関するドキュメント](https://download.oracle.com/javase/6/docs/api/java/awt/Font.html)を参照してください。
