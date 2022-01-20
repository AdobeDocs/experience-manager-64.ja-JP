---
title: テーマのカスタマイズ
seo-title: Theme Customization
description: AEM Forms アプリケーションのテーマのカスタマイズ方法
seo-description: How to customize the theme of your AEM Forms app.
uuid: 36632e67-1cc6-416d-ae80-d84bbabab4bd
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: forms-app
discoiquuid: c72f608e-052a-4bf9-b7bc-ddf57483af35
exl-id: fb1e0bec-c943-4468-920d-8ef360a01365
source-git-commit: 2208d23985ebd913b6aa9dee3bf16ce7529a8fa6
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 55%

---

# テーマのカスタマイズ {#theme-customization}

HTML コードおよび CSS ファイルをカスタマイズし、AEM Forms アプリケーションに組織固有の明確なルック＆フィールを提供することができます。たとえば、タスクまたはスタートポイントの背景色や高さを変更できます。次のことを変更する手順を、以下に例で示します。

* 説明の代わりに手順を表示する
* 表示ルート数
* 背景諧調色

## 手順 {#steps}

1. プロジェクトを開きます。

   * iOSの場合は、を開きます。 `Capture.xcodeproj` Xcode 内
   * Android の場合、Eclipse で Android プロジェクトを開きます。
   * Windows の場合は、を開きます。 `MWSWindows.sln` Visual Studio 内。

1. テンプレートフォルダーに移動します。

   * Xcode で、 **Capture > www > wsmobile > js > runtime > templates** フォルダー。
   * Eclipse で、 **assets > www > wsmobile > js > runtime > templates** フォルダー。
   * Visual Studio で、 **MWSWindows > www > wsmobile > js > runtime > templates** フォルダー。

1. を開きます。 `template.html` ファイルを編集します。
1. 次の文字列を探します。

   ```
   <%if ( (task.description !== "") && (task.description !== null) && (typeof task.description !== null) && (typeof task.description !== 'undefined') ) {%>
                  <div class="description_details">
                    <%= task.description %>
                  </div>
                 <%} else 
   ```

   次で置き換えます。 `<%`.

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

   * Xcode で、 **Capture > www > wsmobile > css**.
   * Eclipse で、に移動します。 **assets > www > wsmobile > css**.
   * Visual Studio で、に移動します。 **MWSWindows > www > wsmobile > css**.

1. を開きます。 `_style.css` ファイルを編集します。
1. 背景画像の場合は、 `#323232` から `#fff`.
1. 変更を保存して閉じます `_style.css` ファイル。
1. AEM Forms アプリケーションを開きます。

   AEM Forms アプリケーションには、説明の代わりに手順が表示されるようになっています。
