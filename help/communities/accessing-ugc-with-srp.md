---
title: SRP による UGC へのアクセス
seo-title: Accessing UGC with SRP
description: サイトが ASRP または MSRP を使用するように設定されている場合、実際の UGC はAEMノードストア (JCR) に格納されません
seo-description: When a site is configured to use ASRP or MSRP, the actual UGC is not be stored in AEM's node store (JCR)
uuid: 5f9f8c9b-4c6a-45b0-96ff-14934380eba7
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.4/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: ee786a5c-b985-4d78-9063-6c79ae5e13e6
exl-id: 3a16a771-e1c5-4ae4-9fc6-17a47064db54
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '343'
ht-degree: 3%

---

# SRP による UGC へのアクセス {#accessing-ugc-with-srp}

## SRP について {#about-srp}

すべてのAEM Communitiesのコンポーネントと機能は、 [ソーシャルコンポーネントフレームワーク (SCF)](scf.md):SocialResourceProvider API を呼び出して、すべてのユーザー生成コンテンツ (UGC) にアクセスします。

コミュニティサイトを作成する前に、 [ストレージリソースプロバイダー (SRP)](working-with-srp.md) は、基になる [トポロジ](topologies.md). SRP の実装は、次の 3 つのストレージオプションに基づいています。

1. [ASRP](asrp.md) -Adobeオンデマンドストレージ
2. [MSRP](msrp.md) - MongoDB
3. [JSRP](jsrp.md) - JCR

## UGC ストレージについて {#about-ugc-storage}

UGC のストレージに関して知っておくべき重要な点は、ASRP または MSRP を使用するようにサイトを設定する場合、実際の UGC はAEMに格納されないことです [ノードストア](../../help/sites-deploying/data-store-config.md) (JCR)。

JCR には、UGC に影を付けて有用なメタデータを提供するノードが存在する場合がありますが、これらのノードを実際の UGC と混同しないでください。

詳しくは、 [ストレージリソースプロバイダの概要。](srp.md)

## ベストプラクティス {#best-practice}

カスタムコンポーネントを開発する場合、開発者は現在選択しているトポロジとは別にコーディングをおこなうように注意する必要があり、将来新しいトポロジに移行する柔軟性を維持する必要があります。

### JCR が使用できないと仮定 {#assume-jcr-not-available}

JCR に固有のメソッドは避ける必要があります。

使用するメソッド：

* Sling API（Sling リソース）
   * JCR ノードが存在するとは想定しないでください

* OSGi イベント
   * JCR イベントがあるとは想定しないでください

* [Social Resource Utilities](socialutils.md#socialresourceutilities-package)
* [SCF ユーティリティ](socialutils.md#scfutilities-package)

回避方法：

* ノード API
* JCR イベント
* ワークフローランチャー（JCR イベントを使用）

### コレクションを検索 {#use-search-collections}

異なる SRP は異なるネイティブクエリ言語を持つことができます。 メソッドは、 [com.adobe.cq.social.ugc.api](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/ugc/api/package-summary.html) 適切なクエリ言語を呼び出すためのパッケージ。

詳しくは、 [検索の基本事項](search-implementation.md).

## リソース {#resources}

* [コミュニティコンテンツストレージ](working-with-srp.md) - UGC 共通ストアで使用可能な SRP の選択肢について説明します。
* [ストレージリソースプロバイダの概要](srp.md)  — 概要とリポジトリ使用の概要
* [SRP と UGC の基本事項](srp-and-ugc.md) - SRP ユーティリティメソッドと例
* [検索の基本事項](search-implementation.md) - UGC 検索に関する基本情報
* [SocialUtils リファクタリング](socialutils.md)  — 非推奨のユーティリティメソッドを現在の SRP ユーティリティメソッドにマッピングします
