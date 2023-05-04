---
title: メッセージングの基本事項
seo-title: Messaging Essentials
description: メッセージコンポーネントの概要
seo-description: Messaging component overview
uuid: 53711f4d-6bbc-4be9-aefe-4e75a81cd67f
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.4/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: eb8fd2b3-0a31-425e-b0f1-38f09e1106df
exl-id: c6ad3c2b-8776-4ec4-99da-ab73ecc61153
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '423'
ht-degree: 6%

---

# メッセージングの基本事項 {#messaging-essentials}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

このページでは、メッセージングコンポーネントを使用して Web サイトにメッセージング機能を組み込む方法について詳しく説明します。

## クライアント側の基本事項 {#essentials-for-client-side}

**メッセージを作成**

<table> 
 <tbody> 
  <tr> 
   <td> <strong>resourceType</strong></td> 
   <td><p>social/messaging/components/hbs/composemessage</p> </td> 
  </tr> 
  <tr> 
   <td> <a href="client-customize.md#clientlibs-for-scf"><strong>clientllibs</strong></a></td> 
   <td><p>cq.social.hbs.messaging</p> </td> 
  </tr> 
  <tr> 
   <td> <strong>テンプレート</strong></td> 
   <td>/libs/social/messaging/components/hbs/composemessage/composemessage.hbs</td> 
  </tr> 
  <tr> 
   <td><strong>css</strong></td> 
   <td>/libs/social/messaging/components/hbs/composemessage/clientlibs/composemessage.css</td> 
  </tr> 
  <tr> 
   <td><strong>properties</strong></td> 
   <td>参照 <a href="configure-messaging.md">メッセージの設定</a></td> 
  </tr> 
  <tr> 
   <td><strong>管理設定</strong></td> 
   <td><a href="messaging.md">メッセージングの設定</a></td> 
  </tr> 
 </tbody> 
</table>

**メッセージリスト** （インボックス、送信済みおよびごみ箱用）

<table> 
 <tbody> 
  <tr> 
   <td> <strong>resourceType</strong></td> 
   <td><p>social/messaging/components/hbs/messagebox</p> </td> 
  </tr> 
  <tr> 
   <td> <a href="client-customize.md#clientlibs-for-scf"><strong>clientllibs</strong></a></td> 
   <td><p>cq.social.hbs.messaging</p> </td> 
  </tr> 
  <tr> 
   <td> <strong>テンプレート</strong></td> 
   <td>/libs/social/messaging/components/hbs/messagebox/messagebox.hbs</td> 
  </tr> 
  <tr> 
   <td><strong>css</strong></td> 
   <td>/libs/social/messaging/components/hbs/messagebox/clientlibs/messagebox.css</td> 
  </tr> 
  <tr> 
   <td><strong>properties</strong></td> 
   <td>詳しくは、 <a href="configure-messaging.md">メッセージの設定</a></td> 
  </tr> 
  <tr> 
   <td><strong>管理設定</strong></td> 
   <td><a href="messaging.md">メッセージングの設定</a></td> 
  </tr> 
 </tbody> 
</table>

関連トピック [クライアント側のカスタマイズ](client-customize.md)

## サーバー側の基本事項 {#essentials-for-server-side}

* [メッセージングの設定](configure-messaging.md)

* [メッセージングクライアント API](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/messaging/client/api/package-summary.html) （SCF コンポーネント用）

* [メッセージング API](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/messaging/api/package-summary.html) サービスの

* [メッセージエンドポイント](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/messaging/client/endpoints/package-summary.html)

* [サーバー側のカスタマイズ](server-customize.md)

>[!CAUTION]
>
>次の MessageBuilder メソッドの場合、String パラメーターの末尾にスラッシュ「/」を含めることはできません。
>
>* `setInboxPath`()
>* `setSentItemsPath`()
>
>次に例を示します。
>
>
```
>valid: mb.setInboxPath( "/mail/inbox" );
> not valid: mb.setInboxPath( "/mail/inbox/" );
>```

### コミュニティサイト {#community-site}

