---
title: コンテンツフラグメントモデルのデータタイプをカスタマイズする場合は、公開しないでDELETEしないでください。
seo-title: コンテンツフラグメントモデルのデータタイプのカスタマイズ
description: コンテンツフラグメントモデルで使用されるデータタイプはカスタマイズできます。
seo-description: コンテンツフラグメントモデルで使用されるデータタイプはカスタマイズできます。
page-status-flag: de-activated
uuid: d8215dbf-2dbe-43cb-a5c1-dc1cb412a204
contentOwner: aheimoz
discoiquuid: a8b8155c-852c-4d16-b59b-7e19527c2bd4
noindex: true
translation-type: tm+mt
source-git-commit: 3bdff366a0d455b405c1f9de371ced98d25ae2e2
workflow-type: tm+mt
source-wordcount: '1642'
ht-degree: 2%

---


# コンテンツフラグメントモデルのデータタイプをカスタマイズする場合は、公開しないでDELETEしないでください。{#do-not-publish-but-do-not-delete-customizing-data-types-for-content-fragment-models}

[コンテンツフラグメント](/help/assets/content-fragments.md) は、 [コンテンツフラグメントモデルに基づいています](/help/assets/content-fragments-models.md)。 これらのモデルは、様々なデータタイプの [要素](/help/assets/content-fragments.md#constituent-parts-of-a-content-fragment) 、

1行テキスト、複数行リッチテキスト、数値フィールド、ブールセレクター、ドロップダウンメニューオプション、日付と時間など、あらかじめ用意されている様々なデータタイプを利用できます。 AEMユーザーは、対応するフラグメントの編集上の意図に基づいてデータタイプを選択できます。 これにより、単純なテキストモデルから、様々な種類のコンテンツを持つ複雑なモデルや、関連するフラグメントオーサリング体験に至るまで、様々な方法で作業を進めることができます。

データ型は、リポジトリ内の [特定の場所に保持されるノードプロパティの](#properties) 組み合わせによって定義されます [](#locations-in-the-repository)。 独自の [データ型](#creating-your-data-type) 、および [fieldPropertiesを作成することもできます](#creating-your-own-fieldproperties-property)。

<!-- Please uncomment when files are used>
>[!NOTE]
>
>See also [Customizing Content Fragment Models](/help/sites-developing/customizing-content-fragment-models.md).
-->

## リポジトリ内の場所 {#locations-in-the-repository}

そのまま使用できるすべてのデータ型は、次の場所で宣言されます。

`/libs/settings`

新しいデータ型を追加するには、次の手順に従ってノード構造をオーバーレイし `/apps`ます。

`/apps/settings/dam/cfm/models/formbuilderconfig/datatypes/items`

>[!CAUTION]
>
>`/libs` パス内の設定は一切変更しないでください。
>
>次回のアップグレード時、またはサービスまたは修正パックのインストール時に変更される可能性がある項目です。

## プロパティ {#properties}

ノードプロパティは、データ型の定義に使用されます。

* [データタイプのプロパティ](#data-type-properties)
* とその [fieldProperties内](#fieldproperties)

### データタイプのプロパティ {#data-type-properties}

すべてのデータ型は、次のようにノード構造で表されます。

`/libs/settings/dam/cfm/models/formbuilderconfig/datatypes/items`

の各ノード `/items` には、そのデータ型をモデルエディタ内でどのように表すかを定義するプロパティがあります。

データタイプがモデルエディターに表示されるには、次のプロパティがすべて存在する必要があります。

* `fieldIcon`

   [CoralUIアイコン](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/coral-ui/coralui3/Coral.Icon.html#availableicons) 。モデルエディターUIでデータタイプを表します。

* ` [fieldProperties](#fieldproperties)`

   各データ型の構成プロパティを表す配列。

* `fieldResourceType`

   コンテンツフラグメント内のデータ型をレンダリングするために使用されるSlingリソースタイプです。 様々な方法でレンダリングできるデータ型（例えば、単純なテキスト入力や複数行のテキスト入力）の場合、このプロパティは配列として作成し、すべてのリソース型を含める必要があります。 プロパティ `renderasfield` はに自動的に追加され `fieldProperties` 、モデルに追加する必要のあるリソースの種類をユーザーが選択できるようになります。

* `fieldPropResourceType`

   データ型のデフォルトプロパティをレンダリングするために使用されるSlingリソースタイプです。

   例えば、データタイプが次のようになるとします。

   * 1行のテキスト。これ `fieldPropResourceType` はコンポー `textfield` ネントです
   * ブール値。これ `fieldPropResourceType` はコンポー `checkbox` ネントです

* `fieldViewResourceType`

   モデルを構築する際に、プレビュー内でデータ型をレンダリングするために使用されるSlingリソースタイプです。 ユーザーがデータタイプをモデルエディターの左側にドラッグした場合、 `fieldViewResourceType` プロパティはそこでレンダリングされるコンポーネントを表します。 これは、コンポーネント全体をレンダリングしたくないが、モデルエディタのオーバーヘッドを最小限に抑える代わりをレンダリングする場合に使用します。

* `fieldTitle`

   このデータ型のタイトルを定義するプロパティです。 例えば、コンポーネントに **は1行のテキスト** 、マルチフィールドコンポーネントには `textfield` 1行のテキスト **** 、

* `valueType`

   これは、データ型が内部的に格納されたときに返す値の型です。 「 [マッピング](#mappings)」を参照してください。

* `renderType`

   これは、データタイプの内部表現です。 UIコンポーネント `valueType` に接続します。 「 [マッピング](#mappings)」を参照してください。

* `listOrder`

   各データ型には、リスト内での順序を表す値が必要です。 これは、モデルエディタを保存する際に、様々なフィールドの順序（ドラッグ&amp;ドロップで追加/移動）を正しく設定するために使用します。 この値は整数にする必要があり、昇順に番号を割り当てることをお勧めします。 新しいデータ型を作成する場合は、リスト内の最後のデータ型に基づいて値を割り当てることをお勧めします(データ型に存在する `listOrder` 値の最大値)。

#### マッピング {#mappings}

<table> 
 <tbody> 
  <tr> 
   <td>データタイプ<br /> </td> 
   <td>値タイプ<br /> </td> 
   <td>レンダリングタイプ</td> 
  </tr> 
  <tr> 
   <td>1 行のテキスト</td> 
   <td>文字列</td> 
   <td>text-single</td> 
  </tr> 
  <tr> 
   <td>複数行テキスト</td> 
   <td>文字列、コンテンツタイプ<br /> </td> 
   <td>text-multi</td> 
  </tr> 
  <tr> 
   <td>数値（整数/長整数）<br /> </td> 
   <td>long</td> 
   <td>数値</td> 
  </tr> 
  <tr> 
   <td>数値(重複/浮動小数点)</td> 
   <td>double</td> 
   <td>数値</td> 
  </tr> 
  <tr> 
   <td>Boolean</td> 
   <td>ブール型</td> 
   <td>ブール型</td> 
  </tr> 
  <tr> 
   <td>日時</td> 
   <td>カレンダー</td> 
   <td>時刻</td> 
  </tr> 
  <tr> 
   <td>列挙</td> 
   <td>string/long</td> 
   <td>定義済みリスト</td> 
  </tr> 
  <tr> 
   <td>タグ</td> 
   <td>文字列</td> 
   <td>タグ</td> 
  </tr> 
 </tbody> 
</table>

>[!NOTE]
>
>複数の値を持つタイプもあります( `string`例えば、 `long`その他)。 この場合、レンダリングと編集に使用されるコンポーネントは、通常、マルチフィールドコンポーネント( `granite/ui/components/coral/foundation/form/multifield`)でラップされます。 例外はタグです。タグは、編集コンポーネントが正しくレンダリングする役割を持ちます。

### fieldProperties {#fieldproperties}

各データタイプの設定プロパティ。 値 `fieldProperties`:

* `base`

   これは、すべてのコンポー `fieldProperties` ネントの基本です。 その定義は下にある `/libs/dam/cfm/models/editor/components/datatypeproperties/base`。

   変数が含まれ `fieldRoot`ます。その後で、入力を作成して正しいパスを取得する際に使用で `fieldProperties` きます。

   例： フィールド **ラベルの正しいパスを取得するには** 、これが属するコンポーネントを識別するためのキーが必要です。このフィールドの入力は `fieldRoot` +です `<*fieldLabel*>`

* `checkboxfields`

   ここでは、 `Boolean` データタイプのデフォルトのチェックボックスと、Slingパラメーター `checked@Delete` と `checked@TypeHint`が追加されます。

* `datepickerfields`

   日付選択コンポーネントが機能するために必要な非表示の入力を追加するコンポーネントです。 プロパティ `defaultDateField`、、、、お `displayedFormat`よびの作成が含まれ `emptyText``valueFormat``minDate``maxDate`ます。

* `datetimepickerfields`

   これにより、 `Date&Time` データタイプに対して、とのオプションを区別する選択フィールド `Date` が追加され `Date&Time` ます。

* `datevaluefield`

   これによりプロパティに日付選択が追加され、ユーザーがデータタイプのデフォルトを選択できるようにな `Date&Time` ります。

* `descriptionfield`

   このコンポーネントは、複数行エディターで現在選択されているコンポーネントの説明を表す複数行のテキストフィールドを追加します。 各データタイププロパティの最後に、モデルエディタレンダラーによって自動的に追加されます。

* `labelfield`

   フィールドラベルを持つことのできるデータ型のフィールドラベルを追加する `textfield` 入力を追加するコンポーネント。

* `maptopropertyfield`

   このコンポーネントは、プロパティの `Name` フィールドを追加し、データ型の選択したコンポーネントに識別子を与えます。 この変数は、すべてのデータ型に存在する必要があります。

* `maxlengthfield`

   このプロパティを受け入れるデータ型で使用する `maxLength` プロパティを追加するために使用されます。 例えば、 **1行テキスト**、 **数値**、

* `multieditorfield`

   これにより、複数行エディターが動作するのに必要なすべての非表示フィールドが追加されます。これは、 **複数行テキスト** データ型で表されます。

* `mvfields`

   マルチフィールドコンポーネントの動作に必要なすべての非表示フィールドを追加するコンポーネント。 例えば、 **1行テキスト** データ型の2番目のオプションの場合、 これは、マルチフィールドとしてレンダリングされるすべてのコンポーネントに対して追加する必要があります。

* `numbertypefield`

   Number **データ型のNumber****データ型のオプションを選択します。Number** データ型の場合は、Integer **またはFraction****** を選択します。

* `numbervaluefield`

   [ `numberfield` 数値 **** ]のデフォルト値セレクタ。これにより、 `type.options` 定義済みリスト **** データタイプの入力オプションが追加され、選択ボックスコンポーネントの値を決定するために使用されます。

* `placeholderfield`

   これは、コンポーネントの `emptyText` プロパティの入力として機能するテキストフィールドです。 これは、プレースホルダーを受け入れるすべてのデータ型で使用する必要があります(あまり複雑ではありませんが、 (例： **1行テキスト**、 **数値**)。

* `renderasfield`

   これは、データタイプノードのプロパティに複数の要素が存在する場合 `fieldResourceTypes` に、自動的にレンダリングされるコンポーネントです。

* `requiredfield`

   これは、コンポーネントの `required` プロパティを表すチェックボックスです。 ほとんどのコンポーネントがこの `required` フィールドを受け入れるので、このフィールドはほとんどのデータ型で使用できます。

* `tagsfields`

   コンポーネントをレンダリングするために必要な入力を追加するコンポーネント。 `tagfield` Tags **** データ型で使用されます。

* `tagsroot`

   コンポー **ネントのルートパスを設定するために** Tags `tagsfield` データ型で使用されるパスピッカー。

* `textfield`

   このデータ型で定義されるチェックボックスのフィールドラベルを設定するために `Boolean` データ型で使用されます。

* `textvaluefield`

   「 **1行テキスト** 」データ型のデフォルト値プロパティです。

## データタイプの作成 {#creating-your-data-type}

独自のデータ型を作成するには、次の操作が必要です。

* [ノード構造の作成](#creating-the-node-structure)
* [データ型のプロパティの定義](#defining-the-properties-for-your-data-type)

その後、データ型を [使用できます](#using-your-data-type)。

You can also [create your own `fieldProperties`](#creating-your-own-fieldproperties-property).

### Creating the Node Structure {#creating-the-node-structure}

データタイプをオーバーレイするには、ノード構造 `/apps` をの下に作成する必要があります。 まだ存在しない場合は、次を作成する必要があります。

1. まだ存在しない場合は、次を作成する必要があります。

   ```
   + apps 
     + settings
       + dam 
         + cfm (cq:Page) 
           + models (nt:folder)
             + formbuilderconfig (sling:folder)
               + datatypes (nt:unstructured)
                 + items (nt:unstructured)
   ```

   >[!NOTE]
   >
   >`/apps/settings/dam` が既に存在する必要があります。
   >
   >`/cfm/models/formbuilderconfig/datatypes/items` は、nodetypesを指定して作成する必要があります。

1. 以下 `/items` に、新しいデータ型を表す新しいノードを追加できます。

   * Node Type: `nt:unstructured`
   * &quot;プロパティ： 「データ型のプロパティの [定義」を参照してください。](#defining-the-properties-for-your-data-type)

### データ型のプロパティの定義 {#defining-the-properties-for-your-data-type}

1. 使用するデータ型に必要な次の [データ型プロパティの値を決定します](#data-type-properties) 。

   * `fieldResourceType`
   * `fieldPropResourceType`
   * `fieldViewResourceType`

   これらは、データ型のコンポーネントをレンダリングする方法を定義します。 どのような要素でも構いません。 独自のカスタムコンポーネントを含める(一致する一連のコンポーネントが必要 ` [fieldProperties](#fieldproperties)`)。

   データ型のノード上で、適切な値を使用してこれらのプロパティを定義します。

1. Determine the ` [fieldProperties](#fieldproperties)` to be used. これは、必要な属性またはプロパティに依存し `fieldResourceType` ます。

   例えば、には、 `granite/ui/components/coral/foundation/form/textfield`ラベル名 **、**&#x200B;最大長 **、プレースホルダーテキスト**、デフォルト値プロパティを ******** 含める必要があります。

   標準搭載の [fieldPropertiesから選択するか](#fieldproperties)、独自のプロパティを [作成できます](#creating-your-own-fieldproperties-property)。

   データ型のノード上で、適切な値を使用してこれらのプロパティを定義します。

1. 次の [データタイププロパティの値を決定します](#data-type-properties)。

   * `fieldIcon`
   * `fieldTitle`
   * `renderType`
   * `valueType`
   * `listOrder`

   データ型のノード上で、適切な値を使用してこれらのプロパティを定義します。

### データタイプの使用 {#using-your-data-type}

このノード構造を保存すると、すべてのプロパティが適用された状態で、モデルエディタで任意のモデルを開き、新しいデータ型を確認し、使用できます。

## 独自のfieldPropertiesプロパティの作成 {#creating-your-own-fieldproperties-property}

標準搭載の [fieldPropertiesから選択するか、独自の](#fieldproperties)fieldPropertiesを作成できます。

1. 次の場所でコンポーネントを作成します。

   `/apps/dam/cfm/models/editor/components/datatypeproperties/`

   パスが存在しない場合は、 `nt:folder` ノードを使用して作成できます。

   1. 変数にアクセスするには、次のコンポーネントを拡張する必要があります。

      `/libs/dam/cfm/models/editor/components/datatypeproperties/base`* *

   1. コンポーネントは、次の要素を通して含めることができます。

      `sling:include`

   1. このコンポーネントは、フィールド（ユーザーがデータを導入する必要がある場合）またはデータ型に必要なプロパティを持つ非表示の入力をレンダリングする必要があります。 例えば、マルチフィールドコンポーネントには、重複すべきフィールドのタイプを持つ子ノードが必要なので、特定のタイプの子ノードを(スリングPOST機構を通して)作成できる入力が必要です。

1. このコンポーネントのベース名はに追加する必要があり `fieldProperties`ます。
1. 必要なすべてのプロパティに対して同じ手順を繰り返します。

