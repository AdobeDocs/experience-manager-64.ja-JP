---
title: Adobe Sign の AEM Forms への統合
seo-title: Integrate Adobe Sign with AEM Forms
description: AEM Forms 用に Adobe Sign を設定する方法
seo-description: Learn how to configure Adobe Sign for AEM Forms
uuid: 9efd5c44-3d87-4c56-aa6c-e65397fff243
contentOwner: sashanka
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: develop
discoiquuid: 7d494c2e-d457-4d52-89be-a77ffa07eb88
feature: Adaptive Forms, Adobe Sign
exl-id: e7c27623-a889-4bd5-bfff-cfe513cd1a35
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '967'
ht-degree: 92%

---

# Adobe Sign の AEM Forms への統合 {#integrate-adobe-sign-with-aem-forms}

Adobe Sign により、アダプティブフォームの電子署名ワークフローを有効にすることができます。電子サインを使用すると、法務、販売、給与、人事管理など、様々な分野におけるドキュメント処理ワークフローが改善されます。

Adobe Sign とアダプティブフォームの一般的なシナリオでは、**サービスを申し込む**&#x200B;ためのアダプティブフォームをユーザーが入力します。例えば、クレジットカードの申込フォームや住民サービスフォームなどです。ユーザーが申込フォームの入力、送信、署名を行うと、サービスプロバイダーにそのフォームが送信され、追加の処理が実行されます。サービスプロバイダーは受信した申込フォームを確認し、Adobe Sign を使用してそのフォームを承認します。これに類似した電子署名ワークフローを有効にするには、Adobe Sign を AEM Forms に統合します。

Adobe SignをAEM Formsと共に使用するには、AEM as a Cloud Services でAdobe Signを設定します。

## 前提条件 {#prerequisites}

Adobe Sign を AEM Forms に統合するには、以下のものが必要になります。

