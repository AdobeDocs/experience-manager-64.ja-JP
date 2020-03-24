---
title: デジタルアセットのメタデータの管理
description: メタデータのタイプと、Adobe Experience Manager Assetsがアセットのメタデータを管理し、アセットの分類と整理を簡単にする方法について説明します。 アセットを使用して任意のメタデータを保持および管理できる機能により、Adobe Experience Manager Assetsでは、メタデータに基づいてアセットを自動的に整理および処理できます。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 5ef4c4e42165819191c6e3810c36183110f3f34a

---


# デジタルアセットのメタデータの管理 {#managing-metadata-for-digital-assets}

Adobe Experience Manager Assetsは、すべてのアセットのメタデータを保持します。 これにより、アセットの分類と整理が容易になり、特定のアセットを探している人が役立ちます。 Experience Manager Assetsにアップロードされたファイルからメタデータを抽出する機能により、メタデータ管理はクリエイティブワークフローと統合されます。 Experience Managerの機能を使用して、メタデータを保持し、アセットと共に管理すると、メタデータに基づいてアセットを自動的に整理および処理できます。

* [XMP メタデータ](xmp.md)
* [メタデータの編集と追加](meta-edit.md)
* [メタデータのスキーマに関する参照情報](meta-ref.md)

## メタデータが必要な理由 {#why-we-need-metadata}

メタデータとは、データに関する情報のことです。この場合、データとは、画像などのデジタルアセットを指します。 メタデータは、効率的なアセット管理のために重要です。

メタデータは、アセットで使用できるすべてのデータの集まりですが、その画像に必ずしも含まれているとは限りません。 メタデータの例を次に示します。

* アセットの名前。
* 最終変更の日時。
* リポジトリに保存されたアセットのサイズ。
* 格納先のフォルダの名前。
* 関連するアセットまたは適用されたタグ。

これらは、Experience Managerで管理できる基本的なメタデータプロパティで、最終変更日別に並べ替えられたアセットなど、すべてのアセットを表示できます。これは、リポジトリに最近追加されたアセットを見つける場合に役立ちます。

デジタルアセットに、次のようなさらに詳細なデータを追加できます。

* アセットのタイプ（画像、ビデオ、オーディオクリップ、またはドキュメント）。
* アセットの所有者。
* アセットのタイトル。
* アセットの説明。
* アセットに割り当てられたタグ。

メタデータが多いほど、アセットをより細かく分類でき、デジタル情報量が大きくなるにつれ便利です。数百個のファイルをファイル名に基づいて管理できます。 ただし、このアプローチは拡張性が低く、関与する人の数や管理する資産の数が増えるとすぐに不足します。

アセットにメタデータが追加されると、アセットの値は大きくなります。これは、アセットが

* アクセスのしやすさ - 検索が容易になります.
* 管理のしやすさ - 一連の同じプロパティを持つアセットを容易に検索し、これらのアセットに変更を適用できます.
* より高い複雑性 - アセットに追加するメタデータが多くなるほど、メタデータの管理がより重要になります.

このような理由から、Experience Manager Assetsでは、デジタルアセットのメタデータを作成、管理および交換する適切な方法を提供します。

## メタデータのタイプ {#types-of-metadata}

基本的な2種類のメタデータは、技術的なメタデータと説明的なメタデータです。

テクニカルメタデータは、デジタルアセットを操作しているソフトウェアアプリケーションで役に立つもので、手動で管理できません。Experience Manager Assetsおよび他のソフトウェアは、技術的なメタデータを自動的に判定し、アセットが変更されるとメタデータが変更される場合があります。 アセットで使用可能なテクニカルメタデータは、主にアセットのファイルタイプによって決まります。技術的なメタデータの例を以下に示します。

* ファイルのサイズ
* 画像の寸法（高さと幅）
* オーディオまたはビデオファイルのビットレート
* 画像の解像度（詳細レベル）

