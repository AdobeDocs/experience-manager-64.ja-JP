---
title: コンテンツフラグメント用コンポーネント
seo-title: Components for Content Fragments
description: AEM のコンテンツフラグメントは、ページから独立したアセットとして作成および管理されます
seo-description: AEM content fragments are created and managed as page-independent assets
uuid: 289ed9cb-9531-43a9-b0d8-a3499e2e9ee5
contentOwner: Alison Heimoz
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: components
content-type: reference
discoiquuid: 76b63c7c-f7ea-46be-8d10-6c1a30af2e2b
pagetitle: Components for Content Fragments
exl-id: 516c1561-5c13-4301-8009-9b021087cec7
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '932'
ht-degree: 82%

---

# コンテンツフラグメント用コンポーネント{#components-for-content-fragments}

>[!CAUTION]
>
>一部のコンテンツフラグメント機能には、 [AEM 6.4 Service Pack 2(6.4.2.0)](/help/release-notes/sp-release-notes.md).

## フラグメントオーサリング用コンポーネント {#components-for-fragment-authoring}

>[!CAUTION]
>
>フラグメントエディターで使用する実際のコンポーネントは、まだ変更される可能性があるので、拡張または変更することはお勧めしません。

詳しくは、 [コンテンツフラグメント管理 API — クライアント側](/help/sites-developing/customizing-content-fragments.md#the-content-fragment-management-api-client-side).

## ページオーサリング用コンポーネント {#components-for-page-authoring}

>[!CAUTION]
>
>[コンテンツフラグメントコアコンポーネント](https://helpx.adobe.com/experience-manager/core-components/using/content-fragment-component.html)が推奨されます。詳しくは、[コアコンポーネントの開発](https://helpx.adobe.com/experience-manager/core-components/using/developing.html)を参照してください。
>
>この節では、コンテンツフラグメント用に提供されるオリジナル コンテンツについて説明します（**一般**&#x200B;グループの&#x200B;**コンテンツフラグメント**）。

Adobe Experience Manager（AEM）のコンテンツフラグメントは、[ページに依存しないアセット](/help/assets/content-fragments.md)として作成および管理されます。コンテンツフラグメントを使用すると、チャネルに特化しないコンテンツをチャネル固有のバリエーションと共に作成できます。[その後、コンテンツページをオーサリングする際に、これらのフラグメントとそのバリエーションを使用できます](/help/sites-authoring/content-fragments.md).また、既存のコンテンツフラグメントアセットを使用する場合は、 [アセットブラウザーからページにドラッグする](/help/sites-authoring/content-fragments.md#adding-a-content-fragment-to-your-page) （基盤コンポーネントの画像など、他のアセットベースのコンポーネントに関して）。 既製のコンテンツフラグメントコンポーネントには、参照されているコンテンツフラグメントの[要素](/help/assets/content-fragments.md#constituent-parts-of-a-content-fragment)が 1 つだけ表示されます。コンポーネントダイアログを使用して、 [要素、バリエーションおよびフラグメントの段落の範囲](/help/assets/content-fragments.md#constituent-parts-of-a-content-fragment) を選択します。

>[!NOTE]
>
>このコンテンツフラグメントコンポーネントは、廃止された記事コンポーネントの強化版として AEM 6.2 で導入されました。

>[!NOTE]
>
>コンテンツフラグメントは、クラシック UI ではサポートされません。

### 定義 {#definition}

**コンテンツフラグメント**&#x200B;コンポーネントは、コンテンツフラグメントアセット（効果的に拡張されたテキストアセット）への参照を保持するために使用されます。コンテンツフラグメントのリソースタイプは次のとおりです。

* `dam/cfm/components/contentfragment/contentfragment`

参照を定義するには、次のプロパティを使用します。

* `fileReference`

タッチ操作対応 UI のエディター のみ、コンテンツフラグメントコンポーネントを完全にサポートします。これには、次のクライアントライブラリが含まれます。

* `cq.authoring.editor.plugin.cfm`

このライブラリは、コンテンツフラグメント専用の機能をエディターに追加します。例えば、ページ上のコンテンツフラグメントの追加および設定機能のサポート、アセットブラウザーでのコンテンツフラグメントアセットの検索機能およびサイドパネルでの関連コンテンツの検索機能を使用できます。

### 中間コンテンツ {#in-between-content}

**コンテンツフラグメント**&#x200B;コンポーネントを使用すると、表示される[要素](/help/assets/content-fragments.md#constituent-parts-of-a-content-fragment)のさまざまな段落の間に追加コンポーネントを挿入できます。基本的に、表示される要素は様々な段落で構成されます（各段落はキャリッジリターンによってマークされます）。これらの段落の間に、他のコンポーネントを使用してコンテンツを挿入できます。

技術的には、表示される要素の各段落は個別の parsys 内に存在しており、段落間に追加される各コンポーネントは（内部的な処理では）その parsys に挿入されます。

言い換えると、コンテンツフラグメントコンポーネントのインスタンスが 3 つの段落で構成されている場合、コンポーネントはリポジトリ内に 3 つの異なる parsys を持ちます。コンテンツフラグメントに追加される中間コンテンツはすべて、実際にはこれらの parsys の内部に配置されます。

リポジトリ内では、中間コンテンツは全体の段落構造内での自身の位置を基準として格納されます。実際の段落コンテンツに付加されるわけではありません。

この仕組みを理解するために、次のような状況を考えてみましょう。

* コンテンツフラグメントのインスタンスが 3 つの段落で構成されている
* 2 番目の段落の後に、既にいくつかのコンテンツが挿入されている

   * この場合、コンテンツは 2 番目の parsys に格納されます。

基本的に、このインスタンスの段落構造を変更した場合は（表示される段落のバリエーション、要素または範囲を変更するなど）、表示される中間コンテンツに影響が及びます。例えば次の場合が考えられます。

* コンテンツフラグメントコンポーネントが編集され、2 番目の段落の前に別の段落が追加される：

   * 中間コンテンツは、新規作成された段落の後に表示されます（2 番目の parsys が新規作成された段落を保持するようになります）。

* コンテンツフラグメントコンポーネントが編集され、2 番目の段落が削除される：

   * 中間コンテンツは、以前は 3 番目だった段落の後に表示されます（2 番目の parsys が、以前は 3 番目だった段落を保持するようになります）。

* 最初の段落だけを表示するようにコンテンツフラグメントコンポーネントが設定される：

   * 中間コンテンツは表示されなくなります（新しい設定によって、2 番目の parsys はレンダリングされなくなります）。

### コンテンツフラグメントコンポーネントのカスタマイズ {#customizing-the-content-fragment-component}

既製のコンテンツフラグメントコンポーネントを拡張のブループリントとして使用するときは、次のルールを守ってください。

* HTL レンダリングスクリプトと関連 POJO を再利用して、中間コンテンツ機能の実装方法を確認します。
* コンテンツフラグメントノードを再利用します。 `cq:editConfig`

   * この `afterinsert`/ `afteredit`/ `afterdelete` リスナーは、JS イベントのトリガーに使用されます。 これらのイベントを `cq.authoring.editor.plugin.cfm` クライアントライブラリで処理して、関連コンテンツをサイドパネルに表示します。
   * コンテンツフラグメントアセットのドラッグをサポートするように `cq:dropTargets` を設定します。
   * ページエディターでコンテンツフラグメントのオーサリングをサポートするように `cq:inplaceEditing` を設定します。フラグメントのインプレースエディターは `cq.authoring.editor.plugin.cfm` クライアントライブラリで定義され、クイックリンクによって現在の[要素／バリエーション](/help/assets/content-fragments.md#constituent-parts-of-a-content-fragment)を[フラグメントエディター](/help/assets/content-fragments-variations.md)で開けるようにします。

### レンダリング前のアセットの書き直し {#asset-rewriting-before-rendering}

コンテンツフラグメント管理では、初期レンダリング処理を使用してページの最終的な HTML 出力を生成します。これは、コンテンツフラグメントコンポーネントによって内部で使用されますが、参照ページ上の参照フラグメントを更新するバックグラウンド処理でも使用されます。

内部では、このレンダリングに Sling Rewriter を使用します。それぞれの設定は、次の場所にあります。 `/libs/dam/config/rewriter/cfm` 必要に応じて調整できます。 詳しくは、 [Apache Sling Rewriter](https://sling.apache.org/documentation/bundles/output-rewriting-pipelines-org-apache-sling-rewriter.html) を参照してください。

既成の設定は、次の変換サービスを使用します。

* `transformer-cfm-payloadfilter`  — 取得用 `body` 部分 ( `<body>...</body>`) をフラグメントのHTMLのみ

* `transformer-cfm-parfilter` - 段落範囲が指定されている場合に、不要な段落を除外します（コンテンツフラグメントコンポーネントで実行可能）
* `transformer-cfm-assetprocessor` - フラグメントに埋め込まれたアセットのリストを取得するために内部で使用されます

レンダリング処理は ` [com.adobe.cq.dam.cfm.content.FragmentRenderService](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/javadoc/com/adobe/cq/dam/cfm/ContentFragment.html)` を通じて公開され、必要に応じて、（例えば）カスタムコンポーネントによって活用されます。
