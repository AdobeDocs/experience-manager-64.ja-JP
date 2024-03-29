---
title: 停止した操作および停止したブランチの使用
seo-title: Working with stalled operations and branches
description: 停止した操作ページと停止したブランチページに、停止したプロセスが表示されます。
seo-description: The Stalled Operations page and the Stalled Branches page show the processes that have stalled.
uuid: 5f6202b0-79c2-4c3c-847a-236c0366e60b
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms_workflow
products: SG_EXPERIENCEMANAGER/6.4/FORMS
discoiquuid: 8c2567f3-7220-436a-b9f2-2824a98c1ccc
exl-id: 04a832d5-1ab5-4db3-b185-57fba21eb839
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '743'
ht-degree: 14%

---

# 停止した操作および停止したブランチの使用 {#working-with-stalled-operations-and-branches}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

停止した操作ページと停止したブランチページに、停止したプロセスが表示されます。 操作の実行中または実行後にエラーが発生した場合、またはプロセス内の計画的な停止操作が原因で、プロセスは停止する場合があります。

* 操作は、予期しないエラーが原因で停止する場合があります。 ただし、プロセス内の Stall Branch 操作は、プロセスの実行を意図的に停止し、管理者が介入する必要があります。
* ブランチは、ルールの評価中に操作間で停止する場合があります。

プロセスが停止した場合、問題が修正され、操作またはブランチが再開されるまで、それ以上の操作は実行されません。

停止した項目ごとに、リストに次の情報が表示されます。

**操作名またはブランチ名：**&#x200B;操作またはブランチの名前。

**ステータス：**&#x200B;停止した項目の場合は常に「停止」です。

**エラー：**&#x200B;問題に関する短い説明。

**プロセス ID：**&#x200B;プロセスがインスタンス化される（つまり、ユーザーまたは自動ステップによってプロセスが開始される）ときに、forms ワークフローによって割り当てられる正の整数。この ID を使用して、プロセスインスタンスをライフサイクル全体にわたって追跡できます。

**プロセス名 - バージョン：** Workbench で割り当てられたプロセスの名前。

**停止日：**&#x200B;操作またはブランチが停止した日時。

停止した操作ページまたは停止したブランチページで、次のタスクを実行できます。

* エラーを選択して、その詳細を表示します。 エラーを選択すると、エラーの詳細ページが表示されます。
* 停止した操作を終了または再試行するか、停止したブランチを再試行します。

## 停止した操作またはブランチの終了または再試行 {#terminating-or-retrying-stalled-operations-or-branches}

停止した操作ページで、表示されているプロセスインスタンスを終了できます。

プロセスインスタンスを終了すると、実行が停止し、それ以上の操作は実行されません。 通常、プロセスは、エラーが原因でブロックされたり、使用できなくなったりし、修正して再起動できない場合にのみ終了します。

停止した操作ページまたは停止したブランチページで、操作またはブランチを再試行できます。

操作を再試行すると、Formsワークフローに、操作を再開するリクエストが送信されます。 プロセスの停止を引き起こしたエラーが修正され、再試行リクエストが成功した場合、プロセスは停止した時点から再実行を開始し、ステータスは「実行中」に変わります。 操作を再開できない場合、操作は停止状態のままとなり、終了する必要が生じる場合があります。

### 停止した操作の終了 {#terminate-a-stalled-operation}

1. 管理コンソールで、サービス/forms ワークフロー/停止した操作のエラーをクリックします。
1. 停止した操作ページで、終了する項目を選択し、「終了」をクリックします。

### 停止した操作またはブランチの再試行 {#retry-a-stalled-operation-or-branch}

1. 管理コンソールで、サービス/Forms ワークフローをクリックし、「停止した操作のエラー」または「停止したブランチのエラー」をクリックします。
1. 停止した操作ページまたは停止したブランチページで、再試行する項目を選択し、「再試行」をクリックします。

## 停止した操作またはブランチに関するエラーの詳細の表示 {#viewing-error-details-about-stalled-operations-or-branches}

「停止した操作」ページまたは「停止したブランチ」ページの停止した項目のリストからエラーを選択すると、エラーの詳細ページが表示され、問題のトラブルシューティングに役立つエラーに関する詳細が示されます。

ページの下部にあるボックスには、エラー情報が表示されます。

エラーの詳細ページから、停止した操作を終了または再試行し、停止したブランチを再試行することもできます。

## エスカレーションユーザーが存在しない場合、プロセスは停止しません {#process-does-not-stall-when-escalation-user-does-not-exist}

エラーは、AEM forms User サービスの Assign Task 操作が、特定の期間の経過後に別のユーザーにタスクをエスカレーションするように設定され、Assign Task 操作の実行後、エスカレーションが発生する前にエスカレーションユーザーが削除される場合に発生します。

この状況が発生した場合、設定されたエスカレーション時にプロセスとタスクの状態は変わらず、エスカレーションは発生しませんが、プロセスは停止しません。 次のメッセージがサーバーログに表示されます。

&quot;エスカレーション用に指定されたプリンシパルが、taskID に対して有効ではありません： *数値*、指定されたキュー： *数値*.&quot;

タスクの生成前（Assign Task 操作の実行前）にエスカレーションユーザーが削除された場合、プロセスが停止するか、InvalidPrincipal 例外イベントが発生します。

この問題を回避するには、ユーザーを削除する際に、そのユーザーに属するタスクを検索し、それに応じて対処します。 ( [タスクの操作](/help/forms/using/admin-help/tasks.md#working-with-tasks).)
