---
title: Acrobat SignとAEM Formsの統合
seo-title: Integrate Acrobat Sign with AEM Forms
description: Acrobat Sign for AEM Formsの設定方法を説明します
seo-description: Learn how to configure Acrobat Sign for AEM Forms
uuid: 9efd5c44-3d87-4c56-aa6c-e65397fff243
contentOwner: sashanka
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: develop
discoiquuid: 7d494c2e-d457-4d52-89be-a77ffa07eb88
feature: Adaptive Forms, Acrobat Sign
exl-id: e7c27623-a889-4bd5-bfff-cfe513cd1a35
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '1003'
ht-degree: 38%

---

# Acrobat SignとAEM Formsの統合 {#integrate-adobe-sign-with-aem-forms}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

Acrobat Sign により、アダプティブフォームの電子サインワークフローを有効にできます。電子サインを使用すると、法務、販売、給与、人事管理など、様々な分野におけるドキュメント処理ワークフローが改善されます。

一般的なAcrobat Signおよびアダプティブフォームのシナリオでは、ユーザーは次の手順でアダプティブフォームに入力します。 **サービスを申し込む**. 例えば、クレジットカードの申込フォームや住民サービスフォームなどです。ユーザーが申込フォームに入力、送信、署名すると、フォームがサービスプロバイダーに送信され、さらにアクションが実行されます。 サービスプロバイダーは、申し込みを確認し、Acrobat Signを使用して申し込みを承認済みとマークします。 同様の電子署名ワークフローを有効にするには、Acrobat SignとAEM Formsを統合します。

Acrobat SignをAEM Formsと共に使用するには、AEM as a Cloud Services でAcrobat Signを設定します。

## 前提条件 {#prerequisites}

Acrobat Sign を AEM Forms に統合するには、以下のものが必要です。

