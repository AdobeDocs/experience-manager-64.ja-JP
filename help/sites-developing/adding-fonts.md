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
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 87%

---

# グラフィックレンダリング用のフォントの追加{#adding-fonts-for-graphic-rendering}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

AEM では、コンテンツから動的に取得したテキストを取り込んだグラフィックを生成できます.

その際に、独自のフォントを読み込んで使用することもできます。

現時点で、Java プラットフォームのすべての実装で [TrueType](https://ja.wikipedia.org/wiki/TrueType) フォントがサポートされています。

1. CRXDE Lite を開き、次の場所にあるプロジェクトアプリケーションフォルダーに移動します。

   `/apps/<your-project>/`

1. `/apps/<your-project>/` の下に、新しいノードを作成してください。

   * **名前**：`fonts`
   * **型**：`sling:Folder`

   すべての変更を保存します。

1. WebDAV などを使用して、フォントファイルをこのフォルダー内にコピーします。

   >[!NOTE]
   >
   >リポジトリ内のフォントファイルのサフィックスは、`*.ttf` または `*.TTF` である必要があります。

1. [Day Commons GFX Font Helper](/help/sites-deploying/osgi-configuration-settings.md) の [OSGi 設定](/help/sites-deploying/configuring-osgi.md)を更新します。フォントフォルダーへのパス（`/apps/<your-project>/fonts`）を追加します。

1. CRXDE Lite に戻ります。読み込んだフォントの名前を含むフォルダー内に、`.fontlist`ノードが表示されます。

   これらのフォントは、今後 Java API で使用できます。

Java API でのフォントの使用方法について詳しくは、[Java API の Font クラスに関するドキュメント](https://docs.oracle.com/javase/6/docs/api/java/awt/Font.html)を参照してください。
