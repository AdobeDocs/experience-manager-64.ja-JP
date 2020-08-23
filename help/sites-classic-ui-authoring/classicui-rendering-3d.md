---
title: 3D アセットのレンダリング
seo-title: 3D アセットのレンダリング
description: AEM で操作して保存した 3D アセットをレンダリングして、Web コンテンツページで使用する 2D 画像を作成できます。
seo-description: AEM で操作して保存した 3D アセットをレンダリングして、Web コンテンツページで使用する 2D 画像を作成できます。
uuid: fbbe4fb4-cf21-4752-a2b8-bec2d40e8362
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.4/ASSETS
topic-tags: authoring
content-type: reference
discoiquuid: bf155d8c-c012-4cb4-89a6-ceead715630e
translation-type: tm+mt
source-git-commit: b698a1348df3ec2ab455c236422784d10cbcf7c2
workflow-type: tm+mt
source-wordcount: '705'
ht-degree: 74%

---


# 3D アセットのレンダリング{#rendering-d-assets}

AEM で操作して保存した 3D アセットをレンダリングして、Web コンテンツページで使用する 2D 画像を作成できます。

[ページコンテンツの編集](/help/sites-authoring/qg-page-authoring.md#editing-your-page-content)を参照してください。

## 3D アセットをレンダリングする際のパフォーマンスに関する考慮事項 {#performance-considerations-when-rendering-d-assets}

3D コンテンツのレンダリングには、CPU やメモリなどのサーバーリソースが著しく消費されます。そのため、レンダリングには多大な時間がかかることがよくあります。レンダリング時間は、モデルサイズとサーバーのハードウェアはもちろん、以下の様々な要因によって大幅に異なります。

* **レンダラーの選択**。

   AEM 3D のデフォルトの Rapid Refine™ レンダラーは、レンダリング時間を短縮するために、やや品質を低下させています。それでも多くのアプリケーションに高品質なレンダリングを提供しています。サードパーティ製アプリケーションに付属のレンダラー（Autodesk® Maya® または Autodesk® 3ds Max® によってデプロイされる V-Ray™ や NVIDIA® Mental Ray® など）は、幅広い設定が可能で、ステージのデザイン時にパフォーマンスと品質のバランスを取ります。

* **IBL と従来のライティング**。

   この要因は、デフォルトの Rapid Refine レンダラーにはあまり影響しませんが、Mental Ray などのサードパーティ製レンダラーでは、従来のポイントライトまたはスポットライトを使用した場合に比べ、IBL ステージを使用したレンダリングが大幅にスピードダウンします。

一般的に、Rapid Refine レンダラーで大きな画像をレンダリングするには数分かかります。しかし、サードパーティ製レンダラーを最高品質に設定すると、数十分、場合によっては数時間かかることがよくあります。

サーバーの過負荷を防ぐために、必要に応じて変換、処理およびレンダリングジョブがサーバーのキューに登録されます。The message &quot;Waiting for rendering...&quot; is shown on recently uploaded assets in the [!UICONTROL Card View]. このステータスは、現在のレンダリングジョブが開始できるように、他の処理ジョブまたはレンダリングジョブが終了する必要があることを示します。

>[!NOTE]
>
>AEM 3D のインタラクティブビューに表示されているマテリアルに関わらず、3D アセットは常に元のマテリアルを使用してレンダリングされます。この機能は、組み込みの Rapid Refine レンダラーとすべてのネイティブレンダラーの両方に適用されます。

**3Dアセットをレンダリングするには**:

1. 表示する 3D アセットを開きます。

   [3D アセットの表示](/help/sites-classic-ui-authoring/classicui-view-3d-assets.md)を参照してください。

1. **Adobe Experience Manager** の&#x200B;**[!UICONTROL ナビゲーション]**&#x200B;ページで「**[!UICONTROL アセット]**」をタップします。
1. ページの右上隅付近にある「**[!UICONTROL 表示]**」ドロップダウンリストで「**[!UICONTROL カード表示]**」をタップします。
1. レンダリングする 3D オブジェクトに移動します。

1. 3D オブジェクトのカードをタップして、アセットの詳細ページで開きます。
1. ページの左上隅付近にあるドロップダウンリストをタップして、「**[!UICONTROL レンダリング]**」を選択します。

   ![chlimage_1-13](assets/chlimage_1-13.png)

1. Near the upper-right corner of the asset details page, tap the **[!UICONTROL Stage Selector]** icon (spotlight), then select a stage name with the background and lighting that you want to apply to the 3D object.

   [AEM 3D でのステージの使用](/help/sites-classic-ui-authoring/classicui-stages-aem3d.md)を参照してください。

   ![chlimage_1-14](assets/chlimage_1-14.png)

   [!UICONTROL ステージセレクターアイコン]

1. On the **[!UICONTROL Render]** drop-down list on the left side of the asset details page, select a renderer.

   デフォルトの **[!UICONTROL Rapid Refine]** レンダラーは常に表示されます。選択したステージがネイティブ形式の場合は、対応するサードパーティ製レンダラーもリストに表示され、選択できるようになります。

   [AEM 3D でのステージの使用](/help/sites-classic-ui-authoring/classicui-stages-aem3d.md)を参照してください。

1. 以下の操作を実行してください。

   * In the **[!UICONTROL Width and Height]** fields, enter the pixel width and height that you want your image rendered.
   * In the **[!UICONTROL Image Name]** field, enter the name of the rendered image.
   * In the **[!UICONTROL Export Path]** field, enter the path where you want the rendered image stored. Or, tap the **[!UICONTROL Browse]** icon and navigate to a location.
   * （オプション）「**[!UICONTROL 既存の画像を上書き]**」チェックボックスを選択または選択解除します。

1. Near the upper-right corner of the asset details page, tap the **[!UICONTROL Camera Selector]** icon. レンダリングした画像に適用するカメラ視野を選択します。

   左右または上下のバーは、レンダリングされる視野の部分を示す視覚的なインジケーターです。選択したステージにカメラが含まれる場合は、事前定義されたカメラを選択できます。

   ![chlimage_1-15](assets/chlimage_1-15.png)

   [!UICONTROL カメラセレクターアイコン]

1. 「**[!UICONTROL レンダリングを開始]**」をタップして、レンダリングプロセスを開始します。

   レンダリングが開始されたことを示すメッセージが一時的に表示されます。For convenience, this message also includes a link to the selected [!UICONTROL Output Folder] so you can navigate to it directly.

