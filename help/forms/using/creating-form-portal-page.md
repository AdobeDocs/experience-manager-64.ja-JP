---
title: フォームポータルページの作成
seo-title: フォームポータルページの作成
description: フォームポータルでは、Web開発者にAdobe Experience Manager (AEM)を使用して作成されたWebサイトでフォームポータルを作成してカスタマイズするためのコンポーネントが支給されます。
seo-description: フォームポータルでは、Web開発者にAdobe Experience Manager (AEM)を使用して作成されたWebサイトでフォームポータルを作成してカスタマイズするためのコンポーネントが支給されます。
uuid: 328f3342-d6ca-4413-9f1d-1a550df74bde
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: publish
discoiquuid: 7387dfe8-0029-4ad0-b319-fc519928318b
translation-type: tm+mt
source-git-commit: 1ebe1e871767605dd4295429c3d0b4de4dd66939
workflow-type: tm+mt
source-wordcount: '1622'
ht-degree: 69%

---


# フォームポータルページの作成 {#creating-a-forms-portal-page}

フォームポータルのコンポーネントでは、Web開発者にAdobe Experience Manager (AEM)を使用してフォームポータル用Webサイトを作成し、カスタマイズするためのコンポーネントが用意されています。フォームポータルの概要については、「[ポータル上でフォームを発行する](/help/forms/using/introduction-publishing-forms.md)」を参照してください。

## 前提条件 {#prerequisites}

デフォルトでは、フォームポータルコンポーネントは使用できません。「[フォームポータルのコンポーネントを有効にする](/help/forms/using/enabling-forms-portal-components.md)」の説明に従い、フォームポータルコンポーネントにおける次のカテゴリが有効になっていることを確認してください。

**ドキュメントサービス** :Search &amp; Lister、Link、Drafts and Submissionsコンポーネントが含まれます。

**Document Services Predicates**：「Date Predicate」、「Full Text Predicate」、「Properties Predicate」、および「Tags Predicate」のコンポーネントが含まれています。これらのコンポーネントは、「Search &amp; Lister」コンポーネントで検索を設定する際に使用します。

これらをAEMサイトのページで有効にすると、コンポーネントの各カテゴリはコンポーネントブラウザで使用でるようになります。

![コンポーネントブラウザ](assets/component-categories.png)**図のAEM Formsポータルコンポーネント：** *Formsポータルコンポーネントカテゴリ*

## Search &amp; Lister コンポーネント {#search-amp-lister-component}

「Document Services」のコンポーネントカテゴリにある「Search &amp; Lister」コンポーネントは、ページ上にフォームを一覧表示し、その中から検索を実行するのに使用されます。コンポーネントには、次の2つのペインが含まれます。

* フォームが一覧表示される「リスト」ペイン。
* 検索機能を追加する「検索」ペイン。

「Search &amp; Lister」コンポーネントは、コンポーネントブラウザーの「ドキュメントサービス」コンポーネントカテゴリからページにドラッグ&amp;ドロップできます。 コンポーネントを追加すると、下記の画像のようになります。

![ページ](assets/fp-grid-viw.png)**図のSearch &amp; Listerコンポーネント：** *グリッドレイアウトを持つページ内のSearch &amp; Listerコンポーネント*

### リストペイン {#list-pane}

リストペインはフォームが一覧表示される領域です。Search &amp; Listerコンポーネントには、リストペインでのフォームの表示を制御するために使用できる様々な設定オプションが用意されています。

To configure the List pane, tap the Search and Lister component and then tap ![settings_icon](assets/settings_icon.png). The **[!UICONTROL Edit Component]** dialog opens.

![編集モードのリストペイン](assets/edit-list.png)**図：** *編集モードのリストペイン*

「**[!UICONTROL 編集]**」ダイアログには複数のタブが含まれており、以下の表で説明される設定オプションを提供します。Tap **[!UICONTROL OK]** to save the configuration, when done.

