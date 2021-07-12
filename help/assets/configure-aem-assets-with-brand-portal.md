---
title: AEM Assets と Brand Portal の連携の設定
description: 'AEM AssetsとBrand Portalを連携させて、アセットとコレクションをBrand Portalに公開する方法を説明します。 '
contentOwner: VG
feature: Brand Portal
role: Admin
exl-id: cde35555-259f-4d16-999f-2b93d597b8a5
source-git-commit: 3c050c33a384d586d74bd641f7622989dc1d6b22
workflow-type: tm+mt
source-wordcount: '1649'
ht-degree: 51%

---

# AEM Assets と Brand Portal の連携の設定 {#configure-integration-64}

Adobe Experience Manager(AEM)Assetsは、[!DNL Adobe I/O]を通じてBrand Portalと設定され、Brand Portalテナントの認証用のIMSトークンを取得します。

>[!NOTE]
>
>[!DNL Adobe I/O]を使用したBrand PortalとのAEM Assetsの設定は、AEM 6.4.8.0以降でサポートされています。
>
>これまで、Brand Portal は、旧来の OAuth ゲートウェイを通じてクラシック UI で設定されていました。このゲートウェイは、JWT トークン交換を使用して認証用の IMS アクセストークンを取得します。

>[!TIP]
>
>***既存のお客様のみ***
>
>既存のレガシー OAuth Gateway 設定を引き続き使用することをお勧めします。レガシーOAuth Gateway設定で問題が発生した場合は、既存の設定を削除し、[!DNL Adobe I/O]を介して新しい設定を作成します。

このヘルプでは、次の2つの使用例について説明します。

