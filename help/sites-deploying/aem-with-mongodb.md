---
title: MongoDB を備えた AEM
seo-title: AEM with MongoDB
description: MongoDB を使用したAEMを正常にデプロイするために必要なタスクと考慮事項について説明します。
seo-description: Learn about the tasks and considerations needed for a successful AEM with MongoDB deployment.
uuid: 51c463aa-d467-4857-8fff-e5f81d694145
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: platform
content-type: reference
discoiquuid: 3c59ec8f-b72f-48dd-bac8-9817005ae210
exl-id: 8397352a-51b0-4d03-a72d-19f7da58c07e
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '6531'
ht-degree: 31%

---

# MongoDB を備えた AEM{#aem-with-mongodb}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

この記事では、MongoDB を備えたAdobe Experience Managerのデプロイを成功させるために必要な、タスクと考慮事項に関する知識の向上を目的としています。

デプロイメントに関する詳細については、 [デプロイと保守](/help/sites-deploying/deploy.md) の節を参照してください。

## MongoDB をAEMで使用する場合 {#when-to-use-mongodb-with-aem}

通常、MongoDB は、次の条件の 1 つを満たすAEMオーサーのデプロイメントをサポートするために使用されます。

* 1 日に 1,000 人を超えるユニークユーザー
* 100 人を超える同時ユーザー
* 大量のページ編集
* 大きなロールアウトまたはアクティベーション。

上記の条件は、オーサーインスタンスに対してのみ適用され、すべて TarMK ベースにする必要のあるパブリッシュインスタンスに対しては適用されません。 オーサーインスタンスは未認証のアクセスを許可しないので、ユーザー数は認証済みユーザーを指します。

条件が満たされない場合、可用性に対処するために TarMK のアクティブ/スタンバイデプロイメントをお勧めします。 一般に、MongoDB は、拡張要件が、単一のハードウェアアイテムで実現できる以上の条件を満たす場合に考慮する必要があります。

