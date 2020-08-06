---
title: 重複項目の検出の有効化
description: AEM で重複アセットの検出を有効にする方法について説明します。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 26e860cd513d70d748f872e2ce445a042d075bc6
workflow-type: tm+mt
source-wordcount: '154'
ht-degree: 61%

---


# 重複項目の検出の有効化 {#enabling-duplicate-detection}

Adobe Experience Manager（AEM）Assets に存在するアセットをアップロードしようとすると、重複項目検出機能によって重複として識別されます。重複項目の検出はデフォルトで無効になっています。この機能を有効にするには、次の手順を実行します。

1. Open the **[!UICONTROL Adobe Experience Manager Web Console Configuration]** page at `https://[server]:[port]/system/console/configMgr`.
1. Edit the configuration for the servlet **[!UICONTROL Day CQ DAM Create Asset]**.
1. Select the **[!UICONTROL detect duplicate]** option, and click/tap **[!UICONTROL Save]**.

   ![サーブレットで「重複項目の検出」オプションを選択](assets/chlimage_1-377.png)

これで、重複項目検出機能が AEM Assets で有効になります。AEM に存在するアセットをアップロードしようとすると、システムが競合をチェックして表示します。The assets are identified using SHA-1 hash stored at `jcr:content/metadata/dam:sha1`, which means duplicate assets are detected irrespective of the filenames.

>[!MORELIKETHIS]
>
>* [既存のリポジトリの重複アセット（コミュニティメンバーのチュートリアル）](https://experience-aem.blogspot.com/2019/06/aem-65-find-duplicate-assets-binaries-in-existing-repository.html)

