---
title: ' [!DNL Adobe Experience Manager]で非同期操作を設定します。'
description: リソースを大量に消費する一部のタスクを非同期的に完了して、 [!DNL Experience Manager Assets]のパフォーマンスを最適化します。
contentOwner: AG
translation-type: tm+mt
source-git-commit: f6aa1ab2c7a0ddeda1504e95ce4bd57fe74a65fd
workflow-type: tm+mt
source-wordcount: '628'
ht-degree: 18%

---


# 非同期操作 {#asynchronous-operations}

[!DNL Adobe Experience Manger Assets]は、パフォーマンスに与える悪影響を軽減するために、特定の長時間の、リソースを大量に消費するアセット操作を非同期的に処理します。 非同期処理では、複数のタスクをエンキューし、システムリソースの可用性に応じて順次実行します。 このような操作には以下のようなものがあります。

* 多数のアセットの削除。
* 多数のアセットまたは多数の参照があるアセットの移動.
* アセットメタデータの一括書き出しと読み込み。

非同期タスクのステータスは、**[!UICONTROL 非同期ジョブのステータス]**&#x200B;ページから表示できます。

>[!NOTE]
>
>デフォルトでは、[!DNL Assets]タスクは並行して実行されます。 `N`がCPUコアの数である場合、デフォルトで`N/2`タスクは並行して実行できます。 タスクキューのカスタム設定を使用するには、**[!UICONTROL Webコンソール]から[!UICONTROL Async Operation Default Queue]**&#x200B;の設定を変更します。 詳しくは、[キューの設定](https://sling.apache.org/documentation/bundles/apache-sling-eventing-and-job-handling.html#queue-configurations)を参照してください。

## 非同期操作の状態の監視{#monitoring-the-status-of-asynchronous-operations}

[!DNL Assets]が操作を非同期で処理する場合は常に、[!DNL Experience Manager] [インボックス](/help/sites-authoring/inbox.md)に通知が送信され、電子メールが送信されます。 非同期操作のステータスの詳細を表示するには、**[!UICONTROL 非同期ジョブステータス]**&#x200B;ページに移動します。

1. [!DNL Experience Manager]インターフェイスで、**[!UICONTROL 操作]**/**[!UICONTROL ジョブ]**&#x200B;をクリックします。

1. **[!UICONTROL 非同期ジョブステータス]**&#x200B;ページで、操作の詳細をレビューします。

   ![非同期操作のステータスと詳細](assets/job_status.png)

   操作の進行状況を確認するには、**[!UICONTROL ステータス]**&#x200B;列を参照してください。 進行状況に応じて、以下のいずれかのステータスが表示されます。

   * **[!UICONTROL アクティブ]**：操作は処理中です。。
   * **[!UICONTROL 成功]**:操作が完了しました。
   * **** エラー **[!UICONTROL エラー]**:操作を処理できませんでした。
   * **[!UICONTROL スケジュール済み]**:操作は後で処理するようにスケジュールされます。

1. アクティブな操作を停止するには、リストから操作を選択し、ツールバーの&#x200B;**[!UICONTROL 停止]** ![停止アイコン](assets/do-not-localize/stop_icon.svg)をクリックします。

1. 詳細（説明やログなど）を表示するには、操作を選択し、ツールバーの&#x200B;**[!UICONTROL 開く]** ![open_icon](assets/do-not-localize/edit_icon.svg)をクリックします。 タスクの詳細ページが表示されます。

   ![メタデータ読み込みタスクの詳細](assets/job_details.png)

1. リストから操作を削除するには、ツールバーの「**[!UICONTROL 削除]**」を選択します。詳細を CSV ファイルでダウンロードするには、「**[!UICONTROL ダウンロード]**」をクリックします。

   >[!NOTE]
   >
   >ステータスがアクティブまたはキューに登録されているタスクは削除できません。

## 完了したタスクの削除{#purge-completed-tasks}

[!DNL Experience Manager Assets] 毎日0100時間にパージタスクを実行し、1日以上経過している完了済みの非同期タスクを削除します。

<!-- TBD: Find out from the engineering team and mention the time zone of this 1:00 am task.
-->

削除タスクのスケジュールと、削除前に完了したタスクの詳細を保持する期間を変更できます。 完了したタスクの最大数を設定し、その詳細をいつでも保持することもできます。

1. [!DNL Experience Manager]インターフェイスで、**[!UICONTROL ツール]**/**[!UICONTROL 操作]**/**[!UICONTROL Webコンソール]**&#x200B;をクリックします。
1. **[!UICONTROL Adobe CQDAM非同期ジョブの削除スケジュール済み]**&#x200B;タスクを開きます。
1. 完了したタスクが削除されてからの日数と、詳細が履歴に保持されるタスクの最大数を指定します。 変更内容を保存します。

   ![非同期タスクの削除をスケジュールする設定](assets/purge_job.png)

## 非同期削除操作のしきい値の構成{#configure-thresholds-for-asynchronous-delete-operations}

削除するアセットまたはフォルダーの数が、設定したしきい値を超える場合は、非同期に削除操作が実行されます。

1. [!DNL Experience Manager]インターフェイスで、**[!UICONTROL ツール]**/**[!UICONTROL 操作]**/**[!UICONTROL Webコンソール]**&#x200B;をクリックします。
1. [!UICONTROL Webコンソール]から、**[!UICONTROL Async Delete Operation Job Processing]**&#x200B;の構成を開きます。
1. 「**[!UICONTROL アセット数のしきい値]**」ボックスに、アセット、フォルダーまたは参照を非同期に削除するしきい値を指定します。 変更内容を保存します。

   ![アセットを削除するタスクのしきい値制限を設定](assets/delete_threshold.png)

## 非同期移動操作のしきい値を構成{#configure-thresholds-for-asynchronous-move-operations}

移動するアセット、フォルダーまたは参照の数が、設定したしきい値を超える場合は、移動操作は非同期に実行されます。

1. [!DNL Experience Manager]インターフェイスで、**[!UICONTROL ツール]**/**[!UICONTROL 操作]**/**[!UICONTROL Webコンソール]**&#x200B;をクリックします。
1. [!UICONTROL Webコンソール]から、**[!UICONTROL 非同期移動操作ジョブ処理]**&#x200B;の構成を開きます。
1. 「**[!UICONTROL Threshold number of assets/references]**」ボックスに、アセット、フォルダーまたは参照を非同期に移動するしきい値を指定します。 変更内容を保存します。

   ![タスクがアセットを移動するしきい値の制限を設定](assets/move_threshold.png)

>[!MORELIKETHIS]
>
>* [Experience Managerで電子メールを設定します](/help/sites-administering/notification.md)。
>* [アセットメタデータの一括読み込みおよび書き出し](/help/assets/metadata-import-export.md)

