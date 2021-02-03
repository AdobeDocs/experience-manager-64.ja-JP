---
title: AEM 3D リリースノート
description: Adobe Experience Manager Assets の 3D コンテンツ固有のリリースノート
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.4
topic-tags: release-notes, 3D
content-type: reference
translation-type: tm+mt
source-git-commit: 6be46f6986d1631f711cfd4464cc4f2d17014681
workflow-type: tm+mt
source-wordcount: '1966'
ht-degree: 44%

---


# AEM 3D リリースノート {#aem-d-release-notes}

>[!IMPORTANT]
>
>AEM 6.4のAEM 3D機能パックは、サポートされなくなりました。 Adobeでは、[AEMの3Dアセット機能をCloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/dynamicmedia/assets-3d.html#dynamicmedia)または[AEM 6.5.3以上として使用することをお勧めします。](https://experienceleague.adobe.com/docs/experience-manager-65/assets/dynamic/assets-3d.html#dynamic)

AEM-6.4-DynamicMedia-3Dバージョン3.1.0（2018年10月11日）

AEM 3D機能パックは、AEM Assetsの3Dコンテンツをサポートします。 3D Assets のアップロード、管理、プレビューおよびレンダリングの機能を提供します。表示とレンダリングのサポートは、複数のオブジェクトを持つ複雑なシーンではなく、個々のオブジェクトに対して最適化されています。

AEM 3Dは、Adobe Dimension(Dn)およびglTFのアセットタイプをサポートします。 これらのアセットタイプの実装は、このドキュメントで説明する従来の3Dタイプの実装とは大きく異なります。 [Adobe Dimensionアセットの操作](/help/assets/working-dimension-assets.md)を参照してください。

また、Autodesk® Maya®とのサーバ側統合も含まれています（Windowsのみ）。 AEM と同じサーバーに Maya をインストールして設定すると、Maya 用の NVIDIA® mental ray® Standalone プラグインを使用した高品質なレンダリングなど、ネイティブな Maya ファイル形式をサポートできます。3ds Maxをサーバにインストールして設定すると、ネイティブ.maxファイル形式をサポートできます。

[Autodesk Maya との統合](/help/assets/integrate-maya-with-3d.md)を参照してください。

また [AEM 3D Assets のインストールおよび構成](/help/assets/install-config-3d.md)と[高度な設定](/help/assets/advanced-config-3d.md)も参照してください。

[3D アセットの使用](/help/assets/assets-3d.md)も参照してください。

## システム要件 {#system-requirements}

**前提条件**

* AEM 6.4.2 (AEM 6.4 Service Pack 2)
* Autodesk® FBX® SDK 2016.1.2

**サポートされているオペレーティングシステム**

* Microsoft Windows 2012 Server以降
* Apple OS X El Capitan 10.6以降
* RedHat Enterprise Linux 7.3

**AEM AssetsでサポートされるWebブラウザー**

* Google Chrome 53 またはそれ以降（推奨）
* Apple Safari 9.1 またはそれ以降
* Firefox 48 以降
* Microsoft Edge 25.10586 またはそれ以降

その他のブラウザーでは、AEM での 3D コンテンツのインタラクティブ表示をサポートできません。Google Chrome だけがプレビューの影付けをサポートします。

**ハードウェア要件および推奨**

* CPU - 3D 処理およびレンダリングは、コンピューターの CPU を著しく必要とします。そのため、8 個以上の CPU コアを備えたコンテンポラリサーバーが推奨されます。
* メモリ - 32GB 以上が推奨されます。
* 大容量ストレージ - 高帯域幅 SSD ストレージが推奨されます。

   アップロード時に、3Dアセットは独自の形式に変換され、高速でインタラクティブな表示が可能になります。 3D アセットのタイプによっては、アップロードされる 3D アセットのサイズの 2～3 倍のストレージ容量が必要です。

[3D アセットの使用](/help/assets/assets-3d.md)も参照してください。

## AEM 3D のインストールと設定  {#installing-and-configuring-aem-d}

[AEM 3D のインストールと設定](/help/assets/install-config-3d.md)を参照してください。

[AEM 3DとAutodesk Mayaの統合](/help/assets/integrate-maya-with-3d.md)および[AEM 3DとAutodesk 3ds Max](/help/assets/integrating-aem-3d-with-autodesk-3ds-max.md)の統合も参照してください。

## サポートされている 3D ファイル形式 {#supported-d-file-formats}

| 形式 | 説明 | プラットフォーム | 備考 |
|--- |--- |--- |--- |
| DN | Adobe Dimension | すべての  | クラウドベースのコンバージョンサービスへのアクセスが必要です。 |
| GLTZ | Zipped gITF | すべての  |  |
| GLB | バイナリgITF | すべての  | ダウンロードのみ（GLBレンディションはDNアセット用に作成されます）。 |
| OBJ | Wavefront OBJ 3D | すべての  |  |
| FBX | Autodesk FBX（Kaydara Filmbox） | すべての  | Autodesk FBX SDKは、Authorノードにインストールする必要があります。 |
| MA、MB | ネイティブな Autodesk Maya | Windows のみ | Autodesk Mayaは、作成者ノードでこれらのファイルフォーマットを有効にする必要があります。 [AEM 3DとAutodesk Mayaの統合](/help/assets/integrate-maya-with-3d.md)を参照してください。 |
| JT | Siemens PLM オープン CAD | Windows のみ | Autodesk Mayaは、作成者ノードでこれらのファイルフォーマットを有効にする必要があります。 [AEM 3DとAutodesk Mayaの統合](/help/assets/integrate-maya-with-3d.md)を参照してください。 |
| * | Autodesk Maya でサポートされているその他の 3D 入力形式を有効にすることができます。[Mayaでサポートされる追加フォーマットを有効にする](/help/assets/integrate-maya-with-3d.md#enabling-additional-formats-supported-by-maya)を参照してください。 | Windows のみ | Autodesk Mayaは、作成者ノードでこれらのファイルフォーマットを有効にする必要があります。 [AEM 3DとAutodesk Mayaの統合](/help/assets/integrate-maya-with-3d.md)を参照してください。 |
| MAX | ネイティブAutodesk 3ds Max | Windows のみ | このファイル形式を有効にするには、Autodesk 3ds Maxが作成者ノードで必要です。 [AEM 3DとAutodesk 3ds Max](/help/assets/integrating-aem-3d-with-autodesk-3ds-max.md)の統合を参照してください。 |

## 機能強化と新機能 {#enhancements-and-new-features}

バージョン3.0

* Autodesk 3ds Maxネイティブファイル形式のサポート。
* 安定性、品質、ユーザーエクスペリエンスを向上させるための様々な変更点とバグ修正。
* 構成設定が`/libs/settings/dam/v3d/`に移動されました

バージョン3.1

* Adobe Dimensionのネイティブファイル形式(.dn)のサポートが制限されます。
* glTFアセット用の新しい3Dビューア。
* AmazonAWSでホストされる、クラウドベースのAdobe管理コンバージョンサービスへの新しいインターフェイス。 最初は、このサービスはDnからglTF形式への変換のみを行います。

## 制約と既知の問題 {#restrictions-and-known-issues}

### Adobe Dimensionサポート{#adobe-dimension-support}

* このバージョンのAEM3Dでは、Adobe Dimensionで作成された.dnファイルのサポートは限られています。
* アップロード処理AEMでは、クラウドベースのAdobeホスト変換サービスを利用して、ネイティブの.dnファイルからglTFレンディションを作成します。 変換サービスへのアクセスと、AmazonのAWSエンドポイントの選択が必要です。
* 新しいglTFビューアが提供され、AEM Assetsおよびサイト/画面でのDNアセットの表示がサポートされます。 Viewerでのステージのサポートはまだ行われていません。
* DNモデルは、IBLのライトと背景（存在する場合）を埋め込むことができます。 または、ビューアは初期設定の照明、初期設定の背景色、またはその両方を適用します。
* DNアセットの高品質レンダリングはまだ使用できません。
* テクスチャマップなどの依存関係は、DNアセットに埋め込まれ、AEMで明示的に管理することはできません。

### 互換性 {#compatibility}

* **Windows サービスとしての実行がサポートされていない（Windows のみ）** - 機能する可能性はありますが、テストされていません。
* **Dynamic Media** ( `dynamicmedia-scene7` モード) - AEM3DとAEM 6.4でリリースされた新しいDynamic Mediaソリューションとの互換性は、まだ完全には検証されていません。Dynamic MediaとAEM3Dを一緒にデプロイする場合は、3Dアセットとその依存関係は、Dynamic Mediaに割り当てられていないAEM Assetsリポジトリの領域にのみ配置することをお勧めします。 この推奨は、3Dステージに必要な32ビットTIFFファイルで、Dynamic Mediaではサポートされていない場合に特に重要です。

### 一般 {#general}

* **依存関係解決のショートカット** - このショートカットは、3D アセットのカード表示で使用できます。カード表示されるアセットカードには、「未解決の依存関係」というバナーが表示されます。このショートカットによって、「**依存関係**」タブではなく「**基本のプロパティ**」タブが開きます。回避策：手動で「依存関係」タブに移動します。

* **ステージセレクターを使用できない** - ライトを含む 3D アセットは、AEM により 3D ステージとして自動的にタグ付けされます。詳細ビューでは、ステージに対して使用できるステージセレクターがありません。3D アセットを 3D オブジェクトとしてマークするには、「**基本のプロパティ**」タブに移動し、「**アセットクラス**」を「**3D オブジェクト**」に変更して、「**保存**」をクリックします。

* **従属ファイルとレンディションを持つ 3D アセットのダウンロード** - 「**依存関係**」と「**レンディション**」の両方を選択して AEM から 3D アセットをダウンロードすると、ダウンロードにはプライマリ 3D アセットのレンディションだけでなく、すべての従属ファイルのレンディションも含まれます。

* **Autodesk 3ds Maxの統合** - 3ds Maxとのレンダリングは現時点ではサポートされていません。

### ファイルタイプの制約 {#file-type-restrictions}

* **Mathematica（.ma）ファイル** - Mathematica ファイルは、ネイティブ Maya ファイルと同じファイルサフィックスを使用します。Feature Packがインストールされ、Maya .maファイルフォーマットが有効な場合、AEM3DはMathematicaファイルを取り込もうとしますが、Mayaファイルは取り込めません。 このようなアセットは、エラーバナーをカード表示に表示します。

* **Targa（.tga）画像ファイル** - 古いバージョンの 3D モデルファイルには、TGA ファイルへの参照を含めることができる場合があります。この形式は、AEM ではサポートされていません。3DアセットをAEMにアップロードする前に、このようなファイルを別の形式に変換することをお勧めします。
* **HDR 画像** - HDR 画像は、IBL（Image-Based Lighting）を含むステージに使用されます。現在、このようなステージに対しては 32 ビット TIFF 画像のみがサポートされています。
* **32 ビット TIFF 画像** - 32 ビット TIFF 画像は、Imabe-Based Lighting を含むステージに使用されます。AEMでは、これらのアセットのレンディションの作成がサポートされていないので、サムネールが空白になり、プレビューできなくなります。 IBL ステージと共に使用する場合でも、アセットは正しく機能します。
* **Autodesk 3ds Max (.max)ファイル** - Autodesk 3ds Maxがインストールされ、作成者ノードに設定されている場合、 AEMは.maxファイルの取り込みと変換をサポートします。現時点では、ステージとしての.maxファイルの使用はサポートされていません。

### 依存関係の自動解決 {#automatic-dependency-resolution}

* **アップロード後に未解決のファイル依存関係** - 3D アセットとその従属ファイルを同じアップロード操作でアップロードすると、一部の従属ファイルが自動的に解決されないことがあります。従属ファイルが大きい場合は、この問題が発生する可能性が高くなります。この問題を修正するには、アップロード後に未解決の従属ファイルを表示する、アセットの&#x200B;**プロパティ／依存関係**&#x200B;ページにアクセスします。前に未解決だった従属ファイルは、今度は表示されません。「**保存**」をクリックして、アセットを完成させます。今後、この問題が発生しないようにするには、すべての従属ファイルを別々のトランザクションでアップロードしてから 3D オブジェクトをアップロードします。

* **大文字と小文字の区別** - 依存関係の自動解決では、大文字と小文字を区別してファイル名の照合を試みます。例えば、3Dアセットに見つかった元の依存関係が`image.jpg`である場合、依存関係は`Image.jpg`、`image.JPG`という名前のアセット、またはその他の大文字と小文字が区別されます。

### 3D ステージ {#d-stages}

* **ステージのサムネール**  — ステージの自動生成サムネールは、ステージを正確に表していない場合があります。
* **非 IBL ステージのステージジオメトリ** - Rapid Refine レンダラーは、非 IBL ライティングを含むステージのジオメトリ（背景やグランドプレーン）をレンダリングしません。このようなジオメトリは、アセットの詳細表示(3Dプレビュー)に適切に表示されます。

* **IBL ライティングを含む FBX ステージ** - IBL ライティングを含む FBX ステージをアップロードできます。ただし、FBX 形式には、IBL 画像名を転送するための規定がありません。そのため、ファイルの依存関係を解決できません。IBL 画像は、アップロード後に手動でステージに割り当てる必要があります。**拡散照明環境イメージ**、**反射環境イメージ**、**背景環境イメージ**&#x200B;の3つの依存関係に、同じ32ビットのTIFFイメージを割り当てるか、異なるイメージを割り当てることができます。

* **IBL ステージの背景画像** - IBL シーンによっては、明るすぎたり不鮮明すぎたりするなど、背景画像の品質が低いことがあります。IBL ステージの画像背景の視覚的な品質を最大限に高めるには、個別の高解像度 8 ビット JPEG 画像を作成し、**背景環境画像**&#x200B;として IBL ステージに付加することをお勧めします。

* **Maya で IBL ステージを使用してレンダリングすると黒い画像になる** - この問題は、ステージが参照する元の IBL 画像が別の名前を持つ画像で置き換えられたため、IBL 画像の依存関係が Maya で見つからないことにより引き起こされる可能性があります。この問題を回避するには、Maya IBLステージで参照される3つの依存関係のうち少なくとも1つが、Mayaファイル内の元のIBLファイルリファレンスと同じ名前を持っていることを確認します。
* **IBL ステージの背景画像が反転する** - Autodesk Maya に付属の NVIDIA mental ray レンダラーの動作と一致させるために、IBL ステージの画像が意図的に水平に反転されます。回避策：PhotoshopのIBLステージに使用する画像をアップロードする前に反転します。
* **IBL ステージの明るさ** - IBL 画像を自動解析した結果、シーンが暗くなりすぎたり明るくなりすぎたりすることがあります。IBLステージの照明の明るさを調整するには、**基本プロパティ**&#x200B;に移動し、必要に応じて&#x200B;**環境の照明**&#x200B;の&#x200B;**明るい**&#x200B;値を調整します。

### AEM Sites の 3D コンポーネント {#aem-sites-d-component}

* **1ページにつき1つの3Dコンポーネント**  — 現時点では、各Webページで許可される3Dコンポーネントのインスタンスは1つだけです。複数の3Dコンポーネントを同じページに追加した場合、どの3Dコンポーネントも正しく機能しません。
* **サイトでのプレビュー時に3D表示が見つからない**  ****  — サイトでプレビューを使用する場合は、ブラウザでページを再読み込みして3Dビューアを完全に初期化する必要があります。作成者ノードまたは発行ノードでWebページを直接表示する（つまり`edit.html`がパスから削除される）場合は、この問題は発生しません。

* **iOSデバイスでフルスクリーンモードを使用できない** - iOSデバイスでは、使用するブラウザーに関係なく、フルスクリーンボタンは使用できません。

### 3D コンテンツの公開 {#publishing-d-content}

* **3Dコンポーネントの設定**  — すべてのアクティブなパブリッシュノードに3D Feature Packをインストールする必要があります。各ノードには、の同じ設定オプションで **CRXDE** Liteを設定する必要があり `/libs/settings/dam/v3D/WebGLSites`ます。

* **パブリッシュ後にテクスチャ、背景、照明が見つからない** -  **** Publishmechanismは、3Dモデルや、3Dコンポーネントが参照する3Dステージなど、ページの主な依存関係を自動的にパブリッシュします。しかし、3D ステージと 3D モデルは、通常、AEM Sites の公開メカニズムでは自動的に公開されない IBL 画像とテクスチャマップのセカンダリアセットに依存しています。回避策：サイトからWebページを公開する前に、アセットからすべての3Dアセットを公開します。 これにより、3Dアセットのすべての依存関係がパブリッシュノードで使用できるようになります。
