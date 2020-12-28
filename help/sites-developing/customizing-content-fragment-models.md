---
title: コンテンツフラグメントモデルのカスタマイズはDELETEしないで公開してください。
seo-title: コンテンツフラグメントモデルのカスタマイズ
description: コンテンツフラグメントモデルは、カスタマイズおよび拡張が可能です。
seo-description: コンテンツフラグメントモデルは、カスタマイズおよび拡張が可能です。
page-status-flag: de-activated
uuid: 5bcfb5d8-37d4-4a0e-882d-bc8a1bac6ba7
contentOwner: aheimoz
discoiquuid: 208225ee-9052-4a45-9cfd-f8d27d4d70ed
noindex: true
translation-type: tm+mt
source-git-commit: b61c20c65ceade0153f5cd04fbedfd02e919d483
workflow-type: tm+mt
source-wordcount: '598'
ht-degree: 3%

---


# 公開しないが、コンテンツフラグメントモデルのカスタマイズをDELETEしない{#do-not-publish-but-do-not-delete-customizing-content-fragment-models}

コンテンツフラグメントモデルエディターは、`Formbuilder`に基づくウィザードで、次のファイルから継承されます。

`granite/ui/components/foundation/form/formbuilder`

このコンポーネントには、モデルエディタのドラッグ&amp;ドロップインターフェイスをレンダリングするのに必要なツールが用意されており、それぞれのデータタイプとプロパティを完成させます。

## ロケーション {#locations}

モデルは、`/conf`の下、[Content Fragment Modelsプロパティ](/help/assets/content-fragments-models.md#enable-content-fragment-models)が有効なフォルダーの下に保存され、作成されます。 この設定は、**構成プロパティ**&#x200B;でも確認できます。このプロパティは、**[構成ブラウザー](/help/sites-administering/configurations.md)**&#x200B;からアクセスできます。

1. **ツール**、**一般**、**構成ブラウザー**を介してブラウザーに移動します。
例えば、 
`http://localhost:4502/libs/granite/configurations/content/view.html/conf`

1. ブラウザーから適切な設定を選択し、ツールバーから&#x200B;**プロパティ**&#x200B;を選択します。

   例えば、`global`のプロパティは次のようになります。`http://localhost:4502/libs/granite/configurations/content/edit.html/conf/global`

モデルコンソールに、**Content Fragment Models**&#x200B;プロパティが設定されたすべてのフォルダーが表示されます。 **ツール**、**アセット**、**コンテンツフラグメントモデル**&#x200B;を使用して移動します。例：`http://localhost:4502/libs/dam/cfm/models/console/content/models.html/conf`

ユーザーは、**モデルを作成**&#x200B;ウィザード（コンソールから&#x200B;**作成**&#x200B;を使用）を使用して、[コンテンツフラグメントモデル](/help/assets/content-fragments-models.md#creating-a-content-fragment-model)を作成できます。

>[!CAUTION]
>
>`/libs` パス内の設定は&#x200B;***一切***&#x200B;変更しないでください。
>
>これは、次回インスタンスをアップグレードする際に`/libs`の内容が上書きされるためです（修正プログラムまたは機能パックを適用すると、上書きされる場合があります）。

## モデルの構造{#structure-of-a-model}

ウィザードは、次の構造を持つエントリを作成します。

![cf-54](assets/cf-54.png)

* `../settings/dam/cfm/models`

   すべてのモデルが、このフォルダーのサブフォルダーの下に保存されます。

* `jcr:content`

   すべてのモデルには、次のような`jcr:content`ノードが含まれています。

   * `jcr:title`、`lastModified`、`lastModifiedBy`など、モデルに関する情報プロパティが含まれます
   * 通常は`sling:ResourceType`が`dam/cfm/models/console/components/data/entity/default`で、

      `sling:ResourceSuperType`/`dam/cfm/models/console/components/data/entity`の

* `model`

   `model`ノードにはプロパティ`dataTypesConfig`が含まれ、モデルエディタで使用するデータタイプを決定するために使用されます。

* `items`

   `items`ノードの下に、モデルに追加されたすべてのデータ型が保存されます（モデルエディターでドラッグ&amp;ドロップしたとき）。 各項目にはランダムなノード名が与えられますが、コンテンツフラグメントエディターでこのモデルを使用するには、各項目に`name`プロパティが必要です。 また、このノードでは、コンポーネントのレンダリングに必要なデフォルトのプロパティを含む、特定のデータ型のすべての設定プロパティが保存されます。

>[!CAUTION]
>
>モデルエディターでドラッグ&amp;ドロップしたすべてのデータ型、およびそのインスタンス化のため、****&#x200B;には、ユーザーが入力する`name`プロパティが必要です。
>
>これは、モデルエディターの&#x200B;**プロパティ**&#x200B;タブにある&#x200B;**プロパティ名&amp;ast;**&#x200B;と表示されます。

## モデルエディタの構造{#structure-of-the-model-editor}

**コンテンツフラグメントモデルエディター**&#x200B;は、次の2つの部分で構成されています。

* 左側のプレビュー(表示)パネル。項目をドロップできます。 このスケーリングは：

   * インスタンス化される&#x200B;**データタイプ**&#x200B;のプレビューを表示します。
   * モデルエディタ内での順序付けを許可します。

* 右側のパネルの「**データタイプ**/**プロパティ**」タブ このスケーリングは：

   * ドラッグしてインスタンス化できるデータ型のリストを表示します。
   * 標準搭載のモデルエディターの場合、リストは次の場所にあります。

      `/libs/settings/dam/cfm/models/formbuilderconfig/datatypes`

      <!-- Please uncomment when file is used
      This node contains all the data types currently supported in the model editor. For more information on how to configure the data types, see [Customizing Data Types for Content Fragment Models](/help/sites-developing/customizing-content-fragment-model-data-types.md).
      -->

   * すべてのレンダリングされたデータ型には、インスタンス化の際に表示（左側にレンダリングされるコンポーネント）と&#x200B;**「プロパティ**」タブを形成する2つのスクリプトタグがあり、これらは特定のコンポーネントに対してユーザーが定義できるプロパティを定義します。

>[!CAUTION]
>
>`/libs` パス内の設定は&#x200B;***一切***&#x200B;変更しないでください。
>
>これは、次回インスタンスをアップグレードする際に`/libs`の内容が上書きされるためです（修正プログラムまたは機能パックを適用すると、上書きされる場合があります）。

<!-- Please uncomment when files are used
The properties on the right side define a form that is submitted directly into JCR under `/conf`; see the path in the example [Structure of a Model](/help/sites-developing/customizing-content-fragment-models.md#structure-of-a-model).
-->

データタイプをインスタンス化する場合、コンポーネントをコンテンツフラグメント内にレンダリングする必要があるプロパティごとにHTML入力が作成されます。 例えば、次のように指定します。

* **プロパティ名(&amp;ast);** ( `name`) — コンポーネントの識別子として機能します。

* **Render As** ( `metaType`) — レンダリングするコンポーネントを

* **説明** ( `fieldDescription`) — コンテンツフラグメント内のコンポーネントの説明

* その他.

