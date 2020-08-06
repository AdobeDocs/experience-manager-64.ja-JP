---
title: Adobe Search&Promote との統合
seo-title: Adobe Search&Promote との統合
description: Adobe Search&Promote と統合する方法について説明します。
seo-description: Adobe Search&Promote と統合する方法について説明します。
uuid: ddc4510a-9bd1-4238-a8a8-5f4f563edd8d
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: integration
content-type: reference
discoiquuid: 87e62346-98d5-40ec-a3ef-904adf667425
translation-type: tm+mt
source-git-commit: cdec5b3c57ce1c80c0ed6b5cb7650b52cf9bc340
workflow-type: tm+mt
source-wordcount: '920'
ht-degree: 53%

---


# Adobe Search&amp;Promote との統合{#integrating-with-adobe-search-promote}

Web サイトから Adobe Search&amp;Promote サービスを呼び出すには、次のタスクを実行します。

1. クラウドの URL を指定します。
1. Search&amp;Promote サービスへの接続を設定します。
1. Add Search&amp;Promote components to [!UICONTROL Sidekick].
1. コンポーネントを使用して、コンテンツを作成します（[Web ページへの Search&amp;Promote 機能の追加](/help/sites-authoring/search-and-promote.md)を参照）。
1. バナーをページに追加します。バナー画像は、Search&amp;Promote データの影響を受けます。
1. Search&amp;Promote サービスが使用するサイトマップを生成します。

