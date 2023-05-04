---
title: アセットの命名規則のテスト
seo-title: Naming conventions for assets
description: リポジトリーのノードは、Java コンテンツリポジトリーの命名規則の対象です。ただし、アセットノード名には Adobe Experience Manager によって追加の規則が課せられます。
seo-description: Nodes in the repository are subject to naming conventions of the Java Content Repository. However, Adobe Experience Manager imposes further conventions for the name of asset nodes.
uuid: 6b622a60-90e8-461e-9b67-42c11c7038f9
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.4/ASSETS
topic-tags: authoring
content-type: reference
discoiquuid: 55e66c66-0120-4ed4-94c5-d65a434bb59b
exl-id: 3dc38c37-f2a0-44f5-90f6-fee8c6f84ff4
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 46%

---

# アセットの命名規則のテスト{#naming-conventions-for-assets-testing}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

リポジトリーのノードは、[Java コンテンツリポジトリー](/help/sites-developing/the-basics.md#java-content-repository)の命名規則の対象です。ただし、アセットノード名には Adobe Experience Manager によって追加の規則が課せられます。

## クラシック UI {#classic-ui}

クラシック UI にはより厳しい制限が課されています。

* 次のいずれかの場合に、明示的なノード名でアセット名を検証します。

   * ノード名に変換するために、アセットのタイトルが指定されます。
   * 明示的なノード名が提供されています

* 有効な文字（クラシック UI でアセットを作成した場合、実際には次の文字のみが有効です）:

   * &#39;a&#39; ～ &#39;z&#39;
   * &#39;A&#39; ～ &#39;Z&#39;
   * &#39;0&#39; ～ &#39;9&#39;
   * _（アンダースコア）
   * `-`（ダッシュ／マイナス）
