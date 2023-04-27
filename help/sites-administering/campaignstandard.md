---
title: Adobe Campaign Standard との統合
seo-title: Integrating with Adobe Campaign Standard
description: Adobe Campaign Standard との統合.
seo-description: Integrating with Adobe Campaign Standard.
uuid: ef31339e-d925-499c-b8fb-c00ad01e38ad
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: integration
content-type: reference
discoiquuid: 5c0fec99-7b1e-45d6-a115-e498d288e9e1
exl-id: d8d62c2f-3aa5-4fc9-8f42-86d75b6558ce
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '1313'
ht-degree: 53%

---

# Adobe Campaign Standard との統合{#integrating-with-adobe-campaign-standard}

>[!NOTE]
>
>このドキュメントでは、AEMをサブスクリプションベースのソリューションであるAdobe Campaign Standardと統合する方法について説明します。 Adobe Campaign 6.1 を使用している場合は、 [Adobe Campaign 6.1 との統合](/help/sites-administering/campaignonpremise.md) を参照してください。

Adobe Campaignを使用すると、E メール配信コンテンツやフォームをAdobe Experience Managerで直接管理できます。

両方のソリューションを同時に使用するには、まず、相互に接続するように設定する必要があります。 これには、Adobe CampaignとAdobe Experience Managerの両方の設定手順が含まれます。 これらの手順については、このドキュメントで詳しく説明します。

AEM での Adobe Campaign の操作には、Adobe Campaign を使用してメールおよびフォームを送信する機能が含まれています。これについては、[Adobe Campaign の操作](/help/sites-authoring/campaign.md)で説明します。

