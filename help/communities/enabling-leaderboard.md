---
title: リーダーボード機能
seo-title: リーダーボード機能
description: ページへのリーダーボードコンポーネントの追加
seo-description: ページへのリーダーボードコンポーネントの追加
uuid: 2a766b63-3ab4-44cd-8a26-629a71b837ea
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.4/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 1e96d388-8517-4a84-bb0a-d49567eb4bdf
translation-type: tm+mt
source-git-commit: 1bbd917ef20c4a618e93af66ffe8a6cfc8448e78
workflow-type: tm+mt
source-wordcount: '410'
ht-degree: 72%

---


# リーダーボード機能 {#leaderboard-feature}

## 概要 {#introduction}

The `Leaderboard` component provides the ability to obtain a sense of how members are interacting within the community by ranking members according to points earned (basic scoring) or their expertise (advanced scoring).

ページにリーダーボードコンポーネントを含める前に、[コミュニティのスコアとバッジ](implementing-scoring.md)を設定する必要があります。

ドキュメントのこのセクションでは、以下の内容について説明します。

* Adding the `Leaderboard` component to a [community site](overview.md#community-sites)

* Configuration settings for the `Leaderboard` component

## リーダーボードをページに追加 {#adding-a-leaderboard-to-a-page}

To add a `Leaderboard` component to a page in author mode, locate the component

* `Communities / Leaderboard`

コンポーネントを探し、ページ上の位置にドラッグします。

For necessary information, visit [Communities Components Basics](basics.md).

コミュニティサイトのページに初めて配置されたとき、コンポーネントは次のように表示されます。

![chlimage_1-8](assets/chlimage_1-8.png)

## リーダーボードの設定 {#configuring-leaderboard}

Select the placed `Leaderboard` component to access and select the `Configure` icon which opens the edit dialog.

![chlimage_1-9](assets/chlimage_1-9.png) ![chlimage_1-10](assets/chlimage_1-10.png)

### 「設定」タブ{#settings-tab}

「**[!UICONTROL 設定]**」タブで、メンバーに関連して表示する情報を指定します。

* **[!UICONTROL 表示名]**&#x200B;ボードに表示する説明的な名前。バッジとスコアの表示用に選択されたルールが反映されます。

   Default is `Leaderboard`, if nothing entered.

* **[!UICONTROL バッジ]**&#x200B;オンにすると、リーダーボードにバッジアイコンの列が表示されるようになります。

   初期設定はオフです。

* **[!UICONTROL バッジ名]**&#x200B;オンにすると、リーダーボードにバッジ名の列が表示されるようになります。

   初期設定はオフです。

* **[!UICONTROL ユーザーアバター]**&#x200B;オンにすると、リーダーボードでメンバープロフィールの名前リンクの横にメンバーのアバター画像が表示されるようになります。

   初期設定はオフです。

### 「ルール」タブ{#rules-tab}

「**[!UICONTROL ルール]**」タブで、コミュニティサイト、およびそのスコアルールとバッジルールを指定します。

* **[!UICONTROL ルールの場所]**（必須）スコア／バッジルールを設定する場所

* **[!UICONTROL スコアルール]**（必須）表示するスコアを生成する特定のルール

* **[!UICONTROL バッジルール]**（必須）表示するバッジを生成する特定のルール

* **[!UICONTROL 最大表示数]** 1 ページに表示するメンバー数。

   初期設定は 10 です。

## 例：参加者のリーダーボード {#example-participants-leaderboard}

このリーダーボードには、基本スコアルールを適用した結果が報告されます。

リーダーボードコンポーネントの設定：

* **[!UICONTROL 「設定」タブ：]**

   * 表示名 = `Participation Board`
   *  `checked` の下）で、次の手順をおこないます。

      * バッジ
      * バッジ名
      * ユーザーアバター

* **[!UICONTROL 「ルール」タブ：]**

   * ルールの場所 = `/content/sites/communities/jcr:content`
   * スコアルール = `/etc/community/scoring/rules/forums-scoring`
   * バッジルール = `/etc/community/badging/rules/reference-badging`
   * 最大表示数 = `10`

![chlimage_1-11](assets/chlimage_1-11.png)

## 例：エキスパートのリーダーボード {#example-experts-leaderboard}

このリーダーボードには、高度なスコアルールを適用した結果が報告されます。

リーダーボードコンポーネントの設定：

* **[!UICONTROL 「設定」タブ：]**

   * 表示名 = `Expertise Board`
   *  `checked` の下）で、次の手順をおこないます。

      * バッジ
      * ユーザーアバター

* **[!UICONTROL 「ルール」タブ：]**

   * ルールの場所 = `/content/sites/communities/jcr:content`
   * スコアルール = `/etc/community/scoring/rules/adv-forums-scoring`
   * バッジルール = `/etc/community/badging/rules/adv-forums-badging`
   * 最大表示数 = `10`

![chlimage_1-12](assets/chlimage_1-12.png)

## 追加情報 {#additional-information}

More information may be found on the [Leaderboard Essentials](leaderboard.md) page for developers.

Instructions for creating rules are provided on the [Communities Scoring and Badges](implementing-scoring.md) page for administrators.
