---
title: インターフェイスのカラースキームの変更
seo-title: Changing the color scheme of the interface
description: AEM Forms Workspace のユーザーインターフェイス部分のカラースキームを選択的に変更する方法。
seo-description: How to modify the color scheme of AEM Forms workspace user interface portions selectively.
uuid: 32c32f7a-8271-4d2c-8a1f-ad5ab3c90b83
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: forms-workspace
discoiquuid: 18dab82a-badf-4c32-83a2-cd5cb04cae89
exl-id: efbb9a9e-0ddf-49f2-bcb8-14cd0c6de5ee
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 45%

---

# インターフェイスのカラースキームの変更 {#changing-the-color-scheme-of-the-interface}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

AEM Forms Workspace のユーザーインターフェイス部分のカラースキームは、要件に合わせて変更できます。 代表的なカラースキームのカスタマイズの例を以下に示します。 この記事の手順に加えて、「[AEM Forms Workspace のカスタマイズの一般的な手順](/help/forms/using/generic-steps-html-workspace-customization.md)」を参照してください。

## 上部ナビゲーションバー {#top-navigation-bar}

### 背景画像の使用 {#using-background-image}

AEM Forms Workspace の上部にあるナビゲーションバーを更新するには：

1. 背景画像を作成して色を更新します。 ファイルに newBackground.jpg という名前を付けます。
1. WebDAV クライアントを使用して、/apps/ws/images フォルダーに背景画像ファイルをアップロードします。

   >[!NOTE]
   >
   >WebDAV アクセスの詳細については、 [https://dev.day.com/docs/en/crx/current/how_to/webdav_access.html](https://docs.adobe.com/docs/jp/crx/current/how_to/webdav_access.html) を参照してください。

1. 次のスタイルを追加して、 /apps/ws/css/newStyle.cssで新しい背景画像を参照します。

   ```css
   #header {
       background:#292929 url(../images/newBackground.jpg) repeat-x;
   }
   ```

### CSS でのカラープロパティの使用 {#using-color-property-in-css}

1. /apps/ws/css にある newStyle.css に次のスタイルを追加します。

   ```css
   #header {
   background : none;
   background-color: gray;
   }
   ```

## カテゴリコンポーネント {#category-component}

カテゴリコンポーネントは、左パネルでタスクのさまざまなカテゴリを表示します。この色を変更するには、CSS ファイルの`.category`要素で、背景色を定義します。

## タスクコンポーネント {#task-component}

タスクは、TaskList コンポーネントと呼ばれる中央のパネルに表示されます。色を変更するには、スタイルシートにある .task セレクターに関連付けられたスタイルを変更します。
