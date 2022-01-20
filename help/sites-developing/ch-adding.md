---
title: ページへの ContextHub の追加とストアへのアクセス
seo-title: Adding ContextHub to Pages and Accessing Stores
description: ContextHub 機能を有効にし、ContextHub JavaScript ライブラリにリンクするには、ContextHub をページに追加します
seo-description: Add ContextHub to your pages to enable the ContextHub features and to link to the ContextHub Javascript libraries
uuid: ade37960-21c4-4d64-a525-68f0d199f955
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: personalization
content-type: reference
discoiquuid: ac8f44df-39fb-44ea-ae17-ead0dbd1f6c0
exl-id: 99efe308-bf8a-41ad-8203-b57fce20820c
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '1008'
ht-degree: 96%

---

# ページへの ContextHub の追加とストアへのアクセス {#adding-contexthub-to-pages-and-accessing-stores}

ContextHub 機能を有効にし、ContextHub JavaScript ライブラリにリンクするには、ContextHub をページに追加します

ContextHub JavaScript API を使用すると、ContextHub が管理するコンテキストデータにアクセスできます。このページでは、コンテキストデータにアクセスおよび操作するための API の主な機能について簡単に説明します。詳細情報とコードのサンプルは、API リファレンスドキュメントへのリンクから確認できます。

## ページコンポーネントへの ContextHub の追加 {#adding-contexthub-to-a-page-component}

ContextHub 機能を有効にし、ContextHub JavaScript ライブラリにリンクするには、ページの `head` セクションに ContextHub コンポーネントを含めます。ページコンポーネントの JSP コードは、次の例のようになります。

```xml
<head>
   <sling:include path="contexthub" resourceType="granite/contexthub/components/contexthub" />
</head>
```

