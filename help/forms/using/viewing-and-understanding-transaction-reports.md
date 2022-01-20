---
title: 取引レポートの表示と理解
seo-title: Viewing and Understanding Transaction Reports
description: トランザクションレポートを使用して、製品の使用状況に関する十分な情報に基づく決定を下し、ハードウェアとソフトウェアに対する投資のリバランスを行います。
seo-description: Use transaction reports to make an informed decision about the product usage and rebalancing investments in hardware and software.
uuid: a33abcae-8e37-4e2d-99b0-c92c439745f3
contentOwner: khsingh
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: forms-manager
discoiquuid: bef38e7a-92db-4226-a4ea-8facce573456
exl-id: b132216a-c9b4-4f8f-97e6-738a5a9632d1
source-git-commit: db64b7d5ac9044c4b2fee6ae4adbe9aab1cf4c7d
workflow-type: tm+mt
source-wordcount: '884'
ht-degree: 1%

---

# 取引レポートの表示と理解 {#viewing-and-understanding-transaction-reports}

トランザクションレポートを使用して、製品の使用状況に関する十分な情報に基づく決定を下し、ハードウェアとソフトウェアに対する投資のリバランスを行います。

トランザクションレポートでは、送信されたフォーム、処理されたドキュメント、レンダリングされたドキュメントの数を取得し、追跡できます。 これらのトランザクションを追跡する目的は、製品の使用状況に関する十分な情報に基づく判断を行い、ハードウェアとソフトウェアに対する投資のリバランスを図ることです。 詳しくは、 [AEM Formsトランザクションレポートの概要](/help/forms/using/transaction-reports-overview.md).

## トランザクションレポートの設定  {#setting-up-transaction-reports}

