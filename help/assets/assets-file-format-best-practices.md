---
title: Assets のファイル形式に関するベストプラクティス
description: のファイルサポートのベストプラクティス [!DNL Experience Manager] アセット。
contentOwner: AG
feature: Asset Management,Developer Tools
role: Admin
exl-id: ff739a17-188e-4779-8820-9e4d9b7031d0
source-git-commit: 1679bbab6390808a1988cb6fe9b7692c3db31ae4
workflow-type: tm+mt
source-wordcount: '424'
ht-degree: 17%

---

# Assets のファイル形式に関するベストプラクティス {#assets-file-format-best-practices}

[!DNL Experience Manager Assets] はユーザーの様々なファイルサポート要件に対応するために、アドビ製およびサードパーティ製の数多くのファイル形式ライブラリをサポートしています。サポートされるAdobeライブラリには、Adobe Camera Raw、ギブソン、Adobe PDF Rasterizer、Adobe InDesign Serverなどがあります。 さらに、 [!DNL Assets] は、ImageMagick、TwerbMonkes などのサードパーティライブラリをサポートしています。

サポートされるファイル形式については、[アセットでサポートされるファイル形式](assets-formats.md)を参照してください。

## Adobe Camera Raw Library {#adobe-camera-raw-library}

最適なパフォーマンスを得るには、Adobeでは、次の目的でAdobe Camera Rawライブラリを使用することをお勧めします。

* RAW
* DNG

Adobe Camera Rawライブラリは、入力として CMYK カラープロファイルをサポートします。 ただし、出力はRGBのカラースペースで生成され、出力をJPEG形式でのみサポートします。 サムネール内のソースファイルのカラースペース（CMYK など）は保持されません。

詳しくは、 [Camera Raw支援](camera-raw.md) in [!DNL Assets].

## Adobe PDF Rasterizer ライブラリ {#adobe-pdf-rasterizer-library}

最適な結果を得るには、Adobeは、次のファイルに対してAdobe PDF Rasterizer ライブラリを使用することをお勧めします。

* 大量のコンテンツを集中的に消費するPDF・ファイル
* 標準で生成されていないサムネールを含む AI ファイル
* SPOT (PMS) カラーの AI ファイルの場合

PDFRasterizer を使用して生成されたサムネールとプレビューの画質は、既製のラスター出力に比べて向上します。 Adobe PDF Rasterizer ライブラリは、カラースペースの変換をサポートしていません。 ソースPDFファイルのカラースペースに関係なく、Adobe PDF Rasterizer はRGB出力のみを生成します。

## Adobe InDesign server {#adobe-indesign-cc-server}

Adobeでは、IDML やHTMLなど、Adobe InDesign固有のレンディションを抽出する場合は、Adobe InDesignサーバーを使用することをお勧めします。 詳しくは、 [追加中 [!DNL Experience Manager] Adobe InDesign内の参照としてのアセット](managing-linked-subassets.md#add-aem-assets-as-references-in-adobe-indesign).

## Dynamic Media  {#dynamic-media}

Dynamic Mediaは、グローバルで拡張性が高く、パフォーマンスが最適化されたネットワークを通じて、リッチコンテンツの複数のバリエーションをリアルタイムで生成し、提供します。 インタラクティブな表示エクスペリエンスを提供し、デジタルキャンペーンの管理プロセスを促進します。Dynamic Mediaの有効化について詳しくは、 [Dynamic Mediaの設定](config-dynamic.md).

現在、Dynamic Mediaは、ファイルあたり最大 15 GB のコンテンツに関するビデオをサポートしています。

## ImageMagick ライブラリ {#imagemagick-library}

Adobeでは、次のシナリオで ImageMagick ライブラリの使用をお勧めします。

* EPSファイルのサムネールレンディションを生成するには
* イメージプロファイル情報を保持するとき
* 透明性を保持するとき
* PSD および PSB ファイルを処理するとき

で ImageMagic ライブラリを設定する方法を説明します。 [!DNL Experience Manager]を参照してください。 [ImageMagick の使用](media-handlers.md#an-example-using-imagemagick). 最適な使用方法については、 [ImageMagick の設定のベストプラクティス](best-practices-for-imagemagick.md).

## 画像トランスコーディングライブラリ {#image-transcoding-library}

Adobe画像トランスコーディングライブラリは、画像のエンコーディング、トランスコーディング、再サンプリング、サイズ変更など、主要な画像処理機能を実行する画像処理ソリューションです。

画像トランスコーディングライブラリは、次の MIME タイプをサポートします。

* JPG/JPEG
* PNG（8 ビットおよび 16 ビット）
* GIF
* BMP
* TIFF/圧縮TIFF（32 ビット Tiff と PTiff 以外）。
* ICO
* ICN

詳しくは、[画像トランスコーディングライブラリ](imaging-transcoding-library.md)を参照してください。
