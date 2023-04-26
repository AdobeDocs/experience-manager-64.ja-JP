---
title: メールによるフォーム送信確認の送信
seo-title: Sending a form submission acknowledgement via email
description: AEM Formsでは、フォームの送信時に確認応答をユーザーに送信する電子メール送信アクションを設定できます。
seo-description: AEM Forms allows you to configure the email submit action that sends an acknowledgement to a user on submitting the form.
uuid: 77b3c836-6011-48bd-831c-ebc214218efb
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: publish
discoiquuid: 7ffe6317-174b-4d80-9ac6-9bfb5eed7e29
exl-id: e850d2a5-cb5f-4bd4-81dd-57951923b6d3
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '558'
ht-degree: 22%

---

# メールによるフォーム送信確認の送信 {#sending-a-form-submission-acknowledgement-via-email}

## アダプティブフォームのデータ送信 {#adaptive-form-data-submission}

アダプティブフォームには、すぐに使用できる複数の機能が用意されています [アクションを送信](/help/forms/using/configuring-submit-actions.md) フォームデータを異なるエンドポイントに送信するためのワークフロー。

例えば、 **メールアクション** 送信アクションは、アダプティブフォームの送信が成功すると、電子メールを送信します。 これは、フォームデータと PDF をメールで送信するように設定することもできます。

この記事では、アダプティブフォームで電子メールアクションを有効にする手順と、様々な設定について詳しく説明します。

>[!NOTE]
>
>また、 **メールPDFアクション** ：入力済みのフォームをPDFの添付ファイルとして電子メールで送信します。 このアクションで使用できる設定オプションは、「 E メール」アクションで使用できるオプションと同じです。 PDF のメール送信アクションは、XFA ベースのアダプティブフォームに対してのみ使用できます。

## メールアクション {#email-action}

電子メールアクションを使用すると、アダプティブフォームの送信が完了したときに、作成者が 1 人以上の受信者に電子メールを自動的に送信できます。

>[!NOTE]
>
>電子メールアクションを使用するには、AEM Mail サービスを設定する必要があります。詳しくは、 [メールサービスの設定](/help/sites-administering/notification.md#configuring-the-mail-service).

### アダプティブフォームでの電子メールアクションの有効化 {#enabling-email-action-on-an-adaptive-form}

1. アダプティブフォームを編集モードで開きます。

1. クリック **編集** の横 **アダプティブフォームの開始** ツールバー。

   編集コンポーネントダイアログが開きます。

   ![アダプティブフォームのコンポーネントを編集ダイアログ](assets/start_of_adp_form.png)

1. を選択します。 **送信アクション** 「 」タブで「 」を選択します。 **メールアクション** 送信アクションドロップダウンリストから

   「 」タブには、現在のフォームに対する電子メールアクションを設定するためのオプションが表示されます。

   ![「送信アクション」タブ](assets/dialog.png)

1. 「宛先」、「CC」、「BCC」フィールドに有効な電子メール ID を指定します。

   件名と電子メールの本文を、それぞれ「件名」と「電子メールテンプレート」フィールドに指定します。

   また、フィールドに変数のプレースホルダーを指定することもできます。指定した場合、エンドユーザーがフォームを正常に送信したときにフィールドの値が処理されます。 詳しくは、 [アダプティブフォームのフィールド名を使用した電子メールコンテンツの動的作成](/help/forms/using/form-submission-receipt-via-email.md#p-using-adaptive-form-field-names-to-dynamically-create-email-content-p).

   フォームに添付ファイルがあり、それをメールに添付する場合は、添付ファイルを含めるを選択してください。

   >[!NOTE]
   >
   >次を選択した場合、 **メールPDFアクション**「添付ファイルを含める」オプションを選択する必要があります。

1. 「**OK**」をクリックして、変更を保存します。

### アダプティブフォームのフィールド名を使用した電子メールコンテンツの動的作成 {#using-adaptive-form-field-names-to-dynamically-create-email-content}

アダプティブフォーム内のフィールド名はプレースホルダーと呼ばれ、ユーザーがフォームを送信した後にそのフィールドの値に置き換えられます。

「電子メールアクション」タブでは、アクションの実行時に処理されるプレースホルダーを使用できます。 これは、ユーザーがフォームを送信すると、電子メールのヘッダー（宛先、CC、BCC、件名など）が生成されることを意味します。

プレースホルダーを定義するには、次を指定します。 `${<field name>}` をクリックします。

例えば、フォームに **電子メールアドレス** フィールド、名前 `email_addr`ユーザーの電子メール ID を取り込むために、「宛先」、「CC」または「BCC」フィールドに次の情報を指定できます。

`${email_addr}`

ユーザーがフォームを送信すると、フォームの `email_addr` フィールドに入力されたメール ID にメールが送信されます。

>[!NOTE]
>
>フィールドの&#x200B;**編集**&#x200B;ダイアログにフィールドの名前があります。

変数のプレースホルダーは **件名** および **メールテンプレート** フィールド。

次に例を示します。

`Hi ${first_name} ${last_name},`

`Your form has been received by our department. It usually takes ten business days to process the request.`

`Regards`

`Administrator`

>[!NOTE]
>
>繰り返し可能なパネル内のフィールドは、変数プレースホルダーとして使用することはできません。