* アクティブ [Acrobat Sign開発者アカウント。](https://acrobat.adobe.com/jp/ja/why-adobe/developer-form.html)
* An [SSL が有効](/help/sites-administering/ssl-by-default.md) AEM Formsサーバー。
* An [Acrobat Sign API アプリケーション](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobedocs/adobe-sign/master/gstarted/create_app.md).
* Acrobat Sign API アプリケーションの資格情報（クライアントの ID とクライアントシークレット）
* 再設定時に、オーサーインスタンスとパブリッシュインスタンスの両方から既存のAcrobat Sign設定を削除します。
* オーサーインスタンスとパブリッシュインスタンスには、[同一の暗号キー](/help/sites-administering/security-checklist.md#make-sure-you-properly-replicate-encryption-keys-when-needed)を使用します。

## AEM FormsとのAcrobat Signの設定 {#configure-adobe-sign-with-aem-forms}

前提条件を満たしたら、次の手順を実行して、オーサーインスタンス上でAcrobat SignとAEM Formsを設定します。

1. AEM Forms のオーサーインスタンスで、**ツール** ![ハンマー](assets/hammer.png)／**一般**／**設定ブラウザー**&#x200B;に移動します。
   * 詳しくは、[設定ブラウザーのドキュメント](/help/sites-administering/configurations.md)を参照してください。
1. **[!UICONTROL 設定ブラウザー]**&#x200B;ページで「**[!UICONTROL 作成]**」をタップします。
1. **[!UICONTROL 設定を作成]**&#x200B;ダイアログで、設定の&#x200B;**[!UICONTROL タイトル]**&#x200B;を指定し、「**[!UICONTROL クラウド設定]**」を有効にして「**[!UICONTROL 作成]**」をタップします。これにより、Cloud Services 用の設定コンテナが作成されます。
1. に移動します。 **ツール** ![ハンマー](assets/hammer.png) > **Cloud Services** > **Acrobat Sign** をクリックし、上記の手順で作成した設定コンテナを選択します。

   >[!NOTE]
   >
   >手順 1～4 を実行して、新しい設定コンテナを作成し、コンテナ内にAcrobat Sign設定を作成するか、既存の `global` フォルダー内 **ツール** ![ハンマー](assets/hammer.png) > **Cloud Services** > **Acrobat Sign**. 新しい設定コンテナで設定を作成する場合、必ず&#x200B;**[!UICONTROL 設定コンテナ]**&#x200B;フィールドに値を入力する必要があります。

   >[!NOTE]
   Cloud Services 設定ページの URL が「**HTTPS**」で始まっていることを確認してください。そうでない場合、 [SSL を有効にする](/help/sites-administering/ssl-by-default.md) (AEM Formsサーバー用 )

1. 設定ページで、をタップします。 **[!UICONTROL 作成]** AEM FormsでAcrobat Sign設定を作成します。
1. 内 **[!UICONTROL 一般]** タブ **[!UICONTROL Acrobat Sign設定を作成]** ページで、 **名前** をタップします。 **次へ**. 必要に応じてタイトルを指定し、設定のサムネールを参照して選択することもできます。

1. 現在のブラウザーウィンドウの URL をメモ帳にコピーします。AEM FormsでAcrobat Signアプリケーションを設定する必要があります。

1. Acrobat Signアプリケーションの OAuth 設定を指定します。

   1. ブラウザーウィンドウを開き、 Acrobat Sign Developer アカウントにログインします。
   1. AEM Forms 用に設定されているアプリケーションを選択し、「アプリケーションの OAuth を設定」をタップします。
   1. 内 **リダイレクト URL** ボックスに、前の手順でコピーした HTTPS URL を追加し、 **保存**.
   1. Acrobat Signアプリケーションに対して次の OAuth 設定を有効にし、 **保存**.
   * aggrement_read
   * aggrement_write
   * aggrement_send
   * widget_write
   * workflow_read

   Acrobat Signアプリケーションの OAuth 設定を設定してキーを取得する手順については、 [アプリケーションの OAuth 設定を構成します](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobedocs/adobe-sign/master/gstarted/configure_oauth.md) 開発者向けドキュメント。

   ![OAuth 設定](assets/oauthconfig_new.png)

1. に戻ります。 **Acrobat Sign設定を作成** ページ。 「**[!UICONTROL 設定]**」タブで、「**[!UICONTROL OAuth URL]**」フィールドに以下のデフォルトの URL が表示されます。

   `https://secure.na1.echosign.com/public/oauth`

   各パラメーターの意味は次のとおりです。

   **na1** は、デフォルトのデータベースシャードを参照します。

   データベースシャードの値を更新することができます。データベースシャードの新しい値を使用できるように、サーバーを再起動します。

1. **クライアント ID**（アプリケーション ID）と&#x200B;**クライアントの秘密鍵**&#x200B;の値を指定します。を選択します。 **添付ファイルにAcrobat Signも有効にする** アダプティブフォームに添付されたファイルを、署名用に送信された対応するAcrobat Signドキュメントに添付するオプション。

   タップ **[!UICONTROL Acrobat Signに接続]**. 資格情報の入力を求められたら、Acrobat Signアプリケーションの作成時に使用するアカウントのユーザー名とパスワードを入力します。

   タップ **[!UICONTROL 作成]** Acrobat Sign設定を作成します。

1. AEM web コンソールを開きます。URL は `https://'[server]:[port]'/system/console/configMgr` です。
1. 開く **Forms Common Configuration Service を使用します。**
1. 「**許可**」フィールドで、「すべてのユーザー - すべてのユーザーに（匿名かログインしているかによらず）添付ファイルのプレビューとフォームの検証と署名を許可」を&#x200B;**選択**&#x200B;して「**保存」をクリックします。** オーサーインスタンスがAcrobat Signを使用するように設定されている。
1. [レプリケーション](/help/sites-deploying/replication.md)を使用して、対応する公開インスタンスに同一の構成を作成します。

これで、Acrobat SignはAEM Formsと統合され、アダプティブフォームで使用する準備が整いました。 宛先 [アダプティブフォームでのAcrobat Signサービスの使用](../../forms/using/working-with-adobe-sign.md#configure-adobe-sign-for-an-adaptive-form)で、上記でアダプティブフォームのプロパティで作成した設定コンテナを指定します。

## Acrobat Signスケジューラーを設定して署名ステータスを同期 {#configure-adobe-sign-scheduler-to-sync-the-signing-status}

Acrobat Sign対応のアダプティブフォームは、すべての署名者が署名プロセスを完了した後で送信されます。 デフォルトでは、Acrobat Sign Scheduler サービスは、24 時間ごとに署名者の応答を確認（ポーリング）するようにスケジュールされています。 このデフォルトの間隔は、ご利用の環境に合わせて変更できます。デフォルトの間隔を変更するには、次の手順を実行します。

1. 管理者の資格情報を使用してAEM Formsサーバーにログインし、に移動します。 **ツール** > **運用** > **Web コンソール**.

   ブラウザーウィンドウで、以下の URL に移動することもできます。
   `https://[localhost]:'port'/system/console/configMgr`

1. を探して開きます。 **Acrobat Sign Configuration Service** オプション。 を指定します。 [cron 式](https://en.wikipedia.org/wiki/Cron#CRON_expression) 内 **ステータス更新スケジューラの式** フィールドとクリック **保存**. 例えば、毎日午前 0 時に設定サービスを実行するには、**ステータス更新スケジューラー式**&#x200B;フィールドに `0 0 0 1/1 * ? *` を指定します。

Acrobat Signのステータスを同期するためのデフォルトの間隔が変更されました。

## 関連記事 {#related-articles}

* [アダプティブフォームでのAcrobat Signの使用](../../forms/using/working-with-adobe-sign.md)
* [Acrobat SignとAEM Formsの連携（ビデオ）](https://experienceleague.adobe.com/docs/experience-manager-learn/forms/forms-and-sign/introduction.html?lang=ja)
* [Acrobat SignとAEM Formsの統合](../../forms/using/adobe-sign-integration-adaptive-forms.md)
