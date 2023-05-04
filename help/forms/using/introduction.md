---
title: HTML5 フォームの概要
seo-title: Introduction to HTML5 forms
description: HTML5 フォームは、Adobe Experience Manager 6.0(AEM 6.0) ソフトウェアの新しい機能で、XFA フォームテンプレートをHTML5 形式でレンダリングする機能を提供します。
seo-description: HTML5 forms is a new capability in Adobe Experience Manager 6.0 (AEM 6.0) software that offers rendering of XFA form templates in HTML5 format.
uuid: a68f1ca1-32dd-48f9-9359-8f09abd1c3de
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: hTML5_forms
discoiquuid: b8cd2656-8bc2-4bd7-a3d6-dc76b0a2d429
feature: Mobile Forms
exl-id: c69b5ae6-c5c5-46df-8290-3e41470cd09e
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '450'
ht-degree: 31%

---

# HTML5 フォームの概要 {#introduction-to-html-forms}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

HTML5 フォームは、Adobe Experience Manager 6.0(AEM 6.0) ソフトウェアの新しい機能で、XFA フォームテンプレートをHTML5 形式でレンダリングする機能を提供します。 この機能により、XFA ベースの PDF がサポートされていないモバイルデバイスおよびデスクトップブラウザー上のフォームのレンダリングが可能です。HTML5 フォームは、XFA フォームテンプレートの既存の機能をサポートするだけでなく、モバイルデバイス用に手書き署名などの新しい機能を追加します。

HTML5 フォームは、標準のHTML5 構成に基づいてドキュメントを生成します。 HTML5 フォームは、HTML5 をサポートする最新のすべてのブラウザーで表示できます。 ブラウザーのための追加のブラウザープラグインをインストールする必要がありません。サポートされるブラウザーについて詳しくは、[サポートされるクライアントプラットフォーム](https://adobe.com/go/learn_aemforms_documentation_63_jp)を参照してください。

![](do-not-localize/mobile_form_on_an_ipad_date_14.png)

## HTML5 フォームの主な機能 {#key-capabilities-of-html-forms-br}

* 互換性のあるすべてのブラウザーでサポートされているHTML5 の既存の XFA フォームをレンダリングします。
* 標準の XFA フォームデザイン機能を活用して、モバイルデバイス用のフォームをターゲットにします。
* 動的 XFA 機能をHTML5 形式で使用します。
* 高精度のSVGテキストレイアウト (SVG1.1) を使用して、PDFテキストレイアウトと一致させます。
* JavaScript および FormCalc のサポートを提供します。
* データ駆動型のイベントまたはユーザー入力に基づいて、フラグメントをインタラクティブなフォームに動的にアセンブリします。
* 企業の標準に従ってフォームの外観に合わせたカスタム CSS をサポートします。
* カスタムウィジェットを有効にして、豊富なデータキャプチャエクスペリエンスを提供します。
* Web アプリへの統合をサポートします。

### マルチチャネル公開 {#multichannel-publishing}

フォーム開発者は、XFA テンプレートを使用して、フォームをPDFおよびHTML5 形式でレンダリングできます。 この機能は、HTML5 フォームのデザインプラクティスに合わせて最小限の変更を加える必要がある大規模な XFA フォームセットがある場合に便利です。 既存の XFA フォームをHTML5 にレンダリングして、XFA ベースのPDFがまだサポートされていない様々なデバイスをターゲットに設定できます。

## HTML5 フォームの管理 {#manage-html-forms}

AEMには、AEM Forms UI を使用してすべてのフォームテンプレートを一覧表示および管理するための統合ビューも用意されています。 フォームのアクティベート、アクティベート解除、公開、プレビューを行うことができます。 詳しくは、 [フォーム管理の概要](/help/forms/using/introduction-managing-forms.md).

### Formsのカスタマイズ {#forms-customization}

HTML5 forms は、標準のテンプレート 5 構成を使用してフォームHTMLをレンダリングします。 これにより、Web テクノロジ、主にCSS および JavaScript を使用した、HTML5 形式のフォームの拡張およびカスタマイズが容易になります。既存のウィジェットの外観を簡単にカスタマイズし、独自のウィジェットを作成するか、フォームのカスタムスタイルを使用できます。カスタムウィジェットの作成、および既存のウィジェットのカスタマイズについて詳しくは、[HTML5 フォームのプラグインカスタムウィジェット](/help/forms/using/custom-widgets.md)を参照してください。
