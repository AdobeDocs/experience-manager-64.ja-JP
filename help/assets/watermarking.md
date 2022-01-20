---
title: デジタルアセットへの透かしの追加
description: 透かし処理機能を使用して、アセットにデジタル透かしを追加する方法について説明します。
contentOwner: AG
feature: Asset Management
role: User,Admin
exl-id: ed01143c-b516-44f8-aceb-ad2e3f0106b2
source-git-commit: 1e3cd6ce3138113721183439f7cfb9daed6e0e58
workflow-type: tm+mt
source-wordcount: '319'
ht-degree: 36%

---

# デジタルアセットの透かしの設定 {#watermarking}

[!DNL Adobe Experience Manager Assets] では、アセットにデジタル透かしを追加し、アセットの信頼性や著作権の所有権を確認できます。 [!DNL Experience Manager Assets] では、PNG および JPEG ファイル上の透かしとしてテキストを使用できます。

Adobe Experience Manager Assets では、画像に電子透かしを追加して、アセットの信頼性と著作権の所有権を確認できます。 [!DNL Experience Manager] Assets では、PNG および JPEG ファイル上の透かしとしてテキストを使用できます。

アセットに透かしを適用するには、 [!UICONTROL DAM アセットの更新] ワークフロー。

1. 次にアクセス： [!DNL Experience Manager] ユーザインターフェイスに移動し、に移動します。 **[!UICONTROL ツール]** > **[!UICONTROL ワークフロー]** > **[!UICONTROL モデル]**.
1. ワークフローモデルページで、**[!UICONTROL DAM アセットの更新]**&#x200B;ワークフローを選択し、「**[!UICONTROL 編集]**」をクリックします。

1. サイドパネルから、 **[!UICONTROL 透かしを追加]** 手順を実行し、 [!UICONTROL DAM アセットの更新] ワークフロー。

   ![「DAM アセットの更新」ワークフローに「透かしを追加」ステップをドラッグします](assets/add_watermark_step_aem_assets.png)

   >[!NOTE]
   >
   >を [!UICONTROL 透かしを追加] 前の任意の場所に進む [!UICONTROL サムネールを処理] 手順

1. 「**[!UICONTROL 透かしを追加]**」ステップを開いて、プロパティを表示します。
1. 「**[!UICONTROL 引数]**」タブで、各種フィールド（テキスト、フォントタイプ、サイズ、カラー、位置、向きなど）に有効な値を指定します。変更を確定するには、 **[!UICONTROL 完了]**.

   ![Assets における「透かしを追加」ステップの引数の指定](assets/arguments_add_watermark_aem_assets.png)

1. 透かしステップを追加した **[!UICONTROL DAM アセットの更新]**&#x200B;ワークフローを保存します。
1. 次の [!DNL Experience Manager] ユーザーインターフェイスで、サンプルアセットをアップロードします。 透かしは、フォントサイズ、色などと共に、上記の手順で設定した位置に表示されます。

プログラムでPDFドキュメントに透かしを付ける場合や動的情報を使用する場合は、 [[!DNL Experience Manager] ドキュメントサービス](/help/forms/using/overview-aem-document-services.md) 提供

## ヒントと制限事項 {#tips-limitations}

* テキストベースの透かしのみがサポートされます。 画像は、 [!UICONTROL 透かしの追加プロセス].
* 透かしの使用は、PNG ファイルとJPEGファイルのみサポートされています。 その他のアセット形式には透かしは入りません。
