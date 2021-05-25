---
title: メッセージング機能
seo-title: メッセージング機能
description: メッセージングコンポーネントの設定
seo-description: メッセージングコンポーネントの設定
uuid: 29ab63b6-67a1-4eb8-8cf8-c1ff52ff2bac
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.4/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 88ee8573-58c4-42cd-8e36-2ea4a0d654e4
exl-id: e03cf05c-2469-4883-ae7b-9d7e6660b71f
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '940'
ht-degree: 33%

---

# メッセージング機能 {#messaging-feature}

フォーラムやコメントで公に表示されるインタラクションに加えて、AEM Communitiesのメッセージング機能を使用すると、コミュニティメンバーは互いに非公開でやり取りできます。

この機能は、[コミュニティサイト](overview.md#communitiessites)を作成するときに組み込むことができます。

メッセージング機能では、以下を実行できます。

* 1人以上のコミュニティメンバーにメッセージを送信する
* コミュニティメンバーグループにメッセージを送信する
* 添付ファイル付きのメッセージの送信
* メッセージを転送する
* メッセージに返信
* メッセージの削除
* 削除されたメッセージの復元

メッセージング機能を有効化して変更するには、以下を参照してください。

* [管理者向](messaging.md) けメッセージの設定
* [開発者向け](essentials-messaging.md) のメッセージ

>[!NOTE]
>
>`Compose Message, Message, or Message List`コンポーネント（`Communities`コンポーネントグループ内）を作成者編集モードでページに追加することはサポートされていません。

## メッセージングコンポーネントの設定 {#configuring-messaging-components}

コミュニティサイトでメッセージングを有効にしている場合、メッセージングは完全に設定されており、追加の設定は不要です。この情報は、デフォルトの設定を変更する必要がある場合に提供されます。

### メッセージリスト(messagebox)の設定{#configuring-message-list-messagebox}

メッセージ機能の&#x200B;**インボックス**、**送信済みアイテム**、**ごみ箱**&#x200B;ページのメッセージリストの設定を変更するには、[作成者編集モード](sites-console.md#authoring-site-content)でサイトを開きます。

`Preview`モードで、**[!UICONTROL メッセージ]**&#x200B;リンクを選択して、メインメッセージページを開きます。 次に、「**[!UICONTROL インボックス」、「送信済みアイテム」または「ごみ箱]**」を選択して、そのメッセージリストのコンポーネントを設定します。

`Edit`モードで、ページ上のコンポーネントを選択します。

設定ダイアログにアクセスするには、`link`アイコンを選択して継承をキャンセルする必要があります。

設定が完了したら、`broken link`アイコンを選択して継承を復元する必要があります。

![chlimage_1-396](assets/chlimage_1-396.png)

継承がキャンセルされると、`configure`アイコンを選択して設定ダイアログを開くことができます。

![chlimage_1-397](assets/chlimage_1-397.png)

#### 「基本」タブ{#basic-tab}

![chlimage_1-398](assets/chlimage_1-398.png)

* **[!UICONTROL サービスセレクター]**
(*必須*)これを `serviceSelector.name` AEM Communities Messaging Operations Service [](messaging.md#messaging-operations-service)のプロパティの値に設定します。

* **[!UICONTROL ページを構成]**
(*必須*)メンバーがボタンをクリックしたときに開くペ `Reply` ージ。ターゲットページには、**[!UICONTROL メッセージを作成]**&#x200B;フォームを含める必要があります。

* **[!UICONTROL リソースとして返信／表示]**&#x200B;オンにすると、返信 URL と表示 URL がリソースを参照します。オフにすると、データは URL 内でクエリパラメーターとして渡されます。

* **[!UICONTROL プロファイルの表示フォーム]**&#x200B;送信者のプロファイルの表示に使用するプロファイルフォームです。

* **[!UICONTROL ごみ箱フォルダー]**&#x200B;オンにすると、このメッセージリストコンポーネントには、「削除済み」（ごみ箱）のフラグが設定されているメッセージのみが表示されます。

* **[!UICONTROL フォルダーパス]**
(*必須*) `inbox.path.name` AEM Communities Messaging Operations Serviceの `sentitems.path.name` とに設定された値を参照しま [す](messaging.md#messaging-operations-service)。`Inbox`に対して設定する場合、`inbox.path.name`の値を使用して1つのエントリを追加します。 `Outbox`に対して設定する場合、`sentitems.path.name`の値を使用して1つのエントリを追加します。 `Trash`に対して設定する場合、両方の値を持つ2つのエントリを追加します。

#### 「表示」タブ{#display-tab}

![chlimage_1-399](assets/chlimage_1-399.png)

* **[!UICONTROL 既読をマー]**
クボタンオンにすると、 
`Read`ボタンを使用して、メッセージを既読としてマークできます。

* **[!UICONTROL 未読をマー]**
クボタンオンにすると、 
`Mark Unread` ボタンを使用して、メッセージを既読としてマークできます。

* **[!UICONTROL 削除ボ]**
タンオンにすると、「 
`Delete`ボタンを使用して、メッセージを既読としてマークできます。**`Message Options`**&#x200B;もオンにすると、削除機能が複製されます。

* **[!UICONTROL メッセージ]**
オプションオンにすると、が表示されます 
**`Reply`**、 、 **`Reply All`**&#x200B;および **`Forward`** メ **`Delete`** ッセージを再送信または削除できるボタン。**`Delete Button`**&#x200B;もオンにすると、削除機能が複製されます。

* **[!UICONTROL 1 ページのメッセージ数]**&#x200B;指定した数字がページネーションスキームで 1 ページに表示されるメッセージの最大数になります。数字を指定しない（空白のまま）場合、すべてのメッセージが表示され、ページネーションはありません。

* **[!UICONTROL タイムスタンプのパターン]** 1 つ以上の言語に対してタイムスタンプのパターンを指定します。初期設定は en、de、fr、it、es、ja、zh_CN、ko_KR です。

* **[!UICONTROL Display]**
UserChoose 
**`Sender`** または **`Recipients`** を使用して、送信者と受信者のどちらを表示するかを決定します。

### 「メッセージを作成」の設定{#configuring-compose-message}

メッセージを作成ページの設定を変更するには、[オーサー編集モード](sites-console.md#authoring-site-content)でサイトを開きます。

`Preview`モードで、**[!UICONTROL メッセージ]**&#x200B;リンクを選択して、メインメッセージページを開きます。 次に、「新しいメッセージ」ボタンを選択して`Compose Message`ページを開きます。

`Edit`モードで、メッセージ本文を含むページ上のメインコンポーネントを選択します。

設定ダイアログにアクセスするには、`link`アイコンを選択して継承をキャンセルする必要があります。

設定が完了したら、`broken link`アイコンを選択して継承を復元する必要があります。

![chlimage_1-400](assets/chlimage_1-400.png)

継承がキャンセルされると、`configure`アイコンを選択して設定ダイアログを開くことができます。

![chlimage_1-401](assets/chlimage_1-401.png)

#### 「基本」タブ{#basic-tab-1}

![chlimage_1-402](assets/chlimage_1-402.png)

* **[!UICONTROL リダイレクト URL]**&#x200B;メッセージの送信後に表示されるページの URL を入力します。例： 
`../messaging.html`

* **[!UICONTROL キャンセル URL]**&#x200B;送信者がメッセージをキャンセルした場合に表示されるページの URL を入力します。例： 
`../messaging.html`.

* **[!UICONTROL メッセージ件名の最大の長さ]**「件名」フィールドに許可される最大文字数です。例：500 初期設定は無制限です。

* **[!UICONTROL メッセージ本文の最大の長さ]**「コンテンツ」フィールドに許可される最大文字数です。例：10000 初期設定は無制限です。

* **[!UICONTROL サービスセレクター]**
(*必須*)これを **`serviceSelector.name`** AEM Communities Messaging Operations Service [](messaging.md#messaging-operations-service)のプロパティの値に設定します。

#### 「表示」タブ{#display-tab-1}

![chlimage_1-403](assets/chlimage_1-403.png)

* **[!UICONTROL Show Subject]**
Fieldオンにすると、 
`Subject` フィールドに入力し、メッセージに件名を追加できるようにします。初期設定はオンになっていません。

* **[!UICONTROL 件名ラ]**
ベル 
`Subject` field. デフォルトは `Subject` です。

* **[!UICONTROL ファイルの添付フ]**
ィールドを表示オンにすると、 
`Attachment` 」フィールドに値を入力し、メッセージに添付ファイルを追加する機能を有効にします。初期設定はオンになっていません。

* **[!UICONTROL ファイルのラ]**
ベルを添付する横に表示するテキストを入力します 
`Attachment` フィールド。デフォルトは **`Attach File`** です。

* **[!UICONTROL コンテンツフ]**
ィールドを表示オンにすると、 
`Content` フィールドに値を入力し、メッセージ本文の追加を有効にします。初期設定はオンになっていません。

* **[!UICONTROL コンテ]**
ンツラベル 
`Content` フィールド。デフォルトは **`Body`** です。

* **[!UICONTROL リッチテキストエディターを使用]**&#x200B;オンにすると、独自のリッチテキストエディターを使用するカスタムのコンテンツテキストボックスを使用することを意味します。初期設定はオンになっていません。

* **[!UICONTROL タイムスタンプのパターン]** 1 つ以上の言語に対してタイムスタンプのパターンを指定します。初期設定は en、de、fr、it、es、ja、zh_CN、ko_KR です。
