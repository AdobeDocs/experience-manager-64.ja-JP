---
title: 新しいログイン画面の作成
seo-title: Creating a new login screen
description: AEM Forms Workspace または Forms Manager を例にした、LiveCycle モジュールのログインページの変更方法。
seo-description: How-to modify the login page of LiveCycle modules, for example of AEM Forms workspace or Forms Manager.
uuid: c7643f87-4a08-4c63-b87c-f987dbe18ece
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: forms-workspace
discoiquuid: cfaa6b49-3fd0-4c08-84a2-e86c7e7e3532
exl-id: caa4f835-c353-49d5-b18c-4d0538c1136f
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '468'
ht-degree: 61%

---

# 新規ログイン画面の作成 {#creating-a-new-login-screen}

AEM Forms ログイン画面を使用するすべての AEM Forms モジュールのログイン画面を変更することができます。例えば、変更すると Forms Manager および AEM Forms Workspace の両方のログイン画面に影響が及びます。

## 前提条件 {#prerequisite}

1. 次の場所にログイン： `/lc/crx/de` 管理者権限を持つ。
1. 次のアクションを実行します。

   1. 階層構造をレプリケートします。/ `/libs/livecycle/core/content` 時刻 `/apps/livecycle/core/content`. 同じ（ノード/フォルダー）プロパティおよびアクセス制御を保持します。
   1. 次の内容フォルダーをコピーします。から `/libs/livecycle/core` から `/apps/livecycle/core`.
   1. のコンテンツを削除 `/apps/livecycle/core` フォルダー。

1. 次の操作を実行します。

   1. 階層構造をレプリケートします。/ `/libs/livecycle/core/components/login` 時刻 `/apps/livecycle/core/components/login`. 同じ（ノード/フォルダー）プロパティおよびアクセス制御を保持します。
   1. components フォルダーをコピーします。から `/libs/livecycle/core` から `/apps/livecycle/core`.
   1. フォルダーのコンテンツを削除します。 `/apps/livecycle/core/components/login`.

## 新しいロケールの追加 {#adding-a-new-locale}

1. を `i18n` フォルダー：

   * コピー元：`/libs/livecycle/core/components/login`
   * コピー先：`/apps/livecycle/core/components/login`

1. 内のすべてのフォルダーを削除 `i18n` ただ一人だけは `en`.
1. フォルダー `en` で、以下のアクションを実行します。

   1. フォルダーの名前をサポートするロケール名に変更します。（例：`ar`）。
   1. プロパティを変更します。 `jcr:language` 値 `ar`( `ar` フォルダー )。

   >[!NOTE]
   >
   >`ar-DZ` のようにロケールが言語と国コードの組み合わせである場合は、フォルダー名とプロパティ値を `ar-DZ` に変更します。

1. コピー `login.jsp`:

   * コピー元：`/libs/livecycle/core/components/login`
   * コピー先：`/apps/livecycle/core/components/login`

1. 次のコードのスニペットを `/apps/livecycle/core/components/login/login.jsp`:

   ***ロケールが言語コードである場合***

   ```
   String browserLocale = "en";
       for(int i=0; i<locales.length; i++)
       {
           String prioperty = locales[i];
           if(prioperty.trim().startsWith("en")) {
               browserLocale = "en";
               break;
           }
           if(prioperty.trim().startsWith("de")){
               browserLocale = "de";
               break;
           }
           if(prioperty.trim().startsWith("ja")){
               browserLocale = "ja";
               break;
           }
           if(prioperty.trim().startsWith("fr")){
               browserLocale = "fr";
               break;
           }
       }
   
   To
   
   String browserLocale = "en";
       for(int i=0; i<locales.length; i++)
       {
           String prioperty = locales[i];
           if(prioperty.trim().startsWith("ar")) {
               browserLocale = "ar";
               break;
           }
           if(prioperty.trim().startsWith("en")) {
               browserLocale = "en";
               break;
           }
           if(prioperty.trim().startsWith("de")){
               browserLocale = "de";
               break;
           }
           if(prioperty.trim().startsWith("ja")){
               browserLocale = "ja";
               break;
           }
           if(prioperty.trim().startsWith("fr")){
               browserLocale = "fr";
               break;
           }
       }
   ```

   ***ロケールが言語-国コードである場合***

   ```
   String browserLocale = "en";
       for(int i=0; i<locales.length; i++)
       {
           String prioperty = locales[i];
           if(prioperty.trim().startsWith("en")) {
               browserLocale = "en";
               break;
           }
           if(prioperty.trim().startsWith("de")){
               browserLocale = "de";
               break;
           }
           if(prioperty.trim().startsWith("ja")){
               browserLocale = "ja";
               break;
           }
           if(prioperty.trim().startsWith("fr")){
               browserLocale = "fr";
               break;
           }
       }
   
   To
   
   String browserLocale = "en";
       for(int i=0; i<locales.length; i++)
       {
           String prioperty = locales[i];
           if(prioperty.trim().equalsIgnoreCase("ar-DZ")) {
               browserLocale = "ar-DZ";
               break;
           }
           if(prioperty.trim().startsWith("en")) {
               browserLocale = "en";
               break;
           }
           if(prioperty.trim().startsWith("de")){
               browserLocale = "de";
               break;
           }
           if(prioperty.trim().startsWith("ja")){
               browserLocale = "ja";
               break;
           }
           if(prioperty.trim().startsWith("fr")){
               browserLocale = "fr";
               break;
           }
       }
   ```

   ***デフォルトのロケールを変更するには***

   ```
   String browserLocale = "en";
   for(int i=0; i<locales.length; i++)
   
   To
   
   String browserLocale = "ar";
   for(int i=0; i<locales.length; i++)
   ```

