---
title: 追跡テーブルのカスタマイズ
seo-title: Customize tracking tables
description: AEM Forms Workspace の「監査」タブに表示されるタスクテーブルでのユーザープロセスの詳細の表示をカスタマイズする方法。
seo-description: How-to customize the display of the details of user processes in the task table displayed in the tracking tab of AEM Forms workspace.
uuid: 13d6ebf2-99d5-434f-85f9-b0cba5f5751a
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: forms-workspace
discoiquuid: bb7a6e9f-4f28-4d97-8a0c-949259fd6857
exl-id: 5f925f47-3123-4a27-aea1-0a1c1fba7bb6
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '366'
ht-degree: 35%

---

# 追跡テーブルのカスタマイズ{#customize-tracking-tables}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

AEM Forms Workspace の「追跡」タブを使用すると、ログインしたユーザーが関係するプロセスインスタンスの詳細を表示できます。追跡テーブルを表示するには、最初に左側のペインでプロセス名を選択して、中央のペインでインスタンスのリストを表示します。 プロセスインスタンスを選択して、このインスタンスによって生成されたタスクのテーブルを右側のウィンドウに表示します。 デフォルトでは、テーブル列には次のタスク属性が表示されます（タスクモデル内の対応する属性は括弧内に表示されます）。

* ID（`taskId`）
* 名前（`stepName`）
* 説明（`instructions`）
* 選択されたアクション（`selectedRoute`）
* 作成時刻（`createTime`）
* 完了時刻（`completeTime`）
* 所有者（`currentAssignment.queueOwner`）

タスクテーブルに表示できるタスクモデルの残りの属性は次のとおりです。

<table> 
 <tbody> 
  <tr> 
   <td><p>actionInstanceId</p> </td> 
   <td><p>isOpenFullScreen</p> </td> 
   <td><p>reminderCount</p> </td> 
  </tr> 
  <tr> 
   <td><p>classOfTask</p> </td> 
   <td><p>isOwner</p> </td> 
   <td><p>routeList</p> </td> 
  </tr> 
  <tr> 
   <td><p>consultGroupId</p> </td> 
   <td><p>isRouteSelectionRequired</p> </td> 
   <td><p>savedFormCount</p> </td> 
  </tr> 
  <tr> 
   <td><p>contentType</p> </td> 
   <td><p>isShowAttachments</p> </td> 
   <td><p>serializedImageTicket</p> </td> 
  </tr> 
  <tr> 
   <td><p>createTime</p> </td> 
   <td><p>isStartTask</p> </td> 
   <td><p>serviceName</p> </td> 
  </tr> 
  <tr> 
   <td><p>creationId</p> </td> 
   <td><p>isVisible</p> </td> 
   <td><p>serviceTitle</p> </td> 
  </tr> 
  <tr> 
   <td><p>currentAssignment</p> </td> 
   <td><p>nextReminder</p> </td> 
   <td><p>showACLActions</p> </td> 
  </tr> 
  <tr> 
   <td><p>deadline</p> </td> 
   <td><p>numForms</p> </td> 
   <td><p>showDirectActions</p> </td> 
  </tr> 
  <tr> 
   <td><p>description</p> </td> 
   <td><p>numFormsToBeSaved</p> </td> 
   <td><p>status</p> </td> 
  </tr> 
  <tr> 
   <td><p>displayName</p> </td> 
   <td><p>outOfOfficeUserId</p> </td> 
   <td><p>summaryUrl</p> </td> 
  </tr> 
  <tr> 
   <td><p>forwardGroupId</p> </td> 
   <td><p>outOfOfficeUserName</p> </td> 
   <td><p>supportsSave</p> </td> 
  </tr> 
  <tr> 
   <td><p>isApprovalUI</p> </td> 
   <td><p>優先度</p> </td> 
   <td><p>taskACL</p> </td> 
  </tr> 
  <tr> 
   <td><p>isCustomUI</p> </td> 
   <td><p>processInstanceId</p> </td> 
   <td><p>taskFormType</p> </td> 
  </tr> 
  <tr> 
   <td><p>isDefaultImage</p> </td> 
   <td><p>processInstanceStatus</p> </td> 
   <td><p>taskUserInfo</p> </td> 
  </tr> 
  <tr> 
   <td><p>isLocked</p> </td> 
   <td><p>processVariables</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td><p>isMustOpenToComplete</p> </td> 
   <td><p>readerSubmitOptions</p> </td> 
   <td> </td> 
  </tr> 
 </tbody> 
