---
title: "[!DNL Experience Manager Assets] のホームページエクスペリエンス"
description: アセットのホームページをパーソナライズして、アセットに関する最近のアクティビティのスナップショットなど、豊富なようこそ画面を使用できます。
contentOwner: AG
feature: Developer Tools,Asset Management
role: Admin,User
exl-id: f47c6da7-aa21-4f49-9c66-2a8091e19561
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '593'
ht-degree: 47%

---

# [!DNL Adobe Experience Manager Assets] のホームページエクスペリエンス {#aem-assets-home-page-experience}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

[!DNL Experience Manager Assets] のホームページをカスタマイズして、アセットに関する最近のアクティビティのスナップショットを始め、有益なスタートアップスクリーンエクスペリエンスを実現できます。

この [!DNL Adobe Experience Manager Assets] ホームページには、最近表示されたアセットやアップロードされたアセットなど、最近のアクティビティのスナップショットが含まれ、パーソナライズされた豊富なスクリーンエクスペリエンスが提供されます。

アセットのホームページはデフォルトで無効になっています。 ホームページを有効にするには、次の手順を実行します。

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

Assets のホームページには、次のセクションが含まれます。

* ようこそセクション
* ウィジェットセクション

**ようこそセクション**

自分のプロフィールが存在する場合は、「ようこそ」セクションに、自分宛てのようこそメッセージが表示されます。 さらに、そのユーザーのプロファイル写真とようこそ画像（既に設定されている場合）も表示されます。

プロフィールが不完全な場合は、「ようこそ」セクションに、一般的なようこそメッセージと、プロフィール画像のプレースホルダーが表示されます。

**ウィジェットセクション**

このセクションは「ようこそ」セクションの下に表示され、次のセクションの下に標準のウィジェットが表示されます。

* アクティビティ
* 最近の表示
* 最新情報

**アクティビティ**：このセクションの&#x200B;**マイアクティビティ**&#x200B;ウィジェットには、アセット（レンディションなしのアセットも含む）を使用してログインユーザーが実行した最近のアクティビティが表示されます。例えば、アセットのアップロード、ダウンロード、アセットの作成、編集、コメント、注釈、共有です。

**最近の表示**：このセクションの&#x200B;**最近表示された項目**&#x200B;ウィジェットには、最近ログインユーザーがアクセスしたエンティティが表示されます。フォルダー、コレクション、プロジェクトが含まれます。

**Discover**:この **新規** このセクションのウィジェットには、 [!DNL Assets] インスタンス。

ユーザーアクティビティデータのパージを有効にするには、Configuration Manager で「**DAM Event Purge Service**」を有効にします。このサービスを有効にすると、指定した数を超えるログインユーザーのアクティビティはシステムによって削除されます。

ようこそ画面には、フォルダー、コレクション、カタログにアクセスするためのツールバーのアイコンなど、簡単なナビゲーションツールが表示されます。

>[!NOTE]
>
>「Day CQ DAM Event Recorder」サービスと「DAM Event Purge」サービスを有効にすると、JCR や検索インデックスへの書き込み操作が増加して、[!DNL Experience Manager] サーバーに対する負荷が大幅に増加します。[!DNL Experience Manager] サーバーの負荷が増えると、パフォーマンスに影響が出ることがあります。

>[!CAUTION]
>
>アセットのホームページで必要なユーザーアクティビティのキャプチャ、フィルタリングおよびパージは、パフォーマンスにオーバーヘッドを課します。 したがって、管理者は、ターゲットユーザーに対して効果的にホームページを設定する必要があります。
>
>Adobeでは、一括操作を実行する管理者とユーザーに対して、ユーザーアクティビティの増加を防ぐために、アセットのホームページ機能を使用しないようにすることをお勧めします。 また、管理者は、Configuration Manager で「**Day CQ DAM Event Recorder**」を設定することで、特定のユーザーの記録アクティビティを除外することができます。
>
>この機能を使用する場合は、サーバー負荷を考慮してパージの頻度のスケジュールを設定することをお勧めします。