<table> 
 <tbody> 
  <tr> 
   <th>タブ</th> 
   <th>設定</th> 
   <th>説明</th> 
  </tr> 
  <tr> 
   <td><span class="uicontrol"><strong>アセットフォルダー</strong></span></td> 
   <td>項目を追加</td> 
   <td>アセットのアップロード先フォルダーを、AEM FormsのUIから設定します。デフォルトでは、アップロードされたすべてのアセットが一覧表示されます。AEM Forms の UI に関する詳細は、「<a href="/help/forms/using/introduction-managing-forms.md" target="_blank">フォーム管理の概要</a>」を参照してください。</td> 
  </tr> 
  <tr> 
   <td><p><span class="uicontrol"><strong>ディスプレイ</strong></span></p> </td> 
   <td>タイトルテキスト</td> 
   <td>Search &amp; Listerコンポーネントのタイトルデフォルトのタイトルは<strong>フォームポータルです。</strong></td> 
  </tr> 
  <tr> 
   <td> </td> 
   <td>テンプレートのレイアウト</td> 
   <td>アセットのレイアウト </td> 
  </tr> 
  <tr> 
   <td> </td> 
   <td>詳細検索の無効化</td> 
   <td>このオプションを有効にすると、詳細検索アイコンが非表示になります。</td> 
  </tr> 
  <tr> 
   <td> </td> 
   <td>テキスト検索の無効化</td> 
   <td>このオプションを有効にすると、全文検索バーが非表示になります。</td> 
  </tr> 
  <tr> 
   <td><span class="uicontrol"><strong>結果</strong></span></td> 
   <td>ページごとの結果の数</td> 
   <td>ページに表示するフォームの最大数を設定します。</td> 
  </tr> 
  <tr> 
   <td> </td> 
   <td>結果のテキスト</td> 
   <td><p>結果のテキストを設定します（例えば、1-12/601の</strong>「結果」<strong>）。デフォルト値は<strong>「Results」</strong>です。</strong></p> <p>For example, if you specify <strong>Forms </strong>in this field and there are a total of 601 forms, the result text changes to 1-12 of 601 <strong>Forms.</strong></p> </td> 
  </tr> 
  <tr> 
   <td> </td> 
   <td>ページテキスト</td> 
   <td><p>Configures the page text (for example, <strong>Page </strong>1 of 51). デフォルト値は<strong>「ページ」</strong>です。</p> <p>For example, if you specify <strong>Application Form </strong>in this field and there are 51 pages, the page text changes to <strong>Application Form </strong>1 of 51.</p> </td> 
  </tr> 
  <tr> 
   <td> </td> 
   <td>/ テキスト</td> 
   <td><p>Replaces the word <strong>of</strong> with the specified text (Page 1 <strong>of </strong>51). デフォルト値は <strong>/</strong> です。</p> <p>For example, if you specify <strong>out of </strong>in this field, the text changes to Page 1 <strong>out of </strong>51.</p> </td> 
  </tr> 
  <tr> 
   <td><span class="uicontrol"><strong>フォームリンク</strong></span></td> 
   <td>レンダリングタイプ</td> 
   <td>指定したレンダリングタイプに基づいて、フォームのリストをコントロールします。使用可能なオプションは「PDF」と「HTML」です。例えば、レンダリングタイプとして HTML のみを指定した場合は、PDF フォームが除外されます。</td> 
  </tr> 
  <tr> 
   <td> </td> 
   <td>HTML プロファイル</td> 
   <td>レンダリングに使用されるHTMLプロファイルを設定します。使用可能なすべてのプロファイルがドロップダウンリストに一覧表示されます。</td> 
  </tr> 
  <tr> 
   <td> </td> 
   <td>送信 URL</td> 
   <td><p>フォームデータが送信されるサーブレットを設定します。</p> <p><strong>注意：</strong><em>フォームの送信 URL は、複数の場所で指定できます。また、その優先順位は以下の通りです。</em></p> 
    <ol> 
     <li><em>優先順位が最も高いのは、フォームに埋め込まれている送信URL（送信ボタン）です。</em></li> 
     <li><em>2番目に優先順位が高いのは、AEMフォームUIで説明している送信URLです。</em></li> 
     <li><em>一番優先順位が引くのが、フォームポータルで説明している送信URLです。</em></li> 
    </ol> </td> 
  </tr> 
  <tr> 
   <td> </td> 
   <td>HTMLレンダリングアクションのツールチップ</td> 
   <td>（HTML5のアイコン）<img height="16" src="assets/aem6forms_panel-html.png" width="13" />の上にマウスを置くと表示されるツールチップのテキストを設定します。</td> 
  </tr> 
  <tr> 
   <td> </td> 
   <td>PDFレンダリングアクションのツールチップ</td> 
   <td><img height="16" src="assets/aem6forms_panel-pdf.png" width="14" /> （PDF のアイコン）の上にマウスのポインターを置くと表示されるツールチップのテキストを設定します。</td> 
  </tr> 
  <tr> 
   <td><span class="uicontrol"><strong>スタイル</strong></span></td> 
   <td>スタイルタイプ</td> 
   <td>Allows you to specify <strong>No Style, Default Style</strong>, or <strong>Custom Style </strong>for listing the forms.</td> 
  </tr> 
  <tr> 
   <td> </td> 
   <td>カスタムスタイルパス</td> 
   <td>スタイルタイプとして「カスタム」を選択した場合、カスタム CSS へのパスを参照して指定します。そうでない場合、「デフォルト」を選択します。</td> 
  </tr> 
 </tbody> 
