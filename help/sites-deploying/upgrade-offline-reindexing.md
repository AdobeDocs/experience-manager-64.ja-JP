---
title: オフラインでのインデックス再作成を使用したアップグレード中のダウンタイムの削減
description: AEMのアップグレードを実行する際に、オフラインのインデックス再作成手法を使用して、システムのダウンタイムを短縮する方法を説明します。
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: upgrading
content-type: reference
feature: Upgrading
exl-id: 7d2cf3d6-0dd3-4ce2-be9e-5d8b65a9edab
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '1343'
ht-degree: 1%

---

# オフラインでのインデックス再作成を使用したアップグレード中のダウンタイムの削減 {#offline-reindexing-to-reduce-downtime-during-upgrades}

## はじめに {#introduction}

Adobe Experience Managerのアップグレードにおける主な課題の 1 つは、インプレースアップグレードの実行時にオーサー環境に関連するダウンタイムです。 コンテンツ作成者は、アップグレード中に環境にアクセスできなくなります。 したがって、アップグレードの実行に要する時間を最小限に抑えることをお勧めします。 大規模なリポジトリ、特にAEM Assetsプロジェクトでは、大規模なデータストアと、1 時間あたりの高レベルのアセットアップロードがある場合、Oak インデックスのインデックス再作成は、アップグレードにかなりの時間がかかります。

