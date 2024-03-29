---
title: コンテンツフラグメントモデルのデータタイプのカスタマイズはDELETEしないで公開しないでください
seo-title: Customizing Data Types for Content Fragment Models
description: コンテンツフラグメントモデルで使用されるデータタイプはカスタマイズできます。
seo-description: Data types used in Content Fragment Models can be customized.
page-status-flag: de-activated
uuid: d8215dbf-2dbe-43cb-a5c1-dc1cb412a204
contentOwner: AEM Docs
discoiquuid: a8b8155c-852c-4d16-b59b-7e19527c2bd4
noindex: true
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '1661'
ht-degree: 2%

---


# コンテンツフラグメントモデルのデータタイプのカスタマイズはDELETEしないで公開しないでください{#do-not-publish-but-do-not-delete-customizing-data-types-for-content-fragment-models}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

[コンテンツフラグメント](/help/assets/content-fragments.md) は、次に基づいています： [コンテンツフラグメントモデル](/help/assets/content-fragments-models.md). これらのモデルは、 [要素](/help/assets/content-fragments.md#constituent-parts-of-a-content-fragment) 様々なデータタイプの

1 行テキスト、複数行リッチテキスト、数値フィールド、ブールセレクター、ドロップダウンメニューオプション、日付と時刻など、様々なデータタイプが標準で使用できます。 AEMユーザーは、対応するフラグメントの編集上の意図に基づいてデータタイプを選択できます。 これにより、を通じて単純なテキストモデルを、様々な種類のコンテンツを持つ複雑なモデルや関連するフラグメントオーサリングエクスペリエンスに対応できます。

データタイプは [ノードプロパティの組み合わせ](#properties) ～で開催される [リポジトリ内の特定の場所](#locations-in-the-repository). 独自の [データタイプ](#creating-your-data-type) および [fieldProperties](#creating-your-own-fieldproperties-property).

<!-- Please uncomment when files are used>
>[!NOTE]
>
>See also [Customizing Content Fragment Models](/help/sites-developing/customizing-content-fragment-models.md).
-->

## リポジトリ内の場所 {#locations-in-the-repository}

すべての標準データタイプは、次の場所で宣言されます。

`/libs/settings`

以下のようにノード構造をオーバーレイして、新しいデータ型を追加できます。 `/apps`:

`/apps/settings/dam/cfm/models/formbuilderconfig/datatypes/items`

>[!CAUTION]
>
>`/libs` パス内は一切変更しないでください。
>
>次回のアップグレード時、またはサービスまたは修正パックのインストール時に変更される可能性がある項目。

## プロパティ {#properties}

ノードプロパティは、次のデータ型の定義に使用されます。

* [データタイプのプロパティ](#data-type-properties)
* そしてその中に [fieldProperties](#fieldproperties)

### データタイプのプロパティ {#data-type-properties}

すべてのデータ型は、以下のようにノード構造で表されます。

`/libs/settings/dam/cfm/models/formbuilderconfig/datatypes/items`

以下の各ノード `/items` には、モデルエディター内でのそのデータ型の表現方法を定義するプロパティがあります。

データ型がモデルエディターに表示されるには、次のすべてのプロパティが存在する必要があります。

* `fieldIcon`

   [CoralUI アイコン](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/coral-ui/coralui3/Coral.Icon.html#availableicons) を使用して、モデルエディター UI でデータ型を表します。

* ` [fieldProperties](#fieldproperties)`

   各データ型の設定プロパティを表す配列。

* `fieldResourceType`

   コンテンツフラグメントでデータタイプをレンダリングするために使用される Sling リソースタイプ。 様々な方法（単純なテキスト入力や複数行のテキスト入力など）でレンダリングできるデータ型の場合、このプロパティは、すべてのリソース型を含む配列として作成する必要があります。 この `renderasfield` プロパティは `fieldProperties` モデルに追加する必要のあるリソースタイプをユーザーが選択できるようにするには、

* `fieldPropResourceType`

   データタイプのデフォルトのプロパティをレンダリングするために使用される Sling リソースタイプ。

   例えば、データタイプの場合は、次のようになります。

   * 1 行のテキスト、 `fieldPropResourceType` は `textfield` コンポーネント
   * ブール値 `fieldPropResourceType` は `checkbox` コンポーネント

* `fieldViewResourceType`

   モデルを構築する際に、プレビューでデータタイプをレンダリングするために使用される Sling リソースタイプ。 ユーザーがデータタイプをモデルエディターの左側にドラッグすると、 `fieldViewResourceType` プロパティは、そこでレンダリングされるコンポーネントを表します。 これは、完全なコンポーネントをレンダリングする必要がなく、モデルエディタのオーバーヘッドを最小限に抑える代わりのコンポーネントをレンダリングする場合にのみ使用します。

* `fieldTitle`

   このデータ型のタイトルを定義するプロパティ。 例： **1 行のテキスト** の `textfield` コンポーネント **複数行テキスト** マルチフィールドコンポーネントの場合。

* `valueType`

   これは、データ型が内部的に保存されたときに返される値のタイプです。 詳しくは、 [マッピング](#mappings).

* `renderType`

   これは、データタイプの内部表現です。 これは、 `valueType` を UI コンポーネントに追加します。 詳しくは、 [マッピング](#mappings).

* `listOrder`

   各データ型には、リスト内での順序を表す値が必要です。 これは、モデルエディターの保存時に、様々なフィールド（ドラッグ&amp;ドロップで追加/移動）の正しい順序を保証するために使用されます。 この値は整数にする必要があります。昇順で順序付けされた数値を割り当てることをお勧めします。 新しいデータ型を作成する場合、リストの最後のデータ型 ( `listOrder` の値がデータ型に存在する場合 )。

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
   <td>数値（整数/長さ）<br /> </td> 
   <td>long</td> 
   <td>数値</td> 
  </tr> 
  <tr> 
   <td>数値 (double/float)</td> 
   <td>重複</td> 
   <td>数値</td> 
  </tr> 
  <tr> 
   <td>ブーリアン</td> 
   <td>ブール値</td> 
   <td>ブール値</td> 
  </tr> 
  <tr> 
   <td>日時</td> 
   <td>カレンダー</td> 
   <td>time</td> 
  </tr> 
  <tr> 
   <td>定義済みリスト</td> 
   <td>string/long</td> 
   <td>列挙</td> 
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
>一部のタイプ ( 例： `string`, `long`（特に）は複数の値を持つ場合があります。 この場合、レンダリングと編集に使用されるコンポーネントは通常、マルチフィールドコンポーネント ( `granite/ui/components/coral/foundation/form/multifield`) をクリックします。 例外はタグで、編集コンポーネントが正しくレンダリングをおこないます。

### fieldProperties {#fieldproperties}

各データタイプの設定プロパティ。 の値 `fieldProperties`:

* `base`

   これが全ての `fieldProperties` コンポーネント。 定義はの下に配置されています `/libs/dam/cfm/models/editor/components/datatypeproperties/base`.

   変数が含まれます。 `fieldRoot`( 後続 `fieldProperties` は、入力を作成する際にを使用して、正しいパスを取得できます。

   例：正しいパスを取得するには **フィールドラベル** このフィールドの入力は、このが属するコンポーネントを識別するためのキーが必要です。 `fieldRoot` + `<*fieldLabel*>`

* `checkboxfields`

   このコンポーネントは、 `Boolean` データタイプと Sling パラメーター `checked@Delete` および `checked@TypeHint`.

* `datepickerfields`

   日付選択コンポーネントが機能するために必要な、非表示の入力を追加するコンポーネント。 プロパティの作成を含む `defaultDateField`, `displayedFormat`, `emptyText`, `valueFormat`, `minDate` および `maxDate`.

* `datetimepickerfields`

   これにより、 `Date&Time` 区別するデータタイプ `Date` および `Date&Time` オプション。

* `datevaluefield`

   これにより、プロパティに日付選択が追加され、ユーザーがデフォルトの `Date&Time` データタイプ。

* `descriptionfield`

   このコンポーネントは、複数行エディターで現在選択されているコンポーネントの説明を表す複数行テキストフィールドを追加します。 これは、各データタイププロパティの最後にあるモデルエディターレンダラーによって自動的に追加されます。

* `labelfield`

   を追加するコンポーネント `textfield` フィールドラベルを持つことのできるデータ型のフィールドラベルを追加する入力。

* `maptopropertyfield`

   このコンポーネントは、 `Name` フィールドに値を入力し、データ型の選択したコンポーネントに識別子を付与する。 すべてのデータ型に存在する必要があります。

* `maxlengthfield`

   これは、 `maxLength` このプロパティを受け取るデータ型で使用するプロパティです。 例えば、を使用します。 **1 行のテキスト**, **数値**&#x200B;など

* `multieditorfield`

   これにより、複数行エディターが動作するのに必要な非表示フィールドがすべて追加されます。このフィールドは、 **複数行テキスト** データタイプ。

* `mvfields`

   マルチフィールドコンポーネントの動作に必要なすべての非表示フィールドを追加するコンポーネント。 例えば、 **1 行のテキスト** データタイプ。 これは、マルチフィールドとしてレンダリングされるすべてのコンポーネントに対して追加する必要があります。

* `numbertypefield`

   のオプションを選択します。 **数値** 次の中から選択するデータ型 **整数** または **分数** の **数値** データタイプ。

* `numbervaluefield`

   A `numberfield` のデフォルト値セレクター **数値** `type.options` これにより、 **列挙** データタイプ。選択ボックスコンポーネントの値の決定に使用されます。

* `placeholderfield`

   これは、 `emptyText` プロパティを設定します。 これは、プレースホルダーを受け入れるすべてのデータ型で使用する必要があります（それほど複雑ではありません）。例： **1 行のテキスト**, **数値**&#x200B;など )

* `renderasfield`

   これは、複数の場合に自動的にレンダリングされるコンポーネントです `fieldResourceTypes` は、データ型ノードのプロパティに存在します。

* `requiredfield`

   これは、 `required` プロパティを使用します。 ほとんどのコンポーネントは `required` 「 」フィールドの場合、このフィールドはほとんどのデータタイプで使用できます。

* `tagsfields`

   に必要な入力を追加するコンポーネント `tagfield` レンダリングするコンポーネント ( **タグ** データタイプ。

* `tagsroot`

   パスピッカーは、 **タグ** 次のルートパスを設定するデータタイプ `tagsfield` コンポーネント。

* `textfield`

   使用者 `Boolean` データタイプ：このデータタイプで定義されるチェックボックスのフィールドラベルを設定します。

* `textvaluefield`

   のデフォルト値プロパティ **1 行のテキスト** データタイプ。

## データタイプの作成 {#creating-your-data-type}

独自のデータタイプを作成するには、次の操作が必要です。

* [ノード構造の作成](#creating-the-node-structure)
* [データタイプのプロパティを定義する](#defining-the-properties-for-your-data-type)

その後、 [データタイプを使用](#using-your-data-type).

また、 [独自の `fieldProperties`](#creating-your-own-fieldproperties-property).

### ノード構造の作成 {#creating-the-node-structure}

ノード構造は以下の下に作成する必要があります。 `/apps` を使用して、データタイプをオーバーレイします。 まだ存在しない場合は、次を作成する必要があります。

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
   >`/apps/settings/dam` は既に存在する必要があります。
   >
   >`/cfm/models/formbuilderconfig/datatypes/items` は、ノードタイプを指定して作成する必要があります。

1. の下 `/items` 新しいデータ型を表す新しいノードを追加できます。

   * ノードタイプ： `nt:unstructured`
   * &quot;プロパティ：参照 [データタイプのプロパティの定義](#defining-the-properties-for-your-data-type)

### データタイプのプロパティの定義 {#defining-the-properties-for-your-data-type}

1. 次の値を決定します [データタイプのプロパティ](#data-type-properties) データ型に必要なデータ要素：

   * `fieldResourceType`
   * `fieldPropResourceType`
   * `fieldViewResourceType`

   これらは、データタイプのコンポーネントのレンダリング方法を定義します。 任意のコンポーネントを指定できます。独自のカスタムコンポーネントを含める ( 一致する ` [fieldProperties](#fieldproperties)`) をクリックします。

   これらのプロパティを適切な値で、データ型のノードに定義します。

1. 次を決定： ` [fieldProperties](#fieldproperties)` を使用します。 これは、 `fieldResourceType` が必要です。

   例： `granite/ui/components/coral/foundation/form/textfield`が **ラベル名**, a **最大長**, a **プレースホルダーテキスト** および **デフォルト値** プロパティ。

   標準搭載のから選択できます [fieldProperties](#fieldproperties)または [独自のプロパティを作成する](#creating-your-own-fieldproperties-property).

   これらのプロパティを適切な値で、データ型のノードに定義します。

1. 次の値を決定します [データタイプのプロパティ](#data-type-properties):

   * `fieldIcon`
   * `fieldTitle`
   * `renderType`
   * `valueType`
   * `listOrder`

   これらのプロパティを適切な値で、データ型のノードに定義します。

### データタイプの使用 {#using-your-data-type}

このノード構造を保存すると、すべてのプロパティが適用された状態で、モデルエディターで任意のモデルを開き、新しいデータ型を表示して使用できます。

## 独自の fieldProperties プロパティを作成する {#creating-your-own-fieldproperties-property}

標準搭載のから選択できます [fieldProperties](#fieldproperties)または独自のを作成します。

1. 次の場所にコンポーネントを作成します。

   `/apps/dam/cfm/models/editor/components/datatypeproperties/`

   パスが存在しない場合は、 `nt:folder` ノード。

   1. 変数にアクセスするには、このコンポーネントで次の拡張を行う必要があります。

      `/libs/dam/cfm/models/editor/components/datatypeproperties/base`* *

   1. コンポーネントは、次の通りに含めることができます。

      `sling:include`

   1. このコンポーネントは、フィールド（データを導入する必要がある場合）または非表示の入力（データ型で必要なプロパティを含む）をレンダリングする必要があります。 例えば、マルチフィールドコンポーネントには、複製するフィールドのタイプを持つ子ノードが必要なので、(SlingPOSTメカニクスを通じて ) 特定のタイプの子ノードを作成できる入力が必要です。

1. このコンポーネントのベース名は、 `fieldProperties`.
1. 必要なすべてのプロパティに対して、この手順を繰り返します。

