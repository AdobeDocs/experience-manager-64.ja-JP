---
title: 評価の使用
seo-title: Using Ratings
description: 評価コンポーネントのページへの追加
seo-description: Adding a Rating component to a page
uuid: a986970b-1221-4648-9a69-410f4480e0ae
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.4/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: a0e5491e-66bc-47b0-94a5-45a02bc558da
exl-id: 1de28140-5334-4ca2-a476-5ad253809808
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 5%

---

# 評価の使用 {#using-ratings}

この `Rating`コンポーネントは、スタンドアロンで、または他のコミュニティ機能と組み合わせて使用されます。 このコンポーネントを使用すると、サインインしたコミュニティメンバーは、コンテンツを評価して意見を表明できます。

## ページへの評価の追加 {#adding-a-rating-to-a-page}

を追加するには、以下を実行します。 `Rating`コンポーネントをオーサリングモードでページに追加する場合は、 `Communities / Rating` をクリックし、ページ上の適切な位置（メンバーが評価する機能を基準とした位置など）にドラッグします。

必要な情報については、 [コミュニティコンポーネントの基本](basics.md).

次の場合に [必要なクライアント側ライブラリ](rating-basics.md#essentials-for-client-side) が含まれる場合、この方法で `Rating` コンポーネントが表示されます。

![chlimage_1-493](assets/chlimage_1-493.png)

## 評価の設定 {#configuring-rating}

配置された `Rating` アクセスして選択するコンポーネント `Configure` 編集ダイアログを開くアイコン。

![chlimage_1-494](assets/chlimage_1-494.png)

以下 **[!UICONTROL テキストとラベル]** 」タブでは、評価の内部識別子を指定します。

![chlimage_1-495](assets/chlimage_1-495.png)

**[!UICONTROL 集計名]**
(*必須*) `Rating`このインスタンスを一意に識別する リポジトリの有効なノード名を指定する必要があります。

## サイト訪問者エクスペリエンス {#site-visitor-experience}

### メンバー {#members}

メンバーごとに 1 つの評価のみが許可されます。 会員は、いつでも評価を変更することができます。

### 匿名 {#anonymous}

匿名での評価の投稿はサポートされていません。 サイト訪問者が参加するには、登録（メンバーになる）してサインインする必要があります。

## 追加情報 {#additional-information}

詳しくは、 [評価の基本事項](rating-basics.md) 開発者向けのページ
