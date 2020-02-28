---
title: ページへのSearch&amp;Promote機能の追加
seo-title: ページへのSearch&amp;Promote機能の追加
description: WebサイトでのSearch&Promote機能の統合、Search&amp;Promoteコンポーネントを使用して、キーワード検索、検索結果ページ検索の絞り込み、バナーなどの機能をページに追加できます。
seo-description: WebサイトでのSearch&Promote機能の統合、Search&amp;Promoteコンポーネントを使用して、キーワード検索、検索結果ページ検索の絞り込み、バナーなどの機能をページに追加できます。
uuid: 8831aa56-9d7f-44ca-9d32-5901bf762154
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.4/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 277d7e67-5778-48cb-89bb-29bcc734a485
translation-type: tm+mt
source-git-commit: cdec5b3c57ce1c80c0ed6b5cb7650b52cf9bc340

---


# Adding Search&amp;Promote features to your page {#adding-search-promote-features-to-your-page}

To integrate Search&amp;Promote capabilities in your web site, use the [!UICONTROL Search&amp;Promote] components to add the following features to your pages:

* キーワード検索
* 検索結果のページ
* 検索の絞り込み
* バナー

Search&amp;Promote 機能は、AEM の管理者が有効にしている場合にのみ使用できます。[Adobe Search&amp;Promote との統合](/help/sites-administering/search-and-promote.md)を参照してください。

Search&amp;Promote サーバーでは、ファセットや各コンポーネントが提供する情報が設定されています。次の表で、各コンポーネントの概要について説明します。後続のセクションではそれらの用途の詳細情報を提供します。

<table> 
 <tbody> 
  <tr> 
   <th>Search&amp;Promote のコンポーネント</th> 
   <th>説明</th> 
  </tr> 
  <tr> 
   <td>バナー</td> 
   <td>バナー広告を表示します。バナーは Search&amp;Promote を通じて収集されたデータに基づいて選択されます。<br /> </td> 
  </tr> 
  <tr> 
   <td>パンくず</td> 
   <td>検索キーワードとユーザーが検索結果に適用したフィルターの結果が表示されます。</td> 
  </tr> 
  <tr> 
   <td>チェックボックスリストファセット</td> 
   <td>検索結果をフィルタリングするためのファセットを選択するチェックボックスのリスト。</td> 
  </tr> 
  <tr> 
   <td>ドロップダウンファセット</td> 
   <td>検索結果をフィルタリングするためのファセットのドロップダウンリスト。</td> 
  </tr> 
  <tr> 
   <td>リンクリストファセット</td> 
   <td>検索結果をフィルタリングするためのファセットリンクのリスト。</td> 
  </tr> 
  <tr> 
   <td>ページネーション</td> 
   <td>検索結果のページを検索するためのコントロール。</td> 
  </tr> 
  <tr> 
   <td>結果</td> 
   <td>キーワード検索の結果を表示します。</td> 
  </tr> 
  <tr> 
   <td>検索</td> 
   <td>ページに検索フィールドを追加します。</td> 
  </tr> 
 </tbody> 
</table>

## 検索結果ページの作成 {#creating-the-search-results-page}

WCM Web サイトコンソールを使用して、検索結果を表示するページを作成します。同じ Search&amp;Promote サービスを使用している場合、すべての検索コンポーネントからの検索結果をこのページに表示することができます。

ユーザーは結果コンポーネントとページネーションコンポーネントで検索結果をレビューできます。**[!UICONTROL 結果]**&#x200B;コンポーネントには、編集モードやデザインモードで構成可能なプロパティがありません。結果コンポーネントには検索結果の一覧と、他のページへのリンク、指定の検索キーワードによる検索結果の数が表示されます。

![srchresultscomp](assets/srchresultscomp.png)

**[!UICONTROL ページネーション]**&#x200B;コンポーネントでは、複数ページの検索結果を移動できます。ユーザーはページ数を確認し、次のページや前のページに移動したり、ページを選択して開いたり、すべての結果を 1 つのページに表示したりできます。

![文字列化](assets/srchpagination.png)

You can configure the following component properties in [!UICONTROL Edit] mode to control runtime behavior:

* **[!UICONTROL 単一の結果ページを非表示]** — 検索で結果の単一ページが返された場合にページナビゲーションコントロールを非表示にするには、このオプションを選択します。
* **[!UICONTROL 最初/最後を非表示]** — ユーザーが結果の最初または最後のページにジャンプしないようにするには、このオプションを選択します。
* **[!UICONTROL 前へ/次へを非表示]** — ユーザーが現在のページを基準にして結果ページを移動できるかどうかを指定します。
* **[!UICONTROL Hide view all]** — ユーザーが単一ページですべての検索結果を統合できるかどうかを指定します。 通常、ページ分割されたデータを提供するとサーバーのリソースをより効率的に使用できます。サイズの大きなデータセットを 1 つの応答メッセージで転送されないようにするには、このオプションを選択します。

## ファセットによる結果のフィルタリングの有効化 {#enabling-the-filtering-of-results-by-facets}

ユーザーが検索結果をファセットでフィルタリングできるように設定できます。The **[!UICONTROL Checkbox List Facet]**, **[!UICONTROL Dropdown Facet]**, and **[!UICONTROL Link List Facet]** components enable users to select one or more facets for filtering. これらのコンポーネントを使用する際には、**[!UICONTROL パンくず]**&#x200B;コンポーネントも指定することをお勧めします。パンくずは、現在使用されているフィルターを示します。

