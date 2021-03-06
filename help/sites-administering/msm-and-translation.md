---
title: Web サイト管理
seo-title: Website Administration
description: AEM での多言語 Web サイトの管理方法について説明します。
seo-description: Learn how to manage multilingual websites in AEM.
uuid: a32d458b-a5ad-46ef-a68c-4717c63b4bdd
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: site-features
content-type: reference
discoiquuid: fabaa3e8-1657-4ed4-abb2-990117bec39c
exl-id: e8f83d21-b55e-4415-a581-8df1b71a84b1
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '341'
ht-degree: 100%

---

# Web サイト管理{#website-administration}

Web サイトとページを管理するための以下の管理ツールが用意されています。

* マルチサイトマネージャー（MSM）を使用すると、同じサイトコンテンツを複数の場所で使用できるだけでなく、場所によってバリエーションを持たせることができます。

   * [コンテンツの再利用：マルチサイトマネージャとライブコピー](/help/sites-administering/msm.md)

* 翻訳を使用すると、ページコンテンツ、アセット、ユーザー生成コンテンツの翻訳を自動化して、多言語 Web サイトの作成と管理ができます。

   * [多言語サイトのコンテンツの翻訳](/help/sites-administering/translation.md)

* Web サイトを[多国籍化かつ多言語化](#multinational-and-multilingual-sites)するために、これらの 2 つの機能を組み合わせて使用できます。

## 多国籍な多言語サイト {#multinational-and-multilingual-sites}

マルチサイトマネージャと翻訳ワークフローを併せて使用することで、多国籍な多言語サイトのコンテンツを効率的に作成できます。特定の国向けのマスターサイトを 1 つの言語で作成してから、そのコンテンツをベースに、必要に応じて翻訳を使用して他のサイトを作成します。

* マスターサイトを別の言語に[翻訳](/help/sites-administering/translation.md)します。

* [マルチサイトマネージャ](/help/sites-administering/msm.md)を次の用途で使用します。

   * マスターサイトのコンテンツと翻訳を再利用して、他の国や文化のサイトを作成します。
   * マルチサイトマネージャーの使用は、1 言語のコンテンツに限定してください（例：英語のマスターは英語圏の各国サイト、フランス語のマスターはフランス語圏の各国サイト）。
   * 必要に応じて、ライブコピーの要素を分離してローカリゼーションの詳細を追加します。

次の図に、主な概念がどのように関連するかを示します（関連するすべてのレベルと要素を網羅しているわけではありません）。

![chlimage_1-71](assets/chlimage_1-71.png)

>[!NOTE]
>
>このようなシナリオでは、MSM は異なる言語バージョンを管理することはありません。
>
>* [MSM](/help/sites-administering/msm.md) は言語の境界内で、ブループリント（グローバルマスターなど）からライブコピー（ローカルサイトなど）への翻訳されたコンテンツのデプロイメントを管理します。
>* AEM の[翻訳](/help/sites-administering/translation.md)統合機能は、サードパーティの翻訳管理サービスと連係して、各言語およびそれらの言語へのコンテンツの翻訳を管理します。
>
>より高度な使用事例の場合は、MSM を複数の言語マスターにまたがって使用することもできます。

>[!NOTE]
>
>いずれの使用例の場合も、次のベストプラクティスをお読みになることをお勧めします。
>
>* [MSM のベストプラクティス](/help/sites-administering/msm-best-practices.md)（特に次の事項）
>
>   * [サイトの作成](/help/sites-administering/msm-best-practices.md#create-site)
>   * [MSM と多言語の Web サイト](/help/sites-administering/msm-best-practices.md#msm-and-multilingual-websites)
>
>* [翻訳のベストプラクティス](/help/sites-administering/tc-bp.md)

