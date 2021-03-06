---
title: ページオーサリングのカスタマイズ
seo-title: Customizing Page Authoring
description: AEM には、ページオーサリング機能のカスタマイズを可能にする様々なメカニズムがあります
seo-description: AEM provides various mechanisms to enable you to customize page authoring functionality
uuid: 9dc72d98-c5ff-4a00-b367-688ccf896526
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: 6825dcd6-fa75-4410-b6b2-e7bd4a391224
exl-id: d7617d8a-b9b1-4a55-a8b7-4bdf90fd6905
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '1360'
ht-degree: 77%

---

# ページオーサリングのカスタマイズ{#customizing-page-authoring}

>[!CAUTION]
>
>このドキュメントでは、最新のタッチ操作対応 UI でのページオーサリングのカスタマイズ方法について説明します。クラシック UI には適用されません。

AEM には、オーサーインスタンスのページオーサリング機能（および[コンソール](/help/sites-developing/customizing-consoles-touch.md)）をカスタマイズできる様々な仕組みが用意されています。

* Clientlibs

   clientlibs を使用すると、デフォルトの実装を拡張して新しい機能を実現し、標準の関数、オブジェクト、メソッドを再利用できます。 カスタマイズする際、独自のクライアントライブラリを `/apps.` 新しい clientlib では、次の要件を満たす必要があります。

   * オーサリングクライアントライブラリ `cq.authoring.editor.sites.page` を使用する必要があります。
   * 適切な `cq.authoring.editor.sites.page.hook` カテゴリに含める必要があります。

* オーバーレイ

   オーバーレイはノード定義に基づいており、 `/libs`) を `/apps`) をクリックします。 [Sling Resource Merger](/help/sites-developing/sling-resource-merger.md) は継承を許可しているので、オーバーレイを作成するときに、オリジナルの 1 対 1 のコピーは必要ありません。

