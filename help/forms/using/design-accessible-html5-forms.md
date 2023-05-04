---
title: アクセス可能な HTML5 フォームの設計
seo-title: Designing accessible HTML5 forms
description: HTML5 フォームでは、 ARIAHTML5 アクセシビリティ標準を使用します。 これらのフォームはタブナビゲーションをサポートし、一般的なスクリーンリーダーとの互換性が認定されています。
seo-description: HTML5 forms use the ARIA HTML5 accessibility standard. These forms support tabbed navigation and are certified to be compatible with common screen readers.
uuid: b7757079-5f06-4818-8488-11d67cbe3522
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: hTML5_forms
discoiquuid: ccc59dd5-c0cf-415a-b71a-5bc0cf452ede
feature: Mobile Forms
exl-id: 64d8cf2c-8180-49ce-a725-48cd03476fb8
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '383'
ht-degree: 18%

---

# アクセス可能な HTML5 フォームの設計 {#designing-accessible-html-forms}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

HTML5 フォームは、ARIAHTML5 アクセシビリティ標準を使用して、アクセシブルなHTMLフォームを生成します。 これらのフォームは、タブナビゲーション（Mozilla FireFox を除く）をサポートし、一般的なスクリーンリーダーとの互換性が認定されています。 優れたアクセシビリティ機能を備えたHTML5 フォームを生成するには、いくつかの機能に基づいて XFA フォームテンプレートをデザインします [基本設計ガイドライン](/help/forms/using/best-practices-for-html5-forms.md). デザインガイドラインには正しいタブ順序の設定、および各フォームコントロールのために読み上げテキストコンテンツの提供などが含まれます。AEM Forms Designer ではこれらのフォームコントロール属性を設定し、アクセシビリティを備えた PDF フォームおよび HTML5 フォームを生成できます。

*注意：タブナビゲーションは、値の合計を表示する計算フィールドなど、保護されたフィールドをカバーしません。 スクリーンリーダーが保護されたフィールドの値を読み取るには、保護されたフィールドの上または横に空の読み取り専用フィールドを配置します。 保護されたフィールドの値を新しい読み取り専用フィールドに割り当てます。 スクリーンリーダーまたはタブナビゲーションは、この読み取り専用フィールドを選択し、保護フィールドの値として読み上げることができます。*

AEM Forms Designer には、スクリーンリーダーに渡すことができる多数のスピーチテキストオプションが含まれています。 フォーム内の各オブジェクトに対して、ユーザーはスクリーンリーダーテキストに対して、次のいずれかの設定を指定できます。

* カスタムのスクリーンリーダーテキスト。アクセシビリティパレットを使用して設定できます。 作成者は、ボタン名やフィールド名、目的に注釈を付けることができます。
* ツールチップ（アクセシビリティパレットで設定可能）
* フォーム上のフィールドのキャプション。
* 「連結」タブの「名前」オプションで指定された、オブジェクトの名前。

![アクセシビリティ](assets/accessibility.png)

フォームコントロールで、ツールチップ、画面Readerテキスト、キャプションなど複数のオプションを使用できる場合、画面Readerではこれらのプロパティの 1 つのみが使用されます。 デフォルトの順序は、カスタムスクリーンReaderテキスト、ツールヒント、キャプション、名前です。 デフォルト順序はアクセシビリティパレットにある「**スクリーンリーダーの優先順位**」オプションを使用してオーバーライドできます。
