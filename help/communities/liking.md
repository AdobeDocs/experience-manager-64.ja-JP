---
title: 「いいね!」設定の使用
seo-title: Using Liking
description: 「いいね!」設定コンポーネントの追加と設定
seo-description: Adding and configuring the Liking component
uuid: 12103ab7-1a1c-49cd-8dad-6c7508b4550e
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.4/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: dcde4e03-78ab-4779-96a1-05ac41f14701
exl-id: b5918a54-ef7b-4b3f-bca7-ed0344bab4aa
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 30%

---

# 「いいね!」設定の使用 {#using-liking}

この `Liking`コンポーネントは、フォーラム内のコメントなど、コンテンツの特定の部分に関する意見をユーザーが表現できる便利なツールです。 を使用 `Liking`コンポーネント、メンバーは、肯定的な意見を示す心アイコンを選択します。

## ページへの「いいね!」設定の追加 {#adding-liking-to-a-page}

を追加するには、以下を実行します。 `Liking` コンポーネントをオーサリングモードでページに追加する場合は、コンポーネントブラウザーを使用して

* `Communities / Liking`

を探し、ページ上の適切な位置（ユーザーに「いいね!」してもらう機能の近くなど）にドラッグします。

必要な情報については、 [コミュニティコンポーネントの基本](basics.md).

次の場合に [必要なクライアント側ライブラリ](essentials-liking.md#essentials-for-client-side) が含まれる場合、この方法で `Liking` コンポーネントが表示されます。

![chlimage_1-93](assets/chlimage_1-93.png)

## 「いいね!」の設定 {#configuring-liking}

配置された `Liking` アクセスして選択するコンポーネント `Configure` 編集ダイアログを開くアイコン。

![chlimage_1-94](assets/chlimage_1-94.png)

以下 **[!UICONTROL テキストとラベル]** 「 」タブで、「いいね！」の記録に使用するプロパティを指定します。

![chlimage_1-95](assets/chlimage_1-95.png)

* **[!UICONTROL 肯定的な返信ラベル]**
(
*必須*) 肯定的な応答のプロパティ名。

* **[!UICONTROL 否定的な返信ラベル]**
(
*必須*) 否定的な応答のプロパティ名。

* **[!UICONTROL 集計名]**
(
*必須*) 投票コンポーネントのこのインスタンスの内部で識別可能なプロパティ名。

## サイト訪問者のエクスペリエンス {#site-visitor-experience}

### メンバー {#members}

メンバーは、いつでも「いいね!」を変更できます。

### 匿名 {#anonymous}

匿名での「いいね!」はサポートされていません。Site visitors must register (become a member) and sign in to participate in liking.

## 追加情報 {#additional-information}

詳しくは、 [「いいね！」の設定の基本事項](essentials-liking.md) 開発者向けのページ