>[!NOTE]
>
>詳しくは、[JS ドキュメント](https://helpx.adobe.com/jp/experience-manager/6-4/sites/developing/using/reference-materials/jsdoc/ui-touch/editor-core/index.html)を参照してください。

これらをさまざまな方法で使用して、AEM インスタンスのページオーサリング機能を拡張できます。一部については、以降で（大まかに）説明します。

>[!NOTE]
>
>詳しくは、次のセクションを参照してください。
>
>* [クライアントライブラリ](/help/sites-developing/clientlibs.md)の使用と作成
>* [オーバーレイ](/help/sites-developing/overlays.md)の使用と作成
>* [Granite](https://helpx.adobe.com/jp/experience-manager/6-4/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/index.html)
>* ページオーサリングに使用される構造について詳しくは、[AEM タッチ操作対応 UI の構造](/help/sites-developing/touch-ui-structure.md)を参照してください。

>
>このトピックについては、[AEM Gems](https://docs.adobe.com/content/ddc/en/gems.html) セッション - [User interface customization for AEM 6.0](https://helpx.adobe.com/experience-manager/kt/eseminars/gems/aem-user-interface-customization-for-aem6.html) でも説明しています。

>[!CAUTION]
>
>`/libs` パス内の設定は&#x200B;***一切***&#x200B;変更しないでください。
>
>`/libs` コンテンツは、インスタンスを次回アップグレードするとき（場合によってはホットフィックスまたは機能パックを適用したとき）に上書きされるからです。
>
>設定およびその他の変更に推奨される方法は次のとおりです。
>
>1. 必要な項目（内に存在）を再作成します。 `/libs`) `/apps`
>1. `/apps` 内で変更作業をおこないます。


## 新しいレイヤー（モード）の追加 {#add-new-layer-mode}

ページを編集するときに、さまざまな[モード](/help/sites-authoring/author-environment-tools.md#page-modes)を使用できます。これらのモードは、[レイヤー](/help/sites-developing/touch-ui-structure.md#layer)を使用して実装されます。これらにより、同じページコンテンツの異なるタイプの機能にアクセスできます。標準のレイヤーは、編集、プレビュー、注釈、開発者およびターゲット設定です。

### レイヤーの例：ライブコピーステータス {#layer-example-live-copy-status}

標準 AEM インスタンスは、MSM レイヤーを提供します。これは、[マルチサイト管理](/help/sites-administering/msm.md)に関連するデータにアクセスし、レイヤーでハイライトします。

実行中に表示するには、次の項目を編集します。 [We.Retail 言語コピー](/help/sites-developing/we-retail-globalized-site-structure.md) ページ（または他のライブコピーページ）を選択し、 **ライブコピーステータス** モード。

MSM レイヤーの定義（参照用）は、次のファイルにあります。

`/libs/wcm/msm/content/touch-ui/authoring/editor/js/msm.Layer.js`

### コードサンプル {#code-sample}

これは、MSM 表示用の新規レイヤー（モード）の作成方法を示す、サンプルパッケージです。

GitHub のコード

このページのコードは GitHub にあります

* [GitHub の aem-authoring-new-layer-mode プロジェクトを開きます](https://github.com/Adobe-Marketing-Cloud/aem-authoring-new-layer-mode)
* プロジェクトを [ZIP ファイル](https://github.com/Adobe-Marketing-Cloud/aem-authoring-new-layer-mode/archive/master.zip)としてダウンロードします

## 新しい選択カテゴリをアセットブラウザーに追加 {#add-new-selection-category-to-asset-browser}

アセットブラウザーには、さまざまなタイプまたはカテゴリのアセット（画像、ドキュメントなど）が表示されます。このようなアセットカテゴリを使用して、アセットをフィルターすることもできます。

### コードサンプル {#code-sample-1}

`aem-authoring-extension-assetfinder-flickr` は、新しいグループをアセットファインダーに追加する方法を示すサンプルパッケージです。このサンプルは、[Flickr](https://www.flickr.com) の公開ストリームに接続し、サイドパネルに表示します。

GitHub のコード

このページのコードは GitHub にあります

* [GitHub の aem-authoring-extension-assetfinder-flickr プロジェクトを開きます](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-assetfinder-flickr)
* プロジェクトを [ZIP ファイル](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-assetfinder-flickr/archive/master.zip)としてダウンロードします

## リソースのフィルタリング {#filtering-resources}

ページをオーサリングする際、ユーザーは頻繁にリソース（ページ、コンポーネント、アセットなど）から選択する必要があります。これは、例えば、作成者が項目を選択する必要があるリストの形式で表示されます。

特定の用途に関連する内容を持つ妥当なサイズのリストにするには、カスタム述語の形式でフィルターを実装できます。例えば、 [`pathbrowser`](https://helpx.adobe.com/jp/experience-manager/6-4/sites/developing/using/reference-materials/granite-ui/api/index.html) [Granite](/help/sites-developing/touch-ui-concepts.md#granite-ui) コンポーネントは、ユーザーが特定のリソースへのパスを選択できるようにするために使用します。表示されるパスは、次の方法でフィルタリングできます。

* [`com.day.cq.commons.predicate.AbstractNodePredicate`](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/predicate/package-summary.html) インターフェイスを実装してカスタム述語を実装します。
* 述語の名前を指定し、 `pathbrowser`.

カスタム述語の作成について詳しくは、[この記事](/help/sites-developing/implementing-custom-predicate-evaluator.md)を参照してください。

>[!NOTE]
>
>`com.day.cq.commons.predicate.AbstractNodePredicate` インターフェイスの実装によるカスタム述語の実装は、クラシック UI でも機能します。
>
>クラシック UI でカスタム述語を実装する例については、[このナレッジベースの記事](https://helpx.adobe.com/jp/experience-manager/using/creating-custom-cq-tree.html)を参照してください。

## 新しいアクションをコンポーネントツールバーに追加 {#add-new-action-to-a-component-toolbar}

各コンポーネントには、多くの場合、そのコンポーネントに対して実行できる様々なアクションを呼び出すためのツールバーがあります。

### コードサンプル {#code-sample-2}

`aem-authoring-extension-toolbar-screenshot` は、コンポーネントをレンダリングするカスタムツールバーアクションの作成方法を示すサンプルパッケージです。

GitHub のコード

このページのコードは GitHub にあります

* [GitHub の aem-authoring-extension-toolbar-screenshot プロジェクトを開きます](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-toolbar-screenshot)
* プロジェクトを [ZIP ファイル](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-toolbar-screenshot/archive/master.zip)としてダウンロードします

## 新しいインプレースエディターの追加 {#add-new-in-place-editor}

### 標準インプレースエディター {#standard-in-place-editor}

標準 AEM インストールでは、

1. `/libs/cq/gui/components/authoring/editors/clientlibs/core/js/editors/editorExample.js`

   に、使用可能な各種エディターの定義が保持されています。

1. エディターと、エディターを使用できる各リソースタイプは、（コンポーネントと同様に）関連付けられています。

   * `cq:inplaceEditing`

      次に例を示します。

      * `/libs/foundation/components/text/cq:editConfig`
      * `/libs/foundation/components/image/cq:editConfig`

         * property: `editorType`

            そのコンポーネントに対してインプレース編集が呼び出されたときに使用されるインラインエディターの種類を定義します。例： `text`, `textimage`, `image`, `title`.

1. エディターの追加の設定の詳細は、設定が含まれている `config` ノード、および必要なプラグイン設定の詳細が含まれている `plugin` ノードをさらに使用して設定できます。

   画像コンポーネントの画像切り抜きプラグインの縦横比を定義する例を次に示します。画面サイズが非常に制限されている場合があるので、切り抜きの縦横比はフルスクリーンエディターに移動され、そこでのみ表示できます。

   ```xml
   <cq:inplaceEditing
           jcr:primaryType="cq:InplaceEditingConfig"
           active="{Boolean}true"
           editorType="image">
           <config jcr:primaryType="nt:unstructured">
               <plugins jcr:primaryType="nt:unstructured">
                   <crop jcr:primaryType="nt:unstructured">
                       <aspectRatios jcr:primaryType="nt:unstructured">
                           <_x0031_6-10
                               jcr:primaryType="nt:unstructured"
                               name="16 : 10"
                               ratio="0.625"/>
                       </aspectRatios>
                   </crop>
               </plugins>
           </config>
   </cq:inplaceEditing>
   ```

   >[!CAUTION]
   >
   >AEM では、切り抜き比率は `ratio` プロパティで設定し、**高さ／幅**&#x200B;として定義します。これは、通常の高さ／幅の定義とは異なり、レガシー互換性のための設定です。`name` プロパティを明確に定義していれば、UI に表示されるので、オーサリングユーザーは違いを認識しません。

#### 新しいインプレースエディターの作成 {#creating-a-new-in-place-editor}

新しいインプレースエディターを（クライアントライブラリ内に）実装するには、次のようにします。

>[!NOTE]
>
>例：\
>`/libs/cq/gui/components/authoring/editors/clientlibs/core/js/editors/editorExample.js`

1. 実装方法：

   * `setUp`
   * `tearDown`

1. エディター（コンストラクターを含む）の登録：

   * `editor.register`

1. エディターと、エディターを使用できる各リソースタイプが（コンポーネントと同様に）関連付けられます。

#### 新しいインプレースエディターを作成するためのコードサンプル {#code-sample-for-creating-a-new-in-place-editor}

`aem-authoring-extension-inplace-editor` は、AEMで新しいインプレースエディターを作成する方法を示すサンプルパッケージです。

GitHub のコード

このページのコードは GitHub にあります

* [GitHub の aem-authoring-extension-inplace-editor プロジェクトを開きます](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-inplace-editor)
* プロジェクトを [ZIP ファイル](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-inplace-editor/archive/master.zip)としてダウンロードします

#### 複数のインプレースエディターの設定 {#configuring-multiple-in-place-editors}

コンポーネントに複数のインプレースエディターを含めることができます。複数のインプレースエディターを設定すると、適切なコンテンツを選択して、適切なエディターを開くことができます。詳しくは、 [複数のインプレースエディターの設定](/help/sites-developing/multiple-inplace-editors.md) ドキュメントを参照してください。

## 新しいページアクションの追加 {#add-a-new-page-action}

新しいページアクション（**サイトに戻る**（コンソール）アクションなど）をページツールバーに追加します。

### コードサンプル {#code-sample-3}

`aem-authoring-extension-header-backtosites` は、サイトコンソールに戻るカスタムヘッダーバーアクションを作成する方法を示すサンプルパッケージです。

GitHub のコード

このページのコードは GitHub にあります

* [GitHub の aem-authoring-extension-header-backtosites プロジェクトを開きます](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-header-backtosites)
* プロジェクトを [ZIP ファイル](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-header-backtosites/archive/master.zip)としてダウンロードします

## アクティベーションをリクエストワークフローのカスタマイズ {#customizing-the-request-for-activation-workflow}

既成のワークフローである&#x200B;**アクティベーションをリクエスト**&#x200B;は、コンテンツ作成者が適切な複製権限を持っていない場合に、自動的にトリガーされます。

このようなアクティベーションでの動作をカスタマイズするには、 **アクティベーションのリクエスト** ワークフロー：

1. In `/apps` オーバーレイ **サイト** ウィザード：

   `/libs/wcm/core/content/common/managepublicationwizard`

   >[!NOTE]
   >
   >これ自体は、次の一般的なインスタンスを上書きします。
   >
   >`/libs/cq/gui/content/common/managepublicationwizard`

1. を更新します。 [ワークフローモデル](/help/sites-developing/workflows-models.md) および必要に応じて関連する設定/スクリプトを作成します。
1. の権限を削除します。 [ `replicate` アクション](/help/sites-administering/security.md#actions) すべての関連するページに対するすべての適切なユーザーから：任意のユーザーがページを公開（またはレプリケート）しようとしたときに、このワークフローをデフォルトのアクションとしてトリガーする場合。
