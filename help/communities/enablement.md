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
exl-id: 01cfc774-8ae1-48c0-a7e3-5836c4b39bff
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '448'
ht-degree: 59%

---

# イネーブルメント機能の設定 {#configuring-enablement-features}

## 概要 {#overview}

イネーブルメント機能では、[イネーブルメントコミュニティ](overview.md#enablement-community)を作成できます。

* この機能を実稼動環境で使用するには、追加のライセンスが必要です。

イネーブルメント機能を使用するには、次の必要があります。

以下をインストールします。

* **SCORM** Sharable Content Object Reference Model（SCORM）は、e ラーニングの規格と仕様を集めたものです。SCORM では、コンテンツを転送可能な ZIP ファイルにパッケージ化する方法も定義されています。

* **MySQL** MySQL は、主に、イネーブルメントリソースの SCORM 追跡データおよびレポートデータや、ビデオの再生状況の追跡用テーブルを格納するために使用されるリレーショナルデータベースです。イネーブルメント機能パックで SCORM を使用するには、MySQL JDBC ドライバが必要です。

* **FFmpeg** FFmpeg はオーディオとビデオの変換およびストリーミングのためのソリューションです。インストールすると、[ビデオアセット](../../help/sites-authoring/default-components-foundation.md#video)の適切なトランスコーディングに使用できます。イネーブルメントコミュニティでは、オーサー環境で、アップロードしたリソースのメタデータを取得したり、リソースの一覧に表示するサムネイルを生成するときに FFmpeg を使用します。

以下をセットアップします。

* **コミュニ**
ティマネージャイネーブルメントコミュニティの場合は、 
`Community Enablement Managers` ユーザーグループにはの役割を割り当てることがで `*Community Site* Enablement Manager`き、その権限にはパブリッシュ環境でのコンテンツ作成、割り当て、メンバー管理などが含まれます。

オプションで以下を設定します。

* **Adobe Analytics** Adobe Analytics と統合することで、包括的なレポート機能が追加され、また Analytics に Video Heartbeat を追加できます。

* **Dispatcher**

## 設定手順 {#configuration-steps}

イネーブルコミュニティに必要な手順を以下に示します。

各手順は、必要な詳細が記されたドキュメントにリンクしています。

**すべてのオーサー／パブリッシュインスタンスで、次の手順を実行します。**

1. **[MySQLUse Webコンソール用のJDBCド](deploy-communities.md#jdbc-driver-for-mysql)**
ライバー（バンドル）をインストールします。SCORMパッケージをイ *ンストールする前に、 http://localhost:4502/system/console/*
bundles ** Installをインストールします。

1. **[SCORMパッケージをイ](deploy-communities.md#scorm-package)**
ンストールします。パッケージマネージャーを使用： 
*http://localhost:4502/crx/packmgr/*

**任意のサーバーで、次の手順を実行します。**

1. **[MySQL、MySQL Workbench をインストール](mysql.md)**

1. **[MySQLデータベースのインス](mysql.md#database-setup)**
トールオーサーインスタンスからダウンロードしたSQLスクリプトの実行
\
   MySQL Workbenchの使用

**オーサーインスタンスをホストしている同じサーバーで、次の手順を実行します。**

1. **[FFmpeg をインストール](ffmpeg.md)**

**すべてのオーサー／パブリッシュインスタンスで、次の手順を実行します。**

1. **[JDBC接続プール](mysql.md#configure-jdbc-connections)**
の設定Webコンソール(configMgr)を使用： 
*http://localhost:4502/system/console/configMgr*

1. **[SCORMエンジンサ](mysql.md#aem-communities-scormengine-service)**
ービスの設定Webコンソール(configMgr)を使用： 
*http://localhost:4502/system/console/configMgr*

1. **[CSRFフィルタ](mysql.md#adobe-granite-csrf-filter)**
ーを設定Webコンソール(configMgr)を使用します。 
*http://localhost:4502/system/console/configMgr*

**オーサーインスタンスで、次の手順を実行します。**

1. （*オプション*） **[Analyticsサービスの設定](analytics.md)**
ツール/デプロイメント/Cloud Servicesコンソールを使用します。 
*http://localhost:4502/etc/cloudservices/sitecatalyst.html*

1. **[FFmpegUseワー](ffmpeg.md#configure-ffmpeg-transcoding-service)**
クフロー/モデルコンソールの設定

1. **[トンネルサ](deploy-communities.md#tunnel-service-on-author)**
ービス使用Webコンソール(configMgr)を有効にします。 
*http://localhost:4502/system/console/configMgr*

1. **[コミュニティ管](users.md#creating-community-members)** 理者の作成オーサー環境では、クラシックUIセキュリティコンソールを使用します。 *http://localhost:4502/*
useradmincreate user(s) with path = /home/users/community

   * 次のグループにメンバーを追加します：

      * コミュニティイネーブルメントマネージャー
      * コミュニティ管理者

## Dispatcher {#dispatcher}

デプロイメントに[AEM Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher.html)が含まれている場合、イネーブルメント機能を正しく動作させるには、`clientheader`セクションと`filter`セクションを変更する必要があります。 [コミュニティのための Dispatcher の設定](dispatcher.md#enablement)を参照してください。
