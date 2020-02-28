---
title: AEM 3D リリースノート
seo-title: AEM 3D リリースノート
description: Adobe Experience Manager Assets の 3D コンテンツ固有のリリースノート
seo-description: Adobe Experience Manager Assets の 3D コンテンツ固有のリリースノート
uuid: 6675951f-86f0-4ec5-97e4-d247f6faf913
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.4
content-type: reference
topic-tags: 3D
discoiquuid: 9789d031-fb7e-415a-a9c3-8b8fde978238
translation-type: tm+mt
source-git-commit: 7c850ed0d20dd2ba2626242c67ba190e371f049f

---


# AEM 3D リリースノート {#aem-d-release-notes}

AEM-6.4-DynamicMedia-3Dバージョン3.1.0（2018年10月11日）

AEM 3D機能パックを使用すると、AEM Assetsで3Dコンテンツをサポートできます。 3D Assets のアップロード、管理、プレビューおよびレンダリングの機能を提供します。表示とレンダリングのサポートは、（複数のオブジェクトを含む複雑なシーンではなく）個々のオブジェクトに最適化されています。

AEM 3Dは、Adobe Dimension(Dn)およびglTFアセットタイプをサポートしています。 これらのアセットタイプの実装は、このドキュメントで説明する従来の3Dタイプの実装とは大きく異なります。 詳しくは、 [Adobe Dimensionアセットの操作を参照してください](/help/assets/working-dimension-assets.md)。

また、Autodesk® Maya®とのサーバ側統合も含まれています（Windowsのみ）。 AEM と同じサーバーに Maya をインストールして設定すると、Maya 用の NVIDIA® mental ray® Standalone プラグインを使用した高品質なレンダリングなど、ネイティブな Maya ファイル形式をサポートできます。3ds maxをサーバにインストールして設定すると、ネイティブの.maxファイル形式がサポートされます。

[Autodesk Maya との統合](/help/assets/integrate-maya-with-3d.md)を参照してください。

また [AEM 3D Assets のインストールおよび構成](/help/assets/install-config-3d.md)と[高度な設定](/help/assets/advanced-config-3d.md)も参照してください。

[3D アセットの使用](/help/assets/assets-3d.md)も参照してください。

## システム要件 {#system-requirements}

**前提条件**

* AEM 6.4.2 （Service Pack 2搭載AEM 6.4）
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

   アップロード時に、3Dアセットが独自の形式に変換され、高速でインタラクティブな表示が可能になります。 3D アセットのタイプによっては、アップロードされる 3D アセットのサイズの 2～3 倍のストレージ容量が必要です。

[3D アセットの使用](/help/assets/assets-3d.md)も参照してください。

## AEM 3D のインストールと設定 {#installing-and-configuring-aem-d}

[AEM 3D のインストールと設定](/help/assets/install-config-3d.md)を参照してください。

「AEM 3DとAutodesk mayaの統合 [」および「](/help/assets/integrate-maya-with-3d.md) AEM 3DとAutodesk 3ds maxの統合」も参照してください [](/help/assets/integrating-aem-3d-with-autodesk-3ds-max.md)。

## サポートされている 3D ファイル形式 {#supported-d-file-formats}

