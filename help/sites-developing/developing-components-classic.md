---
title: AEM コンポーネントの開発（クラシック UI）
seo-title: Developing AEM Components (Classic UI)
description: クラシック UI では、ExtJS を使用して、コンポーネントのルックアンドフィールを提供するウィジェットを作成します。HTL は、AEM の推奨スクリプティング言語ではありません。
seo-description: The classic UI uses ExtJS to create widgets that provide the look-and-feel of the components. HTL is not the recommended scripting language for AEM.
uuid: ed53d7c6-5996-4892-81a4-4ac30df85f04
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: components
content-type: reference
discoiquuid: c68f724f-f9b3-4018-8d3a-1680c53d73f8
legacypath: /content/docs/en/aem/6-2/develop/components/components-classic
exl-id: 725e4f82-7019-4365-9c01-b5d95ea2a8fa
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '2391'
ht-degree: 73%

---

# AEM コンポーネントの開発（クラシック UI）{#developing-aem-components-classic-ui}

クラシック UI では、ExtJS を使用して、コンポーネントのルックアンドフィールを提供するウィジェットを作成します。このウィジェットの性質により、クラシック UI と[タッチ操作対応 UI](/help/sites-developing/developing-components.md) では、コンポーネントとのやり取りにいくつかの相違点があります。

>[!NOTE]
>
>コンポーネント開発の多くの側面は、クラシック UI とタッチ操作対応 UI の両方で共通なので、 **次を読む必要があります。 [AEMコンポーネント — 基本](/help/sites-developing/components-basics.md) 前** このページを使用して、クラシック UI の詳細を取り上げます。

