---
title: 「いいね!」設定の使用
seo-title: 「いいね!」設定の使用
description: 「いいね!」設定コンポーネントの追加と設定
seo-description: 「いいね!」設定コンポーネントの追加と設定
uuid: 12103ab7-1a1c-49cd-8dad-6c7508b4550e
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.4/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: dcde4e03-78ab-4779-96a1-05ac41f14701
exl-id: b5918a54-ef7b-4b3f-bca7-ed0344bab4aa
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '234'
ht-degree: 32%

---

# 「いいね!」設定の使用  {#using-liking}

`Liking`コンポーネントは、フォーラム内のコメントなど、コンテンツの特定の部分に関する意見を伝えるのに役立つツールです。 `Liking`コンポーネントを使用して、メンバーは心アイコンを選択し、肯定的な意見を示します。

## ページへの「いいね!」設定の追加 {#adding-liking-to-a-page}

`Liking`コンポーネントをオーサリングモードでページに追加するには、コンポーネントブラウザーを使用して

* `Communities / Liking`

を探し、ページ上の適切な位置（ユーザーに「いいね!」してもらう機能の近くなど）にドラッグします。

必要な情報については、[コミュニティコンポーネントの基本](basics.md)を参照してください。

[必須のクライアント側ライブラリ](essentials-liking.md#essentials-for-client-side)を含めると、`Liking`コンポーネントは次のように表示されます。

![chlimage_1-93](assets/chlimage_1-93.png)

## 「いいね!」の設定{#configuring-liking}

配置済みの`Liking`コンポーネントを選択し、`Configure`アイコンを選択すると、編集ダイアログが開きます。

![chlimage_1-94](assets/chlimage_1-94.png)

「**[!UICONTROL テキストとラベル]**」タブで、「いいね！」の記録に使用するプロパティを指定します。

![chlimage_1-95](assets/chlimage_1-95.png)

* **[!UICONTROL 肯定的な返信ラベル]**
(
*必須*)肯定的な応答のプロパティ名。

* **[!UICONTROL 否定的な返信ラベル]**
(
*必須*)負の応答のプロパティ名。

* **[!UICONTROL 集計名]**
(
*必須*)投票コンポーネントのこのインスタンスの内部で識別可能なプロパティ名。

## サイト訪問者のエクスペリエンス {#site-visitor-experience}

### メンバー {#members}

メンバーは、いつでも「いいね!」を変更できます。

### 匿名 {#anonymous}

匿名での「いいね!」はサポートされていません。サイト訪問者が「いいね！」を設定するには、登録（メンバーになる）してサインインする必要があります。

## 追加情報 {#additional-information}

詳しくは、開発者向けの[「いいね！」の基本事項](essentials-liking.md)ページを参照してください。
