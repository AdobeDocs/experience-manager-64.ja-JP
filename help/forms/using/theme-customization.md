---
title: テーマのカスタマイズ
seo-title: テーマのカスタマイズ
description: AEM Forms アプリケーションのテーマのカスタマイズ方法
seo-description: AEM Forms アプリケーションのテーマのカスタマイズ方法
uuid: 36632e67-1cc6-416d-ae80-d84bbabab4bd
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: forms-app
discoiquuid: c72f608e-052a-4bf9-b7bc-ddf57483af35
exl-id: fb1e0bec-c943-4468-920d-8ef360a01365
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 57%

---

# テーマのカスタマイズ {#theme-customization}

HTML コードおよび CSS ファイルをカスタマイズし、AEM Forms アプリケーションに組織固有の明確なルック＆フィールを提供することができます。たとえば、タスクまたはスタートポイントの背景色や高さを変更できます。次のことを変更する手順を、以下に例で示します。

* 説明の代わりに手順を表示する
* 表示ルート数
* 背景諧調色

## 手順 {#steps}

1. プロジェクトを開きます。

   * iOSの場合は、Xcodeで`Capture.xcodeproj`を開きます。
   * Android の場合、Eclipse で Android プロジェクトを開きます。
   * Windowsの場合は、Visual Studioで`MWSWindows.sln`を開きます。

1. テンプレートフォルダーに移動します。

   * Xcodeで、 **Capture > www > wsmobile > js > runtime > templates**&#x200B;フォルダーに移動します。
   * Eclipseで、 **assets > www > wsmobile > js > runtime > templates**&#x200B;フォルダーに移動します。
   * Visual Studioで、 **MWSWindows > www > wsmobile > js > runtime > templates**&#x200B;フォルダーに移動します。

1. `template.html`ファイルを開いて編集します。
1. 次の文字列を探します。

   ```
   <%if ( (task.description !== "") && (task.description !== null) && (typeof task.description !== null) && (typeof task.description !== 'undefined') ) {%>
                  <div class="description_details">
                    <%= task.description %>
                  </div>
                 <%} else 
   ```

   `<%`に置き換えます。

1. `template.html` ファイル内の次のコードを探します。

   ```
   <ul id="task_menu_list">
                                   <li class="approve" title="<%= task.availableCommands.directCommands[0]%>" data-routename="<%= task.availableCommands.directCommands[0]%>">
                                       <%= task.availableCommands.directCommands[0]%>
                                   </li>
                                   <li class="reject last" title="<%= task.availableCommands.directCommands[1]%>" data-routename="<%= task.availableCommands.directCommands[1]%>">
                                       <%= task.availableCommands.directCommands[1]%>
                                   </li>
   ```

1. 次の行にコメントをつけ、ファイルを保存します。

   ```
   task.availableCommands.directCommands[1]%>">
   <%= task.availableCommands.directCommands[1]%>
   </li>
   ```

1. css フォルダーに移動します。

   * Xcodeで、 **Capture > www > wsmobile > css**&#x200B;に移動します。
   * Eclipseで、**assets > www > wsmobile > css**&#x200B;に移動します。
   * Visual Studioで、**MWSWindows > www > wsmobile > css**&#x200B;に移動します。

1. `_style.css`ファイルを開いて編集します。
1. 背景画像の場合、 `#323232`を`#fff`に変更します。
1. 変更を保存し、`_style.css`ファイルを閉じます。
1. AEM Forms アプリケーションを開きます。

   AEM Forms アプリケーションには、説明の代わりに手順が表示されるようになっています。