さらに、AEM を [Adobe Campaign](https://docs.campaign.adobe.com/doc/standard/en/home.html) と統合する際に参考となるトピックを以下に示します。

* [メールテンプレートのベストプラクティス](/help/sites-administering/best-practices-for-email-templates.md)
* [Adobe Campaign 統合に関するトラブルシューティング](/help/sites-administering/troubleshooting-campaignintegration.md)

Adobe Campaign との統合を拡張する場合は、以下のページが参考になります。

* [カスタム拡張の作成](/help/sites-developing/extending-campaign-extensions.md)
* [カスタムフォームマッピングの作成](/help/sites-developing/extending-campaign-form-mapping.md)

## Adobe Campaignの設定 {#configuring-adobe-campaign}

Adobe Campaignの設定には、次のものが含まれます。

1. の設定 **aemserver** ユーザー。
1. 専用の外部アカウントを作成します。
1. AEMResourceTypeFilter オプションの検証.
1. 専用の配信テンプレートの作成。

>[!NOTE]
>
>これらの操作を実行するには、Adobe Campaign の&#x200B;**管理**&#x200B;の役割を有している必要があります。

### 前提条件 {#prerequisites}

事前に次の要素を用意しておいてください。

* [AEM 作成者インスタンス](/help/sites-deploying/deploy.md#getting-started)
* [AEM パブリッシングインスタンス](/help/sites-deploying/deploy.md#author-and-publish-installs)
* [Adobe Campaign インスタンス](https://docs.adobe.com/content/docs/en/campaign/ACS.html)

>[!CAUTION]
>
>[Adobe Campaign の設定](#configuring-adobe-campaign)および [Adobe Experience Manager の設定](#configuring-adobe-experience-manager)で詳述した操作は、AEM と Adobe Campaign の間の統合機能が正しく動作するために必要です。

### aemserver ユーザーの設定 {#configuring-the-aemserver-user}

Adobe Campaign では、**aemserver** ユーザーを設定する必要があります。**aemserver** は、AEM サーバーを Adobe Campaign に接続するために使用されるテクニカルユーザーです。

**管理**／**ユーザーとセキュリティ**／**ユーザー**&#x200B;に移動し、**aemserver** ユーザーを選択します。クリックして、ユーザー設定を開きます。

* このユーザーのパスワードを設定する必要があります。 これは、UI では実行できません。 この設定は、技術管理者が REST でおこなう必要があります。
* **deliveryPrepare** など、特定の役割をこのユーザーに割り当てることができます。これにより、ユーザーは配信を作成および編集できます。

### Adobe Experience Manager外部アカウントの設定 {#configuring-an-adobe-experience-manager-external-account}

Adobe CampaignをAEMインスタンスに接続できる外部アカウントを設定する必要があります。

>[!NOTE]
>
>AEMで、campaign-remote ユーザーのパスワードを必ず設定してください。 Adobe CampaignとAEMを接続するには、このパスワードを設定する必要があります。 管理者としてログインし、ユーザー管理コンソールで campaign-remote ユーザーを検索して、 **パスワードを設定**.

AEM 外部アカウントを設定するには：

1. **管理**／**アプリケーション設定**／**外部アカウント**&#x200B;に移動します。

   ![chlimage_1-124](assets/chlimage_1-124.png)

1. デフォルトの **aemInstance** 外部アカウントを選択するか、「**作成**」ボタンをクリックして新しく作成します。
1. 「**タイプ**」フィールドで「**Adobe Experience Manager**」を選択し、AEM オーサリングインスタンスで使用するアクセスパラメーター（サーバーアドレス、アカウント名およびパスワード）を入力します。

   >[!NOTE]
   >
   >URL の末尾への **/** スラッシュの追加は必ず避けてください。追加した場合、接続が機能しなくなります。

1. 「**有効**」チェックボックスが選択されていることを確認したら、「**保存**」をクリックして変更を保存します。

### AEMResourceTypeFilter オプションの検証 {#verifying-the-aemresourcetypefilter-option}

「**AEMResourceTypeFilter**」オプションを使用すると、Adobe Campaign で使用できる AEM リソースのタイプをフィルタリングできます。これにより、Adobe Campaignは、Adobe Campaignでのみ使用するように特別に設計されたAEMコンテンツを取得できます。

このオプションは事前設定済みです。ただし、このオプションを変更すると、統合が機能しなくなる場合があります。

**AEMResourceTypeFilter** オプションが設定されていることを検証するには、以下の手順に従います。

1. **管理**／**アプリケーション設定**／**オプション** に移動します。
1. リストで、「**AEMResourceTypeFilter**」オプションがあり、パスが正しいことを確認します。

### AEM固有の E メール配信テンプレートの作成 {#creating-an-aem-specific-email-delivery-template}

デフォルトでは、Adobe Campaignの電子メールテンプレートでAEM機能は有効になっていません。 AEMコンテンツを含む E メールの作成に使用する新しい E メール配信テンプレートを設定できます。

AEM固有の E メール配信テンプレートを作成するには：

1. に移動します。 **リソース** > **テンプレート** > **配信テンプレート**.
1. **選択を有効**&#x200B;にするには、アクションバーでチェックマークをクリックして既存の「**標準メール**」デフォルトテンプレートを選択し、「**コピー**」アイコンをクリックしてテンプレートを複製し、「**確認**」をクリックします。
1. **x** をクリックして選択モードを無効化し、新規作成した「**標準メールのコピー**」テンプレートを開いて、テンプレートダッシュボードのアクションバーから「**プロパティを編集**」を選択します。

   テンプレートの **ラベル** を変更できます。

1. プロパティ内 **コンテンツ** セクションで、 **コンテンツソース** から **Adobe Experience Manager**. 次に、以前に作成した外部アカウントを選択し、「 **確認**.

   **確認** をクリックし、**保存**&#x200B;クリックして、変更を保存します。

   このテンプレートから作成したメール配信は、AEM コンテンツ機能が有効になっています。

   ![chlimage_1-125](assets/chlimage_1-125.png)

## Adobe Experience Managerの設定 {#configuring-adobe-experience-manager}

AEMを設定するには、次の手順を実行する必要があります。

* インスタンス間のレプリケーションを設定します。
* AEMをAdobe Campaignに接続します。
* Externalizer を設定します。

### AEMインスタンス間のレプリケーションの設定 {#configuring-replication-between-aem-instances}

AEMオーサリングインスタンスから作成されたコンテンツは、最初にパブリッシュインスタンスに送信されます。 その後、このパブリッシュインスタンスはコンテンツをAdobe Campaignに転送します。 そのため、AEMオーサリングインスタンスからAEMパブリッシュインスタンスにレプリケートするようにレプリケーションエージェントを設定する必要があります。

>[!NOTE]
>
>レプリケーション URL を使用せずに、公開 URL を使用する場合は、 **パブリック URL** OSGi の次の設定 (**ツール** > **Web コンソール** > **OSGi 設定/AEM Campaign 統合 — 設定**):
**公開 URL：** com.day.cq.mcm.campaign.impl.IntegrationConfigImpl#aem.mcm.campaign.publicUrl

また、この手順は、あるオーサーインスタンス設定をパブリッシュインスタンスにレプリケートするためにも必要です。

AEMインスタンス間のレプリケーションを設定するには：

1. オーサーインスタンスから、 **AEMロゴ**/ **ツール**アイコン > **導入** > **レプリケーション** > **作成者のエージェント**&#x200B;を選択し、「 **デフォルトエージェント**.

   ![chlimage_1-126](assets/chlimage_1-126.png)

   >[!NOTE]
   パブリッシュおよびオーサーインスタンスが両方とも同じコンピューターにない場合は、Adobe Campaign との統合を設定する際に、localhost（すなわち AEM のローカルコピー）を使用しないでください。

1. 「**編集**」をクリックして、「**トランスポート**」タブを選択します。
1. **localhost** を IP アドレスまたは AEM パブリッシュインスタンスのアドレスに置き換えることで、URI を設定します。

   ![chlimage_1-127](assets/chlimage_1-127.png)

### AEMとAdobe Campaignの接続 {#connecting-aem-to-adobe-campaign}

AEMとAdobe Campaignを一緒に使用する前に、両方のソリューションが通信できるように両方のソリューション間のリンクを確立する必要があります。

1. AEMオーサリングインスタンスに接続します。
1. **ツール**／**操作**／**クラウド**／**クラウドサービス**&#x200B;を選択して、Adobe Campaign セクションの「**今すぐ設定**」を選択します。

   ![chlimage_1-128](assets/chlimage_1-128.png)

1. 「**タイトル**」にタイトルを入力して「**作成**」をクリックするか、Adobe Campaign インスタンスとリンクしたい既存の設定を選択することで、新しい設定を作成します。
1. 設定を編集して、Adobe Campaign インスタンスのパラメーターと一致するようにします。

   * **ユーザー名**：**aemserver**（2 つのソリューション間のリンクを確立するために使用される Adobe Campaign AEM 統合パッケージ演算子）。
   * **パスワード**:Adobe Campaign aemserver オペレーターのパスワード。 このオペレーターのパスワードをAdobe Campaignで直接再指定する必要がある場合があります。
   * **API エンドポイント**:Adobe Campaignインスタンス URL。

1. 「**Adobe Campaign に接続**」を選択し、「**OK**」をクリックします。

   ![chlimage_1-129](assets/chlimage_1-129.png)

   >[!NOTE]
   [メールを作成して公開](/help/sites-authoring/campaign.md)したら、パブリッシュインスタンスに設定を再公開する必要があります。

   ![chlimage_1-130](assets/chlimage_1-130.png)

>[!NOTE]
接続に失敗した場合は、次の点を確認してください。
* Adobe Campaignインスタンス (https) へのセキュア接続を使用する際、証明書の問題が発生する場合があります。 Adobe Campaign インスタンス証明書を JDK の cacerts ファイルに追加する必要があります。
* また、 [AEM/Adobe Campaign統合のトラブルシューティング](/help/sites-administering/troubleshooting-campaignintegration.md).
>


### Externalizer の設定 {#configuring-the-externalizer}

以下が必要です。 [externalizer を設定する](/help/sites-developing/externalizer.md) ( オーサーインスタンス上のAEMで )。 Externalizer は、リソースパスを外部 URL および絶対 URL に変換できる OSGi サービスです。 このサービスは、これらの外部 URL を設定して構築するための一元的な場所を提供します。

一般的な説明については、[Externalizer の設定](/help/sites-developing/externalizer.md)を参照してください。Adobe Campaignとの統合では、`https://<host>:<port>/system/console/configMgr/com.day.cq.commons.impl.ExternalizerImpl` のパブリッシュサーバーが `localhost:4503` を指すのではなく、Adobe Campaign コンソールから到達可能なサーバーに必ず設定してください。

`localhost:4503` または Adobe Campaign が到達できない別のサーバーを指している場合、Adobe Campaign コンソールに画像が表示されません。

![chlimage_1-131](assets/chlimage_1-131.png)
