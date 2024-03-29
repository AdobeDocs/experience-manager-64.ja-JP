---
title: リッチテキストエディターの設定
description: AEMリッチテキストエディターの設定について説明します。
contentOwner: AG
exl-id: 2d5e9ada-1567-43dc-ab19-6891e20e1d0b
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '2695'
ht-degree: 59%

---

# リッチテキストエディターの設定 {#configure-the-rich-text-editor}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

リッチテキストエディター (RTE) は、作成者に対して、テキストコンテンツの編集に関する様々な機能を提供します。 アイコン、選択ボックス、ツールバーおよびメニューを使用して、テキストを WYSIWYG で編集できます。

RTE 機能をオーサリングに使用する方法については、[リッチテキストエディターをオーサリングに使用](/help/sites-authoring/rich-text-editor.md)を参照してください。RTE の設定をおこなうことで、オーサリングコンポーネント内で使用可能な機能を有効化、無効化および拡張できます。以下に、Experience Manager の RTE 設定タスクを完了するために推奨されるワークフローを示します。

![リッチテキストエディターを設定するための一般的なワークフロー](assets/rte_workflow_v1.png)

*図：リッチテキストエディターを設定するための一般的なワークフロー*

## タッチ操作 UI とクラシック UI について {#understand-touch-enabled-ui-and-classic-ui}

タッチ操作対応 UI はAEMの標準 UI です。 Adobeでタッチ UI が導入され、 [レスポンシブデザイン](/help/sites-authoring/responsive-layout.md) オーサリング環境の場合、バージョン 5.6。タッチ UI は、タッチデバイスとデスクトップデバイス向けに設計されています。 この UI は、元のクラシック UI とは大きく異なります。

![タッチ操作対応 UI のリッチテキストエディターツールバー](assets/chlimage_1-404.png)

*図：タッチ操作対応 UI のリッチテキストエディターツールバー*

![クラシック UI のリッチテキストエディターツールバー](assets/rtedefault.png)

*図：クラシック UI のリッチテキストエディターツールバー*

