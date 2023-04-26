---
title: AEM 6.4 の RDBMS サポート
seo-title: RDBMS Support in AEM 6.4
description: AEM 6.4 でのリレーショナルデータベースの永続性のサポートと、使用可能な設定オプションについて説明します。
seo-description: Learn about the relational database persistence support in AEM 6.4 and the available configuration options.
uuid: 599d3e61-99eb-4a1c-868b-52b20a615500
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.4/SITES
content-type: reference
topic-tags: deploying
discoiquuid: 56a984a5-4b7f-4a95-8a17-95d2d355bfed
feature: Configuring
exl-id: 89523bb4-e4c4-469c-802b-6fe27c816a2e
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '700'
ht-degree: 57%

---

# AEM 6.4 の RDBMS サポート{#rdbms-support-in-aem}

## 概要 {#overview}

AEMでのリレーショナルデータベース永続性のサポートは、Document Microkernel を使用して実装されます。 Document Microkernel は、MongoDB 永続性の実装にも使用される基盤です。

これは、Mongo Java API をベースとする Java API で構成されます。 BlobStore API の実装も提供されます。 デフォルトでは、BLOB はデータベースに保存されます。

実装の詳細について詳しくは、 [RDBDocumentStore](https://jackrabbit.apache.org/oak/docs/apidocs/org/apache/jackrabbit/oak/plugins/document/rdb/RDBDocumentStore.html) および [RDBBlobStore](https://jackrabbit.apache.org/oak/docs/apidocs/org/apache/jackrabbit/oak/plugins/document/rdb/RDBBlobStore.html) ドキュメント。

>[!NOTE]
>
>のサポート **PostgreSQL 9.4** また、はデモ目的でのみ提供されます。 実稼動環境では使用できません。

## サポートされるデータベース {#supported-databases}

AEM でのリレーショナルデータベースのサポートレベルについて詳しくは、[技術要件のページ](/help/sites-deploying/technical-requirements.md)を参照してください。

## 設定手順 {#configuration-steps}

リポジトリは、`DocumentNodeStoreService` OSGi サービスを設定することで作成されます。このサービスは、MongoDB に加えてリレーショナルデータベース永続性もサポートするように拡張されています。

このサービスが動作するためには、AEM でデータソースを設定する必要があります。この設定は、`org.apache.sling.datasource.DataSourceFactory.config` ファイルを通して行われます。ローカル設定内の OSGi バンドルとは別に、対応するデータベースの JDBC ドライバを指定する必要があります。

JDBC ドライバー用の OSGi バンドルの作成手順については、次を参照してください [ドキュメント](https://wiki.eclipse.org/Create_and_Export_MySQL_JDBC_driver_bundle) を Apache Sling Web サイトにコピーします。

>[!NOTE]
>
>一部の SQL ドライバーは、既に OSGi バンドルとしてパッケージ化されています。
>
>この場合は、jar ファイルを install-path/crx-quickstart/install/9にコピーします。

バンドルを配置したら、次の手順に従って、RDB 永続性を持つAEMを設定します。

1. データベースのデーモンが起動しており、AEM で使用するためのアクティブなデータベースがあることを確認します。
1. AEM 6.3 jar をインストールディレクトリにコピーします。
1. インストールディレクトリ内に `crx-quickstart\install` というフォルダーを作成します。
1. ドキュメントノードストアを設定するために、この `crx-quickstart\install` ディレクトリ内に、次の名前の設定ファイルを作成します。

   * `org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.config`

1. データソースと JDBC パラメーターを設定するために、この `crx-quickstart\install` フォルダー内に、また別の次の名前の設定ファイルを作成します。

   * `org.apache.sling.datasource.DataSourceFactory-oak.config`
   >[!NOTE]
   >
   >サポートされているそれぞれのデータベースに関するデータソース設定について詳しくは、[データソース設定オプション](/help/sites-deploying/rdbms-support-in-aem.md#data-source-configuration-options)を参照してください。

1. 次に、AEM で使用する JDBC OSGi バンドルを準備します。

   1. https://dev.mysql.com/downloads/connector/j/から ZIP アーカイブをダウンロードします。
      * バージョンは 5.1.38 以降である必要があります
   1. を抽出します。 `mysql-connector-java-version-bin.jar` （バンドル）をアーカイブから
   1. Web コンソールを使用して、バンドルをインストールして起動します。
      * に移動します。 *http://serveraddress:serverport/system/console/bundles*
      * 選択 **インストール/更新**
      * ダウンロードした ZIP アーカイブから抽出したバンドルを参照して選択します。
      * 確認する **Oracle社の MySQLcom.mysql.jdbc 用 JDBC ドライバ** がアクティブで、起動します。

1. 最後に、`crx3` および `crx3rdb` 実行モードで AEM を起動します。

   ```java
   java -jar quickstart.jar -r crx3,crx3rdb
   ```

## データソース設定オプション {#data-source-configuration-options}

AEM とデータベース永続性レイヤー間の通信のために必要になるパラメーターの設定には、`org.apache.sling.datasource.DataSourceFactory-oak.config` OSGi 設定を使用します。

以下の設定オプションを使用できます。

* `datasource.name:`データソース名。デフォルトは、`oak` です。

* `url:` JDBC で使用する必要のあるデータベースの URL 文字列。データベースタイプごとに独自の URL 文字列の形式が設定されています。詳しくは、後述の [URL 文字列の形式](/help/sites-deploying/rdbms-support-in-aem.md#url-string-formats)を参照してください。

* `driverClassName:` JDBC ドライバーのクラス名。これは、使用するデータベースと、その後接続に必要なドライバーによって異なります。AEM でサポートされるすべてのデータベースのクラス名を次に示します。

   * `org.postgresql.Driver`（PostgreSQL の場合）
   * `com.ibm.db2.jcc.DB2Driver`（DB2 用の場合）
   * `oracle.jdbc.OracleDriver`（Oracle の場合）
   * `com.mysql.jdbc.Driver`（MySQL および MariaDB、試行用）
   * c`om.microsoft.sqlserver.jdbc.SQLServerDriver`（Microsoft SQL Server の場合）（試行用）

* `username:` データベースを実行するユーザー名。

* `password:` データベースのパスワード。

### URL 文字列形式 {#url-string-formats}

データソースの設定では、使用する必要のあるデータベースタイプに応じて、異なる URL 文字列形式が使用されます。 AEMが現在サポートしているデータベースの形式を以下に示します。

* `jdbc:postgresql:databasename`（PostgreSQL の場合）

* `jdbc:db2://localhost:port/databasename`（DB2 用の場合）
* `jdbc:oracle:thin:localhost:port:SID`（Oracle の場合）
* `jdbc:mysql://localhost:3306/databasename`（MySQL および MariaDB、試行用）

*  `jdbc:sqlserver://localhost:1453;databaseName=name`（Microsoft SQL Server の場合）（試行用）

## 既知の制限事項 {#known-limitations}

単一のデータベースを持つ複数のAEMインスタンスの同時使用は RDBMS の永続性でサポートされますが、同時インストールはサポートされません。

この制限を回避するには、まず 1 つのメンバーでインストールを実行し、最初のインストールが完了した後で、他のメンバーを追加します。
