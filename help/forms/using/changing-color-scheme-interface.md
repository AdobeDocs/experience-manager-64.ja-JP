---
title: インターフェイスのカラースキーム変更
seo-title: Changing the color scheme of the interface
description: AEM Forms Workspace ユーザーインターフェイス部分のカラースキームを選択して変更する方法。
seo-description: How to modify the color scheme of AEM Forms workspace user interface portions selectively.
uuid: 32c32f7a-8271-4d2c-8a1f-ad5ab3c90b83
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: forms-workspace
discoiquuid: 18dab82a-badf-4c32-83a2-cd5cb04cae89
exl-id: efbb9a9e-0ddf-49f2-bcb8-14cd0c6de5ee
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '229'
ht-degree: 68%

---

# インターフェイスのカラースキーム変更 {#changing-the-color-scheme-of-the-interface}

AEM Forms Workspace ユーザーインターフェイス部分のカラースキームを必要に合わせて変更できます。代表的なカラースキームのカスタマイズの例を以下にいくつか示します。この記事で説明する手順に加えて、 [AEM Forms Workspace のカスタマイズの一般的な手順](/help/forms/using/generic-steps-html-workspace-customization.md).

## トップナビゲーションバー {#top-navigation-bar}

### 背景画像の使用 {#using-background-image}

AEM Forms Workspace 上部のナビゲーションバーを更新するには：

1. 背景画像を作成して色を更新します。ファイルに newBackground.jpg と名前を付けます。
1. WebDAV クライアントを使用して背景画像を /apps/ws/images フォルダーにアップロードします。

   >[!NOTE]
   >
   >WebDAV アクセスの詳細については、 [https://dev.day.com/docs/en/crx/current/how_to/webdav_access.html](https://docs.adobe.com/docs/en/crx/current/how_to/webdav_access.html).

1. 次のスタイルを追加することによって、/apps/ws/css/newStyle.css にある新しい背景画像を参照します。

   ```css
   #header {
       background:#292929 url(../images/newBackground.jpg) repeat-x;
   }
   ```

### CSS におけるカラープロパティの使用 {#using-color-property-in-css}

1. /apps/ws/css にある newStyle.css に次のスタイルを追加します。

   ```css
   #header {
   background : none;
   background-color: gray;
   }
   ```

## カテゴリコンポーネント {#category-component}

カテゴリコンポーネントは、左パネルでタスクのさまざまなカテゴリを表示します。 色を変更するには、 `.category` 要素に含める必要があります。

## タスクコンポーネント {#task-component}

タスクは、TaskList コンポーネントと呼ばれる中央のパネルに表示されます。色を変更するには、スタイルシートの.task セレクターに関連付けられたスタイルを変更します。
