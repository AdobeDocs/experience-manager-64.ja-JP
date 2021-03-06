---
title: コミュニティ機能
seo-title: Community Functions
description: コミュニティ機能コンソールにアクセスする方法を説明します
seo-description: Learn how to access the Community Functions console
uuid: 5cce05f5-1dd7-496d-94c2-8fccc0177d13
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.4/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: cc993b71-e2f2-48e7-ad4e-469cb5ce2dc1
role: Admin
exl-id: 2007336d-d75c-4e01-af81-181751c04cfe
source-git-commit: 3c050c33a384d586d74bd641f7622989dc1d6b22
workflow-type: tm+mt
source-wordcount: '2532'
ht-degree: 47%

---

# コミュニティ機能 {#community-functions}

コミュニティに必要とされる機能の種類はだいたい決まっています。コミュニティ機能は、コミュニティ機能として使用できます。 基本的に、コミュニティ機能を実装するために事前に配線された 1 つ以上のページです。この場合、オーサリングモードでページにコンポーネントを追加するだけでは済みません。 これらは、 [コミュニティサイトテンプレート](sites.md) どのコミュニティサイトから [作成済み](sites-console.md).

コミュニティサイトを作成した後、標準の [AEMオーサリングモード](../../help/sites-authoring/editing-content.md).

コミュニティ機能コンソールには数多くのコミュニティ機能が用意されており、すぐに使用できます。今後のリリースでは、コミュニティ機能がさらに提供される予定です。カスタム機能も作成される可能性があります。

>[!NOTE]
>
>作成用のコンソール [コミュニティサイト](sites-console.md), [コミュニティサイトテンプレート](sites.md), [コミュニティグループテンプレート](tools-groups.md) および [コミュニティ機能](functions.md) は、オーサー環境でのみ使用されます。

## コミュニティ機能コンソール {#community-functions-console}

オーサー環境でコミュニティ機能コンソールに移動するには、

* グローバルナビゲーションから： **[!UICONTROL ツール/コミュニティ/コミュニティ機能]**

![chlimage_1-379](assets/chlimage_1-379.png)

## 標準で提供される機能 {#pre-built-functions}

AEM Communities で提供される機能を以下で簡単に説明します。各機能は、コミュニティコンポーネントを含む 1 つ以上のAEMページで構成され、1 つの機能に簡単に組み込めるように、1 つの機能に結び付けられます。 [コミュニティサイトテンプレート](sites.md).

コミュニティサイトテンプレートは、ログイン、ユーザープロファイル、通知、メッセージング、サイトメニュー、検索、テーマ、ブランディング機能など、コミュニティサイトの構造を定義します。

### タイトルと URL の設定 {#title-and-url-settings}

**タイトル**&#x200B;と **URL** は、すべてのコミュニティ機能に共通するプロパティです。

