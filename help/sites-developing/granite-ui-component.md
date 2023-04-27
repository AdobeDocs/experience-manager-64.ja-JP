---
title: 新しい Granite UI フィールドコンポーネントの作成
seo-title: Creating a New Granite UI Field Component
description: Granite UI は、フィールドと呼ばれる、フォームで使用するように設計された様々なコンポーネントを提供します
seo-description: Granite UI provides a range of components designed to be used in forms, called fields
uuid: cf26e057-4b0c-45f4-8975-2c658517f20e
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: platform
content-type: reference
discoiquuid: 94b9eeee-aae3-4b28-9d6f-1be0e4acd982
exl-id: 9a6cc25e-e54e-4b8a-8fdd-bcd65d8fe601
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '539'
ht-degree: 43%

---

# 新しい Granite UI フィールドコンポーネントの作成{#creating-a-new-granite-ui-field-component}

Granite UI には、フォームで使用するようにデザインされた幅広いコンポーネントが用意されています。これらを Granite の UI 用語では「フィールド」と呼びます&#x200B;*。*&#x200B;標準の Granite フォームコンポーネントは、次の場所で使用できます。

`/libs/granite/ui/components/foundation/form/*`

>[!NOTE]
>
>これらの Granite UI フォームフィールドは、 [コンポーネントダイアログ](/help/sites-developing/developing-components.md).

>[!NOTE]
>
>フィールドの詳細については、 [Granite UI ドキュメント](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/granite-ui/api/index.html).

Granite UI Foundation フレームワークを使用して、Granite コンポーネントを開発または拡張します。 これには次の 2 つの要素があります。

* サーバー側：

   * 基盤コンポーネントのコレクション

      * 基盤 — モジュラー型、合成可能、レイヤブル、再利用可能
      * コンポーネント - Sling コンポーネント
   * アプリケーション開発を支援するヘルパー


* クライアント側：

   * ハイパーメディア駆動型 UI を通じて一般的なインタラクションパターンを実現するための語彙 (HTML言語の拡張 ) を提供する clientlib のコレクション

一般的な Granite UI コンポーネントである `field` は、以下の 2 つのファイルで構成されています。

* `init.jsp`：ラベル付けや説明などの一般的な処理を扱い、フィールドをレンダリングする際に必要になるフォーム値を提供します。
* `render.jsp`：ここで、フィールドの実際のレンダリングが実行され、カスタムフィールドの場合は上書きされる必要があります。`init.jsp` にインクルードされます。

詳しくは、 [Granite UI ドキュメント — フィールド](https://helpx.adobe.com/jp/experience-manager/6-4/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/components/foundation/form/field/index.html) 詳細を表示する場合

例えば、以下を参照してください。

* `cqgems/customizingfield/components/colorpicker`

   * [コードサンプル](/help/sites-developing/developing-components-samples.md#code-sample-how-to-customize-dialog-fields)で提供

* `granite/ui/components/foundation/form`

>[!NOTE]
>
>このメカニズムは JSP を使用するので、i18n と XSS は標準では提供されません。 つまり、文字列を国際化してエスケープする必要があります。 次のディレクトリには、標準インスタンスの汎用フィールドが含まれています。これらを参照として使用できます。
>
>`/libs/granite/ui/components/foundation/form` ディレクトリ

## コンポーネント用のサーバーサイドスクリプトの作成 {#creating-the-server-side-script-for-the-component}

カスタマイズしたフィールドは、`render.jsp` スクリプトのみを上書きする必要があります。このスクリプトは、コンポーネントのマークアップを提供します。この JSP（レンダリングスクリプト）は、マークアップのラッパーと見なすことができます。

1. `sling:resourceSuperType` プロパティを使用して、以下から継承する新しいコンポーネントを作成します。

   `/libs/granite/ui/components/foundation/form/field`

1. 以下のスクリプトを上書きします。

   `render.jsp`

   このスクリプトでは、生成された要素の操作方法をクライアントが把握できるように、ハイパーメディアマークアップ（つまり、ハイパーメディアアフォーダンスを含むエンリッチメントされたマークアップ）を生成する必要があります。 これは、Granite UI のサーバー側のコーディングスタイルに従う必要があります。

   カスタマイズする際に守る必要のある唯一の&#x200B;*決まりごと*&#x200B;は、以下を使用して、リクエストからフォーム値（`init.jsp` で初期化）を読み取ることです。

   ```
   // Delivers the value of the field (read from the content)
   ValueMap vm = (ValueMap) request.getAttribute(Field.class.getName());
   vm.get("value, String.class"); 
   ```

   詳しくは、デフォルトの Granite UI フィールドの実装（例：`/libs/granite/ui/components/foundation/form/textfield`）を参照してください。

   >[!NOTE]
   >
   >現時点では、JSP が推奨されるスクリプティングメソッドです。あるコンポーネントから別のコンポーネントに情報を渡す方法（フォームやフィールドのコンテキストでは非常に頻繁に使用されます）は、HTL では容易には使用できません。

## コンポーネントのクライアントライブラリの作成 {#creating-the-client-library-for-the-component}

特定のクライアント側の動作をコンポーネントに追加するには：

1. カテゴリ `cq.authoring.dialog` のクライアントライブラリを作成します。
1. カテゴリ `cq.authoring.dialog` のクライアントライブラリを作成し、その内部に `JS`／`CSS` を定義します。

   クライアントライブラリの内部に `JS`／`CSS` を定義します。

   >[!NOTE]
   >
   >現時点では、Granite UI には、JS 動作を直接追加するために使用できる、標準のリスナーやフックは用意されていません。 そのため、コンポーネントに JS 動作を追加するには、JS フックをカスタムクラスに実装し、マークアップの生成中にコンポーネントに割り当てる必要があります。
