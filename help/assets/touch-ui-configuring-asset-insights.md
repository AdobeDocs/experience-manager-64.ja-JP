---
title: アセットインサイトの設定
description: でアセットインサイトを設定する方法を説明します。 [!DNL Experience Manager] アセット。
contentOwner: AG
feature: Asset Insights,Asset Reports
role: User,Admin
exl-id: b0d62dd3-1868-4d73-95f7-3d6c3ff474d9
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '266'
ht-degree: 39%

---

# アセットインサイトの設定 {#configuring-asset-insights}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

Adobe Experience Manager Assets が [!DNL Experience Manager] Adobe Analyticsのサードパーティ Web サイトで使用されるアセット。 アセットインサイトでこのデータを取得してインサイトを生成できるようにするには、まずAdobe Analyticsと統合する機能を設定します。

>[!NOTE]
>
>インサイトのサポートおよび提供が行われるのは、画像に対してのみです。

1. AEM で&#x200B;**[!UICONTROL ツール／アセット]**&#x200B;をクリックします。

   ![chlimage_1-210](assets/chlimage_1-210.png)

1. 「**[!UICONTROL Insights 設定]**」カードをクリックします。
1. ウィザードで、データセンターを選択し、組織名、ユーザー名、パスワードなどの資格情報を指定します。

   ![chlimage_1-211](assets/insights_config2.png)

1. 「**[!UICONTROL 認証]**」をクリックまたはタップします。
1. [!DNL Experience Manager] によって資格情報が認証されたら、**[!UICONTROL レポートスイート]**&#x200B;リストから、アセットインサイトでデータをフェッチする Adobe Analytics レポートスイートを選択します。「**[!UICONTROL 追加]**」をクリックします。
1. 後 [!DNL Experience Manager] レポートスイートを設定し、 **[!UICONTROL 完了]**.

## ページトラッカー {#page-tracker}

 Analytics アカウントを設定すると、ページトラッカーコードが生成されます。サードパーティの web サイトで使用される [!DNL Experience Manager] アセットをアセットインサイトで追跡できるようにするには、web サイトコードにページトラッカーコードを組み込みます。でのページトラッカーユーティリティの使用 [!DNL Experience Manager] ページトラッカーコードを生成するアセット。 サードパーティの Web ページにページトラッカーコードを含める方法について詳しくは、 [Web ページでのページトラッカーと埋め込みコードの使用](touch-ui-using-page-tracker.md).

1. AEMで、 **[!UICONTROL ツール/アセット]**.

   ![chlimage_1-214](assets/chlimage_1-214.png)

1. **[!UICONTROL ナビゲーション]**&#x200B;ページで、「**[!UICONTROL インサイトページトラッカー]**」カードをクリックします。
1. 次をクリック： **[!UICONTROL ダウンロード]** アイコンを使用して、ページトラッカーコードをダウンロードします。
