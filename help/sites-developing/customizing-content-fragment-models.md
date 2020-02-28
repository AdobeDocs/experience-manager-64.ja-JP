---
title: コンテンツフラグメントモデルのカスタマイズは公開しないが削除しない
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

---


# コンテンツフラグメントモデルのカスタマイズは公開しないが削除しない{#do-not-publish-but-do-not-delete-customizing-content-fragment-models}

コンテンツフラグメントモデルエディターは、次のファイルに基づくウィザ `Formbuilder`ードです。

`granite/ui/components/foundation/form/formbuilder`

このコンポーネントには、モデルエディターのドラッグ&amp;ドロップインターフェイスをレンダリングするのに必要なツールが用意されており、それぞれのデータタイプとプロパティが完成しています。

## ロケーション {#locations}

モデルは、「コンテンツフラグメントモデル」プ `/conf`ロパティが有効なフォルダーの下に [保存され、作成されます](/help/assets/content-fragments-models.md#enable-content-fragment-models) 。 この設定は、設定ブラウザーからアク **セスできる**「設定プロパティ」でも **確認できます**。

1. ツール、一般、設定ブラウ **ザー**(例： **ツ**&#x200B;ール **)を使**&#x200B;用してブラウザーに移動します。 `http://localhost:4502/libs/granite/configurations/content/view.html/conf`

1. ブラウザで適切な設定を選択し、ツールバーから **「Properties** 」を選択します。

   例えば、次のプロパティがありま `global`す。 `http://localhost:4502/libs/granite/configurations/content/edit.html/conf/global`

モデルコンソールに、 **Content Fragment Modelsプロパティを持つすべてのフォ** ルダーが表示されます。 ツール、アセ **ット**、コ **ンテン**&#x200B;ツフラグメントモデル ****、例えば、 `http://localhost:4502/libs/dam/cfm/models/console/content/models.html/conf`.

ユーザーは、モデル [を作成ウィザード](/help/assets/content-fragments-models.md#creating-a-content-fragment-model) (コンソールから「作 **成」を使用****** )を使用して、コンテンツフラグメントモデルを作成できます。

>[!CAUTION]
>
>You ***must*** not change anything in the `/libs` path.
>
>This is because the content of `/libs` is overwritten the next time you upgrade your instance (and may be overwritten when you apply either a hotfix or feature pack).

## モデルの構造 {#structure-of-a-model}

ウィザードは、次の構造を持つエントリを作成します。

![cf-54](assets/cf-54.png)

* `../settings/dam/cfm/models`

   すべてのモデルは、このフォルダのサブフォルダに保存されます。

* `jcr:content`

   すべてのモデルには、次のようなノード `jcr:content` が含まれています。

   * には、、などのモデルに関する情報プロパティが含ま `jcr:title`れま `lastModified`す。 `lastModifiedBy`
   * 通常は `sling:ResourceType` ～ `dam/cfm/models/console/components/data/entity/default`の

      ～と共 `sling:ResourceSuperType` に `dam/cfm/models/console/components/data/entity`

* `model`

   ノード `model` には、モデルエディタ `dataTypesConfig`ーで使用するデータタイプを決定するために使用されるプロパティが含まれます。

* `items`

   ノードの下 `items` に、モデルに追加されたすべてのデータ型が保存されます（モデルエディターでドラッグ&amp;ドロップした状態）。 各項目にはランダムなノード名が割り当てられますが、コンテンツフラグメントエディターがこのモデルで機能するには、各項目にプロパティが必要 `name` です。 さらに、このノードでは、特定のデータタイプの設定プロパティがすべて保存され、コンポーネントのレンダリングに必要なデフォルトのプロパティも含まれます。

>[!CAUTION]
>
>モデルエディターでドラッグ&amp;ドロップしたすべてのデータ型、およびインスタンス化されたデータ型の場合 **は** 、ユーザーがプ `name` ロパティを入力する必要があります。
>
>**これは、** Property Name &amp;ast；と表示されます。モデルエデ **ィタの** 「プロパティ」タブで、

## モデルエディタの構造 {#structure-of-the-model-editor}

コンテンツ **フラグメントモデルエディターには** 、次の2つの部分があります。

* 左側のプレビュー（ビュー）パネル。項目をドロップできます。 このクライアントライブラリは:

   * インスタンス化されるデータ **型のプレビュー** を表示します。
   * モデルエディター内での順序付けを許可します。

* 右側 **のパネルの「** Data Types **/** Properties」タブ。 このクライアントライブラリは:

   * ドラッグしてインスタンス化できるデータ型のリストを表示します。
   * 標準搭載のモデルエディターの場合、リストは次の場所にあります。

      `/libs/settings/dam/cfm/models/formbuilderconfig/datatypes`

      <!-- Please uncomment when file is used
      This node contains all the data types currently supported in the model editor. For more information on how to configure the data types, see [Customizing Data Types for Content Fragment Models](/help/sites-developing/customizing-content-fragment-model-data-types.md).
      -->

   * すべてのレンダリングされたデータ型には2つのスクリプトタグがあり、インスタンス化するとビュー（左側にレンダリングされたコンポーネント）が形成され、「 **Properties** 」タブが定義されます。このタブは、特定のコンポーネントに対してユーザーが定義できるプロパティを定義します。

>[!CAUTION]
>
>You ***must*** not change anything in the `/libs` path.
>
>This is because the content of `/libs` is overwritten the next time you upgrade your instance (and may be overwritten when you apply either a hotfix or feature pack).

<!-- Please uncomment when files are used
The properties on the right side define a form that is submitted directly into JCR under `/conf`; see the path in the example [Structure of a Model](/help/sites-developing/customizing-content-fragment-models.md#structure-of-a-model).
-->

データ型をインスタンス化する場合、コンポーネントをコンテンツフラグメントにレンダリングする必要があるすべてのプロパティに対してHTML入力が作成されます。 例えば、次のように指定します。

* **** プロパティ名(&amp;A);ast;( `name`) — コンポーネントの識別子として機能します。

* **Render As** ( `metaType`) — レンダリングするコンポーネントを

* **説明** ( `fieldDescription`) — コンテンツフラグメント内のコンポーネントの説明

* その他.

