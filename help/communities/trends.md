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

`Community Activity List`コンポーネントは、メンバー別の投稿および表示に関するトレンド情報と、コンテンツの投稿および表示を追加する機能を提供します。

ドキュメントのこのセクションでは、以下の内容について説明します。

* `Community Activity List`コンポーネントを[コミュニティサイト](overview.md#community-sites)に追加する

* `Community Activity List`コンポーネントの構成設定

## 要件 {#requirement}

`Community Activity List`のデータは、Adobe Analyticsがコミュニティサイトに対してライセンスを取得し、設定されている場合にのみ利用できます。

[コミュニティ機能のための Analytics の設定](analytics.md)を参照してください。

## コミュニティのアクティビティリストをページに追加  {#adding-a-community-activity-list-to-a-page}

作成者モードで`Community Activity List`コンポーネントをページに追加するには、コンポーネント`Communities / Community Activity List`を見つけてページ上の位置にドラッグします。

必要な情報については、[Communities Components Basics](basics.md)を参照してください。

コミュニティサイトのページに初めて配置されたとき、コンポーネントは次のように表示されます。

![chlimage_1-227](assets/chlimage_1-227.png)

## コミュニティのアクティビティリストの設定  {#configuring-community-activity-list}

アクセスする配置済みの`Community Activity List`コンポーネントを選択し、編集ダイアログを開く`Configure`アイコンを選択します。

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

   データの上に表示する説明的なタイトル（`Trending Content`など）。

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

   オフにする（オフにする）と、最上位レベルの投稿のみがカウントされます。 例えば、コンテキストがルートページ（デフォルト）の場合、`Activity Type`/`Posts`は、ルートページにコンテンツを投稿できないので、アクティビティを表示しません。 オンにすると、すべての下位のページがカウントに含まれます。

   初期設定はオンです。

## 4 つのコンポーネントがあるページの例 {#example-page-with-components}

**上位の訪問者**&#x200B;の設定：タイプ = メンバー、アクティビティタイプ = ビュー

**Top** Contributorsconfig:タイプ=メンバー、アクティビティタイプ=投稿

**Top** Contentconfig:Type = Content、アクティビティタイプ=表示、

**トレンド** の内容：タイプ=コンテンツ、アクティビティタイプ=投稿

![chlimage_1-230](assets/chlimage_1-230.png)
