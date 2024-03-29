---
title: タスクの操作
seo-title: Working with Tasks
description: タスクは、コンテンツで行われる作業項目を表し、現在のタスクの完了レベルを決定するためにプロジェクトで使用されます
seo-description: Tasks represent items of work to be done on content and are used in projects to determine the level of completeness of current tasks
uuid: df4efb3f-8298-4159-acfe-305ba6b46791
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: projects
content-type: reference
discoiquuid: 1b79d373-73f4-4228-b309-79e74d191f3e
exl-id: 6480a0ba-ff65-42af-a14f-ce9fdbb7945f
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '605'
ht-degree: 29%

---

# タスクの操作{#working-with-tasks}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

タスクは、コンテンツ上で行う作業の項目を表します。タスクが割り当てられると、ワークフローインボックスに表示されます。タスク項目のタイプ列には task の値が含まれます。

タスクは、プロジェクトでも使用され、ワークフロータスクを含む現在のタスクの完了レベルを決定します。

## プロジェクトの進行状況の追跡 {#tracking-project-progress}

プロジェクトの進行状況は、 **タスク** タイル。 プロジェクトの進行状況は、次の方法で決定できます。

* **タスクタイル：**&#x200B;プロジェクトの全体的な進行状況は、プロジェクトの詳細ページに表示されるタスクタイルに表示されます。

* **タスクリスト：**&#x200B;タスクタイルをクリックすると、タスクのリストが表示されます。このリストには、プロジェクトに関連するすべてのタスクの詳細情報が含まれます。

ワークフロータスクと、 **タスク** タイル。

### タスクタイル {#task-tile}

プロジェクトに関連タスクがある場合は、プロジェクト内にタスクタイルが表示されます。 タスクタイルには、プロジェクトの現在のステータスが表示されます。 これは、ワークフロー内の既存のタスクに基づいており、ワークフローの進行に伴って将来生成されるタスクは含まれていません。 次の情報がタスクタイルに表示されます。

* 完了したタスクの割合
* アクティブなタスクの割合
* 期限切れタスクの割合

![chlimage_1-98](assets/chlimage_1-98.png)

### プロジェクト内のタスクの表示または変更 {#viewing-or-modifying-the-tasks-in-a-project}

進行状況の追跡に加えて、プロジェクトに関する詳細情報を表示したり、変更したりすることもできます。

#### タスクリスト {#task-list}

タスクタイルの省略記号 (...) をクリックして、プロジェクトに関連するタスクのリストを表示します。 タスクは親ワークフローで分割されます。 期限、担当者、優先度、ステータスなどのメタデータと共に、タスクの詳細が表示されます。

![chlimage_1-99](assets/chlimage_1-99.png)

#### タスクの詳細 {#task-details}

特定のタスクの詳細を表示するには、タスクリストでタスクをタップまたはクリックして、タスクの詳細を開きます。

![chlimage_1-100](assets/chlimage_1-100.png)

### タスクのコメントの表示および変更 {#viewing-and-modifying-task-comments}

タスクの詳細では、コメントを編集または追加できます。 また、プロジェクト内のすべてのコメントは、「コメント」領域に表示されます。

![chlimage_1-101](assets/chlimage_1-101.png)

### タスクの追加 {#adding-tasks}

プロジェクトに新しいタスクを追加できます。 これらのタスクはタスクタイルに表示され、通知インボックスでアクションを実行できます。

タスクを追加するには：

1. プロジェクトの&#x200B;**タスク**&#x200B;タイルで、「+」アイコンをタップまたはクリックします。**タスクを追加**&#x200B;ウィンドウが開きます。
1. タスクに関する情報を入力します。 タスクのタイトルと、タスクを割り当てるグループは必須です。 コンテンツのパス、説明、タスクの優先度、期限などの追加情報はオプションです。 また、 **詳細** タブを使用して、URL の名前を付けるために使用されるタスクの名前を入力します。

   ![chlimage_1-102](assets/chlimage_1-102.png)

1. 「**作成**」をタップまたはクリックします。

## インボックス内でのタスクの使用 {#working-with-tasks-in-the-inbox}

タスクにアクセスする別の方法は、インボックスからアクセスする方法です。 インボックスからコンテンツを開き、必要な変更を実装できます。 完了したら、タスクのステータスを「完了」に設定します。 タスクが所属するユーザーグループに割り当てられると、タスクがインボックスに表示されます。 この場合、グループの任意のメンバーが作業を実行し、タスクを完了できます。

![chlimage_1-103](assets/chlimage_1-103.png)

タスクを完了するには、タスクを選択し、 **完了**. タスクに情報を追加し、 **完了**. 詳しくは、 [インボックス](/help/sites-authoring/inbox.md) を参照してください。

![chlimage_1-104](assets/chlimage_1-104.png)
