---
title: Q&A フォーラム機能
seo-title: Q&A フォーラム機能
description: Q&A フォーラム機能をページに追加
seo-description: Q&A フォーラム機能をページに追加
uuid: 006c0bf0-c230-4890-8080-65651f4b4dac
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.4/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: bbbe32bb-9d97-461e-822f-a7ddc6c9f9ef
translation-type: tm+mt
source-git-commit: 5ddbcb2addff2d6e3a3e9d7e100a6d9ba89fdd60
workflow-type: tm+mt
source-wordcount: '1216'
ht-degree: 61%

---


# Q&amp;A フォーラム機能 {#q-a-forum-feature}

## 概要 {#introduction}

QnA（質問と回答）フォーラム機能を使用すると、コミュニティメンバーが次のような質問や回答をすることができます。

* 新しい質問の作成
* インライン画像（ドラッグアンドドロップのサポートあり）
* 表示と回答
* 質問の検索
* QnAコンテンツのモデレートの支援
* 最適な回答を特定する
* QnA質問をページ間で移動する

ドキュメントのこのセクションでは、以下の内容について説明します。

* AEMサイトへのQnAフォーラム機能の追加
* Configuration settings for the `QnA`component

## Q&amp;A フォーラムをページに追加 {#adding-a-q-a-forum-to-a-page}

作成者モードでページに `QnA` コンポーネントを追加するには、コンポーネントブラウザーを使用してQnAフォーラムが表示されるページを探し `Communities / QnA` 、その場所にドラッグします。

For necessary information, visit [Communities Components Basics](basics.md).

