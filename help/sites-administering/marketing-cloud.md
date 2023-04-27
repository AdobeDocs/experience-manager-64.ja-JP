---
title: Adobe Marketing Cloud との統合
description: Adobe Experience Manager と Adobe Marketing Cloud を統合する方法を学びます。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: integration
content-type: reference
exl-id: e2295f71-ea3a-483c-9d7b-29acd151845d
source-git-commit: 8220795bbf0c92ead3bb68dd6f8bbb48cc9ca2cd
workflow-type: tm+mt
source-wordcount: '862'
ht-degree: 50%

---

# Adobe Marketing Cloud との統合{#integrating-with-the-adobe-marketing-cloud}

この [Adobe Marketing Cloud](https://www.adobe.com/jp/solutions/digital-marketing.html)には、オンラインイニシアチブを成功に導くための実用的なリアルタイムのデータとインサイトを提供する、強力な web 分析および web サイト最適化製品が含まれます。 オンラインビジネスの最適化のための統合されたオープンなプラットフォームを提供します。 Cloud は、顧客インサイトの力を収集し、解放して、顧客の獲得、コンバージョン、および保持の取り組みを最適化し、コンテンツの作成と配信をおこなう統合アプリケーションで構成されます。

Adobe Experience Managerを使用すれば、Adobe Marketing Cloudの次の製品とシームレスに統合できます。

* Adobe Analytics：マーケティング担当者は、オンライン戦略やマーケティング戦略に関して、すぐに利用可能なリアルタイムの情報を入手できます。
* Adobe Target：顧客へのオンラインコンテンツの関連性を継続的に高め、より多くのコンバージョンを生み出すための機能をマーケティング担当者に提供します。
* Adobe Dynamic Media Classic は、メディア管理の自動化、web パブリッシングの効率化、および web エクスペリエンスの強化をホストされた環境内で行います。
* Adobe Dynamic Tag Management：アドビやサードパーティのタグをいくつでもすばやく簡単に管理できる直感的なツールをマーケティング担当者に提供します。
<!-- Search&Promote was end of life September 1, 2022. * Adobe Search&Promote gives marketers the ability to control and optimize the search results on their sites. -->
* Adobe Campaign：メール配信コンテンツを Adobe Experience Manager で直接管理できます。

さらに、Adobe Experience Managerを [Creative Cloud](/help/assets/aem-cc-integration-best-practices.md) および [サードパーティのサービス](/help/sites-administering/third-party-services.md).

## Adobe Analytics との統合 {#integrating-with-adobe-analytics}

[Adobe Analytics](https://www.omniture.com/jp/products/analytics/sitecatalyst) は、様々なマーケティングチャネルにまたがるオンライン戦略全体からの統合データを 1 箇所で測定、分析、最適化できる場をディジタルマーケターに提供する、業界最先端のソリューションです。マーケティング担当者は、デジタル戦略やマーケティング施策に関して、すぐに利用可能なリアルタイムの web 分析情報を入手できます。Adobe Analyticsは、Web サイトで最も収益性の高いパスをすばやく特定し、トラフィックをセグメント化して価値の高い Web 訪問者を特定し、訪問者がサイトから出て行く場所を特定し、オンラインマーケティングキャンペーンの重要な成功指標を特定します。

Adobe Analytics を使用すると、サイトのデータを分析できます。

Adobe Analytics との統合によって、次の操作ができるようになります。

* Analytics のユーザートラッキングを有効にする。
* 実行モード（オーサー、パブリッシュなど）をそれぞれ異なるレポートスイートにマッピングする。
* ClientContext 変数をコンバージョン変数またはトラフィックプロパティとして送信します。
* 事前定義済みの変数マッピングを使用します。
* 完全なサイトセクションを一度に設定できます。
* カスタム定義イベントを追跡する。

Adobe Experience Managerと Analytics の統合について詳しくは、 [Adobe Analyticsとの統合](/help/sites-administering/adobeanalytics.md).

[オプトインウィザード](/help/sites-administering/opt-in.md)を使用して簡単に統合を行うこともできます。

## Adobe Target との統合 {#integrating-with-adobe-target}

[Adobe Target](https://www.omniture.com/jp/products/conversion/test-and-target) を使用すると、マーケティング担当者は、オンラインテストをデザインして実行し、行動に基づいたオーディエンスセグメントをその場で作成し、コンテンツとオンラインのエクスペリエンスを自動的にターゲット設定できるようになります。

現在、オンライン消費者は常にニーズを進化させ、幅広いサイトやコンテンツソースから選択できる、関連性の高いパーソナライズされたコンテンツも期待しています。 オンラインオーディエンスを惹きつけるには、どのオファーやコンテンツがオーディエンスに関連し、魅力的かをオンラインマーケターがすばやく特定することが重要です。 この知識に基づいて、マーケターは、サイトを継続的に発展させ、適切なコンテンツを様々なオーディエンスにターゲット設定する機能が必要になります。

[Adobe Targetとの統合](/help/sites-administering/target.md) では、サイトをAdobe Targetと統合する方法について説明します。

[オプトインウィザード](/help/sites-administering/opt-in.md)を使用して簡単に統合を行うこともできます。

## Analytics と Target のオプトイン {#opting-in-to-analytics-and-target}

Adobe Experience Managerは、Adobe AnalyticsおよびAdobe Targetと統合するための簡単なオプトイン手順を提供します。 管理者としてログインし、プロジェクトコンソールにアクセスすると、オプトインウィザードが表示されます。

![chlimage_1-107](assets/chlimage_1-107.png)

Analytics や Target との統合をオプトインして、ページトラッキング機能、分析機能、パーソナライゼーション機能を使用できるようにします。 オプトイン時に、ユーザーアカウント情報を入力し、追跡するページを指定する必要があります。

詳しくは、 [Adobe AnalyticsとAdobe Targetのオプトイン。](/help/sites-administering/opt-in.md)

##  Dynamic Media Classic との統合 {#integrating-with-scene}

Adobe Dynamic Media Classic は、動的なマーケティングアセットやリッチなビジュアルマーチャンダイジングを公開、管理、強化したり、web、モバイル、メール、ソーシャルメディア、インターネットに接続されたディスプレイやプリンターへ配信したりするためのホスト型ソリューションです。

Adobe Experience Manager では、デジタルアセットを Adobe Experience Manager から Dynamic Media Classic に直接公開でき、Dynamic Media Classic から Adobe Experience Manager にも公開できます。

また、Dynamic Media Classic に公開された Adobe Experience Manager アセットを、ベーシックズームやビデオなどの様々なビューアで表示できます。

Adobe Experience ManagerとDynamic Media Classicの統合について詳しくは、 [Dynamic Media Classicとの統合](/help/sites-administering/scene7.md) ドキュメント。

## Adobe Dynamic Tag Management との統合 {#integrating-with-adobe-dynamic-tag-management}

[Adobe Dynamic Tag Management](https://www.adobe.com/jp/solutions/digital-marketing/dynamic-tag-management.html) は直感的なツールであり、このツールを使用することでマーケティング担当者は、アドビやサードパーティのタグを数に制限なく、すばやく簡単に管理できます。ほぼすべてのオンラインアセットをより細かく、より柔軟に最適化でき、かつ IT リソースへの依存度を減らすことができます。

[統合AdobeダイナミックTag Management](/help/sites-administering/dtm.md) Adobe Experience Managerを使用して、Dynamic Tag Management Web プロパティを使用してAdobe Experience Managerサイトを追跡できるようにします。

## Adobe Audience Manager との統合 {#integrating-with-adobe-audience-manager}

Audience Managerの統合は、Adobe Experience Manager 6.3 で削除されました。

<!-- Search&Promote was end of life September 1, 2022. ## Integrating with Search&Promote {#integrating-with-search-promote} -->

<!-- Search&Promote was end of life September 1, 2022. Adobe Search&Promote enables marketers to optimize how visitors browse, find, compare, and select relevant products and content on web and mobile sites. Businesses can easily promote priority items based on business objectives and visitor intent, as well as automate merchandising and promotions activity by way of KPI-based triggers or metrics. -->

<!-- Search&Promote was end of life September 1, 2022. Adobe Search&Promote is a reliable and scalable hosted site search application, capable of scaling to millions of pages or products, for heavily visited online businesses ranging from retail to news sites. It offers unprecedented levels of marketer control and metrics-based relevance. -->

<!-- Search&Promote was end of life September 1, 2022. For information about integrating Adobe Experience Manager and Search&Promote, see [Integrating with Adobe Search&Promote](/help/sites-administering/search-and-promote.md). -->

## Adobe Campaign との統合 {#integrating-with-adobe-campaign}

[Adobe Campaign](https://www.adobe.com/jp/solutions/campaign-management.html) では、メール配信コンテンツを Adobe Experience Manager で直接管理できます。

Adobe Experience ManagerとAdobe Campaignの統合について詳しくは、 [Adobe Campaignとの統合](/help/sites-administering/campaignstandard.md).
