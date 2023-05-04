---
title: パーソナライズとコンテンツのターゲティング
seo-title: Personalization and Content Targeting
description: パーソナライズされたコンテンツを AEM で作成する方法を説明します。
seo-description: Learn how AEM can create personalized content
uuid: 3a1aaa3d-5f57-4fb7-a4be-523f0d274b79
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.4/SITES
content-type: reference
topic-tags: personalization
discoiquuid: 850da0da-f7c3-4dd7-bb06-404c14a2a791
exl-id: 669e2509-e563-46ff-b01c-3f05ec196df5
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '555'
ht-degree: 62%

---

# パーソナライズとコンテンツのターゲティング {#personalization}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

## パーソナライゼーションとコンテンツのターゲティング {#personalization-and-content-targeting}

AEM には、ターゲットとなるコンテンツをオーサリングして、パーソナライズされたエクスペリエンスを提供するためのツールのフレームワークが用意されています。

## ターゲティングモード {#targeting-mode}

[AEM のターゲットモードを使用してターゲットコンテンツをオーサリングします。](/help/sites-authoring/content-targeting-touch.md)ターゲティングモードと Target コンポーネントは、マーケティングアクティビティのエクスペリエンス用コンテンツを作成するためのツールを提供します。

## アクティビティ {#activities}

アクティビティは、マーケティング活動を定義し、整理します。 アクティビティは、ターゲットとするオーディエンスと、ターゲティングが適用される期間で構成されます。

たとえば、We.Retail の商品カタログには、季節商品に注目したティーザーが掲載されています。Summer Sports アクティビティは、このティーザーが夏季のターゲットとするマーケティングセグメントを定義します。

アクティビティも [ターゲティングエンジン](/help/sites-authoring/personalization.md#targeting-engine) ページで使用される

ブランドのアクティビティを作成および管理するには、[アクティビティコンソール](/help/sites-authoring/activitylib.md)を使用します。[ターゲットコンテンツをオーサリング](/help/sites-authoring/content-targeting-touch.md)する際に、アクティビティを作成することもできます。

## エクスペリエンス {#experiences}

アクティビティごとに、ターゲットとするオーディエンスを識別する 1 つ以上のエクスペリエンスを定義します。AEM では、各エクスペリエンスを構成するコンテンツを自由に制御できます。

オーディエンスは、AEMまたはAdobe Targetで作成されたマーケティングセグメントに基づいています。 訪問者が Web ページを開く際、ページロジックによってその訪問者が属するオーディエンスが決定され、そのオーディエンス用に作成したコンテンツが表示されます。

例えば、あるアクティビティが「30 歳以上の女性」と「30 歳未満の女性」という 2 つの異なるオーディエンス用のエクスペリエンスを定義するものとします。We.Retail の女性向けページでは、エクスペリエンスごとに異なる商品が表示されます。

アクティビティのエクスペリエンスを定義します。 以下を使用して、 [アクティビティコンソール](/help/sites-authoring/activitylib.md#adding-editing-an-activity-using-the-activities-console) または [ターゲットモード](/help/sites-authoring/content-targeting-touch.md#adding-and-removing-experiences-using-targeting-mode) をクリックして、エクスペリエンスをアクティビティに追加します。

## オファー {#offers}

オファーとは、エクスペリエンスのページ上の場所に表示されるコンテンツです。 様々なエクスペリエンスに異なるオファーを使用して、オーディエンス向けのコンテンツの効果を最大化します。

たとえば、We.Retail サンプル Web サイトの女性向けページでは、オファーをティーザー画像として使用して、ページ上部に表示することができます。30 歳以上の女性向けエクスペリエンスと、30 歳未満の女性向けエクスペリエンスには、それぞれ異なるオファーをティーザーとして使用します。

以下を使用： [オファーコンソール](/help/sites-authoring/offerlib.md) を使用して、複数のエクスペリエンスで使用できるオファーを作成します。 次の場合に、単一使用のオファーを作成するか、オファーライブラリからオファーを追加します。 [ターゲットコンテンツのオーサリング](/help/sites-authoring/content-targeting-touch.md).

## ターゲティングエンジン {#targeting-engine}

ターゲティングエンジンは、ターゲットコンテンツのロジックを駆動するメカニズムです。 使用可能なターゲティングエンジンには AEM と Adobe Target の 2 種類があり、どちらを使用するかは[アクティビティ](/help/sites-authoring/activitylib.md)で設定します。

### AEM {#aem}

AEM は、ページリクエストの処理や、表示コンテンツの判断を行う組み込みのターゲティングエンジンを備えています。AEM ターゲティングエンジンを使用する場合、エクスペリエンスのオーディエンス定義には、AEM で作成されるセグメントのみを使用できます。

### Adobe Target {#adobe-target}

Adobe Target ターゲティングエンジンを使用すると、ページへの訪問から収集された情報が Adobe Target で追跡されます。

* このターゲティングエンジンを使用する場合、エクスペリエンスのオーディエンス定義には、Adobe Target から読み込んだセグメントを使用します。
* Adobe Targetエンジンを使用するアクティビティは、 [Target に同期済み](/help/sites-authoring/activitylib.md#synchronizing-activities-with-adobe-target).

このエンジンを使用できるのは、[Adobe Target と統合](/help/sites-administering/opt-in.md)している場合のみです。
