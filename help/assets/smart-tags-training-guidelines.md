---
title: スマートコンテンツサービスのトレーニングガイドライン
description: アセットにスマートタグを適用するための AI サービスのトレーニング
products: SG_EXPERIENCEMANAGER/6.4/ASSETS
uuid: 1c011496-be6e-470b-9da8-48db8c6d1108
contentOwner: AG
discoiquuid: a5aab094-8b2d-4a23-890f-be6f9e5137bd
feature: Tagging,Metadata,Smart Tags
role: User
exl-id: 14241f8d-fd0b-4bcf-b2bb-1d0e52bf7748
source-git-commit: a778c3bbd0e15bb7b6de2d673b4553a7bd146143
workflow-type: tm+mt
source-wordcount: '455'
ht-degree: 89%

---

# スマートコンテンツサービスのトレーニングガイドライン {#smart-content-service-training-guidelines}

To be able to effectively tag your brand images, the Smart Content Service requires that the training images conform to certain guidelines.

## トレーニングのガイドライン {#guidelines-for-training}

最適な結果を得るには、トレーニングセット内の画像は次のガイドラインに従う必要があります。

**Quantity and size:** Minimum **30 images per tag**. 長辺が 500 ピクセル以上である必要があります。

**一貫性**：タグの各画像は、似たような外観にする必要があります。

例えば、以下の画像は似ていないので、これらの画像すべてを my-party **（トレーニング用）としてタグ付けするのは適切ではありません。

![トレーニングガイドラインの例を示すイラスト](assets/do-not-localize/coherence.png)

**対象範囲**：トレーニングの画像には十分な多様性が必要です。[!DNL Experience Manager] が適切に焦点を当てることを学習できるよう、数は少なくても多様性の高い例を提供します。見た目が大きく異なる画像に同じタグを適用する場合は、それぞれの種類に 5 つ以上の例を含めてください。

例えば、*model-down-pose* というタグの場合、タグ付け時、類似する画像をより正確に識別できるよう、以下のハイライト表示された画像に似たトレーニング画像を増やします。

![トレーニングガイドラインの例を示すイラスト](assets/do-not-localize/coverage_1.png)

**妨害物と障害物**：サービスのトレーニングには、障害物（目立つ背景、メインとなる対象と一緒に含まれる物や人物などの関連性のない付随物）が少ない画像のほうが効果的です。

例えば、*casual-shoe* というタグの場合、2 つ目の画像はトレーニングの候補として適切ではありません。

![トレーニングガイドラインの例を示すイラスト](assets/do-not-localize/distraction.png)

**完全性**：画像が複数のタグの対象となる場合は、適用可能なすべてのタグを追加してから、画像をトレーニングに含めます。例えば、*raincoat* と *model-side-view* などのタグの場合、対象となるアセットに両方のタグを追加してから、そのアセットをトレーニングに含めます。

![トレーニングガイドラインの例を示すイラスト](assets/do-not-localize/completeness.png)

## 制限事項 {#limitations}

拡張スマートタグは、ブランド画像とそのタグの学習モデルに基づいています。これらのモデルは、タグを識別するうえで常に完璧であるわけではありません。スマートコンテンツサービスの現行バージョンには次の制限事項があります。

* 画像内の細かい違いを認識することはできません。例えば、シャツのサイズが細身か標準かなどの違いは認識できません。
* 画像の細かい模様や部分に基づいてタグを識別することはできません。例えば、T シャツのロゴなどです。
* タグ付けは、 [!DNL Experience Manager] はでサポートされています。 言語の一覧については、](/help/release-notes/smart-content-service-release-notes.md)スマートコンテンツサービスのリリースノート[を参照してください。

スマートタグ（通常または拡張）付きのアセットを検索するには、アセットのオムニサーチ（全文検索）を使用します。スマートタグには個別の検索用述語はありません。

>[!NOTE]
>
>スマートコンテンツサービスでタグのトレーニングを実施し、それらのタグを他の画像に適用できるかどうかは、トレーニングで使用する画像の質によって決まります。
>
>最適な結果を得るには、視覚的に似ている画像を使用し、それぞれのタグについてサービスのトレーニングを実施することをお勧めします。
