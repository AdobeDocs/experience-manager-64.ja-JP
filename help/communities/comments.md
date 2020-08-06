---
title: コメントの使用
seo-title: コメントの使用
description: サインインしているサイト訪問者はコメント機能を使用して、意見や知識を共有できます
seo-description: サインインしているサイト訪問者はコメント機能を使用して、意見や知識を共有できます
uuid: 30fc48ac-134c-4acb-a65c-398855c93829
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.4/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: b074ebfa-2894-4a2d-aa8e-28168049971a
translation-type: tm+mt
source-git-commit: 59d40b5bddc42a4ac057ef600243f396aefc926b
workflow-type: tm+mt
source-wordcount: '1008'
ht-degree: 37%

---


# コメントの使用 {#using-comments}

## 概要 {#introduction}

サインインしているサイト訪問者（メンバー）は、コメント機能を使用して、サイト上のコンテンツに関する意見や知識を共有できます。この機能は他の機能に既に存在する場合が多く、どのWebサイトにも追加できます。

ドキュメントのこのセクションでは、以下の内容について説明します。

* ページ `Comments`への追加
* Configuration settings for the `Comments`component

>[!NOTE]
>
>匿名でのコメント投稿はサポートされていません。サイト訪問者は参加するには、登録（会員になる）し、サインインする必要があります。

## コメントをページに追加 {#adding-comments-to-a-page}

To add a `Comments`component to a page in author mode, use the component browser to locate

* `Communities / Comments`

コンポーネントを探し、ページ上の適切な位置（ユーザーにコメントしてもらう機能の近くなど）や、単にページの下部にドラッグします。

For necessary information, visit [Communities Components Basics](basics.md).

