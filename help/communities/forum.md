---
title: フォーラム機能
seo-title: フォーラム機能
description: フォーラム機能を追加および設定する方法
seo-description: フォーラム機能を追加および設定する方法
uuid: ced860ef-6f8a-4df2-acc8-6a48140fca83
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.4/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 3495f983-d71e-4704-be4e-8a42a63f72db
translation-type: tm+mt
source-git-commit: 28948f1f8678512f8fc970a4289cb01cde86c5c2
workflow-type: tm+mt
source-wordcount: '1056'
ht-degree: 66%

---


# フォーラム機能 {#forum-feature}

## 概要 {#introduction}

フォーラム機能は、パブリッシュ環境にサインインしているサイト訪問者（コミュニティメンバー）が以下を実行できる領域を提供します。

* 新しいトピックの作成
* 表示とトピックへの返信
* トピックをフォロー
* フォーラムの検索
* フォーラムのコンテンツのモデレートの支援
* フォーラムトピックをページ間で移動する

ドキュメントのこのセクションでは、以下の内容について説明します。

* AEMサイトへのフォーラム機能の追加
* Configuration settings for the `Forum`component

## フォーラムをページに追加 {#adding-a-forum-to-a-page}

To add a `Forum` component to a page in author mode, use the component browser to locate

* `Communities / Forum`

フォーラムが表示されるページにドラッグします。

For necessary information, visit [Communities Components Basics](basics.md).

