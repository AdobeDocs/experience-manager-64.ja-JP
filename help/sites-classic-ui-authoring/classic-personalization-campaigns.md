---
title: キャンペーンの管理
seo-title: Campaign Management
description: キャンペーン管理は、デジタルマーケターに対して、パーソナライズされたコンテンツを配信し、訪問者に向けた専用のエクスペリエンスを作成する機会を提供します。 Web、E メール、モバイルサービスにわたってマーケティングキャンペーンを調整し、訪問者を惹きつけることができます。
seo-description: Campaign management provides digital marketers the opportunity to deliver personalized content and so create dedicated experiences for visitors. It allows you to orchestrate your marketing campaigns across the web, email and mobile services and so engage your visitors.
uuid: 202d614b-a607-45de-8c24-1ee66b230315
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: personalization
content-type: reference
discoiquuid: e8b70971-4f23-45f8-8c23-e147413243c2
exl-id: 2980ec6d-cdd4-4fbd-b4a4-5e45e4508903
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '664'
ht-degree: 40%

---

# キャンペーンの管理 {#campaign-management}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

キャンペーン管理は、デジタルマーケターに対して、パーソナライズされたコンテンツを配信し、訪問者に向けた専用のエクスペリエンスを作成する機会を提供します。

Web、E メール、モバイルサービスにわたってマーケティングキャンペーンを調整し、訪問者を惹きつけることができます。 コンテンツの作成、訪問者のセグメント化、特定のユーザープロファイル向けのターゲットコンテンツのプッシュやプロモーション、複数のチャネルにわたるキャンペーンの管理をおこなうことができます。

このドキュメントでは、キャンペーンを構成する様々な要素について説明します。 詳しくは、次のドキュメントを参照してください。

* [ティーザーと戦略 ](/help/sites-classic-ui-authoring/classic-personalization-campaigns-teasers-strategy.md)
* [メールマーケティング](/help/sites-classic-ui-authoring/classic-personalization-campaigns-email.md)
* [ランディングページ](/help/sites-classic-ui-authoring/classic-personalization-campaigns-landingpage.md)
* [Target オファー](/help/sites-classic-ui-authoring/classic-personalization-campaigns-target-offers.md)
* [Marketing Campaign Manager の使用 ](/help/sites-classic-ui-authoring/classic-personalization-campaigns-mktg-manager.md)
* [セグメント化について ](/help/sites-classic-ui-authoring/classic-personalization-campaigns-segmentation.md)
* [キャンペーンの設定 ](/help/sites-classic-ui-authoring/classic-personalization-campaigns-setting-up-your.md)

キャンペーン管理は、次の様々な要素で構成されています。

* **ブランド**
AEMでは、ブランドは最上位の単位で、 
**キャンペーン**&#x200B;のコレクションを形成します。

* **Campaigns**
キャンペーンは個別の 
**エクスペリエンス**&#x200B;のコレクションです。

* **エクスペリエンス**
様々なエクスペリエンスを形成するフォーカスされたコンテンツです。 
それぞれの&#x200B;**タッチポイント**&#x200B;で訪問者に表示されます。次のような様々なタイプのエクスペリエンスを使用できます。

   * **ティーザー**
      [ティーザーページ／段落](#teasers)を使用して、特定の訪問者&#x200B;**セグメント**&#x200B;を、その訪問者の関心に基づきフォーカスされたコンテンツに誘導します。

      ティーザーページでは、次のことが可能です。

      * 訪問者が選択できる様々なオプションを提示する
      * 特定の訪問者セグメントに基づくティーザー段落を 1 つだけ表示する。例えば、表示されるティーザー段落は、訪問者の年齢によって異なる場合があります。

      通常、ティーザーページは、次のティーザーページに置き換えられるまで、特定の期間持続する一時的なアクションです。

   * **ニュースレター**

      [メール通信](#emailmarketing)を使用してユーザーとの関係を深め、web サイトを訪問するよう促します。通常はニュースレターの形式で&#x200B;**リード**（通常は&#x200B;**リスト**&#x200B;にグループ化されます）に送信されます。**注意：**&#x200B;この機能がさらに強化される予定はありません。[Adobe Campaign や AEM との統合を利用](/help/sites-administering/campaign.md)することをお勧めします。

   * **Adobe Target**

       Adobe Target （旧称 Test&amp;Target）と統合します。これにより、マーケティング担当者はコンバージョン web サイト最適化ツールを使用できるようになります。このツールには、オンラインコンテンツおよびオファーと顧客との関連性を継続的に高め、より多くのコンバージョンを生み出すために必要な機能があります。Adobe Target の直感的なインターフェイスにより、テストのデザインと実行、オーディエンスセグメントの作成、およびコンテンツのターゲット設定ができます。これらの機能はすべて 1 つのアプリケーションから提供されます。


* **タッチポイント**

   これらは、訪問者とキャンペーンの間の連絡先です。 タッチポイントは、作成したエクスペリエンスに関連付けられています。

   例えば、ティーザーの場合はティーザー段落が配置されているコンテンツページで、ニュースレターの場合はメーリングリストです。

* **リード数**

   訪問者について収集した情報で、これらの訪問者への連絡方法がリードの基盤となります。**注意：**&#x200B;この機能がさらに強化される予定はありません。

   [Adobe Campaign や AEM との統合を利用](/help/sites-administering/campaign.md)することをお勧めします。

* **リスト**

   リードは通常、リストにグループ分けされ、これらのリード全体に対してアクションを実行することができます。**注意：**&#x200B;この機能がさらに強化される予定はありません。

   [Adobe Campaign の利用や AEM との統合環境の利用](/help/sites-administering/campaign.md)をお勧めします。

* **セグメント**

   サイト訪問者がサイトに来訪したときの興味や目標は異なります。 Web サイト上のアクティビティ、登録されたプロファイル情報、他の Web サイト上のアクティビティなどの要因に基づいてこれを分析すると、セグメントを定義するのに役立ちます。 一致するセグメントに応じて、訪問者のニーズと興味に特別にターゲットしたコンテンツを作成できます。

* **MCM**

   マーケティングキャンペーンマネージャー (MCM) は、キャンペーン、ブランド、エクスペリエンス、タッチポイント、リード、リスト、セグメントおよびレポートの作成および制御に必要なすべての機能にアクセスできるコンソールです。

   様々な場所 ( **キャンペーン**) またはを次の URL などに置き換えます。

   `http://localhost:4502/libs/mcm/content/admin.html`
