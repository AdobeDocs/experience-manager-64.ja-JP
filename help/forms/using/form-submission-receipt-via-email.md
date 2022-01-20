---
title: 電子メールによるフォーム送信確認の送信
seo-title: Sending a form submission acknowledgement via email
description: AEM Forms では、フォームの送信時に確認をユーザーに送信する電子メール送信アクションを設定できます。
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
ht-degree: 88%

---

# 電子メールによるフォーム送信確認の送信 {#sending-a-form-submission-acknowledgement-via-email}

## アダプティブフォームのデータ送信 {#adaptive-form-data-submission}

アクティビティフォームでは、あらかじめ用意されたいくつかの[送信アクション](/help/forms/using/configuring-submit-actions.md)が使用でき、フォームデータを複数のエンドポイントに送信できます。

例えば、 **メールアクション** 送信アクションは、アダプティブフォームの送信が成功すると、電子メールを送信します。 これは、フォームデータと PDF を電子メールで送信するように設定することもできます。

この記事では、アダプティブフォームで電子メールアクションを有効にする手順や、さまざまな設定について詳しく説明します。

>[!NOTE]
>
>また、 **メールPDFアクション** ：入力済みのフォームをPDFの添付ファイルとして電子メールで送信します。 このアクションで使用できる設定オプションは、電子メールアクションで使用できるオプションと同じです。PDF のメール送信アクションは、XFA ベースのアダプティブフォームに対してのみ使用できます。

## メール送信アクション {#email-action}

電子メールアクションを使用すると、アダプティブフォームの送信に成功したときに、1 人または複数の受信者に電子メールを自動的に送信できます。

>[!NOTE]
>
>電子メールアクションを使用するには、[電子メールサービスの設定](/help/sites-administering/notification.md#configuring-the-mail-service)で説明されているように AEM メールサービスを設定する必要があります。

### アダプティブフォームでの電子メールアクションの有効化 {#enabling-email-action-on-an-adaptive-form}

1. アダプティブフォームを編集モードで開きます。

1. **アダプティブフォームの開始**&#x200B;ツールバーの横にある&#x200B;**編集**&#x200B;をクリックします。

   コンポーネントを編集ダイアログが開きます。

   ![アダプティブフォームのコンポーネントの編集ダイアログ](assets/start_of_adp_form.png)

1. を選択します。 **送信アクション** 「 」タブで「 」を選択します。 **メールアクション** 送信アクションドロップダウンリストから

   このタブには、現在のフォームに対して電子メールアクションを設定するためのオプションが表示されます。

   ![送信アクションタブ](assets/dialog.png)

1. 宛先、CC、および BCC フィールドに有効な電子メール ID を指定します。

   件名および電子メールテンプレートフィールドに、それぞれ件名と電子メール本文を指定します。

   フィールドに変数プレースホルダーを指定することもできます。この場合、フィールドの値は、フォームがエンドユーザーによって正しく送信されたときに処理されます。詳細については、「[アダプティブフォームのフィールド名を使用した電子メールコンテンツの動的作成](/help/forms/using/form-submission-receipt-via-email.md#p-using-adaptive-form-field-names-to-dynamically-create-email-content-p)」を参照してください。

   フォームに添付ファイルがありそれを電子メールに添付する場合は、添付ファイルを含めるを選択してください。

   >[!NOTE]
   >
   >**PDF のメール送信アクション**&#x200B;を選択した場合は、添付ファイルを含めるオプションを選択する必要があります。

1. 「**OK**」をクリックして、変更を保存します。

### アダプティブフォームのフィールド名を使用した電子メールコンテンツの動的作成 {#using-adaptive-form-field-names-to-dynamically-create-email-content}

アダプティブフォームのフィールド名はプレースホルダーと呼ばれ、ユーザーがフォームを送信した後にそのフィールドの値によって置き換えられます。

電子メールアクションタブでは、アクションが実行されたときに処理されるプレースホルダーを使用できます。すなわち、電子メールのヘッダー（例えば宛先、CC、BCC、件名）を、ユーザーがフォームを送信したときに生成するようにできることを意味します。

プレースホルダーを定義するには、次を指定します。 `${<field name>}` をクリックします。

例えば、フォームが **** という`email_addr`電子メールアドレスフィールドを持っている場合、ユーザーの電子メール ID を取得するために、宛先、CC、または BCC フィールドに次のプレースホルダーを指定できます。

`${email_addr}`

ユーザーがフォームを送信すると、フォームの `email_addr` フィールドに入力された電子メール ID に電子メールが送信されます。

>[!NOTE]
>
>フィールドの&#x200B;**編集**&#x200B;ダイアログにフィールドの名前があります。

変数プレースホルダーは、**件名**&#x200B;や&#x200B;**電子メールテンプレート**&#x200B;フィールドにも使用できます。

以下に例を示します。

`Hi ${first_name} ${last_name},`

`Your form has been received by our department. It usually takes ten business days to process the request.`

`Regards`

`Administrator`

>[!NOTE]
>
>繰り返し可能なパネル内のフィールドは、変数プレースホルダーとして使用することはできません。
