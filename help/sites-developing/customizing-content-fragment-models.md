---
title: 公開しないが、コンテンツフラグメントモデルのカスタマイズをDELETEしない
seo-title: Customizing Content Fragment Models
description: コンテンツフラグメントモデルは、カスタマイズおよび拡張できます。
seo-description: Content Fragment Models can be customized and extended.
page-status-flag: de-activated
uuid: 5bcfb5d8-37d4-4a0e-882d-bc8a1bac6ba7
contentOwner: aheimoz
discoiquuid: 208225ee-9052-4a45-9cfd-f8d27d4d70ed
noindex: true
source-git-commit: b61c20c65ceade0153f5cd04fbedfd02e919d483
workflow-type: tm+mt
source-wordcount: '586'
ht-degree: 13%

---


# 公開しないが、コンテンツフラグメントモデルのカスタマイズをDELETEしない{#do-not-publish-but-do-not-delete-customizing-content-fragment-models}

コンテンツフラグメントモデルエディターは、 `Formbuilder`、から継承：

`granite/ui/components/foundation/form/formbuilder`

このコンポーネントには、モデルエディターのドラッグ&amp;ドロップインターフェイスをレンダリングするために必要なツールがあり、それぞれのデータタイプとプロパティを備えています。

## ロケーション {#locations}

モデルは、の下に保存および作成されます。 `/conf`( [コンテンツフラグメントモデルのプロパティ](/help/assets/content-fragments-models.md#enable-content-fragment-models) 有効。 この設定は、 **設定プロパティ**（からアクセス可能） **[設定ブラウザー](/help/sites-administering/configurations.md)**.

1. 次を使用してブラウザーに移動します。 **ツール**, **一般**, **設定ブラウザー**
例： 
`http://localhost:4502/libs/granite/configurations/content/view.html/conf`

1. ブラウザーから、適切な設定を選択し、 **プロパティ** をクリックします。

   例えば、 `global`: `http://localhost:4502/libs/granite/configurations/content/edit.html/conf/global`

モデルコンソールで、 **コンテンツフラグメントモデル** プロパティが表示されます。 次の場所に移動： **ツール**, **Assets**, **コンテンツフラグメントモデル**;例： `http://localhost:4502/libs/dam/cfm/models/console/content/models.html/conf`.

ユーザーが [コンテンツフラグメントモデルの作成](/help/assets/content-fragments-models.md#creating-a-content-fragment-model) の使用 **モデルを作成** ウィザード ( 使用 **作成** （コンソールから）。

>[!CAUTION]
>
>`/libs` パス内の設定は&#x200B;***一切***&#x200B;変更しないでください。
>
>`/libs` のコンテンツは、インスタンスを次回アップグレードするとき（場合によってはホットフィックスまたは機能パックを適用したとき）に上書きされるからです。

## モデルの構造 {#structure-of-a-model}

ウィザードは、次の構造を持つエントリを作成します。

![cf-54](assets/cf-54.png)

* `../settings/dam/cfm/models`

   すべてのモデルは、このフォルダーのサブフォルダーに保存されます。

* `jcr:content`

   すべてのモデルには `jcr:content` 次のノードに設定します。

   * には、次のようなモデルに関する情報プロパティが含まれます。 `jcr:title`, `lastModified`, `lastModifiedBy`
   * 通常は `sling:ResourceType` / `dam/cfm/models/console/components/data/entity/default`,

      と `sling:ResourceSuperType` / `dam/cfm/models/console/components/data/entity`

* `model`

   この `model` ノードにプロパティが含まれる `dataTypesConfig`：モデルエディターで使用するデータタイプを決定するために使用されます。

* `items`

   以下 `items` ノードに追加したすべてのデータタイプが（モデルエディターでドラッグ&amp;ドロップして）保存されます。 各項目にはランダムなノード名が付けられますが、コンテンツフラグメントエディターがこのモデルで機能するには、各項目に `name` プロパティ。 さらに、このノードでは、特定のデータ型の設定プロパティがすべて保存されます。これには、コンポーネントのレンダリングに必要なデフォルトのプロパティも含まれます。

>[!CAUTION]
>
>モデルエディターでドラッグ&amp;ドロップしたすべてのデータタイプ、およびインスタンス化された **必須** 持っている `name` ユーザーが入力したプロパティ。
>
>これは、 **プロパティ名&amp;ast;** 内 **プロパティ** 」タブをクリックします。

## モデルエディターの構造 {#structure-of-the-model-editor}

この **コンテンツフラグメントモデルエディター** には 2 つの部分があります。

* 左側のプレビュー（ビュー）パネルで項目をドロップできます。 この特徴は次のとおりです。

   * 次のプレビューを表示： **データタイプ** がインスタンス化されている。
   * モデルエディタ内での並べ替えを許可します。

* この **データタイプ**/**プロパティ** タブを使用して、ページの右側に表示されます。 この特徴は次のとおりです。

   * ドラッグおよびインスタンス化が可能なデータ型のリストを表示します。
   * 標準モデルエディターの場合、リストは次の場所に表示されます。

      `/libs/settings/dam/cfm/models/formbuilderconfig/datatypes`

      <!-- Please uncomment when file is used
      This node contains all the data types currently supported in the model editor. For more information on how to configure the data types, see [Customizing Data Types for Content Fragment Models](/help/sites-developing/customizing-content-fragment-model-data-types.md).
      -->

   * すべてのレンダリングされたデータタイプには、インスタンス化の際にビュー（左側にレンダリングされるコンポーネント）を形成する 2 つのスクリプトタグと **プロパティ** タブ：特定のコンポーネントに対してユーザーが定義できるプロパティを定義します。

>[!CAUTION]
>
>`/libs` パス内の設定は&#x200B;***一切***&#x200B;変更しないでください。
>
>`/libs` のコンテンツは、インスタンスを次回アップグレードするとき（場合によってはホットフィックスまたは機能パックを適用したとき）に上書きされるからです。

<!-- Please uncomment when files are used
The properties on the right side define a form that is submitted directly into JCR under `/conf`; see the path in the example [Structure of a Model](/help/sites-developing/customizing-content-fragment-models.md#structure-of-a-model).
-->

データタイプがインスタンス化されると、HTML入力が作成され、コンポーネントをコンテンツフラグメントにレンダリングする必要があるプロパティごとに作成されます。 例えば、次のようなものがあります。

* **プロパティ名&amp;ast;** ( `name`) — コンポーネントの識別子として機能します

* **レンダリング形式** ( `metaType`) — レンダリングするコンポーネントを

* **説明** ( `fieldDescription`) — コンテンツフラグメント内のコンポーネントの説明

* その他.

