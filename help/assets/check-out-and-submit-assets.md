---
title: デジタルアセットをチェックインし、編集用にチェックアウトする
description: 編集のためにアセットをチェックアウトし、変更が完了した後にアセットをチェックインする方法を説明します。
contentOwner: AG
feature: Asset Management
role: User
exl-id: 0c79ed42-0acd-426e-8e14-412bb4117585
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '429'
ht-degree: 37%

---

# アセット内ファイルのチェックイン、チェック-アウト {#check-in-and-check-out-files-in-assets}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

Adobe Experience Manager Assets では、編集のためにアセットをチェックアウトし、変更終了後にアセットをチェックインすることができます。 アセットをチェックアウトした後は、そのユーザーだけがアセットを編集、注釈、公開、移動、削除できます。 アセットのチェックアウトでアセットにロックがかかることになります。他のユーザーは、アセットをに再度チェックインするまで、アセットに対してこれらの操作を実行できません。 [!DNL Experience Manager] アセット。 ただし、ロックされたアセットのメタデータは変更することができます。

アセットをチェックアウトまたはチェックインするには、アセットに対する書き込みアクセス権が必要です。

この機能は、複数のユーザーがチーム間でワークフローの編集で共同作業する場合に、作成者が加えた変更が他のユーザーによって上書きされるのを防ぐのに役立ちます。

## アセットのチェックアウト {#checking-out-assets}

1. Assets UI で、チェックアウトするアセットを選択します。 複数のアセットを選択してチェックアウトすることもできます。

   ![chlimage_1-468](assets/chlimage_1-468.png)

1. ツールバーの「**[!UICONTROL チェックアウト]**」アイコンをクリックまたはタップします。

   ![chlimage_1-469](assets/chlimage_1-469.png)

   「**[!UICONTROL チェックアウト]**」アイコンが、鍵の開いた「**[!UICONTROL チェックイン]**」アイコンに変わることを確認します。

   ![chlimage_1-470](assets/chlimage_1-470.png)

   チェックアウトしたアセットを他のユーザーが編集できるかを確認するには、別のユーザーとしてログインします。チェックアウトしたアセットのサムネールにロックアイコンが表示されます。

   ![chlimage_1-471](assets/chlimage_1-471.png)

   アセットを選択します。アセットを編集、注釈、公開、削除するためのオプションはツールバーに表示されません。

   ![chlimage_1-472](assets/chlimage_1-472.png)

   ただし、 **[!UICONTROL プロパティを表示]** アイコンをクリックして、ロックされたアセットのメタデータを編集します。

1. 「編集」アイコンをクリックまたはタップして、アセットを編集モードで開きます。

   ![chlimage_1-473](assets/chlimage_1-473.png)

1. アセットを編集して、変更内容を保存します。例えば、画像を切り抜いて保存します。

   ![chlimage_1-474](assets/chlimage_1-474.png)

   アセットに注釈を付けたり公開したりすることもできます。

1. Assets UI で編集したアセットを選択し、ツールバーで&#x200B;**[!UICONTROL チェックイン]**&#x200B;アイコンをクリックまたはタップします。

   ![chlimage_1-475](assets/chlimage_1-475.png)

   変更されたアセットは [!DNL Assets] にチェックインされ、他のユーザーが編集できるようになります。

## 強制チェックイン {#forced-check-in}

管理者は、他のユーザーがチェックアウトしたアセットをチェックインできます。

1. 管理者として [!DNL Assets] にログインします。
1. Assets UI から、他のユーザーがチェックアウトした 1 つ以上のアセットを選択します。

   ![chlimage_1-476](assets/chlimage_1-476.png)

1. ツールバーの **[!UICONTROL ロックを解除]** アイコン アセットはチェックインされ、他のユーザーが編集できるようになります。

   ![chlimage_1-477](assets/chlimage_1-477.png)
