---
title: Assets と Activity Stream の統合
description: の記録機能を説明します。 [!DNL Experience Manager] および設定方法 [!DNL Experience Manager] を使用して特定のイベントを記録します。
contentOwner: AG
feature: Asset Management
role: Developer
exl-id: c25a4da7-1c58-41cf-9ff6-c094b50208e6
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '308'
ht-degree: 30%

---

# Assets と Activity Stream の統合 {#integrating-assets-with-activity-stream}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

Adobe Experience Manager Assets のユーザーは、アセットの作成、アップロード、削除など、様々な操作を実行します。 ユーザーが何を実行かについて履歴を提供できるよう、これらのアクションを記録することができます。この節では、[!DNL Experience Manager] の記録機能と、特定のイベントを記録するための [!DNL Experience Manager] の設定方法について説明します。

## パフォーマンスに関する考慮事項とデフォルト動作 {#performance-considerations-and-default-behavior}

この統合は、一括して読み込むときなどに多くの CPU およびディスク領域を消費する可能性があります。こうした理由から、 [!DNL Experience Manager] Assets と Activity Stream の統合は、デフォルトで無効になっています。

## サポートされているアクションイベント {#supported-action-events}

記録するイベントは以下のように設定できます。

* 使用許諾済み（許可済み）
* 作成されたアセット (ASSET_CREATED)
* 移動されたアセット (ASSET_MOVED)
* 削除されたアセット (ASSET_REMOVED)
* ライセンス拒否（却下）
* ダウンロードされたアセット（ダウンロード済み）
* バージョン管理されたアセット（バージョン管理）
* 復元されたアセットのバージョン (RESTORED)
* 更新されたアセットメタデータ (METADATA_UPDATED)
* 外部システムに公開されたアセット (PUBLISHED_EXTERNAL)
* アセットのオリジナルの更新 (ORIGINAL_UPDATED)
* 更新されたアセットレンディション (RENDITION_UPDATED)
* 削除されたアセットのレンディション (RENDITION_REMOVED)
* 更新されたサブアセット (SUBASSET_UPDATED)
* サブアセットが削除されました (SUBASSET_REMOVED)

## 設定 [!DNL Assets] イベントの記録 {#configuring-aem-assets-events-recording}

[Web コンソール](/help/sites-deploying/configuring-osgi.md)から、 Event Recorder のチューニングにアクセスできます。[!DNL Assets]次の手順で [!DNL Assets] イベントレコーダー：次の手順に従います。

1. 次に移動： **[!UICONTROL Web コンソール]**

1. クリック **[!UICONTROL 設定]**.

1. ダブルクリック **[!UICONTROL Day CQ DAM Event Recorder]**.

1. チェック **[!UICONTROL このサービスを有効にする]**.

1. 確認する **[!UICONTROL イベントタイプ]** ユーザーアクティビティストリームに記録する

1. 「**[!UICONTROL 保存]**」をクリックします。

## 記録されたイベントの読み取り {#reading-recorded-events}

記録されたイベントはアクティビティとして保存されます。これらを読み取るには、 [ActivityManager API](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/javadoc/com/adobe/granite/activitystreams/ActivityManager.html).
