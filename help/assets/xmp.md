---
title: XMP Metadata
description: で使用されるXMP(Extensible Metadata Platform) メタデータ標準について説明します。 [!DNL Experience Manager] メタデータ管理用のアセット。 XMP で提供される標準形式によって、多様なアプリケーションに対応したメタデータの作成、処理およびやり取りができます。
contentOwner: AG
feature: Metadata
role: User,Admin
exl-id: 32c4ca3d-2e9e-46a3-b4c7-70dcc50daaaa
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '846'
ht-degree: 54%

---

# XMP メタデータ {#xmp-metadata}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

XMP(Extensible Metadata Platform) は、 [!DNL Experience Manager] すべてのメタデータ管理用のアセット。 XMP で提供される標準形式によって、多様なアプリケーションに対応したメタデータの作成、処理およびやり取りができます。

XMP では、すべてのファイル形式に埋め込むことができる共通のメタデータエンコーディングのほか、リッチ[コンテンツモデル](xmp.md#xmp-core-concepts)も提供され、[アドビによるサポート](xmp.md#advantages-of-xmp)やその他各社のサポートがあるので、XMP を Assets と組み合わせて使用すると強力なプラットフォームを構築できます。[!DNL Experience Manager]

[XMP の仕様](https://www.adobe.com/devnet/xmp.html)は、アドビから入手できます。

## XMP とは {#what-is-xmp}

[!DNL Experience Manager] Assets は、XMP (Adobeが主導する拡張メタデータプラットフォーム ) をネイティブでサポートしています。 XMP は、デジタルアセット内の標準化されたメタデータと独自メタデータを処理および格納するための規格です。XMP は、複数のアプリケーションでメタデータを効率的に使用するための共通規格となるよう設計されています。

例えば制作のプロフェッショナルは、アドビのアプリケーションに組み込まれた XMP サポートを使用して、複数のファイル形式に情報を渡します。この [!DNL Experience Manager] アセットリポジトリは、XMPメタデータを抽出し、それを使用してコンテンツのライフサイクルを管理し、自動化ワークフローを作成する機能を提供します。

XMPは、データモデル、ストレージモデル、スキーマを提供して、メタデータの定義、作成および処理方法を標準化します。 これらの概念はすべて、この節で説明します。

EXIF、ID3、Microsoft Office のすべての従来のメタデータは、自動的にXMPに翻訳され、製品カタログなど、顧客固有のメタデータスキーマをサポートするように拡張できます。

XMPのメタデータは、一連のプロパティで構成されます。 これらのプロパティは、常に
\
リソースとして参照される特定のエンティティに関連付けられます。つまり、プロパティはリソースの「説明」です。XMP の場合、リソースとなるのは常にアセットです。

### アドビ {#adobe}

XMP 規格は、アドビが初めて Adobe Acrobat ソフトウェア製品の一部として導入しました。それ以降、XMP 規格が広く採用されてきました。

### XMP のエコシステム {#xmp-ecosystem}

XMP によって定義される[メタデータ](https://en.wikipedia.org/wiki/Metadata)モデルは、任意の定義済みメタデータ項目のセットと併用できます。また、XMP によって、リソースで複数の処理手順が行われる際にその履歴を記録するうえで便利な基本的なプロパティに対して、特定の[スキーマ](https://en.wikipedia.org/wiki/XML_schema)も定義されます。処理手順は、撮影、[スキャン](https://en.wikipedia.org/wiki/Image_scanner)またはテキスト作成から、画像編集手順（[切り抜き](https://en.wikipedia.org/wiki/Cropping_%28image%29)やカラー調整など）を経て、最終的な画像へのアセンブリまでです。XMP の処理中に、各ソフトウェアプログラムまたはデバイスでデジタルリソースに独自の情報を付加できます。この情報は、最終的なデジタルファイルで保持されます。

XMP のシリアライズおよび格納は、通常 [W3C](https://ja.wikipedia.org/wiki/World_Wide_Web_Consortium) [Resource Description Framework](https://ja.wikipedia.org/wiki/Resource_Description_Framework)（RDF）のサブセットを使用して実行され、[XML](https://ja.wikipedia.org/wiki/XML) で表記されます。

## XMP の利点 {#advantages-of-xmp}

XMPには、他のエンコーディング規格やスキーマと比較して次の利点があります。

* XMP ベースのメタデータは利便性が高く、細かく分類されています。
* XMP では 1 つのプロパティに複数の値を指定できます。
* XMPは標準化されたエンコーディングを備えており、メタデータを簡単に交換できます。
* XMPは拡張可能です。 アセットに追加情報を追加できます。

### 拡張可能 {#extensible}

XMP標準は拡張可能に設計されており、カスタムタイプのメタデータをXMPデータに追加できます。 一方、EXIF は拡張できないプロパティの固定リストを持っています。

>[!NOTE]
>
>通常、XMPではバイナリデータ型の埋め込みは許可されていません。 XMPでバイナリデータ（サムネール画像など）を扱う場合、XML に対応するフォーマット（Base64 など）でエンコードする必要があります。

## XMPの中心概念 {#xmp-core-concepts}

次の節では、名前空間とスキーマ、プロパティと値、代替言語など、XMP の中心概念について説明します。

### 名前空間とスキーマ {#namespaces-and-schemata}

XMPスキーマは、共通の XML 名前空間内のプロパティ名のセットで、\
データタイプと説明情報。 XMPスキーマは、その XML 名前空間 URI で識別されます。 名前空間を使用すると、同じ名前で意味が異なる異なるスキーマ内のプロパティ間の競合を防ぐことができます。

例えば、別個に設計された 2 つのスキーマにある **Creator** プロパティは、アセットを作成した個人を意味する場合と、アセットの作成元アプリケーション（Adobe Photoshop など）を意味する場合があります。

### プロパティと値 {#properties-and-values}

XMP には、1 つ以上のスキーマからプロパティを選択し含めることができます。

多くのアドビアプリケーションで使用される一般的なサブセットに含まれるプロパティの例を示します。

* Dublin Core スキーマ：dc:title, dc:creator, dc:subject, dc:format, dc:rights
* XMP基本スキーマ：xmp:CreateDate, xmp:CreatorTool, xmp:ModifyDate, xmp:metadataDate
* XMP rights management スキーマ：xmpRights:WebStatement, xmpRights:Marked
* XMP media management スキーマ：xmpMM:DocumentID

### 代替言語 {#language-alternatives}

XMPでは、 **xml:lang** プロパティをテキストプロパティに設定して、テキストの言語を指定します。
