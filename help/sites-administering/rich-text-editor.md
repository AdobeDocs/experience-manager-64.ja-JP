---
title: リッチテキストエディターの設定
description: AEM リッチテキストエディターの設定について説明します。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 6a43a972b8ff5ce5603f0fdaa999558cdf3cbb0e

---


# リッチテキストエディターの設定 {#configure-the-rich-text-editor}

リッチテキストエディター（RTE）には、テキストコンテンツの編集に使用できる幅広い機能が用意されています。アイコン、選択ボックス、ツールバーおよびメニューを使用して、テキストを WYSIWYG で編集できます。

RTE の設定をおこなうことで、オーサリングコンポーネント内で使用可能な機能を有効化、無効化および拡張できます。RTE 機能をオーサリングに使用する方法については、[リッチテキストエディターをオーサリングに使用](/help/sites-authoring/rich-text-editor.md)を参照してください。

以下に、RTE 設定タスクの推奨されるワークフローを示します。

![リッチテキストエディターを設定する標準的なワークフロー](assets/rte_workflow_v1.png)

*図：リッチテキストエディターを設定するための一般的なワークフロー*

## タッチ操作 UI とクラシック UI について {#understand-touch-enabled-ui-and-classic-ui}

タッチ操作 UI は AEM の標準 UI です。Adobe introduced Touch UI with [responsive design](/help/sites-authoring/responsive-layout.md) for authoring environment, in version 5.6. The Touch UI is designed for touch and desktop devices. 元のクラシック UI とは大きく異なります。

![タッチ操作 UI のリッチテキストエディターツールバー](assets/chlimage_1-404.png)

*図：タッチ対応UIのリッチテキストエディターツールバー*

![クラシック UI のリッチテキストエディターツールバー](assets/rtedefault.png)

*図：クラシックUIのリッチテキストエディタのツールバー*

