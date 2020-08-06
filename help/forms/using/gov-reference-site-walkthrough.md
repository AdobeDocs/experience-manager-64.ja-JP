---
title: We.Gov リファレンスサイトのチュートリアル
seo-title: We.Gov リファレンスサイトのチュートリアル
description: '行政が AEM Forms を使用して個人情報を管理している方法については、We.Gov リファレンスサイトのチュートリアルを参照してください。 '
seo-description: '行政が AEM Forms を使用して個人情報を管理している方法については、We.Gov リファレンスサイトのチュートリアルを参照してください。 '
uuid: 348f9067-28b5-47ed-8e83-0dbadeff0854
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: introduction
discoiquuid: 25a6d702-9995-4c63-99d8-3e5d710bb0c4
translation-type: tm+mt
source-git-commit: 7e58d1d861f832d073fb178868804995ee8d855b
workflow-type: tm+mt
source-wordcount: '2737'
ht-degree: 74%

---


# We.Gov リファレンスサイトのチュートリアル {#we-gov-reference-site-walkthrough}

## 必要条件 {#pre-requisite}

「[AEM Forms リファレンスサイトのセットアップおよび設定](/help/forms/using/setup-reference-sites.md)」を参照して We.Gov リファレンスサイトをセットアップします。

## リファレンスサイトのシナリオ {#reference-site-scenario}

We.Gov は、養子縁組をした場合に養親がチャイルドサポートの申込を行う公的機関です。このサイトでは以下を管理します。

* 申込者（養親）の適格性
* 申込者の個人情報と職業の詳細（申込者がチャイルドサポートに適格の場合）
* 養子の個人的な内容

   申込者は、複数の子の詳細を入力できます
* チャイルドサポート手当を受け取るための申込者の銀行口座の詳細
* 申込手数料の払い戻し
* 申込の査定
* 申込の承認
* 申込者への自動通知

申込が送信され手数料が支払われると、申込者は提出した申込の送信確認の電子メールを受信します。

We.Gov 機関は申込を受信します。機関側で申込の査定が行われ、正当とされる申込が承認されます。

申込が承認されると、申込者は We.Gov サイトから電子メールを受信します。The **View Document** option in the email links to a document with the enrollment details of the applicant.

以下の解説図は、We.Gov リファレンスサイトシナリオのワークフローを順を追って示しています。

![workflow_aem_gov_2](assets/workflow_aem_gov_2.png)

このシナリオでは、以下の人物が登場します。

* Sarah Rose（チャイルドサポートの申込を行う養親）
* Joe（養子）
* Gloria Rios（We.Gov の承認部署の責任者）
* Conard Simms（申込査定担当のフィールドエージェント）

## Sarah が適格性の確認を開始 {#sarah-initiates-her-eligibility-check}

申込者はチャイルドサポート手当を受ける適格性があるか確認できます。ユーザーは We.Gov サイトで設定された質問に答えることで、自分の申込に手当が適用されるか判断します。養親である Sarah は、見込申込者です。適格性のフォームは、We.GovサイトのApplication for Child Supportサービスの一部です。 To check her eligibility, Sarah clicks **[!UICONTROL Child Support]** on the We.Gov website. In the Child Support page, Sarah clicks **[!UICONTROL Check Your Eligibility]**.

上記の方法に加えて、Sarah はホームページで「**[!UICONTROL Get Started]**」（始める）をクリックすることができます。Sarah は「All Applications」（すべての申込）ページに移動し、「**[!UICONTROL Application for Child Support Services]**」（チャイルドサポートサービス申込）内の「Apply」（申し込む）をクリックできます。次に、Sarahは適格性の確認を受けます。

「Check Eligibility For Child Support」（チャイルドサポートの適格性を確認）ページで、Sarah はチャイルドサポート手当の適格性の判断材料となる一連の質問への回答を求められます。一連の質問では、以下が尋ねられます。

* Sarah は親権を持つ親であるかどうか
* Sarah とその子の生活状態が GX かどうか
* 子の年齢層と学歴

これらの質問に Sarah が回答し、適格性が検証されます。回答に基づいて、Sarah がチャイルドサポートに適格か判断されます。

