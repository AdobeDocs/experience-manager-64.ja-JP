---
title: Adobe Campaign フォームコンポーネントを使用したカスタム AEM ページテンプレートの作成
seo-title: Creating Custom AEM Page Template with Adobe Campaign Form Components
description: Adobe Campaign Form コンポーネントを使用するカスタムページテンプレートの作成
seo-description: Build a custom page template that uses Adobe Campaign Form components
uuid: 8162ace2-b661-4c39-b0fb-288e1c035b9c
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: c3f6eed4-bbda-454a-88ce-c7f2041d4217
exl-id: e70c9d23-5a4d-4137-82ad-3f3237f468c0
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '274'
ht-degree: 55%

---

# Adobe Campaign フォームコンポーネントを使用したカスタム AEM ページテンプレートの作成{#creating-custom-aem-page-template-with-adobe-campaign-form-components}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

このページでは、Geometrixx-outdoors テンプレート（`/apps/geometrixx-outdoors/components/page_campaign_profile`）の実装方法を確認することによって、[Adobe Campaign フォーム](/help/sites-authoring/adobe-campaign-components.md)コンポーネントを使用するカスタムページテンプレートの作成方法を説明し、独自のカスタムテンプレート作成時に必要になる可能性がある重要な情報を示します。

>[!NOTE]
>
>[メールとフォームのサンプルは、Geometrixx でのみ使用できます](/help/sites-developing/we-retail.md)。Geometrixx のサンプルコンテンツを Package Share からダウンロードしてください。

Adobe Campaignフォームコンポーネントを使用してカスタムAEMページテンプレートを作成するには、必ず以下の点を確認してください。

1. **正しい resourceSuperType**

   ページコンポーネントを `mcm/campaign/components/profile` から継承していることを確認してください。

   これは、サーブレットが情報を取得および保存するために必要です。

   * `com.day.cq.mcm.campaign.servlets.TemplateListServlet`
   * `com.day.cq.mcm.campaign.servlets.SaveProfileServlet`

   ![chlimage_1-201](assets/chlimage_1-201.png)

1. **ClientContext 設定**

   ClientContext 設定（`/etc/designs/geometrixx-outdoors/jcr:content/page_campaign_profile`）には、次の設定があります。

   * ClientContext が `/etc/clientcontext/campaign` を指している
   * 追加の *config* ノードもあります。

   ![chlimage_1-202](assets/chlimage_1-202.png)

1. **head.jsp (/apps/geometrixx-outdoors/components/page_campaign_profile/head.jsp)**

   In **head.jsp**&#x200B;を見ると、次の行が **clientcontext-config** そして **cloudservice-hook**:

   ```
   <cq:include path="config" resourceType="cq/personalization/components/clientcontext_optimized/config"/>
   <sling:include path="contexthub" resourceType="granite/contexthub/components/contexthub"/>
   <cq:include script="/libs/cq/cloudserviceconfigs/components/servicelibs/servicelibs.jsp"/>
   ```

1. **body.jsp (/apps/geometrixx-outdoors/components/page_campaign_profile/body.jsp)**

   **body.jsp** では、クラウドサービスがページ下部に読み込まれます。

   ```
   <cq:include path="cloudservices" resourceType="cq/cloudserviceconfigs/components/servicecomponents"/>
   ```

1. **キャンペーンページのプロパティ**

   Adobe Campaignテンプレートを選択できるように、ページプロパティは **Campaign** タブ：

   `/apps/geometrixx-outdoors/components/page_campaign_profile/dialog/items/tabs/items/campaign`

   ![chlimage_1-203](assets/chlimage_1-203.png)

1. **テンプレートの設定**

   テンプレート（`/apps/geometrixx-outdoors/templates/campaign_profile/jcr:content`）には、次のデフォルト値があります。

   | **acMapping** | mapRecipient(Adobe Campaign 6.1 の場合 )、プロファイル (Adobe Campaign Standardの場合 ) |
   |---|---|
   | **acTemplateId** | メール |

   ![chlimage_1-204](assets/chlimage_1-204.png)
