---
title: ページへのワークフローの適用
seo-title: Applying Workflows to Pages
description: ワークフローは、Web サイトコンソールから、またはページの編集時にサイドキックから開始できます。
seo-description: Workflows can be started from either the Websites console or, when editing a page, from Sidekick.
uuid: 55f6f1d7-da54-4732-b9ff-b7479622db51
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.4/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 22712b73-90f2-4329-b32f-dbb7ce802d1d
exl-id: f10680e5-e8ae-49a0-ae52-3aa1f22b2d3e
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '289'
ht-degree: 37%

---

# ページへのワークフローの適用 {#applying-workflows-to-pages}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

ワークフローを適用する際には、次の情報を指定します。

* 適用されるワークフロー。


   （AEM 管理者によって割り当てられた、アクセス権限がある）任意のワークフローを適用できます。
* オプション：

   * ワークフローを開始した理由に関する情報を提供するコメント。
   * ユーザーのインボックス内のワークフローインスタンスの特定に役立つタイトル。

>[!NOTE]
>
>AEM管理者は、 [その他の方法](/help/sites-administering/workflows-starting.md).

## ワークフローの適用 {#applying-workflows}

ワークフローは、Web サイトコンソールから、またはページの編集時にサイドキックから開始できます。

**Web サイト**&#x200B;コンソールの「**ステータス**」列は、ワークフローがページに適用されているかどうかを示します。

![WorkflowStatus](assets/workflowstatus.png)

### Web サイトコンソールからのワークフローの開始 {#starting-a-workflow-from-the-websites-console}

1. Web サイトコンソールを開きます。 ([http://localhost:4502/siteadmin](http://localhost:4502/siteadmin))
1. Web サイトツリーで、ワークフローを適用するページの親を選択します。
1. ページリストで、ページを選択し、「ワークフロー」をクリックします。
1. ワークフローを開始ダイアログで、適用するワークフローを選択します。 任意で、コメントとタイトルを入力します。 次に、「開始」をクリックします。

### サイドキックを使用したワークフローの開始 {#starting-a-workflow-using-sidekick}

1. Web サイトコンソールを開きます。
1. 必要なページを開きます。
1. サイドキックから「ワークフロー」タブを選択します。
1. **ワークフロー**&#x200B;ダイアログを展開して「**ワークフロー**」を選択し、必要に応じて、**ワークフロータイトル**&#x200B;と&#x200B;**コメント**&#x200B;を入力します。

   ![workflowstartsidekick](assets/workflowstartsidekick.png)

1. クリック **ワークフローを開始** 設定したプロパティと現在のページをペイロードとして、新しいワークフローインスタンスを開始する場合。 これで、ワークフローが実行されています。
