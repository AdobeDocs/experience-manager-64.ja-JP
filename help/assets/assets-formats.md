---
title: でサポートされるファイル形式 [!DNL Experience Manager] Assets
description: Assets でサポートされているファイル形式と MIME タイプの一覧と、各形式でサポートされている機能です。
contentOwner: AG
feature: Asset Management,Renditions
role: User,Admin
exl-id: ee25fe8f-36fb-42b3-9f90-0ea77bc02e2f
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '1681'
ht-degree: 57%

---

# でサポートされるファイル形式 [!DNL Adobe Experience Manager Assets] {#assets-supported-formats}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

[!DNL Experience Manager Assets] は幅広いファイル形式をサポートしており、各機能は異なる MIME タイプに様々なサポートを提供しています。

統合する [!DNL Assets] 標準に準拠したその他のデジタルアセット管理 (DAM) ソリューションやデスクトップソフトウェアを使用する場合は、Adobeの Extensible Metadata Platform(XMP) を使用します。

凡例を使用すると、サポートレベルがわかります。

| サポートレベル | 説明 |
|:---:|---|
| ✓ | サポート対象 |
| &#42; | アドオン機能により対応 |
| − | 適用なし |

## ラスターイメージ形式 {#supported-raster-image-formats}

アセット管理機能でサポートされるラスター画像形式は次のとおりです。

