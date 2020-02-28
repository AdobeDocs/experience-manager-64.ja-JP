---
title: AEM Screens の FAQ
seo-title: AEM Screens の FAQ
description: ここでは、AEM Screens プロジェクトに関連する FAQ への回答を掲載しています。
seo-description: ここでは、AEM Screens プロジェクトに関連する FAQ への回答を掲載しています。
uuid: e394b1bd-1e63-4bd1-b669-923b2a298743
contentOwner: jsyal
products: SG_EXPERIENCEMANAGER/6.4/SCREENS
content-type: reference
topic-tags: troubleshoot
discoiquuid: 558a7c2f-b32e-428e-89f6-123d72ca1108
translation-type: tm+mt
source-git-commit: 9f505017b80fe54e228daea9b248fb0a7db93ca2

---


# AEM Screens の FAQ{#aem-screens-faqs}

次の節では、AEM Screens プロジェクトに関してよく寄せられる質問に対する回答を示します。

## チャネルの管理 {#channel-management}

### What is the difference between an online and an offline channel? {#what-is-the-difference-between-an-online-and-an-offline-channel}

***オンラインチャネル***&#x200B;では、最新のコンテンツがリアルタイム環境で表示されるのに対して、***オフラインチャネル***&#x200B;では、キャッシュされたコンテンツが表示されます。

### How do I make a channel online? {#how-do-i-make-a-channel-online}

チャネルを選択し、アクションバーからチャネルのプロパティに移動します。「**チャネル**」タブで「**開発者モード (チャネルをオンラインに強制)**」をオンにして、チャネルをオンラインにします。

### What is the use of the Channel Role field? {#what-is-the-use-of-the-channel-role-field}

「チャネルロール」は、作成者が汎用のエクスペリエンスに直接専念できるように、実行される実際のチャネルを抽象化したものです。チャネルをそのコンテキスト（ディスプレイまたはスケジュール）で一意に識別する一種のタグと考えることができます。

### How does actual channel resolution happen? {#how-does-actual-channel-resolution-happen}

*静的参照*&#x200B;の場合、解決は指定されたパスに従うだけです。

*動的参照*&#x200B;の場合は、チャネルが（スケジュールではなく）ディスプレイに割り当てられると、解決がおこなわれます。ディスプレイのパスがチャネルのコンテキストになり、解決は次のように（優先順位の高い順に）おこなわれます。

1. ディスプレイに、参照先のチャネル名と一致する子ノードがあります
1. ディスプレイに、参照先のチャネル名と一致する兄弟ノードがあります
1. ディスプレイの親の場所に、参照先のチャネル名と一致する子ノードがあります
1. ディスプレイの祖父母の場所に、参照先のチャネル名と一致する子ノードがあります

場所フォルダーに到達するまでこのような解決を繰り返し、到達した時点で停止します（例えば、チャネルフォルダー内のチャネルを参照することはできません。参照できるのは、場所サブツリー内のチャネルだけです）。

## デバイスの登録 {#device-registration}

### デバイスのオンボーディングや登録の要求などのエンドポイントを検出した場合、多数のデバイスをスクリプト化して、これらのデバイスを登録できます。 これをブランチ Wi-Fi にロックする以外に、これらの要求のセキュリティを確保することは可能ですか？ {#if-i-discover-endpoints-such-as-requests-for-device-onboarding-and-registration-i-can-script-a-large-number-of-devices-and-register-these-devices-besides-locking-this-to-a-branch-wi-fi-is-it-possible-to-secure-these-requests}

現在、登録はオーサーインスタンス上でのみ可能です。登録サービスは認証されていませんが、保留中のデバイスを AEM に作成するだけで、実際にデバイスを登録したりディスプレイを割り当てたりすることはありません。

デバイスを登録する（つまり、デバイスのユーザーを AEM に作成する）には、やはり AEM に対する認証が必要です。現時点では、登録ウィザードに従って手動で登録を完了する必要があります。理論的には、悪意のあるユーザーが保留中のデバイスを複数作成する可能性がありますが、AEM にログインしない限り、デバイスを登録することはできません。

### Is there a way to transform HTTP GET requests into HTTP POST with some form of authentication? {#is-there-a-way-to-transform-http-get-requests-into-http-post-with-some-form-of-authentication}

登録要求は POST 要求です。

