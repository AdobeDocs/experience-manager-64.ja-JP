---
title: コミュニティ機能
seo-title: コミュニティ機能
description: コミュニティ機能コンソールにアクセスする方法を説明します
seo-description: コミュニティ機能コンソールにアクセスする方法を説明します
uuid: 5cce05f5-1dd7-496d-94c2-8fccc0177d13
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.4/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: cc993b71-e2f2-48e7-ad4e-469cb5ce2dc1
translation-type: tm+mt
source-git-commit: 28948f1f8678512f8fc970a4289cb01cde86c5c2
workflow-type: tm+mt
source-wordcount: '2542'
ht-degree: 48%

---


# コミュニティ機能 {#community-functions}

コミュニティに必要とされる機能の種類はだいたい決まっています。コミュニティ機能はコミュニティ機能として利用できます。 基本的に、これらは、コミュニティ機能を実装するために事前に配線された1つ以上のページです。コミュニティ機能を実装するには、作成者モードでページにコンポーネントを追加する以外にも必要です。 They are the building blocks used to define the structure of a [community site template](sites.md) from which community sites are [created](sites-console.md).

Once a community site is created, content may be added to the resulting pages using the standard [AEM authoring mode](../../help/sites-authoring/editing-content.md).

コミュニティ機能コンソールには数多くのコミュニティ機能が用意されており、すぐに使用できます。今後のリリースでは、より多くのコミュニティ関数が提供される予定です。また、カスタム関数も作成される可能性があります。

>[!NOTE]
>
>The consoles for the creation of [community sites](sites-console.md), [community site templates](sites.md), [community group templates](tools-groups.md) and [community functions](functions.md) are for use only in the author environment.

## Community Functions Console {#community-functions-console}

オーサー環境でコミュニティ機能コンソールに移動するには、

* From global navigation: **[!UICONTROL Tools > Communities > Community Functions]**

![chlimage_1-379](assets/chlimage_1-379.png)

## 標準で提供される機能 {#pre-built-functions}

AEM Communities で提供される機能を以下で簡単に説明します。Each function is comprised of one or more AEM pages containing Communities components wired together into a feature that is easily incorporated into a [community site template](sites.md).

コミュニティサイトテンプレートは、ログイン、ユーザープロファイル、通知、メッセージング、サイトメニュー、検索、テーマ、ブランディング機能など、コミュニティサイトの構造を定義します。

### タイトルと URL の設定 {#title-and-url-settings}

**タイトル**&#x200B;と **URL** は、すべてのコミュニティ機能に共通するプロパティです。

コミュニティ機能をコミュニティサイトテンプレートに追加するか、コミュニティサイトの構造を[変更](sites-console.md#modifying-site-properties)すると、その機能のダイアログが開き、タイトルと URL を設定できます。

#### 設定機能の詳細 {#configuration-function-details}

![chlimage_1-380](assets/chlimage_1-380.png)

* **[!UICONTROL タイトル]**
(
*required*)サイトの機能のメニューに表示されるテキスト

* **[!UICONTROL URL]**(*必須*)URIの生成に使用する名前。 The name must conform to the [naming conventions](../../help/sites-developing/naming-conventions.md) imposed by AEM and JCR.

例えば、[使用の手引き](getting-started.md)のチュートリアルに従って作成したサイトを使用し、

* タイトル = Web ページ
* URL = page

次に、ページのURLがhttp://local_host:4503/content/sites/engage/en/page.htmlになり、そのページのメニューリンクが次のように表示されます。

![chlimage_1-381](assets/chlimage_1-381.png)

### アクティビティストリーム機能 {#activity-stream-function}

アクティビティストリーム機能は、選択されたすべてのビュー（すべてのアクティビティ、ユーザーアクティビティおよびフォロー）を備えた[アクティビティストリームコンポーネント](activities.md)を含むページです。See also [Activity Stream Essentials](essentials-activities.md) for developers.

テンプレートに追加すると、次のダイアログが開きます。

#### 設定機能の詳細 {#configuration-function-details-1}

![chlimage_1-382](assets/chlimage_1-382.png)

* See [Title and URL Settings](#title-and-url-settings)
* **[!UICONTROL [マイアクティビティ]表示を表示する]**]オンにすると、アクティビティページに、現在のメンバーによってコミュニティ内で生成されたフィルターに基づいてアクティビティを行うタブが含まれます。 初期設定はオンです。

* **[!UICONTROL [すべてのアクティビティ]表示を表示する]**]オンにすると、アクティビティページにタブが含まれ、現在のメンバがアクセス権を持つコミュニティ内で生成されたすべてのアクティビティが含まれます。 初期設定はオンです。