チャイルドサポートに適格であることと、申込手数料が25ドルであることが Sarah に通知されます。

### 仕組み {#how-it-works}

Sarah の適格性は、ルールエディターによって作成された適格性バリアにより検証されます。申込者が申込フォームを記入するために必要な条件を、ルールエディターで指定することができます。申込者である Sarah が適格性の条件すべてに適合すると、申込フォームに移動できるようになります。

適格性の確認は、チャイルドサポート申込のアダプティブフォームの一部です。以下の場合に、ルールは適格性を検証します。

* 申込者が親権を持つ親である
* 申込者と子どもが GX の状態にある
* 申込者が日常的に子どもの面倒をみている
* サポートサービスの適用を受ける子どもの年齢が 16 歳未満である。

### 実際の動作確認 {#see-it-yourself}

In your browser, open `https://<hostname>:<PublishPort>/content/we-gov/en.html`. We.Gov サイトで、「Child Support」（チャイルドサポート）をクリックします。「Child Support」（チャイルドサポート）ページで、「Check Your Eligibility」（適格性を確認）をクリックします。

ルールを表示するには：

1. 作成者インスタンス上で、フォームを編集モードで開きます。URL: `https://<hostname>:<AuthorPort>/editor.html/content/forms/af/we-gov/child-support/css.html`.
1. Select a component and click ![edit-rules](assets/edit-rules.png).

   ルールエディターが開き、フォームに適用されるすべてのルールが一覧表示されます。

1. 適格性確認の仕組みを理解するには、左側のパネルでルール `passMsg` および `failMsg` をクリックします。

## Sarah がチャイルドサポートの申込を開始 {#sarah-starts-her-application-for-child-support}

チャイルドサポートに適格であると通知された後、Sarah は「**[!UICONTROL Start Application]**」（申込を開始）をクリックします。\
「Application For Child Support Services」（チャイルドサポートサービス申込）ページで、Sarah は以下のセクションに詳細を入力します。

* **[!UICONTROL About Applicant]**（申込者について）：Sarah はこのセクションで、自分についての詳細を入力します。

* **[!UICONTROL 子情報]**: 子の情報をSarahが入力できるようにします。子の情報はサポートサービスの対象となります。

* **[!UICONTROL Payment]**（支払）：Sarah は、毎月の手当が We.Gov から振り込まれる自分の銀行口座の詳細を入力します。

* **[!UICONTROL Fee Payment]**（手数料支払）：Sarah は、申込手数料の支払いに使用する自分のクレジットカードの詳細を入力します。

By default, Sarah is taken to the **[!UICONTROL About Applicant]** section.

![デスクトップでのチャイルドサポート申込](assets/desktop.png)

At any time, Sarah can click **[!UICONTROL Come back later]** and resume with her application. When she clicks **[!UICONTROL Come back later]**, her progress is saved as a draft, and she gets an option to email the draft.

When she clicks **[!UICONTROL Send Email]**, she receives an email with a link to the draft of her form.

We.Gov サイトにおけるチャイルドサポートフォームにはアダプティブフォームが使用されています。Sarah は電子メールのリンクをクリックして、モバイルデバイスからフォームを入力することができます。

>[!NOTE]
>
>resume-from-email ワークフローは、ログインしているユーザーでのみ機能します。リファレンスサイトのシナリオでは、ユーザー Sarah Rose が追加されていることを確認します。Sarah&#39;s login credentials are `srose/password`.

![mob1](assets/mob1.png)

どのセクションにも Sarah は詳細を入力することができます。ただし、すべてのセクションで必須の情報を入力し終えるまでは、申込手数料は受理されません。手数料が支払われていない申込は完了したと見なされません。アスタリスクが付いているフィールドは必須です。

### <strong>Sarah が自分の情報を提出</strong> {#strong-sarah-provides-her-information-strong}

「**[!UICONTROL Start Application]**」（申込を開始）をクリックすると、デフォルトで「Application For Child Support Services」（チャイルドサポートサービス申込）ページの「Applicant Information」（申込情報）セクションに移動します。「Applicant Information」（申込情報）で、Sarah は各タブに移動し、申込に必要な個人情報を入力します。「**[!UICONTROL Next]**」（次へ）をクリックして、タブ間を移動します。

