---
title: Dynamic Media アセットの配信
seo-title: Delivering Dynamic Media Assets
description: Dynamic Media アセットの配信方法について説明します
seo-description: Learn how to deliver dynamic media assets
uuid: e87754a9-4c34-4658-9971-cd7ceb26523f
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.4/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: ec394bd3-2fa6-4f50-b974-bc10f643ecac
exl-id: e5110a90-ddc9-4244-8466-f91adfca8469
feature: Asset Management
role: User
source-git-commit: 5d96c09ef764b02e08dcdf480da1ee18f4d9a30c
workflow-type: tm+mt
source-wordcount: '317'
ht-degree: 44%

---

# Dynamic Media アセットの配信 {#delivering-dynamic-media-assets}

ビデオと画像の両方の Dynamic Media アセットの配信方法は、Web サイトの実装方法によって異なります。

Dynamic Mediaでは、次の複数のオプションを使用できます。

* Web サイトがAEM上でホストされている場合、Dynamic Media アセットをページに直接追加する必要があります。
* Web サイトが AEM 上にない場合は、次のいずれかの方法を選択します。

   * Web サイトへのビデオまたは画像の埋め込み。
   * Web アプリケーションに URL をリンクします。ビデオプレーヤーをポップアップウィンドウまたはモーダルウィンドウとして配信する場合には、リンク機能を使用します。
   * レスポンシブサイトの場合は、[最適化された画像を配信できます。](responsive-site.md)

>[!NOTE]
>
>スマートイメージングは、既存の画像プリセットで機能し、配信の直前にインテリジェンスを使用して、ブラウザーまたはネットワークの接続速度に基づいて画像のファイルサイズをさらに低減します。詳しくは、[スマートイメージング](imaging-faq.md)を参照してください。

詳しくは、次のトピックを参照してください。

* [Web ページへのDynamic Media Assets の追加](adding-dynamic-media-assets-to-pages.md)
* [Web ページへのビデオビューアまたは画像ビューアの埋め込み](embed-code.md)
* [Dynamic Media でのホットリンク保護の有効化](https://experienceleague.adobe.com/docs/experience-manager-64/assets/dynamic/hotlink-protection.html?lang=ja#dynamic)
* デジタル非表示透かし (Digimarc) とDynamic Mediaの統合（近日公開）
* [Web アプリケーションへの URL のリンク](linking-urls-to-yourwebapplication.md)
* [レスポンシブサイト用に最適化された画像の配信](responsive-site.md)
* [コンテンツの HTTP/2 配信](http2.md)
* [CDN にキャッシュされたコンテンツの無効化](invalidate-cdn-cached-content.md)
* [ルールセットを使用した URL の変換](using-rulesets-to-transform-urls.md)

## Dynamic Media アセットの HTTP/2 配信 {#http-delivery-of-dynamic-media-assets}

AEMは、HTTP/2 経由でのすべてのDynamic Mediaコンテンツ（画像とビデオ）の配信をサポートするようになりました。 つまり、画像やビデオの公開済み URL または埋め込みコードを、ホストされているアセットを受け入れる任意のアプリケーションと統合できるようになります。 その公開済みアセットは、HTTP/2 プロトコルを使用して配信されます。 この配信方法を使用すると、ブラウザーとサーバーの通信方法が改善され、すべてのDynamic Mediaアセットの応答時間と読み込み時間が向上します。

詳しくは、 [コンテンツの HTTP/2 配信に関するよくある質問](/help/sites-administering/scene7-http2faq.md) を参照してください。
