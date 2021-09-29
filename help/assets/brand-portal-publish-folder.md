---
title: Brand Portal へのフォルダーの公開
description: Brand Portal へのフォルダーの公開および非公開の方法を説明します。
contentOwner: VG
feature: Brand Portal
role: User
exl-id: f41ab750-5780-42ae-a131-5bc748280215
source-git-commit: de5632ff0ee87a4ded88e792b57e818baf4c01a3
workflow-type: tm+mt
source-wordcount: '552'
ht-degree: 44%

---

# Brand Portal へのフォルダーの公開 {#publish-folders-to-brand-portal}

Adobe Experience Manager Assets管理者は、アセットやフォルダーを組織の[!DNL Experience Manager Assets Brand Portal]インスタンスに公開（または公開ワークフローを後の日時にスケジュール）できます。 ただし、まず[!DNL Experience Manager Assets]を[!DNL Brand Portal]と統合する必要があります。 詳しくは、[Brand Portal](configure-aem-assets-with-brand-portal.md)での [!DNL Experience Manager Assets] の設定を参照してください。

アセットまたはフォルダーを公開すると、Brand Portalのユーザーがそのアセットまたはフォルダーを使用できるようになります。

[!DNL Assets]内の元のアセットまたはフォルダーに後で変更を加えた場合、その変更は、アセットまたはフォルダーを再公開するまでBrand Portalに反映されません。 このため、作業中の変更が Brand Portal に提供されることがありません。管理者が公開した承認済みの変更のみが Brand Portal で提供されます。

## Brand Portal へのフォルダーの公開 {#publish-folders-to-brand-portal-1}

1. [!DNL Assets]インターフェイスで、目的のフォルダーの上にマウスポインターを置き、クイックアクションから「**[!UICONTROL 公開]**」オプションを選択します。

   あるいは、目的のフォルダーを選択して後述の手順に従います。

   ![publish2bp](assets/publish2bp.png)

2. **フォルダーを今すぐ公開**

   選択したフォルダーを Brand Portal に公開するには、次のいずれかを実行します。

   * ツールバーで「**[!UICONTROL クイック公開]**」を選択します。次に、メニューから「**[!UICONTROL Brand Portalに公開]**」を選択します。
   * ツールバーで「**[!UICONTROL 公開を管理]**」を選択します。

3. 次に、「**[!UICONTROL アクション]**」から「**[!UICONTROL Brand Portalに公開]**」を選択し、「**[!UICONTROL スケジュール]**」から「**[!UICONTROL 今すぐ]**」を選択します。 「**[!UICONTROL 次へ]」をタップします。**
4. **[!UICONTROL 範囲]**&#x200B;内で選択を確定し、「**[!UICONTROL Brand Portalに公開]**」をタップします。

   フォルダーが Brand Portal への公開用のキューに入れられたことを示すメッセージが表示されます。Brand Portal のインターフェイスにログインして、公開されたフォルダーを確認します。

   **フォルダーを後で公開**

   アセットフォルダーのBrand Portalへの公開ワークフローを後の日時にスケジュールするには：

   1. 公開するアセット/フォルダーを選択したら、上部のツールバーの「**[!UICONTROL 公開を管理]**」を選択します。
   2. **[!UICONTROL 公開を管理]**&#x200B;ページで、**[!UICONTROL アクション]**&#x200B;から「**[!UICONTROL Brand Portalに公開]**」を選択し、**[!UICONTROL スケジュール]**&#x200B;から「**[!UICONTROL 後で]**」を選択します。

      ![publishlaterbp](assets/publishlaterbp.png)

   3. 「**[!UICONTROL アクティベート日]**」を選択して時刻を指定します。「**[!UICONTROL 次へ]**」をタップします。
   4. 「**[!UICONTROL 範囲]**」で選択内容を確認します。「**[!UICONTROL 次へ]**」をタップします。
   5. 「**[!UICONTROL ワークフロー]**」でワークフロータイトルを指定します。「**[!UICONTROL 後で公開]**」をタップします。

      ![manageschedulepub](assets/manageschedulepub.png)

## Brand Portal へのフォルダーの非公開 {#unpublish-folders-from-brand-portal}

[!DNL Experience Manager]オーサーインスタンスから非公開にすることで、Brand Portalに公開されているアセットフォルダーを削除できます。 元のフォルダーを非公開にすると、Brand Portal ユーザーはそのコピーを使用できなくなります。

Brand Portal へのフォルダーの公開をすぐに取り消すことも、取り消しのスケジュールを未来の日時で設定することもできます。Brand Portal へのアセットフォルダーを非公開にするには、次の手順を実行します。

1. [!DNL Experience Manager]オーサーインスタンスの[!DNL Assets]インターフェイスから、非公開にするフォルダーを選択します。

   ![publish2bp-1](assets/publish2bp-1.png)

2. ツールバーで「**[!UICONTROL 公開を管理]**」をタップまたはクリックします。

3. **Brand Portal への公開を今すぐ取り消し**

   Brand Portal へのフォルダーの公開をすぐに取り消すには、次のようにします。

   1. **[!UICONTROL 公開を管理]**&#x200B;ページで、**[!UICONTROL アクション]**&#x200B;から「**[!UICONTROL Brand Portalで非公開]**」を選択し、「**[!UICONTROL スケジュール]**」から「**[!UICONTROL 今すぐ]**」を選択します。
   2. **[!UICONTROL 「次へ]」をタップまたはクリックします。**
   3. **[!UICONTROL 範囲]**&#x200B;内で選択を確定し、「**[!UICONTROL Brand Portalから非公開]**」をタップします。

   ![confirm-unpublish](assets/confirm-unpublish.png)

   **後でBrand Portalから非公開にする**

   Brand Portal へのフォルダーの公開を停止するスケジュールを未来の日時で設定するには、次のようにします。

   1. **[!UICONTROL 公開を管理]**&#x200B;ページで、**[!UICONTROL アクション]**&#x200B;から「**[!UICONTROL Brand Portalで非公開]**」を選択し、「**[!UICONTROL スケジュール]**」から「**[!UICONTROL 後で].**」を選択します。
   2. 「**[!UICONTROL アクティベート日]**」を選択して時刻を指定します。「**[!UICONTROL 次へ]**」をタップします。
   3. **[!UICONTROL 範囲]**&#x200B;内で選択を確定し、「**[!UICONTROL 次へ]**」をタップします。
   4. **[!UICONTROL Workflows]**&#x200B;の下に&#x200B;**[!UICONTROL Workflow title]**&#x200B;を指定します。 **[!UICONTROL 後で非公開にする].**&#x200B;をタップします。

      ![unpublishworkflows](assets/unpublishworkflows.png)


>[!NOTE]
>
>Brand Portalに対してアセットを公開/非公開にする手順は、フォルダーに対する対応する手順と似ています。
