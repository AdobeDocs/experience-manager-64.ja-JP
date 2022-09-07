---
title: Dynamic Media - Scene7 モードの設定
description: Dynamic Media - Scene7 モードの設定方法を学習します。
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.4/ASSETS
topic-tags: dynamic-media
content-type: reference
exl-id: b0f0c6e4-77c8-40db-a9f4-699d1a633571
feature: Configuration,Scene7 Mode
role: Admin,User,Developer
source-git-commit: a045c70f8cbfa03295c4fcbfbb2df1831c3f7292
workflow-type: tm+mt
source-wordcount: '5619'
ht-degree: 66%

---

# Dynamic Media - Scene7 モードの設定 {#configuring-dynamic-media-scene-mode}

開発、ステージング、実稼動など、異なる環境用にAdobe Experience Managerをセットアップして使用する場合は、各環境用にDynamic MediaCloud Servicesを設定する必要があります。

## Dynamic Media - Scene7 モードのアーキテクチャ図 {#architecture-diagram-of-dynamic-media-scene-mode}

以下のアーキテクチャ図に Dynamic Media - Scene7 モードの仕組みを示します。

新しいアーキテクチャでは、Experience Managerはプライマリアセットを担当し、Dynamic Mediaと同期してアセットの処理と公開をおこないます。

1. プライマリアセットがExperience Managerにアップロードされると、Dynamic Mediaにレプリケートされます。 その時点で、Dynamic Media は、ビデオエンコーディングおよび画像の動的バリアントなど、すべてのアセットの処理とレンディションの生成を扱います。
1. レンディションが生成されると、Experience Manager から、リモート Dynamic Media レンディションに安全にアクセスしてプレビューできます（バイナリが Experience Manager インスタンスに送り返されることはありません）。
1. コンテンツを公開および承認する準備ができると、Dynamic Media サービスがトリガーされ、コンテンツが配信サーバーにプッシュされて、CDN にコンテンツがキャッシュされます。

![chlimage_1](assets/chlimage_1.png)

## Scene7 モードの Dynamic Media の有効化 {#enabling-dynamic-media-in-scene-mode}

