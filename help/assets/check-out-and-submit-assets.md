---
title: デジタルアセットをチェックインし、編集用にチェックアウトする
description: 編集のためにアセットをチェックアウトし、変更が完了した後にアセットをチェックインする方法を説明します。
contentOwner: AG
feature: Asset Management
role: User
exl-id: 0c79ed42-0acd-426e-8e14-412bb4117585
source-git-commit: 8948bca63f1f5ec9d94ede2fb845ed01b4e23333
workflow-type: tm+mt
source-wordcount: '393'
ht-degree: 66%

---

# アセット内ファイルのチェックイン、チェック-アウト {#check-in-and-check-out-files-in-assets}

Adobe Experience Manager Assets では、編集のためにアセットをチェックアウトし、変更終了後にアセットをチェックインすることができます。 アセットをチェックアウトした後は、そのユーザーだけがアセットを編集、注釈、公開、移動、削除できます。 アセットのチェックアウトでアセットにロックがかかることになります。他のユーザーは、アセットをに再度チェックインするまで、アセットに対してこれらの操作を実行できません。 [!DNL Experience Manager] アセット。 ただし、ロックされたアセットのメタデータは変更することができます。

アセットをチェックアウトまたはチェックインするには、アセットに対する書き込みアクセス権が必要です。

この機能は、複数のユーザーが複数のチームにわたるワークフローの編集で共同作業をする際、ある作成者が変更した内容を他のユーザーが書き換えてしまう事態を防ぐのに役立ちます。

## アセットのチェックアウト {#checking-out-assets}

1. Assets UI で、チェックアウトするアセットを選択します。 複数のアセットを選択してチェックアウトすることもできます。

   ![chlimage_1-468](assets/chlimage_1-468.png)

1. ツールバーの「**[!UICONTROL チェックアウト]**」アイコンをクリックまたはタップします。

   ![chlimage_1-469](assets/chlimage_1-469.png)

   「**[!UICONTROL チェックアウト]**」アイコンが、鍵の開いた「**[!UICONTROL チェックイン]**」アイコンに変わることを確認します。

   ![chlimage_1-470](assets/chlimage_1-470.png)

   チェックアウトしたアセットを他のユーザーが編集できるかを確認するには、別のユーザーとしてログインします。チェックアウトしたアセットのサムネールには鍵のアイコンが表示されます。

   ![chlimage_1-471](assets/chlimage_1-471.png)

   アセットを選択します。アセットを編集、注釈、公開または削除するためのオプションがツールバーに一切表示されないことを確認します。

   ![chlimage_1-472](assets/chlimage_1-472.png)

   ただし、「**[!UICONTROL プロパティを表示]**」アイコンをクリックまたはタップすれば、ロックされたアセットのメタデータを編集できます。

1. 編集アイコンをクリックまたはタップして、編集モードでアセットを開きます。

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
1. Assets UI で他のユーザーにチェックアウトされているアセットを 1 つ以上選択します。

   ![chlimage_1-476](assets/chlimage_1-476.png)

1. ツールバーの「**[!UICONTROL ロックを解除]**」アイコンをクリックまたはタップします。アセットはチェックインされ、他のユーザーが編集できるようになります。

   ![chlimage_1-477](assets/chlimage_1-477.png)
