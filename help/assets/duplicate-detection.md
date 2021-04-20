---
title: 重複項目の検出の有効化
description: AEM で重複アセットの検出を有効にする方法について説明します。
contentOwner: AG
feature: Asset Management,Asset Reports
role: Business Practitioner,Administrator
translation-type: tm+mt
source-git-commit: 29e3cd92d6c7a4917d7ee2aa8d9963aa16581633
workflow-type: tm+mt
source-wordcount: '161'
ht-degree: 60%

---


# 重複項目の検出の有効化 {#enabling-duplicate-detection}

Adobe Experience Manager（AEM）Assets に存在するアセットをアップロードしようとすると、重複項目検出機能によって重複として識別されます。重複項目の検出はデフォルトで無効になっています。この機能を有効にするには、次の手順を実行します。

1. `https://[server]:[port]/system/console/configMgr`の&#x200B;**[!UICONTROL Adobe Experience ManagerWebコンソール設定]**&#x200B;ページを開きます。
1. サーブレット&#x200B;**[!UICONTROL Day CQ DAM Create Asset]**&#x200B;の設定を編集します。
1. 「**[!UICONTROL 重複を検出]**」オプションを選択し、「**[!UICONTROL 保存]**」をクリックまたはタップします。

   ![サーブレットで「重複項目の検出」オプションを選択](assets/chlimage_1-377.png)

これで、重複項目検出機能が AEM Assets で有効になります。AEM に存在するアセットをアップロードしようとすると、システムが競合をチェックして表示します。アセットは、`jcr:content/metadata/dam:sha1`に保存されているSHA-1ハッシュを使用して識別されます。つまり、ファイル名に関係なく、重複アセットが検出されます。

>[!MORELIKETHIS]
>
>* [既存のリポジトリの重複アセット（コミュニティメンバーのチュートリアル）](https://experience-aem.blogspot.com/2019/06/aem-65-find-duplicate-assets-binaries-in-existing-repository.html)