この節では、Oak-run ツールを使用してリポジトリを再インデックスする方法について説明します **前** アップグレードを実行することで、実際のアップグレード中のダウンタイムを削減できます。 以下に示す手順を適用できます。 [Lucene](https://jackrabbit.apache.org/oak/docs/query/lucene.html) バージョンAEM 6.4 以降のインデックスです。

## 概要 {#overview}

新しいバージョンのAEMでは、機能セットが拡張されると、Oak インデックス定義に変更が加えられます。 AEMインスタンスのアップグレード時に、Oak インデックスを変更すると、インデックスが強制的に再作成されます。 アセットのテキスト（pdf ファイルのテキストなど）が抽出されてインデックスが作成されるので、インデックス再作成はアセットのデプロイメントには高価です。 MongoMK リポジトリを使用すると、データはネットワークを介して保持され、インデックス再作成に要する時間がさらに長くなります。

アップグレード中にほとんどのお客様が直面する問題は、ダウンタイム時間を短縮することです。 解決策は次のとおりです。 **スキップ** アップグレード中のインデックス再作成アクティビティ。 これは、新しいインデックを作成することで実現できます **前** アップグレードを実行するには、アップグレード中にインポートするだけです。

## アプローチ {#approach}

![offline-reindexing-upgrade-text-extraction](assets/offline-reindexing-upgrade-process.png)

目的のAEMバージョンのインデックス定義に対して、アップグレード前にインデックスを作成し、 [Oak-run](/help/sites-deploying/indexing-via-the-oak-run-jar.md) ツール 上の図は、オフラインでのインデックス再作成のアプローチを示しています。

さらに、アプローチで説明した手順の順序は次のとおりです。

1. バイナリからのテキストが最初に抽出されます
2. ターゲットインデックス定義が作成されます
3. オフラインインデックスが作成されます
4. その後、アップグレードプロセス中にインデックスがインポートされます

### テキスト抽出 {#text-extraction}

AEMで完全なインデックス作成を有効にするには、PDFなどのバイナリからテキストを抽出し、インデックスに追加します。 これは通常、インデックス作成プロセスの高コストな手順です。 テキスト抽出は、多数のバイナリを格納するので、特にアセットリポジトリのインデックス再作成に提案される最適化手順です。

![offline-reindexing-upgrade-text-extraction](assets/offline-reindexing-upgrade-text-extraction.png)

システムに保存されたバイナリのテキストは、 tika ライブラリを持つ ge oak-run ツールを使用して抽出できます。 本番システムのクローンは、アップグレードの前に取得でき、このテキスト抽出プロセスに使用できます。 次の手順を実行すると、この処理によってテキストストアが作成されます。

**1.リポジトリを移動し、バイナリの詳細を収集します**

この手順では、パスと BLOB ID を含むバイナリのタプルを含む CSV ファイルを生成します。

インデックスを作成するディレクトリから次のコマンドを実行します。 次の例では、リポジトリのホームディレクトリを想定しています。

```
java java -jar oak-run.jar tika <nodestore path> --fds-path <datastore path> --data-file text-extraction/oak-binary-stats.csv --generate
```

ここで、 `nodestore path` が `mongo_ur` または `crx-quickstart/repository/segmentstore/`

以下を使用： `--fake-ds-path=temp` パラメーターの代わりに `–fds-path` プロセスを高速化する。

**2.既存のインデックスで使用可能なバイナリテキストストアを再利用**

既存のシステムからインデックスデータをダンプし、テキストストアを抽出します。

次のコマンドを使用して、既存のインデックスデータをダンプできます。

```
java -jar oak-run.jar index <nodestore path> --fds-path=<datastore path> --index-dump
```

ここで、 `nodestore path` が `mongo_ur` または `crx-quickstart/repository/segmentstore/`

次に、上記のインデックスダンプを使用してストアに入力します。

```
java -jar oak-run.jar tika --data-file text-extraction/oak-binary-stats.csv --store-path text-extraction/store --index-dir ./indexing-result/index-dumps/<oak-index-name>/data populate
```

ここで、 `oak-index-name` はフルテキストインデックスの名前です（例：「lucene」）。

**3.上記の手順で除外したバイナリに対して、tika ライブラリを使用してテキスト抽出プロセスを実行します**

```
java -cp oak-run.jar:tika-app-1.21.jar org.apache.jackrabbit.oak.run.Main tika --data-file text-extraction/oak-binary-stats.csv --store-path text-extraction/store --fds-path <datastore path> extract
```

ここで、 `datastore path` はバイナリデータストアへのパスです。

作成したテキストストアは、将来のシナリオでインデックス再作成のために更新および再利用できます。

テキスト抽出プロセスについて詳しくは、 [Oak-run ドキュメント](https://jackrabbit.apache.org/oak/docs/query/pre-extract-text.html).

### オフラインインデックス再作成 {#offline-reindexing}

![offline-reindexing-upgrade-offline-reindexing](assets/offline-reindexing-upgrade-offline-reindexing.png)

アップグレードの前に、Lucene インデックスをオフラインで作成します。 MongoMK を使用する場合、ネットワークのオーバーヘッドを回避するので、MongoMk ノードの 1 つで直接実行することをお勧めします。

インデックスをオフラインで作成するには、次の手順に従います。

**1.ターゲットAEMバージョンの Oak Lucene インデックス定義を生成します**

既存のインデックス定義をダンプします。 変更を受けたインデックス定義は、対象のAEMバージョンのAdobeGranite リポジトリバンドルと oak-run を使用して生成されました。

インデックス定義を **ソース** AEMインスタンス、次のコマンドを実行します。

>[!NOTE]
>
>インデックス定義のダンプについて詳しくは、 [Oak ドキュメント](https://jackrabbit.apache.org/oak/docs/query/oak-run-indexing.html#async-index-data).

```
java -jar oak-run.jar index --fds-path <datastore path> <nodestore path> --index-definitions
```

ここで、 `datastore path` および `nodestore path` は、 **ソース** AEMインスタンス。

次に、 **ターゲット** ターゲットバージョンの Granite リポジトリバンドルを使用するAEMバージョン。

```
java -cp oak-run.jar:bundle-com.adobe.granite.repository.jar org.apache.jackrabbit.oak.index.IndexDefinitionUpdater --in indexing-definitions_source.json --out merge-index-definitions_target.json --initializer com.adobe.granite.repository.impl.GraniteContent
```

>[!NOTE]
>
> 上記のインデックス定義の作成プロセスは、 `oak-run-1.12.0` バージョン以降。 ターゲティングは、Granite リポジトリバンドルを使用しておこなわれます `com.adobe.granite.repository-x.x.xx.jar`.

上記の手順では、という名前の JSON ファイルを作成します。 `merge-index-definitions_target.json` これはインデックス定義です。

**2.リポジトリでのチェックポイントの作成**

実稼動環境でのチェックポイントの作成 **ソース** 長い有効期間のAEMインスタンス。 これは、リポジトリのクローンを作成する前に行う必要があります。

次の場所にある JMX コンソールを使用 `http://serveraddress:serverport/system/console/jmx`に移動します。 `CheckpointMBean` を作成し、有効期間が十分に長いチェックポイントを作成します（例：200 日）。 これには、を呼び出します。 `CheckpointMBean#createCheckpoint` と `17280000000` を、全期間（ミリ秒）の引数として指定します。

その後、新しく作成したチェックポイント ID をコピーし、JMX を使用して有効期間を検証します `CheckpointMBean#listCheckpoints`.

>[!NOTE]
>
> このチェックポイントは、後でインデックスがインポートされると削除されます。

詳しくは、 [チェックポイントの作成](https://jackrabbit.apache.org/oak/docs/query/oak-run-indexing.html#out-of-band-create-checkpoint) Oak ドキュメントから。

**生成されたインデックス定義に対してオフラインでのインデックス作成を実行**

Lucene のインデックス再作成は、oak-run を使用してオフラインで実行できます。 このプロセスは、以下のディスクにインデックスデータを作成します。 `indexing-result/indexes`. 該当 **not** リポジトリに書き込むので、実行中のAEMインスタンスを停止する必要はありません。 作成したテキストストアがこのプロセスに入力されます。

```
java -Doak.indexer.memLimitInMB=500 -jar oak-run.jar index <nodestore path> --reindex --doc-traversal-mode --checkpoint <checkpoint> --fds-path <datastore path> --index-definitions-file merge-index-definitions_target.json --pre-extracted-text-dir text-extraction/store

Sample <checkpoint> looks like r16c85700008-0-8
—fds-path: path to data store.
--pre-extracted-text-dir: Directory of pre-extracted text.
merge-index-definitions_target: JSON file having merged definitions for the target AEM instance. indexes in this file will be re-indexed.
```

の使用方法 `--doc-traversal-mode` パラメーターは、リポジトリコンテンツをローカルフラットファイルにスプールすることで再インデックス時間を大幅に改善するので、MongoMK のインストールで便利です。 ただし、リポジトリの 2 倍のサイズの追加のディスク領域が必要です。

MongoMK の場合、この手順を MongoDB インスタンスに近いインスタンスで実行すると、このプロセスを高速化できます。 同じマシン上で実行すると、ネットワークのオーバーヘッドを回避できます。

技術的な詳細については、 [インデックス作成用の oak-run ドキュメント](https://jackrabbit.apache.org/oak/docs/query/oak-run-indexing.html).

### インデックスのインポート {#importing-indexes}

AEM 6.4 以降のバージョンでは、AEMには、起動シーケンス時にディスクからインデックスをインポートする機能が組み込まれています。 フォルダー `<repository>/indexing-result/indexes` は、起動中にインデックスデータが存在するのを監視します。 作成済みのインデックスを上記の場所に、 [アップグレードプロセス](in-place-upgrade.md#performing-the-upgrade) の新しいバージョンを使用する前に **ターゲット** AEM jar. AEMはリポジトリに読み込み、対応するチェックポイントをシステムから削除します。 したがって、再インデックスは完全に回避されます。

## その他のヒントとトラブルシューティング {#troubleshooting}

以下に、役立つヒントとトラブルシューティング手順を示します。

### 実稼動システムへの影響の軽減 {#reduce-the-impact-on-the-live-production-system}

本番システムのクローンを作成し、そのクローンを使用してオフラインインデックスを作成することをお勧めします。 これにより、本番システムに与える影響を排除できます。 ただし、インデックスのインポートに必要なチェックポイントは、本番システムに存在する必要があります。 したがって、クローンを作成する前にチェックポイントを作成することが重要です。

### Runbook と体験版の実行を準備する {#prepare-a-runbook-and-trial-run}

を準備することをお勧めします。 [Runbook](https://docs.adobe.com/content/help/en/experience-manager-65/deploying/upgrading/upgrade-planning.html#building-the-upgrade-and-rollback-runbook) 実稼動環境でアップグレードを実行する前に、いくつかの試用を実行します。

### オフラインインデックス付きドキュメントトラバーサルモード {#doc-traversal-mode-with-offline-indexing}

オフラインのインデックス作成には、リポジトリ全体の複数のトラバーサルが必要です。 MongoMK のインストールでは、インデックス作成プロセスのパフォーマンスに影響を与えるネットワークを介してリポジトリにアクセスします。 1 つの選択肢は、MongoDB レプリカ自体でオフラインインデックス作成プロセスを実行することで、ネットワークのオーバーヘッドをなくすことです。 もう 1 つのオプションは、doc traversal モードの使用です。

ドキュメントトラバーサルモードは、コマンドラインパラメーター `—doc-traversal` を oak-run コマンドに追加し、オフラインでのインデックス作成を実行します。 このモードでは、ローカルディスク内のリポジトリ全体のコピーがフラットファイルとしてスプールされ、インデックス作成の実行に使用されます。
