---
title: Adobe Target との統合の前提条件
seo-title: Prerequisites for Integrating with Adobe Target
description: Adobe Target との統合の前提条件について説明します。
seo-description: Find out about the prerequisites for integrating with Adobe Target.
uuid: 88be6a97-c964-4e42-a3a2-ed9b2c9ee49e
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: integration
content-type: reference
discoiquuid: a84fd0ab-0bcd-48cf-bba3-fb29308fa0f8
exl-id: f47e5c6a-ed52-4493-83bd-73e5e693d117
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '524'
ht-degree: 80%

---

# Adobe Target との統合の前提条件{#prerequisites-for-integrating-with-adobe-target}

[AEM と Adobe Target の統合](/help/sites-administering/target.md)の一環として、Adobe Target を登録し、レプリケーションエージェントを設定して、パブリッシュノードでアクティビティ設定を保護する必要があります。

## Adobe Target の登録 {#registering-with-adobe-target}

AEM と Adobe Target を統合するには、有効な Adobe Target アカウントが必要です。このアカウントには、少なくとも**承認者**レベルの権限が必要です。 Adobe Target に登録すると、クライアントコードを受け取ります。AEM を Adobe Target に接続するには、クライアントコードおよび Adobe Target のログイン名とパスワードが必要です。

クライアントコードは、Adobe Target サーバーを呼び出すときに Adobe Target の顧客アカウントを識別します。

>[!NOTE]
>
>統合を使用するには、Target チームによってご自身のアカウントも有効にされている必要があります。
>
>
>そうでない場合は、[Adobe Target カスタマーケア](https://docs.adobe.com/content/help/en/target/using/cmp-resources-and-contact-information.html)にご連絡ください。

## Target レプリケーションエージェントの有効化 {#enabling-the-target-replication-agent}

Test &amp; Target [レプリケーションエージェント](/help/sites-deploying/replication.md)を作成者インスタンス上で有効にする必要があります。AEM のインストールに [nosamplecontent](/help/sites-deploying/configure-runmodes.md#using-samplecontent-and-nosamplecontent) 実行モードを使用した場合、このレプリケーションエージェントはデフォルトでは有効になっていません。実稼動環境の保護に関する情報については、[セキュリティチェックリスト](/help/sites-administering/security-checklist.md)を参照してください。

1. AEM のホームページで、**ツール**／**導入**／**レプリケーション**&#x200B;をクリックまたはタップします。
1. 「**作成者のエージェント**」をクリックまたはタップします。
1. **Test &amp; Target**&#x200B;レプリケーションエージェントをクリックまたはタップして、「**編集**」をクリックまたはタップします。
1. 「有効」オプションをオンにして、「**OK**」をクリックまたはタップします。

   >[!NOTE]
   >
   >Test &amp; Target レプリケーションエージェントを設定する場合、URI は、「**トランスポート**」タブでデフォルトで **tnt:///** に設定されています。この URI を次で置き換えない **https://admin.testandtarget.omniture.com**.
   >
   >**tnt:///** を使用して接続をテストしようとすると、エラーが発生することに注意してください。この URI は内部でのみ使用され、では使用しないので、これは期待された動作です。 **接続をテスト**.

## アクティビティ設定ノードの保護 {#securing-the-activity-settings-node}

権限のないユーザーがアクセスできないように、パブリッシュインスタンスでアクティビティ設定ノード **cq:ActivitySettings** を保護する必要があります。アクティビティ設定ノードには、Adobe Target へのアクティビティの同期を処理するサービスのみがアクセスできるようにしてください。

この **cq:ActivitySettings** ノードは、CRXDE lite の下の `/content/campaigns/*nameofbrand*`* *activitys jcr:content ノードの下で、* 例： `/content/campaign/we-retail/master/myactivity/jcr:content/cq:ActivitySettings`. このノードは、コンポーネントのターゲティング後にのみ作成されます。

この **cq:ActivitySettings** アクティビティの jcr:content の下のノードは、次の ACL で保護されています。

* すべて拒否（全員）
* &quot;target-activity-authors&quot; に jcr:read,rep:write を許可（デフォルトで作成者はこのグループのメンバー）
* &quot;targetservice&quot; に jcr:read,rep:write を許可

これらの設定により、権限を持たないユーザーがノードプロパティにアクセスできなくなります。オーサーインスタンスとパブリッシュインスタンスの両方で同じ ACL を使用します。詳しくは、 [ユーザー管理とセキュリティ](/help/sites-administering/security.md) を参照してください。

## AEM Externalizer の設定 {#configuring-the-aem-externalizer}

Adobe Target でアクティビティを編集する場合、AEM オーサーノードで URL を変更していなければ、URL は **localhost** を指しています。

AEM Externalizer を設定するには：

1. OSGi Web コンソール ( ) に移動します。 **https://&lt;server>:&lt;port>/system/console/configMgr.**
1. **Day CQ Link Externalizer** を探し、オーサーノードのドメインを入力します。

   ![chlimage_1-120](assets/chlimage_1-120.png)
