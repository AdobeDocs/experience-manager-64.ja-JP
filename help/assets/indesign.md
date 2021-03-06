---
title: 統合 [!DNL Experience Manager] Adobe InDesign Serverを使用したアセット
description: の統合方法を説明します [!DNL Experience Manager] InDesign Server
contentOwner: AG
feature: Publishing
role: Admin
exl-id: d80562f7-071c-460a-9c68-65f48d36fbd9
source-git-commit: cc9b6d147a93688e5f96620d50f8fc8b002e2d0d
workflow-type: tm+mt
source-wordcount: '1674'
ht-degree: 46%

---

# Assets とAdobe InDesign Serverの統合 {#integrating-aem-assets-with-indesign-server}

Adobe Experience Manager Assets では、次のものを使用します。

* プロキシ：特定の処理タスクのロードを分配するために使用します。プロキシは [!DNL Experience Manager] プロキシワーカーと通信して特定のタスクを実行し、他のタスクを実行するインスタンス [!DNL Experience Manager] インスタンスを使用して結果を配信します。
* プロキシワーカー：特定のタスクを定義し管理するために使用します。

これらは様々な作業をカバーできます。例えば、Adobe InDesign Serverを使用してファイルを処理する場合です。

ファイルをに完全にアップロードするには [!DNL Experience Manager] プロキシとしてAdobe InDesignで作成したアセットが使用されます。 このプロキシはプロキシワーカーを使用して Adobe InDesign Server と通信します。Adobe InDesign Server ではメタデータを抽出し、 Assets 用の様々なレンディションを生成するための[スクリプト](https://www.adobe.com/jp/devnet/indesign/documentation.html#idscripting)が実行されます。[!DNL Experience Manager]プロキシワーカーは、InDesign Serverと [!DNL Experience Manager] インスタンスがクラウド設定に含まれています。

>[!NOTE]
>
>Adobe InDesign は次の 2 製品で構成されます。
>
>* [InDesign](https://www.adobe.com/jp/products/indesign.html)\
   >  印刷やデジタル配信のためのページレイアウトをデザインできます。
>
>* [InDesign Server](https://www.adobe.com/jp/products/indesignserver.html)\
   >  このエンジンを使用すれば、InDesign での作成物に基づいてドキュメントをプログラムによって自動生成できます。このエンジンは、[ExtendScript](https://www.adobe.com/jp/devnet/scripting.html) エンジンへのインターフェイスを提供するサービスとして動作します。\
   >  スクリプトは、JavaScript に似たExtendScriptで記述されます。 Adobe InDesignスクリプトについて詳しくは、 [https://www.adobe.com/devnet/indesign/documentation.html#idscripting](https://www.adobe.com/devnet/indesign/documentation.html#idscripting).

>


## 抽出の仕組み {#how-the-extraction-works}

InDesign Serverは、 [!DNL Experience Manager] アセットをInDesign( `.indd`) をアップロードし、レンディションを生成して、 *すべて* 抽出されてアセットとして保存されたメディア（例：ビデオ）:

>[!NOTE]
>
>以前のバージョンの [!DNL Experience Manager] はXMPとサムネールを抽出でき、現在はすべてのメディアを抽出できます。

1. 次をアップロード： `.indd` ～に提出する [!DNL Experience Manager] アセット。
1. フレームワークにより、コマンドスクリプトが SOAP（Simple Object Access Protocol）経由で InDesign Server に送信されます。

   このコマンドスクリプトは、次のことを実行します。

   * の取得 `.indd` ファイル。
   * InDesign Server コマンドを実行します。

      * 構造、テキストおよびすべてのメディアファイルが抽出されます。
      * PDF と JPG のレンディションが生成されます。
      * HTML と IDML のレンディションが生成されます。
   * 結果のファイルをに投稿します。 [!DNL Experience Manager] アセット。

   >[!NOTE]
   >
   >IDML は、InDesign ファイル内のすべての要素をレンダリングする XML ベースの形式です。**[Zip](https://www.techterms.com/definition/zip) 圧縮を使用した圧縮パッケージとして保存されます。
   >
   >詳しくは、 [Adobe InDesign INX および IDML 形式](https://www.peachpit.com/articles/article.aspx?p=1381880&amp;seqNum=8) を参照してください。

   >[!CAUTION]
   >
   >InDesign Serverがインストールされていない場合や設定されていない場合でも、 `.indd` ～に押し込む [!DNL Experience Manager]. ただし、生成されるレンディションは次の条件に制限されます。 `png` および `jpeg`を生成できない場合、 `html`, `idml` またはページのレンディション。

1. 抽出およびレンダリング生成後：

   * 構造が `cq:Page`（レンディションタイプ）に複製されます。
   * 抽出したテキストとファイルは、 [!DNL Experience Manager] アセット。
   * すべてのレンディションは、 [!DNL Experience Manager] アセット内のアセット。

## InDesign Server と の統合[!DNL Experience Manager] {#integrating-the-indesign-server-with-aem}

で使用するInDesign Serverを統合するには [!DNL Experience Manager] Assets と、プロキシを設定した後は、次の操作が必要です。

1. [InDesign Server をインストールします](#installing-the-indesign-server)。
1. 必要に応じて、 [設定 [!DNL Experience Manager] Assets ワークフロー](#configuring-the-aem-assets-workflow).

   これは、デフォルト値がインスタンスに適さない場合にのみ必要です。

1. [InDesign Server のプロキシワーカー](#configuring-the-proxy-worker-for-indesign-server)を設定します。

### InDesign Server のインストール {#installing-the-indesign-server}

で使用するInDesign Serverをインストールして開始するには [!DNL Experience Manager]:

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

### の設定 [!DNL Experience Manager] Assets ワークフロー {#configuring-the-aem-assets-workflow}

[!DNL Experience Manager] Assets には事前設定済みのワークフローがあります **DAM アセットの更新**( 特にInDesign用の複数のプロセスステップを持つ )

* [メディア抽出](#media-extraction)
* [ページ抽出](#page-extraction)

このワークフローは、様々なオーサーインスタンス上で設定に合わせて調整できるデフォルト値が設定されています ( これは標準ワークフローなので、詳しくは、 [ワークフローの編集](/help/sites-developing/workflows-models.md#configuring-a-workflow-step)) をクリックします。 デフォルト値（SOAP ポートを含む）を使用する場合は、設定は不要です。

設定後、にInDesignファイルをアップロード [!DNL Experience Manager] アセットは（通常の方法のいずれかによって）アセットを処理し、様々なレンディションを準備するために必要なワークフローをトリガーします。 `.indd`[!DNL Experience Manager] ファイルを Assets にアップロードし、IDS で作成された各種レンディションが  の下にあることを確認して、設定をテストしてください。`<*your_asset*>.indd/Renditions`

#### メディア抽出 {#media-extraction}

この手順では、 `.indd` ファイル。

カスタマイズするには、**[!UICONTROL メディア抽出]**&#x200B;ステップの「**[!UICONTROL 引数]**」タブを編集します。

![メディア抽出の引数とスクリプトパス](assets/media_extraction_arguments_scripts.png)

メディア抽出の引数とスクリプトパス

* **ExtendScript Library**:これは、他のスクリプトに必要な単純な http get/post メソッドライブラリです。

* **スクリプトを拡張**:ここで様々なスクリプトの組み合わせを指定できます。 InDesign サーバーで独自のスクリプトを実行する場合は、`/apps/settings/dam/indesign/scripts` にスクリプトを保存します。

   InDesign・スクリプトの詳細は、 [https://www.adobe.com/devnet/indesign/documentation.html#idscripting](https://www.adobe.com/devnet/indesign/documentation.html#idscripting).

>[!CAUTION]
>
>ExtendScript ライブラリは変更しないでください。ライブラリは、Sling との通信に必要な HTTP 機能を提供します。 この設定では、Adobe InDesign Serverに送信してそこで使用するライブラリを指定します。

この `ThumbnailExport.jsx` メディア抽出ワークフローステップで実行されるスクリプトにより、サムネールのレンディションがJPG形式で生成されます。 このレンディションは、サムネールを処理ワークフローステップで使用され、 [!DNL Experience Manager].

サムネールを処理ワークフローステップは、異なるサイズの静的レンディションを生成するように設定できます。デフォルト値は、 [!DNL Experience Manager] Assets UI 最後に、画像プレビューレンディションを削除ワークフローステップで不要になった .jpg 形式のサムネールレンディションが削除されます。

#### ページ抽出 {#page-extraction}

これにより、 [!DNL Experience Manager] ページを抽出します。 抽出ハンドラーが、レンディション（現時点では HTML または IDML）からデータを抽出するために使用されます。このデータを元に、PageBuilder を使用してページが作成されます。

カスタマイズするには、**ページ抽出**&#x200B;ステップの「**[!UICONTROL 引数]**」タブを編集します。

![chlimage_1-289](assets/chlimage_1-289.png)

* **ページ抽出ハンドラー**:ドロップダウンリストから、使用するハンドラーを選択します。 抽出ハンドラーは、関連する `RenditionPicker`（`ExtractionHandler` API を参照）によって選択された特定のレンディションに対して動作します。デフォルトでは、IDML 書き出し抽出ハンドラーを使用できます。 これは、 `IDML` レンディションを MediaExtract ステップで生成しました。

* **ページ名**:結果ページに割り当てる名前を指定します。空白の場合、名前は「page」（「page」が既に存在する場合は派生形）になります。

* **ページタイトル**:結果ページに割り当てるタイトルを指定します。

* **ページルートパス**:結果ページのルート位置へのパス。 空白のままにした場合、アセットのレンディションを保持しているノードが使用されます。

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

   * **IDS プール**:InDesign Serverとの通信に使用する SOAP エンドポイント。必要に応じて、項目の追加、削除および並べ替えをおこなうことができます。

1. 「**[!UICONTROL OK]**」をクリックして保存します。

### Day CQ Link Externalizer の設定  {#configuring-day-cq-link-externalizer}

InDesign Serverと [!DNL Experience Manager] は別のホスト上にあるか、これらのアプリケーションの一方または両方がデフォルトポートで動作していません。を構成してください。 **Day CQ Link Externalizer** をクリックして、InDesign Serverのホスト名、ポート、およびコンテンツパスを設定します。

1. `https://[AEM_server]:[port]/system/console/configMgr` の URL で Configuration Manager にアクセスします。
1. 設定の場所 **[!UICONTROL Day CQ Link Externalizer]**. クリック **[!UICONTROL 編集]** をクリックして開きます。
1. Link Externalizer の設定は、 [!DNL Experience Manager] デプロイメントと [!DNL InDesign Server]. 用途 **[!UICONTROL ドメイン]** ホスト名と [!DNL Adobe InDesign Server]. 画面に表示される手順に従ってください。「**[!UICONTROL 保存]**」をクリックします。

   ![Link externalizer 設定](assets/link-externalizer-config.png)

### InDesign Serverの並列ジョブ処理の有効化 {#enabling-parallel-job-processing-for-indesign-server}

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
1. AdobeCS6 以降のマルチセッションサポートを有効にするには、 `enable.multisession.name` 下のチェックボックス `com.day.cq.dam.ids.impl.IDSJobProcessor.name configuration`.
1. の作成 [プール &lt; `*x*>` IDS ワーカー設定に SOAP エンドポイントを追加することによる IDS ワーカー](#configuring-the-proxy-worker-for-indesign-server).

   複数のマシンで InDesign Server を実行している場合は、マシンあたりのプロセッサー数から 1 を減算した数の SOAP エンドポイントを各マシンに追加します。

   >[!NOTE]
   >
   >ワーカーのプールを使用する場合、IDS ワーカーのブロックリストを有効にできます。
   >
   >それには、`com.day.cq.dam.ids.impl.IDSJobProcessor.name` 設定の下にある「enable.retry.name」チェックボックスをオンにします。これにより、IDS ジョブ再試行が有効になります。
   >
   >また、`com.day.cq.dam.ids.impl.IDSPoolImpl.name``max.errors.to.blacklist` 設定の下のパラメーターに正の値を設定します。このパラメーターは、IDS をジョブハンドラーリストから除外するまでのジョブ再試行回数を指定します。
   >
   >デフォルトでは、設定可能な (`retry.interval.to.whitelist.name`) 時間（分単位）、IDS ワーカーの再検証。 ワーカーがオンラインである場合は、ブロックリストから削除されます。

<!-- TBD: Make updates to configurations for allow and block list after product updates are done. See CQ-4298427.
-->

## Adobe InDesign Server 10.0 以降のサポートを有効にする {#enabling-support-for-indesign-server-or-higher}

InDesign Server 10.0 以降では、次の手順を実行してマルチセッションサポートを有効化します。

1. 次の場所から Configuration Manager を開きます。 [!DNL Assets] インスタンス `https://[aem_server]:[port]/system/console/configMgr`.
1. 設定 `com.day.cq.dam.ids.impl.IDSJobProcessor.name` を編集します。
1. 選択 **[!UICONTROL ids.cc.enable]** オプションを選択し、をクリックします。 **[!UICONTROL 保存]**.

>[!NOTE]
>
>の場合 [!DNL InDesign Server] ～との統合 [!DNL Assets]統合に必要なセッションサポート機能はシングルコアシステムではサポートされていないので、マルチコアプロセッサーを使用してください。

## Experience Manager資格情報の設定 {#configure-aem-credentials}

デフォルトの管理者資格情報（ユーザー名とパスワード）を変更して、 [!DNL Experience Manager] Adobe InDesignサーバーとの統合に支障をきたさずにインスタンスを作成できます。

1. `/etc/cloudservices/proxy.html` にアクセスします。
1. ダイアログで、新しいユーザー名とパスワードを指定します。
1. この資格情報を保存します。
