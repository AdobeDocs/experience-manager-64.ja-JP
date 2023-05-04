---
title: Apache Tika を使用してデジタルアセットの MIME タイプを検出する
description: Apache Tika のヘルプを有効にする [!DNL Experience Manager] Assets では、アップロード操作時に、ファイル拡張子ではなくコンテンツストリームからアセットの MIME タイプを検出します。
contentOwner: AG
feature: Metadata,Developer Tools,Asset Management
role: Admin,Architect
exl-id: 6c9e53e9-5e54-4816-9431-41e796340d1e
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '230'
ht-degree: 28%

---

# Apache Tika を使用してデジタルアセットの MIME タイプを検出する {#detecting-mime-type-of-assets-using-apache-tika}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

通常、Adobe Experience Manager Assets は、アップロードするアセットの MIME タイプをファイル拡張子から検出します。 Apache Tika を使用してアセットをアップロードする場合、 [!DNL Experience Manager] Assets は、アップロード操作中に、ファイル拡張子ではなくコンテンツストリームから MIME タイプを検出します。

この機能はデフォルトでは無効になっています。この機能を有効にするには、Configuration Manager で **Day CQ DAM Mime タイプ**&#x200B;サービスを設定してください。

>[!NOTE]
>
>Apache Tika ライブラリを使用した MIME タイプの検出は、リソースを集中的に消費する操作です。

1. に移動します。 `https://[AEM_server]:[port]/system/console/configMgr` をクリックして、Configuration Manager Web コンソールを開きます。
1. サービスのリストから、 **[!UICONTROL Day CQ DAM Mime Type Service]** 次に、 **[!UICONTROL 編集]** アイコンをクリックし、編集モードで開きます。

1. アップロードされたアセットの解析を有効にし、ファイルの拡張子を無視して MIME タイプを検出するには、「**[!UICONTROL コンテンツから MIME タイプを検出]**」オプションを選択してください。デフォルトでは、このオプションはオフになっています。

   ![chlimage_1-333](assets/chlimage_1-333.png)

1. 「**[!UICONTROL 保存]**」をクリックまたはタップして、変更を保存します。
