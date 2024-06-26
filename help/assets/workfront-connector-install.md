---
title: ' [!DNL Workfront for Experience Manager enhanced connector] のインストール'
description: ' [!DNL Workfront for Experience Manager enhanced connector] のインストール'
role: Admin
feature: Integrations
exl-id: 967391db-e7ba-4cf8-af9e-28c28d2d96d5
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '526'
ht-degree: 94%

---

# [!DNL Workfront for Experience Manager enhanced connector] のインストール  {#assets-integration-overview}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

[!DNL Adobe Experience Manager] の管理者アクセス権を持つユーザーが拡張コネクタをインストールします。インストールする前に、プラットフォームのサポートとその他の[コネクタの前提条件](https://one.workfront.com/s/csh?context=2467&amp;pubname=the-new-workfront-experience)を確認してください。

>[!TIP]
>
>AEM as a Cloud Service の [!DNL Workfront for Experience Manager enhanced connector] ドキュメントを探している場合は、[ここ](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/integrations/workfront-connector-install.html?lang=ja)をクリックしてください。

>[!IMPORTANT]
>
>* Adobeは、認定パートナーまたは [!DNL Adobe Professional Services] を介してのみ [!DNL Adobe Workfront for Experience Manager enhanced connector] のデプロイメントと構成を必要とします。認定パートナーなしでデプロイおよび設定した場合、または [!DNL Adobe Professional Services]の場合、Adobe ではサポートされません。
>
>* アドビは、このコネクターを冗長にする[!DNL Adobe Workfront]および [!DNL Adobe Experience Manager] の更新をリリースする可能性があります。この場合、お客様はこのコネクターの使用から移行する必要が生じることがあります。
>
>* アドビでは、拡張コネクタバージョン 1.7.4 以降をサポートしています。以前のプレリリースバージョンやカスタムバージョンはサポートされていません。拡張コネクタのバージョンを確認するには、[パッケージマネージャー](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=ja)の左側のパネルで使用可能な `digital.hoodoo` グループに移動します。
>
>* 詳しくは、[Workfront for Experience Manager Assets 拡張コネクタに関するパートナー認定試験](https://solutionpartners.adobe.com/solution-partners/home/applications/experience_cloud/workfront/journey/dev_core.html)を参照してください。試験について詳しくは、[試験ガイド](https://express.adobe.com/page/Tc7Mq6zLbPFy8/)を参照してください。


コネクタをインストールするには、次の手順に従います。

1. [[!DNL Software Distribution] リンク](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/product/assets/workfront-tools.ui.apps.zip)からコネクタをダウンロードします。

1. [ファイアウォールを設定します](https://one.workfront.com/s/document-item?bundleId=the-new-workfront-experience&amp;topicId=Content%2FAdministration_and_Setup%2FGet_started-WF_administration%2Fconfigure-your-firewall.html)。

1. Dispatcher で、`authorization`、`username` および `apikey` という HTTP ヘッダーを許可します。`/bin/workfront-tools` への `GET`、`POST` および `PUT` リクエストを許可します。

1. [!DNL Experience Manager] リポジトリに次のパスが存在しないことを確認します。

   * `/apps/dam/gui/coral/components/admin/schemaforms/formbuilder`
   * `/apps/dam/gui/coral/components/admin/folderschemaforms/formbuilder`
   * `/apps/dam/gui/content/foldermetadataschemaeditor`
   * `/apps/dam/cfm/models/editor/components/datatypeproperties`
   * `/apps/settings/dam/cfm/models/formbuilderconfig`

1. [!UICONTROL パッケージマネージャー]を使ってパッケージをインストールします。パッケージのインストール方法については、[パッケージマネージャーのドキュメント](/help/sites-administering/package-manager.md)を参照してください。

1. [!DNL Experience Manager] ユーザーグループに `wf-workfront-users` を作成し、`jcr:all` 権限を `/content/dam` に割り当てます。

システムユーザー `workfront-tools` が自動的に作成され、必須の権限が自動的に管理されます。このコネクタを使用するすべての [!DNL Workfront] ユーザーが、このグループの一部として自動的に追加されます。

## [!DNL Experience Manager] と [!DNL Workfront] との接続の設定 {#configure-connection}

Workfront との接続を作成するには、次の手順に従います。

1. [!DNL Experience Manager] で、 **[!UICONTROL ツール]**／**[!UICONTROL クラウドサービス]**／**[!UICONTROL Workfront ツール設定]**&#x200B;を選択します。

1. 左パネルで `workfront-tools` を選択し、ページの右上の領域にある「**[!UICONTROL 作成]** 」オプションを選択します。

1. **[!UICONTROL Workfront 接続]**&#x200B;ダイアログで、[!DNL Workfront] デプロイメントの必須の詳細事項を入力して、「**[!UICONTROL Workfront に接続]**」オプションを選択します。正常に接続されると、[!DNL Workfront] ドキュメントのカスタム統合が [!DNL Workfront] 環境に自動的に作成されます。

   ![接続：[!DNL Experience Manager] と [!DNL Workfront]](/help/assets/assets/wf-connection-config.png)

1. 接続を確認するには、[!DNL Workfront] でアクセスして、API キーが同じで接続が&#x200B;**[!UICONTROL 有効]**&#x200B;であることを確認します。それには、[!DNL Workfront] で **[!UICONTROL 設定]**／**[!UICONTROL ドキュメント]**／**[!UICONTROL カスタム統合]**&#x200B;を選択します。

## 更新 [!DNL Workfront for Experience Manager enhanced connector] {#update-enhanced-connector-for-workfront}

Experience Manager Assets では、[!DNL Workfront for Experience Manager enhanced connector] を旧バージョンから最新バージョンに更新できます。

[!DNL Workfront for Experience Manager enhanced connector] を最新バージョンに変更する手順は次のとおりです。

1. 拡張コネクタの最新バージョンを[[!DNL Software Distribution] リンク](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/product/assets/workfront-tools.ui.apps.zip)からダウンロードします。

1. [!UICONTROL パッケージマネージャー]を使ってパッケージをインストールします。パッケージのインストール方法については、[パッケージマネージャーのドキュメント](/help/sites-administering/package-manager.md)を参照してください。
