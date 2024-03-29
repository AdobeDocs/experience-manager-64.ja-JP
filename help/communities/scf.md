---
title: ソーシャルコンポーネントフレームワーク
seo-title: Social Component Framework
description: ソーシャルコンポーネントフレームワーク (SCF) を使用すると、コミュニティコンポーネントの設定、カスタマイズ、拡張を簡単におこなうことができます
seo-description: The social component framework (SCF) simplifies the process of configuring, customizing, and extending Communities components
uuid: 23b4418d-b91c-46fc-bf42-1154ef79fe5a
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.4/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: d7b5b5e3-2d84-4a6b-bcc2-d490882ff3ed
exl-id: 9264c888-a583-40eb-9178-273146f8a12b
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '1524'
ht-degree: 2%

---

# ソーシャルコンポーネントフレームワーク {#social-component-framework}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

ソーシャルコンポーネントフレームワーク (SCF) を使用すると、サーバー側とクライアント側の両方で Communities コンポーネントを設定、カスタマイズ、拡張するプロセスが簡単になります。

フレームワークの利点：

* **機能**:80%の使用例に対するカスタマイズがほとんどあるいはまったく行われず、すぐに使用できる簡単な統合
* **スキン可能**:CSS スタイル設定でのHTML属性の一貫した使用
* **拡張可能**:コンポーネントの実装は、オブジェクト指向でビジネスロジックが軽量で、サーバー上に増分的なビジネスログインを簡単に追加できます。
* **柔軟**:簡単にオーバーレイおよびカスタマイズできる、単純なロジックのない JavaScript テンプレート
* **アクセス可能**:HTTP API は、任意のクライアント（モバイルアプリを含む）からの投稿をサポートしています
* **ポータブル**:あらゆるテクノロジーで構築された Web ページに統合/埋め込み

インタラクティブを使用してオーサーインスタンスまたはパブリッシュインスタンスで参照する [コミュニティコンポーネントガイド](components-guide.md).

## 概要 {#overview}

SCF では、コンポーネントは、SocialComponent POJO、Handlebars JS テンプレート（コンポーネントをレンダリングする）、および CSS（コンポーネントのスタイルを設定する）で構成されます。

Handlebars JS テンプレートは、モデル/ビュー JS コンポーネントを拡張して、クライアント上のコンポーネントとのユーザーインタラクションを処理できます。

データの変更をサポートする必要があるコンポーネントの場合は、従来の Web アプリケーションのモデル/データオブジェクトと同様に、データの編集/保存をサポートするように、SocialComponent API の実装を記述できます。 また、操作リクエストの処理、ビジネスロジックの実行、およびモデル/データオブジェクトでの API の呼び出しを行うために、操作（コントローラー）と操作サービスを追加できます。

SocialComponent API を拡張して、ビューレイヤーまたは HTTP クライアントに対してクライアントが必要とするデータを提供できます。

### クライアント用のページのレンダリング方法 {#how-pages-are-rendered-for-client}

![chlimage_1-25](assets/chlimage_1-25.png)

### コンポーネントのカスタマイズと拡張 {#component-customization-and-extension}

コンポーネントをカスタマイズまたは拡張するには、オーバーレイと拡張のみを/apps ディレクトリに書き込み、将来のリリースへのアップグレードプロセスを簡素化します。

