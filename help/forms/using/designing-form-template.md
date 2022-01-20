---
title: HTML5 フォーム用のフォームテンプレートのデザイン
seo-title: Designing form templates for HTML5 forms
description: 'AEM Forms は、HTML5 形式への XFA フォームテンプレートのレンダリングを提供します。フォームデザイナーは Designer を使用してフォームテンプレートをデザインし、HTML5 レンダリングの機能を使用することができます。 '
seo-description: AEM Forms offers rendering XFA form template to HTML5 format. Form designers can design form templates using Designer and use the HTML5 rendition capability.
uuid: 41a00ec5-d7f9-4717-a961-00d20d8e7b2a
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: hTML5_forms
discoiquuid: e135fa01-fede-4285-b4dd-2d23acbb4d26
feature: Mobile Forms
exl-id: 248e56c7-51b7-41d3-8bc9-a5d737bf178b
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '343'
ht-degree: 64%

---

# HTML5 フォーム用のフォームテンプレートのデザイン {#designing-form-templates-for-html-forms}

AEM の HTML5 フォームコンポーネントは、HTML5 形式への XFA フォームテンプレートのレンダリングを提供します。フォームデザイナーは [Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63) を使用してフォームテンプレートをデザインし、HTML5 レンダリングの機能を使用することができます。これらのフォームテンプレートはアセットとともに、AEM リポジトリやファイルシステムに配置するか、http で公開することができます。ただし、Forms Manager を使用してフォームを管理する場合は、テンプレートとアセットをAEMリポジトリに格納する必要があります。

HTML5 フォームの動作は、その大部分が PDF フォームの動作に一致していますが、両方の形式には他方の形式で適用されない機能がいくつかあります。例えば、Adobe ReaderのPDFフォームにバーコードを適用する方法は、Mobile フォームとは異なる場合や、フォームの電子署名の方法も形式によって異なります。 このようなバリエーションについて詳しくは、 [HTML5 フォームとPDF formsの機能の違い](/help/forms/using/feature-differentiation-html5-forms-pdf-forms.md).

一般的な XFA 機能の場合、両方の形式で機能するフォームをデザインするために、次のベストプラクティスとガイドラインを参照してください。

## AEM Forms Designer の HTML5 フォーム向けの機能 {#capabilities-in-aem-forms-designer-for-html-forms}

### HTML のブレビュー {#preview-html}

フォームデザイナーのデザインモードに、HTML5 形式でフォームをプレビューするための「Preview HTML」タブが追加されました。AEM Forms Designer でこの機能を有効化して設定する方法について詳しくは、「[HTML のプレビュー](/help/forms/using/preview-xdp-forms-html.md)」を参照してください。

### 手書き署名 {#scribble-signature}

HTML5 フォームの主な対象はタッチデバイスです。そのため、AEM Forms Designer に新しい手書き署名コントロールが追加されました。手書き署名コントロールをフォームテンプレート上でクリックまたはドラッグ&amp;ドロップし、設定することができます。 これは Scribble フィールドとしてHTML5 レンディションでレンダリングされ、タッチデバイスでの手書き署名に使用できます。 デスクトップマシンでは、それはマウスコントロールの使用により手書きフィールドとして使用できます。この機能の使用方法について詳しくは、 [XFA 手書きフィールド](/help/forms/using/scribble-signature.md).

![4](assets/4.png)
