---
title: Dynamic Media のセットアップ
seo-title: Setting Up Dynamic Media
description: Dynamic Media をセットアップするには、Dynamic Media を設定して、画像やビューアのプリセットを管理する必要があります
seo-description: To set up dynamic media, you need to configure dynamic media and manage image and viewer presets
uuid: bcd1f9ab-4201-4222-9e4a-ba82b3c7cd6c
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.4/ASSETS
discoiquuid: 36a4a4e7-8bb2-4853-b335-cf9148be410c
exl-id: dd43de7b-8556-4e3f-9d90-14f0f5bd13e7
feature: Configuration
role: Admin,User,Developer
source-git-commit: 5d96c09ef764b02e08dcdf480da1ee18f4d9a30c
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 71%

---

# Dynamic Media のセットアップ {#setting-up-dynamic-media}

[Dynamic Media ](https://www.adobe.com/solutions/web-experience-management/dynamic-media.html)では、マーチャンダイジングおよびマーケティング用のリッチなビジュアルアセットをオンデマンドで配信し、アセットを管理できます。これらのアセットは、Web、モバイルおよびソーシャルサイトでの利用に合わせて自動的に拡大縮小されます。Dynamic Media は、一連のマスターアセットを使用し、パフォーマンスが最適化されスケーラビリティに優れたグローバルネットワーク経由で、複数のリッチコンテンツのバリエーションをリアルタイムで生成および配信します。

>[!NOTE]
>
>このドキュメントは、AEM に直接統合された Dynamic Media の機能について説明します。AEMに統合されたDynamic Media Classicを使用している場合は、 [Dynamic Media Classic統合ドキュメント](/help/sites-administering/scene7.md).
>
>詳しくは、 [二重使用シナリオ](/help/sites-administering/scene7.md#dual-use-scenario) Dynamic Media Classicと統合されたAEMをDynamic Mediaと共に使用したい場合に役立ちます。

Dynamic Media の管理者には、次のトピックが参考になります。

* [Dynamic Media-Scene7モードの設定](config-dms7.md)  — 新規のDynamic Mediaユーザーの場合は、この設定を使用します。
* [Dynamic Media — ハイブリッドモードの設定](config-dynamic.md)  — 既存のDynamic Mediaのお客様がAEMをアップグレードする場合は、この設定を使用します。
* [画像プリセットの管理](managing-image-presets.md)
* [ビューアプリセットの管理](managing-viewer-presets.md)
* [Dynamic Media のトラブルシューティング - Scene7モード](troubleshoot-dms7.md)

次のトピックも参照してください。

* [ビデオエンコーディングとビデオプロファイル](video-profiles.md)
* [イメージプロファイル](image-profiles.md)

>[!NOTE]
>
>**アップグレードする場合：**
>
>* AEM を実行状態にした後にアップロードしたすべてのアセットで、Dynamic Media が自動的に有効になります（システム管理者によって明示的に無効にされた場合を除く）。アップグレードされた AEM インスタンスで Dynamic Media を新たに使用する場合、Dynamic Media を使用できるようアセットを再処理する必要が生じる場合があります。

