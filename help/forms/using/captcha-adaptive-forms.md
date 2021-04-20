---
title: アダプティブフォームの CAPTCHA の使用
seo-title: アダプティブフォームの CAPTCHA の使用
description: アダプティブフォームで AEM CAPTCHA または Google reCAPTCHA サービスを設定する方法を説明します。
seo-description: アダプティブフォームで AEM CAPTCHA または Google reCAPTCHA サービスを設定する方法を説明します。
uuid: 8bcb0dd7-b43c-4a36-8f6b-7875b68f9ba1
contentOwner: vishgupt
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: author, adaptive_forms
discoiquuid: 32369b0b-5abf-487d-ae6b-972c254eb7e2
feature: Adaptive Forms
translation-type: tm+mt
source-git-commit: 75312539136bb53cf1db1de03fc0f9a1dca49791
workflow-type: tm+mt
source-wordcount: '675'
ht-degree: 82%

---


# アダプティブフォームの CAPTCHA の使用 {#using-captcha-in-adaptive-forms}

CAPTCHA（Completely Automated Public Turing test to tell Computers and Humans Apart）は、オンライントランザクションにおいて人間と自動プログラムやボットとを区別するために一般的に使用されるプログラムです。テストを行ってユーザーの反応を評価し、サイトを使用しているのが人間かボットかを判断します。これにより、テストに失敗した場合ユーザーは続行できないため、ボットによるスパムの投稿や悪意のある目的を防止し、オンライントランザクションを安全に保ちます。

AEM によるアダプティブフォームの CAPTCHA のサポートGoogleのreCAPTCHAサービスを使用して、CAPTCHAを実装できます。

>[!NOTE]
>
>AEM Forms は reCaptcha v2 のみをサポートします。その他のバージョンはサポートされません。
>
>アダプティブフォームの CAPTCHA は、AEM Forms アプリケーションのオフラインモードではサポートされていません。

## Google が提供する reCAPTCHA サービスの設定  {#google-recaptcha}

フォームの作成者は、Google による reCAPTCHA サービスを使用してアダプティブフォームに CAPTCHA を実装することができます。これにより、サイトを保護する高度な CAPTCHA 機能が提供されます。reCAPTCHA の仕組みについて詳しくは、「[Google reCAPTCHA](https://developers.google.com/recaptcha/)」を参照してください。

![奪い取る](assets/recaptcha.png)

AEM Forms で reCAPTCHAを実装するには：

1. Google から [reCAPTCHA API キーペア](https://www.google.com/recaptcha/admin)を取得します。これにはサイトキーと秘密鍵が含まれます。
1. クラウドサービス用の設定コンテナを作成します。

   1. **[!UICONTROL ツール/一般/設定ブラウザー]**&#x200B;に移動します。
      * 詳しくは、[設定ブラウザーのドキュメント](/help/sites-administering/configurations.md)を参照してください。
   1. 以下の手順を実行して、global フォルダーをクラウド設定用に有効にします。クラウドサービス設定用に別のフォルダーを作成する場合は、この手順をスキップしてください。

      1. 設定ブラウザーで、「**[!UICONTROL global]**」フォルダーを選択して「**[!UICONTROL プロパティ]**」をタップします。
      1. 設定プロパティダイアログで、「**[!UICONTROL クラウド設定]**」を有効にします。
      1. 「**[!UICONTROL 保存して閉じる]**」をタップして設定内容を保存し、ダイアログを閉じます。
   1. 設定ブラウザーで「**[!UICONTROL 作成]**」をタップします。
   1. 設定を作成ダイアログでフォルダーのタイトルを指定し、「**[!UICONTROL クラウド設定]**」を有効にします。
   1. 「**[!UICONTROL 作成]**」をタップして、クラウドサービス設定用に有効なフォルダーを作成します。


1. reCAPTCHA のクラウドサービスを設定します。

   1. AEMオーサーインスタンスで、![ツール](assets/tools.png) > **Cloud Services**&#x200B;に移動します。
   1. 「**[!UICONTROL reCAPTCHA]**」をタップします。設定ページが表示されます。上記の手順で作成した設定コンテナを選択し、「**[!UICONTROL 作成]**」をタップします。
   1. reCAPTCHAサービスの名前、サイトキー、秘密キーを指定し、「**[!UICONTROL 作成]**」をタップして、クラウドサービスの設定を作成します。
   1. コンポーネントを編集ダイアログで、サイトおよび手順 1 で取得した秘密鍵を指定します。「**[!UICONTROL 設定を保存]**」をタップし、「**[!UICONTROL OK]**」をタップして設定を完了します。

   reCAPTCHA サービスを設定すると、アダプティブフォームで使用できるようになります。詳しくは、「[アダプティブフォームの CAPTCHA の使用](#using-captcha)」を参照してください。

## アダプティブフォームで CAPTCHA を使用する  {#using-captcha}

アダプティブフォームで CAPTCHA を使用するには：

1. アダプティブフォームを編集モードで開きます。

   >[!NOTE]
   >
   >アダプティブフォームの作成時に選択した設定コンテナに、reCAPTCHA クラウドサービスが含まれていることを確認してください。アダプティブフォームのプロパティを編集して、そのアダプティブフォームに関連付けられている設定コンテナを変更することもできます。

1. コンポーネントブラウザーから&#x200B;**[!UICONTROL Captcha]** コンポーネントを、アダプティブフォームにドラッグアンドドロップしますす。

   >[!NOTE]
   >
   >アダプティブフォームにおける複数の Captcha コンポーネントの使用はサポートされていません。また、遅延読み込みとしてマークされているパネルやフラグメント内のパネルで CAPTCHA を使用することはお勧めしません。

   >[!NOTE]
   >
   >Captcha は、約 1 分間で期限切れになります。そのため、アダプティブフォームに「送信」ボタンを配置する直前に Captcha コンポーネントを配置することをお勧めします。

1. 追加したCaptchaコンポーネントを選択し、![cmppr](assets/cmppr.png)をタップしてプロパティを編集します。
1. CAPTCHA ウィジェットのタイトルを指定します。デフォルト値は&#x200B;**Captcha**&#x200B;です。 タイトルを表示しない場合は、「**[!UICONTROL タイトルを非表示にする]**」を選択します。
1. **[!UICONTROL Captcha service]**&#x200B;ドロップダウンから、**[!UICONTROL reCaptcha]**&#x200B;を選択し、Google](#google-recaptcha)による[ReCAPTCHAサービスの説明に従ってreCAPTCHAサービスを設定した場合に、このサービスを有効にします。 「設定」ドロップダウンから設定を選択します。また、reCAPTCHA ウィジェットのサイズを「**[!UICONTROL 標準]**」または「**[!UICONTROL コンパクト]**」から選択します。

   >[!NOTE]
   >
   >デフォルトの AEM CAPTCHA サービスは非推奨であるため、「Captcha サービス」ドロップダウンで「**[!UICONTROL デフォルト]**」を選択しないでください。

1. 各プロパティを保存します。

アダプティブフォーム上で reCAPTCHA サービスが有効になります。フォームをプレビューして、CAPTCHA が機能していることを確認できます。
