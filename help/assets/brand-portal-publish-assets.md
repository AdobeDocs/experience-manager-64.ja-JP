---
title: Brand Portal へのフォルダーの公開
description: Brand Portalにアセットを公開および非公開する方法を説明します。
contentOwner: VG
feature: Brand Portal
role: Business Practitioner
translation-type: tm+mt
source-git-commit: 75312539136bb53cf1db1de03fc0f9a1dca49791
workflow-type: tm+mt
source-wordcount: '425'
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

* ツールバーで「**[!UICONTROL クイック公開]**」を選択します。次に、メニューから「**[!UICONTROL ブランドポータルに公開]**」を選択します。

* ツールバーで「**[!UICONTROL 公開を管理]**」を選択します。

   1. 次に、**[!UICONTROL アクション]**&#x200B;で「**[!UICONTROL ブランドポータルに公開]**」を選択し、**[!UICONTROL スケジュール]**&#x200B;で「**[!UICONTROL 今すぐ]**」を選択します。 「**[!UICONTROL 次へ]」をタップまたはクリックします。**

   2. **[!UICONTROL スコープ]**&#x200B;内で、選択を確認し、「**[!UICONTROL ブランドポータルに発行]**」をタップまたはクリックします。

アセットが Brand Portal への公開用のキューに入れられたことを示すメッセージが表示されます。Brand Portal のインターフェイスにログインして、公開されたアセットを確認します。

## アセットを後で公開 {#publish-later}

アセットを Brand Portal に公開するスケジュールを後の日時に設定するには、次の手順を実行します。

1. 発行するアセット/フォルダを選択したら、上部のツールバーから「**[!UICONTROL パブリケーションを管理]**」を選択します。
2. **[!UICONTROL パブリケーションの管理]**&#x200B;ページで、**[!UICONTROL アクション]**&#x200B;から「**[!UICONTROL ブランドポータルに公開]**」を選択し、**[!UICONTROL スケジュール]**&#x200B;から「**[!UICONTROL 後で]**」を選択します。

   ![publishlaterbp-1](assets/publishlaterbp-1.png)

3. 「**[!UICONTROL アクティベート日]**」を選択して時刻を指定します。「**[!UICONTROL 次へ]**」をタップまたはクリックします。
4. 「**[!UICONTROL アクティベート日]**」を選択して時刻を指定します。「**[!UICONTROL 次へ]**」をタップまたはクリックします。
5. 「**[!UICONTROL ワークフロー]**」でワークフロータイトルを指定します。「**[!UICONTROL 後で公開]**」をタップまたはクリックします。

   ![publishworkflow](assets/publishworkflow.png)

次に、Brand Portalにログインして、公開されたアセットがBrand Portalインターフェイスで使用できるかどうかを確認します。

![bp_631_landing_page](assets/bp_landing_page.png)
