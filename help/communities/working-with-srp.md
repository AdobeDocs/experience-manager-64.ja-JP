---
title: SRP - コミュニティコンテンツストレージ
seo-title: SRP - コミュニティコンテンツストレージ
description: AEM Communities 6.1 以降、ユーザー生成コンテンツ（UGC）は、ストレージリソースプロバイダー（SRP）により提供される単一の共通ストアに格納されます
seo-description: AEM Communities 6.1 以降、ユーザー生成コンテンツ（UGC）は、ストレージリソースプロバイダー（SRP）により提供される単一の共通ストアに格納されます
uuid: 651af1d7-70e8-4b56-8c01-871cb397678e
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.4/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: e975e026-e815-4445-be3e-b1237ed3f6b2
translation-type: tm+mt
source-git-commit: 8f169bb9b015ae94b9160d3ebbbd1abf85610465

---


# SRP - コミュニティコンテンツストレージ {#srp-community-content-storage}

## 概要 {#introduction}

AEM Communities 6.1以降、ユーザー生成コンテンツ(UGC)は、ストレージリソースプロバイダー(SRP)が提供する単一の共通ストアに保存されます。 ASRP、MSRP、JSRPなど、選択できるSRPオプションがいくつかあります。

以前のリリースとは異なり、AEM インスタンス間の UGC のリバース／フォワードレプリケーションはありません。代わりに、JSRPを除き、UGCは、すべての作成者インスタンスとパブリッシュインスタンスから、作成、読み取り、更新、削除(CRUD)操作に直接アクセスできるようになります。

