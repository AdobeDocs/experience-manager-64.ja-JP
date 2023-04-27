---
title: HTML5 フォーム用のフォームテンプレートのデザイン
seo-title: Designing form templates for HTML5 forms
description: AEM Formsオファーは、XFA フォームテンプレートをHTML5 形式にレンダリングします。 フォームデザイナーは、Designer を使用してフォームテンプレートをデザインし、HTML5 のレンディション機能を使用できます。
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
ht-degree: 54%

---

# HTML5 フォーム用のフォームテンプレートのデザイン {#designing-form-templates-for-html-forms}

AEMのHTML5 フォームコンポーネントは、XFA フォームテンプレートをHTML5 形式にレンダリングする機能を提供します。 フォームデザイナーは、 [Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63_jp) とは、HTML5 のレンディション機能を使用します。 これらのフォームテンプレートは、アセットと共に、AEMリポジトリやファイルシステムに配置することも、http 経由で公開することもできます。 ただし、Forms Manager を使用してフォームを管理する場合には、テンプレートとアセットを AEM リポジトリに置く必要があります。

HTML5 フォームの動作は、その大部分が PDF フォームの動作に一致していますが、両方の形式には他方の形式で適用されない機能がいくつかあります。たとえば、Adobe Reader でバーコードが PDF フォームに適用される方法が Mobile フォームとは異なったり、フォームにデジタル署名を行う方法も各形式で異なります。そのような違いについて詳しくは、[HTML5 フォームと PDF フォームの機能の違い](/help/forms/using/feature-differentiation-html5-forms-pdf-forms.md)を参照してください。

XFA の一般的な機能については、次のベストプラクティスとガイドラインを参照して、両方の形式で機能するフォームをデザインします。

## AEM Forms Designer の HTML5 フォーム向けの機能 {#capabilities-in-aem-forms-designer-for-html-forms}

### プレビューHTML {#preview-html}

フォームデザイナーのデザインモードに「プレビューHTML」タブが追加され、デザインプロセス中にHTML5 形式でフォームをプレビューできます。 AEM Forms Designer でこの機能を有効にして設定する方法について詳しくは、 [プレビューHTML](/help/forms/using/preview-xdp-forms-html.md).

### 手書き署名 {#scribble-signature}

HTML5 フォームの主なターゲットはタッチデバイスです。 そのため、AEM Forms Designer に新しい手書き署名コントロールが追加されました。 手書き署名のコントロールは、クリックしてフォームテンプレートにドラッグ＆ドロップすると設定できます。HTML5 レンディションでは手書きフィールドとしてレンダリングされるため、タッチデバイスで署名を手書きするのに使用できます。デスクトップ機器では、手書きフィールドとしてマウスのコントロールで使用できます。この機能の使用方法について詳しくは、[XFA 手書きフィールド](/help/forms/using/scribble-signature.md)を参照してください。

![4](assets/4.png)
