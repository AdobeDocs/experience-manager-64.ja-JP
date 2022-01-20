---
title: プロセスレポートの事前定義済みレポート
seo-title: Pre-defined reports in Process Reporting
description: JEE 上のAEM Formsプロセスデータのクエリを実行して、長時間実行中のプロセス、プロセス期間、ワークフローボリュームに関するレポートを作成します。
seo-description: Query for AEM Forms on JEE process data to create reports on long running processes, Process duration, and Workflow volume
uuid: ba3a1809-270e-4c94-ade4-d2f6af86d860
content-type: reference
topic-tags: process-reporting
products: SG_EXPERIENCEMANAGER/6.4/FORMS
discoiquuid: 6320c632-c7ec-4e56-9d12-cd27e3e9306e
exl-id: 21f5fb7e-53b3-485d-9b6a-813182f14781
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '698'
ht-degree: 0%

---

# プロセスレポートの事前定義済みレポート {#pre-defined-reports-in-process-reporting}

AEM Forms Process Reporting には次の機能が付属しています *すぐに使える* レポート：

* **[長時間実行されるプロセス](/help/forms/using/process-reporting/pre-defined-reports-in-process-reporting.md#p-long-running-processes-p)**:指定した時間以上かかったすべてのAEM Formsプロセスのレポート

* **[プロセス期間のグラフ](/help/forms/using/process-reporting/pre-defined-reports-in-process-reporting.md#p-process-duration-report-br-p)**:期間別の指定したAEM Formsプロセスのレポート

* **[ワークフローボリューム](/help/forms/using/process-reporting/pre-defined-reports-in-process-reporting.md#p-workflow-volume-report-p)**:指定したプロセスの実行中および完了したインスタンスの日別レポート

## 長時間実行されるプロセス {#long-running-processes}

長時間実行プロセスレポートには、指定した時間以上かかったAEM Formsプロセスが表示されます。

### 「長時間実行プロセス」レポートを実行する手順は、次のとおりです。 {#to-execute-a-long-running-process-report-br}

1. プロセス・レポートで事前定義済レポートのリストを表示するには、 **プロセスのレポート** ツリー表示で、 **レポート** ノード。
1. 次をクリック： **長時間実行されるプロセス** レポートノードを使用します。

   ![long_running_node](assets/long_running_node.png)

   レポートを選択すると、 **レポートのパラメーター** ツリービューの右側にパネルが表示されます。

   ![長時間実行プロセスレポートパラメータパネル](assets/report_parameters_panel.png)

   パラメーター:

   * **期間**(*必須*):期間と時間の単位を指定します。 指定された期間以上実行されたすべてのAEM Formsプロセスを表示します。
   * **次の日から開始** (*オプション*):日付を選択します。 指定した日付の後に開始したプロセスインスタンスを表示するように、レポートをフィルターします。
   * **次より前に開始** (*オプション*):日付を選択します。 指定した日付の前に開始したプロセスインスタンスを表示するように、レポートをフィルターします。

1. クリック **移動** をクリックしてレポートを実行します。

   レポートが **レポート** 右側のパネル **プロセスのレポート** ウィンドウ

   ![long_running_processes](assets/long_running_processes.png)

   の右上隅にあるオプションを使用します。 **レポート** パネルを使用して、レポートに対して次の操作を実行します。

   * **更新**:ストレージに存在する最新のデータでレポートを更新します
   * **凡例の色を変更**:レポートの凡例の色を選択および変更する
   * **CSV に書き出し**:レポートのデータをコンマ区切りファイルにエクスポートしてダウンロードする

## プロセス期間レポート {#process-duration-report-br}

プロセス期間レポートには、Formsプロセスのインスタンス数が、各インスタンスが実行された日数別に表示されます。

### 「プロセス期間」レポートを実行するには、以下を実行します。 {#to-execute-a-process-duration-report-br}

1. プロセスレポートで事前定義されたレポートを表示するには、 **プロセスのレポート** ツリー表示で、 **レポート** ノード。
1. 次をクリック： **プロセスの期間** レポートノードを使用します。

   ![process_duration_node](assets/process_duration_node.png)

   レポートを選択すると、 **レポートのパラメーター** ツリービューの右側にパネルが表示されます。

   ![長時間実行プロセスレポートパラメータパネル](assets/process_duration_params.png)

   パラメーター:

   * **プロセスを選択** (*必須*):AEM Formsプロセスを選択します。

1. クリック **移動** をクリックしてレポートを実行します。

   レポートが **レポート** 「プロセス・レポート」ウィンドウの右側にあるパネル。

   ![process_duration_report](assets/process_duration_report.png)

   の右上隅にあるオプションを使用します。 **レポート** パネルを使用して、レポートに対して次の操作を実行します。

   * **更新**:ストレージに存在する最新のデータでレポートを更新します
   * **凡例の色を変更**:レポートの凡例の色を選択および変更する
   * **CSV に書き出し**:レポートのデータをコンマ区切りファイルにエクスポートしてダウンロードする

## ワークフローボリュームレポート {#workflow-volume-report}

ワークフローボリュームレポートには、AEM Formsプロセスの現在実行中および完了したインスタンスの数がカレンダー日別に表示されます。

### ワークフローボリュームレポートを実行するには {#to-execute-a-workflow-volume-report-br}

1. プロセスレポートで事前定義されたレポートを表示するには、 **プロセスのレポート** ツリー表示で、 **レポート** ノード。
1. 次をクリック： **ワークフローボリューム** レポートノードを使用します。

   ![workflow_volume_node](assets/workflow_volume_node.png)

   レポートを選択すると、 **レポートのパラメーター** ツリービューの右側にパネルが表示されます。

   ![長時間実行プロセスレポートパラメータパネル](assets/workflow_volume_params.png)

   パラメーター:

   * **プロセスを選択**(*必須*):AEM Formsプロセスを選択します。
   * **次の日から開始** (*オプション*):日付を選択します。 指定した日付の後に開始したプロセスインスタンスを表示するように、レポートをフィルターします。
   * **次より前に開始** (*オプション*):日付を選択します。 指定した日付の前に開始したプロセスインスタンスを表示するように、レポートをフィルターします。

1. クリック **移動** をクリックしてレポートを実行します。

   レポートが **レポート** 右側のパネル **プロセスのレポート** ウィンドウ

   ![workflow_volume_report](assets/workflow_volume_report.png)

   の右上隅にあるオプションを使用します。 **レポート** パネルを使用して、レポートに対して次の操作を実行します。

   * **更新**:ストレージに存在する最新のデータでレポートを更新します
   * **凡例の色を変更**:レポートの凡例の色を選択および変更する
   * **CSV に書き出し**:レポートのデータをコンマ区切りファイルにエクスポートしてダウンロードする
