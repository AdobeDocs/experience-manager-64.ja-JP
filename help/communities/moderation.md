---
title: モデレートコンソール
seo-title: モデレートコンソール
description: モデレートコンソールへのアクセス方法
seo-description: モデレートコンソールへのアクセス方法
uuid: 920124b9-af6f-4622-adb6-b8e294c5607d
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.4/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 6c405543-e339-4916-aa0f-b61d0b798cf3
translation-type: tm+mt
source-git-commit: f78f83ef3b9373bcbee3e5179a9bbec4d9462255
workflow-type: tm+mt
source-wordcount: '1855'
ht-degree: 57%

---


# モデレートコンソール {#moderation-console}

In AEM Communities, bulk [moderation of community content](moderate-ugc.md) is possible from both the author and publish environments by administrators and community moderators (trusted community members assigned as moderators).

Administrators and community moderators may also perform [in-context moderation](in-context.md) in the publish environment.

A feature of all [community sites](sites-console.md) is an `Administration`menu item available to users who sign in with administrative privileges. The `Administration`link provides access to the Moderation console.

モデレートコンソールでは、管理者とコミュニティモデレーターが、モデレート権限を持っているすべてのユーザー生成コンテンツ（UGC）にアクセスできます。複数のサイトのモデレートを許可すると、すべてのサイトにわたる投稿の表示や、選択したコミュニティのサイトによるフィルターが可能です。

For more detailed information visit [Managing Users and User Groups](users.md).

モデレートコンソールでは以下の操作を実行できます。
* モデレートタスクの一括実行
* UGCの検索
* UGC詳細の表示
* UGC作成者の詳細の表示

Only when signed in as an administrator, or a member with ` [moderator permissions](in-context.md#identifyingtrustedmembers)`, may moderation tasks be performed.

## パブリッシュ環境からのアクセス {#publish-environment-access}

公開済みのコミュニティサイトからモデレートコンソールにアクセスするには、コミュニティモデレーターがサインインしたときに表示される管理リンクからアクセスします。

![publishewertel](assets/publishweretail.png)

管理リンクを選択すると、以下のモデレートコンソールが表示されます。

![moderationconsole-publish](assets/moderationconsole-publish.png)

## オーサー環境からのアクセス {#author-environment-access}

オーサー環境でモデレートコンソールに移動するには、

* From global navigation: **[!UICONTROL Navigation > Communities > Moderation]**

Only when signed in as an administrator, or as a member with ` [moderator permissions](in-context.md#identifyingtrustedmembers)`, may moderation tasks be performed. 表示されるコミュニティコンテンツは、サインインしたメンバーがモデレートを許可されるものだけです。

>[!NOTE]
>
>パブリッシュ環境の UGC をオーサー環境で表示できるのは、選択した SRP で共通ストアが実装されている場合のみです。例えば、デフォルトでは、ストレージはJSRPです。JSRPは、作成者および発行用の一般的なストアではありません。 See [Community Content Storage](working-with-srp.md).

![moderationconsoleauthor](assets/moderationconsoleauthor.png)

## モデレートコンソールの UI {#moderation-console-ui}

左側のナビゲーションレール（オーサー環境では表示されますが、パブリッシュ環境では表示されません）の他に、モデレートコンソールの UI には次の主な領域があります。

