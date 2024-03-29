---
title: フォームポータルページの作成
seo-title: Creating a forms portal page
description: Forms Portal では、Web 開発者に、Adobe Experience Manager(AEM) を使用して作成された Web サイトでフォームポータルを作成してカスタマイズするためのコンポーネントが支給されます。
seo-description: Forms Portal equips Web Developers with components to create and customize a forms portal on websites authored using Adobe Experience Manager (AEM).
uuid: 328f3342-d6ca-4413-9f1d-1a550df74bde
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: publish
discoiquuid: 7387dfe8-0029-4ad0-b319-fc519928318b
feature: Forms Portal
exl-id: 4d66ab64-a132-4f2a-89ca-3fbd8dc56ce2
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '1682'
ht-degree: 49%

---

# フォームポータルページの作成  {#creating-a-forms-portal-page}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

Formsポータルコンポーネントを使用すると、Web 開発者にAdobe Experience Manager(AEM) で作成された Web サイト上でフォームポータルを作成し、カスタマイズするためのコンポーネントが支給されます。 フォームポータルの概要については、 [ポータル上のフォーム発行の概要](/help/forms/using/introduction-publishing-forms.md).

## 前提条件 {#prerequisites}

Formsポータルのコンポーネントは、デフォルトでは使用できません。 以下のフォームポータルコンポーネントカテゴリが有効になっていることを確認します。詳しくは、 [フォームポータルコンポーネントの有効化](/help/forms/using/enabling-forms-portal-components.md).

**Document Services**：検索とリスター、リンクおよびドラフトと送信のコンポーネントが含まれています。

**Document Services の述語** 日付の述語、フルテキストの述語、プロパティの述語、タグの述語の各コンポーネントが含まれます。 これらのコンポーネントは、Search &amp; Lister コンポーネントで検索を設定するために使用されます。

AEMサイトページで有効にしたコンポーネントカテゴリは、コンポーネントブラウザーで使用できます。

![コンポーネントブラウザにおけるAEM Formsポータルコンポーネント](assets/component-categories.png)
**図：** *Forms portal コンポーネントのカテゴリ*

## Search &amp; Lister コンポーネント {#search-amp-lister-component}

Document Services コンポーネントカテゴリの下にある Search &amp; Lister コンポーネントは、ページ上のフォームのリストを表示し、リストに表示されたフォームに検索を実装するために使用されます。 このコンポーネントには、次の 2 つのペインが含まれます。

* フォームが一覧表示されるリストペイン。
* 検索機能を追加する検索ペイン。

検索とリスターコンポーネントは、コンポーネントブラウザの Document Services コンポーネントカテゴリからページまでドラッグ＆ドロップすることができます。コンポーネントを追加すると、下記の画像のようになります。

![ページ中のSearch &amp; Lister コンポーネント](assets/fp-grid-viw.png)
**図：** *グリッドレイアウトを持つページ内の Search &amp; Lister コンポーネント*

### リストウィンドウ {#list-pane}

リストペインはフォームが一覧表示される領域です。検索とリスターコンポーネントでは各種の設定オプションが提供されており、リストウィンドウでフォームの表示を制御するのに使用します。

リストウィンドウを設定するには、検索とリスターコンポーネントをタップし、![settings_icon](assets/settings_icon.png) をタップします。**[!UICONTROL 編集コンポーネント]**&#x200B;ダイアログが開きます。

![編集モードのリストペイン](assets/edit-list.png)
**図：** *編集モードのリストペイン*

