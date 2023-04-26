---
title: タスクのタブのカスタマイズ
seo-title: Customizing tabs for a task
description: LiveCycleAEM Forms Workspace でタスクのタブ名をカスタマイズする方法。
seo-description: How-to customize the names of the tabs for your tasks, in LiveCycle AEM Forms workspace.
uuid: 77eabb63-f8ea-4ec0-8a41-b51c65cdecc0
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: forms-workspace
discoiquuid: ac0a281f-f589-4a70-9bc7-1a23e054b02f
exl-id: 42671435-e0f0-41db-af83-182b01742954
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '101'
ht-degree: 85%

---

# タスクのタブのカスタマイズ {#customizing-tabs-for-a-task}

`Start Process` Uber ビューの `Start Process` コンポーネントと `ToDo` Uber ビューの `Task Details` コンポーネントのタブ名をカスタマイズできます。

1. 「[AEM Forms Workspace のカスタマイズの一般的な手順](/help/forms/using/generic-steps-html-workspace-customization.md)」に従います。
1. `translation.json` ファイルにある `tabname` の値を変更します。

   たとえば、英語の場合は `/apps/ws/locales/en-US/translation.json` を次のように変更します。

   * 開始プロセスで開始したタスクの場合は、`"startprocess" : {}` ブロックから次のスニペットを使用します。

   ```
   "tabname" : {
               "form" : "Application",
               "details" : "Overview",
               "attachments" : "Attachments",
               "notes" : "Helper Notes"
           }
   ```

   * To-do のタスクの場合は、`"todo" : {}` ブロックから次のスニペットを使用します。

   ```
   "tabname" : {
               "summary" : "Bird's-eye view",
               "history" : "Past",
               "form" : "Form",
               "details" : "Overview",
               "attachments" : "Attachments",
               "notes" : "Notes"
   }
   ```

   >[!NOTE]
   >
   >対応するキーと値のペアをすべてのサポートされている言語に追加します。
