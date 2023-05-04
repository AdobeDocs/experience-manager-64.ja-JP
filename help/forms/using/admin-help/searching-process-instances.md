---
title: プロセスインスタンスの検索
seo-title: Searching for process instances
description: 「プロセスの検索」ページを使用して、プロセスインスタンスを検索するための検索条件を入力します。
seo-description: Use the Process Search page to enter search criteria for finding a process instance.
uuid: 4a9c5b05-add5-4278-9c6f-d1928b6860d2
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms_workflow
products: SG_EXPERIENCEMANAGER/6.4/FORMS
discoiquuid: 88b634bb-8f6c-4830-ad01-821668609615
exl-id: 25a01630-47ec-4823-ad11-9a636697f3dc
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '485'
ht-degree: 14%

---

# プロセスインスタンスの検索{#searching-for-process-instances}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

「プロセスの検索」ページを使用して、プロセスインスタンスを検索するための検索条件を入力します。 プロセスの検索ページには、フォームワークフローページからアクセスするか、プロセスインスタンスページの「検索」をクリックしてアクセスできます。

一般検索を実行する基本条件、詳細検索を実行する特定の属性、または基本条件と特定の属性の組み合わせを入力して結合検索を実行できます。

## 一般検索の実行 {#perform-a-general-search}

プロセスの一般的な検索は、プロセスインスタンスのプロセス ID がわかっている場合、関連するプロセスインスタンスのグループを探している場合、または少数のプロセスインスタンスのみが実行中の場合に、最も適しています。

基本条件を入力して、一般検索を実行します。 複数の条件を入力した場合、検索は暗黙の AND 条件に基づいて実行されます。

1. 管理コンソールで、サービス/Forms workflow/Process Search をクリックします。
1. プロセス検索ページの「一般検索」で、次の条件を指定します。

   * **プロセス ID：**&#x200B;一意の各プロセスインスタンスを識別する正の整数。
   * **プロセスのステータス：**&#x200B;リストからステータスを選択します。
   * **アプリケーション：**&#x200B;リストからアプリケーションを選択します。デプロイされたアプリケーションのみ表示されます。
   * **プロセス名 - バージョン：**&#x200B;メニューからプロセス名を選択します。デプロイされたプロセスのみが表示されます。

1. 「検索」をクリックします。 「プロセスインスタンス」ページが表示され、見つかったインスタンスが一覧表示されます。

## プロセスの詳細検索の実行 {#perform-a-detailed-search-for-a-process}

特定の属性を入力して、詳細検索を実行できます。 詳細検索は、多数のプロセスインスタンスが実行中で、特定の条件に基づいて検出可能な件数を絞り込む必要がある場合に最も適しています。

1. 管理コンソールで、サービス/Forms workflow/Process Search をクリックします。
1. プロセス検索ページの「詳細検索」で、最初の条件セットを指定します。

   * 「属性」リストで、属性を選択します。
   * 「フィルター」リストで、演算子を選択します。
   * [ 値 ] ボックスに、選択した属性に適した値を入力します。

1. 別の行を追加するには、「その他のフィルター」を選択します。 「属性」、「フィルタ」、「値」の各リストの他に、「条件」リストも表示されます。
1. 「条件」で、「および」または「または」を選択します。 必要に応じてステップ 1 ～ 3 を繰り返して、検索を絞ります。
1. 行を追加または削除するには、[ フィルタの追加 ] または [ フィルタの減少 ] をクリックします。 1 ～ 4 行を指定できます。
1. 「検索」をクリックします。 「プロセスインスタンス」ページが表示され、見つかったインスタンスが一覧表示されます。

[プロセスインスタンスのステータスについて](/help/forms/using/admin-help/processes.md#about-process-instance-statuses)

## プロセスの結合検索の実行 {#perform-a-combined-search-for-a-process}

暗黙の AND を使用して、一般検索と詳細検索の両方に基づく検索を作成するには、プロセス検索ページの「一般検索」と「詳細検索」の両方の領域に検索条件を入力します。

検索が狭すぎる場合、インスタンスは見つかりません。
