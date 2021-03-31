---
title: デジタルアセットへの透かしの追加
description: 透かし処理機能を使用して、アセットにデジタル透かしを追加する方法について説明します。
contentOwner: AG
feature: アセット管理
role: 業務担当者、管理者
translation-type: tm+mt
source-git-commit: 29e3cd92d6c7a4917d7ee2aa8d9963aa16581633
workflow-type: tm+mt
source-wordcount: '328'
ht-degree: 36%

---


# デジタルアセットの透かし{#watermarking}

[!DNL Adobe Experience Manager Assets] アセットに電子透かしを追加できます。これにより、ユーザーはアセットの信頼性と著作権の所有権を検証できます。[!DNL Experience Manager Assets] では、PNG および JPEG ファイル上の透かしとしてテキストを使用できます。

Adobe Experience Manager(AEM)アセットを使用すると、画像に電子透かしを追加できます。これにより、アセットの信頼性と著作権の所有権を検証できます。 AEM Assets では、PNG および JPEG ファイル上の透かしとしてテキストを使用できます。

アセットに透かしを適用するには、[!UICONTROL DAM Update Asset]ワークフローで透かしを追加します。

1. [!DNL Experience Manager]ユーザーインターフェイスにアクセスし、**[!UICONTROL ツール]**/**[!UICONTROL ワークフロー]**/**[!UICONTROL モデル]**&#x200B;に移動します。
1. ワークフローモデルページで、**[!UICONTROL DAM アセットの更新]**&#x200B;ワークフローを選択し、「**[!UICONTROL 編集]**」をクリックします。

1. サイドパネルから、追加&#x200B;**[!UICONTROL 透かし]**&#x200B;ステップをドラッグし、[!UICONTROL DAM更新アセット]ワークフローに追加します。

   ![DAM更新アセットワークフローの透かしの追加手順をドラッグします](assets/add_watermark_step_aem_assets.png)

   >[!NOTE]
   >
   >[!UICONTROL 透かし追加]ステップを[!UICONTROL サムネールを処理]ステップの前の任意の場所に配置します。

1. 「**[!UICONTROL 透かしを追加]**」ステップを開いて、プロパティを表示します。
1. 「**[!UICONTROL 引数]**」タブで、各種フィールド（テキスト、フォントタイプ、サイズ、カラー、位置、向きなど）に有効な値を指定します。変更を確認するには、「**[!UICONTROL 完了]**」をクリックします。

   ![Assets における「透かしを追加」ステップの引数の指定](assets/arguments_add_watermark_aem_assets.png)

1. 透かしステップを追加した **[!UICONTROL DAM アセットの更新]**&#x200B;ワークフローを保存します。
1. AEMユーザーインターフェイスから、サンプルアセットをアップロードします。 上記の手順で設定した位置に、フォントサイズ、色などの透かしが表示されます。

プログラム的に、または動的な情報を使用してPDFドキュメントに透かしを付けるには、[AEMドキュメントサービス](/help/forms/using/overview-aem-document-services.md)オファーを使用することを検討してください。

## ヒントと制限事項 {#tips-limitations}

* テキストベースの透かしのみがサポートされます。 [!UICONTROL 透かしプロセス]の作成時に画像をアップロードできる場合でも、画像は透かしとして追加使用されません。
* 透かしの設定は、PNGファイルとJPEGファイルのみサポートされています。 その他のアセット形式は、透かしが埋め込まれていません。
