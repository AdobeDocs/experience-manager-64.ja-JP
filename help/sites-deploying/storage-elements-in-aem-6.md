---
title: AEM 6.4 のストレージ要素
seo-title: Storage Elements in AEM 6.4
description: AEM 6.4 で使用可能なノードストレージ実装と、リポジトリのメンテナンス方法について説明します。
seo-description: Learn about the node storage implementations available in AEM 6.4 and how to maintain the repository.
uuid: 3b018830-c42e-48e0-9b6f-cd230b02d914
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: platform
content-type: reference
discoiquuid: 0aa2c22f-32bb-4e50-8328-63ed73c0f19e
legacypath: /content/docs/en/aem/6-0/deploy/upgrade/microkernels-in-aem-6-0
exl-id: 3b1100ed-44c6-4c09-aec4-9e6670234567
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '714'
ht-degree: 65%

---

# AEM 6.4 のストレージ要素{#storage-elements-in-aem}

この記事では、以下について説明します。

* [AEM 6 のストレージの概要](/help/sites-deploying/storage-elements-in-aem-6.md#overview-of-storage-in-aem)
* [リポジトリのメンテナンス](/help/sites-deploying/storage-elements-in-aem-6.md#maintaining-the-repository)

## AEM 6 のストレージの概要 {#overview-of-storage-in-aem}

AEM 6 で最も重要な変更の 1 つは、リポジトリレベルでのイノベーションです。

現在、AEM6 には 2 つのノードストレージ実装が使用できます。Tar ストレージと MongoDB ストレージ。

### Tar ストレージ {#tar-storage}

#### 新規にインストールした AEM インスタンスと Tar ストレージの実行 {#running-a-freshly-installed-aem-instance-with-tar-storage}

>[!CAUTION]
>
>セグメントノードストアの PID は、以前のバージョンの AEM 6 の org.apache.jackrabbit.oak.**plugins**.segment.SegmentNodeStoreService から、AEM 6.3 では org.apache.jackrabbit.oak.segment.SegmentNodeStoreService に変更されました。この変更が反映されるように、必要な設定を調整してください。

デフォルトでは、AEM 6 は Tar ストレージを使用して、デフォルトの設定オプションを使用してノードとバイナリを保存します。 ストレージ設定を手動で構成するには、次の手順に従います。

1. AEM 6 quickstart jar をダウンロードし、新しいフォルダーに配置します。
1. 次を実行してAEMを解凍します。

   `java -jar cq-quickstart-6.jar -unpack`

1. インストールディレクトリ内に `crx-quickstart\install` というフォルダーを作成します。

1. 新しく作成したフォルダー内に `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.cfg` というファイルを作成します。

1. ファイルを編集し、設定オプションを設定します。 AEM Tar ストレージ実装の基盤となるセグメントノードストアでは、次のオプションを使用できます。

   * `repository.home`：リポジトリのホームのパスです。リポジトリ関連の様々なデータが格納されます。デフォルトでは、crx-quickstart/segmentstore ディレクトリにセグメントファイルが格納されます。
   * `tarmk.size`：セグメントの最大サイズ（MB 単位）です。デフォルトは 256MB です。

1. AEM を起動します。

### Mongo ストレージ {#mongo-storage}

#### 新規にインストールした AEM インスタンスと Mongo ストレージの実行 {#running-a-freshly-installed-aem-instance-with-mongo-storage}

次の手順に従って、AEM 6 を MongoDB ストレージと共に実行するように設定できます。

1. AEM 6 quickstart jar をダウンロードし、新しいフォルダーに配置します。
1. 次のコマンドを実行してAEMを解凍します。

   `java -jar cq-quickstart-6.jar -unpack`

1. MongoDB がインストールされていること、および `mongod` のインスタンスが実行されていることを確認します。詳しくは、[MongoDB のインストール](https://docs.mongodb.org/manual/installation/)を参照してください。
1. インストールディレクトリ内に `crx-quickstart\install` というフォルダーを作成します。
1. ノードストアを設定します。使用する設定の名前を持つ設定ファイルを `crx-quickstart\install` ディレクトリに作成します。

   ドキュメントノードストア（AEM の MongoDB ストレージ実装の基盤）では、`org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.cfg` というファイルを使用します。

1. ファイルを編集し、設定オプションを設定します。 以下のオプションが利用できます。

   * `mongouri`：Mongo データベースに接続するために必要な [MongoURI](https://docs.mongodb.org/manual/reference/connection-string/) です。デフォルトは `mongodb://localhost:27017` です
   * `db`：Mongo データベースの名前です。新しい AEM 6 のインストールでは、デフォルトのデータベース名として **aem-author** を使用します。
   * `cache`：キャッシュサイズ（MB 単位）です。これは DocumentNodeStore で使用される様々なキャッシュに分散されます。デフォルトは 256 です。
   * `changesSize`：Mongo で差分出力のキャッシュに使用される capped コレクションのサイズ（MB 単位）です。デフォルトは 256 です。
   * `customBlobStore`：カスタムデータストアが使用されることを示すブール値です。デフォルトは false です。

1. 使用するデータストアの PID を持つ設定ファイルを作成し、そのファイルを編集して設定オプションを設定します。詳しくは、[ノードストアとデータストアの設定](/help/sites-deploying/data-store-config.md)を参照してください。

1. 次のコマンドを実行して、AEM 6 jar を MongoDB ストレージバックエンドと共に起動します。

   ```shell
   java -jar cq-quickstart-6.jar -r crx3,crx3mongo
   ```

   **`-r`** はバックエンドの実行モードです。この例では、MongoDB サポートを指定して起動します。

#### 透明な巨大ページの無効化 {#disabling-transparent-huge-pages}

Red Hat Linux は、Transparent Huge Pages(THP) と呼ばれるメモリ管理アルゴリズムを使用します。 AEMは詳細な読み取りと書き込みを実行しますが、THP は大規模な操作に最適化されています。 このため、Tar と Mongo ストレージの両方で THP を無効にすることをお勧めします。 アルゴリズムを無効にするには、次の手順に従います。

1. `/etc/grub.conf` ファイルを任意のテキストエディターで開きます。
1. **grub.conf** ファイルに次の行を追加します。

   ```
   transparent_hugepage=never
   ```

1. 最後に、次のコマンドを実行して、設定が有効になったかどうかを確認します。

   ```
   cat /sys/kernel/mm/redhat_transparent_hugepage/enabled
   ```

   THP が無効の場合、上記のコマンドの出力は次のようになります。

   ```
   always madvise [never]
   ```

>[!NOTE]
>
>また、次のリソースも参照してください。
>
>* Red Hat Linux 上の Transparent Huge Pages について詳しくは、こちらの[記事](https://access.redhat.com/solutions/46111)を参照してください。
>* Linux のチューニングのヒントについては、こちらの[記事](https://helpx.adobe.com/experience-manager/kb/performance-tuning-tips.html)を参照してください。
>


## リポジトリのメンテナンス {#maintaining-the-repository}

リポジトリを更新するたびに、新しいコンテンツのリビジョンが作成されます。その結果、更新のたびにリポジトリのサイズが大きくなります。制御できないリポジトリの増加を避けるには、古いリビジョンをクリーンアップして、ディスクリソースを解放する必要があります。 このメンテナンス機能は、リビジョンクリーンアップと呼ばれます。リビジョンクリーンアップのメカニズムによって、ディスク領域を再利用するために、リポジトリから古いデータが削除されます。リビジョンクリーンアップについて詳しくは、[リビジョンクリーンアップのページ](/help/sites-deploying/revision-cleanup.md)を参照してください。
