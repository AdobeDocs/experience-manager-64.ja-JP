---
title: コンテンツの HTTP/2 配信の FAQ
description: HTTP/2 コンテンツ配信について説明します。
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: integration
content-type: reference
exl-id: 2da4c0b3-119e-436e-9f03-f794283e9a37
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '820'
ht-degree: 72%

---

# コンテンツの HTTP/2 配信の FAQ{#http-delivery-of-content-faq}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

コンテンツの HTTP/2 配信が可能になったことをお知らせします。HTTP/2 を使用すると、パフォーマンスが全体的に向上します。

## HTTP/2 とは  {#what-is-http}

HTTP/2 によりブラウザーとサーバーの通信が改善され、必要な処理能力を抑えながら情報をより高速に転送できます。

次の Web サイトでは、HTTP/2 とその利点について簡単かつ簡単に説明します。

[https://www.engadget.com/2015/02/24/what-you-need-to-know-about-http-2/](https://www.engadget.com/2015/02/24/what-you-need-to-know-about-http-2/)

## コンテンツ配信を HTTP/2 に移行する主なメリット  {#what-are-the-key-benefits-of-moving-to-http-for-content-delivery}

パフォーマンスの向上は、Web サイトのコード、Dynamic Mediaの使用方法、消費者のデバイス、画面、場所などの要因によって大きく異なります。

アドビ独自のテストでは、以下の結果が出ています。

* 画像の場合、デバイスおよびブラウザーに応じて、応答時間が 7％～28％向上しました。パフォーマンスの最も顕著な向上は、iOSデバイスでした。
* ビューアの場合、読み込み時間のパフォーマンスが 15％向上しました。

次のデモは、HTTP/1 と HTTP/2 の読み込みの違いを示しています。

[https://http2.akamai.com/demo](https://http2.akamai.com/demo)

## HTTP/2 に切り替える資格はありますか？ {#am-i-eligible-to-switch-over-to-http}

HTTP/2 を使用するには、次の要件を満たす必要があります。

* リッチメディアリクエストにセキュア HTTPS を使用している。
* アドビ製品にバンドルされたコンテンツ配信ネットワーク（CDN）を Dynamic Media Classic ライセンスの一部として使用している。
* 汎用の Dynamic Media Classic ドメイン（`s7d1.scene7.com`、`s7d2.scene7.com`、`s7d13.scene7.com` のいずれか）ではなく、専用ドメイン（`images.company.com` または `mycompany.scene7.com`）を使用している。

   ドメインを見つけるには、 [Dynamic Media Classicデスクトップアプリケーション](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/intro/dynamic-media-classic-desktop-app.html?lang=ja#system-requirements-dmc-app). 次に、 **[!UICONTROL 「設定」>「アプリケーション設定」>「一般設定」]**. **公開先サーバー名**&#x200B;というラベルの付いたフィールドを見つけます。現在、汎用の Dynamic Media ドメインを使用している場合は、この切り替えの一環として独自のカスタムドメインへの移行をリクエストできます。

## Dynamic Media Classic アカウントに対して HTTP/2 を有効にする方法  {#what-is-the-process-for-enabling-http-for-my-scene-account}

1. [Admin Console を使用してサポートケースを作成](https://helpx.adobe.com/jp/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html)し、HTTP/2 に切り替えるように要求する必要があります。自動的には切り替わりません。
1. サポートケースには、次の情報を記入してください。

   * 主要連絡先名、メールおよび電話番号。
   * HTTP/2 への切り替えが必要なすべてのドメイン。つまり、`images.company.com` または `mycompany.scene7.com`。

      ドメインを見つけるには、 [Dynamic Media Classicデスクトップアプリケーション](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/intro/dynamic-media-classic-desktop-app.html?lang=ja#system-requirements-dmc-app). 次に、 **[!UICONTROL 「設定」>「アプリケーション設定」>「一般設定」]**. ラベルの付いたフィールドを探します **[!UICONTROL 公開先サーバー名。]**
   **[!UICONTROL 設定／アプリケーション設定／一般設定]**&#x200B;をクリックします。「**[!UICONTROL 公開先サーバー名]**」というラベルの付いたフィールドを見つけます。

   * リッチメディアリクエストにセキュアな HTTPS を使用していることを確認します。
   * 直接の関係で管理されていない、Adobeを通じて CDN を使用していることを確認します。
   * 専用ドメインを使用していることを確認します。つまり、`s7d1.scene7.com`、`s7d2.scene7.com`、`s7d13.scene7.com` などの汎用の Dynamic Media ドメインではなく、`images.company.com` または `mycompany.scene7.com` です。

      ドメインを見つけるには、 [Dynamic Media Classicデスクトップアプリケーション](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/intro/dynamic-media-classic-desktop-app.html?lang=ja#system-requirements-dmc-app). 次に、 **[!UICONTROL 「設定」>「アプリケーション設定」>「一般設定」]**. **[!UICONTROL 公開先サーバー名というラベルの付いたフィールドを見つけます。]**&#x200B;現在、汎用の Dynamic Media ドメインを使用している場合は、この切り替えの一環として独自のカスタムドメインへの移行をリクエストできます。
   1. テクニカルサポートによって、リクエストの送信順に基づいて HTTP/2 の顧客待機リストに追加されます。
   1. アドビでリクエストを処理する準備が整うと、サポートから連絡があり、移行についての調整および完了予定日の設定がおこなわれます。
   1. 完了後に通知があり、HTTP/2 への正常な切り替えを確認できます。



## HTTP/2 への切り替え見込み時期  {#when-can-i-expect-to-be-transitioned-over-to-http}

リクエストは、テクニカルサポートに届いた順に処理されます。

>[!NOTE]
>
>HTTP/2 への切り替えにはキャッシュのクリアが含まれるので、リードタイムが長くなる場合があります。そのため、一度に処理できる顧客の移行は数件のみとなります。

## HTTP/2 への切り替えに伴うリスク {#what-are-the-risks-with-moving-to-http}

HTTP/2 への切り替えには、新しい CDN 設定への移行が伴うので、CDN でキャッシュがクリアされます。

キャッシュされていないコンテンツは、キャッシュが再構築されるまで、Adobeの元のサーバーに直接ヒットします。 このため、元のサーバーからリクエストをプルするときに許容できるパフォーマンスが維持されるように、アドビでは一度に少数の顧客の移行を処理するよう計画します。

## URL または Web サイトが HTTP/2 でアクティベートされていることを確認する方法 {#how-can-you-verify-whether-a-url-or-website-is-activated-with-http}

Web ブラウザーで使用する拡張機能をダウンロードする必要があります。Firefox および Chrome の場合は、「**[!UICONTROL HTTP/2 and SPDY Indicator]**」という拡張機能があります。ブラウザーは HTTP/2 をセキュア接続でのみサポートするので、確認するには https の付いた URL を呼び出す必要があります。この拡張では、HTTP/2 がサポートされている場合、青い稲妻マークおよび「X-Firefox-Spdy: h2」というヘッダーによって示されます。
