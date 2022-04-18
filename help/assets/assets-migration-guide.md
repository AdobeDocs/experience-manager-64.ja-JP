---
title: アセットをAdobe Experience Manager Assets に一括で移行する
description: アセットをAEMに取り込み、メタデータを適用し、レンディションを生成し、パブリッシュインスタンスに対してアクティブ化する方法。
contentOwner: AG
feature: Migration,Renditions,Asset Management
role: Architect,Admin
exl-id: 31da9f3d-460a-4b71-9ba0-7487f1b159cb
source-git-commit: 63a4304a1a10f868261eadce74a81148026390b6
workflow-type: tm+mt
source-wordcount: '1772'
ht-degree: 64%

---

# Assets 移行ガイド {#assets-migration-guide}

アセットを AEM に移行する際には、いくつかの手順を考慮する必要があります。現在のホームからアセットやメタデータを抽出する方法は、実装間で大きく異なるので、このドキュメントの範囲外です。 代わりに、このドキュメントでは、これらのアセットをAEMに取り込み、メタデータを適用し、レンディションを生成し、アセットをアクティベートまたは公開する方法について説明します。

## 前提条件 {#prerequisites}

以下の手順を実行する前に、 [Assets のパフォーマンスチューニングのヒント](performance-tuning-guidelines.md). 最大同時ジョブ数の設定など、多くの手順により、負荷時のサーバーの安定性とパフォーマンスが向上します。 システムにアセットが読み込まれた後は、ファイルデータストアの設定など、他の手順を実行するのが困難です。

