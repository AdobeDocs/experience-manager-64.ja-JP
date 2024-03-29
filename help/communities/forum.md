---
title: フォーラム機能
seo-title: Forum Feature
description: フォーラム機能の追加方法と設定方法
seo-description: How to add and configure the forum feature
uuid: ced860ef-6f8a-4df2-acc8-6a48140fca83
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.4/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 3495f983-d71e-4704-be4e-8a42a63f72db
exl-id: fa6f28b4-3217-4b6a-b223-506da0ecca9e
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '1082'
ht-degree: 2%

---

# フォーラム機能 {#forum-feature}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

## はじめに {#introduction}

フォーラム機能は、パブリッシュ環境でサインインしているサイト訪問者（コミュニティメンバー）が以下を実行できる領域を提供します。

* 新規トピックを作成
* トピックを表示して返信
* トピックのフォロー
* フォーラムの検索
* フォーラムコンテンツのモデレートに役立ちます
* フォーラムトピックを別のページに移動する

ドキュメントのこの節では、

* AEMサイトへのフォーラム機能の追加
* の設定 `Forum`コンポーネント

## フォーラムをページに追加する {#adding-a-forum-to-a-page}

を追加するには、以下を実行します。 `Forum` コンポーネントをオーサリングモードでページに追加する場合は、コンポーネントブラウザーを使用して

* `Communities / Forum`

フォーラムが表示されるページ上の場所にドラッグします。

必要な情報については、 [コミュニティコンポーネントの基本](basics.md).

