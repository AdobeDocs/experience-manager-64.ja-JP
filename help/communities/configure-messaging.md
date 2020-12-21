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
translation-type: tm+mt
source-git-commit: 8c66f2b0053882bd1c998d8e01dbb0573881bc87
workflow-type: tm+mt
source-wordcount: '940'
ht-degree: 33%

---


# メッセージング機能 {#messaging-feature}

AEM Communitiesのメッセージ機能は、フォーラムやコメントで公開されるインタラクションに加え、コミュニティメンバー同士がもう一度プライベートに交流できるようにします。

この機能は、[コミュニティサイト](overview.md#communitiessites)を作成するときに組み込むことができます。

メッセージング機能では、以下を実行できます。

* 1人以上のコミュニティメンバーにメッセージを送信する
* コミュニティメンバーグループにメッセージを送信する
* 添付ファイル付きメッセージの送信
* メッセージの転送
* メッセージへの返信
* メッセージの削除
* 削除したメッセージの復元

メッセージング機能を有効化して変更するには、以下を参照してください。

* [管理者向け](messaging.md) メッセージの設定
* [開発者へのメッセージ](essentials-messaging.md) の基本

>[!NOTE]
>
>`Compose Message, Message, or Message List`コンポーネント（`Communities`コンポーネントグループにあります）をページに追加する場合は、作成者編集モードではサポートされません。

## メッセージングコンポーネントの設定 {#configuring-messaging-components}

コミュニティサイトでメッセージングを有効にしている場合、メッセージングは完全に設定されており、追加の設定は不要です。この情報は、デフォルトの設定を変更する必要がある場合に表示されます。

### メッセージリストの設定（メッセージボックス） {#configuring-message-list-messagebox}

メッセージング機能の&#x200B;**インボックス**、**送信済みアイテム**、**ごみ箱**&#x200B;ページのメッセージリストの設定を変更するには、[作成者編集モード](sites-console.md#authoring-site-content)でサイトを開きます。

`Preview`モードで、**[!UICONTROL メッセージ]**&#x200B;リンクを選択して、メインメッセージングページを開きます。 次に、**[!UICONTROL 「インボックス」、「送信済みアイテム」、または「ごみ箱]**」を選択して、そのメッセージリストのコンポーネントを設定します。

`Edit`モードで、ページ上のコンポーネントを選択します。

設定ダイアログにアクセスするには、`link`アイコンを選択して継承をキャンセルする必要があります。

設定が完了したら、`broken link`アイコンを選択して継承を復元する必要があります。

![chlimage_1-396](assets/chlimage_1-396.png)

継承がキャンセルされると、`configure`アイコンを選択して設定ダイアログを開くことができます。

![chlimage_1-397](assets/chlimage_1-397.png)

#### 「基本」タブ{#basic-tab}

![chlimage_1-398](assets/chlimage_1-398.png)

* **[!UICONTROL サービスセレクタ]**
(*必須*)これは、 `serviceSelector.name` AEM Communities・メッセージング・オペレーション・サービス [のプロパティの値に設定します](messaging.md#messaging-operations-service)。

* **[!UICONTROL 構成ページ]**
(*必須*)：メンバーが `Reply` ボタンをクリックしたときに開くページ。ターゲットページには、**[!UICONTROL メッセージを作成]**&#x200B;フォームを含める必要があります。

* **[!UICONTROL リソースとして返信／表示]**&#x200B;オンにすると、返信 URL と表示 URL がリソースを参照します。オフにすると、データは URL 内でクエリパラメーターとして渡されます。

* **[!UICONTROL プロファイルの表示フォーム]**&#x200B;送信者のプロファイルの表示に使用するプロファイルフォームです。

* **[!UICONTROL ごみ箱フォルダー]**&#x200B;オンにすると、このメッセージリストコンポーネントには、「削除済み」（ごみ箱）のフラグが設定されているメッセージのみが表示されます。

* **[!UICONTROL Folder Paths]**
(*必須*): `inbox.path.name` AEM Communities・メッセージング・オペレーション・サービス `sentitems.path.name` と [の値セットを参照します](messaging.md#messaging-operations-service)。`Inbox`の設定時に、`inbox.path.name`の値を使用して1つのエントリを追加します。 `Outbox`の設定時に、`sentitems.path.name`の値を使用して1つのエントリを追加します。 `Trash`の設定時に、両方の値を持つ2つのエントリを追加します。

#### 「表示」タブ{#display-tab}

![chlimage_1-399](assets/chlimage_1-399.png)

* **[!UICONTROL 既読の]**
ボタンをマークオンにすると、 
`Read`ボタンをクリックし、メッセージを既読としてマークできます。

* **[!UICONTROL 未読をマーク]**
ボタンオンの場合、 
`Mark Unread` ボタンをクリックし、メッセージを既読としてマークできます。

* **[!UICONTROL 削除]**
ボタンオンにすると、 
`Delete`ボタンをクリックし、メッセージを既読としてマークできます。**`Message Options`**&#x200B;もチェックされている場合は、削除機能を重複します。

* **[!UICONTROL メッセージ]**
オプションオンの場合、 
**`Reply`**、 **`Reply All`**、 **`Forward`** および **`Delete`** メッセージを再送または削除するボタン。**`Delete Button`**&#x200B;もチェックされている場合は、削除機能を重複します。

* **[!UICONTROL 1 ページのメッセージ数]**&#x200B;指定した数字がページネーションスキームで 1 ページに表示されるメッセージの最大数になります。数字を指定しない（空白のまま）場合、すべてのメッセージが表示され、ページネーションはありません。

* **[!UICONTROL タイムスタンプのパターン]** 1 つ以上の言語に対してタイムスタンプのパターンを指定します。初期設定は en、de、fr、it、es、ja、zh_CN、ko_KR です。

* **[!UICONTROL 表示]**
ユーザー選択 
**`Sender`** または送信者と受信者 **`Recipients`** のどちらを表示するかを決定する場合に使用します。

### 「メッセージを作成」の設定{#configuring-compose-message}

構成メッセージページの設定を変更するには、[作成者編集モード](sites-console.md#authoring-site-content)でサイトを開きます。

`Preview`モードで、「**[!UICONTROL メッセージ]**」リンクを選択して、メインメッセージングページを開きます。 次に、「新しいメッセージ」ボタンを選択して`Compose Message`ページを開きます。

`Edit`モードで、メッセージの本文を含むページのメインコンポーネントを選択します。

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

* **[!UICONTROL メッセージ件名の最大の長さ]**「件名」フィールドに許可される最大文字数です。例えば、500のように指定します。 初期設定はno limitです。

* **[!UICONTROL メッセージ本文の最大の長さ]**「コンテンツ」フィールドに許可される最大文字数です。例えば、10000のように指定します。 初期設定はno limitです。

* **[!UICONTROL サービスセレクタ]**
(*必須*)これは、 **`serviceSelector.name`** AEM Communities・メッセージング・オペレーション・サービス [のプロパティの値に設定します](messaging.md#messaging-operations-service)。

#### 「表示」タブ{#display-tab-1}

![chlimage_1-403](assets/chlimage_1-403.png)

* **[!UICONTROL Show Subject]**
Fieldオンの場合、 
`Subject` フィールドにサブジェクトを追加し、メッセージにサブタイトルを追加できます。デフォルトはチェックされていません。

* **[!UICONTROL 件名]**
ラベル 
`Subject` field. デフォルトは `Subject` です。

* **[!UICONTROL Show Attach File]**
Fieldオンの場合、 
`Attachment` フィールドに値を入力し、メッセージに添付ファイルを追加できるようにします。デフォルトはチェックされていません。

* **[!UICONTROL ファイルの]**
ラベルを添付横に表示するテキストを入力します。 
`Attachment` フィールド。デフォルトは **`Attach File`** です。

* **[!UICONTROL コンテンツ]**
フィールドを表示オンにすると、 
`Content` フィールドに値を入力し、メッセージ本文の追加を有効にします。デフォルトはチェックされていません。

* **[!UICONTROL コンテンツ]**
ラベル 
`Content` フィールド。デフォルトは **`Body`** です。

* **[!UICONTROL リッチテキストエディターを使用]**&#x200B;オンにすると、独自のリッチテキストエディターを使用するカスタムのコンテンツテキストボックスを使用することを意味します。デフォルトはチェックされていません。

* **[!UICONTROL タイムスタンプのパターン]** 1 つ以上の言語に対してタイムスタンプのパターンを指定します。初期設定は en、de、fr、it、es、ja、zh_CN、ko_KR です。

