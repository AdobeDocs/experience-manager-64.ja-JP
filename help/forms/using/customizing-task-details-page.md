---
title: タスクの詳細ページのカスタマイズ
seo-title: Customizing the task details page
description: AEM Forms Workspace のタスクの詳細ページをカスタマイズして、タスクについて表示されるデフォルトの情報を変更する方法。
seo-description: How-to customize the task details page in AEM Forms workspace to modify the default information displayed about a task.
uuid: d85fae55-8e66-4595-8560-5485622b6841
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: forms-workspace
discoiquuid: 16e57cf6-aaa1-406d-a6ad-71ec60b15386
exl-id: de97e6f7-25bf-462b-b67d-0d3fbd86a321
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '263'
ht-degree: 91%

---

# タスクの詳細ページのカスタマイズ {#customizing-the-task-details-page}

タスクの詳細ページには、タスクおよびそのプロセスに関する情報が含まれています。しかしながら、タスクの詳細ページをカスタマイズして情報を追加したり、削除したりすることができます。

次の情報をタスクの詳細ページに追加することができます。

* タスクの JSON オブジェクトで入手できる情報（[AEM Forms Workspace JSON オブジェクトの説明の「タスク」セクション](/help/forms/using/html-workspace-json-object-description.md)）
* プロセスインスタンスの JSON オブジェクトで入手できる情報（[AEM Forms Workspace JSON オブジェクトの説明の「プロセスインスタンス」セクション](/help/forms/using/html-workspace-json-object-description.md)）

タスクの詳細ページをカスタマイズするには：

1. [AEM Forms Workspace のカスタマイズの一般的な手順](/help/forms/using/generic-steps-html-workspace-customization.md)に従います。
1. 追加の情報を表示するには、対応するキーと値のペアを`todo`ブロック／`details`ブロック／`app`ブロック／[ `required` ブロック] にある `translation.json` ファイルに追加してください。

   [ `required`ブロック]は、タスク情報の task ブロック、プロセス情報の process ブロック、および保留中のタスク情報の currentpendingtask ブロックなど、使用可能なブロックを指します。

   たとえば、タスクの詳細ページに必要なルート選択に関する情報を追加するには、以下のキーと値のペアを task ブロックに追加することができます。

   ```
   "todo" : {
       .
       .
       .
       "details" : {
           .
           .
           "task" : {
               .
               .
               "RouteSelectionRequired" : "Route Selection Required"
           }
       }
   }
   ```

   >[!NOTE]
   >
   >対応するキーと値のペアをすべてのサポートされている言語に追加します。

1. `/libs/ws/js/runtime/templates/taskdetails.html` を `/apps/ws/js/runtime/templates/taskdetails.html` にコピーします。

   新しい情報を `/apps/ws/js/runtime/templates/taskdetails.html` に追加します。次は例です。

   ```css
   <div class="detailsContainer">
       .
       .
       <ul>
           .
           .
           <li>
               <label for="routeSelectionRequired" title="<%= $.t('todo.details.task.RouteSelectionRequired')%>"><%= $.t('todo.details.task.RouteSelectionRequired')%></label>
               <div>
                   <span id="routeSelectionRequired"><%= isRouteSelectionRequired != null ? isRouteSelectionRequired : ''%></span>
               </div>
           </li>
           .
           .
       </ul>
   </div>
   ```

1. /apps/ws/js/registry.js を開いて編集します。

   `text!/lc/libs/ws/js/runtime/templates/taskdetails.html` を検索して `text!/lc/apps/ws/js/runtime/templates/taskdetails.html` で置き換えます。

>[!NOTE]
>
>AEM Forms Workspace の「**開始プロセス**」タブで作成したタスクでタスクの詳細ページをカスタマイズするには、新しい情報をに追加します。 `/apps/ws/js/runtime/templates/startprocess.html`.
>
>詳細ページで追加した情報に新しいスタイルを追加するには、[ワークスペースのカスタマイズ](/help/forms/using/changing-locale-user-interface.md)にある&#x200B;*ユーザーインターフェイスの変更*&#x200B;セクションを使用して CSS ファイルを変更してください。
