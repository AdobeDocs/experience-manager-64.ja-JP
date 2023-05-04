---
title: oak-run.jar でのインデックス作成の使用例
seo-title: Oak-run.jar Indexing Use Cases
description: Oak-run ツールを使用してインデックス作成を実行する様々なユーザーケースについて説明します。
seo-description: Learn about the various user cases for performing indexing with the Oak-run tool.
uuid: 3c50080d-1e0d-4886-8d37-269f06881eb4
products: SG_EXPERIENCEMANAGER/6.4/SITES
content-type: reference
topic-tags: deploying
discoiquuid: 084075b8-826d-4f27-9342-35f33368f24f
noindex: true
exl-id: 62f1d3e6-b0d2-4d64-b62e-91836b573e8c
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '1411'
ht-degree: 58%

---

# oak-run.jar でのインデックス作成の使用例{#oak-run-jar-indexing-use-cases}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

Oak-run は、コマンドラインで以下のようなインデックスに関する使用例をサポートします。AEM の JMX コンソールを使用する必要はありません。

oak-run.jar インデックスコマンドを使用して Oak インデックスを管理する全般的なメリットとして、以下のものがあります。

1. Oak-run index コマンドは、AEM 6.4 用の新しいインデックス作成ツールセットを提供します。
1. Oak-run を使用すると、インデックス再作成の時間を短縮でき、大きなリポジトリでのインデックス再作成時間を短縮できます。
1. Oak-run を使用すると、AEMでインデックスを再作成する際のリソース消費を削減でき、全体的なシステムパフォーマンスが向上します。
1. Oak-run は、帯域外のインデックス再作成を提供し、実稼動環境を利用する必要がある状況をサポートし、インデックス再作成に必要なメンテナンスやダウンタイムを許容できません。

以下の節では、サンプルコマンドを示します。 oak-run index コマンドは、すべての NodeStore および BlobStore 設定をサポートします。 以下に示す例は、FileDataStore と SegmentNodeStore を持つ設定に関するものです。

## 使用例 1 — インデックスの整合性チェック {#usercase1indexconsistencycheck}

これは、インデックスの破損に関連する使用例です。 場合によっては、破損しているインデックスを特定できないことがありました。 したがって、Adobeには次のようなツールが用意されています。

1. すべてのインデックスでインデックスの整合性チェックを実行し、有効なインデックスと無効なインデックスに関するレポートを提供します。
1. このツールは、AEM にアクセスできない場合でも使用可能です。
1. このツールは簡単に使用できます。

破損しているインデックスのチェックは、`--index-consistency-check` 操作を使用して実行できます。

```shell
java -jar oak-run*.jar index --fds-path=/path/to/datastore  /path/to/segmentstore/ --index-consistency-check
```

これにより、`indexing-result/index-consistency-check-report.txt` にレポートが生成されます。サンプルレポートについては、以下を参照してください。

```
Valid indexes :
        - /content/oak:index/enablementResourceName
        - /oak:index/cqProjectLucene
        - /oak:index/cqTagLucene
        - /oak:index/lucene
        - /oak:index/ntBaseLucene
        - /oak:index/socialLucene
    Invalid indexes :
        - /oak:index/atDamIndex
        - /oak:index/atIndex
        - /oak:index/cqPageLucene
        - /oak:index/damAssetLucene
        - /oak:index/groups
        - /oak:index/slingeventJob
        - /oak:index/users
        - /oak:index/workflowDataLucene
    Ignored indexes as these are not of type lucene:
        - /oak:index/acPrincipalName
        - /oak:index/active
```

### メリット {#uc1benefits}

このツールをサポートおよびシステム管理者が使用して、破損しているインデックスをすばやく判断し、再インデックスできます。

## 使用例 2 — インデックス統計 {#usecase2indexstatistics}

クエリのパフォーマンスAdobeに関する事例の一部を診断するには、多くの場合、既存のインデックス定義、お客様の設定からのインデックス関連の統計が必要でした。 これまで、この情報は複数のリソースに分散されていました。 トラブルシューティングを容易にするために、Adobeは次のツールを作成しました。

1. システムに存在するすべてのインデックス定義を 1 つの JSON ファイルにダンプします。

1. 既存のインデックスの重要な統計をダンプします。

1. オフライン分析のためにインデックスコンテンツをダンプします。

1. AEM にアクセスできない場合でも使用可能です。

前述の操作は、次の操作用の index コマンドを使用して実行できるようになりました。

* `--index-info` - インデックスに関連するさまざまな統計を収集してダンプします。

* `--index-definitions` - インデックス定義を収集してダンプします。

* `--index-dump` - インデックスコンテンツをダンプします。

