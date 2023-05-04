---
title: SRP 用の Solr 設定
seo-title: Solr Configuration for SRP
description: 1 つの Apache Solr のインストールは、異なるコレクションを使用することで、ノードストア (Oak) と共通ストア (SRP) の間で共有できます
seo-description: An Apache Solr installation may be shared between the node store (Oak) and common store (SRP) by using different collections
uuid: 7356343d-073c-4266-bdcb-c7e999281476
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.4/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: e228f1db-91ea-4ec3-86da-06d89d74bc72
role: Admin
exl-id: b506018d-67dc-4e47-a3d8-83ae288b5d7e
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '1617'
ht-degree: 3%

---

# SRP 用の Solr 設定 {#solr-configuration-for-srp}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

## AEM Platform 用 Solr {#solr-for-aem-platform}

An [Apache Solr](https://lucene.apache.org/solr/) インストールは、 [ノードストア](../../help/sites-deploying/data-store-config.md) (Oak) および [共通店](working-with-srp.md) (SRP) 別のコレクションを使用。

Oak コレクションと SRP コレクションの両方を集中的に使用する場合は、パフォーマンス上の理由から 2 つ目の Solr をインストールすることができます。

実稼動環境の場合、 [SolrCloud モード](#solrcloud-mode) では、スタンドアロンモード（単一のローカル Solr 設定）よりも高いパフォーマンスを提供します。

### 要件 {#requirements}

Apache Solr をダウンロードしてインストールします。

* [バージョン 4.10](https://archive.apache.org/dist/lucene/solr/4.10.4/) または [バージョン 5](https://archive.apache.org/dist/lucene/solr/5.5.3/)

* Solr には Java 1.7 以降が必要です
* サービスは不要
* 実行モードの選択：

   * スタンドアロンモード
   * [SolrCloud モード](#solrcloud-mode) （実稼動環境に推奨）

* 多言語検索 (MLS) の選択

   * [標準の MLS のインストール](#installing-standard-mls)
   * [高度な MLS のインストール](#installing-advanced-mls)

## SolrCloud モード {#solrcloud-mode}

[SolrCloud](https://cwiki.apache.org/confluence/display/solr/SolrCloud) 実稼動環境では、モードをお勧めします。 SolrCloud モードで実行する場合は、多言語検索 (MLS) をインストールする前に、SolrCloud をインストールして設定する必要があります。

SolrCloud のインストール手順に従うことをお勧めします。

* 同じサーバー上の 3 つの SolrCloud ノード
* 外部の Apache ZooKeeper

メモリ使用量とガベージコレクションを調整する JVM を設定することもお勧めします。

### JVM 設定例 {#jvm-configuration-example}

```shell
JVM_OPTS="-server -Xmx2048m -XX:MaxPermSize=768M -XX:+UseConcMarkSweepGC -XX:+CMSClassUnloadingEnabled -Xloggc:../logs/gc.log -XX:+PrintGCDetails -XX:+PrintGCDateStamps -Djava.awt.headless=true"  
```

### SolrCloud 設定コマンド {#solrcloud-setup-commands}

SolrCloud モードで実行する場合は、MLS をインストールする前に、次の SolrCloud の設定コマンドを使用し、知識が必要です。

#### 1. ZooKeeper に設定をアップロードする {#upload-a-configuration-to-zookeeper}

参照:\
[https://cwiki.apache.org/confluence/display/solr/Command+Line+Utilities](https://cwiki.apache.org/confluence/display/solr/Command+Line+Utilities)

使用方法：\
sh./scripts/cloud-scripts/zkcli.sh \\
-cmd upconfig \\
-zkhost *server:port* \\
-confname *myconfig-name *\\
-solrhome *solr-home-path* \\
-confdir *config-dir*

#### 2.コレクションを作成する {#create-a-collection}

参照:\
[https://cwiki.apache.org/confluence/display/solr/Solr+Start+Script+Reference#SolrStartScriptReference-Create](https://cwiki.apache.org/confluence/display/solr/Solr+Start+Script+Reference#SolrStartScriptReference-Create)

使用方法：\
。/bin/solr 作成\\
-c *mycollection-name*\\
-d *config-dir* \\
-n *myconfig-name* \\
-p *ポート*\\
-s *破片数* \\
-rf *レプリカ数*

#### 3.コレクションを設定セットにリンクする {#link-a-collection-to-a-configuration-set}

既に ZooKeeper にアップロード済みの設定にコレクションをリンクします。

参照:\
[https://cwiki.apache.org/confluence/display/solr/Command+Line+Utilities](https://cwiki.apache.org/confluence/display/solr/Command+Line+Utilities)

使用方法：\
sh./scripts/cloud-scripts/zkcli.sh \\
-cmd linkconfig \\
-zkhost *server:port* \\
-collection *mycollection-name* \\
-confname *myconfig-name*

### 標準 MLS と高度な MLS の比較 {#comparison-of-standard-and-advanced-mls}

AEM Communitiesの多言語検索 (MLS) は、Solr プラットフォーム向けに構築されており、英語を含むすべてのサポート言語で検索を改善できます。

AEMコミュニティ用の MLS は、標準の MLS または高度な MLS として使用できます。 標準の MLS には Solr の設定のみが含まれ、プラグインやリソースファイルは除外されます。 高度な MLS はより包括的なソリューションで、Solr の設定に加えて、プラグインや関連リソースも含まれています。

標準の MLS には、次の言語のコンテンツ検索の機能強化が含まれています。

* 英語：単語の派生を一致させようとするための改良されたステマー
* 日本語：半角文字の日本語トークン化の改善

高度な MLS では、次の言語でのコンテンツ検索の機能が強化されています。

* 英語：レマチザーを使用してステマーを交換した
* ドイツ語：追加分解装置
* フランス語：追加された配信処理
* 中国語（簡体字）:よりスマートなトークン化機能を追加しました。
* 各種言語：ステマー、ストップワードリスト、および正規化器を追加しました。

高度な MLS では、すべて以下の 33 言語がサポートされています。

| アラビア語 | ドイツ語 | ノルウェー語 |
|---|---|---|
| ブルガリア語 | ギリシャ語 | ポーランド語 |
| 簡体字中国語 | ハイチ語 | ポルトガル語 |
| 中国語 (繁体) | ヘブライ語 | ルーマニア語 |
| チェコ語 | ハンガリー語 | ロシア語 |
| デンマーク語 | インドネシア語 | スロバキア語 |
| オランダ語 | イタリア語 | スロベニア語 |
| 英語 | 日本語 | スペイン語 |
| エストニア語 | 韓国語 | スウェーデン語 |
| フィンランド語 | ラトビア語 | タイ語 |
| フランス語 | リトアニア語 | トルコ語 |

#### AEM 6.1 Solr 検索、標準の MLS および高度な MLS の比較 {#comparison-of-aem-solr-search-standard-mls-and-advanced-mls}

**注意**:AEM 6.1 は、AEM 6.1 Communities FP3 以前を指します。

![chlimage_1-283](assets/chlimage_1-283.png)

### 標準の MLS のインストール {#installing-standard-mls}

SRP コレクション（MSRP または DSRP）で標準多言語検索 (MLS) をサポートするには、Solr の設定ファイルを 2 つ変更する必要があります。

* **schema.xml**
* **solrconfig.xml**

Solr 4.10 用の標準 MLS ファイル (schema.xml、solrconfig.xml)

Solr 5 用の標準の MLS ファイル (schema.xml、solrconfig.xml)

標準の MLS ファイルはAEMリポジトリに保存されます。

**注意**:Solr ファイルは msrp/フォルダーに格納されますが、DSRP 用にも格納されます（変更は必要ありません）。

**ダウンロード手順**:置換 `solrX` と `solr4` または `solr5` 適切に

1. CRXDE|Lite を使用して、

   * /libs/social/config/datastore/msrp/*solrX*/**schema.xml**
   * /libs/social/config/datastore/msrp/*solrX*/**solrconfig.xml**

1. Solr がデプロイされているローカルサーバーにダウンロード

   * を `jcr:content` ノードの `jcr:data` プロパティ
   * 選択 `view` ダウンロードを開始するには
   * ファイルが適切な名前とエンコード (UTF8) で保存されていることを確認します

1. スタンドアロンモードまたは SolrCloud モードのインストール手順に従います

#### SolrCloud モード — 標準の MLS {#solrcloud-mode-standard-mls}

1. SolrCloud モードでの Solr のインストールと設定
1. 新しい設定を準備します。

   1. 作成 *new-config-dir* 例： *solr-install-dir*/myconfig/

   1. 既存の Solr 設定ディレクトリの内容をにコピーします。 *new-config-dir*

      * Solr4 の場合：コピー *solr-install-dir*/example/solr/collection1/conf/ast;
      * Solr5 の場合：コピー *solr-install-dir*/server/solr/configsets/data_driven_schema_configs/&amp;ast;
   1. ダウンロードした **schema.xml** および **solrconfig.xml** から *new-config-dir* 既存のファイルを上書きするには


1. [新しい設定をアップロード](#upload-a-configuration-to-zookeeper) ZooKeeper へ
1. [コレクションの作成](#create-a-collection) 必要なパラメータ（シャードの数、レプリカの数、構成名など）の指定
1. コレクションの作成時に設定名が指定されていなかった場合、 [この新しく作成したコレクションをリンク](#link-a-collection-to-a-configuration-set) 設定が ZooKeeper にアップロードされている

1. MSRP の場合は、を実行します。 [MSRP インデックス再作成ツール](msrp.md#msrp-reindex-tool)（これが新しいインストールでない場合）

#### スタンドアロンモード — 標準の MLS {#standalone-mode-standard-mls}

1. スタンドアロンモードでの Solr のインストール
1. Solr5 を実行する場合は、（Solr4 と同様に）collection1 を作成します。

   * 。/bin/solr start
   * 。/bin/solr create_core -c collection1 -d sample_techproducts_configs

1. バックアップ **schema.xml** および **solrconfig.xml** Solr の config ディレクトリに次のように入力します。

   * Solr4 の場合： *solr-install-dir*/example/solr/collection1/conf/
   * Solr5 用に作成： *solr-install-dir*/server/solr/collection1/conf/

1. ダウンロードした **schema.xml** および **solrconfig.xml** 同じディレクトリに

1. Solr を再起動
1. MSRP の場合は、を実行します。 [MSRP インデックス再作成ツール](#msrpreindextool)（これが新しいインストールでない場合）

### 高度な MLS のインストール {#installing-advanced-mls}

高度な MLS をサポートする SRP コレクション（MSRP または DSRP）の場合、カスタムスキーマと Solr 設定に加えて、新しい Solr プラグインが必要です。 必要な項目はすべて、ダウンロード可能な zip ファイルにパッケージ化されます。 また、Solr がスタンドアロンモードでデプロイされる場合に使用するインストールスクリプトも含まれています。

高度な MLS パッケージを入手するには、 [高度な MLS のAEM](deploy-communities.md#aem-advanced-mls) （ドキュメントのデプロイ節）を参照してください。

SolrCloud またはスタンドアロンモードでインストールを開始するには、次の手順を実行します。

* AEM-SOLR-MLS zip アーカイブを Solr をホストするサーバーにダウンロードします。
* アーカイブを解凍します。

#### SolrCloud モード — 高度な MLS {#solrcloud-mode-advanced-mls}

インストール手順 — Solr4 と Solr5 のいくつかの違いに注意してください。

1. SolrCloud モードでの Solr のインストールと設定
1. 高度な MLS パッケージの内容をディスクに抽出します。 内容は次のとおりです。

   * **schema.xml**
   * **solrconfig.xml**
   * **ストップワード** フォルダー
   * **プロファイル/** フォルダー
   * **extra-libs/** フォルダー

1. 新しい設定を準備します。

   1. の作成 *new-config-dir*

      * 例： *solr-install-dir*/myconfig/
      * サブフォルダーの stopwords/と lang/を作成する
   1. 既存の Solr config dir の内容をにコピーします。 *new-config-dir*

      * Solr4 の場合：コピー *solr-install-dir*/example/solr/collection1/conf/ast;
      * Solr5 の場合：コピー *solr-install-dir*/server/solr/configsets/data_driven_schema_configs/&amp;ast;
   1. 抽出した **schema.xml** および **solrconfig.xml** から *new-config-dir* 既存のファイルを上書きするには
   1. Solr5 の場合：コピー *solr_install_dir*/server/solr/configsets/sample_techproducts_configs/conf/lang/&amp;ast;.txt&quot;を *new-config-dir*/lang/
   1. 抽出した **ストップワード** フォルダー *new-config-dir* 結果として *new-config-dir*/stopwords/&amp;ast;.txt



1. [新しい設定をアップロード](#upload-a-configuration-to-zookeeper) ZooKeeper へ
1. 新しい **プロファイル/** フォルダー…

   * Solr4 の場合：各ノードの resources/フォルダーにコピーします。
   * Solr5 の場合：各 Solr インストールの server/resources/フォルダーにをコピーします。 すべてのノードが同じ Solr インストールディレクトリにある場合、この手順は 1 回だけ実行されます。

1. の作成 **lib/** SolrCloud の各ノードの solr-home ディレクトリ（solr.xml を含む）内のフォルダー。 次の場所の jar を各ノードの新しい lib/フォルダーにコピーします。

   * **extra-libs/** 高度な MLS パッケージから抽出される
   * *solr-install-dir/contrib/extraction/lib/*.jar
   * *solr-install-dir/dist/solr-cell*.jar
   * *solr-install-dir/contrib/clustering/lib/*.jar
   * *solr-install-dir/dist/solr-clustering*.jar
   * *solr-install-dir/contrib/langid/lib/*.jar
   * *solr-install-dir/dist/solr-langid*.jar
   * *solr-install-dir/contrib/velocity/lib/*.jar
   * *solr-install-dir/dist/solr-velocity*.jar
   * *solr-install-dir/contrib/analysis-extras/lib/*.jar
   * *solr-install-dir/contrib/analysis-extras/lucene-libs/*.jar

1. [コレクションの作成](#create-a-collection) 必要なパラメータ（シャードの数、レプリカの数、構成名など）の指定
1. 設定名が *not* コレクションの作成時に提供されます。 [この新しく作成したコレクションをリンク](#link-a-collection-to-a-configuration-set) 設定が ZooKeeper にアップロードされている

1. MSRP の場合は、を実行します。 [MSRP インデックス再作成ツール](#msrpreindextool)（これが新しいインストールでない場合）

#### スタンドアロンモード — 高度な MLS {#standalone-mode-advanced-mls}

高度な MLS パッケージには、インストールスクリプトが含まれています。

パッケージの内容がスタンドアロンの Solr サーバーをホストするサーバーに抽出されたら、必要なリソースと設定ファイルをインストールするために、インストールスクリプトを実行します。

* スタンドアロンモードでの Solr のインストール
* Solr5 を実行する場合は、（Solr4 と同様に）collection1 を作成します。

   * 。/bin/solr start
   * 。/bin/solr create_core -c collection1 -d sample_techproducts_configs

* インストールスクリプトを実行します。インストール [-v 4|5] [-d solhome] [-c collectionpath]
場所：

   * -d solhome

      Solr インストールディレクトリ

   * -c collectionpath

      solr 内のコレクションパス

   * --help

      印刷コマンドラインオプション

   * -v [4|5]

      solr のバージョンを設定

* Solr 4.10.4の例：

   * Install.bat -v 4 -d c:/solr-4.10.4 -c:/solr-4.10.4/example/solr/collection1

* Solr 5.4.0 の場合の例：

   * Install.sh -v 5 -d /tmp/solr-5.4.0 -c /tmp/solr-5.4.0/server/solr/collection1

**メモ**：

* インストールスクリプトは、新しいバージョンをインストールする前に、&quot;.orig&quot;を追加して schema.xml と solrconfig.xml をバックアップします。

### solrconfig.xml について {#about-solrconfig-xml}

この **solrconfig.xml** ファイルは自動コミット間隔と検索の表示を制御し、テストと調整が必要です。

&lt;autocommit>:既定では、安定した記憶域に対するハードコミットである AutoCommit 間隔は 15 秒に設定されています。 検索表示のデフォルト値は、コミット前のインデックスを使用する。

検索を変更して、コミットによる変更を反映するように更新されたインデックスを使用するには、含まれる &lt;opensearcher> を true に設定します。

&lt;autosoftcommit>:「ソフト」コミットでは、変更が表示される（インデックスが更新される）ことを確認しますが、変更が安定したストレージ（ハードコミット）に同期されることは確認されません。 その結果、パフォーマンスが向上します。 デフォルトでは、 &lt;autosoftcommit> が含まれると無効になります &lt;maxtime> -1 に設定します。
