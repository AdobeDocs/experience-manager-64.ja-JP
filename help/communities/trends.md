---
title: アクティビティのトレンド
seo-title: アクティビティのトレンド
description: コミュニティのアクティビティリストコンポーネントをページに追加
seo-description: コミュニティのアクティビティリストコンポーネントをページに追加
uuid: 6a030340-0e69-432a-98f1-3effb2b97136
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.4/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 93a112fc-ef34-4281-89b8-a0f1b3d3aca9
translation-type: tm+mt
source-git-commit: 5ddbcb2addff2d6e3a3e9d7e100a6d9ba89fdd60
workflow-type: tm+mt
source-wordcount: '360'
ht-degree: 39%

---


# アクティビティのトレンド {#activity-trends}

## 概要 {#introduction}

The `Community Activity List` component provides the ability to add trending information regarding posts and views by members as well as posts and views of content.

ドキュメントのこのセクションでは、以下の内容について説明します。

* Adding the `Community Activity List` component to a [community site](overview.md#community-sites)

* Configuration settings for the `Community Activity List` component

## 要件 {#requirement}

Data for the `Community Activity List` is only available when Adobe Analytics is licensed and configured for the community site.

[コミュニティ機能のための Analytics の設定](analytics.md)を参照してください。

## コミュニティのアクティビティリストをページに追加 {#adding-a-community-activity-list-to-a-page}

作成者モードでページに `Community Activity List` コンポーネントを追加するには、コンポーネントを見つけ `Communities / Community Activity List` てページ上の位置にドラッグします。

For necessary information, visit [Communities Components Basics](basics.md).

コミュニティサイトのページに初めて配置されたとき、コンポーネントは次のように表示されます。

![chlimage_1-227](assets/chlimage_1-227.png)

## コミュニティのアクティビティリストの設定  {#configuring-community-activity-list}

Select the placed `Community Activity List` component to access and select the `Configure` icon which opens the edit dialog.

![chlimage_1-228](assets/chlimage_1-228.png)

「**[!UICONTROL コメント]**」タブでは、アップロードしたファイルに対するコメントを表示するかどうかと、その方法を指定します。

![chlimage_1-229](assets/chlimage_1-229.png)

* **[!UICONTROL 型]**

   コミュニティメンバーに関するデータを表示するか、ユーザー生成コンテンツ(UGC)を表示するかを指定します。

   次から選択
   * `Members`
   * `Content`

   デフォルトは `Members` です。

* **[!UICONTROL 表示タイトル]**

   データの上に表示する説明的なタイトル（例：） `Trending Content`。

   初期設定では、タイトルはありません。

* **[!UICONTROL 表示数]**

   リストする項目数。

   初期設定は 10 です。

* **[!UICONTROL アクティビティタイプ]**

   いずれかを選択
   * `Views`（ページ訪問数）
   * `Posts`（UGCの作成）
   * `Follows`
   * `Likes`

   初期設定は「ビュー」です。

* **[!UICONTROL 期間]**

   いずれかを選択
   * `Last 24 hours`
   * `Last 7 days`
   * `Last 30 days`
   * `Last 90 days`
   * `This year (since Jan 1st)`
   * `Total`

   デフォルトは `Total` です。

* **[!UICONTROL コンテキストパス]**

   特定のブログなど、サイトのサブセットに対するアクティビティのスコープを設定する機能を提供します。

   初期設定は、コミュニティサイト全体です。

* **[!UICONTROL メンバー数の集計]**

   オフにする（オフにする）と、最上位レベルの投稿のみがカウントされます。 For example, if the context is the root page (the default), then an `Activity Type`of `Posts`will never show any activity as there is no ability to post content to the root page. オンにすると、すべての下位のページがカウントに含まれます。

   初期設定はオンです。

## 4 つのコンポーネントがあるページの例 {#example-page-with-components}

**上位の訪問者**&#x200B;の設定：タイプ = メンバー、アクティビティタイプ = ビュー

**上位の寄稿者** : タイプ=メンバー、アクティビティタイプ=投稿

**最上位のコンテンツ** : Type = Content、アクティビティタイプ=表示、

**トレンドコンテンツ** の設定： タイプ=コンテンツ、アクティビティタイプ=投稿

![chlimage_1-230](assets/chlimage_1-230.png)
