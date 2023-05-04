---
title: Communities のデプロイ
seo-title: Deploying Communities
description: AEM Communitiesのデプロイ方法
seo-description: How to deploy AEM Communities
uuid: 1f7faf1a-a339-4eaa-b728-b9110cb350a8
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.4/COMMUNITIES
content-type: reference
topic-tags: deploying
discoiquuid: d0249609-2a9c-4d3b-92ee-dbc5fbdeaac6
exl-id: 0b7496f0-0b3c-4d12-a659-d95744157f14
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '2216'
ht-degree: 5%

---

# Communities のデプロイ {#deploying-communities}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

## 前提条件 {#prerequisites}

* [AEM 6.4 Platform](../../help/sites-deploying/deploy.md)

* AEM Communitiesライセンス

* オプションのライセンス：

   * [Adobe Analytics for Communities の機能](analytics.md)
   * [MSRP 用 MongoDB](msrp.md)
   * [ASRP 用Adobeクラウド](asrp.md)

## インストールチェックリスト {#installation-checklist}

**の [AEM platform](../../help/sites-deploying/deploy.md#what-is-aem)**

* 最新のインストール [AEM 6.4 の更新](#aem-updates)

* デフォルトのポート (4502、4503) を使用しない場合は、 [レプリケーションエージェントの設定](#replication-agents-on-author)
* [暗号鍵を複製する](#replicate-the-crypto-key)
* グローバル化を支援する場合、 [自動翻訳の設定](../../help/sites-administering/translation.md)

   （開発用のサンプル設定が用意されています）

**の [コミュニティ機能](overview.md)**

* をデプロイする場合 [パブリッシュファーム](../../help/sites-deploying/recommended-deploys.md#tarmk-farm), [主なパブリッシャーの特定](#primary-publisher)

* [トンネルサービスを有効にする](#tunnel-service-on-author)
* [ソーシャルログインを有効にする](social-login.md#adobe-granite-oauth-authentication-handler)
* [Adobe Analytics の設定](analytics.md)
* のセットアップ [デフォルトの電子メールサービス](email.md)
* 選択肢の特定 [共有 UGC ストレージ](working-with-srp.md) (**SRP**)

   * MongoDB SRP の場合 [(MSRP)](msrp.md)

      * [MongoDB のインストールと設定](msrp.md#mongodb-configuration)
      * [Solr を設定](solr.md)
      * [MSRP を選択](srp-config.md)
   * リレーショナルデータベース SRP の場合 [(DSRP)](dsrp.md)

      * [MySQL 用の JDBC ドライバーのインストール](#jdbc-driver-for-mysql)
      * [DSRP 用の MySQL のインストールと設定](dsrp-mysql.md)
      * [Solr を設定](solr.md)
      * [DSRP を選択](srp-config.md)
   * AdobeSRP の場合 [(ASRP)](asrp.md)

      * プロビジョニングについては、アカウント担当者にお問い合わせください。
      * [ASRP を選択](srp-config.md)
   * JCR SRP の場合 [(JSRP)](jsrp.md)

      * 共有 UGC ストアではありません：

         * UGC はレプリケートされません
         * UGC は、入力されたAEMインスタンスまたはクラスター上でのみ表示されます
      * デフォルトは JSRP です。

   の **[イネーブルメント機能](overview.md#enablement-community)**

   * [FFmpeg のインストールと設定](ffmpeg.md)
   * [MySQL 用の JDBC ドライバーのインストール](#jdbc-driver-for-mysql)
   * [AEM Communities SCORM-Engine のインストール](#scorm-package)
   * [イネーブルメント用に MySQL をインストールして設定](mysql.md)






## 最新リリース {#latest-releases}

AEM 6.4 Communities GA には Communities パッケージが含まれています。 AEM 6.4 の更新について知るには [コミュニティ](/help/release-notes/release-notes.md#experience-manager-communities)、を参照してください。 [AEM 6.4 リリースノート](/help/release-notes/release-notes.md#release-information).

### AEM 6.4 の更新 {#aem-updates}

AEM 6.3 以降、Communities の更新はAEM Cumulative Fix Packs および Service Pack の一部として提供されます。

AEM 6.4 の最新の更新については、 [Adobe Experience Manager 6.4 累積修正パックおよびサービスパック](https://helpx.adobe.com/jp/experience-manager/aem-releases-updates.html).

### バージョン履歴 {#version-history}

AEM 6.4 以降と同様に、AEM Communitiesの機能とホットフィックスは、AEM Communitiesの累積修正パックおよびサービスパックの一部です。 したがって、別の機能パックはありません。

### MySQL 用 JDBC ドライバー {#jdbc-driver-for-mysql}

2 つのコミュニティ機能で MySQL データベースを使用します。

* の場合 [実施可能](enablement.md):SCORM アクティビティと学習者の記録
* の場合 [DSRP](dsrp.md):ユーザー生成コンテンツ (UGC) の保存

MySQL コネクタを取得し、別途インストールする必要があります。

必要な手順は次のとおりです。

1. から ZIP アーカイブをダウンロードします。 [https://dev.mysql.com/downloads/connector/j/](https://dev.mysql.com/downloads/connector/j/)

   * バージョンは 5.1.38 以降である必要があります

1. mysql-connector-java — を抽出します&lt;version>アーカイブから —bin.jar (bundle)

1. Web コンソールを使用して、バンドルをインストールして起動します。

   * 例： http://localhost:4502/system/console/bundles
   * **`Install/Update`** を選択します。
   * ダウンロードした ZIP アーカイブから抽出したバンドルを参照して選択
   * 確認する *Oracle社の MySQLcom.mysql.jdbc 用 JDBC ドライバ* がアクティブで、アクティブでない場合は開始（またはログを確認）

1. JDBC の設定後に既存のデプロイメントにインストールする場合は、Web コンソールから JDBC 設定を再保存して、JDBC を新しいコネクタに再バインドします。

   * 例： http://localhost:4502/system/console/configMgr
   * 場所 `Day Commons JDBC Connections Pool` 設定
   * 選択して開く
   * `Save` を選択します。

1. すべてのオーサーインスタンスとパブリッシュインスタンスで、手順 3 と 4 を繰り返します。

バンドルのインストールに関する詳細は、 [Web コンソール](/help/sites-deploying/web-console.md#bundles) ページ。

#### 例：MySQL Connector バンドルがインストールされている {#example-installed-mysql-connector-bundle}

![chlimage_1-410](assets/chlimage_1-410.png)

### SCORM パッケージ {#scorm-package}

SCORM(Shareable Content Object Reference Model) は、e ラーニングの標準と仕様の集まりです。 また、SCORM では、コンテンツを転送可能な ZIP ファイルにパッケージ化する方法も定義します。

AEM Communities SCORM エンジンは、 [実施可能](overview.md#enablement-community) 機能。 AEM Communities 6.4 バージョンでサポートされる SCORM パッケージは次のとおりです。

* **[cq -social- scorm -package、バージョン 1.2.11](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq640%2Fsocial%2Fscorm%2Fcq-social-scorm-pkg)**. この SCORM パッケージは、すべてのAEM 6.4 Communities バージョンでサポートされています。

* **[cq -social- scorm -package、バージョン 2.2.2](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq640%2Fsocial%2Fscorm%2Fcq-social-scorm-2017-pkg)** 次を含む [SCORM 2017.1](https://rusticisoftware.com/blog/scorm-engine-2017-released/) エンジン。 この SCORM パッケージは、AEM 6.4.2.x Communities 以降でサポートされます。

SCORM エンジンの新規インストールの場合、次のパッケージが含まれます。 [SCORM 2017.1](https://rusticisoftware.com/blog/scorm-engine-2017-released/) ( [  cq -social- scorm -package、バージョン 2.2.2](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq640%2Fsocial%2Fscorm%2Fcq-social-scorm-2017-pkg)) を使用する必要があります。 SCORM 2017 でサポートされる学習リソースを再生できます。

<!--This section used to be an accordion until converted to straight Markdown. When accordions are enabled, revert-->

### SCORM パッケージを初めてインストールするには

1. のインストール **[cq-social-scorm-package，バージョン 2.2.2](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq640%2Fsocial%2Fscorm%2Fcq-social-scorm-2017-pkg).**
1. ダウンロード **`/libs/social/config/scorm/database_scormengine_data.sql`** cq インスタンスから、mysql サーバーで実行して、アップグレードされた scormEngineDB スキーマを作成します。
1. 追加 `/content/communities/scorm/RecordResults` CSRF フィルターの Excluded Paths プロパティの `https://<hostname>;:<port>/system/console/configMgr` （発行者）

既存の SCORM インストールをにアップグレードできます [**cq-social-scorm-package，バージョン 2.2.2**](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq640%2Fsocial%2Fscorm%2Fcq-social-scorm-2017-pkg) ( [SCORM 2017.1](https://rusticisoftware.com/blog/scorm-engine-2017-released/))、作成したコースコンテンツに SCORM 2017.1 が必要な場合。

>[!NOTE]
>
>SCORM 2017.1 パッケージにアップグレードするには、既存のデータベースを移行する必要があります（詳しくは、後述）。

<!--This section used to be an accordion until converted to straight Markdown. When accordions are enabled, revert-->

### SCORM エンジンのバージョンをアップグレードするには

1. ScormEngineDB スキーマのバックアップを作成します。
1. のインストール **[cq-social-scorm-package，バージョン 2.2.2](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq640%2Fsocial%2Fscorm%2Fcq-social-scorm-2017-pkg).**
1. パッケージのダウンロード元 `/libs/social/config/scorm/ScormEngine.zip` 同じものを抽出します。
1. に移動します。 **インストーラー** 抽出したディレクトリのフォルダ。
1. 更新 `SystemDatabaseConnectionString` を `scorm db connection url` ファイル内 **[!UICONTROL EngineInstall.xml]**.
1. 次のコマンドを使用して、Installer フォルダー内の mysql スキーマアップグレードツールを実行します。

   `java -Dlogback.configurationFile=logback.xml -cp "lib/*" RusticiSoftware.ScormContentPlayer.Logic.Upgrade.ConsoleApp EngineInstall.xml`
1. 監視 `engine_upgrade.log` ファイルに含まれる必要があります。
1. 追加 `/content/communities/scorm/RecordResults` in **[!UICONTROL 除外されたパス]** 次のプロパティを CSRF フィルターで使用 `https://<hostname>:<port>/system/console/configMgr` （発行者）

### SCORM ログ {#scorm-logging}

インストールすると、すべてのイネーブルメントアクティビティがシステムコンソールに完全に記録されます。

必要に応じて、ログレベルを `RusticiSoftware.*` パッケージ。

ログの操作については、 [監査レコードとログファイルの操作](../../help/sites-deploying/monitoring-and-maintaining.md#working-with-audit-records-and-log-files).

### 高度な MLS のAEM {#aem-advanced-mls}

高度な多言語検索 (MLS) をサポートする SRP コレクション（MSRP または DSRP）については、カスタムスキーマと Solr 設定に加えて、新しい Solr プラグインが必要です。 必要な項目はすべて、ダウンロード可能な zip ファイルにパッケージ化されます。

高度な MLS のダウンロード（「phasetwo」とも呼ばれます）は、Adobeリポジトリから入手できます。

* AEM-SOLR-MLS-phasetwo

   高度な MLS パッケージを入手するには、 [高度な MLS のAEM](deploy-communities.md#aem-advanced-mls) （ドキュメントのデプロイ節）を参照してください。

   * バージョン 1.2.40、2016 年 4 月 7 日
   * AEM-SOLR-MLS-phasetwo-1.2.40.zip をダウンロードします。

詳細およびインストール情報については、 [Solr 設定](solr.md) （SRP 用）

### パッケージ共有へのリンクについて {#about-links-to-package-share}

**パッケージはAdobeAEM Cloud で表示**

このページのパッケージへのリンクでは、共有をパッケージ化するので、AEMの実行インスタンスは必要ありません。 `adobeaemcloud.com`. パッケージが表示可能な間は、 `Install`ボタンは、パッケージをAdobe・ホスト・サイトにインストールするためのものです。 ローカルのAEMインスタンスにインストールする場合は、「 」を選択します。 `Install`はエラーを引き起こします。

**ローカルのAEMインスタンスにインストールする方法**

に表示されるパッケージをインストールするには `adobeaemcloud.com` ローカルのAEMインスタンス上で、まずパッケージをローカルディスクにダウンロードする必要があります。

* を選択します。 **[!UICONTROL Assets]** タブ
* 選択 **[!UICONTROL ディスクにダウンロード]**

ローカルのAEMインスタンスで、パッケージマネージャー ( 例： [http://localhost:4502/crx/packmgr/](http://localhost:4502/crx/packmgr/)) をクリックして、ローカルのAEMパッケージリポジトリにアップロードします。

または、ローカルのAEMインスタンスからパッケージ共有を使用してパッケージにアクセスします ( 例： [http://localhost:4502/crx/packageshare/](http://localhost:4502/crx/packageshare/))、 `Download`ボタンをクリックすると、ローカルのAEMインスタンスのパッケージリポジトリにダウンロードされます。

ローカルのAEMインスタンスのパッケージリポジトリで、パッケージマネージャーを使用してパッケージをインストールします。

詳しくは、 [パッケージの操作方法](../../help/sites-administering/package-manager.md#package-share).

## 推奨されるデプロイメント {#recommended-deployments}

AEM Communitiesでは、共通ストアはユーザー生成コンテンツ (UGC) の格納に使用され、多くの場合、 [ストレージリソースプロバイダー (SRP)](working-with-srp.md). 推奨されるデプロイメントは、共通ストアに対する SRP オプションの選択を中心に行われます。

共通ストアは、パブリッシュ環境で UGC のモデレートと分析をサポートし、 [複製](sync.md) UGC の

* [コミュニティコンテンツストア](working-with-srp.md):AEM communities の SRP ストレージオプションについて説明します。

* [推奨されるトポロジ](topologies.md):使用例と SRP の選択に応じて使用するトポロジについて説明します。

## アップグレード {#upgrading}

以前のバージョンのAEMからAEM 6.4 プラットフォームにアップグレードする場合は、 AEM 6.4 へのアップグレードをお読みください。

プラットフォームのアップグレードに加えて、 [AEM Communities 6.4 へのアップグレード](upgrade.md) コミュニティの変更について学ぶには

## 設定 {#configurations}

### プライマリ発行者 {#primary-publisher}

選択したデプロイメントが [パブリッシュファーム](topologies.md#tarmk-publish-farm)その場合、1 つのAEMパブリッシュインスタンスを **`primary publisher`** に依存する機能など、すべてのインスタンスで発生しないアクティビティに対して **通知** または **Adobe Analytics**.

デフォルトでは、 `AEM Communities Publisher Configuration` OSGi 設定は、 **`Primary Publisher`** チェックボックスをオンにして、パブリッシュファーム内のすべてのパブリッシュインスタンスがプライマリとして自己識別されるようにします。

したがって、次の操作が必要です。 **すべてのセカンダリパブリッシュインスタンスで設定を編集** チェックを外す **`Primary Publisher`** チェックボックス。

![chlimage_1-411](assets/chlimage_1-411.png)

パブリッシュファーム内のその他（セカンダリ）パブリッシュインスタンスの場合：

* 管理者権限でログイン
* 次にアクセス： [web コンソール](../../help/sites-deploying/configuring-osgi.md)

   * 例： [http://localhost:4503/system/console/configMgr](http://localhost:4503/system/console/configMgr)

* を `AEM Communities Publisher Configuration`
* 編集アイコンを選択します。
* 「 **[!UICONTROL プライマリ発行者]** ボックス
* 「**[!UICONTROL 保存]**」を選択します

### オーサー環境のレプリケーションエージェント {#replication-agents-on-author}

レプリケーションは、コミュニティグループなど、パブリッシュ環境で作成されたサイトコンテンツに対して使用され、 [トンネルサービス](#tunnel-service-on-author).

プライマリパブリッシャーの場合、 [レプリケーションエージェント設定](../../help/sites-deploying/replication.md) は、パブリッシュサーバーと認証済みユーザーを正しく識別します。 デフォルトの許可されたユーザー `admin,` は既に適切な権限を持っています ( は `Communities Administrators`) をクリックします。

他のユーザーが適切な権限を持つには、そのユーザーをメンバーとして `administrators` ユーザーグループ ( `Communities Administrators`) をクリックします。

オーサー環境には 2 つのレプリケーションエージェントがあり、トランスポート設定を正しく設定する必要があります。

* 作成者のレプリケーションコンソールにアクセス

   * グローバルナビゲーションから： **[!UICONTROL ツール/導入/レプリケーション/作成者のエージェント]**

* 両方のエージェントに対して同じ手順を実行します。

   * **デフォルトエージェント (publish)**
   * **リバースレプリケーションエージェント（パブリッシュリバース）**

      1. エージェントを選択
      1. 選択 **[!UICONTROL 編集]**
      1. を選択します。 **[!UICONTROL 輸送]** タブ
      1. ポートでない場合 `4503`、 **[!UICONTROL URI]** 正しいポートを指定するには
      1. ユーザーでない場合 `admin`、 **[!UICONTROL ユーザー]** および **[!UICONTROL パスワード]** メンバを指定するには `administrators` ユーザーグループ

次の図は、ポートを 4503 から 6103 に変更した結果を示しています。

#### デフォルトエージェント (publish) {#default-agent-publish}

![chlimage_1-412](assets/chlimage_1-412.png)

#### リバースレプリケーションエージェント（パブリッシュリバース） {#reverse-replication-agent-publish-reverse}

![chlimage_1-413](assets/chlimage_1-413.png)

### オーサー環境のトンネルサービス {#tunnel-service-on-author}

オーサー環境を使用して [サイトの作成](sites-console.md), [サイトのプロパティを変更する](sites-console.md#modifying-site-properties) または [コミュニティメンバーの管理](members.md)オーサー環境に登録されているユーザーではなく、パブリッシュ環境に登録されているメンバー（ユーザー）にアクセスする必要があります。

トンネルサービスは、オーサー環境のレプリケーションエージェントを使用してこのアクセスを提供します。

トンネルサービスを有効にするには：

* オン **作成者**
* 管理者権限でログイン
* パブリッシャーが localhost:4503 でないか、トランスポートユーザーが `admin`,

   次に、 [レプリケーションエージェントの設定](#replication-agents-on-author)

* 次にアクセス： [Web コンソール](../../help/sites-deploying/configuring-osgi.md)

   * 例： [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr)

* を `AEM Communities Publish Tunnel Service`
* 編集アイコンを選択します。
* 次を確認します。 **[!UICONTROL 有効]** ボックス
* 「**[!UICONTROL 保存]**」を選択します

![chlimage_1-414](assets/chlimage_1-414.png)

### 暗号鍵のレプリケート {#replicate-the-crypto-key}

AEM Communitiesには 2 つの機能があり、すべてのAEMサーバーインスタンスで同じ暗号化キーを使用する必要があります。 以下が該当します。 [Analytics](analytics.md) および [ASRP](asrp.md).

AEM 6.3 以降では、鍵の素材はファイルシステムに保存され、リポジトリには保存されなくなりました。

オーサーインスタンスから他のすべてのインスタンスに主要資料をコピーするには、次の操作が必要です。

* コピーする主要な素材を含むAEMインスタンス（通常はオーサーインスタンス）にアクセスします

   * を `com.adobe.granite.crypto.file` ローカルファイルシステム内のバンドル

      例：

      * `<author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21`
      * この `bundle.info` ファイルはバンドルを識別します
   * データフォルダーに移動します。

      例：

      * `<author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21/data`
   * hmac ファイルとプライマリノードファイルをコピーする



* 各ターゲットAEMインスタンス

   * データフォルダーに移動します。

      例：

      * `<publish-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21/data`
   * 前にコピーした 2 つのファイルを貼り付けます。
   * ～する必要がある。 [Granite Crypto バンドルを更新します。](#refresh-the-granite-crypto-bundle) (target AEMインスタンスが現在実行中の場合 )


>[!CAUTION]
>
>暗号鍵に基づく別のセキュリティ機能が既に設定されている場合は、暗号鍵をレプリケートすると設定に損害が生じる可能性があります。 サポートが必要な場合は、 [カスタマーケアに問い合わせる](https://helpx.adobe.com/jp/marketing-cloud/contact-support.html).

#### リポジトリレプリケーション {#repository-replication}

AEM 6.2 以前の場合と同様に、キー資料をリポジトリに保存する場合は、各AEMインスタンスの初回起動時に（初期リポジトリを作成する）次のシステムプロパティを指定することで、保持できます。

* `-Dcom.adobe.granite.crypto.file.disable=true`

>[!NOTE]
>
>重要なのは、 [オーサー環境のレプリケーションエージェント](#replication-agents-on-author) が正しく設定されている。

リポジトリに保存されたキー材料を使用して、オーサーから他のインスタンスに暗号キーをレプリケートする方法は次のとおりです。

使用 [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md):

* 参照先 [https://&lt;server>:&lt;port>/crx/de](http://localhost:4502/crx/de)
* 「`/etc/key`」を選択します。
* open `Replication` タブ
* 「`Replicate`」を選択します。

* [Granite Crypto バンドルを更新します。](#refresh-the-granite-crypto-bundle)

![chlimage_1-415](assets/chlimage_1-415.png)

#### Granite 暗号バンドルを更新します。 {#refresh-the-granite-crypto-bundle}

* 各パブリッシュインスタンスで、 [Web コンソール](../../help/sites-deploying/configuring-osgi.md)

   * 例： [https://&lt;server>:&lt;port>/system/console/bundles](http://localhost:4503/system/console/bundles)

* 場所 `Adobe Granite Crypto Support` バンドル (com.adobe.granite.crypto)
* 選択 **[!UICONTROL 更新]**

![chlimage_1-416](assets/chlimage_1-416.png)

* しばらくすると、 **成功** ダイアログが表示されます。

   `Operation completed successfully.`

### Apache HTTP サーバー {#apache-http-server}

Apache HTTP サーバーを使用している場合は、関連するすべてのエントリに対して正しいサーバー名を使用していることを確認します。

特に、正しいサーバー名を使用するように注意してください。 `localhost`、 `RedirectMatch`.

#### httpd.conf のサンプル {#httpd-conf-sample}

```shell
<IfModule alias_module>
     # XAMPP does not have a favicon; this prevents any 404 errors which may arise.
     Redirect 404 /favicon.ico
     <Location /favicon.ico>
         ErrorDocument 404 "No favicon"
     </Location>

    # Return from "Sign Out" generates response header directing you to "/", generating a 404 error
    # The RedirectMatch resolves it correctly when modified for the target Community Site:
    RedirectMatch ^/$ https://[server name]/content/sites/engage/en.html
 ...
 </IfModule>
```

### Dispatcher {#dispatcher}

Dispatcher を使用する場合は、以下を参照してください。

* AEM [Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=ja) ドキュメント
* [Dispatcher のインストール](https://helpx.adobe.com/jp/experience-manager/dispatcher/using/dispatcher-install.html)
* [Communities 用の Dispatcher の設定](dispatcher.md)
* [既知の問題](troubleshooting.md#dispatcher-refetch-fails)

## 関連するコミュニティドキュメント {#related-communities-documentation}

* 訪問 [コミュニティサイトの管理](administer-landing.md) コミュニティサイトの作成、コミュニティサイトテンプレートの設定、コミュニティコンテンツのモデレート、メンバーの管理、メッセージングの設定について説明します。

* 訪問 [コミュニティの開発](communities.md) ソーシャルコンポーネントフレームワーク (SCF) と、コミュニティのコンポーネントと機能のカスタマイズについて説明します。

* 訪問 [コミュニティコンポーネントのオーサリング](author-communities.md) コミュニティコンポーネントを使用して作成および設定する方法を学ぶには、以下を参照してください。
