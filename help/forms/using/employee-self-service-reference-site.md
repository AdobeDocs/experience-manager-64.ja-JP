---
title: 従業員セルフサービスリファレンスサイトのチュートリアル
seo-title: Employee self-service
description: AEM Formsリファレンスサイトでは、組織がAEM Formsの機能を活用して従業員の採用とセルフサービスのワークフローを実装する方法を紹介します。
seo-description: AEM Forms reference site showcases how organizations can leverage AEM Forms features to implement employee recruitment and self-service workflows.
uuid: ecc98e0d-c964-44dc-b219-9ebe92632d22
topic-tags: introduction
products: SG_EXPERIENCEMANAGER/6.4/FORMS
discoiquuid: d2695f71-5126-477c-ae6b-a964fb55728b
exl-id: 7fbdd976-5a70-4af4-b449-7c2d6bcfd915
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '1659'
ht-degree: 3%

---

# 従業員セルフサービスリファレンスサイトのチュートリアル {#employee-self-service-reference-site-walkthrough}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

## 前提条件 {#prerequisite}

リファレンスサイトを設定します ( [AEM Formsリファレンスサイトのセットアップと設定](/help/forms/using/setup-reference-sites.md).

## 概要 {#overview}

一般に企業のイントラネット上でホストされる従業員セルフサービスシステムは、従業員がデスクから利用できる情報やサービスのホストにアクセスできるようにします。 従業員に対し、雇用の詳細へのアクセス、休暇申請、経費報告書の提出などの処理を実行する権限を与え、完全な制御を与えます。 一方、組織は、従業員に対する情報や関与を維持しながら、プロセスの効率性を向上させ、コストを削減できます。

従業員セルフサービスリファレンスサイトでは、AEM Formsを活用して組織に従業員セルフサービスシステムを実装する方法を示します。

>[!NOTE]
>
>従業員セルフサービスの使用例は、We.Finance と We.Gov の両方のリファレンスサイトで利用できます。 このチュートリアルで使用する例、画像、説明では、 We.Finance リファレンスサイトを使用します。 ただし、We.Gov を使用して、これらのユースケースを実行したり、アーティファクトをレビューしたりすることもできます。 これをおこなうには、 **we-finance** と **we-gov** 」と入力します。

## 利益相反アンケートのチュートリアル {#conflict-of-interest-questionnaire-walkthrough}

組織は、組織と競合する可能性のある社員の外部活動や個人関係を、利益相反アンケートの送信を従業員に依頼する場合があります。

Sarah の組織のコンプライアンス部門は、従業員に対し、利益相反アンケートの送信を求めています。

### Sarah が利益相反アンケートを送信 {#sarah-submits-the-conflict-of-interest-questionnaire}

Sarah は組織のポータルに移動し、ログインして、「Employee」をクリックして従業員ダッシュボードにアクセスします。 従業員のダッシュボードで利益相反アンケートを見つけ、「 」をクリックします **[!UICONTROL 適用]**.

![we-finance-home](assets/we-finance-home.png)
**図：** *組織ポータル*

![従業員ダッシュボード](assets/employee-dashboard.png)
**図：** *従業員ダッシュボード*

Sarah は「次へ」ボタンを使用してフォームに移動し、「はじめに」セクションと「定義」セクションを読みます。 Sarah は「質問」セクションの質問に回答します。 最後に、彼女はアンケートに署名して送信します。

組織のポータルとアンケートは、レスポンシブでモバイルに優しいです。 次のワークフローは、Sarah がモバイルデバイス上でアンケートに移動して送信する方法を示しています。

![conflict-form-on-mobile](assets/conflict-form-on-mobile.png)

**仕組み**

組織ポータルと従業員ダッシュボードは、AEM Sitesのページです。 ダッシュボードには、利益相反アンケートなど、複数のセルフサービスオプションが表示されます。 「適用」ボタンは、アダプティブフォームにリンクされています。

アダプティブフォームは、ルールを使用して、「質問」タブで提供された回答に基づいて情報を表示/非表示にします。 また、フォームは「宣言」タブでの署名に手書きメモコンポーネントを使用します。 アダプティブフォームのレビュー ( ) `https://[authorHost]:[authorPort]/editor.html/content/forms/af/we-finance/employee/self-service/conflict-of-interest.html`.

**実際の動作確認**

に移動します。 `https://[publishHost]:[publishPort]/content/we-finance/global/en/self-service-forms.html` を使用してログインし、 `srose/srose` Sarah のユーザー名/パスワード。 クリック **[!UICONTROL 従業員]** ダッシュボードにアクセスし、「 **[!UICONTROL 適用]** 利益相反アンケート アンケートを確認して送信します。

### Gloria は利益相反アンケートの送信を確認し、承認します {#gloria-reviews-and-approves-the-conflict-of-interest-questionnaire-submission}

Sarah が提出した利益相反アンケートは、レビュー用に Gloria Rios に割り当てられます。 Gloria は組織のコンプライアンス担当役員として働いています。 Gloria はAEM Inbox にログインし、自分に割り当てられたタスクを確認します。 Sarah が送信したアンケートを承認し、タスクを完了します。

![conflict-inbox](assets/conflict-inbox.png)
**図：** *Gloria のインボックス*

![競合が承認された](assets/conflict-approved.png)
**図：** *タスクを開く*

**仕組み**

利益相反アンケートの送信アクションにより、Gloria のインボックスに承認用のタスクを作成するワークフローがトリガーされます。 Forms Workflowの確認 `https://[authorHost]:[authorPort]/editor.html/conf/global/settings/workflow/models/we-finance/employee/self-service/we-finance-employee-conflict-of-interest.html`

![employee-self-service-reference-site](assets/employee-self-service-reference-site.png)

**実際の動作確認**

に移動します。 `https://[publishHost]:[publishPort]/content/we-finance/global/en/login.html?resource=/aem/inbox.html` を使用してログインし、 `grios/password` Gloria Rios のユーザー名/パスワード。 利益相反アンケート用に作成したタスクを開き、承認します。

## 会社カードの申し込みのチュートリアル {#corporate-card-application-walkthrough}

Sarah は多くのビジネスを旅し、引っ越し時に自分の請求書を支払うために、会社のクレジットカードを要求します。 彼女は会社の社員ポータルを通じて法人カードを申し込みます。

### Sarah が法人カードの申し込みを送信 {#sarah-submits-the-corporate-card-application}

Sarah は組織のポータルに移動し、ログインして、「 」をクリックします **[!UICONTROL 従業員]** 従業員ダッシュボードにアクセスするには 従業員のダッシュボードで法人カードの申し込みを見つけ、「 」をクリックします **[!UICONTROL 適用]**.

![we-finance-home-1](assets/we-finance-home-1.png)
**図：** *組織ポータル*

![employee-dashboard-1](assets/employee-dashboard-1.png)
**図：** *従業員ダッシュボード*

Sarah はクリックします **[!UICONTROL 適用]** をクリックします。 単一ページのアプリケーションが開きます。 すべての詳細を入力し、クリックします **[!UICONTROL 適用]** をクリックして、申込書を送信します。

![カードフォーム](assets/card-form.png)

**仕組み**

組織ポータルと従業員ダッシュボードは、AEM Sitesのページです。 ダッシュボードには、会社のカードの申し込みなど、複数のセルフサービスオプションが一覧表示されます。 アプリケーションの「適用」ボタンは、アダプティブフォームにリンクされています。

企業カード申し込み用のアダプティブフォームは、1 ページから成るシンプルなレスポンシブアダプティブフォームです。 テキスト、電話、数値ボックス、数値ステッパーなど、基本的なアダプティブフォームコンポーネントを使用します。 次の場所でアダプティブフォームをレビューします。\
`https://[authorHost]:[authorPort]/editor.html/content/forms/af/we-finance/employee/self-service/corporate-card.html`。

**実際の動作確認**

に移動します。 `https://[publishHost]:[publishPort]/content/we-finance/global/en/self-service-forms.html` を使用してログインし、 `srose/srose` Sarah のユーザー名/パスワード。 クリック **[!UICONTROL 従業員]** ダッシュボードにアクセスし、「 **[!UICONTROL 適用]** をクリックします。 詳細を入力し、申込書を送信します。

### Gloria は企業カードの申し込みを確認し承認します {#gloria-reviews-and-approves-the-corporate-card-application}

Sarah が送信した法人カードの申し込みは、確認のために Gloria Rios に割り当てられます。 Gloria はAEM Inbox にログインし、自分に割り当てられたタスクを確認します。 Sarah が送信した申し込みを承認し、タスクを完了します。

![corporate-card-inbox](assets/corporate-card-inbox.png)
**図：** *Gloria のインボックス*

![法人カードで承認された](assets/corporate-card-approved.png)
**図：** *タスクを開く*

**仕組み**

会社カードの申し込みの送信ワークフローは、Gloria のインボックスに承認用のタスクを作成するFormsワークフローをトリガーします。 Forms Workflowの確認 `https://[authorHost]:[authorPort]/editor.html/conf/global/settings/workflow/models/we-finance/employee/self-service/we-finance-employee-corporate-card.html`

![corporate-card-workflow-model](assets/corporate-card-workflow-model.png)

**実際の動作確認**

に移動します。 `https://[publishHost]:[publishPort]/content/we-finance/global/en/login.html?resource=/aem/inbox.html` を使用してログインし、 `grios/password` Gloria Rios のユーザー名/パスワード。 会社カードの申し込み用に作成されたタスクを開き、承認します。

## 経費報告書の送信チュートリアル {#expense-report-submission-walkthrough}

出張中に費やした Sarah は、承認を得るために経費報告書を送信する必要があります。 組織のセルフサービスオプションを使用すると、経費報告書をオンラインで送信できます。

### Sarah が経費報告書の申し込みを送信 {#sarah-submits-the-expense-report-application}

Sarah は組織のポータルに移動し、ログインして、「 」をクリックします **[!UICONTROL 従業員]** 従業員ダッシュボードにアクセスするには 従業員のダッシュボードで経費報告書の申し込みを検索し、「 」をクリックします **[!UICONTROL 適用]**.

![we-finance-home-2](assets/we-finance-home-2.png)
**図：** *組織ポータル*

![employee-dashboard-2](assets/employee-dashboard-2.png)
**図：** *従業員ダッシュボード*

Sarah はクリックします **[!UICONTROL 適用]** をクリックします。 「レポート名」と「レポートの詳細」の 2 つのタブを持つアプリケーションフォームが開きます。 この **+** 「レポートの詳細」タブのアイコンを使用すると、1 つのレポートに複数の支出を追加できます。

組織のポータルやアプリケーションは、レスポンシブでモバイルに優しいです。 次のワークフローは、Sarah がモバイルデバイス上で経費報告書を移動して送信する方法を示しています。

![expense-report-on-mobile](assets/expense-report-on-mobile.png)

**仕組み**

組織ポータルと従業員ダッシュボードは、AEM Sitesのページです。 ダッシュボードには、経費報告書の申請など、複数のセルフサービスオプションが一覧表示されます。 「適用」ボタンは、アダプティブフォームにリンクされています。

アダプティブフォームの「レポート名」タブと「レポートの詳細」タブは、パネルコンポーネントです。 「レポートの詳細」パネルには、「費用」パネルが含まれています。 これは、レポートに複数の支出を追加できる繰り返し可能なパネルです。 アダプティブフォームとその設定を次の場所で確認します。 `https://[authorHost]:[authorPort]/editor.html/content/forms/af/we-finance/employee/expense-report.html`.

**実際の動作確認**

に移動します。 `https://[publishHost]:[publishPort]/content/we-finance/global/en/self-service-forms.html` を使用してログインし、 `srose/srose` Sarah のユーザー名/パスワード。 クリック **[!UICONTROL 従業員]** ダッシュボードにアクセスし、「 **[!UICONTROL 適用]** を選択します。 詳細を入力し、申込書を送信します。

### Gloria が経費報告書を確認し承認 {#gloria-reviews-and-approves-the-expense-report}

Sarah が送信した経費報告書は、確認のために Gloria Rios に割り当てられます。 Gloria はAEM Inbox にログインし、自分に割り当てられたタスクを確認します。 Sarah が送信した申し込みを承認し、タスクを完了します。

![expense-report-inbox](assets/expense-report-inbox.png)
**図：** *Gloria のインボックス*

![expense-report-approved](assets/expense-report-approved.png)
**図：** *タスクを開く*

**仕組み**

経費報告書申請の送信ワークフローは、Gloria のインボックスに承認用のタスクを作成するFormsワークフローをトリガーします。 Forms Workflowの確認 `https://[authorHost]:[authorPort]/editor.html/conf/global/settings/workflow/models/we-finance/employee/self-service/we-finance-employee-expense-report-workflow.html`

![corporate-card-expense-report-workflow-model](assets/corporate-card-expense-report-workflow-model.png)

**実際の動作確認**

に移動します。 `https://[publishHost]:[publishPort]/content/we-finance/global/en/login.html?resource=/aem/inbox.html` を使用してログインし、 `grios/password` Gloria Rios のユーザー名/パスワード。 経費報告書の申し込み用に作成されたタスクを開き、承認します。

## アプリケーションのチュートリアルを終了 {#leave-application-walkthrough}

Sarah は来月、家族の休暇を計画し、1 週間の休暇を申し込みたいと考えています。

### Sarah が休暇申込書を送信 {#sarah-submits-the-leave-application}

Sarah は組織のポータルに移動し、ログインして、「 」をクリックします **[!UICONTROL 従業員]** 従業員ダッシュボードにアクセスするには 従業員のダッシュボードで休暇申請を見つけ、「 」をクリックします **[!UICONTROL 適用]**.

![we-finance-home-3](assets/we-finance-home-3.png)
**図：** *組織ポータル*

![employee-dashboard-3](assets/employee-dashboard-3.png)
**図：** *従業員ダッシュボード*

休暇の申し込みが開き、Sarah の名前と従業員 ID がフォームに事前入力されます。 また、彼女の休暇残高と履歴も表示されます。 休暇の詳細を入力し、承認の申請を送信します。

組織のポータルやアプリケーションは、レスポンシブでモバイルに優しいです。 次のワークフローは、Sarah がモバイルデバイス上で申込書をナビゲートおよび送信する方法を示しています。

![leave-form-on-mobile](assets/leave-form-on-mobile.png)

**仕組み**

組織ポータルと従業員ダッシュボードは、AEM Sitesのページです。 ダッシュボードには、休暇申し込みなど、複数のセルフサービスオプションが一覧表示されます。 「適用」ボタンは、アダプティブフォームにリンクされています。

休暇申し込み用のアダプティブフォームは、従業員がフォームデータモデルから離脱することに基づいています。 「休暇残高」セクションでは、休暇残高テーブルは `getLeavesOf` フォームデータモデルサービス。 「開始日」フィールドと「終了日」フィールドでは、ルールを使用して、日付値が現在の日付以降であることを検証します。 休暇期間は `calcBusinessDays` 関数に置き換えます。

アダプティブフォームとフォームデータモデルは、以下の場所で確認できます。

`https://[authorHost]:[authorPort]/editor.html/content/forms/af/we-finance/employee/self-service/leave-application.html`

`https://[authorHost]:[authorPort]/aem/fdm/editor.html/content/dam/formsanddocuments-fdm/db`

**実際の動作確認**

に移動します。 `https://[publishHost]:[publishPort]/content/we-finance/global/en/self-service-forms.html` を使用してログインし、 `srose/srose` Sarah のユーザー名/パスワード。 クリック **[!UICONTROL 従業員]** ダッシュボードにアクセスし、「 **[!UICONTROL 適用]** 休暇申請時。 詳細を入力し、申込書を送信します。

### Gloria は休暇申込書を確認し承認します {#gloria-reviews-and-approves-the-leave-application}

Sarah が提出した休暇の申し込みは、レビューのために Gloria Rios に割り当てられます。 Gloria はAEM Inbox にログインし、自分に割り当てられたタスクを確認します。 Sarah が送信した申し込みを承認し、タスクを完了します。

![leave-inbox](assets/leave-inbox.png)
**図：** *Gloria のインボックス*

![休職承認済み](assets/leave-approved.png)
**図：** *タスクを開く*

**仕組み**

休暇申し込みの送信ワークフローは、Gloria のインボックスに承認用のタスクを作成するFormsワークフローをトリガーします。 Forms Workflowの確認 `https://[authorHost]:[authorPort]/editor.html/conf/global/settings/workflow/models/we-finance/employee/self-service/we-finance-employee-leave-application.html`

![corporate-card-leave-application-workflow-model](assets/corporate-card-leave-application-workflow-model.png)

**実際の動作確認**

に移動します。 `https://[publishHost]:[publishPort]/content/we-finance/global/en/login.html?resource=/aem/inbox.html` を使用してログインし、 `grios/password` Gloria Rios のユーザー名/パスワード。 休暇申請用に作成されたタスクを開き、承認します。
