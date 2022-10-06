---
title: HTML5 フォーム向けのスクリーンリーダー
seo-title: Screen readers for HTML5 forms
description: HTML5 フォームでサポートされるスクリーンリーダーを一覧表示します。
seo-description: Lists the screen readers supported with HTML5 forms.
uuid: 035354e2-957f-4eb6-bc16-4ca96ec7ac74
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: hTML5_forms
discoiquuid: 53c57180-7004-4534-9146-603f7770a6fe
feature: Mobile Forms
exl-id: c27eb771-d390-4534-8e67-f1277550e760
source-git-commit: 51358642a2fa8f59f3f5e3996b0c37269632c4cb
workflow-type: tm+mt
source-wordcount: '337'
ht-degree: 94%

---

# HTML5 フォーム向けのスクリーンリーダー {#screen-readers-for-html-forms}

HTML5 フォームコンポーネントは XFA フォームテンプレートを HTML5 形式にレンダリングします。すべての標準の HTML5 をサポートするブラウザーはこれらのフォームをレンダリングできます。PDF と HTML5 フォーム同士で似たようなデータ取得の経験をサポートするために、PDF フォームのレイアウトは HTML5 フォームで保持されます。

HTML5 フォームは標準の HTML 構成を使用して、これらのフォームとともに通常の HTML のアクセシビリティツールを使用できるようにします。フォームがアクセシビリティを備えたフォームに関するベストプラクティスに従ってデザインされた場合、サポートされているスクリーンリーダーのどれとでも機能します。さらに、そのようなフォームはキーボードナビゲーションに対応しています。

## アクセシビリティの標準 {#accessibility-standards}

HTML5 フォームは既知の例外を含むアクセシビリティのリハビリテーション法第 508 条に準拠します。詳しくは、[HTML5 フォームの VPAT](https://www.adobe.com/content/dam/cc1/en/accessibility/compliance/pdfs/adobe-livecycle-es4-section-508-vpat-portfolio.pdf) を参照してください。

## HTML5 フォーム向けに認定されたスクリーンリーダー {#certified-screen-readers-for-html-forms}

* Microsoft Windows の JAWS 14.0
* Mac OS X と iPad の VoiceOver

### JAWS {#jaws}

すべてのデフォルトのキーストロークとショートカットは HTML5 フォームで機能します。JAWS の使用について詳しくは、[https://www.freedomscientific.com/jaws-hq.asp](https://www.freedomscientific.com/products/software/jaws/) にアクセスしてください。

### VoiceOver {#voiceover}

HTML5 フォームは VoiceOver のすべてのデフォルトのキーストロークとジェスチャーをサポートします。VoiceOver の設定と使用について詳しくは、[https://www.apple.com/accessibility/voiceover/](https://www.apple.com/accessibility/voiceover/) を参照してください。

## 既知の問題 {#known-issues}

* **（Internal Explorer 9 のみ）** HTML5 フォームでは、ページはオンデマンドで（動的に）読み込まれます。オンデマンドのページ読み込みは、スクリーンリーダーの機能で問題が生じます。スクリーンリーダーのフォーカスがページの最後のフィールドにあり、ユーザーが、次のページの最初のフィールドにフォーカスを設定する代わりに Tab キーを押したときは、スクリーンリーダーはフォームの最初のページの最初のフィールドにフォーカスを戻します。
* **（Internal Explorer 9 のみ）** HTML5 フォームの日付選択のコントロールはキーボードで完全にアクセスできません。日付選択のコントロールで、上向き／下向き矢印キーを複数回押した場合、日付選択のコントロールが閉じて、フォーカスが次／最後のフィールドに移動します。 

* VoiceOver は、iPad safari では日付ウィジェットで矢印キーを検出できません。
