---
title: Camera Raw サポート
description: Adobe Experience Manager AssetsでCamera Rawサポートを有効にする方法を説明します。
contentOwner: AG
feature: 開発者ツール
role: Admin
exl-id: 637c57ae-55a6-4032-9821-b55839b3e567
source-git-commit: 5d96c09ef764b02e08dcdf480da1ee18f4d9a30c
workflow-type: tm+mt
source-wordcount: '406'
ht-degree: 45%

---

# Camera Rawを使用した画像の処理 {#camera-raw-support}

CR2、NEF、RAFなどの生のファイル形式を処理し、画像をJPEG形式でレンダリングするCamera Rawのサポートを有効にできます。 この機能は、Adobe Experience Manager Assetsでは、ソフトウェア配布から入手可能な[Camera Rawパッケージ](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/aem630/product/assets/aem-assets-cameraraw-pkg)を使用してサポートされます。

>[!NOTE]
>
>この機能は JPEG レンディションのみをサポートします。Windows 64ビット、Mac OS、およびRHEL 7.xでサポートされています。

Adobe Experience Manager AssetsでCamera Rawサポートを有効にするには、次の手順に従います。

1. ソフトウェア配布から[Camera Rawパッケージ](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/aem630/product/assets/aem-assets-cameraraw-pkg)をダウンロードします。

1. `https://[aem_server]:[port]/workflow` にアクセスします。**[!UICONTROL DAMアセットの更新]**&#x200B;ワークフローを開きます。

1. **[!UICONTROL サムネールを処理]**&#x200B;の手順を開きます。

1. 「**[!UICONTROL サムネール]**」タブで次の設定を指定します。

   * **[!UICONTROL サムネール]**:  `140:100:false, 48:48:false, 319:319:false`
   * **[!UICONTROL スキップ MIME タイプ]**: `skip:image/dng, skip:image/x-raw-(.*)`

   ![小さな](assets/chlimage_1-334.png)

1. 「**[!UICONTROL Webに対応した画像]**」タブの「**[!UICONTROL リストをスキップ]**」フィールドで、`audio/mpeg, video/(.*), image/dng, image/x-raw-(.*)`と指定します。

   ![小さな](assets/chlimage_1-335.png)

1. サイドパネルから、**[!UICONTROL Camera Raw/DNGハンドラー]**&#x200B;ステップを&#x200B;**[!UICONTROL サムネールの作成]**&#x200B;ステップの下に追加します。

1. **[!UICONTROL Camera Raw/DNGハンドラー]**&#x200B;の手順で、**[!UICONTROL 「引数]**」タブに次の設定を追加します。

   * **[!UICONTROL MIMEタイプ]**: `image/dng` および  `image/x-raw-(.*)`
   * **[!UICONTROL コマンド]**:

      * `DAM_Raw_Converter ${directory}/${filename} ${directory} cq5dam.web.1280.1280.jpeg 1280 1280`
      * `DAM_Raw_Converter ${directory}/${filename} ${directory} cq5dam.thumbnail.319.319.jpeg 319 319`
      * `DAM_Raw_Converter ${directory}/${filename} ${directory} cq5dam.thumbnail.140.100.jpeg 140 100`
      * `DAM_Raw_Converter ${directory}/${filename} ${directory} cq5dam.thumbnail.48.48.jpeg 48 48`

   ![chlimage_1-336](assets/chlimage_1-336.png)

1. 「**[!UICONTROL 保存]**」をクリックします。

>[!NOTE]
>
>上記の設定が **[!UICONTROL Camera RAW および DNG 処理ステップによるサンプルの DAM 更新アセット]**&#x200B;設定と同じであることを確認してください。

これで、Camera Raw ファイルを AEM Assets に読み込むことができます。Camera Rawパッケージをインストールし、必要なワークフローを設定すると、サイドパネルのリストに「**[!UICONTROL 画像調整]**」オプションが表示されます。

![chlimage_1-337](assets/chlimage_1-337.png)

*図：サイドペインのオプション*

![chlimage_1-338](assets/chlimage_1-338.png)

*図：「 」オプションを使用して、画像に軽量な編集を行います*

Camera Raw 画像に対する編集を保存すると、その画像に対して、新しいレンディション「`AdjustedPreview.jpg`」が生成されます。Camera Raw 以外の画像タイプの場合は、変更内容がすべてのレンディションに反映されます。

## ベストプラクティス、既知の問題、および制限 {#best-practices}

この機能には次の制限があります。

* この機能は JPEG レンディションのみをサポートします。これは、Windows 64 ビット、Mac OS および RHEL 7.x でサポートされます。
* メタデータの書き戻しは、RAW および DNG 形式ではサポートされていません。
* Camera Raw ライブラリには、一度に処理できる合計ピクセルに関する制限があります。現在、ファイルの長辺に最大65000ピクセル、または最初に検出された条件に応じて512 MPで処理できます。
