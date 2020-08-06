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


# Apache Tikaを使用してデジタルアセットのMIMEタイプを検出する {#detecting-mime-type-of-assets-using-apache-tika}

通常、Adobe Experience Manager(AEM) Assetsは、ファイルの拡張子からアップロードするアセットのMIMEタイプを検出します。 Apache Tika を使用してアセットをアップロードすると、AEM Assets は、アセットの MIME タイプをファイル拡張子ではなくコンテンツストリームから、アップロード操作中に検出します。

この機能はデフォルトでは無効になっています。To enable the feature, configure the **Day CQ DAM Mime Type** service from Configuration Manager.

>[!NOTE]
>
>Apache Tikaライブラリを使用したMIMEタイプの検出は、リソースを大量に消費する操作です。

1. Go to `https://[AEM_server]:[port]/system/console/configMgr` to open the Configuration Manager web console.
1. From the list of services, locate **[!UICONTROL Day CQ DAM Mime Type Service]** and tap/click the **[!UICONTROL Edit]** icon beside it to open it in Edit mode.

1. Select the **[!UICONTROL Detect MIME from content]** option to enable the parsing of uploaded assets to determine their MIME type while ignoring file extensions. デフォルトでは、このオプションはオフになっています。

   ![chlimage_1-333](assets/chlimage_1-333.png)

1. 「**[!UICONTROL 保存]**」をクリックまたはタップして、変更を保存します。
