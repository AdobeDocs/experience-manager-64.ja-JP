---
title: アセットのアップロード制限の設定
description: Adobe Experience Manager Assets を設定して、ユーザーがアップロードできるアセット（ファイル）のタイプを制限する方法について説明します。
contentOwner: AG
feature: Upload,Asset Ingestion,Asset Management
role: Admin,Architect
exl-id: 0d817cfa-ae06-442a-ad89-5fe619bb2eff
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '252'
ht-degree: 69%

---

# アセットのアップロード制限の設定 {#configuring-asset-upload-restrictions}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

Adobe Experience Manager Assets を設定して、ユーザーがアップロードできるアセット（ファイル）のタイプを制限できます。 この機能により、望ましくない形式のアセットや悪意のあるファイルがユーザーによってアップロードされないようにすることができます。`Day CQ DAM Asset Upload Restriction` サービスを使用すると、ユーザーがアップロードできるファイルの種類を制御できます。デフォルトでは、 [!DNL Experience Manager] Assets を使用すると、すべての MIME タイプのアセットをアップロードできます。 ただし、アップロードを特定の MIME タイプのファイルのみに制限するようにサービスを設定できます。

1. Configuration Manager web コンソールを開くには、 `https://[AEM_server]:[port]/system/console/configMgr` にアクセスしてください。
1. **[!UICONTROL Day CQ DAM Asset Upload Restriction]** サービスを編集モードで開きます。デフォルトでは、「**Allow all MIME**」オプションがオンになっており、すべての MIME タイプのファイルのアップロードが許可されます。

   ![chlimage_1-378](assets/chlimage_1-378.png)

1. アップロードを特定の MIME タイプのファイルのみに制限するには、「**[!UICONTROL Allow all MIME]**」オプションをオフにして、「**[!UICONTROL Allowed Asset MIMEs (regex)]**」フィールドに許可する MIME タイプを正規表現を使用して指定します。

   ![chlimage_1-379](assets/chlimage_1-379.png)

1. 「**[!UICONTROL 保存]**」をクリックまたはタップして、変更を保存します。許可する MIME タイプに MIME 文字列を指定した場合、これらのフィールドに設定した MIME 文字列と一致しないすべての MIME タイプのアセットでは、アップロード操作が失敗します。
