---
title: 公開しないが、コンテンツフラグメントモデルのカスタマイズをDELETEしない
seo-title: コンテンツフラグメントモデルのカスタマイズ
description: コンテンツフラグメントモデルは、カスタマイズおよび拡張できます。
seo-description: コンテンツフラグメントモデルは、カスタマイズおよび拡張できます。
page-status-flag: de-activated
uuid: 5bcfb5d8-37d4-4a0e-882d-bc8a1bac6ba7
contentOwner: aheimoz
discoiquuid: 208225ee-9052-4a45-9cfd-f8d27d4d70ed
noindex: true
source-git-commit: b61c20c65ceade0153f5cd04fbedfd02e919d483
workflow-type: tm+mt
source-wordcount: '598'
ht-degree: 3%

---


# 公開しないが、コンテンツフラグメントモデルのカスタマイズをDELETEしない{#do-not-publish-but-do-not-delete-customizing-content-fragment-models}

コンテンツフラグメントモデルエディターは、`Formbuilder`に基づくウィザードで、次の場所から継承されます。

`granite/ui/components/foundation/form/formbuilder`

このコンポーネントには、モデルエディターのドラッグ&amp;ドロップインターフェイスをレンダリングするために必要なツールがあり、それぞれのデータタイプとプロパティを含みます。

## ロケーション {#locations}

モデルは`/conf`の下に保存され、[コンテンツフラグメントモデルプロパティ](/help/assets/content-fragments-models.md#enable-content-fragment-models)が有効なフォルダーに作成されます。 この設定は、**設定プロパティ**（**[設定ブラウザー](/help/sites-administering/configurations.md)**&#x200B;からアクセス可能）でも確認できます。

1. **ツール**、**一般**、**設定ブラウザー**からブラウザーに移動します。
例： 
`http://localhost:4502/libs/granite/configurations/content/view.html/conf`

1. ブラウザーで適切な設定を選択し、ツールバーの「**プロパティ**」を選択します。

   例えば、`global`のプロパティは次のようになります。`http://localhost:4502/libs/granite/configurations/content/edit.html/conf/global`

モデルコンソールに、**コンテンツフラグメントモデル**&#x200B;プロパティを持つすべてのフォルダーが表示されます。 **ツール**、**アセット**、**コンテンツフラグメントモデル**&#x200B;を使用して移動します。例： `http://localhost:4502/libs/dam/cfm/models/console/content/models.html/conf`

ユーザーは、 **モデルを作成**&#x200B;ウィザードを使用して（コンソールの&#x200B;**作成**&#x200B;を使用して）、コンテンツフラグメントモデル[を作成できます。](/help/assets/content-fragments-models.md#creating-a-content-fragment-model)

>[!CAUTION]
>
>`/libs` パス内の設定は&#x200B;***一切***&#x200B;変更しないでください。
>
>これは、`/libs`のコンテンツが次回インスタンスをアップグレードすると（ホットフィックスまたは機能パックを適用すると上書きされる場合がある）ときに上書きされるからです。

## モデルの構造{#structure-of-a-model}

ウィザードは、次の構造を持つエントリを作成します。

![cf-54](assets/cf-54.png)

* `../settings/dam/cfm/models`

   すべてのモデルは、このフォルダーのサブフォルダーに保存されます。

* `jcr:content`

   すべてのモデルには、以下の`jcr:content`ノードが含まれます。

   * には、`jcr:title`、`lastModified`、`lastModifiedBy`など、モデルに関する情報プロパティが含まれます。
   * 通常、`sling:ResourceType`は`dam/cfm/models/console/components/data/entity/default`、

      `sling:ResourceSuperType`が`dam/cfm/models/console/components/data/entity`の

* `model`

   `model`ノードには、モデルエディターで使用されるデータタイプを決定するために使用されるプロパティ`dataTypesConfig`が含まれます。

* `items`

   `items`ノードの下に、モデルに追加されたすべてのデータタイプが（モデルエディターでドラッグ&amp;ドロップして）保存されます。 各項目にはランダムなノード名が付けられますが、コンテンツフラグメントエディターでこのモデルを使用するには、各項目に`name`プロパティが必要です。 さらに、このノードでは、コンポーネントのレンダリングに必要なデフォルトのプロパティを含め、特定のデータタイプのすべての設定プロパティが保存されます。

>[!CAUTION]
>
>モデルエディターでドラッグ&amp;ドロップしたすべてのデータ型。インスタンス化のため、****&#x200B;には、ユーザーが`name`プロパティを入力する必要があります。
>
>これは、モデルエディターの「**プロパティ**」タブに「**プロパティ名&amp;ast;**」と表示されます。

## モデルエディタの構造{#structure-of-the-model-editor}

**コンテンツフラグメントモデルエディター**&#x200B;には、次の2つの部分があります。

* 左側のプレビュー（ビュー）パネル（項目をドロップできます）。 このスケーリングは：

   * インスタンス化された&#x200B;**データタイプ**&#x200B;のプレビューを表示します。
   * モデルエディタ内での順序付けを許可します。

* 右側のパネルにある「**データタイプ**/**プロパティ**」タブ。 このスケーリングは：

   * ドラッグおよびインスタンス化が可能なデータ型のリストを表示します。
   * 標準モデルエディターの場合、リストは次の場所に表示されます。

      `/libs/settings/dam/cfm/models/formbuilderconfig/datatypes`

      <!-- Please uncomment when file is used
      This node contains all the data types currently supported in the model editor. For more information on how to configure the data types, see [Customizing Data Types for Content Fragment Models](/help/sites-developing/customizing-content-fragment-model-data-types.md).
      -->

   * すべてのレンダリングされたデータ型には、インスタンス化の際にビュー（左側にレンダリングされるコンポーネント）と&#x200B;**「プロパティ**」タブを形成する2つのスクリプトタグがあります。このタブは、特定のコンポーネントに対してユーザーが定義できます。

>[!CAUTION]
>
>`/libs` パス内の設定は&#x200B;***一切***&#x200B;変更しないでください。
>
>これは、`/libs`のコンテンツが次回インスタンスをアップグレードすると（ホットフィックスまたは機能パックを適用すると上書きされる場合がある）ときに上書きされるからです。

<!-- Please uncomment when files are used
The properties on the right side define a form that is submitted directly into JCR under `/conf`; see the path in the example [Structure of a Model](/help/sites-developing/customizing-content-fragment-models.md#structure-of-a-model).
-->

データタイプをインスタンス化する場合、コンポーネントをコンテンツフラグメントにレンダリングする必要があるプロパティごとにHTML入力が作成されます。 例えば、次のものが含まれます。

* **プロパティ名&amp;ast;** ( `name`) — コンポーネントの識別子として機能します

* **レンダリング形式** ( `metaType`) — レンダリングするコンポーネントを

* **説明** ( `fieldDescription`) — コンテンツフラグメント内のコンポーネントの説明

* その他.

