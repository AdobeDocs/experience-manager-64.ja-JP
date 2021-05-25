---
title: Dynamic Media アセットの配信
seo-title: Dynamic Media アセットの配信
description: Dynamic Media アセットの配信方法を学習します
seo-description: Dynamic Media アセットの配信方法を学習します
uuid: e87754a9-4c34-4658-9971-cd7ceb26523f
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.4/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: ec394bd3-2fa6-4f50-b974-bc10f643ecac
exl-id: e5110a90-ddc9-4244-8466-f91adfca8469
feature: アセット管理
role: Business Practitioner
source-git-commit: f9faa357f8de92d205f1a297767ba4176cfd1e10
workflow-type: tm+mt
source-wordcount: '330'
ht-degree: 91%

---

# Dynamic Media アセットの配信 {#delivering-dynamic-media-assets}

ビデオでも画像でも、Dynamic Media アセットの配信方法は、Web サイトの実装方法によって異なります。

Dynamic Media を使用する場合、次の複数のオプションがあります。

* Web サイトが AEM 上にホストされている場合は、Dynamic Media アセットを直接ページに追加します。
* Web サイトが AEM 上にない場合は、次のいずれかの方法を選択します。

   * ビデオまたは画像を Web サイトに埋め込みます。
   * Web アプリケーションに URL をリンクします。ビデオプレーヤーをポップアップウィンドウまたはモーダルウィンドウとして配信する場合には、リンク機能を使用します。
   * レスポンシブサイトの場合は、[最適化された画像を配信できます。](responsive-site.md)

>[!NOTE]
>
>スマートイメージングは、既存の画像プリセットで機能し、配信の直前にインテリジェンスを使用して、ブラウザーまたはネットワークの接続速度に基づいて画像のファイルサイズをさらに低減します。詳しくは、[スマートイメージング](imaging-faq.md)を参照してください。

詳しくは、次のトピックを参照してください。

* [WebページへのDynamic Media Assetsの追加](adding-dynamic-media-assets-to-pages.md)
* [Webページへのビデオビューアまたは画像ビューアの埋め込み](embed-code.md)
* [Dynamic Media でのホットリンク保護の有効化](https://experienceleague.adobe.com/docs/experience-manager-64/assets/dynamic/hotlink-protection.html?lang=ja#dynamic)
* デジタル非表示透かし(Digimarc)とDynamic Mediaの統合（近日公開）
* [Web アプリケーションへの URL のリンク](linking-urls-to-yourwebapplication.md)
* [レスポンシブサイト用に最適化された画像の配信](responsive-site.md)
* [コンテンツの HTTP/2 配信](http2.md)
* [CDN にキャッシュされたコンテンツの無効化](invalidate-cdn-cached-content.md)
* [ルールセットを使用した URL の変換](using-rulesets-to-transform-urls.md)

## Dynamic Media アセットの HTTP/2 配信 {#http-delivery-of-dynamic-media-assets}

AEM は現在、HTTP/2 上でのすべての Dynamic Media コンテンツ（画像とビデオ）の配信をサポートしています。つまり、画像やビデオの公開済み URL や埋め込みコードは、ホストされるアセットを受け取るアプリケーションとの統合に使用できます。その公開済みアセットは、その後、HTTP/2 プロトコルで配信されます。この配信方法により、ブラウザーとサーバーの通信が向上し、すべての Dynamic Media アセットの応答時間と読み込み時間が短くなります。

詳しくは、[コンテンツの HTTP/2 配信に関する FAQ](/help/sites-administering/scene7-http2faq.md) を参照してください。