* **[トップナビゲーションバー](#top-navigation-bar)**
* **[ツールバー](#toolbar)**
* **[コンテンツ領域](#content-area)**

### 上部ナビゲーションバー {#top-navigation-bar}

上部ナビゲーションバーはすべてのコンソールで共通です。For more information, see [Basic Handling](../../help/sites-authoring/basic-handling.md).

### ツールバー {#toolbar}

上部ナビゲーションバーの下にツールバーがあり、その左側に次の切り替えスイッチがあります。

* [フィルターレール](moderation.md#filter-rail)コンテンツのフィルター条件のプロパティを選択できるレールが開きます。

上部ナビゲーションバーの下にツールバーがあり、その左側に次の切り替えスイッチがあります。

![toggleswitch](assets/toggleswitch.png)

[フィルターレール](moderation.md#filter-rail)\
「検索」を選択するとパネルが開き、コンテンツをフィルターするプロパティを選択できます。

![filterrail](assets/filterrail.png)

### コンテンツ領域 {#content-area}

コンテンツ領域には、投稿された UGC に関する以下の情報が表示されます。

* UGCは投稿した
* メンバー名
* 会員アバター
* 投稿の場所
* 投稿日
* 投稿への返信数
* [投稿に関連付けられたセンチメント](moderate-ugc.md#sentiment)
* 承認済みの場合は、チェックマークが表示されます
* 添付ファイルがある場合は、クリップが表示されます

>[!NOTE]
>
>The content area features an *infinite scroll*, which means that it will allow you to continue scrolling until you have reached the end of the content. ツールバーは、スクロール時もコンテンツ領域の上の位置に固定されて表示されます。

### フィルターレール {#filter-rail}

![chlimage_1-472](assets/chlimage_1-472.png)

サイドパネルアイコンにより、フィルターレールが開きます。 コンテンツ領域の左側に表示されるフィルターレールは、様々なフィルターを提供し、それぞれがコンテンツ領域に表示される参照先のUGCに直接影響します。

The filters within each category are **OR** ed together, and the filters in different categories are **AND** ed together.

For example, if you check both **Question** and **Answer**, you will see content that is either a **Question** *or* an **Answer**.

However if you check **Question** and **Pending**, you will only see content that is a **Question** and is **Pending**.

>[!NOTE]
>
>コミュニティモデレーターは、モデレートコンソール UI で事前定義されたフィルターをブックマークできます。これらのフィルターは、URL の末尾に（クエリ文字列パラメーターとして）追加されるので、モデレーターはブックマークしたフィルターに戻ったり、これらのリンクを共有することもできます。

![searchicon](assets/searchicon.png)

フィルターレールが開いているときに「検索」アイコンを選択すると、サイドパネルが閉じます。ただし、フィルターレールを閉じて、ユーザー生成コンテンツのみを表示するには、「検索」アイコンをクリックし、「コンテンツのみ」オプションを選択します。

#### コンテンツのパス {#content-path}

コンテンツのパスは、表示される UGC 参照を、指定したコンテンツリポジトリに配置されている投稿のみに限定します。

![content-path](assets/content-path.png)

#### テキスト検索 {#text-search}

テキスト検索は、表示される UGC 参照を、入力したテキストを含む投稿のみに限定します。

![chlimage_1-473](assets/chlimage_1-473.png)

#### サイト {#site}

サイトは、表示される UGC 参照を、選択したコミュニティサイトへの投稿のみに限定します。サイトがチェックされていない場合は、UGCへのすべての参照が表示されます。

![chlimage_1-474](assets/chlimage_1-474.png)

>[!NOTE]
>
>管理者が一括モデレートコンソールにアクセスしたときは、[サイト作成ウィザード](sites-console.md)を使わずに作成したサイト（Geometrixx サンプルサイトなど）も含め、すべての UGC 参照が表示されます。
>
>信頼されているコミュニティメンバーが一括モデレートコンソールにアクセスしたときは、そのメンバーがモデレート権限を持つコミュニティサイト用に作成された UGC 参照のみが表示されます。これらの UGC 参照はサイトフィルターでフィルタリングできます。

#### コンテンツタイプ {#content-type}

コンテンツタイプは、表示される UGC 参照を、選択したリソースタイプの投稿のみに限定します。次に示すタイプの中から 1 つ以上選択できます。何も選択しない場合は、すべてのタイプが表示されます。

* **コメント**
* **フォーラムトピック**
* **フォーラム返信**
* **Q&amp;A 質問**
* **Q&amp;A 回答**
* **ブログ記事**
* **ブログコメント**
* **カレンダーイベント**
* **カレンダーコメント**
* **ファイルライブラリフォルダー**
* **ファイルライブラリ文書**
* **アイデア**
* **アイディエーションのコメント**

![content-types](assets/content-types.png)

#### 追加のコンテンツタイプ {#additional-content-types}

フィルター条件のリソースをさらに追加するには：

* 作成者インスタンス
* 管理者としてサインイン
* Open [Web Console](http://localhost:4502/system/console/configMgr)
* Locate `AEM Communities Moderation Dashboard Filters`
* 編集モードで開く設定を選択します
* フィルタするコンポーネントのResourceTypeを入力します
   * 例えば、含まれる投票コンポーネントをフィルタするには、次のように入力します。\
      `Voting=social/tally/components/hbs/voting`

![chlimage_1-475](assets/chlimage_1-475.png)

* 「保存」を選択します
* コミュニティの更新 — モデレートコンソール

The result is a new selectable filter for `Voting`under the `Content Type` filter group.

このフィルターを選択すると、ダッシュボードのコンテンツに、入力した ResourceType に一致する UGC が表示されます。

#### ステータス {#status}

ステータスは、表示される UGC 参照を、選択したステータスの投稿のみに限定します。「保留中」、「承認」、「拒否」、「終了」のステータス（ブログ記事の場合は「ドラフト」と「スケジュール済み」、Q&amp;A 質問の場合は「回答済み」と「未回答」もあります）のうち、1 つ以上を選択できます。何も選択しなかった場合は、すべてのものが表示されます。

>[!NOTE]
>
>「未回答」ステータスのみを選択すると、回答済みの質問を除く（すべてのコンテンツタイプの）すべてのコンテンツが表示されます。これは、未回答の質問とフォーラムトピックやブログ記事、コメントなどのコンテンツには、回答済みの質問に関係するプロパティが存在しないからです。

![ステータス](assets/statuses.png)

#### フラグ設定 {#flagging}

フラグ設定は、表示される UGC 参照を、フラグが付いている投稿または非表示の投稿のみに限定します。

Once a piece of content is flagged, it remains flagged until you unflag that single piece of content by selecting the **[!UICONTROL Flag]** button once again. フラグには重要やフォローアップなどのレベルがないことに注意してください。

![chlimage_1-476](assets/chlimage_1-476.png)

#### メンバー {#members}

メンバーは、表示される UGC 参照を、特定のメンバー（メンバー名を入力して指定）が投稿した UGC のみに限定します。

![chlimage_1-477](assets/chlimage_1-477.png)

#### 過去に投稿済み {#posted-in-the-last}

過去に投稿済みは、表示される UGC 参照を、1 時間、1 日以内、1 週間、1 ヶ月または 1 年以内に投稿されたものに限定します。

![chlimage_1-478](assets/chlimage_1-478.png)

#### 好感度 {#sentiment}

[好感度](moderate-ugc.md#sentiment) （センチメント）は、参照先のUGCに表示される投稿を、好感度値が正、負、中立の投稿に制限します。

![chlimage_1-479](assets/chlimage_1-479.png)

## モデレートアクション {#moderation-actions}

[モデレートアクション](moderate-ugc.md#moderation-actions)は、コンテンツ領域で選択された 1 つ以上のコンテンツに対して実行したり、コンテンツの詳細表示時に実行したりできます。

To bulk-moderate the posts, in the content area click the Select ( ![selecticon](assets/selecticon.png)) icon on a post, which appears on hovering over it with the mouse (desktop) or pressing and holding a finger on the post (mobile). この操作をおこなうと、複数選択モードに入ります。複数選択モードでは、一括でモデレートする投稿をクリックするだけで選択できます。ツールバーに表示されるボタンを使用して、選択した投稿に対してモデレートアクションを実行します。どのアクションをおこなうときも、必ず確認メッセージが表示されます。

コンテンツ領域内の 1 つの投稿のみをモデレートする場合は、その投稿の上にマウスポインターを置く（デスクトップの場合）か、その投稿を指で長押しして（モバイルの場合）ボタンを表示します。1 つのコンテンツを操作するときは、削除アクションの場合に限り確認メッセージが表示されます。

### 複数の投稿のモデレート {#moderating-multiple-posts}

Enter the bulk selection mode by clicking the `Select` icon on a post:

![select-icon](assets/select-icon.png)

一括選択モードを終了するには、ツールバーのキャンセル（x）アイコンを選択します。

複数の投稿に対して実行できるモデレートアクションは次のとおりです。

* 拒否
* 削除
* 投稿を閉じる／再度開く

これらのアクションを実行できるアイコンは、複数の投稿を選択したときにのみツールバーに表示されます。

![牛モデレート](assets/bulkmoderate.png)

### 1 つの投稿のモデレート {#moderating-a-single-post}

単一選択モードでは、

* 表示のユーザー名を選択して、ユーザーの詳細を表示します。
* 投稿へのリンクを選択して、投稿をコンテキスト内で表示します
* [返信](#reply)
* [許可](#allow)
* [拒否](#deny)
* [削除](#delete)
* [閉じる](#close)
* View [Moderation History](#moderation-history)
* [詳細を表示](#viewdetails)

モデレートアクションアイコンの上にあるカード表示には、投稿のテキストが表示され、その下には、

* 返信がある場合は、その返信数の前に返信数が表示されます。
* フラグ付けされている場合
* 承認済みの場合
* UGCが投稿された日時

![singleselectmode](assets/singleselectmode.png)

#### 返信 {#reply}

![chlimage_1-480](assets/chlimage_1-480.png)

単一の投稿で作業する場合、UGCタイプが返信をサポートし、返信を許可するように設定されている場合は、返信アイコンが表示されます。

#### アクセス設定 {#allow}

![chlimage_1-481](assets/chlimage_1-481.png)

1 つの投稿を操作するときに、その投稿がフラグ付きか、拒否されている場合は、許可アイコンが表示されます。フラグ付けされた場合、「許可」を選択すると、すべてのフラグがクリアされます。

#### 拒否 {#deny}

![chlimage_1-482](assets/chlimage_1-482.png)

The **Deny** moderation action is only available for content that is moderated, and does not appear on unmoderated content except in multi-selection mode.

モデレート対象でないコンテンツは、必ず承認された状態になります。

モデレート対象のコンテンツは、最初は保留中のステータスになり、後で承認または拒否に変更できます。

保留中から別のステータスに変更されたコンテンツが、保留中に戻ることはありません。承認または拒否のステータスに設定されたコンテンツは、いつでも別のステータスに変更できます。

#### 削除 {#delete}

![chlimage_1-483](assets/chlimage_1-483.png)

単一選択モードまたは一括モードで、アイテムを選択して削除できます。削除のアクションを実行すると、確認ダイアログが表示されます。削除すると、それらの項目はコンテンツ領域からすぐに消えます。 **UGCを削除すると、そのUGCはリポジトリから完全に削除され、後で取得することはできません。**

#### 閉じる {#close}

![chlimage_1-484](assets/chlimage_1-484.png)

単一の投稿で作業する場合、UGCタイプでそのリソースのそれ以上の投稿を防ぐ機能がサポートされていると、閉じるアイコンが表示されます。

#### Moderation History {#moderation-history}

![chlimage_1-485](assets/chlimage_1-485.png)

1 つの投稿を操作するときに、投稿にカーソルを合わせると、モデレート履歴アイコンが表示されます。アイコンを選択すると、UGC投稿に関して行われたアクションの履歴を含むペインが表示されます。

複数の UGC 投稿のコンテンツ領域に戻るには、表示詳細ウィンドウの右上隅の X を選択します。

次に例を示します。

![chlimage_1-486](assets/chlimage_1-486.png)

#### 詳細を表示 {#view-detail}

![chlimage_1-487](assets/chlimage_1-487.png)

1 つの投稿を操作するときに、その UGC を詳細モードで開くと、より詳しい情報を表示できます。

To do so, hover over the post to display the `View Detail` icon and select it to display a panel containing more details of the post.

複数の UGC 投稿のコンテンツ領域に戻るには、表示詳細ウィンドウの右上隅の X を選択します。

次に例を示します。

![chlimage_1-488](assets/chlimage_1-488.png)

