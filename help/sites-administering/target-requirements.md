---
title: Adobe Target との統合の前提条件
seo-title: Prerequisites for Integrating with Adobe Target
description: Adobe Targetとの統合の前提条件について説明します。
seo-description: Find out about the prerequisites for integrating with Adobe Target.
uuid: 88be6a97-c964-4e42-a3a2-ed9b2c9ee49e
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: integration
content-type: reference
discoiquuid: a84fd0ab-0bcd-48cf-bba3-fb29308fa0f8
exl-id: f47e5c6a-ed52-4493-83bd-73e5e693d117
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '558'
ht-degree: 47%

---

# Adobe Target との統合の前提条件{#prerequisites-for-integrating-with-adobe-target}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

の一部として [AEMとAdobe Targetの統合](/help/sites-administering/target.md)を使用する場合は、Adobe Targetに登録し、レプリケーションエージェントを設定し、パブリッシュノードでアクティビティのセキュリティを保護する必要があります。

## Adobe Targetへの登録 {#registering-with-adobe-target}

AEMをAdobe Targetと統合するには、有効なAdobe Targetアカウントが必要です。 このアカウントには、少なくとも**承認者**レベルの権限が必要です。 Adobe Target に登録すると、クライアントコードを受け取ります。AEMをAdobe Targetに接続するには、クライアントコードとAdobe Targetのログイン名およびパスワードが必要です。

クライアントコードは、Adobe Targetサーバーを呼び出す際にAdobe Targetの顧客アカウントを識別します。

>[!NOTE]
>
>統合を使用するには、Target チームによってご自身のアカウントも有効にされている必要があります。
>
>
>該当しない場合は、 [Adobe Targetカスタマーケア](https://experienceleague.adobe.com/docs/target/using/cmp-resources-and-contact-information.html?lang=ja).

## Target レプリケーションエージェントの有効化 {#enabling-the-target-replication-agent}

Test &amp; Target [レプリケーションエージェント](/help/sites-deploying/replication.md)を作成者インスタンス上で有効にする必要があります。AEM のインストールに [nosamplecontent](/help/sites-deploying/configure-runmodes.md#using-samplecontent-and-nosamplecontent) 実行モードを使用した場合、このレプリケーションエージェントはデフォルトでは有効になっていません。実稼動環境の保護について詳しくは、 [セキュリティチェックリスト](/help/sites-administering/security-checklist.md).

1. AEMホームページで、「 」をクリックまたはタップします。 **ツール** > **導入** > **レプリケーション**.
1. クリックまたはタップ **作成者のエージェント**.
1. クリックまたはタップ **Test と Target（test と Target）** レプリケーションエージェントをクリックまたはタップします。 **編集**.
1. 「有効」オプションを選択し、「 」をクリックまたはタップします **OK**.

   >[!NOTE]
   >
   >Test と Target のレプリケーションエージェントを設定する際に、 **輸送** 」タブに設定されている場合、URI はデフォルトで「 **tnt:///**. この URI を **https://admin.testandtarget.omniture.com** に置換しないでください。
   >
   >**tnt:///** を使用して接続をテストしようとすると、エラーが発生することに注意してください。これは想定されている動作です。この URI は内部でのみ使用されるべきものであり、**接続をテスト**&#x200B;では使用すべきではありません。

## アクティビティ設定ノードの保護 {#securing-the-activity-settings-node}

アクティビティ設定ノードを保護する必要があります **cq:ActivitySettings** 通常のユーザーがアクセスできないように、パブリッシュインスタンス上で実行します。 アクティビティ設定ノードには、Adobe Target へのアクティビティの同期を処理するサービスのみがアクセスできるようにしてください。

**cq:ActivitySettings** ノードは、*アクティビティ jcr:content ノードの下*&#x200B;の `/content/campaigns/*nameofbrand*`* の下の CRXDE Lite で利用できます（例：`/content/campaign/we-retail/master/myactivity/jcr:content/cq:ActivitySettings`）。このノードは、コンポーネントのターゲティング後にのみ作成されます。

アクティビティの jcr:content の下にある **cq:ActivitySettings** ノードは、次の ACL によって保護されています。

* 全員に対してすべて拒否
* 「target-activity-authors」に対して jcr:read,rep:write を許可します (author はこのグループのメンバーです。
* 「targetservice」の jcr:read,rep:write を許可

これらの設定により、通常のユーザーはノードプロパティにアクセスできなくなります。 オーサーとパブリッシュで同じ ACL を使用します。 詳しくは、[ユーザー管理とセキュリティ](/help/sites-administering/security.md)を参照してください。

## AEM Externalizer の設定 {#configuring-the-aem-externalizer}

Adobe Target でアクティビティを編集する場合、AEM オーサーノードで URL を変更していなければ、URL は **localhost** を指しています。

AEM Externalizer を設定するには：

1. **https://&lt;server>:&lt;port>/system/console/configMgr** の OSGi Web コンソールに移動します。
1. **Day CQ Link Externalizer** を探し、オーサーノードのドメインを入力します。

   ![chlimage_1-120](assets/chlimage_1-120.png)
