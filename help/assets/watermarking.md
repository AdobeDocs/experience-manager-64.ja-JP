---
title: 画像の透かし
description: 透かし機能を使用して、PNG画像とJPEG画像に電子透かしを追加します。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 0e0e2aa693c30c8e1ef1033b936b82d83e5b348e

---


# アセットの透かし {#watermarking}

Adobe Experience Manager (AEM)Assetsを使用すると、画像に電子透かしを追加して、アセットの信頼性と著作権の所有権を確認できます。 AEM Assets では、PNG および JPEG ファイル上の透かしとしてテキストを使用できます。

To be able to apply watermark on assets, add the [!UICONTROL Watermark] step in the [!UICONTROL DAM Update Asset] workflow.

1. Tap the AEM logo, and go to **[!UICONTROL Tools]** > **[!UICONTROL Workflow]** > **[!UICONTROL Models]**.
1. From the Workflow Models page, select the **[!UICONTROL DAM Update Asset]** workflow and click **[!UICONTROL Edit]**.

1. From the side panel, drag the **[!UICONTROL Add Watermark]** step and add it to the [!UICONTROL DAM Update Asset] workflow.

   ![「DAM アセットの更新」ワークフローへの「透かしを追加」ステップのドラッグ](assets/add_watermark_step_aem_assets.png)

   >[!NOTE]
   >
   >Place the [!UICONTROL Add Watermark] step anywhere before the [!UICONTROL Process Thumbnail] step.

1. 「**[!UICONTROL 透かしを追加]**」ステップを開いて、プロパティを表示します。
1. 「**[!UICONTROL 引数]**」タブで、各種フィールド（テキスト、フォントタイプ、サイズ、カラー、位置、向きなど）に有効な値を指定します。変更を確定するために、完了アイコンをタップまたはクリックします。

   ![Assets における「透かしを追加」ステップの引数の指定](assets/arguments_add_watermark_aem_assets.png)

1. 透かしステップを追加した **[!UICONTROL DAM アセットの更新]**&#x200B;ワークフローを保存します。
1. AEMユーザーインターフェイスから、サンプルアセットをアップロードします。 上記の手順で設定した位置に、フォントサイズや色などの透かしが表示されます。
