---
title: コンテンツフラグメントモデルのデータタイプのカスタマイズはDELETEしないでください。
seo-title: コンテンツフラグメントモデルのデータタイプのカスタマイズ
description: コンテンツフラグメントモデルで使用されるデータタイプはカスタマイズできます。
seo-description: コンテンツフラグメントモデルで使用されるデータタイプはカスタマイズできます。
page-status-flag: de-activated
uuid: d8215dbf-2dbe-43cb-a5c1-dc1cb412a204
contentOwner: aheimoz
discoiquuid: a8b8155c-852c-4d16-b59b-7e19527c2bd4
noindex: true
source-git-commit: 3bdff366a0d455b405c1f9de371ced98d25ae2e2
workflow-type: tm+mt
source-wordcount: '1642'
ht-degree: 2%

---


# 公開しないが、コンテンツフラグメントモデルのデータタイプのカスタマイズをDELETEしない{#do-not-publish-but-do-not-delete-customizing-data-types-for-content-fragment-models}

[コンテンツフ](/help/assets/content-fragments.md) ラグメントは、コンテンツフ [ラグメントモデルに基づいています](/help/assets/content-fragments-models.md)。これらのモデルは、異なるデータ型の[要素](/help/assets/content-fragments.md#constituent-parts-of-a-content-fragment)から構築されます。

1行テキスト、複数行リッチテキスト、数値フィールド、ブールセレクター、ドロップダウンメニューオプション、日付と時刻など、様々なデータタイプが標準で使用できます。 AEMユーザーは、対応するフラグメントの編集上の意図に基づいてデータタイプを選択できます。 これにより、単純なテキストモデルを、様々な種類のコンテンツを持つ複雑なモデルや、関連するフラグメントのオーサリングエクスペリエンスにまで引き渡すことができます。

データ型は、[リポジトリ内の特定の場所](#locations-in-the-repository)に保持されるノードプロパティ](#properties)の[の組み合わせによって定義されます。 独自の[データ型](#creating-your-data-type)と[fieldProperties](#creating-your-own-fieldproperties-property)を作成することもできます。

<!-- Please uncomment when files are used>
>[!NOTE]
>
>See also [Customizing Content Fragment Models](/help/sites-developing/customizing-content-fragment-models.md).
-->

## リポジトリ内の場所{#locations-in-the-repository}

すべての標準データ型は、次の場所で宣言されます。

`/libs/settings`

`/apps`の下に次のようにノード構造をオーバーレイすることで、新しいデータ型を追加できます。

`/apps/settings/dam/cfm/models/formbuilderconfig/datatypes/items`

>[!CAUTION]
>
>`/libs` パス内のものは一切変更しないでください。
>
>次回のアップグレード時、またはサービスパックや修正パックのインストール時に変更される可能性がある項目。

## プロパティ {#properties}

ノードプロパティは、データ型の定義に使用されます。

* [データタイプのプロパティ](#data-type-properties)
* と、それらの[fieldProperties](#fieldproperties)内

### データタイプのプロパティ{#data-type-properties}

すべてのデータ型は、次のようにノード構造で表されます。

`/libs/settings/dam/cfm/models/formbuilderconfig/datatypes/items`

`/items`の下の各ノードには、モデルエディター内でそのデータ型をどのように表すかを定義するプロパティがあります。

データ型をモデルエディターに表示するには、次のすべてのプロパティが存在する必要があります。

* `fieldIcon`

   [CoralUIアイコ](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/coral-ui/coralui3/Coral.Icon.html#availableicons) ンは、モデルエディターUIのデータタイプを表します。

* ` [fieldProperties](#fieldproperties)`

   各データタイプの設定プロパティを表す配列。

* `fieldResourceType`

   コンテンツフラグメントでデータタイプをレンダリングするために使用されるSlingリソースタイプ。 様々な方法でレンダリングできるデータ型（単純なテキスト入力や複数行のテキスト入力など）の場合、このプロパティは、すべてのリソース型を含む配列として作成する必要があります。 `renderasfield`プロパティが`fieldProperties`に自動的に追加され、モデルに追加する必要のあるリソースタイプをユーザーが選択できるようになります。

* `fieldPropResourceType`

   データタイプのデフォルトのプロパティをレンダリングするために使用されるSlingリソースタイプ。

   例えば、データタイプの場合は次のようになります。

   * 1行のテキストの場合、`fieldPropResourceType`は`textfield`コンポーネントになります。
   * ブール値。`fieldPropResourceType`は`checkbox`コンポーネントです。

* `fieldViewResourceType`

   モデルを作成する際に、プレビューでデータタイプをレンダリングするために使用されるSlingリソースタイプ。 ユーザーがデータタイプをモデルエディターの左側にドラッグすると、`fieldViewResourceType`プロパティはそこでレンダリングされるコンポーネントを表します。 これは、コンポーネント全体をレンダリングする必要はなく、モデルエディタのオーバーヘッドを最小限に抑える代わりにをレンダリングする場合に使用します。

* `fieldTitle`

   このデータ型のタイトルを定義するプロパティ。 例えば、**`textfield`コンポーネントの場合は1行のテキスト**、マルチフィールドコンポーネントの場合は&#x200B;**複数行のテキスト**&#x200B;を指定します。

* `valueType`

   これは、データ型が内部的に格納されたときに返される値のタイプです。 [マッピング](#mappings)を参照してください。

* `renderType`

   これは、データタイプの内部表現です。 `valueType`をUIコンポーネントに接続します。 [マッピング](#mappings)を参照してください。

* `listOrder`

   各データ型には、リスト内での順序を表す値が必要です。 これは、モデルエディターを保存する際に、様々なフィールドの正しい順序（ドラッグ&amp;ドロップによる追加/移動）を保証するために使用されます。 この値は整数にする必要があり、昇順で番号を割り当てることをお勧めします。 新しいデータ型を作成する場合は、リスト内の最後のデータ型（データ型に存在する`listOrder`の最も大きい値）に基づいて値を割り当てることをお勧めします。

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
   <td>数値(double/float)</td> 
   <td>double</td> 
   <td>数値</td> 
  </tr> 
  <tr> 
   <td>ブール値</td> 
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
>一部の型（特に`string`、`long`など）は複数値を持つ場合があります。 この場合、レンダリングと編集に使用されるコンポーネントは通常、マルチフィールドコンポーネント(`granite/ui/components/coral/foundation/form/multifield`)でラップされます。 例外はタグで、編集コンポーネントが正しくレンダリングをおこないます。

### fieldProperties {#fieldproperties}

各データタイプの設定プロパティ。 `fieldProperties`の値：

* `base`

   これは、すべての`fieldProperties`コンポーネントの基礎です。 定義は`/libs/dam/cfm/models/editor/components/datatypeproperties/base`の下に配置されています。

   変数`fieldRoot`が含まれ、後続の`fieldProperties`は、正しいパスを取得するための入力を作成する際に使用できます。

   例：**フィールドラベル**&#x200B;の正しいパスを取得するには、このフィールドの入力は`fieldRoot` + `<*fieldLabel*>`である必要があります。

* `checkboxfields`

   このコンポーネントは、`Boolean`データタイプのデフォルトのチェックボックスと、Slingパラメーター`checked@Delete`および`checked@TypeHint`を追加します。

* `datepickerfields`

   日付選択コンポーネントが機能するために必要な非表示の入力を追加するコンポーネント。 プロパティ`defaultDateField`、`displayedFormat`、`emptyText`、`valueFormat`、`minDate`、`maxDate`の作成が含まれます。

* `datetimepickerfields`

   これにより、`Date`と`Date&Time`のオプションを区別するために、`Date&Time`データ型の選択フィールドが追加されます。

* `datevaluefield`

   これにより、プロパティに日付選択が追加され、ユーザーが`Date&Time`データタイプのデフォルトを選択できるようになります。

* `descriptionfield`

   このコンポーネントは、複数行エディターで現在選択されているコンポーネントの説明を表す複数行テキストフィールドを追加します。 これは、各データタイププロパティの最後に、モデルエディターレンダラーによって自動的に追加されます。

* `labelfield`

   フィールドラベルを持つことができるデータ型のフィールドラベルを追加する`textfield`入力を追加するコンポーネント。

* `maptopropertyfield`

   このコンポーネントは、プロパティに`Name`フィールドを追加し、データ型の選択したコンポーネントに識別子を提供します。 すべてのデータ型に存在する必要があります。

* `maxlengthfield`

   このプロパティを受け入れるデータ型で使用する`maxLength`プロパティを追加するために使用されます。 例えば、**1行のテキスト**、**数値**&#x200B;などを使用します。

* `multieditorfield`

   これにより、複数行エディターが動作するために必要なすべての非表示フィールドが追加されます。このフィールドは、**複数行テキスト**&#x200B;データ型で表されます。

* `mvfields`

   マルチフィールドコンポーネントの動作に必要なすべての非表示フィールドを追加するコンポーネント。 例えば、**1行のテキスト**&#x200B;データ型の2番目のオプションの場合、 これは、マルチフィールドとしてレンダリングされるすべてのコンポーネントに対して追加する必要があります。

* `numbertypefield`

   **数値**&#x200B;データ型のオプションを選択します。**整数**&#x200B;または&#x200B;**分数**&#x200B;を、**数値**&#x200B;データ型として選択します。

* `numbervaluefield`

   **数値** `type.options`用の`numberfield`デフォルト値セレクター。これにより、**列挙**&#x200B;データ型のオプション入力が追加され、選択ボックスコンポーネントの値を決定するのに使用されます。

* `placeholderfield`

   これは、コンポーネントの`emptyText`プロパティの入力として機能するテキストフィールドです。 これは、プレースホルダーを受け取るすべてのデータ型で使用する必要があります（あまり複雑ではありません）。例：**1行のテキスト**、**数値**&#x200B;など)。

* `renderasfield`

   これは、データタイプノードのプロパティに複数の`fieldResourceTypes`が存在する場合に、自動的にレンダリングされるコンポーネントです。

* `requiredfield`

   これは、コンポーネントの`required`プロパティを表すチェックボックスです。 ほとんどのコンポーネントは`required`フィールドを受け入れるので、このフィールドはほとんどのデータ型で使用できます。

* `tagsfields`

   `tagfield`コンポーネントをレンダリングするために必要な入力を追加するコンポーネント。**タグ**&#x200B;データタイプで使用されます。

* `tagsroot`

   **タグ**&#x200B;データ型で`tagsfield`コンポーネントのルートパスを設定するために使用されるパスピッカー。

* `textfield`

   `Boolean`データ型で使用され、このデータ型で定義されるチェックボックスのフィールドラベルを設定します。

* `textvaluefield`

   **1行のテキスト**&#x200B;データ型のデフォルト値プロパティ。

## データタイプ{#creating-your-data-type}の作成

独自のデータ型を作成するには、次の操作が必要です。

* [ノード構造の作成](#creating-the-node-structure)
* [データタイプのプロパティの定義](#defining-the-properties-for-your-data-type)

その後、[データ型](#using-your-data-type)を使用できます。

[独自の`fieldProperties`](#creating-your-own-fieldproperties-property)を作成することもできます。

### ノード構造の作成{#creating-the-node-structure}

データ型をオーバーレイするには、`/apps`の下にノード構造を作成する必要があります。 まだ存在しない場合は、次を作成する必要があります。

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

1. `/items`の下に、新しいデータ型を表す新しいノードを追加できます。

   * ノードタイプ：`nt:unstructured`
   * 「プロパティ：[データ型のプロパティの定義](#defining-the-properties-for-your-data-type)を参照してください。

### データ型{#defining-the-properties-for-your-data-type}のプロパティの定義

1. 使用するデータ型に必要な次の[データ型プロパティ](#data-type-properties)の値を決定します。

   * `fieldResourceType`
   * `fieldPropResourceType`
   * `fieldViewResourceType`

   これらは、データタイプのコンポーネントのレンダリング方法を定義します。 どのコンポーネントでもかまいません。独自のカスタムコンポーネントを含めます（` [fieldProperties](#fieldproperties)`と一致するセットが必要です）。

   これらのプロパティを適切な値で、データ型のノードに定義します。

1. 使用する` [fieldProperties](#fieldproperties)`を決定します。 これは、`fieldResourceType`で必要な属性やプロパティによって異なります。

   例えば、`granite/ui/components/coral/foundation/form/textfield`には、**ラベル名**、**最大長**、**プレースホルダーテキスト**、**デフォルト値**&#x200B;の各プロパティが必要です。

   標準の[fieldProperties](#fieldproperties)から選択するか、[独自のプロパティ](#creating-your-own-fieldproperties-property)を作成します。

   これらのプロパティを適切な値で、データ型のノードに定義します。

1. 次の[データタイププロパティ](#data-type-properties)の値を決定します。

   * `fieldIcon`
   * `fieldTitle`
   * `renderType`
   * `valueType`
   * `listOrder`

   これらのプロパティを適切な値で、データ型のノードに定義します。

### データタイプ{#using-your-data-type}の使用

このノード構造を保存した後、すべてのプロパティを適用した状態で、モデルエディターで任意のモデルを開き、新しいデータ型を表示して使用できます。

## 独自のfieldPropertiesプロパティ{#creating-your-own-fieldproperties-property}の作成

標準の[fieldProperties](#fieldproperties)から選択するか、独自のを作成できます。

1. 次の場所にコンポーネントを作成します。

   `/apps/dam/cfm/models/editor/components/datatypeproperties/`

   パスが存在しない場合は、`nt:folder`ノードを使用してパスを作成できます。

   1. 変数にアクセスするには、このコンポーネントで次の要素を拡張する必要があります。

      `/libs/dam/cfm/models/editor/components/datatypeproperties/base`* *

   1. コンポーネントは、次の方法で含めることができます。

      `sling:include`

   1. このコンポーネントは、フィールド（ユーザーがデータを導入する必要がある場合）またはデータタイプで必要なプロパティを含む非表示の入力をレンダリングする必要があります。 例えば、マルチフィールドコンポーネントには、複製するフィールドのタイプを持つ子ノードが必要なので、(SlingPOSTメカニズムを通じて)特定のタイプの子ノードを作成できる入力が必要です。

1. このコンポーネントのベース名は`fieldProperties`に追加する必要があります。
1. 必要なすべてのプロパティに対して繰り返します。

