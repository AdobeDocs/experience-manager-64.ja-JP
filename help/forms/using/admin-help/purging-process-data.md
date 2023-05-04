---
title: プロセスデータの削除
seo-title: Purging process data
description: 長期間有効なプロセスの呼び出し時に生成されるプロセスデータが大きくなりすぎるため、AEM Forms のパフォーマンスが低下し、不要なディスク領域が使用される可能性があります。 プロセスデータをパージする方法を参照してください。
seo-description: Process data that is generated when a long-lived process is invoked can become too large, resulting in lower AEM forms performance and the use of unnecessary disk space. See how you can purge process data.
uuid: 2f04452c-71c6-452c-88c2-7560d35e7dec
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.4/FORMS
discoiquuid: 3157bb92-4b07-40f2-be4c-8f5807f9a380
exl-id: ecedde63-abbb-4e69-901e-1e4b7a59f539
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '230'
ht-degree: 16%

---

# プロセスデータの削除 {#purging-process-data}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

長期間有効なプロセスの呼び出し時に生成されるプロセスデータが大きくなりすぎるため、AEM Forms のパフォーマンスが低下し、不要なディスク領域が使用される可能性があります。 レコードが不要になった場合は、プロセスデータをパージすることをお勧めします。 AEM forms には、プロセスデータをパージするいくつかの方法が用意されています。

* 管理コンソールを使用して、長期間有効なプロセスに関連する古いレコードを 1 回限り削除したり、定期的な自動削除をスケジュールしたりできます。 ( [ジョブマネージャーデータベースからレコードをパージ](/help/forms/using/admin-help/purge-records-job-manager-database.md#purge-records-from-the-job-manager-database).)
* AEM forms Java API と Web サービス API を使用して、長期間有効なプロセスに関連するプロセスデータをプログラムによってパージできます。 ( 詳しくは、 [AEM forms によるプログラミング](https://www.adobe.com/go/learn_aemforms_programming_63_jp).)
* プロセス名と他のパラメータに基づいてプロセスをパージするには、プロセスパージツールを使用します。 詳しくは、*[aem_forms root]*\sdk\misc\Foundation\ProcessPurgeTool\ReadMe.txt にあるプロセス削除ツールの ReadMe ファイルを参照してください。
