---
title: アクティビティストリーム機能
seo-title: アクティビティストリーム機能
description: サインインしているコミュニティメンバーのアクティビティ
seo-description: サインインしているコミュニティメンバーのアクティビティ
uuid: 8a05a5ed-0edf-4528-a145-f9dc37d10247
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.4/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: ccaebb4c-cc1c-4ee7-b080-99667f348427
translation-type: tm+mt
source-git-commit: 3d2b91565e14e85e9e701663c8d0ded03e5b430c
workflow-type: tm+mt
source-wordcount: '468'
ht-degree: 37%

---


# アクティビティストリーム機能 {#activity-streams-feature}

## 概要 {#introduction}

The activities of a signed in community member, such as posting to a forum or blog, are collected into a stream which may be filtered and displayed in various ways through configuration of the `Activity Streams` component.

コミュニティメンバーが関心のある投稿をフォローしたり、他のコミュニティメンバーのアクティビティをフォローしているときは、フォロー機能によって、アクティビティを別の見方で捉えることができます。

ドキュメントのこのセクションでは、以下の内容について説明します。

* AEMサイトへのアクティビティストリームコンポーネントの追加
* アクティビティストリームコンポーネントの構成設定

## アクティビティストリームをページに追加 {#adding-activity-streams-to-a-page}

If it is desired to add an `Activity Streams` component to a page in author mode, use the component browser to locate

* `Communities / Activity Streams`

コンポーネントを探し、ページ上のアクティビティストリームを表示したい位置にドラッグします。

For necessary information, visit [Communities Components Basics](basics.md).

[必要なクライアント側ライブラリが含まれる場合](essentials-activities.md#essentials-for-client-side) 、次のようにコンポー `Activity Streams` ネントが表示されます。

![chlimage_1-195](assets/chlimage_1-195.png)

## アクティビティストリームの設定 {#configuring-activity-streams}

Select the placed `Activity Streams` component to access and select the `Configure` icon which opens the edit dialog.

![chlimage_1-196](assets/chlimage_1-196.png)

「**[!UICONTROL ユーザーアクティビティ]**」タブでは、表示するアクティビティを指定します。

![chlimage_1-197](assets/chlimage_1-197.png)

* **[!UICONTROL 最大アクティビティ数]**&#x200B;表示するアクティビティ数
* **[!UICONTROL ストリームリソースパス]**&#x200B;空白のままにすると、コミュニティサイトまたはコミュニティグループがデフォルトになります。ストリームリソースパスは、アクティビティのソースを識別します。 初期設定は空白です。
* **[!UICONTROL ユーザーアクティビティビューを表示]**&#x200B;オンにすると、アクティビティページに、現在のメンバーがコミュニティ内で生成するアクティビティに基づいてアクティビティをフィルタリングできるタブが表示されます。初期設定はオンです。
* **[!UICONTROL [すべてのアクティビティを表示]表示]**&#x200B;オンにすると、アクティビティページにタブが含まれ、現在のメンバがアクセス権を持つコミュニティ内で生成されたすべてのアクティビティが含まれます。 初期設定はオンです。
* **[!UICONTROL [次の表示を表示]**]オンにすると、アクティビティページに、現在のメンバに基づくフィルターアクティビティがフォローしているタブが含まれます。 初期設定はオンです。

## フォロービュー {#following-view}

フォローを有効にするようにコンポーネントを設定する必要があります。Features that allow following are [blog](blog-feature.md), [forum](forum.md), [QnA](working-with-qna.md), [calendar](calendar.md), [filelibrary](file-library.md), and [comments](comments.md).

![chlimage_1-198](assets/chlimage_1-198.png)

The **Follow** button provides a means to follow entries as activities, [notifications](notifications.md), and/or [subscriptions](subscriptions.md). Each time the **Follow** button is selected, it is possible to toggle on or off a selection. The `Email Subscriptions` selection is only present when configured.

フォロー方法が選択されると、ボタンのテキストが「**フォロー中**」に変わります。 For convenience, it is possible to select `Unfollow All` to toggle off all methods.

The **Follow** button will appear:

* 別のメンバーのプロファイルを表示する場合
* フォーラム、QnA、ブログなどのメイン機能ページ
   * その一般的な機能のすべてのアクティビティに従う

* フォーラムトピック、QnA質問、ブログ記事など、特定のエントリ
   * 特定のエントリのすべてのアクティビティに従う

## 追加情報 {#additional-information}

開発者向けの詳細情報は、[アクティビティストリームの基本事項](essentials-activities.md)ページを参照してください。