デバイス ID は、パラメーターとして渡すのではなく、セッションから取得することをお勧めします。これにより、サーバーログ、ブラウザーキャッシュなどがクリーンアップされます。現時点では、これでセキュリティ上の問題にはなっていません。なお、意味的には、GET は、サーバー上で状態変化がない場合に使用され、状態変化がある場合は POST が使用されます。

### デバイス登録要求を拒否する方法はありますか。

登録要求を拒否することはできません。その代わり、Adobe Experience Manager Web コンソールで設定したタイムアウト時間の経過後に登録要求の有効期限が切れます。

デフォルトでは、この値は 1 日に設定され、メモリキャッシュに保存されます。

## デバイスの監視とヘルスレポート {#device-monitoring-and-health-reports}

### How do I troubleshoot, if my AEM Screens player shows blank screen? {#how-do-i-troubleshoot-if-my-aem-screens-player-shows-blank-screen}

画面が空白になる問題のトラブルシューティングをおこなうには、以下の可能性がないか確認してください。

* AEM がオフラインコンテンツをプッシュできない
* チャネルにコンテンツがない
* 現時点で表示予定のアセットがない

### What do I do if AEM Screens player cannot register and its state is displayed as Failure? {#what-do-i-do-if-aem-screens-player-cannot-register-and-its-state-is-displayed-as-failure}

Apache Sling Referrer Filter の「Allow Empty」をオンにする必要があります。これは、AEM Screens Player と AEM Screens サーバーの間の制御プロトコルの最適な動作のために必要です。

1. **Adobe Experience Manager Web コンソールの設定**&#x200B;に移動します。
1. 「allow.empty」チェックボックスをオンにします。
1. 「**保存**」をクリックします。

### How to troubleshoot if while registering an AEM Screens player, device shows FAILURE and the console logs display ENAME_NOT_FOUND error? {#how-to-troubleshoot-if-while-registering-an-aem-screens-player-device-shows-failure-and-the-console-logs-display-ename-not-found-error}

この問題は、プレーヤーが AEM Screens サーバーの DNS を検出できない場合に発生する可能性があります。IP アドレスを使用して接続してみてください。サーバーの IP アドレスを取得するには、*arp &lt;server_dns_name>* を使用します。

### AMSは、すべてのデバイスにAndroidウォッチドッグを実装することをお勧めしますか？ ウォッチドッグ（Cordova）プラグインは APK に含まれていますか？ {#does-ams-recommend-implementing-an-android-watchdog-on-all-devices-is-the-watchdog-cordova-plugin-included-as-part-of-the-apk}

純粋な Android API を使用するクロスプラットフォームの Android ウォッチドッグは、既に APK に含まれています。追加のソフトウェアは必要ありませんが、使用するデバイスによっては、APK に再署名して、完全な電源サイクルを実行するためのシステム権限（PowerManager API）を取得しなければならない場合があります。製造元のキーを使用して再署名しない場合は、アプリケーションが終了して再起動しますが、電源のオン／オフはおこなわれません。

