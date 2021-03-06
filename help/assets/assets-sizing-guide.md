---
title: Assets サイジングガイド
description: '導入に必要なインフラストラクチャとリソースの見積もりに効率的な指標を決定するためのベストプラクティス [!DNL Experience Manager] アセット。 '
uuid: f847c07d-2a38-427a-9c38-8cdca3a1210c
contentOwner: AG
products: SG_EXPERIENCEMANAGER/6.4/ASSETS
discoiquuid: 82c1725e-a092-42e2-a43b-72f2af3a8e04
feature: Asset Management
role: Architect,Admin
exl-id: 6115e5e8-9cf5-417c-91b3-0c0c9c278b5b
source-git-commit: de5632ff0ee87a4ded88e792b57e818baf4c01a3
workflow-type: tm+mt
source-wordcount: '1840'
ht-degree: 73%

---

# Assets サイジングガイド {#assets-sizing-guide}

Adobe Experience Manager Assets 実装の環境をサイズ設定する場合は、ディスク、CPU、メモリ、IO、ネットワークスループットなどのリソースに十分な空きがあることを確認することが重要です。 これらのリソースのサイジングには、システムに読み込まれたアセットの数を理解しておく必要があります。わかりやすい指標がない場合は、ライブラリの有効期間から既存のライブラリのサイズを分割し、アセットが作成されたときの割合を見つけることができます。

## ディスク {#disk}

### データストア {#datastore}

Assets の実装に必要なディスク領域をサイジングするときによくある間違いは、システムに取り込まれる Raw 画像のサイズに基づいて計算することです。デフォルトでは、 [!DNL Experience Manager] は、元の画像に加えて 3 つのレンディションを作成し、 [!DNL Experience Manager] UI 要素 以前の実装では、これらのレンディションは取り込まれるアセットのサイズの倍と想定されていました。

ほとんどのユーザーは、既製のレンディションに加えてカスタムレンディションを定義します。レンディションに加えて、Assets では、InDesignやIllustratorなどの共通のファイルタイプからサブアセットを抽出できます。

最後に、AEM のバージョン管理機能により、アセットの複製がバージョン履歴に保存されます。パージするバージョンを頻繁に設定できます。 ただし、多くのユーザーはバージョンをシステムに長い間保持するので、ストレージ領域をさらに消費します。

これらの要素を考慮して、ユーザーのアセットを保存するための正確なストレージ領域を計算する手法が必要です。

1. システムに読み込まれるアセットのサイズと数を決定します。
1. AEM にアップロードされるアセットの代表的なサンプルを取得します。例えば、システムに PSD、JPG、AI および PDF ファイルを読み込む場合、各ファイル形式の複数のサンプル画像が必要です。また、これらのサンプルは異なるファイルサイズや画像が混在する中で代表的なものである必要があります。
1. 使用するレンディションを定義します。
1. でのレンディションの作成 [!DNL Experience Manager] ImageMagick またはAdobeのCreative Cloudアプリケーション ユーザーが指定したレンディションに加えて、既製のレンディションを作成します。Dynamic Media Classicを実装するユーザーは、IC バイナリを使用してAEMに保存する PTIFF レンディションを生成できます。
1. サブアセットを使用する場合は、適切なファイルタイプに合わせて生成します。InDesign のファイルからサブアセットのページを生成する、または Illustrator のレイヤーから PNG ファイルや PDF ファイルを生成する方法については、オンラインドキュメントを参照してください。
1. 出力された画像、レンディションおよびサブアセットのサイズを元の画像と比較します。これにより、システムの読み込み時に予想される成長率を生成できます。 例えば、1 GB のアセットを処理した後に合計サイズが 3 GB のレンディションとサブアセットを生成した場合、レンディションの拡張係数は 3 です。
1. アセットのバージョンがシステムで管理される最大時間を決定します。
1. 既存のアセットがシステムで変更される頻度を決定します。If [!DNL Experience Manager] は、クリエイティブワークフローのコラボレーションハブとして使用され、変更の量が多くなります。 完了したアセットのみがシステムにアップロードされる場合、この数はかなり少なくなります。
1. 毎月システムに読み込まれるアセットの数を決定します。正しい数字がわからない場合は、現在使用できるアセットの数を確認し、その数を最も古いアセットの年齢で除算して、おおよその数を計算します。

ステップ 1 から 9 を実行することで、次の数を決定できます。

* 読み込まれるアセットの Raw サイズ
* 読み込まれるアセットの数
* レンディションの拡張係数
* 月ごとのアセットの変更回数
* アセットのバージョンを管理する月数
* 月ごとに読み込まれる新しいアセットの数
* 空き容量を割り当てる対象の成長年数

これらの数を「ネットワークサイジング」スプレッドシートに指定してデータストアに必要な空き容量の合計を決定できます。また、内でアセットのバージョンを管理したりアセットを変更したりした場合の影響を判断するのに便利なツールです。 [!DNL Experience Manager] ディスクの増大時に

