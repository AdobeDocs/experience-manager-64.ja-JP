---
title: イネーブルメント機能のための MySQL 設定
seo-title: MySQL Configuration for Enablement Features
description: MySQL サーバーの接続
seo-description: Connecting your MySQL server
uuid: e02d9404-de75-4fdb-896c-ea3f64f980a3
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.4/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 9222bc93-c231-4ac8-aa28-30d784a4ca3b
role: Admin
exl-id: 1dfb55c2-41cb-445f-9bf8-f12ab6b8e9d8
source-git-commit: 3c050c33a384d586d74bd641f7622989dc1d6b22
workflow-type: tm+mt
source-wordcount: '1091'
ht-degree: 46%

---

# イネーブルメント機能のための MySQL 設定 {#mysql-configuration-for-enablement-features}

MySQL は、イネーブルメントリソースの SCORM 追跡データおよびレポートデータに主に使用されるリレーショナルデータベースです。ビデオの一時停止/再開の追跡など、その他の機能に関する表が含まれています。

この手順では、MySQL サーバーに接続する方法、イネーブルメントデータベースを構築する方法およびデータベースに初期データを入力する方法について説明します。

## 要件 {#requirements}

MySQL をコミュニティサイトのイネーブルメント機能用に設定する前に、以下をおこなう必要があります。

