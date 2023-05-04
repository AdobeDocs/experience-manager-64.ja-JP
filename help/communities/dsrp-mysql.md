---
title: DSRP 向け MySQL 設定
seo-title: MySQL Configuration for DSRP
description: MySQL サーバーに接続し、UGC データベースを確立する方法
seo-description: How to connect to the MySQL server and establish the UGC database
uuid: c058cc88-7ca2-4aed-9a36-b080e603f886
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.4/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: edc3043c-7ec4-4e4a-b008-95f1784f012e
role: Admin
exl-id: 1de1ffc6-63f8-4316-a2fa-5095d407c265
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '759'
ht-degree: 6%

---

# DSRP 向け MySQL 設定 {#mysql-configuration-for-dsrp}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

MySQL は、ユーザー生成コンテンツ (UGC) の保存に使用できるリレーショナルデータベースです。

以下の手順では、MySQL サーバーに接続し、UGC データベースを確立する方法を説明します。

## 要件 {#requirements}

* [最新のコミュニティ機能パック](deploy-communities.md#latestfeaturepack)
* [MySQL 用 JDBC ドライバー](deploy-communities.md#jdbc-driver-for-mysql)
* リレーショナルデータベース：

   * [MySQL サーバー](https://dev.mysql.com/downloads/mysql/) Community Server バージョン 5.6 以降

      * AEMと同じホスト上で実行するか、リモートで実行できます
   * [MySQL workbench](https://dev.mysql.com/downloads/tools/workbench/)


## MySQL のインストール {#installing-mysql}

[MySQL](https://dev.mysql.com/downloads/mysql/) ターゲット OS の指示に従って、をダウンロードしてインストールする必要があります。

### 小文字のテーブル名 {#lower-case-table-names}

SQL では大文字と小文字が区別されないので、大文字と小文字が区別されるオペレーティングシステムでは、すべてのテーブル名を小文字にする設定を含める必要があります。

例えば、Linux OS ですべての小文字テーブル名を指定するには、次のようにします。

* ファイルを編集 `/etc/my.cnf`
* 内 `[mysqld]` セクションで、次の行を追加します。

   `lower_case_table_names = 1`

### UTF8 文字セット {#utf-character-set}

より多言語サポートを提供するには、UTF8 文字セットを使用する必要があります。

MySQL を UTF8 の文字セットに変更します。

* mysql> SET NAMES &#39;utf8&#39;;

MySQL データベースをデフォルトの UTF8 に変更します。

* ファイルを編集 `/etc/my.cnf`
* 内 `[client]` セクションで、次の行を追加します。

   `default-character-set=utf8`

* 内 `[mysqld]` セクションで、次の行を追加します。

   `character-set-server=utf8`

## MySQL Workbench のインストール {#installing-mysql-workbench}

MySQL Workbench には、スキーマと初期データをインストールする SQL スクリプトを実行するための UI が用意されています。

ターゲット OS の手順に従って、MySQL Workbench をダウンロードし、インストールする必要があります。

## Communities Connection {#communities-connection}

MySQL Workbench を初めて起動したときは、他の目的で既に使用されている場合を除き、接続はまだ表示されません。

![chlimage_1-104](assets/chlimage_1-104.png)

### 新しい接続設定 {#new-connection-settings}

1. を選択します。 `+` 右のアイコン `MySQL Connections`.
1. ダイアログ内 `Setup New Connection`、使用するプラットフォームに適した値を入力

   デモ用に、オーサーAEMインスタンスと MySQL を同じサーバー上に配置します。

   * 接続名： `Communities`
   * 接続方法： `Standard (TCP/IP)`
   * ホスト名： `127.0.0.1`
   * ユーザー名：`root`
   * パスワード：`no password by default`
   * デフォルトのスキーマ： `leave blank`

1. 選択 `Test Connection` 実行中の MySQL サービスへの接続を検証するには、以下を実行します。

**備考**:

* デフォルトのポートは `3306`
* 選択した接続名が、データソース名としてに入力されます。 [JDBC OSGi 設定](#configurejdbcconnections)

#### 新規コミュニティ連携 {#new-communities-connection}

![chlimage_1-105](assets/chlimage_1-105.png)

## データベース設定 {#database-setup}

データベースをインストールするには、コミュニティ接続を開きます。

![chlimage_1-106](assets/chlimage_1-106.png)

### SQL スクリプトの取得 {#obtain-the-sql-script}

SQL スクリプトはAEMリポジトリから取得されます。

1. 参照してCRXDE Lite

   * 例： [http://localhost:4502/crx/de](http://localhost:4502/crx/de)

1. /libs/social/config/datastore/dsrp/schema フォルダーを選択します。
1. ダウンロード `init-schema.sql`

![chlimage_1-107](assets/chlimage_1-107.png)

スキーマをダウンロードする方法の 1 つは、次の操作です。

* を選択します。 `jcr:content`sql ファイルのノード
* の値 `jcr:data`プロパティは表示リンクです

* データをローカルファイルに保存するには、表示リンクを選択します

### DSRP データベースの作成 {#create-the-dsrp-database}

以下の手順に従って、データベースをインストールします。 データベースのデフォルト名はです。 `communities`.

スクリプト内でデータベース名を変更する場合は、 [JDBC 設定](#configurejdbcconnections).

#### 手順 1:SQL ファイルを開く {#step-open-sql-file}

MySQL Workbench 内

* [ ファイル ] プルダウンメニューから
* ダウンロードした `init_schema.sql`

![chlimage_1-108](assets/chlimage_1-108.png)

#### 手順 2:SQL スクリプトを実行 {#step-execute-sql-script}

手順 1 で開いたファイルの Workbench ウィンドウで、 `lightening (flash) icon` スクリプトを実行します。

次の画像では、 `init_schema.sql` ファイルを実行する準備が整いました：

![chlimage_1-109](assets/chlimage_1-109.png)

#### 更新 {#refresh}

スクリプトを実行した後は、 `SCHEMAS`セクション `Navigator` 新しいデータベースを確認するために。 「スキーマ」の右にある更新アイコンを使用します。

![chlimage_1-110](assets/chlimage_1-110.png)

## JDBC 接続の設定 {#configure-jdbc-connection}

の OSGi 設定 **Day Commons JDBC Connections Pool** MySQL JDBC ドライバーを設定します。

すべてのパブリッシュインスタンスとオーサーAEMインスタンスは、同じ MySQL サーバーを指す必要があります。

MySQL をAEMとは異なるサーバーで実行する場合は、JDBC コネクタの「localhost」の代わりにサーバーホスト名を指定する必要があります。

* 各オーサーおよびパブリッシュAEMインスタンスで
* 管理者権限でサインインしています
* 次にアクセス： [web コンソール](../../help/sites-deploying/configuring-osgi.md)

   * 例： [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr)

* を `Day Commons JDBC Connections Pool`
* を選択します。 `+` 新しい接続設定を作成するアイコン

![chlimage_1-111](assets/chlimage_1-111.png)

* 次の値を入力します。

   * **[!UICONTROL JDBC driver class]**: `com.mysql.jdbc.Driver`
   * **[!UICONTROL JDBC 接続 URI]**: `jdbc:mysql://localhost:3306/communities?characterEncoding=UTF-8`

      MySQL サーバーが「this」AEMサーバーと同じでない場合は、localhost の代わりにサーバーを指定します

      *コミュニティ* はデフォルトのデータベース（スキーマ）名です

   * **[!UICONTROL ユーザー名]**: `root`

      MySQL サーバーに設定されているユーザー名（「root」でない場合）を入力します。

   * **[!UICONTROL パスワード]**:

      MySQL のパスワードが設定されていない場合は、このフィールドをクリアします。

      「 」を選択しない場合は、MySQL ユーザー名用に設定したパスワードを入力します。
   * **[!UICONTROL データソース名]**:次に対して入力された名前： [MySQL 接続](#new-connection-settings)例： 「コミュニティ」

* 「**[!UICONTROL 保存]**」を選択します
