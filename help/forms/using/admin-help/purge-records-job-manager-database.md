---
title: ジョブマネージャーのデータベースからの古いレコードの削除
seo-title: Purge records from the Job Manager database
description: プロセスデータが大きいと、AEM forms のパフォーマンスが低下する場合があります。 レコードが不要になった場合は、プロセスデータをパージすることをお勧めします。
seo-description: Large process data can result in lower AEM forms performance. It is good practice to purge process data when records are no longer necessary.
uuid: cf214498-36e9-4dcc-b4d4-e7c46f80dbab
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/health_monitor
products: SG_EXPERIENCEMANAGER/6.4/FORMS
discoiquuid: 69a406f2-4fa8-40bb-b671-7b0f5b6a2c4c
exl-id: be2e2a4b-5aac-4612-81b6-b4bbb3036d77
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '504'
ht-degree: 5%

---

# ジョブマネージャーのデータベースからの古いレコードの削除 {#purge-records-from-the-job-manager-database}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

長期間有効なプロセスの呼び出し時に生成されるプロセスデータが大きくなりすぎるため、AEM Forms のパフォーマンスが低下し、不要なディスク領域が使用される可能性があります。 レコードが不要になった場合は、プロセスデータをパージすることをお勧めします。

管理コンソールを使用して、古いレコードを 1 回限り削除したり、定期的な自動削除をスケジュールしたりできます。 古いレコードをパージするその他の方法については、 [プロセスデータのパージ](/help/forms/using/admin-help/purging-process-data.md#purging-process-data).

**「ジョブ削除スケジューラー」ページへのアクセス**

1. 管理コンソールで、ページの右上隅にある「ヘルスモニター」をクリックします。
1. 「ジョブパージスケジューラー」タブをクリックします。

現在スケジュールされている削除に関する情報が「ジョブパージスケジューラ情報」ボックスに表示されます。

>[!NOTE]
>
>「スケジューラーを停止」をクリックすると、今後スケジュールされたパージは停止されますが、既に進行中のパージジョブは停止されません。

**1 回限りのパージのスケジュール設定**

1. 「1 回のみ」を選択します。
1. 「完了したレコードのパージフィルター」領域で、レコードが古いと見なされ、パージの準備が整った日数または週数を指定します。

   >[!NOTE]
   >
   >完了していないプロセスに関連するレコードは、指定された期間より古い場合でもパージされません。

1. パージを実行するタイミングを指定します。 「現在の日時を使用」チェックボックスをオンにするか、チェックボックスをオフにし、カレンダーアイコンと時計アイコンをクリックして、パージを実行する日時を指定します。

   >[!NOTE]
   >
   >開始日時を過去の日時に指定した場合、「スケジューラーを開始」をクリックするとすぐにパージが実行されます。

1. 「スケジューラーを開始」をクリックします。 以前にスケジューラー設定が行われた場合は、新しい設定に置き換えられます。

**自動パージスケジュールの設定**

1. 「繰り返し間隔」を選択し、パージ間隔の日数または週数を指定します。
1. 「完了したレコードのパージフィルター」領域で、レコードが古いと見なされ、パージの準備が整った日数または週数を指定します。 値を `0` に設定することはできません。

   >[!NOTE]
   >
   >完了していないプロセスに関連するレコードは、指定された期間より古い場合でもパージされません。

1. 削除を開始するタイミングを指定します。 「現在の日時を使用」チェックボックスをオンにするか、チェックボックスをオフにし、カレンダーアイコンと時計アイコンをクリックして、パージを実行する日時を指定します。

   >[!NOTE]
   >
   >過去の開始日時を指定した場合、AEM forms は指定した日付に基づいて次の開始日を論理的に計算します。 例えば、週次で 4 月 7 日から始まるジョブの削除をスケジュールし、現在は 4 月 9 日になっている場合、最初の削除は 4 月 14 日に行われます。

1. 「スケジューラーを開始」をクリックします。 以前にスケジューラー設定が行われた場合は、新しい設定に置き換えられます。
