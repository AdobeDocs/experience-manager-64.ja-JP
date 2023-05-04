---
title: 命名規則
seo-title: Naming Conventions
description: リポジトリのノードは、Java コンテンツリポジトリーの命名規則の対象です
seo-description: Nodes in the repository are subject to naming conventions of the Java Content Repository
uuid: 0515c5c5-3e93-4710-983f-c08c146467fc
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: platform
content-type: reference
discoiquuid: 198098c0-432b-4a93-a94e-2552337435dd
exl-id: 741043c7-2ebb-455d-8163-a246b874a7b3
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '337'
ht-degree: 51%

---

# 命名規則{#naming-conventions}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

リポジトリのノードは、[Java コンテンツリポジトリ](/help/sites-developing/the-basics.md#java-content-repository)の命名規則の対象です。ただし、AEM によってページノード名に追加の規則が課せられます。

## ページの命名規則 {#naming-conventions-for-pages}

これらの命名規則は、以下のような様々なレベルで実装されます。

* JcrUtil:のAEM実装 [JCR ユーティリティ](#jcr-utilities).
* ページマネージャー：[ページマネージャー](#page-manager)は、ページレベルの操作用のメソッドを提供します。
* 使用されている UI に応じて、次の手順を実行します。

   * [標準のタッチ操作対応 UI](#standard-ui)
   * [クラシック UI](#classic-ui)

### JCR ユーティリティ {#jcr-utilities}

[JcrUtil](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/commons/jcr/JcrUtil.html) は、JCR ユーティリティのAEM実装です。 名前の検証に特に関心があるのは、文字マッピングを制御し、次の検証を行う点です。

* `isValidName`

   * 名前が空でなく、有効な文字のみを含んでいるかどうかをチェックします。
   * 提案された名前が有効かどうかを確認するために使用できます。

* `createValidName`

   * 任意の文字列から有効なラベルを作成します。
   * タイトルから名前を作成するのに使用できます。

### ページマネージャー {#page-manager}

[ページマネージャー](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/PageManager.html)は、[JCRUtil](#jcr-utilities) に基づいて、ページレベル操作用のメソッドを提供します。

### 標準 UI {#standard-ui}

標準のタッチ操作対応 UI は次のとおりです。

* 次のいずれかの場合に、PageManager が課した制限に従って名前を検証します。

   * ノード名に変換するために、ページタイトルが指定されます。
   * 明示的なノード名が提供されています

### クラシック UI {#classic-ui}

クラシック UI にはより厳しい制限が課されています。

* 次のいずれかの場合に、明示的なノード名を検証します。

   * ノード名に変換するために、ページタイトルが指定されます。
   * 明示的なノード名が提供されています

* 有効な文字（`PageManagerImpl` によって他の文字の使用が許可されていても、クラシック UI でページを作成する場合は、次の文字のみが有効です）。

   * &#39;a&#39; ～ &#39;z&#39;
   * &#39;A&#39; ～ &#39;Z&#39;
   * &#39;0&#39; ～ &#39;9&#39;
   * _（アンダースコア）
   * `-`（ダッシュ／マイナス）
