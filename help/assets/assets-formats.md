---
title: でサポートされるファイル形式 [!DNL Experience Manager] Assets
description: Assets でサポートされているファイル形式と MIME タイプの一覧と、各形式でサポートされている機能です。
contentOwner: AG
feature: Asset Management,Renditions
role: User,Admin
exl-id: ee25fe8f-36fb-42b3-9f90-0ea77bc02e2f
source-git-commit: cc6de21180c9fff74f7d64067db82f0c11ac9333
workflow-type: tm+mt
source-wordcount: '1635'
ht-degree: 59%

---

# でサポートされるファイル形式 [!DNL Adobe Experience Manager Assets] {#assets-supported-formats}

[!DNL Experience Manager Assets] は幅広いファイル形式をサポートしており、各機能は異なる MIME タイプに様々なサポートを提供しています。

統合する [!DNL Assets] 標準に準拠したその他のデジタルアセット管理 (DAM) ソリューションやデスクトップソフトウェアを使用する場合は、Adobeの Extensible Metadata Platform(XMP) を使用します。

凡例を使用すると、サポートレベルがわかります。

| サポートレベル | 説明 |
|:---:|---|
| ✓ | サポート対象 |
| * | アドオン機能により対応 |
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

**‡** 結合された画像は、画像ファイルからPSDされます。 この画像は Adobe Photoshop によって生成され、PSD ファイルに含まれます。設定によって、結合された画像は実際の画像である場合とそうでない場合があります。

Dynamic Media機能でサポートされるラスター画像形式は次のとおりです。

| 形式 | アップロード<br> （入力形式） | 作成<br> 画像<br> プリセット<br> （出力形式） | プレビュー<br> 動的<br> rendition | 配信<br> 動的<br> rendition | ダウンロード<br> 動的<br> rendition |
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

**‡** 結合された画像は、画像ファイルからPSDされます。 この画像は Adobe Photoshop によって生成され、PSD ファイルに含まれます。設定によって、結合された画像は実際の画像である場合とそうでない場合があります。

上記の情報に加えて、以下を考慮してください。