[必要なクライアント側のライブラリが含まれる場合](essentials-comments.md#essentials-for-client-side) 、これがコンポー `Comments`ネントの表示方法です。

![chlimage_1-428](assets/chlimage_1-428.png)

>[!NOTE]
>
>Only one `Comments`component may exist on a page. コミュニティの機能の中には、既にブログ、カレンダー、フォーラム、QnA、レビューなどのコメントが含まれているものもあります。

## コメントの設定 {#configuring-comments}

Select the placed `Comments` component to access and select the `Configure` icon which opens the edit dialog.

![configure](assets/configure.png) ![commentsettings](assets/commentssettings.png)

### 「コメント」タブ{#comments-tab}

「**[!UICONTROL コメント]**」タブでは、訪問者によるコメントの入力方法を指定します。

* **[!UICONTROL 返信を許可]**

   このオプションを選択すると、メンバーは既存のコメントに返信できます。 初期設定はオフです。

* **[!UICONTROL 1 ページのコメント数]**

   1ページに表示するコメントの数と表示する返信の数を制限します。 初期設定は 10 です。

* **[!UICONTROL ファイルのアップロードを許可]**

   オンにすると、ファイルをアップロードするオプションにテキスト入力ボックスが表示されます。 初期設定はオフです。

* **[!UICONTROL 最大ファイルサイズ]**

   「ファイルのアップロードを許可」がオンになっている場合にのみ関連します。 この値によって、アップロードするファイルサイズが制限されます。デフォルトは 10 MB です。

* **[!UICONTROL メッセージの最大長]**

   テキストボックスに入力できる最大文字数。 初期設定は 4096 文字です。

* **[!UICONTROL 許可されるファイルタイプ]**

   「ファイルのアップロードを許可」がオンになっている場合にのみ関連します。 区切り文字「ドット」を使用したファイル拡張子のカンマ区切りリスト。 例：.jpg, .jpeg, .png, .doc, .docx, .pdf）。ファイルの種類を指定すると、指定されていないファイルは許可されません。 初期設定は、すべてのファイルタイプを許可するように指定されません。

* **[!UICONTROL リッチテキストエディター]**

   オンにすると、注釈と共にコメントを入力できます。 初期設定はオフです。

* **[!UICONTROL 投票を許可]**

   オンにすると、上下に投票するオプションにテキスト入力ボックスが表示されます。 初期設定はオフです。

* **[!UICONTROL フォローを許可]**

   このオプションを選択すると、メンバーはコメントをフォローできます。 初期設定はオフです。

* **[!UICONTROL バッジを表示]**

   オンの場合、獲得および落札済みのバッジの表示を許可します。 初期設定はオフです。

### 「ユーザーモデレート」タブ {#user-moderation-tab}

Under the **[!UICONTROL User Moderation]** tab, specify how the posted comments are managed. For more information, see [Moderating User Generated Content](moderate-ugc.md).

* **[!UICONTROL 事前モデレート]**

   このオプションを選択すると、コメントが発行サイトに表示される前に、承認される必要があります。 初期設定はオフです。

* **[!UICONTROL コメントを削除]**

   オンにすると、コメントを投稿したメンバーに、コメントを削除する機能が与えられます。 初期設定はオフです。

* **[!UICONTROL コメントを拒否]**

   オンにした場合、モデレーターがコメントを拒否できます。 初期設定はオフです。

* **[!UICONTROL コメントを閉じる / 再度開く]**

   このオプションを選択すると、モデレーターはコメントを閉じたり、再度開いたりできます。 初期設定はオフです。

* **[!UICONTROL コメントにフラグを設定]**

   このオプションを選択すると、メンバーは不適切としてコメントにフラグを付けることができます。 初期設定はオフです。

* **[!UICONTROL フラグ設定理由リスト]**

   このオプションを選択すると、メンバーは、コメントに不適切なフラグを付ける理由をドロップダウンリストから選択できます。 初期設定はオフです。

* **[!UICONTROL カスタムフラグ設定理由]**

   このオプションを選択すると、コメントに不適切なフラグを付ける場合に、メンバーが自分の理由を入力できます。 初期設定はオフです。

* **[!UICONTROL モデレートのしきい値]**

   モデレーターに通知する前に、メンバーがコメントにフラグを付ける必要がある回数を入力します。 初期設定は1回です。

* **[!UICONTROL フラグ付けの制限]**

   コメントが公開表示に表示されなくなるまでにフラグを付ける必要がある回数を入力します。 This number must be greater than or equal to the **[!UICONTROL Moderation Threshold]**. 初期設定は 5 です。

### 「並べ替え設定」タブ{#sort-settings-tab}

Under the **[!UICONTROL Sort Settings]** tab, specify how the posted comments are sorted when displayed.

* **[!UICONTROL 並べ替えフィールド]**

   プルダウンして、またはのいずれかを選択 `Newest, Oldest, Last Updated, Most Viewed, Most Active, Most Followed`しま `Most Liked`す。

* **[!UICONTROL 並べ替え順序]**

   プルダウンして、またはのいずれかを選択 `Ascending` しま `Descending`す。

### カスタムコメントタイプへの変更 {#changing-to-a-custom-comment-type}

コメントリソースタイプを変更すると、デフォルトを使用するコメントのインスタンスではなく、開発者によってカスタマイズ（拡張）されたコメントのインスタンスが生成されるようになります。

Once the custom resource types is known, enter [Design Mode](../../help/sites-authoring/default-components-designmode.md) and double click on the placed `Comments` component to open a dialog with an additional tab.

Under the **[!UICONTROL Resource Types]** tab, specify the custom resourceType for new instances of the `Comments or Voting`components:

![chlimage_1-429](assets/chlimage_1-429.png)

* **[!UICONTROL コメントリソースタイプ]**

   /apps内の拡張 `comment`コンポーネント（1つのコメント）のresourceTypeに移動します。 例：`/apps/social/commons/components/hbs/comments/comment`

   このリソースは、訪問者がコメントを投稿したときに作成されたUGCのresourceTypeを識別します。

* **[!UICONTROL 投票リソースタイプ]**

   /apps内の拡張 `voting`コンポーネントのresourceTypeに移動します。 例：`/apps/social/components/hbs/voting`

   このリソースは、訪問者が投票を行ったときに作成されたUGCのリソースタイプを識別します。

* **[!UICONTROL コメントシステムリソースタイプ]**

   /apps内の拡張 `comments`コンポーネント（コメントシステム）のresourceTypeに移動します。 Leave blank unless the page template [dynamically includes](scf.md#add-or-include-a-communities-component) the Comment System in the underlying script instead of being added to the page as a resource (comments node). Learn more by reading about the [{{include}} helper](handlebars-helpers.md#include).

## サイト訪問者のエクスペリエンス {#site-visitor-experience}

### モデレーターおよび管理者 {#moderators-and-administrators}

サインインしているユーザーがモデレーター権限または管理者権限を持っている場合は、誰がコメントを作成したかにかかわらず、コンポーネントの設定によって許可されているモデレートタスクを実行できます。

### メンバー {#members}

サイト訪問者がサインインすると、設定に応じて次のことができます。

* 新しいコメントの投稿
* 自分のコメントの編集
* 自分のコメントを削除する
* 他のユーザーのコメントにフラグを付ける

### 匿名 {#anonymous}

サインインしていないサイト訪問者は、投稿されたコメントを閲覧することしかできず（サポートされている場合は翻訳も可）、コメントを追加したり、他のユーザーのコメントにフラグを設定することはできません。

## 追加情報 {#additional-information}

More information may be found on the [Comments Essentials](essentials-comments.md) page for developers.

For moderation of posted comments, see [Moderating User Generated Content](moderate-ugc.md).

投稿されたコメントの翻訳については、[ユーザー生成コンテンツの翻訳](translate-ugc.md)を参照してください。
