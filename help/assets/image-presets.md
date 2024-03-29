---
title: Dynamic Media画像プリセットの適用
seo-title: Applying Dynamic Media image presets
description: Dynamic Media での画像プリセットの適用方法を説明します
seo-description: Learn how to apply image presets in Dynamic Media
uuid: 8bafcbd0-6df0-4d5b-b2f7-116ddb4ec060
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.4/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: 5c1f60ac-3741-4002-9c5d-c128f118342b
exl-id: 07a4f315-a60e-456b-b02d-035b3f6ad9ad
feature: Image Presets
role: User
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 69%

---

# Dynamic Media画像プリセットの適用 {#applying-image-presets}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

画像プリセットを使用すると、Assets は異なるサイズや異なる形式の画像、あるいは動的に生成された他の画像プロパティを設定した画像を動的に配信できます。画像を書き出す際にプリセットを選択できます。また、管理者が指定した仕様に合わせて画像が再フォーマットされます。

さらに、レスポンシブな画像プリセットを選択することもできます（画像プリセットを選択したら「**[!UICONTROL RESS]**」ボタンを使用して指定します）。

この節では、画像プリセットの使用方法について説明します。 [画像プリセットの作成と設定は管理者が行うことができます](managing-image-presets.md)。

>[!NOTE]
>
>スマートイメージングは、既存の画像プリセットで機能し、配信の直前にインテリジェンスを使用して、ブラウザーまたはネットワークの接続速度に基づいて画像のファイルサイズをさらに低減します。詳しくは、[スマートイメージング](imaging-faq.md)を参照してください。

作成者は画像をプレビューするときに、いつでも画像プリセットを適用できます。

**Dynamic Media画像プリセットを適用するには：**:

1. アセットを開き、左側のレールでドロップダウンメニューをタップして、「**[!UICONTROL レンディション]**」をタップします。

   >[!NOTE]
   >
   >* 静的レンディションは、パネルの上半分に表示されます。 動的レンディションは下半分に表示されます。動的レンディションのみの場合は、URL を使用して画像を表示できます。「**[!UICONTROL URL]**」ボタンは、動的レンディションを選択した場合にのみ表示されます。「**[!UICONTROL RESS]**」ボタンは、レスポンシブ画像プリセットを選択した場合にのみ表示されます。
   >
   >* 「 **[!UICONTROL レンディション]** （アセットの詳細表示） 表示されるプリセットの数を増やすことができます。[表示される画像プリセット数の引き上げ](managing-image-presets.md#increasing-or-decreasing-the-number-of-image-presets-that-display)を参照してください。


   ![chlimage_1-208](assets/chlimage_1-208.png)

1. 次のいずれかの操作を行います。

   * 動的レンディションを選択して、画像プリセットをプレビューします。
   * 「**[!UICONTROL URL]**」、「**[!UICONTROL 埋め込み]**」または「**[!UICONTROL RESS]**」をタップして、ポップアップを表示します。

   >[!NOTE]
   >
   >アセット&#x200B;*と*&#x200B;画像プリセットがまだ公開されていない場合、「**[!UICONTROL URL]**」ボタン（または該当する場合は「**[!UICONTROL URL]**」ボタンと「**[!UICONTROL RESS]**」ボタン）は使用できません。
   >
   >また、Dynamic Media サーバーでは画像プリセットが自動的に公開されることにも注意が必要です。
