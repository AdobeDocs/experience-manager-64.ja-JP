---
title: パノラマ画像
seo-title: パノラマ画像
description: Dynamic Media でのパノラマ画像の使用方法を学習します。
seo-description: Dynamic Media でのパノラマ画像の使用方法を学習します。
uuid: dfd7a55c-7bcc-4d62-8c3a-a73726881103
contentOwner: Rick Brough
topic-tags: dynamic-media
products: SG_EXPERIENCEMANAGER/6.4/ASSETS
content-type: reference
discoiquuid: fc285b25-2bce-493c-87bc-5f1a8a26eb42
translation-type: tm+mt
source-git-commit: e2bb2f17035e16864b1dc54f5768a99429a3dd9f
workflow-type: tm+mt
source-wordcount: '591'
ht-degree: 47%

---


# パノラマ画像 {#panoramic-images}

ここでは、パノラマ画像ビューアを使用して球パノラマ画像をレンダリングし、室内、物件、場所、風景などをあらゆる角度から見ることができる臨場感あふれる体験を提供する方法について説明します。

[ビューアプリセットの管理](managing-viewer-presets.md)も参照してください。

![panoramic-image2](assets/panoramic-image2.png)

## パノラマ画像ビューアで使用するアセットのアップロード {#uploading-assets-for-use-with-the-panoramic-image-viewer}

アップロードするアセットが、パノラマ画像ビューアで使用する球パノラマ画像として適格となるには、アセットが以下の一方または両方の条件を満たしている必要があります。

* 縦横比が 2 である必要があります。

   You can override the default aspect ratio setting of 2 in **[!UICONTROL CRXDE Lite]** at the following:

   `/conf/global/settings/cloudconfigs/dmscene7/jcr:content`

* キーワード `equirectangular`、または `spherical` と `panorama`、または `spherical` と `panoramic` でタグ付けされている必要があります。[タグの使用](/help/sites-authoring/tags.md)を参照してください。

縦横比とキーワードの両方の条件が、アセットの詳細ページと「**[!UICONTROL パノラマメディア]**」 コンポーネントのパノラマアセットに適用されます。

パノラマ画像ビューアで使用するアセットをアップロードするには、[アセットのアップロード](managing-assets-touch-ui.md#uploading-assets)を参照してください。

## Configuring Dynamic Media Classic {#configuring-dynamic-media-classic-scene}

パノラマ画像ビューアをAEM内で正しく動作させるには、パノラマ画像ビューアプリセットをDynamic Media ClassicおよびDynamic Media Classic固有のメタデータと同期して、JCRでビューアプリセットを更新する必要があります。 これを行うには、次の方法でDynamic Media Classicを設定します。

1. [各会社アカウントにDynamic Media Classic](https://www.adobe.com/jp/marketing/experience-manager/scene7-login.html) のインスタンスにログインします。

1. ページの右上隅付近で、**[!UICONTROL 設定／アプリケーション設定／公開設定／Image Server]** をクリックします。
1. On the **[!UICONTROL Image Server Publish]** page, from the **[!UICONTROL Publish Context]** drop-down menu near the top, select **[!UICONTROL Image Serving]**.

1. On the same **[!UICONTROL Image Server Publish]** page, locate the heading **[!UICONTROL Request Attributes]**.
1. Under the **[!UICONTROL Request Attributes]** heading, locate **[!UICONTROL Reply Image Size Limit]**. Then, in the associated **[!UICONTROL Width]** and **[!UICONTROL Height]** fields, increase the maximum allowable image size for panoramic images.

   Dynamic Media Classicの制限は25,000,000ピクセルです。 縦横比が2:1の画像で許可される最大サイズは7000 x 3500です。 ただし、通常のデスクトップ画面の場合、4096 x 2048 ピクセルで十分です。

   >[!NOTE]
   >
   >許容される最大画像サイズ以内の画像のみがサポートされます。サイズ制限を超える画像を要求すると、403 応答が生成されます。

1. Under the **Request Attributes]** heading, do the following:

   * Set **[!UICONTROL Request Obfuscation Mode]** to **[!UICONTROL Disabled]**.
   * Set **[!UICONTROL Request Locking Mode]** to **[!UICONTROL Disabled]**.

   These settings are necessary for using the **[!UICONTROL Panoramic Media]** component in AEM.

1. **[!UICONTROL Image Server公開]** ページの下部の左側で、「 **[!UICONTROL 保存]**」をタップします。

1. In the lower-right corner, tap **[!UICONTROL Close]**.

### パノラマメディア コンポーネントのトラブルシューティング {#troubleshooting-the-panoramic-media-wcm-component}

If you dropped an image into the **[!UICONTROL Panoramic Media]** component in your WCM and the component placeholder collapsed, you may want to troubleshoot the following:

* 403 Forbidden エラーが発生する場合は、要求された画像のサイズが大きすぎることが原因となっている可能性があります。[Dynamic Media Classic（Scene7）の設定](#configuring-dynamic-media-classic-scene)でおこなった「*返信画像のサイズ制限*」の設定を確認します。

* For an *Invalid lock* on the asset or *Parsing error* displayed on the page, check **[!UICONTROL Request Obfuscation Mode]** and **[!UICONTROL Request Locking Mode]** to ensure they are disabled.
* For a tainted canvas error, setup a **[!UICONTROL Rule Set Definition File Path and Invalidate CTN]** for the previous requests for the image asset.
* サポートされている制限を超えるサイズの画像を要求した後に画質が大幅に低下した場合は、**[!UICONTROL JPEG エンコード属性／画質]**&#x200B;の設定が空でないことを確認します。A typical setting for the **[!UICONTROL Quality]** field is `95`. You can find the setting on the **[!UICONTROL Image Server Publish]** page. To access the page, see [Configuring Dynamic Media Classic](#configuring-dynamic-media-classic-scene).

## パノラマ画像のプレビュー {#previewing-panoramic-images}

詳しくは、[アセットのプレビュー](previewing-assets.md)を参照してください。

## パノラマ画像の公開 {#publishing-panoramic-images}

[アセットの公開](publishing-dynamicmedia-assets.md)を参照してください。
