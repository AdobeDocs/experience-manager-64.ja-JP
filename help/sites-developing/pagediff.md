---
title: 開発とページの差分
seo-title: Developing and Page Diff
description: 開発とページの差分
seo-description: null
uuid: 48bbeca3-fe16-48ef-bb4d-ac605fe0ca76
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: introduction
content-type: reference
discoiquuid: 13e8cbef-698f-4e69-9f8c-f9bee82e9fd1
exl-id: 365e944d-d8a3-4f4e-8925-88629845232f
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '479'
ht-degree: 79%

---

# 開発とページの差分{#developing-and-page-diff}

## 機能概要 {#feature-overview}

コンテンツの作成は反復的なプロセスです。効率的にオーサリングをおこなうには、反復するごとに何が変更されたかがわかるようにする必要があります。あるページバージョンを見てから別のページバージョンを見るのは非効率的であり、エラーが発生しやすくなります。作成者は、現在のページと前のバージョンを並べて比較する際に、差分が強調表示されるようにしたいと考えています。

ページの差分機能を使用すると、ユーザーは現在のページをローンチや以前のバージョンなどと比較できます。このユーザー機能について詳しくは、[ページの差分](/help/sites-authoring/page-diff.md)を参照してください。

## 操作の詳細 {#operation-details}

ページのバージョンを比較する場合、差分を検出しやすくするために、比較対象となる以前のバージョンが AEM によってバックグラウンドで再作成されます。これは、[並べて比較](/help/sites-authoring/page-diff.md#presentation-of-differences)できるようにコンテンツをレンダリングするために必要です。

この再作成操作は AEM の内部でおこなわれるもので、ユーザーに対しては透過的であり、ユーザーの介入は必要ありません。ただし、管理者が CRX DE Lite などでリポジトリーを閲覧している場合は、再作成されたこれらのバージョンがコンテンツ構造内に表示されます。

AEMパッチレベルに応じて、動作は異なり、正しく機能するために特定の権限が必要になる場合があります。

### AEM 6.4.3 以前 {#prior-to-aem}

コンテンツを比較すると、比較対象のページまでのツリー全体が次の場所に再作成されます。

`/content/versionhistory/<userId>/<site structure>`

ページの差分メカニズムを使用する場合、AEMでは以前のバージョンのページが再作成されるので、この機能を使用するには、特定の JCR 権限が必要です。

>[!CAUTION]
>
>ページの差分機能を使用するには、 **変更/作成/削除** ノードに対する権限 `/content/versionhistory`.

### AEM 6.4.3 以降 {#as-of-aem}

コンテンツを比較すると、比較対象のページまでのツリー全体が次の場所に再作成されます。

`/tmp/versionhistory/`

このコンテンツは、現在のユーザーの表示を制限する権限を持つサービスユーザーが作成します。 このため、特別な権限は必要ありません。

クリーンアップタスクが自動的に実行されて、この一時コンテンツがクリーンアップされます。

## 開発者の制限事項 {#developer-limitations}

以前の Classic UI では、AEM の差分取得を容易にするために開発に関して特別な考慮が必要でした（例えば、`cq:text` タグライブラリの使用、`DiffService` OSGi サービスのコンポーネントへのカスタム統合など）。新しい差分機能ではこのような考慮は必要なくなりました。差分は DOM 比較を介してクライアント側で実行されるからです。

ただし、開発者が考慮する必要がある制限事項はいくつかあります。

* この機能では、AEM 製品の名前空間にない CSS クラスが使用されます。同じ名前の付いた他のカスタム CSS クラスまたはサードパーティの CSS クラスがページに含まれている場合、差分の表示に影響が及ぶ可能性があります。

   * `html-added`
   * `html-removed`
   * `cq-component-added`
   * `cq-component-removed`
   * `cq-component-moved`
   * `cq-component-changed`

* 差分はクライアント側でページの読み込み時に実行されるので、クライアント側の差分サービスが実行された後に DOM を調整しても、その効果はありません。これは、次の項目に影響を与える可能性があります。

   * AJAX を使用してコンテンツを取り込むコンポーネント
   * 単一ページアプリケーション
   * ユーザーインタラクションに対して DOM を操作する JavaScript ベースのコンポーネント