| 形式 | ストレージ | メタデータの管理 | メタデータ抽出 | サムネールの生成 | インタラクティブ編集 | メタデータの書き戻し | インサイト |
|---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| PNG | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| GIF | ✓ | ✓ | ✓ | ✓ | ✓ |  | ✓ |
| TIFF | ✓ | ✓ | ✓ | ✓ |  | ✓ | ✓ |
| JPEG | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| BMP | ✓ | ✓ | ✓ | ✓ | ✓ |  | ✓ |
| PNM | ✓ | ✓ |  |  |  |  | ✓ |
| PGM | ✓ | ✓ |  |  |  |  | ✓ |
| PBM | ✓ | ✓ |  |  |  |  | ✓ |
| PPM | ✓ | ✓ |  |  |  |  | ✓ |
| PSD **‡** | ✓ | ✓ | ✓ | ✓ |  |  | ✓ |
| [EPS](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | ✓ | ✓ | ✓ | ✓ |  | ✓ |  |
| PICT |  |  |  |  |  |  | ✓ |
| PSB | ✓ | ✓ | ✓ | ✓ |  |  |  |

**‡** 結合された画像は、画像ファイルからPSDされます。 これは、Adobe Photoshopによって生成され、画像ファイルに含まれるPSDです。 設定によって、結合された画像は実際の画像とは異なる場合があります。

Dynamic Media機能でサポートされるラスター画像形式は次のとおりです。

| 形式 | アップロード<br>（入力形式） | 画像<br>プリセット<br>の作成<br>（出力形式） | 動的<br>レンディション<br>のプレビュー | 動的<br>レンディション<br>の配信 | 動的<br>レンディション<br>のダウンロード |
|---|:---:|:---:|:---:|:---:|:---:|
| PNG | ✓ | ✓ | ✓ | ✓ | ✓ |
| GIF | ✓ | ✓ | ✓ | ✓ | ✓ |
| TIFF | ✓ | ✓ | ✓ | ✓ | ✓ |
| JPEG | ✓ | ✓ | ✓ | ✓ | ✓ |
| BMP | ✓ |  |  |  |  |
| PNM |  |  |  |  |  |
| PGM |  |  |  |  |  |
| PBM |  |  |  |  |  |
| PPM |  |  |  |  |  |
| PSD **‡** | ✓ |  |  |  |  |
| [EPS](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | ✓ | ✓ | ✓ | ✓ | ✓ |
| PICT | ✓ |  |  |  |  |
| PSB |  |  |  |  |  |

**‡** 結合された画像は、画像ファイルからPSDされます。 これは、Adobe Photoshopによって生成され、画像ファイルに含まれるPSDです。 設定によって、結合された画像は実際の画像とは異なる場合があります。

上記の情報に加えて、次の点を考慮してください。

* EPSファイルのサポートは、ラスターイメージにのみ適用されます。 例えば、EPSのベクトル画像のサムネールの生成は、デフォルトではサポートされていません。 サポートを追加するには、[ImageMagick を設定](best-practices-for-imagemagick.md)してください。サードパーティ製のツールを統合して追加機能を有効にするには、[コマンドラインベースのメディアハンドラー](media-handlers.md#command-line-based-media-handler)を参照してください。

* PSB ファイル形式でのメタデータの書き戻しは、`NComm` ハンドラーに追加すると機能するようになります。

* Dynamic Mediaを使用してEPSファイルの動的レンディションをプレビューおよび生成するには、 [Adobe Illustrator(AI)、Postscript(EPS) およびPDFのファイル形式。](../assets/managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats)

* EPS ファイルの場合、メタデータの書き戻しは、PostScript Document Structuring Convention（PS-Adobe）バージョン 3.0 以降でサポートされています。

## Dynamic Mediaでサポートされていないラスターイメージ形式 {#unsupported-image-formats-dynamic-media}

次のリストは、次に示すラスターイメージファイル形式のサブタイプを示しています。 *not* Dynamic Mediaでサポートされています。

関連トピック [Dynamic Mediaでサポートされていないファイル形式を検出する](https://helpx.adobe.com/jp/experience-manager/kb/detect-unsupported-assets-for-dynamic-media.html).

* 100 MB を超える IDAT チャンクサイズを持つ PNG ファイル。
* PSB ファイル。
* CMYK、RGB、グレースケール、ビットマップ以外のカラースペースを持つ PSD ファイルはサポートされません。DuoTone、Lab、インデックス化カラースペースはサポートされません。
* 16 を超えるビット深度を持つ PSD ファイル。
* 浮動小数点データを持つ TIFF ファイル。
* Lab カラースペースを持つ TIFF ファイル。

## PDFRasterizer ライブラリ {#supported-pdf-rasterizer-library}

Adobe PDF Rasterizer ライブラリは、大きくコンテンツを大量に消費するAdobe IllustratorおよびPDFファイル用に、高品質のサムネールとプレビューを生成します。 次のようなファイルで PDF Rasterizer ライブラリを使用することをお勧めします。

* 処理でリソースに負担がかかる、コンテンツ集約型の AI ファイルや PDF ファイル。
* AI/PDFファイル（デフォルトではサムネールは生成されません）。
* Pantone Matching System（PMS）カラーを使用した AI ファイル.

[PDF ラスタライザーの使用](aem-pdf-rasterizer.md)を参照してください。

## 画像トランスコーディングライブラリ {#supported-image-transcoding-library}

Adobe画像トランスコーディングライブラリは、エンコーディング、トランスコーディング、再サンプリング、サイズ変更などの主要な画像処理機能を実行する画像処理ソリューションです。

画像トランスコーディングライブラリは、JPG/JPEG、PNG（8 ビットおよび 16 ビット）、GIF、BMP、TIFF/圧縮TIFF(32 ビットTIFFファイルおよび PTIFF ファイルを除く )、ICO および ICN の MIME タイプをサポートします。

[画像トランスコーディングライブラリ](imaging-transcoding-library.md)を参照してください。

## Camera Raw {#supported-camera-raw}

Adobe Camera Rawライブラリは、 [!DNL Assets] ：生の画像を取り込みます。 詳しくは、 [Camera Rawサポート](camera-raw.md).

## ドキュメント形式 {#supported-document-formats}

アセット管理機能でサポートしているドキュメント形式は、次のとおりです。

| 形式 | ストレージ | メタデータ<br> 管理 | Fulltext<br> 抽出 | メタデータ<br> 抽出 | サムネールの<br>生成 | サブアセット<br> 抽出 | メタデータ<br> 書き戻し |
|---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| [AI](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | ✓ | ✓ |  | ✓ | ✓ | ✓ | ✓ |
| DOC | ✓ | ✓ | ✓ | ✓ |  |  |  |
| DOCX | ✓ | ✓ | ✓ | ✓ |  |  |  |
| ODT | ✓ | ✓ | ✓ |  |  |  |  |
| [PDF](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| HTML | ✓ | ✓ | ✓ |  |  |  |  |
| RTF | ✓ | ✓ | ✓ |  |  |  |  |
| TXT | ✓ | ✓ | ✓ |  |  |  |  |
| XLS | ✓ | ✓ | ✓ |  |  |  |  |
| XLSX | ✓ | ✓ | ✓ | ✓ |  |  |  |
| ODS | ✓ | ✓ | ✓ |  |  |  |  |
| PPT | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |  |
| PPTX | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |  |
| ODP | ✓ | ✓ | ✓ |  |  |  |  |
| [INDD](managing-image-presets.md#indesign-indd-file-format) | ✓ | ✓ |  | ✓ | ✓ | ✓ | ✓ |
| PS | ✓ | ✓ |  |  |  |  |  |
| QXP | ✓ | ✓ |  |  |  |  |  |
| EPUB | ✓ | ✓ |  | ✓ | ✓ |  |  |

Dynamic Mediaの機能でサポートされるドキュメント形式は次のとおりです。

| 形式 | アップロード<br>（入力形式） | 画像<br>プリセット<br>の作成<br>（出力形式） | 動的<br>レンディション<br>のプレビュー | 動的<br>レンディション<br>の配信 | 動的<br>レンディション<br>のダウンロード |
|---|:---:|:---:|:---:|:---:|:---:|
| [AI](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | ✓ |  |  |  |  |
| DOC |  |  |  |  |  |
| DOCX |  |  |  |  |  |
| ODT |  |  |  |  |  |
| [PDF](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats)（下記のメモを参照） | ✓ | ✓ | ✓ | ✓ | ✓ |
| HTML |  |  |  |  |  |
| RTF |  |  |  |  |  |
| TXT |  |  |  |  |  |
| XLS |  |  |  |  |  |
| XLSX |  |  |  |  |  |
| ODS |  |  |  |  |  |
| PPT |  |  |  |  |  |
| PPTX |  |  |  |  |  |
| ODP |  |  |  |  |  |
| [INDD](managing-image-presets.md#indesign-indd-file-format) | ✓ |  |  |  |  |
| PS |  |  |  |  |  |
| QXP |  |  |  |  |  |
| EPUB |  |  |  |  |  |

>[!NOTE]
>
>安全な PDF の場合、アップロードのみがサポートされます。

上記の機能に加えて、次を考慮する必要があります。

* Dynamic Mediaを使用してPDFファイルの動的レンディションを生成するには、 [Adobe Illustrator(AI)、Postscript(EPS) およびPDFのファイル形式。](../assets/managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats)

* Dynamic Mediaを使用して AI ファイルの動的レンディションをプレビューおよび生成するには、 [Adobe Illustrator(AI)、Postscript(EPS) およびPDFのファイル形式。](../assets/managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats)

* INDD ファイルの動的レンディションの生成に Dynamic Media を使用するには、[InDesign（INDD）ファイル形式](../assets/managing-image-presets.md#indesign-indd-file-format)を参照してください。

## マルチメディア形式 {#supported-multimedia-formats}

| 形式 | ストレージ | メタデータの管理 | メタデータ抽出 | サムネールの生成 | FFMPEG トランスコード |
|:---|:---:|:---:|:---:|:---:|:---:|
| AAC | ✓ | ✓ |  | − | &#42; |
| MIDI | ✓ | ✓ |  | − | &#42; |
| 3GP | ✓ | ✓ |  | − | &#42; |
| MP3 | ✓ | ✓ | ✓ | − | &#42; |
| MPG | ✓ | ✓ |  | − | &#42; |
| OGA | ✓ | ✓ |  | − | &#42; |
| OGG | ✓ | ✓ |  | − | &#42; |
| RA | ✓ | ✓ |  | − | &#42; |
| WAV | ✓ | ✓ |  | − | &#42; |
| WMA | ✓ | ✓ |  | − | &#42; |
| DVI | ✓ | ✓ |  | &#42; | &#42; |
| FLV | ✓ | ✓ |  | &#42; | &#42; |
| M4V | ✓ | ✓ |  | &#42; | &#42; |
| MPEG | ✓ | ✓ |  | &#42; | &#42; |
| OGV | ✓ | ✓ |  | &#42; | &#42; |
| MOV | ✓ | ✓ |  | &#42; | &#42; |
| WMV | ✓ | ✓ |  | &#42; | &#42; |
| SWF | ✓ | ✓ |  |  |  |

## Dynamic Mediaトランスコード用の入力ビデオ形式 {#supported-input-video-formats-for-dynamic-media-transcoding}

| ビデオファイル拡張子 | コンテナ | 推奨されるビデオコーデック | サポートされないビデオコーデック |
|---|---|---|---|
| MP4 | MPEG-4 | H264/AVC （すべてのプロファイル） |  |
| MOV、QT | Apple QuickTime | H264/AVC、Apple ProRes422 &amp; HQ、Sony XDCAM、Sony DVCAM、HDV、Panasonic DVCPro、Apple DV（DV25）、Apple PhotoJPEG、Sorenson、Avid DNxHD、Avid AVR | Apple Intermediate、Apple Animation |
| FLV、F4V | AdobeFlash | H264/AVC、Flix VP6、H263、Sorenson | SWF（ベクトルアニメーションファイル） |
| WMV | Windows Media 9 | WMV3(v9)、WMV2(v8)、WMV1(v7)、GoToMeeting(G2M2、G2M3、G2M4) | Microsoft Screen(MSS2)、Microsoft Photo Story(WVP2) |
| MPG、VOB、M2V、MP2 | MPEG-2 | MPEG-2 |  |
| M4V | Apple iTunes | H264/AVC |  |
| AVI | A/V インターリーブ | XVID、DIVX、HDV、MiniDV (DV25)、Techsmith Camtasia、Huffyuv、Fraps、Panasonic DVCPro | Indeo3 (IV30)、MJPEG、Microsoft Video 1 (MS-CRAM) |
| WebM | WebM | Google VP8 |  |
| OGV、OGG | Ogg | シオラ、VP3、ディラク |  |
| MXF | MXF | Sony XDCAM、MPEG-2、MPEG-4、パナソニック DVCPro |  |
| MTS | AVCHD | H264/AVC |  |
| MKV | マトロスカ | H264/AVC |  |
| R3D、RM | 赤い生のビデオ | MJPEG 2000 |  |
| RAM、RM | RealVideo | サポート対象外 | Real G2（RV20）、Real 8（RV30）、Real 10（RV40） |
| FLAC | ネイティブ Flac | 無料の可逆オーディオコーデック |  |
| MJ2 | Motion JPEG 2000 | Motion JPEG 2000 codec |  |

## アーカイブ形式 {#supported-archive-formats}

次の表に、サポートされるアーカイブ形式と、一般的な DAM ワークフローの適用可能性を示します。

| 形式 | ストレージ | バージョン管理 | ワークフロー | 公開 | アクセス制御 | Dynamic Media Delivery |
|---|:---:|:---:|:---:|:---:|:---:|:---:|
| TGZ | ✓ | ✓ | ✓ | ✓ | ✓ |  |
| JAR | ✓ | ✓ | ✓ | ✓ | ✓ |  |
| RAR | ✓ | ✓ | ✓ | ✓ | ✓ |  |
| TAR | ✓ | ✓ | ✓ | ✓ | ✓ |  |
| ZIP **†** | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |

**†** 結合された画像は、画像ファイルからPSDされます。 これは、Adobe Photoshopによって生成され、画像ファイルに含まれるPSDです。 設定によって、結合された画像は実際の画像とは異なる場合があります。を使用して作成された ZIP アーカイブ `Deflate64` AEMでは、アルゴリズムのサポートが制限されています。 アーカイブ操作とアーカイブ解除操作はサポートされていません。 ただし、アップロード、参照、ダウンロードなどの操作はサポートされています。

## その他のサポートされる形式 {#other-supported-formats}

その他のいくつかのファイル形式に対する一般的な DAM ワークフローの適用可能性について、次の表で説明します。

| 形式 | ストレージ | バージョン管理 | ワークフロー | 公開 | アクセス制御 | Dynamic Media Delivery |
|---|:---:|:---:|:---:|:---:|:---:|:---:|
| **#** | ✓ | ✓ | ✓ | ✓ | ✓ |  |
| SVG | ✓ | ✓ | ✓ | ✓ | ✓ |  |
| CSS | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| VTT | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| XML | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| JavaScript（独自の配信ドメインで設定する場合） |  |  |  |  |  | ✓ |

**#** その他の形式は、ストレージ、バージョン管理、ACL、ワークフロー、公開およびメタデータの管理で、DAM でサポートされます。

## サポートされる MIME タイプ {#supported-mime-types}

デフォルトでは、[!DNL Experience Manager] は、ファイル拡張子を使用してファイルタイプを検出します。[!DNL Experience Manager] は、ファイルのコンテンツからこれを検出できます。後者の場合、[!DNL Experience Manager] web コンソールの「[!UICONTROL Day CQ DAM Mime Type Service]」で「[!UICONTROL Detect MIME from content]」オプションを選択します。

サポートされる MIME タイプのリストは、次の場所にあるCRXDE Liteで利用できます。 `/conf/global/settings/cloudconfigs/dmscene7/jcr:content/mimeTypes`.

| ファイル拡張子 | MIME タイプ／インターネットメディアタイプ | デフォルトの jobParam 値 | 許可される jobParam 値 |
|---|---|---|---|
| 画像 | image/s7asset | `usmAmount=1.75&usmRadius=0.2`<br>`&usmThreshold=2&usmMonochrome=0&` | デフォルトの jobParam は、すべての画像の MIME タイプのアセットに適用されます。<ul><li>[knockoutBackgroundOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-knockout-background-options.html?lang=ja)</li><li>[manualCropOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-manual-crop-options.html?lang=ja)</li><li>[autoColorCropOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-auto-color-crop-options.html?lang=ja)</li><li>[autoTransparentCropOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-auto-transparent-crop-options.html?lang=ja)</li><li>[colorManagementOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-color-management-options.html?lang=ja)</li><li>[autoSetCreationOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-auto-set-creation-options.html?lang=ja)</li><li>[emailSetting](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/sting-constants/r-email-settings.html?lang=ja)</li><li>[xmpKeywords](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-xmp-keywords.html?lang=ja)</li><li>[unsharpMaskOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-unsharp-mask-options.html?lang=ja)</li></ul> |
| 3G2 | video/3gpp2 |  | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html?lang=ja) |
| 3GP | video/3gpp |  | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html?lang=ja) |
| AAC | audio/x-aac |  |  |
| AFM | application/x-font-type1 |  |  |
| AI | application/postscript | `aiprocess=Rasterize&airesolution=150`<br>`&aicolorspace=Auto&aialpha=false` | <ul><li>[postScriptOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-post-script-options.html?lang=ja)</li><li> [illustratorOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-illustrator-options.html?lang=ja)</li></ul> |
| AIFF | audio/x-aiff |  |  |
| AVI | video/x-msvideo |  | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html?lang=ja) |
| BMP | image/bmp |  |  |
| CSS | text/css |  |  |
| DOC | application/msword |  |  |
| EPS | <ul><li>application/postscript</li><li>application/eps</li><li>application/x-eps</li><li>image/eps</li><li>image/x-eps</li> |  |  |
| F4V | video/x-f4v |  | ExcludeMasterVideoFromAVS |
| FLA | application/x-shockwave-flash |  |  |
| FLV | video/x-flv |  | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html?lang=ja) |
| FPX | image/vnd.fpx |  |  |
| GIF | image/gif |  |  |
| ICC | application/vnd.iccprofile |  |  |
| ICM | application/vnd.iccprofile |  |  |
| INDD | application/x-indesign |  |  |
| JPEG | image/jpeg |  |  |
| JPG | image/jpeg |  |  |
| M2V | video/mpeg |  | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html?lang=ja) |
| M4V | video/x-m4v |  | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html?lang=ja) |
| MOV | video/quicktime |  | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html?lang=ja) |
| MP3 | audio/mpeg |  |  |
| MP4 | video/mp4 |  | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html?lang=ja) |
| MPEG | video/mpeg |  | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html?lang=ja) |
| MPG | video/mpeg |  | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html?lang=ja) |
| MTS | model/vnd.mts |  |  |
| OGV | video/ogg |  | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html?lang=ja) |
| OTF | application/x-font-otf |  |  |
| PDF | application/pdf | `pdfprocess=Rasterize&resolution=150`<br>`&colorspace=Auto&pdfbrochure=false`<br>`&keywords=false&links=false` | [pdfOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-photoshop-options.html?lang=ja) |
| PFB | application/x-font-type1 |  |  |
| PFM | application/x-font-type1 |  |  |
| PICT | image/x-pict |  |  |
| PNG | image/png |  |  |
| PPT | application/vnd.ms-powerpoint |  |  |
| PS | application/postscript | `psprocess=Rasterize&psresolution=150`<br>`&pscolorspace=Auto&psalpha=false`<br>`&psextractsearchwords=false`<br>`&aiprocess=Rasterize&airesolution=150`<br>`&aicolorspace=Auto&aialpha=false` | <ul><li>[postScriptOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-post-script-options.html?lang=ja)</li><li>[illustratorOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-illustrator-options.html?lang=ja)</li></ul> |
| PSD | image/vnd.adobe.photoshop | `process=None&layerNaming=Layername`<br>`&anchor=Center&createTemplate=false`<br>`&extractText=false&extendLayers=false` | <ul><li>[photoshopOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-photoshop-options.html?lang=ja)</li><li>[photoshopLayerOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-photoshop-layer-options.html?lang=ja)</li></ul> |
| RTF | application/rtf |  |  |
| SVG | image/svg+xml |  |  |
| SWF | application/x-shockwave-flash |  |  |
| TAR | application/x-tar |  |  |
| TIF /TIFF | image/tiff |  |  |
| TTC | application/x-font-ttf |  |  |
| TTF | application/x-font-ttf |  |  |
| VOB | video/dvd |  | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html?lang=ja) |
| VTT | text/vtt |  |  |
| WAV | audio/x-wav |  |  |
| WEBM | video/webm |  | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html?lang=ja) |
| WMA | audio/x-ms-wma |  |  |
| WMV | video/x-ms-wmv |  | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html?lang=ja) |
| XLS | application/vnd.ms-excel |  |  |
| ZIP | application/zip |  |  |

>[!MORELIKETHIS]
>
>* [MIME タイプベースの Assets／Dynamic Media Classic アップロードジョブパラメーターサポートの有効化](/help/sites-administering/scene7.md#enabling-mime-type-based-assets-scene-upload-job-parameter-support).
>* [アップロードジョブパラメーターサポートの MIME タイプベースの設定](config-dynamic.md)を参照してください。