Sarah は「Applicant Information」（申込情報）の以下のタブで、詳細を入力するよう求められます。

* **[!UICONTROL 基本情報]**

（基本情報） ここには身分証明情報と個人情報を入力します。個人情報には、Sarahの名前、電子メールID、および社会保障番号が含まれます。

* **[!UICONTROL 関係]**

   「Relationship」で、Sarahは婚姻状況に関する情報を入力します。

* **[!UICONTROL 追加情報]**

   （追加情報） ここには識別番号、生年月日、現住所、電話番号を入力します。

### Sarah が子の情報を提出 {#sarah-provides-child-information}

自分の個人情報を入力した後、「**[!UICONTROL Next]**」（次へ）をクリックし、Sarah は「Child Information」（子供の情報）セクションに移動します。

Child Informationセクションで、次の詳細を入力します。

* チャイルドサポートサービスを要求する子の人数
* 子の名前、社会保証番号、生年月日、出生地

子が複数の場合は、入力の詳細が同一のフォームを、追加で使用できます。\
Sarah は唯一の子である Joe を選び、その名前を入力します。

### Sarah が支払情報を入力 {#sarah-provides-payment-information}

1 人以上の養子に関する情報を入力し終えると、「**[!UICONTROL Next]**」（次へ）をクリックして、「Payment Information」（支払情報）セクションに移動します。****

「Payment Information」（支払情報）セクションでは、チャイルドサポート手当を受け取るための銀行口座の詳細を入力します。\
Sarah は 10 桁の口座番号を入力します。

## Sarah が申込手数料を支払い、フォームに署名する {#sarah-pays-the-application-fee-and-signs-the-form}

申込の利用規約に同意した後、Sarah は 25 ドルの申込手数料を支払います。申込を処理するには、申込手数料が必要です。\
Sarah はクレジットカードの詳細を入力し、「**[!UICONTROL Pay Now]**」（今すぐ支払う）をクリックします。料金を支払うと、PDF版のアプリが表示され、署名フィールドが表示されます。

![sarah-sign-1](assets/sarah-sign-1.png)

Sarah は、手入力、描画による手書き、署名画像の挿入、またはモバイル機器のタッチスクリーンでの描画のいずれかによって署名できます。Sarah は自分の名前を入力し、「Click To Sign」（クリックして署名）をクリックします。

Sarah の申込は We.Gov のサイトに送信されます。

### <strong>Sarah が送信確認の電子メールを受信</strong> {#strong-sarah-receives-an-acknowledgement-email-strong}

申込手数料を支払った後、Sarah は We.Gov サイトから送信確認の電子メールを受け取ります。\
 We.Gov は申込を処理し、申込が承認されると、毎月の手当を受け取れることが Sarah に通知されます。

![sarah-ack-email](assets/sarah-ack-email.png)

### 仕組み {#how-it-works-1}

チャイルドサポート申込用のパネルには、上部タブ、ウィザード、アコーディオンなどが組み合わせてレイアウトされています。ここでは、We.Gov チャイルドテンプレートというフォームテンプレートが使用されています。

申込者は各セクションを移動することにより、フォームの各種コンポーネントに入力できます。フォームを入力、送信し、利用規約に同意して、手数料を支払うと、カスタムワークフローが開始されます。カスタムワークフローは、申込の送信を確認する電子メールを申込者に自動送信します。申込は、検証および承認のために機関の関連部署に転送されます。

フォームのレイアウトは、「Gov Child Support Service テーマ」内で指定します。スタイル設定には、コンポーネントスタイル、ページの背景色、コンポーネントのフォーマットのエラー状態、およびフォントスタイルが含まれます。

適格性チェックでは、フォーム内で指定されたルールが使用されます。以下に示す有効性チェックを使用します。

`SHOW passMsgWHEN (Does the child live in the state of GX? is equal to Yes) AND (Do you live in the state of GX? is equal to Yes) AND ( (Who has the main day-to-day care of the child? is equal to You) AND (Are you: is equal to The custodial parent) ) AND (Is the child you are applying for: is equal to Under 16 years) ELSE Hide`