</table>

次のタスクテーブルのカスタマイズの場合は、ソースコードでセマンティックの変更を行う必要があります。Workspace SDK を使用してセマンティックの変更を行い、変更されたソースから縮小パッケージを構築する方法については、「[AEM Forms Workspace のカスタマイズの概要](/help/forms/using/introduction-customizing-html-workspace.md)」を参照してください。

## テーブルの列と順序の変更 {#changing-table-columns-and-their-order}

1. テーブルに表示されるタスク属性とその順序を変更するには、ファイル/ws/js/runtime/templates/processinstancehistory.htmlを設定します。

   ```as3
   <table>
       <thead>
           <tr>
               <!-- put the column headings in order here, for example-->
               <th><%= $.t('history.fixedTaskTableHeader.taskName')%></th>
               <th><%= $.t('history.fixedTaskTableHeader.taskInstructions')%></th>
               <th><%= $.t('history.fixedTaskTableHeader.taskRoute')%></th>
               <th><%= $.t('history.fixedTaskTableHeader.taskCreateTime')%></th>
               <th><%= $.t('history.fixedTaskTableHeader.taskCompleteTime')%></th>
           </tr>
       </thead>
   </table>
   ```

   ```as3
   <table>
       <tbody>
           <%_.each(obj, function(task){%>
           <tr>
               <!-- Put the task attributes in the order of headings, for example -->
               <td><%= task.stepName %></td>
               <td><%= task.instructions %></td>
               <td><%= !task.selectedRoute?'':(task.selectedRoute=='null'?'Default':task.selectedRoute) %></td>
               <td><%= task.createTime?task.formattedCreateTime:'' %></td>
               <td><%= task.completeTime? task.formattedCompleteTime:'' %></td>
           </tr>
           <%});%>
       </tbody>
   </table>
   ```

## トラッキングテーブルの並べ替え {#sorting-a-tracking-table}

列見出しをクリックしたときにタスクリストテーブルを並べ替えるには：

1. ファイル `js/runtime/views/processinstancehistory.js` の `.fixedTaskTableHeader th` にクリックハンドラーを登録します。

   ```as3
   events: {
       //other handlers
       "click .fixedTaskTableHeader th": "onTaskTableHeaderClick",
       //other handlers
   }
   ```

   ハンドラーで、`js/runtime/util/history.js` の `onTaskTableHeaderClick` 関数を呼び出します。

   ```as3
   onTaskTableHeaderClick: function (event) {
           history.onTaskTableHeaderClick(event);
   }
   ```

1. `TaskTableHeaderClick` メソッドを `js/runtime/util/history.js` で公開します。

   メソッドは、click イベントから task 属性を検索し、その属性の tasklist を並べ替え、並べ替えられた tasklist を使用して task テーブルをレンダリングします。

   並べ替えは、比較関数を提供することで、タスクリストコレクションの Backbone 並べ替え関数を使用して行われます。

   ```as3
       return {
           //other methods
           onTaskTableHeaderClick  : onTaskTableHeaderClick,
           //other methods
       };
   ```

   ```as3
   onTaskTableHeaderClick = function (event) {
           var target = $(event.target),
            comparator,
               attribute;
           if(target.hasClass('taskName')){
            attribute = 'stepName';
           } else if(target.hasClass('taskInstructions')){
               attribute = 'instructions'; 
           } else if(target.hasClass('taskRoute')){
               attribute = 'selectedRoute'; 
           } else if(target.hasClass('taskCreateTime')){
               attribute = 'createTime'; 
           } else if(target.hasClass('taskCompleteTime')){
               attribute = 'completeTime'; 
           }
           taskList.comparator = function (task) {
            return task.get(attribute);
           };
           taskList.sort();
           render();
       };
   ```
