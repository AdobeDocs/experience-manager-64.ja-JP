---
title: Dynamic Media の操作
seo-title: Working with Dynamic Media
description: Dynamic Media を使用して、Web、モバイルおよびソーシャルサイトで使用するためにアセットを配信する方法を学習します。
seo-description: Learn how to use Dynamic Media to deliver assets for consumption on web, mobile, and social sites.
uuid: 4dc0f436-d20e-4e8b-aeff-5515380fa44d
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.4/ASSETS
topic-tags: introduction
content-type: reference
discoiquuid: a8063d43-923a-42ac-9a16-0c7fadd8f73f
exl-id: f8a3936e-82b5-46c7-9614-b97162e27d6a
feature: Asset Management,Renditions
role: Admin,User
source-git-commit: 2bbc7e2a6b3aa36a7c2803d12ba402a5739c9a5c
workflow-type: tm+mt
source-wordcount: '416'
ht-degree: 90%

---

# Dynamic Media の操作 {#working-with-dynamic-media}

[Dynamic Media](https://www.adobe.com/solutions/web-experience-management/dynamic-media.html) は、マーチャンダイジングおよびマーケティング用のリッチなビジュアルアセットをオンデマンドで配信するもので、これらのアセットは、Web、モバイルおよびソーシャルサイトでの利用に合わせて自動的に拡大縮小されます。Dynamic Media は、一連のマスターアセットを使用し、パフォーマンスが最適化されスケーラビリティに優れたグローバルネットワーク経由で、複数のリッチコンテンツのバリエーションをリアルタイムで生成および配信します。

ダイナミックメディアは、ズーム、360 度スピン、ビデオなどのインタラクティブな閲覧エクスペリエンスを提供します。ダイナミックメディアは Adobe Experience Manager デジタルアセット管理（AEM アセット）ソリューションのワークフローを独自に取り込むことで、デジタルキャンペーン管理プロセスを簡易化し、効率化します。

<!-- DEAD ARTICLE >[!NOTE]
>
>A Community article is available on [Working with Adobe Experience Manager and Dynamic Media](https://helpx.adobe.com/experience-manager/using/aem_dynamic_media.html). -->

## Dynamic Media の機能 {#what-you-can-do-with-dynamic-media}

Dynamic Media では、公開前のアセットを管理できます。一般的なアセットの操作方法については、[デジタルアセットの操作](managing-assets-touch-ui.md)で詳しく説明しています。一般的なトピックには、アセットのアップロード、ダウンロード、編集、公開と、プロパティの表示、編集、アセットの検索が含まれます。

Dynamic Media 限定の機能は次のとおりです。

* [カルーセルバナー](carousel-banners.md)
* [画像セット](image-sets.md)
* [インタラクティブ画像](interactive-images.md)
* [インタラクティブビデオ](interactive-videos.md)
* [混在メディアセット](mixed-media-sets.md)
* [パノラマ画像](panoramic-images.md)

* [スピンセット](spin-sets.md)
* [ビデオ](video.md)
* [Dynamic Media アセットの配信](delivering-dynamic-media-assets.md)
* [アセットの管理](managing-assets.md)
* [クイックビューを使用したカスタムポップアップの作成](custom-pop-ups.md)

[Dynamic Media の設定](administering-dynamic-media.md)も参照してください。

>[!NOTE]
>
>Dynamic Mediaの使用とAEMとのDynamic Media Classicの統合の違いについては、 [Dynamic Media Classic統合とDynamic Media](/help/sites-administering/scene7.md#aem-scene-integration-versus-dynamic-media).

## Dynamic Media が有効な場合と無効な場合の比較 {#dynamic-media-on-versus-dynamic-media-off}

Dynamic Media が有効（オン）になっているかどうかは、次の特徴から判断できます。

* アセットのダウンロードやプレビューで動的レンディションを使用できる。
* 画像セット、スピンセット、混在メディアセットを使用できる。
* PTIFF レンディションが作成されている。

画像アセットをクリックした場合、Dynamic Mediaとはアセットの表示が異なります [有効](config-dynamic.md#enabling-dynamic-media). Dynamic Media では、オンデマンドの HTML5 ビューアが使用されます。

### 動的レンディション {#dynamic-renditions}

「**[!UICONTROL 動的]**」の下にある画像プリセットやビューアプリセットなどの動的レンディションは、Dynamic Media が有効な場合に使用できます。

![chlimage_1-358](assets/chlimage_1-358.png)

### 画像セット、スピンセット、混在メディアセット {#image-sets-spins-sets-mixed-media-sets}

画像セット、スピンセットおよび混在メディアセットは、Dynamic Media が有効な場合に使用できます。

![chlimage_1-359](assets/chlimage_1-359.png)

### PTIFF レンディション {#ptiff-renditions}

Dynamic Media 対応のアセットには `pyramid.tiffs` が含まれています。

![chlimage_1-360](assets/chlimage_1-360.png)

### アセットのビューの変化 {#asset-views-change}

Dynamic Media を有効にすると、「`+`」ボタンをクリックしてズームインし、「`-`」ボタンをクリックしてズームアウトすることができます。クリックまたはタップして、特定の領域にズームインすることもできます。元に戻すアイコンをクリックすると元のバージョンに戻ります。また、斜めの矢印をクリックすると、画像を全画面表示にすることができます。Dynamic Media を有効にした場合の画面は次のようになります。

![chlimage_1-361](assets/chlimage_1-361.png)

Dynamic Media を無効にした場合は、次のようにズームイン、ズームアウトおよび元のサイズに戻す操作が可能です。

![chlimage_1-362](assets/chlimage_1-362.png)
