---
title: SRP による UGC へのアクセス
seo-title: Accessing UGC with SRP
description: ASRP または MSRP を使用するようにサイトが設定されている場合、実際の UGC は AEM のノードストア（JCR）に格納されません。
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
ht-degree: 59%

---

# SRP による UGC へのアクセス {#accessing-ugc-with-srp}

## SRP について {#about-srp}

すべてのAEM Communitiesのコンポーネントと機能は、 [ソーシャルコンポーネントフレームワーク (SCF)](scf.md):SocialResourceProvider API を呼び出して、すべてのユーザー生成コンテンツ (UGC) にアクセスします。

コミュニティサイトを作成する前に、 [ストレージリソースプロバイダー (SRP)](working-with-srp.md) は、基になる [トポロジ](topologies.md). SRP の実装は、次の 3 つのストレージオプションに基づいています。

1. [ASRP](asrp.md) - Adobe オンデマンドストレージ
2. [MSRP](msrp.md) - MongoDB
3. [JSRP](jsrp.md) - JCR

## UGC のストレージについて {#about-ugc-storage}

UGC のストレージに関して知っておくべき重要な点は、ASRP または MSRP を使用するようにサイトを設定する場合、実際の UGC はAEMに格納されないことです [ノードストア](../../help/sites-deploying/data-store-config.md) (JCR)。

UGC をコピーして有用なメタデータを提供するノードが JCR 内に存在する場合がありますが、実際の UGC とこれらのノードを混同しないでください。

[ストレージリソースプロバイダーの概要](srp.md)を参照してください。

## ベストプラクティス {#best-practice}

カスタムコンポーネントを開発する際、開発者は、現在どのトポロジを選択しているかに関係なく、将来新しいトポロジに移行する柔軟性を保ちながら、慎重にコーディングする必要があります。

### JCR を使用できないことを想定する {#assume-jcr-not-available}

JCR に固有のメソッドの使用は避ける必要があります。

使用するメソッドは次のとおりです。

* Sling API（Sling リソース）
   * JCR ノードが存在するとは想定しないでください

* OSGi イベント
   * JCR イベントがあるとは想定しないでください

* [Social Resource Utilities](socialutils.md#socialresourceutilities-package)
* [SCF ユーティリティ](socialutils.md#scfutilities-package)

使用を避けるメソッドは次のとおりです。

* Node API
* JCR イベント
* ワークフローランチャー（JCR イベントを使用）

### 検索コレクションを使用する {#use-search-collections}

SRP ごとにネイティブなクエリー言語が異なる場合があります。[com.adobe.cq.social.ugc.api](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/ugc/api/package-summary.html) パッケージのメソッドを使用して、適切なクエリー言語を呼び出すことをお勧めします。

詳しくは、[検索の基本事項](search-implementation.md)を参照してください。

## リソース {#resources}

* [コミュニティコンテンツストレージ](working-with-srp.md) - UGC 共通ストアに使用できる SRP の選択肢
* [ストレージリソースプロバイダーの概要](srp.md) - 序論とリポジトリの使用方法の概要
* [SRP と UGC の基本事項](srp-and-ugc.md) - SRP ユーティリティメソッドと例
* [検索の基本事項](search-implementation.md) - UGC の検索に関する基本情報
* [SocialUtils のリファクタリング](socialutils.md) - 廃止されたユーティリティメソッドと現在の SRP ユーティリティメソッドの対応関係
