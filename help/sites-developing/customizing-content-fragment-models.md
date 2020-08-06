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
source-git-commit: 3bdff366a0d455b405c1f9de371ced98d25ae2e2
workflow-type: tm+mt
source-wordcount: '598'
ht-degree: 3%

---


# コンテンツフラグメントモデルのカスタマイズはDELETEしないで公開してください。{#do-not-publish-but-do-not-delete-customizing-content-fragment-models}

コンテンツフラグメントモデルエディターは、次のファイルに基づくウィザード `Formbuilder`です。

`granite/ui/components/foundation/form/formbuilder`

このコンポーネントには、モデルエディタのドラッグ&amp;ドロップインターフェイスをレンダリングするのに必要なツールが用意されており、それぞれのデータタイプとプロパティを完成させます。

## ロケーション {#locations}

モデルは、「 `/conf`コンテンツフラグメントモデル」プロパティが有効なフォルダーの下 [に保存され、作成されます](/help/assets/content-fragments-models.md#enable-content-fragment-models) 。 この設定は、 **設定ブラウザーからアクセスできる**&#x200B;設定プロパティ **でも確認できます**。

1. 「 **ツール**」、「 **一般」、「**&#x200B;設定ブラウザー」な ****&#x200B;どを使用してブラウザーに移動します。 
`http://localhost:4502/libs/granite/configurations/content/view.html/conf`

1. ブラウザーで適切な設定を選択し、ツールバーの「 **プロパティ** 」を選択します。

   例えば、次のプロパティがあり `global`ます。 `http://localhost:4502/libs/granite/configurations/content/edit.html/conf/global`

モデルコンソールに、「 **コンテンツフラグメントモデル** 」プロパティを持つすべてのフォルダーが表示されます。 **ツール**、 **アセット**、 **コンテンツフラグメントモデルを使用した移動**、 例えば、 `http://localhost:4502/libs/dam/cfm/models/console/content/models.html/conf`。

ユーザーは、「モデルを [作成](/help/assets/content-fragments-models.md#creating-a-content-fragment-model) 」ウィザード(コンソールから「 **作成** 」を使用)を使用して、コンテンツフラグメントモデルを **** 作成できます。

>[!CAUTION]
>
>`/libs` パス内の設定は&#x200B;***一切***&#x200B;変更しないでください。
>
>This is because the content of `/libs` is overwritten the next time you upgrade your instance (and may be overwritten when you apply either a hotfix or feature pack).

## モデルの構造 {#structure-of-a-model}

ウィザードは、次の構造を持つエントリを作成します。

![cf-54](assets/cf-54.png)

* `../settings/dam/cfm/models`

   すべてのモデルが、このフォルダーのサブフォルダーの下に保存されます。

* `jcr:content`

   すべてのモデルには、次のような `jcr:content` ノードが含まれます。

   * には、 `jcr:title`、などのモデルに関する情報プロパティが含まれ `lastModified`ます。 `lastModifiedBy`
   * 通常は `sling:ResourceType``dam/cfm/models/console/components/data/entity/default`の

      ～と共に `sling:ResourceSuperType` `dam/cfm/models/console/components/data/entity`

* `model`

   ノードにはプロパティが含まれ `model``dataTypesConfig`ており、モデルエディタで使用するデータタイプを決定するために使用されます。

* `items`

   ノードの下に、モデルに追加されたすべてのデータ型が保存されます（モデルエディターでドラッグ&amp;ドロップしたとき）。 `items` 各項目にはランダムなノード名が与えられますが、コンテンツフラグメントエディターがこのモデルで動作するようにするには、各項目に `name` プロパティが必要です。 また、このノードでは、コンポーネントのレンダリングに必要なデフォルトのプロパティを含む、特定のデータ型のすべての設定プロパティが保存されます。

>[!CAUTION]
>
>モデルエディターでドラッグ&amp;ドロップしたすべてのデータ型と、そのインスタンス化のために **、ユーザーが**`name` プロパティ入力を持つ必要があります。
>
>これは、 **プロパティ名&amp;ast；と見なされます。** (モデルエディタの **プロパティ** タブ)。

## モデルエディタの構造 {#structure-of-the-model-editor}

コン **テンツフラグメントモデルエディターには** 、次の2つの部分があります。

* 左側のプレビュー(表示)パネル。項目をドロップできます。 このスケーリングは：

   * インスタンス化される **データ型** (Data Type)のプレビューを表示します。
   * モデルエディタ内での順序付けを許可します。

* 右側のパネルの「 **データタイプ**/**プロパティ** 」タブ このスケーリングは：

   * ドラッグしてインスタンス化できるデータ型のリストを表示します。
   * 標準搭載のモデルエディターの場合、リストは次の場所にあります。

      `/libs/settings/dam/cfm/models/formbuilderconfig/datatypes`

      <!-- Please uncomment when file is used
      This node contains all the data types currently supported in the model editor. For more information on how to configure the data types, see [Customizing Data Types for Content Fragment Models](/help/sites-developing/customizing-content-fragment-model-data-types.md).
      -->

   * すべてのレンダリングされたデータ型には、インスタンス化の際に表示（左側にレンダリングされるコンポーネント）を形成する2つのscriptタグと、特定のコンポーネントに対してユーザーが定義できるプロパティを定義する「 **プロパティ** 」タブがあります。

>[!CAUTION]
>
>`/libs` パス内の設定は&#x200B;***一切***&#x200B;変更しないでください。
>
>This is because the content of `/libs` is overwritten the next time you upgrade your instance (and may be overwritten when you apply either a hotfix or feature pack).

<!-- Please uncomment when files are used
The properties on the right side define a form that is submitted directly into JCR under `/conf`; see the path in the example [Structure of a Model](/help/sites-developing/customizing-content-fragment-models.md#structure-of-a-model).
-->

データタイプをインスタンス化する場合、コンポーネントをコンテンツフラグメント内にレンダリングする必要があるプロパティごとにHTML入力が作成されます。 例えば、次のように指定します。

* **プロパティ名(&amp;amp);ast;** ( `name`) — コンポーネントの識別子として機能します。

* **Render As** ( `metaType`) — レンダリングするコンポーネントを

* **説明** ( `fieldDescription`) — コンテンツフラグメント内のコンポーネントの説明

* その他.

