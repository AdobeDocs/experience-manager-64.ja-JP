---
title: AEM Forms Workspace のカスタマイズの一般的な手順
seo-title: Generic steps for AEM Forms workspace customization
description: AEM Forms Workspace ユーザーインターフェイスをカスタマイズする方法。
seo-description: How to get started customizing AEM Forms workspace user interface.
uuid: 555b5039-cd68-4090-8a8f-30b654474f55
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: forms-workspace
discoiquuid: 54326a05-3fb0-4111-a6ec-230b6473052e
exl-id: 2c0dab68-d77e-46fb-832d-90edea510750
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '282'
ht-degree: 49%

---

# AEM Forms Workspace のカスタマイズの一般的な手順に従います。 {#generic-steps-for-aem-forms-workspace-customization}

カスタマイズを実行するための一般的な手順を以下に示します。

1. にアクセスしてCRXDE Liteにログイン `https://[server]:[port]/lc/crx/de/index.jsp`.
1. という名前のフォルダーを作成します。 `ws`時刻 `/apps`（存在しない場合） 「**[!UICONTROL すべて保存]**」をクリックします。
1. 参照先 `/apps/ws`をクリックし、 **[!UICONTROL アクセス制御]** タブをクリックします。
1. 内 **[!UICONTROL アクセス制御]** リスト、クリック **[!UICONTROL +]** をクリックして、新しいエントリを追加します。 もう一度「**[!UICONTROL +]**」をクリックします。
1. を検索して選択します。 **[!UICONTROL PERM_WORKSPACE_USER]** 校長。

   ![HTML Workspace をカスタマイズするための汎用手順の一部として PERM_WORKSPACE_USER プリンシパルを選択します](assets/perm_workspace_user.png)

1. 与える `jcr:read` プリンシパルに対する権限
1. 「**[!UICONTROL すべて保存]**」をクリックします。
1. を `GET.jsp` および `html.jsp`ファイル `/libs/ws`フォルダーを `/apps/ws` フォルダー。
1. を `/libs/ws/locales` フォルダーを `/apps/ws` フォルダー。 「**[!UICONTROL すべて保存]**」をクリックします。
1. の参照と相対パスを更新します。 `GET.jsp` ファイル（下図を参照）を選択し、「 **[!UICONTROL すべて保存]**.

   ```
   <meta http-equiv="refresh" content="0;URL='/lc/apps/ws/index.html'" />
   ```

1. CSS のカスタマイズは以下のようにして実行します。

   1. 次に移動： `/apps/ws` フォルダーを作成し、 `css`.
   1. `css` フォルダに `newStyle.css` という名前の新しいファイルを作成します。
   1. 開く `/apps/ws/html`.jsp と

   ```css
   <link lang="en" rel="stylesheet" type="text/css" href="css/style.css" />
   <link lang="en" rel="stylesheet" type="text/css" href="css/jquery-ui.css"/>
   ```

   コピー先：

   ```css
   <link lang="en" rel="stylesheet" type="text/css" href="../../libs/ws/css/style.css" />
   <link lang="en" rel="stylesheet" type="text/css" href="css/newStyle.css" />
   <link lang="en" rel="stylesheet" type="text/css" href="../../libs/ws/css/jquery-ui.css"/>
   ```

   >[!NOTE]
   >
   >上記のように、newStyle.css のエントリの後ろにユーザー定義された CSS ファイルのエントリを配置します。

1. /apps/ws/html.jsp ファイルで、

   ```css
   <script data-main="js/main" src="js/libs/require/require.js"></script>
   ```

   コピー先：

   ```css
   <script data-main="js/main" src="../../libs/ws/js/libs/require/require.js"></script>
   ```

1. 以下の操作を実行します。

   1. という名前のフォルダーを作成します。 `js`時刻 `/apps/ws`. 「**[!UICONTROL すべて保存]**」をクリックします。
   1. という名前のフォルダーを作成します。 `libs`時刻 `/apps/ws/js`. 「**[!UICONTROL すべて保存]**」をクリックします。
   1. という名前のフォルダーを作成します。 `jqueryui`時刻 `/apps/ws/js/libs`. 「**[!UICONTROL すべて保存]**」をクリックします。
   1. `/libs/ws/js/libs/jqueryui/jquery.ui.datepicker-ja.js` を `/apps/ws/js/libs/jqueryui` にコピーします。「**[!UICONTROL すべて保存]**」をクリックします。

1. HTML のカスタマイズは以下のようにして実行します。

   1. の下 `/apps/ws/js`、という名前のフォルダーを作成します。 `runtime`. 「**[!UICONTROL すべて保存]**」をクリックします。
   1. の下 `/apps/ws/js/runtime`、という名前のフォルダーを作成します。 `templates`. 「**[!UICONTROL すべて保存]**」をクリックします。
   1. `/libs/ws/js/main.js` を `/apps/ws/js/main.js` にコピーします。
   1. /libs/ws/js/registry.jsをにコピーします。 `/apps/ws/js/registry.js`.

1. 「**[!UICONTROL Save All]**」をクリックし、キャッシュをクリアして AEM Forms Workspace を更新します。

   URL にアクセス `https://[server]:[port]/lc/ws` 管理者/パスワードの資格情報を使用してログインします。 ブラウザーはにリダイレクトします。 `https://[server]:[port]/lc/apps/ws/index.html`.
