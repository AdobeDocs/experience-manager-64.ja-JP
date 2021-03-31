---
title: アセットのアップロード制限の設定
description: Adobe Experience Manager（AEM）Assets の設定でユーザーがアップロードできるアセット（ファイル）のタイプを制限する方法を学習します。
contentOwner: AG
feature: デベロッパー
role: 管理者，アーキテクト
translation-type: tm+mt
source-git-commit: 29e3cd92d6c7a4917d7ee2aa8d9963aa16581633
workflow-type: tm+mt
source-wordcount: '222'
ht-degree: 91%

---


# アセットのアップロード制限を設定{#configuring-asset-upload-restrictions}

Adobe Experience Manager（AEM）Assets の設定で、ユーザーがアップロードできるアセット（ファイル）のタイプを制限できます。この機能により、望ましくない形式のアセットや悪意のあるファイルがユーザーによってアップロードされないようにすることができます。`Day CQ DAM Asset Upload Restriction` サービスを使用すると、ユーザーがアップロードできるファイルの種類を制御できます。デフォルトでは、AEM Assets はすべての MIME タイプのアセットのアップロードを許可します。ただし、アップロードを特定の MIME タイプのファイルのみに制限するようにサービスを設定できます。

1. Configuration Manager Webコンソールを開くには、`https://[AEM_server]:[port]/system/console/configMgr`にアクセスします。
1. **[!UICONTROL Day CQ DAM Asset Upload Restriction]** サービスを編集モードで開きます。デフォルトでは、「**Allow all MIME**」オプションがオンになっており、すべての MIME タイプのファイルのアップロードが許可されます。

   ![chlimage_1-378](assets/chlimage_1-378.png)

1. アップロードを特定の MIME タイプのファイルのみに制限するには、「**[!UICONTROL Allow all MIME]**」オプションをオフにして、「**[!UICONTROL Allowed Asset MIMEs (regex)]**」フィールドに許可する MIME タイプを正規表現を使用して指定します。

   ![chlimage_1-379](assets/chlimage_1-379.png)

1. 「**[!UICONTROL 保存]**」をクリックまたはタップして、変更を保存します。許可する MIME タイプに MIME 文字列を指定した場合、これらのフィールドに設定した MIME 文字列と一致しないすべての MIME タイプのアセットでは、アップロード操作が失敗します。
