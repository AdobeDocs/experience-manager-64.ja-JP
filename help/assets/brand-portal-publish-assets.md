---
title: Brand Portal へのフォルダーの公開
description: Brand Portalにアセットを公開および非公開する方法を説明します。
contentOwner: VG
translation-type: tm+mt
source-git-commit: f09853921dec6602952f369982a1563c7e4a9727
workflow-type: tm+mt
source-wordcount: '421'
ht-degree: 52%

---


# Brand Portal へのアセットの公開 {#publish-assets-to-brand-portal}

Adobe Experience Manager(AEM)アセット管理者は、組織のAEM Assetsブランドポータルインスタンスにアセットを公開（または公開ワークフローを後日にスケジュール）できます。 ただし、最初にBrand Portalを使用してAEM Assetsを設定する必要があります。 詳しくは [AEM Assets と Brand Portal の連携の設定](configure-aem-assets-with-brand-portal.md)を参照してください。

アセットを公開すると、ブランドポータルでユーザーが利用できるようになります。

AEM Assetsで元のアセットに後で変更を加えた場合、そのアセットを再公開するまで、その変更はBrand Portalに反映されません。 このため、作業中の変更が Brand Portal に提供されることがありません。管理者が公開した承認済みの変更のみが Brand Portal で提供されます。

レプリケーションが正常に終了したら、アセット、フォルダー、コレクションを Brand Portal に公開することができます。アセットを Brand Portal に公開するには、次の手順を実行します。

>[!NOTE]
>
>AEM オーサーが過剰なリソースを占有しないように、できればピーク時を避け、時間をずらして公開することをお勧めします。

1. アセットコンソールで目的のアセットにマウスポインターを置き、クイックアクションから「**[!UICONTROL 公開]**」オプションを選択します。

   または、Brand Portal に公開するアセットを選択します。

   ![publish2bp-2](assets/publish2bp-2.png)

2. アセットをBrand Portalに公開するには、次の2つのオプションを使用できます。
   * [アセットを直ちに公開](#publish-now)
   * [アセットを後で公開](#publish-later)

## アセットを今すぐ公開 {#publish-now}

選択したアセットを Brand Portal に公開するには、次のいずれかを実行します。

* ツールバーで「**[!UICONTROL クイック公開]**」を選択します。Then from the menu, select **[!UICONTROL Publish to Brand Portal]**.

* ツールバーで「**[!UICONTROL 公開を管理]**」を選択します。

   1. Then from the **[!UICONTROL Action]** select **[!UICONTROL Publish to Brand Portal]**, and from **[!UICONTROL Scheduling]** select **[!UICONTROL Now]**. Tap/ click **[!UICONTROL Next].**

   2. Within **[!UICONTROL Scope]**, confirm your selection and tap/ click **[!UICONTROL Publish to Brand Portal]**.

アセットが Brand Portal への公開用のキューに入れられたことを示すメッセージが表示されます。Brand Portal のインターフェイスにログインして、公開されたアセットを確認します。

## アセットを後で公開 {#publish-later}

アセットを Brand Portal に公開するスケジュールを後の日時に設定するには、次の手順を実行します。

1. Once you have selected assets/ folders to publish, select **[!UICONTROL Manage Publication]** from the tool bar at the top.
2. On **[!UICONTROL Manage Publication]** page, select **[!UICONTROL Publish to Brand Portal]** from **[!UICONTROL Action]** and select **[!UICONTROL Later]** from **[!UICONTROL Scheduling]**.

   ![publishlaterbp-1](assets/publishlaterbp-1.png)

3. 「**[!UICONTROL アクティベート日]**」を選択して時刻を指定します。「**[!UICONTROL 次へ]**」をタップまたはクリックします。
4. 「**[!UICONTROL アクティベート日]**」を選択して時刻を指定します。「**[!UICONTROL 次へ]**」をタップまたはクリックします。
5. 「**[!UICONTROL ワークフロー]**」でワークフロータイトルを指定します。Tap/ click **[!UICONTROL Publish Later]**.

   ![publishworkflow](assets/publishworkflow.png)

次に、Brand Portalにログインして、公開されたアセットがBrand Portalインターフェイスで使用できるかどうかを確認します。

![bp_631_landing_page](assets/bp_landing_page.png)
