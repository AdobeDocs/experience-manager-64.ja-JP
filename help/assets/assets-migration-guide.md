---
title: アセットの一括移行
description: アセットをAEMに取り込み、メタデータを適用し、レンディションを生成し、それらをアクティブ化して発行インスタンスを作成する方法。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 976d037d701eb7cc61a62e14e554675961d6179c

---


# Assets migration guide {#assets-migration-guide}

アセットを AEM に移行する際には、いくつかの手順を考慮する必要があります。実装によって大きく異なるので、現在のホームからアセットとメタデータを抽出する方法は、このドキュメントの範囲外です。 代わりに、このドキュメントでは、これらのアセットをAEMに取り込み、メタデータを適用し、レンディションを生成し、アセットをアクティブ化または公開する方法を説明します。

## 前提条件 {#prerequisites}

Before performing any of the steps described below, review and implement the guidance in [Assets performance tuning tips](performance-tuning-guidelines.md). 最大同時ジョブ数の設定など、多くの手順を実行すると、読み込み中のサーバーの安定性とパフォーマンスが向上します。 システムにアセットが読み込まれた後は、ファイルデータストアの設定など、他の手順を実行するのは困難です。

>[!NOTE]
>
>次のアセット移行ツールは、Adobe Experience Managerには含まれていません。 アドビカスタマーケアはこれらのツールをサポートしていません。
>
>* ACS AEM ツールの Tag Maker
>* ACS AEM ツールの CSV Asset Importer
>* ACS Commons の Bulk Workflow Manager
>* ACS Commons の Fast Action Manager
>* 合成ワークフロー
>
>
このソフトウェアはオープンソースで、[Apache v2 License](https://adobe-consulting-services.github.io/pages/license.html) が適用されます。質問や問題を報告するには、それぞれ [ACS AEM ツール](https://github.com/Adobe-Consulting-Services/acs-aem-commons/issues)と [ACS AEM Commons に関する GitHub の問題](https://github.com/Adobe-Consulting-Services/acs-aem-tools/issues)を利用してください。

## AEMへの移行 {#migrate-to-aem}

AEM にアセットを移行するにはいくつかの手順を経る必要があるので、フェーズ別に処理することをお勧めします。移行のフェーズは次のとおりです。

1. ワークフローを無効化する。
1. タグを読み込む。
1. アセットを取り込む。
1. レンディションを処理する。
1. アセットをアクティベートする。
1. ワークフローを有効化する。

![chlimage_1-223](assets/chlimage_1-223.png)

### Disable workflows {#disable-workflows}

移行を開始する前に、ワークフローのランチャーを無効に `DAM Update Asset` します。 すべてのアセットをシステムに取り込んでから、ワークフローを一括で実行することをお勧めします。 移行の実行中に既に稼働中の場合は、これらのアクティビティをオフ時間に実行するようにスケジュールできます。

### Load tags {#load-tags}

画像に適用するタグ分類は既に用意されていることがあります。CSVアセットインポーターやメタデータプロファイル機能などのツールを使用すると、アセットへのタグの適用を自動化できます。 その前に、Experience Managerでタグを追加します。 The [ACS AEM Tools Tag Maker](https://adobe-consulting-services.github.io/acs-aem-tools/features/tag-maker/index.html) feature lets you populate tags by using a Microsoft Excel spreadsheet that is loaded into the system.

### Ingest assets {#ingest-assets}

アセットをシステムに取り込む際に重要なのは、パフォーマンスと安定性です。Experience Managerで多くのデータを読み込む場合は、システムのパフォーマンスが良いことを確認します。 これにより、データの追加に要する時間を最小限に抑え、システムの過負荷を回避できます。 これは、特に実稼動中のシステムで、システムのクラッシュを防ぐのに役立ちます。

システムにアセットを読み込むには、HTTP を使用したプッシュベースのアプローチと JCR の API を使用したプルベースのアプローチがあります。

#### HTTP経由でプッシュ {#push-through-http}

アドビの Managed Services チームは Glutton というツールを使用してお客様の環境にデータを読み込みます。Glutton は小さな Java アプリケーションで、AEM インスタンスのあるディレクトリから別のディレクトリにすべてのアセットを読み込みます。Glutton の代わりに、Perl スクリプトなどのツールを使用してアセットをリポジトリに投稿することもできます。

httpsをプッシュスルーするアプローチを使用する場合、主に次の2つの方法があります。

1. アセットをHTTP経由でサーバーに送信します。 これには大量のオーバーヘッドが発生し、時間もかかるので、移行に要する時間が長くなります。
1. アセットに適用する必要があるタグやカスタムメタデータがある場合、このアプローチでは、アセットを取り込んだ後にこのメタデータを適用するという、2 段階のカスタムプロセスを実行する必要がある。

アセットを取り込むもう一方のアプローチでは、ローカルファイルシステムからアセットを引っ張ってきます。ただし、プルベースのアプローチを実行する外部ドライブやネットワーク共有がサーバーにマウントされていない場合は、HTTP を通じたアセットの投稿が最適なオプションです。

#### ローカルファイルシステムからのプル {#pull-from-the-local-file-system}

[ACS AEM Tools CSV Asset Importerは](https://adobe-consulting-services.github.io/acs-aem-tools/features/csv-asset-importer/index.html) 、アセットをファイルシステムから取り込み、アセットの読み込み用のCSVファイルからアセットのメタデータを取り込みます。 AEM Asset Manager API はアセットをシステムに取り込み、設定したメタデータプロパティを適用します。アセットはネットワークファイルマウントまたは外部ドライブを介してサーバーにマウントされているのが理想です。

アセットがネットワークを介して送信されないと、全体的なパフォーマンスが大幅に向上します。 通常、この方法は、アセットをリポジトリに読み込む最も効率的な方法です。 また、ツールがメタデータの取り込みをサポートしているので、すべてのアセットとメタデータを1つの手順で読み込むこともできます。 メタデータを適用する場合は、別のツールを使用する場合など、他の手順は必要ありません。

### Process renditions {#process-renditions}

アセットをシステムに読み込んだ後、メタデータを抽出してレンディションを生成するには、DAM アセットの更新ワークフローを通じてアセットを処理する必要があります。この手順を実行する前に、DAM アセットの更新ワークフローをニーズに合わせて複製および変更する必要があります。Scene7 PTIFFの生成やInDesignサーバ統合など、初期設定のワークフローの一部の手順が必要でない場合があります。

必要に応じてワークフローを設定した後、次の2つの方法でワークフローを実行できます。

1. The simplest approach is [ACS Commons’ Bulk Workflow Manager](https://adobe-consulting-services.github.io/acs-aem-commons/features/bulk-workflow-manager.html). このツールを使用すると、クエリを実行し、クエリの結果をワークフローを通じて処理します。バッチサイズを設定するオプションも用意されています。
1. [ACS Commons の Fast Action Manager](https://adobe-consulting-services.github.io/acs-aem-commons/features/fast-action-manager.html) は [合成ワークフロー](https://adobe-consulting-services.github.io/acs-aem-commons/features/synthetic-workflow.html)と合わせて使用できます。このアプローチはより複雑ですが、AEM ワークフローエンジンのオーバーヘッドを削除し、サーバーリソースの使用を最適化します。さらに、Fast Action Manager はサーバーリソースを動的に監視し、システムに配置された読み込みをスロットリングすることでパフォーマンスを大幅に向上します。サンプルスクリプトは ACS Commons の機能ページに記載されています。

### Activate assets {#activate-assets}

パブリッシュ層のあるデプロイメントでは、アセットをパブリッシュファームにアクティベートする必要があります。アドビは 1 つ以上のパブリッシュインスタンスを実行することを推奨していますが、すべてのアセットを 1 つのパブリッシュインスタンスにレプリケートして、そのインスタンスをクローンする方法が最も効率的です。多数のアセットをアクティベートするときは、ツリーのアクティベートを実行した後に、干渉する必要がある場合があります。理由は次のとおりです。アクティブ化を実行しない場合、アイテムはSlingジョブ/イベントキューに追加されます。 このキューのサイズがだいたい 40,000 項目を超えると、処理速度が劇的に低下します。このキューのサイズが 100,000 項目を超えると、システムの安定性に影響を及ぼします。

この問題を回避するには、[Fast Action Manager](https://adobe-consulting-services.github.io/acs-aem-commons/features/fast-action-manager.html) を使用してアセットのレプリケートを管理します。これは Sling キューを使用することなく動作し、オーバーヘッドを減らすほか、ワークロードをスロットルしてサーバーのオーバーロードを防ぎます。レプリケーションの管理に FAM を使用する例は、この機能のドキュメントページに記載しています。

アセットをパブリッシュファームに移行するその他のオプションは、[vlt-rcp](https://jackrabbit.apache.org/filevault/rcp.html) または [oak-run](https://github.com/apache/jackrabbit-oak/tree/trunk/oak-run) を使用する方法です。これらは Jackrabbit の一部のツールとして提供されます。AEM インフラストラクチャのオープンソースツール [Grabbit](https://github.com/TWCable/grabbit) を使用する方法もあります。vit よりも高いパフォーマンスを発揮すると言われています。

これらのアプローチで注意すべき点は、オーサリングインスタンス上でアセットがアクティベートされていると表示されないことです。アセットのアクティベート状態を正しくフラグするには、アセットをアクティベート済みとマークする別のスクリプトも実行する必要があります。

>[!NOTE]
>
>アドビは Grabbit を管理およびサポートしません。

### Clone Publish {#clone-publish}

アセットがアクティベートされたら、パブリッシュインスタンスをクローンしてデプロイメントに必要なコピーを必要な分だけ作成できます。サーバーのクローンは比較的簡単ですが、いくつか重要な手順があります。パブリッシュをクローンするには：

1. ソースインスタンスとデータストアをバックアップします。
1. インスタンスとデータストアのバックアップを対象の場所に復元します。続く手順はすべてこの新しいインスタンスを参照します。
1. 「 `crx-quickstart/launchpad/felix` for 」でファイル・システム検索を実行しま `sling.id`す。 このファイルを削除します。
1. データストアのルートパスで、`repository-XXX` ファイルを探してすべて削除します。
1. を編集 `crx-quickstart/install/org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config` し、 `crx-quickstart/launchpad/config/org/apache/jackrabbit/oak/plugins/blob/datastore/FileDataStore.config` 新しい環境上のデータストアの場所を指定します。
1. 環境を開始します。
1. オーサー環境にあるすべてのレプリケーションエージェントが正しいパブリッシュインスタンスを指す、または新しいインスタンスのディスパッチャーのフラッシュエージェントが新しい環境の正しいディスパッチャーを参照するように設定を更新します。

### Enable workflows {#enable-workflows}

移行が完了したら、レンディションの生成とメタデータの抽出をサポートするように DAM の更新アセットワークフローのランチャーを再度有効化し、稼動中のシステムが日常的に使用できるようにします。

## AEMデプロイメント間でのアセットの移行 {#migrate-between-aem-instances}

それほど一般的ではありませんが、ある AEM インスタンスからもう一方のインスタンスに大量のデータを移行する必要があることもあります。例えば、AEM やお使いのハードウェアをアップグレードする場合や、AMS の移行などに伴い新しいデータセンターに移行する場合などです。

このケースでは、移行するアセットには既にメタデータが入力されており、レンディションは既に生成されています。インスタンス間の移動に集中することができます。AEM インスタンス間で移行するには、次の手順を実行します。

1. ワークフローの無効化：レンディションをアセットと共に移行するので、DAM Update Assetのワークフローランチャーを無効にする必要があります。

1. タグの移行：ソースAEMインスタンスに既にタグが読み込まれているので、コンテンツパッケージ内にタグを作成し、ターゲットインスタンスにパッケージをインストールできます。

1. アセットの移行：AEMインスタンス間でアセットを移動する場合は、次の2つのツールを使用することをお勧めします。

   * **Vault Remote Copy**(または `vlt rcp`)を使用すると、ネットワーク全体でvltを使用できます。 移動元と移動先のディレクトリを指定すると、vit がすべてのリポジトリデータを一方のインスタンスからダウンロードし、もう一方に読み込みます。Vlt rcp is documented at [https://jackrabbit.apache.org/filevault/rcp.html](https://jackrabbit.apache.org/filevault/rcp.html)
   * **Grabbit**。Time Warner Cable が AEM の実装のために開発した、オープンソースのコンテンツ同期ツールです。継続的なデータストリームを使用するので、vlt rcp と比較して待ち時間が少なく、vlt rcp の 2 倍から 10 倍高速であると言われています。また、Grabbit はデルタコンテンツのみの同期をサポートし、最初の移行パスが完了した後に加えられた変更を同期できます。

1. Activate assets: Follow the instructions for [activating assets](#activate-assets) documented for the initial migration to AEM.

1. 公開のコピー：新しい移行と同様に、単一の発行インスタンスを読み込んでコピーする方が、両方のノードでコンテンツをアクティブにするよりも効率的です。 [パブリッシュインスタンスのクローン](#clone-publish)を参照してください。

1. ワークフローの有効化：移行が完了したら、DAMアセットの更新ワークフローのランチャーを再度有効にして、レンディションの生成とメタデータの抽出をサポートし、日々のシステム使用を継続できるようにします。
