---
title: イネーブルメント機能の設定
seo-title: イネーブルメント機能の設定
description: Communities でイネーブルメント機能を設定します
seo-description: Communities でイネーブルメント機能を設定します
uuid: 27be3128-1a7d-412e-99a9-6e3b3b0aec1c
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.4/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 765a3d9b-4552-403e-872c-fdf684ac271d
role: Administrator
translation-type: tm+mt
source-git-commit: 75312539136bb53cf1db1de03fc0f9a1dca49791
workflow-type: tm+mt
source-wordcount: '449'
ht-degree: 59%

---


# イネーブルメント機能の設定 {#configuring-enablement-features}

## 概要 {#overview}

イネーブルメント機能では、[イネーブルメントコミュニティ](overview.md#enablement-community)を作成できます。

* この機能を使用するには、実稼働環境で使用する追加のライセンスが必要です。

イネーブルメント機能を使用するには、次の必要があります。

以下をインストールします。

* **SCORM** Sharable Content Object Reference Model（SCORM）は、e ラーニングの規格と仕様を集めたものです。SCORM では、コンテンツを転送可能な ZIP ファイルにパッケージ化する方法も定義されています。

* **MySQL** MySQL は、主に、イネーブルメントリソースの SCORM 追跡データおよびレポートデータや、ビデオの再生状況の追跡用テーブルを格納するために使用されるリレーショナルデータベースです。イネーブルメント機能パックで SCORM を使用するには、MySQL JDBC ドライバが必要です。

* **FFmpeg** FFmpeg はオーディオとビデオの変換およびストリーミングのためのソリューションです。インストールすると、[ビデオアセット](../../help/sites-authoring/default-components-foundation.md#video)の適切なトランスコーディングに使用できます。イネーブルメントコミュニティでは、オーサー環境で、アップロードしたリソースのメタデータを取得したり、リソースの一覧に表示するサムネイルを生成するときに FFmpeg を使用します。

以下をセットアップします。

* **コミュニティ**
マネージャ有効化コミュニティでは、 
`Community Enablement Managers` ユーザーグループにのロールを割り当てるこ `*Community Site* Enablement Manager`とができます。このロールの権限には、公開環境でのコンテンツ作成、割り当て、メンバー管理が含まれます。

オプションで以下を設定します。

* **Adobe Analytics** Adobe Analytics と統合することで、包括的なレポート機能が追加され、また Analytics に Video Heartbeat を追加できます。

* **Dispatcher**

## 設定手順 {#configuration-steps}

イネーブルコミュニティに必要な手順を以下に示します。

各手順は、必要な詳細が記されたドキュメントにリンクしています。

**すべてのオーサー／パブリッシュインスタンスで、次の手順を実行します。**

1. **[MySQLUse Web Console用のJDBCドライバ](deploy-communities.md#jdbc-driver-for-mysql)**
ーのインストール（バンドル）:SCORMパッケージのイ *ンストール*
前にhttp://localhost:4502/system/console/ **  bundlesInstallを実行する

1. **[SCORM](deploy-communities.md#scorm-package)**
パッケージのインストールパッケージマネージャーの使用： 
*http://localhost:4502/crx/packmgr/*

**任意のサーバーで、次の手順を実行します。**

1. **[MySQL、MySQL Workbench をインストール](mysql.md)**

1. **[MySQL](mysql.md#database-setup)**
データベースのインストール作成者インスタンスからダウンロードしたSQLの実行スクリプト
\
   MySQL Workbenchの使用

**オーサーインスタンスをホストしている同じサーバーで、次の手順を実行します。**

1. **[FFmpeg をインストール](ffmpeg.md)**

**すべてのオーサー／パブリッシュインスタンスで、次の手順を実行します。**

1. **[configure JDBC Connections](mysql.md#configure-jdbc-connections)**
poolWebコンソールを使用(configMgr): 
*http://localhost:4502/system/console/configMgr*

1. **[SCORMエンジン](mysql.md#aem-communities-scormengine-service)**
サービスの設定Webコンソールを使用(configMgr): 
*http://localhost:4502/system/console/configMgr*

1. **[csrf](mysql.md#adobe-granite-csrf-filter)**
フィルタの設定Webコンソールを使用(configMgr): 
*http://localhost:4502/system/console/configMgr*

**オーサーインスタンスで、次の手順を実行します。**

1. （*オプション*） **[Analyticsサービスの設定](analytics.md)**
ツール、デプロイメント、Cloud Servicesコンソールを使用します。 
*http://localhost:4502/etc/cloudservices/sitecatalyst.html*

1. **[FmpegUse Workflow/Modelsコンソールの](ffmpeg.md#configure-ffmpeg-transcoding-service)**
設定

1. **[トンネル](deploy-communities.md#tunnel-service-on-author)**
サービスを有効にするWebコンソールを使用(configMgr): 
*http://localhost:4502/system/console/configMgr*

1. **[コミュニティ](users.md#creating-community-members)** 管理者の作成作成者環境は、クラシックUIセキュリティコンソールを使用します。 *http://localhost:4502/*
 useradmincreate user(s) with path = /home/users/community

   * メ追加ンバーを次のグループに追加します：

      * コミュニティイネーブルメントマネージャー
      * コミュニティ管理者

## Dispatcher {#dispatcher}

展開に[AEM Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher.html)が含まれている場合、有効化機能を正しく動作させるために、`clientheader`セクションと`filter`セクションを変更する必要があります。 [コミュニティのための Dispatcher の設定](dispatcher.md#enablement)を参照してください。
