---
title: イネーブルメント機能の設定
seo-title: Configuring Enablement Features
description: コミュニティでのイネーブルメント機能の設定
seo-description: Configure enablement features in Communities
uuid: 27be3128-1a7d-412e-99a9-6e3b3b0aec1c
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.4/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 765a3d9b-4552-403e-872c-fdf684ac271d
role: Admin
exl-id: 01cfc774-8ae1-48c0-a7e3-5836c4b39bff
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '476'
ht-degree: 11%

---

# イネーブルメント機能の設定 {#configuring-enablement-features}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

## 概要 {#overview}

イネーブルメント機能を使用すると、 [実施可能コミュニティ](overview.md#enablement-community).

* この機能を実稼動環境で使用するには、追加のライセンスが必要です。

イネーブルメント機能を使用するには、以下が必要です。

次のインストール：

* **SCORM**
Sharable Content Object Reference Model(SCORM) は、e ラーニングの標準と仕様の集まりです。 また、SCORM では、コンテンツを転送可能な ZIP ファイルにパッケージ化する方法も定義します。

* **MySQL**
MySQL は、主にイネーブルメントの SCORM 追跡データとレポートデータに使用されるリレーショナルデータベースと、ビデオの進行状況を追跡するためのテーブルです。 イネーブルメント機能パック用の SCORM には、MySQL JDBC ドライバが必要です。

* **FFmpeg**
FFmpeg は、オーディオとビデオの変換とストリーミングを行うソリューションで、インストール時に、 [ビデオアセット](../../help/sites-authoring/default-components-foundation.md#video). イネーブルメントコミュニティの場合、オーサー環境では、アップロードされたリソースのメタデータを取得したり、リソースのリスト時に表示するサムネールを生成したりするのに使用されます。

設定：

* **コミュニティマネージャー**
イネーブルメントコミュニティの場合、 
`Community Enablement Managers` ユーザーグループには、 `*Community Site* Enablement Manager`（権限には、コンテンツの作成、割り当て、パブリッシュ環境でのメンバー管理などが含まれます）

オプション設定：

* **Adobe Analytics**
Adobe Analyticsとの統合により、包括的なレポート機能が追加され、Analytics へのビデオハートビート追加がサポートされます。

* **Dispatcher**

## 設定手順 {#configuration-steps}

イネーブルメントコミュニティに必要な手順を次に示します。

各手順は、必要な詳細を提供するドキュメントにリンクしています。

**すべてのオーサー/パブリッシュインスタンスで、次の操作を実行します。**

1. **[MySQL 用の JDBC ドライバーのインストール](deploy-communities.md#jdbc-driver-for-mysql)**
Web コンソール（バンドル）を使用：インストール *http://localhost:4502/system/console/bundles*
インストール *前* SCORM パッケージのインストール

1. **[SCORM パッケージをインストールする](deploy-communities.md#scorm-package)**
パッケージマネージャを使用： 
*http://localhost:4502/crx/packmgr/*

**任意のサーバー上：**

1. **[MySQL、MySQL Workbench のインストール](mysql.md)**

1. **[MySQL データベースのインストール](mysql.md#database-setup)**
オーサーインスタンスからダウンロードした SQL スクリプトを実行
\
   MySQL Workbench の使用

**オーサーインスタンスをホストする同じサーバー上：**

1. **[FFmpeg のインストール](ffmpeg.md)**

**すべてのオーサー/パブリッシュインスタンスで、次の操作を実行します。**

1. **[JDBC 接続プールの設定](mysql.md#configure-jdbc-connections)**
Web コンソール (configMgr) を使用： 
*http://localhost:4502/system/console/configMgr*

1. **[SCORM エンジンサービスの設定](mysql.md#aem-communities-scormengine-service)**
Web コンソール (configMgr) を使用： 
*http://localhost:4502/system/console/configMgr*

1. **[CSRF フィルターの設定](mysql.md#adobe-granite-csrf-filter)**
Web コンソール (configMgr) を使用： 
*http://localhost:4502/system/console/configMgr*

**オーサーインスタンス上：**

1. (*オプション*) **[Analytics サービスの設定](analytics.md)**
ツール/デプロイメント/Cloud Servicesコンソールを使用します。 
*http://localhost:4502/etc/cloudservices/sitecatalyst.html*

1. **[FFmpeg の設定](ffmpeg.md#configure-ffmpeg-transcoding-service)**
ワークフロー/モデルコンソールの使用

1. **[トンネルサービスの有効化](deploy-communities.md#tunnel-service-on-author)**
Web コンソール (configMgr) を使用： 
*http://localhost:4502/system/console/configMgr*

1. **[コミュニティ管理者の作成](users.md#creating-community-members)** オーサー環境の場合は、クラシック UI セキュリティコンソールを使用します。 *http://localhost:4502/useradmin*
パス= /home/users/community でユーザーを作成

   * 次のグループにメンバーを追加します：

      * コミュニティイネーブルメントマネージャ
      * コミュニティ管理者

## Dispatcher {#dispatcher}

デプロイメントに次の条件が含まれる場合 [AEM Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=ja)イネーブルメント機能を正しく動作させるには、 `clientheader`および `filter`セクションは変更が必要です。 詳しくは、 [コミュニティ用の Dispatcher の設定](dispatcher.md#enablement).
