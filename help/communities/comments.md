---
title: コメントの使用
seo-title: Using Comments
description: サインインしているサイト訪問者はコメント機能を使用して、意見や知識を共有できます
seo-description: Comments feature lets signed-in site visitors share their opinions and knowledge
uuid: 30fc48ac-134c-4acb-a65c-398855c93829
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.4/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: b074ebfa-2894-4a2d-aa8e-28168049971a
exl-id: 8ad5ce3e-c5dd-48d7-8812-43172eda36cc
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '995'
ht-degree: 36%

---

# コメントの使用 {#using-comments}

## はじめに {#introduction}

サインインしているサイト訪問者（メンバー）は、コメント機能を使用して、サイト上のコンテンツに関する意見や知識を共有できます。この機能は、多くの場合、他の機能に既に存在しますが、Web サイトに追加することもできます。

ドキュメントのこのセクションでは、以下の内容について説明します。

* 追加中 `Comments`ページに
* の設定 `Comments`コンポーネント

>[!NOTE]
>
>匿名でのコメント投稿はサポートされていません。サイト訪問者が参加するには、登録（メンバーになる）してサインインする必要があります。

## コメントをページに追加 {#adding-comments-to-a-page}

を追加するには、以下を実行します。 `Comments`コンポーネントをオーサリングモードでページに追加する場合は、コンポーネントブラウザーを使用して

* `Communities / Comments`

コンポーネントを探し、ページ上の適切な位置（ユーザーにコメントしてもらう機能の近くなど）や、単にページの下部にドラッグします。

必要な情報については、 [コミュニティコンポーネントの基本](basics.md).