コミュニティ機能をコミュニティサイトテンプレートに追加するか、コミュニティサイトの構造を[変更](sites-console.md#modifying-site-properties)すると、その機能のダイアログが開き、タイトルと URL を設定できます。

#### 設定機能の詳細 {#configuration-function-details}

![chlimage_1-380](assets/chlimage_1-380.png)

* **[!UICONTROL タイトル]**
(
*必須*) サイトの機能のメニューに表示されるテキスト

* **[!UICONTROL URL]**
(*必須*) URI の生成に使用される名前。 名前は [命名規則](../../help/sites-developing/naming-conventions.md) AEMと JCR によって課せられます。

例えば、[使用の手引き](getting-started.md)のチュートリアルに従って作成したサイトを使用し、

* タイトル = Web ページ
* URL = page

次に、ページの URL がhttp://local_host:4503/content/sites/engage/en/page.htmlになり、そのページのメニューリンクが次のように表示されます。

![chlimage_1-381](assets/chlimage_1-381.png)

### アクティビティストリーム機能 {#activity-stream-function}

アクティビティストリーム機能は、選択されたすべてのビュー（すべてのアクティビティ、ユーザーアクティビティおよびフォロー）を備えた[アクティビティストリームコンポーネント](activities.md)を含むページです。関連トピック [Activity Stream Essentials](essentials-activities.md) 開発者向け

テンプレートに追加すると、次のダイアログが開きます。

#### 設定機能の詳細 {#configuration-function-details-1}

![chlimage_1-382](assets/chlimage_1-382.png)

* 詳しくは、 [タイトルと URL の設定](#title-and-url-settings)
* **[!UICONTROL 「マイアクティビティ」ビューを表示]**
オンにすると、アクティビティページに、現在のメンバーがコミュニティ内で生成したアクティビティに基づいてアクティビティをフィルタリングするタブが表示されます。 初期設定はオンです。

* **[!UICONTROL 「すべてのアクティビティ」ビューを表示]**
オンにすると、アクティビティページにタブが表示され、現在のメンバーがアクセスできるコミュニティ内で生成されたすべてのアクティビティが含まれます。 初期設定はオンです。

* **[!UICONTROL 「ニュースフィード」ビューを表示]**
オンにすると、アクティビティページに、現在のメンバーがフォローしているアクティビティに基づいてアクティビティをフィルタリングするタブが含まれます。 初期設定はオンです。

### 割り当て機能 {#assignments-function}

割り当て機能は、 [イネーブルメントのためのコミュニティサイト](overview.md#enablement-community). コミュニティメンバーにイネーブルメントリソースを割り当てることができます。 関連トピック [割り当ての基本事項](essentials-assignments.md) 開発者向け

この関数は、 [イネーブルメントアドオン](enablement.md). イネーブルメントアドオンを実稼動環境で使用するには、追加のライセンスが必要です。

テンプレートへの追加時には、[タイトルと URL 設定](#title-and-url-settings)のみを設定します。

### ブログ機能 {#blog-function}

ブログ機能は、タグ付け、ファイルのアップロード、フォロー、メンバー自身による編集、投票、モデレートに対応した[ブログコンポーネント](blog-feature.md)を含むページです。関連トピック [ブログの基本事項](blog-developer-basics.md) 開発者向け

テンプレートに追加すると、次のダイアログが開きます。

![chlimage_1-383](assets/chlimage_1-383.png)

* 詳しくは、 [タイトルと URL の設定](#title-and-url-settings)
* **[!UICONTROL 権限を持つメンバーを許可]**
オンにすると、ブログでは権限を持つメンバーだけが記事を作成できるようになります。 [権限を持つメンバーグループ](users.md#privileged-members-group). オフにすると、すべてのコミュニティメンバーが記事を作成できます。初期設定はオフです。

* **[!UICONTROL ファイルのアップロードを許可]**
オンにすると、メンバーがファイルをアップロードする機能がブログに含まれます。 初期設定はオンです。

* **[!UICONTROL スレッド化された返信を許可]**
オンにしないと、ブログは記事への返信（コメント）を許可しますが、コメントへの返信は許可されません。 初期設定はオンです。

* **[!UICONTROL おすすめコンテンツを許可]**
オンにすると、アイデアは次のように識別されます。 [おすすめコンテンツ](featured.md). 初期設定はオンです。

### カレンダー機能 {#calendar-function}

カレンダー機能は、タグ付けに対応した[カレンダーコンポーネント](calendar.md)を含むページです。関連トピック [カレンダーの基本事項](calendar-basics-for-developers.md) 開発者向け

テンプレートに追加すると、次のダイアログが開きます。

![chlimage_1-384](assets/chlimage_1-384.png)

* 詳しくは、 [タイトルと URL の設定](#title-and-url-settings)
* **[!UICONTROL ピン留めを許可]**
オンにすると、フォーラムでトピックの返信をコメントのリストの先頭にピン留めできます。 初期設定はオンです。

* **[!UICONTROL 権限を持つメンバーを許可]**
オンにすると、ブログでは権限を持つメンバーだけが記事を作成できるようになります。 [権限を持つメンバーグループ](users.md#privileged-members-group). オフにすると、すべてのコミュニティメンバーが記事を作成できます。初期設定はオフです。

* **[!UICONTROL ファイルのアップロードを許可]**
オンにすると、メンバーがファイルをアップロードする機能がブログに含まれます。 初期設定はオンです。

* **[!UICONTROL スレッド化された返信を許可]**
オンにしないと、ブログは記事への返信（コメント）を許可しますが、コメントへの返信は許可されません。 初期設定はオンです。

* **[!UICONTROL おすすめコンテンツを許可]**
オンにすると、アイデアは次のように識別されます。 [おすすめコンテンツ](featured.md). 初期設定はオンです。

### カタログ機能 {#catalog-function}

カタログ機能を使用すると、 [実施可能コミュニティ](overview.md#enablement-community) メンバー：割り当てられていないイネーブルメントリソースを参照します。 詳しくは、 [イネーブルメントリソースのタグ付け](tag-resources.md) および [カタログの基本事項](catalog-developer-essentials.md) 開発者向け

コミュニティサイトのすべてのイネーブルメントリソースと学習パスは、プロパティの場合はすべてのカタログに表示されます。 ` [Show in Catalog](resources.md)`が true に設定されている場合、エラーは発生しません。 リソースと学習パスを明示的に含めるには、 [プリフィルター](catalog-developer-essentials.md#pre-filters) をカタログに追加します。

テンプレートに追加した場合、この設定により、サイト訪問者に表示されるタグフィルターの設定に使用されるタグ名前空間を指定できます。

![catalogfunc](assets/catalogfunc.png)

* 詳しくは、 [タイトルと URL の設定](#title-and-url-settings)
* **[!UICONTROL すべての名前空間を選択]**

   * 選択したタグ名前空間は、カタログに一覧表示されているイネーブルメントリソースのリストをフィルタリングするために、訪問者が選択できるタグを定義します。
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

* 詳しくは、 [タイトルと URL の設定](#title-and-url-settings)
* **[!UICONTROL ピン留めを許可]**
オンにすると、フォーラムでトピックの返信をコメントのリストの先頭にピン留めできます。 初期設定はオンです。

* **[!UICONTROL 権限を持つメンバーを許可]**
オンにすると、フォーラムでは権限を持つメンバーのみがトピックを投稿できるようになり、 [権限を持つメンバーグループ](users.md#privileged-members-group). オフにすると、すべてのコミュニティメンバーが投稿できるようになります。初期設定はオフです。

* **[!UICONTROL ファイルのアップロードを許可]**
オンにすると、メンバーがファイルをアップロードする機能がフォーラムに含まれます。 初期設定はオンです。

* **[!UICONTROL スレッド化された返信を許可]**
オンにしないと、フォーラムはトピックに対するコメントを許可しますが、それらのコメントに対する返信は許可されません。 初期設定はオンです。

* **[!UICONTROL おすすめコンテンツを許可]**
オンにすると、アイデアは次のように識別されます。 [おすすめコンテンツ](featured.md). 初期設定はオンです。

### グループ機能 {#groups-function}

>[!CAUTION]
>
>グループ機能は、 *not* は *最初でも唯一でも* 機能をサイトの構造内、またはコミュニティサイトテンプレート内に組み込むことができます。
>
>他の機能（[ページ機能](#page-function)など）を含め、その機能を 1 番目にリストする必要があります。

グループ機能を使用すると、パブリッシュ環境でコミュニティメンバーがコミュニティサイト内にサブコミュニティを作成できます。

グループ機能を[コミュニティサイトテンプレート](sites.md)に含めるときの[設定](sites-console.md#groupmanagement)によって、グループを公開または非公開にしたり、1 つ以上のコミュニティグループテンプレートを設定しておいて、コミュニティグループを（パブリッシュ環境から）実際に作成するときにテンプレートを選択できるようにすることも可能です。A [コミュニティグループテンプレート](tools-groups.md) フォーラムやカレンダーなど、グループページ用に作成するコミュニティ機能を指定します。

コミュニティグループを作成すると、この新しいグループに対してメンバーグループが動的に作成され、メンバーの割り当てや追加ができるようになります。詳しくは、 [ユーザーとユーザーグループの管理](users.md).

Communities [機能パック 1](deploy-communities.md#latestfeaturepack) 以降では、コミュニティグループはオーサー環境で[コミュニティサイトのグループコンソール](groups.md)を使用して作成します。また、有効な場合はパブリッシュ環境でも作成できます。

テンプレートに追加すると、次のダイアログが開きます。

![chlimage_1-386](assets/chlimage_1-386.png)

* 詳しくは、 [タイトルと URL の設定](#title-and-url-settings)
* **[!UICONTROL グループテンプレートを選択]**
（パブリッシュ環境で）新しいコミュニティグループの作成者が選択できる、1 つ以上の有効なグループテンプレートを選択できるプルダウンメニュー。

* **[!UICONTROL 権限を持つメンバーを許可]**
オンにすると、フォーラムでは権限を持つメンバーのみがトピックを投稿できるようになり、 [権限を持つメンバーのセキュリティグループ](users.md#privileged-members-group). オフにすると、すべてのコミュニティメンバーが投稿できるようになります。初期設定はオフです。

* **[!UICONTROL 公開作成を許可]**&#x200B;オンにすると、権限を持つコミュニティメンバーがパブリッシュ環境でグループを作成できるようになります。オフにすると、新しいグループ（サブコミュニティ）は、オーサー環境のコミュニティサイトのグループコンソールからのみ作成できます。

   デフォルトは `checked` です。

### アイディエーション機能 {#ideation-function}

アイディエーション機能とは、[アイディエーションコンポーネント](ideation-feature.md)を 1 つ含むページです。

テンプレートに追加すると、次のダイアログが開きます。ここで、タイトルおよび URL 名のデフォルトと、テンプレートのデフォルト表示設定を指定します。

![chlimage_1-387](assets/chlimage_1-387.png)

* 詳しくは、 [タイトルと URL の設定](#title-and-url-settings)
* **[!UICONTROL 権限を持つメンバーを許可]**
オンにすると、フォーラムでは権限を持つメンバーのみがトピックを投稿できるようになり、 [権限を持つメンバーのセキュリティグループ](users.md#privileged-members-group). オフにすると、すべてのコミュニティメンバーが投稿できるようになります。初期設定はオフです。

* **[!UICONTROL ファイルのアップロードを許可]**
オンにすると、メンバーがファイルをアップロードする機能がアイデアに含まれます。 初期設定はオンです。

* **[!UICONTROL スレッド化された返信を許可]**
オンにしない場合、アイデアはトピックへの返信（コメント）を許可しますが、コメントへの返信は許可されません。 初期設定はオンです。

* **[!UICONTROL おすすめコンテンツを許可]**
オンにすると、アイデアは次のように識別されます。 [おすすめコンテンツ](featured.md). 初期設定はオンです。

### リーダーボード機能 {#leaderboard-function}

リーダーボード機能とは、[リーダーボーコンポーネント](enabling-leaderboard.md)を 1 つ含むページです。

**注意**：リーダーボード機能を含むコミュニティテンプレートからコミュニティサイトを作成した後に、リーダーボードコンポーネントで追加の設定が必要となります。**&#x200B;リーダーボードコンポーネントの [ルール](enabling-leaderboard.md#rules-tab) を指定する必要があります。これは、 [スコアとバッジ](implementing-scoring.md) コミュニティサイト用。

テンプレートに追加すると、次のダイアログが開きます。ここで、タイトルおよび URL 名のデフォルトと、テンプレートのデフォルト表示設定を指定します。

![chlimage_1-388](assets/chlimage_1-388.png)

* 詳しくは、 [タイトルと URL の設定](#title-and-url-settings)
* **[!UICONTROL バッジを表示]**&#x200B;オンにすると、リーダーボードにバッジアイコンの列が表示されるようになります。

   初期設定はオフです。

* **[!UICONTROL バッジ名を表示]**&#x200B;オンにすると、リーダーボードにバッジ名の列が表示されるようになります。

   初期設定はオフです。

* **[!UICONTROL アバターを表示]**&#x200B;オンにすると、リーダーボードでメンバープロフィールの名前リンクの横にメンバーのアバター画像が表示されるようになります。

   初期設定はオフです。

### ページ機能 {#page-function}

ページ機能を使用すると、ログイン、メニュー、通知、メッセージング、テーマ、ブランディングといったコミュニティサイトの機能が組み込まれた空白のページがコミュニティサイトに追加されます。コンテンツは、 [標準AEMオーサリングモード](../../help/sites-authoring/editing-content.md).

テンプレートへの追加時には、[タイトルと URL 設定](#title-and-url-settings)のみを設定します。

### Q&amp;A 機能 {#qna-function}

Q&amp;A 機能は、タグ付け、ファイルのアップロード、フォロー、メンバー自身による編集、投票、モデレートに対応した [Q&amp;A コンポーネント](working-with-qna.md)を含むページです。

テンプレートへの追加時に、権限を持つメンバーだけが投稿できるような設定をすることができます。

![chlimage_1-389](assets/chlimage_1-389.png)

* 詳しくは、 [タイトルと URL の設定](#title-and-url-settings)
* **[!UICONTROL ピン留めを許可]**
オンにすると、フォーラムでトピックの返信をコメントのリストの先頭にピン留めできます。 初期設定はオンです。

* **[!UICONTROL 権限を持つメンバーを許可]**
オンにすると、Q&amp;A フォーラムでは、権限を持つメンバーに対してのみ、 [権限を持つメンバーグループ](users.md#privileged-members-group). オフにすると、すべてのコミュニティメンバーが投稿できるようになります。初期設定はオフです。

* **[!UICONTROL ファイルのアップロードを許可]**
オンにすると、Q&amp;A フォーラムにメンバーがファイルをアップロードする機能が含まれます。 初期設定はオンです。

* **[!UICONTROL スレッド化された返信を許可]**
オンにしないと、Q&amp;A フォーラムでは投稿された質問に対するコメント（回答）が許可されますが、回答に対する返信は許可されません。 初期設定はオンです。

* **[!UICONTROL おすすめコンテンツを許可]**
オンにすると、アイデアは次のように識別されます。 [おすすめコンテンツ](featured.md). 初期設定はオンです。

## コミュニティ機能を作成 {#create-community-function}

コミュニティ機能を作成する機能には、 `Create Community Function` コミュニティ機能コンソールの上部にあるアイコン 同じAEMブループリントに基づく複数の関数を作成し、オーサー編集モードで開いて一意にカスタマイズできます。

![chlimage_1-390](assets/chlimage_1-390.png)

### コミュニティ機能名 {#community-function-name}

![chlimage_1-391](assets/chlimage_1-391.png)

コミュニティ機能名パネルでは、機能の名前および説明と、機能を有効にするか無効にするかを設定します。

* **[!UICONTROL コミュニティ機能名]**
表示と保存に使用する関数名

* **[!UICONTROL コミュニティ機能の説明]**
表示する関数の説明

* **[!UICONTROL 無効/有効]**
関数が参照可能かどうかを制御する切り替えスイッチ

### AEM ブループリント {#aem-blueprint}

![chlimage_1-392](assets/chlimage_1-392.png)

の `AEM Blueprint` パネルの場合は、コミュニティ機能の基盤となるブループリントを選択できます。

コミュニティ機能は、1 つまたは複数のページで構成されるミニサイトです。ログイン、ユーザープロファイル、通知、メッセージング、サイトメニュー、検索、テーマ、ブランディングなどの機能が、コミュニティサイトに組み込める形であらかじめ構築されています。関数を作成した後は、次の操作を実行できます。 [関数を開く](#open-community-function) オーサー編集モードで、ページやコンポーネントの設定をカスタマイズします。

コミュニティ機能は [ライブコピー](../../help/sites-administering/msm.md#live-copies) の [ブループリント](../../help/sites-administering/msm-livecopy.md#creatingablueprint)を使用すると、関数に対して行われた変更をロールアウトできます。この変更は、 [コミュニティサイトテンプレート](sites.md) または [コミュニティグループテンプレート](tools-groups.md) 関数を含む ページレベルで変更を加えるために、ページを親ブループリントから関連付け解除することもできます。

[マルチサイトマネージャー](../../help/sites-administering/msm.md)も参照してください。

### サムネール {#thumbnail}

![chlimage_1-393](assets/chlimage_1-393.png)

サムネールパネルでは、[コミュニティ機能コンソール](#community-functions-console)に表示する画像をアップロードできます。

## コミュニティ機能を開く {#open-community-function}

![chlimage_1-394](assets/chlimage_1-394.png)

を選択します。 `Open Community Function` ページコンテンツをオーサリングし、機能コンポーネントの設定を変更するためのオーサー編集モードに入るアイコン。

### コンポーネントの設定 {#configuring-components}

コミュニティ機能は、AEM ブループリントのライブコピーとして実装されます（ライブコピーについては[マルチサイトマネージャー](../../help/sites-administering/msm.md)を参照）。

ページコンテンツのオーサリングだけでなく、コンポーネントの設定をすることもできます。

作成したコミュニティサイトのページ上にあるコンポーネントを設定する場合、コンポーネントを設定するために、[継承](../../help/sites-administering/msm-livecopy.md#changing-live-copy-content)の解除が必要になることがあります。設定が完了したら、継承を再確立する必要があります。

設定について詳しくは、作成者向けの[コミュニティコンポーネント](author-communities.md)を参照してください。

## コミュニティ機能を編集 {#edit-community-function}

![chlimage_1-395](assets/chlimage_1-395.png)

を選択します。 `Edit Community Function` アイコンをクリックし、 [コミュニティ機能の作成](#create-community-function)（関数の有効化または無効化を含む）
