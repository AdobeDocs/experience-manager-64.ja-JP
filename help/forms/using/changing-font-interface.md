---
title: インターフェイスのフォントの変更
seo-title: Changing the font on the interface
description: ユーザインターフェイス上のフォントを選択的に変更する方法。
seo-description: How to change the fonts on the user interface selectively.
uuid: d079f656-76f8-4908-9989-dde79e215eb2
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: forms-workspace
discoiquuid: 487e3966-443a-408e-b5af-899fcba6fca6
exl-id: bd7ec9d6-b1d2-4f01-8cef-05e5e1eceda1
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 41%

---

# インターフェイスのフォントの変更 {#changing-the-font-on-the-interface}

AEM Forms Workspace に表示されるフォントを変更できます。 ユーザーインターフェイスの特定のセクションで使用されるフォントは、スタイルシートの対応するセクションで定義されます。 ユーザーインターフェイス上のフォントを選択的に変更できます。

[AEM Forms Workspace のカスタマイズの一般的な手順](/help/forms/using/generic-steps-html-workspace-customization.md)に従います。要件に応じて、CSS、HTML、またはその両方をカスタマイズするための手順に従います。

1. 既存のスタイルのフォントファミリを変更または追加します。
1. フォント要素のフォントファミリインラインを変更またはHTMLします。
1. スタイルを追加し、それをHTML要素に使用します。

例えば、トップナビゲーションバーのアンカーテキストのフォントを「Courier New」に変更するには、次の手順に従います。

1. `https://[server]:[port]/lc/crx/de/index.jsp` にアクセスして CRXDE Lite にログインします。
1. 次のいずれかの操作を行います。

   1. 既存のスタイルのフォントファミリを変更するには、/apps/ws/css にある newStyle.css ファイルに以下を追加します。

      ```css
      #topnav a {
         font-family: "Courier New";
      }
      ```

   1. フォントファミリインラインを HTML 要素に追加するには、`/libs/ws/js/runtime/templates/appnavigation.html` ファイルを `/apps/ws/js/runtime/templates/appnavigation.html` にコピーします。

      /apps/ws/js/runtime/templates/appnavigation.html ファイルを次のようにして更新します。

      ```
      <li class="process"><a href="#" title="<%= $.t('index.header.topnav.startprocess.detail')%>" style="font-family:Courier New;" ><%= $.t('index.header.topnav.startprocess.name')%></a></li>
      <li class="todo"><a href="#/todo" title="<%= $.t('index.header.topnav.todo.detail')%>" style="font-family:Courier New;" ><%= $.t('index.header.topnav.todo.name')%></a></li>
      <li class="track"><a href="#/tracking" title="<%= $.t('index.header.topnav.tracking.detail')%>" style="font-family:Courier New;" ><%= $.t('index.header.topnav.tracking.name')%></a></li>
      <li class="preference"><a href="#/preferences" title="<%= $.t('index.header.topnav.preferences.detail')%>" style="font-family:Courier New;" ><%= $.t('index.header.topnav.preferences.name')%></a></li>
      ```

      編集のため /apps/ws/js/registry.js ファイルを開き、`text!/lc/libs/ws/js/runtime/templates/appnavigation.html` を `text!/lc/apps/ws/js/runtime/templates/appnavigation.html` に置き換えます。

   1. フォントファミリを定義するスタイルを追加するには、 /apps/ws/css にある newStyle.css ファイルに以下を追加します。

      ```css
      .myNewFontStyle a {
         font-family: "Courier New";
      }
      ```

      HTML要素に font-family インラインを追加するには、/apps/ws/js/runtime/templates にある appnavigation.html ファイルに以下を追加します。

      ```css
      <div id="topnav" class="myNewFontStyle">
          <ul>
              <li class="process"><a href="#" title="<%= $.t('index.header.topnav.startprocess.detail')%>" ><%= $.t('index.header.topnav.startprocess.name')%></a></li>
              <li class="todo"><a href="#/todo" title="<%= $.t('index.header.topnav.todo.detail')%>"><%= $.t('index.header.topnav.todo.name')%></a></li>
              <li class="track"><a href="#/tracking" title="<%= $.t('index.header.topnav.tracking.detail')%>" ><%= $.t('index.header.topnav.tracking.name')%></a></li>
              <li class="preference"><a href="#/preferences" title="<%= $.t('index.header.topnav.preferences.detail')%>" ><%= $.t('index.header.topnav.preferences.name')%></a></li>
          </ul>
      </div>
      ```

1. ワークスペースを再起動し、変更を表示するためにブラウザーのキャッシュをクリアします。

![change_font_before](assets/change_font_before.png)
**図：** *フォントをカスタマイズする前の上部ナビゲーションバー*

![change_font_after](assets/change_font_after.png)
**図：** *最初のタブのフォントをカスタマイズした後の上部ナビゲーションバー*
