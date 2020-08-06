---
title: アクティビティストリームの基本事項
seo-title: アクティビティストリームの基本事項
description: メンバーが実行した最近のアクティビティのリスト、または単一のコンテンツスレッドの最近のアクティビティのリスト
seo-description: メンバーが実行した最近のアクティビティのリスト、または単一のコンテンツスレッドの最近のアクティビティのリスト
uuid: 6e4734bb-52a8-4670-b665-e640108b036e
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.4/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 8cc04993-4021-4cb7-b973-5afc4da1ed11
translation-type: tm+mt
source-git-commit: 4d64494dff34108d32e060a96209df697b2ce11f
workflow-type: tm+mt
source-wordcount: '319'
ht-degree: 74%

---


# アクティビティストリームの基本事項 {#activity-stream-essentials}

フォーラムまたはブログへの投稿など、サインインしているコミュニティメンバーのアクティビティを 1 つのストリームにまとめ、アクティビティストリームコンポーネントの設定を使用して、さまざまな方法でフィルタリングしたり、表示したりできます。

コミュニティメンバーが関心のある投稿や他のコミュニティメンバーをフォローしているときは、フォロー機能によって、別のアクティビティセットが追加されます。

どの[コミュニティサイト](overview.md#communitiessites)にも、サインインしているメンバーのユーザープロファイルページが用意されており、メンバーのアクティビティが同じ形式で表示されます。

## 概念 {#concepts}

アクティビティストリーム&#x200B;**&#x200B;とは、メンバーが行った最新のアクティビティ、またはフォーラムトピックやブログなどの単一のコンテンツスレッドで発生した最新のアクティビティをリストにしたものです。

メンバーは、別の個人やコンテンツをフォローすることによって、アクティビティストリームをフォローできます。

ニュースフィード&#x200B;**&#x200B;とは、メンバーがフォローしている複数のアクティビティストリームを単一のストリームに統合したものです。

[ソーシャルグラフ](essentials-socialgraph.md)とは、メンバー間のフォロー関係を表したものです。

## クライアント側の基本事項 {#essentials-for-client-side}

<table> 
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td> 
   <td>social/activitystreams/components/hbs/activitystreams</td> 
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>インクルード可能</strong></a></td> 
   <td>不可</td> 
  </tr>
  <tr>
   <td> <a href="clientlibs.md"><strong>clientllibs</strong></a></td> 
   <td>cq.social.hbs.activitystreams</td> 
  </tr>
  <tr>
   <td> <strong>テンプレート</strong></td> 
   <td> /libs/social/activitystreams/components/hbs/activitystreams/activitystreams.hbs<br /> /libs/social/activitystreams/components/hbs/activitystreams/activity/activity-title.hbs<br /> /libs/social/activitystreams/components/hbs/activitystreams/activity/activity.hbs</td> 
  </tr>
  <tr>
   <td> <strong>css</strong></td> 
   <td> /libs/social/activitystreams/components/hbs/activitystreams/clientlibs/activitystreams.css</td> 
  </tr>
  <tr>
   <td><strong> properties</strong></td> 
   <td>See <a href="activities.md">Activity Streams Feature</a></td> 
  </tr>
 </tbody>
</table>

* [クライアント側のカスタマイズ](client-customize.md)

## サーバー側の基本事項 {#essentials-for-server-side}

* [アクティビティストリーム API](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/activitystreams/api/package-frame.html)

* [アクティビティストリームリスナー API](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/activitystreams/listener/api/package-frame.html)

* [サーバー側のカスタマイズ](server-customize.md)

### アクティビティストリーム機能 {#activity-stream-function}

A community site structure that includes the [Activity Stream function](functions.md#activity-stream-function), includes a configured `activity streams` component.