* インストール [MySQL サーバー](https://dev.mysql.com/downloads/mysql/) Community Server バージョン 5.6
   * バージョン 5.7 は SCORM ではサポートされていません
   * オーサーAEMインスタンスと同じサーバーである可能性があります
* すべてのAEMインスタンスで、公式の [MySQL 用 JDBC ドライバー](deploy-communities.md#jdbc-driver-for-mysql)
* インストール [MySQL workbench](https://dev.mysql.com/downloads/tools/workbench/)
* すべてのAEMインスタンスで、 [SCORM パッケージ](enablement.md#scorm)

## MySQL のインストール {#installing-mysql}

対象 OS の手順に従い、MySQL をダウンロードしてインストールする必要があります。

### 小文字のテーブル名 {#lower-case-table-names}

SQL では大文字と小文字が区別されます。大文字と小文字が区別されるオペレーティングシステムでは、すべてのテーブル名を小文字にする設定を含める必要があります。

例えば、Linux OS でテーブル名をすべて小文字に指定するには、

* ファイルを編集 `/etc/my.cnf`
* 内 `[mysqld]` セクションで、次の行を追加します。
   `lower_case_table_names = 1`

### UTF8 文字セット {#utf-character-set}

より優れた多言語対応を実現するには、UTF8 文字セットを使用する必要があります。

以下の操作で MySQL の文字セットを UTF8 に変更します。
* mysql> SET NAMES &#39;utf8&#39;;

以下の操作で MySQL データベースをデフォルトから UTF8 に変更します。
* ファイルを編集 `/etc/my.cnf`
* 内 `[client]` セクションで、次の行を追加します。
   `default-character-set=utf8`
* 内 `[mysqld]` セクションで、次の行を追加します。
   `character-set-server=utf8`

## MySQL Workbench のインストール {#installing-mysql-workbench}

MySQL Workbench には、スキーマと初期データをインストールする SQL スクリプトを実行するための UI が用意されています。

ターゲット OS の手順に従って、MySQL Workbench をダウンロードし、インストールする必要があります。

## イネーブルメント機能のための接続 {#enablement-connection}

MySQL Workbench を初めて起動したときは（他の目的で既に使用されていない場合）、接続はまだ表示されません。

![chlimage_1-327](assets/chlimage_1-327.png)

### 新しい接続の設定 {#new-connection-settings}

1. の右にある「+」アイコンを選択します。 `MySQL Connections`.
1. ダイアログ内 `Setup New Connection`を使用する場合は、プラットフォームのデモ用に適切な値を入力します。オーサーAEMインスタンスと MySQL を同じサーバー上に置きます。
   * 接続名: `Enablement`
   * 接続方法： `Standard (TCP/IP)`
   * Hostname：`127.0.0.1`
   * ユーザー名: `root`
   * パスワード: `no password by default`
   * デフォルトのスキーマ： `leave blank`
1. 選択 `Test Connection` 実行中の MySQL サービスへの接続を検証するには、以下を実行します。

**備考**:

* デフォルトのポートは `3306`
* この `Connection Name` 次の項目を選択しました： `datasource` 名前を入力 [JDBC OSGi 設定](#configure-jdbc-connections)

#### 成功した接続 {#successful-connection}

![chlimage_1-328](assets/chlimage_1-328.png)

#### 新しい接続 Enablement  {#new-enablement-connection}

![chlimage_1-329](assets/chlimage_1-329.png)

## データベースのセットアップ {#database-setup}

新しい接続 Enablement を開くと、テストスキーマとデフォルトのユーザーアカウントがあります。

![chlimage_1-330](assets/chlimage_1-330.png)

### SQL スクリプトの取得 {#obtain-sql-scripts}

SQL スクリプトを取得するには、オーサーインスタンスで CRXDE Lite を使用します。この [SCORM パッケージ](deploy-communities.md#scorm) をインストールする必要があります。

1. 参照してCRXDE Lite
   * 例：[http://localhost:4502/crx/de](http://localhost:4502/crx/de)
1. を展開します。 `/libs/social/config/scorm/` フォルダー
1. ダウンロード `database_scormengine.sql`
1. ダウンロード `database_scorm_integration.sql`

![chlimage_1-331](assets/chlimage_1-331.png)

スキーマをダウンロードする方法の 1 つは、次の操作です。

* を選択します。 `jcr:content`sql ファイルのノード
* の値 `jcr:data`プロパティは表示リンクです
* データをローカルファイルに保存するには、表示リンクを選択します

### SCORM データベースの作成 {#create-scorm-database}

作成するイネーブルメント SCORM データベースは次のとおりです。

* name: `ScormEngineDB`
* 以下のスクリプトから作成：
   * リストとして: `database_scormengine.sql`
   * データ： `database_scorm_integration.sql`
以下の手順に従います (
[open](#step-open-sql-file), [execute](#step-execute-sql-script)) をインストールします。 [SQL スクリプト](#obtain-sql-scripts) . [更新](#refresh) 必要に応じて、スクリプトの実行結果を確認します。

データをインストールする前にスキーマをインストールしてください。

>[!CAUTION]
>
>データベース名を変更した場合は、以下の設定で適切な名前を指定してください。
>
>* [JDBC 設定](#configure-jdbc-connections)
>* [SCORM 設定](#configure-scorm)

>


#### Step 1 : open SQL file {#step-open-sql-file}

MySQL Workbench で、以下の設定をおこないます。

* [ ファイル ] プルダウンメニューから
*  `Open SQL Script ...`
* この順序で、次のいずれかを選択します。
   1. `database_scormengine.sql`
   1. `database_scorm_integration.sql`

![chlimage_1-332](assets/chlimage_1-332.png)

#### Step 2 : execute SQL Script {#step-execute-sql-script}

手順 1 で開いたファイルの Workbench ウィンドウで、 `lightening (flash) icon` スクリプトを実行します。

`database_scormengine.sql` スクリプトを実行して SCORM データベースを作成するときは、完了までに少し時間がかかる場合があります。

![chlimage_1-333](assets/chlimage_1-333.png)

#### 更新 {#refresh}

スクリプトの実行が完了したら、新しいデータベースを表示するために、`SCHEMAS` の `Navigator` セクションを更新する必要があります。以下のように、「SCHEMAS」の右側にある更新アイコンを使用します。

![chlimage_1-334](assets/chlimage_1-334.png)

#### 結果：scormenginedb {#result-scormenginedb}

SCHEMAS のインストールと更新が完了すると、**`scormenginedb`** が表示されます。

![chlimage_1-335](assets/chlimage_1-335.png)

## JDBC 接続の設定 {#configure-jdbc-connections}

**Day Commons JDBC Connections Pool** の OSGi 設定では、MySQL JDBC ドライバーを設定します。

すべての AEM パブリッシュインスタンスおよびオーサーインスタンスが、同じ MySQL サーバーを指している必要があります。

MySQL をAEMとは異なるサーバーで実行する場合は、JDBC コネクタの「localhost」の代わりにサーバーホスト名を指定する必要があります ( これにより、 [ScormEngine](#configurescormengineservice) 設定 ) を参照してください。

* 各オーサーおよびパブリッシュAEMインスタンスで
* 管理者権限でサインインしています
* 次にアクセス： [web コンソール](../../help/sites-deploying/configuring-osgi.md)
   * 例： [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr)
* を `Day Commons JDBC Connections Pool`
* を選択します。 `+` 新しい設定を作成するアイコン

![chlimage_1-336](assets/chlimage_1-336.png)

* 次の値を入力します。
   * **[!UICONTROL JDBC ドライバークラス]**: `com.mysql.jdbc.Driver`
   * **DBC 接続 URIJ**: `jdbc:mysql://localhost:3306/aem63reporting` MySQL サーバーが「this」AEMサーバーと同じでない場合は、localhost の代わりにサーバーを指定します
   * **[!UICONTROL ユーザー名]**:Root にするか、MySQL サーバー用に設定されたユーザー名を入力します（「root」でない場合）。
   * **[!UICONTROL パスワード]**:MySQL のパスワードが設定されていない場合はこのフィールドをクリアし、設定されていない場合は MySQL ユーザー名用に設定されたパスワードを入力します
   * **[!UICONTROL データソース名]**:次に対して入力した名前： [MySQL 接続](#new-connection-settings)（例： &#39;enablement&#39;）
* 選択 **[!UICONTROL 保存]**

## SCORM の設定 {#configure-scorm}

### AEM Communities ScormEngine Service {#aem-communities-scormengine-service}

**AEM Communities ScormEngine Service** の OSGi 設定では、イネーブルメントコミュニティで MySQL サーバーを使用するために SCORM を設定します。

[SCORM パッケージ](deploy-communities.md#scorm-package)がインストールされているときは、設定が表示されます。

すべてのパブリッシュインスタンスおよびオーサーインスタンスが、同じ MySQL サーバーを指している必要があります。

MySQL をAEMとは異なるサーバーで実行する場合は、ScormEngine サービスの「localhost」の代わりにサーバーホスト名を指定する必要があります。このホスト名は通常、 [JDBC 接続](#configure-jdbc-connections) config.

* 各オーサーおよびパブリッシュAEMインスタンスで
* 管理者権限でサインインしています
* 次にアクセス： [web コンソール](../../help/sites-deploying/configuring-osgi.md)
   * 例： [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr)
* を `AEM Communities ScormEngine Service`
* 編集アイコンを選択します。
   ![chlimage_1-337](assets/chlimage_1-337.png)
* 次のパラメータ値が [JDBC 接続](#configurejdbcconnectionspool) config:
   * **[!UICONTROL JDBC 接続 URI]**: `jdbc:mysql://localhost:3306/ScormEngineDB` *ScormEngineDB* は、SQL スクリプトのデフォルトのデータベース名です
   * **[!UICONTROL ユーザー名]**:Root にするか、MySQL サーバー用に設定されたユーザー名を入力します（「root」でない場合）。
   * **[!UICONTROL パスワード]**:MySQL のパスワードが設定されていない場合はこのフィールドをクリアし、設定されていない場合は MySQL ユーザー名用に設定されたパスワードを入力します
* 次のパラメーターに関して：
   * **[!UICONTROL Scorm ユーザーパスワード]**:編集しない

      内部でのみ使用されます。AEM Communitiesが SCORM エンジンと通信する際に使用する特別なサービスユーザー用です。
* 選択 **[!UICONTROL 保存]**

### Adobe Granite CSRF Filter {#adobe-granite-csrf-filter}

イネーブルメントコースがすべてのブラウザーで正しく動作するかを確認するには、Mozilla を CSRF フィルターでは確認されないユーザーエージェントとして追加する必要があります。

* 各パブリッシュAEMインスタンスで
* 管理者権限でサインインしています
* 次にアクセス： [web コンソール](../../help/sites-deploying/configuring-osgi.md)
   * 例： [http://localhost:4503/system/console/configMgr](http://localhost:4503/system/console/configMgr)
* 場所 `Adobe Granite CSRF Filter`
* 編集アイコンを選択します。
   ![chlimage_1-338](assets/chlimage_1-338.png)
* を選択します。 `[+]` 安全なユーザーエージェントを追加するためのアイコン
* `Mozilla/*` と入力します。
* 選択 **[!UICONTROL 保存]**