[Dynamic Media](https://www.adobe.com/marketing-cloud/enterprise-content-management/dynamic-media.html) はデフォルトで無効になっています。Dynamic Media の機能を活用するには、Dynamic Media を有効にする必要があります。

>[!WARNING]
>
>Dynamic Media - Scene7 モードは *Experience Manager オーサーインスタンス専用*&#x200B;です。そのために、 `runmode=dynamicmedia_scene7`Experience Managerオーサーインスタンスで、 *not* Experience Managerパブリッシュインスタンス

Dynamic Mediaを有効にするには、 `dynamicmedia_scene7` ターミナルウィンドウで次のように入力して、コマンドラインから実行モードを指定します（使用するポートの例は 4502）。

```shell
java -Xms4096m -Xmx4096m -Doak.queryLimitInMemory=500000 -Doak.queryLimitReads=500000 -jar cq-quickstart-6.4.0.jar -gui -r author,dynamicmedia_scene7 -p 4502
```

## （オプション）Dynamic Media のプリセットおよび設定を 6.3 から 6.4 にダウンタイムなしで移行 {#optional-migrating-dynamic-media-presets-and-configurations-from-to-zero-downtime}

Experience ManagerDynamic Mediaを 6.3 から 6.4 にアップグレードする場合（ダウンタイムなしのデプロイメント機能を含む）、次の curl コマンドを実行して、すべてのプリセットと設定を `/etc` から `/conf` CRXDE Lite

>[!NOTE]
>
>Experience Managerインスタンスを互換モードで実行する場合（つまり、互換性パッケージがインストールされている場合）、これらのコマンドを実行する必要はありません。

カスタムプリセットと設定を次の場所から移行するには： `/etc` から `/conf`、次の Linux® curl コマンドを実行します。

`curl -u admin:admin http://localhost:4502/libs/settings/dam/dm/presets.migratedmcontent.json`

互換パッケージの有無を問わず、すべてのアップグレードについて、次のコマンドを実行することにより標準提供ビューアプリセットをコピーできます。

`curl -u admin:admin http://localhost:4502/libs/settings/dam/dm/presets/viewer.pushviewerpresets`

## （オプション）一括アセット移行用の機能パック18912のインストール {#installing-feature-pack}

機能パック 18912 を使用すると、FTP 経由でアセットを一括取り込みするか、Experience Manager で Dynamic Media - ハイブリッドモードまたは Dynamic Media Classic から Dynamic Media - Scene7 モードにアセットを移行できます。これは、Adobe Professional Services から入手できます。

詳しくは、 [一括アセット移行用の機能パック18912をインストールしています](bulk-ingest-migrate.md) を参照してください。

## Dynamic Media クラウドサービスの設定 {#configuring-dynamic-media-cloud-services}

パスワードを変更してから、Dynamic MediaCloud Servicesを設定します。 Dynamic Media資格情報を含むプロビジョニング電子メールを受け取ったら、 [サインイン](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/intro/dynamic-media-classic-desktop-app.html?lang=ja#system-requirements-dmc-app) をDynamic Media Classicデスクトップアプリケーションにアクセスして、パスワードを変更します。 プロビジョニング電子メールで提供されたパスワードは、システムが生成したもので、一時的なパスワードです。Dynamic Media Cloud Service が正しい資格情報で設定されるように、パスワードを更新することが重要です。

>[!NOTE]
>
>デフォルトでは、Cloud Servicesの設定パスは `/content/dam`. その他の設定パスは、Dynamic Media - Scene7モードではサポートされません。

**Dynamic Media クラウドサービスを設定するには：**

1. Experience Managerオーサーインスタンスで、Experience Managerのロゴをタップしてグローバルナビゲーションコンソールにアクセスし、ツールアイコンをタップしてから、 **[!UICONTROL Cloud Services]** > **[!UICONTROL Dynamic Media Configuration]**.
1. Dynamic Media設定ブラウザーページの左側のパネルで、をタップします。 **[!UICONTROL global]** とタップします。 **[!UICONTROL 作成]**. 左側のフォルダーアイコンをタップまたは選択しないでください。 [!UICONTROL global].
1. の [!UICONTROL Dynamic Media設定を作成] ページ、タイトル、Dynamic Mediaアカウントの電子メールアドレス、パスワードを入力します。 地域を選択します。 この情報は、プロビジョニングメールのAdobeによって提供されます。 メールを受け取っていない場合は、アドビカスタマーサポートにお問い合せください。

   タップ **[!UICONTROL Dynamic Mediaに接続]**.

   >[!NOTE]
   >
   >Dynamic Media資格情報を含むプロビジョニング電子メールを受け取ったら、 [Dynamic Media Classicデスクトップアプリケーション](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html?lang=ja#getting-started)」をクリックし、会社のアカウントにサインインして、パスワードを変更します。 プロビジョニング電子メールで提供されたパスワードは、システムが生成したもので、一時的なパスワードです。Dynamic MediaCloud Serviceが正しい資格情報で設定されるように、パスワードを更新することが重要です。

1. 接続に成功すると、次も設定できます。

   * **[!UICONTROL 会社]** - Dynamic Media アカウントの名前です。

      >[!IMPORTANT]
      >
      >Experience ManagerのインスタンスでサポートされるDynamic MediaCloud Servicesは 1 つだけです。複数の設定を追加しないでください。 1 つのExperience Managerインスタンス上の複数のDynamic Media設定 *not* Adobeでサポートまたは推奨。<!-- CQDOC-19579 and CQDOC-19612 -->
   * **[!UICONTROL 会社のルートフォルダのパス]**  — 会社のルートフォルダーパス。
   * **[!UICONTROL アセットを公開]** - 「**[!UICONTROL 即時]**」オプションは、アセットがアップロードされると、システムによってアセットが取り込まれ、URL／埋め込みがすぐに提供されることを意味します。アセットを公開するためにユーザーが操作する必要はありません。オプション **[!UICONTROL アクティベーション時]** とは、URL/埋め込みリンクが提供される前に、最初にアセットを明示的に公開する必要があることを意味します。
   * **[!UICONTROL プレビューサーバーを保護]** - セキュアなレンディションプレビューサーバーへの URL パスを指定できます。つまり、レンディションが生成されると、Experience Manager は、リモート Dynamic Media レンディションに安全にアクセスしてプレビューできます（バイナリが Experience Manager インスタンスに送り返されることはありません）。


      自社のサーバーまたは特別なサーバーを使用する特別な設定がない限り、Adobeではデフォルト設定を使用することをお勧めします。
   >[!NOTE]
   >
   >DMS7 ではバージョン管理はサポートされていません。また、遅延アクティベーションは、「Dynamic Media 設定を編集」ページの&#x200B;**[!UICONTROL アセットを公開]**が&#x200B;**[!UICONTROL アクティベーション時]**&#x200B;に設定されている場合にのみ、アセットが最初にアクティベートされるまでの間に限って適用されます。
   >
   >アセットがアクティベートされるとすぐに、すべての更新が S7 配信にライブ公開されます。

   ![dynamicmediaconfiguration2updated](assets/dynamicmediaconfiguration2updated.png)

1. 「**[!UICONTROL 保存]**」をタップします。
1. Dynamic Mediaコンテンツを公開する前に安全にプレビューするには、Experience Managerオーサーインスタンスを「許可リスト」して、Dynamic Mediaに接続する必要があります。

   * [Dynamic Media Classic デスクトップアプリケーション](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)を開き、アカウントにログインします。資格情報とログオンの詳細は、プロビジョニング時にアドビから付与されたものです。この情報をお持ちでない場合は、テクニカルサポートにお問い合わせください。
   * ページ右上付近のナビゲーションバーで、をタップします。 **[!UICONTROL 設定]** > **[!UICONTROL アプリケーション設定]** > **[!UICONTROL 公開設定]** > **[!UICONTROL Image Server]**.
   * Image Server 公開ページの「公開コンテキスト」ドロップダウンリストで、「**[!UICONTROL 画像サービングをテスト]**」を選択します。
   * 「クライアントアドレスフィルター」で、**[!UICONTROL 「追加」]**&#x200B;をタップします。
   * アドレスを有効（オン）にするには、チェックボックスをオンにします。Dispatcher IP ではなく、Experience Managerオーサーインスタンスの IP アドレスを入力します。
   * 「**[!UICONTROL 保存]**」をタップします。

これで基本設定が完了しました。Dynamic Media - Scene7 モードを使用する準備が整いました。

設定をさらにカスタマイズする場合は、[（オプション）Dynamic Media - Scene7 モードでの詳細設定](#optional-configuring-advanced-settings-in-dynamic-media-scene-mode)で示す任意のタスクをオプションで実行できます。

## （オプション）Dynamic Media - Scene7 モードでの詳細設定 {#optional-configuring-advanced-settings-in-dynamic-media-scene-mode}

Dynamic Media - Scene7 モードのセットアップと設定をさらにカスタマイズしたり、パフォーマンスを最適化したりする場合は、次のオプションタスクを 1 つまたは複数実行できます。

* [（オプション）Dynamic Media - Scene7 モードのセットアップと設定](#optional-setup-and-configuration-of-dynamic-media-scene-mode-settings-p)

* [（オプション）Dynamic Media - Scene7 モードのパフォーマンスの調整](#optional-tuning-the-performance-of-dynamic-media-scene-mode)
* [（オプション）レプリケーション用のアセットのフィルタリング](#optional-filtering-assets-for-replication)

### （オプション）Dynamic Media - Scene7 モードのセットアップと設定</p> {#optional-setup-and-configuration-of-dynamic-media-scene-mode-settings-p}

次の場所にいるとき： **dynamicmedia_scene7** 実行モードでは、Dynamic Media Classicユーザーインターフェイスを使用してDynamic Media設定を変更できます。

上記のタスクの一部では、[Dynamic Media Classic デスクトップアプリケーション](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)を開いて、アカウントにログインする必要があります。

セットアップおよび設定のタスクは次のとおりです。

* [Image Server の公開設定](#publishing-setup-for-image-server)
* [アプリケーションの一般設定の指定](#configuring-application-general-settings)
* [カラーマネジメントの設定](#configuring-color-management)
* [サポートされる形式の MIME タイプの編集](#editing-mime-types-for-supported-formats)
* [サポートされていない形式のカスタム MIME タイプの追加](#adding-mime-types-for-unsupported-formats)
* [画像セットおよびスピンセットを自動生成するためのバッチセットプリセットの作成](#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets)

#### Image Server の公開設定 {#publishing-setup-for-image-server}

公開設定は、アセットがデフォルトで Dynamic Media からどのように配信されるかを決定します。設定が指定されていない場合、Dynamic Media は、公開設定で定義されたデフォルト設定に従ってアセットを配信します。例えば、解像度属性が含まれていない画像を配信するように要求した場合、画像は初期設定のオブジェクト解像度設定で配信されます。

公開設定を設定するには：Dynamic Media Classicでをタップします。 **[!UICONTROL 設定]** > **[!UICONTROL アプリケーション設定]** > **[!UICONTROL 公開設定]** > **[!UICONTROL Image Server]**.

Image Server 画面では、画像を配信するためのデフォルト設定を指定します。各設定の説明については、ユーザインターフェイスを参照してください。

* **[!UICONTROL 要求属性]** - これらの設定は、サーバーから配信できる画像を制限します。
* **[!UICONTROL 初期設定の要求属性]** - これらの設定は、画像のデフォルトの表示に関係します。
* **[!UICONTROL 共通のサムネール属性]** - これらの設定は、サムネール画像のデフォルトの表示に関係します。
* **[!UICONTROL カタログフィールドの初期設定]** - これらの設定は、画像の解像度とデフォルトのサムネールの種類に関係します。
* **[!UICONTROL カラーマネジメント属性]** - これらの設定は、使用する ICC カラープロファイルを決定します。
* **[!UICONTROL 互換性の属性]** - この設定により、後方互換性の確保のためにバージョン 3.6 の場合と同様に、テキストレイヤーの先頭と末尾の段落が処理されます。
* **[!UICONTROL ローカリゼーションサポート]** - これらの設定によって、複数のロケール属性を管理します。また、ロケールマップ文字列を指定することもできます。これにより、ビューアのツールチップで使用する言語を指定できます。ローカリゼーションサポートの設定について詳しくは、 [ローカリゼーションサポートを実装する際の重要な考慮事項](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/setup/publish-setup.html#image-server).

#### アプリケーションの一般設定の指定 {#configuring-application-general-settings}

次の手順で [!UICONTROL アプリケーションの一般設定] ページで、Dynamic Media Classicグローバルナビゲーションバーの **[!UICONTROL 設定]** > **[!UICONTROL アプリケーション設定]** > **[!UICONTROL 一般設定]**.

**[!UICONTROL サーバー -]**アカウントのプロビジョニング時に、会社に割り当てられているサーバーが Dynamic Media によって自動的に提供されます。これらのサーバーは、web サイトとアプリケーションの URL 文字列を生成するのに使用されます。これらの URL 呼び出しは、アカウントに固有です。Experience Manager のサポートから明示的に指示されない限り、サーバー名は変更しないでください。


**[!UICONTROL 画像を上書き]** - Dynamic Media は、2 つのファイルが同じ名前を持つことを許可しません。各項目の URL ID（ファイル名から拡張子を取り除いた部分）は一意である必要があります。これらのオプションは、置き換えるアセットのアップロード方法、つまり元のアセットを置き換えるか、重複させるかを指定します。重複するアセット名には「-1」が付けられます（例えば、chair.tif は chair-1.tif に変更されます）。これらのオプションは、元のアセットとは別のフォルダーにアップロードされるアセットや、元のアセットと異なるファイル名拡張子（JPG、TIF、PNG など）を持つアセットに影響を与えます。

* **[!UICONTROL 現在のフォルダーでベース名と拡張子が同じファイルを上書き]** - このオプションは最も厳格な置換規則です。置き換え画像を元の画像と同じフォルダーにアップロードし、置き換え画像と元の画像のファイル名拡張子が同じになっている必要があります。これらの要件が満たされない場合は、重複が作成されます。

>[!NOTE]
>
>Experience Managerとの一貫性を維持するには、 **[!UICONTROL 現在のフォルダでベース名と拡張子が同じファイルを上書き]**.

* **[!UICONTROL 任意のフォルダでベース名と拡張子が同じファイルを上書き]**  — 置き換える画像のファイル名拡張子が元の画像と同じである必要があります ( 例： `chair.jpg` 置き換え `chair.jpg` およびでない `chair.tif`) をクリックします。 ただし、置換画像を、元の画像と別のフォルダーにアップロードできます。更新された画像は新しいフォルダーにあり、元の場所のファイルはなくなります。
* **[!UICONTROL 任意のフォルダーでベース名が同じファイルを上書き]** - このオプションは最も包括的な置換規則です。置換画像を、元の画像と別のフォルダーにアップロードでき、ファイル名拡張子が異なるファイルをアップロードして、元のファイルと置換することができます。元のファイルが別のフォルダーにある場合、置換画像は、アップロード先の新しいフォルダーに存在します。

**[!UICONTROL 初期設定のカラープロファイル]** - 詳細については、[カラーマネジメントの設定](#configuring-color-management)を参照してください。

>[!NOTE]
>
>デフォルトでは、アセットの詳細表示で「**[!UICONTROL レンディション]**」を選択した場合 15 個のレンディションが表示され、「**[!UICONTROL ビューア]**」を選択した場合 15 個のビューアプリセットが表示されます。この制限は増やすことができます。詳しくは、 [表示される画像プリセット数の増加](managing-image-presets.md#increasing-or-decreasing-the-number-of-image-presets-that-display) または [表示されるビューアプリセットの数の増減](managing-viewer-presets.md#increasing-the-number-of-viewer-presets-that-display).

#### カラーマネジメントの設定 {#configuring-color-management}

Dynamic Media カラーマネジメントを使用すると、アセットをカラー補正できます。カラー補正により、取り込まれたアセットは、カラースペース（RGB、CMYK、グレー）および埋め込みカラープロファイルを維持します。動的レンディションを要求した場合、画像の色は、CMYK、RGB またはグレー出力を使用するターゲットのカラースペースに補正されます。[画像プリセットの設定](managing-image-presets.md)を参照してください。

**画像を要求する際にカラー補正を有効にするためのデフォルトのカラープロパティを設定するには：**

1. [Dynamic Media Classic デスクトップアプリケーション](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)を開き、プロビジョニング時に提供された資格情報を使用してアカウントにログインします。に移動します。 **[!UICONTROL 設定]** > **[!UICONTROL アプリケーション設定]**.
1. 「**[!UICONTROL 公開設定]**」領域を展開して、「**[!UICONTROL Image Server]**」を選択します。パブリッシュインスタンスのデフォルトを設定する際に、「**[!UICONTROL 公開コンテキスト]**」を「**[!UICONTROL 画像サービング]**」に設定します。
1. 変更が必要なプロパティまでスクロールします。例えば、 **[!UICONTROL カラーマネジメント属性]** 領域

   次のカラー補正プロパティを設定できます。

   * [!UICONTROL CMYK のデフォルトカラースペース] - デフォルトの CMYK カラープロファイルの名前
   * [!UICONTROL グレースケールのデフォルトカラースペース] - デフォルトのグレーカラープロファイルの名前
   * [!UICONTROL RGB のデフォルトカラースペース] - デフォルトの RGB カラープロファイルの名前
   * [!UICONTROL カラー変換レンダリングの方法] - レンダリング方法を指定します。指定できる値は次のとおりです。 `perceptual`, `relative` `colometric`, `saturation`、および `absolute colometric`. Adobeが推奨 `relative` をデフォルトとして使用します。

1. 「**[!UICONTROL 保存]**」をタップします。

例えば、**[!UICONTROL RGB の初期設定カラースペース]**&#x200B;を `sRGB` に、**[!UICONTROL CMYK の初期設定カラースペース]**&#x200B;を `WebCoated` に設定できます。

それには、次のようにします。

* RGB および CMYK 画像のカラー補正を有効にします。
* カラープロファイルを持たない RGB 画像は、`sRGB` カラースペースにあると見なされます。
* カラープロファイルを持たない CMYK 画像は、`WebCoated` カラースペースにあると見なされます。
* RGB出力を返す動的レンディションは、 `sRGB` カラースペース。
* CMYK 出力を返す動的レンディションは、CMYK 出力を `WebCoated` カラースペース。

#### サポートされる形式の MIME タイプの編集 {#editing-mime-types-for-supported-formats}

Dynamic Media によって処理されるアセットタイプを定義して、高度なアセット処理パラメーターをカスタマイズできます。例えば、アセット処理パラメーターを指定して次のことができます。

* Adobe PDF を eCatalog アセットに変換する。
* Adobe Photoshop ドキュメント（.PSD）をパーソナライズ用のバナーテンプレートアセットに変換する。
* Adobe Illustrator ファイル（.AI）または Adobe Photoshop Encapsulated PostScript® ファイル（.EPS）をラスタライズする。
* [ビデオプロファイル](/help/assets/video-profiles.md)および[イメージングプロファイル](/help/assets/image-profiles.md)は、それぞれ、ビデオおよび画像の処理を定義するのに使用できます。

[アセットのアップロード](managing-assets-touch-ui.md#uploading-assets)を参照してください。

**サポートされる形式の MIME タイプを編集するには：**

1. Experience Managerで、Experience Managerのロゴをタップしてグローバルナビゲーションコンソールにアクセスし、 **[!UICONTROL ツール]** （ハンマー）アイコンをクリックし、に移動します。 **[!UICONTROL 一般]** > **[!UICONTROL CRXDE Lite]**.
1. 左側のパネルで、次の場所に移動します。

   `/conf/global/settings/cloudconfigs/dmscene7/jcr:content/mimeTypes`

   ![mimetypes](assets/mimetypes.png)

1. 以下 `mimeTypes` フォルダーで、mime タイプを選択します。
1. CRXDE Lite ページの右側の下部で、次の操作をおこないます。

   * 「**[!UICONTROL 有効]**」フィールドをダブルクリックします。デフォルトでは、すべてのアセットの MIME タイプが有効になって（**[!UICONTROL true]** に設定されて）います。これは、処理に関してアセットが Dynamic Media に同期されることを意味します。このアセットの MIME タイプを処理から除外する場合、この設定を **[!UICONTROL false]** に変更します。
   * **[!UICONTROL jobParam]** をダブルクリックして、関連するテキストフィールドを開きます。特定の MIME タイプに使用可能な、許可されている処理パラメーター値のリストについては、[サポートされる MIME タイプ](assets-formats.md#supported-mime-types)を参照してください。

1. 次のいずれかの操作を行います。

   * 手順 3 ～ 4 を繰り返して、さらに MIME タイプを編集します。
   * メニューページのCRXDE Liteバーで、 **[!UICONTROL すべて保存]**.

1. ページの左上隅にあるをタップします。 **[!UICONTROL CRXDE Lite]** Experience Managerに戻る

#### サポートされていない形式のカスタム MIME タイプの追加 {#adding-custom-mime-types-for-unsupported-formats}

Experience Manager Assets でサポートされていない形式のカスタム MIME タイプを追加できます。CRXDE Liteに追加した新しいノードがExperience Managerによって削除されないようにするには、MIME タイプをの前に移動します。 **[!UICONTROL image_]** 有効な値は次の値に設定されます。 **[!UICONTROL false]**.

**サポートされていない形式のカスタム MIME タイプを追加するには:**

1. Experience Managerで、 **[!UICONTROL ツール]** > **[!UICONTROL 運用]** > **[!UICONTROL Web コンソール]**.

   ![Web コンソール](assets/2019-08-02_16-13-14.png)

1. 新しいブラウザータブが開き、**[!UICONTROL Adobe Experience Manager Web コンソール設定]**&#x200B;ページが表示されます。

   ![Experience ManagerWeb コンソールの設定](assets/2019-08-02_16-17-29.png)

1. ページ上で、名前まで下にスクロールします。 **[!UICONTROL Adobe CQ Scene7 Asset MIME type Service]**. 名前の右側にあるをタップします。 **[!UICONTROL 設定値の編集]** （鉛筆アイコン）を使用します。

   ![設定値を編集](assets/2019-08-02_16-44-56.png)

1. の **[!UICONTROL Adobe CQ Scene7 Asset MIME type Service]** ページ、任意のプラス記号アイコンをクリック `+`. 新しい MIME タイプを追加する場合にクリックする、プラス記号のテーブルの場所はすぐわかります。

   ![プラス記号アイコン](assets/2019-08-02_16-27-27.png)

1. 空のテキストフィールドに追加した `DWG=image/vnd.dwg` を入力します。

   この`DWG=image/vnd.dwg`の例は、説明の目的でのみ使用します。ここで追加する MIME タイプは、その他のサポートされていない形式でもかまいません。

   ![MIME タイプの追加の例](assets/2019-08-02_16-36-36.png)

1. ページの右下隅で、 **[!UICONTROL 保存]**.

   この時点で、Adobe Experience Manager web コンソール設定ページが開いているブラウザータブを閉じることができます。

1. Experience Manager のコンソールを開いているブラウザータブに戻ります。

1. Experience Managerで、 **[!UICONTROL ツール]** > **[!UICONTROL 一般]** > **[!UICONTROL CRXDE Lite]**.

   ![CRXDE Liteページ](assets/2019-08-02_16-55-41.png)

1. 左側のパネルで、次の場所に移動します。

   `conf/global/settings/cloudconfigs/dmscene7/jcr:content/mimeTypes`

1. MIME タイプをドラッグします `image_vnd.dwg` を直上にドロップします。 `image_` を設定します。

   ![MIME タイプをドラッグ](assets/CRXDELite_CQDOC-14627.png)

1. MIME タイプを使用 `image_vnd.dwg` ツリー内の **[!UICONTROL プロパティ]** タブ、 **[!UICONTROL 有効]** 行、 **[!UICONTROL 値]** 列見出しを使用する場合は、値をダブルクリックして **[!UICONTROL 値]** 」ドロップダウンリストから選択できます。

1. フィールドに `false` と入力します（または、ドロップダウンリストから「`false`」を選択します）。

   ![False 値](assets/2019-08-02_16_60_30.png)

1. CRXDE Lite ページの左上隅付近にある「**[!UICONTROL すべて保存]**」をクリックします。

#### 画像セットおよびスピンセットを自動生成するためのバッチセットプリセットの作成 {#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets}

アセットを Dynamic Media にアップロードしながら画像セットやスピンセットを自動作成するには、バッチセットプリセットを使用します。

最初に、アセットをセットにグループ化するための命名規則を定義します。次に、バッチセットプリセットを作成できます。このプリセットは、プリセット手法で定義された命名規則に一致する画像を使用してセットの構成方法を定義する、固有の名前を持つ自己完結した命令のセットです。

ファイルをアップロードする際に、Dynamic Media によって、アクティブプリセット内の定義された命名規則に一致するすべてのファイルのセットが自動的に作成されます。

**デフォルトの命名規則の設定**

任意のバッチセットプリセット手法で使用するデフォルトの命名規則を作成します。バッチセットプリセット定義で選択されたデフォルトの命名規則は、バッチセットの生成に会社で必要なものだけである可能性があります。 バッチセットプリセットは、定義するデフォルトの命名規則を使用するために作成されます。会社が定義するデフォルトの命名規則に例外がある場合のために、特定のコンテンツのセットに必要な代替のカスタム命名規則を含むバッチセットプリセットを、必要なだけいくつでも作成できます。

バッチセットプリセット機能を使用するためにデフォルトの命名規則を設定する必要はありませんが、この命名規則を使用して、1 つのセットにグループ化する命名規則の要素をいくつでも定義できます。 これにより、バッチセット作成を合理化できます。

または、フォームフィールドを利用しないで、「**[!UICONTROL コードを表示]**」を使用することもできます。この表示では、正規表現を使用する命名規則の定義を作成します。

定義には、次の 2 つの要素を使用できます。 **[!UICONTROL 一致]** および **[!UICONTROL ベース名]**. これらのフィールドでは、命名規則のすべての要素を定義して、要素が含まれるセットを命名するために使用される規則の一部を指定できます。会社の個々の命名規則では、これらの要素ごとに 1 行以上の定義を使用できます。 一意の定義に対して最大数の行を使用し、それらを個別の要素にグループ化します。 例えば、メイン画像、カラー要素、代替ビュー要素、スウォッチ要素などです。

**デフォルトの命名規則を設定するには、以下の手順に従います。**

1. [Dynamic Media Classic デスクトップアプリケーション](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)を開き、アカウントにログインします。

   資格情報とログオンの詳細は、プロビジョニング時にアドビから付与されたものです。この情報をお持ちでない場合は、テクニカルサポートにお問い合わせください。

1. ページ上部付近のナビゲーションバーで、をタップします。 **[!UICONTROL 設定]** > **[!UICONTROL アプリケーション設定]** > **[!UICONTROL バッチセットプリセット]** > **[!UICONTROL デフォルトの名前]**.
1. 「**[!UICONTROL フォームを表示]**」または「**[!UICONTROL コードを表示]**」を選択し、各要素に関する情報の表示と入力の方法を指定します。

   「**[!UICONTROL コードを表示]**」チェックボックスを選択して、選択した形式と同時に作成される正規表現値を表示できます。フォーム表示により制限を受ける場合、命名規則の要素を定義するために正規表現値を入力または変更できます。値をフォーム表示で解析できない場合は、フォームフィールドは非アクティブになります。

   >[!NOTE]
   >
   >非アクティブなフォームフィールドは、正規表現の正誤に関する検証を実行しません。「結果」行で各要素に作成する正規表現の結果を確認できます。完全な正規表現は、ページの一番下に表示されます。

1. 必要に応じて各要素を展開し、使用する命名規則を入力します。
1. 必要に応じて、次の操作をおこないます。

   * 別の命名規則を要素に追加するには、「**[!UICONTROL 追加]**」をタップします。
   * 要素の命名規則を削除するには、「**[!UICONTROL 削除]**」をタップします。

1. 次のいずれかの操作をおこないます。

   * 「**[!UICONTROL 名前を付けて保存]**」をタップし、プリセットの名前を入力します。
   * 既存のプリセットを編集している場合は、「**[!UICONTROL 保存]**」をタップします。

**バッチセットプリセットの作成**

Dynamic Media では、バッチセットプリセットを使用して、アセットをビューアで表示するための画像のセット（代替画像、カラーオプション、360 スピン）に整理します。バッチセットプリセットは、Dynamic Media でのアセットアップロード処理と同時に自動的に実行されます。

バッチセットプリセットを作成、編集および管理できます。バッチセットプリセット定義には次の 2 つの形式があります。1 つは設定したデフォルトの命名規則、もう 1 つはその場で作成するカスタムの命名規則です。

バッチセットプリセットを定義するフォームフィールドメソッドとコードメソッドのどちらかを使用できます（正規表現を使用できます）。「デフォルトの名前」のように、 [!UICONTROL コードを表示] を [!UICONTROL フォーム表示] 正規表現を使用して定義を作成します。 また、どちらかの表示をオフにして、一方の表示のみを使用することもできます。

**バッチセットプリセットを作成するには：:**

1. [Dynamic Media Classic デスクトップアプリケーション](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)を開き、アカウントにログインします。

   資格情報とログオンの詳細は、プロビジョニング時にアドビから付与されたものです。この情報をお持ちでない場合は、テクニカルサポートにお問い合わせください。

1. ページ上部付近のナビゲーションバーで、をタップします。 **[!UICONTROL 設定]** > **[!UICONTROL アプリケーション設定]** > **[!UICONTROL バッチセットプリセット]** > **[!UICONTROL バッチセットプリセット]**.

   詳細ページの右上隅に設定されている「[!UICONTROL フォームを表示][!UICONTROL 」は、デフォルトの表示です。]

1. プリセットリストパネルで、 **[!UICONTROL 追加]** 定義フィールドを有効にするには、 **[!UICONTROL 詳細]** パネルを使用して、画面の右側に表示されます。
1. 内 **[!UICONTROL 詳細]** パネル、 **[!UICONTROL プリセット名]** 「 」フィールドに、プリセットの名前を入力します。
1. 内 **[!UICONTROL バッチセットの種類]** ドロップダウンメニューから、プリセットの種類を選択します。
1. 次のいずれかの操作を行います。

   * 以前に **[!UICONTROL アプリケーション設定]** > **[!UICONTROL バッチセットプリセット]** > **[!UICONTROL デフォルトの名前]**、展開 **[!UICONTROL アセットの命名規則]**&#x200B;をクリックし、 **[!UICONTROL ファイル名]** ドロップダウンリストから、 **[!UICONTROL デフォルト]**.
   * プリセット設定時に新しい命名規則を定義するには、次の手順を実行します。 **[!UICONTROL アセットの命名規則]**&#x200B;をクリックし、 **[!UICONTROL ファイル名]** ドロップダウンリストから、 **[!UICONTROL カスタム]**.

1. の場合 [!UICONTROL シーケンスの順序]」では、セットがDynamic Mediaでグループ化された後の画像の表示順を定義できます。

   デフォルトでは、アセットはアルファベット順に並んでいます。ただし、コンマ区切りの正規表現リストを使用して順番を定義できます。

1. の場合 **[!UICONTROL 名前を設定]** および **[!UICONTROL 作成規則]**&#x200B;を使用する場合は、 **[!UICONTROL アセットの命名規則]**. また、Dynamic Media のフォルダー構造内のセットの作成場所を定義します。

   多数のセットを定義する場合は、アセット自体を含むフォルダーとは別にセットを保持します。 例えば、画像セットフォルダーを作成して、そこに生成されたセットを配置できます。

1. 内 **[!UICONTROL 詳細]** パネル、タップ **[!UICONTROL 保存]**.
1. 新しいプリセット名の隣にある「**[!UICONTROL アクティブ]**」をタップします。

   プリセットをアクティブにすると、アセットを Dynamic Media にアップロードする際に、バッチセットプリセットを適用してセットを生成できます。

**2D スピンセットを自動生成するためのバッチセットプリセットの作成**

バッチセットの種類の&#x200B;**[!UICONTROL 多軸スピンセット]**&#x200B;を使用して、2D スピンセットの生成を自動化する手法を作成できます。画像のグループ化では行と列の正規表現を使用するので、画像アセットが多次元の配列の対応する場所に正しく配置されます。多軸スピンセットの行数または列数には、上限または下限はありません。

例として、`spin-2dspin` という名前の多軸スピンセットを作成します。1 行あたり 12 個の画像が含まれる 3 行のスピンセット画像セットがあります。画像の名前は次のとおりです。

```
spin-01-01 
 spin-01-02 
 … 
 spin-01-12 
 spin-02-01 
 … 
 spin-03-12
```

この情報を使用すると、 [!UICONTROL バッチセットの種類] レシピは次のように作成できます。

![chlimage_1-1](assets/chlimage_1-1.png)

スピンセットのアセット名における共通部分のグループは、（ハイライト表示されているように）「**[!UICONTROL 一致]**」フィールドに追加しています。行と列を含むアセット名の可変部分は、それぞれ「**[!UICONTROL 行]**」フィールドと「**[!UICONTROL 列]**」フィールドに追加しています。

スピンセットをアップロードして公開する際に、の下に表示される 2D スピンセット手法の名前をアクティブ化します。 **[!UICONTROL バッチセットプリセット]** 内 **[!UICONTROL アップロードジョブオプション]** ダイアログボックス

**2D スピンセットを自動生成するためのバッチセットプリセットを作成するには：**

1. [Dynamic Media Classic デスクトップアプリケーション](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)を開き、アカウントにログインします。

   資格情報とログオンの詳細は、プロビジョニング時にアドビから付与されたものです。この情報をお持ちでない場合は、テクニカルサポートにお問い合わせください。

1. ページ上部付近のナビゲーションバーで、をタップします。 **[!UICONTROL 設定]** > **[!UICONTROL アプリケーション設定]** > **[!UICONTROL バッチセットプリセット]** > **[!UICONTROL バッチセットプリセット]**.

   詳細ページの右上隅に設定されている「[!UICONTROL フォームを表示][!UICONTROL 」は、デフォルトの表示です。]

1. 内 **[!UICONTROL プリセットリスト]** パネル、タップ **[!UICONTROL 追加]** 定義フィールドを有効にするには、 **[!UICONTROL 詳細]** パネルを使用して、画面の右側に表示されます。
1. 内 **[!UICONTROL 詳細]** パネル、 [!UICONTROL プリセット名] 「 」フィールドに、プリセットの名前を入力します。
1. 内 **[!UICONTROL バッチセットの種類]** ドロップダウンメニューで、「 **[!UICONTROL アセットセット]**.
1. 内 **[!UICONTROL サブタイプ]** ドロップダウンリストで、「 **[!UICONTROL 多軸スピンセット]**.
1. 展開 **[!UICONTROL アセットの命名規則]**&#x200B;をクリックし、 **[!UICONTROL ファイル名]** ドロップダウンリストから、 **[!UICONTROL カスタム]**.
1. **[!UICONTROL 一致]**&#x200B;およびオプションとして&#x200B;**[!UICONTROL ベース名]**&#x200B;の属性を使用して、グループを構成する画像アセットの命名に使用する正規表現を定義します。

   リテラルの Match 正規表現の例を次に示します。

   `(w+)-w+-w+`

1. 「**[!UICONTROL 行と列の位置]**」を展開し、2D スピンセット配列内の画像アセットの位置の名前形式を定義します。

   ファイル名内での行または列の位置は丸括弧で囲みます。

   例えば、行の正規表現の場合、次のようになります。

   `\w+-R([0-9]+)-\w+`

   または

   `\w+-(\d+)-\w+`

   列の正規表現の例を次に示します。

   `\w+-\w+-C([0-9]+)`

   または

   `\w+-\w+-C(\d+)`

   これらの式は、デモ用の例に過ぎません。 必要に応じて独自の正規表現を作成できます。

   >[!NOTE]
   >
   >行と列の正規表現の組み合わせで、多次元スピンセット配列内のアセットの位置を判断できない場合、そのアセットはセットに追加されず、エラーが記録されます。

1. の場合 **[!UICONTROL 名前を設定]** および **[!UICONTROL 作成規則]**&#x200B;を使用する場合は、 **[!UICONTROL アセットの命名規則]**.

   また、Dynamic Media Classicのフォルダー構造内でスピンセットを作成する場所を定義します。

   多数のセットを定義する場合は、アセット自体を含むフォルダーとは別にセットを保持します。 例えば、スピンセットフォルダーを作成して、そこに生成されたセットを配置します。

1. 内 **[!UICONTROL 詳細]** パネル、タップ **[!UICONTROL 保存]**.
1. 新しいプリセット名の隣にある「**[!UICONTROL アクティブ]**」をタップします。

   プリセットをアクティブにすると、アセットを Dynamic Media にアップロードする際に、バッチセットプリセットを適用してセットを生成できます。

### （オプション）Dynamic Media - Scene7 モードのパフォーマンスの調整 {#optional-tuning-the-performance-of-dynamic-media-scene-mode}

Dynamic Media - Scene7 モードのスムーズな実行を維持するために、アドビでは、以下の同期パフォーマンス／スケーラビリティの微調整のヒントをお勧めします。

* 様々なファイル形式の処理に対応する定義済みのジョブパラメーターを更新する。
* 事前定義済みの Granite のワークフロー（ビデオアセット）キューワーカースレッドを更新する。
* Granite の事前定義済みの一時的なワークフロー（画像および非ビデオアセット）キューワーカースレッドを更新する。
* Dynamic Media Classic サーバーへの最大アップロード接続数を更新する。

#### 様々なファイル形式の処理に対応する定義済みのジョブパラメーターを更新する

ジョブパラメーターを調整して、ファイルアップロード時の処理を高速化できます。例えば、PSD ファイルをアップロードしても、テンプレートとして処理しない場合は、レイヤー抽出を false（オフ）に設定できます。この場合、調整されたジョブパラメーターは次のように表示されます。`process=None&createTemplate=false`

テンプレートの作成を有効にする場合は、次のパラメーターを使用します。`process=MaintainLayers&layerNaming=AppendName&createTemplate=true`

<!-- REMOVED BASED ON CQDOC-17657 You can tune job parameters for faster processing when you upload files. For example, if you are uploading PSD files, but do not want to process them as templates, you can set layer extraction to false (off). In such case, the tuned job parameter would appear as `process=None&createTemplate=false`. -->

PDF ファイル、PostScript® ファイル、PSD ファイルには、以下の「調整済み」ジョブパラメーターを使用することをお勧めします。

<!-- OLD PDF JOB PARAMETERS `pdfprocess=Rasterize&resolution=150&colorspace=Auto&pdfbrochure=false&keywords=false&links=false` -->

<!-- OLD POSTSCRIPT JOB PARAMETERS `psprocess=Rasterize&psresolution=150&pscolorspace=Auto&psalpha=false&psextractsearchwords=false&aiprocess=Rasterize&airesolution=150&aicolorspace=Auto&aialpha=false` -->

| ファイルタイプ | 推奨されるジョブパラメーター |
| ---| ---|
| PDF | `pdfprocess=Thumbnail&resolution=150&colorspace=Auto&pdfbrochure=false&keywords=false&links=false` |
| PostScript® | `psprocess=Rasterize&psresolution=150&pscolorspace=Auto&psalpha=false&psextractsearchwords=false&aiprocess=Thumbnail&airesolution=150&aicolorspace=Auto&aialpha=false` |
| PSD | `process=None&layerNaming=AppendName&anchor=Center&createTemplate=false&extractText=false&extendLayers=false` |

<!-- CQDOC-17657 for PSD entry in table above -->

これらのパラメーターのいずれかを更新するには、[MIME タイプベースの Assets／Dynamic Media Classic アップロードジョブパラメーターサポートの有効化](/help/sites-administering/scene7.md#enabling-mime-type-based-assets-scene-upload-job-parameter-support)の手順に従います。

#### Granite の一時的なワークフローキューの更新 {#updating-the-granite-transient-workflow-queue}

Granite の一時的なワークフローキューは、**[!UICONTROL DAM アセットの更新]**&#x200B;ワークフローに使用されます。Dynamic Media では、画像の取り込みおよび処理に使用されます。

**Granite の一時的なワークフローキューを更新するには：**

1. [https://&lt;server>/system/console/configMgr](http://localhost:4502/system/console/configMgr) に移動して、**[!UICONTROL Queue: Granite Transient Workflow Queue]** を検索します。

   >[!NOTE]
   >
   >OSGi PID は動的に生成されるので、ダイレクト URL ではなく、テキスト検索が必要です。

1. 「**[!UICONTROL 並列ジョブの最大数]**」フィールドで、目的の値に数値を変更します。

   **[!UICONTROL 並列ジョブの最大数]**&#x200B;を増やすと、Dynamic Media へのファイルの大量アップロードを適切にサポートできます。正確な値は、ハードウェアの容量に依存します。初回移行や 1 回限りのバルクアップロードなど、特定のシナリオでは、大きな値を使用できます。ただし、大きな値（コア数の 2 倍など）を使用すると、他の同時アクティビティに悪影響を及ぼす可能性があることに注意してください。そのため、特定事例で値をテストして整する必要があります。

<!--    By default, the maximum number of parallel jobs depends on the number of available CPU cores. For example, on a 4-core server, it assigns 2 worker threads. (A value between 0.0 and 1.0 is ratio based, or any numbers greater than 1 will assign the number of worker threads.)

   Adobe recommends that 32 **[!UICONTROL Maximum Parallel Jobs]** be configured to adequately support heavy upload of files to Dynamic Media Classic. -->

![chlimage_1](assets/chlimage_1.jpeg)

1. 「**[!UICONTROL 保存]**」をタップします。

#### Granite のワークフローキューの更新 {#updating-the-granite-workflow-queue}

Granite のワークフローキューは、一時的でないワークフローに使用されます。Dynamic Media では、**[!UICONTROL Dynamic Media エンコーディングビデオ]**&#x200B;ワークフローでビデオを処理するために使用されます。

**Granite のワークフローキューを更新するには：**

1. `https://<server>/system/console/configMgr` に移動して、**[!UICONTROL Queue: Granite Workflow Queue]** を検索します。

   >[!NOTE]
   >
   >OSGi PID は動的に生成されるので、ダイレクト URL ではなく、テキスト検索が必要です。

1. 「**[!UICONTROL 並列ジョブの最大数]**」フィールドで、目的の値に数値を変更します。

   デフォルトでは、並列ジョブの最大数は、使用可能な CPU コア数によって異なります。例えば、4 コアサーバーでは、2 つの作業スレッドが割り当てられます。（0.0～1.0 の値は比率ベースです。1 より大きい場合は作業スレッドが割り当てられます）。

   ほとんどの事例では、デフォルト設定の 0.5 で十分です。

   ![chlimage_1-1](assets/chlimage_1-1.jpeg)

1. 「**[!UICONTROL 保存]**」をタップします。

#### Scene7 アップロード接続の更新 {#updating-the-scene-upload-connection}

Scene7アップロード接続設定は、Experience Manager AssetsをDynamic Media Classicサーバーに同期します。

**Scene7 アップロード接続を更新するには：**

1. `https://<server>/system/console/configMgr/com.day.cq.dam.scene7.impl.Scene7UploadServiceImpl` に移動します。
1. 「[!UICONTROL Number of connections]」フィールドおよび「[!UICONTROL Active job timeout]」フィールドで、必要に応じて数値を変更します。

   「**[!UICONTROL 接続数]**」の設定は、Experience Manage が Dynamic Media へのアップロードで許可される HTTP 接続の最大数を制御します。通常、事前定義済みの値の 10 接続で十分です。

   「**[!UICONTROL Active job timeout]**」設定は、アップロードされた Dynamic Media アセットが配信サーバーで公開されるまでの待機時間を決定します。デフォルトでは、この値は 2100 秒または 35 分です。

   ほとんどの事例では、2100 の設定で十分です。

   ![chlimage_1-2](assets/chlimage_1-2.jpeg)

1. 「**[!UICONTROL 保存]**」をタップします。

### （オプション）レプリケーション用のアセットのフィルタリング {#optional-filtering-assets-for-replication}

非Dynamic Mediaデプロイメントでは、 *すべて* アセット（画像とビデオの両方）をExperience Managerオーサー環境からExperience Managerパブリッシュノードに移動します。 Experience Manager のパブリッシュサーバーもアセットを配信するので、このワークフローが必要になります。

ただし、Dynamic Mediaデプロイメントでは、アセットはCloud Serviceを通じて配信されるので、同じアセットをExperience Managerのパブリッシュノードにレプリケートする必要はありません。 そのような「ハイブリッドパブリッシング」ワークフローでは、ストレージコストの増大を防ぎ、アセットをレプリケートするための処理時間を短縮します。サイトページなどのその他のコンテンツは、引き続き「パブリッシュ」Experience Managerから提供されます。

フィルターを使用すると、次のことができます。 *除外* アセットのレプリケートを「Experience Manager公開」ノードに移行しない。

#### レプリケーションへのデフォルトのアセットフィルターの使用 {#using-default-asset-filters-for-replication}

Dynamic Mediaを画像やビデオ、またはその両方に使用している場合は、Adobeがそのまま提供するデフォルトのフィルターを使用できます。 以下のフィルターがデフォルトでアクティブです。

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
     <li>オリジナル画像と静的画像レンディションがレプリケーションから除外されます。</li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td>ダイナミックメディアビデオ配信</td> 
   <td>filter-video</td> 
   <td><strong>video/</strong> で始まる</td> 
   <td>標準提供の「filter-video」では、次のようになります。 
    <ul> 
     <li>元のビデオと静的なサムネールのレンディションをレプリケーションから除外します。<br /> <br /> </li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table>

>[!NOTE]
>
>フィルターは、MIME タイプに適用されます。パスを指定することはできません。

#### レプリケーション用のアセットフィルターのカスタマイズ {#customizing-asset-filters-for-replication}

1. Experience Managerで、Experience Managerのロゴをタップしてグローバルナビゲーションコンソールにアクセスし、 **[!UICONTROL ツール]** アイコンをクリックし、 **[!UICONTROL 一般]** > **[!UICONTROL CRXDE Lite]**.
1. 左側のフォルダーツリーで、`/etc/replication/agents.author/publish/jcr:content/damRenditionFilters` に移動し、フィルターを確認します。

   ![chlimage_1-2](assets/chlimage_1-2.png)

1. フィルターの MIME タイプを定義するために、次のように MIME タイプを特定することができます。

   左側のレールで、を展開します。 **[!UICONTROL コンテンツ]** > **[!UICONTROL dam]** > **[!UICONTROL &lt;`locate_your_asset`>]** > **[!UICONTROL jcr:content]** > **[!UICONTROL メタデータ]**&#x200B;を選択し、右側のテーブルで **[!UICONTROL dc:format]**.

   次の図は、あるアセットの dc:format へのパスの例を示しています。

   ![chlimage_1-3](assets/chlimage_1-3.png)

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

   に移動します。 **content/dam/&lt;`locate your asset`>/jcr:content/renditions**.

   次の図は、あるアセットのレンディションの例を示しています。

   ![chlimage_1-4](assets/chlimage_1-4.png)

   オリジナルのみをレプリケートする場合は、「`+original`」と入力します。
