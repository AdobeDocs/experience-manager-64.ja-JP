---
title: フォームポータルページの作成
seo-title: Creating a forms portal page
description: フォームポータルでは、Web開発者にAdobe Experience Manager (AEM)を使用して作成されたWebサイトでフォームポータルを作成してカスタマイズするためのコンポーネントが支給されます。
seo-description: Forms Portal equips Web Developers with components to create and customize a forms portal on websites authored using Adobe Experience Manager (AEM).
uuid: 328f3342-d6ca-4413-9f1d-1a550df74bde
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: publish
discoiquuid: 7387dfe8-0029-4ad0-b319-fc519928318b
feature: Forms Portal
exl-id: 4d66ab64-a132-4f2a-89ca-3fbd8dc56ce2
source-git-commit: 977ada5fefe476c7cd2fe1470eb024a517a681d2
workflow-type: tm+mt
source-wordcount: '1646'
ht-degree: 68%

---

# フォームポータルページの作成 {#creating-a-forms-portal-page}

フォームポータルのコンポーネントでは、Web開発者にAdobe Experience Manager (AEM)を使用してフォームポータル用Webサイトを作成し、カスタマイズするためのコンポーネントが用意されています。フォームポータルの概要については、「[ポータル上でフォームを発行する](/help/forms/using/introduction-publishing-forms.md)」を参照してください。

## 前提条件 {#prerequisites}

デフォルトでは、フォームポータルコンポーネントは使用できません。「[フォームポータルのコンポーネントを有効にする](/help/forms/using/enabling-forms-portal-components.md)」の説明に従い、フォームポータルコンポーネントにおける次のカテゴリが有効になっていることを確認してください。

**ドキュメントサービス** 「Search &amp; Lister」、「Link」、「Drafts and Submissions 」の各コンポーネントが含まれます。

**Document Services Predicates**：「Date Predicate」、「Full Text Predicate」、「Properties Predicate」、および「Tags Predicate」のコンポーネントが含まれています。これらのコンポーネントは、「Search &amp; Lister」コンポーネントで検索を設定する際に使用します。

これらをAEMサイトのページで有効にすると、コンポーネントの各カテゴリはコンポーネントブラウザで使用でるようになります。

![コンポーネントブラウザー内のAEM Formsポータルコンポーネント](assets/component-categories.png)
**図：** *Forms portal コンポーネントのカテゴリ*

## Search &amp; Listerコンポーネント {#search-amp-lister-component}

「Document Services」のコンポーネントカテゴリにある「Search &amp; Lister」コンポーネントは、ページ上にフォームを一覧表示し、その中から検索を実行するのに使用されます。コンポーネントには、次の2つのペインが含まれます。

* フォームが一覧表示される「リスト」ペイン。
* 検索機能を追加する「検索」ペイン。

Search &amp; Lister コンポーネントは、コンポーネントブラウザーの Document Services コンポーネントカテゴリからページにドラッグ&amp;ドロップできます。 コンポーネントを追加すると、下記の画像のようになります。

![ページ内の Search &amp; Lister コンポーネント](assets/fp-grid-viw.png)
**図：** *グリッドレイアウトを持つページ内の Search &amp; Lister コンポーネント*

### 「リスト」ペイン {#list-pane}

リストペインはフォームが一覧表示される領域です。Search &amp; Lister コンポーネントは、リストペインでのフォームの表示を制御するために使用できる様々な設定オプションを提供します。

リストパネルを設定するには、「Search &amp; Lister」コンポーネントをタップし、 ![settings_icon](assets/settings_icon.png). この **[!UICONTROL コンポーネントを編集]** ダイアログが開きます。

![編集モードのリストペイン](assets/edit-list.png)
**図：** *編集モードのリストペイン*

「**[!UICONTROL 編集]**」ダイアログには複数のタブが含まれており、以下の表で説明される設定オプションを提供します。タップ **[!UICONTROL OK]** 設定を保存します（完了したら）。

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
   <td><p>結果のテキストを設定します（例えば、1-12/601の</strong>「結果」<strong>）。デフォルト値は<strong>「Results」</strong>です。</strong></p> <p>例えば、 <strong>Forms </strong>このフィールドに含まれるフォームの総数は 601 で、結果のテキストは 601 の 1 ～ 12 に変わります <strong>Forms。</strong></p> </td>
  </tr>
  <tr>
   <td> </td>
   <td>ページテキスト</td>
   <td><p>ページテキストを設定します ( 例： <strong>ページ </strong>1 / 51)。 デフォルト値は<strong>「ページ」</strong>です。</p> <p>例えば、 <strong>申し込みフォーム </strong>このフィールドと 51 ページがある場合、ページテキストは <strong>申し込みフォーム </strong>1 / 51.</p> </td>
  </tr>
  <tr>
   <td> </td>
   <td>/ テキスト</td>
   <td><p>次の単語を置き換えます。 <strong>/</strong> 指定したテキストを使用します（1 ページ目） <strong>/ </strong>51) を参照してください。 デフォルト値は <strong>/</strong> です。</p> <p>例えば、 <strong>～から </strong>このフィールドのテキストは「1 ページ目」に変わります。 <strong>～から </strong>51.</p> </td>
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
   <td>次を指定できます。 <strong>スタイルなし、デフォルトスタイル</strong>または <strong>カスタムスタイル </strong>フォームを一覧表示するために使用します。</td>
  </tr>
  <tr>
   <td> </td>
   <td>カスタムスタイルパス</td>
   <td>スタイルタイプとして「カスタム」を選択した場合、カスタム CSS へのパスを参照して指定します。そうでない場合、「デフォルト」を選択します。</td>
  </tr>
 </tbody>
