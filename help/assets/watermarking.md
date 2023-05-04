---
title: デジタルアセットへの透かしの追加
description: 透かし処理機能を使用して、アセットにデジタル透かしを追加する方法について学びます。
contentOwner: AG
feature: Asset Management
role: User,Admin
exl-id: ed01143c-b516-44f8-aceb-ad2e3f0106b2
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '355'
ht-degree: 60%

---

# デジタルアセットに透かしをつける {#watermarking}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

[!DNL Adobe Experience Manager Assets] では、アセットにデジタル透かしを追加し、ユーザーがアセットの信頼性や著作権の所有権を確認できるようにします。[!DNL Experience Manager Assets] では、PNG および JPEG ファイル上の透かしとしてテキストを使用できます。

Adobe Experience Manager Assets では、画像に電子透かしを追加して、アセットの信頼性と著作権の所有権を確認できます。 [!DNL Experience Manager] Assets では、PNG および JPEG ファイル上の透かしとしてテキストを使用できます。

アセットに透かしを適用できるようにするには、[!UICONTROL DAM アセットの更新] ワークフローに透かしステップを追加してください。

1. [!DNL Experience Manager] ユーザインターフェイスにアクセスし、**[!UICONTROL ツール]**／**[!UICONTROL ワークフロー]**／**[!UICONTROL モデル]**&#x200B;に移動してください。 
1. ワークフローモデルページで、**[!UICONTROL DAM アセットの更新]**&#x200B;ワークフローを選択し、「**[!UICONTROL 編集]**」をクリックします。

1. サイドパネルから、 **[!UICONTROL 透かしを追加]** 手順を実行し、 [!UICONTROL DAM アセットの更新] ワークフロー。

   ![「DAM アセットの更新」ワークフローに「透かしを追加」ステップをドラッグします](assets/add_watermark_step_aem_assets.png)

   >[!NOTE]
   >
   >[!UICONTROL 透かしを追加]手順は、[!UICONTROL サムネールを処理]手順の前の任意の位置に配置します。

1. を開きます。 **[!UICONTROL 透かしを追加]** ステップを使用してプロパティを表示します。
1. 内 **[!UICONTROL 引数]** 「 」タブで、各種フィールドに有効な値（テキスト、フォントタイプ、サイズ、色、位置、向きなど）を指定します。 変更を確定するには、「**[!UICONTROL 完了]**」をクリックしてください。

   ![Assets の透かしを追加ステップで引数を指定します。](assets/arguments_add_watermark_aem_assets.png)

1. 透かしステップを追加した **[!UICONTROL DAM アセットの更新]**&#x200B;ワークフローを保存します。
1. [!DNL Experience Manager] ユーザーインターフェイスから、サンプルアセットをアップロードします。透かしは、フォントサイズ、色などと共に、上記の手順で設定した位置に表示されます。

プログラムで、あるいは動的情報を使用して PDF ドキュメントに透かしを付ける場合は、 [[!DNL Experience Manager]  ドキュメントサービス](/help/forms/using/overview-aem-document-services.md)の使用を検討してください。

## ヒントと制限事項 {#tips-limitations}

* テキストベースの透かしのみがサポートされます。 [!UICONTROL 透かしプロセスの追加]を作成する際には画像をアップロードできますが、画像は透かしとして使用されません。
* 透かしの使用は、PNG ファイルと JPEG ファイルのみでサポートされています。 その他のアセット形式には透かしは入りません。
