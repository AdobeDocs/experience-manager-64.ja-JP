---
title: 2 つの AEM Forms ワークプレースインスタンスを 1 つのサーバー上にホストする
seo-title: Hosting two AEM Forms workspace instances on one server
description: LC 管理者がHTMLWS をカスタマイズして、異なる URL を介してアクセス可能な単一のサーバー上で 2 つのインスタンスをホストする方法。
seo-description: How LC administrators can customize HTML WS to host two instances on a single server accessible via different URLs.
uuid: 0584f512-6b92-4418-b71c-93605cfa1927
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: forms-workspace
discoiquuid: 1254a7c2-2c67-4661-803e-afd53e817916
exl-id: ef2ad8e1-5007-4587-97ca-cf21070be9a6
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '335'
ht-degree: 47%

---

# 2 つの AEM Forms ワークプレースインスタンスを 1 つのサーバー上にホストする {#hosting-two-aem-forms-workspace-instances-on-one-server}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

AEM Formsのデフォルトのインストールと設定では、1 つのAEM Forms Workspace のみをサーバー上で使用できます。 ただし、場合によっては、AEM Forms Workspace の 2 つの異なるインスタンスを 1 つのAEM Formsサーバー上でホストする必要があります。 2 つのインスタンスは、異なる URL でアクセスできます。

AEM Formsの管理者は、ワークスペースをカスタマイズして 2 つの異なる URL を作成し、2 つのワークスペースを同じサーバーで使用できるようにします。 このカスタマイズ記事では、 2 つのワークスペースが `https://[server]:[port]/lc/ws` と `https://[server]:[port]:/lc/ws2`でアクセスできることを前提としています。

次の手順に従って、AEM Forms Workspace を設定します。

1. サーバーにAEM Forms Workspace の dev パッケージをインストールします。 詳しくは、 [開発パッケージ](/help/forms/using/introduction-customizing-html-workspace.md#p-crx-package-p)を参照してください。
1. `https://[server]:[port]/lc/crx/de/index.jsp` にアクセスして、管理者として CRXDE Lite にログインします。
1. ノード ws を/content にコピーし、/content に貼り付けます。 ノード名を ws2 に変更します。 「**[!UICONTROL すべて保存]**」をクリックします。このノードのプロパティで、`sling:resourceType` の値を ws2 に変更します。「**[!UICONTROL すべて保存]**」をクリックします。

1. /libs からフォルダー ws をコピーし、/apps に貼り付けます。 フォルダーの名前を ws2 に変更します。 「**[!UICONTROL すべて保存]**」をクリックします。
1. `GET.jsp` にある `/apps/ws2` で、次のコード変更を行います。次を

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

1. `registry.js` にある `/apps/ws2/js` で、テンプレートのパスを、`/apps/ws2/js/runtime/templates` にあるテンプレートを参照するように変更します。次のコードを

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

1. `userinfo.js`にある`/apps/ws2/js/runtime/models`および`/apps/ws2/js/runtime/views`で、文字列を`/lc/content/ws`から`lc/content/ws2`に変更します。

1. `/apps/ws2/js/runtime/services/service.js`で、 `getLocalizationData`関数のパスを`/lc/apps/ws2/Locale.html`に指すように変更します。

1. 新しいワークスペースの`pdf.html`に参照するには、`/apps/ws2/js/runtime/views/forms/pdftaskform.js`にある`pdf.html`のパスを変更します。

1. 新しいワークスペースの`pdf.html`に参照するには、 `startprocess.html`にある`pdf.html`と`WsNextAdapter.swf`、および`/apps/ws2/js/runtime/templates`で`taskdetails.html`と`processinstancehistory.html` のパスを変更します。

1. `/etc/map/ws`フォルダーをコピーし、`/etc/map`にペーストします。新しいフォルダーの名前を ws2 に変更します。 「すべて保存」をクリックします。

1. `ws2`のプロパティで、`sling:redirect`の値を`content/ws2`に変更します。

1. 値を`sling:match`から`^[^/\||]/[^/\||]/ws2$`に変更します。
