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
translation-type: tm+mt
source-git-commit: 75312539136bb53cf1db1de03fc0f9a1dca49791
workflow-type: tm+mt
source-wordcount: '729'
ht-degree: 31%

---


# メッセージングの設定 {#configuring-messaging}

## 概要 {#overview}

AEM Communities のメッセージング機能を使用すると、サインイン済みのサイト訪問者（メンバー）が互いにメッセージを送信できます。このメッセージには、サイトにサインインしているときにアクセス可能です。

コミュニティサイトのメッセージングを有効にするには、[コミュニティサイトの作成](sites-console.md)中にチェックボックスをオンにします。

このページでは、デフォルト設定と可能な調整についての情報を紹介します。

開発者向けの追加情報については、[Messaging Essentials](essentials-messaging.md)を参照してください。

## メッセージング操作サービス {#messaging-operations-service}

[AEM Communitiesメッセージング操作サービス](http://localhost:4502/system/console/configMgr/com.adobe.cq.social.messaging.client.endpoints.impl.MessagingOperationsServiceImpl)は、メッセージング関連の要求を処理するエンドポイント、サービスがメッセージの格納に使用するフォルダー、およびメッセージに添付ファイルが含まれる場合は、許可されるファイルの種類を識別します。

[Communitiesのサイトコンソール](sites-console.md)を使用して作成したコミュニティサイトでは、サービスのインスタンスが既に存在し、インボックスは`/mail/community/inbox`に設定されています。

### コミュニティのメッセージング操作サービス {#community-messaging-operations-service}

以下に示すとおり、[サイト作成ウィザード](sites-console.md)で作成されたサイトには、サービスの設定があります。設定の横にある鉛筆アイコンを選択して、設定を表示または編集できます。

![chlimage_1-63](assets/chlimage_1-63.png)

### 新しい設定 {#new-configuration}

新しい設定を追加するには、サービス名の横にあるプラス「**+**」アイコンを選択します。

![chlimage_1-64](assets/chlimage_1-64.png)

* **[!UICONTROL メッセージフィールド]**
の許可リスト構成メッセージコンポーネントユーザーが編集および保持できるプロパティを指定します。新しいフォーム要素を追加する場合は、SRPに保存する必要がある場合は、要素IDを追加する必要があります。 初期設定は2つのエントリです。 
** 主観と *内容*。

* **[!UICONTROL メッセージボックスサイズの]**
制限各ユーザーのメッセージボックスの最大バイト数。初期設定は です。 
*1073741824* (1 GB)。

* **[!UICONTROL メッセージ数の]**
制限1人のユーザーに許可されるメッセージの合計数です。値を —1に設定した場合、許可されるメッセージの数に制限はなく、メッセージボックスのサイズ制限に従います。 初期設定は です。 
*10000* (10k)

* **[!UICONTROL 配信の]**
失敗を通知するオンにすると、メッセージ配信が一部の受信者に失敗した場合に送信者に通知します。初期設定は です。 
*checked*.

* **[!UICONTROL 失敗配信の送信者]**
idName配信失敗メッセージに表示される送信者の名前。初期設定は です。 
*failureNotifier*。

* **[!UICONTROL 失敗メッセージテンプレートの]**
パス失敗した配信メッセージテンプレートのルートの絶対パス。初期設定は です。 
*/etc/notification/messaging/default*.

* **[!UICONTROL maxRetries.name]**&#x200B;配信に失敗したメッセージの再送を試行する回数です。初期設定は です。 
*3*.

* **[!UICONTROL minWaitBetweenRetries.name]**&#x200B;送信に失敗したメッセージの再送を試行するまでの間隔（秒数）です。初期設定は*100 *（秒）です。

* **[!UICONTROL カウント更新プール]**
サイズカウントの更新に使用される同時スレッドの数。初期設定は です。 
*10*.

* **[!UICONTROL inbox.path.name]**
(
*必須*)ユーザーのノードを基準とした、*フォルダーに使用するパス(/home/users/* username **`inbox`** )。パスの末尾にスラッシュ「/」を付けることはできません。 デフォルトは&#x200B;*/mail/inbox*&#x200B;です。

* **[!UICONTROL sentitems.path.name]**
(
*必須*)ユーザーのノードを基準とした、*フォルダーに使用するパス(/home/users/* username **`senditems`** )。パスの末尾にスラッシュ「/」を付けることはできません。 初期設定は&#x200B;*/mail/sentitems*&#x200B;です。

* **[!UICONTROL supportAttachments.name]**&#x200B;オンにすると、ユーザーがメッセージに添付ファイルを追加できるようになります。初期設定は です。 
*チェック済み*。

* **[!UICONTROL batchSize.name]**&#x200B;大規模な受信者グループへの送信時に一括送信処理するメッセージの数です。初期設定は です。 
*100*.

* **[!UICONTROL maxTotalAttachmentSize.name]**「supportAttachments」をオンにすると、この値によりすべての添付ファイルの最大許容合計サイズ（バイト単位）が指定されます。初期設定は です。 
*104857600* (100 MB)。

* **[!UICONTROL attachmentTypeBlocklist.]**
nameファイル拡張子のブロックリストで、先頭に「
****」というプレフィックス付き）のブラックリストです。そうでないブロックリストに加える場合は、拡張が許可されます。 拡張子は、「**+**」アイコンと「**-**」アイコンを使用して追加または削除できます。 初期設定は&#x200B;*DEFAULT*&#x200B;です。

* **[!UICONTROL allowedAttachmentTypes.name]**

   **(*操作が必要*** )ファイル拡張子の許可リスト(の逆)。これらを除くすべてのファイル拡張子を許可するには、ブロックリストに加える&#39;**-**&#39;アイコンを使用して、空のエントリを1つ削除します。

* **[!UICONTROL serviceSelector.name]**
(*必須*)サービスを呼び出す絶対パス（エンドポイント）（仮想リソース）。選択するパスのルートは、*OSGi config [ `Apache Sling Servlet/Script Resolver and Error Handler`](http://localhost:4502/system/console/configMgr/org.apache.sling.servlets.resolver.SlingServletResolver)のExecution Paths*&#x200B;構成設定（`/bin/`、`/apps/`、`/services/`など）に含まれている必要があります。 サイトのメッセージング機能に対してこの設定を選択するには、このエンドポイントを`Message List and Compose Message components`の&#x200B;**`Service selector`**&#x200B;値として指定します（[メッセージ機能](configure-messaging.md)を参照）。 初期設定は */bin/messaging* です。

* **[!UICONTROL fieldAllowlist.]**
nameUse 
**Message Fields許可リスト**。

>[!CAUTION]
>
>編集用に`Messaging Operations Service`設定が開かれるたびに、`allowedAttachmentTypes.name`が削除されると、空のエントリが再度追加され、プロパティを設定可能にします。 1つの空のエントリを指定すると、添付ファイルが有効に無効になります。
>
>これらを除くすべてのファイル拡張子を許可するには、ブロックリストに加える&#39;**-**&#39;アイコンを使用して（もう一度）空のエントリを1つ削除してから、**[!UICONTROL 保存]**&#x200B;をクリックします。

## トラブルシューティング {#troubleshooting}

問題のトラブルシューティングの1つの方法は、ログで[デバッグメッセージを有効にすることです。](../../help/sites-administering/troubleshooting.md)

[個々のサービス用のロガーとライター](../../help/sites-deploying/configure-logging.md#loggers-and-writers-for-individual-services)も参照してください。

監視するパッケージは`com.adobe.cq.social.messaging`です。
