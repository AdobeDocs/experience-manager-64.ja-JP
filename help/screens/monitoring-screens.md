---
title: デバイスコントロールセンターからのトラブルシューティング
seo-title: Screens の監視
description: このページに従って、デバイスダッシュボードを使用して、画面プレイヤーのアクティビティとデバイスのパフォーマンスを監視し、トラブルシューティングします。
seo-description: このページに従って、デバイスダッシュボードを使用して、画面プレイヤーのアクティビティとデバイスのパフォーマンスを監視し、トラブルシューティングします。
uuid: 9e3d87c4-a5ff-43cb-a0b0-8919a6086586
contentOwner: Jyotika Syal
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/SCREENS
topic-tags: troubleshoot
discoiquuid: 58738b4e-90ba-4656-85a7-2283e54d7919
translation-type: tm+mt
source-git-commit: 1ebe1e871767605dd4295429c3d0b4de4dd66939

---


# デバイスコントロールセンターからのトラブルシューティング{#troubleshooting-device-control-center}

デバイスダッシュボードを使用すると、Screens Player のアクティビティやデバイスのパフォーマンスを監視およびトラブルシューティングできます。このページでは、Screens Player や割り当てられているデバイスを監視し、確認されたパフォーマンスの問題をトラブルシューティングする方法について説明します。

## デバイスコントロールセンターからの監視およびトラブルシューティング {#monitor-and-troubleshoot-from-device-control-center}

デバイスダッシュボードを使用して、アクティビティを監視し、画面プレイヤーのトラブルシューティングを行うことができます。

### デバイスダッシュボード {#device-dashboard}

デバイスダッシュボードに移動するには、次の手順を実行します。

1. プロジェクトからデバイスダッシュボードに移動します（例：***Test Project***／***デバイス***）。

   アクションバーから「**デバイス**」および「**デバイスマネージャー**」を選択します。

   ![chlimage_1-51](assets/chlimage_1-51.png)

1. 監視対象のデバイスを選択します。

   ![chlimage_1-52](assets/chlimage_1-52.png)

1. このページには、デバイスのアクティビティや機能を監視できるように、デバイス情報、アクティビティおよびデバイス詳細が表示されます。

   ![chlimage_1-53](assets/chlimage_1-53.png)

### デバイスアクティビティの監視 {#monitor-device-activity}

**アクティビティ**&#x200B;パネルには、Screens Player の最後の ping とそのタイムスタンプが表示されます。最後の ping は、デバイスがサーバーに最後にアクセスした時間と一致します。

![chlimage_1-54](assets/chlimage_1-54.png)

さらに、**アクティビティ**&#x200B;パネルの右上隅にある「**ログを収集**」をクリックすると、プレーヤーのログが表示されます。

### デバイス詳細の更新 {#update-device-details}

デバイスの IP、ストレージ使用状況、ファームウェアバージョンおよびプレーヤー稼動時間を確認するには、**デバイスの詳細**&#x200B;パネルをチェックします。

![chlimage_1-55](assets/chlimage_1-55.png)

さらに、このパネルでは、「**キャッシュをクリア**」および「**更新**」をクリックして、デバイスのキャッシュをクリアしたり、[ファームウェア](screens-glossary.md)バージョンを更新したりすることもできます。

また、**デバイスの詳細**&#x200B;パネルの右上隅にある「**...**」をクリックして、プレーヤーを再起動したり、ステータスを更新したりすることもできます。

![chlimage_1-56](assets/chlimage_1-56.png)

### デバイス情報の更新 {#update-device-information}

Check the **DEVICE INFORMATION** panel to view the configuration update, device, platform, version, and the diplay associated with the device.

![chlimage_1-57](assets/chlimage_1-57.png)

さらに、デバイス情報パネルの右上隅にある「**...**」をクリックして、プロパティを表示したり、デバイスを更新したりすることもできます。

![chlimage_1-58](assets/chlimage_1-58.png)