記述メタデータは、アセットが属するビジネスなど、アプリケーションドメインに関するメタデータです。記述メタデータは自動で定義できません。手動または半自動で作成されます。 例えば、GPS対応のカメラでは、緯度と経度を自動的に追跡し、画像に地理タグを追加できます。

記述メタデータ情報の作成にかかる手動作業はコストが高いので、ソフトウェアシステムと組織との間でメタデータのやり取りを容易にするための規格が確立されています。

Experience Manager Assetsは、メタデータ管理に関連するすべての標準をサポートしています。

メタデータは重要なもので、メタデータの作成には膨大な手動作業を必要とするので、やり取りを容易にするための規格が確立されています。

## Encoding standards {#encoding-standards}

メタデータをファイルに埋め込む方法は様々です。 エンコーディング規格は、次の中から選択できます。

* XMP:抽出されたメタデータをリポジトリに格納するためにExperience Manager Assetsで使用されます。
* ID3：オーディオファイルおよびビデオファイル用の規格です。
* Exif:（画像ファイル用）。
* その他/レガシー：Microsoft Word、PowerPoint、Excelなどから

### XMP {#xmp}

XMP(Extensible Metadata Platform)は、Experience Manager Assetsですべてのメタデータ管理に使用されるオープンスタンダードです。 この標準では、すべてのファイル形式に埋め込むことのできるユニバーサルメタデータエンコーディングを提供しています。 アドビや他の会社は、リッチコンテンツモデルを提供するXMP標準をサポートしています。 XMP標準およびExperience Manager Assetsのユーザーは、強力なプラットフォームを基盤としています。 詳しくは、 [XMPを参照してください](https://www.adobe.com/products/xmp.html)。

### ID3 {#id}

これらの ID3 タグに格納されたデータは、コンピューターまたはポータブル MP3 プレーヤー上でデジタルオーディオファイルの再生時に表示されます。

ID3 タグは、MP3 ファイルフォーマット用に設計されています。各フォーマットのその他の情報：

* ID3タグは、MP3およびmp3PROファイルで機能します。
* WAV ではタグが使用されません。
* WMAには、オープンソース実装を許可しない独自のタグがあります。
* Ogg Vorbis では、Ogg コンテナに埋め込まれた Xiph コメントを使用します。
* AAC では独自のタグフォーマットが使用されます。

### Exif {#exif}

Exif(Exchangeable image file format)は、デジタル写真で最も人気の高いメタデータ形式です。 JPEG、TIFF、RIFF、WAVなど、多くのファイル形式でメタデータプロパティの固定語彙を埋め込む方法を提供します。 Exifは、メタデータをメタデータ名とメタデータ値のペアとして保存します。 これらのメタデータの名前と値のペアはタグとも呼ばれ、Experience Managerのタグと混同しないでください。 Exifは最新のデジタルカメラで自動的に作成され、最新のグラフィックソフトウェアを通じてサポートされるので、メタデータ管理の最も低い共通要素と見なすことができます。

Exifの主な制限は、BMP、GIF、PNGなどの一般的な画像ファイル形式ではサポートされないことです。

通常、Exifで定義されるメタデータフィールドは技術的な性質を持ち、説明的なメタデータ管理には限られています。 このため、Experience Manager Assetsでは、Exifプロパティの共通メタデータスキーマへのマッピ [ングと](metadata-schemas.md) XMPへのマッピングを提供 [します](xmp-writeback.md)。

### Other metadata {#other-metadata}

ファイルから埋め込むことのできるその他のメタデータには、Microsoft Word、PowerPoint、Excelなどがあります。

## Metadata schemata {#metadata-schemata}

メタデータスキーマは、様々なアプリケーションで使用できるメタデータプロパティ定義の定義済みセットです。 プロパティは常にアセットと関連付けられています。つまり、プロパティはリソースの「説明」です。

必要に応じて独自のメタデータスキーマが存在しない場合は、独自のメタデータスキーマを設計することもできます。 既存の情報を複製しない。 組織内でスキーマを分割すると、メタデータの共有が容易になります。 Experience Managerには、最も人気の高いメタデータスキーマのデフォルトのリストが表示されます。 このリストを使用すると、メタデータ戦略をすばやく開始し、必要なメタデータプロパティをすばやく選択できます。

サポートされるメタデータスキーマを以下に示します。

### Standard metadata {#standard-metadata}

* dc - Dublin Core - 最も重要で広く使用されるメタデータのセット.
* DICOM - Digital Imaging and Communications in Medicine.
* Iptc4xmpCore &amp; iptc4xmpExt - International Press Communications Standard — 多数のサブジェクト固有のメタデータ。
* rdf - Resource Description Framework - 汎用のセマンティック Web メタデータ用.
* xmp - Extensible Metadata Platform.
* xmpBJ - Basic Job Ticketing.

### Application-specific metadata {#application-specific-metadata}

アプリケーション固有のメタデータは、技術的および説明的なメタデータを含む。 これらのメタデータを使用すると、他のアプリケーションでそのメタデータを使用することはできません。例えば、Adobe Photoshopメタデータを持つアセットがあり、別の画像レンダリングアプリケーションがそのメタデータにアクセスしようとすると、そのメタデータにアクセスできない場合があります。 アセットに多くのアプリケーション固有のメタデータが含まれている場合は、アプリケーション固有のプロパティを標準のプロパティに変更するワークフロー手順を作成できます。

* acdsee - metadata managed by the ACDSee program [www.acdsee.com/](https://www.acdsee.com/).
* album - Adobe Photoshop アルバム.
* cq - Experience Manager Assetsで使用されます。
* dam - Experience Manager Assetsで使用されます。
* dex - Optima SC Description Explorer.
* crs - Adobe Photoshop Camera Raw.
* lr - Adobe Lightroom.
* mediapro - iView MediaPro.
* MicrosoftPhoto、MP - Microsoft Photo.
* pdf、pdfx
* photoshop、psAux - Adobe Photoshop

### Digital Rights Management metadata {#digital-rights-management-metadata}

* cc - クリエイティブコモンズ
* xmpRights
* plus - Picture Licensing Universal System - https://www.useplus.com/
* prism - https://www.idealliance.org/prism-metadata Publishing Requirements for Industry Standard Metadata
* prl - Prism Rights Language
* pur - Prism Usage Rights
* xmpPlus - PLUS と XMP との統合

### Photography-specific metadata {#photography-specific-metadata}

* exif - カメラからの数多くのテクニカル情報（GPS 位置など）
* crs - Photoshop Camera Raw
* Iptc4xmpCoreとiptc4xmpExt
* TIFF - 画像メタデータ（TIFF 画像に限りません）

### Print-specific metadata {#print-specific-metadata}

* pdfおよびpdfx - Adobe PDFおよびサードパーティアプリケーション
* prism - [www.prismstandard.org](https://www.prismstandard.org) Publishing Requirements for Industry Standard Metadata
* xmp
* xmpPG - ページ化されたテキスト用の xmp

### Multimedia-specific metadata {#multimedia-specific-metadata}

* xmpDM - Dynamic Media
* xmpMM - Media Management

## Metadata-driven workflows {#metadata-driven-workflows}

メタデータ主導型のワークフローを作成すると、一部のプロセスを自動化でき、効率が向上します。 メタデータ駆動型のワークフローでは、ワークフロー管理システムでワークフローが読み取られ、その結果、事前定義された動作が実行されます。例として、メタデータ駆動型のワークフローの使用方法をいくつか示します。

* ワークフローで、画像にタイトルがあるかどうかをチェックできます。タイトルがない場合、タイトルを追加するよう特定のユーザーに通知されます。
* ワークフローで、アセットの著作権情報によって配布が許可されているかどうかをチェックできます。許可されている場合、アセットが 1 つのサーバーに送信されます。許可されていない場合、アセットが別のサーバーに送信されます。
* ワークフローは、事前定義された必須のメタデータがないか、無効なメタデータが含まれているかをチェ *ックで* きます。
