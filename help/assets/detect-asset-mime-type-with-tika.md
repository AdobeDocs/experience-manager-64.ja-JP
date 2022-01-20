---
title: Apache Tika を使用してデジタルアセットの MIME タイプを検出する
description: Apache Tika のヘルプを有効にする [!DNL Experience Manager] Assets では、アップロード操作時に、ファイル拡張子ではなくコンテンツストリームからアセットの MIME タイプを検出します。
contentOwner: AG
feature: Metadata,Developer Tools,Asset Management
role: Admin,Architect
exl-id: 6c9e53e9-5e54-4816-9431-41e796340d1e
source-git-commit: 8948bca63f1f5ec9d94ede2fb845ed01b4e23333
workflow-type: tm+mt
source-wordcount: '194'
ht-degree: 10%

---

# Apache Tika を使用してデジタルアセットの MIME タイプを検出する {#detecting-mime-type-of-assets-using-apache-tika}

通常、Adobe Experience Manager Assets は、アップロードするアセットの MIME タイプをファイル拡張子から検出します。 Apache Tika を使用してアセットをアップロードする場合、 [!DNL Experience Manager] Assets は、アップロード操作中に、ファイル拡張子ではなくコンテンツストリームから MIME タイプを検出します。

この機能はデフォルトでは無効になっています。この機能を有効にするには、 **Day CQ DAM MIME Type** サービスを Configuration Manager から取得します。

>[!NOTE]
>
>Apache Tika ライブラリを使用した MIME タイプの検出は、リソースを集中的に消費する操作です。

1. に移動します。 `https://[AEM_server]:[port]/system/console/configMgr` をクリックして、Configuration Manager Web コンソールを開きます。
1. サービスのリストから、 **[!UICONTROL Day CQ DAM Mime Type Service]** 次に、 **[!UICONTROL 編集]** アイコンをクリックし、編集モードで開きます。

1. を選択します。 **[!UICONTROL コンテンツから MIME を検出]** アップロードされたアセットの解析を有効にして、ファイル拡張子を無視しながら MIME タイプを判断するオプション。 デフォルトでは、このオプションはオフになっています。

   ![chlimage_1-333](assets/chlimage_1-333.png)

1. 「**[!UICONTROL 保存]**」をクリックまたはタップして、変更を保存します。
