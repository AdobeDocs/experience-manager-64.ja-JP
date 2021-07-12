---
title: AEM DS の設定
seo-title: AEM DS の設定
description: フォームを送信する前に、処理サーバーの URL を指定する必要があります。
seo-description: フォームを送信する前に、処理サーバーの URL を指定する必要があります。
uuid: 2b415c99-275b-4b67-bb8e-35329514ecbb
contentOwner: amgoyal
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: Configuration
discoiquuid: fbb9044a-a737-45f6-8062-0ef5424a92f8
role: Admin
exl-id: f60beaae-4082-4165-8a37-9d9c94e360b2
source-git-commit: 3c050c33a384d586d74bd641f7622989dc1d6b22
workflow-type: tm+mt
source-wordcount: '257'
ht-degree: 69%

---

# AEM DS の設定 {#configuring-aem-ds-settings}

この記事では、**AEM DS Settings Service** の設定方法について説明します。この設定は、次のような場合に使用できます。

* Correspondence Management内

   * AEM Forms ワークフローを設定する場合
   * ドラフトまたは送信のリモート保存にフォームポータルを使用する場合

* アダプティブフォームにおいては、アダプティブフォームが発行インスタンスから送信される場合

次の手順に従って、「**[!UICONTROL AEM DS 設定]**」を構成します。

1. URLを使用して、パブリッシュインスタンス上のConfiguration Managerを開きます。

   *http://localhost:port/system/console/configMgr*&#x200B;を参照してください。

   ![aem_web_configuration_console](assets/aem_web_configuration_console.png)

1. **[!UICONTROL Adobe Experience Manager Webコンソール設定]**&#x200B;ウィンドウで、「**[!UICONTROL AEM DS設定]**」オプションを探してクリックします。

   ![ds_settings](assets/ds_settings.png)

1. **[!UICONTROL AEM DS 設定サービス]**&#x200B;ウィンドウに、AEM DS コンポーネントの共通設定が表示されます。

   ![ds_settings_1](assets/ds_settings_1.png)

1. 次の情報をそれぞれのフィールドに追加します。

   **[!UICONTROL 処理サーバーURL]**:処理サーバーは、FormsまたはAEMワークフローをトリガーする必要があるサーバーです。これは、AEM オーサーインスタンスの URL または他のサーバー URL（つまり、http://localhost:port/）と同じである可能性があります。

   **[!UICONTROL 処理サーバーのユーザー名]**:使用中のサーバーURLに基づ [くワークフローユーザーのユーザー名]

   **[!UICONTROL 処理サーバーのパスワード]**：ワークフローユーザーのパスワード

   >[!NOTE]
   >
   >* Forms または AEM ワークフローのいずれかを使用しているときは、発行サーバーから送信を行う前に、DS 設定サービスを構成する必要があります。このサービスを構成しないと、フォームの送信が失敗します。

