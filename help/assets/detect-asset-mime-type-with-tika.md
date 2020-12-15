---
title: Apache Tikaを使用してデジタルアセットのMIMEタイプを検出する
description: Apache Tika を使用して、AEM Assets がアセットの MIME タイプをファイル拡張子ではなくコンテンツストリームから、アップロード操作中に検出できるようにします。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 0d70a672a2944e2c03b54beb3b5f734136792ab1
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 37%

---


# Apache Tikaを使用してデジタルアセットのMIMEタイプを検出{#detecting-mime-type-of-assets-using-apache-tika}

通常、Adobe Experience Manager(AEM) Assetsは、ファイルの拡張子からアップロードするアセットのMIMEタイプを検出します。 Apache Tika を使用してアセットをアップロードすると、AEM Assets は、アセットの MIME タイプをファイル拡張子ではなくコンテンツストリームから、アップロード操作中に検出します。

この機能はデフォルトでは無効になっています。この機能を有効にするには、Configuration Managerから&#x200B;**Day CQ DAM Mime Type**&#x200B;サービスを設定します。

>[!NOTE]
>
>Apache Tikaライブラリを使用したMIMEタイプの検出は、リソースを大量に消費する操作です。

1. `https://[AEM_server]:[port]/system/console/configMgr`に移動し、Configuration Manager Webコンソールを開きます。
1. サービスのリストから、「**[!UICONTROL Day CQ DAM MIME Type Service]**」を探し、横の「**[!UICONTROL Edit]**」アイコンをタップまたはクリックして、編集モードで開きます。

1. 「**[!UICONTROL コンテンツ]**&#x200B;からMIMEを検出する」オプションを選択すると、アップロードされたアセットの解析を有効にして、ファイル拡張子を無視してMIMEタイプを決定できます。 デフォルトでは、このオプションはオフになっています。

   ![chlimage_1-333](assets/chlimage_1-333.png)

1. 「**[!UICONTROL 保存]**」をクリックまたはタップして、変更を保存します。
