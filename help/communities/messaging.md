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
source-git-commit: 09f8adac1d5fc4edeca03d6955faddf5ea045405
workflow-type: tm+mt
source-wordcount: '725'
ht-degree: 29%

---


# メッセージングの設定 {#configuring-messaging}

## 概要 {#overview}

AEM Communities のメッセージング機能を使用すると、サインイン済みのサイト訪問者（メンバー）が互いにメッセージを送信できます。このメッセージには、サイトにサインインしているときにアクセス可能です。

コミュニティサイトのメッセージングを有効にするには、[コミュニティサイトの作成](sites-console.md)中にチェックボックスをオンにします。

このページでは、デフォルト設定と可能な調整についての情報を紹介します。

For additional information for developers, see [Messaging Essentials](essentials-messaging.md).

## メッセージング操作サービス {#messaging-operations-service}

The [AEM Communities Messaging Operations Service](http://localhost:4502/system/console/configMgr/com.adobe.cq.social.messaging.client.endpoints.impl.MessagingOperationsServiceImpl) identifies the endpoint which handles messaging related requests, the folders the service should use for storing messages, and if messages may include file attachments, what file types are allowed.

For community sites created using the [Communities Sites console](sites-console.md), an instance of the service already exists, with the inbox set to `/mail/community/inbox`.

### コミュニティのメッセージング操作サービス {#community-messaging-operations-service}

以下に示すとおり、[サイト作成ウィザード](sites-console.md)で作成されたサイトには、サービスの設定があります。設定の横にある鉛筆アイコンを選択して、設定を表示または編集できます。

![chlimage_1-63](assets/chlimage_1-63.png)

### 新しい設定 {#new-configuration}

To add a new configuration, select the plus &#39;**+**&#39; icon next to the service&#39;s name:

![chlimage_1-64](assets/chlimage_1-64.png)

* **[!UICONTROL 「Message Fields」許可リスト]**「Compose Message」コンポーネントのユーザーが編集および永続化できるプロパティを指定します。 新しいフォーム要素を追加する場合は、SRPに保存する必要がある場合は、要素IDを追加する必要があります。 Default is two entries: *subject* and *content*.
**[!UICONTROL メッセージボックスサイズ制限]**&#x200B;各ユーザーのメッセージボックスの最大バイト数。 Default is *1073741824* (1 GB).**

* **[!UICONTROL メッセージ数の制限]**:1人のユーザーに許可されるメッセージの合計数です。 値を —1に設定した場合、許可されるメッセージの数に制限はありません。メッセージボックスのサイズ制限に従います。 Default is *10000* (10k).
**[!UICONTROL 配信エラーを通知する]**&#x200B;オンにすると、メッセージ配信が一部の受信者に失敗した場合に送信者に通知します。 初期設定は&#x200B;*オン*&#x200B;です。*

* **[!UICONTROL 失敗配信送信者ID]**&#x200B;配信失敗メッセージに表示される送信者の名前。 Default is *failureNotifier*.
**[!UICONTROL 失敗メッセージテンプレートのパス]**&#x200B;失敗した配信メッセージテンプレートのルートの絶対パス。 Default is */etc/notification/messaging/default*.*

* **[!UICONTROL maxRetries.name]**&#x200B;配信に失敗したメッセージの再送を試行する回数です。デフォルトは *3* です。
**[!UICONTROL minWaitBetweenRetries.name]**&#x200B;送信に失敗したメッセージの再送を試行するまでの間隔（秒数）です。初期設定は*100 *（秒）です。*

* **[!UICONTROL カウント更新プールサイズ]**&#x200B;カウントの更新に使用される同時スレッドの数。 デフォルトは *10* です。
**[!UICONTROL inbox.path.name]**(*必須*)フォルダーに使用する、ユーザーのノードを基準とする相対パス(/home/users/*username***`inbox`** )。 パスの末尾にスラッシュ「/」を付けることはできません。 Default is */mail/inbox* .*

* **[!UICONTROL sentitems.path.name]**(*必須*)フォルダーに使用する、ユーザーのノードに対する相対パス(/home/users/*username***`senditems`** )。 パスの末尾にスラッシュ「/」を付けることはできません。 Default is */mail/sentitems* .
**[!UICONTROL supportAttachments.name]**&#x200B;オンにすると、ユーザーがメッセージに添付ファイルを追加できるようになります。初期設定は&#x200B;*オン*&#x200B;です。*

* **[!UICONTROL batchSize.name]**&#x200B;大規模な受信者グループへの送信時に一括送信処理するメッセージの数です。デフォルトは *100* です。
**[!UICONTROL maxTotalAttachmentSize.name]**「supportAttachments」をオンにすると、この値によりすべての添付ファイルの最大許容合計サイズ（バイト単位）が指定されます。Default is *104857600* (100 MB).*

* **[!UICONTROL attachmentTypeAllowlist.name]**&#x200B;ファイル拡張子のブロックリスト。先頭に「**.**」というプレフィックス付き）のブラックリストです。ブロックリストに含まれていない場合は、拡張が許可されます。 Extensions may be added or removed using the &#39;**+**&#39; and &#39;**-**&#39; icons. Default is *DEFAULT*.

* **[!UICONTROL allowedAttachmentTypes.name]**

**(*操作が必要*)** ファイル拡張子の許可リスト(ブロックリストの逆)。 To allow all file extensions, except for those blocklisted, use the &#39;**-**&#39; icon to remove the single empty entry.

* **[!UICONTROL serviceSelector.name]**(*必須*)サービスを呼び出す絶対パス（エンドポイント）（仮想リソース）。 The root of the path chosen must be one included in the *Execution Paths* configuration setting of OSGi config [ `Apache Sling Servlet/Script Resolver and Error Handler`[#$tu39], such as `/bin/`, `/apps/`, and `/services/`. サイトのメッセージング機能に対してこの設定を選択するには、このエンドポイントをの **`Service selector`** 値として指定します `Message List and Compose Message components` ( [メッセージ機能](configure-messaging.md))。 初期設定は */bin/messaging* です。


* 


* 


* 


* 
*104857600* (100 MB).

* **[!UICONTROL attachmentTypeAllowlist.name]**
A blocklist of file extensions, prefixed with &#39;
**.**&#39;, that will be rejected by the system. If not blocklisted, then the extension is allowed. Extensions may be added or removed using the &#39;**+**&#39; and &#39;**-**&#39; icons. Default is *DEFAULT*.

* **[!UICONTROL allowedAttachmentTypes.name]**

   **(*Action Required*)** An allowlist of file extensions, the opposite of the blocklist. To allow all file extensions, except for those blocklisted, use the &#39;**-**&#39; icon to remove the single empty entry.

* **[!UICONTROL serviceSelector.name]**
(*Required*) An absolute path (endpoint) through which the service is invoked (a virtual resource). The root of the path chosen must be one included in the *Execution Paths* configuration setting of OSGi config [ `Apache Sling Servlet/Script Resolver and Error Handler`-ERR:REF-NOT-FOUND-, such as `/bin/`, `/apps/`, and `/services/`. To select this configuration for a site&#39;s messaging feature, this endpoint is provided as the **`Service selector`** value for the `Message List and Compose Message components` (see [Message Feature](configure-messaging.md)). The default is */bin/messaging* .

* **[!UICONTROL fieldAllowlist.name]**
Use 
**Message Fields Allowlist**.

>[!CAUTION]
>
>Each time a `Messaging Operations Service` configuration is opened for edit, if `allowedAttachmentTypes.name` had been removed, an empty entry is re-added to make the property configurable. A single empty entry effectively disables file attachments.
>
>To allow all file extensions, except for those blocklisted, use the &#39;**-**&#39; icon to (again) remove the single empty entry before clicking **[!UICONTROL Save]**.

## Troubleshooting {#troubleshooting}

One way to troubleshoot problems is to enable [debugging messages in the log.](../../help/sites-administering/troubleshooting.md)

See also [Loggers and Writers for Individual Services](../../help/sites-deploying/configure-logging.md#loggers-and-writers-for-individual-services).

The package to monitor is `com.adobe.cq.social.messaging`.
