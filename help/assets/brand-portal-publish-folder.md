---
title: Brand Portal へのフォルダーの公開
description: Brand Portal へのフォルダーの公開および非公開の方法を説明します。
contentOwner: VG
translation-type: tm+mt
source-git-commit: 33210032c45e38963aed429e70eec4095c5d75f1

---


# Brand Portal へのフォルダーの公開 {#publish-folders-to-brand-portal}

Adobe Experience Manager（AEM）Assets の管理者は、アセットやフォルダーを組織の AEM Assets Brand Portal インスタンスに公開（または公開ワークフローを未来の日時で設定）できます。ただし、最初に AEM Assets を Brand Portal と統合する必要があります。For details, see [Configure AEM Assets with Brand Portal](configure-aem-assets-with-brand-portal.md).

アセットまたはフォルダを公開すると、Brand Portalでそのアセットまたはフォルダをユーザが使用できるようになります。

AEM Assetsの元のアセットまたはフォルダーに対して後で変更を行った場合、その変更は、アセットまたはフォルダーを再公開するまでBrand Portalに反映されません。 この機能を使用すると、作業中の変更がBrand Portalで使用できなくなります。 Brand Portalでは、管理者が発行した承認済みの変更のみを利用できます。

## Brand Portal へのフォルダーの公開 {#publish-folders-to-brand-portal-1}

1. From the AEM Assets interface, hover over the desired folder and select **[!UICONTROL Publish]** option from the quick actions.

   あるいは、目的のフォルダーを選択して後述の手順に従います。

   ![publish2bp](assets/publish2bp.png)

2. **フォルダーを今すぐ公開**

   選択したフォルダーを Brand Portal に公開するには、次のいずれかを実行します。

   * From the toolbar, select **[!UICONTROL Quick Publish]**. Then from the menu, select **[!UICONTROL Publish to Brand Portal]**.
   * From the toolbar, select **[!UICONTROL Manage Publication]**.

3. Then from the **[!UICONTROL Action]** select **[!UICONTROL Publish to Brand Portal]**, and from **[!UICONTROL Scheduling]** select **[!UICONTROL Now]**. 「**[!UICONTROL 次へ]」をタップします。**
4. Within **[!UICONTROL Scope]**, confirm your selection and tap **[!UICONTROL Publish to Brand Portal]**.

   フォルダーが Brand Portal への公開用のキューに入れられたことを示すメッセージが表示されます。Brand Portal のインターフェイスにログインして、公開されたフォルダーを確認します。

   **フォルダーを後で公開**

   アセットフォルダのBrand Portalへの投稿ワークフローを後日にスケジュールするには：

   1. Once you have selected assets/folders to publish, select **[!UICONTROL Manage Publication]** from the tool bar at the top.
   2. On **[!UICONTROL Manage Publication]** page, select **[!UICONTROL Publish to Brand Portal]** from **[!UICONTROL Action]** and select **[!UICONTROL Later]** from **[!UICONTROL Scheduling]**.

      ![publishlatebp](assets/publishlaterbp.png)

   3. Select an **[!UICONTROL Activation date]** and specify time. 「**[!UICONTROL 次へ]**」をタップします。
   4. Confirm your selection in **[!UICONTROL Scope]**. 「**[!UICONTROL 次へ]**」をタップします。
   5. Specify a Workflow title under **[!UICONTROL Workflows]**. Tap **[!UICONTROL Publish Later]**.

      ![manageschedulepub](assets/manageschedulepub.png)

## Brand Portal へのフォルダーの公開の取り消し {#unpublish-folders-from-brand-portal}

AEM オーサーインスタンスからアセットインスタンスの公開を取り消すことで、Brand Portal に公開されているアセットフォルダーを削除できます。元のフォルダーの公開を取り消すと、そのコピーはBrand Portalユーザーは使用できなくなります。

Brand Portal へのフォルダーの公開をすぐに取り消すことも、取り消しのスケジュールを未来の日時で設定することもできます。Brand Portal へのアセットフォルダーの公開を取り消すには、次のようにします。

1. AEM オーサーインスタンス内の AEM Assets インターフェイスで、公開を取り消すフォルダーを選択します。

   ![publish2bp-1](assets/publish2bp-1.png)

2. ツールバーで「**[!UICONTROL 公開を管理]**」をタップまたはクリックします。

3. **Brand Portal への公開を今すぐ取り消し**

   Brand Portal へのフォルダーの公開をすぐに取り消すには、次のようにします。

   1. On **[!UICONTROL Manage Publication]** page, from **[!UICONTROL Action]** select **[!UICONTROL Unpublish from Brand Portal]** and from **[!UICONTROL Scheduling]** select **[!UICONTROL Now]**.
   2. Tap/ click **[!UICONTROL Next].**
   3. Within **[!UICONTROL Scope]**, confirm your selection and tap **[!UICONTROL Unpublish from Brand Portal]**.
   ![非公開の確認](assets/confirm-unpublish.png)

   **後でBrand Portalから非公開にする**

   Brand Portal へのフォルダーの公開を停止するスケジュールを未来の日時で設定するには、次のようにします。

   1. On **[!UICONTROL Manage Publication]** page, from **[!UICONTROL Action]** select **[!UICONTROL Unpublish from Brand Portal]** and from **[!UICONTROL Scheduling]** select **[!UICONTROL Later].**
   2. Select an **[!UICONTROL Activation date]** and specify the time. 「**[!UICONTROL 次へ]**」をタップします。
   3. Within **[!UICONTROL Scope]**, confirm your selection and tap **[!UICONTROL Next]**.
   4. Specify a **[!UICONTROL Workflow title]** under **[!UICONTROL Workflows]**. Tap **[!UICONTROL Unpublish Later].**

      ![unpublishworkflows](assets/unpublishworkflows.png)


>[!NOTE]
>
>Brand Portalに対してアセットを公開/非公開する手順は、フォルダの対応する手順と似ています。