</table>

### 検索ペイン {#search-pane}

検索ペインでは、サイドキックの「Document Services Predicates」カテゴリから、「Date Predicate」、「Full Text Predicate」、「Properties Predicate」、および「Tags Predicate」コンポーネントを追加することができます。これらのコンポーネントは、リストに表示されたフォームに対してユーザーが検索を実行するための検索機能を実装します。

**チップ：***フォームポータルに表示されるフォームのリストを既定の条件に基づいて制御し、エンドユーザーに対して検索機能を非表示にできます。フォームのリストを制御するには、検索フィルターを適用するためにPredicateコンポーネントを使用します。また、デフォルトのフィルター値を指定し、コンポーネントを編集ダイアログの「表示」タブで検索を無効にすることもできます。*

![日付、フルテキスト、プロパティおよびタグの述語を含む検索パネル](assets/search-with-predicates.png)
**図：** *日付、フルテキスト、プロパティおよびタグの述語を含む検索パネル*

#### 日付の述語 {#date-predicate}

「Date Predicate」コンポーネントが追加されている場合は、指定された期間に変更されたフォームについて、一覧表示されたフォームの中から検索できます。

「Date Predicate」コンポーネントを構成するには、次の手順を実行します。

1. コンポーネントをタップし、 ![settings_icon](assets/settings_icon.png). 編集ダイアログが開きます。
1. 以下のプロパティを指定します。

   * **[!UICONTROL タイプ：]** 次のオプションのみを使用できます。 **[!UICONTROL 最終変更日]**.
   * **[!UICONTROL テキスト：]** Date Predicateコンポーネントのラベルまたはキャプションです。デフォルト値は **[!UICONTROL 最終変更日]**.
   * **[!UICONTROL 開始日のラベル：]** 開始日フィールドのラベルまたはキャプション。
   * **[!UICONTROL 終了日のラベル：]** 終了日フィールドのラベルまたはキャプションです。
   * **[!UICONTROL 非表示：]** デフォルトの日付フィルターを適用してフォームを一覧表示する場合。

1. 「**[!UICONTROL OK]**」をタップします。

#### フルテキストの述語 {#full-text-predicate}

「Full Text Predicate」コンポーネントは、フォームデータに対して名前や説明などを検索する、フルテキスト検索を実装します。名前や説明にテキストを含む戻りフォームで、テキスト文字列を検索できます。

Full Text Predicate コンポーネントを構成するには、次の手順を実行します。

1. コンポーネントをタップし、 ![settings_icon](assets/settings_icon.png). 編集ダイアログが開きます。
1. 「**[!UICONTROL メインタイトル]**」フィールドにタイトルを指定します。
1. タップ **[!UICONTROL Ok]**.

#### プロパティの述語 {#properties-predicate}

Properties Predicateコンポーネントは、フォームプロパティ（タイトル、作成者および説明など）に基づいたフォームの検索機能を実装します。

Properties Predicate コンポーネントを構成するには、次の手順を実行します。

1. コンポーネントをタップし、 ![settings_icon](assets/settings_icon.png). この **[!UICONTROL 編集ダイアログ]** が開きます。
1. 内 **[!UICONTROL 一般]** 「 」タブで、検索ラベルを指定します。 デフォルト値は **[!UICONTROL プロパティ]**.

1. 内 **[!UICONTROL オプション]** タブ、タップ **[!UICONTROL 項目を追加]**.
1. ドロップダウンリストからプロパティを選択し、ドロップダウンリストの下のフィールドでプロパティの検索ラベルを指定します。
1. 手順 4 を繰り返してさらにプロパティを追加します。デフォルトのフィルター値を指定して、指定した条件に基づいてフォームを一覧表示し、エンドユーザーによる検索用のプロパティを非表示にすることもできます。 プロパティの「非表示」チェックボックスを選択し、デフォルトフィルター値を指定します。

   例えば、タイトルに「Travel」という文字を含むフォームを表示するには、「タイトル」プロパティ横の「非表示」を選択します。さらに、「デフォルトのフィルター値の移動」テキストボックスを指定します。