次の場合に [必要なクライアント側ライブラリ](essentials-comments.md#essentials-for-client-side) が含まれる場合、この方法で `Comments`コンポーネントが表示されます。

![chlimage_1-428](assets/chlimage_1-428.png)

>[!NOTE]
>
>1 つだけ `Comments`コンポーネントは、ページ上に存在する場合があります。 一部のコミュニティ機能には、ブログ、カレンダー、フォーラム、Q&amp;A、レビューなどのコメントが既に含まれています。

## コメントの設定 {#configuring-comments}

配置された `Comments` アクセスして選択するコンポーネント `Configure` 編集ダイアログを開くアイコン。

![設定](assets/configure.png) ![commentsettings](assets/commentssettings.png)

### 「コメント」タブ {#comments-tab}

「**[!UICONTROL コメント]**」タブでは、訪問者によるコメントの入力方法を指定します。

* **[!UICONTROL 返信を許可]**

   オンにすると、メンバーは既存のコメントに返信できます。 初期設定はオフです。

* **[!UICONTROL 1 ページのコメント数]**

   1 ページに表示するコメントの数と、表示する返信の数を制限します。 初期設定は 10 です。

* **[!UICONTROL ファイルのアップロードを許可]**

   オンにすると、ファイルをアップロードするオプションに、テキスト入力ボックスが表示されます。 初期設定はオフです。

* **[!UICONTROL 最大ファイルサイズ]**

   「ファイルのアップロードを許可」がオンの場合にのみ関連します。 この値によって、アップロードするファイルサイズが制限されます。デフォルトは 10 MB です。

* **[!UICONTROL メッセージの最大長]**

   テキストボックスに入力できる最大文字数。 初期設定は 4096 文字です。

* **[!UICONTROL 許可されるファイルタイプ]**

   「ファイルのアップロードを許可」がオンの場合にのみ関連します。 「ドット」区切り記号を使用したファイル拡張子のコンマ区切りリスト。 例：.jpg, .jpeg, .png, .doc, .docx, .pdf）。ファイルタイプを指定した場合、指定しなかったファイルは許可されません。 初期設定では何も指定されず、すべてのファイルタイプが許可されます。

* **[!UICONTROL リッチテキストエディター]**

   オンにすると、マークアップを使用してコメントを入力できます。 初期設定はオフです。

* **[!UICONTROL 投票を許可]**

   オンにすると、上下に投票するオプションにテキスト入力ボックスが表示されます。 初期設定はオフです。

* **[!UICONTROL フォローを許可]**

   オンにすると、メンバーはコメントをフォローできます。 初期設定はオフです。

* **[!UICONTROL バッジを表示]**

   オンにすると、獲得および授与されたバッジを表示できます。 初期設定はオフです。

### 「ユーザーモデレート」タブ {#user-moderation-tab}

以下 **[!UICONTROL ユーザーモデレート]** タブで、投稿されたコメントの管理方法を指定します。 詳しくは、 [ユーザー生成コンテンツのモデレート](moderate-ugc.md).

* **[!UICONTROL 事前モデレート]**

   オンにすると、コメントは、公開サイトに表示される前に承認が必要になります。 初期設定はオフです。

* **[!UICONTROL コメントを削除]**

   オンにすると、コメントを投稿したメンバーはコメントを削除できます。 初期設定はオフです。

* **[!UICONTROL コメントを拒否]**

   オンにすると、モデレーターはコメントを拒否できます。 初期設定はオフです。

* **[!UICONTROL コメントを閉じる / 再度開く]**

   オンにすると、モデレーターはコメントを閉じて再度開くことができます。 初期設定はオフです。

* **[!UICONTROL コメントにフラグを設定]**

   オンにすると、メンバーはコメントに「不適切」のフラグを設定できます。 初期設定はオフです。

* **[!UICONTROL フラグ設定理由リスト]**

   オンにすると、メンバーはコメントに「不適切」のフラグを設定した理由をドロップダウンリストから選択できます。 初期設定はオフです。

* **[!UICONTROL カスタムフラグ設定理由]**

   オンにすると、メンバーはコメントに「不適切」のフラグを設定した独自の理由を入力できます。 初期設定はオフです。

* **[!UICONTROL モデレートのしきい値]**

   メンバーがコメントに何回フラグを設定したらモデレーターに通知するかを指定します。 初期設定は 1 回 (1) です。

* **[!UICONTROL フラグ付けの制限]**

   コメントに何回フラグを設定したら、公開ビューで非表示にするかを指定します。 この数は **[!UICONTROL モデレートのしきい値]**. 初期設定は 5 です。

### 「並べ替え設定」タブ {#sort-settings-tab}

以下 **[!UICONTROL 並べ替え設定]** タブで、投稿されたコメントを表示する際の並べ替え方法を指定します。

* **[!UICONTROL 並べ替えフィールド]**

   プルダウンして次のいずれかを選択 `Newest, Oldest, Last Updated, Most Viewed, Most Active, Most Followed`または `Most Liked`.

* **[!UICONTROL 並べ替え順序]**

   プルダウンして次のいずれかを選択 `Ascending` または `Descending`.

### カスタムコメントタイプへの変更 {#changing-to-a-custom-comment-type}

コメントリソースタイプを変更すると、デフォルトを使用するコメントのインスタンスではなく、開発者によってカスタマイズ（拡張）されたコメントのインスタンスが生成されるようになります。

カスタムリソースタイプがわかったら、次のように入力します。 [デザインモード](../../help/sites-authoring/default-components-designmode.md) そして、配置された `Comments` 追加のタブを含むダイアログを開くコンポーネント。

以下 **[!UICONTROL リソースタイプ]** タブで、新しいインスタンスのカスタム resourceType を指定します。 `Comments or Voting`コンポーネント：

![chlimage_1-429](assets/chlimage_1-429.png)

* **[!UICONTROL コメントリソースタイプ]**

   拡張の resourceType に移動します。 `comment`/apps 内のコンポーネント（単一のコメント）。 例：`/apps/social/commons/components/hbs/comments/comment`

   このリソースは、訪問者がコメントを投稿したときに作成された UGC の resourceType を識別します。

* **[!UICONTROL 投票リソースタイプ]**

   拡張の resourceType に移動します。 `voting`/apps 内のコンポーネント。 例：`/apps/social/components/hbs/voting`

   このリソースは、訪問者が投票を投稿したときに作成された UGC のリソースタイプを識別します。

* **[!UICONTROL コメントシステムリソースタイプ]**

   拡張の resourceType に移動します。 `comments`/apps 内のコンポーネント（コメントシステム）。 ページテンプレートがない場合は空白のままにします [動的に含む](scf.md#add-or-include-a-communities-component) コメントシステムをリソースとしてページに追加する代わりに、基になるスクリプト内で使用します（コメントノード）。 詳しくは、 [{{include}} ヘルパー](handlebars-helpers.md#include).

## サイト訪問者のエクスペリエンス {#site-visitor-experience}

### モデレーターおよび管理者 {#moderators-and-administrators}

サインインしているユーザーがモデレーター権限または管理者権限を持っている場合は、誰がコメントを作成したかにかかわらず、コンポーネントの設定によって許可されているモデレートタスクを実行できます。

### メンバー {#members}

サイト訪問者がサインインすると、設定に応じて次のことができます。

* 新しいコメントを投稿
* 自分のコメントを編集
* 自分のコメントを削除
* 他のユーザーのコメントにフラグを設定する

### 匿名 {#anonymous}

サインインしていないサイト訪問者は、投稿されたコメントを閲覧することしかできず（サポートされている場合は翻訳も可）、コメントを追加したり、他のユーザーのコメントにフラグを設定することはできません。

## 追加情報 {#additional-information}

詳しくは、 [コメントの基本事項](essentials-comments.md) 開発者向けのページ

投稿されたコメントのモデレートについては、 [ユーザー生成コンテンツのモデレート](moderate-ugc.md).

投稿されたコメントの翻訳については、[ユーザー生成コンテンツの翻訳](translate-ugc.md)を参照してください。
