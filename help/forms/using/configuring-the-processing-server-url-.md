---
title: AEM DS の設定
seo-title: Configuring AEM DS settings
description: フォームを送信する前に、処理サーバーの URL を指定する必要があります。
seo-description: You need to specify the processing server URL before you submit a form.
uuid: 2b415c99-275b-4b67-bb8e-35329514ecbb
contentOwner: amgoyal
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: Configuration
discoiquuid: fbb9044a-a737-45f6-8062-0ef5424a92f8
role: Admin
exl-id: f60beaae-4082-4165-8a37-9d9c94e360b2
source-git-commit: 3c050c33a384d586d74bd641f7622989dc1d6b22
workflow-type: tm+mt
source-wordcount: '240'
ht-degree: 40%

---

# AEM DS の設定 {#configuring-aem-ds-settings}

この記事では、 **AEM DS Settings Service**. この設定は、次のような複数のシナリオで使用できます。

* Correspondence Management では

   * AEM Forms Workflow を設定する場合
   * ドラフト/送信のリモート保存にフォームポータルを使用する場合

* アダプティブフォームでは、パブリッシュインスタンスからアダプティブフォームが送信された場合に使用します。

次に、 **[!UICONTROL AEM DS 設定]**:

1. 次の URL で、パブリッシュインスタンスにある Configuration Manager を開きます。

   *http://localhost:port/system/console/configMgr*.

   ![aem_web_configuration_console](assets/aem_web_configuration_console.png)

1. **[!UICONTROL Adobe Experience Manager web コンソール設定]**&#x200B;ウィンドウで、「**[!UICONTROL AEM DS 設定]**」オプションを見つけてクリックします。

   ![ds_settings](assets/ds_settings.png)

1. **[!UICONTROL AEM DS 設定サービス]**&#x200B;ウィンドウに、AEM DS コンポーネントの共通設定が表示されます。

   ![ds_settings_1](assets/ds_settings_1.png)

1. 次の情報をそれぞれのフィールドに追加します。

   **[!UICONTROL 処理サーバー URL]**：処理サーバーは、Forms または AEM ワークフローをトリガーする必要のあるサーバーです。これは、AEMオーサーインスタンスの URL または他のサーバー URL( 例：http:// localhost:port/) と同じにすることができます。

   **[!UICONTROL 処理サーバーのユーザー名]**：ワークフローユーザーのユーザー名は、[使用するサーバー URL に基づいています]

   **[!UICONTROL 処理サーバーのパスワード]**:ワークフローユーザーのパスワード

   >[!NOTE]
   >
   >* FormsまたはAEMワークフローを使用している場合、パブリッシュサーバーから送信する前に、DS 設定サービスを設定する必要があります。 そうしないと、フォームの送信が失敗します。

