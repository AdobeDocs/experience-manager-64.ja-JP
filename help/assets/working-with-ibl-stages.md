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
exl-id: 074ab20f-02df-4f9e-9512-93a76f5d234f
feature: 3D アセット
role: Business Practitioner
translation-type: tm+mt
source-git-commit: f9faa357f8de92d205f1a297767ba4176cfd1e10
workflow-type: tm+mt
source-wordcount: '850'
ht-degree: 54%

---

# IBL ステージの使用について {#about-working-with-ibl-stages}

AEM 3D では、組み込みの Adobe Rapid Refine™ レンダラーおよびサードパーティのレンダラーでのインタラクティブな表示およびレンダリングの両方で、Image-Based Lighting（IBL）をサポートしています。Autodesk® Maya®やAutodesk® 3ds Max®などの一般的なオーサリングツールを使用して、IBLステージを作成できます。

## IBL の画像 {#images-for-ibl}

最適な結果を得るには、Image-Based Lighting に使用する画像が High Dynamic Range（HDR）であることが必要です。環境をすべてカバーする球形のマッピングをおこなった、緯度／経度の形式であることが必要です。

現在、AEM 3D では、32 ビットの TIFF のみをサポートしています。必要に応じて、Adobe Photoshop などのツールを使用し、Adobe Photoshop の TIFF 書き出しダイアログボックスで以下の設定を使用して HDR 画像を TIFF に変換します。

* **[!UICONTROL ビット深度]** - 32ビット（浮動小数点）
* **[!UICONTROL Pixel Order]** - Interleaved(RGBRGB)
* **[!UICONTROL 画像圧縮]** - LZW
* **[!UICONTROL バイト順序]** - IBM PC

IBL ステージでは、多くの場合 1 枚の HDR 画像で十分ですが、AEM 3D は最大 3 つの異なる画像を使用した追加の IBL エフェクトの制御を提供しています。

* **拡散照明環境イメージ**  — このタイプのイメージはHDRイメージにする必要がありますが、比較的小さい場合もあります。これは、拡散反射光ライティングに使用する前にイメージが大きくフィルタされるからです。
* **[反射環境イメージ** ]：このタイプのイメージは、オブジェクトサーフェスの反射を作成するのに使用されます。反射に必要な画質およびシャープネスを提供するサイズおよび解像度の、標準的な 8 ビットの RGB 画像を使用できます。HDR 画像が指定されている場合、AEM 3D は、独自のアルゴリズムを使用する前にその画像を 8 ビットの RGB に変換します。
* **背景の環境画像**  — この種の画像は背景として使用されます。ステージの背景に必要なサイズ、解像度および詳細度の、標準的な 8 ビットの RGB 画像を使用できます。HDR 画像が指定されている場合、AEM 3D は、独自のアルゴリズムを使用してその画像を 8 ビットの RGB に変換します。

>[!NOTE]
>
>特定の IBL 画像では、変換アルゴリズムが適切に機能しないことがあります。その結果、プレビューや Rapid Refine でレンダリングするときに、背景が明るすぎたり、過度に飽和したりすることがあります。このような場合は、Photoshop などのツールを使用して、手動で IBL 画像を 8 ビットの RGB 画像に変換することをお勧めします。この画像を別途アップロードし、背景環境画像としてステージに追加します。拡散ライティング環境画像および反射環境画像は、32 ビットの TIFF である必要があります。

## IBL ステージの外観の調整  {#adjusting-the-ibl-stage-appearance}

以下のステージプロパティを使用して、IBL ステージの外観を調整できます。

<table> 
 <tbody> 
  <tr> 
   <td><strong>プロパティ</strong><br /> </td> 
   <td><strong>説明</strong></td> 
  </tr> 
  <tr> 
   <td>IBL 太陽詳細</td> 
   <td><p>太陽をシミュレートする補助光源の方向と強度を調整できます。 <span class="diff-html-added">この光源は、照明の明るさを高め、オブジェクトを地表面にドロップシャドウを投影します。ドロップシャドウの表示は、Rapid Refine を使用したレンダリング、および Google Chrome でのプレビュー時にサポートされていますが、現在のところ他のブラウザーではサポートされていません。</span></p> 
    <ul> 
     <li><strong>lat</strong>  — 太陽光源(<code>0.0</code>-<code>1.0</code>)の垂直位置。<br /> の設定 <code>0.0</code> は水平線(拡散反射光ライティング環境イメージの垂直中心)にあり、 <code>1.0</code> は最頂点([拡散反射光ライティング]環境イメージの上端)にあります。</li> 
     <li><strong>long</strong>  — 太陽光源(<code>0.0</code>-<code>1.0</code>)の水平位置。<br /> 0.0に設定すると左側に対応し、1.0は、[拡散反射光ライティング]環境イメージの右端に対応します。<br /> </li> 
     <li><strong>bright</strong>  — 太陽光源の明るさ。この値を大きくすると、日光の光源が明るくなります。この値を小さくすると暗くなります。<br /> を設定すると、補助照明が <code>0</code> オフになり、影付けが無効になります。パラメーターは、環境反射には影響しません。<br /> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td>IBL カメラの高さ</td> 
   <td>水平線の近くでIBLの背景が歪んで表示される場合は、このプロパティを調整することで、歪みを減らしたり、除去したりできます。<br /> </td> 
  </tr> 
  <tr> 
   <td>環境照明</td> 
   <td><p><span class="diff-html-added">拡散反射光の照明を制御できます。 拡散ライティング環境画像が通常よりも明るかったり、暗かったりする場合（夜のシーンなど）、このプロパティを手動で調整して、ライティングの明るさを修正する必要がある場合があります。</span></p> 
    <ul> 
     <li><strong>r, g, b</strong>  — 現在は使用されていません。</li> 
     <li><strong>bright</strong> - <span class="diff-html-added">明るさの乗数。この値を大きくしたり小さくしたりすると、全体的なライティングの強度が強くなったり弱くなったりします（基本的な IBL ライティングと日光の光源の明るさの両方）。</span></li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table>

## IBLステージの球状の背景の直径の増加{#increasing-the-spherical-background-diameter-of-an-ibl-stage}

IBLステージは、デフォルトで直径20メートルの球状の背景画像を使用します。 10メートルまでの物に対しては、このようなステージが適しています。 ただし、大きいオブジェクトを表示する場合は、IBLステージの球状の背景の直径を大きくすることができます。

**IBLステージの球状の背景径を大きくするには**:

1. CRXDE Liteで、背景の球面直径を増やしたいステージに移動します。 例：

   `/content/dam/test3d/stage-helipad.fbx`

1. ステージノードを`jcr:content/metadata`に展開します。
1. プロパティ`dam:gPlaneRadius`を目的のミリメートル値に設定します。

   レンダリングの効率性を高めるために、Adobeでは、この値を、ステージに表示する最大のオブジェクトのおよそ最大のディメンションに制限することをお勧めします。

   例えば、長さ20メートルのジェット平面モデルは、`dam:gPlaneRadius=20000`の場合は正しく表示されます。

1. CRXDE Liteページの左上隅近くにある「**[!UICONTROL すべて保存]**」をタップします。
