---
title: プロセスレポートの仕組み
seo-title: プロセスレポートの仕組み
description: JEE上のAEM Forms Process Reportingを構成するサービスの説明とプロセスレポートUIの概要
seo-description: JEE上のAEM Forms Process Reportingを構成するサービスの説明とプロセスレポートUIの概要
uuid: 00a2dd6d-8a6f-4c7b-b03e-81cfd4bcf50d
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: process-reporting
discoiquuid: 4afc68fc-6b39-4c31-95fa-2ef3111c57da
translation-type: tm+mt
source-git-commit: 9ce0d4c714d8ff55c64a884d90462bcd75629ae0

---


# プロセスレポートの仕組み {#how-process-reporting-works}

プロセスレポートは、JEE上のAEM Formsのレポートモジュールです。

プロセスレポートを使用すると、AEM Formsのプロセスとタスクでレポートを実行できます。

Process Reportingは、埋め込みのProcess Reportingリポジトリを使用してFormsデータを発行します。 その後、そのデータを使用してレポートが実行されます。

Process Reportingは、次のモジュールで構成されています。

* [ProcessDataPublisherサービス](/help/forms/using/process-reporting/process-reporting-architecture.md#p-processdatapublisher-service-br-p)
* [ProcessDataStorageサービス](/help/forms/using/process-reporting/process-reporting-architecture.md#p-processdatastorageprovider-service-br-p)
* [OSGi サービス](/help/forms/using/process-reporting/process-reporting-architecture.md#p-osgi-service-br-p)
* [Query Dataサーブレット](/help/forms/using/process-reporting/process-reporting-architecture.md#p-querydataservlet-service-br-p)
* [Process Reportingユーザーインターフェイス](/help/forms/using/process-reporting/process-reporting-architecture.md#p-process-reporting-user-interface-br-p)

## Process Reportingアーキテクチャ {#process-reporting-architecture-br}

![processingreportingarchitecture](assets/processreportingarchitecture.png)

## プロセスレポートモジュール {#process-reporting-modules}

### ProcessDataPublisherサービス {#processdatapublisher-service-br}

ProcessDataPublisherサーバーは、定期的にAEM Formsデータベース上で実行され、サービスの最後の実行以降に変更されたデータを抽出します。 次に、データをProcess Data Storageサービスに発行します。

サービスの設定について詳しくは、「ProcessDataPublisherサービスの設定」 [を参照してください](/help/forms/using/process-reporting/install-start-process-reporting.md#p-reportconfiguration-service-p)。

### ProcessDataStorageProviderサービス {#processdatastorageprovider-service-br}

ProcessDataStorageProviderサービスは、ProcessDataPublisherサービスからプロセスデータを受け取り、データをProcess Reportingリポジトリに保存します。

サービスの設定について詳しくは、「ProcessDataStorageProviderサービスの設 [定」を参照してくださ](/help/forms/using/process-reporting/install-start-process-reporting.md#p-to-configure-the-process-reporting-repository-locations-p)い。

### OSGi サービス {#osgi-service-br}

QueryDataServletは、このサービスを使用して、Process Reportingリポジトリからレポートデータを取得します。

### QueryDataServletサービス {#querydataservlet-service-br}

QueryDataServletサービスは、Process Reportingユーザーインターフェイスからクエリーを受け入れます。

次に、サービスはOSGiサービスを使用して関連するレポートデータを取得し、データを処理し、ユーザーインターフェイスにデータを返します。

### Process Reportingユーザーインターフェイス {#process-reporting-user-interface-br}

Process Reportingユーザーインターフェイスは、Webブラウザーベースのインターフェイスです。 このインターフェイスを使用して、AEM Formsデータベースから発行されたプロセスおよびタスクの情報を表示します。

### QueryDataServletサービス {#querydataservlet-service-br-1}

QueryDataServletサービスは、Process Reportingユーザーインターフェイスからクエリーを受け入れます。

次に、サービスはOSGiサービスを使用して関連するレポートデータを取得し、データを処理し、ユーザーインターフェイスにデータを返します。

### カスタムレポート {#custom-reports-br}

独自のカスタムレポートを作成し、これらのレポートをプロセスレポートユーザーインターフェイスの「カスタムレポート」タブに表示できます。

カスタムレポートを作成する手順については、「カスタムレポートを作成するには」を参照し [てください](/help/forms/using/process-reporting/process-reporting-custom-reports.md)。

[サポートへのお問い合わせ](https://www.adobe.com/account/sign-in.supportportal.html)
