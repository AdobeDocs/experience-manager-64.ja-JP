---
title: タスクの詳細ページのカスタマイズ
seo-title: Customizing the task details page
description: AEM Forms Workspace のタスクの詳細ページをカスタマイズして、タスクに関して表示されるデフォルト情報を変更する方法。
seo-description: How-to customize the task details page in AEM Forms workspace to modify the default information displayed about a task.
uuid: d85fae55-8e66-4595-8560-5485622b6841
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: forms-workspace
discoiquuid: 16e57cf6-aaa1-406d-a6ad-71ec60b15386
exl-id: de97e6f7-25bf-462b-b67d-0d3fbd86a321
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '299'
ht-degree: 35%

---

# タスクの詳細ページのカスタマイズ {#customizing-the-task-details-page}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

タスクの詳細ページには、タスクとそのプロセスに関する情報が含まれます。 ただし、タスクの詳細ページをカスタマイズして、情報を追加または削除できます。

次の情報をタスクの詳細ページに追加できます。

* タスクの JSON オブジェクトで使用できる情報 ( [AEM Forms Workspace JSON オブジェクトの説明](/help/forms/using/html-workspace-json-object-description.md))
* プロセスインスタンスの JSON オブジェクト ( [AEM Forms Workspace JSON オブジェクトの説明](/help/forms/using/html-workspace-json-object-description.md))

タスクの詳細ページをカスタマイズするには：

1. フォロー [AEM Forms Workspace のカスタマイズの一般的な手順です。](/help/forms/using/generic-steps-html-workspace-customization.md)
1. 追加の情報を表示するには、対応するキーと値のペアを`todo`ブロック／`details`ブロック／`app`ブロック／[ `required` ブロック] にある `translation.json` ファイルに追加してください。

   [ `required`ブロック]は、タスク情報の task ブロック、プロセス情報の process ブロック、および保留中のタスク情報の currentpendingtask ブロックなど、使用可能なブロックを指します。

   たとえば、タスクの詳細ページで Route Selection Required に関する情報を追加するには、次のキーと値のペアを task ブロックに追加します。

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
   >対応するキーと値のペアを、サポートされるすべての言語に追加します。

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
