---
title: AEM Screens Player での作業
seo-title: ' Screens Player での作業'
description: このページに従って Screens Player について学習してください。また Admin UI とチャネルスイッチャーについても説明します。
seo-description: このページに従って Screens Player について学習してください。また Admin UI とチャネルスイッチャーについても説明します。
uuid: 93e113ea-fbef-4757-982b-b7dc52fc76a7
contentOwner: jyotika syal
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/SCREENS
topic-tags: authoring
discoiquuid: 4ad51b5e-c628-4440-9f2e-41d17cb10bc3
translation-type: tm+mt
source-git-commit: cdec5b3c57ce1c80c0ed6b5cb7650b52cf9bc340

---


# AEM Screens Player での作業{#working-with-aem-screens-player}

AEM Screens Player でチャネルコンテンツなどの設定を管理できます。

>[!NOTE]
>
>***Ctrl+Cmd+F*** を押すと、OS X AEM Screens Player のフルスクリーンモードを終了できます。

チャネルをディスプレイに割り当てると AEM Screens Player にコンテンツが表示されます。Admin UI の環境設定（ダッシュボード上）を使用して、またはプレーヤー自体からプレーヤーの設定を構成できます。

## デバイスダッシュボードの使用 {#using-the-device-dashboard}

AEM オーサリングインスタンスを介してアクセスできる、デバイスダッシュボードからデバイスの環境設定を構成できます。

1. プロジェクトからデバイスダッシュボードに移動します（例：***Test Project***／***デバイス***）。

   アクションバーから「**デバイス**」および「**デバイスマネージャー**」を選択します。

   ![chlimage_1-66](assets/chlimage_1-66.png)

1. デバイスをクリックしてデバイスダッシュボードを開きます。

   ![chlimage_1-67](assets/chlimage_1-67.png)

1. **環境設定**&#x200B;パネルを確認します。オプションからプレーヤーの「**管理 UI**」と「**チャネルスイッチャー**」の有効／無効を切り替えることができます。

   ![chlimage_1-68](assets/chlimage_1-68.png)

### 管理 UI {#the-admin-ui}

環境設定パネルから「**管理 UI**」を有効にすると、ユーザーは Screens Player から管理者設定を開くことができます。さらに、このオプションをデバイスダッシュボードから無効にすると、ユーザーはプレーヤーから Admin UI を開くことができなくなります。

Screens Player から Admin UI を表示するには、タッチ有効の AEM Screens Player またはマウスを使用して左上角を長押しして、Admin メニューを開きます。登録が完了しチャネルがロードされた後、ここに情報が表示されます。

>[!NOTE]
>
>さらに、AEM Screens Player アプリのアップタイムを表示して、アプリの正常性をチェックできます。

![chlimage_1-3](assets/chlimage_1-3.gif)

サイドメニューから「**設定**」オプションを選択した場合は、このダイアログボックスから「**ファームウェア**」、「**環境設定**」または「**デフォルト設定**」をリセットすることもできます。

さらに、AEM Screens Player の最大ログファイル数を「**保持するログファイルの最大数**」に指定できます。詳しくは、以下のスクリーンショットを参照してください。

>[!NOTE]
>
>「**ファームウェアを更新**」オプションは、Android プレーヤーなどの cordova でのみ機能します。

![screen_shot_2018-10-15at101257am](assets/screen_shot_2018-10-15at101257am.png)

AEM Screens Player の Admin UI から、チャネルおよびアプリケーションのキャッシュをクリアできます。

サイドレールから「**コンテンツキャッシュ**」を選択して、キャッシュを更新します。

![screen_shot_2018-10-15at105717am](assets/screen_shot_2018-10-15at105717am.png)

### チャネルスイッチャー {#the-channel-switcher}

環境設定パネルから「**チャネルスイッチャー**」を有効にすると、Screens Player からチャネル選択／設定を開くことができます。

さらに、このオプションをデバイスダッシュボードから無効にすると、ユーザーは、Screens Player からチャネル環境設定を管理できなくなります。

Screens Player からチャネルの設定を切り替えて管理できます。

プレーヤーからチャネルスイッチャーを表示するには、左下角を長押しします。こうするとチャネルスイッチャーが開いて、チャネルなどの機能を切り替えることができます。

![chlimage_1-69](assets/chlimage_1-69.png)

>[!NOTE]
>
>また、Screens player から管理者メニューおよびプレーヤー用のチャネルスイッチャーの有効と無効を切り替えることができます。
>
>（下のセクションで言及されている「*Screens Player からの設定変更*」を参照してください）

### AEM Screens Player からの設定管理 {#managing-preferences-from-the-aem-screens-player}

プレーヤー自体からも Admin UI およびチャネルスイッチャーの設定を変更できます。

以下の手順に従って、プレーヤーから設定を変更します。

1. アイドルチャネルの左上角を長押しして管理者パネルを開きます。
1. 左のアクションメニューから&#x200B;**設定**&#x200B;に移動します。
1. **Admin UI** または&#x200B;**チャネルスイッチャー**&#x200B;の設定の有効／無効を切り替えます。

![screen_shot_2018-10-15at101257am-1](assets/screen_shot_2018-10-15at101257am-1.png)

## AEM Screens Player のトラブルシューティング {#troubleshooting-aem-screens-player}

AEM Screens Player に関係する様々な問題をトラブルシューティングすることができます。

| **問題** | **推奨事項** |
|---|---|
| プレーヤーのストレージがいっぱいです | 不要なファイルを削除してください |
| プレーヤーのネットワーク接続が途切れました | Cat-5/Cat-6 ケーブルを使用してください。Wi-Fi の場合は、ルーターからプレーヤーデバイスまでの距離を短くしてください |
| AEM Screens Player がクラッシュしました | AEM Screens Player が常時動作しているようにウォッチドッグアプリを使用することをお勧めします |
| AEM Screens Player の設定がなくなりました | AEM サーバーへの接続を確認してください |
| AEM Screens Player が再起動後に自動起動しません | OS のスタートフォルダーまたは初期化手順を確認してください |
| AEM Screens Player のコンテンツ表示が間違っていたり古かったりします | ネットワーク接続を確認してください |

### AEM Screens Player のアップデート {#updates-for-aem-screens-player}

AEM Screens Player には、次の 2 とおりの更新方法があります。

| **方法** | **詳細** | **リモート経由** | **自動** | **ダウンタイムなし** |
|---|---|---|---|---|
| ファームウェアの更新 | リモートコマンドを介して既存のインストール済みプレーヤーに適用されます。アップデート後に、プレーヤーは既存のコンテンツで自動リロードされます。 | はい | カスタム | ほぼ 1～3 秒 |
| プレーヤーシェルの更新 | これは、プレーヤーにデプロイされる新しい実行可能ファイルです。これには、新しいバイナリをプレーヤーにリモートコピーして、現在実行中のプレーヤーを停止して、新しいバージョンを起動する必要があります。これには、事前ロードされているパッケージの再ダウンロードが必要なことがあります。 | はい（リモートシェル経由） | カスタム | いいえ |