「**プロパティ**」をクリックすると、**デバイスのプロパティ**&#x200B;ダイアログボックスが表示されます。デバイスのタイトルを編集したり、設定の更新オプションとして「**手動**」または「**自動**」を選択したりすることができます。

>[!NOTE]
>
>デバイスの自動更新または手動更新に関連するイベントについて詳しくは、***チャネルの管理***&#x200B;の[自動アップデートとデバイスダッシュボードからの手動アップデート](managing-channels.md)の節を参照してください。

![chlimage_1-59](assets/chlimage_1-59.png)

### プレーヤーのスクリーンショットの表示 {#view-player-screenshot}

プレイヤーのスクリーンショットパネルを使用すると、デバイスからプレーヤーのスクリーンショットを表示できます。

プレイヤーのスクリーンショットパネルの右上隅にある「**...**」をクリックし、「スクリーンショットを更新」を選択すると、実行中のプレーヤーのスナップショットが表示されます。

![chlimage_1-60](assets/chlimage_1-60.png)

### 環境設定の管理 {#manage-preferences}

**環境設定**&#x200B;パネルでは、デバイスの&#x200B;**管理 UI**、**チャネルスイッチャー**、**リモートデバッグ**&#x200B;の環境設定を変更できます。

>[!NOTE]
>
>これらのオプションについて詳しくは、[AEM Screens Player](working-with-screens-player.md) を参照してください。

![chlimage_1-61](assets/chlimage_1-61.png)

さらに、右上隅にある「**環境設定を表示**」をクリックして、サーバーの URL および解像度を更新できます。

![chlimage_1-62](assets/chlimage_1-62.png)

## OSGI 設定のトラブルシューティング {#troubleshoot-osgi-settings}

デバイスからサーバーへのデータの投稿を許可するには、空のリファラーを有効にする必要があります。例えば、空のリファラーのプロパティが無効になっていると、デバイスからスクリーンショットを投稿できません。

現在、これらの機能の一部は、OSGI 設定で *Apache Sling Referrer Filter の Allow Empty 設定*&#x200B;が有効になっている場合にのみ使用できます。ダッシュボードには、セキュリティ設定がこれらの機能の一部の動作を妨げる可能性があることを示す警告が表示される場合があります。

Apache Sling Referrer Filter の Allow Empty 設定を有効にするには、次の手順を実行します。

1. Navigate to [Adobe Experience Manager Web Console Configuration](http://localhost:4502/system/console/configMgr/org.apache.sling.security.impl.ReferrerFilter).
1. 「allow.empty」チェックボックスをオンにします。
1. 「**保存**」をクリックします。

![chlimage_1-63](assets/chlimage_1-63.png)

### 推奨事項 {#recommendations}

次の節では、ヘルスを把握したり、問題に対処したりするために、ネットワークリンク、サーバーおよびプレーヤーを監視することが推奨されています。

AEM の組み込みの監視では、次の点がチェックされます。

* 5 秒間隔の&#x200B;*ハートビート*。これは、AEM Screens Player が動作中であることを示します。
* プレーヤーの&#x200B;*スクリーンショット*。これは、プレーヤーに現在何が表示されているかを示します。
* AEM Screens Player *ファームウェア*&#x200B;バージョンがプレーヤーにインストールされていること。
* プレーヤー上に&#x200B;*空きストレージ領域*&#x200B;が存在すること。

サードパーティソフトウェアを使用してリモート監視をおこなう場合は、次の点をチェックすることが推奨されています。

* プレーヤー上の CPU 使用量。
* AEM Screens Player プロセスの動作状態。
* プレーヤーのリモート再起動。
* リアルタイム通知。

プレーヤーハードウェアおよび OS をデプロイする際には、リモートログインを許可して問題の診断やプレーヤーの再起動をおこなえるようにすることをお勧めします。

#### その他のリソース {#additional-resources}

チャネルで再生するビデオのデバッグとトラブルシューティングについては、[ビデオ再生の設定およびトラブルシューティング](troubleshoot-videos.md)を参照してください。
