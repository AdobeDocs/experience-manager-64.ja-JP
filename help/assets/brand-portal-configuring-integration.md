---
title: AEM Assets と Brand Portal の統合の設定
description: 'アセットおよびコレクションを Brand Portal に公開するために AEM Assets を Brand Portal と統合する方法について説明します。 '
contentOwner: VG
translation-type: tm+mt
source-git-commit: 0d70a672a2944e2c03b54beb3b5f734136792ab1

---


# AEM Assets と Brand Portal の統合の設定 {#configure-aem-assets-integration-with-brand-portal}

アセットおよびコレクションを Brand Portal に公開するために AEM Assets を Brand Portal と統合する方法について説明します。

Adobe Experience Manager(AEM)Assets Brand portalのお客様は、AEM AssetsをBrand portalと統合して、Brand portalにアセットを公開できます。 この統合は、Adobe.io インターフェイスを使用して設定できます。

> [!N注]
>
>AEM Assets Brand Portal と AEM Assets を連携させるには、AEM 6.4.1.0 以降にアップグレードすることをお勧めします。AEM 6.4 では、Brand Portal との連携を設定する際にエラーが発生し、レプリケーションが失敗します。

最初に、Marketing Cloud の公開ゲートウェイに、認証メカニズムを含むアプリケーションを作成します。次に、ゲートウェイから取得したアプリケーション ID を使用して、AEM Assets インスタンスにプロファイルを作成します。

この設定を使用して、AEM Assets から Brand Portal にアセットを公開します。バックエンドでは、AEM サーバーがゲートウェイを使用してプロファイルを認証し、AEM Assets と Brand Portal を統合します。

