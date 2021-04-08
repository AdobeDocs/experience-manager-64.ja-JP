---
title: Autodesk Maya および Mental Ray での IBL ステージの設定
seo-title: Autodesk Maya および Mental Ray での IBL ステージの設定
description: Autodesk Maya および Mental Ray での IBL ステージの設定方法
seo-description: Autodesk Maya および Mental Ray での IBL ステージの設定方法
uuid: 353ff561-0d30-4d62-8cad-68890c883c92
contentOwner: Rick Brough
topic-tags: 3D
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/ASSETS
discoiquuid: 752e521f-198f-425a-abfa-051993f9c694
exl-id: ecb489e2-fd6f-4163-9739-5d7ff497d305
feature: 3D アセット
role: Administrator,Business Practitioner
translation-type: tm+mt
source-git-commit: 13eb1d64677f6940332a2eeb4d3aba2915ac7bba
workflow-type: tm+mt
source-wordcount: '543'
ht-degree: 74%

---

# Autodesk Maya および Mental Ray での IBL ステージの設定 {#setting-up-an-ibl-stage-with-autodesk-maya-and-mental-ray}

1. Maya で、新しい空のシーンを作成します。

1. 表現モデルへの（一時的な）参照を作成します。これにより、ライティングの評価、カメラの設定、レンダラーの設定が容易になります。
1. Image-Based Lighting を設定します。

   1. **[!UICONTROL Render Settings]**&#x200B;で、「**[!UICONTROL Render Render Using:mental ray]**&#x200B;を開き、[シーン]タブを開きます。
   1. **[!UICONTROL レンダリング環境]**&#x200B;アコーディオンを開き、**[!UICONTROL [レンダリング] [イメージベースの照明を作成]]**&#x200B;をクリックします。
   1. ボックスの左側に右向き矢印の付いたボックスアイコンをクリックしてIBLノード`mentalRayIblShape1`を選択し、**[!UICONTROL レンダリング設定]**&#x200B;を終了します。
   1. **[!UICONTROL アトリビュートエディタ]**&#x200B;で、トランスフォームノード`mentalRayIbl1`を選択し、トランスフォームノードの名前を`AdobeIbl`に変更します。
   1. 環境球体がこのステージで表示する最大の 3D オブジェクトよりも十分に大きくなるように、ノードのスケールを設定します（`10000,10000,10000` など）。
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

   **[!UICONTROL レンダリング設定]**&#x200B;を次の推奨値で構成します。

   * **** 共通タブ

      **[!UICONTROL すべての**[!UICONTROL &#x200B;レンダリング可能なカメラ&#x200B;]**の「アルファチャネル（マスク）]**」チェックボックスをオフにします。

   * **[!UICONTROL 「画質」タブ]**

      * **全般の画質** - `0.5` 以下
      * **間接拡散(GI)モード** -  `Final Gather`
      * **フィルタサイズ** -  `2.0`、  `2.0`
   * 使用する一般的な画像サイズでシーンをレンダリングします。必要に応じて、ライトを絞り込むか、レンダリング設定をおこなうか、またはその両方をおこないます。

      Mental Ray でレンダリングする場合、Image-Based Lighting を使用すると、処理が非常に遅くなり、CPU 使用率が高くなることに注意してください。必要なレンダリング品質を保てる最低の画質設定を使用することをお勧めします。


1. 手順 2 で作成した参照を削除します。

1. シーンを保存し、Autodesk Maya を終了します。

1. シーンおよび IBL PTIFF を AEM にアップロードし、アップロード処理が完了するのを待機します。

   [アセットのアップロード](managing-assets-touch-ui.md#uploading-assets)を参照してください。

1. ファイルの依存関係を解決します。

   [ファイルの依存関係の解決](resolve-file-dependencies.md)を参照してください。

   AEM 3D は、ステージに設定されている IBL 画像を検出できない場合があります。そのような場合は、不足している依存関係を手動で解決する必要があります。不足しているそれぞれの依存関係に、既にアップロードしているのと同じ IBL PTIFF 画像を割り当てることができます。または、別の画像を割り当てて、さらに IBL エフェクトを制御することもできます。依存関係を解決したら、「**[!UICONTROL 保存]**」をタップして、再処理を開始します。

1. AEM でアセットのプロパティを開きます。**[!UICONTROL タイトル]**&#x200B;を、**[!UICONTROL ステージセレクター]**&#x200B;ドロップダウンリストに表示される適切な文字列に設定します。 「**[!UICONTROL クラス]**」が「**[!UICONTROL 3D ステージ]**」に設定されていることを確認します。保存して終了します。

1. 3D アセットを開き、新しいステージを選択して、予期したとおりにプレビューされ、レンダリングされることを確認します。
