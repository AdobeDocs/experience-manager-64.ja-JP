---
title: ' [!DNL Adobe Experience Manager] でのデジタルアセットのメタデータ管理'
description: メタデータのタイプと方法について説明します [!DNL Adobe Experience Manager Assets] は、アセットのメタデータを管理して、アセットの分類と整理を容易におこなえるようにします。 [!DNL Experience Manager] を使用すると、メタデータに基づいてアセットを自動的に整理および処理できます。
contentOwner: AG
feature: Tagging, Metadata
role: Architect, Leader
exl-id: 05bbf89a-4cf5-49bb-aea8-a585c641eda2
source-git-commit: fc725206728e238ab9da1fb30cee8fb407257b62
workflow-type: tm+mt
source-wordcount: '1409'
ht-degree: 97%

---

# デジタルアセットのメタデータの管理 {#managing-metadata-for-digital-assets}

[!DNL Adobe Experience Manager Assets] では、あらゆるアセットのメタデータを保持します。したがって、アセットの分類と編成が容易にでき、特定のアセットを検索しやすくなります。メタデータ管理は、[!DNL Experience Manager Assets] にアップロードされるファイルからメタデータを抽出する機能と共に、クリエイティブワークフローに統合されます。アセットの任意のメタデータを保持して管理する機能によって、メタデータに基づいてアセットを自動的に編成および処理できます。

* [XMP メタデータ](xmp.md)。
* [メタデータの編集と追加](meta-edit.md).
* [メタデータのスキーマに関する参照情報](meta-ref.md).

## メタデータが必要な理由 {#why-we-need-metadata}

メタデータとは、データに関する情報のことです。この点に関して、データは、例えば画像などのデジタルアセットを指します。メタデータは、効率的なアセット管理を行うために重要です。

メタデータは、対象のアセットで使用できるすべてのデータのコレクションですが、次のようなデータはそのアセットに含まれているとは限りません。メタデータの例を以下に示します。

* アセットの名前。
* 最終変更の日時。
* リポジトリーに格納されたときのアセットのサイズ。
* アセットが含まれるフォルダーの名前。
* 関連するアセットまたは適用したタグ。

上記は、アセットに対して [!DNL Experience Manager] が管理できる基本的なメタデータプロパティです。これにより、ユーザーはすべてのアセットを表示できます。例えば、最終変更日にアセットを並べ替えると、最近追加したアセットを検出する場合に便利です。

デジタルアセットに、次のようなデータをさらに追加できます。

* アセットのタイプ（画像、ビデオ、オーディオクリップ、ドキュメントなど）。
* アセットの所有者。
* アセットのタイトル。
* アセットの説明。
* アセットに割り当てられたタグ。

メタデータが多いほど、アセットをより細かく分類でき、デジタル情報量が大きくなるにつれ便利です。数百個のファイルをファイル名だけに基づいて管理することは可能です。ただし、このアプローチは拡張性に欠けます。関係者の数や管理対象のアセット数が増えると不十分になります。

メタデータを追加すると、以下の理由からデジタルアセットの価値が大きくなります。

* アクセスが容易になる - システムやユーザーが簡単に見つけることができます。
* 管理しやすくなる - 一連の同じプロパティを持つアセットを容易に検索し、これらのアセットに変更を適用できます。
* 完全 - アセットは、より多くの情報とコンテキスト、より多くのメタデータを保持します。

したがって、[!DNL Assets] ではデジタルアセットのメタデータの作成、管理およびやり取りを行う適切な方法を提供します。

## メタデータのタイプ {#types-of-metadata}

メタデータの 2 つの基本的なタイプは、テクニカルメタデータと記述メタデータです。

テクニカルメタデータは、デジタルアセットを操作しているソフトウェアアプリケーションで役に立つもので、手動で管理できません。[!DNL Experience Manager Assets] と他のソフトウェアは、自動的にテクニカルメタデータを決定し、アセットが変更されるとメタデータが変更される場合があります。アセットで使用可能なテクニカルメタデータは、主にアセットのファイルタイプによって決まります。テクニカルメタデータの例を以下に示します。

* ファイルのサイズ。
* 画像の寸法（高さと幅）。
* オーディオまたはビデオファイルのビットレート。
* 画像の解像度（詳細レベル）。