* [新しい設定](#configure-new-integration-64):新しいBrand Portalユーザーで、AEM AssetsオーサーインスタンスをBrand Portalと共に設定する場合は、で新しい設定を作成できま [!DNL Adobe I/O]す。
* [設定のアップグレード](#upgrade-integration-64):旧来のOAuth Gateway上でBrand Portalを使用してAEM Assetsオーサーインスタンスを設定している既存のBrand Portalユーザーの場合は、既存の設定を削除し、で新しい設定を作成することをお勧めし [!DNL Adobe I/O]ます。

具体的には、以下の操作に関する十分な知識があるユーザーを対象としています。

* Adobe Experience ManagerおよびAEMパッケージのインストール、設定および管理

* LinuxおよびMicrosoft Windowsオペレーティングシステムの使用

## 前提条件 {#prerequisites}

AEM Assets と Brand Portal の連携を設定するには以下が必要です。

* 最新のサービスパックを適用した実行中の AEM Assets オーサーインスタンス
* Brand Portal テナント URL
* Brand Portal テナントの IMS 組織に対するシステム管理者権限を持つユーザー

[AEM 6.4をダウンロードしてインストールする](#aemquickstart)

[最新の AEM サービスパックをダウンロードしてインストールする](#servicepack)

### AEM 6.4をダウンロードしてインストールする {#aemquickstart}

AEMオーサーインスタンスを設定するには、AEM 6.4を使用することをお勧めします。 AEM が稼働していない場合は、以下の場所から AEM をダウンロードしてください。

* 既にAEMをご利用のお客様の場合は、[AdobeライセンスWebサイト](http://licensing.adobe.com)からAEM 6.4をダウンロードしてください。

* Adobeパートナーの場合は、[Adobeパートナートレーニングプログラム](https://adobe.allegiancetech.com/cgi-bin/qwebcorporate.dll?idx=82357Q)を使用してAEM 6.4をリクエストします。

AEM をダウンロードしたら、「[デプロイメントと保守](https://helpx.adobe.com/jp/experience-manager/6-4/sites/deploying/using/deploy.html#defaultlocalinstall)」の説明に従い、AEM オーサーインスタンスの設定を行ってください。

### 最新の AEM サービスパックをダウンロードしてインストールする {#servicepack}

詳しい手順については、

* [AEM 6.4 Service Pack リリースノート](https://helpx.adobe.com/jp/experience-manager/6-4/release-notes/sp-release-notes.html)

**最新のAEMパッケ** ージまたはService Packが見つからない場合は、カスタマーケアにお問い合わせください。

## 設定の作成 {#configure-new-integration-64}

AEM AssetsとBrand Portalを初めて設定する場合は、以下の手順を順に実行します。

1. [公開証明書の取得](#public-certificate)
1. [ [!DNL Adobe I/O] 統合の作成](#createnewintegration)
1. [IMS アカウント設定の作成](#create-ims-account-configuration)
1. [Cloud Service の設定](#configure-the-cloud-service)
1. [設定のテスト](#test-integration)

>[!NOTE]
>
>AEM Assetsオーサーインスタンスは、1つのBrand Portalテナントでのみ設定できます。

### IMS 設定の作成 {#create-ims-configuration}

IMS 設定は、AEM Assets オーサーインスタンスを使用して Brand Portal テナントを認証します。

IMS 設定には、次の 2 つの手順が含まれます。

* [公開証明書の取得](#public-certificate)
* [IMS アカウント設定の作成](#create-ims-account-configuration)

### 公開証明書の取得 {#public-certificate}

公開証明書を使用すると、[!DNL Adobe I/O]でプロファイルを認証できます。

1. AEM Assetsオーサーインスタンスにログインします。
デフォルトURL:http:// localhost:4502/aem/start.html
1. **ツール** ![ツール](assets/tools.png)パネルから、**[!UICONTROL セキュリティ]** >> **[!UICONTROL AdobeIMS設定]**&#x200B;に移動します。

   ![Adobe IMS アカウント設定 UI](assets/ims-config1.png)

1. Adobe IMS 設定ページが開きます。

   「**[!UICONTROL 作成]**」をクリックします。

   これにより、**[!UICONTROL AdobeIMSテクニカルアカウント設定]**&#x200B;ページが表示されます。

1. デフォルトでは、「**証明書**」タブが開きます。

   **クラウドソリューション**&#x200B;で「**[!UICONTROL Adobe Brand Portal]**」を選択します。

1. 「**[!UICONTROL 新しい証明書を作成]**」チェックボックスをオンにし、証明書の&#x200B;**エイリアス**&#x200B;を指定します。 ここで入力したエイリアスが、ダイアログ名として表示されます。

1. 「**[!UICONTROL 証明書を作成]**」をクリックします。ダイアログが表示されます。「**[!UICONTROL OK]**」をクリックして公開証明書を生成します。

   ![証明書を作成](assets/ims-config2.png)

1. 「**[!UICONTROL 公開鍵をダウンロード]**」をクリックし、*AEM-Adobe-IMS.crt* 証明書ファイルをローカルマシンに保存します。証明書ファイルは、[ [!DNL Adobe I/O] 統合](#createnewintegration)の作成に使用されます。

   ![証明書をダウンロード](assets/ims-config3.png)

1. 「**[!UICONTROL 次へ]**」をクリックします。

   「**アカウント**」タブで、Adobe IMS アカウントを作成するには、統合環境の詳細が必要です。このページは開いたままにしておきます。

   新しいタブを開き、[ [!DNL Adobe I/O] 統合](#createnewintegration)を作成して、IMSアカウント設定の統合の詳細を取得します。

### [!DNL Adobe I/O]統合の作成 {#createnewintegration}

[!DNL Adobe I/O] 統合環境により、API キー、クライアント秘密鍵、および IMS アカウント設定の設定で必要なペイロード（JWT）が生成されます。

1. Brand PortalテナントのIMS組織のシステム管理者権限で[!DNL Adobe I/O]コンソールにログインします。

   デフォルト URL：[https://console.adobe.io/](https://console.adobe.io/)

1. 「**[!UICONTROL 統合を作成]**」をクリックします。

1. 「**[!UICONTROL API にアクセス]**」を選択し、「**[!UICONTROL 続行]**」をクリックします。

   ![新しい統合の作成](assets/create-new-integration1.png)

1. 新しい統合を作成ページを開きます。

   ドロップダウンリストからご自身の組織を選択します。

   **[!UICONTROL Experience Cloud]** で「**[!UICONTROL AEM Brand Portal]**」を選択し、「**[!UICONTROL 続行]**」をクリックします。

   「Brand Portal」オプションが無効になっている場合は、「**[!UICONTROL アドビのサービス]**」オプションの上にあるドロップダウンボックスで正しい組織が選択されているかどうかを確認してください。自分がどの組織に属しているかわからない場合は、管理者に問い合わせてください。

   ![統合の作成](assets/create-new-integration2.png)

1. 新しい統合環境の名前と説明を入力します。「**[!UICONTROL お使いのコンピューターからファイルを選択]**」をクリックし、「[公開証明書を取得する](#public-certificate)」セクションでダウンロードした `AEM-Adobe-IMS.crt` ファイルをアップロードします。

1. 組織のプロファイルを選択します。

   または、デフォルトのプロファイル **[!UICONTROL Assets Brand Portal]** を選択し、「**[!UICONTROL 統合を作成]**」をクリックします。統合環境が作成されます。

1. 「**[!UICONTROL 統合の詳細情報に進む]**」をクリックして、統合環境の詳細情報を表示します。

   **[!UICONTROL API キーのコピー]**

   「**[!UICONTROL クライアント秘密鍵を取得]**」をクリックし、クライアント秘密鍵をコピーします。

   ![統合環境の API キー、クライアント秘密鍵、ペイロード情報の表示画面](assets/create-new-integration3.png)

1. 「**[!UICONTROL JWT]**」タブに移動し、**[!UICONTROL JWT ペイロード]**&#x200B;をコピーします。

   API キー、クライアント秘密鍵、JWT ペイロード情報は、IMS アカウント設定の作成に使用されます。

### IMS アカウント設定の作成 {#create-ims-account-configuration}

次の手順を実行したことを確認します。

* [公開証明書の取得](#public-certificate)
* [ [!DNL Adobe I/O] 統合の作成](#createnewintegration)

**IMS アカウント設定の作成手順：**

1. IMS 設定ページの「**[!UICONTROL アカウント]**」タブを開きます。（このページは、「[公開証明書を取得する](#public-certificate)」セクションの最後で開いたままにしておいたページです）。

1. IMS アカウントの&#x200B;**[!UICONTROL タイトル]**&#x200B;を指定します。

   「**[!UICONTROL 認証サーバー]**」に次の URL を入力します。[https://ims-na1.adobelogin.com/](https://ims-na1.adobelogin.com/)

   [Create [!DNL Adobe I/O] integration](#createnewintegration)の最後にコピーしたAPIキー、クライアント秘密鍵、JWTペイロードを貼り付けます。

   「**[!UICONTROL 作成]**」をクリックします。

   統合環境が作成されます。

   ![IMS アカウントの設定](assets/create-new-integration6.png)

1. 作成した IMS 設定を選択して「**[!UICONTROL ヘルスチェック]**」をクリックします。ダイアログボックスが表示されます。

   「**[!UICONTROL チェック]**」をクリック。接続が成功すると、*トークンが正常に取得された*&#x200B;ことを示すメッセージが表示されます。

   ![](assets/create-new-integration5.png)

>[!CAUTION]
>
>IMS 設定は 1 つだけにする必要があります。複数の IMS 設定を作成しないでください。
>
>IMS 設定がヘルスチェックに合格していることを確認します。設定がヘルスチェックに合格しない場合は無効です。削除して、新しい有効な設定を作成する必要があります。

### Cloud Service の設定 {#configure-the-cloud-service}

Brand Portal クラウドサービス設定を作成するには、以下の手順を実行します。

1. AEM Assetsオーサーインスタンスにログインします。

   デフォルト URL は http://localhost:4502/aem/start.html です。
1. **ツール** ![ツール](assets/tools.png)パネルから、**[!UICONTROL Cloud Services/>AEM Brand Portal]**&#x200B;に移動します。

   Brand Portal 設定ページが開きます。

1. 「**[!UICONTROL 作成]**」をクリックします。

1. 設定の&#x200B;**[!UICONTROL タイトル]**&#x200B;を入力します。

   [IMS アカウント設定の作成](#create-ims-account-configuration)手順で作成した IMS 設定を選択します。

   「**[!UICONTROL サービス URL]**」に、Brand Portal テナント URL を入力します。

   ![](assets/create-cloud-service.png)

1. 「**[!UICONTROL 保存して閉じる]**」をクリックします。クラウド設定が作成されます。これで、AEM AssetsオーサーインスタンスがBrand Portalテナントと統合されました。

### 設定のテスト {#test-integration}

1. AEM Assetsオーサーインスタンスにログインします。

   デフォルト URL は http://localhost:4502/aem/start.html です。

1. **ツール** ![ツール](assets/tools.png)パネルから、**[!UICONTROL デプロイメント/>レプリケーション]**&#x200B;に移動します。

   ![](assets/test-integration1.png)

1. レプリケーションページが開きます。

   「**[!UICONTROL 作成者のエージェント]**」をクリックします。

   ![](assets/test-integration2.png)

1. 各テナントに対して4つのレプリケーションエージェントが作成されます。

   Brand Portalテナントのレプリケーションエージェントを見つけます。

   レプリケーションエージェントのURLをクリックします。

   ![](assets/test-integration3.png)


   >[!NOTE]
   >
   >レプリケーションエージェントは並行して動作し、ジョブの配布を均等に共有するので、公開速度は元の速度の4倍に増えます。 クラウドサービスを設定した後は、複数のアセットを並行して公開できるように、デフォルトで有効化されるレプリケーションエージェントを有効にするために追加の設定は必要ありません。

1. AEM AssetsオーサーとBrand Portalの間の接続を検証するには、「**[!UICONTROL 接続をテスト]**」をクリックします。

   ![](assets/test-integration4.png)

1. テスト結果の一番下を見て、レプリケーションが成功したことを確認します。

   ![](assets/test-integration5.png)


1. 4つのレプリケーションエージェントすべてでテスト結果を1つずつ確認します。

   >[!NOTE]
   >
   >どのレプリケーションエージェントも無効にしないでください。一部のアセットのレプリケーションが失敗する可能性があります。
   >
   >タイムアウトエラーを回避するために、4つのレプリケーションエージェントがすべて設定されていることを確認します。 [Brand Portal](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/publish/troubleshoot-parallel-publishing.html#connection-timeout)への並列公開における問題のトラブルシューティングを参照してください。

Brand PortalがAEM Assetsオーサーインスタンスで正常に設定されました。 次の操作が可能になっています。

* [AEM Assets から Brand Portal へのアセットの公開](../assets/brand-portal-publish-assets.md)
* [AEM Assets から Brand Portal へのフォルダーの公開](../assets/brand-portal-publish-folder.md)
* [AEM Assets から Brand Portal へのコレクションの公開](../assets/brand-portal-publish-collection.md)
* [Brand Portalユーザー](https://docs.adobe.com/content/help/ja/experience-manager-brand-portal/using/asset-sourcing-in-brand-portal/brand-portal-asset-sourcing.html) がAEM Assetsにアセットを投稿して公開できるようにする、アセットソースの設定。

## 設定のアップグレード {#upgrade-integration-64}

既存の設定をアップグレードするには、以下の手順を上記の手順で実行します。
1. [実行中のジョブの確認](#verify-jobs)
1. [既存の設定の削除](#delete-existing-configuration)
1. [設定の作成](#configure-new-integration-64)

### 実行中のジョブの確認 {#verify-jobs}

変更を加える前に、AEM Assetsオーサーインスタンスで公開ジョブが実行されていないことを確認してください。 そのために、4つのレプリケーションエージェントをすべて検証し、キューが理想的/空であることを確認できます。

1. AEM Assetsオーサーインスタンスにログインします。

   デフォルト URL は http://localhost:4502/aem/start.html です。

1. **ツール** ![ツール](assets/tools.png)パネルから、**[!UICONTROL デプロイメント/>レプリケーション]**&#x200B;に移動します。

1. レプリケーションページが開きます。

   「**[!UICONTROL 作成者のエージェント]**」をクリックします。

   ![](assets/test-integration2.png)

1. Brand Portalテナントのレプリケーションエージェントを見つけます。

   すべてのレプリケーションエージェントに対して&#x200B;**QueueがIdle**&#x200B;であることを確認します。公開ジョブがアクティブでないことを確認します。

   ![](assets/test-integration3.png)

### 既存の設定の削除 {#delete-existing-configuration}

既存の設定を削除する際に、次のチェックリストを実行する必要があります。
* 4つのレプリケーションエージェントをすべて削除する
* クラウドサービスの削除
* MACユーザーの削除

次の手順を実行して、既存の設定を削除します。

1. AEM Assetsオーサーインスタンスにログインし、管理者としてCRX Liteを開きます。

   デフォルトURL:http:// localhost:4502/crx/de/index.jsp

1. `/etc/replications/agents.author`に移動し、Brand Portalテナントの4つのレプリケーションエージェントをすべて削除します。

   ![](assets/delete-replication-agent.png)

1. `/etc/cloudservices/mediaportal`に移動し、**Cloud Service設定**&#x200B;を削除します。

   ![](assets/delete-cloud-service.png)

1. `/home/users/mac`に移動し、Brand Portalテナントの&#x200B;**MACユーザー**&#x200B;を削除します。

   ![](assets/delete-mac-user.png)


これで、[!DNL Adobe I/O]上のAEM 6.4オーサーインスタンスに[設定](#configure-new-integration-64)を作成できます。



<!--
   Comment Type: draft

   <li> </li>
   -->

<!--
   Comment Type: draft

   <li>Step text</li>
   -->

レプリケーションが正常に終了したら、アセット、フォルダー、コレクションを Brand Portal に公開することができます。詳しくは、次を参照してください。

* [Brand Portal へのアセットの公開](brand-portal-publish-assets.md)
* [アセットおよびフォルダーの Brand Portal への公開](brand-portal-publish-folder.md)
* [Brand Portal へのコレクションの公開](brand-portal-publish-collection.md)