`HIDE failMsg WHEN (Does the child lives in the state of GX? is equal to Yes) AND ( (Do you live in the state of GX? is equal to Yes) AND (Who has the main day-to-day care of the child? is equal to You) ) AND (Is the child you are applying for: is equal to Under 16 years) AND (Are you: is equal to The custodial parent) ELSE Show`

### 実際の動作確認 {#see-it-yourself-1}

In your browser, open `https://<hostname>:<PublishPort>/content/forms/af/we-gov/child-support/css.html` and fill the required information. 必要な情報を入力し、料金を支払い、ドキュメントに署名した後、申込書を送信すると、送信確認の電子メールが届きます。

We.Gov子テンプレートはこちらを参照してください。 `https://<hostname>:<AuthorPort>/editor.html/conf/we-gov/settings/wcm/templates/we-gov-child-template/structure.html`

テーマはこちらを参照してください。 `https://<hostname>:<AuthorPort>/editor.html/content/dam/formsanddocuments-themes/we-gov/we-gov-theme-A/jcr:content`

すべてのルールを確認するには、以下の手順を実行します。

1. オーサリングモードでフォームを開きます。

   URL: `https://<hostname>:<AuthorPort>/editor.html/content/forms/af/we-gov/child-support/css.html`

1. Select a component, and tap ![edit-rules](assets/edit-rules.png). 上記のルールを含む、すべてのルールがルールエディターに表示されます。

## Gloria が申込を受信 {#gloria-receives-the-application}

We.Gov の承認部署の責任者である Gloria は、送信された申込を表示、承認、または拒否することができます。AEM インボックスでは、Gloria はすべての送信済み申込を 1 つの場所で見ることができます。

### 仕組み {#how-it-works-2}

Sarah がチャイルドサポート申込を入力して送信すると、申込の PDF またはレコードのドキュメントが作成され、Gloria Rios のインボックスに送信されます。Gloria は送信された申込を確認し、申込を承認または拒否することができます。

### 実際の動作確認 {#see-it-yourself-2}

ページを開く `https://<hostname***>:<PublishPort>/content/we-gov/en.html`. ページで「 **[!UICONTROL サインイン]**」をタップし、「代表者として **[!UICONTROL ログイン]** 」チェックボックスを選択して、Gloria Riosのユーザー名/パスワードとしてgrios/passwordを使用してAEMインボックスにログインします。 チャイルドサポート申込書が表示されます。 For information about using AEM Inbox for forms-centric workflow tasks, see [Manage Forms applications and tasks in AEM Inbox](/help/forms/using/manage-applications-inbox.md).

![We.Gov リファレンスサイトの Gloria のインボックス](assets/gloria-inbox.png)

Gloria は申込ダッシュボードから申込を確認、承認、または拒否することができます。

### 仕組み {#how-it-works-3}

We.Gov の承認部署の責任者である Gloria が、AEM インボックスを開きます。Gloria は自分のタスク一覧でレビュータスクを確認します。レビュータスクを開き、表示します。

Gloria は、Sarah が詳細を入力したフォームの PDF および Sarah がアップロードしたドキュメントを確認します。\
 Gloria は申込を承認または拒否することができます。However, Gloria clicks **[!UICONTROL Assessment Required]** to get the application assessed.

![gloria-sends-assessment](assets/gloria-sends-assessment.png)

Sarah の申込が AEM ワークフローの開始点です。チャイルドサポート申込フォームが送信されると、AEM ワークフローが開始されます。AEM ワークフローで Gloria のタスクが作成されると、Gloria の AEM インボックスに表示されます。Gloria がオンサイト査定をリクエストすると、フィールドエージェントの新しいタスクが作成されます。

### 実際の動作確認 {#see-it-yourself-3}

設定が問題なく完了している場合、フォームを送信した直後に AEM ワークフローが開始します。Gloria の資格情報を使用してインボックスにログインします。

