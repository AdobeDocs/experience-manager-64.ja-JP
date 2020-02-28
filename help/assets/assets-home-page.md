---
title: AEM Assets のホームページの使用
description: AEM Assets のホームページをカスタマイズして、アセットに関する最近のアクティビティのスナップショットを始め、有益なスタートアップスクリーンエクスペリエンスを実現できます。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 0d70a672a2944e2c03b54beb3b5f734136792ab1

---


# AEM Assets のホームページの使用 {#aem-assets-home-page-experience}

AEM Assets のホームページをカスタマイズして、アセットに関する最近のアクティビティのスナップショットを始め、有益なスタートアップスクリーンエクスペリエンスを実現できます。

Adobe Experience Manager（AEM）Assets のホームページでは、最近のアクティビティのスナップショット（最近表示またはアップロードされたアセットなど）を始め、カスタマイズした有益なスタートアップスクリーンエクスペリエンスを実現できます。

Assets のホームページは、デフォルトでは無効になっています。ホームページを有効にするには、次の手順を実行します。

1. AEM Configuration Managerにアクセスするには、ツール/操作/Web **[!UICONTROL コンソールをクリックします]**。
1. Open the **Day CQ DAM Event Recorder** service.
1. Select the **[!UICONTROL Enable this service]** to enable activity recording.

   ![chlimage_1-250](assets/chlimage_1-250.png)

1. From the **Event Types** list, select the events to be recorded and save the changes.

   >[!CAUTION]
   >
   >「Asset viewed」、「Projects viewed」、「Collections viewed」の各オプションを有効にすると、記録対象のイベント数が大幅に増加します。

1. Open the **[!UICONTROL DAM Asset Home Page Feature Flag]** service from Configuration Manager `https://[AEM_server]:[port]/system/console/configMgr`.
1. Select the **[!UICONTROL isEnabled.name]** option to enable the Assets Home page feature. 変更内容を保存します。

   ![chlimage_1-251](assets/chlimage_1-251.png)

1. Open the **[!UICONTROL User Preferences]** dialog, and select **[!UICONTROL Enable Assets Home Page]**. 変更内容を保存します。

   ![user_preferences](assets/user_preferences.png)

アセットのホームページを有効にした後、ナビゲーションページからアセットユーザーインターフェイスに移動します。

![home_page](assets/home_page.png)

Tap/click the **[!UICONTROL Click here to configure your experience link]** to add your username, background image, and profile image.

Assets のホームページには次のセクションが含まれます。

* 「ようこそ」セクション
* 「ウィジェット」セクション

**「ようこそ」セクション**

ユーザーのプロファイルが存在する場合、「ようこそ」セクションには、そのユーザー向けのようこそメッセージが表示されます。さらに、プロフィール画像とウェルカム画像が表示されます（既に設定されている場合）。

ユーザーのプロファイル設定が完了していない場合、「ようこそ」セクションには、一般的なようこそメッセージとプロファイル写真用のプレースホルダーが表示されます。

**「ウィジェット」セクション**

このセクションは「ようこそ」セクションの下にあり、既製ウィジェットが次のセクションに表示されます。

* アクティビティ
* 最近の表示
* 最新情報

**アクティビティ**:この節では、マイアクティビティ **** ウィジェットは、アセット（レンディションなしのアセットを含む）を持つログインユーザーによって実行された最近のアクティビティ（アセットのアップロード、ダウンロード、アセットの作成、編集、コメント、注釈、共有など）を表示します。

**最新**:このセク **ションの下の最近表示したWidgetには** 、フォルダー、コレクション、プロジェクトなど、ログインユーザーが最近アクセスしたエンティティが表示されます。

**Discover**:このセク **ションの新規** Widgetには、AEM Assetsインスタンスに最近アップロードされたアセットとレンディションが表示されます。

To enable purging of user activity data, enable the **DAM Event Purge Service** from Configuration Manager. このサービスを有効にすると、ログインユーザーのアクティビティのうち指定した数を超えたものがシステムによって削除されます。

ようこそ画面には、フォルダー、コレクション、カタログにアクセスするためのツールバー上のアイコンなど、簡単に操作するための機能が含まれています。

>[!NOTE]
>
>Day CQ DAM Event RecorderサービスとDAM Event purgeサービスを有効にすると、JCRおよび検索インデックスへの書き込み操作が増え、AEMサーバーの負荷が大幅に増加します。 AEM サーバーの負荷が増えるとパフォーマンスに影響が出ることがあります。

>[!CAUTION]
>
>Assets のホームページで必要なユーザーアクティビティのキャプチャ、フィルタリングおよびパージをおこなうと、パフォーマンスのオーバーヘッドが発生します。そのため、管理者はターゲットユーザーのためにホームページを効果的に設定する必要があります。
>
>一括操作を実行する管理者およびユーザーは、ユーザーアクティビティが増えるのを避けるため、Asset のホームページ機能を使用しないことをお勧めします。また、管理者は、設定マネージャーで「**Day CQ DAM Event Recorder**」を設定することで、特定のユーザーの記録アクティビティを除外することができます。
>
>この機能を使用する場合は、サーバー負荷を考慮してパージの頻度を計画することをお勧めします。
