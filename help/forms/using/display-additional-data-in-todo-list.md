---
title: TODO リストでの追加のデータの表示
seo-title: Displaying additional data in ToDo list
description: LiveCycle AEM Forms Workspace の TODO リストの表示をカスタマイズして、デフォルト以外の情報を表示する方法。
seo-description: How-to customize the display of the To-do list of LiveCycle AEM Forms workspace to show more information besides the default.
uuid: 4c678d9c-7794-4b62-8705-d62c7780c13f
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: forms-workspace
discoiquuid: b74a0933-2b96-4a88-9995-6fb21df141aa
exl-id: 42d8472d-0eab-4cf9-a7c3-bf2775ee6bec
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '282'
ht-degree: 89%

---

# TODO リストでの追加のデータの表示 {#displaying-additional-data-in-todo-list}

デフォルトで、AEM Forms Workspace TODO リストにタスクの表示名および説明が表示されます。しかしながら、作成日や締切日などのその他の情報を追加することができます。また、アイコンを追加したり、表示のスタイルを変更することもできます。

![デフォルト設定を表示する HTML Workspace の「TODO」タブ](assets/html-todo-list.png)

この記事では、TODO リストの各タスクに情報を追加する手順について説明します。

## 追加できる情報 {#what-can-be-added}

サーバーによって送信された `task.json` にある情報を追加することができます。情報は、平文テキストとして追加することも、スタイルを使用して情報をフォーマットすることもできます。

JSON オブジェクトの説明についての詳細は、[この](/help/forms/using/html-workspace-json-object-description.md)記事を参照してください。

## タスクでの情報の表示 {#displaying-information-on-a-task}

1. 「[AEM Forms Workspace のカスタマイズの一般的な手順](/help/forms/using/generic-steps-html-workspace-customization.md)」に従います。
1. タスクに追加の情報を表示するには、対応するキーと値のペアを `translation.json` のタスクブロック内に追加する必要があります。

   例：change `/apps/ws/locales/en-US/translation.json` 英語の場合：

   ```
   "task" : {
           "reminder" : {
               "value" : "Reminder",
               "tooltip" : "This is reminder __reminderCount__, for this task."
           },
           "deadlined" : {
               "value" : "Deadlined",
               "tooltip" : "This task has deadlined"
           },
           "save" : {
               "message" : "Task has been saved successfully"
           },
           "status" : {
               "deadlined" : "Deadlined",
               "created" : "Created",
               "assignedsaved" : "Draft from assigned task",
               "terminated" : "Terminated",
               "assigned" : "Assigned",
               "unknown" : "Unknown",
               "createdsaved" : "Draft from created task",
               "completed" : "Completed"
           },
           "draft" : {
               "value" : "Saved",
               "tooltip" : "This task is marked as a draft"
           },
           "escalated" : {
               "value" : "Escalated",
               "tooltip" : "This task has been escalated"
           },
           "forward" : {
               "value" : "Forwarded",
               "tooltip" : "This task was forwarded"
           },
           "priority" : {
               "highest" : "Highest priority",
               "normal" : "Normal priority",
               "high" : "High priority",
               "low" : "Low priority",
               "lowest" : "Lowest priority"
           },
           "claimed" : {
               "value" : "Claimed",
               "tooltip" : "This task has been claimed"
           },
           "locked" : {
               "value" : "Locked",
               "tooltip" : "This task is locked"
           },
           "consulted" : {
               "value" : "Consulted",
               "tooltip" : "This task has been consulted"
           },
           "returned" : {
               "value" : "Returned",
               "tooltip" : "This task was returned back"
           },
           "multiplesubmitbuttons" : {
               "message" : "The form associated with this task has multiple submit buttons so the Workspace Complete button will be disabled. Click the appropriate button on the form to submit it."
           },
           "nosubmitbutton" : {
               "message" : "The form associated with this task does not appear to have submit buttons. You may need to upgrade your Adobe Reader version to 9.1 or greater and enable the Reader Submit option in your process."
           },
           "icon" : {
               "tooltip" : "open the task __taskName__"
           }
       }
   ```

   >[!NOTE]
   >
   >対応するキーと値のペアをすべてのサポートされている言語に追加します。

1. たとえば、次のようにしてタスクブロック内に情報を追加します。

   ```
   "stepname" : {
               "value" : "Step Name",
               "tooltip" : "This task belongs to __stepName__ step"
   }
   ```

## 新規プロパティでの CSS の定義 {#defining-css-for-the-new-property}

1. タスクに追加された情報（プロパティ）にスタイルを適用できます。これをおこなうには、新しいプロパティをに追加するスタイル情報を追加する必要があります。 `/apps/ws/css/newStyle.css`.

   たとえば、以下を追加します。

   ```css
   .task .taskProperties .stepname{
       width: 25px;
       background: url(../images/stepname.png) no-repeat; /*-------- Or just reuse background image / image-sprite defined .task .taskProperties span of style.css---------------------*/
       background-position: 0px 0px; /*-------- Dummy values, need to be configured as per user background image / image-sprite ---------------------*/
   }
   ```

## HTML テンプレートへのエントリの追加 {#adding-entry-in-the-html-template}

最後に、タスクに追加する各プロパティの開発パッケージにエントリを含める必要があります。作成する方法については、「AEM Forms Workspace コードの構築」を参照してください。

1. コピー `task.html`:

   * 追加の: `/libs/ws/js/runtime/templates/`
   * を: `/apps/ws/js/runtime/templates/`

1. 新しい情報の追加先 `/apps/ws/js/runtime/templates/task.html`.

   例えば、次の場所にを追加します。 `div class="taskProperties"`:

   ```
   <span class="stepname" alt="<%= $.t('task.stepname.value')%>" title = '<%= $.t("task.stepname.tooltip",{stepName:stepName})%>'/>
   ```
