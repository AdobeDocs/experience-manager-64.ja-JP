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
exl-id: 279b2f89-5b91-4b8f-ab0f-8ade9b9f3932
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 0%

---

# プロセスレポートの概要{#introduction-to-process-reporting}

![プロセスレポート](assets/process-reporting.png)

プロセスレポートは、AEM Formsのプロセスとタスクに関するレポートを作成および表示するために使用する、ブラウザーベースのツールです。

Process Reportingは、長時間実行されるプロセス、プロセス期間、ワークフローの量に関する情報をフィルター、表示できる、あらかじめ用意された一連のレポートを提供します。

また、プロセス・レポートは、アドホック・クエリを実行し、カスタム・レポート・ビューをプロセス・レポートのユーザー・インタフェースに統合するためのインタフェースを提供します。

サポートされているブラウザーの一覧については、「[AEM Formsでサポートされているプラットフォーム](/help/forms/using/aem-forms-jee-supported-platforms.md)」を参照してください。

Process Reportingは、次のモジュールに基づいて構築されています。

* AEM Forms Databaseからのプロセスデータの読み取り
* 埋め込みのProcess Reportingリポジトリへのプロセスデータの公開
* レポートを表示するためのブラウザーベースのユーザーインターフェイスを提供します

## 主な機能{#key-capabilities}

### 常時稼動するレポート{#always-on-reporting}

![site-management](assets/site-management.png)

長時間実行されているプロセスのリスト、プロセス期間グラフの表示、フィルターを使用したカスタムクエリの実行を行います。

プロセスレポートには、レポートおよびクエリデータをCSV形式で書き出すオプションも用意されています。

### アドホックレポート{#adhoc-reports}

![print-&amp;-color](assets/print-&-colour.png)

フィルターを使用して、データの特定の表示を取得します。

ID、期間、開始日と終了日、プロセス開始者などを基準にして、プロセスまたはタスクを検索できます。

複数のフィルターを組み合わせて、特定のレポートを作成できます。

その後、後で実行するようにレポートフィルターを保存できます。

### プロセス/タスクの履歴{#process-task-history}

![ファイル管理](assets/file-management.png)

AEM Formsサーバーは、多数のプロセスを並行して実行します。 これらのプロセスは、ある状態から別の状態への移行を継続します。 Formsのデータを一定の間隔でProcess Reportingリポジトリに公開すると、Process ReportingはAEM Formsで実行されているプロセスに関する移行情報を保持します。

### アクセス制御 {#access-control-br}

![名称未設定](assets/untitled.png)

Process Reportingは、ユーザーインターフェイスに対する権限ベースのアクセスを提供します。

つまり、レポート権限を持つユーザーのみがProcess Reportingユーザーインターフェイスにアクセスできます。
