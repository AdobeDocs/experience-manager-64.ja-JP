---
title: 画像の透かし
description: 透かし機能を使用して、PNG画像とJPEG画像に電子透かしを追加します。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 04de28347ddf0082d2e224aa3853297cad3aacd8
workflow-type: tm+mt
source-wordcount: '247'
ht-degree: 41%

---


# アセットの透かしの設定 {#watermarking}

Adobe Experience Manager(AEM)アセットを使用すると、画像に電子透かしを追加できます。これにより、アセットの信頼性と著作権の所有権を検証できます。 AEM Assets では、PNG および JPEG ファイル上の透かしとしてテキストを使用できます。

アセットに透かしを適用するには、[!UICONTROL DAM Update Asset]ワークフローの[!UICONTROL Watermark]手順を追加します。

1. AEMのロゴをタップし、**[!UICONTROL ツール]**/**[!UICONTROL ワークフロー]**/**[!UICONTROL モデル]**&#x200B;に移動します。
1. ワークフローモデルページで、**[!UICONTROL DAM アセットの更新]**&#x200B;ワークフローを選択し、「**[!UICONTROL 編集]**」をクリックします。

1. サイドパネルから、追加&#x200B;**[!UICONTROL 透かし]**&#x200B;ステップをドラッグし、[!UICONTROL DAM更新アセット]ワークフローに追加します。

   ![「DAM アセットの更新」ワークフローへの「透かしを追加」ステップのドラッグ](assets/add_watermark_step_aem_assets.png)

   >[!NOTE]
   >
   >[!UICONTROL 透かし追加]ステップを[!UICONTROL サムネールを処理]ステップの前の任意の場所に配置します。

1. 「**[!UICONTROL 透かしを追加]**」ステップを開いて、プロパティを表示します。
1. 「**[!UICONTROL 引数]**」タブで、各種フィールド（テキスト、フォントタイプ、サイズ、カラー、位置、向きなど）に有効な値を指定します。変更を確定するために、完了アイコンをタップまたはクリックします。

   ![Assets における「透かしを追加」ステップの引数の指定](assets/arguments_add_watermark_aem_assets.png)

1. 透かしステップを追加した **[!UICONTROL DAM アセットの更新]**&#x200B;ワークフローを保存します。
1. AEMユーザーインターフェイスから、サンプルアセットをアップロードします。 上記の手順で設定した位置に、フォントサイズ、色などの透かしが表示されます。

プログラム的に、または動的な情報を使用してPDFドキュメントに透かしを付けるには、[AEMドキュメントサービス](/help/forms/using/overview-aem-document-services.md)オファーを使用することを検討してください。
