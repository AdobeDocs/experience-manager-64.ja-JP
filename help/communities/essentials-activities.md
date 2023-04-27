---
title: アクティビティストリームの基本事項
seo-title: Activity Stream Essentials
description: メンバーが実行した最近のアクティビティのリスト、またはコンテンツの単一のスレッド上の最近のアクティビティのリスト
seo-description: List of recent activites performed by a member or a list of recent activities on a single thread of content
uuid: 6e4734bb-52a8-4670-b665-e640108b036e
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.4/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 8cc04993-4021-4cb7-b973-5afc4da1ed11
exl-id: 74dcbefa-e670-419b-af9b-b3d3c593ebaa
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '296'
ht-degree: 4%

---

# アクティビティストリームの基本事項 {#activity-stream-essentials}

フォーラムやブログへの投稿など、サインインしたコミュニティメンバーのアクティビティは、ストリームに収集され、アクティビティストリームコンポーネントの設定を通じて、様々な方法でフィルタリングおよび表示できます。

コミュニティメンバーが関心のある投稿や他のコミュニティメンバーの投稿をフォローする際に、フォロー機能は別のアクティビティのセットを追加します。

すべて [コミュニティサイト](overview.md#communitiessites) 同じ方法でメンバーアクティビティを表示するサインイン済みメンバーのユーザープロファイルページを含めます。

## 概念  {#concepts}

An *アクティビティストリーム* は、メンバーが実行した最近のアクティビティのリスト、またはフォーラムトピックやブログなどの単一のコンテンツスレッド上で最近実行されたアクティビティのリストです。

メンバーは、別の個人またはコンテンツをフォローすることで、アクティビティストリームをフォローします。

A *ニュースフィード* は、メンバーが続くアクティビティストリームを単一のストリームに結合したものです。

A [ソーシャルグラフ](essentials-socialgraph.md) は、あるメンバーと別のメンバーとの次の関係をキャプチャします。

## クライアント側の基本事項 {#essentials-for-client-side}

<table> 
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td> 
   <td>social/activitystreams/components/hbs/activitystreams</td> 
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>包含可能な</strong></a></td> 
   <td>いいえ</td> 
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
   <td>詳しくは、 <a href="activities.md">アクティビティストリーム機能</a></td> 
  </tr>
 </tbody>
</table>

* [クライアント側のカスタマイズ](client-customize.md)

## サーバー側の基本事項 {#essentials-for-server-side}

* [アクティビティストリーム API](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/activitystreams/api/package-frame.html)

* [アクティビティストリームリスナー API](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/activitystreams/listener/api/package-frame.html)

* [サーバー側のカスタマイズ](server-customize.md)

### アクティビティストリーム機能 {#activity-stream-function}

を含むコミュニティサイト構造 [アクティビティストリーム関数](functions.md#activity-stream-function)（設定済みを含む） `activity streams` コンポーネント。
