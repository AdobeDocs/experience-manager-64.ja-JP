---
title: アダプティブフォームの CAPTCHA の使用
seo-title: Using CAPTCHA in adaptive forms
description: アダプティブフォームでAEM CAPTCHA またはGoogle reCAPTCHA サービスを設定する方法を説明します。
seo-description: Learn how to configure AEM CAPTCHA or Google reCAPTCHA service in adaptive forms.
uuid: 8bcb0dd7-b43c-4a36-8f6b-7875b68f9ba1
contentOwner: vishgupt
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: author, adaptive_forms
discoiquuid: 32369b0b-5abf-487d-ae6b-972c254eb7e2
feature: Adaptive Forms
exl-id: 1129004b-5e8b-42fd-98ed-f203edde93b9
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '691'
ht-degree: 47%

---

# アダプティブフォームの CAPTCHA の使用 {#using-captcha-in-adaptive-forms}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

CAPTCHA（Computers and Humans Apart を伝える完全自動公開チューリングテスト）は、人と自動化されたプログラムまたはボットを区別するためにオンライントランザクションで一般的に使用されるプログラムです。 テストを行ってユーザーの反応を評価し、サイトを使用しているのが人間かボットかを判断します。テストが失敗した場合の続行を防ぎ、ボットがスパムや悪意のある目的を掲示するのを防ぎ、オンライントランザクションのセキュリティを確保します。

AEM Formsは、アダプティブフォームで CAPTCHA をサポートしています。 Google が提供する reCAPTCHA サービスを使用して、CAPTCHA を実装できます。

>[!NOTE]
>
>AEM Formsは reCaptcha v2 のみをサポートします。 その他のバージョンはサポートされません。
>
>アダプティブフォームの CAPTCHA は、AEM Formsアプリのオフラインモードではサポートされていません。

## Google が提供する reCAPTCHA サービスの設定 {#google-recaptcha}

フォーム作成者は、Googleの reCAPTCHA サービスを使用して、アダプティブフォームに CAPTCHA を実装できます。 サイトを保護する高度な CAPTCHA 機能を提供します。 reCAPTCHA の仕組みについて詳しくは、 [Google reCAPTCHA](https://developers.google.com/recaptcha/).

![recaptcha](assets/recaptcha.png)

AEM Forms で reCAPTCHAを実装するには、以下の手順を実行します。

1. 取得 [reCAPTCHA API キーペア](https://www.google.com/recaptcha/admin) Googleから サイトキーと秘密鍵が含まれます。
1. クラウドサービスの設定コンテナを作成します。

   1. **[!UICONTROL ツール／一般／設定ブラウザー]**&#x200B;に移動します。
      * 詳しくは、[設定ブラウザーのドキュメント](/help/sites-administering/configurations.md)を参照してください。
   1. 以下の手順を実行して、global フォルダーをクラウド設定用に有効にします。クラウドサービス設定用に別のフォルダーを作成する場合は、この手順をスキップしてください。

      1. 設定ブラウザーで、**[!UICONTROL global]** フォルダーを選択して「**[!UICONTROL プロパティ]**」をタップします。
      1. 設定プロパティダイアログで、「**[!UICONTROL クラウド設定]**」を有効にします。
      1. 「**[!UICONTROL 保存して閉じる]**」をタップして設定内容を保存し、ダイアログを閉じます。
   1. 設定ブラウザーで「**[!UICONTROL 作成]**」をタップします。
   1. 設定を作成ダイアログでフォルダーのタイトルを指定し、「**[!UICONTROL クラウド設定]**」を有効にします。
   1. 「**[!UICONTROL 作成]**」をタップします。これで、クラウドサービス設定が有効になったフォルダーが作成されました。


1. reCAPTCHA のクラウドサービスを設定します。

   1. AEMオーサーインスタンスで、に移動します。 ![ツール](assets/tools.png) >  **Cloud Services**.
   1. タップ **[!UICONTROL reCAPTCHA]**. 設定ページが開きます。 前の手順で作成した設定コンテナを選択し、をタップします。 **[!UICONTROL 作成]**.
   1. reCAPTCHA サービスの名前、サイトキー、秘密鍵を指定し、「**[!UICONTROL 作成]**」をタップして、クラウドサービスの設定を作成します。
   1. コンポーネントを編集ダイアログで、サイトおよび手順 1 で取得した秘密鍵を指定します。「**[!UICONTROL 設定を保存]**」をタップしてから、「**[!UICONTROL OK]**」をタップして設定を完了します。

   reCAPTCHA サービスを設定すると、アダプティブフォームで使用できるようになります。 詳しくは、 [アダプティブフォームでの CAPTCHA の使用](#using-captcha).

## アダプティブフォームでの CAPTCHA の使用 {#using-captcha}

アダプティブフォームで CAPTCHA を使用するには：

1. アダプティブフォームを編集モードで開きます。

   >[!NOTE]
   >
   >アダプティブフォームの作成時に選択した設定コンテナに reCAPTCHA クラウドサービスが含まれていることを確認します。 アダプティブフォームのプロパティを編集して、フォームに関連付けられた設定コンテナを変更することもできます。

1. コンポーネントブラウザーから、 **[!UICONTROL Captcha]** コンポーネントをアダプティブフォームに追加します。

   >[!NOTE]
   >
   >アダプティブフォーム内での複数の Captcha コンポーネントの使用はサポートされていません。 また、遅延読み込み用とマークされたパネルやフラグメントでは、CAPTCHA を使用しないことをお勧めします。

   >[!NOTE]
   >
   >Captcha は時間に依存し、約 1 分で有効期限が切れます。 したがって、Captcha コンポーネントは、アダプティブフォーム内の「送信」ボタンの直前に配置することをお勧めします。

1. 追加した Captcha コンポーネントを選択して、![cmppr](assets/cmppr.png) をタップし、プロパティを編集します。
1. CAPTCHA ウィジェットのタイトルを指定します。デフォルト値は **Captcha** です。タイトルを表示しない場合は、「**[!UICONTROL タイトルを非表示にする]**」を選択します。
1. **[!UICONTROL Captcha サービス]**&#x200B;ドロップダウンで「**[!UICONTROL reCaptcha]**」を選択して、reCAPTCHA サービスを有効にします（「[Google による reCAPTCHA サービス](#google-recaptcha)」に記載されている手順に従って reCAPTCHA サービスが設定されている場合）。設定ドロップダウンから設定を選択します。また、サイズとして「 」を選択します。 **[!UICONTROL 標準]** または **[!UICONTROL コンパクト]** reCAPTCHA ウィジェット用。

   >[!NOTE]
   >
   >デフォルトの AEM CAPTCHA サービスは非推奨なので、Captcha サービスドロップダウンで「**[!UICONTROL デフォルト]**」を選択しないでください。

1. 各プロパティを保存します。

アダプティブフォームで reCAPTCHA サービスが有効になっている。 フォームをプレビューして、CAPTCHA が機能していることを確認できます。