[必要なクライアント側ライブラリが含まれる場合](qna-essentials.md#essentials-for-client-side) 、次のようにコンポー `QnA` ネントが表示されます。

![chlimage_1-280](assets/chlimage_1-280.png)

### Q&amp;A の設定 {#configuring-qna}

Select the placed `QnA` component to access and select the `Configure` icon which opens the edit dialog.

![chlimage_1-281](assets/chlimage_1-281.png) ![chlimage_1-282](assets/chlimage_1-282.png)

#### 「設定」タブ{#settings-tab}

「**[!UICONTROL 設定]**」タブでは、トピック（質問）と返信（回答）の基本機能を設定します。

* **[!UICONTROL 1 ページのトピック数]** 1 ページに表示する質問数または投稿数を定義します。初期設定は 10 です。

* **[!UICONTROL モデレート]**&#x200B;オンにすると、トピックおよびコメントの投稿を公開サイトに表示する前に承認が必要になります。初期設定はオフです。

* **[!UICONTROL 閉じる]**&#x200B;オンにすると、フォーラムは新しい質問やコメントを受け付けなくなります。初期設定はオフです。

* **[!UICONTROL リッチテキストエディター]**&#x200B;オンにすると、マークアップを使用してトピックおよびコメントを入力できます。初期設定はオフです。

* **[!UICONTROL タグ付けを許可]**&#x200B;オンにすると、メンバーは自分の投稿にタグラベルを付加できます（「**[!UICONTROL タグフィールド]**」タブを参照）。初期設定はオフです。

* **[!UICONTROL ファイルのアップロードを許可]**&#x200B;オンにすると、質問またはコメントに添付ファイルを付加できます。初期設定はオフです。

* **[!UICONTROL 最大ファイルサイズ]**&#x200B;関連( 
`Allow File Uploads` がチェックされている。 このフィールドは、アップロードされるファイルのサイズ（バイト単位）を制限します。 初期設定は104857600(10 Mb)です。

* **[!UICONTROL 許可されているファイルタイプ]**&#x200B;は、 
`Allow File Uploads` がチェックされている。 ドット付きのファイル拡張子をコンマ区切りで指定します（例：.jpg, .jpeg, .png, .doc, .docx, .pdf）。ファイルの種類が指定されている場合、指定されていないファイルはアップロードできません。 初期設定は、すべてのファイルタイプを許可するように指定されません。

* **[!UICONTROL 「ファイルのアップロードを許可」が選択されている場合のみ、「添付画像ファイルの最大サイズ]**」が関連します。 アップロードされた画像ファイルの最大バイト数。 初期設定は2097152(2 Mb)です。

* **[!UICONTROL フォローを許可]**&#x200B;オンにすると、フォーラム投稿のフォロー機能が追加され、新しい投稿をメンバーに[通知](notifications.md)できます。初期設定はオフです。

* **[!UICONTROL ピン留めを許可]**&#x200B;オンにすると、フォーラムトピックをトピックリストの上部にピン留めできます。初期設定はオフです。

* **[!UICONTROL 電子メール購読を許可]**&#x200B;オンにすると、新しい投稿があった場合にメンバーに電子メールで通知できるようになります（[購読](subscriptions.md)）。Requires `Allow Following` to be checked and [email configured](email.md). 初期設定はオフです。

* **[!UICONTROL 応答を許可]**&#x200B;オンにすると、質問に投稿されたコメントへの返信を許可します。初期設定はオフです。

* **[!UICONTROL ユーザーによるコメントおよびトピックの削除を許可]**&#x200B;オンにすると、メンバーは自分が投稿したコメントおよび質問を削除できます。初期設定はオフです。

* **[!UICONTROL 投票を許可]**&#x200B;オンにすると、質問に投票機能が組み込まれます。初期設定はオフです。

* **[!UICONTROL 選択した回答を一番上に移動]**&#x200B;オンにすると、選択した回答が最初に表示される回答になります。初期設定はオンです。

* **[!UICONTROL バッジを表示]**&#x200B;オンにすると、獲得した[バッジ](implementing-scoring.md)と割り当てられたバッジがメンバーのブログエントリに表示されます。初期設定はオフです。

* **[!UICONTROL おすすめコンテンツを許可]**&#x200B;オンにすると、アイデアを[おすすめコンテンツ](featured.md)として指定できます。初期設定はオフです。

#### 「ユーザーモデレート」タブ {#user-moderation-tab}

Under the **[!UICONTROL User Moderation]** tab, specify how the posted topics (quetions) and answers (user generated content) are managed. For more information, see [Moderating User Generated Content](moderate-ugc.md).

* **[!UICONTROL 回答を拒否]**&#x200B;オンにすると、信頼されているメンバーモデレーターが投稿された回答を拒否して、公開 Q&amp;A フォーラムへの表示を止めることができます。初期設定はオフです。

* **[!UICONTROL トピックを閉じる／再度開く]**&#x200B;オンにすると、信頼されているメンバーモデレーターが、質問（トピック）をそれ以上編集および回答できないように閉じたり、再度開いたりすることができます。初期設定はオフです。

* **[!UICONTROL トークンを移動]**&#x200B;オンにすると、パブリッシュ側のモデレーターが質問を移動できます。初期設定はオフです。

* **[!UICONTROL 投稿にフラグを設定]**&#x200B;オンにすると、メンバーは他のメンバーの質問または回答に「不適切」のフラグを設定できます。初期設定はオフです。

* **[!UICONTROL フラグ設定理由リスト]**&#x200B;オンにすると、メンバーは質問または回答に「不適切」のフラグを設定した理由をドロップダウンリストから選択できます。初期設定はオフです。

* **[!UICONTROL カスタムフラグ設定理由]**&#x200B;オンにすると、メンバーは質問または回答に「不適切」のフラグを設定した独自の理由を入力できます。初期設定はオフです。

* **[!UICONTROL モデレートのしきい値]**&#x200B;メンバーが質問または回答に何回フラグを設定したらモデレーターに通知するかを指定します。初期設定は1（1回）です。

* **[!UICONTROL フラグ付けの制限]**&#x200B;質問または回答に何回フラグが設定されたら、公開表示から非公開にするかを指定します。-1に設定した場合、フラグ付けされた質問または回答がパブリック表示に隠されることはありません。 それ以外の場合は、この数値をモデレートしきい値以上にする必要があります。 初期設定は 5 です。

#### 「タグフィールド」タブ{#tag-field-tab}

「**[!UICONTROL タグフィールド]**」タブでは、「**[!UICONTROL 設定]**」タブでタグ付けが許可されている場合に、適用できるタグを名前空間に従って制限します。

* **[!UICONTROL 許可されている名前空間]**&#x200B;関連( 
`Allow Tagging` が「 **設定** 」タブでチェックされている。 適用できるタグは、チェック対象の名前空間カテゴリ内のタグに限定されます。 名前空間のリストには、「標準タグ」(デフォルトの名前空間)と「すべてのタグを含む」があります。 初期設定はオフで、すべての名前空間が許可されます。

* **[!UICONTROL 推奨の制限]**&#x200B;フォーラムに投稿するメンバーに表示する推奨タグの数を入力します。値 
`-1` は、制限がないことを意味します。 初期設定は 0 です。

#### 「並べ替え設定」タブ{#sort-settings-tab}

Under the **[!UICONTROL Sort Settings]** tab, specify how the posted comments are sorted when displayed.

* **[!UICONTROL 並べ替えの基準]**：許可されている並べ替えの選択項目をすべて選択します。 
`Newest, Oldest, Last Updated, Most Viewed, Most Active, Most Followed and Most Liked`」を選択します。デフォルトは `Newest, Oldest, Last Updated` です。

* **[!UICONTROL デフォルトとして設定]**&#x200B;プルダウンして、オンになっている並べ替えオプションのいずれかを選択し、デフォルトとして表示されるようにします。初期設定は です。 
`Newest`。

* **[!UICONTROL Analytics Sortingのプルダウンの「Time Options」を選択し]**&#x200B;て、 
`All, Last 24 Hours, Last 7 Days, Last 30 Days`」を選択します。デフォルトは `All` です。

## サイト訪問者のエクスペリエンス {#site-visitor-experience}

### 回答の指定 {#identifying-answers}

One answer can be marked as a correct or useful answer using the `Select Answer` button. Once a Question is marked as Answered, another answer cannot be selected until the first one has been unselected using the `Unmark Chosen Answer`button.

Once selected as a viable answer, it may be unselected using the `Unmark Chosen Answer` button.

Once an answer is selected as the viable answer, an indication that the question has been `Answered`is displayed next to the question topic on the main QnA page.

### モデレーターおよび管理者 {#moderators-and-administrators}

サインインしているユーザーがモデレーター権限または管理者権限を持っている場合は、誰が質問または回答を作成したかにかかわらず、コンポーネントの設定によって許可されているモデレートタスクを実行できます。

回答を指定することもできます。

### メンバー {#members}

サイト訪問者がサインインすると、設定に応じて次のことができます。

* 新しい質問の投稿
* 自分が作成した質問を編集または削除する
* 他のユーザーの質問や回答にフラグを付けることもできます。
* 自分が作成した質問に対する回答を特定できる

### 匿名 {#anonymous}

サインインしていないサイト訪問者は、投稿された質問と回答を閲覧することしかできず（サポートされている場合は翻訳も可）、質問または回答を追加したり、他のユーザーの投稿にフラグを設定したりすることはできません。

## 追加情報 {#additional-information}

詳しくは、開発者向けの [Q&amp;A の基本事項](qna-essentials.md)ページを参照してください。

投稿されたトピックとコメントのモデレートについては、[ユーザー生成コンテンツのモデレート](moderate-ugc.md)を参照してください。

投稿されたトピックとコメントのタグ付けについては、[ユーザー生成コンテンツのタグ付け](tag-ugc.md)を参照してください。
