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

Adobe Experience Manager Assets 管理者は、アセットやフォルダーをに公開できます [!DNL Experience Manager Assets Brand Portal] 組織のインスタンス（または公開ワークフローを後の日時にスケジュール）を作成する必要があります。 ただし、最初に [!DNL Experience Manager Assets] と [!DNL Brand Portal]. 詳しくは、 [設定 [!DNL Experience Manager Assets] Brand Portal](configure-aem-assets-with-brand-portal.md).

アセットまたはフォルダーを公開すると、Brand Portalのユーザーがそのアセットまたはフォルダーを使用できるようになります。

その後、 [!DNL Assets]を使用した場合、アセットまたはフォルダーを再公開するまで、変更はBrand Portalに反映されません。 このため、作業中の変更が Brand Portal に提供されることがありません。管理者が公開した承認済みの変更のみが Brand Portal で提供されます。

## Brand Portal へのフォルダーの公開 {#publish-folders-to-brand-portal-1}

1. 次の [!DNL Assets] インターフェイスで、目的のフォルダーの上にマウスポインターを置いて、「 」を選択します。 **[!UICONTROL 公開]** 」オプションを使用します。

   あるいは、目的のフォルダーを選択して後述の手順に従います。

   ![publish2bp](assets/publish2bp.png)

2. **フォルダーを今すぐ公開**

   選択したフォルダーを Brand Portal に公開するには、次のいずれかを実行します。

   * ツールバーで「**[!UICONTROL クイック公開]**」を選択します。次に、メニューから、 **[!UICONTROL Brand Portalに公開]**.
   * ツールバーで「**[!UICONTROL 公開を管理]**」を選択します。

3. 次に、 **[!UICONTROL アクション]** 選択 **[!UICONTROL Brand Portalに公開]**、および **[!UICONTROL スケジュール]** 選択 **[!UICONTROL 今すぐ]**. 「**[!UICONTROL 次へ]」をタップします。**
4. 内 **[!UICONTROL 範囲]**&#x200B;をクリックし、選択を確定してをタップします。 **[!UICONTROL Brand Portalに公開]**.

   フォルダーが Brand Portal への公開用のキューに入れられたことを示すメッセージが表示されます。Brand Portal のインターフェイスにログインして、公開されたフォルダーを確認します。

   **フォルダーを後で公開**

   アセットフォルダーのBrand Portalへの公開ワークフローを後の日時にスケジュールするには：

   1. 公開するアセット/フォルダーを選択したら、「 」を選択します。 **[!UICONTROL 公開を管理]** 上部のツールバーから。
   2. オン **[!UICONTROL 公開を管理]** ページ、選択 **[!UICONTROL Brand Portalに公開]** から **[!UICONTROL アクション]** を選択し、 **[!UICONTROL 後で]** から **[!UICONTROL スケジュール]**.

      ![publishlaterbp](assets/publishlaterbp.png)

   3. 「**[!UICONTROL アクティベート日]**」を選択して時刻を指定します。「**[!UICONTROL 次へ]**」をタップします。
   4. 「**[!UICONTROL 範囲]**」で選択内容を確認します。「**[!UICONTROL 次へ]**」をタップします。
   5. 「**[!UICONTROL ワークフロー]**」でワークフロータイトルを指定します。タップ **[!UICONTROL 後で公開]**.

      ![manageschedulepub](assets/manageschedulepub.png)

## Brand Portal へのフォルダーの非公開 {#unpublish-folders-from-brand-portal}

Brand Portalに公開されているアセットフォルダーを削除するには、次の場所から非公開にします。 [!DNL Experience Manager] オーサーインスタンス。 元のフォルダーを非公開にすると、Brand Portal ユーザーはそのコピーを使用できなくなります。

Brand Portal へのフォルダーの公開をすぐに取り消すことも、取り消しのスケジュールを未来の日時で設定することもできます。Brand Portal へのアセットフォルダーを非公開にするには、次の手順を実行します。

1. 次の [!DNL Assets] ～とのインターフェース [!DNL Experience Manager]  オーサーインスタンス、非公開にするフォルダーを選択します。

   ![publish2bp-1](assets/publish2bp-1.png)

2. ツールバーで「**[!UICONTROL 公開を管理]**」をタップまたはクリックします。

3. **Brand Portal への公開を今すぐ取り消し**

   Brand Portal へのフォルダーの公開をすぐに取り消すには、次のようにします。

   1. オン **[!UICONTROL 公開を管理]** ページ、元 **[!UICONTROL アクション]** 選択 **[!UICONTROL Brand Portalから非公開]** およびから **[!UICONTROL スケジュール]** 選択 **[!UICONTROL 今すぐ]**.
   2. タップまたはクリック **[!UICONTROL 次へ].**
   3. 内 **[!UICONTROL 範囲]**&#x200B;をクリックし、選択を確定してをタップします。 **[!UICONTROL Brand Portalから非公開]**.

   ![confirm-unpublish](assets/confirm-unpublish.png)

   **後でBrand Portalから非公開にする**

   Brand Portal へのフォルダーの公開を停止するスケジュールを未来の日時で設定するには、次のようにします。

   1. オン **[!UICONTROL 公開を管理]** ページ、元 **[!UICONTROL アクション]** 選択 **[!UICONTROL Brand Portalから非公開]** およびから **[!UICONTROL スケジュール]** 選択 **[!UICONTROL 後で].**
   2. 「**[!UICONTROL アクティベート日]**」を選択して時刻を指定します。「**[!UICONTROL 次へ]**」をタップします。
   3. 内 **[!UICONTROL 範囲]**&#x200B;をクリックし、選択を確定してをタップします。 **[!UICONTROL 次へ]**.
   4. を指定します。 **[!UICONTROL ワークフロータイトル]** under **[!UICONTROL ワークフロー]**. タップ **[!UICONTROL 後で非公開にする].**

      ![unpublishworkflows](assets/unpublishworkflows.png)


>[!NOTE]
>
>Brand Portalに対してアセットを公開/非公開にする手順は、フォルダーに対する対応する手順と似ています。
