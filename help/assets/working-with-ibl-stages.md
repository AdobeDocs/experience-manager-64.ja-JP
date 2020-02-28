---
title: IBL ステージの使用について
seo-title: IBL ステージの使用について
description: AEM 3D では、組み込みの Adobe Rapid Refine™ レンダラーおよびサードパーティのレンダラーでのインタラクティブな表示およびレンダリングの両方で、Image-Based Lighting（IBL）をサポートしています。
seo-description: AEM 3D では、組み込みの Adobe Rapid Refine™ レンダラーおよびサードパーティのレンダラーでのインタラクティブな表示およびレンダリングの両方で、Image-Based Lighting（IBL）をサポートしています。
uuid: 495ba9cc-02f5-4ce5-9503-9f61ca5482db
contentOwner: Rick Brough
topic-tags: 3D
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/ASSETS
discoiquuid: 658ff671-16b9-41bd-ba24-b77a32b3346b
translation-type: tm+mt
source-git-commit: 5acb16b1734331767554261bbcf9640947f2e23f

---


# IBL ステージの使用について {#about-working-with-ibl-stages}

AEM 3D では、組み込みの Adobe Rapid Refine™ レンダラーおよびサードパーティのレンダラーでのインタラクティブな表示およびレンダリングの両方で、Image-Based Lighting（IBL）をサポートしています。IBLステージは、Autodesk® Maya®やAutodesk® 3ds Max®などの一般的なオーサリングツールを使用して作成できます。

## IBL の画像 {#images-for-ibl}

最適な結果を得るには、Image-Based Lighting に使用する画像が High Dynamic Range（HDR）であることが必要です。環境をすべてカバーする球形のマッピングをおこなった、緯度／経度の形式であることが必要です。

現在、AEM 3D では、32 ビットの TIFF のみをサポートしています。必要に応じて、Adobe Photoshop などのツールを使用し、Adobe Photoshop の TIFF 書き出しダイアログボックスで以下の設定を使用して HDR 画像を TIFF に変換します。

* **[!UICONTROL ビットデプス]** - 32ビット（浮動小数点）
* **[!UICONTROL Pixel Order]** - Interleaved(RGBRGB)
* **[!UICONTROL 画像圧縮]** - LZW
* **[!UICONTROLバイト順序** - IBM PC

IBL ステージでは、多くの場合 1 枚の HDR 画像で十分ですが、AEM 3D は最大 3 つの異なる画像を使用した追加の IBL エフェクトの制御を提供しています。

* **拡散照明環境イメージ** — このタイプのイメージはHDRイメージにする必要がありますが、小さくすることもできます。これは、拡散照明に使用する前にイメージを大幅にフィルタするためです。
* **Reflection Environment Image** — このタイプのイメージは、オブジェクトサーフェスに反射を作成するために使用します。 反射に必要な画質およびシャープネスを提供するサイズおよび解像度の、標準的な 8 ビットの RGB 画像を使用できます。HDR 画像が指定されている場合、AEM 3D は、独自のアルゴリズムを使用する前にその画像を 8 ビットの RGB に変換します。
* **背景の環境画像** — このタイプの画像は背景として使用されます。 ステージの背景に必要なサイズ、解像度および詳細度の、標準的な 8 ビットの RGB 画像を使用できます。HDR 画像が指定されている場合、AEM 3D は、独自のアルゴリズムを使用してその画像を 8 ビットの RGB に変換します。 ``

>[!NOTE]
>
>特定の IBL 画像では、変換アルゴリズムが適切に機能しないことがあります。その結果、プレビューや Rapid Refine でレンダリングするときに、背景が明るすぎたり、過度に飽和したりすることがあります。このような場合は、Photoshop などのツールを使用して、手動で IBL 画像を 8 ビットの RGB 画像に変換することをお勧めします。この画像を別途アップロードし、背景環境画像としてステージに追加します。拡散ライティング環境画像および反射環境画像は、32 ビットの TIFF である必要があります。

## IBL ステージの外観の調整 {#adjusting-the-ibl-stage-appearance}

以下のステージプロパティを使用して、IBL ステージの外観を調整できます。

<table> 
 <tbody> 
  <tr> 
   <td><strong>プロパティ</strong><br /> </td> 
   <td><strong>説明</strong></td> 
  </tr> 
  <tr> 
   <td>IBL 太陽詳細</td> 
   <td><p>太陽をシミュレートする追加の光源の方向と強さを調整できます。 <span class="diff-html-added">この光源は、照明の明るさを増し、オブジェクトを地表にドロップシャドウを投影します。 ドロップシャドウの表示は、Rapid Refine を使用したレンダリング、および Google Chrome でのプレビュー時にサポートされていますが、現在のところ他のブラウザーではサポートされていません。</span></p> 
    <ul> 
     <li><strong>lat</strong> — 太陽光源の垂直位置(<code>0.0</code>-<code>1.0</code>)。<br /> の設定は、水平 <code>0.0</code> 線（拡散照明環境イメージの垂直中心）にあります。は最 <code>1.0</code> 頂部（[拡散照明環境イメージ]の上端）にあります。</li> 
     <li><strong>long</strong> — 太陽光源の水平位置(<code>0.0</code>-<code>1.0</code>)。<br /> 0.0に設定すると左側に対応します。1.0は、[拡散照明環境イメージ]の右端に対応します。<br /> </li> 
     <li><strong>bright</strong> — 太陽光源の明るさ。 この値を大きくすると、日光の光源が明るくなります。この値を小さくすると暗くなります。<br /> を指定すると、追加のラ <code>0</code> イトがオフになり、影付けが無効になります。 パラメーターは、環境反射には影響しません。<br /> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td>IBL カメラの高さ</td> 
   <td>If the IBL background appears distorted near the horizon, it is possible to reduce or eliminate the distortion by adjusting this property. <br /> </td> 
  </tr> 
  <tr> 
   <td>環境照明</td> 
   <td><p><span class="diff-html-added">拡散光の照明を制御できます。 拡散ライティング環境画像が通常よりも明るかったり、暗かったりする場合（夜のシーンなど）、このプロパティを手動で調整して、ライティングの明るさを修正する必要がある場合があります。</span></p> 
    <ul> 
     <li><strong>r, g, b</strong> — 現在は使用されていません。</li> 
     <li><strong>bright</strong> — 明る <span class="diff-html-added">さの乗数。 この値を大きくしたり小さくしたりすると、全体的なライティングの強度が強くなったり弱くなったりします（基本的な IBL ライティングと日光の光源の明るさの両方）。</span></li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table>

## IBLステージの球状の背景直径の増加 {#increasing-the-spherical-background-diameter-of-an-ibl-stage}

IBLステージは、直径20メートルの球状の背景画像をデフォルトで使用します。 このようなステージは、最大10メートルの物体に適しています。 ただし、大きいオブジェクトを表示する場合は、IBLステージの球面の背景の直径を大きくすることができます。

**IBLステージの球状の背景径を大きくするには**:

1. CRXDE Liteで、背景の球の直径を増やすステージに移動します。 例：

   `/content/dam/test3d/stage-helipad.fbx`

1. ステージノードを展開して、を開きま `jcr:content/metadata`す。
1. プロパティを目 `dam:gPlaneRadius` 的のミリメートル値に設定します。

   レンダリングを効率化するために、この値は、ステージに表示するオブジェクトの最大サイズに制限することをお勧めします。

   例えば、長さ20メートルのジェットプレーンモデルは、正しく表示されま `dam:gPlaneRadius=20000`す。

1. Near the upper-left corner of the CRXDE Lite page, tap **[!UICONTROL Save All]**.

