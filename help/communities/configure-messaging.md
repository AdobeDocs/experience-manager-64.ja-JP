---
title: メッセージング機能
seo-title: Messaging Feature
description: メッセージングコンポーネントの設定
seo-description: Configuring Messaging components
uuid: 29ab63b6-67a1-4eb8-8cf8-c1ff52ff2bac
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.4/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 88ee8573-58c4-42cd-8e36-2ea4a0d654e4
exl-id: e03cf05c-2469-4883-ae7b-9d7e6660b71f
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '935'
ht-degree: 3%

---

# メッセージング機能 {#messaging-feature}

フォーラムやコメントで公開されるインタラクションに加えて、AEM Communitiesのメッセージ機能を使用すると、コミュニティメンバーは互いに非公開でやり取りできます。

この機能は、 [コミュニティサイト](overview.md#communitiessites) が作成されました。

メッセージ機能を使用すると、次のことができます。

* 1 人以上のコミュニティメンバーにメッセージを送信する
* コミュニティメンバーグループにメッセージを送信する
* 添付ファイル付きのメッセージを送信
* メッセージを転送
* メッセージに返信
* メッセージの削除
* 削除したメッセージを復元

メッセージング機能を有効にして変更するには、次にアクセスします。

* [メッセージの設定](messaging.md) 管理者向け
* [メッセージの基本事項](essentials-messaging.md) 開発者向け

>[!NOTE]
>
>追加はサポートされていません `Compose Message, Message, or Message List` コンポーネント ( `Communities`コンポーネントグループ ) をオーサリング編集モードでページに追加する必要があります。

## メッセージングコンポーネントの設定 {#configuring-messaging-components}

コミュニティサイトでメッセージを有効にすると、設定が不要で完全に設定されます。 この情報は、デフォルトの設定を変更する必要がある場合に提供されます。

### メッセージリストの設定 (messagebox) {#configuring-message-list-messagebox}

次のメッセージのリストの設定を変更するには： **インボックス**, **送信済みアイテム**、および **ごみ箱** メッセージング機能のページで、 [オーサー編集モード](sites-console.md#authoring-site-content).

In `Preview` モード、 **[!UICONTROL メッセージ]** メインメッセージページを開くためのリンク 次に、 **[!UICONTROL インボックス、送信済みアイテムまたはごみ箱]** を設定して、そのメッセージリストのコンポーネントを設定します。

In `Edit` モード」で、ページ上のコンポーネントを選択します。

設定ダイアログにアクセスするには、継承をキャンセルするために、 `link`アイコン

設定が完了したら、 `broken link` アイコン

![chlimage_1-396](assets/chlimage_1-396.png)

継承がキャンセルされると、 `configure` アイコンをクリックして、設定ダイアログを開きます。

![chlimage_1-397](assets/chlimage_1-397.png)

#### 「基本」タブ {#basic-tab}

![chlimage_1-398](assets/chlimage_1-398.png)

* **[!UICONTROL サービスセレクター]**
(*必須*) これをプロパティの値に設定します。 `serviceSelector.name` から [AEM Communities Messaging Operations Service](messaging.md#messaging-operations-service).

* **[!UICONTROL ページを作成]**
(*必須*) メンバーが `Reply` 」ボタンをクリックします。 ターゲットページには、 **[!UICONTROL メッセージを作成]** フォーム。

* **[!UICONTROL 返信/リソースとして表示]**
オンにすると、返信 URL と表示 URL でリソースが参照されます。オンにしない場合、データは URL でクエリパラメーターとして渡されます。

* **[!UICONTROL プロファイル表示フォーム]**
送信者のプロファイルの表示に使用するプロファイルフォームです。

* **[!UICONTROL ごみ箱フォルダ]**
オンにすると、このメッセージリストコンポーネントには、削除済み（ごみ箱）としてフラグ付けされたメッセージのみが表示されます。

* **[!UICONTROL フォルダーパス]**
(*必須*) `inbox.path.name` および `sentitems.path.name` 内 [AEM Communities Messaging Operations Service](messaging.md#messaging-operations-service). を `Inbox`、値を使用して 1 つのエントリを追加 `inbox.path.name`. を `Outbox`、値を使用して 1 つのエントリを追加 `sentitems.path.name`. を設定する際 `Trash`、両方の値を持つ 2 つのエントリを追加します。

#### 「表示」タブ {#display-tab}

![chlimage_1-399](assets/chlimage_1-399.png)

* **[!UICONTROL 既読をマークボタン]**
オンにすると、 
`Read`ボタンを使用して、メッセージを既読としてマークすることができます。

* **[!UICONTROL 未読のマークボタン]**
オンにすると、 
`Mark Unread` ボタンを使用して、メッセージを既読としてマークすることができます。

* **[!UICONTROL 削除ボタン]**
オンにすると、 
`Delete`ボタンを使用して、メッセージを既読としてマークすることができます。 次の場合に削除機能が複製されます： **`Message Options`** がオンになっている。

* **[!UICONTROL メッセージオプション]**
オンにすると、が表示されます 
**`Reply`**, **`Reply All`**, **`Forward`** および **`Delete`** ボタンを使用して、メッセージを再送信または削除できます。 次の場合に削除機能が複製されます： **`Delete Button`** がオンになっている。

* **[!UICONTROL 1 ページのメッセージ数]**
指定した数は、ページネーションスキームで 1 ページに表示されるメッセージの最大数です。 数を指定しない場合（空白のまま）、すべてのメッセージが表示され、ページ番号は設定されません。

* **[!UICONTROL タイムスタンプのパターン]**
1 つ以上の言語のタイムスタンプパターンを指定します。 デフォルトは en, de, fr, it, es, ja, zh_CN, ko_KR です。

* **[!UICONTROL ユーザーを表示]**
次のいずれかを選択 
**`Sender`** または **`Recipients`** をクリックして、「送信者」と「受信者」のどちらを表示するかを決定します。

### メッセージを作成の設定 {#configuring-compose-message}

メッセージを作成ページの設定を変更するには、 [オーサー編集モード](sites-console.md#authoring-site-content).

In `Preview`モード、 **[!UICONTROL メッセージ]** メインメッセージページを開くためのリンク 次に、「新しいメッセージ」ボタンを選択して、 `Compose Message` ページ…

In `Edit` モード：メッセージ本文を含むページ上のメインコンポーネントを選択します。

設定ダイアログにアクセスするには、継承をキャンセルするために、 `link`アイコン

設定が完了したら、 `broken link` アイコン

![chlimage_1-400](assets/chlimage_1-400.png)

継承がキャンセルされると、 `configure` アイコンをクリックして、設定ダイアログを開きます。

![chlimage_1-401](assets/chlimage_1-401.png)

#### 「基本」タブ {#basic-tab-1}

![chlimage_1-402](assets/chlimage_1-402.png)

* **[!UICONTROL リダイレクト URL]**
メッセージの送信後に表示されるページの URL を入力します。 例： 
`../messaging.html`

* **[!UICONTROL キャンセル URL]**
送信者がメッセージをキャンセルした場合に表示されるページの URL を入力します。 例： 
`../messaging.html`

* **[!UICONTROL メッセージ件名の最大長]**
「件名」フィールドに入力できる最大文字数。 例：500 初期設定は無制限です。

* **[!UICONTROL メッセージ本文の最大長]**
「コンテンツ」フィールドに入力できる最大文字数です。 例：10000。 初期設定は無制限です。

* **[!UICONTROL サービスセレクター]**
(*必須*) これをプロパティの値に設定します。 **`serviceSelector.name`** から [AEM Communities Messaging Operations Service](messaging.md#messaging-operations-service).

#### 「表示」タブ {#display-tab-1}

![chlimage_1-403](assets/chlimage_1-403.png)

* **[!UICONTROL 件名フィールドを表示]**
オンにすると、 
`Subject` フィールドに入力し、メッセージへの件名の追加を有効にします。 初期設定はオンになっていません。

* **[!UICONTROL 件名ラベル]**
横に表示するテキストを入力 
`Subject` field. デフォルトは `Subject` です。

* **[!UICONTROL ファイルの添付フィールドを表示]**
オンにすると、 
`Attachment` フィールドに値を入力し、メッセージへの添付ファイルの追加を有効にします。 初期設定はオンになっていません。

* **[!UICONTROL ファイルラベルを添付]**
横に表示するテキストを入力 
`Attachment` field. デフォルトは **`Attach File`** です。

* **[!UICONTROL コンテンツフィールドを表示]**
オンにすると、 
`Content` フィールドに値を入力し、メッセージ本文の追加を有効にします。 初期設定はオンになっていません。

* **[!UICONTROL コンテンツラベル]**
横に表示するテキストを入力 
`Content` field. デフォルトは **`Body`** です。

* **[!UICONTROL リッチテキストエディターを使用]**
オンにすると、独自のリッチテキストエディターでカスタムの「コンテンツ」テキストボックスが使用されることを示します。 初期設定はオンになっていません。

* **[!UICONTROL タイムスタンプのパターン]**
1 つ以上の言語のタイムスタンプパターンを指定します。 デフォルトは en, de, fr, it, es, ja, zh_CN, ko_KR です。