ContextHub ツールバーをプレビューモードで表示するかどうかも設定する必要があります。[ContextHub UI の表示／非表示](/help/sites-administering/contexthub-config.md#showing-and-hiding-the-contexthub-ui)を参照してください。

## ContextHub ストアについて {#about-contexthub-stores}

コンテキストデータを保持するには、ContextHub ストアを使用します。ContextHub には、すべてのストアタイプの基礎となる次のタイプのストアが用意されています。

* [PersistedStore](/help/sites-developing/contexthub-api.md#contexthub-store-persistedstore)
* [SessionStore](/help/sites-developing/contexthub-api.md#contexthub-store-sessionstore)
* [JSONPStore](/help/sites-developing/contexthub-api.md#contexthub-store-persistedjsonpstore)
* [PersistedJSONPStore](/help/sites-developing/contexthub-api.md#contexthub-store-persistedstore)

すべてのストアタイプは、[`ContextHub.Store.Core`](/help/sites-developing/contexthub-api.md#contexthub-store-core) クラスの拡張です。新しいストアタイプの作成については、[カスタムストアの作成](/help/sites-developing/ch-extend.md#creating-custom-store-candidates)を参照してください。ストアタイプのサンプルについては、[ContextHub ストア候補のサンプル](/help/sites-developing/ch-samplestores.md)を参照してください。

### 永続モード {#persistence-modes}

ContextHub ストアは、次のいずれかの永続モードを使用します。

* **ローカル：** HTML5 localStorage を使用してデータを保持します。ローカルストレージは、セッションをまたがってブラウザー上に保持されます。
* **セッション：** HTML5 sessionStorage を使用してデータを保持します。セッションストレージは、ブラウザーセッションが持続する間、保持され、すべてのブラウザーウィンドウで使用可能です。
* **Cookie：**&#x200B;ブラウザーのデータストレージ用 cookie のネイティブサポートを使用します。cookie データは、HTTP 要求としてサーバーとの間で送受信されます。
* **Window.name：** window.name プロパティを使用してデータを保持します。
* **メモリ：** JavaScript オブジェクトを使用してデータを保持します。

デフォルトでは、ContextHub は「ローカル」永続モードを使用します。ブラウザーが HTML5 localStorage をサポートまたは許可していない場合は、「セッション」永続モードが使用されます。ブラウザーが HTML5 sessionStorage をサポートまたは許可していない場合は、「Window.name」永続モードが使用されます。

### ストアデータ {#store-data}

ストアデータは内部的にツリー構造を形成しており、値をプライマリタイプまたは複合オブジェクトとして追加できます。複合オブジェクトをストアに追加すると、オブジェクトのプロパティがデータツリーにブランチを形成します。例えば、次の複合オブジェクトを location という名前の空のストアに追加します。

```xml
Object {
   number: 321,
   data: {
      city: "Basel",
      country: "Switzerland",
      details: {
         population: 173330,
         elevation: 260
      }
   }
}
```

ストアデータのツリー構造は、次のように概念化できます。

```xml
/
|- number
|- data
      |- city
      |- country
      |- details
            |- population
            |- elevation
```

ツリー構造は、ストア内のデータ項目をキーと値のペアとして定義します。上記の例では、キー `/number` が値 `321` に対応し、キー `/data/country` が値 `Switzerland` に対応しています。

### オブジェクトの操作 {#manipulating-objects}

ContextHub には、JavaScript オブジェクトを操作するための [`ContextHub.Utils.JSON.tree`](/help/sites-developing/contexthub-api.md#contexthub-utils-json-tree) クラスが用意されています。JavaScript オブジェクトをストアに追加する前またはストアから取得した後に、このクラスの関数を使用して JavaScript オブジェクトを操作します。

さらに、[`ContextHub.Utils.JSON`](/help/sites-developing/contexthub-api.md#contexthub-utils-json) クラスには、オブジェクトを文字列にシリアライズしたり、文字列をオブジェクトにデシリアライズしたりするための関数があります。`JSON.parse` 関数および `JSON.stringify` 関数をネイティブに含まないブラウザーをサポートするには、このクラスを使用して JSON データを処理します。

## ContextHub ストアとのやり取り {#interacting-with-contexthub-stores}

ストアを JavaScript オブジェクトとして取得するには、[`ContextHub`](/help/sites-developing/contexthub-api.md#ui-event-constants) JavaScript オブジェクトを使用します。ストアオブジェクトを取得したら、そのストアに格納されているデータを操作できます。ストアを取得するには、[`getAllStores`](/help/sites-developing/contexthub-api.md#getallstores) 関数または [`getStore`](/help/sites-developing/contexthub-api.md#getstore-name) 関数を使用します。

### ストアデータへのアクセス {#accessing-store-data}

[`ContexHub.Store.Core`](/help/sites-developing/contexthub-api.md#contexthub-store-core) JavaScript クラスは、ストアデータとやり取りするための関数を定義します。次の関数は、オブジェクトに格納されている複数のデータ項目を保存および取得します。

* [addAllItems](/help/sites-developing/contexthub-api.md#addallitems-tree-options)
* [getTree](/help/sites-developing/contexthub-api.md#gettree-includeinternals)

個々のデータ項目は、一連のキーと値のペアとして保存されます。値を保存および取得するには、対応するキーを指定します。

* [getItem](/help/sites-developing/contexthub-api.md#getitem-key)
* [setItem](/help/sites-developing/contexthub-api.md#setitem-key-value-options)

カスタムストア候補は、ストアデータへのアクセスを提供する追加の関数を定義できます。

>[!NOTE]
>
>ContextHub は、デフォルトでは、パブリッシュサーバーを使用した現在のログインを認識しません。そうしたユーザーは ContextHub では「匿名」と見なされます。
>
>[We.Retail 参照サイト](/help/sites-developing/we-retail.md)に実装したプロファイルストアを読み込むことで、ContextHub でログインユーザーを識別できます。[GitHub で関連するコード](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/blob/master/ui.apps/src/main/content/jcr_root/apps/weretail/components/structure/header/clientlib/js/utilities.js)を参照してください。

### ContextHub のイベンティング {#contexthub-eventing}

ContextHub には、ストアイベントに自動的に対処できるようにするイベントフレームワークが含まれています。各ストアオブジェクトには、ストアの [`ContextHub.Utils.Eventing`](/help/sites-developing/contexthub-api.md#contexthub-utils-eventing) プロパティとして使用できる [`eventing`](/help/sites-developing/contexthub-api.md#eventing) オブジェクトが含まれています。JavaScript 関数をストアイベントにバインドするには、[`on`](/help/sites-developing/contexthub-api.md#on-name-handler-selector-triggerforpastevents) 関数または [`once`](/help/sites-developing/contexthub-api.md#once-name-handler-selector-triggerforpastevents) 関数を使用します。

## ContextHub を使用した cookie の操作 {#using-context-hub-to-manipulate-cookies}

ContextHub JavaScript API には、ブラウザー cookie を処理するためのクロスブラウザーサポートがあります。[`ContextHub.Utils.Cookie`](/help/sites-developing/contexthub-api.md#contexthub-utils-cookie) 名前空間は、Cookie を作成、操作、削除するための関数を定義します。

## 解決された ContextHub セグメントの特定 {#determining-resolved-contexthub-segments}

ContextHub のセグメントエンジンを使用して、現在のコンテキストで解決された登録済みセグメントを特定できます。解決されたセグメントを取得するには、[`ContextHub.SegmentEngine.SegmentManager`](/help/sites-developing/contexthub-api.md#contexthub-segmentengine-segmentmanager) クラスの getResolvedSegments 関数を使用します。その後で、`getName` クラスの `getPath` 関数または [`ContextHub.SegmentEngine.Segment`](/help/sites-developing/contexthub-api.md#contexthub-segmentengine-segment) 関数を使用して、セグメントをテストします。

### インストール済みのセグメント {#installed-segments}

ContextHub のセグメントは、`/conf/we-retail/settings/wcm/segments` ノードの下にインストールされます。

* female（女性）
* female-over-30（30 歳より上の女性）
* female-under-30（30 歳より下の女性）
* male（男性）
* male-over-30（30 歳より上の男性）
* male-under-30（30 歳より下の男性）
* order-value-75-to-100（注文額が 75 ～ 100）
* order-value-over-100（注文額が 100 より上）
* over-30（30 歳より上）
* summer（夏）
* summer-female（夏 - 女性）
* summer-female-over-30（夏 - 30 歳より上の女性）
* summer-female-under-30（夏 - 30 歳より下の女性）
* summer-male（夏 - 男性）
* summer-male-over-30（夏 - 30 歳より上の男性）
* summer-male-under-30（夏 - 30 歳より下の男性）
* under-30（30 歳より下）
* winter（冬）
* winter-female（冬 - 女性）
* winter-female-over-30（冬 - 30 歳より上の女性）
* winter-female-under-30（冬 - 30 歳より下の女性）
* winter-male（冬 - 男性）
* winter-male-over-30（冬 - 30 歳より上の男性）
* winter-male-under-20（冬 - 20 歳より下の男性）

これらのセグメントの解決に使用されるルールを要約すると次のようになります。

* 女性か男性かは、`gender`profile[ ストアの ](/help/sites-developing/ch-samplestores.md#granite-profile-sample-store-candidate) データ項目から判断されます。

* 年齢は、profile ストアの age データ項目から判断されます。
* シーズンは、 [位置情報](/help/sites-developing/ch-samplestores.md#contexthub-geolocation-sample-store-candidate) store 、および surferinfo ストアの月のデータ項目です。

>[!WARNING]
>
>インストールされたセグメントは、プロジェクト用の独自の専用設定を構築するのに役立つリファレンス設定として提供されています。直接使用しないでください。

## ContextHub のデバッグメッセージのログ {#logging-debug-messages-for-contexthub}

開発時に役立つ詳細なデバッグメッセージをログに記録するように、Adobe Granite ContextHub OSGi サービス（PID = `com.adobe.granite.contexthub.impl.ContextHubImpl`）を設定します。

サービスを設定するには、 [Web コンソール](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console) または [リポジトリ内の JCR ノード](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository):

* Web コンソール：デバッグメッセージをログに記録するには、Debug プロパティを選択します。
* JCR ノード：デバッグメッセージをログに記録するには、`com.adobe.granite.contexthub.debug` ブールプロパティを `true` に設定します。

## ContextHub フレームワークの概要の確認 {#see-an-overview-of-the-contexthub-framework}

ContextHub には、ContextHub フレームワークの概要を確認できる[診断ページ](/help/sites-developing/ch-diagnostics.md)があります。
