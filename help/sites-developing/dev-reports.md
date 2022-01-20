---
title: レポートの開発
seo-title: Developing Reports
description: AEM には、レポートフレームワークに基づく様々な標準レポートが用意されています。
seo-description: AEM provides a selection of standard reports based on a reporting framework
uuid: 1b406d15-bd77-4531-84c0-377dbff5cab2
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: 50fafc64-d462-4386-93af-ce360588d294
exl-id: 837c79af-a50f-40bb-b60d-205e1cac3f39
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '5238'
ht-degree: 48%

---

# レポートの開発{#developing-reports}

AEMは、 [標準レポート](/help/sites-administering/reporting.md) そのほとんどはレポートフレームワークに基づいています。

このフレームワークを使用して、これらの標準レポートを拡張することも、まったく新規のレポートを独自に開発することもできます。レポートフレームワークは、既存の CQ5 の概念や原則と緊密に統合されているので、開発者は、CQ5 に関する既存の知識を、レポートの開発の出発点として使用できます。

AEMで配信される標準レポートの場合：

* これらのレポートは、次のレポートフレームワークに基づいて構築されます。

   * [コンポーネントのレポート](/help/sites-administering/reporting.md#component-report)
   * [ページアクティビティレポート](/help/sites-administering/reporting.md#page-activity-report)
   * [ユーザーレポート](/help/sites-administering/reporting.md#user-report)
   * [ワークフローインスタンスレポート](/help/sites-administering/reporting.md#workflow-instance-report)

* 次のレポートは、個々の原則に基づいているので、拡張できません。

   * [ディスク使用量](/help/sites-administering/reporting.md#disk-usage)
   * [ヘルスチェック](/help/sites-administering/reporting.md#health-check)
   * [ワークフローレポート](/help/sites-administering/reporting.md#workflow-report)

>[!NOTE]
>
>[独自のレポートの作成 - 例](#creating-your-own-report-an-example)のチュートリアルでも、以下で説明する原理のうち使用できるものを示しています。
>
>標準レポートを参照し、他の実装例を確認することもできます。

>[!NOTE]
>
>以下の例と定義では、次の表記が使用されています。
>
>* 各行は、次の場所にあるノードまたはプロパティを定義します。
>
>  * `N:<name> [<nodeType>]`

   > 
   >     という名前のノードを表します。 `<*name*>` およびのノードタイプ `<*nodeType*>`*.*
>
>  * `P:<name> [<propertyType]`
   >
   >     という名前のプロパティを記述します。 `<*name*>` およびのプロパティタイプ `<*propertyType*>`.
>
>  * `P:<name> = <value>`
   >
   >     プロパティを記述します `<name>` を `<value>`.
>
>* インデントは、ノード間の階層的依存関係を示します。
>* 次で区切られた項目 |は可能な項目のリストを示します。例えば、型や名前は次のようになります。

>
>  例： `String|String[]` は、プロパティが String または String のいずれかであることを示します。[].
>
>* `[]` は配列を示し、例：文字列[] または、 [クエリ定義](#query-definition).
>
>特に指定のない限り、デフォルトのタイプは次のようになります。
>
>* ノード数 - `nt:unstructured`
>* プロパティ - `String`


## レポートフレームワーク {#reporting-framework}

レポートフレームワークは、次のような原理で使用されます。

* CQ5 QueryBuilder が実行するクエリによって返される結果セットに、完全に基づいています。
* 結果セットは、レポートに表示するデータを定義します。 結果セットの各行は、レポートの表形式ビューの行に対応します。
* 結果セットの実行に使用できる操作は、RDBMS の概念に似ています。主に *グループ化* および *集計*.

* データの取得と処理は、ほとんどサーバー側でおこなわれます。
* クライアントは、事前に処理されたデータの表示のみをおこないます。 小規模な処理タスク（セルコンテンツ内のリンクの作成など）のみがクライアント側で実行されます。

レポートフレームワーク（標準レポートの構造で示される）は、次の構成要素を使用し、処理キューによって送信されます。

![chlimage_1-248](assets/chlimage_1-248.png)

### レポートページ {#report-page}

レポートページ：

* 標準の CQ5 ページです。
* [レポート用に設定された CQ5 の標準テンプレート](#report-template)に基づいています。

### レポートベース {#report-base}

[`reportbase` コンポーネント](#report-base-component)は、次のようにすべてのレポートの基礎となるものです。

* 基になる結果セットのデータを提供する[クエリ](#the-query-and-data-retrieval)の定義を保持します。

* すべての列を含む、適応した段落システムです ( `columnbase`) がレポートに追加されました。
* 使用可能なチャートタイプおよび現在アクティブなチャートタイプを定義します。
* 編集ダイアログを定義します。このダイアログでは、レポートの特定の側面を設定できます。

### 列ベース {#column-base}

各列は、 [ `columnbase` コンポーネント](#column-base-component) 次の内容：

* は parsys ( `reportbase`) に含まれます。
* リンク先の [基になる結果セット](#the-query-and-data-retrieval);つまり、この結果セット内で参照される特定のデータと、その処理方法を定義します。
* 追加の定義を保持します。例えば、使用可能な集計やフィルターをデフォルト値と共に使用できます。

### クエリとデータの取得 {#the-query-and-data-retrieval}

クエリの概要は次のとおりです。

* [`reportbase`](#report-base) コンポーネントの一部として定義されます。
* [CQ QueryBuilder](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/javadoc/com/day/cq/search/QueryBuilder.html) に基づいています。
* レポートの基準として使用されるデータを取得します。 結果セット（テーブル）の各行が、ノードに 1 つずつ関連付けられ、クエリから返されます。特定の情報： [個々の列](#column-base-component) がこのデータセットから抽出されます。

* 通常、次のデータから構成されます。

   * ルートパス。

      これにより、検索対象とするリポジトリのサブツリーが指定されます。

      パフォーマンスの低下を最小限にするため、クエリの対象をリポジトリの特定のサブツリーになるべく制限することをお勧めします。このルートパスは、[レポートテンプレート](#report-template)で事前定義するか、または[設定（編集）ダイアログ](#configuration-dialog)でユーザーが設定することができます。

   * [1 つ以上の条件](#query-definition)。

      これらは、（最初の）結果セットの生成時に適用されます。ノードタイプの制限や、プロパティの制限などがあります。

**重要な点は、クエリの結果セットに返されるノードを 1 つ使用して、レポートの行が 1 つ生成される（ノードと行は 1 対 1 の関係にある）ことです。**

開発者は、レポートに対して定義したクエリによって、そのレポートに適切なノードセットが返されることを確認する必要があります。ただし、ノード自体に必要な情報をすべて保持する必要はありません。親ノードや子ノードから派生させることもできます。 例えば、[ユーザーレポート](/help/sites-administering/reporting.md#user-report)で使用されるクエリでは、ノードタイプ（この場合は `rep:user`）に基づいてノードが選択されます。ただし、このレポートのほとんどの列は、これらのノードから直接データを取り出すのではなく、子ノードからデータを取り出します `profile`.

### 処理キュー {#processing-queue}

[クエリ](#the-query-and-data-retrieval)によって返される結果セットのデータが、レポート上で行として表示されます。結果セットの各行は、（サーバー側の）[いくつかのフェーズ](#phases-of-the-processing-queue)で処理をおこなってから、クライアントに転送され、レポートに表示されます。

次のような操作が可能です。

* 基になる結果セットからの複数の値の抽出や取得。

   例えば、2 つのプロパティ値の差を計算することで、その 2 つの値を 1 つの値として処理できます。

* 抽出した値の解決。様々な方法でおこなうことができます。

   例えば、パスをタイトル（対応する *jcr:title* プロパティの、わかりやすいコンテンツ）にマップできます。

* 様々なポイントでフィルターを適用する。
* 必要に応じて、複合値を作成します。

   例えば、ユーザーに表示されるテキストから、値を作成してソートに使用したり、追加の URL を作成して（クライアント側で）リンクの作成に使用したりできます。

#### 処理キューのワークフロー {#workflow-of-the-processing-queue}

処理キューのワークフローを以下に示します。

![chlimage_1-249](assets/chlimage_1-249.png)

#### 処理キューのフェーズ {#phases-of-the-processing-queue}

具体的な手順と要素は次のとおりです。

1. が返す結果を変換します [初期クエリ (reportbase)](#query-definition) を、値抽出を使用して基本の結果セットに追加します。

   値抽出は、[列のタイプ](#column-specific-definitions)によって自動的に選択されます。値抽出を使用して、基になる JCR クエリから値を読み取り、その値から結果セットを作成し、その後の処理で適用できるようにします。例えば、 `diff` 値抽出では、2 つのプロパティが読み取られ、結果セットに追加される単一の値が計算されます。 値抽出を設定できません。

1. 生データを含むこの初期結果セットに、[初期フィルター](#column-specific-definitions)（*raw* フェーズ）が適用されます。

1. *apply* フェーズの定義に従い、値が[前処理](#processing-queue)されます。

1. 前処理された値に対して、[フィルタリング](#column-specific-definitions)（*preprocessed* フェーズに割り当てられています）が実行されます。

1. [指定されたリゾルバー](#processing-queue)によって、値が解決されます。
1. 解決された値に対して、[フィルタリング](#column-specific-definitions)（*resolved* フェーズに割り当てられています）が実行されます。

1. データは [グループ化および集計](#column-specific-definitions).
1. 配列データは、 （文字列ベースの）リストに変換することで解決されます。

   この手順は、複数の値を持つ結果をリストに変換して表示できるようにする暗黙の手順です。複数の値を持つ JCR プロパティに基づいた（集計されていない）セル値が必要です。

1. 値が再び [前処理済み](#processing-queue);定義された *afterApply* フェーズ。

1. データが並べ替えられます。
1. 処理されたデータはクライアントに転送されます。

>[!NOTE]
>
>基になるデータの結果セットを返す初期クエリは、`reportbase` コンポーネントで定義されます。
>
>処理キューの他の要素は、 `columnbase` コンポーネント。

## レポートの構成と設定 {#report-construction-and-configuration}

レポートの構成および設定には、次の要素が必要です。

* [独自のレポートコンポーネントの定義で使用する場所](#location-of-report-components)
* a [ `reportbase` コンポーネント](#report-base-component)
* 1 つ以上の [`columnbase` コンポーネント](#column-base-component)
* [ページコンポーネント](#page-component)
* [レポートデザイン](#report-design)
* [レポートテンプレート](#report-template)

### レポートコンポーネントの場所 {#location-of-report-components}

デフォルトのレポートコンポーネントは、の下に保持されます。 `/libs/cq/reporting/components`.

ただし、これらのノードは更新しないで、以下に独自のコンポーネントノードを作成することを強くお勧めします。 `/apps/cq/reporting/components` またはより適切な場合 `/apps/<yourProject>/reports/components`.

定義（例）は次のとおりです。

```
N:apps 
    N:cq [nt:folder]
        N:reporting|reports [sling:Folder]
            N:components [sling:Folder]
```

この下にレポートのルートを作成し、このルート下にレポートベースコンポーネントおよび列ベースコンポーネントを作成します。

```
N:apps 
    N:cq [nt:folder]
        N:reporting|reports [sling:Folder]
            N:components [sling:Folder]
                N:<reportname> [sling:Folder]
                        N:<reportname> [cq:Component]  // report base component
                        N:<columnname> [cq:Component]  // column base component
```

### ページコンポーネント  {#page-component}

レポートページでは、 `sling:resourceType` / `/libs/cq/reporting/components/reportpage`.

ページコンポーネントのカスタマイズは、（ほとんどの場合）必要ありません。

## レポートベースコンポーネント {#report-base-component}

各レポートタイプには、 `/libs/cq/reporting/components/reportbase`.

このコンポーネントは、レポート全体のコンテナとして使用され、次の情報が含まれます。

* [クエリ定義](#query-definition)。
* レポート設定用の[（オプションの）ダイアログ](#configuration-dialog)。
* レポートに組み込まれる[チャート](#chart-definitions)。

```
N:<reportname> [cq:Component]
    P:sling:resourceSuperType = "cq/reporting/components/reportbase"
    N:charting
    N:dialog [cq:Dialog]
    N:queryBuilder
```

### クエリ定義 {#query-definition}

```xml
N:queryBuilder
    N:propertyConstraints
    [
        N:<name> // array of nodes (name irrelevant), each with the following properties:
            P:name
            P:value
    ]
    P:nodeTypes [String|String[]] 
    P:mandatoryProperties [String|String[]
  ]
```

* `propertyConstraints`

   特定のプロパティと値を持つノードのみを結果セットに含める場合に使用できます。複数の制限が指定された場合、含まれるノードはこれらすべての制限を満たす（AND 演算による）必要があります。

   次に例を示します。

   ```
   N:propertyConstraints
    [
    N:0
    P:sling:resourceType
    P:foundation/components/textimage
    N:1
    P:jcr:modifiedBy
    P:admin
    ]
   ```

   すべての `textimage` 最後に変更されたコンポーネント `admin` ユーザー。

* `nodeTypes`

   指定したノードタイプのみを結果セットに含める場合に使用します。複数のノードタイプを指定できます。

* `mandatoryProperties`

   指定したプロパティをすべて持つノードのみを結果セットに含める場合に使用できます。**&#x200B;プロパティの値は考慮されません。

すべてはオプションで、必要に応じて組み合わせることができますが、少なくとも 1 つを定義する必要があります。

### チャート定義 {#chart-definitions}

```xml
N:charting
    N:settings
        N:active [cq:WidgetCollection]
        [
            N:<name> // array of nodes, each with the following property
                P:id   // must match the id of a child node of definitions 
        ]
    N:definitions [cq:WidgetCollection]
    [
        N:<name> // array of nodes, each with the following properties
            P:id
            P:type
            // additional, chart type specific configurations
    ]
```

* `settings`

   アクティブなグラフの定義を保持します。

   * `active`

      複数の設定を定義できるので、これを使用して現在アクティブなノードを定義できます。これらはノードの配列によって定義されます ( これらのノードには必須の命名規則はありませんが、標準レポートでは通常、 `0`, `1`... `x`) に分類され、それぞれが次のプロパティを持ちます。

      * `id`

         アクティブなグラフの ID。 チャート定義（`definitions`）のいずれかのチャートの ID に一致する必要があります。

* `definitions`

   レポートでの使用が可能なチャートタイプを定義します。`definitions` のうち使用されるタイプが、`active` で指定されます。

   定義は、ノードの配列を使用して指定します（同じ名前を付けることが多い）。 `0`, `1`... `x`) に分類され、それぞれに次のプロパティがあります。

   * `id`

      グラフ ID。

   * `type`

      使用可能なグラフのタイプ。 次から選択：

      * `pie`円グラフ。現在のデータのみから生成されます。

      * `lineseries`線系列（実際のスナップショットを表す点をつないだもの）履歴データからのみ生成されます。
   * グラフのタイプに応じて、追加のプロパティを使用できます。

      * グラフのタイプ `pie`:

         * `maxRadius`（`Double/Long`）

            この円グラフで許容される半径の最大値、つまりこのチャートで許容される最大サイズ（凡例を使用しない場合）。次の場合は無視 `fixedRadius` が定義されている。

         * `minRadius`（`Double/Long`）

            円グラフに使用できる最小半径です。 次の場合は無視 `fixedRadius` が定義されている。

         * `fixedRadius` ( `Double/Long`) 円グラフの固定半径を定義します。
      * グラフのタイプ [`lineseries`](/help/sites-administering/reporting.md#display-limits):

         * `totals`（`Boolean`）

            True を指定すると、 **合計** が表示される必要があります。
default: `false`

         * `series`（`Long`）

            表示する行数/系列数。
デフォルト：`9`（この値は許容される最大値です）

         * `hoverLimit`（`Long`）

            ポップアップを表示する最大の集計スナップショット（各水平線に表示され、個別の値を表すドット）の数。つまり、ユーザーがグラフの凡例の個別の値または対応するラベルにマウスポインターを置いたときに表示されます。

            デフォルト：`35`（現在のチャート設定で適用される個別の値が 35 個を超える場合は、ポップアップが表示されません）。

            このほかに、同時表示できるポップアップ数（凡例のテキストにマウスオーバーしたときに表示できる複数のポップアップ）を 10 個までに制限できます。



### 設定ダイアログ {#configuration-dialog}

各レポートには設定ダイアログを設定でき、ユーザーはレポートの様々なパラメーターを指定できます。 このダイアログには、 **編集** 」ボタンをクリックします。

このダイアログは標準の CQ です [ダイアログ](/help/sites-developing/components-basics.md#dialogs) また、 [CQ.Dialog](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Dialog) を参照 )。

ダイアログの例を次に示します。

```xml
<?xml version="1.0" encoding="UTF-8"?>
<jcr:root xmlns:cq="https://www.day.com/jcr/cq/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0"
    jcr:primaryType="cq:Dialog"
    height="{Long}424">
    <items jcr:primaryType="cq:WidgetCollection">
        <props jcr:primaryType="cq:Panel">
            <items jcr:primaryType="cq:WidgetCollection">
                <title
                    jcr:primaryType="cq:Widget"
                    path="/libs/cq/reporting/components/commons/title.infinity.json"
                    xtype="cqinclude"/>
                <description
                    jcr:primaryType="cq:Widget"
                    path="/libs/cq/reporting/components/commons/description.infinity.json"
                    xtype="cqinclude"/>
                <rootPath
                    jcr:primaryType="cq:Widget"
                    fieldLabel="Root path"
                    name="./report/rootPath"
                    rootPath=""
                    rootTitle="Repository root"
                    xtype="pathfield"/>
                <processing
                    jcr:primaryType="cq:Widget"
                    path="/libs/cq/reporting/components/commons/processing.infinity.json"
                    xtype="cqinclude"/>
                <scheduling
                    jcr:primaryType="cq:Widget"
                    path="/libs/cq/reporting/components/commons/scheduling.infinity.json"
                    xtype="cqinclude"/>
            </items>
        </props>
    </items>
</jcr:root>
```

いくつかの事前設定されたコンポーネントを使用できます。`xtype` プロパティに値 `cqinclude` を指定して、これらのコンポーネントをダイアログで参照できます。

* **`title`**

   `/libs/cq/reporting/components/commons/title`

   レポートタイトルを定義するテキストフィールド。

* **`description`**

   `/libs/cq/reporting/components/commons/description`

   レポートの説明を定義するテキスト領域。

* **`processing`**

   `/libs/cq/reporting/components/commons/processing`

   レポートの処理モード用のセレクター（手動/自動）。

* **`scheduling`**

   `/libs/cq/reporting/components/commons/scheduling`

   履歴グラフのスナップショットをスケジュールするためのセレクター。

>[!NOTE]
>
>参照されるコンポーネントは、 `.infinity.json` サフィックス（上記の例を参照）

### ルートパス {#root-path}

このほか、レポートのルートパスを指定することもできます。

* **`rootPath`**

   レポートの対象を、リポジトリの特定のセクション（ツリーまたはサブツリー）に限定できます。パフォーマンスの最適化のために、限定することをお勧めします。このルートパスは、各レポートページの `rootPath` ノードの `report` プロパティで指定します（ページの作成時、テンプレートから取得されます）。

   次の方法で指定できます。

   * の [レポートテンプレート](#report-template) （固定値または設定ダイアログのデフォルト値として）。
   * ユーザー（このパラメーターを使用）

## 列ベースコンポーネント {#column-base-component}

各列タイプには、 `/libs/cq/reporting/components/columnbase`.

列コンポーネントは、次の組み合わせを定義します。

* [列固有のクエリ](#column-specific-query)の設定。
* [リゾルバーと前処理](#resolvers-and-preprocessing)。
* [列固有の定義](#column-specific-definitions)（フィルターや集計など。`definitions` の子ノード）。
* [列のデフォルト値](#column-default-values)。
* サーバーによって返されるデータから、表示する情報を抽出するための[クライアントフィルター](#client-filter)。
* 以上のほか、列コンポーネントの `cq:editConfig` で適切なインスタンスを指定し、必要な[イベントとアクション](#events-and-actions)を指定する必要があります。
* [一般列](#generic-columns)の設定。

```
N:<columnname> [cq:Component]
    P:componentGroup
    P:jcr:title
    P:sling:resourceSuperType = "cq/reporting/components/columnbase"
    N:cq:editConfig [cq:EditConfig] // <a href="#events-and-actions">Events and Actions</a>
    N:defaults // <a href="#column-default-values">Column Default Values</a>
    N:definitions
      N:queryBuilder // <a href="#column-specific-query">Column Specific Query</a>
        P:property [String|String[]] // Column Specific Query
        P:subPath // Column Specific Query
        P:secondaryProperty [String|String[]] // Column Specific Query
        P:secondarySubPath // Column Specific Query
      N:data
        P:clientFilter [String] // <a href="#client-filter">Client Filter</a>
        P:resolver // <a href="#resolvers-and-preprocessing">Resolvers and Preprocessing</a>
        N:resolverConfig // Resolvers and Preprocessing
        N:preprocessing // Resolvers and Preprocessing
      P:type // <a href="#column-specific-definitions">Column Specific Definitions</a>
      P:groupable [Boolean] // Column Specific Definitions
      N:filters [cq:WidgetCollection] // Column Specific Definitions
      N:aggregates [cq:WidgetCollection] // Column Specific Definitions
```

[新規レポートの定義](#defining-your-new-report)も参照してください。

### 列固有のクエリ {#column-specific-query}

個別の列で使用する特定のデータを（[レポートデータの結果セット](#the-query-and-data-retrieval)から）抽出する方法を定義します。

```xml
N:definitions 
    N:queryBuilder
        P:property [String|String[]] 
        P:subPath
        P:secondaryProperty [String|String[]]
        P:secondarySubPath
```

* `property`

   セルの実値の計算に使用するプロパティを指定します。

   プロパティが String として定義されている場合[] 複数のプロパティが（順に）スキャンされ、実際の値が見つかります。

   例えば、次の場合です。

   `property = [ "jcr:lastModified", "jcr:created" ]`

   対応する値抽出（ここで制御している）は、次のようになります。

   * 有効な jcr:lastModified プロパティが存在するかどうかを確認し、存在する場合はそのプロパティを使用します。
   * 使用可能な jcr:lastModified プロパティがない場合は、代わりに jcr:created の内容が使用されます。

* `subPath`

   クエリによって返されるノードに結果を配置しない場合、このプロパティを実際に配置する場所を `subPath` で指定します。

* `secondaryProperty`

   セルの実値の計算に必要な、2 つ目のプロパティを定義します。このプロパティは、特定の列のタイプ（diff および sortable）でのみ使用されます。

   例えばワークフローインスタンスレポートの場合、開始時間と終了時間の時間差（ミリ秒単位）の実値を格納するときに使用するプロパティを指定できます。

* `secondarySubPath`

   subPath に似ている場合、 `secondaryProperty` が使用されます。

ほとんどの場合、`property` のみを使用します。

### クライアントフィルター {#client-filter}

クライアントフィルタは、サーバから返されたデータから表示する情報を抽出する。

>[!NOTE]
>
>このフィルターは、サーバーサイドの処理全体が適用された後に、クライアントサイドで実行されます。

```xml
N:definitions
    N:data
        P:clientFilter [String]
```

`clientFilter` は、JavaScript 関数として、次のように定義されます。

* 入力として、は 1 つのパラメーターを受け取ります。サーバーから返されたデータ（完全に前処理済み）
* 出力時、フィルターを適用した後の（処理後の）値を返します。返すデータは、入力時のデータから抽出または取得したものです。

次の例では、コンポーネントのパスから対応するページパスが抽出されます。

```
function(v) {
    var sepPos = v.lastIndexOf('/jcr:content');
    if (sepPos < 0) {
        return v;
    }
    return v.substring(sepPos + '/jcr:content'.length, v.length);
}
```

### リゾルバーと前処理 {#resolvers-and-preprocessing}

[処理キュー](#processing-queue)で様々なリゾルバーを指定し、前処理を設定します。

```xml
N:definitions
    N:data
        P:resolver
        N:resolverConfig
        N:preprocessing
            N:apply
            N:applyAfter
```

* `resolver`

   使用するリゾルバーを定義します。 次のリゾルバーを使用できます。

   * `const`

      値を他の値にマップします。例えば `en` などの定数を、対応する値 `English` に解決できます。

   * `default`

      デフォルトのリゾルバー。 これは、実際に何も解決しないダミーのリゾルバーです。

   * `page`

      パスの値を、対応するページのパス（正確には、対応する `jcr:content` ノード）に解決します。例： `/content/.../page/jcr:content/par/xyz` が次の値に解決されます： `/content/.../page/jcr:content`.

   * `path`

      パスの値にオプションとしてサブパスを付加し、解決されたパスにあるノードのプロパティ（`resolverConfig` で指定）から実値を取得することで、パスの値を解決します。例： `path` / `/content/.../page/jcr:content` を `jcr:title` プロパティを使用する場合、ページパスはページタイトルに解決されます。

   * `pathextension`

      パスを先頭に付加し、解決されたパスのノードのプロパティから実値を取得することで、値を解決します。例：値 `de` 次のような経路の前に `/libs/wcm/core/resources/languages`（プロパティから値を取得） `language`（国コードを解決する場合） `de` 言語の説明に `German`.

* `resolverConfig`

   リゾルバーの定義をおこないます。以下のうち使用できるオプションは、`resolver` の選択によって決まります。

   * `const`

      プロパティを使用して、解決する定数を指定します。プロパティの名前で、解決する定数を指定します。プロパティの値で、解決後の値を指定します。

      例えば、 **名前**= `1` および **値** `=One` は 1 を 1 に解決します。

   * `default`

      使用できる設定がありません。

   * `page`

      *  (オプション)`propertyName`

         値の解決に使用するプロパティの名前を指定します。指定しない場合、 *jcr:title* （ページタイトル）が使用されます。の `page` つまり、パスが最初にページパスに解決され、次にページタイトルに解決されます。
   * `path`

      *  (オプション)`propertyName`

         値の解決に使用するプロパティの名前を指定します。指定しない場合、 `jcr:title` が使用されます。

      *  (オプション)`subPath`

         このプロパティは、値を解決する前にパスに付加する接尾辞を指定するときに使用します。
   * `pathextension`

      * `path` (mandatory)

         先頭に付加するパスを指定します。

      * `propertyName` （必須）

         実際の値が存在する解決されたパスのプロパティを定義します。

      * `i18n` （オプション）type Boolean)

         解決された値が *国際化* ( 例： [CQ5 の国際化サービス](/help/sites-administering/tc-manage.md)) をクリックします。



* `preprocessing`

   前処理はオプションで、処理フェーズに（別々に）結び付けることができます *適用* または *applyAfter*:

   * `apply`

      初期の前処理フェーズ（[処理キューの説明での手順 3](#processing-queue)）に適用。

   * `applyAfter`

      前処理後（[処理キューの説明での手順 9](#processing-queue)）に適用。

#### リゾルバー {#resolvers}

リゾルバーを使用して、必要な情報を抽出します。 様々なリゾルバーの例を次に示します。

**定数**

次のコードを実行すると、 `VersionCreated` 文字列に `New version created`.

参照先 `/libs/cq/reporting/components/auditreport/typecol/definitions/data`.

```xml
N:data
    P:resolver=const
    N:resolverConfig
        P:VersionCreated="New version created"
```

**ページ**

パス値を、対応するページの jcr:content（子）ノードの jcr:description プロパティに解決します。

参照先 `/libs/cq/reporting/components/compreport/pagecol/definitions/data`.

```xml
N:data
    P:resolver=page
    N:resolverConfig
        P:propertyName="jcr:description"
```

**パス**

以下は、 `/content/.../page` を `jcr:title` プロパティを使用する場合、ページパスはページタイトルに解決されます。

参照先 `/libs/cq/reporting/components/auditreport/pagecol/definitions/data`.

```xml
N:data
    P:resolver=path
    N:resolverConfig
        P:propertyName="jcr:title"
        P:subPath="/jcr:content"
```

**パス拡張**

次のコードでは、値の前に `de` パスの拡張子を持つ `/libs/wcm/core/resources/languages`を呼び出し、プロパティから値を取得します。 `language`（国コードを解決する場合） `de` 言語の説明に `German`.

参照先 `/libs/cq/reporting/components/userreport/languagecol/definitions/data`.

```xml
N:data
    P:resolver=pathextension
    N:resolverConfig
        P:path="/libs/wcm/core/resources/languages"
        P:propertyName="language"
```

#### 前処理 {#preprocessing}

`preprocessing` の定義は、次のどちらかに適用できます。

* 元の値：

   元の値の前処理の定義をに指定します。 `apply` および/または `applyAfter` 直接

* 値の集計状態：

   必要に応じて、集計ごとに個別の定義を指定できます。

   集計値の前処理を明示的に指定するには、前処理の定義をそれぞれの `aggregated` 子ノード ( `apply/aggregated`, `applyAfter/aggregated`) をクリックします。 個別の集計に対して、前処理を明示的に指定する必要がある場合は、各集計の名前が付いた子ノード（例えば `apply/aggregated/min/max` などの集計）で前処理の定義をおこなう必要があります。

前処理中に使用する次のいずれかを指定できます。

* [パターンの検索と置換](#preprocessing-find-and-replace-patterns)検索後、指定したパターン（正規表現として指定）を他のパターンに置き換えます。例えば、元の値からサブ文字列を抽出するときに使用できます。

* [データタイプフォーマッター](#preprocessing-data-type-formatters)

   数値を相対文字列に変換します。例えば、1 時間の時間差を表す値「」は、 `1:24PM (1 hour ago)`.

次に例を示します。

```xml
N:definitions
    N:data
        N:preprocessing
            N:apply|applyAfter
                P:pattern         // regex
                P:replace         // replacement for regex
                // and/or
                P:format          // data type formatter
```

#### 前処理 - パターンの検索と置換 {#preprocessing-find-and-replace-patterns}

前処理の場合は、 `pattern` ( [正規表現](https://en.wikipedia.org/wiki/Regular_expression) または正規表現 ) を検索し、 `replace` パターン：

* `pattern`

   サブ文字列の検索に使用する正規表現。

* `replace`

   元の文字列の置き換えに使用する文字列、または文字列の表現。通常、`pattern` の正規表現によって検索される文字列のサブ文字列を示します。

置き換え例を次のように分類できます。

* ノードの `definitions/data/preprocessing/apply` を次の 2 つのプロパティと共に使用します。

   * `pattern`: `(.*)(/jcr:content)(/|$)(.*)`
   * `replace`: `$1`

* 次のような文字列が検索されます。

   * `/content/geometrixx/en/services/jcr:content/par/text`

* 次の 4 つのセクションに分類されます。

   * `$1` - `(.*)` - `/content/geometrixx/en/services`
   * `$2` - `(/jcr:content)` - `/jcr:content`
   * `$3` - `(/|$)` - `/`
   * `$4` - `(.*)` - `par/text`

* で表される文字列に置き換えられます。 `$1`:

   * `/content/geometrixx/en/services`

#### 前処理 - データタイプフォーマッター {#preprocessing-data-type-formatters}

これらのフォーマッタは、数値を相対文字列に変換します。

例えば、これを `min`, `avg` および `max` 集計。 形式 `min`/ `avg`/ `max` 集計は *時間差* ( 例： `10 days ago`) の場合は、データフォーマッターが必要です。 この場合、 `datedelta` フォーマッタが `min`/ `avg`/ `max` 集計値。 次の場合、 `count` また、元の値も含まず、フォーマッタも必要なく、集計を使用することもできます。

現在使用可能なデータ型フォーマッターは次のとおりです。

* `format`

   データタイプフォーマッター：

   * `duration`

      期間は、2 つの定義された日付の間の期間です。 例えば、ワークフローアクションの開始から終了までの時間を 1 時間とした場合、開始を 2011 年 2 月 13 日 11 時 23 分とすると、終了は 1 時間後の 2011 年 2 月 13 日 12 時 23 分となります。

      数値（ミリ秒と解釈）を期間文字列に変換します。例： `30000` は*の形式で指定します `30s`.*

   * `datedelta`

      過去の日付から「現在」までのタイムスパンです（したがって、レポートを後の時点で表示すると、結果が異なります）。

      数値（日単位の時間差として解釈）が、対応する日付の文字列に変換されます。例えば、1 という値は 1 日前にフォーマットされます。

次の例は、 `datedelta` フォーマット `min` および `max` 集計：

```xml
N:definitions
    N:data
        N:preprocessing
            N:apply
                N:aggregated
                    N:min
                        P:format = "datedelta"
                    N:max
                        P:format = "datedelta"
```

### 列固有の定義 {#column-specific-definitions}

列固有の定義は、その列で使用できるフィルターや集計を指定するものです。

```xml
N:definitions
    P:type
    P:groupable [Boolean]
    N:filters [cq:WidgetCollection] 
    [
        N:<name> // array of nodes (names irrelevant) with the following properties:
            P:filterType
            P:id
            P:phase
    ]
    N:aggregates [cq:WidgetCollection]
    [
        N:<name> // array of nodes (names irrelevant) with the following properties:
            P:text
            P:type
    ]
```

* `type`

   標準オプションとして使用できるものは次のとおりです。

   * `string`
   * `number`
   * `int`
   * `date`
   * `diff`
   * `timeslot`

      日付から、集計に必要な部分を抽出する場合（例えば年でグループ化し、年ごとに集計したデータを取得する場合）に使用します。

   * `sortable`

      異なる値（異なるプロパティの値）を使用してソートし、表示できる値に適用します。
   それに加えて. 上記のいずれかを複数の値として定義できます。例： `string[]` 文字列の配列を定義します。

   値抽出は、列のタイプによって選択されます。値抽出が列のタイプに対して使用可能な場合は、この抽出が使用されます。 それ以外の場合は、デフォルト値抽出が使用されます。

   タイプには、（オプションとして）パラメーターを指定できます。例： `timeslot:year` 日付フィールドから年を抽出します。 タイプとそのパラメーター：

   * `timeslot`  — 値は、 `java.utils.Calendar`.

      * `timeslot:year` - `Calendar.YEAR`
      * `timeslot:month-of-year` - `Calendar.MONTH`
      * `timeslot:week-of-year` - `Calendar.WEEK_OF_YEAR`
      * `timeslot:day-of-month` - `Calendar.DAY_OF_MONTH`
      * `timeslot:day-of-week` - `Calendar.DAY_OF_WEEK`
      * `timeslot:day-of-year` - `Calendar.DAY_OF_YEAR`
      * `timeslot:hour-of-day` - `Calendar.HOUR_OF_DAY`
      * `timeslot:minute-of-hour` - `Calendar.MINUTE`


* `groupable`

   レポートをこの列でグループ化できるかどうかを指定します。

* `filters`

   フィルターの定義。

   * `filterType`

      使用可能なフィルターは次のとおりです。

      * `string`

         文字列ベースのフィルター。
   * `id`

      フィルター識別子。

   * `phase`

      利用可能なフェーズ：

      * `raw`

         生データにフィルターを適用します。

      * `preprocessed`

         前処理されたデータにフィルターが適用されます。

      * `resolved`

         解決されたデータにフィルターが適用されます。


* `aggregates`

   集計の定義。

   * `text`

      集計のテキスト名。 `text` の指定がない場合、集計のデフォルトの説明が使用されます。例えば `minimum` 集計の場合、`min` が使用されます。

   * `type`

      集計タイプ。 使用可能な集計は次のとおりです。

      * `count`

         行数を数えます。

      * `count-nonempty`

         空でない行の数をカウントします。

      * `min`

         最小値を指定します。

      * `max`

         最大値を指定します。

      * `average`

         平均値を示します。

      * `sum`

         すべての値の合計を提供します。

      * `median`

         中央値を示します。

      * `percentile95`

         各値の 95 パーセンタイル値を求めます。

### 列のデフォルト値 {#column-default-values}

列のデフォルト値の定義を次に示します。

```xml
N:defaults
    P:aggregate
```

* `aggregate`

   有効 `aggregate` の値は、 `type` under `aggregates` ( [列固有の定義（定義 — フィルター/集計）](#column-specific-definitions) ) をクリックします。

### イベントおよびアクション {#events-and-actions}

編集設定を使用して、リスナーが検出する必要のあるイベントおよびそのイベント発生後に適用するアクションを定義できます。詳しくは、 [コンポーネント開発の概要](/help/sites-developing/components.md) 」を参照してください。

必要なアクションがすべて実行されるようにするには、次の値を指定します。

```xml
N:cq:editConfig [cq:EditConfig] 
    P:cq:actions [String[]] = "insert", "delete" 
    P:cq:dialogMode = "floating"
    P:cq:layout = "auto"
    N:cq:listeners [cq:EditListenersConfig]
        P:aftercreate = "REFRESH_INSERTED"
        P:afterdelete = "REFRESH_SELF"
        P:afteredit = "REFRESH_SELF"
        P:afterinsert = "REFRESH_INSERTED"
        P:aftermove = "REFRESH_SELF"
        P:afterremove = "REFRESH_SELF"
```

### 一般列 {#generic-columns}

汎用列は、列定義の（ほとんどの）がコンポーネントノードではなく列ノードのインスタンスに格納される拡張です。

個々の汎用コンポーネントに対して、カスタマイズした（標準）ダイアログを使用します。 このダイアログを使用して、レポートのユーザーがレポートページ上の一般列のプロパティを指定できます（「**列のプロパティ...**」のメニューオプションを使用）。

例えば、 **汎用** 列 **ユーザーレポート**;参照 `/libs/cq/reporting/components/userreport/genericcol`.

列を汎用にするには：

* を `type` 列の `definition` ノードから `generic`.

   参照先 `/libs/cq/reporting/components/userreport/genericcol/definitions`

* 列の `definition` ノードで、（標準）ダイアログの定義をおこないます。

   参照先 `/libs/cq/reporting/components/userreport/genericcol/definitions/dialog`

   * ダイアログのフィールドが、対応するコンポーネントプロパティと同じ名前（パスを含む）を参照する必要があります。

      例えば、汎用列のタイプをダイアログで設定できるようにする場合は、「 `./definitions/type`.

   * UI（ダイアログ）を使用して指定されるプロパティは、`columnbase` コンポーネントで指定されるプロパティより優先されます。

* 編集設定を定義します。

   参照先 `/libs/cq/reporting/components/userreport/genericcol/cq:editConfig`

* 標準のAEMの方法を使用して、列のプロパティを定義します。

   プロパティがコンポーネントインスタンスと列インスタンスの両方で指定されている場合、列インスタンスの値が優先されることに注意してください。

   一般列で使用できるプロパティは次のとおりです。

   * `jcr:title`  — 列名
   * `definitions/aggregates`  — 集計
   * `definitions/filters` - filters
   * `definitions/type` — 列のタイプ（セレクター/コンボボックスまたは非表示のフィールドを使用して、ダイアログで定義する必要があります）
   * `definitions/data/resolver` および `definitions/data/resolverConfig` ( ただし、 `definitions/data/preprocessing` または `.../clientFilter`) — リゾルバーと設定
   * `definitions/queryBuilder`  — クエリビルダーの設定
   * `defaults/aggregate`  — デフォルトの集計

   「**ユーザーレポート**」の一般列に新しいインスタンスを作成した場合、ダイアログで指定されるプロパティは次の場所に保持されます。

   `/etc/reports/userreport/jcr:content/report/columns/genericcol/settings/generic`

## レポートデザイン {#report-design}

デザインによって、レポートの作成に使用できる列のタイプが定義されます。 列を追加する段落システムも定義します。

各レポートに個別のデザインを作成することを強くお勧めします。 これにより、完全な柔軟性が確保されます。 [新規レポートの定義](#defining-your-new-report)も参照してください。

デフォルトのレポートコンポーネントは、の下に保持されます。 `/etc/designs/reports`.

レポートの格納場所は、独自のコンポーネントを配置した場所によって次のいずれかになります。

* `/etc/designs/reports/<yourReport>` は、レポートが `/apps/cq/reporting`

* `/etc/designs/<yourProject>/reports/<*yourReport*>` を使用してレポートを作成する `/apps/<yourProject>/reports` pattern

必要なデザインプロパティは、に登録されます。 `jcr:content/reportpage/report/columns` ( 例： `/etc/designs/reports/<reportName>/jcr:content/reportpage/report/columns`):

* `components`

   レポートで使用できるコンポーネントやコンポーネントグループ。

* `sling:resourceType`

   プロパティと値 `cq/reporting/components/repparsys`.

（コンポーネントレポートのデザインから取得した）デザインスニペットの例を次に示します。

```xml
<!-- ... -->
    <jcr:content
        jcr:primaryType="nt:unstructured"
        jcr:title="Component Report"
        sling:resourceType="wcm/core/components/designer">
        <reportpage jcr:primaryType="nt:unstructured">
            <report jcr:primaryType="nt:unstructured">
                <columns
                    jcr:primaryType="nt:unstructured"
                    sling:resourceType="cq/reporting/components/repparsys"
                    components="group:Component Report"/>
            </report>
        </reportpage>
    </jcr:content>
<!-- ... -->
```

個々の列に対してデザインを指定する必要はありません。 使用可能な列は、デザインモードで定義できます。

>[!NOTE]
>
>標準のレポートデザインは変更しないことをお勧めします。 これは、ホットフィックスのアップグレード時やインストール時に変更内容が失われないようにするためです。
>
>標準レポートをカスタマイズする場合は、レポートとそのデザインをコピーしてください。

>[!NOTE]
>
>レポートの作成時に、デフォルトの列を自動的に作成できます。 これらはテンプレートで指定されます。

## レポートテンプレート {#report-template}

各レポートタイプは、テンプレートを提供する必要があります。 これらは標準です [CQ テンプレート](/help/sites-developing/templates.md) また、そのように設定できます。

テンプレートは次の条件を満たす必要があります。

* 設定 `sling:resourceType` から `cq/reporting/components/reportpage`

* 使用するデザインを示す
* を作成する `report` コンテナ ( `reportbase`) コンポーネントを `sling:resourceType` プロパティ

（コンポーネントレポートテンプレートから取得される）テンプレートスニペットの例を次に示します。

```xml
<!-- ... -->
    <jcr:content
        cq:designPath="/etc/designs/reports/compreport"
        jcr:primaryType="cq:PageContent"
        sling:resourceType="cq/reporting/components/reportpage">
        <report
            jcr:primaryType="nt:unstructured"
            sling:resourceType="cq/reporting/components/compreport/compreport"/>
    </jcr:content>
<!-- .. -->
```

（ユーザーレポートテンプレートから取得した）ルートパスの定義を示すテンプレートスニペットの例を次に示します。

```xml
<!-- ... -->
    <jcr:content
        cq:designPath="/etc/designs/reports/userreport"
        jcr:primaryType="cq:PageContent"
        sling:resourceType="cq/reporting/components/reportpage">
        <report
            jcr:primaryType="nt:unstructured"
            rootPath="/home/users"
            sling:resourceType="cq/reporting/components/compreport/compreport"/>
    </jcr:content>
<!-- .. -->
```

デフォルトのレポートテンプレートは、の下に保持されます。 `/libs/cq/reporting/templates`.

ただし、これらのノードは更新しないで、以下に独自のコンポーネントノードを作成することを強くお勧めします。 `/apps/cq/reporting/templates` またはより適切な場合 `/apps/<yourProject>/reports/templates`.

定義例は次のとおりです（[レポートコンポーネントの場所](#location-of-report-components)も参照）。

```xml
N:apps 
    N:cq [nt:folder]
        N:reporting|reports [sling:Folder]
            N:templates [sling:Folder]
```

この場所に、テンプレートのルートを作成します。

```xml
N:apps 
    N:cq [nt:folder]
        N:reporting|reports [sling:Folder]
            N:templates [sling:Folder]
                N:<reportname> [sling:Folder]
```

## 独自のレポートの作成 - 例 {#creating-your-own-report-an-example}

### 新しいレポートの定義 {#defining-your-new-report}

新しいレポートを定義するには、以下を作成して設定する必要があります。

1. レポートコンポーネントのルート
1. レポートベースコンポーネント
1. 1 つ以上の列ベースコンポーネント
1. レポートデザイン
1. レポートテンプレートのルート
1. レポートテンプレート

これらの手順を説明するために、次の例では、リポジトリ内のすべての OSGi 設定をリストするレポートを定義します。つまり、 `sling:OsgiConfig` ノード。

>[!NOTE]
>
>既存のレポートをコピーして新しいバージョンにカスタマイズすることもできます。

1. 新しいレポートのルートノードを作成します。

   例えば、次の場所に `/apps/cq/reporting/components/osgireport`.

   ```xml
   N:cq [nt:folder]
       N:reporting [sling:Folder]
           N:components [sling:Folder]
               N:osgireport [sling:Folder]
   ```

1. レポートベースを定義します。例： `osgireport[cq:Component]` under `/apps/cq/reporting/components/osgireport`.

   ```xml
   N:osgireport [sling:Folder]
       N:osgireport [cq:Component]
           P:sling:resourceSuperType [String] = "cq/reporting/components/reportbase"
           N:charting [nt:unstructured]
               N:settings [nt:unstructured]
                   N:active [cq:WidgetCollection]
                       N:0 [nt:unstructured]
                           P:id [String] = "pie"
                       N:1 [nt:unstructured]
                           P:id [String] = "lineseries"
               N:definitions [cq:WidgetCollections]
                   N:0 [nt:unstructured]
                       P:id [String] = "pie"
                       P:maxRadius [Long] = 180
                       P:type [String] = "pie"
                   N:1 [nt:unstructured]
                       P:id [String] = "lineseries"
                       P:type [String] = "lineseries"
           N:dialog [cq:Dialog]
               P:height [Long] = 424
               N:items [cq:WidgetCollection]
                   N:props [cq:Panel]
                       N:items [cq:WidgetCollection]
                           N:title [cq:Widget]
                               P:path [String] = "/libs/cq/reporting/components/commons/title.infinity.json"
                               P:xtype [String] = "cqinclude"
                           N:description [cq:Widget]
                               P:path [String] = "/libs/cq/reporting/components/commons/description.infinity.json"
                               P:xtype [String] = "cqinclude"
                           N:rootPath [cq:Widget]
                               P:fieldLabel [String] = "Root path"
                               P:name [String] = "./report/rootPath"
                               P:xtype [String] = "pathfield"
                           N:processing [cq:Widget]
                               P:path [String] = "/libs/cq/reporting/components/commons/processing.infinity.json"
                               P:xtype [String] = "cqinclude"
                           N:scheduling [cq:Widget]
                               P:path [String] = "/libs/cq/reporting/components/commons/scheduling.infinity.json"
                               P:xtype [String] = "cqinclude"
           N:queryBuilder [nt:unstructured]
               P:nodeTypes [String[]] = "sling:OsgiConfig"
   ```

   これは、次のようなレポートベースコンポーネントを定義します。

   * タイプのすべてのノードを検索 `sling:OsgiConfig`
   * 次の両方を表示 `pie` および `lineseries` グラフ
   * ユーザーがレポート設定できるダイアログを提供する

1. 最初の列（columnbase）コンポーネントを定義します。例： `bundlecol[cq:Component]` under `/apps/cq/reporting/components/osgireport`.

   ```xml
   N:osgireport [sling:Folder]
       N:bundlecol [cq:Component]
           P:componentGroup [String] = "OSGi Report"
           P:jcr:title = "Bundle"
           P:sling:resourceSuperType [String] = "cq/reporting/components/columnbase"
           N:cq:editConfig [cq:EditConfig]
               P:cq:actions [String[]] = "insert", "delete"
               P:cq:dialogMode [String] = "floating"
               P:cq:layout [String] = "auto"
               N:cq:listeners [cq:EditListenersConfig]
                   P:aftercreate [String] "REFRESH_INSERTED"
                   P:afterdelete [String] "REFRESH_SELF"
                   P:afteredit [String] "REFRESH_SELF"
                   P:afterinsert [String] "REFRESH_INSERTED"
                   P:aftermove [String] "REFRESH_SELF"
                   P:afterremove [String] "REFRESH_SELF"
           N:defaults [nt:unstructured]
               P:aggregate [String] = "count"
           N:definitions [nt:unstructured]
               P:groupable [Boolean] = false
               P:type [String] = "string"
               N:queryBuilder [nt:unstructured]
                   P:property [String] = "jcr:path"
   ```

   これは、次のような列の基本コンポーネントを定義します。

   * サーバーから受信する値（この場合、`jcr:path` の各ノードの `sling:OsgiConfig` プロパティ）を検索し、その値を返す
   * には `count` 集計
   * グループ化はできない
   * タイトル（テーブル内の列タイトル）は `Bundle`
   * サイドキックグループ内にある `OSGi Report`
   * 指定のイベントで更新される

   >[!NOTE]
   >
   >この例では、 `N:data` および `P:clientFilter`. これは、サーバーから受け取った値が 1:1 単位で返されるためです。これはデフォルトの動作です。
   >
   >これは、定義と同じです。
   >
   >
   ```
   >N:data [nt:unstructured]
   >   P:clientFilter [String] = "function(v) { return v; }"
   >```
   >この関数は、受け取った値を返すだけです。

1. レポートデザインを定義します。例： `osgireport[cq:Page]` under `/etc/designs/reports`.

   ```xml
   N:osgireport [cq:Page]
       N:jcr:content [nt:unstructured]
           P:jcr:title [String] = "OSGi report"
           P:sling:resourceType [String] = "wcm/core/components/designer"
           N:reportpage [nt:unstructured]
               N:report [nt:unstructured]
                   N:columns [nt:unstructured]
                       P:components [String] = "group:OSGi Report"
                       P:sling:resourceType [String] = "cq/reporting/components/repparsys"
   ```

1. 新しいレポートテンプレートのルートノードを作成します。

   例えば、次の場所に `/apps/cq/reporting/templates/osgireport`.

   ```xml
   N:cq [nt:folder]
       N:reporting [sling:Folder]
           N:templates [sling:Folder]
               N:osgireport [cq:Template]
   ```

1. レポートテンプレートを定義します。例： `osgireport[cq:Template]` under `/apps/cq/reporting/templates`.

   ```xml
   N:osgireport [cq:Template]
       P:allowedPaths [String[]] = "/etc/reports(/.*)?"
       P:jcr:description [String] = "Use this report generator to create a new OSGi report."
       P:jcr:title [String] = "OSGi Report Template"
       P:ranking [Long] = 100
       P:shortTitle [String] = "OSGi Report"
       N:jcr:content [cq:PageContent]
           P:cq:designPath [String] = "/etc/designs/reports/osgireport"
           P:sling:resourceType [String] = "cq/reporting/components/reportpage"
           N:report [nt:unstructured]
               P:rootPath [String] = "/"
               P:sling:resourceType [String] = "cq/reporting/components/osgireport/osgireport"
       N:thumbnail.png [nt:file]
   ```

   これは、次のようなテンプレートを定義します。

   * は、 `allowedPaths` 結果のレポートの場合 — 上記の場合は、 `/etc/reports`
   * テンプレートのタイトルと説明を指定する
   * テンプレートリストで使用するサムネール画像を指定する（このノードの詳細な定義は表示していません。既存のレポートから thumbnail.png のインスタンスをコピーするのが最も簡単な方法です）。

### 新規レポートのインスタンスの作成 {#creating-an-instance-of-your-new-report}

新しいレポートのインスタンスを、次のように作成できます。

1. **ツール**&#x200B;コンソールを開きます。

1. 左側のウィンドウで、「**レポート**」を選択します。
1. 次に、 **新規…** をクリックします。 を定義 **タイトル** および **名前**」で、新しいレポートタイプ ( **OSGi レポートテンプレート**) をクリックし、 **作成**.
1. 新しいレポートインスタンスがリストに表示されます。 ダブルクリックして開きます。
1. サイドキックからコンポーネント（この例では、「**OSGi Report**」グループの「**バンドル**」）をドラッグして最初の列を作成し、[レポートの定義を開始](/help/sites-administering/reporting.md#the-basics-of-report-customization)します。

   >[!NOTE]
   >
   >この例では、グループ化可能な列がないので、グラフは使用できません。 グラフを表示するには、 `groupable` から `true`:
   >
   >
   ```
   >N:osgireport [sling:Folder]
   > N:bundlecol [cq:Component]
   > N:definitions [nt:unstructured]
   > P:groupable [Boolean] = true
   >```

## レポートフレームワークサービスの設定 {#configuring-the-report-framework-services}

この節では、レポートフレームワークの実装に使用する OSGi サービスの高度な設定オプションについて説明します。

これらは、Web コンソールの設定メニュー ( 例えば、 `http://localhost:4502/system/console/configMgr`) をクリックします。 AEM を操作しているときは、このようなサービスの設定を管理する方法がいくつかあります。詳細および推奨事項については、[OSGi の設定](/help/sites-deploying/configuring-osgi.md)を参照してください。

### 基本サービス（Day CQ レポート設定） {#basic-service-day-cq-reporting-configuration}

* **タイムゾーン** は、に対するタイムゾーン履歴データの作成を定義します。 これは、過去のグラフで、世界中の各ユーザーの同じデータが確実に表示されるようにするためです。
* **ロケール** は、 **タイムゾーン** 履歴データに対して。 ロケールは、ロケール固有のカレンダー設定（週の最初の曜日が日曜日か月曜日かなど）を決定するために使用されます。

* **スナップショットパス** 履歴グラフのスナップショットを保存するルートパスを定義します。
* **レポートへのパス** は、レポートの場所のパスを定義します。 これは、実際にスナップショットを作成するレポートを決定するために、スナップショットサービスで使用されます。
* **毎日のスナップショット** は、毎日のスナップショットを取る 1 日の時間を定義します。 指定された時間は、サーバーのローカルタイムゾーンになります。
* **時間別スナップショット** は、時間別のスナップショットを取得する時間（分）を定義します。
* **行（最大）** は、各スナップショットに対して保存される最大行数を定義します。 この値は合理的に選択する必要があります。値が大きすぎる場合は、リポジトリのサイズに影響します。値が小さすぎる場合は、履歴データの処理方法が原因で、データが正確でない可能性があります。
* **偽データ**&#x200B;有効にした場合、 `fakedata` セレクター；無効にした場合、 `fakedata` セレクターは例外をスローします。

   フェイクデータは、必ずテストおよびデバッグの用途でのみ使用してください。**

   `fakedata` セレクターを使用すると、レポートが暗黙的に終了するので、既存のデータがすべて失われます。データは手動で復元できますが、非常に時間のかかる作業となります。

* 「**Snapshot user**」で、スナップショットの取得に使用できるオプションのユーザーを指定します。

   通常、レポートを終了したユーザーに対してスナップショットが取得されます。例えばパブリッシュシステムで、ユーザーアカウントが複製されていないのでこのユーザーが存在しない場合など、このユーザーの代わりに使用する代替ユーザーの指定が必要な場合があります。

   ただし、ユーザーを指定するとセキュリティリスクが高まる可能性もあります。

* 「**Enforce snapshot user**」を有効にすると、すべてのスナップショットが、「Snapshot user **」で指定したユーザーを使用して取得されます。正しく処理されない場合は、セキュリティに重大な影響が及ぶ可能性があります。

### キャッシュ設定（Day CQ レポートキャッシュ） {#cache-settings-day-cq-reporting-cache}

* **有効にする** では、レポートデータのキャッシュを有効または無効にできます。 レポートのキャッシュを有効にすると、複数の要求がおこなわれる間、レポートデータがメモリに保持されます。これにより、パフォーマンスが向上しますが、メモリ消費が増加し、極端な状況ではメモリ不足に陥る場合があります。
* **TTL** は、レポートデータがキャッシュされる時間（秒）を定義します。 数値を大きくするとパフォーマンスが向上しますが、期間内にデータが変更された場合は不正確なデータが返される場合もあります。
* **最大エントリ数** は、一度にキャッシュできるレポートの最大数を定義します。

>[!NOTE]
>
>レポートデータは、ユーザーと言語ごとに異なる場合があります。 したがって、レポートデータは、レポート、ユーザーおよび言語ごとにキャッシュされます。 これは、 **最大エントリ数** 値 `2` は、次のいずれかのデータを実際にキャッシュします。
>
>* 言語設定が異なる 2 人のユーザー向けの 1 つのレポート
>* 1 人のユーザーに対し、2 つのレポート
>

