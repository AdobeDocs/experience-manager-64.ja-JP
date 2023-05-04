---
title: Assets パフォーマンスチューニングガイド
description: 次の領域に焦点を当てる [!DNL Experience Manager] 構成、ハードウェア、ソフトウェア、ネットワーク・コンポーネントの変更により、ボトルネックを解消し、パフォーマンスを最適化 [!DNL Experience Manager] アセット。
contentOwner: AG
feature: Asset Management
role: Architect,Admin
exl-id: 6c1bff46-f9e0-4638-9374-a9e820d30534
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '3203'
ht-degree: 43%

---

# Assets パフォーマンスチューニングガイド {#assets-performance-tuning-guide}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

Adobe Experience Manager Assets のセットアップには、多数のハードウェア、ソフトウェアおよびネットワークコンポーネントが含まれています。 導入のシナリオによっては、パフォーマンス上のボトルネックを排除するために、ハードウェア、ソフトウェアおよびネットワークコンポーネントに対して特殊な設定変更が必要になる場合があります。

また、特定のハードウェアおよびソフトウェア最適化ガイドラインを識別して遵守することで、お客様の [!DNL Experience Manager] パフォーマンス、拡張性、信頼性に関する期待に応えるアセットのデプロイメント。

でのパフォーマンスが低下 [!DNL Experience Manager] Assets は、インタラクティブなパフォーマンス、アセット処理、ダウンロード速度などの領域に関するユーザーエクスペリエンスに影響を与える可能性があります。

パフォーマンスの最適化は、すべてのプロジェクトでターゲット指標を確立する前に実行する、基本的なタスクです。

ユーザーに影響を及ぼす前にパフォーマンス上の問題を検出して修正する必要がある主な領域は次のとおりです。

## Platform {#platform}

While [!DNL Experience Manager] は多くのプラットフォームでサポートされており、Adobeは、最適なパフォーマンスと実装の容易さに貢献する Linux および Windows 上のネイティブツールの最大のサポートを見つけました。 64 ビットオペレーティングシステムを導入して、 [!DNL Experience Manager] Assets のデプロイメント。 任意の [!DNL Experience Manager] 導入時には、可能な限り TarMK を実装する必要があります。 TarMK は単一のオーサーインスタンスを超えて拡張できませんが、パフォーマンスは MongoMK よりも優れています。TarMK オフロードインスタンスを追加して、 [!DNL Experience Manager] Assets のデプロイメント。

### 一時フォルダー {#temp-folder}

アセットのアップロード時間を短縮するには、Java 一時ディレクトリに高性能ストレージを使用します。Linux および Windows の場合は、RAM ドライブまたは SSD を使用できます。クラウドベースの環境では、同等の高速ストレージタイプを使用できます。例えば、Amazon EC2 では、 [短命駆動](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/InstanceStorage.html) ドライブを一時フォルダーに使用できます。

サーバーに十分なメモリがあるという前提で、RAM ドライブを設定します。Linux の場合、8GB RAM ドライブを作成するには、次のコマンドを実行します。

```shell
mkfs -q /dev/ram1 800000
 mkdir -p /mnt/aem-tmp
 mount /dev/ram1 /mnt/aem-tmp
 df -H | grep aem-tmp
```

Windows OS では、サードパーティのドライバを使用して RAM ドライブを作成するか、SSD などの高性能ストレージを使用する必要があります。

高パフォーマンスの一時ボリュームの準備が整ったら、JVM パラメーター-Djava.io.tmpdir を設定します。 例えば、AEM の bin/start スクリプト内の CQ_JVM_OPTS 変数の下に次の JVM パラメーターを追加できます。

`-Djava.io.tmpdir=/mnt/aem-tmp`

## Java の設定 {#java-configuration}

### Java バージョン {#java-version}

oracleは 2015 年 4 月に Java 7 の更新プログラムのリリースを停止したので、Adobeは [!DNL Experience Manager] Java 8 のアセット。 場合によってはパフォーマンスの改善が見られます。

### JVM パラメーター {#jvm-parameters}

次の JVM パラメーターを設定してください。

