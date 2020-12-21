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

フォーラムやブログへの投稿など、ログインしたコミュニティメンバーのアクティビティは、`Activity Streams`コンポーネントの設定を通じて、様々な方法でフィルタリングおよび表示できるストリームに収集されます。

コミュニティメンバーが関心のある投稿をフォローしたり、他のコミュニティメンバーのアクティビティをフォローしているときは、フォロー機能によって、アクティビティを別の見方で捉えることができます。

ドキュメントのこのセクションでは、以下の内容について説明します。

* AEMサイトへのアクティビティストリームコンポーネントの追加
* アクティビティストリームコンポーネントの構成設定

## アクティビティストリームをページに追加 {#adding-activity-streams-to-a-page}

作成者モードで`Activity Streams`コンポーネントをページに追加する場合は、コンポーネントブラウザーを使用して

* `Communities / Activity Streams`

コンポーネントを探し、ページ上のアクティビティストリームを表示したい位置にドラッグします。

必要な情報については、[Communities Components Basics](basics.md)を参照してください。

[必要なクライアント側ライブラリ](essentials-activities.md#essentials-for-client-side)が含まれる場合、`Activity Streams`コンポーネントは次のように表示されます。

![chlimage_1-195](assets/chlimage_1-195.png)

## アクティビティストリームの設定 {#configuring-activity-streams}

アクセスする配置済みの`Activity Streams`コンポーネントを選択し、編集ダイアログを開く`Configure`アイコンを選択します。

![chlimage_1-196](assets/chlimage_1-196.png)

「**[!UICONTROL ユーザーアクティビティ]**」タブでは、表示するアクティビティを指定します。

![chlimage_1-197](assets/chlimage_1-197.png)

* **[!UICONTROL 最大ア]**
クティビティ数表示するアクティビティ数
* **[!UICONTROL ストリームリソースパス]**&#x200B;空白のままにすると、コミュニティサイトまたはコミュニティグループがデフォルトになります。ストリームリソースパスは、アクティビティのソースを識別します。 初期設定は空白です。
* **[!UICONTROL ユーザーアクティビティビューを表示]**&#x200B;オンにすると、アクティビティページに、現在のメンバーがコミュニティ内で生成するアクティビティに基づいてアクティビティをフィルタリングできるタブが表示されます。初期設定はオンです。
* **[!UICONTROL [すべてのアクティビティ]**
ビューを表示]オンにすると、アクティビティページにタブが含まれ、現在のメンバがアクセス権を持つコミュニティ内で生成されたすべてのアクティビティが含まれます。初期設定はオンです。
* **[!UICONTROL 次の]**
ビューを表示：オンにすると、アクティビティページに、現在のフィルターに基づくアクティビティがフォローしているタブが含まれます。初期設定はオンです。

## フォロービュー {#following-view}

フォローを有効にするようにコンポーネントを設定する必要があります。次の機能を使用できるのは、[blog](blog-feature.md)、[フォーラム](forum.md)、[QnA](working-with-qna.md)、[カレンダー](calendar.md)、[ファイルライブラリ](file-library.md)、[コメント](comments.md)です。

![chlimage_1-198](assets/chlimage_1-198.png)

「**後**」ボタンは、アクティビティ、[通知](notifications.md)、[購読](subscriptions.md)のエントリを後に続ける手段を提供します。 「**フォロー**」ボタンを選択するたびに、選択のオン/オフを切り替えることができます。 `Email Subscriptions`選択は、設定時にのみ存在します。

フォロー方法が選択されると、ボタンのテキストが「**フォロー中**」に変わります。 便宜上、`Unfollow All`を選択して、すべてのメソッドをオフにすることができます。

「**フォロー**」ボタンが表示されます。

* 別のメンバーのプロファイルを表示する場合
* フォーラム、QnA、ブログなどのメイン機能ページ
   * その一般的な機能のすべてのアクティビティに従う

* フォーラムトピック、QnA質問、ブログ記事など、特定のエントリ
   * 特定のエントリのすべてのアクティビティに従う

## 追加情報 {#additional-information}

開発者向けの詳細情報は、[アクティビティストリームの基本事項](essentials-activities.md)ページを参照してください。