ツールに取り込まれているサンプルデータは、前述のステップを実行することの重要性を示しています。データストアのサイズを読み込まれる Raw 画像のみを基準に設定（1 TB）すると、係数が 15 になり、リポジトリサイズが少なく見積もられることがあります。

[ファイルを入手](assets/disk_sizing_tool.xlsx)

### 共有データストア {#shared-datastores}

大規模なデータストアの場合、ネットワークに接続されたドライブ上の共有ファイルデータストアを介して、または S3 データストアを介して、共有データストアを実装できます。 この場合、個々のインスタンスでバイナリのコピーを管理する必要がありません。また、共有データストはバイナリなしのレプリケーションを可能にし、パブリッシュ環境へのアセットのレプリケートやインスタンスのオフロードに使用される帯域幅を減らすのに役立ちます。

#### ユースケース {#use-cases}

データストアはプライマリとスタンバイのオーサーインスタンス間で共有し、プライマリインスタンスで加えられた変更をスタンバイインスタンスで更新するのにかかる時間を最小化できます。ワークフローのオフロードでオーバーヘッドを減らすように、プライマリのオーサーインスタンスとオフロードのオーサーインスタンス間でデータストアを共有することをお勧めします。また、オーサーインスタンスとパブリッシュインスタンス間でデータストアを共有し、レプリケーション中のトラフィックを最小化することもできます。

#### ドローバック {#drawbacks}

データストアの共有が常に推奨されるとは限りません。いくつかの落とし穴が存在します。

#### 単一障害点 {#single-point-of-failure}

共有データストアは、インフラストラクチャに単一障害点をもたらすことがあります。次のシナリオを検討してみましょう。システムにオーサーインスタンスが 1 つ、パブリッシュインスタンスが 2 つあり、それぞれ独自のデータストアがあるとします。いずれか 1 つがクラッシュしても、残りの 2 つは引き続き稼動します。ただし、データストアが共有されている場合、1 つのディスクに障害が発生すると、インフラストラクチャ全体がダウンします。このため、データストアを簡単に復元できる場所に共有データストアのバックアップが必要です。

共有データストアには AWS S3 サービスをデプロイすることをお勧めします。これにより、通常のディスクアーキテクチャと比較して、障害が発生する確率を大幅に減らします。

#### 複雑さの増加 {#increased-complexity}

共有データストアは、ガベージコレクションなどの操作を複雑にします。通常、スタンドアロンのデータストアのガベージコレクションは、1 つのクリックで開始できます。しかし、共有データストアの場合は、単一のノードで実際のコレクションを実行することに加えて、そのデータストアを使用する各メンバーでマークスイープ操作が必要になります。

AWS の操作では、EBS ボリュームの RAID アレイを構築するのではなく、（S3 を介して）1 つの中央ロケーションを実装することで、複雑さやシステム上の操作リスクが大幅に軽減されます。

#### パフォーマンス上の懸念 {#performance-concerns}

共有データストアでは、すべてのインスタンス間で共有されるネットワークにマウントされたドライブにバイナリを保存する必要があります。これらのバイナリはネットワーク経由でアクセスされるので、システムのパフォーマンスに悪影響が及びます。 ネットワーク接続やディスクアレイを高速化することで、その影響を一部軽減できます。しかし、これにはコストがかかります。AWSを操作する場合、すべてのディスクはリモートで、ネットワーク接続が必要です。 エフェメラルボリュームでは、インスタンスが開始または停止するときにデータが失われます。

#### 待ち時間 {#latency}

S3 の実装では、バックグラウンドの書き込みスレッドにより待ち時間が発生します。バックアップ手順では、この待ち時間やオフロード手順を考慮する必要があります。S3 のアセットは、オフロードジョブが開始するときに S3 に存在していない場合があります。また、バックアップを作成するときに Lucene のインデックスが未完成のままになることがあります。これには、S3 データストアに書き込まれ、別のインスタンスからアクセスされる、時間に左右されるすべてのファイルが該当します。

### ノードストア／ドキュメントストア {#node-store-document-store}

次の要素によってリソースが消費されるので、ノードストアやドキュメントストアの正確なサイジングを特定するのは困難です。

* アセットのメタデータ
* アセットのバージョン
* 監査ログ
* アーカイブされたワークフローとアクティブなワークフロー

バイナリはデータストアに保存されるので、各バイナリが空き容量を一部占有します。大部分のリポジトリのサイズは 100 GB を下回ります。ただし、最大で 1 TB のサイズの大きなリポジトリが存在することもあります。また、オフラインコンパクションを実行するには、コンパクション済みのリポジトリをコンパクション前のバージョンの横に書き直すための十分な空き容量がボリュームに必要です。経験則としては、ディスクのサイズをリポジトリの予想サイズの 1.5 倍にすることです。

