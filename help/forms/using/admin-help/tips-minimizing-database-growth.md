---
title: データベースの増大を最小にするためのヒント
seo-title: Tips for minimizing database growth
description: 長期間有効なプロセスは、プロセスデータをAEM forms データベースに保存します。 いくつかの簡単なプロセスデザインと製品設定戦略を使用して、AEM forms データベースの拡大を最小限に抑えることができます。
seo-description: Long-lived processes store process data in the AEM forms database. The growth of the AEM forms database can be minimized using a few easy process design and product configuration strategies.
uuid: 13f99d4f-848e-451e-90d9-55e202dc0bdb
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.4/FORMS
discoiquuid: 89441336-babc-4d1f-9053-d1566cd42d22
exl-id: 7b266170-c7e2-42e7-8ee0-153e1e73a901
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '444'
ht-degree: 5%

---

# データベースの増大を最小にするためのヒント {#tips-for-minimizing-database-growth}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

長期間有効なプロセスは、プロセスデータをAEM forms データベースに保存します。 いくつかの簡単なプロセスデザインと製品設定戦略を使用して、AEM forms データベースの拡大を最小限に抑えることができます。

## プロセスデザインのヒント {#process-design-tips}

可能な限り、短時間のみ有効なプロセスを使用します。 短時間のみ有効なプロセスは、プロセスデータをデータベースに保存しません。 短時間のみ有効なプロセスを使用する場合の欠点は、そのステータスと状態が管理コンソールで追跡されず、プロセスの履歴がないことです。

Assign Task 操作（User サービス）など、一部のサービス操作では、長期間有効なプロセスで使用する必要があります。 この場合、プロセスを複数のサブプロセスにセグメント化し、可能であれば短時間のみ有効にすることができます。 この方法を使用する場合、短時間のみ有効なサブプロセスは、ドキュメント値などの大きなデータ項目を処理する必要があります。

変数は慎重に使用してください。 長時間有効なプロセスを使用する場合、すべてのプロセスインスタンスに対して、プロセス内の各変数に対してデータベースに領域が割り当てられます。 変数を戦略的に使用すると、大量のスペースを節約できます。 例えば、プロセスで古い値が不要になった場合に変数の値を上書きできます。 また、作成済みで使用していない変数を削除します。 プロセスを検証して、未使用の変数を見つけることができます。

単純な変数型（string や int など）を使用し、可能な限り複雑な変数型を使用しないでください。 変数に値が含まれていない場合でも、変数にはデータベース容量が割り当てられます。 複雑な変数は、通常、単純な変数よりも多くのスペースを必要とします。

## 製品管理に関するヒント {#product-administration-tips}

グローバルドキュメントストレージ (GDS) を効果的に使用します。 forms サーバー上の GDS ディレクトリは、特に、プロセス内のAEM forms の一部であるサービスに渡されるファイルを保存するために使用されます。 パフォーマンスを向上させるために、小さいドキュメントは代わりにメモリ内に保存され、データベースに保持されます。

メモリ内に保存され、データベースに保持されるドキュメントの最大サイズを設定するための「 Default Document Max Inline Size 」プロパティが管理コンソールに表示されます。 （[一般的な AEM Forms の設定](/help/forms/using/admin-help/configure-general-aem-forms-settings.md#configure-general-aem-forms-settings)を参照してください。）このプロパティを低い値に設定すると、ほとんどのドキュメントは、データベースではなく、GDS ディレクトリに保持されます。 利点は、GDS ディレクトリに保存する際に不要になったファイルを、より簡単に削除できることです。
