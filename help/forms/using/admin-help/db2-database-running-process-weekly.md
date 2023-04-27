---
title: "DB2 データベース：毎週プロセスを実行"
seo-title: "DB2 database: Running a process weekly"
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
ht-degree: 26%

---

# DB2 データベース：週単位のプロセス実行{#db-database-running-a-process-weekly}

AEM forms DB2 データベースの実行が遅くなり始めた場合は、次のプロセスを週単位で実行すると、パフォーマンスが向上します。

1. DB2 コントロールセンターを起動します。

   (Windows) スタート/プログラム/IBM DB2/General Administration Tools/Control Center を選択します。

   （Linux および UNIX）コマンドプロンプトから、`db2jcc` コマンドを入力します。

1. DB2 コントロールセンターのオブジェクトツリーで、[ すべてのデータベース ] をクリックします。
1. AEM forms 用に作成したデータベースをクリックし、 Tables フォルダーをクリックします。
1. コンテンツ・ペインですべてのデータベース・テーブルを選択し、右クリックして「統計の実行」を選択します。
1. 統計/インデックス統計に移動します。
1. 「すべてのインデックスに関する統計情報を収集」を選択し、「拡張された詳細な統計情報を含むインデックスに関する統計情報を収集」を選択して、「OK」をクリックします。

プロセスが完了すると、メッセージが表示されます。 メッセージを閉じます。