* `-XX:+UseConcMarkSweepGC`
* `-Doak.queryLimitInMemory`=500000
* `-Doak.queryLimitReads`=100000
* `-Dupdate.limit`=250000
* `-Doak.fastQuerySize`=true

## データストアとメモリの設定 {#data-store-and-memory-configuration}

### ファイルデータストアの設定 {#file-data-store-configuration}

すべての [!DNL Experience Manager] Assets ユーザー。 また、`maxCachedBinarySize` パラメーターと `cacheSizeInMB` パラメーターを設定することでパフォーマンスを最大化するのに役立ちます。キャッシュに含めることができるように、`maxCachedBinarySize` を最小のファイルサイズに設定します。`cacheSizeInMB` 内のデータストアで使用するインメモリキャッシュのサイズを指定します。この値は合計ヒープサイズの 2～10％に設定することをお勧めします。ただし、負荷/パフォーマンステストは理想的な設定を決定するのに役立ちます。

### バッファーされる画像キャッシュの最大サイズの設定 {#configure-the-maximum-size-of-the-buffered-image-cache}

多数のアセットを Adobe Experience Manager にアップロードするときは、メモリ消費の予期しないスパイクに対応するために、また OutOfMemoryErrors による JVM エラーを避けるために、バッファーされる画像キャッシュの最大サイズを減らしてください。例えば、最大ヒープ（-`Xmx` パラメーター）が 5 GB のシステムで、Oak BlobCache が 1 GB、文書キャッシュが 2 GB に設定されているとします。この場合、バッファ・キャッシュは最大 1.25 GB とメモリを使用し、予期しないスパイクが発生した場合は 0.75 GB のメモリしか残りません。

OSGi Web コンソールでバッファーされたキャッシュのサイズを設定します。 `https://host:port/system/console/configMgr/com.day.cq.dam.core.impl.cache.CQBufferedImageCache` で、プロパティ `cq.dam.image.cache.max.memory` をバイト単位で指定します。例えば、1073741824 は 1 GB です（1024 x 1024 x 1024 = 1 GB）。