* 有効な [Adobe Sign 開発者アカウント](https://acrobat.adobe.com/jp/ja/why-adobe/developer-form.html)
* [SSL が有効になっている](/help/sites-administering/ssl-by-default.md) AEM Forms サーバー
* [Adobe Sign API アプリケーション](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobedocs/adobe-sign/master/gstarted/create_app.md)。
* Adobe Sign API アプリケーションの資格情報（クライアントの ID と秘密鍵）
* 再設定時に、オーサーインスタンスとパブリッシュインスタンスの両方から既存のAdobe Sign設定を削除します。
* オーサーインスタンスとパブリッシュインスタンスには、[同一の暗号キー](/help/sites-administering/security-checklist.md#make-sure-you-properly-replicate-encryption-keys-when-needed)を使用します。

## AEM Forms を使用して Adobe Sign を設定する {#configure-adobe-sign-with-aem-forms}

上記の前提条件の準備が完了したら、以下の手順により、オーサーインスタンス上の AEM Forms を使用して Adobe Sign を設定します。

1. AEM Forms のオーサーインスタンスで、**ツール** ![ハンマー](assets/hammer.png)／**一般**／**設定ブラウザー**&#x200B;に移動します。
   * 詳しくは、[](/help/sites-administering/configurations.md)設定ブラウザーのドキュメントを参照してください。
1. **[!UICONTROL 設定ブラウザー]**&#x200B;ページで「**[!UICONTROL 作成]**」をタップします。
1. **[!UICONTROL 設定を作成]**&#x200B;ダイアログで、設定の&#x200B;**[!UICONTROL タイトル]**&#x200B;を指定し、「**[!UICONTROL クラウド設定]**」を有効にして「**[!UICONTROL 作成]**」をタップします。これにより、Cloud Services 用の設定コンテナが作成されます。
1. **ツール** ![ハンマー](assets/hammer.png)／**Cloud Services**／**Adobe Sign** に移動し、上記の手順で作成した設定コンテナを選択します。

   >[!NOTE]
   >
   >手順 1～4 を実行して、新しい設定コンテナを作成し、コンテナ内にAdobe Sign設定を作成するか、既存の `global` フォルダー内 **ツール** ![ハンマー](assets/hammer.png) > **Cloud Services** > **Adobe Sign**. 新しい設定コンテナで設定を作成する場合、必ず&#x200B;**[!UICONTROL 設定コンテナ]**&#x200B;フィールドに値を入力する必要があります。

   >[!NOTE]
   Cloud Services 設定ページの URL が「**HTTPS**」で始まっていることを確認してください。「HTTPS」で始まっていない場合は、AEM Forms サーバーで [SSL を有効](/help/sites-administering/ssl-by-default.md)にしてください。

1. 設定ページで、をタップします。 **[!UICONTROL 作成]** AEM FormsでAdobe Sign設定を作成します。
1. **[!UICONTROL Adobe Sign 設定を作成]**&#x200B;ページの「**[!UICONTROL 一般]**」タブで、設定の&#x200B;**名前**&#x200B;を指定して「**次へ**」をタップします。必要に応じてタイトルを指定し、設定のサムネールを参照して選択することもできます。

1. 現在のブラウザーウィンドウの URL をメモ帳にコピーします。この URL は、AEM Forms で Adobe Sign アプリケーションを設定する際に必要になります。

1. 以下の手順により、Adobe Sign アプリケーション用に OAuth 設定を構成します。

   1. ブラウザーウィンドウを開き、Adobe Sign 開発者アカウントにサインインします。
   1. AEM Forms 用に設定されているアプリケーションを選択し、「アプリケーションの OAuth を設定」をタップします。
   1. 上記の手順でコピーした HTTPS URL を「**リダイレクト URL**」ボックスに追加して「**保存**」をクリックします。
   1. Adobe Sign アプリケーションに対して以下の OAuth 設定を有効にして、「**保存**」をクリックします。
   * aggrement_read
   * aggrement_write
   * aggrement_send
   * widget_write
   * workflow_read

   Adobe Sign アプリケーション用に OAuth 設定を構成してキーを取得するための詳しい手順については、開発者用ドキュメントの「[アプリケーション用に OAuth 設定を構成する](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobedocs/adobe-sign/master/gstarted/configure_oauth.md)」を参照してください。

   ![OAuth 設定](assets/oauthconfig_new.png)

1. **Adobe Sign 設定を作成**&#x200B;ページに戻ります。「**[!UICONTROL 設定]**」タブで、「**[!UICONTROL OAuth URL]**」フィールドに以下のデフォルトの URL が表示されます。

   `https://secure.na1.echosign.com/public/oauth`

   各パラメーターの意味は次のとおりです。

   **na1** は、デフォルトのデータベースシャードを参照します。

   データベースシャードの値を更新することができます。サーバーを再起動すると、データベースシャードの新しい値を使用することができます。

1. **クライアント ID**（アプリケーション ID）と&#x200B;**クライアントの秘密鍵**&#x200B;の値を指定します。「**添付ファイルにも Adobe Sign を有効にする**」オプションを選択すると、アダプティブフォームに添付されているファイルが、署名用に送信された対応する Adobe Sign ドキュメントに添付されます。

   「**[!UICONTROL Adobe Sign に接続]**」をタップします。資格情報の入力画面が表示されたら、Adobe Sign アプリケーションの作成時に使用したユーザー名とパスワードを入力します。

   「**[!UICONTROL 作成]**」をタップして、Adobe Sign 設定を作成します。

1. AEM web コンソールを開きます。URL は `https://'[server]:[port]'/system/console/configMgr` です。
1. **Forms 共通設定サービス**&#x200B;を開きます。
1. 「**許可**」フィールドで、「すべてのユーザー - すべてのユーザーに（匿名かログインしているかによらず）添付ファイルのプレビューとフォームの検証と署名を許可」を&#x200B;**選択**&#x200B;して「**保存」をクリックします。**&#x200B;オーサーインスタンスが Adobe Sign を使用するように設定されます。
1. [レプリケーション](/help/sites-deploying/replication.md)を使用して、対応する公開インスタンスに同一の構成を作成します。

これで Adobe Sign が AEM Forms に統合され、アダプティブフォームで使用できるようになりました。[アダプティブフォームで Adobe Sign サービスを使用する](../../forms/using/working-with-adobe-sign.md#configure-adobe-sign-for-an-adaptive-form)には、上記のとおりアダプティブフォームのプロパティで作成した設定コンテナを指定します。

## Adobe Sign スケジューラーを設定して署名ステータスを同期する {#configure-adobe-sign-scheduler-to-sync-the-signing-status}

Adobe Sign が有効になっているアダプティブフォームは、すべての署名者がフォームに署名するまで送信されません。Adobe Sign スケジューラーサービスは、デフォルトで、署名者からの応答を 24 時間ごとにチェック（ポーリング）するように設定されています。このデフォルトの間隔は、ご利用の環境に合わせて変更できます。デフォルトの間隔を変更するには、次の手順を実行します。

1. 管理者の資格情報を使用して AEM Forms サーバーにログインし、**ツール**／**操作**／**Web コンソール**&#x200B;に移動します。

   ブラウザーウィンドウで、以下の URL に移動することもできます。
   `https://[localhost]:'port'/system/console/configMgr`

1. 「**Adobe Sign 設定サービス**」オプションを探して選択します。「[ステータス更新スケジューラーの式](https://en.wikipedia.org/wiki/Cron#CRON_expression)」フィールドで **Cron 式**&#x200B;を指定して「**保存**」をクリックします。例えば、毎日午前 0 時に設定サービスを実行するには、**ステータス更新スケジューラー式**&#x200B;フィールドに `0 0 0 1/1 * ? *` を指定します。

これで、Adobe Sign のステータスを同期するデフォルトの間隔が変更されました。

## 関連記事 {#related-articles}

* [アダプティブフォームで Adobe Sign を使用する](../../forms/using/working-with-adobe-sign.md)
* [AEM Forms で Adobe Sign を利用する（ビデオ）](https://experienceleague.adobe.com/docs/experience-manager-learn/forms/forms-and-sign/introduction.html?lang=ja)
* [Adobe Sign の AEM Forms への統合](../../forms/using/adobe-sign-integration-adaptive-forms.md)
