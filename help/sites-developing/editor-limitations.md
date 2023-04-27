---
title: エディターの制限事項
seo-title: Editor Limitations
description: タッチ操作対応 UI のエディターは、オーバーレイを使用して iframe に含まれるコンテンツを操作します。 この操作には、エディターの使用と開発者に対していくつかの制限事項があります。
seo-description: The editor in the touch-enabled UI makes use of overlays to interact with content confined in an iframe. This interaction creates some limitations in both usage of the editor and also for developers.
uuid: ff524530-3f3a-4c5b-9f94-4aa9aeb9d461
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.4/SITES
content-type: reference
topic-tags: introduction
discoiquuid: d748decb-a614-4c9e-a502-d6176b720f1a
exl-id: ce860880-5954-4f72-8ec6-60209c1ec659
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '316'
ht-degree: 53%

---

# エディターの制限事項{#editor-limitations}

タッチ操作対応 UI のエディターは、オーバーレイを使用して iframe に含まれるコンテンツを操作します。 この操作には、エディターの使用と開発者に対していくつかの制限事項があります。このページでは、これらの制限事項の概要を説明し、可能な場合は解決策や回避策を提供します。

## 機能の制限 {#functional-limitations}

作成者は、エディターを使用してページを作成する際に、次の機能上の制限を受ける場合があります。

### リンクがアクティブではありません {#links-not-active}

[ページの編集](/help/sites-authoring/editing-content.md)時に、リンクがアクティブになりません。

* [コンテンツ内のリンクを使用して移動するには、**プレビュー**&#x200B;モード](/help/sites-authoring/editing-content.md#preview-mode)に切り替えます。

### 構造ページ {#structure-pages}

ページに `structure` と名前が付けられない 。`structure` と名前が付けられたページは、ページエディターで編集できません。

## CSS の制限 {#css-limitations}

開発者は、エディターでの CSS の操作に次の制限が生じる場合があります。

### 絶対位置の要素 {#absolutely-positioned-elements}

絶対に配置された要素は、オーバーレイの位置で問題を引き起こす可能性があります。

* この場合、エディターはまったく同じ寸法のオーバーレイを作成するので、絶対位置にある要素の寸法が正しいことを確認してください。

### vh 単位 {#vh-units}

iframe の高さは AEM によって自動調整されるので、`vh` 単位はサポートされません。

### 固定の背景画像 {#fixed-background-images}

固定の背景画像は、iframe 内に埋め込まれるので、スクロール時に固定されて表示されない場合があります。

* ヘッダーバーのアクションで「**公開済みとしてページを表示**」を選択すると、ページが正しく表示されます。

### 100 ％の高さ {#height}

ページの body 要素では、100 ％の高さはサポートされていません。

* フルスクリーンの body を実装するためには、次のように body 要素を「拡張」することで、回避策が可能になります。

```xml
body {
    position: absolute;
    top: 0;
    bottom: 0;
    right: 0;
    left: 0;
}
```

### 余白の折りたたみ {#margin-collapsing}

余白の折りたたみの問題は、body 要素の最初の子要素に余白がある場合に発生することがあります。

* 解決策として、次のように body 要素レベルに clearfix を追加します。

```xml
body:before, body:after{
    content: ' ';
    display: table;
}
```
