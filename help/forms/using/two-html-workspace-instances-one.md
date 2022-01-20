---
title: 2 つの AEM Forms ワークプレースインスタンスを 1 つのサーバー上にホストする
seo-title: Hosting two AEM Forms workspace instances on one server
description: LC 管理者が HTML WS をカスタマイズして 2 つのインスタンスを 1 つのサーバーにホストし、異なる URL を使ってアクセスできるようにする方法。
seo-description: How LC administrators can customize HTML WS to host two instances on a single server accessible via different URLs.
uuid: 0584f512-6b92-4418-b71c-93605cfa1927
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: forms-workspace
discoiquuid: 1254a7c2-2c67-4661-803e-afd53e817916
exl-id: ef2ad8e1-5007-4587-97ca-cf21070be9a6
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '299'
ht-degree: 67%

---

# 2 つの AEM Forms ワークプレースインスタンスを 1 つのサーバー上にホストする {#hosting-two-aem-forms-workspace-instances-on-one-server}

AEM Forms のデフォルトのインストールと設定では、1 つの AEM Forms ワークスペースのみがサーバー上で使用できます。ただし、AEM Forms ワークスペースの 2 つの異なるインスタンスを 1 つの AEM Forms サーバーにホストしたい場合があります。これら 2 つのインスタンスは異なる URL によってアクセス可能です。

AEM Forms 管理者はワークスペースをカスタマイズして、2 つの異なる URL を作成し、 2 つのワークスペースを同じサーバー上で使用できるようにします。このカスタマイズ記事では、2 つのワークスペースが `https://[server]:[port]/lc/ws` および `https://[server]:[port]:/lc/ws2`.

以下の手順に従って AEM Forms ワークスペースを設定します。

1. AEM Forms ワークスペースの dev パッケージをサーバーにインストールします。作成方法については、[dev パッケージ](/help/forms/using/introduction-customizing-html-workspace.md#p-crx-package-p)を参照してください。
1. にアクセスして、CRXDE Liteに管理者としてログインします。 `https://[server]:[port]/lc/crx/de/index.jsp`.
1. /content の node ws をコピーし、それを /content にペーストします。node の名前を ws2 に変更します。「**[!UICONTROL すべて保存]**」をクリックします。このノードのプロパティで、`sling:resourceType` の値を ws2 に変更します。 「**[!UICONTROL すべて保存]**」をクリックします。

1. /libs にあるフォルダー ws を /apps にペーストします。このフォルダーの名前を ws2 に変更します。「**[!UICONTROL すべて保存]**」をクリックします。
1. In `GET.jsp` 時刻 `/apps/ws2`、次のコード変更をおこないます。 次のコードを

   ```
   <html lang="en">
   <head>
       <meta charset="utf-8">
       <title>Workspace Next</title>
       <meta http-equiv="refresh" content="0;URL='/lc/libs/ws/index.html'" /><html lang="en">
   <head>
       <meta charset="utf-8">
       <title>Workspace Next</title>
       <meta http-equiv="refresh" content="0;URL='/lc/libs/ws/index.html'" />
   ```

   次のコードで置き換えます。

   ```
   <html lang="en">
   <head>
       <meta charset="utf-8">
       <title>Workspace Next</title>
       <meta http-equiv="refresh" content="0;URL='/lc/apps/ws2/index.html'" />
   ```

1. In `registry.js` 時刻 `/apps/ws2/js`、テンプレートを参照するようにテンプレートのパスを変更します。 `/apps/ws2/js/runtime/templates`. 次のコードを

   ```css
   "tasklist" : {
   "name": "tasklist",
   "path": "tasklistview",
   "model": "tasklist",
   "template": "text!/lc/libs/ws/js/runtime/templates/tasklist.html",
   "utility": "utility",
   "view": "taskview",
   "errorModel": null
   }
   ```

   次のコードで置き換えます。

   ```css
   "tasklist" : {
   "name": "tasklist",
   "path": "tasklistview",
   "model": "tasklist",
   "template": "text!/lc/apps/ws2/js/runtime/templates/tasklist.html",
   "utility": "utility",
   "view": "taskview",
   "errorModel": null
   }
   ```

1. In `userinfo.js` 時刻 `/apps/ws2/js/runtime/models` および `/apps/ws2/js/runtime/views`，文字列を変更 `/lc/content/ws` から `lc/content/ws2`.

1. In `/apps/ws2/js/runtime/services/service.js`、 `getLocalizationData` 指す機能 `/lc/apps/ws2/Locale.html`.

1. 参照先： `pdf.html` 新しい Workspace のパスを変更 `pdf.html` in `/apps/ws2/js/runtime/views/forms/pdftaskform.js`.

1. 参照先： `pdf.html` 新しい Workspace の、 `pdf.html` および `WsNextAdapter.swf` in `startprocess.html`, `taskdetails.html`、および `processinstancehistory.html` 時刻 `/apps/ws2/js/runtime/templates`.

1. コピー `/etc/map/ws` フォルダーと貼り付け先 `/etc/map`. この新しいフォルダーの名前を ws2 に変更します。「すべて保存」をクリックします。

1. のプロパティ内 `ws2`、値を変更 `sling:redirect` から `content/ws2`.

1. 値の変更 `sling:match` から `^[^/\||]/[^/\||]/ws2$`.
