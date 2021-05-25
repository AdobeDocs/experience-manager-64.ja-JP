---
title: 投票の使用
seo-title: 投票の使用
description: 投票コンポーネントをページに追加
seo-description: 投票コンポーネントをページに追加
uuid: 56e6cced-2f2d-434a-8fde-92a6c2478a04
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.4/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 071cac6d-05c5-47ab-85bc-ead6693ca1f4
exl-id: 660a7106-0c21-4073-8319-4d6d20b9bc49
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 25%

---

# 投票の使用 {#using-voting}

`Voting`コンポーネントは、コミュニティメンバーがQ&amp;Aコンポーネント内の回答など、特定のコンテンツを評価するのに役立つツールです。 `Voting`コンポーネントを使用して、メンバーは上向き矢印または下向き矢印を選択して意見を示します。

## 投票をページに追加 {#adding-voting-to-a-page}

`Voting`コンポーネントをオーサリングモードでページに追加するには、コンポーネントブラウザーを使用して`Communities / Voting`を探し、ページ上の位置（ユーザーが投票する機能に対する相対位置など）にドラッグします。

必要な情報については、[コミュニティコンポーネントの基本](basics.md)を参照してください。

[必須のクライアント側ライブラリ](essentials-voting.md#essentials-for-client-side)を含めると、`Voting`コンポーネントは次のように表示されます。

![chlimage_1-307](assets/chlimage_1-307.png)

## 投票の設定 {#configuring-voting}

配置済みの`Voting`コンポーネントを選択し、`Configure`アイコンを選択すると、編集ダイアログが開きます。

![chlimage_1-308](assets/chlimage_1-308.png)

「**[!UICONTROL テキストとラベル]**」タブで、投票の記録に使用するプロパティを指定します。

![chlimage_1-309](assets/chlimage_1-309.png)

* **[!UICONTROL 肯定的な返信ラベル]**
(
*必須*)肯定的な応答の内部プロパティ名。

* **[!UICONTROL 否定的な返信ラベル]**
(
*必須*)負の応答の内部プロパティ名。

* **[!UICONTROL 集計名]**
(
*必須*)投票コンポーネントのこのインスタンスの内部で識別可能なプロパティ名。

## サイト訪問者のエクスペリエンス {#site-visitor-experience}

### メンバー {#members}

メンバーが投票できるのは 1 回だけですが、いつでも投票を変更できます。

### 匿名 {#anonymous}

匿名での投票はサポートされていません。サイト訪問者が1回投票に参加するには、登録（メンバーになる）し、サインインする必要があります。

## 追加情報 {#additional-information}

詳しくは、開発者向けの[投票の基本事項](essentials-voting.md)ページを参照してください。