>[!NOTE]
>
>The UI for configuring oAuth integrations is hosted in [https://legacy-oauth.cloud.adobe.io/](https://legacy-oauth.cloud.adobe.io/), which was earlier hosted in [https://marketing.adobe.com/developer/](https://marketing.adobe.com/developer/).

## JWT アプリケーションの作成 {#create-jwt-application}

1. Log in to [https://legacy-oauth.cloud.adobe.io/](https://legacy-oauth.cloud.adobe.io/) with your Adobe ID. 「 [!UICONTROL JWT Applications] 」ページに移動します。

   >[!NOTE]
   >
   >組織のシステム管理者の場合にのみ、アプリケーション ID を作成できます。テナントは、Adobe Marketing Cloud に登録している会社を意味する用語です。

2. Select **[!UICONTROL Add Application]** to create an application.
3. 「アプリケーシ **[!UICONTROL ョン名]** 」と「説明」を指定 **[!UICONTROL します]**。
4. 「**[!UICONTROL 組織]**」リストからアセットを同期する組織を選択します。
5. From the **[!UICONTROL Scope]** list, select **[!UICONTROL dam-read]**, **[!UICONTROL dam-sync]**, **[!UICONTROL dam-write]**, and **[!UICONTROL cc-share]**.
6. 「**[!UICONTROL 追加]**」をタップまたはクリックします。JWT サービスアプリケーションが作成されます。アプリケーションを編集して保存することができます。
7. 新規アプリケーションに対して生成されたアプリケーション ID をコピーします。

   >[!NOTE]
   >
   >アプリケーション ID ではなくアプリケーションの秘密鍵を誤ってコピーしないようにしてください。

## 新しいクラウド設定の作成 {#create-a-new-cloud-configuration}

1. ローカル AEM Assets インスタンスの&#x200B;**[!UICONTROL ナビゲーション]**&#x200B;ページで、左側にある&#x200B;**[!UICONTROL ツール]**&#x200B;アイコンをタップまたはクリックします。

   ![chlimage_1-252](assets/chlimage_1-252.png)

2. Navigate to **[!UICONTROL Cloud Services > Legacy Cloud Services]**.

   ![cloudservices](assets/cloudservices.png)

3. In the [!UICONTROL Cloud Services] page, locate the **[!UICONTROL Assets Brand Portal]** service under **[!UICONTROL Adobe Experience Cloud]**.

   ![bpcloudservices](assets/bpcloudservices.png)

4. Tap/ click the **[!UICONTROL Configure now]** link below the service to display the [Create Configuration] dialog.
5. In the [!UICONTROL Create Configuration] dialog, specify a title and name for the new configuration and tap/click **[!UICONTROL Create]**.

   ![bp-config](assets/bp-config.png)

6. In the [!UICONTROL AEM Assets Brand Portal Replication] dialog, specify the URL of your organization in the [!UICONTROL Tenant URL] field.
7. 「[!UICONTROL クライアント ID]」フィールドに、[アプリケーションの作成](#create-jwt-application)の手順の最後でコピーしたアプリケーション ID を貼り付けます。「**[!UICONTROL OK]**」をクリックします。

   ![public-folder-publish](assets/public-folder-publish.png)

8. To make the assets (published from AEM) publicly available to general users of Brand Portal, enable the **[!UICONTROL Public Folder Publish]** check box .

   >[!NOTE]
   >
   >「**[!UICONTROL 公開フォルダーの公開]**」を有効にするオプションは、AEM 6.3.2.1 以降で利用できます。

9. [!UICONTROL Brand Portal の設定]ページで、「**[!UICONTROL 公開鍵を表示]**」をタップまたはクリックして、インスタンス用に生成した公開鍵を表示します。

   ![display-public-key](assets/display-public-key.png)

   Alternatively, click **[!UICONTROL Download Public Key for OAuth Gateway]** to download the file containing the public key. 次に、ファイルを開いて公開鍵を表示します。

## 統合の有効化 {#enable-integration}

1. Display the public key using one of the following methods mentioned in the last step of the procedure [Add a new configuration to Marketing Cloud](#create-a-new-cloud-configuration).

   * 「**[!UICONTROL 公開鍵を表示]**」ボタンをクリックして、鍵を表示します。
   * 鍵が含まれるダウンロードファイルを開きます。

2. Open the Marketing Cloud Developer Connection interface and click the application you created in [Create an application](#create-jwt-application).
3. 設定インターフェイスの「**[!UICONTROL 公開鍵]**」フィールドに公開鍵を貼り付けます。
4. 「**[!UICONTROL 保存]**」をタップまたはクリックします。アプリケーションが更新されたことを確認するメッセージが表示されます。

## 統合のテスト {#test-the-integration}

1. ローカルの AEM Assets インスタンスの&#x200B;**[!UICONTROL ナビゲーション]**&#x200B;ページで、左側の&#x200B;**[!UICONTROL ツール]**&#x200B;アイコンをクリックします。

   ![chlimage_1-253](assets/chlimage_1-253.png)

2. Navigate to **[!UICONTROL Deployment > Replication]**.

   ![deploymentreplication](assets/deploymentreplication.png)

3. In the [!UICONTROL Replication] page, tap/click **[!UICONTROL Agents on author]**.

   ![agents_on_author](assets/agents_on_author.png)

4. AEM オーサーと Brand Portal の間の接続を検証するには、4 つのレプリケーションエージェントのいずれかを開き、「**[!UICONTROL 接続をテスト]**」をクリックします。

   >[!NOTE]
   >
   >レプリケーションエージェントは並行して動作し、ジョブの分散を均等に共有するので、パブリッシング速度が元の速度の4倍に向上します。 クラウドサービスの設定後は、複数のアセットの並行公開を有効にするために、デフォルトでアクティブ化される複製エージェントを有効にするために、追加の設定は必要ありません。

   >[!NOTE]
   >
   >どのレプリケーションエージェントも無効にしないでください。一部のアセットのレプリケーションが失敗する可能性があります。

   ![aem_assets_parallelpublishing](assets/aem_assets_parallelpublishing.png)

5. テスト結果の一番下を見て、レプリケーションが成功したことを確認します。

   ![replication_succeeded](assets/replication_succeeded.png)

レプリケーションが正常に終了したら、アセット、フォルダー、コレクションを Brand Portal に公開することができます。詳しくは、次を参照してください。

* [アセットおよびフォルダーの Brand Portal への公開](brand-portal-publish-folder.md)
* [Brand Portal へのコレクションの公開](brand-portal-publish-collection.md)

## Brand Portal へのアセットの公開 {#publish-assets-to-brand-portal}

レプリケーションが正常に終了したら、アセット、フォルダー、コレクションを Brand Portal に公開することができます。アセットを Brand Portal に公開するには、次の手順を実行します。

>[!NOTE]
>
>AEM オーサーが過剰なリソースを占有しないように、できればピーク時を避け、時間をずらして公開することをお勧めします。

1. アセットコンソールで目的のアセットにマウスポインターを置き、クイックアクションから「**[!UICONTROL 公開]**」オプションを選択します。

   または、Brand Portal に公開するアセットを選択します。

   ![publish2bp-2](assets/publish2bp-2.png)

2. アセットをBrand Portalに公開するには、次の2つのオプションを使用できます。
   * [アセットを直ちに発行](#publish-now)
   * [アセットを後で公開](#publish-later)

### アセットを今すぐ公開 {#publish-now}

選択したアセットを Brand Portal に公開するには、次のいずれかを実行します。

* From the toolbar, select **[!UICONTROL Quick Publish]**. Then from the menu, select **[!UICONTROL Publish to Brand Portal]**.

* From the toolbar, select **[!UICONTROL Manage Publication]**.

   1. Then from the **[!UICONTROL Action]** select **[!UICONTROL Publish to Brand Portal]**, and from **[!UICONTROL Scheduling]** select **[!UICONTROL Now]**. Tap/ click **[!UICONTROL Next].**

   2. Within **[!UICONTROL Scope]**, confirm your selection and tap/ click **[!UICONTROL Publish to Brand Portal]**.

アセットが Brand Portal への公開用のキューに入れられたことを示すメッセージが表示されます。Brand Portal のインターフェイスにログインして、公開されたアセットを確認します。

### アセットを後で公開 {#publish-later}

アセットを Brand Portal に公開するスケジュールを未来の日時で設定するには、次のようにします。

1. Once you have selected assets/ folders to publish, select **[!UICONTROL Manage Publication]** from the tool bar at the top.
2. On **[!UICONTROL Manage Publication]** page, select **[!UICONTROL Publish to Brand Portal]** from **[!UICONTROL Action]** and select **[!UICONTROL Later]** from **[!UICONTROL Scheduling]**.

   ![publishlaterbp-1](assets/publishlaterbp-1.png)

3. Select an **[!UICONTROL Activation date]** and specify time. 「**[!UICONTROL 次へ]**」をタップまたはクリックします。
4. Select an **[!UICONTROL Activation date]** and specify time. 「**[!UICONTROL 次へ]**」をタップまたはクリックします。
5. Specify a Workflow title under **[!UICONTROL Workflows]**. Tap/ click **[!UICONTROL Publish Later]**.

   ![publishworkflow](assets/publishworkflow.png)

次に、Brand portalにログインして、公開されたアセットがBrand portalインターフェイスで使用できるかどうかを確認します。

![bp_631_landing_page](assets/bp_landing_page.png)
