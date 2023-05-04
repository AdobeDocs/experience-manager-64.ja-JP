---
title: パノラマ画像
description: Dynamic Mediaでパノラマ画像を使用する方法を説明します。
contentOwner: Rick Brough
topic-tags: dynamic-media
products: SG_EXPERIENCEMANAGER/6.4/ASSETS
content-type: reference
exl-id: 51150d51-865e-4b8e-9990-ca755e4c7778
feature: Panoramic Images
role: User
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '617'
ht-degree: 30%

---

# パノラマ画像 {#panoramic-images}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

ここでは、パノラマ画像ビューアを使用して球パノラマ画像をレンダリングし、室内、物件、場所、風景などをあらゆる角度から見ることができる臨場感あふれる体験を提供する方法について説明します。

関連トピック [ビューアプリセットの管理](managing-viewer-presets.md).

![panoramic-image2](assets/panoramic-image2.png)

## パノラマ画像ビューアで使用するアセットのアップロード {#uploading-assets-for-use-with-the-panoramic-image-viewer}

アップロードするアセットが、パノラマ画像ビューアで使用する球体パノラマ画像として認められるためには、アセットが次のいずれかまたは両方を満たしている必要があります。

* 縦横比が 2 である。

   デフォルトの縦横比設定である 2 を **[!UICONTROL CRXDE Lite]** 次の場所に移動します。

   `/conf/global/settings/cloudconfigs/dmscene7/jcr:content`

* キーワード `equirectangular`、または `spherical` と `panorama`、または `spherical` と `panoramic` でタグ付けされている必要があります。[タグの使用](/help/sites-authoring/tags.md)を参照してください。

縦横比とキーワードの両方の条件が、アセットの詳細ページと「**[!UICONTROL パノラマメディア]**」 コンポーネントのパノラマアセットに適用されます。

パノラマ画像ビューアで使用するアセットをアップロードするには、[アセットのアップロード](managing-assets-touch-ui.md#uploading-assets)を参照してください。

## Dynamic Media Classicの設定 {#configuring-dynamic-media-classic-scene}

パノラマ画像ビューアがAEM内で正しく動作するようにするには、パノラマ画像ビューアプリセットをDynamic Media ClassicおよびDynamic Media Classic固有のメタデータと同期して、ビューアプリセットが JCR で更新されるようにする必要があります。 これをおこなうには、次の方法でDynamic Media Classicを設定します。

1. [Dynamic Media Classicデスクトップアプリケーションへのログイン](https://experienceleague.adobe.com/docs/?lang=jadynamic-media-classic/using/intro/dynamic-media-classic-desktop-app.html#system-requirements-dmc-app) 会社アカウントごとに

1. ページの右上隅にある「 **[!UICONTROL 設定/アプリケーション設定/公開設定/Image Server]**.
1. の **[!UICONTROL Image Server 公開]** ページの **[!UICONTROL 公開コンテキスト]** 上部付近のドロップダウンメニューで、「 **[!UICONTROL 画像サービング]**.

1. 同じ **[!UICONTROL Image Server 公開]** ページで、見出しを探します。 **[!UICONTROL 要求属性]**.
1. 以下 **[!UICONTROL 要求属性]** 見出し、場所 **[!UICONTROL 返信画像のサイズ制限]**. 次に、 **[!UICONTROL 幅]** および **[!UICONTROL 高さ]** フィールドで指定する場合、パノラマ画像に使用できる最大画像サイズを大きくします。

   Dynamic Media Classic には、25,000,000 ピクセルという制限があります。縦横比が 2:1 の画像の最大許容サイズは 7000 x 3500 です。ただし、通常のデスクトップ画面の場合、4096 x 2048 ピクセルで十分です。

   >[!NOTE]
   >
   >許容される最大画像サイズ以内の画像のみがサポートされます。サイズ制限を超える画像に対するリクエストに対しては、403 応答が返されます。

1. 以下 **[要求属性]** 見出しには、次の操作を行います。

   * 設定 **[!UICONTROL 要求の難読化モード]** から **[!UICONTROL 無効]**.
   * 設定 **[!UICONTROL リクエストロックモード]** から **[!UICONTROL 無効]**.

   これらの設定は、 **[!UICONTROL パノラマメディア]** AEMのコンポーネント。

1. の下部に **[!UICONTROL Image Server 公開]** ページの左側で、をタップします。 **[!UICONTROL 保存]**.

1. 右下隅でをタップします。 **[!UICONTROL 閉じる]**.

### パノラマメディアコンポーネントのトラブルシューティング {#troubleshooting-the-panoramic-media-wcm-component}

画像を **[!UICONTROL パノラマメディア]** WCM のコンポーネントが折りたたまれ、コンポーネントプレースホルダーが折りたたまれた場合、次のトラブルシューティングをおこなうことができます。

* 403 Forbidden エラーが発生した場合は、要求された画像サイズが大きすぎることが原因である可能性があります。 以下を確認します。 *返信画像のサイズ制限* の設定 [Dynamic Media Classicの設定](#configuring-dynamic-media-classic-scene).

* の *無効なロック* ( アセットまたは *解析エラー* ページに表示された場合は、 **[!UICONTROL 要求の難読化モード]** および **[!UICONTROL リクエストロックモード]** をクリックして、これらが無効になっていることを確認します。
* 汚染されたキャンバスエラーの場合は、 **[!UICONTROL ルールセット定義ファイルのパスと CTN の無効化]** を設定します。
* サポートされている制限を超えるサイズの画像リクエストの後、画質が非常に低くなった場合は、 **[!UICONTROL JPEGエンコーディング属性/画質]** の設定が空ではありません。 「**[!UICONTROL 画質]**」フィールドの一般的な設定は、`95` です。設定は、 **[!UICONTROL Image Server 公開]** ページ。 ページにアクセスするには、 [Dynamic Media Classicの設定](#configuring-dynamic-media-classic-scene).

## パノラマ画像のプレビュー {#previewing-panoramic-images}

詳しくは、 [アセットのプレビュー](previewing-assets.md).

## パノラマ画像の公開 {#publishing-panoramic-images}

[アセットの公開](publishing-dynamicmedia-assets.md)を参照してください。
