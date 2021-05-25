---
title: ソーシャルグラフの使用
seo-title: ソーシャルグラフの使用
description: コンポーネントをページに追加
seo-description: コンポーネントをページに追加
uuid: 8be6334b-e6c9-40bc-90a8-750b98419470
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.4/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 0ce57ab1-e4c6-4c38-963d-556eef8757f2
exl-id: ab829d28-278d-4139-af16-edcc24b3d56b
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 23%

---

# ソーシャルグラフの使用 {#using-social-graph}

## はじめに {#introduction}

コミュニティメンバーが[アクティビティ](activities.md)をフォローし、フォローする機能は、次の2つのコンポーネントを通じて確立されます。`Follow`と`Following`が含まれます。

`Follow`コンポーネントは別のリソースに関連付ける必要があり、この関連付けはコミュニティのメンバーと機能に対して既に確立されています。

`Following`コンポーネントは、現在のメンバーをフォローしているメンバー、または現在のメンバーをフォローしているメンバーを一覧表示します。 このメンバー間の関係のソーシャルグラフは、[コミュニティサイト](overview.md#communitiessites)用に確立されたユーザープロファイルに含まれます。

## フォロー中コンポーネントをページに追加 {#adding-following-to-a-page}

オーサリングモードでページに`Following`コンポーネントを追加する場合は、コンポーネント`Communities / Following`を選択し、ソーシャルグラフが表示されるページ上の位置にドラッグします。

必要な情報については、[コミュニティコンポーネントの基本](basics.md)を参照してください。

[必須のクライアント側ライブラリ](essentials-socialgraph.md#essentials-for-client-side)を含めると、`Following`コンポーネントは次のように表示されます。

![chlimage_1-447](assets/chlimage_1-447.png)

## フォロー中コンポーネントの設定 {#configuring-following}

現在、コンポーネントが`follows`関係を表示するか、`following`関係を表示するかを指定するプロパティを設定する必要があります。

## 追加情報 {#additional-information}

詳しくは、開発者向けの[ソーシャルグラフの重要事項](essentials-socialgraph.md)ページを参照してください。
