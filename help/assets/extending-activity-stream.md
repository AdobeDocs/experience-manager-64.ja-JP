---
title: Assets とアクティビティストリームの統合
description: 特定のイベントを記録する [!DNL Experience Manager] and how to configure [!DNL Experience Manager] の記録機能について説明します。
contentOwner: AG
feature: Asset Management
role: Developer
exl-id: c25a4da7-1c58-41cf-9ff6-c094b50208e6
source-git-commit: cc9b6d147a93688e5f96620d50f8fc8b002e2d0d
workflow-type: tm+mt
source-wordcount: '268'
ht-degree: 67%

---

# Assets とアクティビティストリームの統合 {#integrating-assets-with-activity-stream}

Adobe Experience Manager Assetsのユーザーは、アセットの作成、アップロード、削除など、様々な操作を実行します。 ユーザーが何を実行かについて履歴を提供できるよう、これらのアクションを記録することができます。この節では、[!DNL Experience Manager]の記録機能と、特定のイベントを記録するための[!DNL Experience Manager]の設定方法について説明します。

## パフォーマンスに関する考慮事項とデフォルトの動作 {#performance-considerations-and-default-behavior}

この統合は、一括して読み込むときなどに多くの CPU およびディスク領域を消費する可能性があります。このため、アクティビティストリームとの[!DNL Experience Manager] Assets統合は、デフォルトで無効になっています。

## サポートされるアクションイベント {#supported-action-events}

以下のイベントを記録対象として設定できます。

* ライセンス許可（ACCEPTED）
* アセットの作成（ASSET_CREATED）
* アセットの移動（ASSET_MOVED）
* アセットの削除（ASSET_REMOVED）
* ライセンス拒否（REJECTED）
* アセットのダウンロード（DOWNLOADED）
* アセットのバージョン設定（VERSIONED）
* アセットのバージョンの復元（RESTORED）
* アセットのメタデータの更新（METADATA_UPDATED）
* アセットの外部システムへの公開（PUBLISHED_EXTERNAL）
* 元のアセットの更新（ORIGINAL_UPDATED）
* アセットのレンディションの更新（RENDITION_UPDATED）
* アセットのレンディションの削除（RENDITION_REMOVED）
* サブアセットの更新（SUBASSET_UPDATED）
* サブアセットの削除（SUBASSET_REMOVED）

## [!DNL Assets]イベントの記録の設定 {#configuring-aem-assets-events-recording}

[Webコンソール](/help/sites-deploying/configuring-osgi.md)から、[!DNL Assets]イベントレコーダーのチューニングにアクセスできます。 [!DNL Assets]イベントレコーダーを設定するには、次の手順に従います。

1. **[!UICONTROL Web コンソール]**&#x200B;に移動します。

1. 「**[!UICONTROL 設定]**」をクリックします。

1. 「**[!UICONTROL Day CQ DAM Event Recorder]**」をダブルクリックします。

1. 「**[!UICONTROL このサービスを有効にする]**」チェックボックスをオンにします。

1. ユーザーアクティビティストリームで記録する&#x200B;**[!UICONTROL イベントタイプ]**&#x200B;のチェックボックスをチェックします。

1. 「**[!UICONTROL 保存]**」をクリックします。

## 記録されたイベントの読み取り {#reading-recorded-events}

記録されたイベントはアクティビティとして保存されます。[ActivityManager API](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/javadoc/com/adobe/granite/activitystreams/ActivityManager.html) を使用して、プログラムで読み取ることができます。
