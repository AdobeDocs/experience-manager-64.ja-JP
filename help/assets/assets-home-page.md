---
title: '"[!DNL Experience Manager Assets] のホームページエクスペリエンス"'
description: ' Assets のホームページをカスタマイズして、アセットに関する最近のアクティビティのスナップショットを始め、有益なスタートアップスクリーンエクスペリエンスを実現できます。'
contentOwner: AG
feature: Developer Tools,Asset Management
role: Admin,User
exl-id: f47c6da7-aa21-4f49-9c66-2a8091e19561
source-git-commit: d9cfb5376210234b3b05877509c273c52d9cecf3
workflow-type: tm+mt
source-wordcount: '557'
ht-degree: 81%

---

# [!DNL Adobe Experience Manager Assets] のホームページエクスペリエンス {#aem-assets-home-page-experience}

[!DNL Experience Manager Assets] のホームページをカスタマイズして、アセットに関する最近のアクティビティのスナップショットを始め、有益なスタートアップスクリーンエクスペリエンスを実現できます。

この [!DNL Adobe Experience Manager Assets] ホームページには、最近表示されたアセットやアップロードされたアセットなど、最近のアクティビティのスナップショットが含まれ、パーソナライズされた豊富なスクリーンエクスペリエンスが提供されます。

Assets のホームページは、デフォルトでは無効になっています。ホームページを有効にするには、次の手順を実行します。

1. アクセスするには [!DNL Experience Manager] Configuration Manager で、 **[!UICONTROL ツール/操作/ Web コンソール]**.
1. 「**Day CQ DAM Event Recorder**」サービスを開きます。
1. 「**[!UICONTROL Enable this service]**」を選択して、アクティビティの記録を有効にします。

   ![chlimage_1-250](assets/chlimage_1-250.png)

1. 記録するイベントを **Event Types** リストから選択して、変更内容を保存します。

   >[!CAUTION]
   >
   >「閲覧したアセット」、「閲覧したプロジェクト」、「閲覧したコレクション」の各オプションを有効にすると、記録対象のイベント数が大幅に増加します。

1. Configuration Manager `https://[AEM_server]:[port]/system/console/configMgr` で「**[!UICONTROL DAM Asset Home Page Feature Flag]**」サービスを開きます。
1. を選択します。 **[!UICONTROL isEnabled.name]** オプションを使用して、Assets のホームページ機能を有効にします。 変更内容を保存します。

   ![chlimage_1-251](assets/chlimage_1-251.png)

1. **[!UICONTROL User Preferences]** ダイアログを開き、「**[!UICONTROL Enable Assets Home Page]**」を選択します。変更内容を保存します。

   ![user_preferences](assets/user_preferences.png)

アセットのホームページを有効にした後、ナビゲーションページから Assets ユーザーインターフェイスに移動します。

![home_page](assets/home_page.png)

次をタップまたはクリックします。 **[!UICONTROL エクスペリエンスリンクを設定するには、ここをクリックしてください]** ユーザー名、背景画像、プロファイル画像を追加します。

Assets のホームページには次のセクションが含まれます。

* 「ようこそ」セクション
* 「ウィジェット」セクション

**「ようこそ」セクション**

ユーザーのプロファイルが存在する場合、「ようこそ」セクションには、そのユーザー向けのようこそメッセージが表示されます。さらに、そのユーザーのプロファイル写真とようこそ画像（既に設定されている場合）も表示されます。

ユーザーのプロファイル設定が完了していない場合、「ようこそ」セクションには、一般的なようこそメッセージとプロファイル写真用のプレースホルダーが表示されます。

**「ウィジェット」セクション**

このセクションは「ようこそ」セクションの下にあり、既製ウィジェットが次のセクションに表示されます。

* アクティビティ
* 最近の表示
* 最新情報

**アクティビティ**：このセクションの&#x200B;**マイアクティビティ**&#x200B;ウィジェットには、アセット（レンディションなしのアセットも含む）を使用してログインユーザーが実行した最近のアクティビティが表示されます。例えば、アセットのアップロード、ダウンロード、アセットの作成、編集、コメント、注釈、共有です。

**最近の表示**：このセクションの&#x200B;**最近表示された項目**&#x200B;ウィジェットには、最近ログインユーザーがアクセスしたエンティティが表示されます。フォルダー、コレクション、プロジェクトが含まれます。

**Discover**:この **新規** このセクションのウィジェットには、 [!DNL Assets] インスタンス。

ユーザーアクティビティデータのパージを有効にするには、Configuration Manager で「**DAM Event Purge Service**」を有効にします。このサービスを有効にすると、ログインユーザーのアクティビティのうち指定した数を超えたものがシステムによって削除されます。

ようこそ画面には、フォルダー、コレクション、カタログにアクセスするためのツールバー上のアイコンなど、簡単に操作するための機能が含まれています。

>[!NOTE]
>
>「Day CQ DAM Event Recorder」サービスと「DAM Event Purge」サービスを有効にすると、JCR や検索インデックスへの書き込み操作が増加して、[!DNL Experience Manager] サーバーに対する負荷が大幅に増加します。[!DNL Experience Manager] サーバーの負荷が増えると、パフォーマンスに影響が出ることがあります。

>[!CAUTION]
>
>Assets のホームページで必要なユーザーアクティビティのキャプチャ、フィルタリングおよびパージをおこなうと、パフォーマンスのオーバーヘッドが発生します。そのため、管理者はターゲットユーザーのためにホームページを効果的に設定する必要があります。
>
>一括操作を実行する管理者およびユーザーは、ユーザーアクティビティが増えるのを避けるため、Asset のホームページ機能を使用しないことをお勧めします。また、管理者は、Configuration Manager で「**Day CQ DAM Event Recorder**」を設定することで、特定のユーザーの記録アクティビティを除外することができます。
>
>この機能を使用する場合は、サーバー負荷を考慮してパージの頻度のスケジュールを設定することをお勧めします。
