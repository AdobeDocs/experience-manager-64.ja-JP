---
title: Apache Tikaを使用したデジタルアセットのMIMEタイプの検出
description: Apache Tikaを有効にして、 [!DNL Experience Manager] Assetsがファイル拡張子ではなく、アップロード操作中にコンテンツストリームからアセットのMIMEタイプを検出できるようにします。
contentOwner: AG
feature: Metadata,Developer Tools,Asset Management
role: Admin,Architect
exl-id: 6c9e53e9-5e54-4816-9431-41e796340d1e
source-git-commit: 8948bca63f1f5ec9d94ede2fb845ed01b4e23333
workflow-type: tm+mt
source-wordcount: '194'
ht-degree: 10%

---

# Apache Tikaを使用したデジタルアセットのMIMEタイプの検出 {#detecting-mime-type-of-assets-using-apache-tika}

通常、Adobe Experience Manager Assetsは、アップロードするアセットのMIMEタイプをファイル拡張子から検出します。 Apache Tikaを使用してアセットをアップロードする場合、[!DNL Experience Manager] Assetsは、アップロード操作中に、ファイル拡張子ではなくコンテンツストリームからMIMEタイプを検出します。

この機能はデフォルトでは無効になっています。この機能を有効にするには、Configuration Managerで&#x200B;**Day CQ DAM Mime Type**&#x200B;サービスを設定します。

>[!NOTE]
>
>Apache Tikaライブラリを使用したMIMEタイプ検出は、リソースを大量に消費する操作です。

1. `https://[AEM_server]:[port]/system/console/configMgr`に移動して、Configuration Manager Webコンソールを開きます。
1. サービスのリストで、「**[!UICONTROL Day CQ DAM Mime Type Service]**」を探し、その横にある&#x200B;**[!UICONTROL 編集]**&#x200B;アイコンをタップまたはクリックして編集モードで開きます。

1. **[!UICONTROL 「コンテンツからMIMEを検出]** 」オプションを選択して、アップロードされたアセットの解析を有効にし、ファイル拡張子を無視してMIMEタイプを判断します。 デフォルトでは、このオプションはオフになっています。

   ![chlimage_1-333](assets/chlimage_1-333.png)

1. 「**[!UICONTROL 保存]**」をクリックまたはタップして、変更を保存します。
