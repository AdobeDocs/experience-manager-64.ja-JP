---
title: ポータル上のフォーム発行の概要
seo-title: Introduction to publishing forms on a portal
description: AEM Forms はフォームポータルを構築するために使用できるコンポーネントを提供します。この記事では、使用可能なフォームポータルコンポーネントを紹介します。
seo-description: AEM Forms provides with components that you can use to build your forms portal. This articles introduces you to the available forms portal components.
uuid: 96aa4fe2-a111-4675-a33c-7dee8b82cbc2
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: publish
discoiquuid: 44871fe1-ddc9-492c-8784-5df3ca392f9b
source-git-commit: da7691a64cebd8c279ec72eca2a41c468a79f9fb
workflow-type: tm+mt
source-wordcount: '1055'
ht-degree: 58%

---


# ポータル上のフォーム発行の概要 {#introduction-to-publishing-forms-on-a-portal}

## AEM Forms ポータルコンポーネントの概要 {#aem-forms-portal-components-overview}

一般的なフォーム中心のポータル展開シナリオでは、フォームの開発とポータルの開発が別々に行われます。フォーム開発者はフォームを設計してリポジトリに保存する一方、Web 開発者は Web アプリケーションを作成してフォームを一覧表示し、フォームの送信を処理します。フォームリポジトリと Web アプリケーション間では通信が行われないため、フォームは Web 層にコピーされます。

このようなシナリオでは、管理問題が発生したり生産が遅延したりすることがよくあります。例えば、リポジトリで新しいバージョンのフォームを利用できる場合、Web 層でフォームを置換し、Web アプリケーションを変更し、公共サイトでフォームを再展開する必要があります。Web アプリケーションの再展開によって、サーバーのダウンタイムが発生する可能性があります。通常、サーバーのダウンタイムは計画的に行われるため、変更を瞬時に公共サイトにプッシュすることはできません。

AEM Forms は管理のオーバーヘッドと実稼働の遅延を低減するポータルコンポーネントを提供します。コンポーネントにより、Web 開発者は Adobe Experience Manager（AEM）を使用して作成された Web サイト上にフォームポータルを作成してカスタマイズできます。

![AEM Forms ポータル](assets/aem-forms-portal.png)

フォームポータルコンポーネントにより、次の機能が追加されます。

* カスタマイズしたレイアウトによってフォームを一覧表示する。リスト表示、カード表示、パネル表示用のレイアウトをすぐに使用できる。独自のカスタムレイアウトを作成する。
* 一覧表示からカスタムメタデータおよびカスタムアクションを表示する。
* フォームポータルコンポーネントを使用しているパブリッシュインスタンス上の AEM Forms UI によって発行されたフォームを一覧表示する。
* HTML 形式および PDF 形式でフォームをレンダリングする。 
* カスタム HTML プロファイルを使用してフォームをレンダリングする。
* さまざまな検索条件（フォームプロパティ、メタデータ、タグなど）に基づいたフォームの検索を有効にする。 
* フォームデータをサーブレットに送信する。
* カスタム CSS を使用してポータルの外観をカスタマイズする。 
* フォームへのリンクを作成する。
* エンドユーザーが作成したアダプティブフォームに関連するドラフトおよび送信を一覧表示する。

## 使用可能な AEM Forms ポータルコンポーネント {#available-aem-forms-portal-components}

AEM Forms はすぐに使える次のポータルコンポーネントを、**Document Services** および **Document Services Predicates** コンポーネントグループの下にグループ化して提供します。

### 検索とリスター {#search-amp-lister}

Search &amp; Lister コンポーネントは、フォームリポジトリのフォームをポータルページに一覧表示するほか、指定した検索条件に基づいてフォームを一覧表示するオプションを提供します。また、検索条件を指定することにより、ポータルユーザーがフォームの一覧から検索できるようにします。

### ドラフトと送信 {#drafts-amp-submissions}

Search &amp; Lister コンポーネントはフォーム作成者によって発行されたフォームを表示する一方、Drafts &amp; Submissions コンポーネントはドラフトとして保存され、後で完了して送信されるフォームを表示します。このコンポーネントはログインユーザーに対してパーソナライズされたエクスペリエンスを提供します。

### リンク {#link}

Link コンポーネントでは、ページ上の任意の場所にあるフォームへのリンクを作成できます。トレーニングプログラムを提供し、ユーザーがフォームを送信してトレーニングに登録できるようにするシナリオを検討します。お客様は当社の Web サイトに、プログラムの詳細を投稿しました。次に示す詳細に、登録フォームへのリンクを記述しています。Link コンポーネントはリンクの作成に役立ちます。

## Forms Portal のワークフロー {#forms-portal-workflow}

