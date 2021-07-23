---
title: AEM AssetsとAdobe InDesign Serverの統合
description: AEM Assets と InDesign Server を統合する方法を学習します。
contentOwner: AG
feature: 公開
role: Admin
exl-id: d80562f7-071c-460a-9c68-65f48d36fbd9
source-git-commit: fc725206728e238ab9da1fb30cee8fb407257b62
workflow-type: tm+mt
source-wordcount: '1703'
ht-degree: 60%

---

# AEM AssetsとAdobe InDesign Serverの統合 {#integrating-aem-assets-with-indesign-server}

Adobe Experience Manager (AEM) Assets では、次のものが使用されます。

* プロキシ：特定の処理タスクのロードを分配するために使用します。プロキシとは、プロキシワーカーと通信して特定のタスクを実行し、他の AEM インスタンスと通信して結果を送信する AEM インスタンスです。
* プロキシワーカー：特定のタスクを定義し管理するために使用します。

これらは、様々な作業をカバーできます。例えば、Adobe InDesign Serverを使用してファイルを処理します。

Adobe InDesign で作成したファイルを AEM Assets に完全にアップロードするために、プロキシが使用されます。このプロキシはプロキシワーカーを使用して Adobe InDesign Server と通信します。Adobe InDesign Server ではメタデータを抽出し、AEM Assets 用の様々なレンディションを生成するための[スクリプト](https://www.adobe.com/jp/devnet/indesign/documentation.html#idscripting)が実行されます。プロキシワーカーは、クラウド構成での InDesign Server と AEM インスタンスとの双方向通信を実現します。

>[!NOTE]
>
>Adobe InDesign は次の 2 製品で構成されます。
>
>* [InDesign](https://www.adobe.com/jp/products/indesign.html)\
   >  印刷やデジタル配信のためのページレイアウトをデザインできます。
   >
   >
* [InDesign Server](https://www.adobe.com/jp/products/indesignserver.html)\
   >  このエンジンを使用すれば、InDesign での作成物に基づいてドキュメントをプログラムによって自動生成できます。このエンジンは、[ExtendScript](https://www.adobe.com/jp/devnet/scripting.html) エンジンへのインターフェイスを提供するサービスとして動作します。\
   >  スクリプトは、JavaScriptに似たExtendScriptで記述されます。 Indesign のスクリプトについて詳しくは、[https://www.adobe.com/jp/devnet/indesign/documentation.html#idscripting](https://www.adobe.com/devnet/indesign/documentation.html#idscripting) を参照してください。

>



## 抽出の仕組み {#how-the-extraction-works}

InDesign ServerをAEM Assetsと統合して、InDesign( `.indd` )で作成されたファイルのアップロード、レンディションの生成、 *すべての*&#x200B;メディアの抽出（ビデオなど）およびアセットとしての保存をおこなうことができます。

>[!NOTE]
>
>以前のバージョンの AEM では XMP とサムネールを抽出できましたが、現在はすべてのメディアを抽出できるようになりました。

1. `.indd`ファイルをAEM Assetsにアップロードします。
1. フレームワークにより、コマンドスクリプトが SOAP（Simple Object Access Protocol）経由で InDesign Server に送信されます。

   このコマンドスクリプトは、次のことを実行します。

   * `.indd`ファイルを取得します。
   * InDesign Server コマンドを実行します。

      * 構造、テキストおよびすべてのメディアファイルが抽出されます。
      * PDF と JPG のレンディションが生成されます。
      * HTML と IDML のレンディションが生成されます。
   * 生成されたファイルを AEM Assets に送り返します。

   >[!NOTE]
   >
   >IDML は、InDesign ファイル内のすべての要素をレンダリングする XML ベースの形式です。**[Zip](https://www.techterms.com/definition/zip) 圧縮を使用した圧縮パッケージとして保存されます。
   >
   >詳しくは、 [Adobe InDesignのデータ交換形式INXおよびIDML](https://www.peachpit.com/articles/article.aspx?p=1381880&amp;seqNum=8)を参照してください。

   >[!CAUTION]
   >
   >InDesign Serverがインストールされていない場合や設定されていない場合でも、`.indd`ファイルをAEMにアップロードできます。 ただし、生成されるレンディションは`png`と`jpeg`に制限され、`html`、`idml`またはページレンディションを生成することはできません。

1. 抽出およびレンダリング生成後：

   * 構造が `cq:Page`（レンディションタイプ）に複製されます。
   * 抽出されたテキストとファイルが AEM Assets に保存されます。
   * すべてのレンディションが AEM Assets のアセット自体に保存されます。

## InDesign Server と AEM の統合 {#integrating-the-indesign-server-with-aem}

プロキシの設定の後に、InDesign Server を AEM Assets と連携させて使用するには、次の手順を実行する必要があります。

1. [InDesign Server をインストールします](#installing-the-indesign-server)。
1. 必要に応じて、[AEM Assets ワークフロー](#configuring-the-aem-assets-workflow)を設定します。

   これは、デフォルト値がインスタンスに適さない場合にのみ必要です。

1. [InDesign Server のプロキシワーカー](#configuring-the-proxy-worker-for-indesign-server)を設定します。

### InDesign Server のインストール {#installing-the-indesign-server}

InDesign Server をインストールして AEM と連携して使用を開始するには：

1. Adobe InDesign Server をダウンロードしてインストールします。

   >[!NOTE]
   >
   >InDesign Server（CS6 以降）。

1. 必要に応じて、InDesign Server インスタンスの設定をカスタマイズできます。

1. コマンドラインから、サーバーを起動します。

   `<*ids-installation-dir*>/InDesignServer.com -port 8080`

   SOAP プラグインがポート 8080 でリスンする状態でサーバーが起動されます。すべてのログメッセージと出力がコマンドウィンドウに直接書き込まれます。

   >[!NOTE]
   >
   >ファイルに出力メッセージを保存してリダイレクトを使用する場合は、例えば Windows の場合は次のように実行します。
   >
   >`<ids-installation-dir>/InDesignServer.com -port 8080 > ~/temp/INDD-logfile.txt 2>&1`

### AEM Assets ワークフローの設定 {#configuring-the-aem-assets-workflow}

AEM Assetsには、InDesign用に特別にいくつかのプロセスステップを持つ事前設定済みのワークフロー「**DAMアセットの更新**」があります。

* [メディア抽出](#media-extraction)
* [ページ抽出](#page-extraction)

このワークフローは、様々なオーサーインスタンスで設定に合わせて調整できるデフォルト値を使用して設定されます（これは標準のワークフローなので、詳しくは、[ワークフローの編集](/help/sites-developing/workflows-models.md#configuring-a-workflow-step)を参照してください）。 デフォルト値（SOAPポートを含む）を使用している場合は、設定は不要です。

設定後、通常の方法のいずれかによって InDesign ファイルを AEM Assets にアップロードすると、そのアセットを処理して各種レンディションを準備するのに必要となるワークフローが実行されます。`.indd` ファイルを AEM Assets にアップロードし、IDS で作成された各種レンディションが `<*your_asset*>.indd/Renditions` の下にあることを確認して、設定をテストしてください。

#### メディア抽出 {#media-extraction}

この手順では、`.indd`ファイルからのメディアの抽出を制御します。

カスタマイズするには、**[!UICONTROL メディア抽出]**&#x200B;ステップの「**[!UICONTROL 引数]**」タブを編集します。

![メディア抽出の引数とスクリプトパス](assets/media_extraction_arguments_scripts.png)

メディア抽出の引数とスクリプトパス

* **ExtendScriptライブラリ**:これは、他のスクリプトに必要な単純なhttp get/postメソッドライブラリです。

* **スクリプトの拡張**:ここで様々なスクリプトの組み合わせを指定できます。InDesign サーバーで独自のスクリプトを実行する場合は、`/apps/settings/dam/indesign/scripts` にスクリプトを保存します。

   InDesignスクリプトについて詳しくは、[https://www.adobe.com/devnet/indesign/documentation.html#idscripting](https://www.adobe.com/devnet/indesign/documentation.html#idscripting)を参照してください。

>[!CAUTION]
>
>ExtendScript ライブラリは変更しないでください。ライブラリは、Slingとの通信に必要なHTTP機能を提供します。 この設定では、Adobe InDesign Serverに送信してそこで使用するライブラリを指定します。

メディア抽出ワークフローステップで実行される`ThumbnailExport.jsx`スクリプトにより、サムネールのレンディションがJPG形式で生成されます。 このレンディションはサムネールを処理ワークフローステップによって使用され、AEM で要求される静的レンディションを生成します。

サムネールを処理ワークフローステップは、異なるサイズの静的レンディションを生成するように設定できます。デフォルトの設定は AEM Assets UI によって要求されるので、削除しないでください。最後に、画像プレビューレンディションを削除ワークフローステップで不要になった .jpg 形式のサムネールレンディションが削除されます。

#### ページ抽出 {#page-extraction}

抽出された要素から AEM ページを作成します。抽出ハンドラーが、レンディション（現時点では HTML または IDML）からデータを抽出するために使用されます。このデータを元に、PageBuilder を使用してページが作成されます。

カスタマイズするには、**ページ抽出**&#x200B;ステップの「**[!UICONTROL 引数]**」タブを編集します。

![chlimage_1-289](assets/chlimage_1-289.png)

* **ページ抽出ハンドラー**:ドロップダウンリストから、使用するハンドラーを選択します。抽出ハンドラーは、関連する `RenditionPicker`（`ExtractionHandler` API を参照）によって選択された特定のレンディションに対して動作します。デフォルトでは、IDML書き出し抽出ハンドラーを使用できます。 MediaExtractステップで生成された`IDML`レンディションで動作します。

* **ページ名**:生成されるページに割り当てる名前を指定します。空白の場合、名前は「page」（「page」が既に存在する場合は派生形）になります。

* **ページタイトル**:生成されるページに割り当てるタイトルを指定します。

* **ページルートパス**:生成されるページのルート位置へのパス。空白の場合、アセットのレンディションを保持しているノードが使用されます。

* **ページテンプレート**:ページの生成時に使用するテンプレート。

* **ページデザイン**:ページの生成時に使用するページデザイン。

### InDesign Server のプロキシワーカーの設定 {#configuring-the-proxy-worker-for-indesign-server}

>[!NOTE]
>
>ワーカーは、プロキシインスタンス上にあります。

1. 「ツール」コンソールの左側のウィンドウで、「**[!UICONTROL クラウドサービス設定]**」を展開します。次に、「**[!UICONTROL クラウドプロキシ設定]**」を展開します。

1. 「**[!UICONTROL IDS ワーカー]**」をダブルクリックし、開いて設定します。

1. 「**[!UICONTROL 編集]**」をクリックして設定ダイアログを開き、必要な設定を定義します。

   ![proxy_idsworkerconfig](assets/proxy_idsworkerconfig.png)

   * **IDSプール**:InDesign Serverとの通信に使用するSOAPエンドポイント。必要な項目の追加、削除および並べ替えを行うことができます。

1. 「**[!UICONTROL OK]**」をクリックして保存します。

### Day CQ Link Externalizer の設定  {#configuring-day-cq-link-externalizer}

InDesign ServerとAEMが異なるホスト上にある場合、またはこれらのアプリケーションの一方または両方がデフォルトのInDesign Serverで動作しない場合は、**Day CQ Link Externalizer**&#x200B;を設定して、ポートのホスト名、ポートおよびコンテンツのパスを設定します。

1. `https://[AEM_server]:[port]/system/console/configMgr` の URL で Configuration Manager にアクセスします。
1. 設定&#x200B;**[!UICONTROL Day CQ Link Externalizer]**&#x200B;を探します。 **[!UICONTROL 編集]**&#x200B;をクリックして開きます。
1. Link Externalizerの設定は、[!DNL Experience Manager]デプロイメントと[!DNL InDesign Server]の絶対URLを作成するのに役立ちます。 **[!UICONTROL Domains]**&#x200B;フィールドを使用して、[!DNL Adobe InDesign Server]のホスト名とコンテキストパスを指定します。 画面に表示される手順に従ってください。「**[!UICONTROL 保存]**」をクリックします。

   ![Link Externalizerの設定](assets/link-externalizer-config.png)

### ジョブの並列ジョブ処理のInDesign Server {#enabling-parallel-job-processing-for-indesign-server}

IDS の並列ジョブ処理を有効にすることができます。

まず、InDesign Server が処理できる並列ジョブの最大数（`x`）を決定する必要があります。

* 単一のマルチプロセッサーマシンでは、InDesign Server が処理できる並列ジョブの最大数（x）は、IDS を実行するプロセッサー数から 1 を減算した数です。
* 複数のマシンで IDS を実行する場合は、すべてのマシンで使用可能なプロセッサーの総数を把握して、そこからマシン総数を減算する必要があります。

IDS 並列ジョブ数を設定するには：

1. Felix Console の「**[!UICONTROL Configurations]**」タブを開きます。次に URL の例を挙げます。

   `http://localhost:4502/system/console/configMgr`

1. 次の場所で IDS 処理キューを選択します。

   `Apache Sling Job Queue Configuration`

1. 次のように設定します。

   * **[!UICONTROL Type]** - `Parallel`
   * **[!UICONTROL Maximum Parallel Jobs]** - `<*x*>`（上で計算した値）

1. これらの変更を保存します。
1. AdobeCS6以降のマルチセッションサポートを有効にするには、`com.day.cq.dam.ids.impl.IDSJobProcessor.name configuration`の下にある`enable.multisession.name`チェックボックスをオンにします。
1. IDSワーカー設定](#configuring-the-proxy-worker-for-indesign-server)にSOAPエンドポイントを追加して、`*x*>`個のIDSワーカーの[プールを作成します。

   複数のマシンで InDesign Server を実行している場合は、マシンあたりのプロセッサー数から 1 を減算した数の SOAP エンドポイントを各マシンに追加します。

   >[!NOTE]
   >
   >ワーカーのプールを操作する場合、IDSワーカーのブロックリストを有効にできます。
   >
   >それには、`com.day.cq.dam.ids.impl.IDSJobProcessor.name` 設定の下にある「enable.retry.name」チェックボックスをオンにします。これにより、IDS ジョブ再試行が有効になります。
   >
   >また、`com.day.cq.dam.ids.impl.IDSPoolImpl.name``max.errors.to.blacklist` 設定の下のパラメーターに正の値を設定します。このパラメーターは、IDS をジョブハンドラーリストから除外するまでのジョブ再試行回数を指定します。
   >
   >デフォルトでは、設定可能な(`retry.interval.to.whitelist.name`)時間（分）が経過すると、IDSワーカーが再検証されます。 ワーカーがオンラインである場合は、ブロックリストから削除されます。

<!-- TBD: Make updates to configurations for allow and block list after product updates are done. See CQ-4298427.
-->

## Adobe InDesign Server 10.0以降のサポートの有効化 {#enabling-support-for-indesign-server-or-higher}

InDesign Server 10.0 以降では、次の手順を実行してマルチセッションサポートを有効化します。

1. [!DNL Assets]インスタンス`https://[aem_server]:[port]/system/console/configMgr`からConfiguration Managerを開きます。
1. 設定 `com.day.cq.dam.ids.impl.IDSJobProcessor.name` を編集します。
1. **[!UICONTROL ids.cc.enable]**&#x200B;オプションを選択し、「**[!UICONTROL 保存]**」をクリックします。

>[!NOTE]
>
>[!DNL Assets]との[!DNL InDesign Server]統合の場合、統合に必要なセッションサポート機能はシングルコアシステムではサポートされないので、マルチコアプロセッサを使用してください。

## Experience Manager資格情報の設定 {#configure-aem-credentials}

Adobe InDesignサーバーとの統合を中断することなく、AEMインスタンスからInDesignサーバーにアクセスするためのデフォルトの管理者資格情報（ユーザー名とパスワード）を変更できます。

1. `/etc/cloudservices/proxy.html` にアクセスします。
1. ダイアログで、新しいユーザー名とパスワードを指定します。
1. この資格情報を保存します。