ウィザードを使用して作成したコミュニティサイト構造には、メッセージング機能が含まれます。 詳しくは、 `User Management` 設定 [コミュニティサイトコンソール](sites-console.md#user-management).

### サンプルコード：メッセージ受信通知 {#sample-code-message-received-notification}

ソーシャルメッセージ機能では、例えば操作に対してイベントが発生します `send`, `marking read`, `marking delete`. これらのイベントを取得し、イベントに含まれるデータに対して実行されるアクションを取得できます。

次の例は、 `message sent` イベントを送信し、 `Day CQ Mail Service`.

サーバー側のサンプルスクリプトを試すには、開発環境と OSGi バンドルを構築する機能が必要です。

1. 管理者としてにログインします。 ` [CRXDE|Lite](http://localhost:4502/crx/de)`
1. の作成 `bundle node`in `/apps/engage/install` 任意の名前を持つ

   * **[!UICONTROL 記号名]**:com.engage.media.social.messaging.MessagingNotification
   * **[!UICONTROL 名前]**:使用の手引きチュートリアルのメッセージ通知
   * **[!UICONTROL 説明]**:ユーザーがメッセージを受信したときに電子メール通知を送信するサンプルサービス
   * **[!UICONTROL パッケージ]**: `com.engage.media.social.messaging.notification`

1. `/apps/engage/install/com.engage.media.social.messaging.MessagingNotification/src/main/java/com/engage/media/social/messaging/notification` に移動します。

   1. を削除します。 `Activator.java` 自動作成されたクラス
   1. クラスを作成 `MessageEventHandler.java`
   1. 以下のコードをにコピー&amp;ペーストします。 `MessageEventHandler.java`

1. クリック **[!UICONTROL すべて保存]**
1. に移動します。 `/apps/engage/install/com.engage.media.social.messaging.MessagingNotification/com.engage.media.social.messaging.MessagingNotification.bnd` そして、 `MessageEventHandler.java` コード。
1. バンドルをビルドします。
1. 確認 `Day CQ Mail Service`OSGi サービスが設定されている
1. 1 人のデモユーザーとしてログインし、別のデモユーザーに電子メールを送信する
1. 受信者は、新しいメッセージに関する E メールを受信する必要があります

#### MessageEventHandler.java {#messageeventhandler-java}

```java
package com.engage.media.social.messaging.notification;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Properties;
import org.apache.felix.scr.annotations.Property;
import org.apache.felix.scr.annotations.Service;
import org.apache.felix.scr.annotations.Reference;
import org.apache.sling.api.resource.ResourceResolver;
import org.apache.sling.api.resource.ResourceResolverFactory;
import org.apache.sling.api.resource.Resource;
import org.apache.commons.mail.Email;
import org.apache.commons.mail.EmailException;
import org.apache.commons.mail.SimpleEmail;
import org.apache.commons.mail.HtmlEmail;
import java.util.List;
import org.osgi.service.event.Event;
import org.osgi.service.event.EventHandler;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import com.adobe.cq.social.messaging.api.Message;
import com.adobe.cq.social.messaging.api.MessagingEvent;
import com.day.cq.mailer.MessageGatewayService;
import com.day.cq.mailer.MessageGateway;

@Component(immediate=true)
@Service(EventHandler.class)
@Properties({
        @Property(name = "event.topics", value = "com/adobe/cq/social/message")
})
public class MessagingEventHandler implements EventHandler {
    private Logger logger = LoggerFactory.getLogger(MessagingEventHandler.class);

    @Reference
    ResourceResolverFactory resourceResolverFactory;

    @Reference
    private MessageGatewayService messageGatewayService;

    ResourceResolver resourceResolver=null;
    MessageGateway messageGateway=null;

    public void sendMail(String from, String to,String subject, String content){
        Email email = new SimpleEmail();
        messageGateway = messageGatewayService.getGateway(SimpleEmail.class);
        try {
         email.addTo(to);
            email.addReplyTo(from);
            email.setFrom(from);
            email.setMsg(content);
            email.setSubject(subject);
         messageGateway.send(email);
        } catch(EmailException ex) {
            logger.error("MessageNotificaiton : Error sending email : "+ex.getMessage());
        }
        logger.info("**** MessageNotification **** Mail sent to " + to);
    }

    public void handleEvent(Event event) {
        //Get Message Path and originator User's ID from event
        String messagePath = (String) event.getProperty("path");
        String senderId = (String) event.getProperty("userId");
        MessagingEvent.MessagingActions action = (MessagingEvent.MessagingActions) event.getProperty("action");
        try{
            if(MessagingEvent.MessagingActions.MessageSent.equals(action)){
                resourceResolver = resourceResolverFactory.getAdministrativeResourceResolver(null);

                //Read message
                Resource resource = resourceResolver.getResource(messagePath);
                Message msg = resource.adaptTo(Message.class);

                //Get list of recipient Ids from message
                //For Getting Started Tutorial, Id is same as email. If that is not the case in your site, 
                //an additional step is needed to retrieve the email for the Id
                List<String> reclist = msg.getRecipientIdList();
                for(int i=0;i<reclist.size();i++){
                    //Send Email using Mailing Service
                    sendMail("admin@cqadmin.qqq",reclist.get(i),"New message on Getting Started Tutorial", "Hi\nYou have received a new message from  " +  senderId + ". To read it, sign in to Getting Started Tutorial.\n\n-Engage Admin");
                }
            }
        } catch(Exception ex){
            logger.error("Error getting message info : " + ex.getMessage());
        } finally {
            resourceResolver.close();
        }

    }
}
```