* **[!UICONTROL 「ニュースフィード」表示を表示]**：オンにすると、アクティビティページに、現在のメンバーに基づくフィルターアクティビティがフォローしているのタブが含まれます。 初期設定はオンです。

### 割り当て機能 {#assignments-function}

The assignments function is the basic feature which defines a [community site for enablement](overview.md#enablement-community). コミュニティのメンバーに有効化リソースを割り当てることができます。 See also [Assignments Essentials](essentials-assignments.md) for developers.

This function is available as a feature of the [enablement add-on](enablement.md). 有効化アドオンは、実稼働環境で使用するために追加のライセンスが必要です。

テンプレートへの追加時には、[タイトルと URL 設定](#title-and-url-settings)のみを設定します。

### ブログ機能 {#blog-function}

ブログ機能は、タグ付け、ファイルのアップロード、フォロー、メンバー自身による編集、投票、モデレートに対応した[ブログコンポーネント](blog-feature.md)を含むページです。See also [Blog Essentials](blog-developer-basics.md) for developers.

テンプレートに追加すると、次のダイアログが開きます。

![chlimage_1-383](assets/chlimage_1-383.png)

* See [Title and URL Settings](#title-and-url-settings)
* **[!UICONTROL Allow Privileged Members]**：このチェックボックスをオンにすると、特権を持つメンバーグループの選択を許可して、特権を持つメンバーの記事の作成のみがブログで許可され [ます](users.md#privileged-members-group)。 オフにすると、すべてのコミュニティメンバーが記事を作成できます。初期設定はオフです。

* **[!UICONTROL ファイルのアップロードを許可]**：オンにすると、メンバーがファイルをアップロードする機能がブログに含まれます。 初期設定はオンです。

* **[!UICONTROL スレッド化された返信を許可]**&#x200B;このチェックボックスをオンにしない場合、ブログでは記事への返信（コメント）は許可されますが、コメントへの返信は許可されません。 初期設定はオンです。

* **[!UICONTROL 重点コンテンツ]**&#x200B;を許可することを選択すると、そのアイデアは [重点コンテンツとして識別できます](featured.md)。 初期設定はオンです。

### カレンダー機能 {#calendar-function}

カレンダー機能は、タグ付けに対応した[カレンダーコンポーネント](calendar.md)を含むページです。See also [Calendar Essentials](calendar-basics-for-developers.md) for developers.

テンプレートに追加すると、次のダイアログが開きます。

![chlimage_1-384](assets/chlimage_1-384.png)

* See [Title and URL Settings](#title-and-url-settings)
* **[!UICONTROL ピン留めを許可]**&#x200B;するオンにすると、トピックの返信をコメントのリストの先頭にピン留めできます。 初期設定はオンです。

* **[!UICONTROL Allow Privileged Members]**：このチェックボックスをオンにすると、特権を持つメンバーグループの選択を許可して、特権を持つメンバーの記事の作成のみがブログで許可され [ます](users.md#privileged-members-group)。 オフにすると、すべてのコミュニティメンバーが記事を作成できます。初期設定はオフです。

* **[!UICONTROL ファイルのアップロードを許可]**：オンにすると、メンバーがファイルをアップロードする機能がブログに含まれます。 初期設定はオンです。

* **[!UICONTROL スレッド化された返信を許可]**&#x200B;このチェックボックスをオンにしない場合、ブログでは記事への返信（コメント）は許可されますが、コメントへの返信は許可されません。 初期設定はオンです。

* **[!UICONTROL 重点コンテンツ]**&#x200B;を許可することを選択すると、そのアイデアは [重点コンテンツとして識別できます](featured.md)。 初期設定はオンです。

### カタログ機能 {#catalog-function}

The catalog function provides the ability for [enablement community](overview.md#enablement-community) members to browse enablement resources which are not assigned to them. See [Tagging Enablement Resources](tag-resources.md) and [Catalog Essentials](catalog-developer-essentials.md) for developers.

All enablement resources and learning paths for the community site will show in all catalogs if their property, ` [Show in Catalog](resources.md)`, is set to true. To explicitly include resources and learning paths, it is necessary to apply a [pre-filter](catalog-developer-essentials.md#pre-filters) to the catalog.

テンプレートに追加した場合、この設定により、サイト訪問者に表示されるタグフィルターの設定に使用されるタグ名前空間を指定できます。

![catalogfunc](assets/catalogfunc.png)

* See [Title and URL Settings](#title-and-url-settings)
* **[!UICONTROL すべての名前空間を選択]**

   * 選択したタグ名前空間は、カタログにリストされているイネーブルメントリソースのリストをフィルタリングする訪問者が選択できるタグを定義します。
   * オンにすると、コミュニティサイトに対して許可されるタグ名前空間がすべて使用可能になります。
   * オフにすると、コミュニティサイトに許可される名前空間を 1 つ以上選択できます。
   * 初期設定はオンです。

### おすすめコンテンツ機能 {#featured-content-function}

おすすめコンテンツ機能は、コメントの追加と削除に対応した[おすすめコンテンツコンポーネント](featured.md)を含むページです。

おすすめコンテンツの機能は、コンポーネントごとに許可または禁止することができます（[ブログ機能](#blog-function)、[カレンダー機能](#calendar-function)、[フォーラム機能](#forum-function)、[アイディエーション機能](#ideation-function)、[Q&amp;A 機能](#qna-function)を参照してください）。

テンプレートへの追加時には、[タイトルと URL 設定](#title-and-url-settings)のみを設定します。

### ファイルライブラリ機能 {#file-library-function}

ファイルライブラリ機能は、コメントの追加と削除に対応した[ファイルライブラリコンポーネント](file-library.md)を含むページです。

テンプレートへの追加時には、[タイトルと URL 設定](#title-and-url-settings)のみを設定します。

### フォーラム機能 {#forum-function}

フォーラム機能は、タグ付け、ファイルのアップロード、フォロー、メンバー自身による編集、投票、モデレートに対応した[フォーラムコンポーネント](forum.md)を含むページです。

テンプレートに追加すると、次のダイアログが開きます。

#### 設定機能の詳細 {#configuration-function-details-2}

![chlimage_1-385](assets/chlimage_1-385.png)

* See [Title and URL Settings](#title-and-url-settings)
* **[!UICONTROL ピン留めを許可]**&#x200B;するオンにすると、トピックの返信をコメントのリストの先頭にピン留めできます。 初期設定はオンです。

* **[!UICONTROL 「Allow Privileged Members]**」を選択すると、特権を持つメンバーグループの選択を許可して、権限を持つメンバーの投稿のみがフォーラムで許可され [ます](users.md#privileged-members-group)。 オフにすると、すべてのコミュニティメンバーが投稿できるようになります。初期設定はオフです。

* **[!UICONTROL ファイルのアップロードを許可]**：オンにすると、メンバーがファイルをアップロードする機能がフォーラムに含まれます。 初期設定はオンです。

* **[!UICONTROL スレッド化された返信を許可]**&#x200B;するこのチェックボックスをオンにしない場合、トピックに対するコメントは許可されますが、これらのコメントに対する返信は許可されません。 初期設定はオンです。

* **[!UICONTROL 重点コンテンツ]**&#x200B;を許可することを選択すると、そのアイデアは [重点コンテンツとして識別できます](featured.md)。 初期設定はオンです。

### グループ機能 {#groups-function}

>[!CAUTION]
>
>The groups function must *not* be the *first nor the only* function in a site&#39;s structure or in a community site template.
>
>他の機能（[ページ機能](#page-function)など）を含め、その機能を 1 番目にリストする必要があります。

グループ機能を使用すると、パブリッシュ環境でコミュニティメンバーがコミュニティサイト内にサブコミュニティを作成できます。

グループ機能を[コミュニティサイトテンプレート](sites.md)に含めるときの[設定](sites-console.md#groupmanagement)によって、グループを公開または非公開にしたり、1 つ以上のコミュニティグループテンプレートを設定しておいて、コミュニティグループを（パブリッシュ環境から）実際に作成するときにテンプレートを選択できるようにすることも可能です。A [community group template](tools-groups.md) specifies which Communities features are created for the group pages, such as forums and calendars.

コミュニティグループを作成すると、この新しいグループに対してメンバーグループが動的に作成され、メンバーの割り当てや追加ができるようになります。For more information, see [Managing Users and User Groups](users.md).

Communities [機能パック 1](deploy-communities.md#latestfeaturepack) 以降では、コミュニティグループはオーサー環境で[コミュニティサイトのグループコンソール](groups.md)を使用して作成します。また、有効な場合はパブリッシュ環境でも作成できます。

テンプレートに追加すると、次のダイアログが開きます。

![chlimage_1-386](assets/chlimage_1-386.png)

* See [Title and URL Settings](#title-and-url-settings)
* **[!UICONTROL Select Group Templates]**（グループテンプレートの選択）プルダウンメニューでは、(公開環境で)新しいコミュニティグループの将来の作成者が選択できる、1つ以上の有効なグループテンプレートを選択できます。

* **[!UICONTROL Allow Privileged Members]**：このチェックボックスをオンにすると、特権を持つメンバーのセキュリティグループを選択して、特権を持つメンバーの投稿のみがフォーラムで許可され [](users.md#privileged-members-group)ます。 オフにすると、すべてのコミュニティメンバーが投稿できるようになります。初期設定はオフです。

* **[!UICONTROL 公開作成を許可]**&#x200B;オンにすると、権限を持つコミュニティメンバーがパブリッシュ環境でグループを作成できるようになります。オフにすると、新しいグループ（サブコミュニティ）は、オーサー環境のコミュニティサイトのグループコンソールからのみ作成できます。

   デフォルトは `checked` です。

### アイディエーション機能 {#ideation-function}

アイディエーション機能とは、[アイディエーションコンポーネント](ideation-feature.md)を 1 つ含むページです。

テンプレートに追加すると、次のダイアログが開きます。ここで、タイトルおよび URL 名のデフォルトと、テンプレートのデフォルト表示設定を指定します。

![chlimage_1-387](assets/chlimage_1-387.png)

* See [Title and URL Settings](#title-and-url-settings)
* **[!UICONTROL Allow Privileged Members]**：このチェックボックスをオンにすると、特権を持つメンバーのセキュリティグループを選択して、特権を持つメンバーの投稿のみがフォーラムで許可され [](users.md#privileged-members-group)ます。 オフにすると、すべてのコミュニティメンバーが投稿できるようになります。初期設定はオフです。

* **[!UICONTROL ファイルのアップロードを許可]**&#x200B;このチェックボックスをオンにすると、メンバーがファイルをアップロードする機能がアイデアに含まれます。 初期設定はオンです。

* **[!UICONTROL スレッド化された返信を許可]**&#x200B;このチェックボックスをオンにしない場合、アイデアではトピックへの返信（コメント）は許可されますが、コメントへの返信は許可されません。 初期設定はオンです。

* **[!UICONTROL 重点コンテンツ]**&#x200B;を許可することを選択すると、そのアイデアは [重点コンテンツとして識別できます](featured.md)。 初期設定はオンです。

### リーダーボード機能 {#leaderboard-function}

リーダーボード機能とは、[リーダーボーコンポーネント](enabling-leaderboard.md)を 1 つ含むページです。

**注意**：リーダーボード機能を含むコミュニティテンプレートからコミュニティサイトを作成した後に、リーダーボードコンポーネントで追加の設定が必要となります。** The Leaderboard component&#39;s [rules](enabling-leaderboard.md#rules-tab) will need to be specified, which depend on configuration of [scoring and badges](implementing-scoring.md) for the community site.

テンプレートに追加すると、次のダイアログが開きます。ここで、タイトルおよび URL 名のデフォルトと、テンプレートのデフォルト表示設定を指定します。

![chlimage_1-388](assets/chlimage_1-388.png)

* See [Title and URL Settings](#title-and-url-settings)
* **[!UICONTROL バッジを表示]**&#x200B;オンにすると、リーダーボードにバッジアイコンの列が表示されるようになります。

   初期設定はオフです。

* **[!UICONTROL バッジ名を表示]**&#x200B;オンにすると、リーダーボードにバッジ名の列が表示されるようになります。

   初期設定はオフです。

* **[!UICONTROL アバターを表示]**&#x200B;オンにすると、リーダーボードでメンバープロフィールの名前リンクの横にメンバーのアバター画像が表示されるようになります。

   初期設定はオフです。

### ページ機能 {#page-function}

ページ機能を使用すると、ログイン、メニュー、通知、メッセージング、テーマ、ブランディングといったコミュニティサイトの機能が組み込まれた空白のページがコミュニティサイトに追加されます。Content may be added to the page using the [standard AEM authoring mode](../../help/sites-authoring/editing-content.md).

テンプレートへの追加時には、[タイトルと URL 設定](#title-and-url-settings)のみを設定します。

### Q&amp;A 機能 {#qna-function}

Q&amp;A 機能は、タグ付け、ファイルのアップロード、フォロー、メンバー自身による編集、投票、モデレートに対応した [Q&amp;A コンポーネント](working-with-qna.md)を含むページです。

テンプレートへの追加時に、権限を持つメンバーだけが投稿できるような設定をすることができます。

![chlimage_1-389](assets/chlimage_1-389.png)

* See [Title and URL Settings](#title-and-url-settings)
* **[!UICONTROL ピン留めを許可]**&#x200B;するオンにすると、トピックの返信をコメントのリストの先頭にピン留めできます。 初期設定はオンです。

* **[!UICONTROL Allow Privileged Members]**：このチェックボックスをオンにすると、QnAフォーラムは、 [特権メンバーグループの選択を許可して、特権メンバーが質問を投稿することを許可します](users.md#privileged-members-group)。 オフにすると、すべてのコミュニティメンバーが投稿できるようになります。初期設定はオフです。

* **[!UICONTROL ファイルのアップロードを許可]**：オンにすると、QnAフォーラムにメンバーがファイルをアップロードする機能が含まれます。 初期設定はオンです。

* **[!UICONTROL スレッド化された返信を許可]**&#x200B;することを選択しない場合、QnAフォーラムでは投稿された質問に対するコメント（回答）は許可されますが、回答に対する返信は許可されません。 初期設定はオンです。

* **[!UICONTROL 重点コンテンツ]**&#x200B;を許可することを選択すると、そのアイデアは [重点コンテンツとして識別できます](featured.md)。 初期設定はオンです。

## コミュニティ機能を作成 {#create-community-function}

The ability to create a community function is reached by selecting the `Create Community Function` icon located at the top of the Community Functions console. 同じAEM Blueprintに基づく複数の機能を作成し、作成者編集モードで開いて独自にカスタマイズできます。

![chlimage_1-390](assets/chlimage_1-390.png)

### コミュニティ機能名 {#community-function-name}

![chlimage_1-391](assets/chlimage_1-391.png)

コミュニティ機能名パネルでは、機能の名前および説明と、機能を有効にするか無効にするかを設定します。

* **[!UICONTROL コミュニティ関数名]**&#x200B;表示とストレージに使用する関数名

* **[!UICONTROL コミュニティ関数の説明]**&#x200B;表示する関数の説明

* **[!UICONTROL 無効/有効]**&#x200B;関数が参照可能かを制御するトグルスイッチ

### AEM ブループリント {#aem-blueprint}

![chlimage_1-392](assets/chlimage_1-392.png)

On the `AEM Blueprint` panel, it is possible to select the blueprint which is the underlying implementation of the community function.

コミュニティ機能は、1 つまたは複数のページで構成されるミニサイトです。ログイン、ユーザープロファイル、通知、メッセージング、サイトメニュー、検索、テーマ、ブランディングなどの機能が、コミュニティサイトに組み込める形であらかじめ構築されています。Once the function is created, it is possible to [open the function](#open-community-function) in author edit mode and customize the page and/or component settings.

Since the community function is implemented as a [live copy](../../help/sites-administering/msm.md#live-copies) of a [blueprint](../../help/sites-administering/msm-livecopy.md#creatingablueprint), it is possible to rollout changes made to a function which affects all community site pages created from the [community site template](sites.md) or [community group template](tools-groups.md) that included the function. また、ページレベルの変更を行うために、親の青写真からページの関連付けを解除することもできます。

[マルチサイトマネージャー](../../help/sites-administering/msm.md)も参照してください。

### サムネール {#thumbnail}

![chlimage_1-393](assets/chlimage_1-393.png)

サムネールパネルでは、[コミュニティ機能コンソール](#community-functions-console)に表示する画像をアップロードできます。

## コミュニティ機能を開く {#open-community-function}

![chlimage_1-394](assets/chlimage_1-394.png)

Select the `Open Community Function` icon to enter author edit mode for authoring the page content and modifying the configuration of the feature component(s).

### コンポーネントの設定 {#configuring-components}

コミュニティ機能は、AEM ブループリントのライブコピーとして実装されます（ライブコピーについては[マルチサイトマネージャー](../../help/sites-administering/msm.md)を参照）。

ページコンテンツのオーサリングだけでなく、コンポーネントの設定をすることもできます。

作成したコミュニティサイトのページ上にあるコンポーネントを設定する場合、コンポーネントを設定するために、[継承](../../help/sites-administering/msm-livecopy.md#changing-live-copy-content)の解除が必要になることがあります。構成が完了したら、継承を再確立する必要があります。

設定について詳しくは、作成者向けの[コミュニティコンポーネント](author-communities.md)を参照してください。

## コミュニティ機能を編集 {#edit-community-function}

![chlimage_1-395](assets/chlimage_1-395.png)

Select the `Edit Community Function` icon to edit the function&#39;s properties using the same panels as [creating a community function](#create-community-function), including enabling or disabling the function.
