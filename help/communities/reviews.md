---
title: レビューおよびレビューの概要（表示）の使用
seo-title: Using Reviews and Reviews Summary (Display)
description: レビューおよびレビューサマリーコンポーネントをページに追加する
seo-description: Adding the Reviews and Reviews Summary components to a page
uuid: bd1ccee7-b26b-4a27-b1ea-89609f5080af
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.4/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: bf4e7809-8def-4647-aaa6-3ac36865511f
exl-id: 5aae7744-73cc-472b-a4e6-ecd88284b70c
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '1338'
ht-degree: 3%

---

# レビューおよびレビューの概要（表示）の使用 {#using-reviews-and-reviews-summary-display}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

この `Reviews`コンポーネントは、 [ `Comments`](comments.md) および [ `Rating`](rating.md) コンポーネントを使用する準備が整いました。

この `Reviews Summary (Display)` コンポーネントは、アクティブなインスタンスまたは閉じたインスタンスの概要を提供します `Reviews` サイト上の他の場所に表示するコンポーネント。

>[!NOTE]
>
>レビューの匿名投稿はサポートされていません。 サイト訪問者が参加するには、登録（メンバーになる）してサインインする必要があります。 サインインした訪問者は、いつでもレビューを更新できます。

## ページへのレビューの追加 {#adding-a-review-to-a-page}

を追加するには、以下を実行します。 `Reviews` コンポーネントをオーサリングモードでページに追加する場合は、コンポーネントブラウザーを使用して `Communities / Reviews` をクリックし、ページ上の適切な位置（ユーザーが確認できる機能を基準とした位置など）にドラッグします。

必要な情報については、 [コミュニティコンポーネントの基本](basics.md).

