---
title: コンテンツフラグメントモデルのデータタイプのカスタマイズは、公開しないで削除しないでください。
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

---


# コンテンツフラグメントモデルのデータタイプのカスタマイズは、公開しないで削除しないでください。{#do-not-publish-but-do-not-delete-customizing-data-types-for-content-fragment-models}

[コンテンツフラグメントは](/help/assets/content-fragments.md) 、コンテンツフラグメント [モデルに基づいていま](/help/assets/content-fragments-models.md)す。 これらのモデルは、様々なデータタイプ [の要素](/help/assets/content-fragments.md#constituent-parts-of-a-content-fragment) から構築されます。

1行テキスト、複数行リッチテキスト、数値フィールド、ブールセレクター、ドロップダウンメニューオプション、日時など、様々なデータタイプが標準で使用できます。 AEMユーザーは、対応するフラグメントの編集上の意図に基づいてデータタイプを選択できます。 これにより、単純なテキストモデルを様々な種類のコンテンツを持つ複雑なモデルや、関連するフラグメントオーサリングエクスペリエンスに導くことができます。

データ型は、リポジトリ内の特定の [場所に保持されるノード](#properties) ・プロパ [ティの組み合わせで定義されます](#locations-in-the-repository)。 独自のデータ型とfieldPropertiesを作 [成すること](#creating-your-data-type) もで [きます](#creating-your-own-fieldproperties-property)。

<!-- Please uncomment when files are used>
>[!NOTE]
>
>See also [Customizing Content Fragment Models](/help/sites-developing/customizing-content-fragment-models.md).
-->

## リポジトリ内の場所 {#locations-in-the-repository}

そのまま使用できるすべてのデータ型は、以下の場所で宣言されます。

`/libs/settings`

新しいデータ型を追加するには、次の節に示すようにノード構造をオーバーレイしま `/apps`す。

`/apps/settings/dam/cfm/models/formbuilderconfig/datatypes/items`

>[!CAUTION]
>
>You must not change anything in the `/libs` path.
>
>次回のアップグレード、またはサービスまたは修正パックのインストール時に変更される可能性のある項目です。

## プロパティ {#properties}

ノードのプロパティは、データ型を定義するために使用されます。

* [データタイプのプロパティ](#data-type-properties)
* およびそのfieldProperties内 [で](#fieldproperties)

### データタイプのプロパティ {#data-type-properties}

すべてのデータ型は、次のようにノード構造で表されます。

`/libs/settings/dam/cfm/models/formbuilderconfig/datatypes/items`

の下の各ノードに `/items` は、モデルエディター内でのそのデータ型の表現方法を定義するプロパティがあります。

モデルエディターにデータ型を表示するには、次のすべてのプロパティが必要です。

* `fieldIcon`

   [CoralUIアイコン](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/coral-ui/coralui3/Coral.Icon.html#availableicons) 。モデルエディターUIでデータタイプを表します。

* ` [fieldProperties](#fieldproperties)`

   各データ型の構成プロパティを表す配列。

* `fieldResourceType`

   コンテンツフラグメント内のデータタイプをレンダリングするために使用されるSlingリソースタイプです。 様々な方法でレンダリングできるデータ型（例えば、単純なテキスト入力や複数行テキスト入力）の場合、このプロパティはすべてのリソース型を含む配列として作成する必要があります。 プロパ `renderasfield` ティーが自動的ににに追加さ `fieldProperties` れ、モデルに追加する必要のあるリソースタイプをユーザーが選択できるようになります。

* `fieldPropResourceType`

   データ型のデフォルトプロパティをレンダリングするために使用されるSlingリソースタイプです。

   例えば、次のデータタイプの場合、

   * 1行テキスト、コンポーネ `fieldPropResourceType` ントになりま `textfield` す。
   * ブール値。コンポ `fieldPropResourceType` ーネントになり `checkbox` ます

* `fieldViewResourceType`

   モデルを構築する際に、プレビューでデータタイプをレンダリングするために使用されるSlingリソースタイプです。 ユーザがデータタイプをモデルエディターの左側にドラッグすると、そこでレンダリングされ `fieldViewResourceType` るコンポーネントがプロパティに表示されます。 これは、コンポーネント全体をレンダリングしないが、モデルエディタのオーバーヘッドを最小限に抑える代わりにレンダリングする場合に使用します。

* `fieldTitle`

   このデータ型のタイトルを定義するプロパティです。 例えば、コンポーネ **ントの1行テキスト** 、マルチフィー `textfield` ルドコンポ **ーネントの複数行テキスト** などです。

* `valueType`

   これは、データ型が内部に保存された場合に返される値の型です。 「マッピ [ング](#mappings)」を参照。

* `renderType`

   これは、データタイプの内部表現です。 UIコンポーネン `valueType` トに接続します。 「マッピ [ング](#mappings)」を参照。

* `listOrder`

   各データ型には、リスト内での順序を表す値が必要です。 これは、モデルエディターを保存する際に、様々なフィールド（ドラッグ&amp;ドロップで追加/移動）の正しい順序を保証するために使用します。 この値は整数である必要があり、昇順で番号を割り当てることをお勧めします。 新しいデータ型を作成する場合は、リスト内の最後のデータ型（データ型に存在する値の最も高い値）に基づいて値を割り当てるこ `listOrder` とをお勧めします。

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
   <td>Number（倍精度浮動小数点数）</td> 
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
   <td>文字列/長</td> 
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
>複数の値を持つタイプ( `string`例え `long`ば、その他)もあります。 この場合、レンダリングと編集に使用されるコンポーネントは、通常、マルチフィールドコンポーネント( `granite/ui/components/coral/foundation/form/multifield`)でラップされます。 例外はタグで、編集コンポーネントが正しくレンダリングを行います。

### fieldProperties {#fieldproperties}

各データタイプの設定プロパティ。 値 `fieldProperties`:

* `base`

   これは、すべてのコンポーネントの基本 `fieldProperties` です。 その定義は下にある `/libs/dam/cfm/models/editor/components/datatypeproperties/base`。

   変数が含まれ、その後で `fieldRoot`入力を作成し `fieldProperties` て正しいパスを取得する際に使用できます。

   例：フィールドラベルの正しいパス **を取得するには** 、これが属するコンポーネントを識別するためのキーが必要です。このフィールドの入力は `fieldRoot` +です `<*fieldLabel*>`

* `checkboxfields`

   ここでは、データタイプのデフォルトのチェッ `Boolean` クボックスと、Slingパラメーターおよびが追加 `checked@Delete` されま `checked@TypeHint`す。

* `datepickerfields`

   日付選択コンポーネントが機能するために必要な非表示の入力を追加するコンポーネント。 プロパティ、、、、お `defaultDateField`よびの `displayedFormat`作成が含ま `emptyText`れ `valueFormat`ます `minDate``maxDate`。

* `datetimepickerfields`

   これにより、とオプションを区別するた `Date&Time` めのデータ型の選択フィールド `Date` が追加 `Date&Time` されます。

* `datevaluefield`

   これにより、プロパティに日付選択が追加され、ユーザーがデータタイプのデフォルトを選択できるよ `Date&Time` うになります。

* `descriptionfield`

   このコンポーネントは、複数行エディターで現在選択されているコンポーネントの説明を表す複数行のテキストフィールドを追加します。 各データタイププロパティの最後に、モデルエディターレンダラーによって自動的に追加されます。

* `labelfield`

   フィールドラベルを持つこ `textfield` とができるデータ型のフィールドラベルを追加する入力を追加するコンポーネントです。

* `maptopropertyfield`

   このコンポーネントは、プ `Name` ロパティにフィールドを追加し、データ型の選択したコンポーネントに識別子を与えます。 すべてのデータ型に存在する必要があります。

* `maxlengthfield`

   このプロパティを受け入れるデータ `maxLength` 型で使用するプロパティを追加するために使用します。 例えば、1行 **テキスト**、 **Number**、

* `multieditorfield`

   これにより、複数行エディターが動作するのに必要なすべての非表示フィールドが追加されます。このフィールドは、 **Multi Line Text** （複数行テキスト）データ型で表されます。

* `mvfields`

   複数フィールドコンポーネントを機能させるために必要なすべての非表示フィールドを追加するコンポーネント。 例えば、1行テキストデータ型の2番目のオ **プションの場合** 、 これは、マルチフィールドとしてレンダリングされるすべてのコンポーネントに対して追加する必要があります。

* `numbertypefield`

   データ型として **Integer** または **Fraction** Number **Dataを選択するNumberデータ型の** オプションを選択し **** ます。

* `numbervaluefield`

   [ `numberfield` Number **]の既定値セレクター** 。 `type.options` Enumeration **** データ型の入力オプションが追加されます。これは、選択ボックスコンポーネントの値を決定するために使用されます。

* `placeholderfield`

   これは、コンポーネントのプロパティの入力として機能するテ `emptyText` キストフィールドです。 これは、プレースホルダーを受け入れるすべてのデータ型で使用する必要があります(あまり複雑ではありませんが、例：1行テ **キスト**、 **番号**、

* `renderasfield`

   これは、データタイプノードのプロパティに複数が存在する場合 `fieldResourceTypes` に自動的にレンダリングされるコンポーネントです。

* `requiredfield`

   これは、コンポーネントのプロパティを表 `required` すチェックボックスです。 ほとんどのコンポーネントがこのフ `required` ィールドを受け入れるので、このフィールドはほとんどのデータ型で使用できます。

* `tagsfields`

   コンポーネントをレンダリングするために必要な入力を `tagfield` 追加するコンポーネントで、 **Tagsデータ型で使用されます** 。

* `tagsroot`

   コンポーネントのルートパスを設定す **るために** 、Tagsデータ型で使用されるパスピッ `tagsfield` カーです。

* `textfield`

   このデータ型によっ `Boolean` て定義されるチェックボックスのフィールドラベルを設定するために、データ型によって使用されます。

* `textvaluefield`

   Single Line Textデータ型のデフォ **ルト値プロパティ** 。

## データ型の作成 {#creating-your-data-type}

独自のデータ型を作成するには、次の操作を行う必要があります。

* [ノード構造の作成](#creating-the-node-structure)
* [データ型のプロパティの定義](#defining-the-properties-for-your-data-type)

その後、データ [型を使用できます](#using-your-data-type)。

You can also [create your own `fieldProperties`](#creating-your-own-fieldproperties-property).

### ノード構造の作成 {#creating-the-node-structure}

データタイプをオーバーレイするには、 `/apps` の下にノード構造を作成する必要があります。 まだ存在しない場合は、次を作成する必要があります。

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

1. 新し `/items` いデータタイプを表す新しいノードを追加できます。

   * Node Type: `nt:unstructured`
   * 「プロパティ：詳しくは、 [データ型のプロパティの定義を参照してください。](#defining-the-properties-for-your-data-type)

### データ型のプロパティの定義 {#defining-the-properties-for-your-data-type}

1. 使用するデータ型に必要な [次のデータ型](#data-type-properties) ・プロパティの値を決定します。

   * `fieldResourceType`
   * `fieldPropResourceType`
   * `fieldViewResourceType`
   これらは、データ型のコンポーネントのレンダリング方法を定義します。 どんな要素でも構いません。独自のカスタムコンポーネントを含める(一致する一連のコンポーネントが必要 ` [fieldProperties](#fieldproperties)`です)。

   適切な値を使用して、データ型のノード上でこれらのプロパティを定義します。

1. Determine the ` [fieldProperties](#fieldproperties)` to be used. これは、必要な属性またはプロパティに依存し `fieldResourceType` ます。

   例えば、ラベル名、最大長 `granite/ui/components/coral/foundation/form/textfield`、プレースホルダ **ーテキスト************** 、初期設定値プロパティを持つ必要があります。

   標準搭載のfieldPropertiesから選択するか、独自のプロパ [ティを作](#fieldproperties)成できます [](#creating-your-own-fieldproperties-property)。

   適切な値を使用して、データ型のノード上でこれらのプロパティを定義します。

1. 次のデータタイププロパティ [の値を決定します](#data-type-properties)。

   * `fieldIcon`
   * `fieldTitle`
   * `renderType`
   * `valueType`
   * `listOrder`
   適切な値を使用して、データ型のノード上でこれらのプロパティを定義します。

### データタイプの使用 {#using-your-data-type}

このノード構造を保存した後、すべてのプロパティが適用された状態で、モデルエディターで任意のモデルを開き、新しいデータ型を確認し、使用できます。

## 独自のfieldPropertiesプロパティの作成 {#creating-your-own-fieldproperties-property}

標準搭載のfieldPropertiesから選択するか、独自の [プロパティ](#fieldproperties)を作成できます。

1. 次の場所にコンポーネントを作成します。

   `/apps/dam/cfm/models/editor/components/datatypeproperties/`

   パスが存在しない場合は、ノードを使用して作成でき `nt:folder` ます。

   1. 変数にアクセスするには、次の拡張が必要です。

      `/libs/dam/cfm/models/editor/components/datatypeproperties/base`* *

   1. コンポーネントは、次の方法で組み込むことができます。

      `sling:include`

   1. このコンポーネントは、フィールド（ユーザーがデータを導入する必要がある場合）またはデータ型に必要なプロパティを持つ非表示の入力をレンダリングする必要があります。 例えば、マルチフィールドコンポーネントには、複製するフィールドのタイプを持つ子ノードが必要なので、特定のタイプの子ノードを（Sling POSTメカニズムを通じて）作成できる入力が必要です。

1. このコンポーネントのベース名をに追加する必要がありま `fieldProperties`す。
1. 必要なすべてのプロパティに対して同じ手順を繰り返します。

