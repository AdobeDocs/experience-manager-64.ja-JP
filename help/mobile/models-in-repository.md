---
title: リポジトリ内のモデル
seo-title: Models in Repository
description: null
seo-description: null
uuid: 54f81180-4178-4e33-a6f0-e9e6ea50798e
contentOwner: User
content-type: reference
discoiquuid: ae1a72f4-d8c1-4c75-ba2c-7322f3743b17
noindex: true
redirecttarget: /content/help/en/experience-manager/6-4/mobile/using/administer-mobile-apps
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '1364'
ht-degree: 2%

---


# リポジトリ内のモデル{#models-in-repository}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

>[!NOTE]
>
>Adobeは、単一ページアプリケーションのフレームワークベースのクライアントサイドレンダリング（React など）を必要とするプロジェクトでは、SPA Editor を使用することをお勧めします。 [詳細情報](/help/sites-developing/spa-overview.md)を参照してください。

モデルには、最終的にコンテンツサービスによってレンダリングされるプロパティを定義する一連のデータ型が含まれます。 また、データの整合性を確保するために、他のモデル間の関係も定義します。

開発者は、リポジトリのモデル構造に精通している必要があります。 アプリの要件に応じて、独自のモデルやエンティティを作成できます。

## モデルタイプの作成 {#creating-model-types}

の下に 2 つのシステム提供のモデルタイプがあります */libs/settings/mobileapps/model-types*. システムモデルタイプを上書きする場合は、 *mobileapps/model-types* 上書きを実行する設定ノードの下にノードを作成する必要があります。

例えば、 */conf/myconf1* および */conf/myconf2* でシステムモデルタイプを上書きする *conf1* ただし、 *mobileapps/model-types* ノードを *conf1*.

データタイプをモデルに追加できるようにするには、モデルタイプに「cq:Page」タイプの「scaffolding」という名前の子ノードと、次のリソースタイプが必要です。 *wcm/scaffolding/components/scaffolding*.

基礎モードページには、 *dataTypesConfig* プロパティを PageContent ノードに設定します。このタイプから作成されたデータタイプモデルが使用できることを示します。

>[!NOTE]
>
>A **基礎モード** は、モデルに基づいてエンティティが編集できるデータタイプを定義するページです。 各データタイプを設定して、UI でのフィールドの表示方法や、データ値の保持方法を定義することもできます。

### データタイプ設定 {#data-types-config}

データタイプ config ノードには、データタイプ項目のリストが含まれます。 各データタイプ項目では、データタイプがモデルエディターでどのように表示されるか、およびエンティティによる最終的なレンダリングのためにデータタイプを保持する方法を指定します。

| **プロパティ名** | **説明** |
|---|---|
| fieldIcon | データ型を表す CoralUI アイコンのクラス |
| fieldPropResourceType | データタイプを設定するためのすべてのプロパティをレンダリングするコンポーネント |
| fieldProperties | fieldPropResourceType が *mobileapps/caas/gui/components/models/editor/datatypes/field* |
| fieldResourceType | データタイプの永続化されたノードの resourceType（つまり、エンティティエディターでプロパティをレンダリングするコンポーネント） |
| fieldViewResourceType | モデルエディタービューでデータ型のレンダリングに使用するコンポーネント（このプロパティを省略した場合は fieldResourceType が使用されます） |
| fieldTitle | モデルエディターに表示するデータタイプの名前 |
| multiFieldResourceType | 複数値が選択されている場合に、永続化されたノードで使用するリソースタイプ |
| renderType | クライアントサイドレンダリングのヒントのレンダリング |

### データタイプ設定オーバーレイ {#data-types-config-overlay}

「dataTypesConfig」プロパティは、Sling リソースの結合をサポートします。 つまり、システムモデルタイプ（またはカスタムモデルタイプ）で使用されるデータタイプは、オーバーレイノードを使用してカスタマイズできます。

のオーバーレイ */libs/settings/mobileapps/models/formbuilderconfig/datatypes* を作成し、必要に応じてカスタマイズする必要があります。

例えば、fieldResourceType をカスタムコンポーネントに変更するために、String データ型のオーバーレイを追加できます。

Sling Resource Merges について詳しくは、を参照してください。 [AEMでの Sling Resource Merger の使用](/help/sites-developing/sling-resource-merger.md).

![chlimage_1-7](assets/chlimage_1-7.png)

### データタイプ {#data-types}

モデルデータ型は、フォームの投稿時に含めるデータを含めることができるフォームコンポーネントです。 データタイプコンポーネントは、必要に応じて複雑になる場合があります。 カスタムデータ型の例としては、特定の国の住所ブロックを使用し、プリミティブデータ型を使用して常に再作成する必要がないようにすることができます。

カスタムデータタイプの例としては、「/libs/mobileapps/caas/components/form/contentreference」を参照してください。