1. 「**[!UICONTROL OK]**」をタップします。

#### タグの述語 {#tags-predicate}

Tags Predicate コンポーネントは、Forms Manager で定義されているタグに基づいて、フォームの検索機能を実装します。

Tags Predicate コンポーネントを構成するには、次の手順を実行します。

1. コンポーネントをタップし、 ![settings_icon](assets/settings_icon.png). この **[!UICONTROL 編集ダイアログ]** が開きます。
1. 「タグ」フィールド横の下向き矢印ボタンをタップします。
1. 適切なタグを選択します。
1. 「**[!UICONTROL OK]**」をタップします。

選択したタグが、選択のためのチェックボックスと一緒に検索ペインに表示されます。ユーザーはこのタグに基づいて検索を絞り込めるようになります。

## ページ上でフォームを一覧表示 {#list-forms-on-a-page-br}

ページ上でフォームを一覧表示するには、そのページに&#x200B;**[!UICONTROL Search &amp; Listerコンポーネントを追加し、]**&#x200B;リストペインを設定します&#x200B;****。エンドユーザーが、日付、テキスト、およびタグでフォームを検索できるようにするには、**[!UICONTROL 検索ペイン]**&#x200B;コンポーネントを追加します。

ページ上の任意の場所からフォームにリンクするには、リンクコンポーネントを使用します。リンクコンポーネントについて詳しくは、 [ページへのリンクコンポーネントの埋め込み](/help/forms/using/embedding-link-component-page.md).

ドラフト状態で、既に送信済みのフォームをリストするには、「**[!UICONTROL ドラフト&amp;送信]**」コンポーネントを使用します。詳しくは、「[ドラフト・送信コンポーネントのカスタマイズ](/help/forms/using/draft-submission-component.md)」を参照してください。

## モバイルデバイスへの適合性 {#mobile-device-friendliness}

フォームポータルのSearch &amp; Listerコンポーネントは、モバイルデバイスフレンドリーで、デバイスに応じて表示幅を調整します。3 つのデフォルトビュー：Web ページも適応するので、サイトを開いたデバイスに応じてグリッド、カード、パネルが再レイアウトされます。 簡単に言えば、Search &amp; Listerは単なるコンポーネントであり、ページレベルのスタイリングは管理しません。

次の画像は、モバイルデバイス上で開いた場合の Search &amp; Lister コンポーネントを示します。

![Search &amp; Lister コンポーネントのスクリーンショット](assets/search_lister.png)
**図：** *Search &amp; Lister コンポーネント*

## フォームポータルページのカスタマイズ {#customizing-a-forms-portal-page-br}

フォームポータルページをカスタマイズすることで、特徴のある外観にすることができます。また、メタデータを追加することで、検索機能の改善、ページのレイアウト変更、およびカスタムCCSスタイルの追加を行うこともできます。詳しくは、 [Forms Portal コンポーネントのテンプレートのカスタマイズ](/help/forms/using/customizing-templates-forms-portal-components.md).

AEMフォームUIでは、カスタムメタデータをフォームに追加することができます。カスタムメタデータは、エンドユーザーに対してフォームの展開・検索機能を提供するのに役に立ちます。カスタムメタデータについて詳しくは、 [Forms Portal コンポーネントのテンプレートのカスタマイズ](/help/forms/using/customizing-templates-forms-portal-components.md).

フォームポータルは、デフォルトでレンダリングアクションを提供します。フォームポータルをカスタマイズして、他のオプションを追加することもできます。詳しくは、「[フォームリスター項目にカスタムアクションボタンを追加する](/help/forms/using/add-custom-action-form-lister.md)」を参照してください。

## 関連記事

* [フォームポータルコンポーネントの有効化](/help/forms/using/enabling-forms-portal-components.md)
* [フォームポータルページの作成](/help/forms/using/creating-form-portal-page.md)
* [API を使用した Web ページ上のフォームの一覧表示](/help/forms/using/listing-forms-webpage-using-apis.md)
* [ドラフトと送信コンポーネントの使用](/help/forms/using/draft-submission-component.md)
* [ドラフトと送信済みフォームのストレージのカスタマイズ](/help/forms/using/draft-submission-component.md)
* [ドラフトと送信コンポーネントとデータベースの統合のサンプル](/help/forms/using/integrate-draft-submission-database.md)
* [フォームポータルコンポーネントのテンプレートをカスタマイズする](/help/forms/using/customizing-templates-forms-portal-components.md)
* [ポータル上のフォーム発行の概要](/help/forms/using/introduction-publishing-forms.md)