[必要なクライアント側ライブラリが含まれる場合](essentials-forum.md#essentials-for-client-side) 、次のように `Forum`コンポーネントが表示されます。

![chlimage_1-60](assets/chlimage_1-60.png)

## フォーラムの設定 {#configuring-a-forum}

Select the placed `Forum` component to access and select the `Configure` icon which opens the edit dialog.

![chlimage_1-61](assets/chlimage_1-61.png) ![chlimage_1-62](assets/chlimage_1-62.png)

### 「設定」タブ{#settings-tab}

「**[!UICONTROL 設定]**」タブでは、トピックと返信の基本機能を設定します。

* **[!UICONTROL 1 ページのトピック数]** 1 ページに表示するトピック数または投稿数を定義します。初期設定は 10 です。

* **[!UICONTROL モデレート]**&#x200B;オンにすると、トピックおよびコメントの投稿を公開サイトに表示する前に承認が必要になります。初期設定はオフです。

* **[!UICONTROL 閉じる]**&#x200B;オンにすると、フォーラムは新しいトピックやコメントを受け付けなくなります。初期設定はオフです。

* **[!UICONTROL リッチテキストエディター]**&#x200B;オンにすると、マークアップを使用してトピックおよびコメントを入力できます。初期設定はオフです。

* **[!UICONTROL タグ付けを許可]**&#x200B;オンにすると、メンバーは自分の投稿にタグラベルを付加できます（「**[!UICONTROL タグフィールド]**」タブを参照）。初期設定はオフです。

* **[!UICONTROL ファイルのアップロードを許可]**&#x200B;オンにすると、トピックまたはコメントに添付ファイルを付加できます。初期設定はオフです。

* **[!UICONTROL フォローを許可]**&#x200B;オンにすると、フォーラム投稿のフォロー機能が追加され、新しい投稿をメンバーに[通知](notifications.md)できます。初期設定はオフです。

* **[!UICONTROL ピン留めを許可]**&#x200B;オンにすると、フォーラムトピックをトピックリストの上部にピン留めできます。初期設定はオフです。

* **[!UICONTROL おすすめコンテンツを許可]**&#x200B;オンにすると、アイデアを[おすすめコンテンツ](featured.md)として指定できます。初期設定はオフです。

* **[!UICONTROL 電子メール購読を許可]**&#x200B;オンにすると、新しい投稿があった場合にメンバーに電子メールで通知できるようになります（[購読](subscriptions.md)）。Requires `Allow Following` to be checked and [email configured](email.md). 初期設定はオフです。

* **[!UICONTROL 最大ファイルサイズ]**&#x200B;関連( 
`Allow File Uploads` がチェックされている。 このフィールドは、アップロードされるファイルのサイズ（バイト単位）を制限します。 初期設定は104857600(10 Mb)です。

* **[!UICONTROL 許可されているファイルタイプ]**&#x200B;は、 
`Allow File Uploads` がチェックされている。 ドット付きのファイル拡張子をコンマ区切りで指定します（例：.jpg, .jpeg, .png, .doc, .docx, .pdf）。ファイルの種類が指定されている場合、指定されていないファイルはアップロードできません。 初期設定は、すべてのファイルタイプを許可するように指定されません。

* **[!UICONTROL 「ファイルのアップロードを許可」が選択されている場合のみ、「添付画像ファイルの最大サイズ]**」が関連します。 アップロードされた画像ファイルの最大バイト数。 初期設定は2097152(2 Mb)です。

* **[!UICONTROL スレッド化された返信を許可]**&#x200B;オンにすると、トピックに投稿されたコメントへの返信を許可します。初期設定はオフです。

* **[!UICONTROL ユーザーによるコメントおよびトピックの削除を許可]**&#x200B;オンにすると、メンバーは自分が投稿したコメントおよびトピックを削除できます。初期設定はオフです。

* **[!UICONTROL 投票を許可]**&#x200B;オンにすると、トピックに投票機能が組み込まれます。初期設定はオフです。

* **[!UICONTROL パンくずリストを表示]**&#x200B;オンにすると、トピックページにナビゲーション用のパンくずリストが表示されます。初期設定はオンです。

* **[!UICONTROL バッジを表示]**&#x200B;オンにすると、獲得した[バッジ](implementing-scoring.md)と割り当てられたバッジがメンバーのブログエントリに表示されます。初期設定はオフです。

>[!NOTE]
>
>トピックに対するコメントを有効にする場合は、お `AllowThreaded Replies` よび両方 `Allow users to Delete Comments and Topics` を確認する必要があります。

### 「ユーザーモデレート」タブ{#user-moderation-tab}

Under the **[!UICONTROL User Moderation]** tab, specify how the posted topics and replies (user generated content) are managed. For more information, see [Moderating User Generated Content](moderate-ugc.md).

* **[!UICONTROL 投稿を拒否]**&#x200B;オンにすると、信頼されているメンバーモデレーターが投稿を拒否して、公開フォーラムへの表示を止めることができます。初期設定はオフです。

* **[!UICONTROL トピックを閉じる／再度開く]**&#x200B;オンにすると、信頼されているメンバーモデレーターが、トピックをそれ以上編集およびコメントできないように閉じたり、再度開いたりすることができます。初期設定はオフです。

* **[!UICONTROL トピックを移動]**&#x200B;オンにすると、公開側のモデレーターはトピックを移動できます。 初期設定はオンです。

* **[!UICONTROL 投稿にフラグを設定]**&#x200B;オンにすると、メンバーは他のメンバーのトピックまたはコメントに「不適切」のフラグを設定できます。初期設定はオフです。

* **[!UICONTROL フラグ設定理由リスト]**&#x200B;オンにすると、メンバーはトピックまたはコメントに「不適切」のフラグを設定した理由をドロップダウンリストから選択できます。初期設定はオフです。

* **[!UICONTROL カスタムフラグ設定理由]**&#x200B;オンにすると、メンバーはトピックまたはコメントに「不適切」のフラグを設定した独自の理由を入力できます。初期設定はオフです。

* **[!UICONTROL モデレートのしきい値]**&#x200B;メンバーがトピックまたはコメントに何回フラグを設定したらモデレーターに通知するかを指定します。初期設定は1（1回）です。

* **[!UICONTROL フラグ付けの制限]**&#x200B;トピックまたはコメントに何回フラグが設定されたら、公開表示から非表示にするかを指定します。-1に設定した場合、フラグ付けされたトピックまたはコメントはパブリック表示に表示されません。 それ以外の場合は、この数値をモデレートしきい値以上にする必要があります。 初期設定は 5 です。

### 「タグフィールド」タブ{#tag-field-tab}

「**[!UICONTROL タグフィールド]**」タブでは、「**[!UICONTROL 設定]**」タブでタグ付けが許可されている場合に、適用できるタグを名前空間に従って制限します。

* **[!UICONTROL 「]**&#x200B;設定 `Allow Tagging` 」タブで「関連」が選択さ **[!UICONTROL れている場合は、「許可された名前空間]** 」。 適用できるタグは、チェック対象の名前空間カテゴリ内のタグに限定されます。 名前空間のリストには、「標準タグ」(デフォルトの名前空間)と「すべてのタグを含む」があります。 初期設定はオフで、すべての名前空間が許可されます。

* **[!UICONTROL 推奨の制限]**&#x200B;フォーラムに投稿するメンバーに表示する推奨タグの数を入力します。初期設定は です。 
**-** 1（制限なし）。

### 「翻訳」タブ{#translation-tab}

「**[!UICONTROL 翻訳]**」タブでは、コミュニティサイトの翻訳が有効になっている場合に、選択された投稿だけでなくトピック全体を翻訳するかどうかを設定できます。

* **[!UICONTROL すべてを翻訳]**&#x200B;オンにすると、フォーラムスレッドはユーザーの選択した言語に翻訳されます。初期設定はオフです。

### 「並べ替え設定」タブ{#sort-settings-tab}

Under the **[!UICONTROL Sort Settings]** tab, specify how the posted comments are sorted when displayed.

* **[!UICONTROL 並べ替えの基準]**：許可されている並べ替えの選択項目をすべて選択します。 
`Newest, Oldest, Last Updated, Most Viewed, Most Active, Most Followed and Most Liked`」を選択します。デフォルトは `Newest, Oldest, Last Updated` です。

* **[!UICONTROL デフォルトとして設定]**&#x200B;プルダウンして、オンになっている並べ替えオプションのいずれかを選択し、デフォルトとして表示されるようにします。初期設定は です。 
`Newest`。

* **[!UICONTROL Analytics Sortingのプルダウンの「Time Options」を選択し]**&#x200B;て、 
`All, Last 24 Hours, Last 7 Days, Last 30 Days`」を選択します。デフォルトは `All` です。

## 追加情報 {#additional-information}

詳しくは、開発者向けの[フォーラムの基本事項](essentials-forum.md)ページを参照してください。

投稿されたトピックとコメントのモデレートについては、[ユーザー生成コンテンツのモデレート](moderate-ugc.md)を参照してください。

投稿されたトピックとコメントのタグ付けについては、[ユーザー生成コンテンツのタグ付け](tag-ugc.md)を参照してください。

投稿されたトピックとコメントの翻訳については、[ユーザー生成コンテンツの翻訳](translate-ugc.md)を参照してください。
