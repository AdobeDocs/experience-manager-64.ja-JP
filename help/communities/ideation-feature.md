---
title: アイディエーション機能
seo-title: アイディエーション機能
description: アイディエーション機能の追加と設定
seo-description: アイディエーション機能の追加と設定
uuid: b21507da-10c8-4149-9e2c-a4ff5dec582b
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.4/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 7c0a9120-2edb-431b-b460-68398832d5ec
translation-type: tm+mt
source-git-commit: 5ddbcb2addff2d6e3a3e9d7e100a6d9ba89fdd60

---


# アイディエーション機能 {#ideation-feature}

## 概要 {#introduction}

アイディエーション機能は、パブリッシュ環境にサインインしているサイト訪問者（コミュニティメンバー）が以下を実行できる領域を提供します。

* コミュニティで共有するアイデアを作成する
* アイデアの表示とコメント
* アイデアに従う
* アイデアに対する投票

ドキュメントのこのセクションでは、以下の内容について説明します。

* AEMサイトへのID機能の追加
* Ideationコンポーネントの設定

## ページへのアイディエーションの追加 {#adding-a-ideation-to-a-page}

作成者モードで `Ideation` ページにコンポーネントを追加するには、コンポーネントブラウザーを使用してアイデアを表示するペ `Communities / Ideation` ージ上の位置にコンポーネントを配置し、ドラッグします。

For necessary information, visit [Communities Components Basics](basics.md).

