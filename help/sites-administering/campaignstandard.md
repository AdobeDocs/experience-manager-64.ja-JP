---
title: Adobe Campaign Standard との統合
seo-title: Integrating with Adobe Campaign Standard
description: Adobe Campaign Standard との統合。
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
ht-degree: 71%

---

# Adobe Campaign Standard との統合{#integrating-with-adobe-campaign-standard}

>[!NOTE]
>
>このドキュメントでは、AEM をサブスクリプションベースのソリューション、Adobe Campaign Standard と統合する方法について説明します。Adobe Campaign 6.1 を使用している場合、手順については [Adobe Campaign 6.1 との統合](/help/sites-administering/campaignonpremise.md)を参照してください。

Adobe Campaign を使用すると、電子メール配信コンテンツおよびフォームを Adobe Experience Manager で直接管理できます。

両方のソリューションを同時に使用するには、最初に互いの接続を設定する必要があります。これには、Adobe Campaign と Adobe Experience Manager の両方での設定手順が含まれます。これらの手順は、このドキュメントで詳しく説明します。

AEM での Adobe Campaign の操作には、Adobe Campaign を使用して電子メールおよびフォームを送信する機能が含まれています。これについては、[Adobe Campaign の操作](/help/sites-authoring/campaign.md)で説明します。