## 新しいテキストの追加、または既存のテキストの変更 {#adding-new-text-or-modifying-existing-text}

1. コピー `i18n` フォルダー：

   * コピー元：`/libs/livecycle/core/components/login`
   * コピー先：`/apps/livecycle/core/components/login`

1. ここで、テキストを変更するノード（該当するロケールコードフォルダの下）のプロパティ `sling:message` の値を変更します。翻訳は、ノードのプロパティ `sling:key` の値に示されているキーを介して行われます。
1. 新しいキーと値のペアを追加するには、次のアクションを実行します。次に続くスクリーンショットの例を確認してください。

   1. `sling:MessageEntry` タイプのノードを作成するか、またはすべてのロケールフォルダーの下で既存のノードをコピーして名前を変更します。
   1. コピー `login.jsp` :

      * コピー元：`/libs/livecycle/core/components/login`
      * コピー先：`/apps/livecycle/core/components/login`
   1. 変更 `/apps/livecycle/core/components/login/login.jsp` 新しく追加したテキストを取り込む。

   ![キャプチャ](assets/capture.png)

   ```
   div class="loginContent">
                       <span class="loginFlow"></span>
                       <span class="loginVersion"><%= i18n.get("Version: 11.0.0") %></span>
                       <span class="loginTitle"><%= i18n.get("Login") %></span>
                       <% if (loginFailed) {%>
   
   To
   
   div class="loginContent">
                       <span class="loginFlow"></span>
                       <span class="loginVersion"><%= i18n.get("My Welcome Message") %></span>
                       <span class="loginVersion"><%= i18n.get("Version: 11.0.0") %></span>
                       <span class="loginTitle"><%= i18n.get("Login") %></span>
                       <% if (loginFailed) {%>
   ```

## 新しいスタイルの追加、または既存のスタイルの変更 {#adding-new-style-or-modifying-existing-style}

1. コピー `login` ノード：

   * コピー元：`/libs/livecycle/core/content`
   * コピー先：`/apps/livecycle/core/content`

1. ファイルを削除 `login.js` および `jquery-1.8.0.min.js`ノードから `/apps/livecycle/core/content/login.`
1. CSS ファイルのスタイルを変更します。
1. 新しいスタイルを追加するには：

   1. 新しいスタイルの追加先 `/apps/livecycle/core/content/login/login.css`
   1. コピー `login.jsp`

      * コピー元：`/libs/livecycle/core/components/login`
      * コピー先：`/apps/livecycle/core/components/login`
   1. 変更 `/apps/livecycle/core/components/login/login.jsp` 新しく追加されたスタイルを組み込む。


1. 次に例を示します。

   * 以下をに追加します。 `/apps/livecycle/core/content/login/login.css`.

   ```css
   .newLoginContentArea {
    width: 700px;
    padding: 100px 0px 0px 100px;
   }
   ```

   * /apps/livecycle/core/components/login.jsp で次を変更します。

   ```
   <div class="loginContentArea">
   
   To
   
   <div class="newLoginContentArea">
   ```

>[!NOTE]
>
>既存の画像が `/apps/livecycle/core/content/login` ( コピー元： `/libs/livecycle/core/content/login`) が削除され、対応する参照が CSS から削除されます。

## 新しい画像の追加 {#add-new-images}

1. 新しいスタイルの追加または既存のスタイルの変更の手順に従います（前述）。
1. に新しい画像を追加 `/apps/livecycle/core/content/login`. 画像を追加するには：

   1. WebDAV クライアントをインストールします。
   1. に移動します。 `/apps/livecycle/core/content/login` フォルダー、webDAV クライアントを使用。 詳しくは、以下を参照してください。 [https://dev.day.com/docs/en/crx/current/how_to/webdav_access.html](https://docs.adobe.com/docs/en/crx/current/how_to/webdav_access.html).
   1. 新しい画像を追加します。

1. に新しいスタイルを追加 `/apps/livecycle/core/content/login/login.css,` ～に追加された新しい画像に対応する `/apps/livecycle/core/content/login`.
1. で新しいスタイルを使用 `login.jsp` 時刻 `/apps/livecycle/core/components`.
1. 以下に例を示します。

   * `/apps/livecycle/core/content/login/login.css` に次の内容を追加します

   ```css
   .newLoginContainerBkg {
    background-image: url(my_Bg.gif);
    background-repeat: no-repeat;
    background-position: left top;
    width: 727px;
   }
   ```

   * /apps/livecycle/core/components/login.jsp で次を変更します。

   ```
   <div class="loginContainerBkg">
   
   To
   
   <div class="newLginContainerBkg">
   ```
