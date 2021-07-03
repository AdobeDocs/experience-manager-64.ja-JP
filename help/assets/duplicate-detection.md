---
title: 重複項目の検出の有効化
description: AEM で重複アセットの検出を有効にする方法について説明します。
contentOwner: AG
feature: アセット管理、アセットレポート
role: User,Admin
exl-id: 138cf649-9e21-415e-9861-b07caacc85db
source-git-commit: 5d96c09ef764b02e08dcdf480da1ee18f4d9a30c
workflow-type: tm+mt
source-wordcount: '158'
ht-degree: 60%

---

# 重複項目の検出の有効化 {#enabling-duplicate-detection}

Adobe Experience Manager（AEM）Assets に存在するアセットをアップロードしようとすると、重複項目検出機能によって重複として識別されます。重複項目の検出はデフォルトで無効になっています。この機能を有効にするには、次の手順を実行します。

1. **[!UICONTROL Adobe Experience Manager Webコンソール設定]**&#x200B;ページ(`https://[server]:[port]/system/console/configMgr`)を開きます。
1. サーブレット&#x200B;**[!UICONTROL Day CQ DAM Create Asset]**&#x200B;の設定を編集します。
1. 「**[!UICONTROL 重複を検出]**」オプションを選択し、「**[!UICONTROL 保存]**」をクリックまたはタップします。

   ![サーブレットで「重複項目の検出」オプションを選択](assets/chlimage_1-377.png)

これで、重複項目検出機能が AEM Assets で有効になります。AEM に存在するアセットをアップロードしようとすると、システムが競合をチェックして表示します。アセットは、`jcr:content/metadata/dam:sha1`に保存されているSHA-1ハッシュを使用して識別されます。つまり、重複するアセットは、ファイル名に関係なく検出されます。

>[!MORELIKETHIS]
>
>* [既存のリポジトリ内のアセットの複製（コミュニティメンバーのチュートリアル）](https://experience-aem.blogspot.com/2019/06/aem-65-find-duplicate-assets-binaries-in-existing-repository.html)

