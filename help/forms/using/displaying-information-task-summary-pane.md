---
title: タスクの概要ペインでの情報の表示
seo-title: Displaying information in the Task Summary pane
description: AEM Forms ワークスペースでは、タスクの概要ペインを設定して、タスクのサマリを表示したりその他の任意の Web ページを表示したりできます。
seo-description: In AEM Forms workspace, a Task Summary pane can be configured to summarize the task or display any other web page.
uuid: 2fcc3d9f-0ec2-4250-8dc1-9746fd72ea60
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: forms-workspace
discoiquuid: 90d0f584-b598-4b21-85d7-31da5f13d404
exl-id: cb9de2d7-04ad-4221-8db7-403464c9888b
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '277'
ht-degree: 65%

---

# タスクの概要ペインでの情報の表示 {#displaying-information-in-the-task-summary-pane}

AEM Forms ワークスペースでタスクを開くと、タスクの概要ペインはタスクのサマリーを表示できます。タスクに対するこの追加の関連情報は、AEM Forms ワークスペースのエンドユーザーにとってより価値のあるものになります。

AEM Forms workspace を使用すると、[ タスクの概要 ] ペインで選択した Web ページを表示できます。 Workbench を使用してタスクの概要ペインを表示するためのプロセスを作成することができます。

1. Workbench で「Assign Task」処理を作成します。「Assign Task」操作についての詳細は、[Workbench ヘルプ](https://help.adobe.com/en_US/AEMForms/6.1/WorkbenchHelp/)のサービスリファレンストピックを参照してください。

   >[!NOTE]
   >
   >タスクの概要 URL がある場合は、タスクの概要の表示がデフォルトでフォーム表示の代わりに開きます。この場合は、ユーザーが「Assign Task」で「Open the form in maximized mode」オプションを有効にしている場合でも、フォームは最大化モードで開きません。

1. タスクの概要 URL フィールドを設定します。リテラル値、テンプレート、変数、または XPath 式を指定できます。
1. タスクの概要ページに関する情報を表示する例を以下に示します。

   * 次の場所にあるCRXDE Lite環境にログイン `https://[server]:[port]/lc/crx/de`.
   * `Create a node`**SampleSummary** ` under `/content` with type `nt:unstructured`. In the properties of this node, add `sling:resourceType` of type String and value `SampleSummary`. In the Access Control List of this node, add an entry for `PERM_WORKSPACE_USER` allowing `jcr:read` privileges.`
   * `Create a folder`**SampleSummary** under `/apps`. 次のアクセス制御リスト： `/apps/SampleSummary`、 `PERM_WORKSPACE_USER` 許可 `jcr:readprivileges`.
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

   * タスクの概要 URL の値を次のように設定 `/lc/content/SampleSummary.html` タスクの割り当て手順の説明です。
   * このタスクの割り当て手順に関連付けられているタスクがAEM Forms Workspace で開かれると、 `html.esp` 時刻 `/apps/SampleSummary` は、タスクの概要ペインにレンダリングされます。
