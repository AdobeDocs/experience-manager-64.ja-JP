---
title: タスクのタブのカスタマイズ
seo-title: タスクのタブのカスタマイズ
description: LiveCycle AEM Forms Workspace でタスクのタブ名をカスタマイズする方法。
seo-description: LiveCycle AEM Forms Workspace でタスクのタブ名をカスタマイズする方法。
uuid: 77eabb63-f8ea-4ec0-8a41-b51c65cdecc0
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: forms-workspace
discoiquuid: ac0a281f-f589-4a70-9bc7-1a23e054b02f
translation-type: tm+mt
source-git-commit: f13d358a6508da5813186ed61f959f7a84e6c19f
workflow-type: tm+mt
source-wordcount: '121'
ht-degree: 51%

---


# タスクのタブのカスタマイズ  {#customizing-tabs-for-a-task}

`Start Process` Uber表示内の`Start Process`コンポーネントおよび`ToDo` Uber表示内の`Task Details`コンポーネントのタブ名をカスタマイズできます。

1. 「[AEM Forms Workspace のカスタマイズの一般的な手順](/help/forms/using/generic-steps-html-workspace-customization.md)」に従います。
1. `translation.json`ファイルの`tabname`の値を変更します。

   例えば、英語の場合は`/apps/ws/locales/en-US/translation.json`を次のように変更します。

   * 開始プロセスで開始されたタスクに対しては、`"startprocess" : {}`ブロックの次のスニペットを使用します。

   ```
   "tabname" : {
               "form" : "Application",
               "details" : "Overview",
               "attachments" : "Attachments",
               "notes" : "Helper Notes"
           }
   ```

   * TODO内のタスクに対しては、`"todo" : {}`ブロックの次のスニペットを使用します。

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
