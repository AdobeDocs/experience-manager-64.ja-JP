---
title: プロセス・レポートの仕組み
seo-title: How Process Reporting Works
description: JEE 上のAEM Forms Process Reporting を構成するサービスの説明と Process Reporting UI の概要
seo-description: Description of the services that make up the AEM Forms on JEE Process Reporting and an introduction to the Process Reporting UI
uuid: 00a2dd6d-8a6f-4c7b-b03e-81cfd4bcf50d
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: process-reporting
discoiquuid: 4afc68fc-6b39-4c31-95fa-2ef3111c57da
exl-id: 05ef8b08-bb1d-441d-8b02-5f047efbabcb
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '345'
ht-degree: 1%

---

# プロセス・レポートの仕組み {#how-process-reporting-works}

Process Reporting は、JEE 上のAEM Formsのレポートモジュールです。

プロセスレポートを使用すると、AEM Formsのプロセスとタスクに関するレポートを実行できます。

Process Reporting は、組み込みの Process Reporting リポジトリを使用してFormsデータを公開します。 その後、そのデータを使用してレポートを実行します。

Process Reporting は、次のモジュールで構成されています。

* [ProcessDataPublisher サービス](/help/forms/using/process-reporting/process-reporting-architecture.md#p-processdatapublisher-service-br-p)
* [ProcessDataStorage サービス](/help/forms/using/process-reporting/process-reporting-architecture.md#p-processdatastorageprovider-service-br-p)
* [OSGi サービス](/help/forms/using/process-reporting/process-reporting-architecture.md#p-osgi-service-br-p)
* [クエリデータサーブレット](/help/forms/using/process-reporting/process-reporting-architecture.md#p-querydataservlet-service-br-p)
* [Process Reporting ユーザーインターフェイス](/help/forms/using/process-reporting/process-reporting-architecture.md#p-process-reporting-user-interface-br-p)

## プロセスレポートのアーキテクチャ {#process-reporting-architecture-br}

![processreportingarchitecture](assets/processreportingarchitecture.png)

## プロセスレポートモジュール {#process-reporting-modules}

### ProcessDataPublisher サービス {#processdatapublisher-service-br}

ProcessDataPublisher サーバーは、AEM Formsデータベースで定期的に実行され、サービスの最後の実行以降に変更されたデータを抽出します。 次に、データを Process Data Storage サービスに公開します。

サービスの設定について詳しくは、 [ProcessDataPublisher サービスを設定する](/help/forms/using/process-reporting/install-start-process-reporting.md#p-reportconfiguration-service-p).

### ProcessDataStorageProvider サービス {#processdatastorageprovider-service-br}

ProcessDataStorageProvider サービスは、ProcessDataPublisher サービスからプロセスデータを受け取り、そのデータを Process Reporting リポジトリに保存します。

サービスの設定について詳しくは、 [ProcessDataStorageProvider サービスの設定](/help/forms/using/process-reporting/install-start-process-reporting.md#p-to-configure-the-process-reporting-repository-locations-p).

### OSGi サービス {#osgi-service-br}

QueryDataServlet は、このサービスを使用して、Process Reporting リポジトリからレポートデータを取得します。

### QueryDataServlet サービス {#querydataservlet-service-br}

QueryDataServlet サービスは、Process Reporting ユーザーインターフェイスからクエリを受け入れます。

次に、このサービスは OSGi サービスを使用して関連するレポートデータを取得し、そのデータを処理して、ユーザーインターフェイスにデータを返します。

### Process Reporting ユーザーインターフェイス {#process-reporting-user-interface-br}

Process Reporting のユーザー・インタフェースは、Web ブラウザ・ベースのインタフェースです。 このインターフェイスを使用して、AEM Formsデータベースから公開されたプロセスおよびタスク情報を表示します。

### QueryDataServlet サービス {#querydataservlet-service-br-1}

QueryDataServlet サービスは、Process Reporting ユーザーインターフェイスからクエリを受け入れます。

次に、このサービスは OSGi サービスを使用して関連するレポートデータを取得し、そのデータを処理して、ユーザーインターフェイスにデータを返します。

### カスタムレポート {#custom-reports-br}

独自のカスタムレポートを作成し、これらのレポートをプロセスレポートユーザーインターフェイスの「カスタムレポート」タブに表示できます。

カスタムレポートを作成する手順については、この記事の「カスタムレポートを作成するには」を参照してください。 [処理中のレポートのカスタムレポート](/help/forms/using/process-reporting/process-reporting-custom-reports.md).