トランザクションレポートの機能は、AEM forms アドオンパッケージの一部です。 すべてのオーサーインスタンスとパブリッシュインスタンスにアドオンパッケージをインストールする方法について詳しくは、 [AEM forms のインストールと設定](https://helpx.adobe.com/jp/experience-manager/6-4/forms/using/installing-configuring-aem-forms-osgi.html). AEM forms アドオンパッケージをインストールしたら、以下の手順を実行します。

* すべてのパブリッシュインスタンスでリバースレプリケーションを有効にする
* トランザクションレポートの有効化
* トランザクションレポートを表示する権限の指定
* （オプション）トランザクションフラッシュ期間とアウトボックスの設定

>[!NOTE]
>
>* AEM Formsトランザクションレポートは、パブリッシュインスタンスのみを含むトポロジをサポートしていません。
>* トランザクションレポートを使用する前に、すべてのパブリッシュインスタンスでリバースレプリケーションが有効になっていることを確認します。
>* トランザクションデータは、パブリッシュインスタンスから、対応するオーサーまたは処理インスタンスにのみリバースレプリケーションされます。 オーサーインスタンスまたは処理インスタンスは、別のインスタンスにデータをレプリケートできません。

>


### すべてのパブリッシュインスタンスでリバースレプリケーションを有効にする {#enable-reverse-replication-on-all-the-publish-instances}

トランザクションレポートでは、リバースレプリケーションを使用して、パブリッシュインスタンスのトランザクション数をオーサーインスタンスに統合します。 すべてのパブリッシュインスタンスでリバースレプリケーションをセットアップします。 リバースレプリケーションを設定する手順について詳しくは、 [複製](/help/sites-deploying/replication.md).

### トランザクションレポートの有効化 {#enable-transaction-reports}

トランザクションレポートは、デフォルトで無効になっています。 AEM Web コンソールからレポートを有効にできます。 AEM Forms環境でトランザクションレポートを有効にするには、すべてのオーサーインスタンスとパブリッシュインスタンスで次の手順を実行します。

1. AEMインスタンスに管理者としてログインします。 に移動します。 **ツール** > **運用** > **Web コンソール**.
1. を探して開きます。 **Forms Transaction Reporting** サービス。
1. 「取引の記録」チェック・ボックスを選択します。 「**保存**」をクリックします。

   すべてのオーサーインスタンスとパブリッシュインスタンスで、手順 1 ～ 3 を繰り返します。

### トランザクションレポートを表示する権限の指定 {#provide-rights-to-view-a-transaction-report}

トランザクションレポートを表示できるのは、fd-administrator グループのメンバーだけです。 ユーザーがトランザクションレポートを表示できるようにするには、fd-administrator グループのユーザーにします。 ユーザーをAEMグループのメンバーにする手順については、 [ユーザー、グループ、アクセス権の管理](/help/sites-administering/user-group-ac-admin.md).

### （オプション）トランザクションフラッシュ期間とアウトボックスの設定 {#optional-configure-transaction-flush-period-and-outboxes}

トランザクションは、リポジトリに保存される前にメモリにキャッシュされます。 リポジトリへの書き込みが頻繁におこなわれないように、プロセスが実行されます。 デフォルトでは、キャッシュ期間（トランザクションフラッシュ期間）は 60 秒に設定されています。 デフォルトの期間は、環境に合わせて変更できます。 デフォルトのキャッシュ期間を変更するには、次の手順を実行します。

1. 管理者としてオーサーインスタンスにログインします。 に移動します。 **ツール** > **運用** > **Web コンソール**.
1. を探して開きます。 **Forms Transaction Repository Storage Provider** サービス。
1. 秒数を **トランザクションフラッシュ期間** フィールドに入力します。 「**保存**」をクリックします。

リバースレプリケーションは、トランザクションデータをオーサーインスタンスのデフォルトのアウトボックスにコピーします。 トランザクションデータは、カスタム送信トレイに配置できます。 次の手順を実行して、カスタムアウトボックスを指定します。

1. 管理者としてオーサーインスタンスにログインします。 に移動します。 **ツール** >  **運用** >  **Web コンソール**.
1. を探して開きます。 **Forms Transaction Repository Storage Provider** サービス。
1. カスタムアウトボックスの名前を **送信トレイ** フィールドに入力します。 「**保存**」をクリックします。指定した名前のアウトボックスがすべてのオーサーインスタンス上に作成されます。

## トランザクションレポートの表示 {#viewing-the-transaction-report}

オーサーインスタンスまたはパブリッシュインスタンスのトランザクションレポートを表示できます。 オーサーインスタンスのトランザクションレポートは、設定されたオーサーインスタンスとパブリッシュインスタンスで発生するすべてのトランザクションの集計合計を提供します。 パブリッシュインスタンスのトランザクションレポートは、基になるパブリッシュインスタンスでのみ発生するトランザクションの数を提供します。 レポートを表示するには、次の手順を実行します。

1. AEM Formsサーバー ( ) にログインします。 `https://[hostname]:[port]`.
1. に移動します。 **ツール** >  **Forms** >  **トランザクションレポートの表示**.

## レポートについて {#understanding-the-report}

AEM Formsには、次の要約レポートに示すように、設定した日付以降のトランザクションレポートが表示されます。

![sample-transaction-report-author](assets/sample-transaction-report-author.png)

* 以下を使用： **日付を今日にリセット** トランザクションレコードをリセットするオプション。 日付を今日にリセットすると、以前のトランザクションレコードはすべて失われます。 オーサーインスタンスで日付をリセットした場合、この変更はパブリッシュインスタンスのトランザクションレポートに影響を与えず、逆も同様です。
* 以下を使用： **パブリッシュインスタンスのトランザクションのみを表示** 設定済みのパブリッシュインスタンスまたはパブリッシュファームでのみ発生したすべてのトランザクションを表示する場合。
* 次のカテゴリを使用します。 **処理済みのドキュメント**, **レンダリングされたドキュメント**、および **Forms Submitted** 対応するトランザクションを表示します。 これらのカテゴリに計上される取引のタイプは、 [請求可能なトランザクションレポート API](/help/forms/using/transaction-reports-billable-apis.md).

## トランザクションレポートログの表示 {#view-transaction-reporting-logs}

トランザクションレポートでは、レポートに表示されるすべての情報と一部の追加情報がログに記録されます。 ログに表示される情報は、上級ユーザーにとって役立ちます。 例えば、ログでは、トランザクションが複数の詳細カテゴリに分割され、レポートに表示される 3 つの統合カテゴリに比べて異なります。 ログは、 `error.log` ファイルを `/crx-repository/logs/` ディレクトリ。 ログは、AEM Web コンソールからトランザクションレポートを有効にしない場合でも使用できます。

## 関連記事 {#related-articles}

* [トランザクションレポートの概要](/help/forms/using/transaction-reports-overview.md)
* [トランザクションレポート請求可能 API](/help/forms/using/transaction-reports-billable-apis.md)
* [カスタム実装のトランザクションの記録](/help/forms/using/record-transaction-custom-implementation.md)
