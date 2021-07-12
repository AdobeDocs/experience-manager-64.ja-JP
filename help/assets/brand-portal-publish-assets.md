---
title: Brand Portal へのフォルダーの公開
description: Brand Portalへのアセットの公開と非公開の方法について説明します。
contentOwner: VG
feature: Brand Portal
role: User
exl-id: 6b78124d-4022-452f-8d0f-b667de337bf4
source-git-commit: 3c050c33a384d586d74bd641f7622989dc1d6b22
workflow-type: tm+mt
source-wordcount: '423'
ht-degree: 52%

---

# Brand Portal へのアセットの公開 {#publish-assets-to-brand-portal}

Adobe Experience Manager(AEM)Assets管理者は、組織のAEM Assets Brand Portalインスタンスにアセットを公開（または公開ワークフローを後の日時にスケジュール）できます。 ただし、最初にAEM AssetsとBrand Portalを連携させるように設定する必要があります。 詳しくは [AEM Assets と Brand Portal の連携の設定](configure-aem-assets-with-brand-portal.md)を参照してください。

公開したアセットは、Brand Portalでユーザーが利用できます。

その後、AEM Assetsで元のアセットに変更を加えても、その変更はアセットを再公開するまでBrand Portalに反映されません。 このため、作業中の変更が Brand Portal に提供されることがありません。管理者が公開した承認済みの変更のみが Brand Portal で提供されます。

レプリケーションが正常に終了したら、アセット、フォルダー、コレクションを Brand Portal に公開することができます。アセットを Brand Portal に公開するには、次の手順を実行します。

>[!NOTE]
>
>AEM オーサーが過剰なリソースを占有しないように、できればピーク時を避け、時間をずらして公開することをお勧めします。

1. アセットコンソールで目的のアセットにマウスポインターを置き、クイックアクションから「**[!UICONTROL 公開]**」オプションを選択します。

   または、Brand Portal に公開するアセットを選択します。

   ![publish2bp-2](assets/publish2bp-2.png)

2. アセットをBrand Portalに公開するには、次の2つのオプションを使用できます。
   * [アセットを直ちに公開する](#publish-now)
   * [アセットを後で公開](#publish-later)

## アセットを今すぐ公開 {#publish-now}

選択したアセットを Brand Portal に公開するには、次のいずれかを実行します。

* ツールバーで「**[!UICONTROL クイック公開]**」を選択します。次に、メニューから「**[!UICONTROL Brand Portalに公開]**」を選択します。

* ツールバーで「**[!UICONTROL 公開を管理]**」を選択します。

   1. 次に、「**[!UICONTROL アクション]**」から「**[!UICONTROL Brand Portalに公開]**」を選択し、「**[!UICONTROL スケジュール]**」から「**[!UICONTROL 今すぐ]**」を選択します。 **[!UICONTROL 「次へ]」をタップまたはクリックします。**

   2. **[!UICONTROL 範囲]**&#x200B;内で選択を確定し、「**[!UICONTROL Brand Portalに公開]**」をタップまたはクリックします。

アセットが Brand Portal への公開用のキューに入れられたことを示すメッセージが表示されます。Brand Portal のインターフェイスにログインして、公開されたアセットを確認します。

## アセットを後で公開 {#publish-later}

アセットを Brand Portal に公開するスケジュールを後の日時に設定するには、次の手順を実行します。

1. 公開するアセット/フォルダーを選択したら、上部のツールバーから「**[!UICONTROL 公開を管理]**」を選択します。
2. **[!UICONTROL 公開を管理]**&#x200B;ページで、**[!UICONTROL アクション]**&#x200B;から「**[!UICONTROL Brand Portalに公開]**」を選択し、**[!UICONTROL スケジュール]**&#x200B;から「**[!UICONTROL 後で]**」を選択します。

   ![publishlaterbp-1](assets/publishlaterbp-1.png)

3. 「**[!UICONTROL アクティベート日]**」を選択して時刻を指定します。「**[!UICONTROL 次へ]**」をタップまたはクリックします。
4. 「**[!UICONTROL アクティベート日]**」を選択して時刻を指定します。「**[!UICONTROL 次へ]**」をタップまたはクリックします。
5. 「**[!UICONTROL ワークフロー]**」でワークフロータイトルを指定します。「**[!UICONTROL 後で公開]**」をタップまたはクリックします。

   ![publishworkflow](assets/publishworkflow.png)

次に、Brand Portalにログインして、公開したアセットがBrand Portalインターフェイスで使用可能かどうかを確認します。

![bp_631_landing_page](assets/bp_landing_page.png)
