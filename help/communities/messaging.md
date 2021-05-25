---
title: メッセージングの設定
seo-title: メッセージングの設定
description: Communities のメッセージング
seo-description: Communities のメッセージング
uuid: 35d98667-a82e-4ed1-b6a1-1ffbbe1d08b5
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.4/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 5cb571ae-eeb5-4943-a6b8-92e346e85be2
role: Administrator
exl-id: 0e906f67-b908-4c41-b243-e4f90100ce5d
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '728'
ht-degree: 31%

---

# メッセージングの設定  {#configuring-messaging}

## 概要 {#overview}

AEM Communities のメッセージング機能を使用すると、サインイン済みのサイト訪問者（メンバー）が互いにメッセージを送信できます。このメッセージには、サイトにサインインしているときにアクセス可能です。

コミュニティサイトのメッセージングを有効にするには、[コミュニティサイトの作成](sites-console.md)中にチェックボックスをオンにします。

このページでは、デフォルト設定と可能な調整についての情報を紹介します。

開発者向けの追加情報については、[メッセージングの基本事項](essentials-messaging.md)を参照してください。

## メッセージング操作サービス {#messaging-operations-service}

[AEM Communities Messaging Operations Service](http://localhost:4502/system/console/configMgr/com.adobe.cq.social.messaging.client.endpoints.impl.MessagingOperationsServiceImpl)は、メッセージ関連の要求を処理するエンドポイント、メッセージの保存に使用するフォルダー、メッセージに添付ファイルが含まれる場合は許可されるファイルタイプを識別します。

[コミュニティサイトコンソール](sites-console.md)を使用して作成されたコミュニティサイトの場合、インボックスが`/mail/community/inbox`に設定された状態で、サービスのインスタンスが既に存在します。

### コミュニティのメッセージング操作サービス {#community-messaging-operations-service}

以下に示すとおり、[サイト作成ウィザード](sites-console.md)で作成されたサイトには、サービスの設定があります。設定の横にある鉛筆アイコンを選択すると、設定を表示または編集できます。

![chlimage_1-63](assets/chlimage_1-63.png)

### 新しい設定 {#new-configuration}

新しい設定を追加するには、サービス名の横にあるプラス「**+**」アイコンを選択します。

![chlimage_1-64](assets/chlimage_1-64.png)

* **[!UICONTROL メッセージフィ]**
ールド許可リストユーザーが編集および保持できるメッセージを作成コンポーネントのプロパティを指定します。新しいフォーム要素を追加する場合、SRPに格納するには、要素IDを追加する必要があります。 デフォルトは2つのエントリです。 
** 件名とコ *ンテンツ*

* **[!UICONTROL メッセージボ]**
ックスサイズの制限各ユーザーのメッセージボックスの最大バイト数です。初期設定は です。 
*1073741824* (1 GB)。

* **[!UICONTROL メッセージ]**
数の制限：ユーザーごとに許可されるメッセージの合計数です。値を —1に設定した場合、許可されるメッセージ数は無制限で、メッセージボックスのサイズ制限に従います。 初期設定は です。 
*10,000* (10k)

* **[!UICONTROL 配信の失敗を通]**
知オンにすると、メッセージの配信が一部の受信者に失敗した場合に送信者に通知します。初期設定は です。 
*checked*.

* **[!UICONTROL 配信失敗メッセージに表示される送信者のidName。]**
初期設定は です。 
*failureNotifier*&#x200B;を参照してください。

* **[!UICONTROL 失敗メッセージテンプ]**
レートのpathFailedメッセージテンプレートのルートへの絶対パス。初期設定は です。 
*/etc/notification/messaging/default*&#x200B;を設定します。

* **[!UICONTROL maxRetries.name]**&#x200B;配信に失敗したメッセージの再送を試行する回数です。初期設定は です。 
*3*.

* **[!UICONTROL minWaitBetweenRetries.name]**&#x200B;送信に失敗したメッセージの再送を試行するまでの間隔（秒数）です。初期設定は「*100 *（秒）」です。

* **[!UICONTROL カウント更新プー]**
ルのサイズ更新に使用する同時スレッドの数。初期設定は です。 
*10*.

* **[!UICONTROL inbox.path.name]**
(
*必須*)フォルダーに使用するユーザーのノード(/home/users/*username*)を基準としたパス **`inbox`** 。パスの末尾にフォワードスラッシュ「/」を付けることはできません。 初期設定は&#x200B;*/mail/inbox*&#x200B;です。

* **[!UICONTROL sentitems.path.name]**
(
*必須*)フォルダーに使用するユーザーのノード(/home/users/*username*)を基準としたパス **`senditems`** 。パスの末尾にフォワードスラッシュ「/」を付けることはできません。 初期設定は&#x200B;*/mail/sentitems*&#x200B;です。

* **[!UICONTROL supportAttachments.name]**&#x200B;オンにすると、ユーザーがメッセージに添付ファイルを追加できるようになります。初期設定は です。 
**&#x200B;をオンにします。

* **[!UICONTROL batchSize.name]**&#x200B;大規模な受信者グループへの送信時に一括送信処理するメッセージの数です。初期設定は です。 
*100*.

* **[!UICONTROL maxTotalAttachmentSize.name]**「supportAttachments」をオンにすると、この値によりすべての添付ファイルの最大許容合計サイズ（バイト単位）が指定されます。初期設定は です。 
*104857600* (100 MB)。

* **[!UICONTROL attachmentTypeBlocklist.nameフ]**
ァイブロックリストル拡張子の。先頭に「
****」というプレフィックス付き）のブラックリストです。選択しなブロックリストに加えるい場合、拡張機能は許可されます。 拡張は、「**+**」および「**-**」アイコンを使用して追加または削除できます。 初期設定は&#x200B;*DEFAULT*&#x200B;です。

* **[!UICONTROL allowedAttachmentTypes.name]**

   **(*アクションが必要*)** ファイル拡張子許可リストの(拡張子の逆ブロックリスト)。すべてのファイル拡張子（されたものを除く）を許可するにブロックリストに加えるは、「**-**」アイコンを使用して、1つの空のエントリを削除します。

* **[!UICONTROL serviceSelector.name]**
(*必須*)サービスが呼び出される絶対パス（エンドポイント）です（仮想リソース）。選択するパスのルートは、*OSGi設定[ `Apache Sling Servlet/Script Resolver and Error Handler`](http://localhost:4502/system/console/configMgr/org.apache.sling.servlets.resolver.SlingServletResolver)の設定（`/bin/`、`/apps/`、`/services/`など）に含まれているパスである必要があります。*&#x200B;サイトのメッセージング機能に対してこの設定を選択するには、このエンドポイントを`Message List and Compose Message components`の&#x200B;**`Service selector`**&#x200B;値として提供します（[メッセージ機能](configure-messaging.md)を参照）。 初期設定は */bin/messaging* です。

* **[!UICONTROL fieldAllowlist.]**
nameUse 
**メッセージフィールドの許可リスト**&#x200B;を参照してください。

>[!CAUTION]
>
>`Messaging Operations Service`設定を編集用に開くたびに、`allowedAttachmentTypes.name`が削除された場合は、空のエントリが再追加され、プロパティを設定できるようになります。 1つの空のエントリを指定すると、添付ファイルが無効になります。
>
>すべてのファイル拡張子（されたものを除く）を許可するにブロックリストに加えるは、「**-**」アイコンを使用して（再び）空のエントリを1つ削除してから、「**[!UICONTROL 保存]**」をクリックします。

## トラブルシューティング {#troubleshooting}

問題をトラブルシューティングする1つの方法は、ログで[メッセージのデバッグを有効にすることです。](../../help/sites-administering/troubleshooting.md)

[個々のサービス用のロガーとライター](../../help/sites-deploying/configure-logging.md#loggers-and-writers-for-individual-services)も参照してください。

監視するパッケージは`com.adobe.cq.social.messaging`です。