<table> 
 <tbody>
  <tr>
   <td><strong>形式</strong></td> 
   <td><strong>説明</strong></td> 
   <td><strong>プラットフォーム</strong></td> 
   <td><strong>メモ</strong></td> 
  </tr>
  <tr>
   <td>DN</td> 
   <td>Adobe Dimension</td> 
   <td>すべての </td> 
   <td>クラウドベースのコンバージョンサービスへのアクセスが必要です。</td> 
  </tr>
  <tr>
   <td>GLTZ</td> 
   <td>Zipped gITF</td> 
   <td>すべての </td> 
   <td> </td> 
  </tr>
  <tr>
   <td>GLB</td> 
   <td>バイナリgITF</td> 
   <td>すべての </td> 
   <td>ダウンロードのみ（GLBレンディションはDNアセット用に作成されます）。</td> 
  </tr>
  <tr>
   <td>OBJ</td> 
   <td>Wavefront OBJ 3D </td> 
   <td>すべての </td> 
   <td> </td> 
  </tr>
  <tr>
   <td>FBX</td> 
   <td>Autodesk FBX（Kaydara Filmbox）</td> 
   <td>すべての </td> 
   <td>Autodesk FBX SDKは、Authorノードにインストールする必要があります。</td> 
  </tr>
  <tr>
   <td>MA、MB</td> 
   <td>ネイティブな Autodesk Maya</td> 
   <td>Windows のみ</td> 
   <td>Autodesk mayaは、作成者ノードでこれらのファイルフォーマットを有効にする必要があります。 See <a href="/help/assets/integrate-maya-with-3d.md" target="_blank">Integrating AEM 3D with Autodesk Maya</a>.</td> 
  </tr>
  <tr>
   <td>JT</td> 
   <td>Siemens PLM オープン CAD</td> 
   <td>Windows のみ</td> 
   <td>Autodesk mayaは、作成者ノードでこれらのファイルフォーマットを有効にする必要があります。 See <a href="/help/assets/integrate-maya-with-3d.md">Integrating AEM 3D with Autodesk Maya</a>.</td> 
  </tr>
  <tr>
   <td>*</td> 
   <td><p>Autodesk Maya でサポートされているその他の 3D 入力形式を有効にすることができます。</p> <p>See <a href="/help/assets/integrate-maya-with-3d.md#enabling-additional-formats-supported-by-maya" target="_blank">Enabling Additional Formats Supported by Maya</a>.</p> </td> 
   <td>Windows のみ</td> 
   <td>Autodesk mayaは、作成者ノードでこれらのファイルフォーマットを有効にする必要があります。 See <a href="/help/assets/integrate-maya-with-3d.md">Integrating AEM 3D with Autodesk Maya</a>.</td> 
  </tr>
  <tr>
   <td>MAX</td> 
   <td>ネイティブAutodesk 3ds Max</td> 
   <td>Windows のみ</td> 
   <td>このファイル形式を有効にするには、作成者ノードでAutodesk 3ds maxが必要です。 「AEM 3D <a href="/help/assets/integrating-aem-3d-with-autodesk-3ds-max.md">とAutodesk 3ds maxの連携」を参照してください</a>。</td> 
  </tr>
 </tbody>
</table>

## 機能強化と新機能 {#enhancements-and-new-features}

バージョン3.0

* Autodesk 3ds maxネイティブファイル形式のサポート。
* 安定性、品質、ユーザーエクスペリエンスを向上させるための様々な変更点とバグ修正。
* 構成設定の移動先 `/libs/settings/dam/v3d/`

バージョン3.1

* Adobe Dimensionのネイティブファイル形式(.dn)のサポートは限定的です。
* glTFアセット用の新しい3Dビューア。
* Amazon AWSでホストされる、クラウドベースのアドビ管理コンバージョンサービスへの新しいインターフェイス。 最初は、このサービスはDnからglTF形式にのみ変換されます。

## 制約と既知の問題 {#restrictions-and-known-issues}

### Adobe Dimensionのサポート {#adobe-dimension-support}

* このバージョンのAEM3Dでは、Adobe Dimensionで作成される.dnファイルのサポートが制限されています。
* アップロード処理中に、AEMはクラウドベースのアドビホストの変換サービスを利用して、ネイティブの.dnファイルからglTFレンディションを作成します。 変換サービスにアクセスし、Amazon AWSエンドポイントを選択する必要があります。
* 新しいglTFビューアが提供され、AEM Assetsおよびサイト/画面でのDNアセットの表示がサポートされます。 Viewerでのステージのサポートはまだ行われていません。
* DNモデルは、IBLのライトと背景（存在する場合）を埋め込むことができます。 また、ビューアは初期設定の照明、初期設定の背景色、またはその両方を適用します。
* DNアセットの高品質レンダリングはまだ使用できません。
* テクスチャマップなどの依存関係は、DNアセットに埋め込まれ、AEMで明示的に管理することはできません。

### 互換性 {#compatibility}

