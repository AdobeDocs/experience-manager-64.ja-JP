---
title: プロセスレポートの事前定義済みレポート
seo-title: プロセスレポートの事前定義済みレポート
description: JEE上のAEM Formsプロセスデータに対するクエリを実行し、長時間実行しているプロセス、プロセス期間、ワークフローボリュームに関するレポートを作成します
seo-description: JEE上のAEM Formsプロセスデータに対するクエリを実行し、長時間実行しているプロセス、プロセス期間、ワークフローボリュームに関するレポートを作成します
uuid: ba3a1809-270e-4c94-ade4-d2f6af86d860
content-type: reference
topic-tags: process-reporting
products: SG_EXPERIENCEMANAGER/6.4/FORMS
discoiquuid: 6320c632-c7ec-4e56-9d12-cd27e3e9306e
translation-type: tm+mt
source-git-commit: ec74a1c3b1d3686a1f5216e06dfc33dc1dccfb2f

---


# プロセスレポートの事前定義済みレポート {#pre-defined-reports-in-process-reporting}

AEM Forms Process Reportingには、次の追加設 *定不要のレポートが付属します* 。

* **[Long Running Processes](/help/forms/using/process-reporting/pre-defined-reports-in-process-reporting.md#p-long-running-processes-p)**:完了に指定時間以上かかったすべてのAEM Formsプロセスのレポート

* **[プロセス期間グラフ](/help/forms/using/process-reporting/pre-defined-reports-in-process-reporting.md#p-process-duration-report-br-p)**:期間別の指定されたAEM Formsプロセスのレポート

* **[Workflow Volume](/help/forms/using/process-reporting/pre-defined-reports-in-process-reporting.md#p-workflow-volume-report-p)**:指定したプロセスの実行中および完了済みインスタンスの日付別レポート

## 長時間実行するプロセス {#long-running-processes}

長時間実行中のプロセスレポートは、完了に指定時間以上かかったAEM Formsプロセスを表示します。

### 長時間実行中のプロセスレポートを実行するには {#to-execute-a-long-running-process-report-br}

1. プロセスレポートで事前定義済みのレポートのリストを表示するには、「 **Process Reporting** 」ツリービューで、「 **Reports** 」ノードをクリックします。
1. 「 **Long Running Processes」レポートノードをクリックします** 。

   ![long_running_node](assets/long_running_node.png)

   レポートを選択すると、ツリ **ービューの右側に[レポートパラメータ** ]パネルが表示されます。

   ![長時間実行中のプロセスのレポートパラメーターパネル](assets/report_parameters_panel.png)

   パラメーター:

   * **期間**(*必須*):期間と時間の単位を指定します。 指定した期間以上実行されたすべてのAEM Formsプロセスを表示します。
   * **開始日** (オ&#x200B;*プション*):日付を選択します。 レポートをフィルターして、指定した日付以降に開始したプロセスインスタンスを表示します。
   * **以前に開始** (オ&#x200B;*プション*):日付を選択します。 指定した日付より前に開始したプロセスインスタンスを表示するように、レポートをフィルターします。

1. 「移動 **** 」をクリックしてレポートを実行します。

   レポートは、「プロセスレポート」ウィンドウの右側の「**レポート* **** 」パネルに表示されます。

   ![long_running_processes](assets/long_running_processes.png)

   **Report **panelの右上隅にあるオプションを使用して、レポートに対して次の操作を実行します。

   * **更新**:ストレージに存在する最新のデータでレポートを更新
   * **凡例の色を変更**:レポートの凡例の色を選択して変更する
   * **CSVにエクスポート**:レポートからデータを書き出し、コンマ区切りファイルにダウンロードします

## プロセス期間レポート {#process-duration-report-br}

プロセス期間レポートは、Formsプロセスのインスタンス数を各インスタンスが実行された日数別に表示します。

### プロセス期間レポートを実行するには {#to-execute-a-process-duration-report-br}

1. プロセスレポートで事前定義済みのレポートを表示するには、「 **Process Reporting** 」ツリービューで **、「** Reports」ノードをクリックします。
1. 「プロセス期間」 **レポートノードをクリック** します。

   ![process_duration_node](assets/process_duration_node.png)

   レポートを選択すると、ツリ **ービューの右側に[レポートパラメータ** ]パネルが表示されます。

   ![長時間実行中のプロセスのレポートパラメーターパネル](assets/process_duration_params.png)

   パラメーター:

   * **Select Process** (必&#x200B;*須*):AEM formsプロセスを選択します。

1. 「移動 **** 」をクリックしてレポートを実行します。

   このレポートは、「プロセスレ **ポート** 」ウィンドウの右側のレポートパネルに表示されます。

   ![process_duration_report](assets/process_duration_report.png)

   レポートパネルの右上隅にあるオプションを **使用して** 、レポートに対して次の操作を実行します。

   * **更新**:ストレージに存在する最新のデータでレポートを更新
   * **凡例の色を変更**:レポートの凡例の色を選択して変更する
   * **CSVにエクスポート**:レポートからデータを書き出し、コンマ区切りファイルにダウンロードします

## ワークフローの量レポート {#workflow-volume-report}

ワークフローの量レポートは、AEM Formsプロセスの現在実行中および完了したインスタンスの数をカレンダーの日別に表示します。

### ワークフローボリュームレポートを実行するには {#to-execute-a-workflow-volume-report-br}

1. プロセスレポートで事前定義済みのレポートを表示するには、「 **Process Reporting** 」ツリービューで **、「** Reports」ノードをクリックします。
1. 「ワークフローの **量」レポートノード** をクリックします。

   ![workflow_volume_node](assets/workflow_volume_node.png)

   レポートを選択すると、ツリ **ービューの右側に[レポートパラメータ** ]パネルが表示されます。

   ![長時間実行中のプロセスのレポートパラメーターパネル](assets/workflow_volume_params.png)

   パラメーター:

   * **Select Process**(*必須*):AEM formsプロセスを選択します。
   * **開始日** (オ&#x200B;*プション*):日付を選択します。 レポートをフィルターして、指定した日付以降に開始したプロセスインスタンスを表示します。
   * **以前に開始** (オ&#x200B;*プション*):日付を選択します。 指定した日付より前に開始したプロセスインスタンスを表示するようにレポートをフィルターします。

1. 「移動 **** 」をクリックしてレポートを実行します。

   レポートは、 **Process Reporting** （プロセスレポート）ウィンドウの右側の **Report** （レポート）パネルに表示されます。

   ![workflow_volume_report](assets/workflow_volume_report.png)

   レポートパネルの右上隅にあるオプションを **使用して** 、レポートに対して次の操作を実行します。

   * **更新**:ストレージに存在する最新のデータでレポートを更新
   * **凡例の色を変更**:レポートの凡例の色を選択して変更する
   * **CSVにエクスポート**:レポートからデータを書き出し、コンマ区切りファイルにダウンロードします

[サポートへのお問い合わせ](https://www.adobe.com/account/sign-in.supportportal.html)