「**[!UICONTROL 編集]**」ダイアログには複数のタブが含まれており、以下の表で説明される設定オプションを提供します。終わったら「**[!UICONTROL OK]**」をタップして、設定を保存します。

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
   <td>AEM Forms UI を使用してアセットがアップロードされるフォルダーを設定します。 デフォルトでは、アップロードされたすべてのアセットがリストされます。 AEM Forms UI について詳しくは、 <a href="/help/forms/using/introduction-managing-forms.md" target="_blank">フォーム管理の概要</a>.</td>
  </tr>
  <tr>
   <td><p><span class="uicontrol"><strong>ディスプレイ</strong></span></p> </td>
   <td>タイトルテキスト</td>
   <td>Search &amp; Lister コンポーネントのタイトル。 デフォルトのタイトルはです。 <strong>Forms Portal</strong></td>
  </tr>
  <tr>
   <td> </td>
   <td>テンプレートのレイアウト</td>
   <td>アセットのレイアウト </td>
  </tr>
  <tr>
   <td> </td>
   <td>詳細検索の無効化</td>
   <td>有効にすると、詳細検索アイコンが非表示になります。</td>
  </tr>
  <tr>
   <td> </td>
   <td>テキスト検索を無効にする</td>
   <td>有効にすると、全文検索バーが非表示になります。</td>
  </tr>
  <tr>
   <td><span class="uicontrol"><strong>結果</strong></span></td>
   <td>1 ページあたりの結果数</td>
   <td>ページに表示するフォームの最大数を設定します。</td>
  </tr>
  <tr>
   <td> </td>
   <td>結果のテキスト</td>
   <td><p>結果のテキストを設定します（例： 601 の 1-12） <strong>結果</strong>) をクリックします。 デフォルト値は <strong>結果</strong>.</p> <p>例えば、このフィールドで<strong>フォーム</strong>を指定し、合計 601 のフォームがある場合、結果のテキストは 1-12/601 の「<strong>Forms</strong>」に変わります。</p> </td>
  </tr>
  <tr>
   <td> </td>
   <td>ページテキスト</td>
   <td><p>ページテキストを設定します（例：1/51 <strong>ページ</strong>）。デフォルト値は<strong>「ページ」</strong>です。</p> <p>例えば、このフィールドに<strong>アプリケーションフォーム</strong>を指定し、ページが 51 ページある場合、ページテキストは 1/51 <strong>アプリケーションフォーム</strong>に変わります。</p> </td>
  </tr>
  <tr>
   <td> </td>
   <td>/ テキスト</td>
   <td><p>指定されたテキストの <strong>of</strong> という文字を指定したテキストに置き換えます（Page 1 <strong>of </strong>51）。デフォルト値は <strong>/</strong> です。</p> <p>例えば、このフィールドに <strong>out of </strong> を指定した場合、テキストは Page 1 <strong>out of </strong>51 に変わります。</p> </td>
  </tr>
  <tr>
   <td><span class="uicontrol"><strong>フォームリンク</strong></span></td>
   <td>レンダリングタイプ</td>
   <td>指定したレンダリングの種類に基づいてフォームのリストを制御します。 使用可能なオプションは、PDFとHTMLです。 例えば、レンダータイプとして「HTML」のみを選択した場合、PDF formsは除外されます。</td>
  </tr>
  <tr>
   <td> </td>
   <td>HTMLプロファイル</td>
   <td>レンダリングに使用するHTMLプロファイルを設定します。 使用可能なすべてのプロファイルがドロップダウンリストに表示されます。</td>
  </tr>
  <tr>
   <td> </td>
   <td>送信 URL</td>
   <td><p>フォームデータが送信されるサーブレットを設定します。</p> <p><strong>注意：</strong> <em>フォームの送信 URL は複数の場所で指定でき、優先順位は次のとおりです。</em></p>
    <ol>
     <li><em>優先順位が最も高いのは、フォームに埋め込まれている送信URL（送信ボタン）です。</em></li>
     <li><em>2番目に優先順位が高いのは、AEM Forms UIで説明している送信URLです。</em></li>
     <li><em>一番優先順位が引くのが、フォームポータルで説明している送信URLです。</em></li>
    </ol> </td>
  </tr>
  <tr>
   <td> </td>
   <td>HTMLレンダリングアクションツールチップ</td>
   <td>ポインターを合わせたときに表示されるツールヒントのテキストを設定します <img height="16" src="assets/aem6forms_panel-html.png" width="13" /> (HTML5 アイコン )。</td>
  </tr>
  <tr>
   <td> </td>
   <td>PDFレンダリングアクションツールチップ</td>
   <td>ポインターを合わせたときに表示されるツールヒントのテキストを設定します <img height="16" src="assets/aem6forms_panel-pdf.png" width="14" /> (PDFアイコン )。</td>
  </tr>
  <tr>
   <td><span class="uicontrol"><strong>スタイル</strong></span></td>
   <td>スタイルタイプ</td>
   <td>フォームのリスト表示には、<strong>書式なし、デフォルトスタイル</strong>または<strong>カスタムスタイル</strong>を指定できます。</td>
  </tr>
  <tr>
   <td> </td>
   <td>カスタムスタイルパス</td>
   <td>スタイルタイプとして「カスタム」を選択した場合は、カスタム CSS へのパスを参照して指定します。選択しない場合は、「デフォルト」を選択します。</td>
  </tr>
 </tbody>
