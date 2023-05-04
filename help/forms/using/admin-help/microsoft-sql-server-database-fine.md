---
title: "Microsoft SQL Server データベース：設定の最適なチューニング"
seo-title: "Microsoft SQL Server database: Fine-tuning the configuration"
description: Microsoft SQL Server データベースの設定の最適なチューニング方法について説明します。
seo-description: Learn how you can fine tune the configuration of your Microsoft SQL Server database.
uuid: 2d618aab-3c67-4edb-a28f-a20904689e6f
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.4/FORMS, SG_AEMFORMS
discoiquuid: 70559a94-42ea-411a-a32f-5f38bc17ff96
exl-id: 5392027c-eb5a-49c4-bf9b-fe7d399ae0a1
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '330'
ht-degree: 10%

---

# Microsoft SQL Server データベース：設定の最適なチューニング {#microsoft-sql-server-database-fine-tuning-the-configuration}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

Microsoft SQL Server を使用する場合は、デフォルトの設定を変更する必要があります。 Enterprise Manager でローカル・サーバーを右クリックして、Oracle・ダイアログ・ボックスにアクセスします。

## メモリ設定 {#memory-settings}

最小メモリ割り当てをできるだけ大きい数に変更します。 データベースが別のコンピュータで実行されている場合は、すべてのメモリを使用します。 デフォルト設定では、積極的にメモリを割り当てないので、ほとんどのデータベースでのパフォーマンスが低下します。 実稼動マシンにメモリを割り当てる際は、最も積極的に行う必要があります。

## プロセッサ設定 {#processor-settings}

プロセッサの設定を変更し、最も重要な点は、[Windows での SQL Server の優先度を上げる ] チェックボックスをオンにして、サーバができるだけ多くのサイクルを使用できるようにします。 [NT ファイバを使用 ] の設定はあまり重要ではありませんが、この設定を選択することもできます。

## データベース設定 {#database-settings}

データベース設定を変更します。 最も重要な設定は、クラッシュ後に回復を待機する最大時間を指定する [ 回復間隔 ] です。 デフォルト設定は 1 分です。 5 ～ 15 分の大きな値を使用すると、サーバはデータベースログからデータベースファイルに変更を書き戻す時間を長くするので、パフォーマンスが向上します。

>[!NOTE]
>
>この設定では、起動時に実行する必要のあるログファイルの再生の長さのみが変更されるので、トランザクション動作に影響はありません。

ログとデータ・ファイルの両方の「Space Allocated」サイズを、初期のデータベースよりも大きく設定します。 1 年間にデータベースがどの程度増大するかを検討します。 ログファイルとデータファイルは、連続した範囲で割り当てられ、データがディスク全体で断片化されるのを防ぐのが理想的です。
