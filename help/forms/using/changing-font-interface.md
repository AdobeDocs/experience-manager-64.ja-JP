---
title: インターフェイスのフォントの変更
seo-title: インターフェイスのフォントの変更
description: ユーザーインタフェイス上でフォントを選択して変更する方法。
seo-description: ユーザーインタフェイス上でフォントを選択して変更する方法。
uuid: d079f656-76f8-4908-9989-dde79e215eb2
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: forms-workspace
discoiquuid: 487e3966-443a-408e-b5af-899fcba6fca6
exl-id: bd7ec9d6-b1d2-4f01-8cef-05e5e1eceda1
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '294'
ht-degree: 73%

---

# インターフェイスのフォントの変更  {#changing-the-font-on-the-interface}

AEM Forms Workspace に表示されているフォントを変更することができます。ユーザーインターフェイスの特定のセクションで使用されているフォントは、スタイルシートの対応するセクションに定義されています。フォントは選択的にユーザーインタフェイス上で変更することができます。

[AEM Forms Workspaceのカスタマイズの一般的な手順](/help/forms/using/generic-steps-html-workspace-customization.md)に従い、要件に応じて、CSS、HTMLまたはその両方をカスタマイズする手順に従います。

1. 既存のスタイルのフォントファミリを変更または追加します。
1. HTML 要素でフォントファミリインラインを変更または追加します。
1. スタイルを追加して HTML 要素で使用します。

例えば、トップナビゲーションバーのアンカーテキストのフォントを「Courier New」に変更するには、次の手順に従います。

1. `https://[server]:[port]/lc/crx/de/index.jsp`にアクセスしてCRXDE Liteにログインします。
1. 次のいずれかの操作をおこないます。

   1. 既存のスタイルでフォントファミリーを変更するには、/apps/ws/css にある newStyle.css ファイルに以下を追加します。

      ```css
      #topnav a {
         font-family: "Courier New";
      }
      ```

   1. フォントファミリインラインをHTML要素に追加するには、`/libs/ws/js/runtime/templates/appnavigation.html`ファイルを`/apps/ws/js/runtime/templates/appnavigation.html`にコピーします。

      /apps/ws/js/runtime/templates/appnavigation.html ファイルを次のようにして更新します。

      ```
      <li class="process"><a href="#" title="<%= $.t('index.header.topnav.startprocess.detail')%>" style="font-family:Courier New;" ><%= $.t('index.header.topnav.startprocess.name')%></a></li>
      <li class="todo"><a href="#/todo" title="<%= $.t('index.header.topnav.todo.detail')%>" style="font-family:Courier New;" ><%= $.t('index.header.topnav.todo.name')%></a></li>
      <li class="track"><a href="#/tracking" title="<%= $.t('index.header.topnav.tracking.detail')%>" style="font-family:Courier New;" ><%= $.t('index.header.topnav.tracking.name')%></a></li>
      <li class="preference"><a href="#/preferences" title="<%= $.t('index.header.topnav.preferences.detail')%>" style="font-family:Courier New;" ><%= $.t('index.header.topnav.preferences.name')%></a></li>
      ```

      /apps/ws/js/registry.jsファイルを編集用に開き、`text!/lc/libs/ws/js/runtime/templates/appnavigation.html`を`text!/lc/apps/ws/js/runtime/templates/appnavigation.html`に置き換えます。

   1. フォントファミリを定義するスタイルを追加するには、/apps/ws/css にある newStyle.css ファイルに以下を追加します。

      ```css
      .myNewFontStyle a {
         font-family: "Courier New";
      }
      ```

      フォントファミリインラインを HTML 要素に追加するには、/apps/ws/js/runtime/templates にある appnavigation.html ファイルに以下を追加します。

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

1. Workspace を再起動して変更が表示されるようにブラウザのキャッシュをクリアします。

![change_font_](assets/change_font_before.png)
**beforeFigure:** *フォントをカスタマイズする前の上部ナビゲーションバー*

![change_font_](assets/change_font_after.png)
**afterFigure:** *最初のタブのフォントをカスタマイズした後の上部ナビゲーションバー*