</table>

### 検索ペイン {#search-pane}

検索ペインでは、サイドキックの「Document Services Predicates」カテゴリから、「Date Predicate」、「Full Text Predicate」、「Properties Predicate」、および「Tags Predicate」コンポーネントを追加することができます。これらのコンポーネントにより、一覧表示されるフォームに対してユーザーが検索を実行するための検索機能が実装されます。

**チップ：** *フォームポータルに表示されるフォームのリストを既定の条件に基づいて制御し、エンドユーザーに対して検索機能を非表示にできます。フォームのリストを制御するには、検索フィルターを適用するためにPredicateコンポーネントを使用します。デフォルトフィルター値を指定して、コンポーネントの編集ダイアログの「表示」タブで検索を無効にすることもできます。*

![日付、フルテキスト、プロパティ、およびTags Predicate付きの検索パネル](assets/search-with-predicates.png)
**図：** *日付、フルテキスト、プロパティおよびタグの述語を含む検索パネル*

#### 日付の述語 {#date-predicate}

「 Date Predicate 」コンポーネントを追加すると、リストに表示されているフォームで、指定した期間に変更された検索が可能になります。

Date Predicate コンポーネントを設定するには、次の手順を実行します。

1. コンポーネントをタップし、![settings_icon](assets/settings_icon.png) をタップします。編集ダイアログが開きます。
1. 以下のプロパティを指定します。

   * **[!UICONTROL タイプ：]**&#x200B;選択できるオプションは「**[!UICONTROL 最終変更日]**」のみです。。
   * **[!UICONTROL テキスト：]** Date Predicateコンポーネントのラベルまたはキャプションです。デフォルト値は **[!UICONTROL 最終変更日]**.
   * **[!UICONTROL 開始日のラベル：]** 開始日フィールドのラベルまたはキャプション。
   * **[!UICONTROL 終了日のラベル：]** 終了日フィールドのラベルまたはキャプションです。
   * **[!UICONTROL 非表示：]** デフォルトの日付フィルターを適用してフォームを一覧表示する場合。

1. 「**[!UICONTROL OK]**」をタップします。

#### フルテキストの述語 {#full-text-predicate}

Full Text Predicate コンポーネントは、名前や説明などのフォームデータに対するフルテキスト検索を実装します。 ユーザーは任意のテキスト文字列を検索して、名前や説明にテキストが含まれるフォームを返すことができます。

Full Text Predicate コンポーネントを設定するには、次の手順を実行します。

1. コンポーネントをタップし、![ettings_icon](assets/settings_icon.png) をタップします。編集ダイアログが開きます。
1. 「**[!UICONTROL メインタイトル]**」フィールドにタイトルを指定します。
1. タップ **[!UICONTROL Ok]**.

#### プロパティの述語 {#properties-predicate}

Properties Predicate コンポーネントは、タイトル、作成者、説明などのフォームプロパティに基づいたフォームの検索機能を実装します。

Properties Predicate コンポーネントを設定するには、次の手順を実行します。

1. コンポーネントをタップし、![settings_icon](assets/settings_icon.png) をタップします。この **[!UICONTROL 編集ダイアログ]** が開きます。
1. 内 **[!UICONTROL 一般]** 「 」タブで、検索ラベルを指定します。 デフォルト値は **[!UICONTROL プロパティ]**.

1. 内 **[!UICONTROL オプション]** タブ、タップ **[!UICONTROL 項目を追加]**.
1. ドロップダウンリストからプロパティを選択し、ドロップダウンリストの下のフィールドでプロパティの検索ラベルを指定します。
1. 手順 4 を繰り返してさらにプロパティを追加します。デフォルトのフィルター値を指定して、指定の条件に基づいてフォームをリスト表示したり、エンドユーザーごとに検索のプロパティを非表示にしたりできます。プロパティの「非表示」チェックボックスを選択し、デフォルトフィルター値を指定します。

   例えば、タイトルに「Travel」という文字を含むフォームを表示するには、「タイトル」プロパティ横の「非表示」を選択します。さらに、デフォルトフィルター値のテキストボックスで Travel と指定します。

1. 「**[!UICONTROL OK]**」をタップします。

#### タグの述語 {#tags-predicate}

