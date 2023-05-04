---
title: Brand Portal へのフォルダーの公開
description: フォルダーをBrand Portalに公開および非公開にする方法を説明します。
contentOwner: VG
feature: Brand Portal
role: User
exl-id: f41ab750-5780-42ae-a131-5bc748280215
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '588'
ht-degree: 49%

---

# Brand Portal へのフォルダーの公開 {#publish-folders-to-brand-portal}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

Adobe Experience Manager Assets 管理者は、アセットやフォルダーをに公開できます [!DNL Experience Manager Assets Brand Portal] 組織のインスタンス（または公開ワークフローを後の日時にスケジュール）を作成する必要があります。 ただし、最初に [!DNL Experience Manager Assets] と [!DNL Brand Portal]. 詳しくは、 [設定 [!DNL Experience Manager Assets] Brand Portal](configure-aem-assets-with-brand-portal.md).

アセットまたはフォルダーを公開すると、Brand Portal のユーザーが使用できるようになります。

その後、 [!DNL Assets]を使用した場合、アセットまたはフォルダーを再公開するまで、変更はBrand Portalに反映されません。 このため、作業中の変更が Brand Portal に提供されることがありません。管理者が公開した承認済みの変更のみが Brand Portal で提供されます。

## Brand Portal へのフォルダーの公開 {#publish-folders-to-brand-portal-1}

1. 次の [!DNL Assets] インターフェイスで、目的のフォルダーの上にマウスポインターを置いて、「 」を選択します。 **[!UICONTROL 公開]** 」オプションを使用します。

   あるいは、目的のフォルダーを選択して後述の手順に従います。

   ![publish2bp](assets/publish2bp.png)

2. **フォルダーを今すぐ公開**

   選択したフォルダーをBrand Portalに公開するには、次のいずれかの操作を行います。

   * ツールバーで「**[!UICONTROL クイック公開]**」を選択します。次に、メニューで「**[!UICONTROL Brand Portal に公開]**」を選択します。
   * ツールバーで「**[!UICONTROL 公開を管理]**」を選択します。

3. 次に、**[!UICONTROL アクション]**&#x200B;から「**[!UICONTROL Brand Portal に公開]**」を選択し、**[!UICONTROL スケジュール]**&#x200B;から「**[!UICONTROL 今すぐ]**」を選択します。「**[!UICONTROL 次へ]」をタップします。**
4. 内 **[!UICONTROL 範囲]**&#x200B;をクリックし、選択を確定してをタップします。 **[!UICONTROL Brand Portalに公開]**.

   フォルダーが Brand Portal への公開用のキューに入れられたことを示すメッセージが表示されます。Brand Portalインターフェイスにログインして、公開されたフォルダーを確認します。

   **フォルダーを後で公開**

   次のように、アセットフォルダーの Brand Portal ワークフローへの公開を、後の日時でスケジュールします。

   1. 公開するアセットまたはフォルダーを選択したら、上部のツールバーから「**[!UICONTROL 公開を管理]**」を選択します。
   2. **[!UICONTROL 公開を管理]**&#x200B;ページで、**[!UICONTROL アクション]**&#x200B;から「**[!UICONTROL Brand Portal に公開]**」を選択し、**[!UICONTROL スケジュール]**&#x200B;から「**[!UICONTROL 後で]**」を選択します。

      ![publishlaterbp](assets/publishlaterbp.png)

   3. 「**[!UICONTROL アクティベート日]**」を選択して時刻を指定します。「**[!UICONTROL 次へ]**」をタップします。
   4. 「**[!UICONTROL 範囲]**」で選択内容を確認します。「**[!UICONTROL 次へ]**」をタップします。
   5. 「**[!UICONTROL ワークフロー]**」でワークフロータイトルを指定します。タップ **[!UICONTROL 後で公開]**.

      ![manageschedulepub](assets/manageschedulepub.png)

## Brand Portal へのフォルダーの非公開 {#unpublish-folders-from-brand-portal}

Brand Portalに公開されているアセットフォルダーを削除するには、次の場所から非公開にします。 [!DNL Experience Manager] オーサーインスタンス。 元のフォルダーを非公開にすると、Brand Portal ユーザーはそのコピーを使用できなくなります。

すばやくBrand Portalからフォルダーを非公開にするか、後でフォルダーをスケジュールするかのオプションがあります。 Brand Portal へのアセットフォルダーを非公開にするには、次の手順を実行します。

1. 次の [!DNL Assets] ～とのインターフェース [!DNL Experience Manager]  オーサーインスタンス、非公開にするフォルダーを選択します。

   ![publish2bp-1](assets/publish2bp-1.png)

2. ツールバーのをタップまたはクリックします。 **[!UICONTROL 公開を管理]**.

3. **今すぐBrand Portalから非公開にする**

   目的のフォルダーをBrand Portalからすばやく非公開にするには、次の手順を実行します。

   1. オン **[!UICONTROL 公開を管理]** ページ、元 **[!UICONTROL アクション]** 選択 **[!UICONTROL Brand Portalから非公開]** およびから **[!UICONTROL スケジュール]** 選択 **[!UICONTROL 今すぐ]**.
   2. タップまたはクリック **[!UICONTROL 次へ].**
   3. 内 **[!UICONTROL 範囲]**&#x200B;をクリックし、選択を確定してをタップします。 **[!UICONTROL Brand Portalから非公開]**.

   ![confirm-unpublish](assets/confirm-unpublish.png)

   **Brand Portal への公開を後で取り消し**

   Brand Portal へのフォルダーの公開を停止するスケジュールを未来の日時で設定するには、次のようにします。

   1. オン **[!UICONTROL 公開を管理]** ページ、元 **[!UICONTROL アクション]** 選択 **[!UICONTROL Brand Portalから非公開]** およびから **[!UICONTROL スケジュール]** 選択 **[!UICONTROL 後で].**
   2. 「**[!UICONTROL アクティベート日]**」を選択して時刻を指定します。「**[!UICONTROL 次へ]**」をタップします。
   3. 内 **[!UICONTROL 範囲]**&#x200B;をクリックし、選択を確定してをタップします。 **[!UICONTROL 次へ]**.
   4. を指定します。 **[!UICONTROL ワークフロータイトル]** under **[!UICONTROL ワークフロー]**. タップ **[!UICONTROL 後で非公開にする].**

      ![unpublishworkflows](assets/unpublishworkflows.png)


>[!NOTE]
>
>Brand Portal に対してアセットを公開または非公開にする手順は、フォルダーの場合の手順と同様です。