When the [required client-side libraries](ideation.md#essentials-for-client-side) are included, this is how the `Ideation`component will appear:

![chlimage_1-29](assets/chlimage_1-29.png)

## アイディエーションの設定 {#configuring-an-ideation}

Select the placed `Ideation` component to access and select the `Configure` icon which opens the edit dialog.

![chlimage_1-30](assets/chlimage_1-30.png)![chlimage_1-31](assets/chlimage_1-31.png)

### 「設定」タブ{#settings-tab}

「**[!UICONTROL 設定]**」タブでは、アイデアとコメントの基本機能を設定します。

* **[!UICONTROL アイディエーションのタイトル]**&#x200B;アイデアの表示タイトルです。デフォルトは `Ideation` です。

* **[!UICONTROL アイディエーション説明]**&#x200B;アイデアのサブタイトルとして表示される説明です。初期設定では、説明はありません。

* **[!UICONTROL 1 ページのトピック数]** 1 ページに表示するアイデア数または投稿数を定義します。初期設定は 10 です。

* **[!UICONTROL モデレート]**&#x200B;オンにすると、アイデアおよびコメントの投稿を公開サイトに表示する前に承認が必要になります。初期設定はオフです。

* **[!UICONTROL 閉じる]**&#x200B;オンにすると、アイディエーションフォーラムは新しいアイデアやコメントを受け付けなくなります。初期設定はオフです。

* **[!UICONTROL リッチテキストエディター]**&#x200B;オンにすると、マークアップを使用してアイデアおよびコメントを入力できます。初期設定はオフです。

* **[!UICONTROL タグ付けを許可]**&#x200B;オンにすると、メンバーは自分の投稿にタグラベルを付加できます（「**[!UICONTROL タグフィールド]**」タブを参照）。初期設定はオフです。

* **[!UICONTROL ファイルのアップロードを許可]**&#x200B;オンにすると、アイデアまたはコメントに添付ファイルを付加できます。初期設定はオフです。

* **[!UICONTROL 「Max File Size]** Relevant only if `Allow File Uploads` is」をオンにした場合。 このフィールドは、アップロードするファイルのサイズ（バイト単位）を制限します。 初期設定は104857600(10 Mb)です。

* **[!UICONTROL 「Allowed File Types]** Relevant only if `Allow File Uploads` 」がオンの場合。 ドット付きのファイル拡張子をコンマ区切りで指定します（例：.jpg, .jpeg, .png, .doc, .docx, .pdf）。ファイルタイプを指定した場合、指定しなかったファイルはアップロードできません。 初期設定はnoneで、すべてのファイルタイプが許可されます。

* **[!UICONTROL 「ファイルのアップロードを許可」がオン]**&#x200B;になっている場合にのみ、「添付画像ファイルの最大サイズ」が関連します。 アップロードされた画像ファイルの最大バイト数。 初期設定は2097152(2 Mb)です。

* **[!UICONTROL 応答を許可]**&#x200B;オンにすると、アイデアに投稿されたコメントに返信できます。初期設定はオフです。

* **[!UICONTROL ユーザーによるコメントおよびトピックの削除を許可]**&#x200B;オンにすると、メンバーは自分が投稿したコメントおよびアイデアを削除できます。初期設定はオフです。

* **[!UICONTROL フォローを許可]**&#x200B;オンにすると、アイデアの投稿のフォロー機能が含まれます。これにより、メンバーは新しい投稿の[通知を受け取る](notifications.md)ことができます。初期設定はオフです。

* **[!UICONTROL 電子メール購読を許可]**&#x200B;オンにすると、新しい投稿があった場合にメンバーに電子メールで通知できるようになります（[購読](subscriptions.md)）。Requires `Allow Following` to be checked and [email configured](email.md). 初期設定はオフです。

* **[!UICONTROL 投票を許可]**&#x200B;オンにすると、アイデアのコメントに投票できます。初期設定はオフです。

* **[!UICONTROL バッジを表示]**&#x200B;オンにすると、メンバーのアイデアに割り当て済みおよび獲得済みの[バッジ](implementing-scoring.md)が表示されます。初期設定はオフです。

* **[!UICONTROL おすすめコンテンツを許可]**&#x200B;オンにすると、アイデアを[おすすめコンテンツ](featured.md)として指定できます。初期設定はオフです。

### 「ユーザーモデレート」タブ {#user-moderation-tab}

Under the **[!UICONTROL User Moderation]** tab, specify how the posted ideas and comments (user generated content) are managed. For more information, see [Moderating User Generated Content](moderate-ugc.md).

* **[!UICONTROL 投稿を拒否]**&#x200B;オンにすると、信頼されているメンバーモデレーターが投稿を拒否して、公開フォーラムへの表示を止めることができます。初期設定はオフです。

* **[!UICONTROL トピックを閉じる／再度開く]**&#x200B;オンにすると、信頼されているメンバーモデレーターが、トピックをそれ以上編集およびコメントできないように閉じたり、再度開いたりすることができます。初期設定はオフです。

* **[!UICONTROL 投稿にフラグを設定]**&#x200B;オンにすると、メンバーは他のメンバーのトピックまたはコメントに「不適切」のフラグを設定できます。初期設定はオフです。

* **[!UICONTROL フラグ設定理由リスト]**&#x200B;オンにすると、メンバーはトピックまたはコメントに「不適切」のフラグを設定した理由をドロップダウンリストから選択できます。初期設定はオフです。

* **[!UICONTROL カスタムフラグ設定理由]**&#x200B;オンにすると、メンバーはトピックまたはコメントに「不適切」のフラグを設定した独自の理由を入力できます。初期設定はオフです。

* **[!UICONTROL モデレートのしきい値]**&#x200B;メンバーがトピックまたはコメントに何回フラグを設定したらモデレーターに通知するかを指定します。初期設定は1（1回）です。

* **[!UICONTROL フラグ付けの制限]**&#x200B;トピックまたはコメントに何回フラグが設定されたら、公開表示から非表示にするかを指定します。-1に設定した場合、フラグ付けされたトピックまたはコメントは公開ビューで非表示になりません。 そうでない場合、この数値はモデレートのしきい値以上にする必要があります。 初期設定は 5 です。

### 「タグフィールド」タブ{#tag-field-tab}

「**[!UICONTROL タグフィールド]**」タブでは、「**[!UICONTROL 設定]**」タブでタグ付けが許可されている場合に、適用できるタグを名前空間に従って制限します。

* **[!UICONTROL 「設定」タブで]**「Namespaces `Allow Tagging` Relevant」がオ **ンになっている場合は** 許可されます。 適用できるタグは、チェックされた名前空間カテゴリ内のタグに制限されます。 名前空間のリストには、「Standard Tags」（デフォルトの名前空間）と「Include All Tags」が含まれます。 初期設定はnoneで、すべての名前空間が許可されます。

* **[!UICONTROL 推奨の制限]**&#x200B;フォーラムに投稿するメンバーに表示する推奨タグの数を入力します。A value of **-** 1 means no limit. 初期設定は 0 です。

### 「並べ替え設定」タブ{#sort-settings-tab}

Under the **[!UICONTROL Sort Settings]** tab, specify how the posted comments are sorted when displayed.

* **[!UICONTROL Sort By]** Check all allowed sort selections: `Newest, Oldest, Last Updated, Most Viewed, Most Active, Most Followed and Most Liked`. デフォルトは `Newest, Oldest, Last Updated` です。

* **[!UICONTROL デフォルトとして設定]**&#x200B;プルダウンして、オンになっている並べ替えオプションのいずれかを選択し、デフォルトとして表示されるようにします。デフォルトは `Newest` です。

* **[!UICONTROL 「Analyticsの並べ替えの時間オプション」のプ]**&#x200B;ルダウンを選択して、いずれかを選択しま `All, Last 24 Hours, Last 7 Days, Last 30 Days`す。 デフォルトは `All` です。

## サイト訪問者のエクスペリエンス {#site-visitor-experience}

### アイデアの作成 {#creating-idea}

Communities のすべての機能と同様に、サインインしていない場合、サイト訪問者はアイデアを読むことと、他のユーザーの（コメントや投票／「いいね!」を通じた）意見を見ることしかできません。

メンバーはサインインすると、新しいアイデアを作成できます。

![chlimage_1-32](assets/chlimage_1-32.png)

アイデアを送信する前に、ドラフトとして保存できます。

ボタンを選択す `Save as Draft` ると、ドラフトが保存されます。

![chlimage_1-33](assets/chlimage_1-33.png)

保存したドラフトをタブで表 `My Drafts` 示する場合は、編 `Read More` 集モードに戻す場合に選択します。

![chlimage_1-34](assets/chlimage_1-34.png)

#### フィードバックの提供 {#providing-feedback}

Once the idea is published, other members can sign in, open the idea ( `Read More`) and like the idea, thus adding to the vote count, and make comments.

![chlimage_1-35](assets/chlimage_1-35.png)

### 追加情報 {#additional-information}

開発者向けの詳細情報は、[アイディエーションの基本事項](ideation.md)ページを参照してください。

投稿されたトピックとコメントのモデレートについては、[ユーザー生成コンテンツのモデレート](moderate-ugc.md)を参照してください。

投稿されたトピックとコメントのタグ付けについては、[ユーザー生成コンテンツのタグ付け](tag-ugc.md)を参照してください。
