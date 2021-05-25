---
title: AEM と Web アクセシビリティのガイドライン
seo-title: AEM と Web アクセシビリティのガイドライン
description: AEM を使用して、アクセスしやすい Web サイトおよびコンテンツを作成する方法を学習します。
seo-description: AEM を使用して、アクセスしやすい Web サイトおよびコンテンツを作成する方法を学習します。
uuid: b68281af-3e8a-4842-b762-1c59f9132795
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.4/MANAGING
topic-tags: managing-accessibility, introduction
content-type: reference
discoiquuid: 13c7e0bd-54af-49f3-9743-075ce6f3314d
exl-id: f0ccdeae-3dbb-4dba-89cf-4c8b759da22b
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '500'
ht-degree: 85%

---

# AEM と Web アクセシビリティのガイドライン{#aem-and-the-web-accessibility-guidelines}

様々な社会的、経済的、法的動機により、Web コンテンツを設計する際には、身体的障碍や制限の有無に関係なく、対象とするオーディエンスができるだけアクセスしやすくことが求められます。そのため、優れた Web デザインの側面として、Web アクセシビリティの重要性が高まってきています。

AEM を使用して、アクセスしやすい Web サイトおよびコンテンツを作成する場合、次のような影響があります。

* 管理者は、アクセシビリティ機能が正しく有効化されるよう Adobe Experience Manager（AEM）の設定する必要があります。
* 作成者は、これらの機能を使用してWCAG 2.0の主要なガイドラインをサポートするWebサイトを作成します。

   アクセシブルなコンテンツの作成はプロセスです。AEM には各種機能が用意されていますが、コンテンツ作成者は、アクセスしやすいコンテンツを作成するために必要な手法に従う必要があります。

* テンプレート開発者も同様に、Web サイトデザインを実装する際に、こうした問題を認識する必要があります。

## その他の情報 {#further-information}

情報とガイドラインは、次のページおよびセクションにまとめられています。

* [アクセシブルなサイトを生成するためのリッチテキストエディターの設定](/help/sites-administering/rte-accessible-content.md)

   アクセシブルなコンテンツを生成するためのAEMの設定方法に関するガイドラインです。

* [アクセシブルなコンテンツ（WCAG 2.0 適合）の作成](/help/sites-authoring/creating-accessible-content.md)

   WCAG 2.0のガイドラインは、レベルAとAAの適合レベルの達成基準のリストを示しています。 このページでは、AEM がカバーしている達成基準を詳しく取り上げるとともに、コンテンツ生成時にそれらの達成基準を満たす方法について説明しています。

* [WCAG 2.0 クイックガイド](/help/managing/qg-wcag.md)

   WCAG 2.0に関する背景情報です。

* [アクセシブルなアダプティブFormsの作成](/help/forms/using/creating-accessible-adaptive-forms.md)

   Adobe Experience Manager (AEM) は、障害を持つ様々なユーザーに対するアダプティブフォームの可用性を向上するためのさまざまな特長や機能を備えています。このソリューションは、フォーム作成者がアクセスしやすいアダプティブフォームを作成する上でも役立ちます。

## World Wide Web Consortium および WCAG 2.0 {#world-wide-web-consortium-and-wcag}

[World Wide Web Consortium（W3C）](https://www.w3.org/)は、Web 標準の策定を専門とする国際コミュニティです。アクセスしやすい Web サイトの作成を担当する Web デザイナーや開発者を支援する目的で、[Web Accessibility Initiative（WAI）](https://www.w3.org/WAI/)は 2008 年 12 月に [Web Content Accessibility Guidelines（WCAG）2.0](https://www.w3.org/TR/WCAG20/) を公開しました（1999 年に公開された元のバージョンを更新）。

>[!NOTE]
>
>[更新版のガイドライン](https://www.w3.org/TR/WCAG21/)は現在作成中ですが、このバージョンの AEM については考慮されていません。

Adobe Experience Manager を使用すると、コンテンツ作成者や Web サイトの所有者は、WCAG 2.0 レベル A およびレベル AA の達成基準を満たす Web コンテンツを作成できます。

[WCAG 2.0 クイックガイド](/help/managing/qg-wcag.md)で WCAG 2.0 の特定の側面を取り上げています。

### WCAG 2.0 アクセシビリティ適合レベル  {#wcag-accessibility-conformance-levels}

WCAG 2.0 には、[該当するアクセシビリティレベルをカバーするガイドライン（および関連する達成基準）](https://www.w3.org/TR/UNDERSTANDING-WCAG20/conformance.html)が規定されています。

これらはAEMに関連しており、[レベルAとAA適合](/help/sites-authoring/creating-accessible-content.md)で扱われます。 サイトを作成する際は、サイトの全体的なレベルを特定する必要があります。

>[!NOTE]
>
>特定のタイプのコンテンツでは、レベル AAA のすべての達成基準を満たすことはできないので、適合すべきレベルとしてお勧めすることはできません。

## Adobe におけるアクセシビリティ {#accessibility-at-adobe}

詳しくは、[アドビのアクセシビリティリソースセンター](https://www.adobe.com/accessibility/)にアクセスしてください。