>[!NOTE]
>
>次のアセット移行ツールは、Adobe Experience Managerには含まれていません。 Adobeカスタマーサポートは、これらのツールをサポートしていません。
>
>* ACS [!DNL Experience Manager] ツールタグメーカー
>* ACS [!DNL Experience Manager] ツール CSV Asset Importer
>* ACS Commons の Bulk Workflow Manager
>* ACS Commons の Fast Action Manager
>* 合成ワークフロー
>
>このソフトウェアはオープンソースで、[Apache v2 License](https://adobe-consulting-services.github.io/pages/license.html) が適用されます。質問や問題を報告するには、それぞれ [ [!DNL Experience Manager] ACS ツール](https://github.com/Adobe-Consulting-Services/acs-aem-commons/issues)と [ [!DNL Experience Manager] ACS Commons に関する GitHub の問題](https://github.com/Adobe-Consulting-Services/acs-aem-tools/issues)を利用してください。

## [!DNL Experience Manager] への移行 {#migrate-to-aem}

[!DNL Experience Manager] にアセットを移行するにはいくつかの手順を経る必要があるので、フェーズ別に処理することをお勧めします。移行のフェーズは次のとおりです。

1. ワークフローの無効化.
1. タグの読み込み.
1. アセットの取り込み.
1. レンディションの処理.
1. アセットのアクティベート.
1. ワークフローを有効化する.

![chlimage_1-223](assets/chlimage_1-223.png)

### ワークフローの無効化 {#disable-workflows}

移行を開始する前に、 `DAM Update Asset` ワークフロー。 すべてのアセットをシステムに取り込んでから、ワークフローをバッチで実行することをお勧めします。 移行の実行中に既にライブ状態になっている場合は、これらのアクティビティをスケジュールして、オフ時間に実行するように設定できます。

### タグの読み込み {#load-tags}

画像に適用するタグ分類は既に用意されていることがあります。CSV アセットインポーターやメタデータプロファイル機能などのツールを使用すると、タグをアセットに自動的に適用できます。 その前に、「Experience Manager」にタグを追加します。 [ [!DNL Experience Manager] ACS ツールの Tag Maker](https://adobe-consulting-services.github.io/acs-aem-tools/features/tag-maker/index.html) 機能を使用すると、システムに読み込まれた Microsoft Excel のスプレッドシートを使用してタグを入力できます。

### アセットの取り込み {#ingest-assets}

アセットをシステムに取り込む際に重要なのは、パフォーマンスと安定性です。Experience Managerで多数のデータを読み込む場合は、システムのパフォーマンスが良好であることを確認します。 これにより、データの追加に要する時間が最小限に抑えられ、システムの過負荷を防ぐのに役立ちます。 これは、特に、実稼動環境に既に存在するシステムで、システムのクラッシュを防ぐのに役立ちます。

システムにアセットを読み込むには、HTTP を使用したプッシュベースのアプローチと JCR の API を使用したプルベースのアプローチがあります。

#### HTTP 経由によるプッシュ {#push-through-http}

アドビの Managed Services チームは Glutton というツールを使用してお客様の環境にデータを読み込みます。Glutton は、あるディレクトリから別のディレクトリにあるすべてのアセットを読み込む、小さな Java アプリケーションです。 [!DNL Experience Manager] インスタンス。 Glutton の代わりに、Perl スクリプトなどのツールを使用してアセットをリポジトリに投稿することもできます。

HTTPS を通じたプッシュのアプローチには、主に次の 2 つの欠点があります。

1. アセットを HTTP 経由でサーバーに送信します。 これには大量のオーバーヘッドが発生し、時間もかかるので、移行に要する時間が長くなります。
1. アセットに適用する必要があるタグやカスタムメタデータがある場合、このアプローチでは、アセットを取り込んだ後にこのメタデータを適用するという、2 段階のカスタムプロセスを実行する必要がある。

アセットを取り込むもう一方のアプローチでは、ローカルファイルシステムからアセットを引っ張ってきます。ただし、プルベースのアプローチを実行する外部ドライブやネットワーク共有がサーバーにマウントされていない場合は、HTTP を通じたアセットの投稿が最適なオプションです。

#### ローカルファイルシステムからのプル {#pull-from-the-local-file-system}

この [ACS [!DNL Experience Manager] ツール CSV Asset Importer](https://adobe-consulting-services.github.io/acs-aem-tools/features/csv-asset-importer/index.html) は、ファイルシステムからアセットを、アセットメタデータをアセット読み込みの CSV ファイルから取り込みます。 この [!DNL Experience Manager] Asset Manager API は、アセットをシステムに読み込み、設定済みのメタデータプロパティを適用するために使用します。 アセットはネットワークファイルマウントまたは外部ドライブを介してサーバーにマウントされているのが理想です。

アセットがネットワークを介して送信されない場合、全体的なパフォーマンスが大幅に向上します。 通常、この方法は、アセットをリポジトリに読み込む最も効率的な方法です。 さらに、ツールがメタデータの取り込みをサポートしているので、すべてのアセットとメタデータを 1 つの手順で読み込むことができます。 別のツールを使用するなど、メタデータを適用するために他の手順は必要ありません。

### レンディションの処理 {#process-renditions}

アセットをシステムに読み込んだ後、メタデータを抽出してレンディションを生成するには、DAM アセットの更新ワークフローを通じてアセットを処理する必要があります。この手順を実行する前に、DAM アセットの更新ワークフローをニーズに合わせて複製および変更する必要があります。Dynamic Media Classic PTIFF の生成やInDesignサーバーの統合など、デフォルトのワークフローの一部の手順が不要な場合があります。

必要に応じてワークフローを設定したら、次の 2 つの方法でワークフローを実行できます。

1. 最も簡単なアプローチは、[ACS Commons の Bulk Workflow Manager](https://adobe-consulting-services.github.io/acs-aem-commons/features/bulk-workflow-manager.html) です。このツールを使用すると、クエリを実行し、クエリの結果をワークフローを通じて処理します。バッチサイズを設定するオプションも用意されています。
1. [ACS Commons の Fast Action Manager](https://adobe-consulting-services.github.io/acs-aem-commons/features/fast-action-manager.html) は[合成ワークフロー](https://adobe-consulting-services.github.io/acs-aem-commons/features/synthetic-workflow.html)と組み合わせて使用できます。このアプローチはより複雑ですが、[!DNL Experience Manager] ワークフローエンジンのオーバーヘッドを削除し、サーバーリソースの使用を最適化します。さらに、Fast Action Manager はサーバーリソースを動的に監視し、システムに配置された読み込みをスロットリングすることでパフォーマンスを大幅に向上します。サンプルスクリプトは ACS Commons の機能ページに記載されています。

### アセットのアクティベート {#activate-assets}

パブリッシュ層のあるデプロイメントでは、アセットをパブリッシュファームにアクティベートする必要があります。アドビは 1 つ以上のパブリッシュインスタンスを実行することを推奨していますが、すべてのアセットを 1 つのパブリッシュインスタンスにレプリケートして、そのインスタンスをクローンする方法が最も効率的です。多数のアセットをアクティベートするときは、ツリーのアクティベートを実行した後に、干渉する必要が生じる場合があります。理由は、アクティベートをトリガーするときに、Sling のジョブやイベントキューに項目が追加されるからです。このキューのサイズがだいたい 40,000 項目を超えると、処理速度が劇的に低下します。このキューのサイズが 100,000 項目を超えると、システムの安定性に影響を及ぼします。

この問題を回避するには、[Fast Action Manager](https://adobe-consulting-services.github.io/acs-aem-commons/features/fast-action-manager.html) を使用してアセットのレプリケートを管理します。これは Sling キューを使用することなく動作し、オーバーヘッドを減らすほか、ワークロードをスロットルしてサーバーのオーバーロードを防ぎます。レプリケーションの管理に FAM を使用する例は、この機能のドキュメントページに記載しています。

アセットをパブリッシュファームに移行するその他のオプションは、[vlt-rcp](https://jackrabbit.apache.org/filevault/rcp.html) または [oak-run](https://github.com/apache/jackrabbit-oak/tree/trunk/oak-run) を使用する方法です。これらは Jackrabbit の一部のツールとして提供されます。[!DNL Experience Manager] インフラストラクチャにオープンソースツール [Grabbit](https://github.com/TWCable/grabbit) を使用する方法もあります。vlt よりも高いパフォーマンスを発揮すると言われています。

これらのアプローチで注意すべき点は、オーサーインスタンス上でアセットがアクティベートされていると表示されないことです。アセットのアクティベート状態を正しくフラグ設定するには、アセットをアクティベート済みとマークする別のスクリプトも実行する必要があります。

>[!NOTE]
>
>アドビは Grabbit を管理およびサポートしません。

### パブリッシュをクローン化する {#clone-publish}

アセットがアクティベートされたら、パブリッシュインスタンスをクローンしてデプロイメントに必要なコピーを必要な分だけ作成できます。サーバーのクローンは比較的簡単ですが、いくつか重要な手順があります。パブリッシュをクローンするには：

1. ソースインスタンスとデータストアをバックアップします。
1. インスタンスとデータストアのバックアップを対象の場所に復元します。続く手順はすべてこの新しいインスタンスを参照します。
1. 以下でファイルシステムの検索を実行します。 `crx-quickstart/launchpad/felix` 対象 `sling.id`. このファイルを削除します。
1. データストアのルートパスで、`repository-XXX` ファイルを探してすべて削除します。
1. `crx-quickstart/install/org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config` と `crx-quickstart/launchpad/config/org/apache/jackrabbit/oak/plugins/blob/datastore/FileDataStore.config` を編集し、新しい環境のデータストアの場所を指すようにします。
1. 環境を開始します。
1. オーサー環境にあるすべてのレプリケーションエージェントが正しいパブリッシュインスタンスを指す、または新しいインスタンスの Dispatcher のフラッシュエージェントが新しい環境の正しい Dispatcher を参照するように設定を更新します。

### ワークフローを有効化する {#enable-workflows}

移行が完了したら、レンディションの生成とメタデータの抽出をサポートするように DAM の更新アセットワークフローのランチャーを再度有効化し、稼動中のシステムが日常的に使用できるようにします。

## アセットの移行 [!DNL Experience Manager] デプロイメント {#migrate-between-aem-instances}

ほとんど一般的ではありませんが、1 つから大量のデータを移行する必要が生じる場合があります [!DNL Experience Manager] 例えば別の例へ例えば、 [!DNL Experience Manager] ハードウェアのアップグレード、アップグレード、または AMS の移行など、新しいデータセンターへの移行を行います。

このケースでは、移行するアセットには既にメタデータが入力されており、レンディションは既に生成されています。インスタンス間の移動に集中することができます。次の間の移行時 [!DNL Experience Manager] インスタンスの場合は、次の手順を実行します。

1. ワークフローを無効にする：アセットと共にレンディションを移行するので、DAM アセットの更新のワークフローランチャーを無効にする必要があります。

1. タグを移行：タグは既にソースに読み込まれているので [!DNL Experience Manager] インスタンスを作成する場合は、コンテンツパッケージに組み込み、パッケージをターゲットインスタンスにインストールします。

1. アセットを移行：1 つのアセットからアセットを移動する場合に推奨されるツールは 2 つあります。 [!DNL Experience Manager] インスタンスから別のインスタンスへ：

   * **Vault リモートコピー**&#x200B;または `vlt rcp`を使用すると、ネットワークをまたいで vlt を使用できます。 移動元と移動先のディレクトリを指定すると、vit がすべてのリポジトリデータを一方のインスタンスからダウンロードし、もう一方に読み込みます。vt rcp については、[https://jackrabbit.apache.org/filevault/rcp.html](https://jackrabbit.apache.org/filevault/rcp.html) に記載されています。
   * **Grabbit**：Time Warner Cable が自社の [!DNL Experience Manager] 実装のために開発したオープンソースのコンテンツ同期ツールです。継続的なデータストリームを使用するので、vlt rcp と比較して待ち時間が少なく、vlt rcp の 2 倍から 10 倍高速であると言われています。また、Grabbit はデルタコンテンツのみの同期をサポートし、最初の移行パスが完了した後に加えられた変更を同期できます。

1. アセットのアクティベート：手順に従って、 [アセットのアクティベート](#activate-assets) AEMへの最初の移行については、を参照してください。

1. パブリッシュをクローン化する：新規の移行の場合と同様に、1 つのパブリッシュインスタンスを読み込んでクローン化する方が、両方のノードでコンテンツを有効にするよりも効率的です。[パブリッシュインスタンスのクローン](#clone-publish)を参照してください。

1. ワークフローの有効化：移行が完了したら、レンディションの生成とメタデータの抽出をサポートするように DAM アセットの更新ワークフローのランチャーを再度有効にし、稼動中のシステムが日常的に使用できるようにします。
