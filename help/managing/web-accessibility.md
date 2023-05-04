---
title: AEM と Web アクセシビリティのガイドライン
seo-title: AEM and the Web Accessibility Guidelines
description: AEMを使用して、アクセシブルな Web サイトやコンテンツを作成する方法について説明します。
seo-description: Learn how to create accessible websites and content with AEM.
uuid: b68281af-3e8a-4842-b762-1c59f9132795
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.4/MANAGING
topic-tags: managing-accessibility, introduction
content-type: reference
discoiquuid: 13c7e0bd-54af-49f3-9743-075ce6f3314d
exl-id: f0ccdeae-3dbb-4dba-89cf-4c8b759da22b
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '520'
ht-degree: 40%

---

# AEM と Web アクセシビリティのガイドライン{#aem-and-the-web-accessibility-guidelines}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

様々な社会的、経済的、法的動機により、Web コンテンツを設計する際には、身体的障碍や制限の有無に関係なく、対象とするオーディエンスができるだけアクセスしやすくことが求められます。そのため、優れた Web デザインの側面として、Web アクセシビリティの重要性が高まってきています。

アクセシブルな Web サイトおよびコンテンツの作成とAEMの影響：

* 管理者は、アクセシビリティ機能が正しく有効化されるよう Adobe Experience Manager（AEM）の設定する必要があります。
* 作成者は、これらの機能を使用して、WCAG 2.0 の主要なガイドラインをサポートする Web サイトを作成します。

   アクセシブルなコンテンツの作成はプロセスです。AEMには機能が用意されていますが、コンテンツ作成者は、アクセシブルなコンテンツを作成するために必要な手法に従う必要があります。

* テンプレート開発者も同様に、Web サイトデザインを実装する際に、こうした問題を認識する必要があります。

## その他の情報 {#further-information}

次のページと節では、情報とガイドラインを示します。

* [アクセシブルなサイトを生成するためのリッチテキストエディターの設定](/help/sites-administering/rte-accessible-content.md)

   アクセシブルなコンテンツを生成するためのAEMの設定方法に関するガイドラインです。

* [アクセシブルなコンテンツ（WCAG 2.0 適合）の作成](/help/sites-authoring/creating-accessible-content.md)

   WCAG 2.0 のガイドラインは、レベル A と AA の適合レベルの達成基準のリストを示しています。 このページでは、AEMがカバーする達成基準と、コンテンツを生成する際の達成基準の達成方法について詳しく説明します。

* [WCAG 2.0 のクイックガイド](/help/managing/qg-wcag.md)

   WCAG 2.0 に関する背景情報です。

* [アクセシブルなアダプティブFormsの作成](/help/forms/using/creating-accessible-adaptive-forms.md)

   Adobe Experience Manager(AEM) には、様々な能力を持つユーザー向けのアダプティブフォームの使いやすさを高めるための様々な機能が含まれています。 このソリューションは、フォーム作成者がアクセスしやすいアダプティブフォームを作成する上でも役立ちます。

## World Wide Web Consortium と WCAG 2.0 {#world-wide-web-consortium-and-wcag}

[World Wide Web Consortium（W3C）](https://www.w3.org/)は、Web 標準の策定を専門とする国際コミュニティです。Web デザイナーや開発者がアクセシブルな Web サイトを作成するのに役立つように、 [Web Accessibility Initiative(WAI)](https://www.w3.org/WAI/) 公開済み [Web コンテンツアクセシビリティガイドライン (WCAG)2.0](https://www.w3.org/TR/WCAG20/) 2008 年 12 月（1999 年に公開）

>[!NOTE]
>
>An [ガイドラインの更新バージョン](https://www.w3.org/TR/WCAG21/) は現在開発中ですが、このバージョンのAEMでは考慮されません。

Adobe Experience Managerを使用すると、コンテンツ作成者や Web サイトの所有者は、WCAG 2.0 レベル A およびレベル AA の達成基準を満たす Web コンテンツを作成できます。

[WCAG 2.0 クイックガイド](/help/managing/qg-wcag.md)で WCAG 2.0 の特定の側面を取り上げています。

### WCAG 2.0 Accessibility 準拠レベル {#wcag-accessibility-conformance-levels}

WCAG 2.0 は [アクセシビリティレベルをカバーするガイドライン（および関連する達成基準）](https://www.w3.org/TR/UNDERSTANDING-WCAG20/conformance.html).

これらはAEMに関連しており、以下の項目でカバーされます。 [レベル A と AA の適合](/help/sites-authoring/creating-accessible-content.md). サイトを作成する際は、サイトの全体的なレベルを特定する必要があります。

>[!NOTE]
>
>特定のタイプのコンテンツに対してすべてのレベル AAA 達成基準を満たすことはできないので、適合の必要なレベルとしてお勧めしません。

## Adobe におけるアクセシビリティ {#accessibility-at-adobe}

詳しくは、[アドビのアクセシビリティリソースセンター](https://www.adobe.com/accessibility/)にアクセスしてください。
