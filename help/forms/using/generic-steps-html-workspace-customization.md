---
title: AEM Forms Workspace のカスタマイズの一般的な手順
seo-title: AEM Forms Workspace のカスタマイズの一般的な手順
description: AEM Forms Workspace ユーザーインターフェイスをカスタマイズする方法。
seo-description: AEM Forms Workspace ユーザーインターフェイスをカスタマイズする方法。
uuid: 555b5039-cd68-4090-8a8f-30b654474f55
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: forms-workspace
discoiquuid: 54326a05-3fb0-4111-a6ec-230b6473052e
exl-id: 2c0dab68-d77e-46fb-832d-90edea510750
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '299'
ht-degree: 52%

---

# AEM Forms Workspace のカスタマイズの一般的な手順に従います。  {#generic-steps-for-aem-forms-workspace-customization}

カスタマイズを実行するための一般的な手順を以下に示します。

1. `https://[server]:[port]/lc/crx/de/index.jsp`にアクセスしてCRXDE Liteにログインします。
1. `ws`という名前のフォルダーが存在しない場合は、`/apps`に作成します。 「**[!UICONTROL すべて保存]**」をクリックします。
1. `/apps/ws`を参照し、「**[!UICONTROL アクセス制御]**」タブに移動します。
1. 「**[!UICONTROL アクセス制御]**」リストで、「**[!UICONTROL +]**」をクリックして新しいエントリを追加します。 もう一度「**[!UICONTROL +]**」をクリックします。
1. **[!UICONTROL PERM_WORKSPACE_USER]**&#x200B;プリンシパルを検索して選択します。

   ![HTML Workspace をカスタマイズするための汎用手順の一部として PERM_WORKSPACE_USER プリンシパルを選択します](assets/perm_workspace_user.png)

1. プリンシパルに`jcr:read`権限を付与します。
1. 「**[!UICONTROL すべて保存]**」をクリックします。
1. `GET.jsp`と`html.jsp`ファイルを`/libs/ws`フォルダーから`/apps/ws`フォルダーにコピーします。
1. `/apps/ws`フォルダーの`/libs/ws/locales`フォルダーをコピーします。 「**[!UICONTROL すべて保存]**」をクリックします。
1. `GET.jsp`ファイル内の参照と相対パスを更新し、「**[!UICONTROL すべて保存]**」をクリックします。

   ```
   <meta http-equiv="refresh" content="0;URL='/lc/apps/ws/index.html'" />
   ```

1. CSS のカスタマイズは以下のようにして実行します。

   1. `/apps/ws`フォルダーに移動し、`css`という名前の新しいフォルダーを作成します。
   1. `css` フォルダに `newStyle.css` という名前の新しいファイルを作成します。
   1. `/apps/ws/html`.jspを開き、

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

   1. `js`という名前のフォルダーを`/apps/ws`に作成します。 「**[!UICONTROL すべて保存]**」をクリックします。
   1. `libs`という名前のフォルダーを`/apps/ws/js`に作成します。 「**[!UICONTROL すべて保存]**」をクリックします。
   1. `jqueryui`という名前のフォルダーを`/apps/ws/js/libs`に作成します。 「**[!UICONTROL すべて保存]**」をクリックします。
   1. `/libs/ws/js/libs/jqueryui/jquery.ui.datepicker-ja.js` を `/apps/ws/js/libs/jqueryui` にコピーします。「**[!UICONTROL すべて保存]**」をクリックします。

1. HTML のカスタマイズは以下のようにして実行します。

   1. `/apps/ws/js`の下に、`runtime`という名前のフォルダーを作成します。 「**[!UICONTROL すべて保存]**」をクリックします。
   1. `/apps/ws/js/runtime`の下に、`templates`という名前のフォルダーを作成します。 「**[!UICONTROL すべて保存]**」をクリックします。
   1. `/libs/ws/js/main.js` を `/apps/ws/js/main.js` にコピーします。
   1. /libs/ws/js/registry.jsを`/apps/ws/js/registry.js`にコピーします。

1. 「**[!UICONTROL Save All]**」をクリックし、キャッシュをクリアして AEM Forms Workspace を更新します。

   URL `https://[server]:[port]/lc/ws`にアクセスし、管理者/パスワードの資格情報を使用してログインします。 ブラウザーは`https://[server]:[port]/lc/apps/ws/index.html`にリダイレクトします。