記述メタデータは、アセットが属するビジネスなど、アプリケーションドメインに関するメタデータです。記述メタデータは自動で定義できません。手動または半自動で作成されます。例えば、GPS 対応のカメラでは、緯度と経度を自動的に追跡し、画像に地理タグを追加できます。

記述メタデータ情報を手動で作成する場合のコストは高くなります。そのため、ソフトウェアシステムや組織間でのメタデータの交換を容易にするための基準が確立されています。[!DNL Experience Manager Assets] は、メタデータの管理に関連するすべての規格をサポートします。

## エンコーディング規格 {#encoding-standards}

メタデータをファイルに埋め込む方法は様々です。エンコーディング規格は、次の中から選択できます。

* XMP：[!DNL Assets] で抽出したメタデータをリポジトリーに格納するために使用されます。
* ID3：オーディオファイルおよびビデオファイル用の規格です。
* Exif：画像ファイル用の規格です。
* その他、従来の規格：[!DNL Microsoft Word]、[!DNL PowerPoint]、[!DNL Excel] など。

### XMP {#xmp}

[!DNL Extensible Metadata Platform]（XMP）は、すべてのメタデータ管理に対して [!DNL Experience Manager Assets] で使用されるオープンな標準です。XMP は、すべてのファイル形式に埋め込むことができる、ユニバーサルメタデータエンコーディングを提供します。アドビやその他の企業は、リッチコンテンツモデルを提供する XMP 標準をサポートしています。XMP 標準および [!DNL Experience Manager Assets] のユーザーは、基盤となる強力なプラットフォームを持っています。詳しくは、[XMP](https://www.adobe.com/products/xmp.html) を参照してください。

### ID3 {#id}

これらの ID3 タグに格納されたデータは、コンピューターまたはポータブル MP3 プレーヤー上でデジタルオーディオファイルの再生時に表示されます。

ID3 タグは、MP3 ファイルフォーマット用に設計されています。各フォーマットのその他の情報：

* ID3 タグは、MP3 ファイルおよび mp3PRO ファイルで使用できます。
* WAV ではタグが使用されません。
* WMA には、オープンソースの実装を許可しない独自のタグがあります。
* Ogg Vorbis では、Ogg コンテナに埋め込まれた Xiph コメントを使用します。
* AAC では独自のタグフォーマットが使用されます。

### Exif {#exif}

Exchangeable image file format（Exif）は、デジタル写真で最も一般的に使用されるメタデータフォーマットです。JPEG、TIFF、RIFF、WAV など、多くのファイル形式でメタデータプロパティの固定語彙を埋め込む方法を提供します。Exif によって、メタデータの名前と値のペアとして、メタデータが格納されます。これらのメタデータの名前と値のペアはタグとも呼ばれます。[!DNL Experience Manager] のタグと混同しないようにしてください。最新のデジタルカメラは Exif メタデータを作成し、最新のグラフィックソフトウェアでサポートされています。Exif 形式は、特に画像に関するメタデータ管理で最も一般的な共通項です。

Exif の主な制限は、BMP、GIF、PNG などの一般的な画像ファイル形式ではサポートされないことです。

Exif で定義されるメタデータフィールドは、通常、テクニカルなもので、記述メタデータ管理では使用が制限されています。このため、[!DNL Experience Manager Assets] は Exif プロパティのマッピングを、[共通のメタデータスキーマ](metadata-schemas.md)と [XMP](xmp-writeback.md) に提供します。

### その他のメタデータ {#other-metadata}

ファイルから埋め込み可能なその他のメタデータには、[!DNL Microsoft Word]、[!DNL PowerPoint]、[!DNL Excel] などがあります。

## メタデータスキーマ {#metadata-schemata}

メタデータスキーマは、メタデータプロパティの事前定義のセットで、様々なアプリケーションで使用できます。プロパティは常にアセットと関連付けられています。つまり、プロパティはリソースの「説明」です。

必要なメタデータスキーマが存在しない場合は、独自のメタデータスキーマを設計することもできます。既存の情報を重複しないようにします。組織内でスキーマを分割すると、メタデータを共有しやすくなります。[!DNL Experience Manager] は、最も頻繁に使用されるメタデータスキーマのデフォルトリストを提供します。このリストを使用すると、メタデータ戦略がすぐに開始でき、必要なメタデータプロパティをすばやく選択できます。

サポートされるメタデータスキーマを以下に示します。

### 標準的なメタデータ {#standard-metadata}

* DC - [!DNL Dublin Core] は、重要で広く使用されている一連のメタデータです。
* DICOM - Digital Imaging and Communications in Medicine。
* `Iptc4xmpCore` および `iptc4xmpExt` - International Press Communications Standard には、多くのサブジェクト固有のメタデータが含まれています。
* RDF - Resource Description Framework - 汎用のセマンティック Web メタデータ用。
* XMP - [!DNL Extensible Metadata Platform]。
* `xmpBJ` - Basic Job Ticketing。

### アプリケーション固有のメタデータ {#application-specific-metadata}

アプリケーション固有のメタデータには、テクニカルメタデータも記述メタデータも存在します。そのようなメタデータを使用する場合、他のアプリケーションでそのメタデータを使用することはできません。例えば、別の画像レンダリングアプリケーションが [!DNL Adobe Photoshop] メタデータにアクセスできない場合があります。アプリケーション固有のプロパティを標準プロパティに変更するワークフロー手順を作成できます。

* ACDSee - [!DNL ACDSee] プログラムで管理されるメタデータ。[www.acdsee.com/](https://www.acdsee.com/) を参照してください。
* Album - [!DNL Adobe Photoshop Album]。
* CQ - [!DNL Experience Manager Assets] で使用。
* DAM - [!DNL Experience Manager Assets] で使用。
* DEX - [Optima SC Description explorer](http://www.optimasc.com/products/dex/index.html) は、Windows オペレーティングシステム向けのメタデータおよびファイル管理向けのツールのコレクションです。
* CRS - [Adobe Photoshop Camera Raw](https://helpx.adobe.com/jp/camera-raw/using/introduction-camera-raw.html)。
* LR - [!DNL Adobe Lightroom]。
* MediaPro - [iView MediaPro](https://en.wikipedia.org/wiki/Phase_One_Media_Pro)。
* MicrosoftPhoto および MP - Microsoft Photo。
* PDF および PDF/X。
* Photoshop および psAux - [!DNL Adobe Photoshop]。

### Digital Rights Management メタデータ {#digital-rights-management-metadata}

* CC - [!DNL Creative Commons]。
* [!DNL XMPRights]。
* PLUS - [Picture Licensing Universal System](https://www.useplus.com)。
* PRISM - [Publishing Requirements for Industry Standard Metadata](https://www.idealliance.org/prism-metadata)。
* PRL - PRISM Rights Language。
* PUR - PRISM Usage Rights。
* `xmpPlus` - PLUS と XMP の統合。

### 写真固有のメタデータ {#photography-specific-metadata}

* Exif - GPS 位置など、カメラからのテクニカル情報。
* CRS - [!DNL Camera Raw] スキーマ。
* `iptc4xmpCore` および `iptc4xmpExt`。
* TIFF - 画像メタデータ（TIFF 画像に限らない）。

### 印刷固有のメタデータ {#print-specific-metadata}

* PDF および PDF/X - Adobe PDF およびサードパーティのアプリケーション。
* PRISM - [Publishing Requirements for Industry Standard Metadata](http://www.prismstandard.org/specifications/)。
* XMP - [!DNL Extensible Metadata Platform]。
* `xmpPG` - ページテキストの XMP メタデータ。

### マルチメディア固有のメタデータ {#multimedia-specific-metadata}

* `xmpDM` - [!DNL Dynamic Media]。
* `xmpMM` - メディア管理。

## メタデータ駆動型のワークフロー {#metadata-driven-workflows}

メタデータ駆動型のワークフローを作成することで、一部のプロセスを自動化し、効率性を高めることができます。メタデータ駆動型のワークフローでは、ワークフロー管理システムでワークフローが読み取られ、その結果、事前定義された動作が実行されます。例として、メタデータ駆動型のワークフローの使用方法をいくつか示します。

* ワークフローで画像にタイトルがあるかチェックできます。タイトルがない場合、システムはタイトルを追加するよう通知します。
* ワークフローでアセットの著作権情報によって配布が許可されているかをチェックできます。そのため、システムはアセットを 1 台のサーバーまたは他のサーバーに送信します。
* ワークフローでは、定義済みの必須のメタデータがないアセット、または&#x200B;*無効な*&#x200B;メタデータを持つアセットがないことを確認できます。
