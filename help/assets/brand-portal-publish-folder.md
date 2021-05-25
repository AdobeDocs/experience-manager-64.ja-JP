---
title: Brand Portal へのフォルダーの公開
description: Brand Portal へのフォルダーの公開および非公開の方法を説明します。
contentOwner: VG
feature: Brand Portal
role: Business Practitioner
exl-id: f41ab750-5780-42ae-a131-5bc748280215
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '573'
ht-degree: 58%

---

# Brand Portal へのフォルダーの公開 {#publish-folders-to-brand-portal}

Adobe Experience Manager（AEM）Assets の管理者は、アセットやフォルダーを組織の AEM Assets Brand Portal インスタンスに公開（または公開ワークフローを未来の日時で設定）できます。ただし、最初に AEM Assets を Brand Portal と統合する必要があります。詳しくは [AEM Assets と Brand Portal の連携の設定](configure-aem-assets-with-brand-portal.md)を参照してください。

アセットまたはフォルダーを公開すると、Brand Portalのユーザーがそのアセットまたはフォルダーを使用できるようになります。

その後、AEM Assetsで元のアセットまたはフォルダーに変更を加えても、そのアセットまたはフォルダーを再公開するまで、変更はBrand Portalに反映されません。 このため、作業中の変更が Brand Portal に提供されることがありません。管理者が公開した承認済みの変更のみが Brand Portal で提供されます。

## Brand Portal へのフォルダーの公開 {#publish-folders-to-brand-portal-1}

1. AEM Assetsインターフェイスで、目的のフォルダーの上にマウスポインターを置き、クイックアクションから「**[!UICONTROL 公開]**」オプションを選択します。

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

AEM オーサーインスタンスからアセットインスタンスの公開を取り消すことで、Brand Portal に公開されているアセットフォルダーを削除できます。元のフォルダーを非公開にすると、Brand Portal ユーザーはそのコピーを使用できなくなります。

Brand Portal へのフォルダーの公開をすぐに取り消すことも、取り消しのスケジュールを未来の日時で設定することもできます。Brand Portal へのアセットフォルダーを非公開にするには、次の手順を実行します。

1. AEM オーサーインスタンス内の AEM Assets インターフェイスで、公開を取り消すフォルダーを選択します。

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
