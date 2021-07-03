---
title: アセットインサイトの設定
description: AEM Assetsでアセットインサイトを設定する方法について説明します。
contentOwner: AG
feature: アセットインサイト、アセットレポート
role: User,Admin
exl-id: b0d62dd3-1868-4d73-95f7-3d6c3ff474d9
source-git-commit: 5d96c09ef764b02e08dcdf480da1ee18f4d9a30c
workflow-type: tm+mt
source-wordcount: '241'
ht-degree: 68%

---

# アセットインサイトの設定 {#configuring-asset-insights}

Adobe Experience Manager（AEM）Assets は、サードパーティの Web サイトで使用される AEM アセットに関する使用状況データを Adobe Analytics からフェッチします。アセットインサイトでこのデータを取得してインサイトを生成できるようにするには、まずAdobe Analyticsと統合するように機能を設定します。

>[!NOTE]
>
>インサイトのサポートおよび提供がおこなわれるのは、画像に対してのみです。

1. AEM で&#x200B;**[!UICONTROL ツール／アセット]**&#x200B;をクリックします。

   ![chlimage_1-210](assets/chlimage_1-210.png)

1. 「**[!UICONTROL インサイト設定]**」カードをクリックします。
1. ウィザードで、データセンターを選択し、会社名、ユーザー名、パスワードなどの資格情報を指定します。

   ![chlimage_1-211](assets/insights_config2.png)

1. 「**[!UICONTROL 認証]**」をクリックまたはタップします。
1. AEMが資格情報を認証した後、**[!UICONTROL レポートスイート]**&#x200B;リストから、アセットインサイトでデータを取得するAdobe Analyticsレポートスイートを選択します。 「**[!UICONTROL 追加]**」をクリックします。
1. AEMがレポートスイートを設定したら、「**[!UICONTROL 完了]**」をクリックまたはタップします。

## ページトラッカー {#page-tracker}

 Analytics アカウントを設定すると、ページトラッカーコードが生成されます。サードパーティの Web サイトで使用される AEM アセットをアセットインサイトで追跡できるようにするには、Web サイトコードにトラッカーコードを組み込みます。AEM Assets のページトラッカーユーティリティを使用してページトラッカーコードを生成してください。サードパーティの Web サイトにページトラッカーコードを組み込む方法について詳しくは、[Web ページでのページトラッカーと埋め込みコードの使用](touch-ui-using-page-tracker.md)を参照してください。

1. AEMで、**[!UICONTROL ツール/Assets]**&#x200B;をクリックします。

   ![chlimage_1-214](assets/chlimage_1-214.png)

1. **[!UICONTROL ナビゲーション]**&#x200B;ページで、「**[!UICONTROL インサイトページトラッカー]**」カードをクリックします。
1. **[!UICONTROL ダウンロード]**&#x200B;アイコンをクリックしてページトラッカーコードをダウンロードします。
