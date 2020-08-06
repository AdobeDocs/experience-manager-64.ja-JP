---
title: ASRP - Adobe ストレージリソースプロバイダー
seo-title: ASRP - Adobe ストレージリソースプロバイダー
description: リレーショナルデータベースを共通ストアとして使用するように AEM Communities を設定する
seo-description: リレーショナルデータベースを共通ストアとして使用するように AEM Communities を設定する
uuid: 29826b44-633d-4586-8553-cd87ebe269a2
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.4/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 86349e4d-29ff-4baa-9fcd-c0ab1f0753e9
translation-type: tm+mt
source-git-commit: 09f8adac1d5fc4edeca03d6955faddf5ea045405
workflow-type: tm+mt
source-wordcount: '829'
ht-degree: 47%

---


# ASRP - Adobe ストレージリソースプロバイダー {#asrp-adobe-storage-resource-provider}

## ASRP について {#about-asrp}

AEM Communitiesが共通ストアとしてASRPを使用するように設定されている場合、ユーザー生成コンテンツ(UGC)は、すべてのオーサーインスタンスとパブリッシュインスタンスからアクセスでき、同期や複製は不要です。

[SRP オプションの特性](working-with-srp.md#characteristics-of-srp-options)と[推奨されるトポロジ](topologies.md)も参照してください。

## 要件 {#requirements}

ASRP の使用には追加ライセンスが必要です。

UGCにASRPを使用するようにAEM Communitiesサイトを設定するには、次の点についてアカウント担当者にお問い合わせください。

* データセンター URL（ASRP エンドポイントのアドレス）
* 消費者キー
* 秘密鍵
* レポートスイート ID

消費者キーと秘密鍵は、企業の全レポートスイート間で共通です。テナントごとに1つのレポートスイートがあります。

## 設定 {#configuration}

### ASRP の選択 {#select-asrp}

[ストレージ設定コンソール](srp-config.md) では、デフォルトのストレージ設定を選択できます。これにより、使用するSRPの実装が識別されます。

**作成者**:

* From global navigation: **[!UICONTROL Tools > Communities > Storage Configuration]**

![chlimage_1-310](assets/chlimage_1-310.png)

* Select **[!UICONTROL Adobe Storage Resource Provider (ASRP)]**
* 次の情報は、プロビジョニングプロセスから得られます

   * **[!UICONTROL データセンター URL]**

      プルダウンから、アカウント担当者が特定した本番データセンターを選択します。

   * **[!UICONTROL デフォルトのレポートスイート]**

      デフォルトのレポートスイート名を入力します

   * **[!UICONTROL 消費者キー]**

      Consumer keyを入力

   * **[!UICONTROL 暗号鍵]**

      秘密鍵を入力します

* Select **[!UICONTROL Submit]**

以下を実行してパブリッシュインスタンスを用意します。

* [暗号化キーを複製します](#replicate-the-crypto-key)
* [設定を複製する](#publishing-the-configuration)

設定を送信したら、以下の手順で接続をテストします。

* Select **[!UICONTROL Test Config]**
for each author and publish instance, test the connection to the data center from the Storage Configuration console

* Finally, ensure that the site URLs for profile data are routable from the Data Center by [externalizing links](#externalize-links).

### 暗号鍵のレプリケーション {#replicate-the-crypto-key}

消費者キーと秘密鍵は暗号化されます。キーを正しく暗号化/復号化するためには、すべてのAEMインスタンスでプライマリGranite Cryptoキーが同じである必要があります。

Follow the instructions at [Replicate the Crypto Key](deploy-communities.md#replicate-the-crypto-key).

### リンクの外部向け変換 {#externalize-links}

For correct profile and profile image links, be sure to properly [Configure the Link Externalizer](../../help/sites-developing/externalizer.md).

ドメインは、データセンターURL（ASRPエンドポイント）からルーティング可能なURLに設定してください。

### 時刻の同期 {#time-synchronization}

ASRP エンドポイントでの認証を正常におこなうには、[ネットワークタイムプロトコル（NTP）](https://www.ntp.org/)などを使用して、AEM Communities を実行しているマシンの時刻を同期する必要があります。

### 設定の公開 {#publishing-the-configuration}

すべてのオーサーインスタンスとパブリッシュインスタンスで、ASRP が共通ストアとして指定されている必要があります。

パブリッシュ環境で同一の設定を使用できるようにするには：

* **作成者**:

   * Navigate from main menu to **[!UICONTROL Tools > Operations > Replication]**
   * Select **[!UICONTROL Activate Tree]**
   * **[!UICONTROL 開始パス]**:

      * 参照先 `/etc/socialconfig/srpc/`
   * Uncheck **[!UICONTROL Only Modified]**
   * Select **[!UICONTROL Activate]**


## AEM 6.0 からのアップグレード {#upgrading-from-aem}

>[!CAUTION]
>
>If you enable ASRP on a published community site, any UGC already stored in [JCR](jsrp.md) will no longer be visible as there is no synchronization of data between on-premise storage and cloud storage.

**`AEM Communities Extension`** は、AEM 6.0のソーシャルコミュニティでクラウドサービスとして以前に導入されています。 As of AEM 6.1 Communities, no cloud configuration is necessary, simply select ASRP from the [storage configuration console](srp-config.md).

新しいストレージ構造により、ソーシャルコミュニティからコミュニティにアップグレードするときは、[アップグレード](upgrade.md#adobe-cloud-storage)手順に従う必要があります。

## ユーザーデータの管理 {#managing-user-data}

パブリッシュ環境で頻繁に入力されるユーザー、ユーザープロファイルおよびユーザーグループについては、以下を参照してください。******

* [ユーザーの同期](sync.md)
* [ユーザーとユーザーグループの管理](users.md)

## トラブルシューティング {#troubleshooting}

### アップグレード後に UGC が表示されない {#ugc-disappears-after-upgrade}

If upgrading from an exisitng AEM 6.0 social community site, be sure to follow the [upgrade instructions](upgrade.md#adobe-cloud-storage), else UGC will *appear* to be lost.

### 認証エラー {#authentication-errors}

データセンター URL に対する認証エラーを受け取り、また AEM error.log に古いタイムスタンプに関するメッセージが含まれている場合は、時刻の同期がおこなわれているかを確認してください。

It is recommended to use a tool such as the [Network Time Protocol (NTP)](https://www.ntp.org/) to time synchronize all AEM author and publish servers.

### 新しいコンテンツが検索結果に表示されない {#new-content-does-not-appear-in-searches}

Adobe クラウドストレージのインフラストラクチャは、結果整合性&#x200B;**&#x200B;を用いてスケーリングとパフォーマンスの目標を達成できるようにします。このため、新しいコンテンツは即座には使用可能にならず、検索結果に表示されるまで数秒かかることがあります。

結果整合性に影響を与える間隔は監視されていますが、新しいコンテンツが検索結果に表示されるまでに数秒以上かかる場合は、アカウント担当者に連絡してください。

### UGC が ASRP で表示されない {#ugc-not-visible-in-asrp}

ストレージオプションの設定を確認し、ASRP がデフォルトのプロバイダーに設定されているかを確認してください。デフォルトでは、ストレージリソースプロバイダーはASRPではなくJSRPです。

すべての作成者および発行AEMインスタンスで、ストレージ設定コンソールに再度アクセスするか、AEMリポジトリを確認します。

* In JCR, if [/etc/socialconfig](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/)

   * Does not contain an [srpc](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/srpc) node, it means the storage provider is JSRP
   * If the srpc node exists and contains node [defaultconfiguration](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/srpc/defaultconfiguration), the defaultconfiguration&#39;s properties should define ASRP to be the default provider

