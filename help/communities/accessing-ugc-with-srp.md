---
title: SRP による UGC へのアクセス
seo-title: SRP による UGC へのアクセス
description: ASRP または MSRP を使用するようにサイトが設定されている場合、実際の UGC は AEM のノードストア（JCR）に格納されません。
seo-description: ASRP または MSRP を使用するようにサイトが設定されている場合、実際の UGC は AEM のノードストア（JCR）に格納されません。
uuid: 5f9f8c9b-4c6a-45b0-96ff-14934380eba7
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.4/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: ee786a5c-b985-4d78-9063-6c79ae5e13e6
translation-type: tm+mt
source-git-commit: 565604feff7fa365a1c6b52b62a0b0eb681bb192
workflow-type: tm+mt
source-wordcount: '369'
ht-degree: 62%

---


# SRP による UGC へのアクセス {#accessing-ugc-with-srp}

## SRP について {#about-srp}

All AEM Communities components and features are built on the [social component framework (SCF)](scf.md), which invokes the SocialResourceProvider API to access all user generated content (UGC).

Before a community site is created, the [storage resource provider (SRP)](working-with-srp.md) must be configured to select an implementation consistent with the underlying [topology](topologies.md). SRPの実装は、次の3つのストレージオプションに基づいています。

1. [ASRP](asrp.md) - Adobe オンデマンドストレージ
2. [MSRP](msrp.md) - MongoDB
3. [JSRP](jsrp.md) - JCR

## UGC のストレージについて {#about-ugc-storage}

What is important to know about storage of UGC is, when a site is configured to use ASRP or MSRP, the actual UGC is not be stored in AEM&#39;s [node store](../../help/sites-deploying/data-store-config.md) (JCR).

UGC をコピーして有用なメタデータを提供するノードが JCR 内に存在する場合がありますが、実際の UGC とこれらのノードを混同しないでください。

[ストレージリソースプロバイダーの概要](srp.md)を参照してください。

## ベストプラクティス {#best-practice}

カスタムコンポーネントを開発する際、開発者は、現在どのトポロジを選択しているかに関係なく、将来新しいトポロジに移行する柔軟性を保ちながら、慎重にコーディングする必要があります。

### JCR を使用できないことを想定する {#assume-jcr-not-available}

JCR に固有のメソッドの使用は避ける必要があります。

使用するメソッドは次のとおりです。

* Sling API（Sling リソース）
   * JCRノードがあると想定しない

* OSGi イベント
   * JCRイベントがあると想定しない

* [ソーシャルリソースユーティリティ](socialutils.md#socialresourceutilities-package)
* [SCFユーティリティ](socialutils.md#scfutilities-package)

使用を避けるメソッドは次のとおりです。

* Node API
* JCR イベント
* ワークフローランチャー(JCRイベントを使用)

### 検索コレクションを使用する {#use-search-collections}

SRP ごとにネイティブなクエリー言語が異なる場合があります。[com.adobe.cq.social.ugc.api](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/ugc/api/package-summary.html) パッケージのメソッドを使用して、適切なクエリー言語を呼び出すことをお勧めします。

詳しくは、[検索の基本事項](search-implementation.md)を参照してください。

## リソース {#resources}

* [コミュニティコンテンツストレージ](working-with-srp.md) - UGC 共通ストアに使用できる SRP の選択肢
* [ストレージリソースプロバイダーの概要](srp.md) - 序論とリポジトリの使用方法の概要
* [SRPとUGC Essentials](srp-and-ugc.md) - SRPユーティリティのメソッドと例
* [検索の基本事項](search-implementation.md) - UGC の検索に関する基本情報
* [SocialUtils のリファクタリング](socialutils.md) - 廃止されたユーティリティメソッドと現在の SRP ユーティリティメソッドの対応関係
