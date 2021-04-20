---
title: Camera Raw サポート
description: Adobe Experience Managerアセットのサポートを有効にするCamera Raw方法を説明します。
contentOwner: AG
feature: Developer Tools
role: Administrator
translation-type: tm+mt
source-git-commit: 4acf159ae1b9923a9c93fa15faa38c7f4bc9f759
workflow-type: tm+mt
source-wordcount: '407'
ht-degree: 45%

---


# イメージCamera Rawの処理に使用{#camera-raw-support}

CR2、NEF、RAFなどの生のファイル形式を処理し、Camera Raw画像をJPEG形式でレンダリングするためのサポートを有効にすることができます。 この機能は、Software Distributionの[パッケージCamera Raw](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/aem630/product/assets/aem-assets-cameraraw-pkg)を使用して、Adobe Experience Managerアセットでサポートされます。

>[!NOTE]
>
>この機能は JPEG レンディションのみをサポートします。Windows 64ビット、Mac OS、およびRHEL 7.xでサポートされています。

Adobe Experience ManagerアセットのCamera Rawサポートを有効にするには、次の手順に従います。

1. [パッケージCamera Raw](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/aem630/product/assets/aem-assets-cameraraw-pkg)をSoftware Distributionからダウンロードします。

1. `https://[aem_server]:[port]/workflow` にアクセスします。**[!UICONTROL DAM Update Asset]**&#x200B;ワークフローを開きます。

1. **[!UICONTROL サムネールを処理]**&#x200B;の手順を開きます。

1. 「**[!UICONTROL サムネール]**」タブで次の設定を指定します。

   * **[!UICONTROL サムネール]**:  `140:100:false, 48:48:false, 319:319:false`
   * **[!UICONTROL スキップ MIME タイプ]**: `skip:image/dng, skip:image/x-raw-(.*)`

   ![小粒](assets/chlimage_1-334.png)

1. 「**[!UICONTROL Web対応のリスト]**」タブの「**[!UICONTROL 画像をスキップ]**」フィールドで、`audio/mpeg, video/(.*), image/dng, image/x-raw-(.*)`を指定します。

   ![小粒](assets/chlimage_1-335.png)

1. サイドパネルから、**[!UICONTROL サムネールCamera Rawの作成]**&#x200B;の手順の下に&#x200B;**[!UICONTROL /DNGハンドラー]**&#x200B;の手順を追加します。

1. **[!UICONTROL Camera Raw/DNGハンドラー]**&#x200B;の手順で、**[!UICONTROL 「引数]**」タブに次の設定を追加します。

   * **[!UICONTROL MIMEタイプ]**: `image/dng` と  `image/x-raw-(.*)`
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

これで、Camera Raw ファイルを AEM Assets に読み込むことができます。パッケージをインストールしCamera Rawて必要なワークフローを設定すると、サイドパネルのリストに「**[!UICONTROL 画像の調整]**」オプションが表示されます。

![chlimage_1-337](assets/chlimage_1-337.png)

*図：サイドペインのオプション*

![chlimage_1-338](assets/chlimage_1-338.png)

*図：このオプションを使用して、画像に軽量な編集を行います*

Camera Raw 画像に対する編集を保存すると、その画像に対して、新しいレンディション「`AdjustedPreview.jpg`」が生成されます。Camera Raw 以外の画像タイプの場合は、変更内容がすべてのレンディションに反映されます。

## ベストプラクティス、既知の問題、および制限  {#best-practices}

この機能には次の制限があります。

* この機能は JPEG レンディションのみをサポートします。これは、Windows 64 ビット、Mac OS および RHEL 7.x でサポートされます。
* メタデータの書き戻しは、RAW および DNG 形式ではサポートされていません。
* Camera Raw ライブラリには、一度に処理できる合計ピクセルに関する制限があります。現在、ファイルの長辺で最大65,000ピクセル、または最初に検出される条件に合わせて512 MPで処理できます。
