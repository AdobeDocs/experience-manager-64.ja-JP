---
title: ' [!DNL Adobe Experience Manager]で非同期操作を設定します。'
description: リソースを集中的に消費する一部のタスクを非同期的に完了し、 [!DNL Experience Manager Assets]でパフォーマンスを最適化します。
contentOwner: AG
feature: アセット管理
role: Business Practitioner
exl-id: 0abdfe87-d932-41dd-b1e6-9f5fa5b924fe
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '630'
ht-degree: 18%

---

# 非同期操作 {#asynchronous-operations}

[!DNL Adobe Experience Manger Assets]は、パフォーマンスに悪影響を与えないように、長時間実行されリソースを集中的に消費する特定のアセット操作を非同期的に処理します。 非同期処理では、複数のタスクがエンキューされ、システムリソースの可用性に応じて順次実行されます。 このような操作には以下のようなものがあります。

* 多数のアセットの削除。
* 多数のアセットまたは多数の参照があるアセットの移動.
* アセットメタデータの一括書き出しと読み込み

非同期タスクのステータスは、**[!UICONTROL 非同期ジョブステータス]**&#x200B;ページで確認できます。

>[!NOTE]
>
>デフォルトでは、[!DNL Assets]タスクは並行して実行されます。 `N`がCPUコアの数である場合、デフォルトでは`N/2`タスクを並行して実行できます。 タスクキューのカスタム設定を使用するには、[!UICONTROL Webコンソール]で&#x200B;**[!UICONTROL Async Operation Default Queue]**&#x200B;設定を変更します。 詳しくは、[キューの設定](https://sling.apache.org/documentation/bundles/apache-sling-eventing-and-job-handling.html#queue-configurations)を参照してください。

## 非同期操作のステータスを監視します。{#monitoring-the-status-of-asynchronous-operations}

[!DNL Assets]が操作を非同期で処理する場合は常に、[!DNL Experience Manager] [インボックス](/help/sites-authoring/inbox.md)に電子メールで通知が届きます。 非同期操作のステータスの詳細を表示するには、**[!UICONTROL 非同期ジョブステータス]**&#x200B;ページに移動します。

1. [!DNL Experience Manager]インターフェイスで、**[!UICONTROL 操作]** > **[!UICONTROL ジョブ]**&#x200B;をクリックします。

1. **[!UICONTROL 非同期ジョブステータス]**&#x200B;ページで、操作の詳細をレビューします。

   ![非同期操作のステータスと詳細](assets/job_status.png)

   操作の進行状況を確認するには、**[!UICONTROL ステータス]**&#x200B;列を参照してください。 進行状況に応じて、以下のいずれかのステータスが表示されます。

   * **[!UICONTROL アクティブ]**：操作は処理中です。。
   * **[!UICONTROL 成功]**:操作が完了しました。
   * **** エラー **[!UICONTROL エラー]**:操作を処理できませんでした。
   * **[!UICONTROL スケジュール済み]**:操作は後で処理するようにスケジュールされています。

1. アクティブな操作を停止するには、リストから選択し、ツールバーの&#x200B;**[!UICONTROL 停止]** ![停止アイコン](assets/do-not-localize/stop_icon.svg)をクリックします。

1. 説明やログなど、その他の詳細を表示するには、操作を選択し、ツールバーの「**[!UICONTROL 開く]** ![開く](assets/do-not-localize/edit_icon.svg) 」をクリックします。 タスクの詳細ページが表示されます。

   ![メタデータインポートタスクの詳細](assets/job_details.png)

1. リストから操作を削除するには、ツールバーの「**[!UICONTROL 削除]**」を選択します。詳細を CSV ファイルでダウンロードするには、「**[!UICONTROL ダウンロード]**」をクリックします。

   >[!NOTE]
   >
   >タスクのステータスがアクティブまたはキューに登録されている場合は、タスクを削除できません。

## 完了したタスクの削除{#purge-completed-tasks}

[!DNL Experience Manager Assets] は、毎日0100時間にパージタスクを実行して、1日以上経過した完了済みの非同期タスクを削除します。

<!-- TBD: Find out from the engineering team and mention the time zone of this 1:00 am task.
-->

パージタスクのスケジュールと、完了したタスクの詳細を削除前に保持する期間を変更できます。 また、完了したタスクの最大数を設定し、どの時点でも詳細を保持できます。

1. [!DNL Experience Manager]インターフェイスで、**[!UICONTROL ツール]** / **[!UICONTROL 操作]** / **[!UICONTROL Webコンソール]**&#x200B;をクリックします。
1. **[!UICONTROL Adobe CQ DAM Async Jobs Purge Scheduled]**&#x200B;タスクを開きます。
1. 完了したタスクが削除されるまでの日数のしきい値と、詳細が履歴に保持されるタスクの最大数を指定します。 変更内容を保存します。

   ![非同期タスクのパージをスケジュールする設定](assets/purge_job.png)

## 非同期削除操作のしきい値の設定{#configure-thresholds-for-asynchronous-delete-operations}

削除するアセットまたはフォルダーの数がしきい値を超えると、削除操作が非同期的に実行されます。

1. [!DNL Experience Manager]インターフェイスで、**[!UICONTROL ツール]** / **[!UICONTROL 操作]** / **[!UICONTROL Webコンソール]**&#x200B;をクリックします。
1. [!UICONTROL Webコンソール]から、**[!UICONTROL Async Delete Operation Job Processing]**&#x200B;設定を開きます。
1. 「**[!UICONTROL アセット数のしきい値]**」ボックスで、アセット、フォルダーまたは参照を非同期で削除するしきい値を指定します。 変更内容を保存します。

   ![アセットを削除するタスクのしきい値の制限を設定](assets/delete_threshold.png)

## 非同期移動操作のしきい値の設定{#configure-thresholds-for-asynchronous-move-operations}

移動するアセット、フォルダーまたは参照の数がしきい値の数を超えると、移動操作が非同期的に実行されます。

1. [!DNL Experience Manager]インターフェイスで、**[!UICONTROL ツール]** / **[!UICONTROL 操作]** / **[!UICONTROL Webコンソール]**&#x200B;をクリックします。
1. [!UICONTROL Webコンソール]から、**[!UICONTROL Async Move Operation Job Processing]**&#x200B;設定を開きます。
1. 「**[!UICONTROL アセット/参照の数のしきい値]**」ボックスで、アセット、フォルダーまたは参照を非同期に移動するしきい値を指定します。 変更内容を保存します。

   ![アセットを移動するタスクのしきい値の制限を設定](assets/move_threshold.png)

>[!MORELIKETHIS]
>
>* [Experience Manager](/help/sites-administering/notification.md)で電子メールを設定します。
>* [アセットメタデータの一括読み込みおよび書き出し](/help/assets/metadata-import-export.md)

