---
title: オーサリング - 環境とツール
seo-title: オーサリング - 環境とツール
description: Web サイトコンソールを使用すると、Web サイトを管理したり、Web サイト内を移動したりできます。2 つのペインを使用して、Web サイトの構造を展開したり、必要な要素に対するアクションを実行できます。
seo-description: Web サイトコンソールを使用すると、Web サイトを管理したり、Web サイト内を移動したりできます。2 つのペインを使用して、Web サイトの構造を展開したり、必要な要素に対するアクションを実行できます。
uuid: ec4ccc63-a3b8-464c-9c1a-204fd5d3b121
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 278195a6-3452-4966-9d56-022815cf6fb4
translation-type: tm+mt
source-git-commit: cdec5b3c57ce1c80c0ed6b5cb7650b52cf9bc340
workflow-type: tm+mt
source-wordcount: '933'
ht-degree: 86%

---


# オーサリング - 環境とツール{#authoring-the-environment-and-tools}

AEM のオーサリング環境は、コンテンツを編成および編集するための様々なメカニズムを提供しています。提供されるツールには、様々なコンソールおよびページエディターからアクセスします。

## サイト管理 {#site-administration}

**Web サイト**&#x200B;コンソールを使用すると、Web サイトを管理したり、Web サイト内を移動したりできます。2 つのペインを使用して、Web サイトの構造を拡張したり、必要な要素に対しアクションをおこなうことができます。

![chlimage_1-153](assets/chlimage_1-153.png)

## ページコンテンツの編集 {#editing-your-page-content}

クラシック UI には、コンテンツファインダーとサイドキックを利用する個別のページエディターがあります。

`http://localhost:4502/cf#/content/geometrixx/en/products/triangle.html`

![chlimage_1-154](assets/chlimage_1-154.png)

## ヘルプへのアクセス {#accessing-help}

AEM から様々な&#x200B;**ヘルプ**&#x200B;リソースに直接アクセスできます。

