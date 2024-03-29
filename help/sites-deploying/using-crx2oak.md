---
title: CRX2Oak 移行ツールの使用
seo-title: Using the CRX2Oak Migration Tool
description: CRX2Oak 移行ツールの使用方法を説明します。
seo-description: Learn how to use the CRX2Oak migration tool.
uuid: 9b788981-4ef0-446e-81f0-c327cdd3214b
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: upgrading
content-type: reference
discoiquuid: e938bdc7-f8f5-4da5-81f6-7f60c6b4b8e6
feature: Upgrading
exl-id: 85dbc81a-a9a1-4472-ada7-ff03e2af1074
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '1279'
ht-degree: 56%

---

# CRX2Oak 移行ツールの使用{#using-the-crx-oak-migration-tool}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

## はじめに {#introduction}

CRX2Oak は、異なるリポジトリ間でデータを移行するように設計されたツールです。

Apache Jackrabbit 2 に基づく古い CQ バージョンから Oak にデータを移行するために使用でき、Oak リポジトリ間でのデータのコピーにも使用できます。

次の場所で、パブリックAdobeリポジトリから最新バージョンの crx2oak をダウンロードできます。\
[https://repo.adobe.com/nexus/content/groups/public/com/adobe/granite/crx2oak/](https://repo.adobe.com/nexus/content/groups/public/com/adobe/granite/crx2oak/)

最新バージョンの変更点と修正点の一覧については、 [CRX2Oak リリースノート](/help/release-notes/crx2oak.md).

>[!NOTE]
>
>Apache Oak とAEM永続性の主要概念について詳しくは、 [AEM Platform の概要](/help/sites-deploying/platform.md).

## 移行の使用例 {#migration-use-cases}

このツールは、次の目的で使用できます。

* 古い CQ 5 バージョンからAEM 6 への移行
* 複数の Oak リポジトリ間でのデータのコピー
* 異なる Oak MicroKernel 実装間でのデータの変換。

外部の BLOB ストア（一般的にデータストアと呼ばれます）を使用したリポジトリの移行に対するサポートは、様々な組み合わせで提供されます。 考えられる移行パスの 1 つは、外部 `FileDataStore` を使用する CRX2 リポジトリから `S3DataStore` を使用する Oak リポジトリへの移行です。

下の図に、CRX2Oak がサポートしているすべての移行の組み合わせを示します。

![chlimage_1-151](assets/chlimage_1-151.png)

## 機能 {#features}

CRX2Oak は、永続化モードの再構成を自動化する事前定義済みの移行プロファイルをユーザーが指定できる方法で、AEMのアップグレード時に呼び出されます。 これはクイックスタートモードと呼ばれます。

さらにカスタマイズが必要な場合に備えて、個別に実行することもできます。 ただし、このモードでは、変更はリポジトリに対してのみおこなわれ、AEMの追加の再設定は手動で実行する必要があります。 これはスタンドアロンモードと呼ばれます。

もう 1 つ注意すべき点は、スタンドアロンモードのデフォルト設定では、ノードストアのみが移行され、新しいリポジトリが古いバイナリストレージを再使用することです。

### 自動クイックスタートモード {#automated-quickstart-mode}

AEM 6.3 以降、CRX2Oak は、すでに使用可能なすべての移行オプションを使用して設定できる、ユーザー定義の移行プロファイルを処理できます。 これにより、高い柔軟性と、スタンドアロンモードでツールを使用している場合は使用できないAEMの設定を自動化する機能の両方が可能になります。

CRX2Oak をクイックスタートモードに切り替えるには、次のオペレーティングシステム環境変数を使用して、AEMインストールディレクトリ内の crx-quickstart フォルダーへのパスを定義する必要があります。

**UNIX ベースのシステムおよびmacOSの場合：**

```shell
export SLING_HOME="/path/to/crx-quickstart"
```

**Windows の場合：**

```shell
SET "SLING_HOME=/path/to/crx-quickstart"
```

#### サポートの再開 {#resume-support}

移行はいつでも中断でき、後で再開できます。

#### カスタマイズ可能なアップグレードロジック {#customizable-upgrade-logic}

`CommitHooks`を使用して、カスタム Java ロジックも実装できます。カスタム `RepositoryInitializer` クラスを実装して、カスタム値でリポジトリを初期化できます。

#### メモリマップ操作のサポート {#support-for-memory-mapped-operations}

CRX2Oak は、デフォルトでメモリマッピング操作もサポートします。 メモリマッピングはパフォーマンスを大幅に向上させるので、可能な限り使用する必要があります。

>[!CAUTION]
>
>ただし、Windows プラットフォームでは、メモリマッピング操作はサポートされていません。 そのため、Windows で移行を実行するときには、**--disable-mmap** パラメーターを追加することが推奨されます。

#### コンテンツの選択的移行 {#selective-migration-of-content}

デフォルトでは、このツールは`"/"`パスの下にあるリポジトリ全体を移行します。しかし、どのコンテンツを移行するかは完全に制御できます。

新しいインスタンスに不要な部分がコンテンツにある場合は、 `--exclude-path` パラメーターを使用してそのコンテンツを除外し、アップグレード手順を最適化できます。

#### パスの結合 {#path-merging}

2 つのリポジトリ間でデータをコピーする必要があり、両方のインスタンス上でコンテンツパスが異なる場合は、`--merge-path` パラメーターでコンテンツパスを定義できます。定義すると、CRX2Oak は新しいノードのみをコピー先リポジトリにコピーし、古いノードは元の場所に保持します。

![chlimage_1-152](assets/chlimage_1-152.png)

#### バージョンのサポート {#version-support}

デフォルトでは、AEMは、変更された各ノードまたはページのバージョンを作成し、リポジトリに保存します。 その後、バージョンを使用して、ページを以前の状態に復元できます。

ただし、元のページが削除されても、これらのバージョンはパージされません。 長時間使用されているリポジトリを扱う場合は、孤立したバージョンによって生じた多数の冗長なデータを移行で処理しなければならないことがあります。

このような状況に役立つ機能は、`--copy-versions` パラメーターを付加することです。このパラメーターを使用すると、リポジトリの移行またはコピー中に、バージョンノードをスキップできます。

`--copy-orphaned-versions=true` を付加して、孤立したバージョンをコピーするかどうかを選択することもできます。

特定の日付までのバージョンをコピーする場合、どちらのパラメーターも日付形式 `YYYY-MM-DD` をサポートしています。

![chlimage_1-153](assets/chlimage_1-153.png)

#### オープンソース版 {#open-source-version}

CRX2Oak のオープンソースバージョンは、oak-upgrade の形式で利用できます。 以下を除くすべての機能をサポートします。

* CRX2 サポート
* 移行プロファイルのサポート
* 自動AEM再構成のサポート

詳しくは、 [Apache ドキュメント](https://jackrabbit.apache.org/oak/docs/migration.html) を参照してください。

## パラメーター {#parameters}

### ノードストアオプション {#node-store-options}

* `--cache`：MB 単位でのキャッシュサイズ（デフォルトは `256`）

* `--mmap`：セグメントストア用のメモリマップファイルアクセスを有効化します
* `--src-password:`：ソース RDB データベースのパスワード

* `--src-user:`：ソース RDB のユーザー

* `--user`：ターゲット RDB のユーザー

* `--password`：ターゲット RDB のパスワード

### 移行オプション {#migration-options}

* `--early-shutdown`：ノードのコピー後、コミットフックの適用前に、ソース JCR2 リポジトリをシャットダウンします
* `--fail-on-error`：ソースリポジトリからノードを読み取れない場合、強制的に移行を失敗させます。
* `--ldap`：LDAP ユーザーを CQ 5.x インスタンスから Oak ベースのインスタンスに移行します。これを機能させるには、Oak 設定の ID プロバイダーを ldap という名前にする必要があります。 詳しくは、 [LDAP ドキュメント](/help/sites-administering/ldap-config.md).

* `--ldap-config:`：認証に複数の サーバーを使用していた CQ 5.x リポジトリに対しては、このパラメーターと `--ldap` パラメーターを併用します。このパラメーターを使用して、CQ 5.x の `ldap_login.conf` または `jaas.conf` 設定ファイルを指すことができます。形式は、`--ldapconfig=path/to/ldap_login.conf` です。

### バージョンストアオプション {#version-store-options}

* `--copy-orphaned-versions`：孤立したバージョンのコピーをスキップします。サポートされているパラメーターは、`true`、`false`、`yyyy-mm-dd` です。デフォルトは `true` です。

* `--copy-versions:`：バージョンストレージをコピーします。サポートされているパラメーターは、`true`、`false`、`yyyy-mm-dd` です。デフォルトは `true` です。

#### パスオプション {#path-options}

* `--include-paths:`：コピー時に含めるパスのコンマ区切りのリスト
* `--merge-paths`：コピー時に結合するパスのコンマ区切りのリスト
* `--exclude-paths:`：コピー時に除外するパスのコンマ区切りのリスト

### コピー元 BLOB ストアオプション {#source-blob-store-options}

* `--src-datastore:`：ソース `FileDataStore` として使用するデータストアディレクトリ

* `--src-fileblobstore`：ソース `FileBlobStore` として使用するデータストアディレクトリ

* `--src-s3datastore`：ソース `S3DataStore` として使用するデータストアディレクトリ

* `--src-s3config`：ソース `S3DataStore` の設定ファイル

### コピー先 BlobStore オプション {#destination-blobstore-options}

* `--datastore:`：ターゲット `FileDataStore` として使用するデータストアディレクトリ

* `--fileblobstore:`：ターゲット `FileBlobStore` として使用するデータストアディレクトリ

* `--s3datastore`：ターゲット `S3DataStore` として使用するデータストアディレクトリ

* `--s3config`：ターゲット `S3DataStore` の設定ファイル

### ヘルプオプション {#help-options}

* `-?, -h, --help:`：ヘルプ情報を表示します。

## デバッグ {#debugging}

また、移行プロセスのデバッグ情報を有効にして、プロセス中に発生する可能性のある問題のトラブルシューティングをおこなうこともできます。 有効にする方法は、ツールを実行するモードによって異なります。

<table> 
 <tbody> 
  <tr> 
   <td><strong>CRX2Oak モード</strong></td> 
   <td><strong>アクション</strong></td> 
  </tr> 
  <tr> 
   <td>クイックスタートモード</td> 
   <td>CRX2Oak を実行するときに、コマンドラインに「<strong>--log-level TRACE</strong>」オプションまたは「<strong>--log-level DEBUG </strong>」オプションを追加できます。このモードでは、ログは自動的に <strong>upgrade.log ファイル</strong>にリダイレクトされます。</td> 
  </tr> 
  <tr> 
   <td>スタンドアロンモード</td> 
   <td><p>「<strong>--trace</strong>」オプションを CRX2Oak コマンドラインに追加して、標準出力に TRACE イベントを表示します（後で検査するには、リダイレクト文字：「&gt;」または「tee」コマンドを使用してログを自分でリダイレクトする必要があります）。</p> </td> 
  </tr> 
 </tbody> 
</table>

## その他の注意点 {#other-considerations}

MongoDB 複製セットに移行する場合は、Mongo データベースへのすべての接続で、`WriteConcern` パラメーターを `2` に設定します。

次のように、接続文字列の末尾に `w=2` パラメーターを付加することによって設定できます。

```xml
java -Xmx4092m -XX:MaxPermSize=1024m -jar crx2oak.jar crx-quickstart/repository/ mongodb://localhost:27017/aem-author?replicaset=replica1&w=2
```

>[!NOTE]
>
>詳しくは、MongoDB の接続文字列に関するドキュメントで[書き込み上の懸念](https://docs.mongodb.org/manual/reference/connection-string/#write-concern-options)について参照してください。
