---
title: Camera Raw サポート
description: Adobe Experience Manager Assets でCamera Rawサポートを有効にする方法を説明します。
contentOwner: AG
feature: Developer Tools
role: Admin
exl-id: 637c57ae-55a6-4032-9821-b55839b3e567
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '439'
ht-degree: 45%

---

# Camera Rawを使用して画像を処理 {#camera-raw-support}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

CR2、NEF、RAF などの生のファイル形式を処理し、画像をJPEG形式でレンダリングするCamera Rawサポートを有効にできます。 この機能は、Adobe Experience Manager Assets で [Camera Raw包装](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/aem630/product/assets/aem-assets-cameraraw-pkg) は、「ソフトウェア配布」から入手できます。

>[!NOTE]
>
>この機能は JPEG レンディションのみをサポートします。これは、Windows 64 ビット、Mac OS および RHEL 7.x でサポートされます。

Adobe Experience Manager Assets でCamera Rawサポートを有効にするには、次の手順に従います。

1. をダウンロードします。 [Camera Raw包装](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/aem630/product/assets/aem-assets-cameraraw-pkg) を「ソフトウェア配布」から。

1. `https://[aem_server]:[port]/workflow` にアクセスします。**[!UICONTROL DAM アセットの更新]**&#x200B;ワークフローを開きます。

1. を開きます。 **[!UICONTROL サムネールを処理]** 手順

1. 「**[!UICONTROL サムネール]**」タブで次の設定を入力します。

   * **[!UICONTROL サムネール]**：`140:100:false, 48:48:false, 319:319:false`
   * **[!UICONTROL スキップ MIME タイプ]**：`skip:image/dng, skip:image/x-raw-(.*)`

   ![chlimage](assets/chlimage_1-334.png)

1. 「**[!UICONTROL Web に対応した画像]**」タブの&#x200B;**[!UICONTROL リストをスキップ]**&#x200B;フィールドで、`audio/mpeg, video/(.*), image/dng, image/x-raw-(.*)` を指定します。

   ![chlimage](assets/chlimage_1-335.png)

1. サイドパネルから、 **[!UICONTROL Camera Raw/DNG ハンドラー]** 下のステップ **[!UICONTROL サムネールの作成]** 手順

1. 「**[!UICONTROL Camera Raw/DNG ハンドラー]**」ステップの「**[!UICONTROL 引数]**」タブで、次の設定を入力します。

   * **[!UICONTROL MIME タイプ]**：`image/dng` および `image/x-raw-(.*)`
   * **[!UICONTROL コマンド]**：

      * `DAM_Raw_Converter ${directory}/${filename} ${directory} cq5dam.web.1280.1280.jpeg 1280 1280`
      * `DAM_Raw_Converter ${directory}/${filename} ${directory} cq5dam.thumbnail.319.319.jpeg 319 319`
      * `DAM_Raw_Converter ${directory}/${filename} ${directory} cq5dam.thumbnail.140.100.jpeg 140 100`
      * `DAM_Raw_Converter ${directory}/${filename} ${directory} cq5dam.thumbnail.48.48.jpeg 48 48`

   ![chlimage_1-336](assets/chlimage_1-336.png)

1. 「**[!UICONTROL 保存]**」をクリックします。

>[!NOTE]
>
>上記の設定が **[!UICONTROL Camera RAW および DNG 処理ステップによるサンプルの DAM 更新アセット]**&#x200B;設定と同じであることを確認してください。

これで、Camera Raw ファイルをに読み込めるようになりました。 [!DNL Experience Manager] アセット。 Camera RAW パッケージをインストールして必要なワークフローを設定した後、パネルのリストに「**[!UICONTROL 画像調整]**」オプションが表示されます。

![chlimage_1-337](assets/chlimage_1-337.png)

*図：サイドパネルのオプション*

![chlimage_1-338](assets/chlimage_1-338.png)

*図：画像に軽量な編集を行うには、「 」オプションを使用します*

編集内容をCamera Rawの画像に保存した後、新しいレンディションが作成されます。 `AdjustedPreview.jpg` が画像用に生成されます。 Camera Raw以外の他の画像タイプの場合、変更はすべてのレンディションに反映されます。

## ベストプラクティス、既知の問題および制限事項 {#best-practices}

この機能には次の制限があります。

* この機能は JPEG レンディションのみをサポートします。Windows 64 ビット、Mac OS、および RHEL 7.x でサポートされています。
* RAW および DNG 形式では、メタデータの書き戻しはサポートされていません。
* Camera Rawのライブラリには、一度に処理できるピクセルの合計数に関する制限があります。 現在、最初に検出された条件に応じて、ファイルの長辺で最大 65000 ピクセルまたは 512 MP を処理できます。
