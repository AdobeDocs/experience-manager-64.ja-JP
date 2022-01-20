---
title: アセットの命名規則のテスト
seo-title: Naming conventions for assets
description: リポジトリのノードは、Java コンテンツリポジトリーの命名規則の対象です。ただし、Adobe Experience Manager によってアセットノード名に追加の規則が課せられます。
seo-description: Nodes in the repository are subject to naming conventions of the Java Content Repository. However, Adobe Experience Manager imposes further conventions for the name of asset nodes.
uuid: 6b622a60-90e8-461e-9b67-42c11c7038f9
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.4/ASSETS
topic-tags: authoring
content-type: reference
discoiquuid: 55e66c66-0120-4ed4-94c5-d65a434bb59b
exl-id: 3dc38c37-f2a0-44f5-90f6-fee8c6f84ff4
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '128'
ht-degree: 97%

---

# アセットの命名規則 テスト{#naming-conventions-for-assets-testing}

リポジトリのノードは、[Java コンテンツリポジトリ](/help/sites-developing/the-basics.md#java-content-repository)の命名規則の対象です。ただし、Adobe Experience Manager によってアセットノード名に追加の規則が課せられます。

## クラシック UI {#classic-ui}

クラシック UI にはさらに厳しい制約があります。

* アセット名が有効とされるのは、明示的なノード名が次のいずれかの場合です。

   * ノード名に変換されるようにアセットタイトルが提供されている。
   * 明示的なノード名が提供されている。

* 有効な文字（アセットがクラシック UI で作成されるとき次の文字のみが有効です）：

   * a～z
   * A～Z
   * 0～9
   * _（アンダースコア）
   * `-` （ダッシュ/マイナス）