* スキニング用
   * 次の項目のみ [CSS で編集が必要](client-customize.md#skinning-css)
* 外観と操作性
   * JS テンプレートと CSS の変更
* 外観、操作性、UX
   * JS テンプレート、CSS およびの変更 [JavaScript の拡張/オーバーライド](client-customize.md#extending-javascript)
* JS テンプレートまたはGETエンドポイントで使用可能な情報を変更するには
   * の拡張 [SocialComponent](server-customize.md#socialcomponent-interface)
* 操作中にカスタム処理を追加するには
   * を書く [OperationExtension](server-customize.md#operationextension-class)
* 新しいカスタム操作を追加するには
   * 新しい [Sling Post 操作](server-customize.md#postoperation-class)
   * 既存を使用 [OperationServices](server-customize.md#operationservice-class) 必要に応じて
   * 必要に応じてクライアント側から操作を呼び出す JavaScript コードを追加します

## サーバー側フレームワーク {#server-side-framework}

このフレームワークは、サーバー上の機能にアクセスし、クライアントとサーバーの間のインタラクションをサポートする API を提供します。

### Java API {#java-apis}

Java API は、簡単に継承またはサブクラス化される抽象クラスおよびインターフェイスを提供します。

メインクラスは、 [サーバー側のカスタマイズ](server-customize.md) ページ。

訪問 [ストレージリソースプロバイダの概要](srp.md) を参照してください。

### HTTP API {#http-api}

HTTP API は、PhoneGap アプリ、ネイティブアプリ、その他の統合やマッシュアップ用に、カスタマイズの容易さとクライアントプラットフォームの選択をサポートします。 さらに、HTTP API を使用すると、コミュニティサイトをクライアントなしでサービスとして実行できるので、フレームワークコンポーネントを任意のテクノロジーで構築された任意の Web ページに統合できます。

### HTTP API -GETリクエスト {#http-api-get-requests}

すべての SocialComponent に対して、フレームワークは HTTP ベースの API エンドポイントを提供します。 このエンドポイントにアクセスするには、「.social.json」セレクターと拡張子を使用してGETリクエストをリソースに送信します。 Sling を使用して、要求が `DefaultSocialGetServlet`.

：
`DefaultSocialGetServlet`

1. リソース (resourceType) を `SocialComponentFactoryManager`とは、 `SocialComponent`リソースを表しています。

1. ファクトリを呼び出し、を受け取ります。 `SocialComponent`リソースとリクエストを処理できる
1. を呼び出します。 `SocialComponent`：リクエストを処理し、結果の JSON 表現を返します。
1. JSON 応答をクライアントに返します。

**`GET Request`**

デフォルトのGETサーブレットは、SocialComponent がカスタマイズ可能な JSON を使用して応答する.social.json 要求をリッスンします。

![chlimage_1-26](assets/chlimage_1-26.png)

### HTTP API -POSTリクエスト {#http-api-post-requests}

GET（読み取り）操作に加えて、フレームワークは、作成、更新、削除など、コンポーネントに対する他の操作を有効にするエンドポイントパターンを定義します。 これらのエンドポイントは、入力を受け入れ、HTTP ステータスコードまたは JSON 応答オブジェクトを使用して応答する HTTP API です。

このフレームワークエンドポイントパターンにより、CUD 操作が拡張可能で、再利用可能で、テスト可能になります。

**`POST Request`**

SlingPOST:operation は、すべての SocialComponent 操作に対して存在します。 各操作のビジネスロジックとメンテナンスコードは、HTTP API を通じて、または OSGi サービスとして他の場所からアクセスできる OperationService にラップされます。 前/後のアクションに対するプラグ可能な操作拡張をサポートするフックが提供されます。

![chlimage_1-27](assets/chlimage_1-27.png)

### ストレージリソースプロバイダー (SRP) {#storage-resource-provider-srp}

に保存された UGC の処理について学ぶには、以下を実行します。 [コミュニティコンテンツストア](working-with-srp.md)を参照してください。

* [ストレージリソースプロバイダの概要](srp.md)  — 概要とリポジトリ使用の概要
* [SRP と UGC の基本事項](srp-and-ugc.md) - SRP API ユーティリティメソッドと例
* [SRP を使用した UGC へのアクセス](accessing-ugc-with-srp.md)  — コーディングガイドライン

### サーバー側のカスタマイズ {#server-side-customizations}

訪問 [サーバー側のカスタマイズ](server-customize.md) サーバー側のコミュニティコンポーネントのビジネスロジックと動作のカスタマイズに関する情報。

## Handlebars JS テンプレート言語 {#handlebars-js-templating-language}

新しいフレームワークの顕著な変更の 1 つは、 [Handlebars JS](https://handlebarsjs.com/) テンプレート言語 (HBS)：サーバークライアントレンダリング用の一般的なオープンソーステクノロジーです。

HBS スクリプトはシンプルでロジックがなく、サーバーとクライアントの両方でコンパイルし、オーバーレイとカスタマイズが容易で、HBS はクライアント側のレンダリングをサポートしているので、クライアント UX と自然にバインドされます。

このフレームワークには、次のような機能が用意されています。 [Handlebars ヘルパー](handlebars-helpers.md) これは、SocialComponents を開発する際に役立ちます。

サーバー上で、Sling がGETリクエストを解決すると、そのリクエストの応答に使用されるスクリプトが識別されます。 スクリプトが HBS テンプレート (.hbs) の場合、Sling は要求を Handlebars エンジンに委任します。 次に、Handlebars Engine は、適切な SocialComponentFactory から SocialComponent を取得し、コンテキストを構築し、HTMLをレンダリングします。

### アクセス制限なし {#no-access-restriction}

Handlebars(HBS) テンプレートファイル (.hbs) は、.jsp および.html テンプレートファイルに似ていますが、クライアントブラウザーとサーバーの両方でレンダリングに使用できます。 したがって、クライアント側テンプレートを要求するクライアントブラウザーは、サーバーから.hbs ファイルを受け取ります。

これには、Sling 検索パス内のすべての HBS テンプレート（/libs/または/apps 下の任意の.hbs ファイル）を、オーサーまたはパブリッシュから任意のユーザーが取得できる必要があります。

.hbs ファイルへの HTTP アクセスは禁止されていない可能性があります。

### コミュニティコンポーネントの追加または追加 {#add-or-include-a-communities-component}

ほとんどのコミュニティコンポーネントは、 *追加済み* Sling アドレス可能リソースとして。 一部のコミュニティコンポーネントは、 *含む* を既存のリソース以外としてテンプレートに追加し、ユーザー生成コンテンツ (UGC) を書き込む場所を動的に組み込み、カスタマイズできるようにします。

どちらの場合も、コンポーネントの [必要なクライアントライブラリ](clientlibs.md) は、も存在する必要があります。

**コンポーネントを追加**

コンポーネントの追加とは、コンポーネントブラウザー（サイドキック）から作成者編集モードでページにドラッグした場合など、リソース（コンポーネント）のインスタンスを追加するプロセスを指します。

結果は、par ノードの下の JCR 子ノード（Sling アドレス可能）になります。

**コンポーネントを含める**

コンポーネントを含めると、 [「存在しない」リソース](srp.md#for-non-existing-resources-ners) （JCR ノードなし）をテンプレート内に追加します（スクリプト言語の使用など）。

AEM 6.1 以降では、コンポーネントが追加される代わりに動的に含まれる場合、コンポーネントのプロパティをオーサー*デザイン*モードで編集できます。

動的に含めることができるのは、一部のAEM Communitiesコンポーネントのみです。 次のようになります。

* [コメント](essentials-comments.md)
* [レーティング](rating-basics.md)
* [レビュー](reviews-basics.md)
* [投票](essentials-voting.md)

この [コミュニティコンポーネントガイド](components-guide.md) を使用すると、インクルード可能なコンポーネントを追加からインクルードに切り替えることができます。

**Handlebars を使用する場合** テンプレート言語、存在しないリソースは [ヘルパーを含める](handlebars-helpers.md#include) resourceType を指定する。

`{{include this.id path="comments" resourceType="social/commons/components/hbs/comments"}}`

**JSP を使用する場合**&#x200B;の場合、リソースはタグを使用して [cq:include](../../help/sites-developing/taglib.md#lt-cq-include):

```
<cq:include path="votes" 
 resourceType="social/tally/components/voting" />
```

>[!NOTE]
>
>テンプレートにコンポーネントを追加または追加する代わりに、ページに動的に追加するには、 [コンポーネントのサイドロード](sideloading.md).

### Handlebars ヘルパー {#handlebars-helpers}

詳しくは、 [SCF Handlebars ヘルパー](handlebars-helpers.md) SCF で使用可能なカスタムヘルパーの一覧と説明。

## クライアント側フレームワーク {#client-side-framework}

### Model-View JavaScript フレームワーク {#model-view-javascript-framework}

フレームワークには、 [Backbone.js](https://www.backbonejs.org/)：モデル表示の JavaScript フレームワークで、リッチでインタラクティブなコンポーネントの開発を容易にします。 オブジェクト指向の特性は、拡張可能/再利用可能なフレームワークをサポートします。 クライアントとサーバー間の通信は、HTTP API を使用して簡単になります。

このフレームワークでは、サーバー側の Handlebars テンプレートを利用して、クライアント用にコンポーネントをレンダリングします。 モデルは、HTTP API によって生成された JSON 応答に基づいています。 ビューは、Handlebars テンプレートによって生成されるHTMLに結合され、インタラクティビティを提供します。

### CSS の規則 {#css-conventions}

CSS クラスを定義および使用する際の推奨規則を次に示します。

* 明確に名前空間化された CSS クラスセレクター名を使用し、「heading」、「image」などの汎用名を使用しないでください。
* 特定のクラスセレクタースタイルを定義して、CSS スタイルシートがページ上の他の要素やスタイルとうまく連携するようにします。 例：`.social-forum .topic-list .li { color: blue; }`
* スタイル設定用の CSS クラスを、JavaScript によって駆動される UX 用の CSS クラスとは別に保持する

### クライアント側のカスタマイズ {#client-side-customizations}

クライアント側のコミュニティコンポーネントの外観と動作をカスタマイズするには、 [クライアント側のカスタマイズ](client-customize.md)（次の情報を含む）:

* [オーバーレイ](client-customize.md#overlays)
* [拡張子](client-customize.md#extensions)
* [HTMLマークアップ](client-customize.md#htmlmarkup)
* [CSS のスキニング](client-customize.md#skinning-css)
* [JavaScript の拡張](client-customize.md#extending-javascript)
* [SCF の clientlibs](client-customize.md#clientlibs-for-scf)

## 機能とコンポーネントの基本事項 {#feature-and-component-essentials}

開発者向けの重要な情報については、 [機能とコンポーネントの基本事項](essentials.md) 」セクションに入力します。

開発者に関する追加情報については、 [コーディングのガイドライン](code-guide.md) 」セクションに入力します。

## トラブルシューティング {#troubleshooting}

一般的な問題と既知の問題については、 [トラブルシューティング](troubleshooting.md) 」セクションに入力します。