Forms portal を使用すると、フォームリポジトリからポータルページにフォームをリストできます。 また、検索条件を指定することにより、ポータルユーザーがフォームの一覧から検索できるようにします。また、ドラフトと送信コンポーネントを使用して、後で送信したフォームを完了するためにドラフトとして保存されたフォームを表示することもできます。 これらの機能を Sites ページで使用するには、一連の操作を実行する必要があります。 リストに表示された順序の手順を実行して、コンポーネントと各機能をサイトページで使用できるようにします。

1. **Forms Portal コンポーネントの有効化**:フォームポータルのコンポーネントは、デフォルトでは使用できません。 [AEMサイドキックからのコンポーネントの有効化](/help/forms/using/enabling-forms-portal-components.md) AEM Sitesページ用。
1. **ページ上のフォームを一覧表示する（フォームポータルページを作成する）:** AEM Sitesページと非AEM Site ページの両方でフォームを一覧表示できます。 リストには、パブリッシュインスタンスで使用できるフォームが含まれています。 ユーザーがフォームを開き、入力を開始できます。 ユーザーがフォームを開くたびに、フォームの新しいインスタンスが作成されます。

   1. **AEM Sitesページ上のフォームのリスト**:を **[Search &amp; Lister](/help/forms/using/creating-form-portal-page.md)** ページのコンポーネントと **[リストウィンドウ](/help/forms/using/creating-form-portal-page.md#p-list-pane-p)** ページ上のフォームのリストを作成します。 を追加して設定します。 **[検索ペイン](/help/forms/using/creating-form-portal-page.md#search-pane)** コンポーネント **Search &amp; Lister** コンポーネントを使用して、ページに検索機能を追加することもできます。 フォームポータルコンポーネントを含むページは、 [フォームポータルページ](/help/forms/using/creating-form-portal-page.md).
   1. **非AEM Sitesページ上のフォームのリスト：** 以下を使用： [フォームポータル検索 API](/help/forms/using/listing-forms-webpage-using-apis.md) を使用して、AEM Sites以外のページ上のフォームのクエリ、取得、リストを行います。

1. **フォームポータルページにドラフトフォームと送信済みフォームを一覧表示する**:ドラフトと送信コンポーネントをフォームポータルページに追加して設定します。 コンポーネントは、ドラフト状態のすべてのフォームと、既に送信済みのフォームをリストします。

   送信後のアダプティブフォームを「送信」タブに表示するには、 **送信アクション** から **[Forms Portal 送信アクション](https://helpx.adobe.com/in/experience-manager/6-4/forms/using/configuring-submit-actions.html).** または、「 Forms Portal 送信」オプションを有効にします。 ユーザーがフォームを送信するたびに、フォームは「送信」タブに追加されます。

1. **下書きおよび送信済みのフォームデータのストレージを設定します。** デフォルトでは、ドラフトと送信データはAEMリポジトリに保存されます。 実稼働環境では、ドラフトまたは送信されたフォームデータを AEM リポジトリに保存しないことをお勧めします。[安全な場所にデータを保存するためのフォームポータルコンポーネントの設定](/help/forms/using/draft-submission-component.md#customizing-the-storage).
1. **（オプション）フォームポータルコンポーネントのカスタマイズ：**  [フォームポータルのページテンプレートのカスタマイズ](/help/forms/using/customizing-templates-forms-portal-components.md) 部品に対して独特な外観を提供する。
1. **（オプション）カスタムメタデータをフォームに追加します。** [フォームへのカスタムメタデータの追加](/help/forms/using/customizing-templates-forms-portal-components.md) リストと検索の操作性を向上させる。
1. **フォームポータルページを発行します。** これで、フォームポータルページの準備が整いました。 ページを公開します。

## 関連記事 {#related-articles}

* [フォームポータルコンポーネントの有効化](/help/forms/using/enabling-forms-portal-components.md)
* [フォームポータルページの作成](/help/forms/using/creating-form-portal-page.md)
* [API を使用した Web ページ上のフォームの一覧表示](/help/forms/using/listing-forms-webpage-using-apis.md)
* [ドラフトと送信コンポーネントの使用](/help/forms/using/draft-submission-component.md)
* [ドラフトと送信済みフォームのストレージのカスタマイズ](/help/forms/using/draft-submission-component.md#customizing-the-storage)
* [ドラフトと送信コンポーネントとデータベースの統合のサンプル](https://helpx.adobe.com/in/experience-manager/6-4/forms/using/integrate-draft-submission-database.html)

* [フォームポータルコンポーネントのテンプレートをカスタマイズする](/help/forms/using/customizing-templates-forms-portal-components.md)
* [ポータル上のフォーム発行の概要](/help/forms/using/introduction-publishing-forms.md)