リポジトリの場合は、IOPS レベルが 3000 を超える SSD またはディスクを使用します。 IOPS がパフォーマンスのボトルネックとなる可能性を排除するために、CPU の入出力待機レベルを監視して問題の兆候を早めに把握するようにしてください。

[ファイルを入手](assets/aem_environment_sizingtool.xlsx)

## ネットワーク {#network}

[!DNL Assets] には、他の多くの プロジェクトよりネットワークのパフォーマンスが重要になる使用例がいくつかあります。[!DNL Experience Manager]お客様は高速なサーバーを使用できますが、システムからアセットをアップロードおよびダウンロードするユーザーの負荷をサポートするのに十分な大きさでないネットワーク接続の場合、処理が遅くなっているように見えます。 ～へのユーザのネットワーク接続のチョークポイントを決定する良い方法がある [!DNL Experience Manager] 時刻 [[!DNL Experience Manager]  ユーザーエクスペリエンス、インスタンスのサイズ設定、ワークフローの評価およびネットワークトポロジに関するアセットの考慮事項](assets-network-considerations.md).

## WebDAV {#webdav}

次に [!DNL Experience Manager] WebDAV プロトコルの非効率性により、デスクトップアプリケーションを混在させると、ネットワークの問題がより深刻になります。

この非効率性を説明するために、アドビは OS X 上で WebDAV を使用してシステムのパフォーマンスをテストしました。3.5 MB の InDesign ファイルが開かれて編集され、変更が保存されました。以下の観察を行った。

* 操作が完了するまでに、合計で約 100 回の HTTP リクエストが生成されました
* ファイルが HTTP 経由で 4 回アップロードされました
* ファイルが HTTP 経由で 1 回ダウンロードされました
* 操作全体が完了するまでに 42 秒かかりました
* 合計で 18 MB のデータが転送されました

WebDAV を介したファイルの平均保存時間を分析したところ、帯域幅が 5～10 Mbps のレベルにまで上昇するに連れて、パフォーマンスが劇的に上昇することがわかりました。このため、システムに同時にアクセスする各ユーザーのアップロード速度は 10 Mbps 以上、帯域幅は 5～10 Mbps 以上にすることをお勧めします。

詳しくは、 [トラブルシューティング [!DNL Experience Manager] デスクトップアプリ](https://helpx.adobe.com/jp/experience-manager/kb/troubleshooting-companion-app.html).

## 制限事項 {#limitations}

実装をサイジングするときは、システムの制限事項を頭に入れておくことが重要です。提案された実装がこれらの制限を超える場合は、クリエイティブの戦略（例：アセットを複数の Assets の実装全体で分割する）を採用してください。

メモリ不足（OOM）の問題を起こす要因はファイルのサイズだけではありません。画像のサイズにも依存します。AEM を開始する際にヒープサイズを高く指定することで、OOM の問題を回避できます。

また、 `com.day.cq.dam.commons.handler.StandardImageHandler` 0 より大きい中間一時ファイルを使用するように Configuration Manager のコンポーネントを使用します。

## アセットの最大数 {#maximum-number-of-assets}

<!-- Currently, Adobe has not tested the system for loading greater than 8 million assets. There are limitations both on the number of documents that can exist in an Oak repository and the number of files that can exist in a datastore.

While the limit for the number of nodes in a repository has not been determined, assuming each asset generates roughly 30 nodes, putting the 8 million asset test at 240 million nodes from the assets alone. This does not include audit logs, archived workflows, or versions. -->

データストア内のファイル数は、ファイルシステムの制限により 21 億に制限されています。おそらくリポジトリについては、データストアの制限に到達するかなり前に、ノードが多すぎることによる問題に直面します。

レンディションが誤って生成される場合は、Camera Raw ライブラリを使用します。ただしこの場合、画像の長いほうのサイズが 65000 ピクセルを超えてはいけません。また、画像に 512 MP (512 &amp;ast;) を超える値を含めることはできません1024 &amp;ast;1024 ピクセル )&#39;です。 *アセットのサイズは取るに足らない*.

標準搭載の (OOTB) でサポートされているTIFFファイルのサイズを、 [!DNL Experience Manager] ピクセルサイズなどの追加の要因が処理に影響を与えるためです。 可能性がある [!DNL Experience Manager] では 255 MB OOTB のファイルを処理できますが、18 MB のファイルサイズは処理できません。後者のファイルの構成要素は、前者に比べて異常に多い数のピクセルなのでです。

## アセットのサイズ {#size-of-assets}

デフォルトでは、 [!DNL Experience Manager] では、最大 2 GB のファイルサイズのアセットをアップロードできます。 AEMで非常に大きなアセットをアップロードするには、 [非常に大きなアセットをアップロードするための設定](managing-video-assets.md#configuration-to-upload-video-assets-that-are-larger-than-gb).