* **Windows サービスとしての実行がサポートされていない（Windows のみ）** - 機能する可能性はありますが、テストされていません。
* **ダイナミックメディア** ( `dynamicmedia-scene7` モード) - AEM 3DとAEM 6.4でリリースされた新しいダイナミックメディアソリューションとの互換性は、まだ完全には検証されていません。 ダイナミックメディアとAEM3Dを一緒にデプロイする場合は、ダイナミックメディアに割り当てられていないAEM Assetsリポジトリの領域にのみ3Dアセットとその依存関係を配置することをお勧めします。 この推奨事項は、3Dステージに必要ながダイナミックメディアではサポートされていない32ビットTIFFファイルに対して特に重要です。

### 一般 {#general}

* **依存関係解決のショートカット** - このショートカットは、3D アセットのカード表示で使用できます。カード表示されるアセットカードには、「未解決の依存関係」というバナーが表示されます。このショートカットによって、「**依存関係**」タブではなく「**基本のプロパティ**」タブが開きます。回避策：手動で「依存関係」タブに移動します。

* **ステージセレクターを使用できない** - ライトを含む 3D アセットは、AEM により 3D ステージとして自動的にタグ付けされます。詳細ビューでは、ステージに対して使用できるステージセレクターがありません。3D アセットを 3D オブジェクトとしてマークするには、「**基本のプロパティ**」タブに移動し、「**アセットクラス**」を「**3D オブジェクト**」に変更して、「**保存**」をクリックします。

* **従属ファイルとレンディションを持つ 3D アセットのダウンロード** - 「**依存関係**」と「**レンディション**」の両方を選択して AEM から 3D アセットをダウンロードすると、ダウンロードにはプライマリ 3D アセットのレンディションだけでなく、すべての従属ファイルのレンディションも含まれます。

* **Autodesk 3ds maxの統合** - 3ds maxでのレンダリングは現時点ではサポートされていません。

### ファイルタイプの制約 {#file-type-restrictions}

* **Mathematica（.ma）ファイル** - Mathematica ファイルは、ネイティブ Maya ファイルと同じファイルサフィックスを使用します。Feature Packがインストールされ、Maya .maファイルフォーマットが有効な場合、AEM3DはMathematicaファイルの取り込みに失敗します。 このようなアセットは、カード表示にエラーバナーを表示します。

* **Targa（.tga）画像ファイル** - 古いバージョンの 3D モデルファイルには、TGA ファイルへの参照を含めることができる場合があります。この形式は、AEM ではサポートされていません。3DアセットをAEMにアップロードする前に、このようなファイルを別の形式に変換することをお勧めします。
* **HDR 画像** - HDR 画像は、IBL（Image-Based Lighting）を含むステージに使用されます。現在、このようなステージに対しては 32 ビット TIFF 画像のみがサポートされています。
* **32 ビット TIFF 画像** - 32 ビット TIFF 画像は、Imabe-Based Lighting を含むステージに使用されます。AEMは、これらのアセットのレンディションの作成をサポートしていないので、サムネールが空白になり、プレビューできません。 IBL ステージと共に使用する場合でも、アセットは正しく機能します。
* **Autodesk 3ds Max (.max)ファイル** - Autodesk 3ds maxがインストールされ、作成者ノードに設定されている場合、AEMは.maxファイルの取り込みと変換をサポートします。 現時点では、ステージとしての.maxファイルの使用はサポートされていません。

### 依存関係の自動解決 {#automatic-dependency-resolution}

* **アップロード後に未解決のファイル依存関係** - 3D アセットとその従属ファイルを同じアップロード操作でアップロードすると、一部の従属ファイルが自動的に解決されないことがあります。従属ファイルが大きい場合は、この問題が発生する可能性が高くなります。この問題を修正するには、アップロード後に未解決の従属ファイルを表示する、アセットの&#x200B;**プロパティ／依存関係**&#x200B;ページにアクセスします。前に未解決だった従属ファイルは、今度は表示されません。「**保存**」をクリックして、アセットを完成させます。今後、この問題が発生しないようにするには、すべての従属ファイルを別々のトランザクションでアップロードしてから 3D オブジェクトをアップロードします。

* **大文字と小文字の区別** - 依存関係の自動解決では、大文字と小文字を区別してファイル名の照合を試みます。For example, if the original dependency found in the 3D asset is `image.jpg`, the dependency resolves to an asset named `Image.jpg`, `image.JPG`, or any other case variation.

