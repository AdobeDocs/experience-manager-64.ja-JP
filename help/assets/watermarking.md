---
title: デジタルアセットへの透かしの追加
description: 透かし処理機能を使用して、アセットにデジタル透かしを追加する方法について説明します。
contentOwner: AG
feature: アセット管理
role: Business Practitioner,Administrator
exl-id: ed01143c-b516-44f8-aceb-ad2e3f0106b2
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '325'
ht-degree: 35%

---

# デジタルアセットの透かしの設定 {#watermarking}

[!DNL Adobe Experience Manager Assets] では、アセットにデジタル透かしを追加して、アセットの信頼性と著作権の所有権を確認できます。[!DNL Experience Manager Assets] では、PNG および JPEG ファイル上の透かしとしてテキストを使用できます。

Adobe Experience Manager(AEM)Assetsでは、画像にデジタル透かしを追加して、アセットの信頼性や著作権の所有権を確認できます。 AEM Assets では、PNG および JPEG ファイル上の透かしとしてテキストを使用できます。

アセットに透かしを適用できるようにするには、[!UICONTROL DAMアセットの更新]ワークフローに透かし処理ステップを追加します。

1. [!DNL Experience Manager]ユーザーインターフェイスにアクセスし、**[!UICONTROL ツール]** / **[!UICONTROL ワークフロー]** / **[!UICONTROL モデル]**&#x200B;に移動します。
1. ワークフローモデルページで、**[!UICONTROL DAM アセットの更新]**&#x200B;ワークフローを選択し、「**[!UICONTROL 編集]**」をクリックします。

1. サイドパネルから、「**[!UICONTROL 透かしを追加]**」ステップをドラッグし、「[!UICONTROL DAMアセットの更新]」ワークフローに追加します。

   ![「DAMアセットの更新」ワークフローで「透かしを追加」ステップをドラッグします。](assets/add_watermark_step_aem_assets.png)

   >[!NOTE]
   >
   >[!UICONTROL 透かしを追加]ステップを、[!UICONTROL サムネールを処理]ステップの前の任意の場所に配置します。

1. 「**[!UICONTROL 透かしを追加]**」ステップを開いて、プロパティを表示します。
1. 「**[!UICONTROL 引数]**」タブで、各種フィールド（テキスト、フォントタイプ、サイズ、カラー、位置、向きなど）に有効な値を指定します。変更を確定するには、「**[!UICONTROL 完了]**」をクリックします。

   ![Assets における「透かしを追加」ステップの引数の指定](assets/arguments_add_watermark_aem_assets.png)

1. 透かしステップを追加した **[!UICONTROL DAM アセットの更新]**&#x200B;ワークフローを保存します。
1. AEMユーザーインターフェイスから、サンプルアセットをアップロードします。 透かしは、上記の手順で設定した位置に、フォントサイズや色などと共に表示されます。

プログラムによって、または動的情報を使用してPDFドキュメントに透かしを追加するには、[AEM Document Services](/help/forms/using/overview-aem-document-services.md)の機能を使用することを検討してください。

## ヒントと制限事項 {#tips-limitations}

* テキストベースの透かしのみがサポートされます。 [!UICONTROL 透かしを追加処理]の作成時に画像をアップロードできる場合でも、画像は透かしとして使用されません。
* 透かしはPNGおよびJPEGファイルのみがサポートされています。 その他のアセット形式は透かしにはなりません。