The **[!UICONTROL Checkbox List Facet**, **[!UICONTROL Dropdown Facet]**, and **[!UICONTROL Link List Facet]** components each have the following properties that you configure in **[!UICONTROL Edit]** mode:

* **[!UICONTROL Facet Name]** — フィルターに使用するファセットの名前。

**[!UICONTROL チェックボックスリストファセット]**&#x200B;コンポーネントにファセットのリストと関連するチェックボックスが表示されます。**[!UICONTROL チェックボックスリストファセット]**&#x200B;を使用して、ユーザーが複数のファセットからの項目が含まれる結果のサブセットを表示できるようにします。例えば、複数のブランドが同じ種類の製品を供給する場合は、ブランドファセットが適切です。

検索結果に関連付けられている各ファセットにチェックボックスが表示されます。ユーザーがチェックボックスをオンにすると、ページが再度読み込まれ、結果セットが更新されます。すべてのチェックボックスはページに表示されたままなので、ユーザーはいつでもフィルターに対してファセットを追加または削除できます。

![sandcheckboxcomp](assets/sandpcheckboxcomp.png)

**[!UICONTROL ドロップダウンファセット]**&#x200B;コンポーネントを使用すると、ユーザーがドロップダウンリストからファセット項目を選択できます。このコンポーネントは、一度に 1 つのファセットに絞り込む場合に便利です。例えば、商品検索を性別で絞り込む場合には部門ファセットが適切です。**&#x200B;ジーンズを探しているジョンが部門を「男性」でフィルター。

ドロップダウンリストには、すべての検索結果に関連付けられているファセットが入力されています。ドロップダウンリストで項目を選択すると、ページが再度読み込まれ、結果セットが更新されます。ドロップダウンリストの項目は変わらないので、ユーザーはいつでもファセットを切り替えることができます。

![sanddropdowndepartment](assets/sandpdropdowndepartment.png)

**[!UICONTROL リンクリストファセット]**&#x200B;コンポーネントを使用すると、ユーザーが複数のファセットメンバーまたはファセットで項目を段階的に絞り込むことができます。

ファセットメンバーはリンクのリストとして表示されます。各リンクのテキストは、現在の検索結果に関連付けられているファセットメンバーの名前です。ユーザーがファセットリンクをクリックすると、ページが再度読み込まれ、検索結果のサブセットが表示されます。リンクのリストはクリックに応じて更新され、結果をさらに絞り込むことができます。

![sandplinklistcomp](assets/sandplinklistcomp.png)

The links in the list also changes when a filter is applied from a different type of [!UICONTROL Search&amp;Promote] component. 複数の種類のフィルターコンポーネントを使用することで、フィルターを効果的に組み合わせることができます。

**[!UICONTROL パンくず]**&#x200B;コンポーネントを使用すると、ユーザーが検索結果に現在適用されているフィルターを、適用された順序で確認できます。パンくずの項目をクリックすることで、そのフィルターの組み合わせに戻すことができます。

![sandbreadcrumbcomp](assets/sandpbreadcrumbcomp.png)

編集モードで次のパンくずのプロパティを設定して、コンポーネントの外観をカスタマイズできます。

* **[!UICONTROL Delimiter]** — 各階層リンクの区切り文字として使用する文字または文字列を定義します。 Delimiterフィールドは、任意の文字列を入力として受け付けます。 デフォルトの設定は、&quot;>&quot;（引用符なし）です。
* **[!UICONTROL トレーリング区切り]** — パンくずリストの末尾に表示する文字または文字列を定義します。 「トレーリング区切り」フィールドは、任意の文字列を入力として受け付けます。 このデフォルト設定は「空白」です（階層リンクラインの末尾に何も表示されません）

## 検索ボックスの追加 {#adding-search-boxes}

The **[!UICONTROL Search]** component enables customers to perform keyword searches. 検索機能にアクセス権限を付与する各ページに検索コンポーネントを追加します。

Configure the following properties in **[!UICONTROL Edit]** mode to control runtime behavior:

* **[!UICONTROL Result Page Path]** — 検索結果を表示するページへのパス。
* **[!UICONTROL オートコンプリートを有効にする]** — 顧客が検索ボックスに入力し始めたときに推奨検索キーワードを表示させる場合に選択します。

![sandsearchcomp](assets/sandpsearchcomp.png)

## バナーの追加 {#adding-banners}

The **[!UICONTROL Banners]** component displays banner advertisements according to the customer&#39;s Search&amp;Promote searches. Search&amp;Replace サーバーのロジックにより表示されるバナーが決まります。例えば、「ジーンズ」を検索するとファッション関連のバナーが表示されます。「男性」部門でフィルタリングすると、バナーがさらに絞り込まれます。

The **[!UICONTROL Banners]** component provides one configurable property named **[!UICONTROL Banner Area]**. In **[!UICONTROL Edit]** mode, select one of the property values to specify how the banner appears. Search&amp;Promote サービスにより、値のリストの選択元が決まります。

## Search&amp;Promote 検索ページの例 {#example-search-promote-search-page}

この図は、下の完全に機能する Search&amp;Promote 結果ページを作成するためにページに追加されるコンポーネントを示します。

![1328213789109](assets/1328213789109.png)![sandppageexample](assets/sandppageexample.png)