コマンドが実際にどのように機能するかについての例は、次を参照してください。

```shell
java -jar oak-run*.jar index --fds-path=/path/to/datastore  /path/to/segmentstore/ --index-info --index-definitions --index-dump
```

これらのレポートは、`indexing-result/index-info.txt` および `indexing-result/index-definitions.json` に生成されます。

さらに、同じ詳細が Web コンソール経由で提供され、設定ダンプ zip に含まれます。 次の場所からアクセスできます。

`https://serverhost:serverport/system/console/status-oak-index-defn`

### メリット {#uc2benefits}

このツールを使用すると、インデックス作成やクエリの問題に関する必要なすべての詳細を迅速に収集し、この情報の抽出に費やす時間を短縮できます。

## 使用例 3 — インデックスの再作成 {#usecase3reindexing}

[シナリオ](https://jackrabbit.apache.org/oak/docs/query/indexing.html#reindexing)によっては、インデックス再作成の実行が必要な場合があります。現在、インデックス再作成を行うには、CRXDE またはインデックスマネージャのユーザーインターフェイスを使用して、インデックス定義ノードで `reindex` フラグを `true` に設定します。このフラグを設定すると、インデックス再作成は非同期でおこなわれます。

インデックスの再作成に関する注意事項を次に示します。

* インデックス再作成を `DocumentNodeStore` 設定で行うと、すべてのコンテンツがローカルにある `SegmentNodeStore` 設定で行う場合より、大幅に時間がかかります。

* 現在の設計では、インデックス再作成中に非同期インデクサーがブロックされます。他のすべての非同期インデックスが古くなり、インデックス作成中に更新が取得されません。このため、システムが使用中の場合は、最新の結果が表示されないことがあります。
* インデックス再作成には、リポジトリ全体のトラバーサルが伴います。これは、AEM 設定に大きな負荷がかかる可能性があり、エンドユーザーエクスペリエンスに影響する可能性があります。
* `DocumentNodeStore` インストールでは、インデックス再作成にかなりの時間がかかる可能性があります。操作中に Mongo データベースへの接続に失敗すると、インデックス作成を最初からやり直す必要があります。

* インデックス再作成には、テキストの抽出が原因で時間がかかる場合があります。 これは、主に多数のPDFファイルを持つ設定に固有で、テキストの抽出に費やす時間は、インデックス作成時間に影響を与える可能性があります。

これらの目的を満たすために、oak-run インデックスツールは、必要に応じて使用できるインデックス再作成のための様々なモードをサポートします。 oak-run index コマンドには次の利点があります。

* **out-of-band のインデックス再作成** - oak-run のインデックス再作成は、実行中の AEM 設定とは別に実行できるので、使用中の AEM インスタンスへの影響が最小限に抑えられます。

* **out-of-lane のインデックス再作成** - このインデックス再作成は、インデックス作成操作に影響を与えずに行なわれます。つまり、非同期インデクサーは他のインデックス作成を続行できます。

* **インストールでの簡略化されたインデックス再作成** - `DocumentNodeStore`DocumentNodeStore インストールでは、インデックス再作成が単一のコマンドで実行できます。これにより、インデックス再作成が確実に最適な方法で実行されます。

* **インデックス定義の更新および新しいインデックス定義の導入のサポート**

### インデックス再作成 - DocumentNodeStore {#reindexdocumentnodestore}

`DocumentNodeStore` インストールでは、単一の oak-run コマンドを使用してインデックス再作成を行うことができます。

```shell
java -jar oak-run*.jar index --reindex --index-paths=/oak:index/lucene --read-write --fds-path=/path/to/datastore mongodb://server:port/aem
```

これには次のような利点があります

* 実行中のAEMインスタンスに対する影響は最小限です。 ほとんどの読み取りはセカンダリサーバーから実行できます。実行中の AEM のキャッシュは、インデックス再作成に必要とされるトラバーサルをすべて考慮しても、悪影響は受けません。
* ユーザーは、`--index-definitions-file` オプションを使用して新しいインデックスまたは更新されたインデックスの JSON を提供することもできます。

### インデックス再作成 - SegmentNodeStore {#reindexsegmentnodestore}

`SegmentNodeStore` インストールでは、次のいずれかの方法でインデックス再作成を行うことができます。

#### オンラインのインデックス再作成 - SegmentNodeStore {#onlinereindexsegmentnodestore}

既定の方法に従い、`reindex` フラグを設定してインデックス再作成を行います。

#### オンラインのインデックス再作成 - SegmentNodeStore - AEM インスタンス実行中 {#onlinereindexsegmentnodestoretheaeminstanceisrunning}

`SegmentNodeStore` インストールでは、セグメントファイルに読み取り／書き込みモードでアクセスできるのは 1 つのプロセスのみです。このため、oak-run インデックス作成の一部の操作では、追加の手動手順を実行する必要があります。

これには次のものが含まれます。

1. ステップテキスト
1. AEM で使用される同じリポジトリに `oak-run` を読み取り専用モードで接続し、インデックスを作成します。これを実行する方法の例：

   ```shell
   java -jar oak-run-1.7.6.jar index --fds-path=/Users/dhasler/dev/cq/quickstart/target/crx-quickstart/repository/datastore/ --checkpoint 26b7da38-a699-45b2-82fb-73aa2f9af0e2 --reindex --index-paths=/oak:index/lucene /Users/dhasler/dev/cq/quickstart/target/crx-quickstart/repository/segmentstore/
   ```

1. 最後に、前述のコマンドを実行した後で、`IndexerMBean#importIndex` 操作を使用して、oak-run がインデックスファイルを保存したパスから、作成したインデックスファイルを読み込みます。

このシナリオでは、AEMサーバーを停止したり、新しいインスタンスをプロビジョニングしたりする必要はありません。 ただし、インデックス作成にはリポジトリ全体のトラバーサルが伴うので、インストール時の I/O 負荷が増加し、実行時のパフォーマンスに悪影響が出ます。

#### オンラインインデックス再作成 — SegmentNodeStore - AEMインスタンスがシャットダウンされます {#onlinereindexsegmentnodestoreaeminstanceisdown}

`SegmentNodeStore` インストールでは、単一の oak-run コマンドを使用してインデックス再作成を行うことができます。ただし、AEMインスタンスをシャットダウンする必要があります。

次のコマンドを使用して、インデックス再作成をトリガーできます。

```shell
java -jar oak-run*.jar index --reindex --index-paths=/oak:index/lucene --read-write --fds-path=/path/to/datastore  /path/to/segmentstore/ 
```

このアプローチと上記で説明したアプローチの違いは、チェックポイントの作成とインデックスのインポートが自動的におこなわれる点です。 欠点は、プロセス中にAEMを停止させる必要があることです。

#### 帯域外再インデックス — SegmentNodeStore {#outofbandreindexsegmentnodestore}

この使用例では、クローン設定に対してインデックス再作成を実行し、実行中のAEMインスタンスへの影響を最小限に抑えることができます。

1. JMX 操作でチェックポイントを作成します。これを行うには、[JMX コンソール](/help/sites-administering/jmx-console.md)に移動して、`CheckpointManager` を検索します。次に、**createCheckpoint(long p1)** 操作をクリックして、秒単位の有効期限に大きい値（**2592000** など）を使用します。
1. 新しいマシンに `crx-quickstart` フォルダーをコピーします。
1. oak-run の index コマンドを使用してインデックスを再作成します。

1. 生成されたインデックスファイルを AEM サーバーにコピーします。

1. JMX を使用してインデックスファイルをインポートします。

このユースケースでは、別のインスタンスのデータストアにアクセスできることを前提としていますが、`FileDataStore` が EBS などのクラウドベースのストレージソリューションに配置されている場合は、このデータストアにアクセスできないことがあります。この場合、`FileDataStore` のクローンも作成されるシナリオは除外されます。インデックス定義でフルテキストのインデックス作成が実行されない場合は、`DataStore` へのアクセスは必要ありません。

## 使用例 4 - インデックス定義の更新 {#usecase4updatingindexdefinitions}

現在、インデックス定義の変更は、[ACS Ensure Index](https://adobe-consulting-services.github.io/acs-aem-commons/features/ensure-oak-index/index.html) パッケージ経由で送信できます。これにより、コンテンツパッケージ経由でインデックス定義の送信が可能になります。コンテンツパッケージは後で、`reindex` フラグを `true` に設定してインデックスを再作成する必要があります。

これは、インデックス再作成に時間がかからない小規模なインストールで適切に機能します。 ただし、非常に大きなリポジトリの場合、インデックスの再作成はかなり長い時間でおこなわれます。 このような場合には、oak-run インデックスツールを使用できます。

Oak-run では、JSON 形式でのインデックス定義の提供と、ライブインスタンスで変更が実行されない帯域外モードでのインデックスの作成がサポートされるようになりました。

この使用例で考慮する必要があるプロセスは次のとおりです。

1. 開発者がローカルインスタンスでインデックス定義を更新し、インデックス定義の JSON ファイルを `--index-definitions` オプションを使用して生成します。

1. 更新された JSON がシステム管理者に提供されます。
1. システム管理者は Out of Band 方式に従って、別のインストールでインデックスを準備します。
1. これが完了すると、生成されたインデックスファイルが、実行中の AEM インストールに読み込まれます。