>[!MORELIKETHIS]
>
>* [UI 推奨事項（英語）](/help/sites-deploying/ui-recommendations.md)
>* クラシック UI の廃止については、 [AEM 6.4 リリースノート](/help/release-notes/deprecated-removed-features.md)
>* タッチ UI とクラシック UI の違いについては、[タッチ UI とクラシック UI](https://aemcq5pedia.wordpress.com/2018/01/05/touch-enabled-ui-aem6-3/) を参照してください。
>* タッチ操作対応 UI について詳しくは、 [AEM Touch UI の概念](/help/sites-developing/touch-ui-concepts.md)


## 各種編集モード {#editingmodes}

AEMでは、コンポーネントの各種モードを使用して、テキストコンテンツを作成および編集できます。 コンテンツのオーサリングと書式設定をおこなうためのツールバーオプションと、異なる編集モードでの RTE 対応コンポーネントのユーザーエクスペリエンスは、RTE 設定によって異なります。

| 編集モード | 編集領域 | 有効化が推奨される機能 | タッチ UI | クラシック UI |
|--- |--- |--- |--- |--- |
| インライン | インプレース編集を使用して、小さな編集作業をすばやくおこなうことができます。ダイアログボックスを開かない書式 | 最小限の RTE 機能 | ○ | ○ |
| RTE 全画面 | ページ全体に広がる | 必要なすべての RTE 機能 | ○ | × |
| ダイアログ | ページコンテンツの上にあるダイアログボックス（ページ全体をカバーしない） | クラシック UI の場合、必要なすべての RTE 機能。タッチ UI の場合、必要に応じて機能を有効化／無効化 | ○ | ○ |
| ダイアログ（フルスクリーン） | フルスクリーンモードと同じ。RTE の横にダイアログのフィールドを含む | 必要なすべての RTE 機能 | ○ | × |

>[!NOTE]
>
>タッチ操作対応 UI のインライン編集モードでは、ソース編集機能を使用できません。フルスクリーンモードでは画像をドラッグできません。その他の機能はすべて全モードで使用できます。

### インライン編集 {#inline-editing}

（ゆっくりしたダブルタップまたはクリックで）開いた場合、コンテンツはページ内で編集できます。 基本オプションを備えた、コンパクトなツールバーが表示されます。

![タッチ操作 UI の基本ツールバーを使用したインライン編集](assets/chlimage_1-405.png)

*図：タッチ操作対応 UI の基本ツールバーを使用したインライン編集*

クラシック UI では、コンポーネントをゆっくりダブルクリックすると、インライン編集が可能になり、オレンジ色のアウトラインでコンテンツがハイライトされます。 コンテンツファインダーが開いている場合は、使用可能な RTE フォーマットオプションを含むツールバーがウィンドウの上部に表示されます。 コンテンツファインダーが開かない場合は、フォーマットオプションは表示されず、基本的なテキスト編集のみおこなうことができます。

### 全画面表示での編集 {#full-screen-editing}

AEMコンポーネントをフルスクリーン表示で開くことができます。この表示にした場合は、ページコンテンツが隠され、使用可能なスクリーンが占有されます。 フルスクリーン編集には最も多くの編集オプションがあるので、インライン編集の詳細版と考えてください。フルスクリーン編集を開くには、インライン編集モードの使用中にコンパクトツールバーから ![rte_fullscreen](assets/rte_fullscreen.png) をクリックします。

ダイアログのフルスクリーンモードには、詳細な RTE ツールバーと、ダイアログモードで使用可能なオプションとコンポーネントが表示されます。 このモードは、他のコンポーネントと共に RTE を含むダイアログにのみ適用されます。

![タッチ操作 UI のフルスクリーンモードで編集するときに表示される、詳細な RTE ツールバー](assets/chlimage_1-406.png)

*図：タッチ操作対応 UI のフルスクリーンモードで編集するときに表示される、詳細な RTE ツールバー*

### ダイアログ編集 {#dialog-editing}

クラシック UI でコンポーネントをダブルクリックすると、コンテンツを編集するためのダイアログボックスが開きます。 既存のページの上部にダイアログボックスが開きます。 特定のシナリオでは、ダイアログがポップアップウィンドウとして開きます。 例えば、複数列から成るページレイアウト内の列の一部がテキストコンポーネントで、ダイアログ用の領域が少ない場合などです。

![タッチ操作向け UI のダイアログ編集モード](assets/dialog_editing_modetouchui.png)

*図：タッチ操作対応 UI のダイアログ編集モード*

![編集用の詳細なツールバーを含む、クラシック UI のダイアログボックス](assets/chlimage_1-407.png)

*図：編集用の詳細なツールバーを含む、クラシック UI のダイアログボックス*

## RTE プラグインと関連機能について {#aboutplugins}

この機能は、一連のプラグインを介して使用可能になります。各プラグインには以下が含まれます。

* `features` プロパティ：

   * プラグインの基本機能をアクティベートまたはアクティベート解除するために使用されます。
   * 標準化された手順を使用して設定可能.

* 必要に応じて、特別な設定が必要なその他のプロパティやオプションを追加します。

RTE の基本機能は、該当するプラグインのノードにある `features` プロパティの値によって、アクティベートまたはアクティベート解除されます。

次の表に、現在のプラグインを示します。

* API ドキュメントへのリンクを含むプラグイン ID。 ID は、 [プラグインのアクティベート](/help/sites-administering/configure-rich-text-editor-plug-ins.md#activateplugin).
* `features` プロパティの許可されている値。
* プラグインが提供する機能の説明。

| プラグイン ID | 機能 | 説明 |
|--- |--- |--- |
| edit | cut copy paste-default paste-plaintext paste-wordhtml | [切り取り、コピーおよび 3 つの貼り付けモード](/help/sites-administering/configure-rich-text-editor-plug-ins.md#text-styles). |
| [findreplace](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.FindReplacePlugin) | find replace | 検索と置換。 |
| [format](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.FormatPlugin) | bold italic underline | [基本的なテキストの書式設定](/help/sites-administering/configure-rich-text-editor-plug-ins.md#text-styles). |
| [image](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.ImagePlugin) | 画像 | 基本的な画像サポート（コンテンツまたはコンテンツファインダーからのドラッグ）。ブラウザーの種類に応じて、様々なサポート機能が提供されます |
| [keys](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.KeyPlugin) |  | この値を定義するには、 [タブのサイズ](/help/sites-administering/configure-rich-text-editor-plug-ins.md#tab-size). |
| [justify](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.JustifyPlugin) | justifyleft justifycenter justifyright | 段落の整列。 |
| [リンク](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.LinkPlugin) | modifylink unlink anchor | [ハイパーリンクとアンカー](/help/sites-administering/configure-rich-text-editor-plug-ins.md#link-styles). |
| [lists](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.ListPlugin) | ordered unordered indent outdent | このプラグインは、[インデントとリスト](/help/sites-administering/configure-rich-text-editor-plug-ins.md#indent-margin)（ネストされたリストを含む）の両方を制御します。 |
| [misctools](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.MiscToolsPlugin) | specialchars sourceedit | 各種ツールを使用して、[特殊文字](/help/sites-administering/configure-rich-text-editor-plug-ins.md#special-char)の入力や HTML ソースの編集をおこなうことができます。また、独自のリストを定義する場合は、[特殊文字の範囲](/help/sites-administering/configure-rich-text-editor-plug-ins.md#define-range-char)全体を追加できます。 |
| Paraformat | paraformat | `<h2>`デフォルトの段落形式は、段落、見出し 1、見出し 2 および見出し 3（`<p>`、`<h1>`、`<h3>`）です。以下が可能です。 [他の段落書式を追加する](/help/sites-administering/configure-rich-text-editor-plug-ins.md#para-formats) またはリストを拡張します。 |
| spellcheck | checktext | [言語対応スペルチェッカー](/help/sites-administering/configure-rich-text-editor-plug-ins.md#add-dict). |
| スタイル | スタイル | CSS クラスを使用したスタイル設定のサポート。テキストで使用するスタイルの範囲を独自に追加（または拡張）する場合は、[新しいテキストスタイルを追加](/help/sites-administering/configure-rich-text-editor-plug-ins.md#text-styles)します。 |
| subsuperscript | subscript superscript | 下付き文字や上付き文字を追加して基本的なフォーマットを拡張。 |
| table | table removetable insertrow removerow insertcolumn removecolumn cellprops mergecells splitcell selectrow selectcolumns | テーブル全体または個々のセルに独自のスタイルを追加する場合は、[テーブルスタイルの設定](/help/sites-administering/configure-rich-text-editor-plug-ins.md#table-styles)を参照してください。 |
| undo | undo redo | [取り消しおよびやり直し](/help/sites-administering/configure-rich-text-editor-plug-ins.md#undo-history)操作の履歴サイズ。 |

>[!NOTE]
>
>フルスクリーンプラグインは、ダイアログモードではサポートされません。`dialogFullScreen` 設定を使用して、フルスクリーンモード用のツールバーを設定します。

## 設定パスと設定の場所について {#understand-the-configuration-paths-and-locations}

作成者に提供する [RTE 編集のモード（および UI）](#editingmodes)によって、[RTE プラグインをアクティベート](/help/sites-administering/configure-rich-text-editor-plug-ins.md#activateplugin)するときの設定詳細の場所が決まります。

| 編集モード | タッチ UI の場所 | クラシック UI の場所 |
|---|---|---|
| インライン | `cq:editConfig/cq:inplaceEditing` | `cq:editConfig/cq:inplaceEditing` |
| フルスクリーン | `cq:editConfig/cq:inplaceEditing` | 適用なし |
| ダイアログ | `cq:dialog` | `dialog` |
| フルスクリーンダイアログ | `cq:dialog` | 適用なし |

>[!NOTE]
>
>`cq:inplaceEditing` の下のノードの名前を `config` にしないでください。`cq:inplaceEditing` ノードで、以下のプロパティを定義します。
>
>* **名前**：`configPath`
>* **型**：`String`
>* **値**：実際の設定を含むノードのパス
>
>RTE 設定ノードの名前を `config` にしないでください。この名前にすると、RTE 設定が管理者に対してのみ有効になり、グループ `content-author` のユーザーに対して有効になりません。

ダイアログ編集モードで適用される次のプロパティを設定します（タッチ UI のみ）。

* `useFixedInlineToolbar`：RTE ツールバーをフロートではなく固定にするには、RTE ノード（sling:resourceType= `cq/gui/components/authoring/dialog/richtext` のもの）に定義されているこのブール値プロパティを `True` に設定します。

    このプロパティが true のときは、デフォルト動作により、リッチテキスト編集が「foundation-contentloaded」イベントで開始します。

   これを防ぐには、`customStart` プロパティを `True` に設定し、「rte-start」イベントを呼び出して RTE の編集を開始するようにします。このプロパティが true のときは、デフォルトの動作（クリック時に RTE が開始する）が機能しません。

* `customStart`：RTE を開始するタイミングを `True` イベントの呼び出しによって制御するには、RTE ノードに定義されているこのブール値プロパティを `rte-start` に設定します。

* `rte-start`：このイベントを RTE の `contenteditable-div`（RTE の編集を開始するタイミング）で呼び出します。これは、`customStart` が true に設定されている場合にのみ機能します。

タッチ操作ダイアログで RTE を使用する場合は、問題の発生を避けるために、プロパティ `useFixedInlineToolbar` に true を設定する必要があります。

## インプレース編集のカスタマイズ {#customizing-in-place-editing}

次のプロパティを設定することで、テキストエディターが開始する HTML セレクターを定義できます。

* **`editElementQuery`** - `cq:InplaceEditingConfig` に定義済み。このプロパティは、テキストコンポーネントのインライン編集を開始する HTML 要素のセレクターを指定するのに使用します。プロパティの指定がない場合は、インライン編集がテキストコンポーネント HTML 上で直接開始されます。
* **`textPropertyName`** - `cq:InplaceEditingConfig` に定義済み。このプロパティは、テキストコンポーネントの HTML 値をインライン編集後も保持しておくコンテンツノードに保存するプロパティの名前を指定するのに使用します。

ダイアログモードに対応するプロパティは、`name` です。

## プラグインのアクティベートによる RTE 機能の有効化 {#enable-rte-functionalities-by-activating-plug-ins}

リッチテキストエディター（RTE）の各機能は一連のプラグインから使用でき、それぞれに features プロパティがあります。features プロパティを設定して、各プラグインの様々な機能を有効または無効にできます。

RTE プラグインの詳細な設定については、 [RTE プラグインのアクティベートと設定の方法](/help/sites-administering/configure-rich-text-editor-plug-ins.md).

RTE の設定方法を理解するには、このサンプル設定をダウンロードしてください。 このパッケージではすべての機能が有効になっています。

[ファイルを入手](/help/assets/assets/rte-sample-all-features-enabled-10.zip)

>[!NOTE]
>
>この [コアコンポーネントのテキストコンポーネント](https://helpx.adobe.com/experience-manager/core-components/using/text.html) を使用すると、テンプレートエディターは、多くの RTE プラグインをコンテンツポリシーとしてユーザーインターフェイスに設定できるので、技術的な設定が不要です。 コンテンツポリシーは、 RTE ユーザーインターフェイス設定で説明するとおりに動作します。 詳しくは、 [RTE ユーザーインターフェイス設定とコンテンツポリシー](/help/sites-administering/rich-text-editor.md#rtecontentpolicies), [ページテンプレートの作成](/help/sites-authoring/templates.md)、および [コアコンポーネント開発者向けドキュメント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/overview.html?lang=ja).

>[!NOTE]
>
>参照用として、デフォルトのテキストコンポーネント（標準インストールの一環として提供）が次の場所に用意されています。
>
>* `/libs/wcm/foundation/components/text`
>* `/libs/foundation/components/text`
>
>独自のテキストコンポーネントを作成するには、これらのコンポーネントを編集する代わりに、上記のコンポーネントをコピーします。

## RTE ツールバーの設定 {#dialogfullscreen}

AEMでは、リッチテキストエディターの UI を編集モードごとに異なる設定にできます。 デフォルト設定を以下に示します。これらのデフォルト値は、要件に応じて上書きできます。

最適なオーサリング環境を実現するには：

* フローティングダイアログでは、フローティングダイアログのサイズが小さいので、ポップアップが表示されないプラグインのみを有効にします。
* フルスクリーンダイアログで、必要なプラグインをすべて有効にします。例えば、大きなポップアップを持つプラグイン ( `Paste` プラグインを使用します。 以下を使用： `dialogFullScreen` 設定については、以下を参照してください。

```java
<uiSettings jcr:primaryType="nt:unstructured">
  <cui jcr:primaryType="nt:unstructured">
    <inline
      jcr:primaryType="nt:unstructured"
      toolbar="[format#bold,format#italic,format#underline,#justify,#lists,links#modifylink,links#unlink,#paraformat]">
      <popovers jcr:primaryType="nt:unstructured">
        <justify
          jcr:primaryType="nt:unstructured"
          items="[justify#justifyleft,justify#justifycenter,justify#justifyright]"
          ref="justify"/>
        <lists
          jcr:primaryType="nt:unstructured"
          items="[lists#unordered,lists#ordered,lists#outdent,lists#indent]"
          ref="lists"/>
        <paraformat
          jcr:primaryType="nt:unstructured"
          items="paraformat:getFormats:paraformat-pulldown"
          ref="paraformat"/>
      </popovers>
    </inline>
    <dialogFullScreen
      jcr:primaryType="nt:unstructured"
      toolbar="[format#bold,format#italic,format#underline,justify#justifyleft,justify#justifycenter,justify#justifyright,lists#unordered,lists#ordered,lists#outdent,lists#indent,links#modifylink,links#unlink,table#createoredit,#paraformat,image#imageProps]">
      <popovers jcr:primaryType="nt:unstructured">
        <paraformat
          jcr:primaryType="nt:unstructured"
          items="paraformat:getFormats:paraformat-pulldown"
          ref="paraformat"/>
      </popovers>
    </dialogFullScreen>
    <tableEditOptions
      jcr:primaryType="nt:unstructured"
      toolbar="[table#insertcolumn-before,table#insertcolumn-after,table#removecolumn,-,table#insertrow-before,table#insertrow-after,table#removerow,-,table#mergecells-right,table#mergecells-down,table#mergecells,table#splitcell-horizontal,table#splitcell-vertical,-,table#selectrow,table#selectcolumn,-,table#ensureparagraph,-,table#modifytableandcell,table#removetable,-,undo#undo,undo#redo,-,table#exitTableEditing,-]">
    </tableEditOptions>
  </cui>
</uiSettings>
```

インラインモードとフルスクリーンモードでは、異なる UI 設定が使用されます。 ツールバーのボタンを指定するには、ツールバーのプロパティを使用します。 例えば、ボタン自体が 1 つの機能（例：`Bold`）である場合は、`PluginName#FeatureName` と指定されます（例：`links#modifylink`）。ボタンがポップオーバー（プラグインのいくつかの機能を含む）の場合は、`#PluginName` と指定されます（例：`#format`）。区切り文字 ( | ) ボタンのグループの間には、「 — 」を使用して指定できます。

インラインモードまたはフルスクリーンモードのポップアップノードには、使用するポップオーバーのリストが含まれます。 以下の各子ノード `popovers` ノードはプラグインの名前を取って名付けられます ( 例： `format`) をクリックします。 プロパティがあります `items` プラグインの機能のリストを含む ( 例： `format#bold`) をクリックします。

## RTE ユーザーインターフェイス設定とコンテンツポリシー {#rtecontentpolicies}

管理者は、前述のように設定をおこなう代わりに、コンテンツポリシーを使用して RTE オプションを制御できます。 コンテンツポリシーは、コンポーネントの一部として使用する場合のデザインプロパティを定義します [編集可能なテンプレート](../sites-authoring/templates.md). 例えば、RTE を使用するテキストコンポーネントが編集可能なテンプレートと共に使用されている場合、コンテンツポリシーでは太字オプションを使用可能にし、一部の段落書式オプションを使用可能にするように定義できます。 コンテンツポリシーは再利用可能で、複数のテンプレートに適用できます。

AEM 6.4 Service Pack 3 以降では、RTE フローで使用可能なオプションが、ユーザーインターフェイス設定からコンテンツポリシーに影響します。

* ユーザーインターフェイス設定では、コンテンツポリシーで使用可能なオプションを定義します。
* RTE のユーザーインターフェイス設定が削除されたか、どの項目も有効にしていない場合、コンテンツポリシーではその設定ができません。
* 作成者は、ユーザーインターフェイス設定およびコンテンツポリシーによって使用可能となっている機能にのみアクセスできます。

例については、[テキストコアコンポーネントのドキュメント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/text.html?lang=ja#the-text-component-and-the-rich-text-editor)を参照してください。

## ツールバーアイコンとコマンドのマッピングのカスタマイズ {#iconstoolbar}

RTE ツールバーに表示される Coral アイコンと使用可能なコマンドとのマッピングをカスタマイズできます。Coral アイコンに加えて他のアイコンを使用することはできません。

1. `icons` の下に、`uiSettings/cui` という名前のノードを作成します。

1. そのノードの下に、各アイコンのノードを作成します。
1. 個々のアイコンノードで、Coral アイコンとそのアイコンにマッピングするコマンドを指定します。

以下に、`textItalic` という名前の Coral アイコンにコマンド「Bold」をマッピングするサンプルスニペットを示します。

```java
<text jcr:primaryType="nt:unstructured" sling:resourceType="cq/gui/components/authoring/dialog/richtext" name="./text" useFixedInlineToolbar="{Boolean}true"> 
    <rtePlugins jcr:primaryType="nt:unstructured"> 
        <format jcr:primaryType="nt:unstructured" features="bold,italic"/> 
    </rtePlugins> 
    <uiSettings jcr:primaryType="nt:unstructured"> 
        <cui jcr:primaryType="nt:unstructured"> 
            <inline jcr:primaryType="nt:unstructured" 
                toolbar="[format#bold,format#italic,format#underline,links#modifylink,links#unlink]"> 
            </inline> 
            <icons jcr:primaryType="nt:unstructured"> 
                <bold jcr:primaryType="nt:unstructured" 
                    command="format#bold" 
                    icon="textItalic"/> 
            </icons> 
        </cui> 
    </uiSettings> 
</text>
```

## CoralUI 2 リッチテキストエディターへの切り替え {#switch-to-coralui-rich-text-editor}

ページに、CoralUI 2 RTE clientlib または CoralUI 3 RTE clientlib を含めることができます。デフォルトでは、リッチテキストエディターには CoralUI 3 RTE clientlib が含まれています。 CoralUI 2 RTE に切り替えるには、次の手順を実行します。

>[!NOTE]
>
>Adobeでは、ベストプラクティスとして切り替えをお勧めしません。 CoralUI 2 RTE への切り替えは最後の手段です。CoralUI 2 RTE 用カスタムプラグインは、CoralUI 3 RTE で動作します ( プラグインが RTE の内部（クラスなど）に依存しない場合 )。 CoralUI3 RTE 用カスタムプラグインを使用する場合は、`rte.coralui3` ライブラリを使用してください。

1. ノード `/libs/cq/gui/components/authoring/editors/clientlibs/core` を `/apps` の下にオーバーレイし、次の操作を実行します。

   * dependencies プロパティで、`rte.coralui3` を `rte.coralui2` に置き換えます。
   * 埋め込みプロパティで、`cq.authoring.editor.core.inlineediting.rte.coralui3` を `cq.authoring.editor.core.inlineediting.rte.coralui2` に置き換えます。
   * 埋め込みプロパティで、`cq.authoring.rte.coralui3` を `cq.authoring.rte.coralui2` に置き換えます。

1. ノード`/libs/cq/gui/components/authoring/dialog/richtext/clientlibs/rte/coralui3`および`/libs/cq/gui/components/authoring/dialog/richtext/clientlibs/rte/coralui2`を`/apps`の下にオーバーレイします。

   カテゴリ`cq.authoring.dialog`を`/apps/cq/gui/components/authoring/dialog/richtext/clientlibs/rte/coralui3`から削除して、`/apps/cq/gui/components/authoring/dialog/richtext/clientlibs/rte/coralui2` に追加してください。

1. ページに含まれている他の依存関係を `rte.coralui3` から `rte.coralui2` に変更します。例えば、`/apps`の下のノード`/libs/mcm/campaign/components/touch-ui/clientlibs/rte`をオーバーレイした後、そのノードの依存関係をすべて`rte.coralui3`から`rte.coralui2`に変更します。

1. `/apps`の下のノード`cq/ui/widgets`をオーバーレイします。ノード `/apps/cq/ui/widgets` の依存関係 `cq.rte` を `cq.coralui2.rte` で置き換えます。

>[!NOTE]
>
>CoralUI 2 RTE は、プラグインダイアログにハンドルバーテンプレートを使用します。 したがって、CoralUI 2 RTE クライアントライブラリは、ハンドルバー clientlib に依存していました。 CoralUI 3 RTE は、ハンドルバーテンプレートを使用せず、関連する依存関係も持ちません。 カスタムプラグインでハンドルバーテンプレートを使用する場合は、Web ページに handlebars clientlib を含めます。

## その他の情報 {#further-information}

RTE の設定について詳しくは、 [AEM Widget API](https://helpx.adobe.com/jp/experience-manager/6-4/sites/developing/using/reference-materials/widgets-api/index.html) 参照。

特に、使用可能なプラグインと関連オプションを確認するには、次の手順を実行します。

* この [CQ.form.RichText](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.RichText) コンポーネントは、スタイル設定されたテキスト情報（リッチテキスト）を編集するためのフォームフィールドを提供します。 リッチテキストフォームで使用できるすべてのパラメーターについては、設定オプションを参照してください。
* リッチテキストコンポーネントは、[CQ.form.rte.plugins.Plugin](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.Plugin) の下にリストされるプラグインを使用した幅広い機能を提供します。各プラグインについては、以下を参照してください。

   * 有効（または無効）にできる機能について詳しくは、機能を参照してください。
   * 該当するプラグインの詳細な設定に使用できるすべてのパラメーターについては、「設定オプション」を参照してください。

* リンクのHTMLルールの詳細も参照できます。

上記のオプションを使用して、独自の RTE を拡張およびカスタマイズできます。 例えば、リンク作成時にページで使用できるアンカーをリストするために、`LinkPlugin` を独自に実装できます。

## 既知の制限事項 {#known-limitations}

AEM RTE 機能には次の制限があります。

* RTE 機能は、AEMコンポーネントダイアログでのみサポートされます。 RTE は、ウィザードや、次のような Foundation-forms ではサポートされていません。 [ページプロパティ](/help/sites-developing/page-properties-views.md) および [基礎モード](/help/sites-authoring/scaffolding.md) （タッチ操作対応 UI の場合）

* AEMが機能しない [ハイブリッドデバイス](/help/release-notes/known-issues.md).

* RTE 設定ノードの名前を `config` にしないでください。この名前にすると、RTE 設定が管理者に対してのみ有効になり、グループ `content-author` のユーザーに対して有効になりません。

* RTE は、コンテンツを埋め込むインラインフレームまたは iframe をサポートしていません。

>[!MORELIKETHIS]
>
>* [RTE プラグインの設定](configure-rich-text-editor-plug-ins.md)
>* [リッチテキストエディターをオーサリングに使用](../sites-authoring/rich-text-editor.md)
>* [RTE をアクセス可能なサイト用に設定](rte-accessible-content.md)
>* [タッチ UI とクラシック UI 機能の類似点](../release-notes/touch-ui-features-status.md)
>* [複合マルチフィールドコンポーネントを作成するためのチュートリアルサンプル](https://experience-aem.blogspot.com/2019/05/aem-65-touchui-composite-multifield-with-coral3-rte-rich-text.html)

