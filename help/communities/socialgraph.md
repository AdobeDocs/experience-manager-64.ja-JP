---
title: ソーシャルグラフの使用
seo-title: Using Social Graph
description: ページへのフォローコンポーネントの追加
seo-description: Adding a Following component to a page
uuid: 8be6334b-e6c9-40bc-90a8-750b98419470
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.4/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 0ce57ab1-e4c6-4c38-963d-556eef8757f2
exl-id: ab829d28-278d-4139-af16-edcc24b3d56b
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '187'
ht-degree: 5%

---

# ソーシャルグラフの使用 {#using-social-graph}

## はじめに {#introduction}

コミュニティメンバーがフォローする機能 [アクティビティ](activities.md) それに続くものは、次の 2 つの構成要素を通じて確立されます。 `Follow`および `Following`.

この `Follow`コンポーネントは別のリソースに関連付ける必要があり、この関連付けはコミュニティのメンバーと機能に対して既に確立されています。

この `Following`コンポーネントは、現在のメンバーをフォローしているメンバー、または現在のメンバーの後に続いているメンバーをリストします。 このメンバー間の関係のソーシャルグラフは、 [コミュニティサイト](overview.md#communitiessites).

## ページへのフォローの追加 {#adding-following-to-a-page}

必要に応じて `Following`コンポーネントをオーサリングモードでページに追加する場合は、 `Communities / Following` をドラッグし、ページ上のソーシャルグラフを表示する場所にドラッグします。

必要な情報については、 [コミュニティコンポーネントの基本](basics.md).

次の場合に [必要なクライアント側ライブラリ](essentials-socialgraph.md#essentials-for-client-side) が含まれる場合、この方法で `Following` コンポーネントが表示されます。

![chlimage_1-447](assets/chlimage_1-447.png)

## フォローの設定 {#configuring-following}

現在、コンポーネントに `follows`関係、または `following`関係。

## 追加情報 {#additional-information}

詳しくは、 [ソーシャルグラフの基本事項](essentials-socialgraph.md) 開発者向けのページ
