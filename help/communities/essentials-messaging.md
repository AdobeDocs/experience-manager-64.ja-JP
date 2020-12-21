---
title: メッセージングの基本事項
seo-title: メッセージングの基本事項
description: メッセージングコンポーネントの概要
seo-description: メッセージングコンポーネントの概要
uuid: 53711f4d-6bbc-4be9-aefe-4e75a81cd67f
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.4/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: eb8fd2b3-0a31-425e-b0f1-38f09e1106df
translation-type: tm+mt
source-git-commit: 98fae2d51d73bda946f3c398e9276fe4d5a8a0fe
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 42%

---


# メッセージングの基本事項 {#messaging-essentials}

このページでは、メッセージングコンポーネントを使用してメッセージング機能を Web サイトに組み込む方法の詳細をまとめています。

## クライアント側の基本事項  {#essentials-for-client-side}

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
   <td><a href="configure-messaging.md">メッセージの設定</a>を参照</td> 
  </tr> 
  <tr> 
   <td><strong>管理設定</strong></td> 
   <td><a href="messaging.md">メッセージングの設定</a></td> 
  </tr> 
 </tbody> 
</table>

**メッセージリスト** （受信トレイ、送信済み、ごみ箱用）

<table> 
 <tbody> 
  <tr> 
   <td> <strong>resourceType</strong></td> 
   <td><p>social/messaging/components/hbs/messagebox</p> </td> 
  </tr> 
  <tr> 
   <td> <a href="client-customize.md#clientlibs-for-scf"><strong>clientlibs</strong></a></td> 
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
   <td><strong>プロパティ</strong></td> 
   <td><a href="configure-messaging.md">メッセージの設定</a>を参照</td> 
  </tr> 
  <tr> 
   <td><strong>管理設定</strong></td> 
   <td><a href="messaging.md">メッセージングの設定</a></td> 
  </tr> 
 </tbody> 
</table>

[クライアント側のカスタマイズ](client-customize.md)も参照してください。

## サーバー側の基本事項  {#essentials-for-server-side}

* [メッセージングの設定](configure-messaging.md)

* [SCFコンポーネント用メッセージングクライアント](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/messaging/client/api/package-summary.html) API

* [メッセージング API](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/messaging/api/package-summary.html)（サービス用）

* [メッセージングエンドポイント](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/messaging/client/endpoints/package-summary.html)

* [サーバー側のカスタマイズ](server-customize.md)

>[!CAUTION]
>
>次のMessageBuilderメソッドの場合、Stringパラメーターに末尾にスラッシュ「/」を含めることはできません*。
>
>* `setInboxPath`()
>* `setSentItemsPath`()

>
>
次に例を示します。
>
>
```
>valid: mb.setInboxPath( "/mail/inbox" );
> not valid: mb.setInboxPath( "/mail/inbox/" );
>```

### コミュニティサイト {#community-site}

ウィザードを使用して作成したコミュニティサイト構造には、選択したメッセージング機能が含まれています。[コミュニティサイトコンソール](sites-console.md#user-management)の`User Management`設定を参照してください。

### サンプルコード：メッセージ受信通知 {#sample-code-message-received-notification}

ソーシャルメッセージ機能は、操作（例：`send`、`marking read`、`marking delete`）に対してイベントをスローします。 これらのイベントは、イベントに含まれるデータに対して取得し、実行されるアクションです。

次の例は、`message sent`イベントをリッスンし、`Day CQ Mail Service`を使用するすべてのイベント受信者に電子メールを送信するメッセージハンドラーです。

サーバー側サンプルスクリプトを試すには、開発環境と OSGi バンドルのビルド機能が必要です。

1. ` [CRXDE|Lite](http://localhost:4502/crx/de)`に管理者としてログイン
1. `bundle node`を`/apps/engage/install`内に作成し、次のような任意の名前を付けます。

   * **[!UICONTROL シンボリック名]**:com.engage.media.social.messaging.MessagingNotification
   * ****&#x200B;名前：Getting Started Tutorial Message Notificaton
   * **[!UICONTROL 説明]**:ユーザーがメッセージを受け取ったときに電子メール通知を送信するサンプルサービス
   * **[!UICONTROL パッケージ]**:  `com.engage.media.social.messaging.notification`

1. `/apps/engage/install/com.engage.media.social.messaging.MessagingNotification/src/main/java/com/engage/media/social/messaging/notification` に移動します。

   1. 自動的に作成された`Activator.java`クラスを削除します
   1. クラス`MessageEventHandler.java`を作成
   1. 以下のコードを`MessageEventHandler.java`にコピー&amp;ペーストします。

1. 「**[!UICONTROL すべて保存]**」をクリックします
1. `/apps/engage/install/com.engage.media.social.messaging.MessagingNotification/com.engage.media.social.messaging.MessagingNotification.bnd`に移動し、`MessageEventHandler.java`コードに記述されているとおりに、すべてのインポート文を追加します。
1. バンドルの構築
1. `Day CQ Mail Service`OSGiサービスが構成されていることを確認します
1. 1人のデモユーザーとしてログインし、別のデモユーザーに電子メールを送信する
1. 受信者は、新しいメッセージに関する電子メールを受信する必要があります

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

