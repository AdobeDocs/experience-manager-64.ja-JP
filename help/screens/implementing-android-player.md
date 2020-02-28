---
title: Android プレーヤーの実装
seo-title: Android プレーヤーの実装
description: 'このページでは、Android ウォッチドック（Android プレーヤーをクラッシュから回復させるソリューション）を実装する方法について見ていきます。 '
seo-description: 'このページでは、Android ウォッチドック（Android プレーヤーをクラッシュから回復させるソリューション）を実装する方法について見ていきます。 '
uuid: 37527a6a-dcc5-4256-abeb-e1f95ff80be4
contentOwner: Jyotika syal
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/SCREENS
topic-tags: administering
discoiquuid: e6ec1641-4323-4c79-b932-b857feb1df21
translation-type: tm+mt
source-git-commit: 1ebe1e871767605dd4295429c3d0b4de4dd66939

---


# Android プレーヤーの実装 {#implementing-android-player}

ウォッチドッグとは、プレーヤーをクラッシュから回復させるソリューションです。******&#x200B;アプリケーションは、ウォッチドッグサービスに登録し、アプリケーション自体がアライブであることを知らせるメッセージを定期的に送信する必要があります。ウォッチドッグサービスに、所定の時間内にキープアライブメッセージが届かないと、ウォッチドッグサービスは、デバイスをリブートしてクリーンリカバリを試みるか（ウォッチドッグサービスが十分な権限が持つ場合）、アプリケーションの再起動を試みます。

## Android ウォッチドッグを実装する {#implementing-android-watchdog}

Android のアーキテクチャ上、デバイスをリブートするには、アプリケーションがシステム権限を持っている必要があります。そのためには、製造元の署名キーを使用して apk に署名する必要があります。この署名をおこなわないと、ウォッチドッグはデバイスをリブートするのではなく、プレーヤーアプリケーションを再起動します。

### 製造元のキーを使用した Android apk への署名 {#signage-of-android-apks-using-manufacturer-keys}

To access some of the privileged APIs of Android such as *PowerManager* or *HDMIControlServices*, you need to sign the android apk using the manufacturer&#39;s keys.

>[!CAUTION]
>
>前提条件：
>
>以下の手順を実行する前に、Android SDK をインストールしてください。

次の手順に従って、製造元のキーを使用して Android apk に署名します。

1. Google Play または [AEM Screens Player のダウンロード](https://download.macromedia.com/screens/)ページから apk をダウンロードします。
1. 製造元のプラットフォームキーを入手して、*pk8* ファイルと *pem* ファイルを取得します。

1. find ~/Library/Android/sdk/build-tools -name &quot;apksigner&quot; を使用して、Android SDK の apksigner ツールを見つけます。
1. &lt;pathto> /apksigner sign --key platform.pk8 --cert platform.x509.pem aemscreensplayer.apk
1. Android SDK の zip align ツールへのパスを見つけます。
1. &lt;pathto> /zipalign -fv 4 aemscreensplayer.apk aemscreensaligned.apk
1. adb install を使用して、デバイスに ***aemscreensaligned.apk*** をインストールします。

## Android ウォッチドッグの実装 {#android-watchdog-implementation}

Android ウォッチドッグサービスは、*AlarmManager* を使用した cordova プラグインとして実装されます。

次の図に、ウォッチドッグサービスの実装を示します。

![chlimage_1-43](assets/chlimage_1-43.png)

**1.初期化**：cordova プラグインの初期化時、システム権限を持っているかどうか、さらに、リブート権限を持っているかどうかの確認がおこなわれます。これらの 2 つの条件を満たしている場合は、リブートのペンディングインテントが作成され、条件を満たしていない場合は、（Launch Activity に基づいて）アプリケーションを再起動するためのペンディングインテントが作成されます。

**2.キープアライブタイマー**：15 秒おきにイベントをトリガーするためにキープアライブタイマーが使用されます。このイベントの間に、（アプリケーションをリブートまたは再起動する）既存のペンディングインテントをキャンセルし、次の 60 秒の間に新しいペンディングインテントを登録する（最終的にリブートを延期する）必要があります。

>[!NOTE]
>
>Android では、*AlarmManager* は、アプリケーションがクラッシュして、そのアラーム配信が API 19（Kitkat）から正確におこなわれなくても実行可能な *pendingIntents* を登録するために使用されます。タイマーの間隔と AlarmManager の ** pendingIntents ** のアラームとの間にいくらかの時間を設けるようにしてください。

**3.アプリケーションのクラッシュ**：クラッシュした場合、AlarmManager に登録されているリブートのペンディングインテントはリセットされず、（cordova プラグインの初期化時に使用可能な権限に応じて）アプリケーションのリブートまたは再起動を実行します。