</table>

### 検索ペイン {#search-pane}

検索ペインでは、サイドキックの「Document Services Predicates」カテゴリから、「Date Predicate」、「Full Text Predicate」、「Properties Predicate」、および「Tags Predicate」コンポーネントを追加することができます。これらのコンポーネントは、リストに表示されるフォームに対してユーザーが検索を実行するための検索機能を実装します。

**チップ：***フォームポータルに表示されるフォームのリストを既定の条件に基づいて制御し、エンドユーザーに対して検索機能を非表示にできます。フォームのリストを制御するには、検索フィルターを適用するためにPredicateコンポーネントを使用します。You can also specify the default filter values and disable the search from the Display tab of the Edit Component dialog.*

![日付、フルテキスト、プロパティ、およびTags Predicate](assets/search-with-predicates.png)**図を含む検索パネル：** *日付、フルテキスト、プロパティ、およびTags Predicate付きの検索パネル*

#### 日付の述語 {#date-predicate}

「Date Predicate」コンポーネントが追加されている場合は、指定された期間に変更されたフォームについて、一覧表示されたフォームの中から検索できます。

「Date Predicate」コンポーネントを構成するには、次の手順を実行します。

1. Tap the component and then tap ![settings_icon](assets/settings_icon.png). 編集ダイアログが開きます。
1. 以下のプロパティを指定します。

   * **[!UICONTROL タイプ：]** 使用できるオプションは「 **[!UICONTROL 最終変更日]**」のみです。
   * **[!UICONTROL テキスト：]** Date Predicateコンポーネントのラベルまたはキャプションです。The default value is **[!UICONTROL Last Modified Date]**.
   * **[!UICONTROL 開始日ラベル：]** 開始の日付フィールドのラベルまたはキャプション。
   * **[!UICONTROL 終了日のラベル：]** 終了日フィールドのラベルまたはキャプション。
   * **[!UICONTROL 非表示：]** リストフォームにデフォルトの日付フィルタを適用する場合。

1. 「**[!UICONTROL OK]**」をタップします。

#### フルテキストの述語 {#full-text-predicate}

「Full Text Predicate」コンポーネントは、フォームデータに対して名前や説明などを検索する、フルテキスト検索を実装します。名前や説明にテキストを含む戻りフォームで、テキスト文字列を検索できます。

Full Text Predicate コンポーネントを構成するには、次の手順を実行します。

1. Tap the component and then tap ![settings_icon](assets/settings_icon.png). 編集ダイアログが開きます。
1. 「**[!UICONTROL メインタイトル]**」フィールドにタイトルを指定します。
1. Tap **[!UICONTROL Ok]**.

#### プロパティの述語 {#properties-predicate}

Properties Predicateコンポーネントは、フォームプロパティ（タイトル、作成者および説明など）に基づいたフォームの検索機能を実装します。

Properties Predicate コンポーネントを構成するには、次の手順を実行します。

1. Tap the component and then tap ![settings_icon](assets/settings_icon.png). The **[!UICONTROL Edit dialog]** opens.
1. In the **[!UICONTROL General]** tab, specify the search label. The default value is **[!UICONTROL Properties]**.