送信者 [!DNL Experience Manager] 6.1 SP1( `sling:osgiConfig` ノードでこのプロパティを設定する場合は、データ型を必ず Long に設定してください。 詳しくは、 [CQBufferedImageCache は、アセットのアップロード中にヒープを消費します](https://helpx.adobe.com/jp/experience-manager/kb/cqbufferedimagecache-consumes-heap-during-asset-uploads.html).

### 共有データストア {#shared-data-stores}

S3 または共有ファイルデータストアの実装は、ディスク領域の節約と大規模な実装におけるネットワークスループットの向上に役立ちます。共有データストアの使用に関する長所と短所について詳しくは、 [Assets サイズ設定ガイド](assets-sizing-guide.md).

### S3 データストア {#s-data-store}

次の S3 データストアの設定（`org.apache.jackrabbit.oak.plugins.blob.datastore.S3DataStore.cfg`）は、アドビが 12.8 TB のバイナリラージオブジェクト（BLOB）を既存のファイルデータストアから顧客サイトの S3 データストアに抽出するのに役立ちました。

```conf
accessKey=<snip>
 secretKey=<snip>
 s3Bucket=<snip>
 s3Region=us-standard
 s3EndPoint=<a href="https://s3.amazonaws.com/">s3.amazonaws.com</a>
 connectionTimeout=120000
 socketTimeout=120000
 maxConnections=80
 writeThreads=60
 concurrentUploadsThreads=30
 asyncUploadLimit=30
 maxErrorRetry=1000
 path=/opt/author/crx-quickstart/repository/datastore
 s3RenameKeys=false
 s3Encryption=SSE_S3
 proactiveCaching=true
 uploadRetries=1000
 migrateFailuresCount=400
```

## ネットワークの最適化 {#network-optimization}

多くの企業には HTTP トラフィックをスニッフィングするファイアウォールがあり、ファイルのアップロードに干渉しファイルを破損するので、HTTPS を有効にすることをお勧めします。サイズの大きなファイルのアップロードについては、Wi-Fi ネットワークでは簡単に飽和するおそれがあるので、必ず有線でネットワークに接続してください。ネットワークのボトルネックの特定に関するガイドラインについては、 [Assets サイズ設定ガイド](assets-sizing-guide.md). ネットワークトポロジを分析してネットワークのパフォーマンスを評価するには、[Assets のネットワークに関する考慮事項](assets-network-considerations.md)を参照してください。

第一に、ネットワークの最適化戦略は使用できる帯域幅や、[!DNL Experience Manager] インスタンスに対する負荷によって変わります。ファイアウォールやプロキシを含む一般的な設定オプションは、ネットワークのパフォーマンスを向上させるのに役立ちます。 以下に、覚えておくべき重要なポイントを示します。

* インスタンスのタイプ（小、中、大）に応じて、十分なネットワーク帯域幅があることを確認します。 [!DNL Experience Manager] インスタンス。 [!DNL Experience Manager] で AWS にホストされている場合、帯域幅が適切に分散されていることが特に重要です。
* [!DNL Experience Manager] インスタンスが AWS にホストされている場合、広い用途に対応するスケールポリシーがあると便利です。高い負荷が予想される場合は、インスタンスのサイズを大きくします。適度/低負荷用に縮小します。
* HTTPS:ほとんどのユーザーには HTTP トラフィックをスニッフィングするファイアウォールがあり、アップロード操作中にファイルのアップロードに悪影響を与えたり、ファイルが破損したりする可能性があります。
* 大きなファイルのアップロード：ユーザーがネットワークに有線で接続していることを確認します（WiFi 接続はすぐに飽和します）。

## ワークフロー {#workflows}

### 一時的なワークフロー {#transient-workflows}

可能な限り、「DAM アセットの更新」ワークフローを「一時的」に設定します。この設定にすると、ワークフローが通常のトラッキングやアーカイブ処理をパススルーする必要がなくなるので、ワークフローの処理に必要なオーバーヘッドが大幅に削減されます。

>[!NOTE]
>
>デフォルトでは、DAM アセットの更新ワークフローは、で一時的に設定されています [!DNL Experience Manager] 6.3.この場合、次の手順をスキップできます。

1. 開く `http://localhost:4502/miscadmin` の [!DNL Experience Manager] インスタンスを設定します。

1. ナビゲーションツリーで、**[!UICONTROL ツール]**／**[!UICONTROL ワークフロー]**／**[!UICONTROL モデル]**／**[!UICONTROL dam]** と展開します。
1. ダブルクリック **[!UICONTROL DAM アセットの更新]**.
1. フローティングツールパネルで、「**[!UICONTROL ページ]**」タブに切り替えて「**[!UICONTROL ページプロパティ]**」をクリックします。
1. 選択 **[!UICONTROL 一時的なワークフロー]** クリック **[!UICONTROL OK]**.

   >[!NOTE]
   >
   >一部の機能は一時的なワークフローをサポートしません。次に、 [!DNL Experience Manager] Assets のデプロイメントには、これらの機能が必要です。一時的なワークフローは設定しないでください。

   一時的なワークフローを使用できない場合は、定期的にパージされるワークフローを実行してアーカイブされた「DAM アセットの更新」ワークフローを削除し、システムのパフォーマンスが低下しないようにします。

   通常、パージワークフローは毎週実行する必要があります。 ただし、大規模なアセットの取り込み中など、リソースを大量に消費するシナリオでは、より頻繁に実行できます。

   ワークフローのパージを設定するには、OSGi コンソールを使用して新しいAdobe「 Granite Workflow Purge 」設定を追加します。 次に、週別メンテナンスウィンドウの一部として、ワークフローを設定およびスケジュールします。

   パージが長時間実行され過ぎると、タイムアウトになります。 したがって、多数のワークフローが原因でパージワークフローが完了しない状況を避けるために、必ずパージジョブを完了するようにしてください。

   例えば、一時的でない多数のワークフロー（ワークフローのインスタンスノードを作成する）を実行した後に、[ACS AEM Commons Workflow Remover](https://adobe-consulting-services.github.io/acs-aem-commons/features/workflow-remover.html) をアドホックベースで実行できます。これにより、冗長および完了したワークフローのインスタンスが即座に削除されるので、Adobe Granite のワークフローのパージスケジューラーが実行されるのを待つ必要がありません。

### 並列ジョブの最大数 {#maximum-parallel-jobs}

デフォルトでは、[!DNL Experience Manager] は最大でサーバー上のプロセッサーと同じ数の並列ジョブを実行できます。この設定の問題点は、多くの負荷がかかる期間にはすべてのプロセッサーが「DAM アセットの更新」ワークフローに占有されるので、UI の応答が遅くなり、[!DNL Experience Manager] がサーバーのパフォーマンスや安定性を保護するその他の処理を実行できなくなる点です。次の手順を実行して、この値をサーバーで使用できるプロセッサーの半分の値にすることをお勧めします。

1. オン [!DNL Experience Manager] 作成者、次に移動 [http://localhost:4502/system/console/slingevent](http://localhost:4702/system/console/slingevent).
1. 実装に関連する各ワークフローキュー（Granite の一時的なワークフローキュー など）で「編集」をクリックします。
1. 「並列ジョブの最大数」の値を変更し、「保存」をクリックします。

キューを使用可能なプロセッサの半分に設定することは、作業を開始する際に役立つソリューションです。 ただし、最大スループットを達成し、環境ごとに調整するには、この数を増減する必要が生じる場合があります。 一時的なワークフローと非一時的なワークフロー、および外部ワークフローなどの他のプロセスには、別々のキューがあります。 プロセッサーの 50％に設定された複数のキューが同時にアクティブになると、システムはすぐにオーバーロードします。使用頻度の高いキューは、ユーザーの実装によって大きく異なります。 このため、サーバーの安定性を損なうことなく効率を最大化するには、これらを慎重に設定する必要が生じる場合があります。

### オフロード {#offloading}

ビデオのトランスコードなど、リソースを大量に消費するワークフローやワークフローの場合は、DAM アセットの更新ワークフローを 2 番目のオーサーインスタンスにオフロードすることができます。 多くの場合、オフロードの問題は、ワークフロー処理のオフロードによって保存される負荷が、インスタンス間でコンテンツを相互にレプリケートするコストによって相殺されることです。

現在 [!DNL Experience Manager] 6.2 およびの機能パック [!DNL Experience Manager] 6.1 では、バイナリレスレプリケーションを使用してオフロードを実行できます。 このモデルでは、オーサーインスタンスは共通のデータストアを共有し、転送レプリケーションを通じてメタデータを相互に送信するだけです。 このアプローチは共有ファイルデータストアで適切に動作しますが、S3 データストアに問題が生じる場合があります。 バックグラウンドの書き込みスレッドが遅延を引き起こす可能性があるので、オフロードジョブの開始前にアセットがデータストアに書き込まれていない可能性があります。

### DAM アセットの更新設定 {#dam-update-asset-configuration}

DAM アセットの更新ワークフローには、Dynamic Media Classic PTIFF の生成やInDesign Server統合など、タスク用に設定されたすべての手順が含まれています。 ただし、大多数のユーザーにとってこれらの手順のうちのいくつかは不要です。アドビでは「DAM アセットの更新」ワークフローモデルのカスタムコピーを作成し、不要な手順はすべて削除することをお勧めします。この場合、DAM アセットの更新のランチャーを更新して新しいモデルを参照するようにします。

>[!NOTE]
>
>DAM アセットの更新ワークフローを集中的に実行すると、ファイルデータストアのサイズが急激に増加する可能性があります。Adobeによる実験の結果、約 5,500 個のワークフローを 8 時間以内に実行した場合、データストアのサイズが約 400 GB 増加する可能性があることが示されました。
>
>これは一時的な増加であり、データストアのガベージコレクションタスクを実行した後、データストアが元のサイズに復元されます。
>
>通常、データストアのガベージコレクションタスクは、他の予定されたメンテナンスタスクと共に毎週実行されます。
>
>ディスク領域が限られている場合に、DAM アセットの更新ワークフローを集中的に実行する際は、ガベージコレクションタスクの実行頻度を増やすことを検討してください。

#### 実行時のレンディションの生成 {#runtime-rendition-generation}

顧客は、Web サイト全体で、またはビジネスパートナーに配布するために、様々なサイズや形式の画像を使用します。 各レンディションはリポジトリ内のアセットのフットプリントに追加されるので、Adobeではこの機能を慎重に使用することをお勧めします。 画像の処理と保存に必要なリソースを削減するために、取り込み時にレンディションとしてではなく、実行時にこれらの画像を生成できます。

多くの Sites のお客様は、要求された時点で画像のサイズを変更し、切り抜く画像サーブレットを実装し、パブリッシュインスタンスに追加の負荷をかけます。 ただし、これらの画像をキャッシュできる限り、課題を軽減できます。

別のアプローチは、 Dynamic Media Classicテクノロジーを使用して画像の操作を完全に中断することです。 さらに、レンディション生成の責任を [!DNL Experience Manager] インフラストラクチャのみでなく、パブリッシュ層全体にも影響を与えます。

#### ImageMagick {#imagemagick}

ImageMagick を使用してレンディションを生成するように DAM アセットの更新ワークフローをカスタマイズした場合は、次の場所にある policy.xml ファイルを変更することをAdobeがお勧めします。 */etc/ImageMagick/*. デフォルトでは、ImageMagick は OS ボリュームで使用できるディスク領域と空きメモリをすべて使用します。次の設定変更を `policymap` policy.xml のセクションを使用して、これらのリソースを制限します。

```xml
<policymap>
  <!-- <policy domain="system" name="precision" value="6"/> -->
  <policy domain="resource" name="temporary-path" value="/ephemeral0/imagemagick_tmp"/>
  <policy domain="resource" name="memory" value="1000MiB"/>
  <policy domain="resource" name="map" value="1000MiB"/>
  <!-- <policy domain="resource" name="area" value="1gb"/> -->
  <policy domain="resource" name="disk" value="10000MiB"/>
  <!-- <policy domain="resource" name="file" value="768"/> -->
  <policy domain="resource" name="thread" value="1"/>
  <policy domain="resource" name="throttle" value="50"/>
  <!-- <policy domain="resource" name="time" value="3600"/> -->
</policymap>
```

さらに、 *configure.xml* ファイル（または環境変数を設定して） `MAGIC_TEMPORARY_PATH`) を、十分な容量と IOPS を持つディスクパーティションに割り当てます。

>[!CAUTION]
>
>使用可能なすべてのディスク領域を ImageMagick で使用する場合、設定を誤るとサーバーの動作が不安定になるおそれがあります。大きなファイルを処理するために必要なポリシーを ImageMagick を使用して変更すると、[!DNL Experience Manager] のパフォーマンスに影響する可能性があります。詳しくは、[ImageMagick のインストールと設定](best-practices-for-imagemagick.md)を参照してください。

>[!NOTE]
>
>ImageMagick `policy.xml` および `configure.xml` 次の場所にファイルが見つかる場合があります： `/usr/lib64/ImageMagick-*/config/` の代わりに `/etc/ImageMagick/`. 詳しくは、 [ImageMagick のドキュメント](https://www.imagemagick.org/script/resources.php) 設定ファイルの場所の詳細については、を参照してください。

Adobe Managed Services（AMS）で [!DNL Experience Manager] を使用しており、大きな PSD ファイルまたは PSB ファイルを大量に処理する予定がある場合は、アドビサポートにお問い合わせください。Experience Manager では、30000 x 23000 ピクセルを超える非常に高い解像度の PSB ファイルを処理できない場合があります。

<!-- 

#### Sub-asset generation and page extraction {#sub-asset-generation-and-page-extraction}

During asset uploads, AEM's workflow creates a separate asset for each page in PDF and Office documents. Each of these pages is an asset by itself, which consumes additional disk space, requires versioning and additional workflow processing. If you do not require separate pages, disable Sub Asset Generation and Page Extraction.

To disable Sub Asset generation, do the following:

1. Open the **[!UICONTROL Workflow Console]** tool by going to */libs/cq/workflow/content/console.html*

1. Select the **[!UICONTROL Models]** tab
1. Double click the **[!UICONTROL DAM Update Asset]** workflow model
1. Delete **[!UICONTROL Process Sub Asset]** step from **[!UICONTROL DAM Update Asset]** workflow model.

1. Click on **[!UICONTROL Save]**

To disable Page Extraction:

1. Open the **[!UICONTROL Workflow Console]** tool by going to */libs/cq/workflow/content/console.html*

1. Select the **[!UICONTROL Launchers]** tab
1. Select a launcher that launches **[!UICONTROL DAM Parse Word Documents]** workflow model 
1. Click **[!UICONTROL Edit]**
1. Select **[!UICONTROL Disable]**
1. Click **[!UICONTROL OK]**
1. Repeat steps 3-6 for other launcher items that use **DAM Parse Word Documents **workflow model 

-->

<!--
# Sub-asset generation and page extraction {#sub-asset-generation-and-page-extraction}

>[!CAUTION]
>
>AEM 6.4 has reached the end of extended support and this documentation is no longer updated. For further details, see our [technical support periods](https://helpx.adobe.com/support/programs/eol-matrix.html). Find the supported versions [here](https://experienceleague.adobe.com/docs/).

During asset uploads, AEM's workflow creates a separate asset for each page in PDF and Office documents. Each of these pages is an asset by itself, which consumes additional disk space, requires versioning and additional workflow processing. If you do not require separate pages, disable Sub Asset Generation and Page Extraction.

To disable Sub Asset generation, do the following:

1. Open the **[!UICONTROL Workflow Console]** tool by going to */libs/cq/workflow/content/console.html*

1. Select the **[!UICONTROL Models]** tab
1. Double click the **[!UICONTROL DAM Update Asset]** workflow model
1. Delete **[!UICONTROL Process Sub Asset]** step from **[!UICONTROL DAM Update Asset]** workflow model.

1. Click on **[!UICONTROL Save]**

To disable Page Extraction:

1. Open the **[!UICONTROL Workflow Console]** tool by going to */libs/cq/workflow/content/console.html*

1. Select the **[!UICONTROL Launchers]** tab
1. Select a launcher that launches **[!UICONTROL DAM Parse Word Documents]** workflow model.
1. Click **[!UICONTROL Edit]**
1. Select **[!UICONTROL Disable]**
1. Click **[!UICONTROL OK]**
1. Repeat steps 3-6 for other launcher items that use **DAM Parse Word Documents** workflow model.
-->

### XMP の書き戻し {#xmp-writeback}

XMPの書き戻しでは、AEMでメタデータが変更されるたびに元のアセットが更新されます。その結果、次のようになります。

* アセット自体が変更されます
* アセットのバージョンが作成されます
* 「DAM アセットの更新」がアセットに対して実行されます

上記の結果により、大量のリソースが消費されます。したがって、Adobeは [無効化， XMPの書き戻し](https://helpx.adobe.com/jp/experience-manager/kb/disable-xmp-writeback.html)（不要な場合）

ワークフロー実行フラグがチェックされている場合、大量のメタデータを読み込むと、リソースを集中的に使用する XMP 書き戻しアクティビティが発生するおそれがあります。このような読み込みは、他のユーザーのパフォーマンスに影響しないように、サーバー使用率が低いときに計画します。

## レプリケーション {#replication}

Sites 実装などで、多数のパブリッシュインスタンスにアセットをレプリケートする場合は、Adobeにはチェーンレプリケーションを使用することをお勧めします。 この場合、オーサーインスタンスは 1 つのパブリッシュインスタンスにレプリケートし、他のパブリッシュインスタンスにレプリケートして、オーサーインスタンスを解放します。

### チェーンレプリケーションの設定 {#configure-chain-replication}

1. レプリケーションのチェーン先に使用するパブリッシュインスタンスを選択します。
1. そのパブリッシュインスタンス上に、他のパブリッシュインスタンスを指すレプリケーションエージェントを追加します
1. 各レプリケーションエージェントで、 **[!UICONTROL 受信時]** の **[!UICONTROL トリガー]** タブ

>[!NOTE]
>
>Adobeでは、アセットの自動アクティベートはお勧めしません。 ただし、必要に応じて、Adobeは、ワークフローの最後の手順（通常は DAM アセットの更新）としてこの操作をおこなうことをお勧めします。

## インデックスを検索 {#search-indexes}

システムインデックスの更新が含まれている場合が多いので、最新のサービスパックやパフォーマンス関連のホットフィックスを実装してください。AEM のバージョンに応じて適用できるインデックスの最適化については、[パフォーマンスチューニングヒント | 6.x](https://helpx.adobe.com/experience-manager/kb/performance-tuning-tips.html) を参照してください。

頻繁に実行するクエリにカスタムインデックスを作成します。詳しくは、[スロークエリの分析手法（英語）](https://aemfaq.blogspot.com/2014/08/oak-query-log-file-analyzer-tool.html)と[カスタムインデックスの作成](/help/sites-deploying/queries-and-indexing.md)を参照してください。クエリやインデックスについての追加のインサイトやベストプラクティスについては、[クエリとインデックスに関するベストプラクティス](/help/sites-deploying/best-practices-for-queries-and-indexing.md) を参照してください。

### Lucene Index の設定 {#lucene-index-configurations}

Oak インデックス設定で最適化を行うと、改善に役立ちます。 [!DNL Experience Manager] Assets のパフォーマンス：

LuceneIndexProvider 設定を更新します。

1. /system/console/configMgrorg.apache.jackrabbit.oak.plugins.index.lucene.LuceneIndexProviderService に移動します。
1. 有効にする **[!UICONTROL CopyOnRead 、 CopyOnWrite 、および Prefetch のインデックスファイル]** 以前のバージョンで [!DNL Experience Manager] 6.2.これらの値は、 [!DNL Experience Manager] 6.2 以降のバージョン。

インデックス設定を更新してインデックス再作成時間を改善：

1. CRXDe /crx/de/index.jspを開き、管理ユーザーとしてログインします。
1. /oak:index/lucene を参照します。
1. 文字列を追加[] プロパティ名 **[!UICONTROL excludedPaths]** 値が「/var」、「/etc/workflow/instances」、「/etc/replication」の
1. /oak:index/damAssetLucene を探します。
1. 文字列を追加[] プロパティ名 **[!UICONTROL includedPaths]** 値が 1 つ&quot;/content/dam&quot;の
1. 保存

（AEM 6.1 および 6.2 のみ）ntBaseLucene インデックスを更新して、アセットの削除および移動のパフォーマンスを向上させます。

1. */oak:index/ntBaseLucene/indexRules/nt:base/properties* を参照します。
1. 2 つの nt:unstructured ノードを追加 **[!UICONTROL slingResource]** および **[!UICONTROL damResolvedPath]** under */oak:index/ntBaseLucene/indexRules/nt:base/properties*
1. ノード上で以下のプロパティを設定します（ ordered プロパティと propertyIndex プロパティのタイプはです）。 *ブール値*:

   slingResource

   name=&quot;sling:resource&quot;

   ordered=false

   propertyIndex= true

   type=&quot;String&quot;

   damResolvedPath

   name=&quot;dam:resolvedPath&quot;

   ordered=false

   propertyIndex=true

   type=&quot;String&quot;

1. /oak:index/ntBaseLucene ノードで、プロパティ `reindex=true` を設定します。
1. クリック **[!UICONTROL すべて保存]**
1. error.log を監視して、インデックス作成が完了したかどうかを確認します。

   インデックスの再インデックスが完了しました： [/oak:index/ntBaseLucene]

1. CRXDe で/oak:index/ntBaseLucene ノードを更新すると、reindex プロパティが false に戻るので、インデックス作成が完了したことも確認できます。
1. インデックス作成が完了したら、CRXDe に戻り、 **[!UICONTROL type]** プロパティをこれら 2 つのインデックスで無効にする

   * */oak:index/slingResource*
   * */oak:index/damResolvedPath*

1. クリック **[!UICONTROL すべて保存]**

Lucene テキスト抽出を無効にする：

PDFドキュメントに含まれるテキストの検索など、アセットの内容を検索できる必要がない場合は、この機能を無効にしてインデックスのパフォーマンスを向上させることができます。

1. 次に移動： [!DNL Experience Manager] パッケージマネージャー/crx/packmgr/index.jsp
1. 以下のパッケージをアップロードしてインストールします。

[ファイルを入手](assets/disable_indexingbinarytextextraction-10.zip)

### guessTotal {#guess-total}

大きな結果セットを生成するクエリを作成するときは、クエリ実行時のメモリ消費を抑えるために `guessTotal` パラメーターを使用してください。

## 既知の問題 {#known-issues}

### サイズの大きなファイル {#large-files}

AEM では、サイズの大きなファイルに関連する既知の問題が主に 2 つあります。ファイルのサイズが 2 GB を超えると、コールドスタンバイ同期がメモリ不足の状況に陥る場合があります。 場合によっては、スタンバイ同期の実行を妨げることがあります。 その他の場合は、プライマリインスタンスがクラッシュします。 このシナリオは、コンテンツパッケージを含む、[!DNL Experience Manager] 内の 2 GB を超えるすべてのファイルが該当します。

同様に、共有 S3 データストアを使用している間にファイルのサイズが 2GB に達すると、ファイルがキャッシュからファイルシステムに完全に保持されるまでに時間がかかる場合があります。 結果として、バイナリなしのレプリケーションを使用しているとき、レプリケーションが完了する前にバイナリデータが保持されていなかった可能性があります。この状況は、特に、オフロードシナリオなどでデータの可用性が重要な場合に問題を引き起こす可能性があります。

## パフォーマンスのテスト {#performance-testing}

すべての [!DNL Experience Manager] のデプロイメントでボトルネックをすばやく特定し解決できるように、パフォーマンステストの体制を確立してください。留意点は次のとおりです。

### ネットワークテスト {#network-testing}

お客様が抱えるネットワークパフォーマンスに関するすべての問題に対して、次のタスクを実行します。

* お客様のネットワーク内からネットワークのパフォーマンスをテスト
* ネットワークネットワーク内からAdobeのパフォーマンスをテストする。 AMS ユーザーの場合、CSE を使用してアドビのネットワーク内からテストしてください。
* 別のアクセスポイントからのネットワークパフォーマンスのテスト
* ネットワークベンチマークツールを使用する
* Dispatcher に対するテスト

### [!DNL Experience Manager] インスタンステスト {#aem-instance-testing}

CPU の効率的な使用率と負荷の共有により、待ち時間を最小限に抑え、高いスループットを実現するには、 [!DNL Experience Manager] インスタンスを定期的に作成します。 具体的には、以下のようになります。

* に対して負荷テストを実行 [!DNL Experience Manager] インスタンス
* アップロードのパフォーマンスと UI の応答性を監視する

## [!DNL Experience Manager] アセットパフォーマンスチェックリスト {#aem-assets-performance-checklist}

* HTTPS を有効化して企業の HTTP トラフィックスニッファーに対応する.
* サイズの大きなアセットのアップロードには有線接続を使用する.
* 最適な JVM パラメーターを設定します。
* ファイルシステムのデータストアまたは S3 データストアを設定します。
* サブアセットの生成を無効にします。有効にした場合、AEM ワークフローは複数ページのアセットの各ページに個別のアセットを作成します。これらのページはそれ自体がアセットであり、追加のディスク領域を消費するほか、バージョン管理や追加のワークフロー処理を必要とします。個別のページが必要ない場合は、サブアセットの生成とページの抽出のアクティビティを無効にしてください。
* 一時的なワークフローを有効化する.
* Granite のワークフローキューを調整して同時に実行されるジョブ数を制限する.
* ImageMagick を設定して、リソースの消費を制限します。
* 「DAM アセットの更新」ワークフローから不要な手順を削除します。
* ワークフローとバージョンのパージを設定する.
* Lucene インデックスの設定を最適化します。
* 最新のサービスパックとホットフィックスでインデックスを最適化する。その他のインデックスの最適化方法については、アドビカスタマーサポートまでお問い合わせください。
* 用途 `guessTotal` をクリックして、クエリのパフォーマンスを最適化します。
* 次を設定する場合： [!DNL Experience Manager] ファイルの内容からファイルの種類を検出するには、 [!UICONTROL Day CQ DAM Mime Type Service] 内 [!UICONTROL [!DNL Experience Manager] Web コンソール])、操作がリソースを大量に消費するので、ピーク時以外の時間帯に多数のファイルを一括アップロードします。
