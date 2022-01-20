---
title: コメントコンポーネントの拡張
seo-title: Extend Comments Component
description: コメントコンポーネントを拡張して、特定の用途についてコンポーネントの外観や動作を変更する
seo-description: Extend the Comments component to alter its appearance or behavior for specific uses
uuid: 6f439097-b1d0-4e7d-afcf-01d8f43aa866
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.4/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: a07a4690-0e47-4a76-84cb-96abdc70b835
exl-id: f6722953-ff71-4fba-b76e-1d566f71f6d5
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '255'
ht-degree: 30%

---

# コメントコンポーネントの拡張 {#extend-comments-component}

次の目的 [拡張](client-customize.md#extensions) デフォルトのコンポーネントは、特定の用途でのコンポーネントの外観や動作を変更することです。

コンポーネントへのパスは一意で、デフォルトのコンポーネントをスーパーリソースタイプとして参照します。 There is less risk as the scope is limited compared to the global scope of a component overlay.

>[!NOTE]
>
>[オーバーレイ](client-customize.md#overlays)されるコンポーネントの拡張はサポートされていません。

## 例 {#example}

Suppose the header for the comment component must display with an alternate appearance on one site of the AEM instance, while appearing with the default display on another site. Instead of overlaying the default comment, which changes the comment component for all instances, a better solution is to ensure there are multiple comment components available for use on various sites.

この解決策を実装するには、既存のコンポーネントを拡張（上書き）する新しいコンポーネントを作成し、Handlebars スクリプトを変更します。The area of the site that uses the new comments can use the extended one, while the sites that use the default appearance remain unaffected.

コメントコンポーネントは実際には、コメントシステムを構成する 2 つのコンポーネントのうちの 1 つです。Thus, there are two components to extend: *comments* and *comment*. 編集するスクリプトは、「コメント」コンポーネントの `header.hbs` ファイルを、親 *コメント* コンポーネント（コメントシステム）は、作成者が実際にページに追加するものです。

コメントを拡張するには、次の手順を実行する必要があります。

1. [コンポーネントの作成](extend-create-components.md)
1. [サンプルページへのコメントの追加](extend-sample-page.md)
1. [外観の変更](extend-alter-appearance.md)
