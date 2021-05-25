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
exl-id: a2cb9738-98a5-4ea6-8d5a-a6c0aa04cd32
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '360'
ht-degree: 39%

---

# アクティビティのトレンド {#activity-trends}

## はじめに {#introduction}

`Community Activity List`コンポーネントを使用すると、メンバーによる投稿および表示に関するトレンド情報や、コンテンツの投稿および表示を追加できます。

ドキュメントのこのセクションでは、以下の内容について説明します。

* `Community Activity List`コンポーネントを[コミュニティサイト](overview.md#community-sites)に追加する

* `Community Activity List`コンポーネントの設定

## 要件 {#requirement}

`Community Activity List`のデータは、Adobe Analyticsがライセンスを受け、コミュニティサイトに対して設定されている場合にのみ使用できます。

[コミュニティ機能のための Analytics の設定](analytics.md)を参照してください。

## コミュニティのアクティビティリストをページに追加  {#adding-a-community-activity-list-to-a-page}

`Community Activity List`コンポーネントをオーサリングモードでページに追加するには、コンポーネント`Communities / Community Activity List`を探し、ページ上の場所にドラッグします。

必要な情報については、[コミュニティコンポーネントの基本](basics.md)を参照してください。

コミュニティサイトのページに初めて配置されたとき、コンポーネントは次のように表示されます。

![chlimage_1-227](assets/chlimage_1-227.png)

## コミュニティのアクティビティリストの設定  {#configuring-community-activity-list}

配置済みの`Community Activity List`コンポーネントを選択し、`Configure`アイコンを選択すると、編集ダイアログが開きます。

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

   リストする項目の数。

   初期設定は 10 です。

* **[!UICONTROL アクティビティタイプ]**

   次のいずれかを選択します。
   * `Views`（訪問ページ数）
   * `Posts`（UGCの作成）
   * `Follows`
   * `Likes`

   初期設定は「ビュー」です。

* **[!UICONTROL 期間]**

   次のいずれかを選択します。
   * `Last 24 hours`
   * `Last 7 days`
   * `Last 30 days`
   * `Last 90 days`
   * `This year (since Jan 1st)`
   * `Total`

   デフォルトは `Total` です。

* **[!UICONTROL コンテキストパス]**

   特定のブログなど、サイトのサブセットに対するアクティビティの範囲を設定できます。

   初期設定は、コミュニティサイト全体です。

* **[!UICONTROL メンバー数の集計]**

   オフ（オフ）にすると、最上位の投稿のみがカウントされます。 例えば、コンテキストがルートページ（デフォルト）の場合、`Posts`の`Activity Type`は、ルートページにコンテンツを投稿できないので、アクティビティを表示しません。 オンにすると、すべての下位のページがカウントに含まれます。

   初期設定はオンです。

## 4 つのコンポーネントがあるページの例 {#example-page-with-components}

**上位の訪問者**&#x200B;の設定：タイプ = メンバー、アクティビティタイプ = ビュー

**上位の** 投稿者の設定：タイプ=メンバー、アクティビティタイプ=投稿

**上位の** Contentconfig:タイプ=コンテンツ、アクティビティタイプ=ビュー

**Contentconfigのト** レンド分析：タイプ=コンテンツ、アクティビティタイプ=投稿

![chlimage_1-230](assets/chlimage_1-230.png)
