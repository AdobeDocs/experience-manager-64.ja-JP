---
title: コンテンツの HTTP/2 配信
seo-title: HTTP2 Delivery of Content
description: HTTP/2 によりブラウザーとサーバーの通信が改善され、必要な処理能力を抑えながら情報をより高速に転送できます。
seo-description: HTTP/2 improves the way browsers and servers communicate, allowing for faster transfer of information while reducing the amount of needed processing power.
uuid: d9deb945-bdf5-4d6b-95c8-8bae4442e618
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.4/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: c8e145ad-f021-4043-8190-62151775e296
exl-id: 59cd9f8c-6d01-448d-bf57-bdc9fd2e381b
feature: Asset Management
role: Admin,User
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '741'
ht-degree: 62%

---

# コンテンツの HTTP/2 配信 {#http-delivery-of-content}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

アドビは、パフォーマンスの向上という全体的な利点をもたらすコンテンツの HTTP/2 配信に対応しました。

## HTTP/2 とは  {#what-is-http}

HTTP/2 によりブラウザーとサーバーの通信が改善され、必要な処理能力を抑えながら情報をより高速に転送できます。

次の Web サイトでは、HTTP/2 とそのメリットについて簡単かつ簡単に説明します。

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
* アドビ製品にバンドルされたコンテンツ配信ネットワーク（CDN）を Dynamic Media ライセンスの一部として使用している。
* 専用の（company-h.assetsadobe#.com 以外の）ドメインを使用します。

    既に専用ドメインがある場合、テクニカルサポート経由でオプトインしていただけます。

    専用ドメインがない場合、アドビが 2018 年にお客様の HTTP/2 への切り替えをスケジュールいたします。

## Dynamic Media アカウントに対して HTTP/2 を有効にする方法  {#what-is-the-process-for-enabling-http-for-my-dynamic-media-account}

HTTP/2 に切り替えるためのリクエストを開始する必要があります。自動的にはおこなわれません。

1. HTTP/2 に切り替えるためのテクニカルサポートリクエストを開始します。詳しくは、 [カスタマーサポートポータルへのアクセス](https://helpx.adobe.com/jp/experience-manager/kb/accessing-aem-support-portal.html).

   1. サポートリクエストには、以下の情報を記入してください。

      1. 主要連絡先の氏名、メールアドレス、電話番号。
      1. HTTP/2 への切り替えが必要なすべてのドメイン。
      1. リッチメディアリクエストにセキュアな HTTPS を使用していることを確認します。
      1. Adobeを通じて CDN を使用していること、および直接関係で管理されていないことを確認します。
      1. 専用ドメインを使用していることを確認します。Dynamic Mediaを使用している場合は、既に専用ドメインを使用しています。
   1. テクニカルサポートは、リクエストが送信された順序に基づいて HTTP/2 の顧客待ちリストに追加します。
   1. アドビでリクエストを処理する準備が整うと、サポートから連絡があり、移行についての調整および完了予定日の設定がおこなわれます。
   1. お客様は、完了後の通知で HTTP/2 への切り替えが成功したことを確認できます。

      ブラウザーにはこのことが表示されないので、拡張機能をダウンロードする必要があります。

      Firefox および Chrome の場合は、「HTTP/2 and SPDY Indicator」と呼ばれる拡張機能があります。 ブラウザーは HTTP/2 をセキュア接続でのみサポートするので、確認するには https の付いた URL を呼び出す必要があります。http/2 がサポートされている場合、拡張機能は青いFlash記号とヘッダー「X-Firefox-Spdy」で示されます。&quot;h2&quot;です。


## HTTP/2 への切り替え見込み時期  {#when-can-i-expect-to-be-transitioned-over-to-http}

リクエストは、テクニカルサポートに届いた順に処理されます。

>[!NOTE]
>
>HTTP/2 への切り替えにはキャッシュのクリアが含まれるので、リードタイムが長くなる場合があります。そのため、一度に処理できる顧客の移行は数件のみとなります。

## HTTP/2 への切り替えに伴うリスク {#what-are-the-risks-with-moving-to-http}

HTTP/2 への切り替えには、新しい CDN 設定への移行が伴うので、CDN でキャッシュがクリアされます。

キャッシュされていないコンテンツは、キャッシュが再構築されるまで、Adobeの元のサーバーに直接ヒットします。 このため、元のサーバーからリクエストをプルするときに許容できるパフォーマンスが維持されるように、アドビでは一度に少数の顧客の移行を処理するよう計画します。

## URL または Web サイトが HTTP/2 でアクティベートされていることを確認する方法 {#how-can-you-verify-whether-a-url-or-website-is-activated-with-http}

ブラウザーにはこのことが表示されないので、拡張機能をダウンロードする必要があります。

Firefox および Chrome の場合は、「HTTP/2 and SPDY Indicator」と呼ばれる拡張機能があります。 ブラウザーは HTTP/2 をセキュア接続でのみサポートするので、確認するには https の付いた URL を呼び出す必要があります。http/2 がサポートされている場合、拡張機能は青いFlash記号とヘッダー「X-Firefox-Spdy」で示されます。&quot;h2&quot;です。
