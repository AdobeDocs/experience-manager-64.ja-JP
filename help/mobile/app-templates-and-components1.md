---
title: アプリのテンプレートとコンポーネント
seo-title: App Templates and Components
description: このページでは、アプリのテンプレートとコンポーネントについて説明します。 テンプレートの構造に関する詳細情報が提供されます。
seo-description: Follow this page to learn about App Templates and Components. It provides detailed information on the structure of templates.
uuid: ba2fd91b-de5a-4f39-a976-5455f9983669
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/MOBILE
topic-tags: developing-on-demand-services-app
discoiquuid: 7f31c6a7-92d5-4a87-a9f0-68a82b834d5a
exl-id: 5480ac38-f651-4211-94f6-c588fb44ad55
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '441'
ht-degree: 9%

---

# アプリのテンプレートとコンポーネント{#app-templates-and-components}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

>[!NOTE]
>
>Adobeは、単一ページアプリケーションのフレームワークベースのクライアントサイドレンダリング（React など）を必要とするプロジェクトでは、SPA Editor を使用することをお勧めします。 [詳細情報](/help/sites-developing/spa-overview.md)を参照してください。

テンプレートは、ページの作成に使用され、選択した範囲内で使用できるコンポーネントを定義します。 テンプレートは、作成するページと同じ構造を持ち、実際のコンテンツを持たないノードの階層です。

各テンプレートには、使用可能なコンポーネントが選択されて表示されます。

* テンプレートは [コンポーネント](/help/sites-developing/components.md);
* コンポーネントはウィジェットを使用し、ウィジェットにアクセスできます。ウィジェットはコンテンツのレンダリングに使用されます。

>[!NOTE]
>
>CRXDE Liteを使用したAEMアプリケーションの開発方法については、 [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md).

テンプレートは、ページの基盤です。

ページを作成するには、テンプレートをコピーする必要があります (node-tree) **/apps/&lt;myapp>/templates/&lt;mytemplate>**) を site-tree 内の対応する位置にドラッグします。ページが **Web サイト** タブをクリックします。

また、このコピーアクションは、ページの初期コンテンツ（通常はトップレベルコンテンツのみ）と、ページのレンダリングに使用されるページコンポーネントのパス（子ノード jcr:content 内のすべて）を示す sling:resourceType プロパティも提供します。

## テンプレートの構造 {#structure-of-a-template}

考慮すべき 2 つの側面があります。

* テンプレート自体の構造
* テンプレートを使用する際に作成されるコンテンツの構造

テンプレートは、タイプのノードの下に作成されます **cq:Template**.

特に、様々なプロパティを設定できます。

* **jcr:title**  — テンプレートのタイトル。は、ページの作成時にダイアログに表示されます。
* **jcr:description**  — テンプレートの説明。は、ページの作成時にダイアログに表示されます。

このノードには次が含まれます *jcr:content (cq:PageContent)* 結果ページのコンテンツノードの基礎として使用されるノードこの参照は、 *sling:resourceType*：新しいページの実際のコンテンツのレンダリングに使用するコンポーネント。

>[!NOTE]
>
>AEMのテンプレートとコンポーネントの基本については、以下のリソースを参照してください。
>
>* [テンプレート](/help/sites-developing/templates.md)
>* [コンポーネント](/help/sites-developing/components.md)
>


テンプレートとコンポーネントについての基本的な知識が得られたら、次のリソースを参照してください。

* [テンプレートとコンポーネントの作成および追加](/help/mobile/mobile-ondemand-app-templates.md)
* [コンテンツのプロパティを使用したコンテンツのエクスポート](/help/mobile/on-demand-content-properties-exporting.md)
* [ベストプラクティス](/help/mobile/best-practices-aem-mobile.md)
* [AEM Mobile Content Services の開発](/help/mobile/developing-content-services.md)

### その他のリソース {#additional-resources}

モバイルアプリに関するその他のトピックについては、以下のリンクを参照してください。

* [モバイルとコンテンツ同期](/help/mobile/mobile-ondemand-contentsync.md)
* [モバイルアプリのテスト](/help/mobile/develop-mobile-apps-testing.md)
