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
ht-degree: 37%

---

# Correspondence Management Solution の設定 {#configuring-a-correspondence-management-solution}

## VersionRestoreManagerImpl のオーサーインスタンス URL の定義 {#defining-author-instance-url-for-versionrestoremanagerimpl}

オーサーインスタンスのバージョンを復元するオーサーインスタンスの URL を定義するには、次の手順を実行します。

1. *https://:&lt;PublishHost>:&lt;PublishPort>/lc/system/console/configMgr* に移動します。OSGi Management Console のユーザー資格情報を使ってログインします。デフォルトの資格情報は、admin/admin です。
1. 「**[!UICONTROL com.adobe.livecycle.content.activate.impl.VersionRestoreManagerImpl.name]**」設定の横にある「**[!UICONTROL 編集]**」アイコンをクリックします。
1. 「**[!UICONTROL VersionRestoreManager Author URL]**」フィールドで、オーサーインスタンス VersionRestoreManager の URL を指定します。

   **URL 文字列**:

   `https://<hostname>:<port>:/libs/fd/fdm/content/crud/lc.content.remote.activate.VersionRestoreManager`

   >[!NOTE]
   >
   >ロードバランサーの前に複数のオーサーインスタンス（クラスター化）がある場合は、「**[!UICONTROL VersionRestoreManager Author URL]**」フィールドにその URL を指定します。

1. 「**[!UICONTROL 保存]**」をクリックします。

## ActivationManagerImpl のパブリッシュインスタンス URL の定義（パブリックインスタンスアクティベーションマネージャー） {#defining-the-publish-instance-url-for-activationmanagerimpl-public-instance-activation-manager}

パブリックインスタンスアクティベーションマネージャーのパブリッシュインスタンス URL を定義する手順は次のとおりです。

1. *https://:&lt;authorHost>:&lt;authorPort>/lc/system/console/configMgr* に移動します。OSGi Management Console のユーザー資格情報を使ってログインします。デフォルトの資格情報は、admin/admin です。
1. を検索して、 **[!UICONTROL 編集]** 横のアイコン **[!UICONTROL com.adobe.livecycle.content.activate.impl.ActivationManagerImpl.name]** 設定。
1. 内 **[!UICONTROL ActivationManager 公開 URL]** 「 」フィールドで、パブリッシュインスタンスの ActivationManager にアクセスするための URL を指定します。 次の URL を指定できます。

   * **ロードバランサー URL （推奨）**:ロードバランサー URL を指定します。パブリッシュファーム（複数の非クラスター化パブリッシュインスタンス）の前にロードバランサーとして機能する Web サーバーがある場合。
   * **パブリッシュインスタンス URL**:任意のパブリッシュインスタンス URL を指定します。1 つのパブリッシュインスタンスが存在する場合、またはパブリッシュファームを前面に配置する Web サーバーが、制限によりオーサー環境からアクセスできない場合。 指定したパブリッシュインスタンスが停止した場合は、オーサー側で対処するフォールバックメカニズムがあります。
   * **URL 文字列**：

      `https://<hostname>:<port>:/libs/fd/fdm/content/crud/lc.content.remote.activate.activationManager`

1. 「**[!UICONTROL 保存]**」をクリックします。

Correspondence Management の設定について詳しくは、 [Correspondence Management 設定プロパティ](https://helpx.adobe.com/jp/aem-forms/6-2/cm-configuration-properties.html).