[コンソールツールバーからヘルプに](/help/sites-classic-ui-authoring/author-env-basic-handling.md#accessing-help)アクセスするほかにも、サイドキックから（？アイコンを使用して）ページ編集中にアクセスできます。

![](do-not-localize/sidekick-collapsed-2.png)

または、特定のコンポーネントの編集ダイアログの&#x200B;**ヘルプ**&#x200B;ボタンを使用してアクセスできます。これにより、コンテキスト依存のヘルプが表示されます。

## サイドキック {#sidekick}

サイドキックの「**コンポーネント**」タブでは、現在のページに追加可能なコンポーネントを閲覧できます。目的のグループを展開して、コンポーネントをページ上の必要な位置までドラッグできます。

![chlimage_1-155](assets/chlimage_1-155.png)

## コンテンツファインダー {#the-content-finder}

コンテンツファインダーを使用すると、ページを編集しているときに、リポジトリ内のアセットやコンテンツをすばやく簡単に見つけることができます。

コンテンツファインダーを使用して、幅広いリソースを検索できます。適宜、次の項目をドラッグしてページ上の段落にドロップできます。

* [画像](#finding-images)
* [ドキュメント](#finding-documents)
* [ムービー](#finding-movies)
* [Scene 7 メディアブラウザー](/help/sites-administering/scene7.md#scene7contentbrowser)
* [ページ](/help/sites-classic-ui-authoring/classic-page-author-env-tools.md#finding-pages)
* [段落](#referencing-paragraphs-from-other-pages)
* [製品](/help/sites-classic-ui-authoring/classic-page-author-env-tools.md#products)
* または、[リポジトリ構造から Web サイトを参照](#the-content-finder)できます

すべてのオプションについて、[特定の項目を検索](#the-content-finder)できます。

### 画像の検索 {#finding-images}

このタブには、リポジトリ内の画像が一覧表示されます。

ページで画像の段落を作成したら、その段落に項目をドラッグ＆ドロップできます。

![chlimage_1-156](assets/chlimage_1-156.png)

### ドキュメントの検索 {#finding-documents}

このタブには、リポジトリ内のドキュメントが一覧表示されます。

ページでダウンロードの段落を作成したら、その段落に項目をドラッグ＆ドロップできます。

![chlimage_1-157](assets/chlimage_1-157.png)

### ムービーの検索 {#finding-movies}

このタブには、リポジトリ内のムービー（Flash 項目など）が一覧表示されます。

ページで適切な段落（Flash など）を作成したら、その段落に項目をドラッグ＆ドロップできます。

![chlimage_1-158](assets/chlimage_1-158.png)

### 製品 {#products}

このタブには、商品が一覧表示されます。ページで適切な段落（商品など）を作成したら、その段落に項目をドラッグ＆ドロップできます。

![chlimage_1-159](assets/chlimage_1-159.png)

### ページの検索 {#finding-pages}

このタブには、すべてのページが表示されます。任意のページを重複クリックして、編集用に開きます。

![chlimage_1-160](assets/chlimage_1-160.png)

### 他のページからの段落の参照 {#referencing-paragraphs-from-other-pages}

このタブを使用すると、他のページを検索できます。そのページのすべての段落が一覧表示されます。段落を現在のページにドラッグできます。これにより、元の段落への参照が作成されます。

![chlimage_1-161](assets/chlimage_1-161.png)

### リポジトリの一覧表示の使用 {#using-the-full-repository-view}

このタブには、リポジトリ内のすべてのリソースが一覧表示されます。

![chlimage_1-162](assets/chlimage_1-162.png)

### コンテンツブラウザーでの検索の使用 {#using-search-with-the-content-browser}

すべてのオプションについて、特定の項目を検索できます。検索パターンに一致するタグとリソースが一覧表示されます。

![screen_shot_2012-02-08at100746am](assets/screen_shot_2012-02-08at100746am.png)

検索にワイルドカードを使用することもできます。サポートされているワイルドカードは、次のとおりです。

* `*` - 0個以上の文字のシーケンスに一致します。

* `?` - 1文字に一致します。

>[!NOTE]
>
>ワイルドカード検索を実行するには、擬似プロパティの「name」を使用する必要があります。

例えば、次の名前でアクセス可能な画像があるとします。

`ad-nmvtis.jpg`

以下の検索パターンで、この画像（およびこのパターンに一致するその他の画像）が見つかります。

* `name:*nmv*`
* `name:AD*`  — 文字のマッチングでは大文字と小文字が ** 区別されません。
* `name:ad?nm??is.*` -クエリには任意の数のワイルドカードを使用できます。

>[!NOTE]
>
>[SQL2](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/javadoc/org/apache/jackrabbit/commons/query/sql2/package-summary.html)検索も使用できます。

## 参照の表示 {#showing-references}

AEM では、現在作業しているページにリンクしているページを表示できます。

直接ページ参照を表示するには：

1. サイドキックで、「**ページ**」タブのアイコンを選択します。

   ![screen_shot_2012-02-16at83127pm](assets/screen_shot_2012-02-16at83127pm.png)

1. **参照を表示を選択…** AEMは、参照ウィンドウを開き、選択したページを参照するページとそのパスを表示します。

   ![screen_shot_2012-02-16at83311pm](assets/screen_shot_2012-02-16at83311pm.png)

状況によっては、サイドキックから次のようなアクションを追加で実行できます。

* [ローンチ](/help/sites-classic-ui-authoring/classic-launches.md)
* [ライブコピー](/help/sites-administering/msm.md)

* [ブループリント](/help/sites-administering/msm-best-practices.md)

その他の[ページ間の関係は Web サイトコンソールから確認できます](/help/sites-classic-ui-authoring/author-env-basic-handling.md#page-information-on-the-websites-console)。

## 監査ログ  {#audit-log}

**監査ログ**&#x200B;には、サイドキックの「**情報**」タブからアクセスできます。ここには、現在のページで実行された最近のアクションが一覧表示されます。次に例を示します。

![chlimage_1-163](assets/chlimage_1-163.png)

## ページ情報 {#page-information}

また、Webサイトコンソール[は、ページ](/help/sites-classic-ui-authoring/author-env-basic-handling.md#page-information-on-the-websites-console)の現在のステータスに関する情報（パブリケーション、変更、ロック、LiveCopyなど）も提供します。

## ページモード {#page-modes}

クラシック UI でページを編集中に、サイドキックの下部のアイコンを使用して次のモードにアクセスできます。

![](do-not-localize/chlimage_1-15.png)

サイドキックの下部に並ぶ 1 行のアイコンは、ページを操作するモードの切り替えに使用します。

* [編集](/help/sites-classic-ui-authoring/classic-page-author-edit-mode.md)

   これがデフォルトのモードであり、ページの編集、コンポーネントの追加または削除およびその他の変更を行うことができます。

* [プレビュー](/help/sites-classic-ui-authoring/classic-page-author-edit-content.md#previewing-pages)

   このモードを使用すると、ページが Web サイトで最終的にどのように表示されるかをプレビューできます。

* [デザイン](/help/sites-classic-ui-authoring/classic-page-author-design-mode.md#main-pars-procedure-0)

   このモードでは、アクセシブルなコンポーネントを設定して、ページのデザインを編集できます。

>[!NOTE]
>
>その他に次のオプションも利用できます。
>
>* [基礎モード](/help/sites-classic-ui-authoring/classic-feature-scaffolding.md)
>* [ClientContext](/help/sites-administering/client-context.md)
>* Web サイト - Web サイトコンソールを開きます。
>* 再読み込み - ページを更新します。


## キーボードショートカット {#keyboard-shortcuts}

様々な[キーボードショートカット](/help/sites-classic-ui-authoring/classic-page-author-keyboard-shortcuts.md)を利用できます。