>[!NOTE]
>
>カスタムプロキシ設定で Search&amp;Promote を使用している場合、AEM には 3.x API を使用する機能と 4.x API を使用する機能があるので、両方の HTTP クライアントプロキシを設定する必要があります。
>
>* 3.x は [http://localhost:4502/system/console/configMgr/com.day.commons.httpclient](http://localhost:4502/system/console/configMgr/com.day.commons.httpclient) のように設定します。
>* 4.x は [http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator](http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator) のように設定します。

>



## Search&amp;Promote サービス URL の変更 {#changing-the-search-promote-service-url}

The default URL that is configured for the Search&amp;Promote service is `https://searchandpromote.omniture.com/px/`. 別のサービスを使用するには、OSGi コンソールを使用して別の URL を指定します。

**Search&amp;PromoteサービスのURLを変更するには**:

1. Open the [!UICONTROL OSGi] console and tap the **[!UICONTROL Configuration]** tab. （[http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr)）。

1. Click the **[!UICONTROL Day CQ Search&amp;Promote Configuration]** item.
1. 「 **[!UICONTROL リモートサーバーURI]** 」テキストフィールドにURLを入力し、「 **[!UICONTROL 保存]**」をタップします。

## Search&amp;Promote への接続の設定 {#configuring-the-connection-to-search-promote}

Search&amp;Promote への 1 つ以上の接続を設定して、Web ページがサービスとやり取りできるようにします。接続するには、Search&amp;Promote アカウントのメンバー ID とアカウント番号が必要です。

**Search&amp;Promoteへの接続を設定するには**:

1. **[!UICONTROL ツール]** アイコン **[!UICONTROL /]**&#x200B;導入 **[!UICONTROL から、]** Cloud Servicesを選択します。

   これにより、クラウドサービスダッシュボードが表示されます。ローカルマシンの場合、ダッシュボードの URI は、次のようになります。

   [http://localhost:4502/libs/cq/core/content/tools/cloudservices.html](http://localhost:4502/libs/cq/core/content/tools/cloudservices.html)

1. [!UICONTROL Cloud Services] ページで、 **[!UICONTROL AdobeSearch&amp;Promote]** リンクまたは **[!UICONTROL Search&amp;Promote]** アイコンをタップします。

1. If this is the first time you are configuring Adobe Search&amp;Promote, tap **[!UICONTROL Configure Now]** to open the [!UICONTROL Create Configuration] panel.

   If you would like to learn more about Search&amp;Promote click **[!UICONTROL Learn more]** instead.

   ![chlimage_1-409](assets/chlimage_1-409.png)

1. Enter a **[!UICONTROL Title]** that is recognizable to page authors, and enter a unique **[!UICONTROL Name]**, then tap **[!UICONTROL Create]**.

   また、新しく作成した設定が、**[!UICONTROL クラウドサービスダッシュボード]**&#x200B;の Adobe Search&amp;Promote リスト項目の「**[!UICONTROL 利用可能な設定]**」の下に表示されます。

   ![chlimage_1-410](assets/chlimage_1-410.png)

1. 「コンポーネントを [!UICONTROL 編集] 」ダイアログボックスで、フィールドに次を追加します。

   * **[!UICONTROL メンバー ID]**
   * **[!UICONTROL アカウント番号]**

   >[!NOTE]
   >
   >この情報を自分で取得するには、次にログインします。
   >
   >[https://searchandpromote.omniture.com/center/](https://searchandpromote.omniture.com/center/)
   >
   >有効な Seach&amp;Promote 資格情報（電子メール／パスワード）を使用します。
   >
   >ブラウザのアドレスバーにURLが表示されていることに注意してください。 次のようになります。
   >
   >[](https://searchandpromote.omniture.com/px/home/?sp_id=XXXXXXXX-spYYYYYYYY)
   >
   >[https://searchandpromote.omniture.com/px/home/?sp_id=XXXXXXXX-spYYYYYYYY](https://searchandpromote.omniture.com/px/home/?sp_id=XXXXXXXX-spYYYYYYYY)
   >
   >ここで、 **XXXXXXXXX****[!UICONTROL は]** メンバIDに対応し、 **[!UICONTROL spYYYYYYYYYY]** はアカウント番号に対応します。

1. Tap **[!UICONTROL Connect To Search&amp;Promote]**.

   When the connection success message appears, tap **[!UICONTROL OK]**.

   （接続後、ボタンのテキストが「**[!UICONTROL Search&amp;Promote に再接続]**」に変更されます。）

1. 「**[!UICONTROL OK]**」をタップします。今作成した設定の Search&amp;Promote 設定ページが表示されます。

## データセンターの設定 {#configuring-the-data-center}

Search&amp;Promoteアカウントがアジアまたはヨーロッパにある場合は、デフォルトのデータセンターを変更して、適切なデータセンターを指すようにする必要があります（デフォルトのデータセンターは北米のアカウント用です）。

**データセンターを設定するには**:

1. Navigate to the Web console at `http://localhost:4502/system/console/configMgr/com.day.cq.searchpromote.impl.SearchPromoteServiceImpl`

   ![chlimage_1-411](assets/chlimage_1-411.png)

1. サーバーの場所に応じて、URI を次のいずれかに変更します。

   * North America: [https://center.atomz.com/px/](https://center.atomz.com/px/)
   * EMEA: [https://center.lon5.atomz.com/px/](https://center.lon5.atomz.com/px/)
   * APAC: [https://center.sin2.atomz.com/px/](https://center.sin2.atomz.com/px/)

1. 「**[!UICONTROL 保存]**」をタップします。

## Search&amp;Promote コンポーネントのサイドキックへの追加 {#adding-search-promote-components-to-sidekick}

[!UICONTROL デザインモードで、] 各コンポーネントを編集し **[!UICONTROL 、]** サイドキックのSearch&amp;Promoteコンポーネントを許可します 。 （詳しくは、[コンポーネント](/help/sites-developing/components.md)のドキュメントを参照）。

For information about using the components, see [Adding Search&amp;Promote features to a Web Page](/help/sites-authoring/search-and-promote.md).

## ページで使用する Search&amp;Promote サービスの指定 {#specifying-the-search-promote-service-that-your-pages-use}

特定の Search&amp;Promote サービスを使用できるように、Web ページを設定します。Search&amp;Promote コンポーネントは、自動的にホストページのサービスを使用します。

ページの Search&amp;Promote プロパティを設定すると、すべての子ページが設定を継承します。必要に応じて、継承された設定を上書きするように子ページを設定できます。

>[!NOTE]
>
>サービス接続は、既に設定されている必要がありますSee [Configure the connection to Search&amp;Promote](#configuring-the-connection-to-search-promote).

1. **[!UICONTROL ページプロパティ]**&#x200B;ダイアログボックスを開きます。例えば、**[!UICONTROL Web サイト]**&#x200B;ページで、ページを右クリックし、「**[!UICONTROL プロパティ]**」をクリックします。

1. 「**[!UICONTROL クラウドサービス]**」タブをクリックします。

1. 親ページからのクラウドサービス設定の継承を無効にするには、継承パスの横にある南京錠アイコンをクリックします。

   ![sandinheritpadlock](assets/sandpinheritpadlock.png)

1. Click **[!UICONTROL Add Service]**, select **[!UICONTROL Adobe Search&amp;Promote]**, then click **[!UICONTROL OK]**.

1. Select the connection configuration for your Search&amp;Promote account, then click **[!UICONTROL OK]**.

## 製品フィード {#product-feed}

Search&amp;Promote統合により、次のことが可能になります。

* Use the [!UICONTROL eCommerce] API, independently of the underlying repository structure and commerce platform.
* Leverage the [!UICONTROL Index Connector] feature of Search&amp;Promote to provide a product feed in XML format.
* Leverage the [!UICONTROL Remote Control] feature of Search&amp;Promote to perform on-demand or scheduled requests of the product feed.
* 様々なSearch&amp;Promoteアカウントに対するフィードの生成（クラウドサービスの設定として設定）

For more information, see [Product Feed](/help/sites-administering/product-feed.md).
