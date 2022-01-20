---
title: We.Finance 自動保険更新リファレンスサイトのチュートリアル
seo-title: We.Finance Auto Insurance Renewal reference site walkthrough
description: AEM forms とMicrosoft Dynamics との統合が、金融サービス会社における顧客体験をパーソナライズする方法を示す、We.Finance 自動保険の使用例に関する詳細なリファレンスサイトのチュートリアルを参照してください。
seo-description: Read on detailed reference site walkthrough of We.Finance Auto Insurance use case which showcases how AEM forms and its integration with Microsoft Dynamics helps personalize customer experience in a financial service company.
uuid: 18676ab4-9f8d-4014-b751-2a722fd152da
contentOwner: dekalra
topic-tags: introduction
discoiquuid: a960d489-f5a3-436a-b028-54292648c7be
exl-id: db416cbc-27a7-4a2c-b4b3-43e8963faf22
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '782'
ht-degree: 29%

---

# We.Finance 自動保険更新リファレンスサイトのチュートリアル {#we-finance-auto-insurance-renewal-reference-site-walkthrough}

## 前提条件 {#pre-requisites}

リファレンスサイトを設定します ( [AEM 6.4 Formsリファレンスサイトのセットアップと設定](/help/forms/using/setup-reference-sites.md).

## We.Finance リファレンスサイトのシナリオ  {#we-finance-reference-site-scenario}

We.Finance サイトは、AEM Formsのインタラクティブ通信機能を学ぶのに役立つ金融サービスサイトです。

AEM forms とMicrosoft Dynamics との統合が、金融サービス会社での顧客体験をパーソナライズする方法を示す、We.Finance 自動保険の使用例に関する詳細なチュートリアルを読みます。 このインタラクティブなガイドは、金融会社での複雑なデジタル取引や顧客とのコミュニケーションの実装を容易にするように設計されています。

**まず、ユースケースをご覧ください。**

Sarah Rose は We.Finance 社の既存の顧客で、自動保険契約を購入しています。今は保険の更新の時期だ。 We.Finance 社の保険営業担当である Gloria Rios は、Sarah に契約の更新について通知します。Sarah は電子メールに記載されている手順に従い、プロセスを正常に完了します。

## 自動保険申し込みのチュートリアル {#auto-insurance-application-walkthrough}

We.Finance 自動保険の申し込みシナリオは、ユーザーに対する視覚的なナレーションであり、次の 2 つのペルソナに基づいています。

* Sarah Rose（We.Finance 社の顧客）
* Gloria Rios（We.Finance 社の保険営業担当）

### Gloria が We.Finance 社から保険契約の更新通知を送信する {#gloria-sends-an-insurance-policy-renewal-communication-from-we-finance}

Gloria がAEMインスタンスにログインし、「 」をクリックします。 **自動保険の更新** その後、 **エージェント UI を開きます。**&#x200B;クリックすると、Sarah Rose の保険証明書に保険証明書が事前入力されます。 Gloria がクリック&#x200B;**送信** 画面に「送信開始」と表示され、数秒後に「送信に成功しました」と表示されます。

Sarah は「Your Auto Insurance Renewal」（自動保険更新）という件名の電子メールを受信します。

![agent_ui_email](assets/agent_ui_email.png)

#### 実際の動作確認 {#see-it-yourself}

に移動します。 **Adobe Experience Manager** > **Forms** > **Forms &amp; Documents** > **We.Finance** > **自動保険**. を選択します。 **自動保険の更新** インタラクティブ通信とクリック **エージェント UI を開く**. エージェント UI でインタラクティブ通信が開きます。ポリシードキュメントが添付された電子メールを受け取る有効な電子メールアドレスを入力し、「送信」をクリックします。

Auto Insurance Renewal インタラクティブ通信には、 `https://[authorHost]: authorPort]/aem/formdetails.html/content/dam/formsanddocuments/we-finance/autoinsurance/auto-insurance-renewal.`

### Sarah は We.Finance 社から保険契約の更新通知を受信し、更新を決める {#sarah-receives-an-insurance-policy-renewal-communication-from-we-finance-and-decides-to-renew}

Sarah は、We.Finance 社から添付ファイルを含む電子メールを受け取り、自動保険契約の期限が切れそうになっていることを通知します。 添付ファイルは、自動保険レターの印刷版です。

Sarah がクリック **今すぐ更新** Auto Insurance レターの Web 版にリダイレクトされます。 この手紙に加えて、Sarah はポリシーの有効期限が切れるまでの残り日数を見つけます。 このページでは、Sarah は保険契約の詳細（保険番号、支払期限、割引オファーやロイヤルティ報酬など）の基本的な概要を提供します。 Sarah が再度クリック **今すぐ更新** ポリシーの下に

![ref1](assets/ref1.png)

#### 仕組み {#how-it-works}

自動保険レターの Web および印刷出力は、インタラクティブ通信のマルチチャネル機能を使用して作成されます。

電子メールに含まれている「今すぐ更新する」ボタンは、自動保管更新の申し込みにリンクされます。これはパブリッシュインスタンス上のインタラクティブ通信です。

#### 実際の動作確認 {#see-it-yourself-1}

PDF が添付された電子メールを受信します。PDFは、自動保険レターの印刷版です。 クリック **今すぐ更新** をクリックして、ポリシーの web バージョンにアクセスします。 個人情報とポリシーの詳細を確認し、 **今すぐ更新** 別のインタラクティブ通信に移動します。

この **今すぐ更新** ボタンをクリックすると、Sarah はポリシーの web バージョンに移動します。 次の URL にアクセスできます。

`https://[authorServer]:[authorPort]/content/document.html?schema=fdm&documentId=/content/forms/af/we-finance/autoinsurance/auto-insurance-renewal/channels/web.html&customerId=1`

自動保険更新の詳細な概要を確認し、 **今すぐ更新** をクリックします。

### 支払いページの表示 {#sarah-reaches-the-payment-page}

We.Finance 社の支払いページが表示されます。Sarah は、自分のレコードと共に、ポリシー番号と有効期限を再確認します。 ページの右側で、Sarah は、合計金額に対して 10%のプレミアム割引を使用して、更新の支払いの概要を確認します。

#### 仕組み {#how-it-works-1}

「今すぐ更新」ボタンをクリックすると、支払いページに移動します。 支払いページはアダプティブフォームです。

#### 実際の動作確認 {#see-it-yourself-2}

「**今すぐ更新する**」をクリックして支払いページにアクセスします。クレジットカード情報を入力し、 **支払いを行う。**

オーサリングインスタンスの支払いページには、次の場所でアクセスできます。

`https://[authorServer]:[authorPort]/content/document.html?documentId=/content/forms/af/we-finance/credit-card/ccbillpayment.html&schema=fdm&customerId=1`

### Sarah は支払いを行ってプロセスを完了する {#sarah-makes-the-payment-and-completes-the-process}

Sarah がクレジットカードの詳細を入力し、クリックします **支払いを行う**.

#### 仕組み {#how-it-works-2}

Sarah がクレジットカードの詳細を入力して「送信」をクリックすると、クレジットカードによる支払い処理が行われ、アダプティブォームで設定された「ありがとうございます」メッセージが画面に表示されます。

#### 実際の動作確認 {#see-it-yourself-3}

次の場所で「支払いを行う」をクリックした後、確認メッセージを表示できます：

`https://[authorServer]:[authorPort]/content/forms/af/we-finance/credit-card/ccbillpayment/jcr:content/guideContainer.guideThankYouPage.html?owner=admin&status=Submitted`