次の場合に [必要なクライアント側ライブラリ](reviews-basics.md#essentials-for-client-side) が含まれる場合、この方法で `Reviews`コンポーネントが表示されます。

![chlimage_1-340](assets/chlimage_1-340.png)

## レビューの設定 {#configuring-reviews}

配置された `Reviews` アクセスして選択するコンポーネント `Configure` 編集ダイアログを開くアイコン。

![chlimage_1-341](assets/chlimage_1-341.png)

以下 **[!UICONTROL 許可された評価]** タブで、メンバーに表示する評価の完全なリストを指定します。 最初の評価は、全体的/一般的な評価である必要があります。これは、の平均評価を提供する評価です。 `Review Summary (Display)` コンポーネント。 デフォルト設定の次の 2 つの評価には、「サブレーティング 1」または「サブレーティング 2」以外の異なるタイトルを付ける必要があります。

![chlimage_1-342](assets/chlimage_1-342.png)

* **[!UICONTROL 許可された評価]**

   メンバーが選択できる評価のリストです。

   上向き矢印、下向き矢印および削除ボタンを使用して、表示される選択項目を変更します。

   クリック **[!UICONTROL 項目を追加]** 別の評価選択肢を追加する場合。

以下 **[!UICONTROL 必須の評価]** 」タブで、 **[!UICONTROL 許可された評価]** 評価が必要です。 「許可された評価」タブでのみ指定された項目は、メンバーが送信した際に、マークが付いていないままにすることができます。

Web サイトでは、必須の評価にアスタリスクが付いています。 項目が必須で、マークが付いていない場合は、必要な評価がすべてマークされるまで、メッセージがメンバーに表示され、送信が拒否されます。

![chlimage_1-343](assets/chlimage_1-343.png)

* **[!UICONTROL 必須の評価]**

   許可された評価のサブセットで、必要な評価を示します。

   上向き矢印、下向き矢印および削除ボタンを使用して、表示される選択項目を変更します。

   クリック **[!UICONTROL 項目を追加]** 別の回答選択肢を追加する場合。

>[!NOTE]
>
>項目が **[!UICONTROL 必須の評価]** タブ **[!UICONTROL 許可された評価]** 」タブに値を入力した場合、評価する項目には含まれません。

以下 **[!UICONTROL レビュー]** タブで、レビューの処理方法を指定します。

![chlimage_1-344](assets/chlimage_1-344.png)

* **[!UICONTROL 返信を許可]**
オンにすると、レビューへの返信が許可されます。 初期設定はオフです。

* **[!UICONTROL クローズ]**
オンにすると、レビューは新しいレビューと返信に対して閉じられます。 初期設定はオフです。

* **[!UICONTROL ファイルのアップロードを許可]**
オンにすると、レビュー用に添付ファイルをアップロードできます。 初期設定はオフです。

* **[!UICONTROL 最大ファイルサイズ]**
次の場合にのみ関連します。 **[!UICONTROL ファイルのアップロードを許可]** がオンになっている。 このフィールドは、アップロードするファイルのサイズ（バイト単位）を制限します。 初期設定は 10 MB です。

* **[!UICONTROL メッセージの最大長]**
テキストボックスに入力できる最大文字数。 デフォルトは 4096 文字です。

* **[!UICONTROL 許可されているファイルタイプ]**
次の場合にのみ関連します。 **[!UICONTROL ファイルのアップロードを許可]** がオンになっている。 「ドット」区切り文字を使用したファイル拡張子のコンマ区切りリスト。 例：.jpg、.jpeg、.png、.doc、.docx、.pdf ファイルタイプが指定されている場合、指定されていないファイルは許可されません。 初期設定では何も指定されず、すべてのファイルタイプが許可されます。

* **[!UICONTROL リッチテキストエディター]**
オンにすると、マークアップを使用して投稿を入力できます。 初期設定はオフです。

* **[!UICONTROL 投票を許可]**
オンにすると、トピックに投票機能が含まれます。 初期設定はオフです。

以下 **[!UICONTROL ユーザーモデレート]** タブで、投稿されたレビューの管理方法を指定します。 詳しくは、 [ユーザー生成コンテンツのモデレート](moderate-ugc.md).

![chlimage_1-345](assets/chlimage_1-345.png)

* **[!UICONTROL モデレート前]**
オンにすると、レビューが公開サイトに表示される前に、承認が必要になります。 初期設定はオフです。

* **[!UICONTROL レビューを削除]**
オンにすると、レビューを投稿したメンバーはレビューを削除できます。 初期設定はオフです。

* **[!UICONTROL レビューを拒否]**
オンにすると、モデレーターはレビューを拒否できます。 初期設定はオフです。

* **[!UICONTROL レビューを閉じる/再度開く]**
オンにすると、モデレーターはレビューを閉じて再度開くことができます。 初期設定はオフです。

* **[!UICONTROL レビューにフラグを設定]**
オンにすると、メンバーはレビューに「不適切」のフラグを設定できます。 初期設定はオフです。

* **[!UICONTROL フラグ設定理由リスト]**
オンにすると、メンバーはレビューを「不適切」にフラグ設定した理由をドロップダウンリストから選択できます。 初期設定はオフです。

* **[!UICONTROL カスタムフラグ設定理由]**
オンにすると、メンバーはレビューに「不適切」のフラグを設定した独自の理由を入力できます。 初期設定はオフです。

* **[!UICONTROL モデレートのしきい値]**
メンバーがレビューに何回フラグを設定したらモデレーターに通知するかを指定します。 初期設定は 1 回 (1) です。

* **[!UICONTROL フラグ付け制限]**
レビューに何回フラグを設定したら、そのレビューを公開ビューから非表示にするかを入力します。 この数は **[!UICONTROL モデレートのしきい値]**. デフォルトは 5 です。

### ページへのレビュー概要（表示）の追加 {#adding-a-review-summary-display-to-a-page}

を追加するには、以下を実行します。 `Reviews Summary (Display)` コンポーネントをオーサリングモードでページに追加する場合は、

* `Communities / Reviews Summary (Display)`

をドラッグし、アクティブなレビューまたは閉じられたレビューの概要を表示するページ上に配置します。

必要な情報については、 [コミュニティコンポーネントの基本](basics.md).

次の場合に [必要なクライアント側ライブラリ](reviews-basics.md#essentials-for-client-side) が含まれる場合、この方法で `Reviews Summary (Display)`コンポーネントが表示されます。

![chlimage_1-346](assets/chlimage_1-346.png)

>[!NOTE]
>
>「平均」は、要約するレビューの「許可された評価」タブにリストされた最初の項目の投票数を反映します。

### レビューの概要（表示）の設定 {#configuring-reviews-summary-display}

配置された `Reviews Summary (Display)` アクセスして選択するコンポーネント `Configure` 編集ダイアログを開くアイコン。

![chlimage_1-347](assets/chlimage_1-347.png)

以下 **[!UICONTROL レビューの概要]** タブ

![chlimage_1-348](assets/chlimage_1-348.png)

* `Review Path`

   配置されたインスタンスを入力するか、参照します `reviews`要約するコンポーネント ( 例えば、 [Geometrixxエンゲージサイト](getting-started.md) パスは次のようになります。

   /content/sites/engage/en/page/jcr:content/content/primary/reviews

* `Include histogram`

   オンにした場合、要約するレビューに含まれる各星評価の数を示す棒グラフの表示を含めます。 初期設定はオフです。

### カスタムレビュータイプへの変更 {#changing-to-a-custom-review-type}

レビューコンポーネントはコメントシステムを使用します。

「コメントのリソースタイプ」を変更すると、コメントシステムはデフォルトのを使用してコメントのインスタンスを生成しなくなり、開発者がカスタマイズ（拡張）したインスタンスを生成します。

カスタムリソースタイプがわかったら、次のように入力します。 [デザインモード](../../help/sites-authoring/default-components-designmode.md) そして、配置された `Comments` 追加のタブを含むダイアログを開くコンポーネント。

以下 **[!UICONTROL リソースタイプ]** タブで、新しいインスタンスのカスタム resourceType を指定します。 `Comments or Voting`コンポーネント：

![chlimage_1-349](assets/chlimage_1-349.png)

* **[!UICONTROL コメントリソースタイプ]**

   拡張の resourceType に移動します。 `comment`/apps 内のコンポーネント（単一のコメント）。 例：`/apps/social/commons/components/hbs/comments/comment`

   このリソースは、訪問者がコメントを投稿したときに作成された UGC の resourceType を識別します。

* **[!UICONTROL 投票リソースタイプ]**

   拡張の resourceType に移動します。 `voting`/apps 内のコンポーネント。 例：`/apps/social/components/hbs/voting`

   このリソースは、訪問者が投票を投稿したときに作成された UGC のリソースタイプを識別します。

* **[!UICONTROL コメントシステムリソースタイプ]**

   拡張の resourceType に移動します。 `comments`/apps 内のコンポーネント（コメントシステム）。 ページテンプレートがない場合は空白のままにします [動的に含む](scf.md#add-or-include-a-communities-component) コメントシステムをリソースとしてページに追加する代わりに、基になるスクリプト内で使用します（コメントノード）。 詳しくは、 [{{include}} ヘルパー](handlebars-helpers.md#include)

## サイト訪問者エクスペリエンス {#site-visitor-experience}

### モデレーターと管理者 {#moderators-and-administrators}

サインインしているユーザーがモデレーターまたは管理者の権限を持っている場合、レビューの作成者に関係なく、コンポーネントの設定で許可されたモデレートタスクを実行できます。

### メンバー {#members}

サイト訪問者がサインインしたとき、設定に応じて、ログイン者によっては

* 新しいレビューを投稿
* 自分のレビューを編集
* 自分のレビューを削除
* 他のユーザーのレビューコメントにフラグを設定する

メンバーごとに 1 つの評価のみが許可されます。 会員は、いつでも評価を変更することができます。

### 匿名 {#anonymous}

サインインしていないサイト訪問者は、投稿されたレビューを読み、サポートされている場合は翻訳するだけですが、評価やレビューを追加したり、他のユーザーのレビューコメントにフラグを設定したりすることはできません。

## 追加情報 {#additional-information}

詳しくは、 [レビューの基本事項](reviews-basics.md) 開発者向けのページ

投稿されたコメントのモデレートについては、 [ユーザー生成コンテンツのモデレート](moderate-ugc.md).

投稿されたコメントの翻訳については、 [ユーザー生成コンテンツの翻訳](translate-ugc.md).