次の場合に [必要なクライアント側ライブラリ](essentials-forum.md#essentials-for-client-side) が含まれる場合、この方法で `Forum`コンポーネントが表示されます。

![chlimage_1-60](assets/chlimage_1-60.png)

## フォーラムの設定 {#configuring-a-forum}

配置された `Forum` アクセスして選択するコンポーネント `Configure` 編集ダイアログを開くアイコン。

![chlimage_1-61](assets/chlimage_1-61.png) ![chlimage_1-62](assets/chlimage_1-62.png)

### 「設定」タブ {#settings-tab}

以下 **[!UICONTROL 設定]** タブで、トピックと返信の設定を指定します。

* **[!UICONTROL 1 ページのトピック数]**
1 ページに表示されるトピック/投稿の数を定義します。 初期設定は 10 です。

* **[!UICONTROL モデレート]**
オンにすると、トピックおよびコメントの投稿を発行サイトに表示する前に承認が必要になります。 初期設定はオフです。

* **[!UICONTROL クローズ]**
オンにすると、フォーラムは新しいトピックおよびコメントを受け付けなくなります。 初期設定はオフです。

* **[!UICONTROL リッチテキストエディター]**
オンにすると、マークアップを使用してトピックとコメントを入力できます。 初期設定はオフです。

* **[!UICONTROL タグ付けを許可]**
オンにすると、メンバーは投稿にタグラベルを追加できます ( **[!UICONTROL タグフィールド]** 」タブ ) をクリックします。 初期設定はオフです。

* **[!UICONTROL ファイルのアップロードを許可]**
オンにすると、トピックまたはコメントに添付ファイルを追加できます。 初期設定はオフです。

* **[!UICONTROL フォローを許可]**
オンにすると、フォーラム投稿に次の機能が含まれ、メンバーは [通知済み](notifications.md) 新しい投稿の数。 初期設定はオフです。

* **[!UICONTROL ピン留めを許可]**
オンにすると、フォーラムトピックがトピックのリストの先頭にピン留めされる場合があります。 初期設定はオフです。

* **[!UICONTROL おすすめコンテンツを許可]**
オンにすると、アイデアを [おすすめコンテンツ](featured.md). 初期設定はオフです。

* **[!UICONTROL メール購読を許可]**
オンにすると、新しい投稿をメールでメンバーに通知することを許可します ([購読](subscriptions.md)) をクリックします。 必要 `Allow Following` チェックされ [電子メール設定済み](email.md). 初期設定はオフです。

* **[!UICONTROL 最大ファイルサイズ]**
次の場合にのみ関連します。 
`Allow File Uploads` がオンになっている。 このフィールドは、アップロードするファイルのサイズ（バイト単位）を制限します。 初期設定は104857600(10 MB) です。

* **[!UICONTROL 許可されているファイルタイプ]**
次の場合にのみ関連します。 
`Allow File Uploads` がオンになっている。 「ドット」区切り文字を使用したファイル拡張子のコンマ区切りリスト。 例：.jpg、.jpeg、.png、.doc、.docx、.pdf ファイルタイプが指定されている場合、指定されていないファイルのアップロードは許可されません。 初期設定では何も指定されず、すべてのファイルタイプが許可されます。

* **[!UICONTROL 添付する画像ファイルの最大サイズ]**
「ファイルのアップロードを許可」がオンの場合にのみ関連します。 アップロードされた画像ファイルの最大バイト数。 初期設定は2097152 (2 MB) です。

* **[!UICONTROL スレッド化された返信を許可]**
オンにすると、トピックに投稿されたコメントに対する返信を許可します。 初期設定はオフです。

* **[!UICONTROL ユーザーによるコメントおよびトピックの削除を許可]**
オンにすると、メンバーは自分が投稿したコメントやトピックを削除できます。 初期設定はオフです。

* **[!UICONTROL 投票を許可]**
オンにした場合、トピックに投票機能を含めます。 初期設定はオフです。

* **[!UICONTROL パンくずリストを表示]**
オンにすると、トピックページにナビゲーション用パンくずリストが表示されます。 初期設定はオンです。

* **[!UICONTROL バッジを表示]**
オンにすると、獲得および割り当て済みを表示します [バッジ](implementing-scoring.md) メンバーのブログエントリを含む 初期設定はオフです。

>[!NOTE]
>
>場合によっては、 `AllowThreaded Replies` および `Allow users to Delete Comments and Topics` トピックに対するコメントを有効にします。

### 「ユーザーモデレート」タブ {#user-moderation-tab}

以下 **[!UICONTROL ユーザーモデレート]** タブで、投稿されたトピックと返信（ユーザー生成コンテンツ）の管理方法を指定します。 詳しくは、 [ユーザー生成コンテンツのモデレート](moderate-ugc.md).

* **[!UICONTROL 投稿を拒否]**
オンにすると、信頼できるメンバーのモデレーターは、投稿を拒否し、公開フォーラムに投稿が表示されなくなります。 初期設定はオフです。

* **[!UICONTROL トピックを閉じる/再度開く]**
オンにすると、信頼されているメンバーモデレーターは、トピックを閉じてさらに編集やコメントを行ったり、トピックを再度開いたりできます。 初期設定はオフです。

* **[!UICONTROL トピックを移動]**
オンにすると、発行側のモデレーターがトピックを移動できます。 初期設定はオンです。

* **[!UICONTROL 投稿にフラグを設定]**
オンにすると、メンバーは他のユーザーのトピックまたはコメントに「不適切」のフラグを設定できます。 初期設定はオフです。

* **[!UICONTROL フラグ設定理由リスト]**
オンにすると、メンバーはトピックまたはコメントに「不適切」のフラグを設定した理由をドロップダウンリストから選択できます。 初期設定はオフです。

* **[!UICONTROL カスタムフラグ設定理由]**
オンにすると、メンバーはトピックまたはコメントに「不適切」のフラグを設定した独自の理由を入力できます。 初期設定はオフです。

* **[!UICONTROL モデレートのしきい値]**
メンバーがトピックまたはコメントに何回フラグを設定したらモデレーターに通知するかを指定します。 初期設定は 1 （1 回）です。

* **[!UICONTROL フラグ付け制限]**
トピックまたはコメントに何回フラグを設定したら、公開ビューで非表示にするかを指定します。 -1 に設定した場合、フラグ付きのトピックまたはコメントが公開ビューで非表示になることはありません。 それ以外の場合は、この数はモデレートのしきい値以上にする必要があります。 デフォルトは 5 です。

### 「タグフィールド」タブ {#tag-field-tab}

以下 **[!UICONTROL タグフィールド]** 」タブに追加します。タグが適用される場合は、 **[!UICONTROL 設定]** タブは、選択した名前空間に応じて制限されます。

* **[!UICONTROL 許可された名前空間]**
次の場合に関連 `Allow Tagging` が **[!UICONTROL 設定]** タブをクリックします。 適用できるタグは、チェックされた名前空間カテゴリ内のタグに限定されます。 名前空間のリストには、「標準タグ」（デフォルトの名前空間）と「すべてのタグを含める」が含まれます。 初期設定はオフです。これは、すべての名前空間が許可されていることを意味します。

* **[!UICONTROL 提案の制限]**
フォーラムに投稿するメンバーに提案として表示するタグの数を入力します。 初期設定は です。 
**-** 1（制限なし）。

### 「翻訳」タブ {#translation-tab}

以下 **[!UICONTROL 翻訳]** タブの「翻訳」がコミュニティサイトで有効になっている場合、トピック全体または選択した投稿を翻訳するように翻訳を設定できます。

* **[!UICONTROL すべて翻訳]**
オンにすると、フォーラムスレッドはユーザーの優先言語に翻訳されます。 初期設定はオフです。

### 「並べ替え設定」タブ {#sort-settings-tab}

以下 **[!UICONTROL 並べ替え設定]** タブで、投稿されたコメントを表示する際の並べ替え方法を指定します。

* **[!UICONTROL 並べ替え基準]**
許可されている並べ替えの選択項目をすべてオンにします。 
`Newest, Oldest, Last Updated, Most Viewed, Most Active, Most Followed and Most Liked`。デフォルトは `Newest, Oldest, Last Updated` です。

* **[!UICONTROL デフォルトとして設定]**
プルダウンして、オンにした並べ替えオプションの 1 つを選択し、デフォルトとして表示します。 初期設定は です。 
`Newest`。

* **[!UICONTROL Analytics 並べ替えの時間オプションの選択]**
プルダウンして次のいずれかを選択 
`All, Last 24 Hours, Last 7 Days, Last 30 Days`。デフォルトは `All` です。

## 追加情報 {#additional-information}

詳しくは、 [フォーラムの基本事項](essentials-forum.md) 開発者向けのページ

投稿されたトピックおよびコメントのモデレートについては、 [ユーザー生成コンテンツのモデレート](moderate-ugc.md).

投稿されたトピックおよびコメントのタグ付けについては、 [ユーザー生成コンテンツのタグ付け](tag-ugc.md).

投稿されたトピックおよびコメントの翻訳については、 [ユーザー生成コンテンツの翻訳](translate-ugc.md).
