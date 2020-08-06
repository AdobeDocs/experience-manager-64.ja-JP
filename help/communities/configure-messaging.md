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

* [管理者へのメッセージの設定](messaging.md)
* [Messaging Essentials](essentials-messaging.md) for developers

>[!NOTE]
>
>作成者編集モードでのページへの `Compose Message, Message, or Message List` コンポー `Communities`ネントの追加（コンポーネントグループに含まれる）はサポートされていません。

## メッセージングコンポーネントの設定 {#configuring-messaging-components}

コミュニティサイトでメッセージングを有効にしている場合、メッセージングは完全に設定されており、追加の設定は不要です。この情報は、デフォルトの設定を変更する必要がある場合に表示されます。

### Configuring Message List (messagebox) {#configuring-message-list-messagebox}

In order to modify the configuration of the list of messages for **Inbox**, **Sent Items**, and **Trash** pages of the messaging feature, open the site in [author edit mode](sites-console.md#authoring-site-content).

In `Preview` mode, select the **[!UICONTROL Messages]** link to open the main messaging page. Then select either **[!UICONTROL Inbox, Sent Items, or Trash]** in order to configure the component for that message list.

In `Edit` mode, select the component on the page.

In order to access the configuraiton dialog, it is necessary to cancel inheritance by selecting the `link`icon.

Once the configuration is complete, it is necessary to restore inheritance by selecting the `broken link` icon.

![chlimage_1-396](assets/chlimage_1-396.png)

Once inheritance is canceled, it will be possible to select the `configure` icon to open the configuration dialog.

![chlimage_1-397](assets/chlimage_1-397.png)

#### 「基本」タブ{#basic-tab}

![chlimage_1-398](assets/chlimage_1-398.png)

* **[!UICONTROL サービスセレクタ]**(*必須*)これは、 `serviceSelector.name` AEM Communities・メッセージング・オペレーション・サービス [](messaging.md#messaging-operations-service)のプロパティの値に設定します。

* **[!UICONTROL 構成ページ]**(*必須*)：メンバーが `Reply` ボタンをクリックしたときに開くページ。 ターゲットページには、**[!UICONTROL メッセージを作成]**&#x200B;フォームを含める必要があります。

* **[!UICONTROL リソースとして返信／表示]**&#x200B;オンにすると、返信 URL と表示 URL がリソースを参照します。オフにすると、データは URL 内でクエリパラメーターとして渡されます。

* **[!UICONTROL プロファイルの表示フォーム]**&#x200B;送信者のプロファイルの表示に使用するプロファイルフォームです。

* **[!UICONTROL ごみ箱フォルダー]**&#x200B;オンにすると、このメッセージリストコンポーネントには、「削除済み」（ごみ箱）のフラグが設定されているメッセージのみが表示されます。

* **[!UICONTROL フォルダーパス]**(*必須*): `inbox.path.name` AEM Communities・メッセージング・オペレーション・サービス `sentitems.path.name` (TM)のと [](messaging.md#messaging-operations-service)の値セットを参照します。 When configuring for an `Inbox`, add one entry using the value of `inbox.path.name`. When configuring for an `Outbox`, add one entry using the value of `sentitems.path.name`. When configuring for `Trash`, add two entries with both values.

#### 「表示」タブ{#display-tab}

![chlimage_1-399](assets/chlimage_1-399.png)

* **[!UICONTROL 既読ボタン]**（オンの場合） 
`Read`ボタンをクリックし、メッセージを既読としてマークできます。

* **[!UICONTROL 未読をマークボタン]**（オンの場合） 
`Mark Unread` ボタンをクリックし、メッセージを既読としてマークできます。

* **[!UICONTROL 削除ボタン]**：オンの場合、 
`Delete`ボタンをクリックし、メッセージを既読としてマークできます。 Will duplicate the delete functionality if **`Message Options`** is also checked.

* **[!UICONTROL メッセージオプション]**：オンの場合、 
**`Reply`**、 **`Reply All`**、 **`Forward`** および **`Delete`** メッセージを再送または削除するボタン。 Will duplicate the delete functionality if **`Delete Button`** is also checked.

* **[!UICONTROL 1 ページのメッセージ数]**&#x200B;指定した数字がページネーションスキームで 1 ページに表示されるメッセージの最大数になります。数字を指定しない（空白のまま）場合、すべてのメッセージが表示され、ページネーションはありません。

* **[!UICONTROL タイムスタンプのパターン]** 1 つ以上の言語に対してタイムスタンプのパターンを指定します。初期設定は en、de、fr、it、es、ja、zh_CN、ko_KR です。

* **[!UICONTROL 表示ユーザー]**&#x200B;選択 
**`Sender`** または[送信者]と[受信者]のどちら **`Recipients`** を表示するかを決定する場合に使用します。

### 「メッセージを作成」の設定{#configuring-compose-message}

In order to modify the configuration of the compose message page, open the site in [author edit mode](sites-console.md#authoring-site-content).

In `Preview`mode, select the **[!UICONTROL Messages]** link to open the main messaging page. Then select the New Message button to open the `Compose Message` page..

In `Edit` mode, select the main component on the page containing the Message body.

In order to access the configuraiton dialog, it is necessary to cancel inheritance by selecting the `link`icon.

Once the configuration is complete, it is necessary to restore inheritance by selecting the `broken link` icon.

![chlimage_1-400](assets/chlimage_1-400.png)

Once inheritance is canceled, it will be possible to select the `configure` icon to open the configuration dialog.

![chlimage_1-401](assets/chlimage_1-401.png)

#### 「基本」タブ{#basic-tab-1}

![chlimage_1-402](assets/chlimage_1-402.png)

* **[!UICONTROL リダイレクト URL]**&#x200B;メッセージの送信後に表示されるページの URL を入力します。例： 
`../messaging.html`。

* **[!UICONTROL キャンセル URL]**&#x200B;送信者がメッセージをキャンセルした場合に表示されるページの URL を入力します。例： 
`../messaging.html`。

* **[!UICONTROL メッセージ件名の最大の長さ]**「件名」フィールドに許可される最大文字数です。例えば、500のように指定します。 初期設定はno limitです。

* **[!UICONTROL メッセージ本文の最大の長さ]**「コンテンツ」フィールドに許可される最大文字数です。例えば、10000のように指定します。 初期設定はno limitです。

* **[!UICONTROL サービスセレクタ]**(*必須*)これは、 **`serviceSelector.name`** AEM Communities・メッセージング・オペレーション・サービス [](messaging.md#messaging-operations-service)のプロパティの値に設定します。

#### 「表示」タブ{#display-tab-1}

![chlimage_1-403](assets/chlimage_1-403.png)

* **[!UICONTROL Show Subject Field]**：オンの場合、 
`Subject` フィールドにサブジェクトを追加し、メッセージにサブタイトルを追加できます。 デフォルトはチェックされていません。

* **[!UICONTROL 件名ラベル]**: 
`Subject` field. デフォルトは `Subject` です。

* **[!UICONTROL Show Attach File Field]**&#x200B;オンの場合、 
`Attachment` フィールドに値を入力し、メッセージに添付ファイルを追加できるようにします。 デフォルトはチェックされていません。

* **[!UICONTROL [ファイルラベルを添付]**] 
`Attachment` field. デフォルトは **`Attach File`** です。

* **[!UICONTROL コンテンツフィールドを表示]**：オンの場合、 
`Content` フィールドに値を入力し、メッセージ本文の追加を有効にします。 デフォルトはチェックされていません。

* **[!UICONTROL コンテンツラベル]**: 
`Content` field. デフォルトは **`Body`** です。

* **[!UICONTROL リッチテキストエディターを使用]**&#x200B;オンにすると、独自のリッチテキストエディターを使用するカスタムのコンテンツテキストボックスを使用することを意味します。デフォルトはチェックされていません。

* **[!UICONTROL タイムスタンプのパターン]** 1 つ以上の言語に対してタイムスタンプのパターンを指定します。初期設定は en、de、fr、it、es、ja、zh_CN、ko_KR です。

