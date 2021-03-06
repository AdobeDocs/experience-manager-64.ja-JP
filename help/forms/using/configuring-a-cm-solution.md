---
title: Correspondence Management Solution の設定
seo-title: Configuring a Correspondence Management solution
description: オーサーインスタンスバージョンの復元用にオーサーインスタンス URL を定義し、パブリックインスタンスアクティベーションマネージャー用にパブリッシュインスタンス URL を定義する方法について説明します。
seo-description: Learn how to define an author instance URL for the author instance version restore and define the Publish instance URL for public instance activation manager.
uuid: 76b25004-fe47-44d7-9bed-7c0fd963306b
topic-tags: correspondence-management
content-type: reference
products: SG_EXPERIENCEMANAGER/6.3/FORMS
discoiquuid: 186ca75c-638b-4057-826e-cd5d56aa0397
feature: Correspondence Management
exl-id: a062957d-a526-4c4b-bbc5-0cda8ab007a3
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '311'
ht-degree: 71%

---

# Correspondence Management Solution の設定 {#configuring-a-correspondence-management-solution}

## VersionRestoreManagerImpl の作成者インスタンス URL の定義 {#defining-author-instance-url-for-versionrestoremanagerimpl}

作成者インスタンスバージョンのリストアの作成者インスタンス URL を定義するには、以下の手順を実行します。

1. に移動します。 *https://:&lt;publishhost>:&lt;publishport>/lc/system/console/configMgr*. OSGi Management Console のユーザー資格情報を使ってログインします。デフォルトの資格情報は、admin/admin です。
1. 「**[!UICONTROL com.adobe.livecycle.content.activate.impl.VersionRestoreManagerImpl.name]**」設定の横にある「**[!UICONTROL 編集]**」アイコンをクリックします。
1. 内 **[!UICONTROL VersionRestoreManager 作成者の URL]** 「 」フィールドで、VersionRestoreManager のオーサーインスタンスの URL を指定します。

   **URL 文字列**:

   `https://<hostname>:<port>:/libs/fd/fdm/content/crud/lc.content.remote.activate.VersionRestoreManager`

   >[!NOTE]
   >
   >ロードバランサーの前に複数のオーサーインスタンス（クラスター化）がある場合は、 **[!UICONTROL VersionRestoreManager 作成者の URL]** フィールドに入力します。

1. 「**[!UICONTROL 保存]**」をクリックします。

## ActivationManagerImpl（発行インスタンス Activation Manager）の発行インスタンス URL の定義 {#defining-the-publish-instance-url-for-activationmanagerimpl-public-instance-activation-manager}

発行インスタンス ActivationManager の発行インスタンス URL を定義するには、以下の手順を実行します。

1. に移動します。 *https://:&lt;authorhost>:&lt;authorport>/lc/system/console/configMgr*. OSGi Management Console のユーザー資格情報を使ってログインします。デフォルトの資格情報は、admin/admin です。
1. 「**[!UICONTROL com.adobe.livecycle.content.activate.impl.ActivationManagerImpl.name]**」設定の横にある「**[!UICONTROL 編集]**」アイコンをクリックします。
1. 「**[!UICONTROL ActivationManager Publish URL]**」フィールドで、発行インスタンス ActivationManager にアクセスするための URL を指定します。次の URL を指定できます。

   * **ロードバランサー URL（推奨）**：発行ファーム（複数の非クラスター発行インスタンス）の前にロードバランサーとして機能する Web サーバーを持っている場合は、そのロードバランサーの URL を指定します。
   * **発行インスタンス URL**: 単一の発行インスタンスのみを持っている場合、あるいは発行ファーム前段の Web サーバーが何らかの理由で作成者完了からアクセスできない場合、任意の発行インスタンス URL を指定します。指定した発行インスタンスがダウンした場合は、フォールバックメカニズムが機能して作成者側で処理します。
   * **URL 文字列**:

      `https://<hostname>:<port>:/libs/fd/fdm/content/crud/lc.content.remote.activate.activationManager`

1. 「**[!UICONTROL 保存]**」をクリックします。

Correspondence Management の設定方法と詳細は、[Correspondence Management 設定プロパティ](https://helpx.adobe.com/aem-forms/6-2/cm-configuration-properties.html)を参照してください。
