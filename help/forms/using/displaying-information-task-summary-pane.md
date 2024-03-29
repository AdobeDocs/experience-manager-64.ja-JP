---
title: タスクの概要ペインでの情報の表示
seo-title: Displaying information in the Task Summary pane
description: AEM Forms Workspace では、タスクの概要ペインを設定して、タスクを要約したり、他の Web ページを表示したりできます。
seo-description: In AEM Forms workspace, a Task Summary pane can be configured to summarize the task or display any other web page.
uuid: 2fcc3d9f-0ec2-4250-8dc1-9746fd72ea60
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: forms-workspace
discoiquuid: 90d0f584-b598-4b21-85d7-31da5f13d404
exl-id: cb9de2d7-04ad-4221-8db7-403464c9888b
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '313'
ht-degree: 41%

---

# タスクの概要ペインでの情報の表示 {#displaying-information-in-the-task-summary-pane}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

AEM Forms Workspace でタスクを開くと、タスクの概要ペインにタスクの概要が表示されます。 タスクに関するこの追加の関連情報により、AEM Forms Workspace のエンドユーザーにとってより多くの価値がもたらされます。

AEM Forms ワークスペースでは、タスクの概要ペインで選択した web ページを表示できます。Workbench を使用してタスクの概要ペインを表示するためのプロセスを作成することができます。

1. Workbench でタスクの割り当てプロセスを作成します。 「Assign Task」操作の詳細については、「Service Reference」( [Workbench ヘルプ](https://help.adobe.com/ja_JP/AEMForms/6.1/WorkbenchHelp/).

   >[!NOTE]
   >
   >TaskSummary URL が存在する場合は、デフォルトでは、フォームビューではなくタスクの概要ビューが開きます。 この場合、ユーザーが「タスクを割り当て」で「最大化モードでフォームを開く」オプションを有効にしても、フォームは最大化モードで開きません。

1. 「タスクの概要 URL 」フィールドを設定します。 リテラル値、テンプレート、変数または XPath 式を指定できます。
1. 「タスクの概要」ページに情報を表示する例を以下に示します。

   * `https://[server]:[port]/lc/crx/de` で CRXDE Lite 環境ログインします。
   * `Create a node`**SampleSummary** ` under `/content` with type `nt:unstructured`. In the properties of this node, add `sling:resourceType` of type String and value `SampleSummary`. In the Access Control List of this node, add an entry for `PERM_WORKSPACE_USER` allowing `jcr:read` privileges.`
   * `/apps` の下にある `Create a folder`**SampleSummary**。アクセス制御リスト `/apps/SampleSummary` に、`jcr:readprivileges` を許可する `PERM_WORKSPACE_USER` のエントリを追加します。
   * `Create a file `html.esp` at `/apps/SampleSummary`. For example, add the following lines in `html.esp`.`

   ```
   <html>
       <body>
           <h1>Sample Summary</h1>
           <br/>
           <p>Hello Sir!
               <br/>
               This is sample summary page for this task.
           </p>
       </body>
   </html>
   ```

   * タスクの割り当て手順で、タスクの概要 URL の値を `/lc/content/SampleSummary.html` に設定します。
   * このタスクの割り当て手順に関連付けられたタスクが AEM Forms ワークスペースで開かれると、`/apps/SampleSummary` の `html.esp` はタスクの概要ペインでレンダリングされます。
