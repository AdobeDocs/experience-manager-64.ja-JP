---
title: '"DB2 データベース：週単位のプロセス実行"'
seo-title: 'DB2 database: Running a process weekly'
description: AEM Forms DB2 データベースのパフォーマンスを向上させる方法について説明します。
seo-description: See how you can improve the performance of your AEM forms DB2 database.
uuid: 36070087-c250-41df-a841-aa922e777697
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.4/FORMS
discoiquuid: fc0e8183-5d50-4fc0-997a-5f3168ba0d70
exl-id: f40fcfab-63e0-4e43-aac5-95426e3dd1fb
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 100%

---

# DB2 データベース：週単位のプロセス実行{#db-database-running-a-process-weekly}

ご使用の AEM forms DB2 データベースの動作が遅くなり始めたら、週単位で以下のプロセスを実行することで、パフォーマンスが向上します。

1. DB2 コントロールセンターを起動します。

   （Windows）スタート／すべてのプログラム／IBM DB2／General Administration Tools／Control Center を選択します。

   （Linux および UNIX）コマンドプロンプトから、`db2jcc` コマンドを入力します。

1. DB2 コントロールセンターのオブジェクトツリーで、「All Databases」をクリックします。
1. AEM Forms 用に作成したデータベースをクリックして、Tables フォルダーをクリックします。
1. コンテンツウィンドウ内のデータベーステーブルをすべて選択し、それらを右クリックして「Run Statistics」を選択します。
1. Statistics／Index Statistics に移動します。
1. 「Collect Statistics For All Indexes」を選択し、「Collect Statistics For Indexes With Extended Detailed Statistics」を選択して、「OK」をクリックします。

プロセスが完了すると、メッセージが表示されます。メッセージを閉じます。