>[!NOTE]
>
>クラシック UI 用のコンポーネントの開発には HTML テンプレート言語（HTL）と JSP のどちらも使用できますが、このページでは JSP を使用した開発について説明します。これは単に、クラシック UI 内では JSP が使用されてきたからです。
>
>現在では、HTL が AEM の推奨スクリプティング言語とされています。詳しくは、 [HTL](https://helpx.adobe.com/jp/experience-manager/htl/user-guide.html) および [AEM Components の開発](/help/sites-developing/developing-components.md) メソッドを比較します。

## 構造 {#structure}

コンポーネントの基本的な構造については、ページで説明します [AEMコンポーネント — 基本](/help/sites-developing/components-basics.md#structure)：タッチ操作対応 UI とクラシック UI の両方を適用します。 新しいコンポーネントでタッチ操作対応 UI の設定を使用する必要がない場合でも、この情報は既存のコンポーネントを継承する際に設定を把握するのに役立ちます。

## JSP スクリプト {#jsp-scripts}

コンポーネントをレンダリングするには JSP スクリプトまたはサーブレットを使用します。Sling のリクエスト処理規則に従って、デフォルトスクリプトの名前は、

`<*componentname*>.jsp`

## global.jsp {#global-jsp}

JSP スクリプトファイルの `global.jsp` は、コンポーネントのレンダリングに使用される任意の JSP スクリプトの特定オブジェクト（コンテンツ）にすばやくアクセスするために使用されます。

したがって、`global.jsp` で提供される 1 つ以上のオブジェクトを使用する場合は、JSP スクリプトをレンダリングするすべてのコンポーネントに `global.jsp` を含める必要があります。

デフォルトの `global.jsp` は次の場所にあります。

`/libs/foundation/global.jsp`

>[!NOTE]
>
>パス `/libs/wcm/global.jsp`は、CQ 5.3 以前のバージョンで使用されていましたが、現在は廃止されています。

### global.jsp、使用される API および Taglib の機能 {#function-of-global-jsp-used-apis-and-taglibs}

デフォルトの `global.jsp` から提供される最も重要なオブジェクトを次に示します。

概要:

* `<cq:defineObjects />`

   * `slingRequest`  — ラップされたリクエストオブジェクト ( `SlingHttpServletRequest`) をクリックします。
   * `slingResponse`  — ラップされた応答オブジェクト ( `SlingHttpServletResponse`) をクリックします。
   * `resource` - Sling Resource オブジェクト ( `slingRequest.getResource();`) をクリックします。
   * `resourceResolver` - Sling Resource Resolver オブジェクト ( `slingRequest.getResoucreResolver();`) をクリックします。
   * `currentNode` - リクエストに対して解決された JCR ノード。
   * `log`  — デフォルトのロガー ()。
   * `sling` - Sling スクリプトヘルパー。
   * `properties`  — 指定されたリソース ( `resource.adaptTo(ValueMap.class);`) をクリックします。
   * `pageProperties` - 指定されたリソースのページのプロパティ。
   * `pageManager` - AEMコンテンツページにアクセスするためのページマネージャー ( `resourceResolver.adaptTo(PageManager.class);`) をクリックします。
   * `component` - 現在の AEM コンポーネントのコンポーネントオブジェクト。
   * `designer`  — デザイン情報を取得するデザイナーオブジェクト ( `resourceResolver.adaptTo(Designer.class);`) をクリックします。
   * `currentDesign` - 指定されたリソースのデザイン。
   * `currentStyle` - 指定されたリソースのスタイル。

### コンテンツへのアクセス {#accessing-content}

AEM WCM のコンテンツにアクセスするには、3 つの方法があります。

* に示すプロパティオブジェクトを使用 `global.jsp`:

   properties オブジェクトは、ValueMap のインスタンス（[Sling API](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/resource/ValueMap.html) を参照）で、現在のリソースのプロパティがすべて含まれています。

   例： `String pageTitle = properties.get("jcr:title", "no title");` ページコンポーネントのレンダリングスクリプトで使用されます。

   例： `String paragraphTitle = properties.get("jcr:title", "no title");` 標準段落コンポーネントのレンダリングスクリプトで使用されます。

* を使用 `currentPage` ～に導入された物 `global.jsp`:

   この `currentPage` オブジェクトはページのインスタンスです ( [AEM API](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/Page.mhtml)) をクリックします。 ページクラスには、コンテンツにアクセスするためのメソッドがいくつかあります。

   例：`String pageTitle = currentPage.getTitle();`

* 経由 `currentNode` ～に導入された物 `global.jsp`:

   この `currentNode` オブジェクトは、ノードのインスタンスです ( [JCR API](https://jackrabbit.apache.org/api/2.16/org/apache/jackrabbit/standalone/cli/core/CurrentNode.html)) をクリックします。 ノードのプロパティには、 `getProperty()` メソッド。

   例：`String pageTitle = currentNode.getProperty("jcr:title");`

## JSP タグライブラリ {#jsp-tag-libraries}

CQ と Sling のタグライブラリを使用すると、テンプレートやコンポーネントの JSP スクリプトで使用する特定の機能にアクセスできます。

詳しくは、 [タグライブラリ](/help/sites-developing/taglib.md).

## クライアント側 HTML ライブラリの使用 {#using-client-side-html-libraries}

最近の Web サイトは、複雑な JavaScript や CSS コードを利用したクライアント側の処理に大きく依存しています。このコードの提供を編成および最適化することが厄介な問題となることがあります。

この問題に対処するために、AEMでは、 **クライアント側ライブラリフォルダー**：クライアント側コードをリポジトリに保存し、カテゴリに整理して、コードの各カテゴリをクライアントに提供するタイミングと方法を定義できます。 その後、クライアント側ライブラリシステムにより、最終的な Web ページで、正しいコードを読み込むための正しいリンクが作成されます。

ドキュメントを参照 [クライアント側HTMLライブラリの使用](/help/sites-developing/clientlibs.md) を参照してください。

## ダイアログ {#dialog}

コンポーネントのコンテンツを作成者が追加したり設定できるようにするには、ダイアログが必要です。

詳しくは、 [AEMコンポーネント — 基本](/help/sites-developing/components-basics.md#dialogs) 詳しくは、を参照してください。

## 編集動作の設定 {#configuring-the-edit-behavior}

コンポーネントの編集動作を設定できます。これには、コンポーネントに対して使用可能なアクションなどの属性、インプレースエディターの特性、コンポーネントに対するイベントに関連するリスナーも含まれます。固有の相違点は多少ありますが、設定はタッチ操作対応 UI とクラシック UI の両方に共通です。

この [コンポーネントの編集動作が設定されている](/help/sites-developing/components-basics.md#edit-behavior) を `cq:editConfig` タイプのノード `cq:EditConfig` コンポーネントノードの下 ( タイプ `cq:Component`) をクリックし、特定のプロパティと子ノードを追加します。

## ExtJS ウィジェットの使用と拡張 {#using-and-extending-extjs-widgets}

詳しくは、[ExtJS ウィジェットの使用と拡張](/help/sites-developing/widgets.md)を参照してください。

## ExtJS ウィジェットに xtype を使用 {#using-xtypes-for-extjs-widgets}

詳しくは、[xtype の使用](/help/sites-developing/xtypes.md)を参照してください。

## 新しいコンポーネントの開発 {#developing-new-components}

この節では、独自のコンポーネントを作成し、それを段落システムに追加する方法について説明します。

既存のコンポーネントをコピーし、必要な変更をおこなうことが、開発を始めるうえで最も簡単な方法です。

コンポーネントの開発方法の例について詳しくは、[テキストコンポーネントと画像コンポーネントの拡張 - 例](#extending-the-text-and-image-component-an-example)を参照してください。

### 新しいコンポーネントの開発（既存のコンポーネントの利用） {#develop-a-new-component-adapt-existing-component}

既存のコンポーネントをベースに新しい AEM コンポーネントを開発するには、既存のコンポーネントをコピーし、新しいコンポーネント用の JavaScript ファイルを作成して、AEM からアクセスできる場所に保存します（「[コンポーネントおよびその他の要素のカスタマイズ](/help/sites-developing/dev-guidelines-bestpractices.md#customizing-components-and-other-elements)」も参照してください）。

1. CRXDE Lite を使用して、新しいコンポーネントフォルダーを以下の場所に作成します。

   / `apps/<myProject>/components/<myComponent>`

   libs 内にあるものと同じノード構造を再作成してから、テキストコンポーネントなどの既存のコンポーネントの定義をコピーします。例えば、テキストコンポーネントをカスタマイズするには、次のようにコピーします。

   * コピー元：`/libs/foundation/components/text`
   * コピー先：`/apps/myProject/components/text`

1. を変更します。 `jcr:title` 新しい名前を反映させる
1. 新しいコンポーネントフォルダーを開き、必要な変更をおこないます。また、フォルダー内にある不要な情報を削除します。

   例えば、次のような変更をおこなうことができます。

   * ダイアログボックスへの新しいフィールドの追加

      * `cq:dialog`  — タッチ操作対応 UI 用のダイアログ
      * `dialog` - クラシック UI 用ダイアログ
   * の置き換え `.jsp` ファイル（新しいコンポーネントの後に名前を付けます）
   * または、コンポーネント全体の作成し直し（必要な場合）

   例えば、標準テキストコンポーネントのコピーを作成した場合、ダイアログボックスにフィールドを追加して、 `.jsp` 入力を処理するために。

   >[!NOTE]
   >
   >使用するコンポーネント：
   >
   >* タッチ操作対応 UI では [Granite](https://helpx.adobe.com/jp/experience-manager/6-4/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/index.html) コンポーネントを使用します。
   >* クラシック UI では [ExtJS ウィジェット](https://helpx.adobe.com/jp/experience-manager/6-4/sites/developing/using/reference-materials/widgets-api/index.html)を使用します。


   >[!NOTE]
   >
   >クラシック UI 用に定義したダイアログは、タッチ操作対応 UI 内で動作します。
   >
   >タッチ操作対応 UI 用に定義したダイアログは、クラシック UI 内では動作しません。
   >
   >インスタンスと作成環境によっては、コンポーネント用に両方のタイプのダイアログを定義する必要が生じる場合があります。

1. 新しいコンポーネントを表示するには、次のいずれかのノードが存在し、適切に初期化されている必要があります。

   * `cq:dialog`  — タッチ操作対応 UI 用のダイアログ
   * `dialog` - クラシック UI 用ダイアログ
   * `cq:editConfig` - 編集環境でのコンポーネントの動作（ドラッグ＆ドロップなど）
   * `design_dialog`  — デザインモード用のダイアログ（クラシック UI のみ）

1. 次のどちらかの方法で、段落システムで新しいコンポーネントを利用できるようにします。

   * CRXDE Liteを使用して値を追加 `<path-to-component>` ( 例： `/apps/geometrixx/components/myComponent`) をノードのプロパティコンポーネントに追加します。 `/etc/designs/geometrixx/jcr:content/contentpage/par`
   * 「[段落システムへの新しいコンポーネントの追加](#adding-a-new-component-to-the-paragraph-system-design-mode)」の手順を実行します。

1. AEM WCM で、Web サイトのページを開き、作成した新しいタイプの段落を挿入してコンポーネントが正常に動作することを確認します。

>[!NOTE]
>
>ページの読み込みのタイミング統計を確認するには、Ctrl + Shift + U — を `?debugClientLibs=true` を URL に設定します。

### 段落システムへの新しいコンポーネントの追加（デザインモード） {#adding-a-new-component-to-the-paragraph-system-design-mode}

コンポーネントを開発したら、段落システムに追加します。この操作により、ページの編集時に、作成者がコンポーネントを選択して使用できるようになります。

1. 例えば段落システムを使用するオーサリング環境内のページにアクセスする `<contentPath>/Test.html`.
1. 次のどちらかの方法でデザインモードに切り替えます。

   * 追加 `?wcmmode=design` を URL の末尾に追加して、再度アクセスする方法を示します。例：

      `<contextPath>/ Test.html?wcmmode=design`

   * サイドキックで「デザイン」をクリックします。

   デザインモードになり、段落システムを編集できるようになります。

1. 「編集」をクリックします。

   その段落システムに所属するコンポーネントのリストが一覧表示されます。新しいコンポーネントも一覧に表示されます。

   これらのコンポーネントをアクティブ化または非アクティブ化することで、ページの編集時に作成者に提供するコンポーネントを決定できます。

1. コンポーネントをアクティブ化したら、標準編集モードに戻り、利用可能かどうかを確認します。

### テキストコンポーネントと画像コンポーネントの拡張 - 例 {#extending-the-text-and-image-component-an-example}

この節では、広く利用されているテキストと画像の標準コンポーネントを、設定可能な画像配置機能を使用して拡張する方法について説明します。

テキストコンポーネントと画像コンポーネントの拡張により、エディターは、コンポーネントのすべての既存機能を使用できるだけでなく、次のどちらかの方法で画像の配置を指定できる追加のオプションも利用できます。

* テキストの左側（現在の動作および新しいデフォルト）
* テキストの右側

このコンポーネントを拡張したら、コンポーネントのダイアログボックスを使用して画像の配置を設定できます。

この演習では、以下の方法を説明します。

* 既存のコンポーネントノードのコピーとメタデータの変更
* コンポーネントのダイアログの変更（親ダイアログボックスからのウィジェットの継承を含む）
* 新機能を実装するためのコンポーネントのスクリプトの変更

>[!NOTE]
>
>この例は、クラシック UI を対象としています。

>[!NOTE]
>
>この例は、Geometrixx サンプルコンテンツに基づいています。これは、AEM に付属されなくなり、We.Retail に置き換えられました。ドキュメントを参照 [We.Retail 参照実装](/help/sites-developing/we-retail.md#we-retail-geometrixx) を参照してください。

#### 既存の textimage コンポーネントの拡張 {#extending-the-existing-textimage-component}

新しいコンポーネントを作成するには、標準の textimage コンポーネントを基礎として使用し、変更します。 ここでは、Geometrixx AEM WCM の例のアプリケーションに新しいコンポーネントを保存します。

1. 標準の textimage コンポーネントを `/libs/foundation/components/textimage` をGeometrixxコンポーネントフォルダーに追加する `/apps/geometrixx/components`（ターゲットノード名として textimage を使用） （コンポーネントに移動し、右クリックして「コピー」を選択し、ターゲットディレクトリに移動することでコンポーネントをコピーします）。

   ![chlimage_1-59](assets/chlimage_1-59.png)

1. この例ではシンプルに保つために、コピーしたコンポーネントに移動し、新しい textimage ノードから、以下に示すサブノードを除く、すべてのサブノードを削除します。

   * ダイアログ定義： `textimage/dialog`
   * コンポーネントスクリプト： `textimage/textimage.jsp`
   * 設定ノードを編集（アセットのドラッグ&amp;ドロップを許可）: `textimage/cq:editConfig`

   >[!NOTE]
   >
   >ダイアログの定義は、UI に依存します。
   >
   >* タッチ操作対応 UI: `textimage/cq:dialog`
   >* クラシック UI: `textimage/dialog`


1. コンポーネントのメタデータを編集します。

   * コンポーネント名

      * 設定 `jcr:description` から `Text Image Component (Extended)`
      * 設定 `jcr:title` から `Text Image (Extended)`
   * サイドキック内でコンポーネントが一覧表示されるグループ（修正しない）

      * 終了 `componentGroup` に設定 `General`
   * 新しいコンポーネントの親コンポーネント（標準の textimage コンポーネント）

      * 設定 `sling:resourceSuperType` から `foundation/components/textimage`

   この手順を終えると、コンポーネントのノードは以下のようになります。

   ![chlimage_1-60](assets/chlimage_1-60.png)

1. を `sling:resourceType` 画像の編集設定ノードのプロパティ ( プロパティ： `textimage/cq:editConfig/cq:dropTargets/image/parameters/sling:resourceType`) から `geometrixx/components/textimage.`

   これで、画像がページ上のコンポーネントにドロップされると、拡張された textimage コンポーネントの `sling:resourceType` プロパティが `geometrixx/components/textimage.` に設定されます。

1. コンポーネントのダイアログボックスを変更して新しいオプションを含めます。新しいコンポーネントは元のコンポーネントと同じダイアログボックスのパーツを継承します。「**詳細**」タブを拡張するために、「**左**」と「**右**」のオプションのある「**画像の位置**」ドロップダウンリストだけを追加します。

   * を `textimage/dialog`プロパティは変更されません。

   `textimage/dialog/items` に、textimage ダイアログボックスの 4 つのタブを表す 4 つのサブノード（tab1 から tab4）があることを確認します。

   * 最初の 2 つのタブ（tab1 および tab2）：

      * xtype を cqinclude に変更します（標準コンポーネントから継承するため）。
      * 値を持つパスプロパティを追加します。 `/libs/foundation/components/textimage/dialog/items/tab1.infinity.json`および `/libs/foundation/components/textimage/dialog/items/tab2.infinity.json`、それぞれ。
      * その他のすべてのプロパティとサブネットを削除します。
   * tab3：

      * プロパティとサブノードは変更せずに保持します。
      * 新しいフィールド定義をに追加 `tab3/items`，タイプのノード位置 `cq:Widget`
      * 新しい `tab3/items/position`ノード：

         * `name`: `./imagePosition`
         * `xtype`: `selection`
         * `fieldLabel`: `Image Position`
         * `type`: `select`
      * サブノードを追加 `position/options` タイプ `cq:WidgetCollection` 画像配置の 2 つの選択肢を表し、その下に 2 つのノード（タイプの o1 と o2）を作成します `nt:unstructured`.
      * ノードの場合 `position/options/o1` プロパティを設定します。 `text` から `Left` および `value` から `left.`
      * ノードの場合 `position/options/o2` プロパティを設定します。 `text` から `Right` および `value` から `right`.
   * tab4 を削除します。

   画像の位置は、`imagePosition` の段落を表すノードの `textimage` プロパティとしてコンテンツ内で保持されます。これらの手順を終えると、コンポーネントのダイアログボックスは以下のようになります。

   ![chlimage_1-61](assets/chlimage_1-61.png)

1. コンポーネントのスクリプト `textimage.jsp` を拡張し、新しいパラメーターの処理を追加します。

   ```xml
   Image image = new Image(resource, "image");
   
   if (image.hasContent() || WCMMode.fromRequest(request) == WCMMode.EDIT) {
        image.loadStyleData(currentStyle);
   ```

   強調表示したコードのフラグメント *%>&lt;div class=&quot;image&quot;>&lt;%* は、このタグのカスタムスタイルを生成する新しいコードで置き換える予定です。

   ```xml
   // todo: add new CSS class for the 'right image' instead of using 
   // the style attribute 
   String style="";
        if (properties.get("imagePosition", "left").equals("right")) { 
             style = "style=\"float:right\""; 
        } 
        %><div <%= style %> class="image"><%
   ```

1. コンポーネントをリポジトリに保存します。コンポーネントをテストする準備ができました。

#### 新しいコンポーネントの確認 {#checking-the-new-component}

コンポーネントを開発したら、段落システムに追加します。この操作により、ページの編集時に、作成者がコンポーネントを選択して使用できるようになります。コンポーネントをテストするには、以下の手順を実行します。

1. Geometrixx でページを開きます（例：English／Company）。
1. サイドキックで「デザイン」をクリックし、デザインモードに切り替えます。
1. ページの中央の段落システムで、「編集」をクリックし、段落システムのデザインを編集します。段落システムに配置できるコンポーネントの一覧が表示されます。一覧には、新しく開発した Text Image (Extended) コンポーネントも含まれます。コンポーネントを選択し、「OK」をクリックして、段落システムに対してコンポーネントをアクティブ化します。
1. 編集モードに戻します。
1. Text Image (Extended) 段落を段落システムに追加し、サンプルコンテンツでテキストと画像を初期化します。変更内容を保存します。
1. テキストと画像の段落のダイアログを開き、「詳細」タブで画像の位置を「右」に変更し、「OK」をクリックして変更を保存します。
1. 段落の右側に画像がレンダリングされます。
1. コンポーネントを使用する準備ができました。

コンポーネントには、Company ページの段落のコンテンツが格納されます。

### 画像コンポーネントのアップロード機能の無効化 {#disable-upload-capability-of-the-image-component}

この機能を無効にするには、標準の画像コンポーネントを基礎として使用し、それを変更します。 Geometrixx の例のアプリケーションに新しいコンポーネントを保存します。

1. 次の標準画像コンポーネントをコピーします。 `/libs/foundation/components/image` をGeometrixxコンポーネントフォルダーに追加する `/apps/geometrixx/components`（ターゲットノード名として画像を使用）

   ![chlimage_1-62](assets/chlimage_1-62.png)

1. コンポーネントのメタデータを編集します。

   * 設定 **jcr:title** から `Image (Extended)`

1. `/apps/geometrixx/components/image/dialog/items/image` に移動します。
1. 新しいプロパティを追加します。

   * **名前**：`allowUpload`
   * **型**：`String`
   * **値**: `false`

   ![chlimage_1-63](assets/chlimage_1-63.png)

1. 「**すべて保存**」をクリックします。コンポーネントをテストする準備ができました。
1. Geometrixx でページを開きます（例：English／Company）。
1. デザインモードに切り替え、Image (Extended) をアクティブ化します。
1. 編集モードに切り替え、画像を段落システムに追加します。次の画像で、元の画像コンポーネントと先ほど作成したコンポーネントの違いを確認できます。

   元の画像コンポーネント：

   ![chlimage_1-64](assets/chlimage_1-64.png)

   新しい画像コンポーネント：

   ![chlimage_1-65](assets/chlimage_1-65.png)

1. コンポーネントを使用する準備ができました。