1. In the **[!UICONTROL Options]** tab, tap **[!UICONTROL Add Item]**.
1. ドロップダウンリストからプロパティを選択し、ドロップダウンリストの下のフィールドでプロパティの検索ラベルを指定します。
1. 手順 4 を繰り返してさらにプロパティを追加します。また、指定した条件に基づいてリストフォームにデフォルトのフィルター値を指定し、エンドユーザーによる検索でプロパティを非表示にすることもできます。 プロパティの「非表示」チェックボックスを選択し、デフォルトフィルター値を指定します。

   例えば、タイトルに「Travel」という文字を含むフォームを表示するには、「タイトル」プロパティ横の「非表示」を選択します。さらに、デフォルトのフィルター値のテキストボックスで「Travel」を指定します。

1. 「**[!UICONTROL OK]**」をタップします。

#### タグの述語 {#tags-predicate}

Tags Predicate コンポーネントは、Forms Manager で定義されているタグに基づいて、フォームの検索機能を実装します。

Tags Predicate コンポーネントを構成するには、次の手順を実行します。

1. Tap the component and then tap ![settings_icon](assets/settings_icon.png). The **[!UICONTROL Edit dialog]** opens.
1. 「タグ」フィールド横の下向き矢印ボタンをタップします。
1. 適切なタグを選択します。
1. 「**[!UICONTROL OK]**」をタップします。

選択したタグが、選択のためのチェックボックスと一緒に検索ペインに表示されます。ユーザーはこのタグに基づいて検索を絞り込めるようになります。

## ページ上でフォームを一覧表示 {#list-forms-on-a-page-br}

ページ上でフォームを一覧表示するには、そのページに&#x200B;**[!UICONTROL Search &amp; Listerコンポーネントを追加し、]**&#x200B;リストペインを設定します&#x200B;****。エンドユーザーが、日付、テキスト、およびタグでフォームを検索できるようにするには、**[!UICONTROL 検索ペイン]**&#x200B;コンポーネントを追加します。

ページ上の任意の場所からフォームにリンクするには、リンクコンポーネントを使用します。For more information about link component, see [Embedding link component in a page](/help/forms/using/embedding-link-component-page.md).

ドラフト状態で、既に送信済みのフォームをリストするには、「**[!UICONTROL ドラフト&amp;送信]**」コンポーネントを使用します。詳しくは、「[ドラフト・送信コンポーネントのカスタマイズ](/help/forms/using/draft-submission-component.md)」を参照してください。

## モバイルデバイスへの適合性 {#mobile-device-friendliness}

フォームポータルのSearch &amp; Listerコンポーネントは、モバイルデバイスフレンドリーで、デバイスに適応します。3つのデフォルト表示すべて： Webページの幅が調整される場合、グリッド、カード、パネルは、サイトが開かれたデバイスに応じて再レイアウトされます。 簡単に言えば、Search &amp; Listerは単なるコンポーネントであり、ページレベルのスタイリングは管理しません。

次の画像は、モバイルデバイス上で開いた場合の Search &amp; Lister コンポーネントを示します。

![Search &amp; Listerコンポーネント](assets/search_lister.png)**図のスクリーンショット：** *Search &amp; Listerコンポーネント*

## フォームポータルページのカスタマイズ {#customizing-a-forms-portal-page-br}

フォームポータルページをカスタマイズすることで、特徴のある外観にすることができます。また、メタデータを追加することで、検索機能の改善、ページのレイアウト変更、およびカスタムCCSスタイルの追加を行うこともできます。For more information, see [Customizing templates for Forms Portal Components](/help/forms/using/customizing-templates-forms-portal-components.md).

AEMフォームUIでは、カスタムメタデータをフォームに追加することができます。カスタムメタデータは、エンドユーザーに対してフォームの展開・検索機能を提供するのに役に立ちます。For more information about Custom metadata, see [Customizing templates for Forms Portal Components](/help/forms/using/customizing-templates-forms-portal-components.md).

フォームポータルは、デフォルトでレンダリングアクションを提供します。フォームポータルをカスタマイズして、他のオプションを追加することもできます。詳しくは、「[フォームリスター項目にカスタムアクションボタンを追加する](/help/forms/using/add-custom-action-form-lister.md)」を参照してください。
