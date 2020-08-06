---
title: 評価の使用
seo-title: 評価の使用
description: 評価コンポーネントをページに追加
seo-description: 評価コンポーネントをページに追加
uuid: a986970b-1221-4648-9a69-410f4480e0ae
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.4/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: a0e5491e-66bc-47b0-94a5-45a02bc558da
translation-type: tm+mt
source-git-commit: 63001012f0d865c2548703ea387c780679128ee7
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 39%

---


# 評価の使用 {#using-ratings}

The `Rating`component is used standalone or in conjunction with other Communities features. ここでは、ログインコミュニティのメンバーが、コンテンツを評価することで意見を述べることを可能にします。

## 評価をページに追加 {#adding-a-rating-to-a-page}

作成者モードで `Rating`コンポーネントをページに追加するには、コンポーネントを見つけ `Communities / Rating` てページ上の位置（メンバーが評価する機能に対する相対位置など）にドラッグします。

For necessary information, visit [Communities Components Basics](basics.md).

[必要なクライアント側のライブラリが含まれる場合](rating-basics.md#essentials-for-client-side) 、これがコンポー `Rating` ネントの表示方法です。

![chlimage_1-493](assets/chlimage_1-493.png)

## 評価の設定 {#configuring-rating}

Select the placed `Rating` component to access and select the `Configure` icon which opens the edit dialog.

![chlimage_1-494](assets/chlimage_1-494.png)

「**[!UICONTROL テキストとラベル]**」タブでは、評価の内部識別子を指定できます。

![chlimage_1-495](assets/chlimage_1-495.png)

**[!UICONTROL Tally Name]**(*必須*)：このインスタンスを一意に識別す `Rating`る、の単純な名前。 リポジトリの有効なノード名を指定する必要があります。

## サイト訪問者のエクスペリエンス {#site-visitor-experience}

### メンバー {#members}

1 人のメンバーが付けられる評価は 1 つだけです。メンバーは、いつでも評価を変更できます。

### 匿名 {#anonymous}

匿名での評価投稿はサポートされていません。サイト訪問者は参加するには、登録（会員になる）し、サインインする必要があります。

## 追加情報 {#additional-information}

More information may be found on the [Rating Essentials](rating-basics.md) page for developers.
