---
title: プロセスレポートの事前定義済みレポート
seo-title: プロセスレポートの事前定義済みレポート
description: JEE上のAEM Formsのプロセスデータに対するクエリで、長時間実行されているプロセス、プロセス期間、ワークフローのボリュームに関するレポートを作成します。
seo-description: JEE上のAEM Formsのプロセスデータに対するクエリで、長時間実行されているプロセス、プロセス期間、ワークフローのボリュームに関するレポートを作成します。
uuid: ba3a1809-270e-4c94-ade4-d2f6af86d860
content-type: reference
topic-tags: process-reporting
products: SG_EXPERIENCEMANAGER/6.4/FORMS
discoiquuid: 6320c632-c7ec-4e56-9d12-cd27e3e9306e
exl-id: 21f5fb7e-53b3-485d-9b6a-813182f14781
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '723'
ht-degree: 0%

---

# プロセスレポートの事前定義レポート{#pre-defined-reports-in-process-reporting}

AEM Forms Process Reportingには、次の&#x200B;*標準の*&#x200B;レポートが付属しています。

* **[長時間実行されるプロセス](/help/forms/using/process-reporting/pre-defined-reports-in-process-reporting.md#p-long-running-processes-p)**:指定された時間以上かかったすべてのAEM Formsプロセスのレポート

* **[プロセス期間のグラフ](/help/forms/using/process-reporting/pre-defined-reports-in-process-reporting.md#p-process-duration-report-br-p)**:期間別の指定されたAEM Formsプロセスのレポート

* **[ワークフローの量](/help/forms/using/process-reporting/pre-defined-reports-in-process-reporting.md#p-workflow-volume-report-p)**:指定したプロセスの実行中および完了したインスタンスの日付別レポート

## 長時間実行中のプロセス{#long-running-processes}

長時間実行中のプロセスレポートには、完了までに指定された時間を超えたAEM Formsプロセスが表示されます。

### 長時間実行プロセスレポートを実行するには{#to-execute-a-long-running-process-report-br}

1. プロセスレポートで事前定義済みレポートのリストを表示するには、**プロセスレポート**&#x200B;ツリービューで、**レポート**&#x200B;ノードをクリックします。
1. **Long Running Processes**&#x200B;レポートノードをクリックします。

   ![long_running_node](assets/long_running_node.png)

   レポートを選択すると、ツリービューの右側に&#x200B;**レポートパラメータ**&#x200B;パネルが表示されます。

   ![長時間実行プロセスレポートパラメーター](assets/report_parameters_panel.png)

   パラメーター:

   * **期間**(*必須*):期間と時間の単位を指定します。指定された期間を超えて実行されたすべてのAEM Formsプロセスを表示します。
   * **** 後に開始(*オプション*):日付を選択します。レポートをフィルターして、指定した日付の後に開始したプロセスインスタンスを表示します。
   * **前に開始** (*オプション*):日付を選択します。レポートをフィルターして、指定した日付より前に開始したプロセスインスタンスを表示します。

1. 「**移動**」をクリックして、レポートを実行します。

   レポートは、**レポートの処理**&#x200B;ウィンドウの右側の&#x200B;**レポート**&#x200B;パネルに表示されます。

   ![long_running_processes](assets/long_running_processes.png)

   **レポート**&#x200B;パネルの右上隅にあるオプションを使用して、レポートに対して次の操作を実行します。

   * **更新**:ストレージ内の最新のデータでレポートを更新
   * **凡例の色の変更**:レポートの凡例の色を選択して変更する
   * **CSVに書き出し**:レポートからのデータのエクスポートとダウンロードをコンマ区切りファイルに行う

## プロセス期間レポート{#process-duration-report-br}

プロセス期間レポートには、Formsプロセスのインスタンス数が、各インスタンスが実行された日数別に表示されます。

### プロセス期間レポート{#to-execute-a-process-duration-report-br}を実行するには

1. プロセスレポートで事前定義済みのレポートを表示するには、**プロセスレポート**&#x200B;ツリービューで、**レポート**&#x200B;ノードをクリックします。
1. **プロセス期間**&#x200B;レポートノードをクリックします。

   ![process_duration_node](assets/process_duration_node.png)

   レポートを選択すると、ツリービューの右側に&#x200B;**レポートパラメータ**&#x200B;パネルが表示されます。

   ![長時間実行プロセスレポートパラメーター](assets/process_duration_params.png)

   パラメーター:

   * **プロセスの選択** (*必須*):AEM Formsプロセスを選択します。

1. 「**移動**」をクリックして、レポートを実行します。

   レポートは、「プロセスのレポート」ウィンドウの右側の「**レポート**」パネルに表示されます。

   ![process_duration_report](assets/process_duration_report.png)

   **レポート**&#x200B;パネルの右上隅にあるオプションを使用して、レポートに対して次の操作を実行します。

   * **更新**:ストレージ内の最新のデータでレポートを更新
   * **凡例の色の変更**:レポートの凡例の色を選択して変更する
   * **CSVに書き出し**:レポートからのデータのエクスポートとダウンロードをコンマ区切りファイルに行う

## ワークフローボリュームレポート{#workflow-volume-report}

ワークフローボリュームレポートには、AEM Formsプロセスの現在実行中および完了したインスタンスの数がカレンダー日別に表示されます。

### ワークフローボリュームレポート{#to-execute-a-workflow-volume-report-br}を実行するには

1. プロセスレポートで事前定義済みのレポートを表示するには、**プロセスレポート**&#x200B;ツリービューで、**レポート**&#x200B;ノードをクリックします。
1. **Workflow Volume**&#x200B;レポートノードをクリックします。

   ![workflow_volume_node](assets/workflow_volume_node.png)

   レポートを選択すると、ツリービューの右側に&#x200B;**レポートパラメータ**&#x200B;パネルが表示されます。

   ![長時間実行プロセスレポートパラメーター](assets/workflow_volume_params.png)

   パラメーター:

   * **プロセスの選択**(*必須*):AEM Formsプロセスを選択します。
   * **** 後に開始(*オプション*):日付を選択します。指定した日付の後に開始したプロセスインスタンスを表示するようにレポートをフィルターします。
   * **前に開始** (*オプション*):日付を選択します。指定した日付より前に開始したプロセスインスタンスを表示するようにレポートをフィルターします。

1. 「**移動**」をクリックして、レポートを実行します。

   レポートは、**レポートの処理**&#x200B;ウィンドウの右側の&#x200B;**レポート**&#x200B;パネルに表示されます。

   ![workflow_volume_report](assets/workflow_volume_report.png)

   **レポート**&#x200B;パネルの右上隅にあるオプションを使用して、レポートに対して次の操作を実行します。

   * **更新**:ストレージ内の最新のデータでレポートを更新
   * **凡例の色の変更**:レポートの凡例の色を選択して変更する
   * **CSVに書き出し**:レポートからのデータのエクスポートとダウンロードをコンマ区切りファイルに行う