インボックス(https://&lt;***hostname***>:&lt;***PublishPort***>/content/we-gov/en.html)にアクセスします。 ページで、「 **[!UICONTROL サインイン]**」をタップし、「代表者として **[!UICONTROL ログイン]** 」チェックボックスを選択して、Gloriaのデフォルトの資格情報を使用します。

* ユーザー名：grios
* パスワード：password

Gloria の AEM インボックスには、Sarah の申込がレビュータスクとして追加されます。そのタスクを選択し、「**Assessment Required**」（査定が必要）をクリックして、次の手順に進みます。

### Conard が 査定タスクを受け取る {#conard-assessment-task}

Gloria が「**[!UICONTROL Assessment Required]**」（査定が必要）をクリックすると、Conard は自分の AEM インボックスでレビュータスクを受け取ります。このタスクは、ワークフローモデルで次の AEM ワークフロー手順として定義されています。レビュータスクを表示し、開きます。

Conard は、以下のように表示される申込者の査定タスクを取得します。

![conrad-inbox](assets/conrad-inbox.png)

チャイルドサポート査定は、タスクと関連付けられたフォームです。Conard は Sarah の詳細情報を、タスクの詳細に添付されたサポートドキュメントと共に取得します。Conard はデバイス上のフィールドにある査定フォームに入力し、再評価用に送信します。

Conard は Sarah が提出したすべての詳細情報を検証し、Sarah は査定内容に署名します。AEM Forms は場所とタイムスタンプの情報を取得し、署名に追加することができます。

![再評価のための提出](assets/submit-for-re-evaluation.png)

Conard clicks **[!UICONTROL Submit For Reevaluation]**, and the AEM workflow submits the assessment to the We.Gov organization.

### 仕組み {#how-it-works-4}

Gloria が査定をリクエストすると、AEM ワークフローの次の手順が開始され、Conard のインボックスに査定タスクが追加されます。Conard はフィールドワーカーの役割を担います。

Conard は Sarah の所在地を訪問して Sarah が提出した情報に偽りがないことを確認し、査定フォームを入力します。Sarah が入力し完了した PDF のフォームに、Conard はアクセスすることができます。

### 実際の動作確認 {#see-it-yourself-4}

タブレットで AEM インボックスを開き、Conard の資格情報を使用してログインします。

デフォルトの Conard の資格情報：

* ユーザー名：csimms
* パスワード：password

新しい査定リクエストタスクがインボックスに追加されています。完了した査定を送信し、次の手順に進みます。

### Gloria が査定をレビューし申込を承認 {#gloria-reviews-the-assessment-and-approves-the-application}

Conard が査定を送信した後、Gloria は自分のインボックスでレビュータスクを確認します。She selects and opens **[!UICONTROL Review]**.

![gloriainbox-1](assets/gloriainbox-1.png)

「タスクの詳細」の下で、Gloriaは「Submit for Re-evaluation」（Conard著）と呼ばれる最後のアクションを確認します。 Conard Simms が申込の査定を行ったことを確認します。

![栄光の承認](assets/gloriaapproves.png)

### 仕組み {#how-it-works-5}

Conard が査定を送信した後、Gloria は自分のインボックスでレビュータスクを確認します。Reviewを選択して開きます。 「Task Details」（タスクの詳細）で、Gloria は Conard により作成された「すべて問題なし」という査定コメントを確認します。

Gloria は申込を承認します。

### 実際の動作確認 {#see-it-yourself-5}

インボックスを開き、Gloria の資格情報を使用してログインします。レビューと呼ばれる新しいタスクがインボックスに表示されます。

タスクを開いて、「最後に実行した操作」のステータスを確認します。査定に基づいて、申込を承認します。

## Sarah が承認の電子メールを受信 {#sarah-receives-an-approval-email}

Gloria が申込を承認した後、Sarah は We.Gov サイトから申込の承認を知らせる電子メールを受信します。

The **[!UICONTROL View Document]** button in the email links to her enrollment details. Sarah clicks **[!UICONTROL View Document.]**

![approval-enrolment-kit-email](assets/approval-enrolment-kit-email.png)

登録ドキュメントには、参照 ID、サポート対象の子、開始日、銀行口座番号、支払間隔、支払金額などの詳細がリストされています。

![sarah-enrollment-details](assets/sarah-enrollment-details.png)

このページで、Sarah は自分がアップロードしたドキュメントを確認できます。

![アップロードされたドキュメント](assets/uploaded-documents.png)

### 仕組み {#how-it-works-6}

Gloria が申込を承認すると、Sarah は登録ドキュメントへのリンクが記載された自動電子メールを受信します。

登録ドキュメントは対話型の通信であり、任意のデバイスで表示できます。 ドキュメントにはチャイルドサポートサービスの詳細と Sarah が提供した情報が含まれます。

### 実際の動作確認 {#see-it-yourself-6}

登録ドキュメントへのリンクが記載された自動電子メールの受信に指定した電子メールクライアントを確認します。

または、ブラウザーでドキュメントを表示するには、次を開きます。 `https://<hostname>:<PublishPort>/content/aemforms-refsite/doclink.html?document=/content/forms/af/we-gov/child-support/enrollment-document&referenceId=[reference-id]&channel=web`

## We.Govは、アプリケーションのパフォーマンスを分析 {#we-gov-analyzes-the-performance-of-the-application}

We.Govは、チャイルドサポートサービス申込のパフォーマンスを時折見直し、お客様が直面する可能性のある問題を確認します。 ユーザーはこの分析を使用して、チャイルドサポートサービスの申し込みに必要な変更に関する十分な情報に基づく判断を行い、ユーザーエクスペリエンスを向上し、フォームの中断率を低減し、コンバージョンを向上します。 同社は、分析のために AEM Forms を Adobe Analytics と統合しています。以下の画像では、同社の Analytics ダッシュボードを紹介しています。

![child-support-analytics-ダッシュボード](assets/child-support-analytics-dashboard.png)

### 仕組み {#how-it-works-7}

チャイルドサポートサービス申込フォームのパフォーマンス指標は、Adobe Analyticsを使用して追跡されます。 Adobe Analytics の設定とレポートの表示について詳しくは、「[フォームおよびドキュメント用の Analytics の設定](/help/forms/using/configure-analytics-forms-documents.md)」を参照してください。

### 実際の動作確認 {#see-it-yourself-7}

Analyticsレポートの表示および調査を行うために、リファレンスサイトでチャイルドサポートサービスアプリケーションのシードデータを提供しています。 シードデータを使用する前に、「[Analytics の設定](/help/forms/using/setup-reference-sites.md#configureanalytics)」を参照してください。シードデータを使用したレポートを閲覧するには、作成者インスタンスで以下の手順を実行します。

1. Go to **[!UICONTROL Forms &amp; Documents]** UI at https://&lt;*hostname*>:&lt;*AuthorPort*>/aem/forms.html/content/dam/formsanddocuments.

1. Click to open the **We.Gov** Folder.
1. 「 **[!UICONTROL Application for Child Support Services]** 」アダプティブフォームを選択し、ツールバーの「Analytics **[!UICONTROL を]** 有効にする」をクリックします。

1. フォームを再度選択し、ツールバーの **[!UICONTROL Analyticsレポート]** をクリックして、レポートを生成します。 最初は、空白のレポートが表示されます。

シードデータを使用してAnalyticsレポートを生成するには：

1. In the address browser of CRXDE lite, type: **/apps/we-gov/demo-artifacts/analyticsTestData/Child support service Analytics Test Data**
1. シードデータは、左側のディレクトリ構造で選択されます。
1. 選択されたファイルをダブルクリックして、右側のパネルにファイルのコンテンツを開きます。
1. テストデータファイル内のすべてのコンテンツをコピーします。
1. In CRXDE, navigate to: **/content/dam/formsanddocuments/we-gov/child-support/css/jcr:content/analyticsdatanode/lastsevendays**
1. 「Properties」（プロパティ）内の analyticsdata フィールドに、テストデータファイルのコピーした内容を貼り付けます。
1. チャイルドサポートサービスの **[!UICONTROL 申し込みの分析レポートを再生成]**。 生成されたレポートにシードデータが表示されます。

