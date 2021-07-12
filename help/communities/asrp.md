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
role: Admin
exl-id: 136c0913-c8b8-451d-bb28-3c3285c172a1
source-git-commit: 3c050c33a384d586d74bd641f7622989dc1d6b22
workflow-type: tm+mt
source-wordcount: '829'
ht-degree: 47%

---

# ASRP - Adobe ストレージリソースプロバイダー {#asrp-adobe-storage-resource-provider}

## ASRP について {#about-asrp}

AEM CommunitiesがASRPを共通ストアとして使用するように設定されている場合、同期やレプリケーションを必要とせずに、すべてのオーサーインスタンスとパブリッシュインスタンスからユーザー生成コンテンツ(UGC)にアクセスできます。

[SRP オプションの特性](working-with-srp.md#characteristics-of-srp-options)と[推奨されるトポロジ](topologies.md)も参照してください。

## 要件 {#requirements}

ASRP の使用には追加ライセンスが必要です。

UGC用のASRPを使用するようにAEM Communitiesサイトを設定するには、次の点についてアカウント担当者にお問い合わせください。

* データセンター URL（ASRP エンドポイントのアドレス）
* 消費者キー
* 秘密鍵
* レポートスイート ID

消費者キーと秘密鍵は、企業の全レポートスイート間で共通です。テナントごとに1つのレポートスイートがあります。

## 設定 {#configuration}

### ASRP の選択 {#select-asrp}

[ストレージ設定コンソール](srp-config.md)では、使用するSRPの実装を指定するデフォルトのストレージ設定を選択できます。

**作成者**:

* グローバルナビゲーションから：**[!UICONTROL ツール/コミュニティ/ストレージ設定]**

![chlimage_1-310](assets/chlimage_1-310.png)

* 「**[!UICONTROL Adobeストレージリソースプロバイダー(ASRP)]**」を選択します。
* 次の情報は、プロビジョニングプロセスから取得されます

   * **[!UICONTROL データセンター URL]**

      プルダウンして、アカウント担当者が特定した本番データセンターを選択します。

   * **[!UICONTROL デフォルトのレポートスイート]**

      デフォルトのレポートスイートの名前を入力します

   * **[!UICONTROL 消費者キー]**

      消費者キーの入力

   * **[!UICONTROL 暗号鍵]**

      秘密鍵を入力します。

* 「**[!UICONTROL 送信]**」を選択します。

以下を実行してパブリッシュインスタンスを用意します。

* [暗号鍵のレプリケート](#replicate-the-crypto-key)
* [設定のレプリケート](#publishing-the-configuration)

設定を送信したら、以下の手順で接続をテストします。

* 「**[!UICONTROL テスト設定]**」を選択します。
オーサーインスタンスとパブリッシュインスタンスごとに、ストレージ設定コンソールからデータセンターへの接続をテストします。

* 最後に、[リンク](#externalize-links)を外部化して、プロファイルデータのサイトURLがデータセンターからルーティング可能であることを確認します。

### 暗号鍵のレプリケーション {#replicate-the-crypto-key}

消費者キーと秘密鍵は暗号化されます。キーを正しく暗号化/復号化するには、プライマリGranite暗号キーがすべてのAEMインスタンスで同じである必要があります。

[暗号鍵のレプリケーション](deploy-communities.md#replicate-the-crypto-key)の手順に従います。

### リンクの外部向け変換 {#externalize-links}

正しいプロファイルとプロファイルイメージリンクを得るには、Link Externalizer](../../help/sites-developing/externalizer.md)を正しく設定してください。[

必ず、データセンターURL（ASRPエンドポイント）からルーティング可能なURLにするドメインを設定してください。

### 時刻の同期 {#time-synchronization}

ASRP エンドポイントでの認証を正常におこなうには、[ネットワークタイムプロトコル（NTP）](https://www.ntp.org/)などを使用して、AEM Communities を実行しているマシンの時刻を同期する必要があります。

### 設定の公開 {#publishing-the-configuration}

すべてのオーサーインスタンスとパブリッシュインスタンスで、ASRP が共通ストアとして指定されている必要があります。

パブリッシュ環境で同一の設定を使用できるようにするには：

* **作成者**:

   * メインメニューから&#x200B;**[!UICONTROL ツール/運営/レプリケーション]**&#x200B;に移動します。
   * 「**[!UICONTROL ツリーをアクティブ化]**」を選択します。
   * **[!UICONTROL 開始パス]**:

      * `/etc/socialconfig/srpc/`を参照します。
   * **[!UICONTROL 変更済み]**&#x200B;のみをオフにします
   * **[!UICONTROL アクティブ化]**&#x200B;を選択します。


## AEM 6.0 からのアップグレード {#upgrading-from-aem}

>[!CAUTION]
>
>公開済みのコミュニティサイトでASRPを有効にした場合、既に[JCR](jsrp.md)に保存されているUGCは、オンプレミスストレージとクラウドストレージの間でデータの同期がおこなわれないので、表示されなくなります。

**`AEM Communities Extension`** は、AEM 6.0のソーシャルコミュニティas a cloud serviceで以前に導入されました。AEM 6.1 Communities以降、クラウド設定は不要です。[ストレージ設定コンソール](srp-config.md)からASRPを選択するだけです。

新しいストレージ構造により、ソーシャルコミュニティからコミュニティにアップグレードするときは、[アップグレード](upgrade.md#adobe-cloud-storage)手順に従う必要があります。

## ユーザーデータの管理 {#managing-user-data}

パブリッシュ環境で頻繁に入力されるユーザー、ユーザープロファイルおよびユーザーグループについては、以下を参照してください。******

* [ユーザー同期](sync.md)
* [ユーザーとユーザーグループの管理](users.md)

## トラブルシューティング {#troubleshooting}

### アップグレード後に UGC が表示されない {#ugc-disappears-after-upgrade}

既存のAEM 6.0ソーシャルコミュニティサイトからアップグレードする場合は、[アップグレード手順](upgrade.md#adobe-cloud-storage)に従ってください。そうしないと、UGCが&#x200B;*表示*&#x200B;されなくなります。

### 認証エラー {#authentication-errors}

データセンター URL に対する認証エラーを受け取り、また AEM error.log に古いタイムスタンプに関するメッセージが含まれている場合は、時刻の同期がおこなわれているかを確認してください。

すべてのAEMオーサーサーバーとパブリッシュサーバーの時刻を同期するには、[Network Time Protocol(NTP)](https://www.ntp.org/)などのツールを使用することをお勧めします。

### 新しいコンテンツが検索結果に表示されない {#new-content-does-not-appear-in-searches}

Adobe クラウドストレージのインフラストラクチャは、結果整合性&#x200B;**&#x200B;を用いてスケーリングとパフォーマンスの目標を達成できるようにします。このため、新しいコンテンツは即座には使用可能にならず、検索結果に表示されるまで数秒かかることがあります。

結果整合性に影響を与える間隔は監視されていますが、新しいコンテンツが検索結果に表示されるまでに数秒以上かかる場合は、アカウント担当者に連絡してください。

### UGC が ASRP で表示されない {#ugc-not-visible-in-asrp}

ストレージオプションの設定を確認し、ASRP がデフォルトのプロバイダーに設定されているかを確認してください。デフォルトでは、ストレージリソースプロバイダーはASRPではなくJSRPです。

すべてのオーサーインスタンスとパブリッシュAEMインスタンスで、ストレージ設定コンソールに再度アクセスするか、AEMリポジトリを確認します。

* JCRで、 [/etc/socialconfig](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/)

   * [srpc](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/srpc)ノードが含まれない場合は、ストレージプロバイダーがJSRPであることを意味します。
   * srpcノードが存在し、ノード[defaultconfiguration](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/srpc/defaultconfiguration)が含まれる場合は、defaultconfigurationのプロパティでASRPをデフォルトのプロバイダーとして定義する必要があります
