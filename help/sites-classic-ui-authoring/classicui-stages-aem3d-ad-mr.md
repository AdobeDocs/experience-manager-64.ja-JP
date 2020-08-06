---
title: Autodesk Maya および Mental Ray での標準ステージの設定
seo-title: Autodesk Maya および Mental Ray での標準ステージの設定
description: Autodesk Maya および Mental Ray で標準ステージを設定する方法を学習します。
seo-description: Autodesk Maya および Mental Ray で標準ステージを設定する方法を学習します。
uuid: 05c4858b-6261-4de3-a87a-03dd6bc519a4
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.4/ASSETS
topic-tags: authoring
content-type: reference
discoiquuid: f30c4039-3bbf-4d02-a9b5-bda6ccce16b9
translation-type: tm+mt
source-git-commit: e0ce860380a28a9dcaa6f8ce94ad278cdbe49fad
workflow-type: tm+mt
source-wordcount: '433'
ht-degree: 81%

---


# Autodesk Maya および Mental Ray での標準ステージの設定{#setting-up-a-standard-stage-with-autodesk-maya-and-mental-ray}

1. Maya で、新しい空のシーンを作成します。
1. 表現モデルへの（一時的な）参照を作成します。これにより、ライティングの評価、カメラの設定、レンダラーの設定が容易になります。

1. 通常どおりライトを追加します。現在、AEM 3D では、以下のタイプのライトがサポートされています。

   * 指向性ライト
   * スポットライト
   * ポイントライト

   他のタイプのライトは無視され、ステージが AEM 3D にアップロードされるときに、上記のサポートされているいずれかのタイプに変換されます。アセットを表示する場合、および組み込みの Rapid Refine レンダラーを使用する場合、変換されたタイプが使用されます。Mayaでレンダリングする際には、オリジナルのライトタイプが使用されます。

1. 必要に応じて、グラウンドプレーンを作成し、適切な素材を適用します。

   グラウンドプレーンは、片面として設定することをお勧めします。これにより、アセットを地面に隠さずに、AEM 3Dの下からアセットを表示できます。

1. （オプション）カメラを作成して設定します。

   アセットを挿入するシーンの中心の「方向」にカメラを向けます。カメラはレンダリング可能に設定します。

1. Mental Ray でレンダリングを設定します。

   Configure the **[!UICONTROL Render Settings]** with the following suggestions:

   * **[!UICONTROL 共通]** タブ

      Deselect the **[!UICONTROL Alpha channel (mask)]** check box for all [!UICONTROL Renderable Cameras].

   * **[!UICONTROL 「画質」タブ]**

      * **[!UICONTROL 全体的なクォリティ]**`- 0.5` 以下
      * **[!UICONTROL 間接拡散(GI)モード]** - `Final Gather`
      * **[!UICONTROL フィルタサイズ]** - `2.0`、 `2.0`
   * 使用する一般的な画像サイズでシーンをレンダリングします。If necessary, refine the lights, or [!UICONTROL Render settings], or do both to achieve the results you want.

      Mental Ray でレンダリングする場合、Image-Based Lighting を使用すると、処理が非常に遅くなり、CPU 使用率が高くなることに注意してください。必要なレンダリング品質を保てる最低の画質設定を使用することをお勧めします。


1. 手順 2 で作成した参照を削除します。
1. シーンを保存し、Autodesk Maya を終了します。
1. シーンを AEM にアップロードし、アップロード処理が完了するのを待ちます。

   [アセットのアップロード](/help/assets/managing-assets-touch-ui.md#uploading-assets)を参照してください。

   Autodesk® Maya® が AEM サーバー上で設定されていない場合は、Maya から FBX を書き出して、AEM にアップロードします。

1. AEM でアセットのプロパティを開きます。タイトルを、ステージセレクターのドロップダウンリストに表示される適切な文字列に設定します。「**[!UICONTROL クラス]**」が「**[!UICONTROL 3D ステージ]**」に設定されていることを確認します。保存して終了します。
1. 3D アセットを開き、新しいステージを選択して、予期したとおりにプレビューされ、レンダリングされることを確認します。

