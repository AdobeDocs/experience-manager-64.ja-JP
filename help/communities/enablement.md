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
translation-type: tm+mt
source-git-commit: 4d64494dff34108d32e060a96209df697b2ce11f
workflow-type: tm+mt
source-wordcount: '448'
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

* **コミュニティマネージャ**&#x200B;ー有効化コミュニティに対しては、 
`Community Enablement Managers` ユーザーグループにのロールを割り当てるこ `*Community Site* Enablement Manager`とができます。このロールの権限には、公開環境でのコンテンツ作成、割り当て、メンバー管理が含まれます。

オプションで以下を設定します。

* **Adobe Analytics** Adobe Analytics と統合することで、包括的なレポート機能が追加され、また Analytics に Video Heartbeat を追加できます。

* **Dispatcher**

## 設定手順 {#configuration-steps}

イネーブルコミュニティに必要な手順を以下に示します。

各手順は、必要な詳細が記されたドキュメントにリンクしています。

**すべてのオーサー／パブリッシュインスタンスで、次の手順を実行します。**

1. **[MySQL](deploy-communities.md#jdbc-driver-for-mysql)**Use Web Console（バンドル）用のJDBCドライバーをインストールします。 
SCORMパッケージをインスト*ールする前に*、http://localhost:4502/system/console/bundles **Installをインストールします。

1. **[SCORMパッケージのインストール](deploy-communities.md#scorm-package)**パッケージマネージャーを使用する：
*http://localhost:4502/crx/packmgr/*

**任意のサーバーで、次の手順を実行します。**

1. **[MySQL、MySQL Workbench をインストール](mysql.md)**

1. **[MySQLデータベースのインストール](mysql.md#database-setup)**作成者インスタンスからダウンロードしたSQLの実行スクリプト
\
   MySQL Workbenchの使用

**オーサーインスタンスをホストしている同じサーバーで、次の手順を実行します。**

1. **[FFmpeg をインストール](ffmpeg.md)**

**すべてのオーサー／パブリッシュインスタンスで、次の手順を実行します。**

1. **[JDBC接続プールの設定](mysql.md#configure-jdbc-connections)**Webコンソールを使用(configMgr):
*http://localhost:4502/system/console/configMgr*

1. **[SCORMエンジンサービスの設定](mysql.md#aem-communities-scormengine-service)**Webコンソールを使用(configMgr):
*http://localhost:4502/system/console/configMgr*

1. **[CSRFフィルターの設定](mysql.md#adobe-granite-csrf-filter)**Webコンソールを使用(configMgr):
*http://localhost:4502/system/console/configMgr*

**オーサーインスタンスで、次の手順を実行します。**

1. (*optional*) **[configure Analytics service](analytics.md)**Use Tools, Deployment, Cloud Services console:
*http://localhost:4502/etc/cloudservices/sitecatalyst.html*

1. **[Fmpeg](ffmpeg.md#configure-ffmpeg-transcoding-service)**Use Workflow/Modelsコンソールの設定

1. **[トンネルサービス](deploy-communities.md#tunnel-service-on-author)**を有効にするWebコンソールを使用(configMgr):
*http://localhost:4502/system/console/configMgr*

1. **[コミュニティ管理者の作成作成者環境](users.md#creating-community-members)**：クラシックUIセキュリティコンソールを使用します。*http://localhost:4502/useradmin*create user(s) with path = /home/users/community

   * メ追加ンバーを次のグループに追加します：

      * コミュニティイネーブルメントマネージャー
      * コミュニティ管理者

## Dispatcher {#dispatcher}

When the deployment includes [AEM&#39;s Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher.html), in order for the enablement features to work properly, the `clientheader`and `filter`sections need modification. [コミュニティのための Dispatcher の設定](dispatcher.md#enablement)を参照してください。
