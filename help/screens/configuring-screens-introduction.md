---
title: AEM Screens の設定とデプロイ
seo-title: Screens の設定とデプロイ
description: AEM Screens Player は Android、Chrome OS、iOS、Windows で使用できます。ここでは、AEM Screens の設定とデプロイメントについて説明し、プレーヤーデバイスのハードウェア選定ガイドラインの概要も説明します。
seo-description: AEM Screens Player は Android、Chrome OS、iOS、Windows で使用できます。ここでは、AEM Screens の設定とデプロイメントについて説明し、プレーヤーデバイスのハードウェア選定ガイドラインの概要も説明します。
uuid: 8ee5311f-b377-4035-af77-e1391a840745
contentOwner: Jyotika syal
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/SCREENS
topic-tags: administering
discoiquuid: a94d0891-d75f-482e-8d2a-e0cbf953a9de
translation-type: tm+mt
source-git-commit: 1ebe1e871767605dd4295429c3d0b4de4dd66939

---


# AEM Screens の設定とデプロイ{#configuring-and-deploying-aem-screens}

このページでは、デバイスにScreensプレーヤーをインストールおよび設定する方法を示し、以下のトピックについて説明します。

* AEM Screens Player のインストール
* サーバーの設定
* プレーヤーデバイスのハードウェア選定ガイドライン
* 次の手順

## AEM Screens Player のインストール {#installing-aem-screens-player}

AEM Screens Player は Android、Chrome OS、iOS、Windows で使用できます。

