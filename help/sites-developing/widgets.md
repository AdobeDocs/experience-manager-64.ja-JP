---
title: ウィジェットの使用および拡張（クラシック UI）
seo-title: Using and Extending Widgets (Classic UI)
description: AEM の Web ベースインターフェイスでは、AJAX やその他の最新のブラウザー技術が使用されています。これらの技術により、作成者は、Web ページ上でコンテンツの WYSIWYG 編集や書式設定をおこなうことができます
seo-description: AEM's web-based interface uses AJAX and other modern browser technologies to enable WYSIWYG editing and formatting of content by authors right on the web page
uuid: e8dfa140-dab7-4e08-a790-d703adf86d6f
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: components
content-type: reference
discoiquuid: 508f4fab-dd87-4306-83ae-12e544b8b723
exl-id: c747bfda-e82a-4b2d-a4af-5792bfe82576
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '5151'
ht-degree: 59%

---

# ウィジェットの使用および拡張（クラシック UI）{#using-and-extending-widgets-classic-ui}

Adobe Experience Manager の Web ベースインターフェイスでは、AJAX やその他の最新のブラウザー技術が使用されています。これらの技術により、作成者は、Web ページ上でコンテンツの WYSIWYG 編集や書式設定を行うことができます。

Adobe Experience Manager（AEM）では、[ExtJS](https://www.sencha.com/) ウィジェットライブラリが使用されています。このライブラリのユーザーインターフェイス要素は、主要なすべてのブラウザーで動作するだけではなく、デスクトップクラスの UI の操作性も実現でき、非常に洗練されたものとなっています。

これらのウィジェットは AEM に組み込まれており、AEM 自体でも使用されていますが、AEM で作成したすべての Web サイトでも使用できます。

AEM で使用可能なすべてのウィジェットについて詳しくは、[ウィジェット API ドキュメント](https://helpx.adobe.com/jp/experience-manager/6-4/sites/developing/using/reference-materials/widgets-api/index.html)または[既存の xtype のリスト](/help/sites-developing/xtypes.md)を参照してください。また、ExtJS フレームワークを所有している [Sencha](https://www.sencha.com/products/extjs/examples/) のサイトには、ExtJS フレームワークの使用方法を示す例が多数掲載されています。

このページをご覧になると、ウィジェットを使用したり、拡張したりする方法についてのヒントが得られます。このページでは、最初に、[クライアント側コードをページに組み込む](#including-the-client-sided-code-in-a-page)方法が説明されています。次に、基本的な使用と拡張の方法を説明するために作成されたサンプルコンポーネントが示されています。これらのコンポーネントは、**パッケージ共有**&#x200B;の **Using ExtJS Widgets**&#x200B;パッケージで提供されています。

このパッケージには、次の例が含まれています。

* すぐに使用できるウィジェットで作成した[基本ダイアログ](#basic-dialogs)。
* すぐに使用できるウィジェットとカスタマイズ済みの Javascript ロジックで作成した[動的ダイアログ](#dynamic-dialogs)。
* [カスタムウィジェット](#custom-widgets)に基づくダイアログ。
* 特定のパスの下に JCR ツリーを表示する[ツリーパネル](#tree-overview)。
* 表形式でデータを表示する[グリッドパネル](#grid-overview)。

>[!NOTE]
>
>Adobe Experience Manager のクラシック UI は、[ExtJS 3.4.0](https://extjs.cachefly.net/ext-3.4.0/docs/) をベースに構築されています。

>[!NOTE]
>
>このページでは、クラシック UI でのウィジェットの使用について説明します。アドビでは、[Coral UI](/help/sites-developing/touch-ui-concepts.md#coral-ui) および [Granite UI](/help/sites-developing/touch-ui-concepts.md#granite-ui-foundation-components) をベースとした最新の[タッチ操作対応 UI](/help/sites-developing/touch-ui-concepts.md) の使用を推奨しています。

## クライアント側コードのページへの組み込み {#including-the-client-sided-code-in-a-page}

クライアント側の JavaScript とスタイルシートコードは、クライアントライブラリに配置する必要があります。

クライアントライブラリを作成するには：

1. 以下にノードを作成します。 `/apps/<project>` を次のプロパティと共に使用します。

   ```
       name="clientlib"
       jcr:mixinTypes="[mix:lockable]"
       jcr:primaryType="cq:ClientLibraryFolder" 
       sling:resourceType="widgets/clientlib" 
       categories="[<category-name>]" 
       dependencies="[cq.widgets]"
   ```

   >[!NOTE]
   >
   >注意： `<category-name>` はカスタムライブラリの名前です ( 例：&quot;cq.extjstraining&quot;) と呼ばれ、ページにライブラリを組み込むために使用されます。

1. 下 `clientlib` を作成します。 `css` および `js` フォルダー (nt:folder)。

1. 下 `clientlib` を作成します。 `css.txt` および `js.txt` ファイル (nt:files) これらの .txt ファイルには、ライブラリに組み込むファイルを記述します。

1. 編集 `js.txt`:「 」で始める必要があります `#base=js`&#39;の後に、CQ クライアントライブラリサービスによって集計されるファイルのリストが続きます。例：

   ```
   #base=js
    components.js
    exercises.js
    CustomWidget.js
    CustomBrowseField.js
    InsertTextPlugin.js
   ```

1. 編集 `css.txt`:「 」で始める必要があります `#base=css`&#39;の後に、CQ クライアントライブラリサービスによって集計されるファイルのリストが続きます。例：

   ```
   #base=css
    components.css
   ```

1. `js` フォルダーの下に、ライブラリに属する Javascript ファイルを配置します。

1. 以下の `css` フォルダーに、 `.css` css ファイルで使用されるファイルとリソース ( 例： `my_icon.png`) をクリックします。

>[!NOTE]
>
>前述のスタイルシートの処理は、必要に応じておこないます。

ページコンポーネント jsp にクライアントライブラリを組み込むには：

* Javascript コードとスタイルシートの両方を組み込むには：

   `<ui:includeClientLib categories="<category-name1>, <category-name2>, ..."/>`

   場所 `<category-nameX>` はクライアント側ライブラリの名前です。

* Javascript コードのみを組み込むには：

   `<ui:includeClientLib js="<category-name>"/>`

詳しくは、[&lt;ui:includeClientLib>](/help/sites-developing/taglib.md#amp-lt-ui-includeclientlib) タグの説明を参照してください。

クライアントライブラリは、オーサーモードでのみ使用可能にして、パブリッシュモードでは除外することが必要な場合があります。これをおこなうには、次のように設定します。

```xml
    if (WCMMode.fromRequest(request) != WCMMode.DISABLED) {
        %><ui:includeClientLib categories="cq.collab.blog"/><%
    }
```

### サンプルの使用 {#getting-started-with-the-samples}

このページのチュートリアルに従うには、 **ExtJS ウィジェットの使用** ローカルAEMインスタンスで、コンポーネントを組み込むサンプルページを作成します。 この作業を行うには、以下の手順を実行します。

1. AEMインスタンスで、という名前のパッケージをダウンロードします。 **ExtJS ウィジェット (v01) の使用** パッケージ共有から、パッケージをインストールします。 プロジェクトが作成されます `extjstraining` 下 `/apps` リポジトリ内に保存されます。

1. サンプルコンポーネントを **Geometrixx** ブランチ：

   in **CRXDE Lite** ファイルを開く `/apps/geometrixx/components/page/headlibs.jsp` をクリックし、 `cq.extjstraining` 既存の `<ui:includeClientLib>` タグの下に次のように記述します。

   `%><ui:includeClientLib categories="apps.geometrixx-main, cq.extjstraining"/><%`

1. で新しいページを作成します。 **Geometrixx** 下の分岐 `/content/geometrixx/en/products` そして、 **ExtJS ウィジェットの使用**.

1. デザインモードに切り替え、**Using ExtJS Widgets** という名前のグループのすべてのコンポーネントを Geometrixx のデザインに追加します。
1. 編集モードに戻ります。グループの構成要素 **ExtJS ウィジェットの使用** は、サイドキックで使用できます。

>[!NOTE]
>
>このページの例は、Geometrixx サンプルコンテンツに基づいています。これは現在、AEM には付属しておらず、We.Retail に置き換えられています。ドキュメントを参照 [We.Retail 参照実装](/help/sites-developing/we-retail.md#we-retail-geometrixx) を参照してください。

### 基本ダイアログ {#basic-dialogs}

通常、ダイアログは、コンテンツを編集するために使用されますが、情報の表示のみをおこなうこともできます。ダイアログを完全に表示する簡単な方法は、その JSON 形式の表現にアクセスすることです。これをおこなうには、ブラウザーで次のように指定します。

`http://localhost:4502/<path-to-dialog>.-1.json`

サイドキックにある **Using ExtJS Widgets** グループの最初のコンポーネントは、**1.Dialog Basics** という名前で、4 つの基本ダイアログが入っています。これらのダイアログは、すぐに使用できるウィジェットで作成されており、カスタマイズした Javascript ロジックは含まれていません。ダイアログは、以下に保存されます。 `/apps/extjstraining/components/dialogbasics`. 基本ダイアログを次に示します。

*  ダイアログ（`full`full ノード）：3 つのタブを持つウィンドウが表示されます。各タブには、2 つのテキストフィールドがあります。

* Single Panel ダイアログ（`singlepanel` ノード）：1 つのタブを持つウィンドウが表示されます。このタブには、2 つのテキストフィールドがあります。
* Multi Panel ダイアログ（`multipanel` ノード）：表示内容は Full ダイアログと同じですが、ダイアログの作成の仕方が異なります。
*  ダイアログ（`design`design ノード）：2 つのタブを持つウィンドウが表示されます。最初のタブには、テキストフィールド、ドロップダウンメニューおよび折り畳み可能なテキスト領域があります。2 番目のタブには、4 つのテキストフィールドを含むフィールドセットと、2 つのテキストフィールドを含む折り畳み可能なフィールドセットがあります。

次の手順に従って、**1.Dialog Basics** コンポーネントをサンプルページに組み込みます。

1. **1.ダイアログの基本** コンポーネントを **ExtJS ウィジェットの使用** 」タブをクリックします。 **サイドキック**.

1. このコンポーネントには、タイトル、テキストおよび&#x200B;**プロパティ**&#x200B;リンクが表示されます。リンクをクリックすると、リポジトリに保存されている段落のプロパティが表示されます。リンクをもう一度クリックすると、プロパティが非表示になります。

このコンポーネントは、次のように表示されます。

![chlimage_1-135](assets/chlimage_1-135.png)

#### 例 1：Full ダイアログ {#example-full-dialog}

**Full** ダイアログには、3 つのタブを持つウィンドウが表示されます。各タブには、2 つのテキストフィールドがあります。これは、**Dialog Basics** コンポーネントのデフォルトダイアログです。特性は次のとおりです。

* 次のノードで定義されます。ノードタイプ= `cq:Dialog`, xtype = [`dialog`](/help/sites-developing/xtypes.md#dialog).

* 3 つのタブが表示されます ( ノードタイプ= `cq:Panel`) をクリックします。
* 各タブには 2 つのテキストフィールドがあります ( ノードタイプ= `cq:Widget`, xtype = [`textfield`](/help/sites-developing/xtypes.md#textfield)) をクリックします。

* ノードによって定義されます：

   `/apps/extjstraining/components/dialogbasics/full`

* 次を要求することで、JSON 形式でレンダリングされます。

   `http://localhost:4502/apps/extjstraining/components/dialogbasics/full.-1.json`

このダイアログは、次のように表示されます。

![screen_shot_2012-01-31at45411pm](assets/screen_shot_2012-01-31at45411pm.png)

#### 例 2：Single Panel ダイアログ {#example-single-panel-dialog}

**Single Panel** ダイアログには、1 つのタブを持つウィンドウが表示されます。このタブには、2 つのテキストフィールドがあります。特性は次のとおりです。

* 1 つのタブが表示されます ( ノードタイプ= `cq:Dialog`, xtype = [`panel`](/help/sites-developing/xtypes.md#panel))

* タブには 2 つのテキストフィールドがあります ( ノードタイプ= `cq:Widget`, xtype = [`textfield`](/help/sites-developing/xtypes.md#textfield))

* ノードによって定義されます：

   `/apps/extjstraining/components/dialogbasics/singlepanel`

* 次を要求することにより、JSON 形式でレンダリングされます。

   `http://localhost:4502/apps/extjstraining/components/dialogbasics/singlepanel.-1.json`

* **Full ダイアログ**&#x200B;の利点の 1 つは、必要な設定が少ないことです。
* 推奨される用途：情報を表示するだけの、またはフィールドが数個しかない単純なダイアログ。

Single Panel ダイアログを使用するには：

1. **Dialog Basics** コンポーネントのダイアログを **Single Panel** ダイアログに置き換えます。

   1. In **CRXDE Lite**、ノードを削除します。 `/apps/extjstraining/components/dialogbasics/dialog`
   1. 「**すべて保存**」をクリックして変更を保存します。
   1. ノードをコピーします。 `/apps/extjstraining/components/dialogbasics/singlepanel`
   1. コピーしたノードを次の場所に貼り付けます。 `/apps/extjstraining/components/dialogbasics`
   1. ノードを選択します。 `/apps/extjstraining/components/dialogbasics/Copy of singlepanel`と名前を変更します。 `dialog`.

1. コンポーネントを編集します。次のようなダイアログが表示されます。

![screen_shot_2012-01-31at45952pm](assets/screen_shot_2012-01-31at45952pm.png)

#### 例 3：Multi Panel ダイアログ {#example-multi-panel-dialog}

**Multi Panel** ダイアログは、**Full** ダイアログと同じ表示内容ですが、ダイアログの作成の仕方が異なります。特性は次のとおりです。

* ノードによって定義されます (node type = `cq:Dialog`, xtype = [`tabpanel`](/help/sites-developing/xtypes.md#tabpanel)) をクリックします。

* 3 つのタブが表示されます ( ノードタイプ= `cq:Panel`) をクリックします。
* 各タブには 2 つのテキストフィールドがあります ( ノードタイプ= `cq:Widget`, xtype = [`textfield`](/help/sites-developing/xtypes.md#textfield)) をクリックします。

* ノードによって定義されます：

   `/apps/extjstraining/components/dialogbasics/multipanel`

* 次を要求することにより、JSON 形式でレンダリングされます。

   `http://localhost:4502/apps/extjstraining/components/dialogbasics/multipanel.-1.json`

* **Full ダイアログ**&#x200B;の利点の一つは、構造が簡単であることです。

* 推奨される用途：複数のタブを持つダイアログ。

マルチパネルダイアログを使用するには：

1. ダイアログを **ダイアログの基本** コンポーネント **マルチパネル** ダイアログ：

   以下の手順に従って、 [例 2:シングルパネルダイアログ](#example-single-panel-dialog)

1. コンポーネントを編集します。次のようなダイアログが表示されます。

![screen_shot_2012-01-31at50119pm](assets/screen_shot_2012-01-31at50119pm.png)

#### 例 4：Rich ダイアログ {#example-rich-dialog}

**Rich** ダイアログには、2 つのタブを持つウィンドウが表示されます。最初のタブには、テキストフィールド、ドロップダウンメニューおよび折り畳み可能なテキスト領域があります。2 番目のタブには、4 つのテキストフィールドを含むフィールドセットと、2 つのテキストフィールドを含む折り畳み可能なフィールドセットがあります。特性は次のとおりです。

* ノードによって定義されます (node type = `cq:Dialog`, xtype = [`dialog`](/help/sites-developing/xtypes.md#dialog)) をクリックします。

* 2 つのタブが表示されます ( ノードタイプ= `cq:Panel`) をクリックします。
* 最初のタブには [`dialogfieldset`](/help/sites-developing/xtypes.md#dialogfieldset) ウィジェット [`textfield`](/help/sites-developing/xtypes.md#textfield) および [`selection`](/help/sites-developing/xtypes.md#selection) 3 つのオプションを持つウィジェットと折りたたみ可能 [`dialogfieldset`](/help/sites-developing/xtypes.md#dialogfieldset) と [`textarea`](/help/sites-developing/xtypes.md#textarea) ウィジェット。

* 2 番目のタブには、 [`dialogfieldset`](/help/sites-developing/xtypes.md#dialogfieldset) 4 つのウィジェット [`textfield`](/help/sites-developing/xtypes.md#textfield) ウィジェットと折りたたみ可能 `dialogfieldset` 2 [`textfield`](/help/sites-developing/xtypes.md#textfield) ウィジェット。

* ノードによって定義されます：

   `/apps/extjstraining/components/dialogbasics/rich`

* 次を要求することにより、JSON 形式でレンダリングされます。

   `http://localhost:4502/apps/extjstraining/components/dialogbasics/rich.-1.json`

**Rich** ダイアログを使用するには：

1. ダイアログを **ダイアログの基本** コンポーネント **リッチ** ダイアログ：

   以下の手順に従って、 [例 2:シングルパネルダイアログ](#example-single-panel-dialog)

1. コンポーネントを編集します。次のようなダイアログが表示されます。

![screen_shot_2012-01-31at50429pm](assets/screen_shot_2012-01-31at50429pm.png) ![screen_shot_2012-01-31at50519pm](assets/screen_shot_2012-01-31at50519pm.png)

### Dynamic Dialogs {#dynamic-dialogs}

サイドキックにある **Using ExtJS Widgets** グループの 2 番目のコンポーネントは、**2.Dynamic Dialogs** という名前で、3 つの動的ダイアログが含まれています。これらのダイアログは、すぐに使用できるウィジェットと、**カスタマイズされた Javascript ロジック**&#x200B;から作成されています。ダイアログは、以下に保存されます。 `/apps/extjstraining/components/dynamicdialogs`. 動的ダイアログは次のとおりです。

* Switch Tabs ダイアログ（`switchtabs` ノード）：2 つのタブを持つウィンドウが表示されます。最初のタブでは、ラジオボタンにより、3 つのオプションのいずれかを選択できます。オプションを選択すると、選択したオプションに関連付けられているタブが表示されます。2 番目のタブには、2 つのテキストフィールドがあります。
*  ダイアログ（`arbitrary`arbitrary ノード）：1 つのタブを持つウィンドウが表示されます。このタブには、2 つのフィールドがあります。一つは、アセットをドロップまたはアップロードするためのフィールド、もう一つは、コンポーネントを含むページに関する情報とアセットに関する情報（アセットが参照されている場合）を表示するフィールドです。
* フィールドを切り替えダイアログ ( `togglefield` ノード ):1 つのタブを持つウィンドウが表示されます。 このタブには、1 つのチェックボックスがあります。このチェックボックスを選択すると、2 つのテキストフィールドを含むフィールドセットが表示されます。

を含めるには、 **2. Dynamic Dialogs** コンポーネントをサンプルページに組み込むには：

1. **2.  Dynamic Dialogs** コンポーネントをサンプルページに追加します（**サイドキック**&#x200B;にある「**Using ExtJS Widgets**」タブから）。

1. このコンポーネントには、タイトル、テキストおよび&#x200B;**プロパティ**&#x200B;リンクが表示されます。リンクをクリックすると、リポジトリに保存されている段落のプロパティが表示されます。リンクをもう一度クリックすると、プロパティが非表示になります。

このコンポーネントは、次のように表示されます。

![chlimage_1-136](assets/chlimage_1-136.png)

#### 例 1：Switch Tabs ダイアログ {#example-switch-tabs-dialog}

**Switch Tabs** ダイアログには、2 つのタブを持つウィンドウが表示されます。最初のタブでは、ラジオボタンにより、3 つのオプションのいずれかを選択できます。オプションを選択すると、選択したオプションに関連付けられているタブが表示されます。2 番目のタブには、2 つのテキストフィールドがあります。

このダイアログの主な特徴を次に示します。

* ノードによって定義されます (node type = `cq:Dialog`, xtype = [`dialog`](/help/sites-developing/xtypes.md#dialog)) をクリックします。

* 2 つのタブが表示されます ( ノードタイプ= `cq:Panel`):「1 選択」タブ、「2 番目のタブ」は、「1 番目のタブでの選択」（3 つのオプション）によって異なります。
* 3 つのオプションのタブがあります ( ノードタイプ= `cq:Panel`) の場合、それぞれに 2 つのテキストフィールドがあります ( ノードタイプ= `cq:Widget`, xtype = [`textfield`](/help/sites-developing/xtypes.md#textfield)) をクリックします。 「オプション」タブは、同時に 1 つしか表示されません。

* が `switchtabs` ノード：

   `/apps/extjstraining/components/dynamicdialogs/switchtabs`

* 次を要求することにより、JSON 形式でレンダリングされます。

   `http://localhost:4502/apps/extjstraining/components/dynamicdialogs/switchtabs.-1.json`

ロジックは、次のようにイベントリスナーと Javascript コードによって実装されています。

* ダイアログノードには、 `beforeshow`」ダイアログが表示される前に、すべてのオプションのタブを非表示にするリスナー：

   `beforeshow="function(dialog){Ejst.x2.manageTabs(dialog.items.get(0));}"`

   `dialog.items.get(0)` 選択パネルと 3 つのオプションパネルを含むタブパネルを取得します。

* この `Ejst.x2` オブジェクトが `exercises.js` ファイルの場所：

   `/apps/extjstraining/clientlib/js/exercises.js`

* 内 `Ejst.x2.manageTabs()` メソッド、 `index` が —1 の場合、すべてのオプションのタブは非表示になります (1 ～ 3)。

* 「選択範囲」タブには、2 つのリスナーがあります。一つは、ダイアログのロード（「`loadcontent`」イベント）時に選択済みのタブを表示するリスナー、もう一つは、選択内容の変更（「`selectionchanged`」イベント）時に選択済みのタブを表示するリスナーです。

   `loadcontent="function(field,rec,path){Ejst.x2.showTab(field);}"`

   `selectionchanged="function(field,value){Ejst.x2.showTab(field);}"`

* 内 `Ejst.x2.showTab()` メソッド：

   `field.findParentByType('tabpanel')` すべてのタブ ( `field` （選択ウィジェットを表します）

   `field.getValue()` 選択の値を取得します。例：tab2

   `Ejst.x2.manageTabs()` 選択したタブが表示されます。

* 各「オプション」タブには、「`render`」イベントでタブを非表示にするリスナーがあります。

   `render="function(tab){Ejst.x2.hideTab(tab);}"`

* 内 `Ejst.x2.hideTab()` メソッド：

   `tabPanel` は、すべてのタブを含むタブパネルです

   `index` はオプションタブのインデックスです

   `tabPanel.hideTabStripItem(index)` タブを非表示にします

次のように表示されます。

![screen_shot_2012-02-01at114745am](assets/screen_shot_2012-02-01at114745am.png)

#### 例 2：Arbitrary ダイアログ {#example-arbitrary-dialog}

ほとんどの場合、ダイアログには、基になるコンポーネントからのコンテンツが表示されます。ここで説明する **Arbitrary** ダイアログは、別のコンポーネントからコンテンツを取り込みます。

**Arbitrary** ダイアログには、1 つのタブを持つウィンドウが表示されます。このタブには、2 つのフィールドがあります。一つは、アセットをドロップまたはアップロードするためのフィールド、もう一つは、コンポーネントを含むページに関する情報とアセットに関する情報（アセットが参照されている場合）を表示するフィールドです。

このダイアログの主な特徴を次に示します。

* ノードによって定義されます (node type = `cq:Dialog`, xtype = [`dialog`](/help/sites-developing/xtypes.md#dialog)) をクリックします。

* 1 つのタブパネルウィジェットを表示します (node type = `cq:Widget`, xtype = [`tabpanel`](/help/sites-developing/xtypes.md#tabpanel)) を 1 つのパネル (node type = `cq:Panel`)

* パネルには smartfile ウィジェットがあります (node type = `cq:Widget`, xtype = [`smartfile`](/help/sites-developing/xtypes.md#smartfile)) と ownerdraw ウィジェット (node type = `cq:Widget`, xtype = [`ownerdraw`](/help/sites-developing/xtypes.md#ownerdraw))

* が `arbitrary` ノード：

   `/apps/extjstraining/components/dynamicdialogs/arbitrary`

* 次を要求することにより、JSON 形式でレンダリングされます。

   `http://localhost:4502/apps/extjstraining/components/dynamicdialogs/arbitrary.-1.json`

ロジックは、次のようにイベントリスナーと Javascript コードによって実装されています。

* ownerdraw ウィジェットには `loadcontent`&quot;コンテンツの読み込み時に、コンポーネントを含むページと smartfile ウィジェットが参照するアセットに関する情報を表示するリスナー：

   `loadcontent="function(field,rec,path){Ejst.x2.showInfo(field,rec,path);}"`

   `field` は ownerdraw オブジェクトで設定されます。

   `path` はコンポーネントのコンテンツパスで設定されます ( 例：/content/geometrixx/en/products/triangle/ui-tutorial/jcr:content/par/dynamicdialogs)

* この `Ejst.x2` オブジェクトが `exercises.js` ファイルの場所：

   `/apps/extjstraining/clientlib/js/exercises.js`

* 内 `Ejst.x2.showInfo()` メソッド：

   `pagePath` は、コンポーネントを含むページのパスです

   `pageInfo` は、ページプロパティを json 形式で表します。

   `reference` は参照元のアセットのパスです

   `metadata` アセットのメタデータを json 形式で表します

   `ownerdraw.getEl().update(html);` 作成した html がダイアログに表示されます

**Arbitrary** ダイアログを使用するには：

1. ダイアログを **動的ダイアログ** コンポーネント **任意** ダイアログ：

   以下の手順に従って、 [例 2:シングルパネルダイアログ](#example-single-panel-dialog)

1. コンポーネントを編集します。次のようなダイアログが表示されます。

![screen_shot_2012-02-01at115300am](assets/screen_shot_2012-02-01at115300am.png)

#### 例 3：Toggle Fields ダイアログ {#example-toggle-fields-dialog}

**Toggle Fields** ダイアログには、1 つのタブを持つウィンドウが表示されます。このタブには、1 つのチェックボックスがあります。このチェックボックスを選択すると、2 つのテキストフィールドを含むフィールドセットが表示されます。

このダイアログの主な特徴を次に示します。

* ノードによって定義されます (node type = `cq:Dialog`, xtype = [`dialog`](/help/sites-developing/xtypes.md#dialog)) をクリックします。

* 1 つのタブパネルウィジェットを表示します (node type = `cq:Widget`, xtype = [`tabpanel`](/help/sites-developing/xtypes.md#textpanel)) を 1 つのパネル (node type = `cq:Panel`) をクリックします。

* パネルには、選択/チェックボックスウィジェット (node type = `cq:Widget`, xtype = [`selection`](/help/sites-developing/xtypes.md#selection), type = [`checkbox`](/help/sites-developing/xtypes.md#checkbox)) と折りたたみ可能な dialogfieldset ウィジェット ( ノードタイプ= `cq:Widget`, xtype = [`dialogfieldset`](/help/sites-developing/xtypes.md#dialogfieldset)) 内に表示されます。デフォルトでは非表示になり、2 つの textfield ウィジェット (node type = `cq:Widget`, xtype = [`textfield`](/help/sites-developing/xtypes.md#textfield)) をクリックします。

* が `togglefields` ノード：

   `/apps/extjstraining/components/dynamicdialogs/togglefields`

* 次を要求することにより、JSON 形式でレンダリングされます。

   `http://localhost:4502/apps/extjstraining/components/dynamicdialogs/togglefields.-1.json`

ロジックは、次のようにイベントリスナーと Javascript コードによって実装されています。

* 「選択」タブには、2 つのリスナーがあります。コンテンツの読み込み時に dialogfieldset を表示するもの (&quot; `loadcontent`&quot;イベント ) と、選択が変更されたときに dialogfieldset を表示するもの (&quot; `selectionchanged`&quot;イベント ):

   `loadcontent="function(field,rec,path){Ejst.x2.toggleFieldSet(field);}"`

   `selectionchanged="function(field,value){Ejst.x2.toggleFieldSet(field);}"`

* この `Ejst.x2` オブジェクトが `exercises.js` ファイルの場所：

   `/apps/extjstraining/clientlib/js/exercises.js`

* 内 `Ejst.x2.toggleFieldSet()` メソッド：

   * `box` は選択オブジェクトです
   * `panel` は、選択および dialogfieldset ウィジェットを含むパネルです
   * `fieldSet` は dialogfieldset オブジェクトです。
   * `show` は選択範囲の値です（true または false）
   * 「 」に基づく `show`&#39; dialogfieldset が表示されているかどうか

次の手順で **フィールドを切り替え** ダイアログ：

1. ダイアログを **動的ダイアログ** コンポーネント **フィールドを切り替え** ダイアログ：

   以下の手順に従って、 [例 2:シングルパネルダイアログ](#example-single-panel-dialog)

1. コンポーネントを編集します。次のようなダイアログが表示されます。

![screen_shot_2012-02-01at115518am](assets/screen_shot_2012-02-01at115518am.png)

### カスタムウィジェット {#custom-widgets}

AEM に付属しているすぐに使用できるウィジェットは、ほとんどのケースに対応できます。ただし、プロジェクト固有の要件をカバーするカスタムウィジェットの作成が必要になる場合があります。 カスタムウィジェットは、既存のウィジェットを拡張して作成できます。こうしたカスタマイズをおこなう際の手助けとなるように、**Using ExtJS Widgets** パッケージには、3 つの異なるカスタムウィジェットを使用する 3 つのダイアログが含まれています。

* Multi Field ダイアログ（`multifield` ノード）。1 つのタブを持つウィンドウが表示されます。このタブには、カスタマイズされた multifield ウィジェットがあり、2 つのオプションを選択できるドロップダウンメニューとテキストフィールドという 2 つのフィールドが含まれています。このタブは、すぐに使用できる `multifield` ウィジェット（テキストフィールドのみを持つ）に基づいているので、`multifield` ウィジェットの機能をすべて使用できます。

* Tree Browse ダイアログ（`treebrowse` ノード）。このダイアログに表示されるウィンドウには、パス参照ウィジェットを含む 1 つのタブがあります。このウィジェットで矢印をクリックすると、ウィンドウが開き、階層を参照しながら項目を選択できます。項目を選択すると、そのパスがパスフィールドに追加され、ダイアログを閉じても保持され続けます。
* リッチテキストエディタープラグインベースのダイアログ（`rteplugin` ノード）。リッチテキストエディターにカスタムボタンを追加したもので、メインテキストにカスタムテキストを挿入できます。`richtext` ウィジェット（RTE）と、RTE プラグインメカニズムを通じて追加されたカスタム機能から構成されています。

カスタムウィジェットとプラグインは、**3.Custom Widgets**（**Using ExtJS Widgets** パッケージに属する）という名前のコンポーネントに含まれています。このコンポーネントをサンプルページに組み込むには：

1. **3.  Custom Widgets** コンポーネントをサンプルページに追加します（**サイドキック**&#x200B;にある「**Using ExtJS Widgets**」タブから）。

1. このコンポーネントには、タイトルとテキストが表示されます。また、**プロパティ**&#x200B;リンクをクリックすると、リポジトリに保存されている段落のプロパティも表示されます。リンクをもう一度クリックすると、プロパティが非表示になります。

   このコンポーネントは、次のように表示されます。

![chlimage_1-137](assets/chlimage_1-137.png)

#### 例 1：Custom Multifield ウィジェット {#example-custom-multifield-widget}

**Custom Multifield** ウィジェットベースのダイアログには、1 つのタブを持つウィンドウが表示されます。このタブには、カスタマイズされた multifield ウィジェットがあります。標準の multifield ウィジェットには 1 つのフィールドがありますが、このウィジェットには、2 つのオプションを選択できるドロップダウンメニューとテキストフィールドという 2 つのフィールドがあります。

**Custom Multifield** ウィジェットベースのダイアログ：

* ノードによって定義されます (node type = `cq:Dialog`, xtype = [`dialog`](/help/sites-developing/xtypes.md#dialog)) をクリックします。

* 1 つのタブパネルウィジェットを表示します (node type = `cq:Widget`, xtype = [`tabpanel`](/help/sites-developing/xtypes.md#tabpanel)) にパネルが含まれている ( ノードタイプ= `cq:Widget`, xtype = [`panel`](/help/sites-developing/xtypes.md#panel)) をクリックします。

* パネルには `multifield` widget ( ノードタイプ= `cq:Widget`, xtype = [`multifield`](/help/sites-developing/xtypes.md#multifield)) をクリックします。

* この `multifield` ウィジェットには fieldconfig があります ( ノードタイプ= `nt:unstructured`, xtype = `ejstcustom`, optionsProvider = `Ejst.x3.provideOptions`) を返します。 `ejstcustom`&#39;:

   * &#39; `fieldconfig`&#39;は、 [`CQ.form.MultiField`](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.MultiField) オブジェクト。
   * &#39; `optionsProvider`&#39;は `ejstcustom` ウィジェット。 これは、 `Ejst.x3.provideOptions` 次で定義されるメソッド： `exercises.js` 時刻：

      `/apps/extjstraining/clientlib/js/exercises.js`

      とは、2 つのオプションを返します。

* が `multifield` ノード：

   `/apps/extjstraining/components/customwidgets/multifield`

* 次を要求することにより、JSON 形式でレンダリングされます。

   `http://localhost:4502/apps/extjstraining/components/customwidgets/multifield.-1.json`

Custom Multifield ウィジェット（xtype = `ejstcustom`）：

* `Ejst.CustomWidget` という名前の Javascript オブジェクトです。

* 次の場所にある `CustomWidget.js` Javascript ファイルで定義されます。

   `/apps/extjstraining/clientlib/js/CustomWidget.js`

* を [`CQ.form.CompositeField`](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.CompositeField) ウィジェット。

* 次の 3 つのフィールドがあります。 `hiddenField` （テキストフィールド）、 `allowField` (ComboBox) および `otherField` （テキストフィールド）

* 上書き `CQ.Ext.Component#initComponent` 3 つのフィールドを追加するには：

   * `allowField` は [CQ.form.Selection](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.Selection) 「select」型のオブジェクト。 optionsProvider は、ダイアログで定義された CustomWidget の optionsProvider 設定でインスタンス化される Selection オブジェクトの設定です
   * `otherField` は、[CQ.Ext.form.TextField](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.TextField) オブジェクトです。

* メソッドを上書き `setValue`, `getValue` および `getRawValue` / [CQ.form.CompositeField](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.CompositeField) 次の形式で CustomWidget の値を設定して取得するには：

   `<allowField value>/<otherField value>, e.g.: 'Bla1/hello'`

* 自身を&#39;として登録 `ejstcustom`&#39; xtype:

   `CQ.Ext.reg('ejstcustom', Ejst.CustomWidget);`

**Custom Multifield** ウィジェットベースのダイアログは、次のように表示されます。

![screen_shot_2012-02-01at115840am](assets/screen_shot_2012-02-01at115840am.png)

#### 例 2：カスタム Treebrowse ウィジェット {#example-custom-treebrowse-widget}

カスタム **Treebrowse** ウィジェットベースのダイアログには、1 つのタブを持つウィンドウが表示されます。このタブには、カスタムパス参照ウィジェットが含まれています。このウィジェットで矢印をクリックすると、ウィンドウが開き、階層を参照しながら項目を選択できます。項目を選択すると、そのパスがパスフィールドに追加され、ダイアログを閉じても保持され続けます。

カスタム treebrowse ダイアログ：

* ノードによって定義されます (node type = `cq:Dialog`, xtype = [`dialog`](/help/sites-developing/xtypes.md#dialog)) をクリックします。

* 1 つのタブパネルウィジェットを表示します (node type = `cq:Widget`, xtype = [`tabpanel`](/help/sites-developing/xtypes.md#tabpanel)) にパネルが含まれている ( ノードタイプ= `cq:Widget`, xtype = [`panel`](/help/sites-developing/xtypes.md#panel)) をクリックします。

* このパネルにはカスタムウィジェットがあります (node type = `cq:Widget`, xtype = `ejstbrowse`)

* が `treebrowse` ノード：

   `/apps/extjstraining/components/customwidgets/treebrowse`

* 次を要求することにより、JSON 形式でレンダリングされます。

   `http://localhost:4502/apps/extjstraining/components/customwidgets/treebrowse.-1.json`

カスタム treebrowse ウィジェット（xtype = `ejstbrowse`）：

* `Ejst.CustomWidget` という名前の Javascript オブジェクトです。
* 次の場所にある `CustomBrowseField.js` Javascript ファイルで定義されます。

   `/apps/extjstraining/clientlib/js/CustomBrowseField.js`

* 拡張 [`CQ.Ext.form.TriggerField`](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.TriggerField).
* `browseWindow` という名前の参照ウィンドウを定義します。

* 上書き [`CQ.Ext.form.TriggerField`](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.TriggerField#onTriggerClick) をクリックすると、参照ウィンドウが表示されます。
* を定義します。 [`CQ.Ext.tree.TreePanel`](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.tree.TreePanel) オブジェクト：

   * データを取得するには、に登録されているサーブレットを呼び出します。 `/bin/wcm/siteadmin/tree.json`.
   * そのルートは「」です。 `apps/extjstraining`&quot;.

* を定義します。 `window` オブジェクト ([`CQ.Ext.Window`](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Window)):

   * 事前定義済みのパネルに基づいています。
   * 選択されたパスの値を設定し、パネルを非表示にする「**OK**」ボタンを組み込みます。

* ウィンドウは、「**パス**」フィールドの下に固定されます。
* 選択されたパスは、`show` イベントが発生したときに、参照フィールドからウィンドウに渡されます。

* 自身を&#39;として登録 `ejstbrowse`&#39; xtype:

   `CQ.Ext.reg('ejstbrowse', Ejst.CustomBrowseField);`

次の手順で **Custom Treebrowse** ウィジェットベースのダイアログ：

1. ダイアログを **カスタムウィジェット** コンポーネント **Custom Treebrowse** ダイアログ：

   以下の手順に従って、 [例 2:シングルパネルダイアログ](#example-single-panel-dialog)

1. コンポーネントを編集します。次のようなダイアログが表示されます。

![screen_shot_2012-02-01at120104pm](assets/screen_shot_2012-02-01at120104pm.png)

#### 例 3：リッチテキストエディター（RTE）プラグイン {#example-rich-text-editor-rte-plug-in}

**リッチテキストエディター（RTE）プラグイン**&#x200B;ベースのダイアログは、大括弧内にカスタムテキストを挿入するためのカスタムボタンがあるリッチテキストエディターベースのダイアログです。カスタムテキストをサーバー側ロジックで解析し、例えば、特定のパスで定義されたテキストを追加することができます（この例では、サーバー側ロジックは実装されていません）。

**RTE プラグイン**&#x200B;ベースのダイアログ：

* 次の場所にある rteplugin ノードによって定義されます。

   `/apps/extjstraining/components/customwidgets/rteplugin`

* 次を要求することにより、JSON 形式でレンダリングされます。

   `http://localhost:4502/apps/extjstraining/components/customwidgets/rteplugin.-1.json`

* この `rtePlugins` ノードに子ノードがあります `inserttext` ( ノードタイプ= `nt:unstructured`) を呼び出します。 このノードには、RTE で使用可能なプラグイン機能を定義する `features` という名前のプロパティがあります。

RTE プラグイン：

* `Ejst.InsertTextPlugin` という名前の Javascript オブジェクトです。

* 次の場所にある `InsertTextPlugin.js` Javascript ファイルで定義されます。

   `/apps/extjstraining/clientlib/js/InsertTextPlugin.js`

* を [`CQ.form.rte.plugins.Plugin`](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.Plugin) オブジェクト。
* 次のメソッドは、[`CQ.form.rte.plugins.Plugin`](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.Plugin) オブジェクトを定義するもので、プラグインの実装時に上書きされます。

   * `getFeatures()` プラグインが使用可能にするすべての機能の配列を返します。
   * `initializeUI()` を使用すると、RTE ツールバーに新しいボタンが追加されます。
   * `notifyPluginConfig()` ボタンにマウスポインターを置くと、タイトルとテキストが表示されます。
   * `execute()` が呼び出され、次のプラグインアクションが実行されます。含めるテキストを定義するウィンドウが表示されます。

* `insertText()` 対応するダイアログオブジェクトを使用してテキストを挿入します。 `Ejst.InsertTextPlugin.Dialog` （後で参照）。

* `executeInsertText()` が `apply()` ダイアログのメソッド。 **OK** 」ボタンがクリックされたときに表示されます。

* 自身を&#39;として登録 `inserttext`&#39;プラグイン：

   `CQ.form.rte.plugins.PluginRegistry.register("inserttext", Ejst.InsertTextPlugin);`

* `Ejst.InsertTextPlugin.Dialog` オブジェクトは、プラグインのボタンがクリックされたときに開くダイアログを定義します。このダイアログは、1 つのパネル、1 つのフォーム、1 つのテキストフィールドおよび 2 つのボタン（「**OK**」と「**キャンセル**」）から構成されます。

**リッチテキストエディター（RTE）プラグイン**&#x200B;ベースのダイアログを使用するには：

1. ダイアログを **カスタムウィジェット** コンポーネント **リッチテキストエディター (RTE) プラグイン** ベースダイアログ：

   以下の手順に従って、 [例 2:シングルパネルダイアログ](#example-single-panel-dialog)

1. コンポーネントを編集します。
1. 右側の最後のアイコン（4 つの矢印の付いたアイコン）をクリックします。 パスを入力して「**OK**」をクリックします。

   パスは角括弧 (`[]`) をクリックします。

1. 「**OK**」をクリックしてリッチテキストエディターを閉じます。

**リッチテキストエディター（RTE）プラグイン**&#x200B;ベースのダイアログは、次のように表示されます。

![screen_shot_2012-02-01at120254pm](assets/screen_shot_2012-02-01at120254pm.png)

>[!NOTE]
>
>この例は、ロジックのクライアント側の部分の実装方法を示しています。プレースホルダ (*[テキスト]*) をサーバー側で明示的に解析する必要があります（例：コンポーネント JSP 内）。

### Tree Overview {#tree-overview}

すぐに使用できる [`CQ.Ext.tree.TreePanel`](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.tree.TreePanel) オブジェクトは、ツリー構造のデータをツリー構造 UI として表示できます。**Using ExtJS Widgets** パッケージに含まれている Tree Overview コンポーネントを見ると、`TreePanel` オブジェクトを使用して特定のパスの下に JCR ツリーを表示する方法がわかります。このウィンドウ自体は、ドッキングすることも、ドッキング解除することもできます。この例の場合、ウィンドウのロジックは、コンポーネント jsp の &lt;script> タグと &lt;/script> タグの間に埋め込まれています。

**Tree Overview** コンポーネントをサンプルページに組み込むには：

1. **4.  Tree Overview** コンポーネントをサンプルページに追加します（**サイドキック**&#x200B;にある「**Using ExtJS Widgets**」タブで）。

1. このコンポーネントには、次のものが表示されます。

   * タイトルとテキスト
   * **プロパティ**&#x200B;リンク。クリックすると、リポジトリに保存されている段落のプロパティが表示されます。リンクをもう一度クリックすると、プロパティが非表示になります。
   * リポジトリをツリーで表現した浮動ウィンドウ。このツリーは展開可能です。

このコンポーネントは、次のように表示されます。

![screen_shot_2012-02-01at120639pm](assets/screen_shot_2012-02-01at120639pm.png)

Tree Overview コンポーネント：

* 次で定義されます。

   `/apps/extjstraining/components/treeoverview`

* このコンポーネントのダイアログでは、ウィンドウサイズの設定やウィンドウのドッキング、ドッキング解除が可能です（以下を参照）。

コンポーネント jsp：

* リポジトリから幅、高さ、ドッキングの各プロパティを取得します。
* ツリー概要のデータ形式に関するテキストを表示します。
* ウィンドウのロジックをコンポーネント jsp の Javascript タグの間に埋め込みます。
* 次で定義されます。

   `apps/extjstraining/components/treeoverview/content.jsp`

コンポーネント jsp に埋め込まれた Javascript コード：

* ページからツリーウィンドウの取得を試みることにより、`tree` オブジェクトを定義します。

* ツリーを表示するウィンドウが存在しない場合は、 `treePanel` ([CQ.Ext.tree.TreePanel](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.tree.TreePanel)) が作成されました。

   * `treePanel` には、ウィンドウの作成に使用されるデータが含まれています。
   * データは、次で登録されたサーブレットを呼び出すことにより、取得されます。
      `/bin/wcm/siteadmin/tree.json`

* この `beforeload` リスナーは、クリックされたノードが読み込まれていることを確認します。
* この `root` オブジェクトはパスを設定します `apps/extjstraining` を、木の根元として。
* `tree` ([`CQ.Ext.Window`](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Window)) は、事前定義された `treePanel`、およびは次の情報と共に表示されます。

   `tree.show();`

* ウィンドウが既に存在する場合、ウィンドウは、リポジトリから取得した幅、高さ、ドッキングの各プロパティに基づいて表示されます。

コンポーネントダイアログ：

* ツリー概要ウィンドウのサイズ（幅と高さ）を設定するための 2 つのフィールドとウィンドウをドッキング、ドッキング解除するための 1 つのフィールドを持つ 1 つのタブを表示します。
* ノードによって定義されます (node type = `cq:Dialog`, xtype = [`panel`](/help/sites-developing/xtypes.md#panel)) をクリックします。

* このパネルには sizefield ウィジェットがあります (node type = `cq:Widget`, xtype = [`sizefield`](/help/sites-developing/xtypes.md#sizefield)) と選択ウィジェット (node type = `cq:Widget`, xtype = [`selection`](/help/sites-developing/xtypes.md#selection), type = `radio`) に 2 つのオプション (true/false) を含める

* 次の場所にある dialog ノードによって定義されます。

   `/apps/extjstraining/components/treeoverview/dialog`

* 次を要求することにより、JSON 形式でレンダリングされます。

   `http://localhost:4502/apps/extjstraining/components/treeoverview/dialog.-1.json`

* 次のように表示されます。

![screen_shot_2012-02-01at120745pm](assets/screen_shot_2012-02-01at120745pm.png)

### Grid Overview {#grid-overview}

グリッドパネルには、データが行と列の表形式で表示されます。このパネルは、次の内容から構成されています。

* ストア：データレコード（行）を保持しているモデル。
* 列モデル：列の構成。
* ビュー：ユーザーインターフェイスが含まれます。
* 選択モデル：選択の動作。

Grid Overview コンポーネントには、 **ExtJS ウィジェットの使用** パッケージでは、データを表形式で表示する方法を示します。

* 例 1 では、静的データを使用しています。
* 例 2 では、リポジトリから取得したデータを使用します。

Grid Overview コンポーネントをサンプルページに含めるには：

1. **5.  Grid Overview** コンポーネントをサンプルページに追加します（**サイドキック**&#x200B;にある「**Using ExtJS Widgets**」タブで）。

1. このコンポーネントには、次のものが表示されます。

   * タイトルとテキスト
   * **プロパティ**&#x200B;リンク。クリックすると、リポジトリに保存されている段落のプロパティが表示されます。リンクをもう一度クリックすると、プロパティが非表示になります。
   * 表形式のデータを含む浮動ウィンドウ。

このコンポーネントは、次のように表示されます。

![screen_shot_2012-02-01at121109pm](assets/screen_shot_2012-02-01at121109pm.png)

#### 例 1：デフォルトグリッド {#example-default-grid}

すぐに使用できるバージョンの場合、**Grid Overview** コンポーネントには、静的データが表形式で含まれているウィンドウが表示されます。この例の場合、ロジックは、コンポーネント jsp に 次の 2 つの方法で埋め込まれます。

* 一般的なロジックは、&lt;script> タグと &lt;/script> タグの間に定義されます。
* 特定のロジックは、個別の .js ファイルで用意され、jsp にリンクされます。このような設定であるので、&lt;script> タグを必要に応じてコメント化すれば、2 つのロジック（静的／動的）を簡単に切り替えることができます。

Grid Overview コンポーネント：

* 次で定義されます。

   `/apps/extjstraining/components/gridoverview`

* このコンポーネントのダイアログでは、ウィンドウサイズの設定やウィンドウのドッキング、ドッキング解除が可能です。

コンポーネント jsp：

* リポジトリから幅、高さ、ドッキングの各プロパティを取得します。
* グリッド概要のデータ形式の紹介としてテキストを表示します。
* GridPanel オブジェクトを定義する Javascript コードを参照します。

   `<script type="text/javascript" src="/apps/extjstraining/components/gridoverview/defaultgrid.js"></script>`

   `defaultgrid.js` では、一部の静的データを GridPanel オブジェクトの基礎として定義します。

* GridPanel オブジェクトを使用する Window オブジェクトを Javascript コードで定義して、Javascript タグの間に埋め込みます。
* 次で定義されます。

   `apps/extjstraining/components/gridoverview/content.jsp`

コンポーネント jsp に埋め込まれた Javascript コード：

* ページからウィンドウコンポーネントの取得を試みることにより、`grid` オブジェクトを定義します。

   `var grid = CQ.Ext.getCmp("<%= node.getName() %>-grid");`

* If `grid` が存在しない場合、 [CQ.Ext.grid.GridPanel](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.GridPanel) オブジェクト ( `gridPanel`) は、 `getGridPanel()` メソッドを使用します（以下を参照）。 このメソッドは、`defaultgrid.js` で定義されます。

* `grid` は [`CQ.Ext.Window`](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Window)オブジェクト（事前定義済みの GridPanel に基づく）を選択し、次の操作を実行して表示します。 `grid.show();`

* If `grid` 既に存在する場合は、リポジトリから取得した幅、高さ、ドッキングの各プロパティに基づいて表示されます。

JavaScript ファイル ( `defaultgrid.js`) をコンポーネント jsp で参照する場合は、 `getGridPanel()` メソッド。JSP に埋め込まれたスクリプトによって呼び出され、 [`CQ.Ext.grid.GridPanel`](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.GridPanel) オブジェクトに作成します。 ロジックを次に示します。

* `myData` は、静的データの配列で、5 列 x 4 行の表として書式設定されています。
* `store` は `CQ.Ext.data.Store` を消費するオブジェクト `myData`.

* `store` はメモリに読み込まれます：

   `store.load();`

* `gridPanel` は [`CQ.Ext.grid.GridPanel`](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.GridPanel) を消費するオブジェクト `store`:

   * 列幅は常に再調整されます。

      `forceFit: true`

   * 選択できる行は一度に 1 つのみです。

      `singleSelect:true`

#### 例 2：参照検索グリッド {#example-reference-search-grid}

パッケージをインストールすると、 `content.jsp` の **グリッドの概要** コンポーネントは、静的データに基づくグリッドを表示します。 次の特徴を持つグリッドを表示するようにコンポーネントを変更することが可能です。

* 3 つの列を持つ。
* サーブレットを呼び出すことにより、リポジトリから取得したデータを基礎にする。
* 最後の列のセルを編集できる。この値は、先頭の列に表示されたパスで定義されたノードの下にある `test` プロパティに保持されます。

前の節で説明したように、window オブジェクトは、 [`CQ.Ext.grid.GridPanel`](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.GridPanel) オブジェクトを `getGridPanel()` メソッドが `defaultgrid.js` ～にファイルを送る `/apps/extjstraining/components/gridoverview/defaultgrid.js`. この **グリッドの概要** コンポーネントは、 `getGridPanel()` メソッド ( `referencesearch.js` ～にファイルを送る `/apps/extjstraining/components/gridoverview/referencesearch.js`. コンポーネント jsp で参照される .js ファイルを切り替えることにより、グリッドは、リポジトリから取得したデータに基づくようになります。

コンポーネント jsp で参照される .js ファイルを切り替えます。

1. **CRXDE Lite** で、コンポーネントの `content.jsp` ファイル内にある `defaultgrid.js` ファイルを含む行をコメント化します。次のようになります。

   `<!-- script type="text/javascript" src="/apps/extjstraining/components/gridoverview/defaultgrid.js"></script-->`

1. `referencesearch.js` ファイルを含む行からコメントを削除します。次のようになります。

   `<script type="text/javascript" src="/apps/extjstraining/components/gridoverview/referencesearch.js"></script>`

1. 変更内容を保存します。
1. サンプルページを更新します。

このコンポーネントは、次のように表示されます。

![screen_shot_2012-02-01at121429pm](assets/screen_shot_2012-02-01at121429pm.png)

コンポーネント jsp で参照される JavaScript コード (`referencesearch.js`) は、 `getGridPanel()` メソッドは、コンポーネント jsp から呼び出され、 [`CQ.Ext.grid.GridPanel`](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.GridPanel) オブジェクトに格納されます。 `referencesearch.js` のロジックでは、一部の動的データが GridPanel の基礎として定義されています。

* `reader` は、JSON 形式のサーブレット応答を読み取る 3 列用の [`CQ.Ext.data.JsonReader`](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.JsonReader) オブジェクトです。

* `cm` は [`CQ.Ext.grid.ColumnModel`](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.ColumnModel) 3 列のオブジェクト。

   「テスト」列のセルは、editor で定義されているので、編集することが可能です。

   `editor: new `[`CQ.Ext.form.TextField`](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.TextField)`({})`

* 列は並べ替え可能です。

   `cm.defaultSortable = true;`

* `store` は [`CQ.Ext.data.GroupingStore`](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.GroupingStore) オブジェクト：

   * データを取得するには、「 」に登録されているサーブレットを呼び出します。 `/bin/querybuilder.json`」を追加します。
   * 前に定義した `reader` に基づきます。
   * 表は、「**jcr:path**」列に従って、昇順で並べ替えられます。

* `gridPanel` は [`CQ.Ext.grid.EditorGridPanel`](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.EditorGridPanel) 編集可能なオブジェクト：

   * 事前定義済みの `store` と列モデル `cm` に基づいています。
   * 選択できる行は一度に 1 つのみです。

      `sm: new `[`CQ.Ext.grid.RowSelectionModel`](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.RowSelectionModel)`({singleSelect:true})`

   * `afteredit` リスナーは、「**テスト**」列のセルが編集されたことを確認します。

      * プロパティ&#39; `test`&#39; &#39;**jcr:path**」列がリポジトリに設定され、セルの値が
      * POST が成功した場合は、値が `store` オブジェクトに追加されます。POST が失敗した場合は、値が拒否されます。
