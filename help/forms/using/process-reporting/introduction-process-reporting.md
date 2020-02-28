---
title: プロセスレポートの概要
seo-title: プロセスレポートの概要
description: JEE上のAEM Forms Process Reportingの概要と主な機能
seo-description: JEE上のAEM Forms Process Reportingの概要と主な機能
uuid: a33ea729-7e1f-4093-bdb6-b8dc3afd59a7
content-type: reference
topic-tags: process-reporting
products: SG_EXPERIENCEMANAGER/6.4/FORMS
discoiquuid: 0cfe62b8-839e-414b-95e5-1bfce6a9d16a
translation-type: tm+mt
source-git-commit: 9ce0d4c714d8ff55c64a884d90462bcd75629ae0

---


# プロセスレポートの概要 {#introduction-to-process-reporting}

![プロセス報告](assets/process-reporting.png)

プロセスレポートは、AEM Formsのプロセスとタスクに関するレポートを作成および表示するために使用するブラウザベースのツールです。

プロセスレポートは、すぐに使用できる一連のレポートを提供し、長時間実行中のプロセス、プロセス期間、ワークフローの量に関する情報をフィルター、表示できます。

追加のプロセスレポートは、アドホッククエリを実行し、カスタムレポートビューをプロセスレポートユーザーインターフェイスに統合するためのインターフェイスを提供します。

サポートされるブラウザのリストについては、「 [AEM Formsでサポートされるプラットフォーム](/help/forms/using/aem-forms-jee-supported-platforms.md)」を参照してください。

Process Reportingは、次の機能を持つモジュールに基づいて構築されています。

* AEM Formsデータベースからのプロセスデータの読み取り
* 埋め込みのProcess Reportingリポジトリへのプロセスデータの発行
* レポートを表示するためのブラウザベースのユーザインターフェイスを提供します。

## Key Capabilities {#key-capabilities}

### 常にオンのレポート {#always-on-reporting}

![現場管理](assets/site-management.png)

長時間実行されるプロセスのリスト、プロセス期間グラフの表示、およびフィルターを使用したカスタムクエリの実行を行います。

また、プロセスレポートには、レポートおよびクエリデータをCSV形式で書き出すオプションも用意されています。

### アドホックレポート {#adhoc-reports}

![print-&amp;-color](assets/print-&-colour.png)

フィルターを使用して、データの特定のビューを取得します。

ID、期間、開始日と終了日、プロセス開始者などでプロセスやタスクを検索できます。

複数のフィルターを組み合わせて、特定のレポートを作成できます。

その後、後で実行するようにレポートフィルターを保存できます。

### プロセス/タスクの履歴 {#process-task-history}

![ファイル管理](assets/file-management.png)

AEM Formsサーバーは、多数のプロセスを並行して実行します。 これらのプロセスは、ある状態から別の状態への移行を継続します。 Formsデータを一定の間隔でProcess Reportingリポジトリに発行すると、Process ReportingはAEM Formsで実行されているプロセスに関する移行情報を保持します。

### アクセス制御 {#access-control-br}

![無題の](assets/untitled.png)

Process Reporingは、ユーザーインターフェイスへの権限ベースのアクセスを提供します。

つまり、レポート権限を持つユーザーのみがプロセスレポートのユーザーインターフェイスにアクセスできます。

[サポートへのお問い合わせ](https://www.adobe.com/account/sign-in.supportportal.html)
