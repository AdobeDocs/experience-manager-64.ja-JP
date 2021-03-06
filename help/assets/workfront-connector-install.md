---
title: ' [!DNL Workfront for Experience Manager enhanced connector] のインストール'
description: ' [!DNL Workfront for Experience Manager enhanced connector] のインストール'
role: Admin
feature: Integrations
exl-id: 967391db-e7ba-4cf8-af9e-28c28d2d96d5
source-git-commit: 6f9a682f441c1087558f86da65e092e549f75a17
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# [!DNL Workfront for Experience Manager enhanced connector] のインストール  {#assets-integration-overview}

[!DNL Adobe Experience Manager] の管理者アクセス権を持つユーザーが拡張コネクタをインストールします。 インストールする前に、プラットフォームのサポートとその他の[コネクタの前提条件](https://one.workfront.com/s/csh?context=2467&amp;pubname=the-new-workfront-experience)を確認してください。

>[!TIP]
>
>次を検索していますか： [!DNL Workfront for Experience Manager enhanced connector] AEMas a Cloud Serviceのドキュメント クリック [ここ](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/integrations/workfront-connector-install.html?lang=en).

>[!IMPORTANT]
>
>* Adobeは、認定パートナーまたは [!DNL Adobe Professional Services] を介してのみ [!DNL Adobe Workfront for Experience Manager enhanced connector] のデプロイメントと構成を必要とします。認定パートナーなしでデプロイおよび設定した場合、または [!DNL Adobe Professional Services]の場合、Adobe ではサポートされません。
>
>* アドビは、このコネクターを冗長にする[!DNL Adobe Workfront]および [!DNL Adobe Experience Manager] の更新をリリースする可能性があります。この場合、お客様はこのコネクターの使用から移行する必要が生じることがあります。
>
>* Adobeは、拡張コネクタバージョン 1.7.4 以降をサポートしています。 以前のプレリリースおよびカスタムバージョンはサポートされていません。 拡張コネクタのバージョンを確認するには、 `digital.hoodoo` の左側のペインで使用可能なグループ [パッケージマネージャー](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=ja).
>
>* 詳しくは、[Workfront for Experience Manager Assets 拡張コネクタに関するパートナー認定試験](https://solutionpartners.adobe.com/solution-partners/home/applications/experience_cloud/workfront/journey/dev_core.html)を参照してください。試験について詳しくは、 [試験ガイド](https://express.adobe.com/page/Tc7Mq6zLbPFy8/).


コネクタをインストールするには、次の手順に従います。

1. [[!DNL Software Distribution] リンク](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/product/assets/workfront-tools.ui.apps.zip)からコネクタをダウンロードします。

1. [ファイアウォールを設定します](https://one.workfront.com/s/document-item?bundleId=the-new-workfront-experience&amp;topicId=Content%2FAdministration_and_Setup%2FGet_started-WF_administration%2Fconfigure-your-firewall.html)。

1. Dispatcher で、 `authorization`、`username` および `apikey` という HTTP ヘッダーを許可します。 `/bin/workfront-tools` への `GET`、`POST` および `PUT` リクエストを許可します。

1. [!DNL Experience Manager] リポジトリに次のパスが存在しないことを確認します。

   * `/apps/dam/gui/coral/components/admin/schemaforms/formbuilder`
   * `/apps/dam/gui/coral/components/admin/folderschemaforms/formbuilder`
   * `/apps/dam/gui/content/foldermetadataschemaeditor`
   * `/apps/dam/cfm/models/editor/components/datatypeproperties`
   * `/apps/settings/dam/cfm/models/formbuilderconfig`

1. [!UICONTROL パッケージマネージャー]を使ってパッケージをインストールします。パッケージのインストール方法については、[パッケージマネージャーのドキュメント](/help/sites-administering/package-manager.md)を参照してください。

1. [!DNL Experience Manager] ユーザーグループに `wf-workfront-users` を作成し、`jcr:all` 権限を `/content/dam` に割り当てます。

システムユーザー `workfront-tools` が自動的に作成され、必須の権限が自動的に管理されます。 このコネクタを使用するすべての [!DNL Workfront] ユーザーが、このグループの一部として自動的に追加されます。

## [!DNL Experience Manager] と [!DNL Workfront] との接続の設定 {#configure-connection}

Workfront との接続を作成するには、次の手順に従います。

1. [!DNL Experience Manager] で、 **[!UICONTROL ツール]**／**[!UICONTROL クラウドサービス]**／**[!UICONTROL Workfront ツール設定]**&#x200B;を選択します。

1. 左パネルで `workfront-tools` を選択し、ページの右上の領域にある「**[!UICONTROL 作成]** 」オプションを選択します。

1. **[!UICONTROL Workfront 接続]**&#x200B;ダイアログで、[!DNL Workfront] デプロイメントの必須の詳細事項を入力して、「**[!UICONTROL Workfront に接続]**」オプションを選択します。正常に接続されると、[!DNL Workfront] ドキュメントのカスタム統合が [!DNL Workfront] 環境に自動的に作成されます。

   ![接続：[!DNL Experience Manager] と [!DNL Workfront]](/help/assets/assets/wf-connection-config.png)

1. 接続を確認するには、[!DNL Workfront] でアクセスして、API キーが同じで接続が&#x200B;**[!UICONTROL 有効]**&#x200B;であることを確認します。それには、[!DNL Workfront] で **[!UICONTROL 設定]**／**[!UICONTROL ドキュメント]**／**[!UICONTROL カスタム統合]**&#x200B;を選択します。

## 更新 [!DNL Workfront for Experience Manager enhanced connector] {#update-enhanced-connector-for-workfront}

Experience Manager Assetsでは、 [!DNL Workfront for Experience Manager enhanced connector] 以前のバージョンから最新のバージョンに移行する場合。

次の手順で [!DNL Workfront for Experience Manager enhanced connector] を最新バージョンに変更するには：

1. 拡張コネクタの最新バージョンをからダウンロードします。 [[!DNL Software Distribution] リンク](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/product/assets/workfront-tools.ui.apps.zip).

1. [!UICONTROL パッケージマネージャー]を使ってパッケージをインストールします。パッケージのインストール方法については、[パッケージマネージャーのドキュメント](/help/sites-administering/package-manager.md)を参照してください。
