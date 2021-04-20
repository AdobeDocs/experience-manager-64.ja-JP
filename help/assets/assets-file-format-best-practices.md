---
title: Assets のファイル形式に関するベストプラクティス
description: AEM Assets のファイルサポートに関するベストプラクティスを紹介します。
contentOwner: AG
feature: Asset Management,Developer Tools
role: Administrator
translation-type: tm+mt
source-git-commit: 29e3cd92d6c7a4917d7ee2aa8d9963aa16581633
workflow-type: tm+mt
source-wordcount: '438'
ht-degree: 91%

---


# Assets のファイル形式に関するベストプラクティス {#assets-file-format-best-practices}

AEM Assets はユーザーの様々なファイルサポート要件に対応するために、アドビ製およびサードパーティ製の数多くのファイル形式ライブラリをサポートしています。サポート対象のアドビのライブラリには、Adobe Camera Raw、Gibson、Adobe PDF Rasterizer、Adobe InDesign Server などがあります。さらに、AEM Assets は ImageMagick や TwelveMonkeys などのサードパーティのライブラリをサポートします。

サポートされるファイル形式については、[アセットでサポートされるファイル形式](assets-formats.md)を参照してください。

## Adobe Camera Raw ライブラリ  {#adobe-camera-raw-library}

最適なパフォーマンスを得るために、以下については Adobe Camera Raw ライブラリを使用することをお勧めします。

* RAW
* DNG

Adobe Camera Raw ライブラリは、入力として CMYK カラープロファイルをサポートします。ただし、出力は RGB カラースペースで生成され、JPEG 形式の出力のみがサポートされます。サムネールにはソースファイルのカラースペース（CMYK など）は保持されません。

詳しくは、AEM Assets の [Camera Raw サポート](camera-raw.md)を参照してください。

## Adobe PDF Rasterizer ライブラリ {#adobe-pdf-rasterizer-library}

最適な結果を得るために、次のファイルで Adobe PDF Rasterizer ライブラリを使用することをお勧めします。

* サイズが大きくコンテンツが多い PDF ファイル
* 追加設定なしでは生成されないサムネールがある AI ファイル
* SPOT（PMS）カラーの AI ファイル

PDF Rasterizer を使用して生成されたサムネールやプレビューの画質は、既製のラスター出力と比較して優れています。Adobe PDF Rasterizer ライブラリはカラースペース変換をサポートしません。ソース PDF ファイルのカラースペースに関わらず、Adobe PDF Rasterizer は RGB 出力のみを生成します。

## Adobe InDesign Server  {#adobe-indesign-cc-server}

IDML や HTML など Adobe InDesign 固有のレンディションを抽出するには、Adobe InDesign Server の使用をお勧めします。詳しくは、「[Adobe InDesign](managing-linked-subassets.md#add-aem-assets-as-references-in-adobe-indesign)でAEMアセットを参照として追加する」を参照してください。

## Dynamic Media  {#dynamic-media}

Dynamic Media は、パフォーマンスが最適化されスケーラビリティに優れたグローバルネットワーク経由で、様々なバリエーションのリッチコンテンツをリアルタイムで生成および配信します。インタラクティブな表示エクスペリエンスを提供し、デジタルキャンペーンの管理プロセスを促進します。Dynamic Media の有効化について詳しくは、[Dynamic Media の設定](config-dynamic.md)を参照してください。

現在、Dynamic Media では、1 ファイルにつき最大 15 GB のコンテンツのビデオをサポートしています。

## ImageMagick ライブラリ {#imagemagick-library}

次のシナリオについては、ImageMagick ライブラリの使用をお勧めします。

* EPS ファイルのサムネールのレンディションを生成するとき
* イメージプロファイル情報を保持するとき
* 透明性を保持するとき
* PSD および PSB ファイルを処理するとき

AEMでのImageMagicライブラリの設定方法について詳しくは、[Using ImageMagick](media-handlers.md#an-example-using-imagemagick)を参照してください。 最適な使用方法については、[ImageMagick の設定のベストプラクティス](best-practices-for-imagemagick.md)を参照してください。

## 画像トランスコーディングライブラリ  {#image-transcoding-library}

アドビの画像トランスコーディングライブラリは、画像のエンコーディング、トランスコーディング、リサンプリング、サイズ変更などの中心的な画像処理機能を実行する画像処理ソリューションです。

画像トランスコーディングライブラリは、以下の MIME タイプをサポートします。

* JPG／JPEG
* PNG（8 ビットおよび 16 ビット）
* GIF
* BMP
* TIFF／圧縮 TIFF（32 ビット TIFF、PTIFF 以外）。
* ICO
* ICN

詳しくは、[イメージングトランスコードライブラリ](imaging-transcoding-library.md)を参照してください。
