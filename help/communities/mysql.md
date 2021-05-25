---
title: イネーブルメント機能のための MySQL 設定
seo-title: イネーブルメント機能のための MySQL 設定
description: MySQL サーバーの接続
seo-description: MySQL サーバーの接続
uuid: e02d9404-de75-4fdb-896c-ea3f64f980a3
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.4/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 9222bc93-c231-4ac8-aa28-30d784a4ca3b
role: Administrator
exl-id: 1dfb55c2-41cb-445f-9bf8-f12ab6b8e9d8
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '1100'
ht-degree: 46%

---

# イネーブルメント機能のための MySQL 設定 {#mysql-configuration-for-enablement-features}

MySQL は、イネーブルメントリソースの SCORM 追跡データおよびレポートデータに主に使用されるリレーショナルデータベースです。ビデオの一時停止/再開の追跡など、その他の機能に関する表が含まれています。

この手順では、MySQL サーバーに接続する方法、イネーブルメントデータベースを構築する方法およびデータベースに初期データを入力する方法について説明します。

## 要件 {#requirements}

MySQL をコミュニティサイトのイネーブルメント機能用に設定する前に、以下をおこなう必要があります。

* [MySQL server](https://dev.mysql.com/downloads/mysql/) Community Serverバージョン5.6をインストールします。
   * バージョン5.7はSCORMではサポートされていません。
   * オーサーインスタンスと同じサーバーであるAEM
* すべてのAEMインスタンスに、MySQL用の[JDBCドライバー](deploy-communities.md#jdbc-driver-for-mysql)
* [MySQL workbench](https://dev.mysql.com/downloads/tools/workbench/)をインストールします
* すべてのAEMインスタンスに、[SCORMパッケージ](enablement.md#scorm)をインストールします。

## MySQL のインストール {#installing-mysql}

対象 OS の手順に従い、MySQL をダウンロードしてインストールする必要があります。

### 小文字のテーブル名  {#lower-case-table-names}

SQL では大文字と小文字が区別されます。大文字と小文字が区別されるオペレーティングシステムでは、すべてのテーブル名を小文字にする設定を含める必要があります。

例えば、Linux OS でテーブル名をすべて小文字に指定するには、

* ファイル`/etc/my.cnf`を編集
* `[mysqld]`セクションに次の行を追加します。
   `lower_case_table_names = 1`

### UTF8 文字セット {#utf-character-set}

より優れた多言語対応を実現するには、UTF8 文字セットを使用する必要があります。

以下の操作で MySQL の文字セットを UTF8 に変更します。
* mysql> SET NAMES &#39;utf8&#39;;

以下の操作で MySQL データベースをデフォルトから UTF8 に変更します。
* ファイル`/etc/my.cnf`を編集
* `[client]`セクションに次の行を追加します。
   `default-character-set=utf8`
* `[mysqld]`セクションに次の行を追加します。
   `character-set-server=utf8`

## MySQL Workbench のインストール {#installing-mysql-workbench}

MySQL Workbench には、スキーマと初期データをインストールする SQL スクリプトを実行するための UI が用意されています。

ターゲットOSの手順に従って、MySQL Workbenchをダウンロードし、インストールする必要があります。

## イネーブルメント機能のための接続 {#enablement-connection}

MySQL Workbench を初めて起動したときは（他の目的で既に使用されていない場合）、接続はまだ表示されません。

![chlimage_1-327](assets/chlimage_1-327.png)

### 新しい接続の設定 {#new-connection-settings}

1. `MySQL Connections`の右側にある「+」アイコンを選択します。
1. ダイアログ`Setup New Connection`で、オーサーAEMインスタンスとMySQLを同じサーバー上に置き、デモ用にプラットフォームに適した値を入力します。
   * 接続名: `Enablement`
   * 接続方法：`Standard (TCP/IP)`
   * Hostname：`127.0.0.1`
   * ユーザー名: `root`
   * パスワード: `no password by default`
   * デフォルトのスキーマ：`leave blank`
1. `Test Connection`を選択して、実行中のMySQLサービスへの接続を確認します

**備考**:

* デフォルトのポートは`3306`です。
* 選択した`Connection Name`は、[JDBC OSGi設定](#configure-jdbc-connections)に`datasource`名として入力されます。

#### 成功した接続 {#successful-connection}

![chlimage_1-328](assets/chlimage_1-328.png)

#### 新しい接続 Enablement {#new-enablement-connection}

![chlimage_1-329](assets/chlimage_1-329.png)

## データベースのセットアップ {#database-setup}

新しい接続 Enablement を開くと、テストスキーマとデフォルトのユーザーアカウントがあります。

![chlimage_1-330](assets/chlimage_1-330.png)

### SQL スクリプトの取得 {#obtain-sql-scripts}

SQL スクリプトを取得するには、オーサーインスタンスで CRXDE Lite を使用します。[SCORMパッケージ](deploy-communities.md#scorm)をインストールする必要があります。

1. CRXDE Lite
   * 例：[http://localhost:4502/crx/de](http://localhost:4502/crx/de)
1. `/libs/social/config/scorm/`フォルダーを展開します。
1. ダウンロード `database_scormengine.sql`
1. ダウンロード `database_scorm_integration.sql`

![chlimage_1-331](assets/chlimage_1-331.png)

スキーマをダウンロードする方法の1つは、次のとおりです。

* sqlファイルの`jcr:content`ノードを選択します。
* `jcr:data`プロパティの値はビューリンクです
* データをローカルファイルに保存するには、表示リンクを選択します

### SCORM データベースの作成 {#create-scorm-database}

作成するイネーブルメントSCORMデータベースは次のとおりです。

* name: `ScormEngineDB`
* 以下のスクリプトから作成：
   * リストとして: `database_scormengine.sql`
   * データ：`database_scorm_integration.sql`
次の手順に従います(
[](#step-open-sql-file)を開き、 [execute](#step-execute-sql-script)を実行)、各SQLスクリプトをインス [トールします](#obtain-sql-scripts) 。[](#refresh) 必要に応じて更新し、スクリプト実行の結果を確認します。

データをインストールする前にスキーマをインストールしてください。

>[!CAUTION]
>
>データベース名を変更した場合は、以下の設定で適切な名前を指定してください。
>
>* [JDBC 設定](#configure-jdbc-connections)
* [SCORM 設定](#configure-scorm)



#### 手順 1：SQL ファイルを開く {#step-open-sql-file}

MySQL Workbench で、以下の設定をおこないます。

* [ファイル]プルダウンメニューから
*  `Open SQL Script ...`
* この順序で、次のいずれかを選択します。
   1. `database_scormengine.sql`
   1. `database_scorm_integration.sql`

![chlimage_1-332](assets/chlimage_1-332.png)

#### 手順 2：SQL スクリプトの実行 {#step-execute-sql-script}

手順1で開いたファイルのWorkbenchウィンドウで、スクリプトを実行する`lightening (flash) icon`を選択します。

`database_scormengine.sql` スクリプトを実行して SCORM データベースを作成するときは、完了までに少し時間がかかる場合があります。

![chlimage_1-333](assets/chlimage_1-333.png)

#### 更新 {#refresh}

スクリプトの実行が完了したら、新しいデータベースを表示するために、`SCHEMAS` の `Navigator` セクションを更新する必要があります。以下のように、「SCHEMAS」の右側にある更新アイコンを使用します。

![chlimage_1-334](assets/chlimage_1-334.png)

#### 結果：scormenginedb {#result-scormenginedb}

SCHEMAS のインストールと更新が完了すると、**`scormenginedb`** が表示されます。

![chlimage_1-335](assets/chlimage_1-335.png)

## Configure JDBC Connections {#configure-jdbc-connections}

**Day Commons JDBC Connections Pool** の OSGi 設定では、MySQL JDBC ドライバーを設定します。

すべての AEM パブリッシュインスタンスおよびオーサーインスタンスが、同じ MySQL サーバーを指している必要があります。

MySQLをAEMとは別のサーバーで実行する場合は、JDBCコネクタの「localhost」の代わりにサーバーホスト名を指定する必要があります（[ScormEngine](#configurescormengineservice)設定を入力します）。

* 各オーサーインスタンスとパブリッシュAEMインスタンスで
* 管理者権限でサインインしています
* [Webコンソール](../../help/sites-deploying/configuring-osgi.md)にアクセスします。
   * 例： [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr)
* `Day Commons JDBC Connections Pool`
* `+`アイコンを選択して、新しい設定を作成します。

![chlimage_1-336](assets/chlimage_1-336.png)

* 次の値を入力します。
   * **[!UICONTROL JDBC ドライバークラス]**: `com.mysql.jdbc.Driver`
   * **DBC接続URIJ**: `jdbc:mysql://localhost:3306/aem63reporting` MySQLサーバーが「this」 AEMサーバーと同じでない場合は、localhostの代わりにサーバーを指定します。
   * **[!UICONTROL ユーザー名]**:rootにするか、MySQLサーバーの設定済みのユーザー名（「root」でない場合）を入力します。
   * **[!UICONTROL パスワード]**:MySQL用にパスワードが設定されていない場合は、このフィールドをクリアします。設定されていない場合は、MySQLユーザー名用に設定されたパスワードを入力します。
   * **[!UICONTROL データソース名]**:MySQL接続用に [入力した名前](#new-connection-settings)（例：「enablement」）
* 「**[!UICONTROL 保存]**」を選択します。

## SCORM の設定 {#configure-scorm}

### AEM Communities ScormEngine Service {#aem-communities-scormengine-service}

**AEM Communities ScormEngine Service** の OSGi 設定では、イネーブルメントコミュニティで MySQL サーバーを使用するために SCORM を設定します。

[SCORM パッケージ](deploy-communities.md#scorm-package)がインストールされているときは、設定が表示されます。

すべてのパブリッシュインスタンスおよびオーサーインスタンスが、同じ MySQL サーバーを指している必要があります。

MySQLをAEMとは異なるサーバーで実行する場合は、ScormEngineサービスの「localhost」の代わりにサーバーホスト名を指定する必要があります。通常は、[JDBC接続](#configure-jdbc-connections)設定から設定します。

* 各オーサーインスタンスとパブリッシュAEMインスタンスで
* 管理者権限でサインインしています
* [Webコンソール](../../help/sites-deploying/configuring-osgi.md)にアクセスします。
   * 例： [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr)
* `AEM Communities ScormEngine Service`
* 編集アイコンを選択します。
   ![chlimage_1-337](assets/chlimage_1-337.png)
* 次のパラメーター値が[JDBC接続](#configurejdbcconnectionspool)設定と一致していることを確認します。
   * **[!UICONTROL JDBC接続URI]**: `jdbc:mysql://localhost:3306/ScormEngineDB` ** ScormEngineDBは、SQLスクリプトのデフォルトのデータベース名です
   * **[!UICONTROL ユーザー名]**:rootにするか、MySQLサーバーの設定済みのユーザー名（「root」でない場合）を入力します。
   * **[!UICONTROL パスワード]**:MySQL用にパスワードが設定されていない場合は、このフィールドをクリアします。設定されていない場合は、MySQLユーザー名用に設定されたパスワードを入力します。
* 次のパラメーターについて：
   * **[!UICONTROL SCORMユーザーパスワード]**:編集しない

      内部でのみ使用されます。AEM CommunitiesがSCORMエンジンと通信する特別なサービスユーザー用です。
* 「**[!UICONTROL 保存]**」を選択します。

### Adobe Granite CSRF Filter {#adobe-granite-csrf-filter}

イネーブルメントコースがすべてのブラウザーで正しく動作するかを確認するには、Mozilla を CSRF フィルターでは確認されないユーザーエージェントとして追加する必要があります。

* 各パブリッシュAEMインスタンスで
* 管理者権限でサインインしています
* [Webコンソール](../../help/sites-deploying/configuring-osgi.md)にアクセスします。
   * 例： [http://localhost:4503/system/console/configMgr](http://localhost:4503/system/console/configMgr)
* `Adobe Granite CSRF Filter`を探します
* 編集アイコンを選択します。
   ![chlimage_1-338](assets/chlimage_1-338.png)
* `[+]`アイコンを選択して、安全なユーザーエージェントを追加します。
* Enter `Mozilla/*`
* 「**[!UICONTROL 保存]**」を選択します。