Tags Predicate コンポーネントは、Forms Manager で定義されたタグに基づいて、フォームの検索機能を実装します。

Tags Predicate コンポーネントを設定するには：

1. コンポーネントをタップし、![settings_icon](assets/settings_icon.png) をタップします。この **[!UICONTROL 編集ダイアログ]** が開きます。
1. 「タグ」フィールド横の下向き矢印ボタンをタップします。
1. 適切なタグを選択します。
1. 「**[!UICONTROL OK]**」をタップします。

選択したタグが、選択用のチェックボックスと共に検索パネルに表示されます。 ユーザーはこのタグに基づいて検索を絞り込めるようになります。

## ページ上でフォームを一覧表示 {#list-forms-on-a-page-br}

ページ上でフォームを一覧表示するには、そのページに **[!UICONTROL Search &amp; Lister]** コンポーネントを追加し、**[!UICONTROL リストペイン]**&#x200B;を設定します。エンドユーザーが日付、テキスト、タグ付きのフォームを検索できるようにするには、 **[!UICONTROL 検索ペイン]** コンポーネント。

ページ上の任意の場所からフォームをリンクするには、リンクコンポーネントを使用します。 リンクコンポーネントについての詳細は、「[ページ内のリンクコンポーネントの埋め込み](/help/forms/using/embedding-link-component-page.md)」を参照してください。

ドラフト状態のフォームと、既に送信済みのフォームを一覧表示するには、 **[!UICONTROL ドラフトと送信]** コンポーネント。 詳しくは、 [ドラフトと送信コンポーネントのカスタマイズ](/help/forms/using/draft-submission-component.md).

## モバイルデバイスへの対応 {#mobile-device-friendliness}

Forms Portal Search &amp; Lister コンポーネントは、モバイルデバイスに適したコンポーネントです。 3 つすべてのデフォルトビュー：グリッド、カード、パネルは、web ページにも適応するという事実を踏まえて、デバイスに応じて再レイアウトされます。簡単な事実は、Search &amp; Lister は単なるコンポーネントであり、ページレベルのスタイル設定は管理しないということです。

次の画像は、モバイルデバイスで開いた際の Search &amp; Lister コンポーネントを示しています。

![Search &amp; Listerコンポーネントのスクリーンショット](assets/search_lister.png)
**図：** *Search &amp; Lister コンポーネント*

## フォームポータルページのカスタマイズ {#customizing-a-forms-portal-page-br}

フォームポータルページをカスタマイズすることで、特徴のある外観にすることができます。また、メタデータを追加することで、検索機能の改善、ページのレイアウト変更、およびカスタム CSS スタイルの追加を行うこともできます。詳しくは、「[フォームポータルコンポーネント用テンプレートのカスタマイズ](/help/forms/using/customizing-templates-forms-portal-components.md)」を参照してください。

AEM Forms UIでは、カスタムメタデータをフォームに追加することができます。カスタムメタデータは、フォームの一覧表示と検索の操作をエンドユーザーに提供する際に役立ちます。 カスタムメタデータについて詳しくは、「[フォームポータルコンポーネント用テンプレートのカスタマイズ](/help/forms/using/customizing-templates-forms-portal-components.md)」を参照してください。

デフォルトでは、フォームポータルはレンダリングアクションを提供します。 フォームポータルをカスタマイズして、その他のアクションを追加できます。 詳しくは、 [フォームリスター項目にカスタムアクションを追加する。](/help/forms/using/add-custom-action-form-lister.md)

## 関連記事

* [フォームポータルコンポーネントの有効化](/help/forms/using/enabling-forms-portal-components.md)
* [フォームポータルページの作成 ](/help/forms/using/creating-form-portal-page.md)
* [API を使用した Web ページ上のフォームの一覧表示](/help/forms/using/listing-forms-webpage-using-apis.md)
* [ドラフトと送信コンポーネントの使用](/help/forms/using/draft-submission-component.md)
* [ドラフトと送信済みフォームのストレージのカスタマイズ](/help/forms/using/draft-submission-component.md)
* [ドラフトと送信コンポーネントとデータベースの統合のサンプル](/help/forms/using/integrate-draft-submission-database.md)
* [フォームポータルコンポーネントのテンプレートをカスタマイズする](/help/forms/using/customizing-templates-forms-portal-components.md)
* [ポータル上のフォーム発行の概要](/help/forms/using/introduction-publishing-forms.md)