To download **AEM Screens Player**, visit the [**AEM 6.4 Player Downloads **](https://download.macromedia.com/screens/)page.

>[!NOTE]
>
>最新のプレーヤー（*.exe*）をダウンロードしたら、以下の手順に従ってプレイヤーのアドホックインストールを完了します。
>
>1. 左上隅を長押しして、管理パネルを開きます。
>1. 左のアクションメニューから「**設定**」に移動し、AEM インスタンスの場所のアドレスを「**サーバー**」に入力して、「**保存**」をクリックします。
   >
   >
1. 左のアクションメニューの「**登録**」リンクをクリックし、以下の手順でデバイス登録プロセスを完了します。
>



### その他のリソース {#additional-resources}

詳細については、以下のトピックを参照してください。

* Android プレーヤーをダウンロードするには、**Google Play** にアクセスします。To learn about implementing Android Watchdog, please refer to **[Implementing Android player](implementing-android-player.md)**.

* To implement Chrome OS Player, please refer to [Chrome Management Console](implementing-chrome-os-player.md) for more information.
* To configure AEM Screens Windows player, please refer to [Implementing Windows Player](implementing-windows-player.md).

## サーバーの設定 {#server-configuration}

>[!NOTE]
>
>**重要**：
>
>AEM Screens Player は、クロスサイトリクエストフォージェリ（CSRF）トークンを利用していません。したがって、AEM Screens で使用できるように AEM サーバーを設定するには、空のリファラーを許可して、リファラーフィルターをスキップします。

### 前提条件 {#prerequisites}

AEM Screens で使用できるように AEM サーバーを設定する際に役立つ重要なポイントを次に示します。

#### 空のリファラー要求の許可 {#allow-empty-referrer-requests}

次の手順に従って、Apache Sling Referrer Filter の「Allow Empty」を有効にします。これは、AEM Screens Player と AEM Screens サーバーの間の制御プロトコルの最適な動作のために必要です。

1. AEM インスタンスでハンマーアイコン／**操作**／**Web コンソール**&#x200B;をクリックして、Adobe Experience Manager Web コンソール設定に移動します。

   ![screen_shot_2019-02-11at15405pm](assets/screen_shot_2019-02-11at15405pm.png)

1. **Adobe Experience Manager Web コンソール設定**&#x200B;が開きます。「sling referrer」を検索します。

   「sling referrer」プロパティを検索するには、**Command + F** キー（**Mac**）または **Ctrl + F** キー（**Windows**）を押します。

   ![screen_shot_2019-02-11at15629pm](assets/screen_shot_2019-02-11at15629pm.png)

1. 「**Allow Empty**」オプションをオンにします（下図を参照）。

   ![screen_shot_2018-12-04at22911pm](assets/screen_shot_2018-12-04at22911pm.png)

1. 「**保存**」をクリックして、Apache Sling Referrer Filter の「Allow Empty」を有効にします。

#### AEM Screens のタッチ操作対応 UI の有効化 {#enable-touch-ui-for-aem-screens}

AEM Screens にはタッチ操作対応 UI が必要で、Adobe Experience Manager（AEM）のクラシック UI では AEM Screens は動作しません。

1. *&lt;yourAuthorInstance>/system/console/configMgr/com.day.cq.wcm.core.impl.AuthoringUIModeServiceImpl* に移動します。
1. 「**Default authoring UI mode**」が「**TOUCH**」に設定されていることを確認します（下図を参照）。

Alternatively, you can also perform the same setting using*&lt;yourAuthorInstance> *->* tools (hammer icon)* -> **Operations** ->**Web Console** and search for **WCM Authoring UI Mode Service**.

![screen_shot_2018-12-04at22425pm](assets/screen_shot_2018-12-04at22425pm.png)

>[!NOTE]
>
>ユーザーの環境設定を使用して、特定のユーザーに対して常にクラシック UI を有効にすることができます。

#### NOSAMPLECONTENT 実行モードの AEM {#aem-in-nosamplecontent-runmode}

実稼動環境での AEM の実行には、**NOSAMPLECONTENT** 実行モードを使用します。Remove the *X-Frame-Options=SAMEORIGIN* header (in the additional response header section) from

[http://localhost:4502/system/console/configMgr/org.apache.sling.engine.impl.SlingMainServlet](http://localhost:4502/system/console/configMgr/org.apache.sling.engine.impl.SlingMainServlet)

これは、AEM Screens Player でオンラインチャネルを再生するために必要です。

#### パスワード制限 {#password-restrictions}

***DeviceServiceImpl*** の最新の変更により、パスワード制限を削除する必要がなくなりました。

次のリンクから ***DeviceServiceImpl*** を設定して、Screens デバイスユーザーのパスワードを作成する際のパスワード制限を有効にすることができます。

[http://localhost:4502/system/console/configMgr/com.adobe.cq.screens.device.impl.DeviceService](http://localhost:4502/system/console/configMgr/com.adobe.cq.screens.device.impl.DeviceService)

以下の手順に従って ***DeviceServiceImpl*** を設定します。

1. AEM インスタンスでハンマーアイコン／**操作**／**Web コンソール**&#x200B;をクリックして、「**Adobe Experience Manager Web コンソール設定**」に移動します。

1. **Adobe Experience Manager Web コンソール設定**&#x200B;が開きます。「deviceservice」を検索します。このプロパティを検索するには、**Command + F** キー（**Mac**）または **Ctrl + F** キー（**Windows**）を押します。

![screen_shot_2019-02-21at24951pm](assets/screen_shot_2019-02-21at24951pm.png)

#### Dispatcher 設定 {#dispatcher-configuration}

**Dispatcherの場合、**.anyファイルにクライアントヘッダーを追加します。 次のヘッダーを許可します。

* &quot;X-Requested-With&quot;
* &quot;X-SET-HEARTBEAT&quot;
* &quot;X-REQUEST-COMMAND&quot;

#### Java エンコーディング {#java-encoding}

***Java エンコーディング***&#x200B;を Unicode に設定します。例えば、*Dfile.encoding=Cp1252* は機能しません。

>[!NOTE]
>
>**推奨事項：**
>
>実稼動環境では AEM Screens サーバーに HTTPS を使用することをお勧めします。

## プレーヤーデバイスのハードウェア選定ガイドライン {#hardware-selection-guidelines-for-player-device}

この節では、Screens プロジェクトのハードウェア選定ガイドラインを示します。

* PC プレーヤーにもディスプレイパネルまたはプロジェクターにも、常に&#x200B;***商用***&#x200B;または&#x200B;***工業用***&#x200B;クラスのコンポーネントを調達します。

* デジタルサイネージマーケットに商品を提供しているベンダーと常に連携します。
* 周囲の気温や相対湿度などの環境要因を常に考慮に入れます。
* 電源要件と電力調整を常に確認します。
* パフォーマンスのニーズとアプリケーションに必要な I/O ポートを慎重に確認します。

AEM Screens プロジェクトの典型的な使用例に対応するハードウェア構成を次の表にまとめます。

<table> 
 <tbody> 
  <tr> 
   <td>プレーヤー設定</td> 
   <td>プロセッサー</td> 
   <td>メモリ</td> 
   <td>ストレージ SSD</td> 
   <td>GPU</td> 
   <td>ディスプレイ</td> 
   <td>I/O</td> 
   <td>典型的な使用例</td> 
  </tr> 
  <tr> 
   <td>基本</td> 
   <td>デュアルコア、i3 またはエントリーレベルのクアッドコア Intel® Atom プロセッサー</td> 
   <td><p>4 GB のメモリ</p> <p>2 MB のキャッシュ</p> </td> 
   <td><p>・Chrome OS：32 GB</p> <p>・Windows：128 GB</p> </td> 
   <td>オンボード</td> 
   <td>1920 x 1080</td> 
   <td>DVI、<br />イーサネット／ワイヤレス、<br />USB x 2</td> 
   <td> 
    <ul> 
     <li>標準フルスクリーンループ <br /> </li> 
     <li>日分割</li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td>標準</td> 
   <td>クアッドコア、Intel® Core i5 プロセッサー</td> 
   <td><p>8 GB のメモリ</p> <p>4 MB のキャッシュ</p> </td> 
   <td>128 GBB</td> 
   <td>オンボード</td> 
   <td>3840 x 2160（4K）</td> 
   <td>DVI、HDMI<br /> イーサネット／ワイヤレス、<br />USB x 2</td> 
   <td> 
    <ul> 
     <li>単一ソースの動的コンテンツ </li> 
     <li>シンプルインタラクティブ</li> 
     <li> 1～3 ゾーンレイアウト</li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td>アドバンス</td> 
   <td>ハイパースレッディング対応クアッドコア、Intel® Core i7 プロセッサー</td> 
   <td><p>16 GB のメモリ</p> <p>8 MB のキャッシュ</p> </td> 
   <td>256 GB</td> 
   <td>Discreet GPU</td> 
   <td>3840 x 2160（4K）</td> 
   <td>DVI、HDMI<br /> イーサネット／ワイヤレス、<br />USB x 4</td> 
   <td> 
    <ul> 
     <li>4 つ以上のコンテンツゾーン、同時ビデオ再生</li> 
     <li> 複数ページインタラクティブ</li> 
     <li>複数ソースデータトリガー</li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table>

## 次の手順 {#the-next-steps}

Screens playerをインストールして設定したら、次のトピックに従って操作を開始します。

1. [Screens プロジェクトの作成と管理](creating-a-screens-project.md)
1. [チャネルの作成と管理](managing-channels.md)
1. [ロケーションの作成と管理](managing-locations.md)
1. [ディスプレイの作成と管理](managing-displays.md)
1. [チャネルの割り当て](channel-assignment.md)
1. [デバイスの管理](managing-devices.md)
1. [デバイスの登録](device-registration.md)
1. [デバイスの割り当て](managing-devices.md)
1. [スケジュールの作成と管理](managing-schedules.md)
1. [AEM Screens Player](working-with-screens-player.md)
1. [Device Control centerのトラブルシューティング](monitoring-screens.md)

