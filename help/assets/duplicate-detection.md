---
title: 重複項目の検出の有効化
description: AEMで重複アセットの検出を有効にする方法を説明します。
contentOwner: AG
feature: Asset Management,Asset Reports
role: User,Admin
exl-id: 138cf649-9e21-415e-9861-b07caacc85db
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 26%

---

# 重複項目の検出の有効化 {#enabling-duplicate-detection}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

Adobe Experience Manager Assets に存在するアセットをアップロードしようとすると、重複の検出機能によって重複と見なされます。 重複の検出は、デフォルトで無効になっています。 この機能を有効にするには、次の手順を実行します。

1. を開きます。 **[!UICONTROL Adobe Experience Manager Web コンソール設定]** ページ `https://[server]:[port]/system/console/configMgr`.
1. サーブレットの **[!UICONTROL Day CQ DAM アセット作成]**&#x200B;の設定を編集します。
1. を選択します。 **[!UICONTROL 重複を検出]** 「 」オプションで、「 」をクリックまたはタップします。 **[!UICONTROL 保存]**.

   ![サーブレットで「重複項目の検出」オプションを選択](assets/chlimage_1-377.png)

重複の検出機能がで有効になりました。 [!DNL Experience Manager] アセット。 ユーザーがAEMに存在するアセットをアップロードしようとすると、システムは競合を確認し、そのことを示します。 `jcr:content/metadata/dam:sha1` に保存されている SHA-1 ハッシュを使用して、アセットが識別されます。つまり、重複アセットはファイル名に関係なく検出されます。

>[!MORELIKETHIS]
>
>* [既存のリポジトリ内のアセットの複製（コミュニティメンバーからのチュートリアル）](https://experience-aem.blogspot.com/2019/06/aem-65-find-duplicate-assets-binaries-in-existing-repository.html)

