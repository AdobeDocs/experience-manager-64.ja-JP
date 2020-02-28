---
title: ブログ機能
seo-title: ブログ機能
description: ジャーナル形式のコミュニティ情報
seo-description: ジャーナル形式のコミュニティ情報
uuid: 01f1a547-d22b-4da6-a69c-ab420e5a9e19
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.4/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: d5519211-8a04-4699-97bc-e162ec0f3781
translation-type: tm+mt
source-git-commit: 13d890d08a032fe4eef1dac793dcf2a3e682a52c

---


# ブログ機能 {#blog-feature}

## 概要 {#introduction}

AEM Communities のブログ機能は、オーサリングアクティビティから、パブリッシュ環境でおこなわれるコミュニティアクティビティへと変わりました。

ブログ機能は、ジャーナル形式でのコミュニティ情報の提供をサポートします。ブログエントリは、公開環境で、許可されたメンバー（登録されたログインユーザー）によって作成されます。

ブログ機能では以下のことが可能です。

* パブリッシュ側でのブログ記事とコメントの作成
* リッチテキスト編集
* インライン画像（ドラッグアンドドロップのサポートあり）
* 埋め込みソーシャルネットワーキングコンテンツ（[oEmbed のサポート](blog-developer-basics.md#allowing-rich-media)）
* ドラフトモード
* 日時指定公開
* 代理作成（[権限を持つメンバー](users.md#privileged-members-group)が他のコミュニティメンバーの代わりにコンテンツを作成できる）
* ブログ記事やコメントの[コンテキスト内モデレートと一括モデレート](moderate-ugc.md)

ドキュメントのこのセクションでは、以下の内容について説明します。

* AEMサイトへのブログ機能の追加
* ブログコンポーネントの構成設定

>[!NOTE]
>
>コンポーネン `Journal`トとタ `Journal Sidebar` イトルはと `Blog` になりま `Blog Sidebar`す。
>
>AEM 6.0 以前のリリースのブログ機能は、現在は削除されています。テンプレートに基づいており、作成者のみが作成者環境でコンテンツを作成できました。

## ブログコンポーネントをページに追加 {#adding-blog-components-to-a-page}

作成者モードでページにブログを追加する場合は、コンポーネントブラウザを使用して、

* `Communities / Blog`
* `Communities / Blog Sidebar`

ブログが表示されるページにドラッグします。

For necessary information, visit [Communities Components Basics](basics.md).

When the [required client-side libraries](blog-developer-basics.md#essentials-for-client-side) are included, this is how the `Blog`component will appear:

![chlimage_1-147](assets/chlimage_1-147.png)

そして、次のよう `Blog Sidebar` に表示されます。

![chlimage_1-148](assets/chlimage_1-148.png)

### ブログの設定 {#configuring-blog}

Select the placed `Blog` component to access and select the `Configure` icon which opens the edit dialog.

![アイコンブログ](assets/chlimage_1-149.png)![の設定](assets/Blog-configure.png)

#### 「設定」タブ{#settings-tab}

「**[!UICONTROL 設定]**」タブでは、以下に示すブログの基本機能を指定します。

* **[!UICONTROL 添付サムネールを許可]** オンにすると、添付された画像のサムネールが作成されます。

* **[!UICONTROL 添付サムネールの最大サイズ]** 添付サムネール画像の最大サイズ（ピクセル単位）です。デフォルト値は、800 x 800 です。

* **[!UICONTROL サムネールの最小画像サイズ]**&#x200B;インライン画像のサムネールを生成するための画像の最小サイズ（バイト単位）。 デフォルト値は100000バイト(100 KB)です。

* **[!UICONTROL Max Thumbnail Sizeインラ]**&#x200B;イン画像のサムネール画像の最大サイズ（ピクセル単位）。 デフォルト値は、800 x 800 です。

* **[!UICONTROL 「Allow Privileged Members]**」を選択すると、「Privileged Members」のみがコンテンツの作成を許可されます。

* **[!UICONTROL 許可された権限を持つメンバー]**&#x200B;コンテンツの作成を許可された、権限を持つメンバーを追加します。

* **[!UICONTROL 作成者編集モードでのユーザー生成コンテンツのブロック]**&#x200B;有効な場合、作成者モードでの編集中にユーザー生成コンテンツがブロックされます。

* **[!UICONTROL ジャーナルタイトル]**&#x200B;ページに表示されるブログのタイトルです。
   >注意：
   >ジャーナルタイトルは、ブログ用の URL を自動的に作成するために使用されます。ここで指定するジャーナルタイトルから、ブログのURLを作成する際に使用する最大50文字（一意性を確保するために5文字を含む）。

* **[!UICONTROL ジャーナルの説明]**&#x200B;ブログの説明です。

* **[!UICONTROL 1 ページのトピック数]**

   1ページに表示するブログエントリ数/コメント数を定義します。 初期設定は 10 です。

* **[!UICONTROL モデレート]**

   オンにした場合、ブログエントリとコメントの投稿は、公開サイトに表示される前に承認する必要があります。 初期設定はオフです。

* **[!UICONTROL 閉じる]**

   オンにすると、ブログは新しいブログエントリとコメントに閉じられます。 初期設定はオフです。

* **[!UICONTROL リッチテキストエディター]**

   オンにすると、ブログエントリとコメントがマークアップ付きで入力される場合があります。 初期設定はオンです。

* **[!UICONTROL タグ付けを許可]**

   If checked, allow members to add tag labels to their post (see **[!UICONTROL Tag field]** tab). 初期設定はオフです。

* **[!UICONTROL ファイルのアップロードを許可]**

   オンにした場合、添付ファイルをブログエントリまたはコメントに追加できます。 初期設定はオフです。

* **[!UICONTROL 最大ファイルサイズ]**

   がオンの場合にのみ `Allow File Uploads` 関連します。 このフィールドは、アップロードするファイルのサイズ（バイト単位）を制限します。 初期設定は104857600(10 Mb)です。

* **[!UICONTROL 許可されるファイルタイプ]**

   がオンの場合にのみ `Allow File Uploads` 関連します。 ドット付きのファイル拡張子をコンマ区切りで指定します（例：.jpg, .jpeg, .png, .doc, .docx, .pdf）。ファイルタイプを指定した場合、指定しなかったファイルはアップロードできません。 初期設定はnoneで、すべてのファイルタイプが許可されます。

* **[!UICONTROL 添付する画像ファイルの最大サイズ]**

   「ファイルのアップロードを許可」がオンになっている場合にのみ関連します。 アップロードされた画像ファイルの最大バイト数。 初期設定は2097152(2 Mb)です。

* **[!UICONTROL 応答を許可]**

   オンの場合、ブログエントリに投稿されたコメントへの返信を許可します。 初期設定はオフです。

* **[!UICONTROL ユーザーによるコメントおよびトピックの削除を許可]**

   オンにした場合、投稿したコメントやブログエントリの削除をメンバーに許可します。 初期設定はオフです。

* **[!UICONTROL フォローを許可]**

   If checked, include the following feature for blog articles, which allows members to be [notified](notifications.md) of new posts. 初期設定はオフです。

* **[!UICONTROL 電子メール購読を許可]**

   If checked, allow members to be notified of new posts by email ([subscription](subscriptions.md)). Requires `Allow Following` to be checked and [email configured](email.md). 初期設定はオフです。

* **[!UICONTROL 投票を許可]**

   オンの場合、ブログエントリに投票機能を含めます。 初期設定はオフです。

* **[!UICONTROL バッジを表示]**

   If checked, display earned and assigned [badges](implementing-scoring.md) with a member&#39;s blog entry. 初期設定はオフです。

* **[!UICONTROL おすすめコンテンツを許可]**

   if checked, the idea is able to be identified as [featured content](featured.md). 初期設定はオフです。

#### 「ユーザーモデレート」タブ {#user-moderation-tab}

「**[!UICONTROL ユーザーモデレート]**」タブでは、以下のモデレート設定を指定します。

* **[!UICONTROL 投稿を拒否]**

   選択すると、信頼されたメンバーのモデレーターは、投稿を拒否し、投稿が公開フォーラムに表示されるのを防ぐことができます。 初期設定はオフです。

* **[!UICONTROL トピックを閉じる / 再度開く]**

   このオプションを選択すると、信頼されたメンバーのモデレーターがトピックを閉じて、さらに編集やコメントを行ったり、トピックを再度開いたりする場合があります。 初期設定はオフです。

* **[!UICONTROL 投稿にフラグを設定]**

   選択した場合、他のユーザーのトピックやコメントに不適切なフラグを付けることを許可します。 初期設定はオフです。

* **[!UICONTROL フラグ設定理由リスト]**

   このオプションを選択すると、トピックまたはコメントに不適切なフラグを付ける理由を、ドロップダウンリストからメンバーが選択できるようになります。 初期設定はオフです。

* **[!UICONTROL カスタムフラグ設定理由]**

   選択した場合、トピックやコメントに不適切としてフラグを付ける独自の理由をメンバーが入力できるようにします。 初期設定はオフです。

* **[!UICONTROL モデレートのしきい値]**

   モデレーターに通知する前に、メンバーがトピックまたはコメントにフラグを付ける必要がある回数を入力します。 初期設定は1（1回）です。

* **[!UICONTROL フラグ付けの制限]**

   トピックまたはコメントが公開ビューに表示されなくなるまでにフラグを付ける必要がある回数を入力します。 -1に設定した場合、フラグ付けされたトピックまたはコメントは公開ビューで非表示になりません。 そうでない場合、この数値はモデレートのしきい値以上にする必要があります。 初期設定は 5 です。

#### 「タグフィールド」タブ{#tag-field-tab}

「**[!UICONTROL タグフィールド]**」タブでは、「**[!UICONTROL 設定]**」タブで「**[!UICONTROL タグ付けを許可]**」がオンの場合に適用できるタグを指定します。

* **[!UICONTROL 許可された名前空間]**

   「設定」タブで `Allow Tagging` 選択されている場合に **[!UICONTROL 関連]** 。 適用できるタグは、チェックされた名前空間カテゴリ内のタグに制限されます。 名前空間のリストには、「Standard Tags」（デフォルトの名前空間）と「Include All Tags」が含まれます。 初期設定はnoneで、すべての名前空間が許可されます。

* **[!UICONTROL 推奨の制限]**

   フォーラムへの投稿に対して提案として表示するタグの数を入力します。 -1 は無制限を意味します。初期設定は 0 です。

### ブログのサイドバーの設定 {#configuring-blog-sidebar}

When you double-click the `Blog Sidebar` component, an edit dialog opens up.

「**[!UICONTROL ジャーナルサイドバー設定]**」タブでは、アーカイブの日付の形式と、サイドバーに表示するエントリのタイプを指定します。

![chlimage_1-151](assets/chlimage_1-151.png)

* **[!UICONTROL 日付の形式]**

   ブログエントリのアーカイブに表示する形式。 Java 表記法に従って、プレースホルダーを使用します。

   * yyyy：4 桁の西暦（例：2015）
   * yy：西暦の下 2 桁（例：15）
   * MMMMM：月の正式名（例：June）
   * MMM：月の短縮名（例：Jun）
   * MM：月の数字（例：06）
   初期設定は「yyyy MMMMM」です。これは「2015 June」のように表示されます。

* **[!UICONTROL 表示タイプ]**

   サイドバーに表示するブログエントリのタイトルとタイプ。 選択肢は次のとおりです。

   * 作成者
   * カテゴリ
   * アーカイブ

* **[!UICONTROL ジャーナルコンポーネントのパス]**

   *(オプション* )ブログ記事のリスト元となるブログリソースの場所。 If left blank, will use the component of resourceType `social/journal/components/hbs/journal` that appears on the same page.

   * 例：`/content/sites/engage/en/blog/jcr:content/content/primary/blog`

* **[!UICONTROL 推奨の制限]**

   表示するブログ記事の数。 -1 は無制限を意味します。初期設定は -1 です。

## サイト訪問者のエクスペリエンス {#site-visitor-experience}

パブリッシュ環境では、ブログ記事は作成の降順に表示されます（最新のブログ記事の後に、古いブログ記事が表示されます）。ブログのサイドバーを使用すると、サイトの訪問者はフィルタを適用して、表示されるブログ記事の選択を制限できます。

ブログ記事の下には、コメントを投稿または表示するためのリンクが表示されます。

ブログ記事を選択すると、そのブログ記事とコメントが表示されます（有効な場合）。

その他の機能は、サイト訪問者がモデレーターか、管理者か、コミュニティメンバーか、権限を持つメンバーか、匿名かによって異なります。

### 記事の操作 {#working-with-articles}

新しいブログ記事を作成するときには、公開方法を以下の中から選択できます。

1. 即時公開する
1. ドラフトを公開する
1. 指定された日時に公開する

ブログ記事は、それぞれ適切なタブ（公開済み、ドラフト、スケジュール済み）で、パブリッシュ環境でオーサリングできるメンバー向けに表示されます。

#### モデレーターおよび管理者 {#moderators-and-administrators}

サインインしているユーザーがモデレーター権限または管理者権限を持っている場合、そのユーザーは、すべてのブログ記事およびブログに投稿されたコメントに対して[モデレートタスク](moderate-ugc.md)を実行できます（実行可能な操作はコンポーネントの設定に従います）。

![chlimage_1-152](assets/chlimage_1-152.png)

### メンバー {#members}

When the signed in user is a community member or [privileged member](users.md#privileged-members-group) (depending on configuration), they are able to select `New Article` to create and post a new blog article.

具体的には、次のことが可能です。

* 新しいブログ記事の作成
* 別のメンバーに代わって新しいブログ記事を投稿する
* ブログ記事へのコメントの投稿
* 自分のブログ記事またはコメントの編集
* 自分のブログ記事またはコメントを削除する
* 他のユーザーのブログ記事またはコメントにフラグを付ける

![chlimage_1-153](assets/chlimage_1-153.png) ![chlimage_1-154](assets/chlimage_1-154.png)

### 匿名 {#anonymous}

サインインしていないサイト訪問者は、投稿されたブログ記事やコメントを閲覧することしかできず（サポートされている場合は翻訳も可）、ブログ記事やコメントを追加したり、他人の記事やコメントにフラグを設定することはできません。

![chlimage_1-155](assets/chlimage_1-155.png)

## 追加情報 {#additional-information}

開発者向けの詳細情報は、[ブログの基本事項](blog-developer-basics.md)ページを参照してください。

ブログエントリとコメントのモデレートについては、[ユーザー生成コンテンツのモデレート](moderate-ugc.md)を参照してください。

ブログエントリとコメントのタグ付けについては、[ユーザー生成コンテンツのタグ付け](tag-ugc.md)を参照してください。

ブログエントリとコメントの翻訳については、[ユーザー生成コンテンツの翻訳](translate-ugc.md)を参照してください。