* EPS ファイルのサポートは画像のラスタライズにのみ適用されます。例えば、EPS ベクター画像のサムネールの生成はデフォルトではサポートされません。サポートを追加するには、[ImageMagick](best-practices-for-imagemagick.md) を設定してください。サードパーティツールを統合して追加機能を有効にするには、 [コマンドラインベースのメディアハンドラー](media-handlers.md#command-line-based-media-handler).

* PSB ファイル形式が PSB ファイルに追加された場合、メタデータの書き戻しが機能します。 `NComm` ハンドラ

* EPS ファイルの動的レンディションのプレビューと生成に Dynamic Media を使用するには、[Adobe Illustrator（AI）、Postscript（EPS）および PDF ファイル形式](../assets/managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats)を参照してください。

* EPS ファイルの場合、メタデータの書き戻しは、PostScript Document Structuring Convention（PS-Adobe）バージョン 3.0 以降でサポートされています。

## Dynamic Mediaでサポートされていないラスターイメージ形式 {#unsupported-image-formats-dynamic-media}

次のリストは、次に示すラスターイメージファイル形式のサブタイプを示しています。 *not* Dynamic Mediaでサポートされています。

関連トピック [Dynamic Mediaでサポートされていないファイル形式を検出する](https://helpx.adobe.com/experience-manager/kb/detect-unsupported-assets-for-dynamic-media.html).

* 100 MB を超える IDAT チャンクサイズを持つ PNG ファイル。
* PSB ファイル。
* CMYK、RGB、グレースケール、ビットマップ以外のカラースペースを持つ PSD ファイルはサポートされません。DuoTone、Lab、インデックス化カラースペースはサポートされません。
* 16 を超えるビット深度を持つ PSD ファイル。
* 浮動小数点データを持つ TIFF ファイル。
* Lab カラースペースを持つ TIFF ファイル。

## PDFRasterizer ライブラリ {#supported-pdf-rasterizer-library}

Adobe PDF Rasterizer ライブラリは、サイズが大きくコンテンツが多い Adobe Illustrator ファイルおよび PDF ファイルの高品質のサムネールとプレビューを生成します。次のようなファイルで PDF Rasterizer ライブラリを使用することをお勧めします。

* 処理にリソースを大量に消費する、コンテンツを集中的に消費する AI/PDFファイル。
* AI／PDF ファイル。デフォルトではサムネールは生成されません。
* Pantone Matching System（PMS）カラーを使用した AI ファイル.

詳しくは、 [Rasterizer のPDF](aem-pdf-rasterizer.md).

## 画像トランスコーディングライブラリ {#supported-image-transcoding-library}

Adobe画像トランスコーディングライブラリは、エンコーディング、トランスコーディング、再サンプリング、サイズ変更などの主要な画像処理機能を実行する画像処理ソリューションです。

画像トランスコーディングライブラリは、JPG/JPEG、PNG（8 ビットおよび 16 ビット）、GIF、BMP、TIFF/圧縮TIFF(32 ビットTIFFファイルおよび PTIFF ファイルを除く )、ICO および ICN の MIME タイプをサポートします。

詳しくは、 [画像トランスコーディングライブラリ](imaging-transcoding-library.md).

## Camera Raw {#supported-camera-raw}

Adobe Camera Rawライブラリは、 [!DNL Assets] ：生の画像を取り込みます。 詳しくは、 [Camera Rawサポート](camera-raw.md).

## ドキュメント形式 {#supported-document-formats}

アセット管理機能でサポートされるドキュメント形式は次のとおりです。

| 形式 | ストレージ | メタデータ<br> 管理 | Fulltext<br> 抽出 | メタデータ<br> 抽出 | サムネール<br> 生成 | サブアセット<br> 抽出 | メタデータ<br> 書き戻し |
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

| 形式 | アップロード<br> （入力形式） | 作成<br> 画像<br> プリセット<br> （出力形式） | プレビュー<br> 動的<br> rendition | 配信<br> 動的<br> rendition | ダウンロード<br> 動的<br> rendition |
|---|:---:|:---:|:---:|:---:|:---:|
| [AI](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | ✓ |  |  |  |  |
| DOC |  |  |  |  |  |
| DOCX |  |  |  |  |  |
| ODT |  |  |  |  |  |
| [PDF](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | ✓ | ✓ | ✓ | ✓ | ✓ |
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
| ePub |  |  |  |  |  |

上記の機能に加えて、次のことを考慮してください。

* PDF ファイルの動的レンディションの生成に Dynamic Media を使用するには、[Adobe Illustrator（AI）、Postscript（EPS）および PDF ファイル形式](../assets/managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats)を参照してください。

* AI ファイルの動的レンディションのプレビューと生成に Dynamic Media を使用するには、[Adobe Illustrator（AI）、Postscript（EPS）および PDF ファイル形式](../assets/managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats)を参照してください。

* Dynamic Mediaを使用して INDD ファイルの動的レンディションを生成するには、 [InDesign(INDD) ファイル形式](../assets/managing-image-presets.md#indesign-indd-file-format).

## マルチメディア形式 {#supported-multimedia-formats}

| 形式 | ストレージ | メタデータの管理 | メタデータ抽出 | サムネールの生成 | FFMPEG トランスコーディング |
|:---|:---:|:---:|:---:|:---:|:---:|
| AAC | ✓ | ✓ |  | - | * |
| MIDI | ✓ | ✓ |  | - | * |
| 3GP | ✓ | ✓ |  | - | * |
| MP3 | ✓ | ✓ | ✓ | - | * |
| MPG | ✓ | ✓ |  | - | * |
| OGA | ✓ | ✓ |  | - | * |
| OGG | ✓ | ✓ |  | - | * |
| RA | ✓ | ✓ |  | - | * |
| WAV | ✓ | ✓ |  | - | * |
| WMA | ✓ | ✓ |  | - | * |
| DVI | ✓ | ✓ |  | * | * |
| FLV | ✓ | ✓ |  | * | * |
| M4V | ✓ | ✓ |  | * | * |
| MPEG | ✓ | ✓ |  | * | * |
| OGV | ✓ | ✓ |  | * | * |
| MOV | ✓ | ✓ |  | * | * |
| WMV | ✓ | ✓ |  | * | * |
| SWF | ✓ | ✓ |  |  |  |

## Dynamic Mediaトランスコード用の入力ビデオ形式 {#supported-input-video-formats-for-dynamic-media-transcoding}

| ビデオファイル拡張子 | コンテナ | 推奨されるビデオコーデック | サポートされないビデオコーデック |
|---|---|---|---|
| MP4 | MPEG-4 | H264/AVC（すべてのプロファイル） |  |
| MOV、QT | Apple QuickTime | H264/AVC、Apple ProRes422 &amp; HQ、Sony XDCAM、Sony DVCAM、HDV、Panasonic DVCPro、Apple DV（DV25）、Apple PhotoJPEG、Sorenson、Avid DNxHD、Avid AVR | Apple Intermediate、Apple Animation |
| FLV、F4V | Adobe Flash | H264/AVC、Flix VP6、H263、Sorenson | SWF（ベクターアニメーションファイル） |
| WMV | Windows Media 9 | WMV3（v9）、WMV2（v8）、WMV1（v7）、GoToMeeting（G2M2、G2M3、G2M4） | Microsoft Screen（MSS2）、Microsoft Photo Story（WVP2） |
| MPG、VOB、M2V、MP2 | MPEG-2 | MPEG-2 |  |
| M4V | Apple iTunes | H264/AVC |  |
| AVI | A/V Interleave | XVID、DIVX、HDV、MiniDV（DV25）、Techsmith Camtasia、Huffyuv、Fraps、Panasonic DVCPro | Indeo3（IV30）、MJPEG、Microsoft Video 1（MS-CRAM） |
| WebM | WebM | Google VP8 |  |
| OGV、OGG | Ogg | Theora、VP3、Dirac |  |
| MXF | MXF | Sony XDCAM、MPEG-2、MPEG-4、Panasonic DVCPro |  |
| MTS | AVCHD | H264/AVC |  |
| MKV | Matroska | H264/AVC |  |
| R3D、RM | Red Raw Video | MJPEG 2000 |  |
| RAM、RM | RealVideo | サポート対象外 | Real G2（RV20）、Real 8（RV30）、Real 10（RV40） |
| FLAC | Native Flac | Free lossless audio codec |  |
| MJ2 | Motion JPEG 2000 | Motion JPEG 2000 codec |  |

## アーカイブ形式 {#supported-archive-formats}

サポートされるアーカイブ形式と一般的な DAM ワークフローの適用性については、次の表で説明します。

| 形式 | ストレージ | バージョン管理 | ワークフロー | 公開 | アクセス制御 | Dynamic Media の配信 |
|---|:---:|:---:|:---:|:---:|:---:|:---:|
| TGZ | ✓ | ✓ | ✓ | ✓ | ✓ |  |
| JAR | ✓ | ✓ | ✓ | ✓ | ✓ |  |
| RAR | ✓ | ✓ | ✓ | ✓ | ✓ |  |
| TAR | ✓ | ✓ | ✓ | ✓ | ✓ |  |
| ZIP **†** | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |

**†** 結合された画像は、画像ファイルからPSDされます。 この画像は Adobe Photoshop によって生成され、PSD ファイルに含まれます。設定によって、結合された画像は実際の画像である場合とそうでない場合があります。を使用して作成された ZIP アーカイブ `Deflate64` AEMでは、アルゴリズムのサポートが制限されています。 アーカイブ操作とアーカイブ解除操作はサポートされていません。 アップロード、参照、ダウンロードなどの操作はサポートされています。

## その他のサポートされる形式 {#other-supported-formats}

他のいくつかのファイル形式に対する一般的な DAM ワークフローの適用性については、以下の表で説明します。

| 形式 | ストレージ | バージョン管理 | ワークフロー | 公開 | アクセス制御 | Dynamic Media の配信 |
|---|:---:|:---:|:---:|:---:|:---:|:---:|
| **#** | ✓ | ✓ | ✓ | ✓ | ✓ |  |
| SVG | ✓ | ✓ | ✓ | ✓ | ✓ |  |
| CSS | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| VTT | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| XML | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| JavaScript（独自の配信ドメインで設定する場合） |  |  |  |  |  | ✓ |

**#** その他の形式は、ストレージ、バージョン管理、ACL、ワークフロー、公開およびメタデータの管理で、DAM でサポートされます。

## サポートされる MIME タイプ {#supported-mime-types}

デフォルトでは、 [!DNL Experience Manager] は、ファイル拡張子を使用してファイルタイプを検出します。 [!DNL Experience Manager] は、ファイルの内容からこれを検出できます。 後者の場合は、「 [!UICONTROL コンテンツから MIME を検出] オプション [!UICONTROL Day CQ DAM Mime Type Service] 内 [!DNL Experience Manager] Web コンソール。

サポートされる MIME タイプのリストは、次の場所にあるCRXDE Liteで利用できます。 `/conf/global/settings/cloudconfigs/dmscene7/jcr:content/mimeTypes`.

| ファイル拡張子 | MIME タイプ／インターネットメディアタイプ | デフォルトの jobParam 値 | 許可される jobParam 値 |
|---|---|---|---|
| 画像 | image/s7asset | `usmAmount=1.75&usmRadius=0.2`<br>`&usmThreshold=2&usmMonochrome=0&` | デフォルトの jobParam は、すべての画像の MIME タイプのアセットに適用されます。<ul><li>[knockoutBackgroundOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-knockout-background-options.html)</li><li>[manualCropOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-manual-crop-options.html)</li><li>[autoColorCropOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-auto-color-crop-options.html)</li><li>[autoTransparentCropOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-auto-transparent-crop-options.html)</li><li>[colorManagementOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-color-management-options.html)</li><li>[autoSetCreationOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-auto-set-creation-options.html)</li><li>[emailSetting](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/sting-constants/r-email-settings.html)</li><li>[xmpKeywords](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-xmp-keywords.html)</li><li>[unsharpMaskOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-unsharp-mask-options.html)</li></ul> |
| 3G2 | video/3gpp2 |  | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| 3GP | video/3gpp |  | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| AAC | audio/x-aac |  |  |
| AFM | application/x-font-type1 |  |  |
| AI | application/postscript | `aiprocess=Rasterize&airesolution=150`<br>`&aicolorspace=Auto&aialpha=false` | <ul><li>[postScriptOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-post-script-options.html)</li><li> [illustratorOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-illustrator-options.html)</li></ul> |
| AIFF | audio/x-aiff |  |  |
| AVI | video/x-msvideo |  | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| BMP | image/bmp |  |  |
| CSS | text/css |  |  |
| DOC | application/msword |  |  |
| EPS | <ul><li>application/postscript</li><li>application/eps</li><li>application/x-eps</li><li>image/eps</li><li>image/x-eps</li> |  |  |
| F4V | video/x-f4v |  | ExcludeMasterVideoFromAVS |
| FLA | application/x-shockwave-flash |  |  |
| FLV | video/x-flv |  | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| FPX | image/vnd.fpx |  |  |
| GIF | image/gif |  |  |
| ICC | application/vnd.iccprofile |  |  |
| ICM | application/vnd.iccprofile |  |  |
| INDD | application/x-indesign |  |  |
| JPEG | image/jpeg |  |  |
| JPG | image/jpeg |  |  |
| M2V | video/mpeg |  | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| M4V | video/x-m4v |  | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| MOV | video/quicktime |  | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| MP3 | audio/mpeg |  |  |
| MP4 | video/mp4 |  | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| MPEG | video/mpeg |  | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| MPG | video/mpeg |  | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| MTS | model/vnd.mts |  |  |
| OGV | video/ogg |  | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| OTF | application/x-font-otf |  |  |
| PDF | application/pdf | `pdfprocess=Rasterize&resolution=150`<br>`&colorspace=Auto&pdfbrochure=false`<br>`&keywords=false&links=false` | [pdfOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-photoshop-options.html) |
| PFB | application/x-font-type1 |  |  |
| PFM | application/x-font-type1 |  |  |
| PICT | image/x-pict |  |  |
| PNG | image/png |  |  |
| PPT | application/vnd.ms-powerpoint |  |  |
| PS | application/postscript | `psprocess=Rasterize&psresolution=150`<br>`&pscolorspace=Auto&psalpha=false`<br>`&psextractsearchwords=false`<br>`&aiprocess=Rasterize&airesolution=150`<br>`&aicolorspace=Auto&aialpha=false` | <ul><li>[postScriptOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-post-script-options.html)</li><li>[illustratorOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-illustrator-options.html)</li></ul> |
| PSD | image/vnd.adobe.photoshop | `process=None&layerNaming=Layername`<br>`&anchor=Center&createTemplate=false`<br>`&extractText=false&extendLayers=false` | <ul><li>[photoshopOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-photoshop-options.html)</li><li>[photoshopLayerOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-photoshop-layer-options.html)</li></ul> |
| RTF | application/rtf |  |  |
| SVG | image/svg+xml |  |  |
| SWF | application/x-shockwave-flash |  |  |
| TAR | application/x-tar |  |  |
| TIF / TIFF | image/tiff |  |  |
| TTC | application/x-font-ttf |  |  |
| TTF | application/x-font-ttf |  |  |
| VOB | video/dvd |  | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| VTT | text/vtt |  |  |
| WAV | audio/x-wav |  |  |
| WEBM | video/webm |  | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| WMA | audio/x-ms-wma |  |  |
| WMV | video/x-ms-wmv |  | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| XLS | application/vnd.ms-excel |  |  |
| ZIP | application/zip |  |  |

>[!MORELIKETHIS]
>
>* [MIME タイプベースの Assets/Dynamic Media Classicアップロードジョブパラメーターサポートの有効化](/help/sites-administering/scene7.md#enabling-mime-type-based-assets-scene-upload-job-parameter-support).
>* [アップロードジョブパラメーターサポートの MIME タイプベースの設定](config-dynamic.md).

