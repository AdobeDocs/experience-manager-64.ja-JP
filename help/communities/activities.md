---
title: アクティビティストリーム機能
seo-title: Activity Streams Feature
description: サインインしているコミュニティメンバーのアクティビティ
seo-description: Activities of a signed-in community member
uuid: 8a05a5ed-0edf-4528-a145-f9dc37d10247
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.4/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: ccaebb4c-cc1c-4ee7-b080-99667f348427
exl-id: e62b7c0d-5004-4672-9fdc-566ece2785c9
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '459'
ht-degree: 36%

---

# アクティビティストリーム機能 {#activity-streams-feature}

## はじめに {#introduction}

サインインしたコミュニティメンバーのアクティビティ（フォーラムやブログへの投稿など）は、ストリームに収集され、フィルタリングされ、様々な方法で表示されます。 `Activity Streams` コンポーネント。

コミュニティメンバーが関心のある投稿をフォローしたり、他のコミュニティメンバーのアクティビティをフォローしているときは、フォロー機能によって、アクティビティを別の見方で捉えることができます。

ドキュメントのこのセクションでは、以下の内容について説明します。

* アクティビティストリームコンポーネントのAEMサイトへの追加
* アクティビティストリームコンポーネントの設定

## アクティビティストリームをページに追加 {#adding-activity-streams-to-a-page}

必要に応じて `Activity Streams` コンポーネントをオーサリングモードでページに追加する場合は、コンポーネントブラウザーを使用して

* `Communities / Activity Streams`

コンポーネントを探し、ページ上のアクティビティストリームを表示したい位置にドラッグします。

必要な情報については、 [コミュニティコンポーネントの基本](basics.md).

次の場合に [必要なクライアント側ライブラリ](essentials-activities.md#essentials-for-client-side) が含まれる場合、この方法で `Activity Streams` コンポーネントが表示されます。

![chlimage_1-195](assets/chlimage_1-195.png)

## アクティビティストリームの設定 {#configuring-activity-streams}

配置された `Activity Streams` アクセスして選択するコンポーネント `Configure` 編集ダイアログを開くアイコン。

![chlimage_1-196](assets/chlimage_1-196.png)

「**[!UICONTROL ユーザーアクティビティ]**」タブでは、表示するアクティビティを指定します。

![chlimage_1-197](assets/chlimage_1-197.png)

* **[!UICONTROL アクティビティの最大数]**
表示するアクティビティの数
* **[!UICONTROL ストリームリソースパス]**&#x200B;空白のままにすると、コミュニティサイトまたはコミュニティグループがデフォルトになります。ストリームリソースパスは、アクティビティのソースを識別します。 初期設定は空白です。
* **[!UICONTROL ユーザーアクティビティビューを表示]**&#x200B;オンにすると、アクティビティページに、現在のメンバーがコミュニティ内で生成するアクティビティに基づいてアクティビティをフィルタリングできるタブが表示されます。初期設定はオンです。
* **[!UICONTROL すべてのアクティビティビューを表示]**
オンにすると、アクティビティページにタブが表示され、現在のメンバーがアクセスできるコミュニティ内で生成されたすべてのアクティビティが含まれます。 初期設定はオンです。
* **[!UICONTROL 次のビューを表示]**
オンにすると、アクティビティページに、現在のメンバーがフォローしているアクティビティに基づいてアクティビティをフィルタリングするタブが含まれます。 初期設定はオンです。

## フォロービュー {#following-view}

フォローを有効にするようにコンポーネントを設定する必要があります。次の機能を使用できます。 [ブログ](blog-feature.md), [フォーラム](forum.md), [Q&amp;A](working-with-qna.md), [カレンダー](calendar.md), [filelibrary](file-library.md)、および [コメント](comments.md).

![chlimage_1-198](assets/chlimage_1-198.png)

この **フォロー** ボタンは、エントリをアクティビティとしてフォローする手段を提供し、 [通知](notifications.md)、または [購読](subscriptions.md). 毎回 **フォロー** ボタンが選択されている場合、選択のオン/オフを切り替えることができます。 この `Email Subscriptions` 選択が存在するのは、設定時のみです。

フォロー方法が選択されると、ボタンのテキストが「**フォロー中**」に変わります。 便宜上、 `Unfollow All` をクリックして、すべてのメソッドをオフにします。

この **フォロー** ボタンが表示されます。

* 別のメンバーのプロファイルを表示する場合
* フォーラム、Q&amp;A、ブログなどのメイン機能ページ
   * その一般的な機能のすべてのアクティビティに従う

* フォーラムトピック、Q&amp;A 質問、ブログ記事などの特定のエントリ
   * その特定のエントリのすべてのアクティビティに従う

## 追加情報 {#additional-information}

開発者向けの詳細情報は、[アクティビティストリームの基本事項](essentials-activities.md)ページを参照してください。