>[!MORELIKETHIS]
>
>* [UI 推奨事項（英語）](/help/sites-deploying/ui-recommendations.md)
>* クラシック UI の廃止については、[AEM 6.4 リリースノート](/help/release-notes/deprecated-removed-features.md)を参照してください。
>* For difference between the UIs, see [Touch UI and Classic UI](https://aemcq5pedia.wordpress.com/2018/01/05/touch-enabled-ui-aem6-3/)
>* タッチ操作 UI について詳しくは、[AEM タッチ操作向け UI の概念](/help/sites-developing/touch-ui-concepts.md)を参照してください。


## 各種編集モード {#editingmodes}

AEM では、コンポーネントの各種モードを使用して、テキストコンテンツを作成および編集できます。コンテンツを作成およびフォーマットするためのツールバーオプションと、各種編集モードにおける RTE 対応コンポーネントのユーザーエクスペリエンスは、RTE 設定によって異なります。

<table> 
 <tbody> 
  <tr> 
   <th>編集モード</th> 
   <th>編集領域</th> 
   <th>有効化が推奨される機能<br /> </th> 
   <th>タッチ UI</th> 
   <th>クラシック UI</th> 
  </tr> 
  <tr> 
   <td>インライン</td> 
   <td>小さな編集をすばやくおこなうのに適したインプレース編集。ダイアログボックスを開かないフォーマット</td> 
   <td>最小限の RTE 機能</td> 
   <td>○</td> 
   <td>○</td> 
  </tr> 
  <tr> 
   <td>RTE フルスクリーン</td> 
   <td>ページ全体に広がる<br /> </td> 
   <td>必要なすべての RTE 機能<br /> </td> 
   <td>○</td> 
   <td>×<br /> </td> 
  </tr> 
  <tr> 
   <td>ダイアログ</td> 
   <td>ページコンテンツの上面にダイアログボックスが表示されるが、ページ全体に広がらない</td> 
   <td>クラシック UI の場合、必要なすべての RTE 機能。タッチ UI の場合、必要に応じて機能を有効化／無効化<br /> </td> 
   <td>○</td> 
   <td>○</td> 
  </tr> 
  <tr> 
   <td>ダイアログ（フルスクリーン）<br /> </td> 
   <td>フルスクリーンモードと同じ。RTE の横にダイアログのフィールドを含む<br /> </td> 
   <td>必要なすべての RTE 機能</td> 
   <td>○</td> 
   <td>×</td> 
  </tr> 
 </tbody> 
</table>

>[!NOTE]
>
>タッチ対応UIのインライン編集モードでは、ソース編集機能を使用できません。 フルスクリーンモードでは画像をドラッグできません。その他の機能はすべて全モードで使用できます。

### インライン編集 {#inline-editing}

（ゆっくりしたダブルタップ／ダブルクリックで）開いた場合、コンテンツはページ内で編集できます。基本オプションを備えた、コンパクトなツールバーが表示されます。

![タッチ操作 UI の基本ツールバーを使用したインライン編集](assets/chlimage_1-405.png)

*図：タッチ対応UIの基本ツールバーを使用したインライン編集*

クラシック UI では、コンポーネントをゆっくりダブルクリックするとインライン編集が可能になり、オレンジ色の輪郭でコンテンツが強調表示されます。コンテンツファインダーが開くと、使用可能な RTE フォーマットオプションを備えたツールバーがウィンドウ上部に表示されます。コンテンツファインダーが開かない場合は、フォーマットオプションは表示されず、基本的なテキスト編集のみおこなうことができます。

### フルスクリーン編集 {#full-screen-editing}

AEM コンポーネントをフルスクリーン表示で開くことができます。この表示にした場合は、ページコンテンツが隠され、使用可能なスクリーンが占有されます。フルスクリーン編集には最も多くの編集オプションがあるので、インライン編集の詳細版と考えてください。It can be opened by clicking ![rte_fullscreen](assets/rte_fullscreen.png), from the compact toolbar when using the inline editing mode.

ダイアログのフルスクリーンモードには、詳細な RTE ツールバー、該当するオプション、ダイアログモードで使用可能なコンポーネントが表示されます。このモードは、他のコンポーネントと共に RTE を含むダイアログにのみ適用されます。

![タッチ操作 UI のフルスクリーンモードで編集するときに表示される、詳細な RTE ツールバー](assets/chlimage_1-406.png)

*図：タッチ対応UIでフルスクリーンモードで編集する場合の詳細なRTEツールバー*

### ダイアログ編集 {#dialog-editing}

クラシック UI でコンポーネントをダブルクリックすると、コンテンツ編集用のダイアログボックスが既存のページの上面に開きます。一部のシナリオでは、ポップアップウィンドウとして開くこともあります。例えば、複数列のページレイアウトで、テキストコンポーネントが列の一部で、ダイアログで使用できる領域が少ない場合、

![タッチ操作向け UI のダイアログ編集モード](assets/dialog_editing_modetouchui.png)

*図：タッチ対応UIのダイアログ編集モード*

![編集用の詳細なツールバーを含む、クラシック UI のダイアログボックス](assets/chlimage_1-407.png)

*図：編集用の詳細ツールバーを含むクラシックUIのダイアログボックス*

## RTE プラグインと関連機能について {#aboutplugins}

この機能は、一連のプラグインを介して使用可能になります。各プラグインには以下が含まれます。

* プロパ `features` ティ：

   * プラグインの基本機能をアクティベートまたはアクティベート解除するために使用します。
   * 標準化された手順を使用して設定できます。

* 特別な設定を必要とする詳細なプロパティやオプションが存在する場合があります。

RTE の基本機能は、該当するプラグインのノードにある `features` プロパティの値によって、アクティベートまたはアクティベート解除されます。

以下の表に最新のプラグインを示します。

* API ドキュメントへのリンクを含むプラグイン ID。ID は、[プラグインをアクティベート](/help/sites-administering/configure-rich-text-editor-plug-ins.md#activateplugin)するときにノード名として使用されます。
* `features` プロパティの許可されている値。
* プラグインが提供する機能の説明。

<table> 
 <tbody> 
  <tr> 
   <td><p>プラグイン ID<br /> <br /> </p> </td> 
   <td><p>features<br /> <br /> </p> </td> 
   <td><p>説明<br /> <br /> </p> </td> 
  </tr> 
  <tr> 
   <td><p>edit</p> </td> 
   <td><p>cut<br /> copy<br /> paste-default<br /> paste-plaintext<br /> paste-wordhtml</p> </td> 
   <td><p><a href="/help/sites-administering/configure-rich-text-editor-plug-ins.md#textstyles" target="_blank">切り取り、コピーおよび 3 つの貼り付けモード</a>。</p> </td> 
  </tr> 
  <tr> 
   <td><p><a href="https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.FindReplacePlugin">findreplace</a></p> </td> 
   <td><p>find<br /> replace</p> </td> 
   <td><p>検索と置換.</p> </td> 
  </tr> 
  <tr> 
   <td><p><a href="https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.FormatPlugin">形式</a></p> </td> 
   <td><p>bold<br /> italic<br /> underline</p> </td> 
   <td><p><a href="/help/sites-administering/configure-rich-text-editor-plug-ins.md#textstyles" target="_blank">基本的なテキストフォーマット</a>。</p> </td> 
  </tr> 
  <tr> 
   <td><p><a href="https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.ImagePlugin">画像</a></p> </td> 
   <td><p>画像</p> </td> 
   <td><p>整列や代替テキストのような画像プロパティを設定します。コンテンツファインダーから画像をドラッグ＆ドロップするための基本サポートは、このプラグインなしでも機能します。</p> <p><em></em>注意：このオーサリング動作はブラウザーによって異なる可能性があります。例えば、Mozilla Firefoxには再サイズ化機能がありますが、Google Chromeにはありません。</p> </td> 
  </tr> 
  <tr> 
   <td><p><a href="https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.KeyPlugin">keys</a></p> </td> 
   <td><p> </p> </td> 
   <td><p>この値を定義するには、<a href="/help/sites-administering/configure-rich-text-editor-plug-ins.md#tabsize" target="_blank">タブサイズ</a>を参照してください。</p> </td> 
  </tr> 
  <tr> 
   <td><p><a href="https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.JustifyPlugin">justify</a></p> </td> 
   <td><p>justifyleft<br /> justifycenter<br /> justifyright</p> </td> 
   <td><p>段落の整列。</p> </td> 
  </tr> 
  <tr> 
   <td><p><a href="https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.LinkPlugin">links</a></p> </td> 
   <td><p>modifylink<br /> unlink<br /> anchor</p> </td> 
   <td><p><a href="/help/sites-administering/configure-rich-text-editor-plug-ins.md#linkstyles" target="_blank">ハイパーリンクおよびアンカー</a>。</p> </td> 
  </tr> 
  <tr> 
   <td><p><a href="https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.ListPlugin">lists</a></p> </td> 
   <td><p>ordered<br />
unordered<br />
indent<br />
outdent</p> </td> 
   <td><p>This plug-in controls both <a href="/help/sites-administering/configure-rich-text-editor-plug-ins.md#indentmargin" target="_blank">indentation and lists</a>; including nested lists.</p> </td> 
  </tr> 
  <tr> 
   <td><p><a href="https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.MiscToolsPlugin">misctools</a></p> </td> 
   <td><p>specialchars<br /> sourceedit</p> </td> 
   <td>Miscellaneous tools allow authors to enter <a href="/help/sites-administering/configure-rich-text-editor-plug-ins.md#spchar" target="_blank">special characters</a> or edit the HTML source. Also, you can add a whole <a href="/help/sites-administering/configure-rich-text-editor-plug-ins.md#definerangechar" target="_blank">range of special characters</a> if you want to define your own list.</td> 
  </tr> 
  <tr> 
   <td><p>Paraformat</p> </td> 
   <td><p>paraformat</p> </td> 
   <td>デフォルトの段落フォーマットは、段落、見出し 1、見出し 2 および見出し 3（&lt;p&gt;、&lt;h1&gt;、&lt;h2&gt; および &lt;h3&gt;）です。<a href="/help/sites-administering/configure-rich-text-editor-plug-ins.md#paraformats" target="_blank">他の段落フォーマットを追加</a>したり、リストを拡張したりできます。</td> 
  </tr> 
  <tr> 
   <td><p>spellcheck</p> </td> 
   <td><p>checktext</p> </td> 
   <td><p><a href="/help/sites-administering/configure-rich-text-editor-plug-ins.md#adddict" target="_blank">言語ごとのスペルチェッカー</a>。</p> </td> 
  </tr> 
  <tr> 
   <td><p>styles</p> </td> 
   <td><p>styles</p> </td> 
   <td>CSS クラスを使用したスタイル設定のサポート。<a href="/help/sites-administering/configure-rich-text-editor-plug-ins.md#textstyles" target="-blank">テキストで使用する</a> 、独自のスタイル範囲を追加（または拡張）する場合は、新しいテキストスタイルを追加します。</td> 
  </tr> 
  <tr> 
   <td><p>subsuperscript</p> </td> 
   <td><p>subscript<br /> superscript</p> </td> 
   <td><p>基本形式の拡張で、サブスクリプトとスーパースクリプトを追加します。</p> </td> 
  </tr> 
  <tr> 
   <td><p>table</p> </td> 
   <td><p>table<br /> removetable<br /> insertrow<br /> removerow<br /> insertcolumn<br /> removecolumn<br /> cellprops<br /> mergecells<br /> splitcell<br /> selectrow<br /> selectcolumns</p> </td> 
   <td>See <a href="/help/sites-administering/configure-rich-text-editor-plug-ins.md#tablestyles" target="_blank">configure table styles</a>, if you want to add your own styles for either entire tables or individual cells.</td> 
  </tr> 
  <tr> 
   <td><p>undo</p> </td> 
   <td><p>undo<br /> redo</p> </td> 
   <td>History size of <a href="/help/sites-administering/configure-rich-text-editor-plug-ins.md#undohistory" target="_blank">undo and redo</a> operations.</td> 
  </tr> 
 </tbody> 
</table>

>[!NOTE]
>
>フルスクリーンプラグインは、ダイアログモードではサポートされません。Use of the `dialogFullScreen` setting to configure the toolbar for full screen mode.

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
>Do not name the node under `cq:inplaceEditing` as `config`. On `cq:inplaceEditing` node, define the following properties:
>
>* **名前**: `configPath`
   >
   >
* **タイプ**: `String`
   >
   >
* **値**：実際の設定を含むノードのパス
>
>
RTE 設定ノードの名前を `config` にしないでください。Otherwise, the RTE configurations take effect for only the administrators and not for the users in the group `content-author`.

ダイアログ編集モードで適用される次のプロパティを設定します（タッチ UI のみ）。

* `useFixedInlineToolbar`:RTEノード（sling:resourceType=のあるもの）で定義されているこのBooleanプロパティをに設定し `cq/gui/components/authoring/dialog/richtext`、RTEツー `True`ルバーをフローティングではなく固定します。

    このプロパティが true のときは、デフォルト動作により、リッチテキスト編集が「foundation-contentloaded」イベントで開始します。

   これを防ぐには、`customStart``True` プロパティを に設定し、「rte-start」イベントを呼び出して RTE の編集を開始するようにします。このプロパティが true のときは、デフォルトの動作（クリック時に RTE が開始する）が機能しません。

* `customStart`：RTE を開始するタイミングを `True` イベントの呼び出しによって制御するには、RTE ノードに定義されているこのブール値プロパティを `rte-start` に設定します。

* `rte-start`：このイベントを RTE の `contenteditable-div`（RTE の編集を開始するタイミング）で呼び出します。これは、`customStart` が true に設定されている場合にのみ機能します。

タッチ操作ダイアログで RTE を使用する場合は、問題の発生を避けるために、プロパティ `useFixedInlineToolbar` に true を設定する必要があります。

## プラグインのアクティベートによる RTE 機能の有効化 {#enable-rte-functionalities-by-activating-plug-ins}

リッチテキストエディター（RTE）の各機能は一連のプラグインを介して使用可能になり、それぞれに features プロパティがあります。features プロパティを設定することで、各プラグインの各種機能を有効化または無効化できます。

RTE プラグインの設定について詳しくは、[RTE プラグインのアクティベートおよび設定方法に関する説明](/help/sites-administering/configure-rich-text-editor-plug-ins.md)を参照してください。


RTE の設定方法について理解するには、このサンプル設定をダウンロードしてください。このパッケージではすべての機能が有効になっています。

[ファイルを入手](/help/assets/assets/rte-sample-all-features-enabled-10.zip)

>[!NOTE]
>
>[コアコンポーネントのテキストコンポーネント](https://helpx.adobe.com/experience-manager/core-components/using/text.html)を使用すると、テンプレートエディターのユーザーインターフェイスで多数の RTE プラグインをコンテンツポリシーとして設定し、技術的な設定を不要にすることができます。コンテンツポリシーは、RTE ユーザーインターフェイス設定と連携させることができます。For more information, see the [RTE user interface settings and content polices](/help/sites-administering/rich-text-editor.md#rtecontentpolicies), [Create page templates](/help/sites-authoring/templates.md), and the [Core Components developer documentation](https://helpx.adobe.com/experience-manager/core-components/using/developing.html).

>[!NOTE]
>
>参照用として、デフォルトのテキストコンポーネント（標準インストールの一環として提供）が次の場所に用意されています。
>
>* `/libs/wcm/foundation/components/text`
>* `/libs/foundation/components/text`
>
>
独自のテキストコンポーネントを作成するには、上記のコンポーネントを直接編集するのではなく、コピーしてください。

## RTE ツールバーの設定 {#dialogfullscreen}

AEM では、リッチテキストエディターの UI を編集モードごとに異なる設定にできます。デフォルト設定を以下に示します。これらの設定を必要に応じて上書きできます。

最適なオーサリング環境を実現するには：

* フローティングダイアログでは、そのサイズが小さいことを考慮して、ポップアップがないプラグインのみを有効にします。
* フルスクリーンダイアログでは、必要なプラグインをすべて有効にします。これは、`Paste` プラグインなど、ポップが大きなプラグインについても当てはまります。以下に示す `dialogFullScreen` 設定を使用します。

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

インラインモードとフルスクリーンモードでは別の UI 設定が使用されます。ツールバープロパティは、ツールバーのボタンの指定に使用します。For example, if the button is itself a feature (for example, `Bold`), it is specified as `PluginName#FeatureName` (for example, `links#modifylink`). If the button is a popover (containing some features of a plug-in), it is specified as `#PluginName` (for example, `#format`). ボタンのグループの間の区切り文字（|）は、「-」で指定できます。

インラインまたはフルスクリーンモードのポップアップノードには、使用するポップオーバーのリストが含まれます。Each child node under the `popovers` node is named after the plug-in (for example, `format`). It has a property `items` containing a list of features of the plug-in (for example, `format#bold`).

## RTE ユーザーインターフェイス設定とコンテンツポリシー {#rtecontentpolicies}

管理者は、上述のような設定をおこなわなくても、コンテンツポリシーを使用して RTE オプションを制御することができます。コンテンツポリシーでは、[編集可能テンプレート](../sites-authoring/templates.md)の一部として使用されるコンポーネントのデザインプロパティが定義されます。例えば、RTE を使用するテキストコンポーネントが編集可能テンプレートで使用される場合は、コンテンツポリシーの定義によって、太字オプションやいくつかの段落フォーマットオプションを使用可能にできます。コンテンツポリシーは再利用が可能であり、複数のテンプレートに対して適用できます。

AEM 6.4 Service Pack 3 以降では、RTE フローで使用可能なオプションに関するユーザーインターフェイス設定がコンテンツポリシーに影響します。

* ユーザーインターフェイス設定では、コンテンツポリシーで使用可能なオプションを定義します。
* RTEのユーザーインターフェイス設定が削除された場合、または項目が有効になっていない場合、コンテンツポリシーは項目を設定できません。
* オーサーは、ユーザーインターフェイス設定およびコンテンツポリシーによって使用可能となっている機能にのみアクセスできます。

例については、[テキストコアコンポーネントのドキュメント](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/components/text.html#the-text-component-and-the-rich-text-editor)を参照してください。

## ツールバーアイコンとコマンドのマッピングのカスタマイズ {#iconstoolbar}

RTE ツールバーに表示される Coral アイコンと使用可能なコマンドとのマッピングをカスタマイズできます。Coralアイコン以外のアイコンは使用できません。

1. Create a node named `icons` under `uiSettings/cui`.

1. そのノードの下に、各アイコンのノードを作成します。
1. 個々のアイコンノードで、Coralアイコンと、アイコンにマッピングするコマンドを指定します。

Below is a sample snippet to map the command Bold to the Coral icon named `textItalic`.

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

ページに、CoralUI 2 RTE clientlibまたはCoralUI 3 RTE clientlibを含めることができます。 デフォルトでは、リッチテキストエディターには CoralUI 3 RTE clientlib が含まれています。CoralUI 2 RTE に切り替えるには、次の手順を実行します。

>[!NOTE]
>
>こうした切り替えは、ベストプラクティスとしてお勧めするものではありません。CoralUI 2 RTE への切り替えは最後の手段です。CoralUI 2 RTE用のカスタムプラグインは、プラグインがクラスなどのRTE内部に依存しない場合、CoralUI 3 RTEと連携します。 CoralUI RTE のカスタムプラグインを使用する場合は、`rte.coralui3`3 ライブラリを使用してください。

1. ノードを下にオー `/libs/cq/gui/components/authoring/editors/clientlibs/core` バーレ `/apps`イし、次の操作を行います。

   * Replace `rte.coralui3` with `rte.coralui2` for the dependencies property.
   * Replace `cq.authoring.editor.core.inlineediting.rte.coralui3` with `cq.authoring.editor.core.inlineediting.rte.coralui2` for the embed property.
   * Replace `cq.authoring.rte.coralui3` with `cq.authoring.rte.coralui2` for the embed property.

1. ノードを下に重ね `/libs/cq/gui/components/authoring/dialog/richtext/clientlibs/rte/coralui3` て表示 `/libs/cq/gui/components/authoring/dialog/richtext/clientlibs/rte/coralui2` しま `/apps`す。

   カテゴリを `cq.authoring.dialog` から削 `/apps/cq/gui/components/authoring/dialog/richtext/clientlibs/rte/coralui3` 除し、に追加しま `/apps/cq/gui/components/authoring/dialog/richtext/clientlibs/rte/coralui2`す。

1. ページに含まれている他の依存関係を `rte.coralui3` から `rte.coralui2` に変更します。For example, after overlaying the node `/libs/mcm/campaign/components/touch-ui/clientlibs/rte` under `/apps`, change any dependency on it from `rte.coralui3` to `rte.coralui2`.

1. Overlay the node `cq/ui/widgets` under `/apps`. ノードの依存関 `cq.rte` 係をに置き換 `/apps/cq/ui/widgets` えます `cq.coralui2.rte`。

>[!NOTE]
>
>CoralUI 2 RTE は、プラグインダイアログのハンドルバーテンプレートを使用します。そのため、CoralUI 2 RTE clientlib は、ハンドルバー clientlib に対して依存関係があります。CoralUI 3 RTE は、ハンドルバーテンプレートを使用しないので、関連する依存関係はありません。カスタムプラグインがハンドルバーテンプレートを使用する場合、Web ページにハンドルバー clientlib を含めます。

## その他の情報 {#further-information}

RTE の設定について詳しくは、[AEM ウィジェット API](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/widgets-api/index.html) リファレンスを参照してください。

特に、使用可能なプラグインおよび関連オプションを確認するには、以下を参照してください。

* [CQ.form.RichText](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.RichText) コンポーネントは、スタイル設定されたテキスト情報（リッチテキスト）を編集するためのフォームフィールドを提供します。リッチテキストフォームに使用可能なすべてのパラメーターについては、「設定オプション」を参照してください。
* The RichText component provides a wide range of functionality using plug-ins listed under [CQ.form.rte.plugins.Plugin](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.Plugin). For each plug-in:

   * 有効化（または無効化）が可能な機能の詳細については「機能」を参照してください。
   * 該当するプラグインの詳細設定に使用可能なすべてのパラメーターについては、「設定オプション」を参照してください。

* リンクの HTML ルールに関する詳細も参照できます。

上記のオプションは、独自の RTE を拡張およびカスタマイズするために使用できます。例えば、リンク作成時にページで使用できるアンカーをリストするために、`LinkPlugin` を独自に実装できます。

## 既知の制限 {#known-limitations}

AEM RTE 機能には次の制限があります。

* RTE 機能は AEM コンポーネントダイアログでのみサポートされます。RTE は、ウィザードやタッチ操作向け UI の基盤フォーム（[ページプロパティ](../sites-developing/page-properties-views.md)や[基礎モード](../sites-authoring/scaffolding.md)など）ではサポートされません。

* AEM は[ハイブリッドデバイス](../release-notes/known-issues.md)では機能しません。

* Do not name the RTE configuration node `config`. Otherwise, the RTE configuration takes effect for only the administrators and not for the users in the group `content-author`.

* RTE は、コンテンツを埋め込むインラインフレームまたは iframe をサポートしていません。

>[!MORELIKETHIS]
>
>* [RTE プラグインの設定](configure-rich-text-editor-plug-ins.md)
>* [リッチテキストエディターをオーサリングに使用](../sites-authoring/rich-text-editor.md)
>* [RTE をアクセス可能なサイト用に設定](rte-accessible-content.md)
>* [タッチ UI とクラシック UI 機能の類似点](../release-notes/touch-ui-features-status.md)
>* [複合マルチフィールドコンポーネントを作成するためのチュートリアルサンプル](https://experience-aem.blogspot.com/2019/05/aem-65-touchui-composite-multifield-with-coral3-rte-rich-text.html)