>[!NOTE]
>
>オーサーインスタンスのサイズ設定と同時ユーザーの定義に関する追加情報については、 [ハードウェアのサイズ設定のガイドライン](/help/managing/hardware-sizing-guidelines.md#authors-working-in-parallel).

### AEM向けの MongoDB の最小デプロイメント {#minimal-mongodb-deployment-for-aem}

以下は、MongoDB 上のAEMの最小限のデプロイメントです。 簡単にするために、SSL 終了と HTTP プロキシコンポーネントが一般化されました。 これは、1 つのプライマリと 2 つのセカンダリを含む単一の MongoDB レプリカセットで構成されています。

![chlimage_1-94](assets/chlimage_1-94.png)

最小デプロイメントには、レプリカセットとして設定された 3 つの `mongod` インスタンスが必要です。1 つのインスタンスはプライマリとして選択され、その他のインスタンスはセカンダリとして選択されます。この選択は、`mongod` によって管理されます。各インスタンスにローカルディスクが接続されています。クラスターでこの負荷に対応するには、1 秒あたりの I/O 操作（IOPS）が 3,000 回を超える、12 MB/秒以上のスループットが推奨されます。

AEM オーサーは `mongod` インスタンスに接続されます。各 AEM オーサーは 3 つの `mongod` インスタンスすべてに接続します。書き込みはプライマリに送信され、読み取りはどのインスタンスからも読み取ることができます。 トラフィックは、Dispatcher による読み込みに基づいて、アクティブなAEMオーサーインスタンスのいずれかに分散されます。 OAK データストアは `FileDataStore` であり、MongoDB の監視は、デプロイメントの場所に応じて、MMS または MongoDB Ops Manager によって提供されます。オペレーティングシステムレベルとログの監視は、Splunk や Ganglia などのサードパーティソリューションによって提供されます。

このデプロイメントでは、実装を成功させるには、すべてのコンポーネントが必要です。 見つからないコンポーネントは、実装が機能しなくなります。

### オペレーティングシステム {#operating-systems}

AEM 6 でサポートされているオペレーティングシステムのリストについては、[技術要件のページ](/help/sites-deploying/technical-requirements.md)を参照してください。

### 環境 {#environments}

プロジェクトを実行する異なる技術チーム間で良好な通信が可能な場合、仮想化環境がサポートされます。 これには、AEMを実行しているチーム、オペレーティングシステムを所有しているチーム、仮想化インフラストラクチャを管理しているチームが含まれます。

仮想化環境を管理するチームが管理する必要がある、MongoDB インスタンスの I/O 容量に関する特定の要件があります。 プロジェクトでAmazon Web Servicesなどのクラウドデプロイメントを使用する場合、MongoDB インスタンスをサポートするために、十分な I/O 容量と一貫性を持つインスタンスをプロビジョニングする必要があります。 そうしないと、MongoDB プロセスと Oak リポジトリが、信頼性の低い誤った実行を行います。

仮想化環境では、MongoDB のストレージエンジンが VMWare のリソース割り当てポリシーによって機能しなくなるように、MongoDB は特定の I/O および VM 設定を必要とします。 実装が成功すれば、様々なチーム間に障壁がなくなり、すべてが必要なパフォーマンスを提供するためにサインアップされます。

## ハードウェアに関する考慮事項 {#hardware-considerations}

### ストレージ {#storage}

早期の水平スケーリングを必要とせずに最高のパフォーマンスを得るために読み取りと書き込みのスループットを実現するために、MongoDB は通常、SSD と同等のパフォーマンスを備えた SSD ストレージまたはストレージを必要とします。

### RAM {#ram}

MMAP ストレージエンジンを使用する MongoDB バージョン 2.6 および 3.0 では、データベースの作業セットとそのインデックスが RAM に適合している必要があります。

RAM が不足すると、パフォーマンスが大幅に低下します。 作業セットとデータベースのサイズは、アプリケーションに大きく依存します。 一部の予測は可能ですが、必要な RAM の量を判断する最も信頼性の高い方法は、AEMアプリケーションを構築し、負荷テストを行うことです。

負荷テストプロセスを支援するために、作業セットの合計データベースサイズに対する次の比率を想定できます。

* 1:10 （SSD ストレージ用）
* ハードディスクストレージの場合は 1:3

つまり、SSD デプロイメントの場合、2 TB のデータベースには 200 GB の RAM が必要です。

MongoDB 3.0 の WiredTiger ストレージエンジンにも同じ制限がありますが、RAM とページの障害は、MMAP ストレージエンジンと同じ方法でメモリマッピングを使用しないほど、作業セット、RAM とページの障害の間の相関が強くありません。

>[!NOTE]
>
>Adobeは、MongoDB 3.0 を使用するAEM 6.1 のデプロイメントには、WiredTiger ストレージエンジンを使用することをお勧めします。

### データストア {#data-store}

MongoDB の作業セットの制限により、データストアは MongoDB とは独立して維持することを強くお勧めします。 ほとんどの環境では、すべての AEM インスタンスに対して使用可能な NAS を使用する `FileDataStore` を使用してください。Amazon Web Services を使用する場合は、`S3 DataStore` もあります。何らかの理由でデータストアが MongoDB 内に保持されている場合は、データストアのサイズを合計データベースサイズに追加し、作業セットの計算を適切に調整する必要があります。 これは、ページ障害が発生しないパフォーマンスを維持するために、RAM のプロビジョニングが大幅に増加することを意味します。

## モニタリング {#monitoring}

プロジェクトを正しく実装するには、監視が不可欠です。 十分な知識があれば、監視を行わずにAEMを MongoDB 上で実行できますが、通常、この知識はデプロイメントの各セクションに特化したエンジニアに見つかります。

これには、通常、Apache Oak Core で作業する R&amp;D エンジニアと MongoDB スペシャリストが関与します。

すべてのレベルで監視しない場合、問題を診断するには、コードベースに関する詳細な知識が必要になります。 監視を実施し、主要な統計に関する適切なガイダンスを提供することで、実装チームは異常値に適切に対応できます。

コマンドラインツールを使用してクラスタの動作のスナップショットを簡単に取得することは可能ですが、多くのホストでリアルタイムで実行することはほとんど不可能です。 コマンドラインツールで数分を超える履歴情報が提供されることはほとんどなく、異なるタイプの指標間でのクロスクロスクロスクロスクロス相関を許可することもありません。 `mongod` のバックグラウンド同期が短期間遅くなると、見かけ上は接続されていない仮想マシンからの共有ストレージリソースに対する I/O の待機や過剰な書き込みレベルの相関関係を見つけるために手動による多大な労力が必要になります。

### MongoDB Cloud Manager {#mongodb-cloud-manager}

MongoDB Cloud Manager は、MongoDB インスタンスの監視と管理を可能にする、MongoDB が提供する無料のサービスです。 MongoDB クラスターのパフォーマンスとヘルスをリアルタイムで確認できます。 インスタンスが Cloud Manager 監視サーバーに到達できる場合、クラウドと非公開でホストされるインスタンスの両方を管理します。

このサービスを使用するには、監視サーバーに接続する MongoDB インスタンスにエージェントがインストールされている必要があります。エージェントには次の 3 つのレベルがあります。

* MongoDB サーバー上のすべての処理を完全に自動化できる自動化エージェント
* `mongod` インスタンスを監視できる監視エージェント
* データのスケジュールバックアップを実行できるバックアップエージェント。

MongoDB クラスターのメンテナンスを自動化するために Cloud Manager を使用すると、多くの日常的なタスクが容易になりますが、必須ではなく、バックアップに Cloud Manager を使用する必要もありません。 ただし、監視する Cloud Manager を選択する場合は、監視が必要です。

MongoDB Cloud Manager について詳しくは、[MongoDB のドキュメント](https://docs.mongodb.com/)を参照してください。

### MongoDB Ops Manager {#mongodb-ops-manager}

MongoDB Ops Manager は、MongoDB Cloud Manager と同じソフトウェアです。 登録が完了すると、Ops Manager は、プライベートデータセンターや他のノート PC やデスクトップマシンにローカルでダウンロードしてインストールできます。 ローカルの MongoDB データベースを使用してデータを保存し、Cloud Manager と同じ方法で管理対象サーバーと通信します。 監視エージェントを禁止するセキュリティポリシーがある場合は、MongoDB Ops Manager を使用する必要があります。

### オペレーティングシステムの監視 {#operating-system-monitoring}

AEM MongoDB クラスターを実行するには、オペレーティングシステムレベルの監視が必要です。

Ganglia はこのようなシステムの良い例であり、CPU、負荷平均、空きディスク容量などの基本的なヘルス指標を超えて、必要な情報の範囲と詳細を示します。 問題を診断するには、エントロピープールレベル、CPU I/O 待機、FIN_WAIT2 状態のソケットなどの下位レベルの情報が必要です。

### ログの集計 {#log-aggregation}

複数のサーバのクラスタを使用する場合、本番システムでは中央ログの集約が必要です。 Splunk のようなソフトウェアは、ログの集計をサポートし、チームは、ログを手動で収集することなく、アプリケーションの動作のパターンを分析できます。

## チェックリスト {#checklists}

この節では、プロジェクトを実装する前に、AEMおよび MongoDB のデプロイメントが適切に設定されていることを確認するために必要な様々な手順について説明します。

### ネットワーク {#network}

1. まず、すべてのホストに DNS エントリがあることを確認します。
1. すべてのホストは、他のすべてのルーティング可能なホストからの DNS エントリで解決可能である必要があります
1. すべての MongoDB ホストは、同じクラスタ内の他のすべての MongoDB ホストからルーティング可能です
1. MongoDB ホストは、MongoDB Cloud Manager およびその他の監視サーバーにパケットをルーティングできます
1. AEMサーバは、すべての MongoDB サーバにパケットをルーティングできます
1. 任意のAEMサーバーと MongoDB サーバーとの間のパケット遅延は 2 ミリ秒未満で、パケット損失がなく、1 ミリ秒以下の標準配布が可能です。
1. AEMと MongoDB サーバー間のホップが 2 つ以下であることを確認します。
1. 2 台の MongoDB サーバー間のホップは 2 つまでです
1. 任意のコアサーバ (MongoDB、AEM、または任意の組み合わせ ) 間に OSI レベル 3 より高いルータは存在しません。
1. VLAN トランキングまたは任意の形式のネットワークトンネリングを使用する場合は、パケットレイテンシチェックに従う必要があります。

### AEM設定 {#aem-configuration}

#### ノードストアの設定 {#node-store-configuration}

AEMインスタンスは、MongoMK でAEMを使用するように設定する必要があります。 AEMでの MongoMK 実装の基礎は、ドキュメントノードストアです。

ノードストアの設定方法について詳しくは、 [AEMでのノードストアとデータストアの設定](/help/sites-deploying/data-store-config.md).

最小限の MongoDB デプロイメントに対するドキュメントノードストアの設定例を以下に示します。

```xml
# org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.config

>[!CAUTION]
>
>AEM 6.4 has reached the end of extended support and this documentation is no longer updated. For further details, see our [technical support periods](https://helpx.adobe.com/support/programs/eol-matrix.html). Find the supported versions [here](https://experienceleague.adobe.com/docs/).
#MongoDB server details
mongodburi=mongodb://aem:aempassword@mongodbserver1.customer.com:27000,mongodbserver2.customer.com:27000
  
#Name of MongoDB database to use
db=aem
  
#Store binaries in custom BlobStore e.g. FileDataStore
customBlobStore=true
  
cache=2048
blobCacheSize=1024
```

ここで、

* `mongodburi`

   
これは、AEM が接続する必要がある MongoDB サーバーです。既定のレプリカセットの既知のすべてのメンバに対して接続が行われます。 MongoDB Cloud Manager を使用すると、サーバーセキュリティが有効になります。 したがって、接続文字列には適切なユーザ名とパスワードが含まれている必要があります。 MongoDB の非エンタープライズバージョンでは、ユーザー名とパスワードの認証のみがサポートされます。 接続文字列の構文について詳しくは、 [ドキュメント](https://docs.mongodb.org/manual/reference/connection-string/).

* `db`

   データベースの名前。AEMのデフォルトは `aem-author`.

* `customBlobStore`

   
デプロイメントでバイナリがデータベースに格納される場合、バイナリは作業セットの一部になります。そのため、MongoDB 内にバイナリを格納しないように、 `FileSystem` NAS 上のデータストア

* `cache`

   
キャッシュサイズ（メガバイト単位）です。これは `DocumentNodeStore`. デフォルトは 256MB です。ただし、Oak の読み取りパフォーマンスは、大きなキャッシュのメリットが得られます。

* `blobCacheSize`

   
頻繁に使用される Blob は、データストアから再取得しなくて済むように、AEM にキャッシュできます。これは、特に MongoDB データベースに BLOB を保存する場合に、パフォーマンスに大きな影響を与えます。 すべてのファイルシステムベースのデータストアは、オペレーティングシステムレベルのディスクキャッシュのメリットを受けます。

#### データストアの設定 {#data-store-configuration}

データストアは、しきい値より大きいサイズのファイルを保存するために使用します。 このしきい値の下では、ファイルはドキュメントノードストア内のプロパティとして保存されます。 `MongoBlobStore` を使用する場合、Blob を格納するための専用のコレクションが MongoDB に作成されます。このコレクションは `mongod` インスタンスの作業セットに含まれ、パフォーマンスの問題を回避するには、より大きな RAM が `mongod` に必要になります。そのため、実稼動デプロイメントでは `MongoBlobStore` を使用せず、すべての AEM インスタンス間で共有される、NAS によって提供される `FileDataStore` を使用する設定をお勧めします。ファイルの管理にはオペレーティングシステムレベルのキャッシュが効率的なので、ディスク上のファイルの最小サイズをディスクのブロックサイズに近い値に設定して、ファイルシステムが効率的に使用され、`mongod` インスタンスの作業セットに多数の小さいドキュメントが過剰に含まれないようにします。

次に、MongoDB を使用した AEM の最小デプロイメントにおける一般的なデータストアの設定を示します。

```xml
# org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config

>[!CAUTION]
>
>AEM 6.4 has reached the end of extended support and this documentation is no longer updated. For further details, see our [technical support periods](https://helpx.adobe.com/support/programs/eol-matrix.html). Find the supported versions [here](https://experienceleague.adobe.com/docs/).
# The minimum size of an object that should be stored in this data store.

>[!CAUTION]
>
>AEM 6.4 has reached the end of extended support and this documentation is no longer updated. For further details, see our [technical support periods](https://helpx.adobe.com/support/programs/eol-matrix.html). Find the supported versions [here](https://experienceleague.adobe.com/docs/).
minRecordLength=4096
path=/datastore
maxCachedBinarySize=4096
cacheSizeInMB=128
```

ここで、

* `minRecordLength`

   
サイズ（バイト単位）。このサイズ以下のバイナリは、ドキュメントノードストアと共に保存されます。 BLOB の ID を保存するのではなく、バイナリのコンテンツが保存されます。 このサイズを超えるバイナリについては、バイナリの ID がドキュメントのプロパティとしてノードのコレクションに格納され、バイナリの本文はディスク上のディスク上の `FileDataStore` に。一般的なファイルシステムのブロックサイズは 4,096 バイトです。

* `path`

   
データストアのルートのパスです。MongoMK デプロイメントの場合、これはすべてのAEMインスタンスで使用できる共有ファイルシステムである必要があります。 通常は、NAS(Network Attached Storage) サーバが使用されます。 Amazon Web Services などのクラウドデプロイメントの場合、`S3DataFileStore` も利用できます。

* `cacheSizeInMB`

   
バイナリキャッシュの合計サイズ（メガバイト単位）です。これは、 `maxCacheBinarySize` 設定。

* `maxCachedBinarySize`

   
バイナリキャッシュにキャッシュされるバイナリの最大サイズ（バイト単位）です。ファイルシステムベースのデータストアを使用する場合、バイナリはオペレーティングシステムによって既にキャッシュされているので、データストアのキャッシュに大きな値を使用することはお勧めしません。

#### クエリヒントの無効化 {#disabling-the-query-hint}

すべてのクエリと共に送信されるクエリヒントを無効にすることをお勧めします。

`-Doak.mongo.disableIndexHint=true`

AEMの起動時 これにより、MongoDB は、内部統計に基づいて、使用する最も適切なインデックスに基づいて計算されます。

クエリヒントが無効になっていない場合、インデックスのパフォーマンス調整はAEMのパフォーマンスに影響しません。

#### MongoMK の永続キャッシュの有効化 {#enable-persistent-cache-for-mongomk}

高い I/O 読み取りパフォーマンスを持つ環境の速度を最大化するために、MongoDB デプロイメントに対して永続的なキャッシュ設定を有効にすることをお勧めします。 詳しくは、 [Jackrabbit Oak ドキュメント](https://jackrabbit.apache.org/oak/docs/nodestore/persistent-cache.html).

## MongoDB オペレーティングシステムの最適化 {#mongodb-operating-system-optimizations}

### オペレーティングシステムのサポート {#operating-system-support}

MongoDB 2.6 は、RAM とディスク間のオペレーティングシステムレベル管理の一部の側面に敏感なメモリマップストレージエンジンを使用します。 MongoDB インスタンスのクエリと読み取りパフォーマンスは、ページフォルトと呼ばれる、低速な I/O 操作を回避または排除することに依存しています。 これらは、特に `mongod` プロセスに適用されるページフォールトです。オペレーティングシステムレベルのページ障害と混同しないでください。

高速な操作のために、MongoDB データベースは、既に RAM にあるデータにのみアクセスする必要があります。 アクセスする必要があるデータは、インデックスとデータで構成されています。 このインデックスとデータのコレクションを作業セットと呼びます。 作業セットが使用可能な RAM より大きい場合、MongoDB は、I/O コストが発生するディスクからそのデータをページに格納する必要があり、既にメモリ内にある他のデータを削除する必要があります。 削除によってデータがディスクページの障害から再読み込みされると、データが支配的になり、パフォーマンスが低下します。 作業セットが動的で変数の場合、操作をサポートするために、より多くのページフォルトが発生します。

MongoDB は、Linux、Windows、Mac OS など、様々な種類のオペレーティングシステムで動作します。 詳しくは、 [https://docs.mongodb.com/manual/installation/#supported-platforms](https://docs.mongodb.com/manual/installation/#supported-platforms) を参照してください。 MongoDB は、お使いのオペレーティングシステムに応じて、オペレーティングシステムレベルの推奨事項が異なります。 次のドキュメントが記載されています： [https://docs.mongodb.com/manual/administration/production-checklist-operations/#operating-system-configuration](https://docs.mongodb.com/manual/administration/production-checklist-operations/#operating-system-configuration) 便宜上、ここに要約した

#### Linux {#linux}

* 透明なハグページとデフラグをオフにします。 詳しくは、 [Transparent Huge Pages 設定](https://docs.mongodb.com/manual/tutorial/transparent-huge-pages/) を参照してください。
* [読み込み先の設定を調整する](https://docs.mongodb.com/manual/administration/production-notes/#readahead) を使用すると、データベースファイルを保存しているデバイスのユースケースに合わせて変更できます。

   * MMAPv1 ストレージエンジンの場合、作業セットのサイズが使用可能な RAM より大きく、ドキュメントのアクセスパターンがランダムな場合は、読み上げを 32 または 16 に減らすことを検討してください。 様々な設定を評価して、常駐メモリを最大限にし、ページフォルトの数を減らす最適な値を見つけます。
   * WiredTiger ストレージエンジンの場合は、ストレージメディアのタイプ（回転、SSD など）に関係なく、readahead を 0 に設定します。 一般に、readahead 設定は、より高い readahead 値を使用する場合に測定可能で繰り返し可能で信頼性の高いメリットが得られる場合を除き、推奨されます。 [MongoDB Professional サポート](https://docs.mongodb.com/manual/administration/production-notes/#readahead) は、ゼロ以外の readahead 設定に関するアドバイスとガイダンスを提供できます。

* 仮想環境で RHEL 7/CentOS 7 を実行している場合は、Tuned ツールを無効にします。
* 仮想環境で RHEL 7/CentOS 7 を実行する場合、調整されたツールは、パフォーマンススループットから派生したパフォーマンスプロファイルを自動的に呼び出し、readahead 設定を自動的に 4MB に設定します。 これは、パフォーマンスに悪影響を与える可能性があります。
* SSD ドライブの noop または deadline ディスクスケジューラを使用します。
* ゲスト VM の仮想化ドライブに対して noop ディスクスケジューラを使用します。
* NUMA を無効にするか、vm.zone_reclaim_mode を 0 に設定して、を実行します。 [モンゴ](https://docs.mongodb.com/manual/administration/production-notes/#readahead) インターリービングノードを持つインスタンス 詳しくは、 [MongoDB と NUMA ハードウェア](https://docs.mongodb.com/manual/administration/production-notes/#readahead) を参照してください。

* 使用事例に合わせてハードウェアの ulimit 値を調整します。 複数の [モンゴ](https://docs.mongodb.com/manual/reference/program/mongod/#bin.mongod) または [モンゴ](https://docs.mongodb.com/manual/reference/program/mongos/#bin.mongos) インスタンスが同じユーザーの下で実行されている場合は、それに応じて ulimit 値を調整します。 詳しくは、 [UNIX ulimit 設定](https://docs.mongodb.com/manual/reference/ulimit/) を参照してください。

* 次に対して noatime を使用 [dbPath](https://docs.mongodb.com/manual/reference/configuration-options/#storage.dbPath) マウントポイント。
* デプロイメントに十分なファイルハンドル (fs.file-max)、カーネルの pid 制限 (kernel.pid_max)、プロセスごとの最大スレッド数 (kernel.threads-max) を設定します。 大規模なシステムでは、次の値が出発点として適しています。

   * fs.file-max 値：98000,
   * kernel.pid_max の値は64000,
   * andkernel.threads-max の値は64000です。

* システムにスワップ領域が設定されていることを確認します。 適切なサイズ設定について詳しくは、オペレーティングシステムのドキュメントを参照してください。
* システムのデフォルトの TCP キープアライブが正しく設定されていることを確認します。 値が 300 の場合は、多くの場合、レプリカセットとシャード化されたクラスタのパフォーマンスが向上します。 詳しくは、 [TCP キープアライブ時間は MongoDB デプロイメントに影響を与えますか？](https://docs.mongodb.com/manual/faq/diagnostics/#faq-keepalive) （よくある質問）を参照してください。

#### Windows {#windows}

* NTFS の「最終アクセス時間」の更新を無効にすることを検討してください。 これは、Unix 系のシステムで atime を無効にする場合と似ています。

### WiredTiger {#wiredtiger}

MongoDB 3.2 以降、MongoDB のデフォルトのストレージエンジンは WiredTiger ストレージエンジンです。 このエンジンは、多数の堅牢で拡張性の高い機能を提供し、あらゆる一般的なデータベースワークロードに適しています。 次のセクションでは、これらの機能について説明します。

#### ドキュメントレベルの同時実行 {#document-level-concurrency}

WiredTiger は、書き込み操作にドキュメントレベルの同時実行制御を使用します。 その結果、複数のクライアントが 1 つのコレクションの異なるドキュメントを同時に変更できます。

ほとんどの読み取りおよび書き込み操作で、WiredTiger は楽観的な同時実行制御を使用します。 WiredTiger は、グローバル、データベース、コレクションレベルでのインテントロックのみを使用します。 ストレージエンジンが 2 つの操作間の競合を検出すると、MongoDB がその操作を透過的に再試行する書き込みの競合が発生します。グローバル操作（通常は複数のデータベースに関する短時間の操作）の中には、引き続きグローバルな「インスタンス全体」ロックが必要です。

コレクションの削除など、その他の操作では、排他的なデータベースロックが必要です。

#### スナップショットとチェックポイント {#snapshots-and-checkpoints}

WiredTiger は、MultiVersion Concurrency Control(MVCC) を使用します。 操作の開始時に、WiredTiger はトランザクションに対するデータのポイントインタイムスナップショットを提供します。 スナップショットは、メモリ内データの一貫した表示を示します。

WiredTiger は、ディスクに書き込む際、すべてのデータファイルでの整合性が保たれるように、スナップショットのすべてのデータをディスクに書き込みます。この[永続化](https://docs.mongodb.com/manual/reference/glossary/#term-durable)されたデータは、データファイル内のチェックポイントとして機能します。チェックポイントを使用すると、最後のチェックポイントに至るまで、および最後のチェックポイントを含めて、データ・ファイルの整合性が確保されます。つまり、チェックポイントは回復ポイントとして機能する場合があります。

MongoDB は、60 秒または 2 GB のジャーナルデータの間隔でチェックポイント（スナップショットデータをディスクに書き込む）を作成するように WiredTiger を設定します。

新しいチェックポイントの書き込み中、以前のチェックポイントは引き続き有効です。 したがって、新しいチェックポイントの書き込み中に MongoDB が終了したりエラーが発生した場合でも、再起動時に MongoDB は最後の有効なチェックポイントから回復できます。

新しいチェックポイントは、WiredTiger のメタデータテーブルが自動的に更新され、新しいチェックポイントを参照する際に、アクセス可能で永続的になります。 新しいチェックポイントにアクセスできるようになると、WiredTiger は古いチェックポイントからページを解放します。

WiredTiger を使用 ( [ジャーナル](https://docs.mongodb.com/manual/reference/glossary/#term-durable)を使用すると、MongoDB は最後のチェックポイントから回復できます。ただし、最後のチェックポイントの後に行った変更を復元するには、を使用してを実行します。 [ジャーナル](https://docs.mongodb.com/manual/core/wiredtiger/#storage-wiredtiger-journal).

#### ジャーナル {#journal}

WiredTiger では、トランザクションログの先行書き込みと[チェックポイント](https://docs.mongodb.com/manual/core/wiredtiger/#storage-wiredtiger-checkpoints)を使用して、データの永続性を確保しています。

WiredTiger ジャーナルは、チェックポイント間のすべてのデータ変更を保持します。 チェックポイント間で MongoDB が終了した場合は、ジャーナルを使用して、最後のチェックポイント以降に変更されたすべてのデータを再生します。 MongoDB がジャーナルデータをディスクに書き込む頻度について詳しくは、 [ジャーナリングプロセス](https://docs.mongodb.com/manual/core/journaling/#journal-process).

WiredTiger ジャーナルは、 [素早い](https://docs.mongodb.com/manual/core/journaling/#journal-process) 圧縮ライブラリ。 別の圧縮アルゴリズムを指定する場合、または圧縮を使用しない場合は、 [storage.wiredTiger.engineConfig.journalCompressor](https://docs.mongodb.com/manual/reference/configuration-options/#storage.wiredTiger.engineConfig.journalCompressor) 設定。

詳しくは、[ジャーナル処理と WiredTiger](https://docs.mongodb.com/manual/core/journaling/#journaling-wiredtiger)を参照してください。

>[!NOTE]
>
>WiredTiger の最小ログレコードサイズは 128 バイトです。 ログレコードが 128 バイト以下の場合、WiredTiger はそのレコードを圧縮しません。
>
>[storage.journal.enabled](https://docs.mongodb.com/manual/reference/configuration-options/#storage.journal.enabled) を false に設定すると、ジャーナル処理を無効にすることができ、ジャーナルを維持するためのオーバーヘッドを削減できます。
>
>の場合 [スタンドアロン](https://docs.mongodb.com/manual/reference/glossary/#term-standalone) インスタンスでは、ジャーナルを使用しない場合、チェックポイント間で MongoDB が予期せず終了すると、一部のデータ変更が失われます。 のメンバーの場合 [レプリカセット](https://docs.mongodb.com/manual/reference/glossary/#term-replica-set)を使用すると、レプリケーションプロセスで十分な耐久性が保証される場合があります。

#### 圧縮 {#compression}

WiredTiger を使用すると、MongoDB はすべてのコレクションとインデックスの圧縮をサポートします。 圧縮により、CPU の追加コストをかけてストレージの使用を最小限に抑えます。

デフォルトで、WiredTiger は、すべてのコレクションで [snappy](https://docs.mongodb.com/manual/reference/glossary/#term-snappy) 圧縮ライブラリを使用したブロック圧縮を、すべてのインデックスで[プレフィックス圧縮](https://docs.mongodb.com/manual/reference/glossary/#term-prefix-compression)を使用します。

コレクションの場合、 [zlib](https://docs.mongodb.com/manual/reference/glossary/#term-zlib) はも利用できます。 別の圧縮アルゴリズムを指定する場合、または圧縮を使用しない場合は、 [storage.wiredTiger.collectionConfig.blockCompressor](https://docs.mongodb.com/manual/reference/glossary/#term-zlib) 設定。

インデックスで[プレフィックス圧縮](https://docs.mongodb.com/manual/reference/glossary/#term-prefix-compression)を無効にするには、[storage.wiredTiger.indexConfig.prefixCompression](https://docs.mongodb.com/manual/reference/configuration-options/#storage.wiredTiger.indexConfig.prefixCompression)設定を使用します。

また、圧縮設定は、コレクションおよびインデックスの作成時に、コレクションごとおよびインデックスごとに設定できます。 詳しくは、 [ストレージエンジンのオプションを指定](https://docs.mongodb.com/manual/reference/method/db.createCollection/#create-collection-storage-engine-options) および [db.collection.createIndex() storageEngine](https://docs.mongodb.com/manual/reference/method/db.collection.createIndex/#createindex-options) オプション。

ほとんどのワークロードでは、デフォルトの圧縮設定により、ストレージ効率と処理要件のバランスが取れます。

WiredTiger ジャーナルもデフォルトで圧縮されています。 ジャーナルの圧縮について詳しくは、 [ジャーナル](https://docs.mongodb.com/manual/core/wiredtiger/#storage-wiredtiger-journal).

#### メモリ使用量 {#memory-use}

WiredTiger を使用すると、MongoDB は WiredTiger の内部キャッシュとファイルシステムのキャッシュの両方を利用します。

3.4 以降、WiredTiger の内部キャッシュでは、デフォルトで、次のいずれかの大きい方を使用します。

* RAM の 50%から 1 GB を引いた、または
* 256 MB

既定では、WiredTiger はすべてのコレクションに対して Snappy ブロック圧縮を使用し、すべてのインデックスに対してプレフィックス圧縮を使用します。 圧縮のデフォルトはグローバルレベルで設定でき、コレクションおよびインデックスの作成時に、コレクションごとおよびインデックスごとに設定することもできます。

WiredTiger の内部キャッシュのデータには、ディスク上の形式とは異なる表現が使用されます。

* ファイル・システム・キャッシュ内のデータは、ディスク上のフォーマットと同じです。データ・ファイルの圧縮のメリットも含まれます。 ファイルシステムのキャッシュは、ディスクの I/O を減らすためにオペレーティングシステムによって使用されます。

WiredTiger の内部キャッシュに読み込まれたインデックスは、ディスク上の形式とは異なるデータ表現を持ちますが、インデックスのプレフィックス圧縮を利用して、RAM の使用量を減らすことができます。

インデックスプレフィックス圧縮は、インデックス付きのフィールドから共通のプレフィックスの重複を排除します。

WiredTiger の内部キャッシュ内の収集データは非圧縮で、ディスク上の形式とは異なる表現を使用します。 ブロック圧縮は、ディスク上のストレージを大幅に節約できますが、サーバがデータを操作するには、データを圧縮解除する必要があります。

MongoDB は、ファイルシステムのキャッシュを介して、WiredTiger のキャッシュや他のプロセスで使用されないすべての空きメモリを自動的に使用します。

WiredTiger の内部キャッシュのサイズを調整するには、 [storage.wiredTiger.engineConfig.cacheSizeGB](https://docs.mongodb.com/manual/reference/configuration-options/#storage.wiredTiger.engineConfig.cacheSizeGB) および [—wiredTigerCacheSizeGB](https://docs.mongodb.com/manual/reference/program/mongod/#cmdoption-wiredtigercachesizegb). WiredTiger の内部キャッシュサイズをデフォルト値より大きくしないでください。

### NUMA {#numa}

NUMA(Non Uniform Memory Access) を使用すると、カーネルはプロセッサーコアにメモリをマッピングする方法を管理できます。 この場合、コアが必要なデータに確実にアクセスできるように、メモリアクセスを高速化しようとしますが、NUMA は MMAP に干渉し、読み取りを予測できないので、追加の待ち時間が発生します。 この理由から、NUMA に対応しているすべてのオペレーティングシステムの `mongod` プロセスでこの機能を無効にする必要があります。

要するに、NUMA アーキテクチャのメモリは CPU に接続され、CPU はバスに接続されます。 SMP または UMA アーキテクチャでは、メモリはバスに接続され、CPU によって共有されます。 スレッドが NUMA CPU にメモリを割り当てると、ポリシーに従って割り当てられます。 デフォルトでは、スレッドのローカル CPU に接続されたメモリを割り当てます（空きがない場合を除く）。空き CPU のメモリをより高いコストで使用します。 割り当て後は、メモリは CPU 間を移動しません。 割り当ては、親スレッドから継承されたポリシーによって実行されます。最終的には、プロセスを開始したスレッドになります。

マシンをマルチコアの均一なメモリアーキテクチャと見なす多くのデータベースでは、これにより、最初の CPU が最初にいっぱいになり、次の CPU がその後にいっぱいになります。中核となるスレッドがメモリバッファを割り当てる場合は特にそうなります。これを解決するには、`mongod`プロセスを開始するために使用されるメインスレッドの NUMA ポリシーを変更します。

これは、次のコマンドを実行して実行できます。

```shell
numactl --interleaved=all <mongod> -f config
```

このポリシーは、すべての CPU ノードに対してラウンドロビン方式でメモリを割り当て、すべてのノードに対して均等に分配します。 複数の CPU ハードウェアを搭載したシステムとは異なり、メモリに対する最高のパフォーマンスアクセスは生成されません。 メモリ操作の約半分は速度が低下し、バスを経由しておこなわれますが、`mongod` は NUMA を目的として最適な方法で記述されているわけではないので、これは合理的な妥協策です。

### NUMA に関する問題 {#numa-issues}

`/etc/init.d` フォルダー以外の場所から `mongod` プロセスが開始された場合、適切な NUMA ポリシーで開始されない可能性があります。デフォルトポリシーによっては、問題が発生することがあります。これは、MongoDB 用の様々な Linux パッケージマネージャーインストーラーが、`/etc/init.d` に設定ファイルとともにサービスをインストールし、それにより上記の手順が実行されるからです。アーカイブ（`.tar.gz`）から直接 MongoDB をインストールして実行する場合は、mongod を `numactl` プロセスで手動で実行する必要があります。

>[!NOTE]
>
>使用可能な NUMA ポリシーについて詳しくは、[numactl のドキュメント](https://linux.die.net/man/8/numactl)を参照してください。

MongoDB プロセスの動作は、個々の割り当てポリシーによって異なります。 

* `-membind=<nodes>`

   
リストされているノードのみで割り当てをおこないます。mongod では、リストされているノードのメモリが割り当てられず、使用可能なメモリの一部が使用されない可能性があります。

* `-cpunodebind=<nodes>`

   
ノードのみで実行します。mongod は、指定されたノードのみで実行され、それらのノードで使用可能なメモリのみを使用します。

* `-physcpubind=<nodes>`

   
リストされている CPU（コア）のみで実行します。mongod は、リストされている CPU のみで実行され、それらの CPU で使用可能なメモリのみを使用します。

* `--localalloc`

   
常に現在のノードのメモリを割り当てますが、スレッドを実行しているすべてのノードを使用します。1 つのスレッドで割り当てが実行されている場合は、その CPU で使用可能なメモリのみが使用されます。

* `--preferred=<node>`

   
指定されたノードへの割り当てを優先しますが、優先されるノードがいっぱいである場合は他のノードにフォールバックします。ノードを定義する相対表記を使用できます。 また、スレッドはすべてのノードで実行されます。

一部のポリシーでは、`mongod` プロセスに割り当てられるメモリが、使用可能なすべての RAM よりも少ない場合があります。MySQL とは異なり、MongoDB はオペレーティングシステムレベルのページングを積極的に回避します。その結果、使用可能であると思われるメモリよりも少ない量のメモリが `mongod` プロセスに割り当てられることがあります。

#### スワップ {#swapping}

データベースのメモリを大量に消費する性質上、オペレーティングシステムレベルのスワップを無効にする必要があります。 MongoDB プロセスは、スワッピングしないように設計されています。

#### リモートファイルシステム {#remote-filesystems}

NFS などのリモートファイルシステムでは、非常に多くの遅延が発生します。そのため、MongoDB の内部データファイル（mongod プロセスデータベースファイル）にはお勧めしません。Oak Blob の格納に必要な共有ファイルシステム（FileDataStore）の場合は、NFS が推奨されます。

#### 先読み {#read-ahead}

ランダム読み取りを使用してページがページインされる際に、不要なブロックがディスクから読み取られ、I/O 帯域幅が不必要に使用されることがないように、先読みを調整する必要があります。

### Linux の要件 {#linux-requirements}

#### カーネルの最小バージョン {#minimum-kernel-versions}

* `ext4` ファイルシステムの場合 **2.6.23**

* `xfs` ファイルシステムの場合 **2.6.25**

#### データベースディスクの推奨設定 {#recommended-settings-for-database-disks}

**atime をオフにする**

データベースを格納するディスクについては `atime` を無効にすることをお勧めします。

**NOOP ディスクスケジューラを設定する**

手順は次のとおりです。

まず、現在設定されている I/O スケジューラを確認します。 これは、次のコマンドを実行して実行できます。

```shell
cat /sys/block/sdg/queue/scheduler
```

応答が `noop` である場合、さらに操作をおこなう必要はありません。

設定されている I/O スケジューラーが NOOP でない場合は、次のコマンドを実行して変更できます。

```shell
echo noop > /sys/block/sdg/queue/scheduler
```

**先読み値を調整する**

MongoDB データベースを実行するディスクには、値 32 を使用することをお勧めします。 これは 16 キロバイトに相当します。 次のコマンドを実行して設定できます。

```shell
sudo blockdev --setra <value> <device>
```

#### NTP を有効にする {#enable-ntp}

MongoDB データベースをホストするマシンに NTP がインストールされ、実行されていることを確認します。 例えば、CentOS マシンで yum パッケージマネージャーを使用してインストールできます。

```shell
sudo yum install ntp
```

NTP デーモンがインストールされ、正常に起動したら、drift ファイルでサーバの時間オフセットを確認できます。

#### 透明な巨大ページを無効にする {#disable-transparent-huge-pages}

Red Hat Linux は、Transparent Huge Pages(THP) と呼ばれるメモリ管理アルゴリズムを使用します。 データベースのワークロードにオペレーティングシステムを使用している場合は、無効にすることをお勧めします。

無効にするには、次の手順に従います。

1. `/etc/grub.conf` ファイルを任意のテキストエディターで開きます。
1. grub.conf ファイルに次の行を追加します。

   ```xml
   transparent_hugepage=never
   ```

1. 最後に、次のコマンドを実行して、設定が有効になったかどうかを確認します。

   ```shell
   cat /sys/kernel/mm/redhat_transparent_hugepage/enabled
   ```

   THP が無効の場合、上記のコマンドの出力は次のようになります。

   ```xml
   always madvise [never]
   ```

>[!NOTE]
>
>Transparent Huge Pages について詳しくは、こちらの[記事](https://access.redhat.com/solutions/46111)を参照してください。

#### NUMA の無効化 {#disable-numa}

NUMA が有効なほとんどのインストール環境では、NUMA が `/etc/init.d` フォルダーからサービスとして実行される場合、MongoDB デーモンによって自動的に無効化されます。

そうでない場合は、各プロセスレベルで NUMA を無効にすることができます。無効にするには、次のコマンドを実行します。

```shell
numactl --interleave=all <path_to_process>
```

`<path_to_process>` は、mongod プロセスへのパスです。

続いて、次のコマンドを実行してゾーンの再利用を無効にします。

```shell
echo 0 > /proc/sys/vm/zone_reclaim_mode
```

#### mongod プロセスの ulimit 設定の微調整 {#tweak-the-ulimit-settings-for-the-mongod-process}

Linux では、`ulimit` コマンドによるリソースの割り当てを設定で制御できます。これは、ユーザーごとに行うことも、プロセスごとに行うこともできます。

mongod プロセスの ulimit は、 [MongoDB 推奨 ulimit 設定](https://docs.mongodb.org/manual/reference/ulimit/#recommended-ulimit-settings).

#### MongoDB I/O パフォーマンスのテスト {#test-mongodb-i-o-performance}

MongoDB には、I/O パフォーマンスのテストを目的とした `mongoperf` というツールが用意されています。このツールを使用して、インフラストラクチャを構成しているすべての MongoDB インスタンスのパフォーマンスをテストすることをお勧めします。

`mongoperf` の使用方法について詳しくは、[MongoDB のドキュメント](https://docs.mongodb.org/manual/reference/program/mongoperf/)を参照してください。

>[!NOTE]
>
> `mongoperf` は、MongoDB が実行されているプラットフォームにおける MongoDB のパフォーマンスの指標となるように設計されています。これによって、実稼動システムでのパフォーマンスを保証するものとして結果を捉えないでください。
>
>より正確なパフォーマンス結果を得るには、`fio` Linux ツールを使用して補完テストを実行できます。

**デプロイメントを構成している仮想マシンでの読み取りパフォーマンスのテスト**

ツールをインストールしたら、テストを実行するために MongoDB データベースディレクトリに切り替えます。続いて、次の設定で `mongoperf` を実行して、最初のテストを開始します。

```shell
echo "{nThreads:32,fileSizeMB:1000,r:true}" | mongoperf
```

すべての MongoDB インスタンスで、最大 1 秒あたり 2 ギガバイト（2 GB/秒）および 500,000 IOPS を 32 スレッドで実行しているのが望ましい結果です。

2 回目のテストを実行します。今回は `mmf:true` パラメーターを設定して、メモリマップファイルを使用します。

```shell
echo "{nThreads:32,fileSizeMB:1000,r:true,mmf:true}" | mongoperf
```

2 回目のテストの結果は最初のテストよりもかなり高くなり、メモリ転送のパフォーマンスが良くなったことを示しています。

>[!NOTE]
>
>テストを実施するときは、オペレーティングシステムのモニタリングシステムで対象の仮想マシンの I/O 使用率の状況を確認してください。I/O 読み取りが 100 パーセントに満たない値を示している場合は、仮想マシンに問題がある可能性があります。

**プライマリ MongoDB インスタンスの書き込みパフォーマンステスト**

次に、同じ設定で MongoDB データベースディレクトリから `mongoperf` を実行して、プライマリ MongoDB インスタンスの I/O 書き込みパフォーマンスを確認します。

```shell
echo "{nThreads:32,fileSizeMB:1000,w:true}" | mongoperf
```

必要な出力は、1 秒あたり 12 メガバイトで、約 3,000 IOPS に達し、スレッド数の差はほとんどありません。

## 仮想化環境の手順 {#steps-for-virtualised-environments}

### VMWare {#vmware}

VMWare ESX を使用して仮想化環境を管理およびデプロイしている場合、MongoDB の動作に対応するために、ESX コンソールで次の設定を行ってください。

1. メモリバルーンを無効にします。
1. MongoDB データベースをホストする仮想マシンのメモリを事前に割り当てて確保します。
1. Storage I/O Control を使用して、十分な I/O を `mongod` プロセスに割り当てます。
1. [CPU 予約](https://pubs.vmware.com/vsphere-4-esx-vcenter/index.jsp?topic=/com.vmware.vsphere.vmadmin.doc_41/vsp_vm_guide/configuring_virtual_machines/t_allocate_cpu_resources.html)を設定して、MongoDB をホストするマシンの CPU リソースを確保します。

1. 準仮想化 I/O ドライバーの使用を検討します。その方法について詳しくは、こちらの[ナレッジベースの記事](https://kb.vmware.com/selfservice/microsites/search.do?language=en_US&amp;cmd=displayKC&amp;externalId=1010398)を参照してください。

### Amazon Web Services {#amazon-web-services}

Amazon Web Servicesでの MongoDB の設定方法に関するドキュメントについては、以下のガイドを参照してください [AWSの MongoDB](https://docs.aws.amazon.com/quickstart/latest/mongodb/welcome.html).

## デプロイ前に MongoDB をセキュリティで保護する {#securing-mongodb-before-deployment}

次の投稿を参照： [MongoDB の安全なデプロイ](https://blogs.adobe.com/security/2015/07/securely-deploying-mongodb-3-0.html) を参照してください。

## Dispatcher {#dispatcher}

### Dispatcher 用のオペレーティングシステムの選択 {#choosing-the-operating-system-for-the-dispatcher}

MongoDB デプロイメントを適切に機能させるには、Dispatcher をホストするオペレーティングシステムが実行されている必要があります **Apache httpd バージョン 2.4 以降。**

また、セキュリティへの影響を最小限に抑えるために、ビルドで使用されているすべてのライブラリが最新であることを確認してください。

### Dispatcher 設定 {#dispatcher-configuration}

一般的な Dispatcher 設定は、1 つのAEMインスタンスの 10～20 倍のリクエストスループットに対応します。

Dispatcher は主にステートレスなので、水平方向に簡単に拡大できます。 一部のデプロイメントでは、作成者が特定のリソースにアクセスできないように制限する必要があります。 こうした理由から、オーサーインスタンスで Dispatcher を使用することを強くお勧めします。

Dispatcher を使用せずにAEMを実行する場合は、SSL を終了し、別のアプリケーションでロードバランシングを実行する必要があります。 セッションは、作成元のAEMインスタンス（スティッキー接続と呼ばれる概念）に対するアフィニティを持つ必要があるので、これが必要です。 これは、コンテンツの更新にかかる遅延を最小限に抑えるためです。

設定方法について詳しくは、[Dispatcher のドキュメント](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=ja)を参照してください。

### 追加設定 {#additional-configuration}

#### スティッキー接続 {#sticky-connections}

スティッキー接続により、1 人のユーザーのパーソナライズされたページとセッションデータを、すべてAEMの同じインスタンスで構成することができます。 このデータはインスタンスに保存されるので、以降の同じユーザーからの要求は同じインスタンスに戻ります。

すべての内部レイヤーでスティッキー接続を有効にして、AEMインスタンスにリクエストをルーティングし、以降のリクエストが同じAEMインスタンスに到達するようにすることをお勧めします。 これは、インスタンス間でコンテンツが更新された場合に目立つ遅延を最小限に抑えるのに役立ちます。

#### 長い有効期限 {#long-expires}

デフォルトでは、AEM Dispatcher から送信されるコンテンツには、Last-Modified ヘッダーと Etag ヘッダーがあり、コンテンツの有効期限を示すものはありません。 これにより、ユーザーインターフェイスは常に最新バージョンのリソースを取得できますが、ブラウザーはGET操作を実行して、リソースが変更されたかどうかを確認します。 これにより、ページの読み込みに応じて、HTTP 応答が 304（未変更）の複数のリクエストが発生する場合があります。 有効期限切れにならないリソースの場合、 Expires ヘッダーを設定し、 Last-Modified ヘッダーと ETag ヘッダーを削除すると、コンテンツがキャッシュされ、 Expires ヘッダーの日付が満たされるまで更新要求はおこなわれません。

ただし、この方法を使用すると、Expires ヘッダーの有効期限が切れる前にブラウザーでリソースの有効期限が切れる妥当な方法がなくなります。 これを軽減するために、クライアントライブラリに不変 URL を使用するように HtmlClientLibraryManager を設定できます。

これらの URL は必ず変更されません。 URL に含まれているリソースの本文が変更された場合、変更内容が URL に自動的に反映され、ブラウザーから適切なバージョンのリソースが要求されます。

デフォルトの設定では、HtmlClientLibraryManager にセレクターが追加されます。 セレクターの場合、リソースは、セレクターがそのままの状態で Dispatcher にキャッシュされます。 また、このセレクターを使用して、正しい有効期限動作を確実にすることもできます。 デフォルトのセレクターでは、`lc-.*?-lc` というパターンが使用されます。次の Apache httpd 設定ディレクティブを使用すると、そのパターンに一致するすべての要求が適切な有効期限で提供されます。

```xml
Header set Expires "Tue, 20 Jan 2037 04:20:42 GMT" "expr=(%{REQUEST_STATUS} -eq 200) && (%{REQUEST_URI} =~ /.*lc-.*?-lc.*/)"
Header set Cache-Control "public, no-transform, max-age=267840000" "expr=(%{REQUEST_STATUS} -eq 200) && (%{REQUEST_URI} =~ /.*lc-.*?-lc.*/)"
Header unset ETag "expr=(%{REQUEST_STATUS} -eq 200) && (%{REQUEST_URI} =~ /.*lc-.*?-lc.*/)"
Header unset Last-Modified "expr=(%{REQUEST_STATUS} -eq 200) && (%{REQUEST_URI} =~ /.*lc-.*?-lc.*/)"
Header unset Pragma "expr=(%{REQUEST_STATUS} -eq 200) && (%{REQUEST_URI} =~ /.*lc-.*?-lc.*/)"
```

#### スニフなし {#no-sniff}

content-type を指定せずにコンテンツを送信する場合、多くのブラウザーでは、コンテンツの最初の数バイトを読み取ることで、コンテンツのタイプを推測しようとします。 これは「スニフィング」と呼ばれます。 スニフィングを行うと、リポジトリに書き込むことのできるユーザーが、コンテンツタイプのない悪意のあるコンテンツをアップロードする可能性があるので、セキュリティの脆弱性が生じます。

そのため、Dispatcher で処理されるリソースに `no-sniff` ヘッダーを追加することをお勧めします。ただし、Dispatcher はヘッダーをキャッシュしません。 つまり、ローカルファイルシステムから提供されるコンテンツのコンテンツタイプは、元のAEMサーバーの元の content-type ヘッダーを使用するのではなく、拡張子によって決定されます。

Web アプリケーションがファイルタイプなしでキャッシュされたリソースを提供しないことがわかっている場合は、スニフを安全に有効にできません。

スニフなし (No Sniff) は、次のように含めて有効にできます。

```xml
Header set X-Content-Type-Options "nosniff"
```

また、次のように選択的に有効にすることもできます。

```xml
RewriteCond %{REQUEST_URI} \.(?:js|jsonp)$ [OR]
RewriteCond %{QUERY_STRING} (callback|jsonp|cb)=\w+
RewriteRule .* - [E=jsonp_request:1]
Header set X-Content-Type-Options "nosniff"  env=jsonp_request
Header setifempty Content-Type application/javascript env=jsonp_request
```

#### コンテンツセキュリティポリシー {#content-security-policy}

デフォルトの Dispatcher 設定では、CSP とも呼ばれるコンテンツセキュリティポリシーを開くことができます。 これにより、ページはブラウザーサンドボックスのデフォルトポリシーに従うすべてのドメインからリソースを読み込むことができます。

信頼できない外部サーバーや検証されていない外部サーバーから JavaScript エンジンにコードが読み込まれるのを防ぐには、リソースの読み込み元を制限することをお勧めします。

CSP を使用すると、ポリシーを微調整できます。 ただし、複雑なアプリケーションでは、ポリシーの制限が厳しすぎるとユーザーインターフェイスの一部が壊れる可能性があるので、CSP ヘッダーを慎重に開発する必要があります。

>[!NOTE]
>
>この機能について詳しくは、 [コンテンツセキュリティポリシーの OWASP ページ](https://www.owasp.org/index.php/Content_Security_Policy).

### サイズ調整 {#sizing}

サイズ設定について詳しくは、 [ハードウェアのサイズ設定のガイドライン](/help/managing/hardware-sizing-guidelines.md).

### MongoDB パフォーマンスの最適化 {#mongodb-performance-optimization}

MongoDB のパフォーマンスに関する一般的な情報については、 [MongoDB のパフォーマンスの分析](https://docs.mongodb.org/manual/administration/analyzing-mongodb-performance/).

## 既知の制限事項 {#known-limitations}

### 同時インストール {#concurrent-installations}

単一のデータベースを持つ複数のAEMインスタンスの同時使用は MongoMK でサポートされますが、同時インストールはサポートされません。

この制限を回避するには、まず 1 つのメンバーでインストールを実行し、最初のインストールが完了した後で、他のメンバーを追加します。

### ページ名の長さ {#page-name-length}

AEMが MongoMK 永続性マネージャーデプロイメントで実行されている場合、 [ページ名は 150 文字までに制限されています](/help/sites-authoring/managing-pages.md#page-name-restrictions-and-best-practices).

>[!NOTE]
>
>MongoDB 自体の既知の制限やしきい値についても理解しておくために、[MongoDB のドキュメントを参照してください](https://docs.mongodb.com/manual/reference/limits/)。
