---
title: 重複項目の検出の有効化
description: AEM で重複アセットの検出を有効にする方法について説明します。
contentOwner: AG
feature: Asset Management,Asset Reports
role: User,Admin
exl-id: 138cf649-9e21-415e-9861-b07caacc85db
source-git-commit: 8948bca63f1f5ec9d94ede2fb845ed01b4e23333
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 40%

---

# 重複項目の検出の有効化 {#enabling-duplicate-detection}

Adobe Experience Manager Assetsに存在するアセットをアップロードしようとすると、重複の検出機能によって重複と見なされます。 重複項目の検出はデフォルトで無効になっています。この機能を有効にするには、次の手順を実行します。

1. **[!UICONTROL Adobe Experience Manager Webコンソール設定]**&#x200B;ページ(`https://[server]:[port]/system/console/configMgr`)を開きます。
1. サーブレット&#x200B;**[!UICONTROL Day CQ DAM Create Asset]**&#x200B;の設定を編集します。
1. 「**[!UICONTROL 重複を検出]**」オプションを選択し、「**[!UICONTROL 保存]**」をクリックまたはタップします。

   ![サーブレットで「重複項目の検出」オプションを選択](assets/chlimage_1-377.png)

重複項目の検出機能が[!DNL Experience Manager] Assetsで有効になりました。 AEM に存在するアセットをアップロードしようとすると、システムが競合をチェックして表示します。アセットは、`jcr:content/metadata/dam:sha1`に保存されているSHA-1ハッシュを使用して識別されます。つまり、重複するアセットは、ファイル名に関係なく検出されます。

>[!MORELIKETHIS]
>
>* [既存のリポジトリ内のアセットの複製（コミュニティメンバーのチュートリアル）](https://experience-aem.blogspot.com/2019/06/aem-65-find-duplicate-assets-binaries-in-existing-repository.html)