すべてのプリミティブデータタイプは、既存の Granite フォームコンポーネントを使用します。 詳しくは、 [https://docs.adobe.com/docs/en/aem/6-3/develop/ref/granite-ui/api/jcr_root/libs/granite/ui/components/coral/foundation/form/index.html](https://docs.adobe.com/docs/en/aem/6-3/develop/ref/granite-ui/api/jcr_root/libs/granite/ui/components/coral/foundation/form/index.html)

その後、任意のカスタムデータタイプをデータタイプ設定に追加して、モデルエディターで使用できます。

## モデルの作成 {#creating-models}

必要なモデルタイプとデータタイプの開発が完了したら、モデルの作成を開始できます。 作成者は最終的にモデルを使用して、データのレンダリングに使用するエンティティを作成します。

モデルの作成は、現在の設定に基づいて許可されたモデルタイプを選択し、タイトルと説明を指定することで構成されます。

ダッシュボードからのモデルの作成と管理については、 [モデルの作成](/help/mobile/administer-mobile-apps.md) （モバイルアプリのオーサリングセクション）を参照してください。

### モデルのプロパティ {#properties-of-a-model}

次の表に、モデルに定義されたプロパティを示します。

| **プロパティ名** | **説明** |
|---|---|
| モデルタイトル | モデルの名前 |
| 説明 | モデルの説明 |
| サムネール | モデルのサムネール画像 |
| モデルタイプ | モデルのタイプ（単純な文字列または実際のコンポーネントへのパスを指定できます） |
| 許可されている子 | このテンプレートの子として使用できるテンプレートのパス |
| 許可された親 | このテンプレートの親として使用できるテンプレートのパス |

>[!NOTE]
>
>この *許可された子* および *許可された親* プロパティは、ページテンプレートと同じルールに従います。 詳しくは、 [ページテンプレート](/help/sites-developing/page-templates-static.md).
>
>参照先 *モデルタイプ* プロパティ、すべてのモデルは、次のスーパータイプを持つ必要があります。 *mobileapps/caas/components/data/entity* ただし、サブタイプを持つことができます。このサブタイプを使用すると、コンテンツ配信をカスタマイズできます。 すべてのモデルタイプを一意にすることは、コンテンツサービスのクライアントがデータ内のオブジェクトを区別するのに役立ちます。

### モデルの編集 {#editing-a-model}

モデルを編集する際には、モデルに関連付けられた基礎モードダイアログフォームを開いて編集します。 一般に、基礎モードはモデルの子ノードですが、必要に応じて「cq:scaffolding」プロパティを使用してパスを指定することで、モデルの外側に配置できます。 異なるプロパティを持つ必要がある複数のモデル間で同じ基礎モードを共有する場合は、これが便利です。

モデルの基礎モードが配置されると、モデルエディターは「jcr:content/cq:dialog/content」の下にあるものをレンダリングします。 現在、クライアント側の FormBuilder エンジンでは、最大 3 列の固定レイアウトのみがサポートされています。 レンダリングされたフォームダイアログの右側に、データタイプ設定で指定されたすべてのデータタイプのリストが表示されます。 データタイプは、クリックして編集できます。 右側のレールが、選択したデータタイプの「プロパティ」タブに切り替わります。 新しいデータタイプは、プレビューキャンバスにドラッグして追加できます。 [ 保存 ] をクリックすると、変更がサーバに反映されます。 「キャンセル」(Cancel) をクリックすると、モデルエディタが閉じます。

>[!NOTE]
>
>すべてのモデルはテンプレートなので、すべてのAEMテンプレートルールに従います。 これにより、次のようなプロパティを使用できます。 *allowedParents*&#x200B;および *allowedChildren* プロパティ。 これらは、モデルに基づいて新しいエンティティを作成する際に有効です。 テンプレートルールを使用すると、エンティティの階層に応じた特定のモデルに基づいたエンティティのみを作成できます。
>
>ダッシュボードからモデルを編集する方法については、 [モデルの作成](/help/mobile/administer-mobile-apps.md) （モバイルアプリのオーサリングセクション）を参照してください。

### システムモデル {#system-models}

簡単なコンテンツ再利用のために、事前に定義された 2 種類のシステムモデルが用意されています。 これらのモデルは編集できません。

**ページモデル** ページモデルを使用すると、Sites の既存のコンテンツを、コンテンツサービスによる配信に再利用する簡単な方法が提供されます。

ページモデルに基づくエンティティの resourceType は次のとおりです。mobileapps/caas/components/data/pages

パス：サイトページへのパス。 このパス（およびその子）のコンテンツは、コンテンツサービスハンドラーによってレンダリングされます。

**アセットモデル** アセットモデルを使用すると、Assets の既存のコンテンツを、コンテンツサービスでの配信に再利用する簡単な方法が提供されます。

ページモデルに基づくエンティティの resourceType は次のとおりです。 *mobileapps/caas/components/data/assets に置き換えます。*

アセットリスト：Assets からのパスのリスト。 各アセットは、resourceType が *wcm/foundation/components/image*.

>[!NOTE]
>
>ダッシュボードからモデルを作成するためにこれらのテンプレートを使用する方法について詳しくは、 [モデルの作成](/help/mobile/administer-mobile-apps.md) （モバイルアプリのオーサリングセクション）を参照してください。