さらに、AEM を [Adobe Campaign](https://docs.campaign.adobe.com/doc/standard/en/home.html) と統合する際に参考となるトピックを次に示します。

* [電子メールテンプレートのベストプラクティス](/help/sites-administering/best-practices-for-email-templates.md)
* [Adobe Campaign 統合に関するトラブルシューティング](/help/sites-administering/troubleshooting-campaignintegration.md)

Adobe Campaign との統合を拡張する場合は、次のページが参考になります。

* [カスタム拡張の作成](/help/sites-developing/extending-campaign-extensions.md)
* [カスタムフォームマッピングの作成](/help/sites-developing/extending-campaign-form-mapping.md)

## Adobe Campaign の設定 {#configuring-adobe-campaign}

Adobe Campaign の設定には、次が含まれます。

1. **aemserver** ユーザーの設定。
1. 専用の外部アカウントの作成。
1. AEMResourceTypeFilter オプションの検証。
1. 専用の配信テンプレートの作成。

>[!NOTE]
>
>これらの操作を実行するには、 **管理** Adobe Campaignでの役割

### 前提条件 {#prerequisites}

事前に、次の要素があることを確認してください。

* [AEM 作成者インスタンス](/help/sites-deploying/deploy.md#getting-started)
* [AEM 発行インスタンス](/help/sites-deploying/deploy.md#author-and-publish-installs)
* [Adobe Campaign インスタンス](https://docs.adobe.com/content/docs/en/campaign/ACS.html)

>[!CAUTION]
>
>操作の詳細については、 [Adobe Campaignの設定](#configuring-adobe-campaign) および [Adobe Experience Managerの設定](#configuring-adobe-experience-manager) 「 」セクションは、AEMとAdobe Campaignの間の統合機能が正しく動作するために必要です。

### aemserver ユーザーの設定 {#configuring-the-aemserver-user}

この **aemserver** ユーザーは、Adobe Campaignで設定する必要があります。 この **aemserver** は、AEMサーバーをAdobe Campaignに接続する際に使用する技術ユーザーです。

に移動します。 **管理** >  **ユーザーとセキュリティ** >  **ユーザー**&#x200B;をクリックし、 **aemserver** ユーザー。 クリックしてユーザー設定を開きます。

* このユーザーにパスワードを設定する必要があります。これは UI では実行できません。技術管理者が REST で設定する必要があります。
* **deliveryPrepare** など、特定の役割をこのユーザーに割り当てることができます。これにより、ユーザーは配信を作成および編集できます。

### Adobe Experience Manager 外部アカウントの設定 {#configuring-an-adobe-experience-manager-external-account}

Adobe Campaign を AEM インスタンスに接続可能な外部アカウントを設定する必要があります。

>[!NOTE]
>
>AEM で、campaign-remote ユーザーのパスワードを設定してください。AEM で Adobe Campaign に接続するにはこのパスワードを設定する必要があります。管理者としてログインし、ユーザー管理コンソールで campaign-remote ユーザーを探して「**パスワードを設定**」をクリックします。

AEM 外部アカウントを設定するには：

1. に移動します。 **管理** > **アプリケーション設定** > **外部アカウント**.

   ![chlimage_1-124](assets/chlimage_1-124.png)

1. デフォルトを選択 **aemInstance** 外部アカウントを作成するか、 **作成** 」ボタンをクリックします。
1. 選択 **Adobe Experience Manager** i **タイプ** フィールドに入力し、AEMオーサリングインスタンスに使用するアクセスパラメーターを入力します。サーバーアドレス、アカウント名およびパスワード。

   >[!NOTE]
   >
   >URL の末尾に **/**（スラッシュ）を追加しないようにします。追加した場合、接続が機能しなくなります。

1. 必ず **有効** 「 」チェックボックスがオンの場合、「 」をクリックします。 **保存** をクリックして変更を保存します。

### AEMResourceTypeFilter オプションの検証 {#verifying-the-aemresourcetypefilter-option}

この **AEMResourceTypeFilter** オプションは、Adobe Campaignで使用できるAEMリソースのタイプをフィルタリングするために使用します。 これにより、Adobe Campaign でのみ使用されるように特別に設計された AEM コンテンツを Adobe Campaign で取得できます。

このオプションは事前設定済みです。ただし、このオプションを変更すると、統合が機能しなくなる可能性があります。

**AEMResourceTypeFilter** オプションが設定されていることを検証するには：

1. **管理**／**（アプリケーション設定**／**オプション**&#x200B;に移動します。
1. リストで、 **AEMResourceTypeFilter** 」オプションが表示され、パスが正しいことを示します。

### AEM 専用の電子メール配信テンプレートの作成 {#creating-an-aem-specific-email-delivery-template}

デフォルトでは、AEM 機能は、Adobe Campaign の電子メールテンプレートでは有効になっていません。AEM コンテンツで電子メールを作成するために使用される新しい電子メール配信テンプレートを設定できます。

AEM 専用の電子メール配信テンプレートを作成するには：

1. **リソース**／**テンプレート**／**配信テンプレート**&#x200B;に移動します。
1. **選択を有効にする** アクションバーのチェックマークをクリックし、既存の **標準メール（メール）** デフォルトのテンプレートを作成し、 **コピー** アイコンとクリック **確認**.
1. 選択モードを無効にするには、 **x** 新しく作成した **標準メールのコピー（メール）** テンプレートを選択し、「 **プロパティを編集** をクリックします。

   テンプレートの&#x200B;**ラベル**&#x200B;を変更できます。

1. プロパティの「**コンテンツ**」セクションで、「**コンテンツソース**」を「**Adobe Experience Manager**」に変更します。次に、以前作成した外部アカウントを選択して、「**Confirm（確認）**」をクリックします。

   「**確認**」をクリックし、「**保存**」をクリックして、変更を保存します。

   このテンプレートから作成した電子メール配信は、AEM コンテンツ機能が有効になっています。

   ![chlimage_1-125](assets/chlimage_1-125.png)

## Adobe Experience Manager の設定 {#configuring-adobe-experience-manager}

AEM を設定するには、次の手順を実行する必要があります。

* インスタンス間のレプリケーションを設定します。
* AEM から Adobe Campaign に接続します。
* Externalizer を設定します。

### AEM インスタンス間のレプリケーションの設定 {#configuring-replication-between-aem-instances}

AEM オーサーインスタンスから作成されたコンテンツは、最初にパブリッシュインスタンスに送信されます。このパブリッシュインスタンスは、次にコンテンツを Adobe Campaign に転送します。レプリケーションエージェントは、その結果として、AEM オーサーインスタンスから AEM パブリッシュインスタンスにレプリケートするように設定される必要があります。

>[!NOTE]
>
>レプリケーション URL を使用しない代わりに公開 URL を使用したい場合は、OSGi（**ツール**／**Web コンソール**／**OSGi Configuration／AEM Campaign Integration - Configuration**）で次の設定をおこなうことで&#x200B;**パブリック URL** を設定できます。
**パブリック URL :** com.day.cq.mcm.campaign.impl.IntegrationConfigImpl#aem.mcm.campaign.publicUrl

また、この手順は、あるオーサーインスタンス設定をパブリッシュインスタンスにレプリケートするためにも必要です。

AEM インスタンス間のレプリケーションを設定するには：

1. オーサーインスタンスから、 **AEMロゴ**/ **ツール**アイコン > **導入** > **レプリケーション** > **作成者のエージェント**&#x200B;を選択し、「 **デフォルトエージェント**.

   ![chlimage_1-126](assets/chlimage_1-126.png)

   >[!NOTE]
   パブリッシュおよびオーサーインスタンスが両方とも同じコンピューターにある場合を除いて、Adobe Campaign との統合を設定する際に、localhost（これは、AEM のローカルコピーです）を使用するのを回避します。

1. クリック **編集** 次に、 **輸送** タブをクリックします。
1. **localhost** を IP アドレスまたは AEM パブリッシュインスタンスのアドレスに置き換えることで、URI を設定します。

   ![chlimage_1-127](assets/chlimage_1-127.png)

### AEM から Adobe Campaign への接続 {#connecting-aem-to-adobe-campaign}

AEM と Adobe Campaign を一緒に使用する前に、両方のソリューション間のリンクを確立して、通信できるようにする必要があります。

1. AEM オーサーインスタンスに接続します。
1. 選択 **ツール** > **運用** > **クラウド** > **Cloud Services**&#x200B;を、 **今すぐ設定** (「 Adobe Campaign 」セクション内 )

   ![chlimage_1-128](assets/chlimage_1-128.png)

1. 新しい設定を作成するには、 **タイトル** をクリックし、 **作成**&#x200B;または、Adobe Campaignインスタンスにリンクする既存の設定を選択します。
1. 設定を編集して、Adobe Campaign インスタンスのパラメーターと一致するようにします。

   * **ユーザー名**: **aemserver**:2 つのソリューション間のリンクを確立するために使用されるAdobe Campaign AEM Integration package 演算子です。
   * **パスワード**：Adobe Campaign aemserver 演算子のパスワード。この演算子のパスワードを Adobe Campaign で直接再指定する必要があることがあります。
   * **API エンドポイント**：Adobe Campaign インスタンス URL。

1. 選択 **Adobe Campaignに接続** をクリックし、 **OK**.

   ![chlimage_1-129](assets/chlimage_1-129.png)

   >[!NOTE]
   [電子メールを作成して公開](/help/sites-authoring/campaign.md)したら、パブリッシュインスタンスに設定を再公開する必要があります。

   ![chlimage_1-130](assets/chlimage_1-130.png)

>[!NOTE]
接続に失敗する場合は、次を確認してください。
* Adobe Campaign インスタンスへのセキュリティで保護された接続（https）を使用する際、証明書の問題が発生する可能性があります。JDK の**cacerts **ファイルにAdobe Campaignインスタンス証明書を追加する必要があります。
* また、[AEM／Adobe Campaign 統合のトラブルシューティング](/help/sites-administering/troubleshooting-campaignintegration.md)も参照してください。


### Externalizer の設定 {#configuring-the-externalizer}

オーサーインスタンスの AEM に [Externalizer を設定](/help/sites-developing/externalizer.md)する必要があります。Externalizer は、リソースパスを外部 URL および絶対 URL に変換できる OSGi サービスです。このサービスは、これらの外部 URL を設定および構築するための一元化された場所を提供します。

一般的な指示については、[Externalizer の設定](/help/sites-developing/externalizer.md)を参照してください。Adobe Campaign統合の場合、次の場所でパブリッシュサーバーを設定していることを確認します。 `https://<host>:<port>/system/console/configMgr/com.day.cq.commons.impl.ExternalizerImpl` 指していない `localhost:4503` Adobe Campaignコンソールから到達可能なサーバーに送信する必要があります。

`localhost:4503` または Adobe Campaign が到達できない別のサーバーを指している場合、Adobe Campaign コンソールに画像が表示されません。

![chlimage_1-131](assets/chlimage_1-131.png)
