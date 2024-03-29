---
title: コンポーネント
seo-title: Components
description: AEMには、すぐに使用できる様々なコンポーネントが付属しており、Web サイト作成者は包括的な機能を使用できます
seo-description: AEM comes with a variety of out-of-the-box components that provide comprehensive functionality for website authors
uuid: 55caeec3-add7-4d05-a620-07e33901adb7
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 53c37f8c-eb75-4134-9f91-8adb0a574360
exl-id: 8b83e8d2-09ad-4010-a69a-2af1907a1ca6
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '463'
ht-degree: 59%

---

# コンポーネント{#components}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

Adobe Experience Manager(AEM) には、すぐに使用できる様々なコンポーネントが付属しており、Web サイト作成者は包括的な機能を使用できます。 これらの機能は、[ページの編集](/help/sites-authoring/editing-content.md)時に使用でき、フィルタリングのために主な機能領域（コンポーネントグループと呼ばれます）でグループ化されています。

コンポーネントは、 [ページの編集](/help/sites-authoring/editing-content.md). フィルタリングを容易にするために、コンポーネントは主な機能領域（コンポーネントグループ）でグループ化されます。

>[!NOTE]
>
>このセクションでは、標準のAEMインストールで標準で使用できるコンポーネントについてのみ説明します。
>
>インスタンスによっては、要件に合わせて明示的に開発されたカスタマイズコンポーネントが存在する場合があります。これらは、ここで説明するいくつかのコンポーネントと同じ名前の場合があります。

## 一般的な使用方法 {#general-usage}

コンポーネントは、 **コンポーネント** タブをクリックします。 [ページの編集](/help/sites-authoring/editing-content.md).

コンポーネントを選択し、ページ上の必要な場所にドラッグできます。 その後、次を使用して編集できます。

* [プロパティの設定](/help/sites-authoring/editing-page-properties.md)
* [コンテンツの編集](/help/sites-authoring/editing-content.md)

* [コンテンツの編集 - 全画面表示モード](/help/sites-authoring/editing-content.md#edit-content-full-screen-mode)

ページへのコンポーネントの追加について詳しくは、[ページのコンテンツの編集](/help/sites-authoring/editing-content.md)を参照してください。\
コンポーネントは、コンポーネントグループと呼ばれる様々なカテゴリーに従って並べ替えられます。このようなコンポーネントグループの例を次に示します。

* **We.Retail**：[We.Retail 参照実装](/help/sites-developing/we-retail.md)で使用するためにプロキシ設定されたコアコンポーネントが含まれています。

* **We.Retail コマース**：カートや商品グリッドなどのコマースコンポーネントが含まれています。

* **一般**:レイアウトコンテナとエクスペリエンスフラグメントを含めます

## 全コンポーネントの概要 {#overview-of-all-components}

この [コンポーネントコンソール](/help/sites-authoring/default-components-console.md) は、AEMのインストールで提供されるコンポーネントグループとコンポーネントの概要を示しています。 個々のコンポーネントとその使用方法に関する主な情報を確認できます。

## コンポーネント - 主な領域 {#components-major-areas}

次のページには、コンポーネントに関する重要な追加情報へのリンクが記載されています。

* [コアコンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=ja) - コアコンポーネントは柔軟かつ機能豊富なオーサリング機能を提供します。ページを作成するうえで不可欠なコンテンツタイプが用意されています。

* [コミュニティ](/help/communities/author-communities.md) - コンポーネントには、web サイトのインタラクティブな機能（フォーラムやコメントなど）が用意されています。このコンポーネントの多くは[コミュニティサイト](/help/communities/overview.md)の作成時に追加されます。

* [e コマース](/help/sites-administering/ecommerce.md) - AEM の e コマース機能にも様々なコンポーネントが含まれています。実際の使用方法は、使用しているコマースエンジンによって異なります。

### コンポーネントの設定 {#configuring-components}

作成者が標準インストールでアクセスできるコンポーネントに加えて、他の様々なコンポーネントも使用できます。

* ページが最新の編集可能な推奨テンプレートに基づいている場合は、[テンプレートを編集](/help/sites-authoring/templates.md)して、コンポーネントを有効／無効にしたり、特定のコンポーネントのパラメーターを編集したりできます。
* ページが静的テンプレートに基づいている場合は、[デザインモード](/help/sites-authoring/default-components-designmode.md#enable-disable-components)を使用して、コンポーネントを有効／無効にしたり、特定のコンポーネントのパラメーターを編集したりできます。
