---
title: Dynamic Media - ハイブリッドモードの設定
seo-title: Configuring Dynamic Media - Hybrid mode
description: Dynamic Media - ハイブリッドモードの設定方法を学習します。
seo-description: Learn how to configure Dynamic Media - Hybrid mode.
uuid: de88f68f-4697-4ff0-8008-3ae6a4684a84
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.4/ASSETS
discoiquuid: 821eb27e-67c9-4589-9196-30dacb84fa59
exl-id: 1e122f97-ac37-44f5-a1cd-bf53ffda6f5b
feature: Configuration,Hybrid Mode
role: Admin,User,Developer
source-git-commit: a750c5425e33c2a115aab581b71862c1d30cf166
workflow-type: tm+mt
source-wordcount: '7780'
ht-degree: 70%

---

# Dynamic Media - ハイブリッドモードの設定 {#configuring-dynamic-media-hybrid-mode}

Dynamic Media — ハイブリッドを使用するには、有効にして設定する必要があります。 Dynamic Media では、使用例に応じて、[サポートされる設定](#supported-dynamic-media-configurations)がいくつか用意されています。

>[!NOTE]
>
>Scene7 実行モードの Dynamic Media を設定して実行する場合は、[Dynamic Media - Scene7 モードの設定](config-dms7.md)を参照してください。
>
>ハイブリッド実行モードの Dynamic Media を設定して実行する場合は、このページの手順に従ってください。

Dynamic Media での[ビデオ](video.md)の操作方法を参照してください。

開発用、ステージング用、実稼動用など、複数の異なる環境向けに Adobe Experience Manager をセットアップして使用する場合は、それぞれの環境向けに Dynamic Media Cloud Services を設定する必要があります。

Dynamic Media 設定に問題がある場合は、Dynamic Media 固有のログファイルを確認することが重要です。これらは Dynamic Media を有効化するときに自動的にインストールされます。

* `s7access.log`
* `ImageServing.log`

これらは、 [AEMインスタンスの監視と保守](/help/sites-deploying/monitoring-and-maintaining.md).

ハイブリッド公開および配信は、Adobe Experience Manager に対して Dynamic Media によって追加される中心機能です。ハイブリッド公開を使用すると、画像、セット、ビデオなどのDynamic Mediaアセットを、AEM公開ノードからではなく、クラウドから配信できます。

 Dynamic Media ビューア、サイトページ、静的コンテンツなどのその他のコンテンツは、引き続き AEM パブリッシュノードから配信されます。

Dynamic Media のユーザーは、すべての Dynamic Media コンテンツの配信メカニズムとしてハイブリッド配信を使用する必要があります。

## ビデオのハイブリッド公開アーキテクチャ {#hybrid-publishing-architecture-for-videos}

![chlimage_1-506](assets/chlimage_1-506.png)

## 画像のハイブリッド公開アーキテクチャ {#hybrid-publishing-architecture-for-images}

![chlimage_1-507](assets/chlimage_1-507.png)

## サポートされるDynamic Media設定 {#supported-dynamic-media-configurations}

各設定タスクで参照される用語を次に示します。

| **用語** | **ダイナミックメディア有効** | **説明** |
|---|---|---|
| AEM オーサーノード | 緑色の円の中に白色のチェックマーク | オンプレミスへ、または Managed Services を通じてデプロイするオーサーノード |
| AEM パブリッシュノード | 赤色の四角の中に白色の「X」 | オンプレミスへ、または Managed Services を通じてデプロイするパブリッシュノード |
| 画像サービスのパブリッシュノード | 緑色の円の中に白色のチェックマーク | アドビによって管理されるデータセンター上で稼働するパブリッシュノード。画像サービスの URL を参照します。 |

Dynamic Media を画像専用、ビデオ専用、またはその両方の用途で実装できます。具体的なシナリオに合わせた Dynamic Media を設定する手順を決定するには、次の表を参照してください。

<table> 
 <tbody> 
  <tr> 
   <td><strong>シナリオ</strong></td> 
   <td><strong>仕組み</strong></td> 
   <td><strong>設定手順</strong></td> 
  </tr> 
  <tr> 
   <td>実稼動環境に画像のみを配信する</td> 
   <td>画像は世界各地のアドビのデータセンターのサーバーを介して配信されます。CDN を使用してキャッシュすることで、スケーラブルなパフォーマンスで全世界に展開できます。</td> 
   <td> 
    <ol> 
     <li>AEM <strong>オーサー</strong>ノードで、<a href="#enabling-dynamic-media">Dynamic Media を有効化</a>します。</li> 
     <li>画像を<a href="#configuring-dynamic-media-cloud-services"> Dynamic Media クラウドサービス</a>で設定します。</li> 
     <li><a href="#configuring-image-replication">画像のレプリケーションを設定</a>します。</li> 
     <li><a href="#replicating-catalog-settings">カタログ設定をレプリケートする</a>.</li> 
     <li><a href="#replicating-viewer-presets">ビューアプリセットをレプリケート</a>します。</li> 
     <li><a href="#using-default-asset-filters-for-replication">レプリケーションへのデフォルトのアセットフィルターの使用</a>.</li> 
     <li><a href="#configuring-dynamic-media-image-server-settings">Dynamic Media Image Server を設定</a>します。</li> 
     <li><a href="#delivering-assets">アセットを配信</a>します。</li> 
    </ol> </td> 
  </tr> 
  <tr> 
   <td>実稼動前の環境（開発、品質評価、ステージングなど）に画像のみを配信する</td> 
   <td>画像は AEM パブリッシュノードを通じて配信されます。このシナリオでは、トラフィックが最小限となるので、画像をアドビのデータセンターに配信する必要はありません。また、実稼動環境での起動前にコンテンツの安全なプレビューが可能となるというメリットもあります</td> 
   <td> 
    <ol> 
     <li>AEM <strong>オーサー</strong>ノードで、<a href="#enabling-dynamic-media">Dynamic Media を有効化</a>します。</li> 
     <li>AEM <strong>公開</strong> ノード <a href="#enabling-dynamic-media">dynamic media を有効にする</a>.</li> 
     <li><a href="#replicating-viewer-presets">ビューアプリセットをレプリケート</a>します。</li> 
     <li><a href="#setting-up-asset-filters-for-imaging-in-non-production-deployments">実稼動環境以外の画像用のアセットフィルター</a>をセットアップします。</li> 
     <li><a href="#configuring-dynamic-media-image-server-settings">Dynamic Media Image Server を設定します。</a></li> 
     <li><a href="#delivering-assets">アセットを配信します。</a></li> 
    </ol> </td> 
  </tr> 
  <tr> 
   <td>任意の環境（実稼動、開発、品質評価、ステージングなど）にビデオのみを配信する</td> 
   <td>画像は CDN を使用してキャッシュすることで、スケーラブルなパフォーマンスで全世界に展開できます。ビデオのポスター画像（再生が開始される前に表示されるビデオのサムネール）が AEM パブリッシュインスタンスにより配信されます。</td> 
   <td> 
    <ol> 
     <li>AEM <strong>オーサー</strong>ノードで、<a href="#enabling-dynamic-media">Dynamic Media を有効化</a>します。</li> 
     <li>AEM <strong>パブリッシュ</strong>ノードで、<a href="#enabling-dynamic-media">Dynamic Media を有効化</a>します（パブリッシュインスタンスがビデオのポスター画像を処理し、ビデオ再生用のメタデータを提供します）。</li> 
     <li><a href="#configuring-dynamic-media-cloud-services">Dynamic Media クラウドサービス</a>でビデオを設定します。</li> 
     <li><a href="#replicating-viewer-presets">ビューアプリセットをレプリケート</a>します。</li> 
     <li><a href="#setting-up-asset-filters-for-video-only-deployments">ビデオ専用のアセットフィルター</a>をセットアップします。</li> 
     <li><a href="#delivering-assets">アセットを配信します。</a></li> 
    </ol> </td> 
  </tr> 
  <tr> 
   <td>実稼動環境に画像とビデオの両方を配信する</td> 
   <td><p>画像は CDN を使用してキャッシュすることで、スケーラブルなパフォーマンスで全世界に展開できます。画像やビデオのポスター画像は世界各地のアドビのデータセンターのサーバーを介して配信されます。CDN を使用してキャッシュすることで、スケーラブルなパフォーマンスで全世界に展開できます。</p> <p>実稼動前の環境での画像やビデオのセットアップ方法については、前の節を参照してください。 </p> </td> 
   <td> 
    <ol> 
     <li>AEM <strong>オーサー</strong>ノードで、<a href="#enabling-dynamic-media">Dynamic Media を有効化</a>します。</li> 
     <li><a href="#configuring-dynamic-media-cloud-services">Dynamic Media クラウドサービス</a>でビデオを設定します。</li> 
     <li>画像を<a href="#configuring-dynamic-media-cloud-services"> Dynamic Media クラウドサービス</a>で設定します。</li> 
     <li><a href="#configuring-image-replication">画像のレプリケーションを設定</a>します。</li> 
     <li><a href="#replicating-catalog-settings">カタログ設定をレプリケートする</a>.</li> 
     <li><a href="#replicating-viewer-presets">ビューアプリセットをレプリケート</a>します。</li> 
     <li><a href="#using-default-asset-filters-for-replication">レプリケーションにデフォルトのアセットフィルターを使用します。</a></li> 
     <li><a href="#configuring-dynamic-media-image-server-settings">Dynamic Media Image Server を設定します。</a></li> 
     <li><a href="#delivering-assets">アセットを配信します。</a></li> 
    </ol> </td> 
  </tr> 
 </tbody> 
</table>

## Dynamic Media の有効化 {#enabling-dynamic-media}

[Dynamic Media ](https://www.adobe.com/solutions/web-experience-management/dynamic-media.html)はデフォルトで無効になっています。Dynamic Mediaの機能を活用するには、 **[!UICONTROL dynamicmedia]** 実行モードを指定します（例： ）。 **[!UICONTROL 公開]** 実行モード。 有効にする前に、[技術要件](/help/sites-deploying/technical-requirements.md#requirements-for-aem-dynamic-media-add-on)を確認してください。

>[!NOTE]
>
>実行モードで Dynamic Media を有効にすると、**[!UICONTROL dynamicMediaEnabled]** フラグを **[!UICONTROL true]** に設定することで Dynamic Media を有効にした AEM 6.1 および AEM 6.0 の機能が置き換えられます。このフラグは AEM 6.2 以降では機能しません。さらに、クイックスタートを再起動して Dynamic Media を有効にする必要はありません。

Dynamic Mediaを有効にすると、Dynamic Media 機能が UI で使用でき、アップロードされたすべての画像アセットが `cqdam.pyramid.tiff` 動的画像レンディションの高速配信に使用するレンディション。 これらの PTIFF には、(1)1 つのマスター画像のみを管理し、追加の保存を必要とせずに無限レンディションをその場で生成する機能、(2) ズーム、パン、スピンなどのインタラクティブなビジュアライゼーションを使用する機能など、大きな利点があります。

AEMでDynamic Media Classicを使用する場合は、 [特定のシナリオ](/help/sites-administering/scene7.md#aem-scene-integration-versus-dynamic-media). Dynamic Mediaは、実行モードでDynamic Mediaを有効にしない限り無効になります。

Dynamic Media を有効にするには、コマンドラインまたはクイックスタートのファイル名から Dynamic Media の実行モードを有効にする必要があります。

**Dynamic Media を有効にするには**:

1. コマンドラインでクイックスタートを起動するときに、次のようにします。

   * 追加 **[!UICONTROL -r dynamicmedia]** を追加します。

   ```shell
   java -Xmx4096m -Doak.queryLimitInMemory=500000 -Doak.queryLimitReads=500000 -jar cq-quickstart-6.4.0.jar -r dynamicmedia
   ```

   s7delivery に公開する場合は、次の trustStore 引数も含める必要があります。

   ```shell
   -Djavax.net.ssl.trustStore=<absoluteFilePath>/customerTrustStoreFileName>
   
    -Djavax.net.ssl.trustStorePassword=<passwordForTrustStoreFile>
   ```

1. リクエスト `http://localhost:4502/is/image` をクリックし、Image Server が実行中であることを確認します。

   >[!NOTE]
   >
   >Dynamic Mediaの問題のトラブルシューティングについては、 **[!UICONTROL crx-quickstart/logs/]** ディレクトリ：
   >
   >* ImageServer-&lt;PortId>-&lt;yyyy>&lt;mm>&lt;dd>.log - ImageServer ログには、内部の ImageServer プロセスの動作を分析するために使用できる統計情報と分析情報があります。

      Image Server ログのファイル名の例：`ImageServer-57346-2019-07-25.log`
   * s7access-&lt;yyyy>&lt;mm>&lt;dd>.log - s7access ログには、`/is/image` および `/is/content` 経由で Dynamic Media に対して実行された各リクエストが記録されます。
   これらのログは、Dynamic Media が有効の場合のみ使用されます。これらは、 **完全にダウンロード** 次から生成されたパッケージ **[!UICONTROL system/console/status-Bundlelist]** ページ；Dynamic Mediaで問題が発生した場合は、カスタマーサポートに連絡する際に、これらのログを問題に追加してください。

### AEM を異なるポートやコンテキストパスにインストールした場合 {#if-you-installed-aem-to-a-different-port-or-context-path}

をデプロイしている場合 [AEM to application server](/help/sites-deploying/application-server-install.md) Dynamic Mediaを有効にするには、 **自己** Externalizer のドメイン。そうしないと、アセットのサムネールの生成が Dynamic Media アセットに対して正しく機能しません。

さらに、異なるポートまたはコンテキストパスで quickstart を実行する場合、**self** ドメインを変更する必要もあります。

Dynamic Media が有効の場合、画像アセットの静的サムネールレンディションが Dynamic Media を使用して生成されます。サムネール生成がダイナミックメディアに対して正常に動作するためには、AEM で自己に対して URL 要求を実行する必要があり、ポート番号とコンテキストパスの両方を把握している必要があります。

AEM では、

* [Externalizer](/help/sites-developing/externalizer.md) の **self** ドメインがポート番号とコンテキストパスの両方を取得するために使用されます。
* 指定しない場合 **自己** ドメインが設定されている場合、ポート番号とコンテキストパスは Jetty HTTP サービスから取得されます。

AEM QuickStart WAR デプロイメントでは、ポート番号とコンテキストパスを導き出せないので、 **自己** ドメイン。詳しくは、 [externalizer に関するドキュメント](/help/sites-developing/externalizer.md) 設定方法 **自己** ドメイン。

>[!NOTE]
[AEM Quickstart スタンドアロンデプロイメント](/help/sites-deploying/deploy.md)では、**self** ドメインは通常設定する必要がありません。ポート番号とコンテキストパスは自動設定されます。ただし、ネットワークインターフェイスがオフの場合は、**self** ドメインを設定する必要があります。

## Dynamic Media の無効化  {#disabling-dynamic-media}

Dynamic Media はデフォルトでは有効になっていません。しかし、以前に Dynamic Media を有効にした場合は、後で無効にすることができます。

有効化した後に Dynamic Media を無効にするには、 **[!UICONTROL -r dynamicmedia]** 実行モードフラグ。

**有効化後にDynamic Mediaを無効にするには**:

1. コマンドラインでクイックスタートを起動するときに、次のいずれかを実行します。

   * 追加しない `-r dynamicmedia` を JAR ファイルの起動時にコマンドラインに追加します。

   ```shell
   java -Xmx4096m -Doak.queryLimitInMemory=500000 -Doak.queryLimitReads=500000 -jar cq-quickstart-6.4.0.jar
   ```

1. `http://localhost:4502/is/image` をリクエストします。Dynamic Media が無効化されたことを示すメッセージが表示されます。

   >[!NOTE]
   Dynamic Media 実行モードを無効にすると、`qdam.pyramid.tiff` レンディションを生成するワークフローステップは自動的にスキップされます。また、動的レンディションのサポートやその他の Dynamic Media 機能も無効になります。
   また、AEM サーバーを設定した後で Dynamic Media 実行モードを無効にすると、その実行モードの下でアップロードされたアセットがすべて無効になることにも注意してください。

## （オプション）Dynamic Mediaのプリセットと設定を 6.3 から 6.4 にダウンタイムなしで移行する {#optional-migrating-dynamic-media-presets-and-configurations-from-to-zero-downtime}

AEM Dynamic Mediaを 6.3 から 6.4 にアップグレードする場合 ( ダウンタイムなし（オプトイン）のデプロイメント機能を含む )、次の curl コマンドを実行して、すべてのプリセットと設定をから移行する必要があります。 `/etc` から `/conf` CRXDE Lite

**注意**:AEMインスタンスを互換モードで実行する場合（つまり、互換パッケージがインストールされている場合）は、これらのコマンドを実行する必要はありません。

カスタムプリセットと設定を次の場所から移行するには： `/etc` から `/conf`、次の Linux curl コマンドを実行します。

`curl -u admin:admin http://localhost:4502/libs/settings/dam/dm/presets.migratedmcontent.json`

互換パッケージの有無を問わず、すべてのアップグレードについて、次のコマンドを実行することにより標準提供ビューアプリセットをコピーできます。

`curl -u admin:admin http://localhost:4502/libs/settings/dam/dm/presets/viewer.pushviewerpresets`

## 画像レプリケーションの設定 {#configuring-image-replication}

Dynamic Mediaの画像配信は、ビデオサムネールを含む画像アセットを AEM オーサーから公開し、Adobeのオンデマンドレプリケーションサービス（レプリケーションサービスの URL）にレプリケートすることで機能します。 その後、アセットはオンデマンド画像配信サービス（画像サービス URL）によって配信されます。

次の手順を実行する必要があります。

1. [認証を設定](#setting-up-authentication)します。
1. [レプリケーションエージェントを設定](#configuring-the-replication-agent)します。

レプリケーションエージェントは、画像、ビデオのメタデータ、セットなどのダイナミックメディアアセットを、アドビにホストされた画像サービスに公開します。レプリケーションエージェントはデフォルトでは有効でありません。

レプリケーションエージェントを設定後、[正しく設定されていることを検証およびテスト](#validating-the-replication-agent-for-dynamic-media)する必要があります。ここでは、これらの手順について説明します。

>[!NOTE]
PTIFF 作成のデフォルトのメモリ制限は、すべてのワークフローで 3 GB です。例えば、他のワークフローを一時停止して、3 GB のメモリを必要とする 1 個の画像を処理できます。または、それぞれ 300 MB のメモリを必要とする 10 個の画像を並行して処理できます。
このメモリ制限は変更できますが、使用可能なシステムリソースおよび処理する画像コンテンツのタイプに合わせる必要があります。非常に大きなアセットが多数あり、システムに十分なメモリがある場合、この制限を引き上げて、画像が並行して処理されるようにすることができます。
最大メモリ制限を超えるメモリを必要とする画像は、拒否されます。
PTIFF 作成のメモリ制限を変更するには、**[!UICONTROL ツール／運営／Web コンソール／Adobe CQ Scene7 PTiffManager]** に移動して、`maxMemory` の値を変更します。

### 認証の設定 {#setting-up-authentication}

Dynamic Media 画像配信サービスに画像をレプリケートするには、作成者にレプリケーション認証を設定する必要があります。これを行うには、キーストアを取得し、 **[!UICONTROL dynamic-media-replication]** ユーザーに割り当てて設定します。 キーストアファイルとプロビジョニング処理中に必要な資格情報が記載されたようこそメールが会社の管理者に送信されます。これを受け取っていない場合は、カスタマーサポートにお問い合わせください。

**認証を設定するには**:

1. キーストアファイルとパスワードをまだお持ちでない場合は、カスタマーサポートにお問い合わせください。 これはプロビジョニングの一部であり、これによりキーがアカウントに関連付けられます。
1. AEM で、AEM のロゴをタップしてグローバルナビゲーションコンソールにアクセスし、**[!UICONTROL ツール／セキュリティ／ユーザー]**&#x200B;をタップします。
1. ユーザー管理ページで、 **[!UICONTROL dynamic-media-replication]** をタップし、開きます。

   ![dm-replication](assets/dm-replication.png)

1. Dynamic-media-replication のユーザー設定を編集ページで、 **[!UICONTROL キーストア]** 「 」タブに移動し、「 」をタップします。 **[!UICONTROL キーストアを作成]**.

   ![dm-replication-keystore](assets/dm-replication-keystore.png)

1. **[!UICONTROL キーストアアクセスパスワードを設定]**&#x200B;ダイアログボックスでパスワードを入力し、パスワードを確認します。

   >[!NOTE]
   入力したパスワードは覚えておいてください。設定時に再度入力する必要があります **[!UICONTROL レプリケーションエージェント]** 後で。

   ![chlimage_1-508](assets/chlimage_1-508.png)

1. **[!UICONTROL dynamic-media-replication のユーザー設定を編集]**&#x200B;ページで「**[!UICONTROL 秘密鍵をキーストアファイルから追加]**」領域を展開し、以下の情報を追加します（下の画像を参照）。

   * 内 **[!UICONTROL 新規エイリアス]** 「 」フィールドで、後でレプリケーション設定で使用するエイリアスの名前を入力します。例： **複製**.
   * 「**[!UICONTROL キーストアファイル]**」をタップします。アドビから提供されたキーストアファイルに移動して選択し、「**[!UICONTROL 開く]**」をタップします。
   * 「**[!UICONTROL キーストアファイルパスワード]**」フィールドで、キーストアファイルパスワードを入力します。これは _not_ 手順 5 で作成したキーストアAdobeで、プロビジョニング中に送信された「ようこそ」の電子メールに、「キーストアファイルパスワード」パスワードパスワードが表示されます。 キーストアファイルパスワードを受け取っていない場合は、アドビのカスタマーサポートにお問い合わせください。
   * 「**[!UICONTROL 秘密鍵のパスワード]**」フィールドで、秘密鍵のパスワードを入力します（以前の手順で指定した秘密鍵のパスワードと同じでも可）。秘密鍵のパスワードは、プロビジョニング中にアドビから送信されたようこそメールに記載されています。秘密鍵のパスワードを受け取っていない場合は、アドビのカスタマーサポートにお問い合わせください。
   * 「**[!UICONTROL 秘密鍵のエイリアス]**」フィールドに秘密鍵のエイリアスを入力します。例：`companyname-alias`。秘密鍵のエイリアスは、プロビジョニング中にアドビから送信されたようこそメールに記載されています。秘密鍵のエイリアスを受け取っていない場合は、アドビのカスタマーサポートにお問い合わせください。

   ![edit_settings_fordynamic-media-replication2](assets/edit_settings_fordynamic-media-replication2.png)

1. 「**[!UICONTROL 保存して閉じる]**」をタップして、このユーザーに対する変更を保存します。

   次に、[レプリケーションエージェントを設定します。](#configuring-the-replication-agent)

### レプリケーションエージェントの設定 {#configuring-the-replication-agent}

1. AEM で、AEM のロゴをタップしてグローバルナビゲーションコンソールにアクセスし、**[!UICONTROL ツール／デプロイ／レプリケーション／作成者のエージェント]**&#x200B;をタップします。
1. 作成者のエージェントページで、「**[!UICONTROL Dynamic Media ハイブリッド画像レプリケーション（s7delivery）]**」をタップします。
1. 「**[!UICONTROL 編集]**」をタップします。
1. 次をタップします。 **[!UICONTROL 設定]** 「 」タブで、次の情報を入力します。

   * **[!UICONTROL 有効]** - レプリケーションエージェントを有効にするには、このチェックボックスを選択します。
   * **[!UICONTROL 地域]** - 北米、ヨーロッパまたはアジアから適切な地域を設定します。
   * **[!UICONTROL テナント ID]** - この値は、レプリケーションサービスに公開している会社またはテナントの名前です。この値は、プロビジョニング中に送信された「ようこそメール」でアドビから提供されたテナント ID です。この情報を受け取っていない場合は、Adobeカスタマーサポートにお問い合わせください。
   * **[!UICONTROL キーストアのエイリアス]**  — この値は、でキーを生成する際に設定された「**新規エイリアス**」の値と同じです。 [認証の設定](#setting-up-authentication);例： `replication`. （[認証の設定](#setting-up-authentication)のステップ 7 を参照。）
   * **[!UICONTROL キーストアのパスワード]**  — これは、タップしたときに作成されたキーストアのパスワードです **[!UICONTROL キーストアを作成]**. このパスワードはアドビが提供するものではありません。[認証の設定](#setting-up-authentication)のステップ 5 を参照してください。

   次の画像はサンプルデータが入力されたレプリケーションエージェントを示します。

   ![chlimage_1-509](assets/chlimage_1-509.png)

1. 「**[!UICONTROL OK]**」をタップします。

### Dynamic Media 用のレプリケーションエージェントの検証 {#validating-the-replication-agent-for-dynamic-media}

Dynamic Media のレプリケーションエージェントを検証するには、以下の手順を実行します。

タップ **[!UICONTROL 接続をテスト]**. 次のように出力されます。

```shell
11.03.2016 10:57:55 - Transferring content for ReplicationAction{type=TEST, path[0]='/content/dam', time=1457722675402, userId='admin', revision='null'}
11.03.2016 10:57:55 - * Auth User: replication-receiver
11.03.2016 10:57:55 - * HTTP Version: 1.1
11.03.2016 10:57:55 - * Using OAuth 2.0 Authorization Grants
11.03.2016 10:57:55 - * OAuth 2.0 User: dynamic-media-replication
11.03.2016 10:57:55 - * OAuth 2.0 Token: '*****' initialized
11.03.2016 10:57:55 - Publishing: POST[https://replicate-na.assetsadobe.com:8580/is-publish/publish-receiver?Cmd=Test&RootId=xfpuu-6613]
11.03.2016 10:57:55 - Publish response: OK[]
11.03.2016 10:57:55 - Transfer succeeded in 141 ms for ReplicationAction{type=TEST, path[0]='/content/dam', time=1457722675402, userId='admin', revision='null'}
-------------------------------------------------------------------------------------------------------------------------------
Replication test succeeded
```

>[!NOTE]
次のいずれかを実行してチェックすることもできます。
* レプリケーションログをチェックしてアセットがレプリケートされていることを確認する。
* 画像をパブリッシュします。画像をタップし、「 」を選択します。 **[!UICONTROL ビューア]** 」と入力します。 ビューアプリセットを選択し、をタップします。 **[!UICONTROL URL]**&#x200B;をクリックし、URL をコピーしてブラウザーに貼り付け、画像が表示されることを確認します。


### 認証のトラブルシューティング {#troubleshooting-authentication}

認証の設定時に発生する可能性がある問題と、その解決策を紹介します。その前に、レプリケーションが設定済みであることを確認してください。

#### 問題：HTTP ステータスコード 401 が「Authorization Required（認可が必要）」というメッセージとともに返る {#problem-http-status-code-with-message-authorization-required}

この問題は、`dynamic-media-replication` ユーザーのキーストアの設定に失敗したことによって発生する可能性があります。

```shell
Replication test to s7delivery:https://s7bern.macromedia.com:8580/is-publish/
17.06.2016 18:54:43 - Transferring content for ReplicationAction{type=TEST, path[0]='/content/dam', time=1466214883309, userId='admin', revision='null'}
17.06.2016 18:54:43 - * Auth User: replication-receiver
17.06.2016 18:54:43 - * HTTP Version: 1.1
17.06.2016 18:54:43 - * Using OAuth 2.0 Authorization Grants
17.06.2016 18:54:43 - * OAuth 2.0 User: dynamic-media-replication
17.06.2016 18:54:43 - No OAuth token available. OAuth not initialized
17.06.2016 18:54:43 - * Using Client Auth SSL alias - replication-alias *
17.06.2016 18:54:43 - Publishing: POST[https://<localhost>:8580/is-publish//publish-receiver?Cmd=Test&RootId=brough]
17.06.2016 18:54:43 - Transfer failed for ReplicationAction{type=TEST, path[0]='/content/dam', time=1466214883309, userId='admin', revision='null'}. java.io.IOException: Failed to execute request
'https://<localhost>:8580/is-publish//publish-receiver?Cmd=Test&RootId=brough':
 Server returned status code 401 with message: Authorization required.
17.06.2016 18:54:43 - Error while replicating: com.day.cq.replication.ReplicationException: Transfer failed for ReplicationAction{type=TEST, path[0]='/content/dam', time=1466214883309,
 userId='admin', revision='null'}. java.io.IOException: Failed to execute request
'https://<localhost>:8580/is-publish//publish-receiver?Cmd=Test&RootId=brough':
 Server returned status code 401 with message: Authorization required.
```

**解決策**:以下を確認します。 `KeyStore` 次に保存： **[!UICONTROL dynamic-media-replication]** ユーザーに割り当てられ、正しいパスワードが提供されます。

#### 問題：鍵を復号化できない - データを復号化できない {#problem-could-not-decrypt-key-could-not-decrypt-data}

```xml
Replication test to s7delivery:https://<localhost>:8580/is-publish/
17.06.2016 19:00:16 - Transferring content for ReplicationAction{type=TEST, path[0]='/content/dam', time=1466215216662, userId='admin', revision='null'}
17.06.2016 19:00:16 - * Auth User: replication-receiver
17.06.2016 19:00:16 - * HTTP Version: 1.1
17.06.2016 19:00:16 - * Using OAuth 2.0 Authorization Grants
17.06.2016 19:00:16 - * OAuth 2.0 User: dynamic-media-replication
17.06.2016 19:00:16 - No OAuth token available. OAuth not initialized
17.06.2016 19:00:16 - * Using Client Auth SSL alias - replication-alias *
17.06.2016 19:00:16 - Transfer failed for ReplicationAction{type=TEST, path[0]='/content/dam', time=1466215216662, userId='admin', revision='null'}. java.lang.SecurityException: java.security.UnrecoverableKeyException: Could not decrypt key: Could not decrypt data.
```

**解決策**：パスワードを確認します。レプリケーションエージェントに保存されたパスワードがキーストアの作成に使用されたパスワードと同じでありません。

#### 問題：InvalidAlgorithmParameterException {#problem-invalidalgorithmparameterexception}

この問題は AEM オーサーインスタンスの設定エラーが原因です。Author の java プロセスが正しい `javax.net.ssl.trustStore` を取得していません。このエラーは次のレプリケーションログで確認できます。

```shell
14.04.2016 09:37:43 - Transfer failed for ReplicationAction{type=TEST, path[0]='/content/dam', time=1460651862089, userId='admin', revision='null'}. java.io.IOException: Failed to execute request 'https://<localhost>:8580/is-publish/publish-receiver?Cmd=Test&RootId=rbrough-osx2': java.lang.RuntimeException: Unexpected error: java.security.InvalidAlgorithmParameterException: the trustAnchors parameter must be non-empty
14.04.2016 09:37:43 - Error while replicating: com.day.cq.replication.ReplicationException: Transfer failed for ReplicationAction{type=TEST, path[0]='/content/dam', time=1460651862089, userId='admin', revision='null'}. java.io.IOException: Failed to execute request 'https://<localhost>:8580/is-publish/publish-receiver?Cmd=Test&RootId=rbrough-osx2': java.lang.RuntimeException: Unexpected error: java.security.InvalidAlgorithmParameterException: the trustAnchors parameter must be non-empty
```

または、次のエラーログで確認できます。

```shell
07.25.2019 12:00:59.893 *ERROR* [sling-threadpool-db2763bb-bc50-4bb5-bb64-10a09f432712-(apache-sling-job-thread-pool)-90-com_day_cq_replication_job_s7delivery(com/day/cq/replication/job/s7delivery)] com.day.cq.replication.Agent.s7delivery.queue Error during processing of replication.
 
java.io.IOException: Failed to execute request 'https://replicate-na.assetsadobe.com:8580/is-publish/publish-receiver?Cmd=Test&RootId=rbrough-osx': java.lang.RuntimeException: Unexpected error: java.security.InvalidAlgorithmParameterException: the trustAnchors parameter must be non-empty
        at com.scene7.is.catalog.service.publish.atomic.PublishingServiceHttp.executePost(PublishingServiceHttp.scala:195)
```

**解決策**:AEM オーサー上の Java プロセスに system プロパティがあることを確認します。 **-Djavax.net.ssl.trustStore=** 有効な truststore に設定します。

#### 問題：キーストアが設定されていないか初期化されていない {#problem-keystore-is-either-not-set-up-or-it-is-not-initialized}

この問題は、ホットフィックスまたは機能パックによって **[!UICONTROL dynamic-media-user]** または **[!UICONTROL keystore]** ノード。

レプリケーションログの例は次のとおりです。

```shell
Replication test to s7delivery:https://replicate-na.assetsadobe.com/is-publish
02.08.2016 14:37:44 - Transferring content for ReplicationAction{type=TEST, path[0]='/content/dam', time=1470173864834, userId='admin', revision='null'}
02.08.2016 14:37:44 - * Auth User: replication-receiver
02.08.2016 14:37:44 - * HTTP Version: 1.1
02.08.2016 14:37:44 - * Using OAuth 2.0 Authorization Grants
02.08.2016 14:37:44 - * OAuth 2.0 User: dynamic-media-replication
02.08.2016 14:37:44 - Transfer failed for ReplicationAction{type=TEST, path[0]='/content/dam', time=1470173864834, userId='admin', revision='null'}. com.adobe.granite.keystore.KeyStoreNotInitialisedException: Uninitialised key store for user dynamic-media-replication
```

**ソリューション**：

1. 次に移動： **[!UICONTROL ユーザー管理]** ページ：

   `localhost:4502/libs/granite/security/content/useradmin.html`
1. の **[!UICONTROL ユーザー管理]** ページで、 **[!UICONTROL dynamic-media-replication]** をタップし、開きます。
1. 次をタップします。 **[!UICONTROL キーストア]** タブをクリックします。 「**[!UICONTROL キーストアを作成]**」ボタンが表示された場合は、前述の[認証の設定](#setting-up-authentication)の手順をやり直す必要があります。
1. もし **[!UICONTROL キーストア]** 設定が必要な場合は、 [レプリケーションエージェントの設定](config-dynamic.md#configuring-the-replication-agent) また同様に。

   s7delivery レプリケーションエージェントを再設定します。

   `localhost:4502/etc/replication/agents.author/s7delivery.html`

1. 「**[!UICONTROL 接続をテスト]**」をタップして設定が有効であることを確認します。

#### 問題：公開エージェントが OAuth ではなく SSL を使用している {#problem-publish-agent-is-using-ssl-instead-of-oauth}

この問題は、ホットフィックスまたは機能パックが正しくインストールされなかったか設定を上書きしたことが原因で発生する可能性があります。

レプリケーションログの例は次のとおりです。

```shell
01.08.2016 18:42:59 - Transferring content for ReplicationAction{type=TEST, path[0]='/content/dam', time=1470073379634, userId='admin', revision='null'}
01.08.2016 18:42:59 - * Auth User: replication-receiver
01.08.2016 18:42:59 - * HTTP Version: 1.1
01.08.2016 18:42:59 - * Using Client Auth SSL alias - replication-receiver *
01.08.2016 18:42:59 - Publishing: POST[https://replicate-eu.assetsadobe2.com:443/is-publish/publish-receiver?Cmd=Test&RootId=altayerstaging]
01.08.2016 18:42:59 - Transfer failed for ReplicationAction{type=TEST, path[0]='/content/dam', time=1470073379634, userId='admin', revision='null'}. java.io.IOException: Failed to execute request 'https://replicate-eu.assetsadobe2.com:443/is-publish/publish-receiver?Cmd=Test&RootId=rbroughstaging': Server returned status code 401 with message: Authorization required.
01.08.2016 18:42:59 - Error while replicating: com.day.cq.replication.ReplicationException: Transfer failed for ReplicationAction{type=TEST, path[0]='/content/dam', time=1470073379634, userId='admin', revision='null'}. java.io.IOException: Failed to execute request 'https://replicate-eu.assetsadobe2.com:443/is-publish/publish-receiver?Cmd=Test&RootId=rbroughstaging': Server returned status code 401 with message: Authorization required.
```

**解決策：**

1. AEM で、**[!UICONTROL ツール／一般／CRXDE Lite]** をタップします。

   `localhost:4502/crx/de/index.jsp`

1. 次に移動： **[!UICONTROL s7delivery レプリケーションエージェント]** ノード。

   `localhost:4502/crx/de/index.jsp#/etc/replication/agents.author/s7delivery/jcr:content`

1. この設定をレプリケーションエージェントに追加します（値を **[!UICONTROL True]** に設定したブール値）。

   `enableOauth=true`

1. ページの左上隅付近にある「**[!UICONTROL すべて保存]**」をタップします。

### 設定のテスト {#testing-your-configuration}

アドビでは、エンドツーエンドで設定のテストを実施することをお勧めしています。

このテストを開始する前に、既に以下をおこなったことを確認してください。

* 画像プリセットを追加した。
* 設定 **Dynamic Media設定（6.3 以前）** under **[!UICONTROL Cloud Services]**. このテストでは画像サービスの URL が必要です。

設定をテストするには：

1. 画像アセットをアップロードします。(Assets で、 **[!UICONTROL 作成/ファイル]** をクリックし、ファイルを選択します )。
1. ワークフローが完了するまで待ちます。
1. 画像アセットを公開します（アセットを選択し、「**[!UICONTROL クイック公開]**」をタップします。）
1. 画像を開いて画像のレンディションに移動し、「**[!UICONTROL レンディション]**」をタップします。

   ![chlimage_1-510](assets/chlimage_1-510.png)

1. 任意の動的レンディションを選択します。
1. タップ **[!UICONTROL URL]** をクリックして、このアセットの URL を取得します。
1. 選択した URL に移動して画像が期待どおりに動作するかどうかを確認します。

アセットが配信されたことをテストするもう 1 つの方法は、URL に req=exists を追加することです。

## Dynamic Media クラウドサービスの設定 {#configuring-dynamic-media-cloud-services}

Dynamic Media クラウドサービスは、画像とビデオのハイブリッド公開および配信、ビデオ分析、ビデオエンコーディングなどの様々なクラウドサービスをサポートします。

設定の一環として、登録 ID、ビデオサービス URL、画像サービス URL、レプリケーションサービス URL を入力し、認証を設定する必要があります。アカウントプロビジョニングプロセスの一環として、この情報をすべて受け取っているはずです。 この情報を受け取っていない場合は、Adobe Experience Manager管理者またはAdobeテクニカルサポートに連絡して、情報を入手してください。

>[!NOTE]
Dynamic Media クラウドサービスを設定する前に、パブリッシュインスタンスを設定しておく必要があります。Dynamic Media クラウドサービスを設定する前に、レプリケーションも設定しておく必要があります。

**Dynamic Media クラウドサービスを設定するには：**:

1. AEMで、AEMロゴをタップしてグローバルナビゲーションコンソールにアクセスし、をタップします。 **[!UICONTROL ツール/Cloud Services/ Dynamic Media設定（6.3 以前）]**.
1. の **[!UICONTROL Dynamic Media Configuration Browser]** ページの左側のウィンドウで、「 」を選択します。 **[!UICONTROL global]**&#x200B;次に、 **[!UICONTROL 作成]**.
1. **[!UICONTROL Dynamic Media 設定を作成]**&#x200B;ダイアログボックスで、「タイトル」フィールドにタイトルを入力します。****
1. ビデオ用に Dynamic Media を設定する場合は、次の操作をおこないます。

   * 「**[!UICONTROL 登録 ID]**」フィールドに登録 ID を入力します。
   * 「**[!UICONTROL ビデオサービスの URL]**」フィールドに、Dynamic Media ゲートウェイのビデオサービス URL を入力します。

1. 画像用に Dynamic Media を設定する場合は、「**[!UICONTROL 画像サービスの URL]**」フィールドに Dynamic Media ゲートウェイの画像サービスの URL を入力します。
1. 「**[!UICONTROL 保存]**」をタップして Dynamic Media 設定ブラウザーページに戻ります。
1. AEM のロゴをタップしてグローバルナビゲーションコンソールにアクセスします。

## ビデオレポートの設定 {#configuring-video-reporting}

Dynamic Media — ハイブリッドモードを使用すると、AEMの複数のインストールにわたってビデオレポートを設定できます。

**使用するタイミング：** 設定時に **[!UICONTROL Dynamic Media設定（6.3 以前）]**&#x200B;を使用すると、ビデオレポートを含む多数の機能が開始されます。 設定時には、地域の Analytics 企業内にレポートスイートが作成されます。複数のオーサーノードを設定すると、ノードごとに異なるレポートスイートが作成されます。このため、インストール間でレポートデータの整合性が取れなくなります。さらに、すべてのオーサーノードが同じハイブリッドパブリッシュサーバーを参照している場合、最後のオーサーノードでのインストール時に、すべてのビデオレポートの報告先となるレポートスイートが変更されてしまいます。この問題が発生すると、過剰な数のレポートスイートによって Analytics システムが過負荷状態に陥ります。

**手順概要：**&#x200B;ビデオレポートを設定するには、以下の 3 つのタスクを実行します。

1. の作成 [!DNL Video Analytics] 設定後のプリセットパッケージ **[!UICONTROL Dynamic Media設定（6.3 以前）]** を最初のオーサーノードに置き換えます。 この最初のタスクは重要です。これにより、新しい設定でも引き続き同じレポートスイートを使用できるからです。
1. のインストール [!DNL Video Analytics] 任意のにプリセットパッケージを ***新規*** 作成者ノード ***前*** Dynamic Media設定（6.3 以前）を設定します。

1. パッケージインストールの検証とデバッグを行います。

### の作成 [!DNL Video Analytics] 最初のオーサーノードを設定した後のプリセットパッケージ {#creating-a-video-analytics-preset-package-after-configuring-the-first-author-node}

このタスクが完了すると、 [!DNL Video Analytics] プリセット。 これらのプリセットには、レポートスイート、トラッキングサーバー、トラッキング名前空間および Marketing Cloud 組織 ID（利用可能な場合）が含まれます。

1. まだおこなっていない場合は、 **[!UICONTROL Dynamic Media設定（6.3 以前）]**.
1. （オプション） **[!UICONTROL レポートスイート ID]** （JCR にアクセスできる必要があります）。 を **[!UICONTROL レポートスイート ID]** が不要な場合は、検証が容易になります。
1. を使用してパッケージを作成 **[!UICONTROL パッケージマネージャー]**.
1. パッケージを編集してフィルターを含めます。

   AEM で: `/conf/global/settings/dam/dm/presets/analytics/jcr:content/userdata`

1. パッケージをビルドします。
1. をダウンロードまたは共有する [!DNL Video Analytics] プリセットパッケージを使用して、後続の新しいオーサーノードと共有できるようにします。

### のインストール [!DNL Video Analytics] プリセットパッケージを使用して、追加のオーサーノードを設定します。 {#installing-the-video-analytics-preset-package-before-you-configure-additional-author-nodes}

このタスクを必ず完了してください _前_ 設定 **[!UICONTROL Dynamic Media設定（6.3 以前）]**. そうしないと、別の未使用のレポートスイートが作成されてしまいます。また、ビデオレポートは引き続き正しく機能しますが、データの収集は最適化されません。

必ず [!DNL Video Analytics] 最初のオーサーノードのプリセットパッケージには、新しいオーサーノードでアクセスできます。

1. をアップロードします。 [!DNL Video Analytics] 以前に作成したプリセットパッケージ **[!UICONTROL パッケージマネージャー]**.
1. のインストール [!DNL Video Analytics] プリセットパッケージ。
1. 設定 **[!UICONTROL Dynamic Media設定（6.3 以前）]**.

### パッケージインストールの確認やデバッグ {#verifying-and-debugging-the-package-installation}

1. 次のいずれかを実施してパッケージのインストールを検証し、必要に応じてデバッグを行います。

   * **次を確認します。 [!DNL Video Analytics] JCR を介して事前設定される**
次の手順で [!DNL Video Analytics] JCR を介して事前に設定されている場合、 **[!UICONTROL CRXDE Lite]**.

      AEM - In **[!UICONTROL CRXDE Lite]**&#x200B;に移動します。 `/conf/global/settings/dam/dm/presets/analytics/jcr:content/userdata  `

      これは `http://localhost:4502/crx/de/index.jsp#/conf/global/settings/dam/dm/presets/analytics/jcr%3Acontent/userdata`

      にアクセスできない場合 **[!UICONTROL CRXDE Lite]** オーサーノードで、パブリッシュサーバーを通じてプリセットを確認できます。

   * **次を確認します。 [!DNL Video Analytics] Image Server を使用してプリセット**

      以下を検証します。 [!DNL Video Analytics] Image Server を作成して直接プリセットする `req=userdata` リクエスト。

      例えば、 [!DNL Video Analytics] プリセットをオーサーノードで設定すると、次のリクエストを実行できます。

      `http://localhost:4502/is/image/conf/global/settings/dam/dm/presets/analytics?req=userdata`

      パブリッシュサーバーでプリセットを検証するには、パブリッシュサーバーに対して同様のリクエストを直接実行します。応答はオーサーノードとパブリッシュノードで同じになります。レスポンスは次のようになります。

      ```
      marketingCloudOrgId=0FC4E86B573F99CC7F000101
       reportSuite=aemaem6397618-2018-05-23
       trackingNamespace=aemvideodal
       trackingServer=aemvideodal.d2.sc.omtrdc.net
      ```

   * **次を確認します。 [!DNL Video Analytics] AEMのビデオレポートツールを使用してプリセット**

      タップ **[!UICONTROL ツール/ Assets /ビデオレポート]** `http://localhost:4502/mnt/overlay/dam/gui/content/s7dam/videoreports/videoreport.html`

      次のエラーメッセージが表示された場合は、レポートスイートは使用可能ですが、未入力です。新しいインストールでは、システムがデータの収集を開始する前であれば、このエラーは正しく、むしろ望ましいと言えます。

      ![screen_shot_2018-05-23at52254pm](assets/screen_shot_2018-05-23at52254pm.png)
   レポートデータを生成するには、1 つのビデオをアップロードして公開します。「**[!UICONTROL URL をコピー]**」を使用し、ビデオを 1 回以上再生します。

   ビデオビューアの使用に基づいてレポートデータが格納されるまで、最大 12 時間かかる可能性があることに注意してください。

    エラーが発生し、レポートスイートが正しく設定されない場合は、次のアラートが表示されます。

   ![screen_shot_2018-05-23at52612pm](assets/screen_shot_2018-05-23at52612pm.png)

   このエラーは、設定前にビデオレポートが実行された場合にも表示されます **[!UICONTROL Dynamic Media設定（6.3 以前）]** サービス。

### ビデオレポートの設定のトラブルシューティング {#troubleshooting-the-video-reporting-configuration}

* インストール中に Analytics API サーバーへの接続がタイムアウトすることがあります。インストール中に接続が 20 回再試行されますが、それでも失敗します。この状況が発生すると、ログファイルに複数のエラーが記録されます。`SiteCatalystReportService` を検索します。
* をインストールしていません [!DNL Video Analytics] 最初にプリセットパッケージを作成すると、新しいレポートスイートが作成されます。
* AEM 6.3 からAEM 6.4 またはAEM 6.4.1 へのアップグレード後の設定 **[!UICONTROL Dynamic Media設定（6.3 以前）]**&#x200B;では、引き続きレポートスイートが作成されます。 これは既知の問題であり、AEM 6.4.2 で修正される予定です。

### について [!DNL Video Analytics] プリセット {#about-the-video-analytics-preset}

この [!DNL Video Analytics] プリセット — 単に analytics プリセットとも呼ばれる場合があります。Dynamic Mediaのビューアプリセットの横に保存されます。 これは基本的にはビューアプリセットと同じですが、AppMeasurement および Video Heartbeat レポートの設定に使用される情報が付加されています。

このプリセットのプロパティは次のとおりです。

* **[!UICONTROL reportSuite]**
* **[!UICONTROL trackingServer]**
* **[!UICONTROL trackingNamespace]**
* **[!UICONTROL marketingCloudOrgId]** ( 古いAEMバージョンには存在しません )

AEM 6.4 以降のバージョンでは、このプリセットを次の場所に保存します。 `/conf/global/settings/dam/dm/presets/analytics/jcr:content/userdata`

## カタログ設定のレプリケート {#replicating-catalog-settings}

設定プロセスの一環として、独自のデフォルトのカタログ設定を JCR を通じて公開する必要があります。カタログ設定をレプリケートするには、以下の手順に従います。

1. ターミナルウィンドウで以下を実行します。

   `curl -u admin:admin localhost:4502/libs/settings/dam/dm/presets/viewer.pushviewerpresets`

1. AEMで、次の場所 ( **[!UICONTROL CRXDE Lite]** （管理者権限が必要）:

   `https://<server>:<port>/crx/de/index.jsp#/conf/global/settings/dam/dm/imageserver/`

1. 「**[!UICONTROL レプリケーション]**」タブをタップします。
1. 「**[!UICONTROL 複製]**」をタップします。

## ビューアプリセットのレプリケート {#replicating-viewer-presets}

ビューアプリセットを使用して アセットを配信するには、 ビューアプリセットをレプリケートおよび公開する必要があります。（すべてのビューアプリセットをアクティベートする必要があります） _および_ レプリケートされているので、URL を取得したり、アセットの埋め込みコードを取得したりできます )。 詳しくは、[ビューアプリセットの公開](managing-viewer-presets.md#publishing-viewer-presets)を参照してください。

>[!NOTE]
デフォルトでは、「 **[!UICONTROL レンディション]** を選択し、 **[!UICONTROL ビューア]** （アセットの詳細表示）。 表示される数を増減させることができます。詳しくは、 [表示される画像プリセット数の増加](/help/assets/managing-image-presets.md#increasing-or-decreasing-the-number-of-image-presets-that-display) または [表示されるビューアプリセットの数の増減](/help/assets/managing-viewer-presets.md#increasing-the-number-of-viewer-presets-that-display).

## レプリケーション用のアセットのフィルタリング {#filtering-assets-for-replication}

非Dynamic Mediaデプロイメントでは、 _すべて_ アセット（画像とビデオの両方）をAEMオーサー環境からAEMパブリッシュノードに移行します。 AEMパブリッシュサーバーもアセットを配信するので、このワークフローが必要です。

ただし、Dynamic Mediaのデプロイメントでは、アセットはクラウド経由で配信されるので、AEMのパブリッシュノードに同じアセットをレプリケートする必要はありません。 そのような「ハイブリッドパブリッシング」ワークフローでは、ストレージコストの増大を防ぎ、アセットをレプリケートするための処理時間を短縮します。Dynamic Media ビューア、サイトページ、静的コンテンツなどのその他のコンテンツは、引き続き AEM パブリッシュノードから配信されます。

アセットのレプリケートに加えて、次のアセット以外の要素もレプリケートされます。

* Dynamic Media 配信設定：`/conf/global/settings/dam/dm/imageserver/configuration/jcr:content/settings`
* 画像プリセット：`/conf/global/settings/dam/dm/presets/macros`
* ビューアプリセット：`/conf/global/settings/dam/dm/presets/viewer`

フィルターによって、アセットを AEM パブリッシュノードへのレプリケート対象から&#x200B;__&#x200B;除外することができます。

### レプリケーションにデフォルトのアセットフィルターを使用 {#using-default-asset-filters-for-replication}

実稼動環境でDynamic Mediaを 1) 画像を使用している場合 _または_ 2) 画像とビデオの場合は、アドビが提供するデフォルトのフィルターをそのまま使用できます。 以下のフィルターがデフォルトでアクティブです。

<table> 
 <tbody> 
  <tr> 
   <td> </td> 
   <td><strong>フィルター</strong></td> 
   <td><strong>MIME タイプ</strong></td> 
   <td><strong>レンディション</strong></td> 
  </tr> 
  <tr> 
   <td>Dynamic Media 画像配信</td> 
   <td><p>filter-images</p> <p>filter-sets</p> <p> </p> </td> 
   <td><p><strong>image/</strong> で始まる</p> <p><strong>application/</strong> を含み、<strong>set</strong> で終わる</p> </td> 
   <td>標準提供の「filter-images」（インタラクティブな画像などの単一の画像アセットに適用）および「filter-sets」（スピンセット、画像セット、混在メディアセットおよびカルーセルセット）では、次のようになります。 
    <ul> 
     <li>PTIFF 画像とメタデータ（<strong>cqdam</strong> で始まるすべてのレンディション）がレプリケーションに含まれます。</li> 
     <li>オリジナル画像と静的画像レンディションがレプリケーションから除外されます。</li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td>ダイナミックメディアビデオ配信</td> 
   <td>filter-video</td> 
   <td><strong>video/</strong> で始まる</td> 
   <td>標準提供の「filter-video」では、次のようになります。 
    <ul> 
     <li>プロキシビデオのレンディション、ビデオサムネールやポスター画像、メタデータ（親ビデオとビデオレンディションの両方）がレプリケーションに含まれます（<strong>cqdam</strong> で始まるすべてのレンディション）。</li> 
     <li>オリジナルのビデオと静的サムネールのレンディションはレプリケーションから除外されます。<br /> <br /> <strong>メモ：</strong>プロキシビデオのレンディションはバイナリを含まず、ノードプロパティのみになります。このため、公開者のリポジトリサイズへの影響はありません。</li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td>Dynamic Media Classic統合</td> 
   <td><p>filter-images</p> <p>filter-sets</p> <p>filter-video</p> </td> 
   <td><p><strong>image/</strong> で始まる</p> <p><strong>application/</strong> を含み、<strong>set</strong> で終わる</p> <p><strong>video/</strong> で始まる</p> </td> 
   <td><p>「トランスポート URI」を、アドビのダイナミックメディアクラウドレプリケーションサービス URL の代わりに AEM パブリッシュサーバーを参照するように設定します。このフィルターを設定すると、AEM パブリッシュインスタンスではなく、Dynamic Media Classic でアセットを配信できます。</p> <p>デフォルトの「filter-images」、「filter-sets」、「filter-video」では次のようになります。</p> 
    <ul> 
     <li>PTIFF 画像、プロキシビデオのレンディション、メタデータがレプリケーションに含まれます。ただし、AEM - Dynamic Media Classic 統合を実行するレプリケーション用の JCR にはこれらの画像やメタデータは存在しないので、実質的には何も起こりません。</li> 
     <li>オリジナル画像、静的画像レンディション、オリジナルビデオ、静的サムネールのレンディションがレプリケーションから除外されます。代わりに、Dynamic Media Classic が画像およびビデオアセットを配信します。</li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table>

>[!NOTE]
フィルターは、MIME タイプに適用され、パス用にはできません。

### ビデオのみのデプロイメント用のアセットフィルターのセットアップ {#setting-up-asset-filters-for-video-only-deployments}

Dynamic Media をビデオのみに使用している場合は、次の手順に従ってレプリケーション用のアセットフィルターを設定します。

1. AEMで、AEMロゴをタップしてグローバルナビゲーションコンソールにアクセスし、をタップします。 **[!UICONTROL ツール/導入/レプリケーション/作成者のエージェント]**.
1. 作成者のエージェントページで、「**[!UICONTROL デフォルトエージェント（公開）]**」をタップします。
1. 「**[!UICONTROL 編集]**」をタップします。
1. **[!UICONTROL エージェントの設定]**&#x200B;ダイアログボックスの「[!UICONTROL 設定]」タブで、「**[!UICONTROL 有効]**」のチェックをオンにしてエージェントを有効にします。
1. 「**[!UICONTROL OK]**」をタップします。
1. AEM で、**[!UICONTROL ツール／一般／CRXDE Lite]** をタップします。
1.  左側のフォルダーツリーで、`/etc/replication/agents.author/dynamic_media_replication/jcr:content/damRenditionFilters` に移動します。
1. [!UICONTROL filter-video] を探して右クリックし、「**[!UICONTROL コピー]**」を選択します。
1.  左側のフォルダーツリーで、`/etc/replication/agents.author/publish` に移動します。
1. [!UICONTROL filter-video] を探して右クリックし、「**[!UICONTROL 貼り付け]**」を選択します。

これにより AEM のパブリッシュインスタンスがビデオのポスター画像と再生に必要なビデオのメタデータを配信するように設定され、ビデオ自体は Dynamic Media メディアクラウドサービスによって配信されます。また、パブリッシュインスタンスに不要な元のビデオと静的なサムネールのレンディションがフィルターによってレプリケーションから除外されます。

### 実稼動以外のデプロイメントでのイメージング用のアセットフィルターのセットアップ {#setting-up-asset-filters-for-imaging-in-non-production-deployments}

実稼動以外のデプロイメントで画像に Dynamic Media を使用している場合は、次の手順に従ってレプリケーション用のアセットフィルターを設定します。

1. AEMで、AEMロゴをタップしてグローバルナビゲーションコンソールにアクセスし、をタップします。 **[!UICONTROL ツール/導入/レプリケーション/作成者のエージェント]**.
1. 作成者のエージェントページで、「**[!UICONTROL デフォルトエージェント（公開）]**」をタップします。
1. 「**[!UICONTROL 編集]**」をタップします。
1. **[!UICONTROL エージェントの設定]**&#x200B;ダイアログボックスの「**[!UICONTROL 設定]**」タブで、「**[!UICONTROL 有効]**」のチェックをオンにしてエージェントを有効にします。
1. 「**[!UICONTROL OK]**」をタップします。
1. AEM で、**[!UICONTROL ツール／一般／CRXDE Lite]** をタップします。
1. 左側のフォルダーツリーで、`/etc/replication/agents.author/dynamic_media_replication/jcr:content/damRenditionFilters` に移動します。

   ![image-2018-01-16-10-22-40-410](assets/image-2018-01-16-10-22-40-410.png)

1. **[!UICONTROL filter-images]** を探して右クリックし、「**[!UICONTROL コピー]**」を選択します。
1.  左側のフォルダーツリーで、`/etc/replication/agents.author/publish` に移動します。
1. 場所 **[!UICONTROL jcr:content]**、右クリックして「 」を選択します。 **[!UICONTROL 作成/ノードを作成]**. タイプ `nt:unstructured` の名前 `damRenditionFilters` を入力します。
1. 場所 [!UICONTROL `damRenditionFilters`]、右クリックして「 」を選択します。 **[!UICONTROL 貼り付け]**.

これにより、AEM のパブリッシュインスタンスが画像を実稼動以外の環境に配信します。また、パブリッシュインスタンスに不要な元の画像と静的なレンディションがフィルターによってレプリケーションから除外されます。

>[!NOTE]
1 人の作成者に異なるフィルターが多数ある場合は、各エージェントに異なるユーザーを割り当てる必要があります。Granite コードでは、ユーザーごとに 1 つのフィルターというモデルが適用されます。フィルターを設定するたびに、必ず、異なるユーザーを使用してください。
1 つのサーバーで複数のフィルター（例えば、公開するレプリケーション用のフィルターと s7delivery 用のフィルター）を使用している場合は、これら 2 つのフィルターに異なるフィルターを設定する必要があります **userId** で割り当てられた **[!UICONTROL jcr:content]** ノード。 次の画像を参照してください。

![image-2018-01-16-10-26-28-465](assets/image-2018-01-16-10-26-28-465.png)

### レプリケーション用のアセットフィルターのカスタマイズ {#customizing-asset-filters-for-replication}

（オプション）レプリケーション用のアセットフィルターをカスタマイズするには：

1. AEMで、AEMロゴをタップしてグローバルナビゲーションコンソールにアクセスし、をタップします。 **[!UICONTROL ツール/一般/CRXDE Lite]**.
1. 左側のフォルダーツリーで、`/etc/replication/agents.author/dynamic_media_replication/jcr:content/damRenditionFilters` に移動し、フィルターを確認します。

   ![chlimage_1-511](assets/chlimage_1-511.png)

1. フィルターの MIME タイプを定義するために、次のように MIME タイプを特定することができます。

   左側のレールで、を展開します。 **[!UICONTROL content/dam > &lt;`locate_your_asset`> > jcr:content > metadata]**&#x200B;をクリックし、テーブルで `dc:format`.

   次の図は、アセットの `dc:format` へのパスの例を示しています。

   ![chlimage_1-512](assets/chlimage_1-512.png)

   アセット `Fiji Red.jpg` の `dc:format` が `image/jpeg` であることを確認してください。

   このフィルターを形式に関係なくすべての画像に適用するには、値を `image/*` に設定します。`*` は、あらゆる形式のすべての画像に適用される正規表現です。

   このフィルターを JPEG タイプの画像のみに適用するには、`image/jpeg` という値を入力します。

1. レプリケーションに含める、または除外するレンディションを定義します。

   レプリケーション用のフィルターに使用できる文字は次のとおりです。

<table> 
 <tbody> 
  <tr> 
   <td><strong>使用する文字</strong></td> 
   <td><strong>レプリケーション用のアセットのフィルター方法</strong></td> 
  </tr> 
  <tr> 
   <td>*</td> 
   <td>ワイルドカード文字<br /> </td> 
  </tr> 
  <tr> 
   <td>+</td> 
   <td>レプリケーション用にアセットを含める。</td> 
  </tr> 
  <tr> 
   <td>-</td> 
   <td>レプリケーションからアセットを除外する.</td> 
  </tr> 
 </tbody> 
</table>

`content/dam/<locate_your_asset>/jcr:content/renditions` に移動します。

次の図は、アセットのレンディションの例を示しています。

![chlimage_1-513](assets/chlimage_1-513.png)

上記の例を使用して PTIFF（Pyramid TIFF）のみをレプリケートする場合は、`+cqdam,*` と入力します。この値は、`cqdam` で始まるすべてのレンディションを含むことを示します。例では、そのレンディションは `cqdam.pyramid.tiff`.

オリジナルのみをレプリケートする場合は、`+original` と入力します。

## Dynamic Media 画像サーバーの設定 {#configuring-dynamic-media-image-server-settings}

Dynamic Media 画像サーバーの設定では、Adobe CQ Scene7 ImageServer バンドルと Adobe CQ Scene7 PlatformServer バンドルの編集をおこないます。

>[!NOTE]
Dynamic Media は、[有効にした後](#enabling-dynamic-media)、すぐに標準の機能を実行することができます。ただし、オプションで、Dynamic Media 画像サーバーを特定の仕様や要件に合うように設定することで、インストールを細かく調整することもできます。

**前提条件**: _前_ Dynamic Media Image Server を設定する場合は、Windows の VM にMicrosoft Visual C++ Libraries のインストールが含まれていることを確認します。 Dynamic Media 画像サーバーを実行するには、このライブラリが必要です。[ここから Microsoft Visual C++ 2010 再頒布可能パッケージ（x64）をダウンロード](https://www.microsoft.com/ja-jp/download/details.aspx?id=26999)できます。

**Dynamic Media Image Server を設定するには**:

1. AEMの左上隅にあるをタップします。 **[!UICONTROL Adobe Experience Manager]** グローバルナビゲーションコンソールにアクセスするには、 **[!UICONTROL ツール/操作/ Web コンソール]**.
1. の **[!UICONTROL Adobe Experience Manager Web コンソール設定]** ページ、タップ **[!UICONTROL OSGi/設定]** :AEM内で現在実行中のすべてのバンドルを一覧表示します。

   Dynamic Media 配信サーバーは、リスト内の次の名前の下にあります。

   * **[!UICONTROL Adobe CQ Scene7 ImageServer]**
   * **[!UICONTROL Adobe CQ Scene7 PlatformServer]**

1. バンドルのリストで、の右側に表示されます。 **[!UICONTROL Adobe CQ Scene7 ImageServer]**、 **[!UICONTROL 編集]** アイコン
1. 内 **[!UICONTROL Adobe CQ Scene7 ImageServer]** ダイアログボックスで、次の設定値を設定します。

   >[!NOTE]
   ほとんどの場合、デフォルト値を変更する必要はありません。ただし、デフォルト値を変更した場合、変更を有効にするには、バンドルを再起動する必要があります。

<table> 
 <tbody> 
  <tr> 
   <td><strong>プロパティ</strong></td> 
   <td><strong>デフォルト値</strong></td> 
   <td><strong>説明</strong></td> 
  </tr> 
  <tr> 
   <td>TcpPort.name</td> 
   <td><code><em>empty</em></code></td> 
   <td>ImageServer プロセスとの通信に使用するポート番号。デフォルトでは、空きのポートが自動的に検出されます。</td> 
  </tr> 
  <tr> 
   <td>AllowRemoteAccess.name</td> 
   <td><code><em>empty</em></code></td> 
   <td><p>Image Server プロセスへのリモートアクセスを許可または拒否します。false の場合、Image Server はローカルホストでのみリッスンします。</p> <p>ローカルホストを指すデフォルトの Externalizer 設定では、特定の VM インスタンスの実際のドメインまたは IP アドレスを指定する必要があります。この理由は、localhost が VM の親システムを指している可能性があるためです。</p> <p>VM のドメインまたは IP アドレスには、自身を解決できるようにホストファイルのエントリを含む必要がある場合があります。</p> </td> 
  </tr> 
  <tr> 
   <td>MaxRenderRgnPixels</td> 
   <td>16 MPixels</td> 
   <td>レンダリングされる最大サイズ（メガピクセル単位）。</td> 
  </tr> 
  <tr> 
   <td>MaxMessageSize</td> 
   <td>16 MBytes</td> 
   <td>配信されるメッセージの最大サイズ（メガバイト単位）。</td> 
  </tr> 
  <tr> 
   <td>RandomAccessUrlTimeout</td> 
   <td>20</td> 
   <td>JCR がタイル範囲リクエストに応答するまで ImageServer が待つ時間（秒）を表すタイムアウト値。</td> 
  </tr> 
  <tr> 
   <td>WorkerThreads</td> 
   <td>10</td> 
   <td>ワーカースレッドの数。</td> 
  </tr> 
 </tbody> 
</table>

1. 「**[!UICONTROL 保存]**」をタップします。
1. バンドルのリストで、の右側に表示されます。 **[!UICONTROL Adobe CQ Scene7 PlatformServer]**、 **[!UICONTROL 編集]** アイコン
1. 内 **[!UICONTROL Adobe CQ Scene7 PlatformServer]** ダイアログボックスで、次の既定値のオプションを設定します。

   >[!NOTE]
   Dynamic Media Image Server は、独自のディスクキャッシュを使用して応答をキャッシュします。AEM HTTP キャッシュと Dispacher を使用して Dynamic Media 画像サーバーからの応答をキャッシュすることはできません。

   | **プロパティ** | **デフォルト値** | **説明** |
   |---|---|---|
   | **[!UICONTROL Cache enabled]** | チェック | 応答キャッシュを有効にするかどうかを指定します。。 |
   | **[!UICONTROL Cache roots]** | キャッシュ | 応答キャッシュフォルダーへの 1 つ以上のパス。相対パスは、内部の s7imaging バンドルフォルダーを基準として解決されます。 |
   | **[!UICONTROL Cache Max Size]** | 200000000 | 応答キャッシュの最大サイズ（バイト単位）。 |
   | **[!UICONTROL Cache Max Entries]** | 100000 | キャッシュ内で許可されるエントリの最大数。 |

### デフォルトのマニフェスト設定 {#default-manifest-settings}

デフォルトのマニフェストでは、Dynamic Media配信応答の生成に使用するデフォルトを設定できます。画質 (JPEGの画質、解像度、再サンプリングモード )、キャッシュ（有効期限）を微調整し、大きすぎる画像のレンダリングを防ぐことができます (defaultpix、defaultthumbpix、maxpix)。

デフォルトのマニフェスト設定の場所は、**[!UICONTROL Adobe CQ Scene7 PlatformServer]** バンドルの **[!UICONTROL Catalog root]** のデフォルト値から取得されます。デフォルトでは、この値は次のパス ( **[!UICONTROL ツール/一般/CRXDE Lite]**:

`/conf/global/settings/dam/dm/imageserver/`

![configimageserverxdelite](assets/configimageservercrxdelite.png)

プロパティの値を変更するには、下の表に記載されているように、新しい値を入力します。

デフォルトのマニフェストの変更が完了したら、ページの左上隅にあるをタップします。 **[!UICONTROL すべて保存]**.

必ず **[!UICONTROL アクセス制御]** タブ ( **[!UICONTROL プロパティ]** 」タブをクリックし、アクセス制御権限を `jcr:read` 全員および dynamic-media-replication ユーザー向けの機能を提供します。

![configimageservercrxdeleteaccesscontroltab](assets/configimageservercrxdeliteaccesscontroltab.png)

マニフェスト設定とデフォルト値の表：

<table> 
 <tbody> 
  <tr> 
   <td><strong>プロパティ</strong></td> 
   <td><strong>デフォルト値</strong></td> 
   <td><strong>説明</strong></td> 
  </tr> 
  <tr> 
   <td>bkgcolor</td> 
   <td>FFFFFF</td> 
   <td><p>デフォルトの背景色。返信画像の中で、実際の画像データが含まれない部分を塗りつぶすために使用する RGB 値。</p> <p>画像サービス API の <a href="https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-bkgcolor.html?lang=ja">BkgColor</a> も参照してください。</p> </td> 
  </tr> 
  <tr> 
   <td>defaultpix</td> 
   <td>300,300</td> 
   <td><p>デフォルトの表示サイズ.サーバーによって、返信画像がこの幅と高さ以内になるように制限されます（要求で wid=、hei= または scl= を使用して表示サイズが明示的に指定されていない場合）。</p> <p>幅と高さ（ピクセル単位）。 0 以上の 2 つの整数で指定し、コンマで区切ります。一方または両方の値を 0 に設定すると、制限なしのまま維持されます。ネストされたリクエストまたは埋め込まれたリクエストに対しては適用されません。</p> <p>画像サービス API の <a href="https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-defaultpix.html?lang=ja">DefaultPix</a> も参照してください。</p> <p>ただし、通常はビューアプリセットまたは画像プリセットを使用してアセットを配信します。DefaultPix はビューアプリセットや画像プリセットを使用していないアセットに適用されます。</p> </td> 
  </tr> 
  <tr> 
   <td>defaultthumbpix</td> 
   <td>100,100</td> 
   <td><p>デフォルトのサムネールのサイズ。サムネール要求（req=tmb）の attribute::DefaultPix の代わりに使用されます。</p> <p>サーバーによって、返信画像がこの幅と高さ以内になるように制限されます（サムネール要求（req=tmb）で wid=、hei= または scl= を使用して表示サイズが明示的に指定されていない場合）。</p> <p>幅と高さ（ピクセル単位）。 0 以上の 2 つの整数で指定し、コンマで区切ります。一方または両方の値を 0 に設定すると、制限なしのまま維持されます。 </p> <p>ネストされたリクエストまたは埋め込まれたリクエストに対しては適用されません。</p> <p>画像サービス API の <a href="https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-defaultthumbpix.html?lang=ja">DefaultThumbPix</a> も参照してください。 </p> </td> 
  </tr> 
  <tr> 
   <td>expiration</td> 
   <td>36000000</td> 
   <td><p>デフォルトのクライアントキャッシュの存続時間。特定のカタログレコードに有効な catalog::Expiration 値が含まれていない場合のデフォルトの有効期限間隔を指定します。</p> <p>0 以上の実数。返信データが生成されてから有効期限が切れるまでの時間数（ミリ秒単位）。0 に設定すると、常に返信画像が即座に有効期限切れになります。実質的に、クライアントキャッシュが無効になります。デフォルトでは、この時間は 10 時間に設定されています。つまり、新しい画像が公開される場合に、古い画像がユーザーのキャッシュから削除されるまで 10 時間かかります。すぐにキャッシュをクリアする必要がある場合は、カスタマーサポートにお問い合わせください。</p> <p>画像サービス API の<a href="https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-expiration.html?lang=ja">有効期限</a>も参照してください。</p> </td> 
  </tr> 
  <tr> 
   <td>jpegquality</td> 
   <td>80</td> 
   <td><p>デフォルトの JPEG エンコード属性。JPEG 返信画像のデフォルト属性を指定します。</p> <p>整数とフラグ（コンマ区切り）。1 つ目の値は 1 ～ 100 の範囲で、画質を定義します。2 つ目の値は、通常動作の場合は 0 を指定し、JPEG エンコーダーによって通常導入される RGB 色度ダウンサンプリングを無効にするには 1 を指定します。</p> <p>画像サービス API の <a href="https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-jpegquality.html?lang=ja">JpegQuality</a> も参照してください。</p> </td> 
  </tr> 
  <tr> 
   <td>maxpix</td> 
   <td>2000,2000</td> 
   <td><p>返信画像のサイズ制限.クライアントに返される返信画像の最大の幅と高さ。</p> <p>返信画像の幅または高さが attribute::MaxPix よりも大きくなるリクエストに対しては、サーバーからエラーが返ります。</p> <p>画像サービス API の <a href="https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-maxpix.html?lang=ja">MaxPix</a> も参照してください。</p> </td> 
  </tr> 
  <tr> 
   <td>resmode</td> 
   <td>SHARP2</td> 
   <td><p>デフォルトの再サンプリングモード.画像データの拡大縮小に使用するデフォルトの再サンプリングおよび補間属性を指定します。</p> <p>resMode= が要求内で指定されていない場合に使用されます。</p> <p>使用できる値は BILIN、BICUB、SHARP2 です。</p> <p>列挙。bilin の場合は 2、bicub の場合は 3、sharp2 補間モードの場合は 4 に設定します。最も良い結果を得るには sharp2 を使用してください。</p> <p>画像サービス API の <a href="https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-is-cat-resmode.html?lang=ja">ResMode</a> も参照してください。</p> </td> 
  </tr> 
  <tr> 
   <td>resolution</td> 
   <td>72</td> 
   <td><p>デフォルトのオブジェクト解像度。特定のカタログレコードに有効な catalog::Resolution 値が含まれていない場合のデフォルトのオブジェクト解像度を指定します。</p> <p>0 以上の実数。通常は ppi（インチあたりピクセル数）で表しますが、ppm（メートルあたりピクセル数）などの他の単位の場合もあります。</p> <p>画像サービス API の<a href="https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-resolution.html">解像度</a>も参照してください。</p> </td> 
  </tr> 
  <tr> 
   <td>thumbnailtime</td> 
   <td>1%,11%,21%,31%,41%,51%,61%,71%,81%,91%</td> 
   <td>これらの値は、ビデオ再生時間のスナップショットを表し、<a href="https://encoding.com/">encoding.com</a> に渡されます。詳しくは、<a href="/help/assets/video.md#about-video-thumbnails">ビデオサムネールについて</a>を参照してください。</td> 
  </tr> 
 </tbody> 
</table>

## Dynamic Media カラーマネジメントの設定 {#configuring-dynamic-media-color-management}

Dynamic Media カラーマネジメントを使用すると、プレビュー用にアセットをカラー補正できます。

カラー補正により、取り込まれたアセットは、生成された Pyramid TIFF レンディションにカラースペース（RGB、CMYK、グレー）および埋め込みカラープロファイルを維持します。動的レンディションを要求した場合、画像の色は、ターゲットのカラースペースに補正されます。JCR の Dynamic Media 公開設定に出力カラープロファイルを設定します。

Adobe カラーマネジメントは ICC プロファイルを使用しています。このプロファイルの形式は、International Color Consortium（ICC）によって定義されています。

Dynamic Media カラーマネジメントを設定して、CMYK、RGB またはグレー出力を使用する画像プリセットを設定できます。[画像プリセットの設定](managing-image-presets.md)を参照してください。

高度な事例では、手動設定の **[!UICONTROL icc=]** 修飾子を使用して出力カラープロファイルを明示的に選択することもあります。

* **[!UICONTROL icc]** - [出力カラープロファイル。](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-icc.html?lang=ja)

* **[!UICONTROL iccEmbed]** - [カラープロファイルを埋め込みます。](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-iccembed.html?lang=ja)

>[!NOTE]
標準のAdobeカラープロファイルセットは、 [ソフトウェア配布の機能パック12445](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/featurepack/cq-6.3.0-featurepack-12445) インストール済み すべての機能パックおよびサービスパックは、[ソフトウェア配布](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)から入手できます。機能パック 12445 は、Adobe カラープロファイルを提供します。

### 機能パック12445をインストール中 {#installing-feature-pack}

Dynamic Media のカラーマネジメント機能を使用するには、機能パック 12445 をインストールする必要があります。

**機能パック12445をインストールするには**:

1. に移動します。 [ソフトウェア配布](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html) およびダウンロード `cq-6.3.0-featurepack-12445`.

   [!DNL Adobe Experience Manager] でのパッケージの使用について詳しくは、[パッケージの操作方法](/help/sites-administering/package-manager.md)を参照してください。

1. 機能パックをインストールします。

### デフォルトカラープロファイルの設定 {#configuring-the-default-color-profiles}

機能パックをインストールしたら、適切なデフォルトカラープロファイルを設定して、RGB または CMYK 画像データを要求する際のカラー補正を有効にする必要があります。

**デフォルトのカラープロファイルを設定するには**:

1. **[!UICONTROL ツール／一般／CRXDE Lite]**&#x200B;で、デフォルトの Adobe カラープロファイルを含む`/conf/global/settings/dam/dm/imageserver/configuration/settings`に移動します。

   ![chlimage_1-514](assets/chlimage_1-514.png)

1. スクロールして **[!UICONTROL プロパティ]** 次の表に示すように、「 」タブを使用して、プロパティ名、タイプ、値を手動で入力します。 値を入力した後、 **[!UICONTROL 追加]** その後 **[!UICONTROL すべて保存]** 値を保存します。

   カラー補正プロパティは、**[!UICONTROL カラー補正プロパティ]**&#x200B;の表に記載しています。カラー補正プロパティに割り当てることができる値は、**[!UICONTROL カラープロファイル]**&#x200B;の表に記載しています。

   例えば、**[!UICONTROL 名前]**&#x200B;に`iccprofilecmyk`を追加し、**[!UICONTROL タイプ]** `String`を選択してから、**[!UICONTROL 値]**&#x200B;として`WebCoated`を追加してください。タップ **[!UICONTROL 追加]**&#x200B;を、 **[!UICONTROL すべて保存]** 値を保存します。

   ![chlimage_1-515](assets/chlimage_1-515.png)

   **カラー補正プロパティの表**

   <table> 
    <tbody> 
      <tr> 
      <td><strong>プロパティ</strong></td> 
      <td><strong>タイプ</strong></td> 
      <td><strong>デフォルト</strong></td> 
      <td><strong>説明</strong></td> 
      </tr> 
      <tr> 
      <td><a href="https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccprofilergb.html">icprofilergb</a></td> 
      <td>文字列</td> 
      <td>&lt;空白&gt;</td> 
      <td>デフォルトの RGB カラープロファイルの名前。</td> 
      </tr> 
      <tr> 
      <td><a href="https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccprofilecmyk.html?lang=ja">iccprofilemyk</a></td> 
      <td>文字列</td> 
      <td>&lt;空白&gt;</td> 
      <td>デフォルトの CMYK カラープロファイルの名前。</td> 
      </tr> 
      <tr> 
      <td><a href="https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccprofilegray.html?lang=ja">icprofilegray</a></td> 
      <td>文字列</td> 
      <td>&lt;空白&gt;</td> 
      <td>デフォルトのグレーカラープロファイルの名前。</td> 
      </tr> 
      <tr> 
      <td><a href="https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccprofilegray.html?lang=ja">iccprofilesrcgb</a></td> 
      <td>文字列</td> 
      <td>&lt;empty&gt;</td> 
      <td>カラープロファイルが埋め込まれていない RGB 画像に使用される、デフォルトの RGB カラープロファイルの名前</td> 
      </tr> 
      <tr> 
      <td><a href="https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccprofilesrccmyk.html">iccprofilesrccmyk</a></td> 
      <td>文字列</td> 
      <td>&lt;empty&gt;</td> 
      <td>カラープロファイルが埋め込まれていない CMYK 画像に使用される、デフォルトの CMYK カラープロファイルの名前。</td> 
      </tr> 
      <tr> 
      <td><a href="https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccprofilesrcgray.html">iccprofilesrcgray</a></td> 
      <td>文字列</td> 
      <td>&lt;empty&gt;</td> 
      <td>カラープロファイルが埋め込まれていない CMYK 画像に使用されるデフォルトのグレーカラープロファイルの名前。</td> 
      </tr> 
      <tr> 
      <td><a href="https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccblackpointcompensation.html">iccblackpointcompensation</a></td> 
      <td>ブール演算式</td> 
      <td>True</td> 
      <td>カラー補正中に黒点補正を行うかどうかを指定します。 アドビでは、これをオンにすることをお勧めします。</td> 
      </tr> 
      <tr> 
      <td><a href="https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccdither.html">iccdither</a></td> 
      <td>ブール演算式</td> 
      <td>False</td> 
      <td>カラー補正中にディザリングを行うかどうかを指定します。</td> 
      </tr> 
      <tr> 
      <td><a href="https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/c-is-home.html?lang=ja">icrenderintent</a></td> 
      <td>文字列</td> 
      <td>相対的</td> 
      <td><p>レンダリングインテントを指定します。指定できる値は、<strong>知覚的、相対的、彩度、絶対的です。</strong><i></i>アドビでは、デフォルトとして<strong>相対的</strong><i></i>を推奨します。</p> </td> 
      </tr> 
    </tbody> 
    </table>

   >[!NOTE]
   プロパティ名は、大文字と小文字が区別され、すべて小文字にする必要があります。

   **カラープロファイルの表**

   次のカラープロファイルがインストールされます。

   <table> 
    <tbody> 
      <tr> 
      <th><p>名前</p> </th> 
      <th><p>カラースペース</p> </th> 
      <th><p>説明</p> </th> 
      </tr> 
      <tr> 
      <td>AdobeRGB</td> 
      <td>RGB</td> 
      <td>Adobe RGB (1998)</td> 
      </tr> 
      <tr> 
      <td>AppleRGB</td> 
      <td>RGB</td> 
      <td>Apple RGB</td> 
      </tr> 
      <tr> 
      <td>CIERGB</td> 
      <td>RGB</td> 
      <td>CIE RGB</td> 
      </tr> 
      <tr> 
      <td>CoatedFogra27</td> 
      <td>CMYK</td> 
      <td>Coated FOGRA27（ISO 12647-2:2004）</td> 
      </tr> 
      <tr> 
      <td>CoatedFogra39</td> 
      <td>CMYK</td> 
      <td>Coated FOGRA39（ISO 12647-2:2004）</td> 
      </tr> 
      <tr> 
      <td>CoatedGraCol</td> 
      <td>CMYK</td> 
      <td>Coated GRACoL 2006（ISO 12647-2:2004）</td> 
      </tr> 
      <tr> 
      <td>ColorMatchRGB</td> 
      <td>RGB</td> 
      <td>ColorMatch RGB</td> 
      </tr> 
      <tr> 
      <td>EuropeISOCoated</td> 
      <td>CMYK</td> 
      <td>Europe ISO Coated FOGRA27</td> 
      </tr> 
      <tr> 
      <td>EuroscaleCoated</td> 
      <td>CMYK</td> 
      <td>Euroscale Coated v2</td> 
      </tr> 
      <tr> 
      <td>EuroscaleUncoated</td> 
      <td>CMYK</td> 
      <td>Euroscale Uncoated v2</td> 
      </tr> 
      <tr> 
      <td>JapanColorCoated</td> 
      <td>CMYK</td> 
      <td>Japan Color 2001 Coated</td> 
      </tr> 
      <tr> 
      <td>JapanColorNewspaper</td> 
      <td>CMYK</td> 
      <td>Japan Color 2002 Newspaper</td> 
      </tr> 
      <tr> 
      <td>JapanColorUncoated</td> 
      <td>CMYK</td> 
      <td>Japan Color 2001 Uncoated</td> 
      </tr> 
      <tr> 
      <td>JapanColorWebCoated</td> 
      <td>CMYK</td> 
      <td>Japan Color 2003 Web Coated</td> 
      </tr> 
      <tr> 
      <td>JapanWebCoated</td> 
      <td>CMYK</td> 
      <td>Japan Web Coated（Ad）</td> 
      </tr> 
      <tr> 
      <td>NewsprintSNAP2007</td> 
      <td>CMYK</td> 
      <td>US Newsprint（SNAP 2007）</td> 
      </tr> 
      <tr> 
      <td>NTSC</td> 
      <td>RGB</td> 
      <td>NTSC（1953）</td> 
      </tr> 
      <tr> 
      <td>PAL</td> 
      <td>RGB</td> 
      <td>PAL／SECAM</td> 
      </tr> 
      <tr> 
      <td>ProPhoto</td> 
      <td>RGB</td> 
      <td>ProPhoto RGB</td> 
      </tr> 
      <tr> 
      <td>PS4Default</td> 
      <td>CMYK</td> 
      <td>Photoshop 4 Default CMYK</td> 
      </tr> 
      <tr> 
      <td>PS5Default</td> 
      <td>CMYK</td> 
      <td>Photoshop 5 Default CMYK</td> 
      </tr> 
      <tr> 
      <td>SheetfedCoated</td> 
      <td>CMYK</td> 
      <td>U.S. Sheetfed Coated v2</td> 
      </tr> 
      <tr> 
      <td>SheetfedUncoated</td> 
      <td>CMYK</td> 
      <td>U.S. Sheetfed Uncoated v2</td> 
      </tr> 
      <tr> 
      <td>SMPTE</td> 
      <td>RGB</td> 
      <td>SMPTE-C</td> 
      </tr> 
      <tr> 
      <td>sRGB</td> 
      <td>RGB</td> 
      <td>sRGB IEC61966-2.1</td> 
      </tr> 
      <tr> 
      <td>UncoatedFogra29</td> 
      <td>CMYK</td> 
      <td>Uncoated FOGRA29 (ISO 12647-2:2004)</td> 
      </tr> 
      <tr> 
      <td>WebCoated</td> 
      <td>CMYK</td> 
      <td>U.S. Web Coated (SWOP) v2</td> 
      </tr> 
      <tr> 
      <td>WebCoatedFogra28</td> 
      <td>CMYK</td> 
      <td>Web Coated FOGRA28 (ISO 12647-2:2004)</td> 
      </tr> 
      <tr> 
      <td>WebCoatedGrade3</td> 
      <td>CMYK</td> 
      <td>Web Coated SWOP 2006 Grade 3 Paper</td> 
      </tr> 
      <tr> 
      <td>WebCoatedGrade5</td> 
      <td>CMYK</td> 
      <td>Web Coated SWOP 2006 Grade 5 Paper</td> 
      </tr> 
      <tr> 
      <td>WebUncoated</td> 
      <td>CMYK</td> 
      <td>U.S. Web Uncoated v2</td> 
      </tr> 
      <tr> 
      <td>WideGamutRGB</td> 
      <td>RGB</td> 
      <td>Wide Gamut RGB</td> 
      </tr> 
    </tbody> 
    </table>

1. 「**[!UICONTROL すべて保存]**」をタップします。

例えば、 **[!UICONTROL icprofilergb]** から `sRGB`、および **[!UICONTROL iccprofilemyk]** から `WebCoated`. それには、次のようにします。

* RGB および CMYK 画像のカラー補正を有効にします。
* カラープロファイルを持たない RGB 画像は、`sRGB` カラースペースにあると見なされます。
* カラープロファイルを持たない CMYK 画像は、`WebCoated` カラースペースにあると見なされます。
* RGB 出力を返す動的レンディションは、RGB 出力を `sRGB` カラースペース内で返します。
* CMYK 出力を返す動的レンディションは、CMYK 出力を `WebCoated` カラースペース内で返します。

## アセットの配信 {#delivering-assets}

これまでのすべてのタスクが完了したら、アクティベートされた Dynamic Media アセットが、画像サービスやビデオサービスから配信されます。AEMでは、この機能は **[!UICONTROL 画像 URL をコピー]**, **[!UICONTROL ビューアの URL をコピー]**, **[!UICONTROL 埋め込みビューアコード]**、WCM 内

[Dynamic Media アセットの配信](delivering-dynamic-media-assets.md) を参照してください。

<table> 
 <tbody> 
  <tr> 
   <td><strong>実行する場合...</strong></td> 
   <td><strong>結果</strong></td> 
  </tr> 
  <tr> 
   <td>画像 URL をコピー</td> 
   <td><p>「URL をコピー」ダイアログボックスに、次のような URL が表示されます（URL はデモ専用です）。</p> <p><code>https://IMAGESERVICEPUBLISHNODE/is/image/content/dam/path/to/Image.jpg?$preset$</code></p> <p>ここで <code>IMAGESERVICEPUBLISHNODE</code> は画像サービスの URL を表します。</p> <p><a href="/help/assets/delivering-dynamic-media-assets.md">Dynamic Media アセットの配信</a>も参照してください。</p> </td> 
  </tr> 
  <tr> 
   <td>ビューア URL のコピー</td> 
   <td><p>「URL をコピー」ダイアログボックスに、次のような URL が表示されます（URL はデモ専用です）。</p> <p><code>https://PUBLISHNODE/etc/dam/viewers/s7viewers/html5/BasicZoomViewer.html?asset=/content/dam/path/to/Image.jpg&amp;config=/conf/global/settings/dam/dm/presets/viewer/Zoom_dark&amp;serverUrl=https://IMAGESERVICEPUBLISHNODE/is/image/&amp;contentRoot=%2F</code></p> <p><code>PUBLISHNODE</code> は通常の AEM パブリッシュノードを表し、<code>IMAGESERVICEPUBLISHNODE</code> は画像サービスの URL を表します。</p> <p><a href="/help/assets/delivering-dynamic-media-assets.md">Dynamic Media アセットの配信</a>も参照してください。</p> </td> 
  </tr> 
  <tr> 
   <td>ビューアの埋め込みコードのコピー</td> 
   <td><p>「埋め込みコードをコピー」ダイアログボックスに、次のようなコードスニペットが表示されます（コード例はデモ専用です）。</p> <p><code class="code">&lt;style type="text/css"&gt;
       #s7basiczoom_div.s7basiczoomviewer{
       width:100%;
       height:auto;
       }
       &lt;/style&gt;
       &lt;script
       type="text/javascript" src="https://PUBLISHNODE/etc/dam/viewers/s7viewers/html5/js/BasicZoomViewer.js"&gt;&lt;/script&gt;
       &lt;div id="s7basiczoom_div"&gt;&lt;/div&gt;
       &lt;script type="text/javascript"&gt;
       var s7basiczoomviewer = new s7viewers.BasicZoomViewer({
       "containerId" : "s7basiczoom_div",
       "params" : {
       "serverurl" : "https://IMAGESERVICEPUBLISHNODE/is/image/",
       "contenturl" : "https://PUBLISHNODE/",
       "config" : "/conf/global/settings/dam/dm/presets/viewer/Zoom_dark",
       "asset" : "/content/dam/path/to/Image.jpg" }
       }).init();
       &lt;/script&gt;</code></p> <p><code>PUBLISHNODE</code> は通常の AEM パブリッシュノードを表し、<code>IMAGESERVICEPUBLISHNODE</code> は画像サービスの URL を表します。</p> <p><a href="/help/assets/delivering-dynamic-media-assets.md">Dynamic Media アセットの配信</a>も参照してください。</p> </td> 
  </tr> 
 </tbody> 
</table>

### WCM の Dynamic Media コンポーネントとインタラクティブメディアコンポーネント {#wcm-dynamic-media-and-interactive-media-components}

Dynamic Media コンポーネントとインタラクティブメディアコンポーネントを参照する WCM ページは、配信サービスを参照します。
