---
title: PDF Rasterizer を使用したレンディションの生成
description: Adobe PDF Rasterizer ライブラリを使用して、高品質のサムネールとレンディションを生成します。
contentOwner: AG
feature: Developer Tools,Renditions
role: Developer,Admin
exl-id: 7d78fba9-16df-44e0-aae6-83f65e8d2bbd
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '757'
ht-degree: 74%

---

# PDF Rasterizer の使用 {#using-pdf-rasterizer}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

サイズが大きくコンテンツが多い PDF や AI ファイルを [!DNL Adobe Experience Manager Assets] にアップロードすると、デフォルトのライブラリで正確な出力が生成されない場合があります。Adobe PDF Rasterizer ライブラリでは、デフォルトライブラリの出力よりも信頼性が高く正確な出力を生成できます。次のようなシナリオで PDF Rasterizer ライブラリを使用することをお勧めします。

次のようなファイルで PDF Rasterizer ライブラリを使用することをお勧めします。

* サイズが大きくコンテンツが多い AI または PDF ファイル。
* デフォルトで生成されないサムネールを含む AI ファイルおよび PDFファイル。
* Pantone Matching System（PMS）カラーを使用した AI ファイル.

PDFRasterizer を使用して生成されたサムネールとプレビューは、標準の出力に比べて画質が優れているので、デバイス間で一貫した表示エクスペリエンスを提供します。 Adobe PDF Rasterizer ライブラリは、カラースペースの変換をサポートしていません。 ソースファイルのカラースペースに関係なく、常にRGBに出力されます。

1. [ソフトウェア配布](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/product/assets/aem-assets-pdf-rasterizer-pkg-4.4.zip) から PDF Rasterizer パッケージを [!DNL Adobe Experience Manager] のデプロイメントにインストールします。

   >[!NOTE]
   >
   >PDF Rasterizer ライブラリは、Windows と Linux のみで使用できます。

1. [!DNL Assets] ワークフローコンソール（`https://[aem_server]:[port]/workflow`）にアクセスします。[!UICONTROL DAM アセットの更新]ワークフローを開きます。

1. デフォルトの方法を使用して PDF ファイルと AI ファイルのサムネールおよび web レンディションが生成されないようにするには、次の手順に従います。

   * を開きます。 **[!UICONTROL サムネール処理]** 手順と追加 `application/pdf` または `application/postscript` 内 **[!UICONTROL スキップ MIME タイプ]** 下のフィールド **[!UICONTROL サムネール]** タブに移動します。

   ![skip_mime_types-2](assets/skip_mime_types-2.png)

   * 「**[!UICONTROL Web に対応した画像]**」タブの「**[!UICONTROL リストをスキップ]**」に、`application/pdf` または `application/postscript` を要件に応じて追加します。

   ![画像形式のサムネール処理をスキップする設定](assets/web_enabled_imageskiplist.png)

1. 「**[!UICONTROL PDF／ AI 画像プレビューレンディションをラスタライズ]**」手順を開き、デフォルトの画像プレビューレンディションの生成をスキップする MIME タイプを除外します。例えば、**[!UICONTROL MIME タイプ]**&#x200B;のリストから、`application/pdf`、 `application/postscript` または `application/illustrator` という MIME タイプを除外します。

   ![process_arguments](assets/process_arguments.png)

1. 「**[!UICONTROL PDF Rasterizer Handler]**」ステップをサイドパネルから「**[!UICONTROL サムネールを処理]**」ステップの下にドラッグします。
1. **[!UICONTROL PDF Rasterizer Handler]**&#x200B;手順で、以下の引数を設定します。

   * MIME タイプ： `application/pdf` または `application/postscript`
   * コマンド: `PDFRasterizer -d -s 1280 -t PNG -i ${file}`
   * サムネールサイズを追加：319:319、140:100、48:48。 必要に応じて、カスタムのサムネール設定を追加します。

   `PDFRasterizer` コマンドのコマンドライン引数には、以下のものがあります。

   * `-d`：テキスト、ベクターアートワークおよび画像のスムーズなレンダリングを有効にするためのフラグより高品質な画像を作成します。 ただし、このパラメーターを指定すると、コマンドの実行速度が遅くなり、画像のサイズが大きくなります。

   * `-s`：画像の最大サイズ（高さまたは幅）これは各ページで DPI に変換されます。ページのサイズが異なる場合、各ページは異なるサイズで拡大/縮小される可能性があります。 デフォルトは実際のページサイズです。

   * `-t`：出力画像のタイプ有効なタイプは、JPEG、PNG、GIF、BMP です。 デフォルト値は JPEG です。

   * `-i`：入力 PDF のパス必須パラメーターです。

   * `-h`: ヘルプ


1. 中間レンディションを削除するには、「**[!UICONTROL 生成されたレンディションを削除]**」を選択します。
1. PDF Rasterizer で web レンディションを生成するには、「**[!UICONTROL Web レンディションを生成]**」を選択します。

   ![generate_web_renditions1](assets/generate_web_renditions1.png)

1. 「**[!UICONTROL Web に対応した画像]**」タブで設定を指定します。

   ![web_enabled_image1](assets/web_enabled_image1.png)

1. ワークフローを保存します。
1. PDF Rasterizer で PDF ライブラリを使用して PDF ページを処理できるようにするには、[!UICONTROL ワークフロー]コンソールから「**[!UICONTROL DAM プロセスのサブアセット]**」モデルを開きます。
1. サイドパネルから、「PDF Rasterizer Handler」手順を 「**[!UICONTROL Web 対応の画像レンディションを作成]**」手順の下にドラッグします。
1. **[!UICONTROL PDF Rasterizer Handler]**&#x200B;手順で、以下の引数を設定します。

   * MIME タイプ： `application/pdf` または `application/postscript`
   * コマンド: `PDFRasterizer -d -s 1280 -t PNG -i ${file}`
   * 追加するサムネールのサイズ：`319:319`、`140:100`、`48:48`必要に応じて、サムネールのカスタム設定を追加します。

   `PDFRasterizer` コマンドのコマンドライン引数には、以下のものがあります。

   * `-d`：テキスト、ベクターアートワークおよび画像のスムーズなレンダリングを有効にするためのフラグより高品質な画像を作成します。 ただし、このパラメーターを指定すると、コマンドの実行速度が遅くなり、画像のサイズが大きくなります。

   * `-s`：画像の最大サイズ（高さまたは幅）これは各ページで DPI に変換されます。ページのサイズが異なる場合、各ページは異なるサイズで拡大/縮小される可能性があります。 デフォルトは実際のページサイズです。

   * `-t`：出力画像のタイプ有効なタイプは、JPEG、PNG、GIF、BMP です。 デフォルト値は JPEG です。

   * `-i`：入力 PDF のパス必須パラメーターです。

   * `-h`: ヘルプ


1. 中間レンディションを削除するには、「**[!UICONTROL 生成されたレンディションを削除]**」を選択します。
1. PDF Rasterizer で web レンディションを生成するには、「**[!UICONTROL Web レンディションを生成]**」を選択します。

   ![generate_web_renditions](assets/generate_web_renditions.png)

1. 「**[!UICONTROL Web に対応した画像]**」タブで設定を指定します。

   ![web_enabled_image-1](assets/web_enabled_image-1.png)

1. ワークフローを保存します。
1. [!DNL Experience Manager Assets] に PDF ファイルまたは AI ファイルをアップロードします。PDF Rasterizer により、ファイルのサムネールと Web レンディションが生成されます。
