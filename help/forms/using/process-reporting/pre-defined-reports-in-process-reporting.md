---
title: プロセスレポートの事前定義済みレポート
seo-title: プロセスレポートの事前定義済みレポート
description: JEE上のAEM Formsのプロセスデータを使用して、長時間実行しているプロセス、プロセス期間、ワークフローの量に関するレポートを作成するクエリ
seo-description: JEE上のAEM Formsのプロセスデータを使用して、長時間実行しているプロセス、プロセス期間、ワークフローの量に関するレポートを作成するクエリ
uuid: ba3a1809-270e-4c94-ade4-d2f6af86d860
content-type: reference
topic-tags: process-reporting
products: SG_EXPERIENCEMANAGER/6.4/FORMS
discoiquuid: 6320c632-c7ec-4e56-9d12-cd27e3e9306e
translation-type: tm+mt
source-git-commit: 79dcf6816e1156604c0c9279b727ea436ad1826a
workflow-type: tm+mt
source-wordcount: '723'
ht-degree: 0%

---


# プロセスレポートの事前定義済みレポート {#pre-defined-reports-in-process-reporting}

AEM Formsプロセスレポートには、次 *の既成のレポートが付属しています* 。

* **[Long Running Processes](/help/forms/using/process-reporting/pre-defined-reports-in-process-reporting.md#p-long-running-processes-p)**: 完了に指定時間以上かかったすべてのAEM Formsプロセスのレポート

* **[プロセス期間グラフ](/help/forms/using/process-reporting/pre-defined-reports-in-process-reporting.md#p-process-duration-report-br-p)**: 期間別の特定AEM Formsプロセスのレポート

* **[ワークフローの量](/help/forms/using/process-reporting/pre-defined-reports-in-process-reporting.md#p-workflow-volume-report-p)**: 日付別に指定されたプロセスの実行中および完了インスタンスのレポート

## 長時間実行するプロセス {#long-running-processes}

長時間実行中のプロセスレポートには、完了に指定時間以上かかったAEM Formsのプロセスが表示されます。

### 「Long Running Process」レポートを実行するには {#to-execute-a-long-running-process-report-br}

1. プロセスレポートで事前定義済みのレポートのリストを表示するには、 **プロセスレポート** ツリー表示で、 **レポート** ノードをクリックします。
1. 「 **Long Running Processes** 」レポートノードをクリックします。

   ![long_running_node](assets/long_running_node.png)

   レポートを選択すると、ツリー表示の右側に **[レポートパラメータ** ]パネルが表示されます。

   ![長時間実行プロセスレポートパラメーター](assets/report_parameters_panel.png)

   パラメーター:

   * **期間**(*必須*): 期間と単位を指定します。 指定した期間を超えて実行されたすべてのAEM Formsプロセスを表示します。
   * **開始後** (*オプション*): 日付を選択します。 レポートをフィルターして、指定した日付以降に開始したプロセスインスタンスを表示します。
   * **以前に開始** (*オプション*): 日付を選択します。 指定した日付より前に開始したプロセスインスタンスを表示するように、レポートをフィルターします。

1. 「 **移動** 」をクリックしてレポートを実行します。

   レポートは、 **プロセスレポート** ( **Process Management** )ウィンドウの右側のレポートパネルに表示されます。

   ![long_running_processes](assets/long_running_processes.png)

   レポートパネルの右上隅にあるオプションを使用して、 **レポートに対して次の操作を実行します** 。

   * **更新**: ストレージ内の最新データを使用してレポートを更新します
   * **凡例の色を変更**: レポートの凡例の色を選択して変更する
   * **CSVにエクスポート**: レポートからデータをエクスポートし、コンマ区切りファイルにダウンロードする

## プロセス期間レポート {#process-duration-report-br}

プロセス期間レポートは、Formsプロセスのインスタンス数を、各インスタンスが実行された日数別に表示します。

### プロセス期間レポートを実行するには {#to-execute-a-process-duration-report-br}

1. プロセスレポートで事前定義済みのレポートを表示するには、 **プロセスレポート** ツリー表示で、 **レポート** ノードをクリックします。
1. 「 **プロセス期間** 」レポートノードをクリックします。

   ![process_duration_node](assets/process_duration_node.png)

   レポートを選択すると、ツリー表示の右側に **[レポートパラメータ** ]パネルが表示されます。

   ![長時間実行プロセスレポートパラメーター](assets/process_duration_params.png)

   パラメーター:

   * **Select Process** (*必須*): AEM Formsプロセスを選択します。

1. 「 **移動** 」をクリックしてレポートを実行します。

   レポートがプロセスレポートウィンドウの右側の **レポート** パネルに表示されます。

   ![process_duration_report](assets/process_duration_report.png)

   レポートパネルの右上隅にあるオプションを使用して、 **レポートに対して次の操作を実行します** 。

   * **更新**: ストレージ内の最新データを使用してレポートを更新します
   * **凡例の色を変更**: レポートの凡例の色を選択して変更する
   * **CSVにエクスポート**: レポートからデータをエクスポートし、コンマ区切りファイルにダウンロードする

## ワークフローボリュームレポート {#workflow-volume-report}

ワークフローの量レポートには、現在実行中の、および完了したAEM Formsプロセスのインスタンス数がカレンダーの日別に表示されます。

### ワークフローボリュームレポートを実行するには {#to-execute-a-workflow-volume-report-br}

1. プロセスレポートで事前定義済みのレポートを表示するには、 **プロセスレポート** ツリー表示で、 **レポート** ノードをクリックします。
1. 「 **ワークフローボリューム** 」レポートノードをクリックします。

   ![workflow_volume_node](assets/workflow_volume_node.png)

   レポートを選択すると、ツリー表示の右側に **[レポートパラメータ** ]パネルが表示されます。

   ![長時間実行プロセスレポートパラメーター](assets/workflow_volume_params.png)

   パラメーター:

   * **Select Process**(*mandatory*): AEM Formsプロセスを選択します。
   * **開始後** (*オプション*): 日付を選択します。 指定した日付以降に開始したプロセスインスタンスを表示するフィルターをレポートに追加します。
   * **以前に開始** (*オプション*): 日付を選択します。 指定した日付より前に開始したプロセスインスタンスを表示するフィルターをレポートに追加します。

1. 「 **移動** 」をクリックしてレポートを実行します。

   レポートは、 **プロセスレポート** ( **Process Management** )ウィンドウの右側のレポートパネルに表示されます。

   ![workflow_volume_report](assets/workflow_volume_report.png)

   レポートパネルの右上隅にあるオプションを使用して、 **レポートに対して次の操作を実行します** 。

   * **更新**: ストレージ内の最新データを使用してレポートを更新します
   * **凡例の色を変更**: レポートの凡例の色を選択して変更する
   * **CSVにエクスポート**: レポートからデータをエクスポートし、コンマ区切りファイルにダウンロードする