### 3D ステージ {#d-stages}

* **ステージのサムネール** — ステージの自動生成サムネールは、ステージを正確に表していない場合があります。
* **非 IBL ステージのステージジオメトリ** - Rapid Refine レンダラーは、非 IBL ライティングを含むステージのジオメトリ（背景やグランドプレーン）をレンダリングしません。このようなジオメトリは、アセットの詳細ビュー（3Dプレビュー）に適切に表示されます。

* **IBL ライティングを含む FBX ステージ** - IBL ライティングを含む FBX ステージをアップロードできます。ただし、FBX 形式には、IBL 画像名を転送するための規定がありません。そのため、ファイルの依存関係を解決できません。IBL 画像は、アップロード後に手動でステージに割り当てる必要があります。You can assign the same 32-bit TIFF image to the three dependencies which are **Diffuse Lighting Environment Image**, **Reflection Envrionment Image**, and **Background Envrionment Image**, or different images may be assigned.

* **IBL ステージの背景画像** - IBL シーンによっては、明るすぎたり不鮮明すぎたりするなど、背景画像の品質が低いことがあります。IBL ステージの画像背景の視覚的な品質を最大限に高めるには、個別の高解像度 8 ビット JPEG 画像を作成し、**背景環境画像**&#x200B;として IBL ステージに付加することをお勧めします。

* **Maya で IBL ステージを使用してレンダリングすると黒い画像になる** - この問題は、ステージが参照する元の IBL 画像が別の名前を持つ画像で置き換えられたため、IBL 画像の依存関係が Maya で見つからないことにより引き起こされる可能性があります。この問題を回避するには、Maya IBLステージで参照される3つの依存関係のうち、少なくとも1つが、Mayaファイル内の元のIBLファイルリファレンスと同じ名前を持っていることを確認します。
* **IBL ステージの背景画像が反転する** - Autodesk Maya に付属の NVIDIA mental ray レンダラーの動作と一致させるために、IBL ステージの画像が意図的に水平に反転されます。回避策：PhotoshopでIBLステージに使用した画像をアップロードする前に反転します。
* **IBL ステージの明るさ** - IBL 画像を自動解析した結果、シーンが暗くなりすぎたり明るくなりすぎたりすることがあります。To adjust the lighting brightness of IBL stages, navigate to **Basic Properties** and adjust the **bright** value of **Environment Lighting** as needed.

### AEM Sites の 3D コンポーネント {#aem-sites-d-component}

* **1ページに1つの3Dコンポーネント** — 現時点では、各Webページで許可される3Dコンポーネントのインスタンスは1つだけです。 複数の3Dコンポーネントを同じページに追加した場合、どの3Dコンポーネントも正しく機能しません。
* **サイトでのプレビュー時に3Dビューが見つからない** — サイトでプレビューを使用する場合は **** 、3Dビューアを完全に初期化するために、ブラウザでページを再読み込みする必要があります。 作成者ノードまたは発行ノードでWebページを直接表示する（つまり、パスから削除する）場合は、こ `edit.html` の問題は発生しません。

* **iOSデバイスでフルスクリーンモードを使用できない** - iOSデバイスでは、使用されているブラウザーに関係なく、フルスクリーンボタンは使用できません。

### 3D コンテンツの公開 {#publishing-d-content}

* **3Dコンポーネントの設定** - 3D Feature packはすべてのアクティブなパブリッシュノードにインストールする必要があり、各ノードは **CRXDE Liteを使用して設定し、の同じ設定オプションを使用する必要がありま**`/libs/settings/dam/v3D/WebGLSites`す。

* **公開後のテクスチャ、背景、照明の欠落** - **** AEM Sitesの公開メカニズムは、3Dコンポーネントが参照する3Dモデルや3Dステージなど、ページの主な依存関係を自動的に公開します。 しかし、3D ステージと 3D モデルは、通常、AEM Sites の公開メカニズムでは自動的に公開されない IBL 画像とテクスチャマップのセカンダリアセットに依存しています。回避策：サイトからWebページを公開する前に、アセットからすべての3Dアセットを公開します。 これにより、3Dアセットの依存関係がパブリッシュノードですべて使用できるようになります。

