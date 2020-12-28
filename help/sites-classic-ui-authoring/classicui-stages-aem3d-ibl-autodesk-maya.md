---
title: Autodesk Maya および Mental Ray での IBL ステージの設定
seo-title: Autodesk Maya および Mental Ray での IBL ステージの設定
description: Autodesk Maya および Mental Ray で IBL ステージを設定する方法を学習します。
seo-description: Autodesk Maya および Mental Ray で IBL ステージを設定する方法を学習します。
uuid: 99878112-74c1-4a52-a7c2-c39927ce0e2a
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.4/ASSETS
topic-tags: authoring
content-type: reference
discoiquuid: 00f7ed25-276b-42c2-ae4c-11de357a9ec6
translation-type: tm+mt
source-git-commit: e0ce860380a28a9dcaa6f8ce94ad278cdbe49fad
workflow-type: tm+mt
source-wordcount: '541'
ht-degree: 75%

---


# Autodesk Maya および Mental Ray での IBL ステージの設定{#setting-up-an-ibl-stage-with-autodesk-maya-and-mental-ray}

1. Maya で、新しい空のシーンを作成します。

1. 表現モデルへの（一時的な）参照を作成します。これにより、ライティングの評価、カメラの設定、レンダラーの設定が容易になります。
1. Image-Based Lighting を設定します。

   1. レンダラー設定で、「**[!UICONTROL 次を使用してレンダリング：Mental Ray]**」を選択し、「シーン」タブを開きます。****
   1. **[!UICONTROL 環境]**&#x200B;アコーディオンを開き、**[!UICONTROL イメージベースの照明を作成]**&#x200B;をクリックします。
   1. ボックスの左側に右向き矢印の付いたボックスアイコンをクリックしてIBLノード`mentalRayIblShape1`を選択し、[!UICONTROL レンダリング設定]を終了します。
   1. **[!UICONTROL アトリビュートエディタ]**&#x200B;で、トランスフォームノード`mentalRayIbl1`を選択し、トランスフォームノードの名前を`AdobeIbl`に変更します。

   1. ノードの[!UICONTROL スケール]を設定して、環境球をこのステージで表示する最大の3Dオブジェクト（例：`10000,10000,10000`）より大きくします。
   1. `AdobeIblShape` ノードを選択して、以下のように設定します。

      * **[!UICONTROL マッピング]** - 球体
      * **[!UICONTROL タイプ]** - 画像ファイル
      * **[!UICONTROL 光の放射]** - true
   1. 必要な32ビットTIFF画像を`AdobeIbl`ノードに添付します。


1. グラウンドプレーンを設定します。

   * グラウンドプレーンとして使用する適切なプレーンを作成し、IBL 球体内に収まるサイズに設定して、座標原点を通るように配置します。
   * **[!UICONTROL 背景]**&#x200B;マテリアルを地表面にアタッチし、`AdobeUseBackground`と名前を付けて地表面オブジェクトにアタッチします。

1. （オプション）カメラを作成して設定します。

   アセットを挿入するシーンの中心の「方向」にカメラを向けます。カメラはレンダリング可能に設定します。

1. Mental Ray でレンダリングを設定します。

   [!UICONTROL レンダリング設定]を次の推奨値で構成します。

   * **** 共通タブ

      すべてのレンダリング可能なカメラの&#x200B;**[!UICONTROL アルファチャネル（マスク）]**&#x200B;チェックボックスをオフにします。

   * **[!UICONTROL 「画質」タブ]**

      * **[!UICONTROL 全般の画質]** - `0.5` 以下
      * **[!UICONTROL 間接拡散(GI)モード]** -  `Final Gather`
      * **[!UICONTROL フィルタサイズ]** -  `2.0`、  `2.0`
   * 使用する一般的な画像サイズでシーンをレンダリングします。必要に応じて、ライトを絞り込むか、レンダリング設定をおこなうか、またはその両方をおこないます。

      Mental Ray でレンダリングする場合、Image-Based Lighting を使用すると、処理が非常に遅くなり、CPU 使用率が高くなることに注意してください。必要なレンダリング品質を保てる最低の画質設定を使用することをお勧めします。


1. 手順 2 で作成した参照を削除します。

1. シーンを保存し、Autodesk Maya を終了します。

1. シーンおよび IBL PTIFF を AEM にアップロードし、アップロード処理が完了するのを待機します。

   [アセットのアップロード](/help/assets/managing-assets-touch-ui.md#uploading-assets)を参照してください。

1. ファイルの依存関係を解決します。

   [ファイルの依存関係の解決](/help/sites-classic-ui-authoring/classicui-upload-proc-3d-resolve-dependencies.md)を参照してください。

   AEM 3D は、ステージに設定されている IBL 画像を検出できない場合があります。そのような場合は、不足している依存関係を手動で解決する必要があります。不足しているそれぞれの依存関係に、既にアップロードしているのと同じ IBL PTIFF 画像を割り当てることができます。または、別の画像を割り当てて、さらに IBL エフェクトを制御することもできます。依存関係を解決したら、「**保存**」をタップして、再処理を開始します。

1. AEM でアセットのプロパティを開きます。タイトルを、ステージセレクターのドロップダウンリストに表示される適切な文字列に設定します。「**[!UICONTROL クラス]**」が「**[!UICONTROL 3D ステージ]**」に設定されていることを確認します。保存して終了します。

1. 3D アセットを開き、新しいステージを選択して、予期したとおりにプレビューされ、レンダリングされることを確認します。