Following are the [characteristics of each SRP option](#characteristics-of-srp-options), which is crucial information for the decision process when choosing the appropriate SRP and [underlying deployment](topologies.md).

For details regarding the use of SRP for UGC, see [Storage Resource Provider Overview](srp.md).

>[!NOTE]
>
>SRP はコミュニティコンテンツにのみ適用されます。It does not affect where site content is stored ([node store](../../help/sites-deploying/data-store-config.md)), and does not affect the secure handling of user registration, user profiles and user groups between AEM instances (see also [Managing User Data](#managing-user-data)).

>[!CAUTION]
>
>As of AEM 6.1, [UGC is never replicated](#ugc-never-replicated).
>
>デプロイメントに共通ストアが含まれていない場合（デフォルトの [JSRP](topologies.md#jsrp) トポロジなど）、UGC は、それが入力された AEM パブリッシュインスタンスまたはオーサーインスタンスでのみ表示可能になります。トポロジにパブリッシュクラスターが含まれる場合にのみ、UGCはパブリッシュインスタンスで表示されます。

## SRP オプションの特性 {#characteristics-of-srp-options}

[ASRP - Adobe ストレージリソースプロバイダー](asrp.md)\
このオプションを使用すると、UGCはアドビがホストし管理するクラウドサービス内でリモートで保持されます。 その場合は、追加のライセンスを取得し、アカウント担当者と協力して、その特定のライセンスのアカウントをプロビジョニングする必要があります。

* コミュニティのコンテンツを保存するために、アドビが提供およびサポートする関連クラウドサービスが必要です
* 特定の地域（米国、EMEA、APAC）のデータセンターを選択する必要がある
* UGCへのすべてのプログラムアクセスがSRP APIを通じて必要
* TarMK発行ファームに適している
* ローカル・ストレージに投資する意図がない場合に適している

>[!NOTE]
>
>ASRPでの投稿（またはコメント）に添付ファイルをアップロードする場合、制限は50 MBです。

[MSRP - MongoDB ストレージリソースプロバイダー](msrp.md)\
このオプションを使用すると、UGCはローカルのMongoDBインスタンスで直接保持されます。

* コミュニティのコンテンツを保存するには、MongoDBのローカルでのライセンス済みインストールが必要です
* Apache Solrのローカルインストールが必要です
* UGCへのすべてのプログラムアクセスがSRP APIを通じて必要
* 既存のTarMK発行ファームに適している
* MongoMKまたはRdbMKクラスターに適している
* 大量のコミュニティコンテンツを期待する場合に適している

[DSRP - リレーショナルデータベースストレージリソースプロバイダー](dsrp.md)\
このオプションを使用すると、UGCはローカルのMySQLデータベースインスタンスに直接保持されます。

* コミュニティコンテンツを保存するには、MySQLのローカルインストールが必要です
* Apache Solrのローカルインストールが必要です
* UGCへのすべてのプログラムアクセスがSRP APIを通じて必要
* 既存のTarMK発行ファームに適している
* MongoMKまたはRdbMKクラスターに適している
* 大量のコミュニティコンテンツを期待する場合に適している

[JSRP - JCR ストレージリソースプロバイダー](jsrp.md)\
デフォルトのオプションでは、共通ストアはありません。 UGCは、入力されたAEMインスタンスと同じJCRリポジトリ内でのみ保持されます。

* コミュニティコンテンツを投稿先のAEM作成者または発行インスタンスのJCRリポジトリに保存します
* UGCへのすべてのプログラムアクセスがSRP APIを通じて必要
* 複数の発行インスタンスがデプロイされている場合（TarMKファーム内の発行インスタンス間に複製メカニズムがない場合）、発行クラスターが必要です
* モデレートは発行環境でのみ実行されます（作成者と発行の間に逆/転送のレプリケーションメカニズムはありません）
* 一般に、開発、デモ、トレーニングに最適

## SRP の設定 {#configuring-srp}

デフォルトのストレージオプションの指定は、基礎となるデプロイメントに基づき、[ストレージ設定コンソール](srp-config.md)でおこないます。

各オプションの設定について詳しくは、以下を参照してください。

* [ASRP - Adobe ストレージリソースプロバイダー](asrp.md)
* [MSRP - MongoDB ストレージリソースプロバイダー](msrp.md)
* [DSRP - リレーショナルデータベースストレージリソースプロバイダー](dsrp.md)
* [JSRP - JCR ストレージリソースプロバイダー](jsrp.md)

ストレージオプションが選択されていない場合は、JSRP がデフォルトで有効になります。

## 追加情報 {#additional-information}

### UGC のレプリケーションの廃止 {#ugc-never-replicated}

作成者はオーサー環境でページコンテンツを作成し、パブリッシュ環境にレプリケートします。ページにコメント、レビュー、フォーラム、ブログ、QnAなどのインタラクティブなAEM Communities機能が含まれる場合、メンバー（サインインサイト訪問者）によるパブリッシュインスタンス上でのインタラクションによって、ユーザ生成コンテンツ(UGC)がパブリッシュ環境に入ります。

これまでは、このコミュニティコンテンツはオーサーインスタンスにリバースレプリケートされ、オーサーインスタンスからパブリッシュインスタンスにレプリケートされていました。逆複製と転送複製を使用してAEMインスタンス間の一貫性を維持すると問題が発生していました。

AEM Communities 6.1 以降では、前述のように、UGC 用の共有ストレージを使用することで UGC のレプリケーションが不要になりました。

サイトコンテンツはレプリケートされますが、UGC はレプリケートされません。

### ユーザーデータの管理 {#managing-user-data}

Also of interest to Communites are [*users *,* user groups *, and* user profiles *](users.md). This user-related data, when created and updated in the publish environment, needs to be made available to other publish instances when the topology is a[publish farm](../../help/sites-deploying/recommended-deploys.md#tarmk-farm).

AEM Communities 6.1 以降、ユーザー関連データは、レプリケーションではなく Sling ディストリビューションを使用して同期されます。For more information visit [User Synchronization](sync.md).

### AEM Communities 6.2 へのアップグレード {#upgrading-to-aem-communities}

AEM Communities 6.3 にアップグレードする際、既存の UGC を保持する必要がある場合は、AEM 5.6.1 または AEM 6.0 のコミュニティで使用しているアドビの UGC のオンデマンドストレージまたはオンプレミスストレージに応じて、手順を実行する必要があります。

詳しくは、[AEM Communities 6.3 へのアップグレード](upgrade.md)を参照してください。
