---
title: 開発とページの差分
seo-title: 開発とページの差分
description: 'null'
seo-description: 'null'
uuid: 48bbeca3-fe16-48ef-bb4d-ac605fe0ca76
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: introduction
content-type: reference
discoiquuid: 13e8cbef-698f-4e69-9f8c-f9bee82e9fd1
translation-type: tm+mt
source-git-commit: 835f1ba1f196c6c6303019f0cc310cad850e1682

---


# 開発とページの差分{#developing-and-page-diff}

## 機能概要 {#feature-overview}

コンテンツの作成は反復的なプロセスです。効率的にオーサリングをおこなうには、反復するごとに何が変更されたかがわかるようにする必要があります。あるページバージョンを見てから別のページバージョンを見るのは非効率的であり、エラーが発生しやすくなります。作成者は、現在のページと前のバージョンを並べて比較する際に、差分が強調表示されるようにしたいと考えています。

ページの差分機能を使用すると、ユーザーは現在のページをローンチや以前のバージョンなどと比較できます。このユーザー機能について詳しくは、[ページの差分](/help/sites-authoring/page-diff.md)を参照してください。

## 操作の詳細 {#operation-details}

ページのバージョンを比較する場合、相違を容易にするために、比較対象の以前のバージョンがバックグラウンドでAEMによって再作成されます。 これは、並べて比較するためにコンテンツをレ [ンダリングできる必要があります](/help/sites-authoring/page-diff.md#presentation-of-differences)。

この再作成操作は、AEMによって内部的に行われ、ユーザーに対して透過的で、介入は必要ありません。 ただし、CRX DE Liteなどでリポジトリを表示している管理者は、コンテンツ構造内で再作成されたバージョンを確認できます。

AEMのパッチレベルによって動作が異なり、正しく動作するために特定の権限が必要になる場合があります。

### AEM 6.4.3より前 {#prior-to-aem}

コンテンツを比較すると、比較するページまでのツリー全体が次の場所に再作成されます。

`/content/versionhistory/<userId>/<site structure>`

ページの相違メカニズムを使用する場合、AEMは以前のバージョンのページを再作成するので、この機能を使用するには、ユーザーに特定のJCR権限が必要です。

>[!CAUTION]
>
>ページの相違機能を使用するには、ユーザーがノードに対して** Modify/Create/Delete***権限を持っている必要があります `/content/versionhistory`。

### As of AEM 6.4.3 {#as-of-aem}

コンテンツを比較すると、比較するページまでのツリー全体が次の場所に再作成されます。

`/tmp/versionhistory/`

このコンテンツは、現在のユーザーに対する表示を制限する権限を持つサービスユーザーによって作成されます。 このため、特別な権限は必要ありません。

この一時コンテンツをクリーンアップするために、クリーンアップタスクが自動的に実行されます。

## 開発者の制限事項 {#developer-limitations}

Previously, in Classic UI, special development consideration had to be made to facilitate AEM diffing (such as using `cq:text` tag lib, or custom integrating the `DiffService` OSGi service into components). 新しい差分機能ではこのような考慮は必要なくなりました。差分は DOM 比較を介してクライアント側で実行されるからです。

ただし、開発者が考慮する必要がある制限事項はいくつかあります。

* この機能では、AEM 製品の名前空間にない CSS クラスが使用されます。同じ名前を持つ他のカスタムCSSクラスまたはサードパーティCSSクラスがページに含まれている場合、相違の表示が影響を受ける可能性があります。

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

