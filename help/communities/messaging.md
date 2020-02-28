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
translation-type: tm+mt
source-git-commit: 13d890d08a032fe4eef1dac793dcf2a3e682a52c

---


# メッセージングの設定 {#configuring-messaging}

## 概要 {#overview}

AEM Communities のメッセージング機能を使用すると、サインイン済みのサイト訪問者（メンバー）が互いにメッセージを送信できます。このメッセージには、サイトにサインインしているときにアクセス可能です。

コミュニティサイトのメッセージングを有効にするには、[コミュニティサイトの作成](sites-console.md)中にチェックボックスをオンにします。

このページでは、デフォルト設定と可能な調整についての情報を紹介します。

For additional information for developers, see [Messaging Essentials](essentials-messaging.md).

## メッセージング操作サービス {#messaging-operations-service}

[](http://localhost:4502/system/console/configMgr/com.adobe.cq.social.messaging.client.endpoints.impl.MessagingOperationsServiceImpl) AEM Communities Messaging Operations Serviceは、メッセージ関連の要求を処理するエンドポイント、サービスがメッセージの保存に使用するフォルダー、およびメッセージに添付ファイルが含まれる場合に許可されるファイルの種類を識別します。

For community sites created using the [Communities Sites console](sites-console.md), an instance of the service already exists, with the inbox set to `/mail/community/inbox`.

### コミュニティのメッセージング操作サービス {#community-messaging-operations-service}

以下に示すとおり、[サイト作成ウィザード](sites-console.md)で作成されたサイトには、サービスの設定があります。設定の横にある鉛筆アイコンを選択して、設定を表示または編集できます。

![chlimage_1-63](assets/chlimage_1-63.png)

### 新しい設定 {#new-configuration}

To add a new configuration, select the plus &#39;**+**&#39; icon next to the service&#39;s name:

![chlimage_1-64](assets/chlimage_1-64.png)

* **[!UICONTROL Message Fields Whitelist]**&#x200B;ユーザーが編集および保持できる、メッセージを作成コンポーネントのプロパティを指定します。新しいフォーム要素を追加する場合、SRPに保存する必要がある場合は、要素IDを追加する必要があります。 Default is two entries: *subject* and *content*.

* **[!UICONTROL Message box size limit]**&#x200B;各ユーザーのメッセージボックスの最大バイト数。 Default is *1073741824* (1 GB).

* **[!UICONTROL Message count limit]**：ユーザーごとに許可されるメッセージの合計数です。 値を —1に設定した場合、許可されるメッセージの数に制限はなく、メッセージボックスのサイズ制限に従います。 Default is *10000* (10k).

* **[!UICONTROL 配信失敗を通知する]**：オンにすると、メッセージ配信が一部の受信者に失敗した場合に送信者に通知します。 初期設定は&#x200B;*オン*&#x200B;です。

* **[!UICONTROL 配信失敗メッセージに表]**&#x200B;示される送信者の名前。 Default is *failureNotifier*.

* **[!UICONTROL 失敗メッセージテンプレート]**&#x200B;パス配信に失敗したメッセージテンプレートルートの絶対パス。 Default is */etc/notification/messaging/default*.

* **[!UICONTROL maxRetries.name]**&#x200B;配信に失敗したメッセージの再送を試行する回数です。デフォルトは *3* です。

* **[!UICONTROL minWaitBetweenRetries.name]**&#x200B;送信に失敗したメッセージの再送を試行するまでの間隔（秒数）です。初期設定は*100 *（秒）です。

* **[!UICONTROL カウント更新プールサイズ]**&#x200B;カウント更新に使用される同時スレッドの数。 デフォルトは *10* です。

* **[!UICONTROL inbox.path.name]**(必須&#x200B;*)フォルダーに使用する、ユーザーのノード(/home/users/* username *)からの相対パス***`inbox`** 。 パスの末尾にスラッシュ「/」を付けることはできません。 Default is */mail/inbox* .

* **[!UICONTROL sentitems.path.name]**(必須&#x200B;*)フォルダーに使用する、ユーザーのノードに対する相対パス(/home/users/* username *)***`senditems`** 。 パスの末尾にスラッシュ「/」を付けることはできません。 Default is */mail/sentitems* .

* **[!UICONTROL supportAttachments.name]**&#x200B;オンにすると、ユーザーがメッセージに添付ファイルを追加できるようになります。初期設定は&#x200B;*オン*&#x200B;です。

* **[!UICONTROL batchSize.name]**&#x200B;大規模な受信者グループへの送信時に一括送信処理するメッセージの数です。デフォルトは *100* です。

* **[!UICONTROL maxTotalAttachmentSize.name]**「supportAttachments」をオンにすると、この値によりすべての添付ファイルの最大許容合計サイズ（バイト単位）が指定されます。Default is *104857600* (100 MB).

* **[!UICONTROL attachmentTypeBlacklist.name]**&#x200B;システムにより拒否されるファイル拡張子（「**.**」というプレフィックス付き）のブラックリストです。ブラックリストに記載されていない場合は、拡張が許可されます。 Extensions may be added or removed using the &#39;**+**&#39; and &#39;**-**&#39; icons. Default is *DEFAULT*.

* **[!UICONTROL allowedAttachmentTypes.name]**
   **(アク&#x200B;*ションが必要*)** ファイル拡張子のホワイトリスト（ブラックリストの逆）。 すべてのファイル拡張子（ブラックリストに入っているものを除く）を許可するには、「**-**」アイコンを使用して 1 つの空のエントリを削除します。

* **[!UICONTROL serviceSelector.name]**(必須&#x200B;**)サービスが呼び出される絶対パス（エンドポイント）（仮想リソース）。 The root of the path chosen must be one included in the *Execution Paths* configuration setting of OSGi config [ `Apache Sling Servlet/Script Resolver and Error Handler`](http://localhost:4502/system/console/configMgr/org.apache.sling.servlets.resolver.SlingServletResolver), such as `/bin/`, `/apps/`, and `/services/`. サイトのメッセージング機能に対してこの設定を選択するには、このエンドポイントをの値とし **`Service selector`** て指定します( `Message List and Compose Message components` 「メッセージ [機能](configure-messaging.md)」を参照)。 初期設定は */bin/messaging* です。

* **[!UICONTROL fieldWhitelist.name]****Message Fields Whitelist** を使用します。

>[!CAUTION]
>
>Each time a `Messaging Operations Service` configuration is opened for edit, if `allowedAttachmentTypes.name` had been removed, an empty entry is re-added to make the property configurable. 1つの空のエントリを指定すると、添付ファイルが事実上無効になります。
>
>すべての拡張子（ブラックリストに含まれるものを除く）を許可するには、「**-**」アイコンを使用してこの空エントリを（再び）削除してから「**[!UICONTROL Save]**」をクリックします。

## トラブルシューティング {#troubleshooting}

One way to troubleshoot problems is to enable [debugging messages in the log.](../../help/sites-administering/troubleshooting.md)

[個々のサービス用のロガーとライター](../../help/sites-deploying/configure-logging.md#loggers-and-writers-for-individual-services)も参照してください。

The package to monitor is `com.adobe.cq.social.messaging`.
