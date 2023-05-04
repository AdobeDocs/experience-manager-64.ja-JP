---
title: Dynamic Media のセットアップ
seo-title: Setting Up Dynamic Media
description: Dynamic Media を設定するには、Dynamic Media を設定し、画像とビューアプリセットを管理する必要があります
seo-description: To set up dynamic media, you need to configure dynamic media and manage image and viewer presets
uuid: bcd1f9ab-4201-4222-9e4a-ba82b3c7cd6c
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.4/ASSETS
discoiquuid: 36a4a4e7-8bb2-4853-b335-cf9148be410c
exl-id: dd43de7b-8556-4e3f-9d90-14f0f5bd13e7
feature: Configuration
role: Admin,User,Developer
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '289'
ht-degree: 43%

---

# Dynamic Media のセットアップ {#setting-up-dynamic-media}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

[Dynamic Media ](https://www.adobe.com/solutions/web-experience-management/dynamic-media.html)では、マーチャンダイジングおよびマーケティング用のリッチなビジュアルアセットをオンデマンドで配信し、アセットを管理できます。これらのアセットは、Web、モバイルおよびソーシャルサイトでの利用に合わせて自動的に拡大縮小されます。Dynamic Mediaでは、一連のマスターアセットを使用して、グローバルで拡張性に優れ、パフォーマンスが最適化されたネットワークを通じて、リッチコンテンツの複数のバリエーションをリアルタイムで生成し、配信します。

>[!NOTE]
>
>このドキュメントでは、AEMに直接統合されるDynamic Mediaの機能について説明します。 AEMに統合されたDynamic Media Classicを使用している場合は、 [Dynamic Media Classic統合ドキュメント](/help/sites-administering/scene7.md).
>
>詳しくは、 [二重使用シナリオ](/help/sites-administering/scene7.md#dual-use-scenario) Dynamic Media Classicと統合されたAEMをDynamic Mediaと共に使用したい場合に役立ちます。

Dynamic Media の管理者は、次のトピックを参照してください。

* [Dynamic Media-Scene7モードの設定](config-dms7.md)  — 新規のDynamic Mediaユーザーの場合は、この設定を使用します。
* [Dynamic Media — ハイブリッドモードの設定](config-dynamic.md)  — 既存のDynamic Mediaのお客様がAEMをアップグレードする場合は、この設定を使用します。
* [画像プリセットの管理](managing-image-presets.md)
* [ビューアプリセットの管理](managing-viewer-presets.md)
* [Dynamic Media のトラブルシューティング - Scene7 モード](troubleshoot-dms7.md)

次のトピックも参照してください。

* [ビデオエンコーディングとビデオプロファイル](video-profiles.md)
* [イメージプロファイル](image-profiles.md)

>[!NOTE]
>
>**アップグレードする場合：**
>
>* AEM を実行状態にした後にアップロードしたすべてのアセットで、Dynamic Media が自動的に有効になります（システム管理者によって明示的に無効にされた場合を除く）。アップグレードされた AEM インスタンスで Dynamic Media を新たに使用する場合、Dynamic Media を使用できるようアセットを再処理する必要が生じる場合があります。

