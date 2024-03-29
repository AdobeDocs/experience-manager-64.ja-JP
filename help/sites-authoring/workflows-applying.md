---
title: ページへのワークフローの適用
seo-title: Applying Workflows to Pages
description: オーサリング時に、ワークフローを呼び出して、ページ上でアクションを実行できます。複数のワークフローを適用することもできます。
seo-description: When authoring, you can invoke workflows to take action on your pages; it is also possible to apply more than one workflow..
uuid: 8a1d16f8-69fc-4e3a-b72a-b799ea381024
contentOwner: AEM Docs
products: SG_EXPERIENCEMANAGER/6.4/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 8556d20a-99bd-4942-b7b8-2db69f64e67c
exl-id: 05c52802-adfd-4b5f-a273-d6a261a00659
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '683'
ht-degree: 53%

---

# ページへのワークフローの適用 {#applying-workflows-to-pages}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

オーサリングでは、ワークフローを呼び出して、ページにアクションを実行することができます。複数のワークフローを適用することもできます。

ワークフローを適用する際には、次の情報を指定します。

* 適用されるワークフロー。


   （AEM 管理者によって割り当てられた、アクセス権限がある）任意のワークフローを適用できます。

* オプションで、ユーザーのインボックス内のワークフローインスタンスを識別するのに役立つタイトルです。
* ワークフローのペイロード。1 つ以上のページを指定できます。

ワークフローは、次の場所から開始できます。

* の **[サイト](#starting-a-workflow-from-the-sites-console)** コンソール。
* ページの編集中に「**[ページ情報](#starting-a-workflow-from-the-page-editor)**」から。

>[!NOTE]
>
>関連トピック：
>
>* [DAM アセットにワークフローを適用する方法](/help/assets/assets-workflow.md).
>* [プロジェクトワークフローの操作](/help/sites-authoring/projects-with-workflows.md)。
>


>[!NOTE]
>
>AEM管理者が [他のいくつかの方法でワークフローを開始](/help/sites-administering/workflows-starting.md).

## Sites コンソールからのワークフローの開始 {#starting-a-workflow-from-the-sites-console}

ワークフローは以下のいずれかから開始できます。

* の **[作成](#starting-a-workflow-from-the-sites-toolbar)** 」オプションを使用します。
* の **[タイムライン](#starting-a-workflow-from-the-timeline)** サイトコンソールのパネル。

どちらの場合も、次の操作が必要です。

* [ワークフローを作成ウィザードでワークフローの詳細を指定します](#specifying-workflow-details-in-the-create-workflow-wizard).

### Sites ツールバーからのワークフローの開始 {#starting-a-workflow-from-the-sites-toolbar}

**サイト**&#x200B;コンソールのツールバーからワークフローを開始できます。

1. 必要なページに移動して選択します。

1. これでツールバーの「**作成**」オプションで「**ワークフロー**」を選択できます。

   ![screen_shot_2019-03-06at121237pm](assets/screen_shot_2019-03-06at121237pm.png)

1. この **ワークフローを作成** ウィザードが役立ちます [ワークフローの詳細を指定](#specifying-workflow-details-in-the-create-workflow-wizard).

### タイムラインからのワークフローの開始 {#starting-a-workflow-from-the-timeline}

**タイムライン**&#x200B;から、選択したリソースに適用されるワークフローを開始できます。

1. [リソースを選択](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources)し、[タイムライン](/help/sites-authoring/basic-handling.md#timeline)を開きます（またはタイムラインを開いてからリソースを選択します）。
1. コメントフィールドの横にある矢印を使用すると、「**ワークフローを開始**」が表示されます。

   ![wf-51](assets/wf-51.png)

1. この **ワークフローを作成** ウィザードが役立ちます [ワークフローの詳細を指定](#specifying-workflow-details-in-the-create-workflow-wizard).

### ワークフローの作成ウィザードでのワークフローの詳細の指定 {#specifying-workflow-details-in-the-create-workflow-wizard}

この **ワークフローを作成** ウィザードは、ワークフローを選択し、必要な詳細を指定するのに役立ちます。

を開いた後 **ワークフローを作成** ウィザードを次のいずれかから選択します。

* の **[作成](#starting-a-workflow-from-the-sites-toolbar)** 」オプションを使用します。
* の **[タイムライン](#starting-a-workflow-from-the-timeline)** サイトコンソールのパネル。

次の詳細を指定できます。

1. 内 **プロパティ** 手順では、ワークフローの基本オプションを定義します。

   * **ワークフローモデル**
   * **ワークフロータイトル**

      * このインスタンスのタイトルを指定して、後の段階で識別しやすくすることができます。

   ワークフローモデルに応じて、次のオプションも使用できます。 これにより、ペイロードとして作成されたパッケージを、ワークフローの完了後も保持できます。

   * **ワークフローパッケージを維持**
   * **パッケージタイトル**

      * 識別に役立つように、パッケージのタイトルを指定できます。
   >[!NOTE]
   >
   >ワークフローが[マルチリソースサポート](/help/sites-developing/workflows-models.md#configuring-a-workflow-for-multi-resource-support)のために設定されており、複数のリソースが選択されている場合は、**ワークフローパッケージを維持**&#x200B;オプションが使用できます。

   完了したら、「**次へ**」を使用して続行します。

   ![wf-52](assets/wf-52.png)

1. **スコープ**&#x200B;ステップで、以下のものを選択できます。

   * 「**コンテンツを追加**」で[パスブラウザー](/help/sites-authoring/author-environment-tools.md#path-browser)を開き、追加リソースを選択します。ブラウザーでは、「**選択**」をクリックまたはタップして、コンテンツをワークフローインスタンスに追加します。
   * 追加のアクションを表示するための既存のリソース

      * 「**子を含める**」で、ワークフローに含まれるそのリソースの子を指定します。

         ダイアログが開いて、以下のものに従って選択を絞り込むことができます。

         * 直近の子のみを含める。
         * 変更されたページのみを含める。
         * 既に公開済みのページのみを含める。

         指定した子は、ワークフローが適用されるリソースのリストに追加されます。

      * **選択項目を削除** をクリックして、そのリソースをワークフローから削除します。

   ![wf-53](assets/wf-53.png)

   >[!NOTE]
   >
   >追加リソースを追加する場合は、「**戻る**」を使用して、**プロパティ**&#x200B;ステップで「**ワークフローパッケージを維持**」の設定を調整できます。

1. 「**作成**」を使用して、ウィザードを閉じ、ワークフローインスタンスを作成します。通知はサイトコンソールに表示されます。

## ページエディターからのワークフローの開始 {#starting-a-workflow-from-the-page-editor}

ページの編集時に、 **ページ情報** をクリックします。 ドロップダウンメニューにはオプションがあります **ワークフローで開始**. これによりダイアログが開き、必要なワークフローと必要な場合はタイトルを指定できます。

![wf-54](assets/wf-54.png)
