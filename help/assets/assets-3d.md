---
title: AEM 3Dアセットの操作
description: AEM 3D での 3D アセットの使用方法を説明します
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.4/ASSETS
topic-tags: introduction
content-type: reference
exl-id: 3cee9b4f-c4be-4ffc-970c-5680c8ebba47
feature: 3D アセット
role: Administrator,Business Practitioner
translation-type: tm+mt
source-git-commit: 13eb1d64677f6940332a2eeb4d3aba2915ac7bba
workflow-type: tm+mt
source-wordcount: '1177'
ht-degree: 78%

---

# AEM 3Dアセットの操作{#working-with-d-assets}

>[!IMPORTANT]
>
>AEM 6.4でのAEM 3Dのサポートは終了しました。 Adobeでは、[AEMの3Dアセット機能をCloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/dynamicmedia/assets-3d.html)または[AEM 6.5.3以上として使用することをお勧めします。](https://experienceleague.adobe.com/docs/experience-manager-65/assets/dynamic/assets-3d.html#dynamic)

Adobe Experience Manager 3D（AEM 3D）を使用して、3D コンテンツをアップロード、管理、表示およびレンダリングできます。表示とレンダリングのサポートは、個々のオブジェクトに最適化されます。

[AEM 3D リリースノート](/help/release-notes/aem3d-release-notes.md)も参照してください。

[AEM 3D のインストールと設定](install-config-3d.md)も参照してください。

## AEM 3D のモデルとステージ  {#about-models-and-stages-in-aem-d}

AEM 3D を使用すると、ステージと呼ばれる事前定義済みの環境で、高品質で静的なスタンドアロンの 3D モデルを表示およびレンダリングできます。基本的に、ステージは、3D シーンの「ライティング」および Autodesk® Maya® や Autodesk 3ds Max® などのネイティブアプリケーションのレンダリング設定を提供します。さらに、オプションで、事前定義済みのカメラ、背景、グラウンドプレーンのジオメトリを含めることができます。

ライトを含む、アップロードされた 3D ファイルは、ステージと考えられます。アセットの詳細ページでアセットを開いて、そのようなアセットをシンプルな 3D オブジェクトに戻すことができます。「**[!UICONTROL プロパティを表示]**」をタップしてから、「**[!UICONTROL 基本]**」タブをタップします。メタデータ見出しの下にあるアセットクラスのドロップダウンリストから、「**[!UICONTROL 3D オブジェクト]**」を選択します。

AEM 3D で使用する 3D モデルを作成する場合は、以下の点に注意してください。

* 3D モデルファイルには、1 つのオブジェクトのみを含め、背景、グラウンドプレーン、シーンのライティングまたはカメラを含めないようにする必要があります。
* グラウンドプレーンの上にモデルを配置します。この位置は、グラウンドプレーンを提供するステージと共に表示またはレンダリングする場合に、特に重要です。設定で、Rapid Refine を使用してプレビューまたはレンダリングする際にオブジェクトをグラウンドプレーンの上に移動させることができます（デフォルトで有効）。この設定は、サードパーティのレンダラー（例えば、Maya）を使用したレンダリングには影響しません。そのため、グラウンドプレーンの上に配置されていないオブジェクトは部分的に非表示になる可能性があります。
* モデルは、座標系の原点（0,0,0）を中心として、なるべく水平方向の中央に配置します。そうすることで、インタラクティブな表示エクスペリエンスが向上します。
* テクスチャマップ以外は、外部ファイル参照がサポートされます。そのため、参照されているコンテンツがある場合は、プライマリモデルファイルに埋め込んでから、AEM にアップロードする必要があります。

   [AEM での 3D アセットのアップロードと処理](upload-processing-3d-assets.md)を参照してください。

* 一般的なシーンのライティングは、ステージに含まれます。したがって、3D モデルファイルにライトを含めることはお勧めしません。モデルにライトを含めることは可能です。ただし、そのモデル固有にする必要があります。例えば、他の部分で覆われたオブジェクトの部分を明るくするために追加のライティングを含める必要があることがあります。そのため、ステージライトだけでは十分に見えません。

## AEM 3D でサポートされているファイル {#supported-files-in-aem-d}

典型的な 3D アセットには、1 つのプライマリモデルファイルと、1 つ以上の参照されているファイルがあります。参照ファイルには、テクスチャマップや&#x200B;**IBL(Image-Based Lighting)**&#x200B;イメージなどが含まれます。

### プライマリ 3D モデルファイル {#about-the-primary-d-model-file}

プライマリ 3D モデルファイルには、実際の 3D モデルジオメトリと、モデルサーフェスに適用される（デフォルトの）マテリアルの定義が含まれます。AEM 3D では、以下のプライマリ 3D モデルファイル形式がサポートされています。

* Wavefront OBJファイル形式(`.obj`)

   OBJ形式には、1つ以上の個別の外部MTLファイル（マテリアルテンプレートライブラリ） (`.mtl`)が必要です。

* Autodesk FBX (Filmbox)ファイル形式(`.fbx`)

   Autodesk 3Dファイル交換形式バイナリ形式とASCII形式の両方。

   サードパーティアプリケーションで FBX ファイルを作成する場合は、以下の設定を推奨します（下の表を参照）。これらの設定を利用すると、AEM で使用する 3D ファイルに最適な結果が得られます。オプション名は、**[!UICONTROL Autodesk Maya FBXエクスポートオプション]**&#x200B;ダイアログボックスから取得されます。

<table> 
 <tbody> 
  <tr> 
   <td><strong>Autodesk Maya の FBX Export ダイアログボックスのオプション</strong></td> 
   <td><strong>説明</strong></td> 
  </tr> 
  <tr> 
   <td>Preserve References<br /> </td> 
   <td><p>選択を解除。</p> <p>現時点では、AEM 3D は外部参照をサポートしていません。</p> </td> 
  </tr> 
  <tr> 
   <td>Smooth Mesh<br /> </td> 
   <td>選択。</td> 
  </tr> 
  <tr> 
   <td>Convert NURBS surfaces to</td> 
   <td><strong>ソフトウェアレンダーメッシュ</strong></td> 
  </tr> 
  <tr> 
   <td>Animation</td> 
   <td><p>選択または選択を解除。</p> <p>このオプションを選択した場合、AEM 3D はファイル内のアニメーション情報を無視します。</p> </td> 
  </tr> 
  <tr> 
   <td>Cameras</td> 
   <td><p><strong>3Dステージ</strong>に対して選択します。</p> <p>3Dモデルの場合は選択を解除します。</p> </td> 
  </tr> 
  <tr> 
   <td>Lights</td> 
   <td><p><strong>3Dステージ</strong>に対して選択します。</p> <p><strong>3Dモデル</strong>の選択を解除します。</p> </td> 
  </tr> 
  <tr> 
   <td>Units - Automatic</td> 
   <td>選択。読み込み時に AEM 3D が変換をおこないます。</td> 
  </tr> 
  <tr> 
   <td>Axis Conversion - Up Axis</td> 
   <td><p><strong>Y-up</strong></p> <p>Y-up は、Maya からのエクスポートに一貫性を持たせます。この AEM 3D リリースでは、FBX ファイルに推奨される座標系です。</p> </td> 
  </tr> 
  <tr> 
   <td>メディアを埋め込む</td> 
   <td>両方のオプションがサポートされています。 「埋め込み」を選択した場合、AEM 3Dは、モデルファイルと同じ名前を持つ隣接するフォルダに埋め込みメディアを抽出します。フォルダ名は<code>.fbm</code>が付きます。</td> 
  </tr> 
  <tr> 
   <td>FBX File Format - Type</td> 
   <td><strong>バイナリ</strong>または <strong>ASCII</strong> がサポートされています。</td> 
  </tr> 
  <tr> 
   <td>FBX File Format - Version</td> 
   <td>FBX 2014/2015 が推奨されます。その他のバージョンでも問題なく機能する可能性があります。</td> 
  </tr> 
 </tbody> 
</table>

次のファイル形式は、Autodesk Maya が AEM オーサリングサーバーにインストールされ、設定されている場合にサポートされます。

* Autodesk Maya

   ASCII `.ma`形式とバイナリ`.mb`形式の両方です。

* `Jupiter Tesselation (ISO 14306-1).jt`

    業界標準の CAD データ交換、コラボレーションおよび製品ビジュアライゼーション形式。

### テクスチャマップファイルのサポート {#support-for-texture-map-files}

3D モデルファイル内のマテリアル定義には、テクスチャマップを提供する外部画像ファイルへの参照を含めることができます。AEM 3D では、以下のタイプのテクスチャマップファイルをサポートしています。

* 拡散色テクスチャ
* 鏡面反射色テクスチャ
* 環境光色テクスチャ
* ディスプレイスメントマップ（バンプマップとも言います）
* 法線マップ
* 不透明度マップ
* 粗さマップ（光沢マップ、反射マップまたはコサインパワーマップとも言います）

プライマリ3Dモデルファイル内のマテリアルは、AEM 3Dで無視される他のタイプのマップを参照できます。

### IBL （イメージベースの照明）イメージ{#ibl-image-based-lighting-images}

ステージを定義する 3D モデルファイルは、単一の IBL 環境画像を参照できます。現在、AEM 3D は、拡散 IBL および反射用には緯度／経度形式の 32 ビット TIFF 画像のみをサポートします。球面のシーンの背景では、8 ビット RGB 画像もサポートされます。

[IBLステージの操作について](working-with-ibl-stages.md)を参照してください。

>[!NOTE]
>
>プライマリ 3D モデルファイル内に存在する上記以外のファイル参照は、現時点では無視されます。AEM 3D は、セカンダリ 3D モデルファイルへの参照をサポートしていません。
Y-upは、このリリースではFBXファイルに適した座標系です。

## プライマリ 3D モデルファイル内のマテリアルシェーディング {#material-shading-in-a-primary-d-model-file}

元のネイティブモデルファイルには、Blinn、Lambert などのシェーダーまたは手続き型シェーダーと共に使用されるマテリアル定義を含めることができます。これらの潜在的に複雑なマテリアルは、対応するネイティブアプリケーション（Autodesk Maya など）を使用してレンダリングする場合のみサポートされます。

表示目的、またはデフォルトの Rapid Refine™ レンダラーを使用してレンダリングする場合は、Phong のようなシェーダーで使用できるように、すべてのマテリアルが単純化されたり、置換されたり、またはその両方がおこなわれます。このシェーダーがサポートする属性は限定的です。マテリアル定義の他の属性は、無視されます。

[3D アセットの表示](viewing-3d-assets.md)を参照してください。

[3D アセットのレンダリング](rendering-3d-assets.md)を参照してください。

## プライマリ 3D モデルファイル内のマテリアルの命名 {#naming-materials-in-a-primary-d-model-file}

*サーフェス*&#x200B;は、同じマテリアルでカバーされる 3D モデルのサーフェス領域として定義されます。このマテリアルは、サーフェスの命名にも使用されます。したがって、プライマリ 3D モデルファイルに含まれるマテリアルにはモデルに応じた名前を付けることをお勧めします。例えば、「Body」、「Windows」、「Tires」、「Rims」などの特定の名前を使用する場合は、「Red」、「Glass」、「Rubber」、「Aluminum」などの曖昧な名前を使用することをお勧めします。