Android プレーヤーの実装方法について詳しくは、[**Android プレーヤーの実装&#x200B;**](implementing-android-player.md)を参照してください。

### What third-party remote monitoring and alerting tools (software) does Adobe/AMS recommend for monitoring each device?  {#what-third-party-remote-monitoring-and-alerting-tools-software-does-adobe-ams-recommend-for-monitoring-each-device}

必要な監視および警告機能にもよりますが、新機能である AEM Screens 通知サービスでは、デバイスがしばらくの間 ping に応答しなかった場合にユーザーに通知します。サードパーティツールは、お使いのオペレーティングシステム（OS）とその機能、およびユーザー固有のニーズによって異なります。

デバイスアクティビティの監視について詳しくは、[**AEM Screens 通知サービス&#x200B;**](screens-notifications-service.md)を参照してください。

### Smart syncで発行デバイストポロジを使用して、スナップショット機能とハートビート機能用に、デバイスはオーサーインスタンスに直接接続されていますか。

いいえ。デバイスは作成者に直接接続されていません。 ユーザーは発行インスタンスにレポートし、発行インスタンスに対して作成者が更新をポーリングします。

## AEM Screens Player {#aem-screens-player}

### How to Install ChromeOS player as Chrome Browser Plugin? {#how-to-install-chromeos-player-as-chrome-browser-plugin}

Chrome OS プレーヤーは、実際の Chrome プレーヤーデバイスがなくても、開発者モードで Chrome ブラウザープラグインとしてインストールできます。インストールについては、次の手順に従います。

1. [ここ](https://download.macromedia.com/screens/)をクリックして、最新の Chrome プレーヤーをダウンロードします。
1. 解凍してディスクに保存します。
1. Chrome ブラウザーを開き、右上隅の 3 ドットメニューをクリックし、**その他のツール**／**拡張機能**&#x200B;を選択するか、***chrome://extensions*** に直接移動します。
1. 右上隅の「**デベロッパーモード**」をオンにします。
1. 左上隅の「パッケージ化されていない拡張機能を読み込む」をクリックし、解凍した Chrome OS プレーヤーを読み込みます。
1. **AEM Screens Chrome Player** プラグインが拡張機能の一覧にあれば、それをオンにします。
1. 新しいタブを開き、左上隅の「**アプリ**」アイコンをクリックするか、***chrome://apps*** に直接移動します。
1. 「**AEM Screens** プラグイン」をクリックして、Chrome プレーヤーを起動します。デフォルトでは、プレーヤーはフルスクリーンモードで起動します。**Esc** キーを押すと、フルスクリーンモードが終了します。

### How to troubleshoot if Screens player is unable to authenticate through publish instance with custom error handler? {#how-to-troubleshoot-if-screens-player-is-unable-to-authenticate-through-publish-instance-with-custom-error-handler}

AEM Screens Player は、起動時に 404 エラーが発生すると、***/content/screens/svc.ping.json*** への要求をおこないます。プレーヤーが認証要求を開始して、パブリッシュインスタンスに対して認証をおこないます。パブリッシュインスタンスにカスタムエラーハンドラーがある場合、匿名ユーザーに対しては、***/content/screens/svc.ping.json*** の実行で必ず 404 のステータスコードを返すようにしてください。

### Android Playerでデバイスの画面を常に表示する方法を教えてください。

次の手順に従って、任意の Android プレーヤーで「スリープモードにしない」をオンにします。

1. Navigate to Android player settings -> **About**
1. ビルド番号を 7 回タップして、設定の「開発者向けオプション」を有効にします。
1. **開発者向けオプション**&#x200B;に移動します。
1. 「**スリープモードにしない**」をオンにします。

### アップデートがAEMから送信され、プレーヤーがオフラインの場合、デバイスがオンラインに戻って更新されたコンテンツを配信するかどうかを確認する再試行メカニズムはありますか。 あとどれ位の期間試してる？

次に入ってくるデバイスからのpingが最後の変更時刻を確認し、新しいコンテンツをダウンロードします。
pingが成功するまで、これは永久に試行されます。

### アセットの使用 {#using-assets}

### 2 GBを超えるAEM Screensチャネルでビデオを使用する方法を教えてください。 {#how-to-use-videos-in-an-aem-screens-channel-larger-than-gb}

デフォルトでは、AEM Assetsのタッチ操作対応UIでは、AEM screensチャネルのファイルサイズ制限により、2 GBを超えるアセットはアップロードできません。 ただし、この上限は CRXDE Lite を開き、/apps ディレクトリ配下にノードを作成することで上書きできます。

/appsディレクトリでより大きなファイルサイズ制限（30 GBなど）を設定する方法について詳しくは、「ビデオアセットの管理」の「 *Configuration to upload video assets* that larger *that* lager the 2 GB [」を参照してください](/help/assets/managing-video-assets.md)。

### トラブルシューティングに関する一般的なヒント {#general-troubleshooting}

### Livefyreを無効にしてA/P画面のエラーを回避する方法

Livefyre を無効にしてログエラーを回避するには、次の手順に従います。

**Livefyreバンドルの無効化：**

1. `http://<host>:<port>/system/console/bundles` に移動します。
1. Search for the AEM Livefyre bundle:  *com.adobe.cq.social.cq-social-livefyre*
1. Click **Stop**.

**Livefyreポーラーの無効化：**

1. CRXDE Liteで、/etc/importers/polling/livefyre-poller/jcr:contentに移動します。 **
1. 新しいプロパティ enabled（Boolean 型）を追加します。
1. **enabled プロパティ**&#x200B;を **false** に設定します。
