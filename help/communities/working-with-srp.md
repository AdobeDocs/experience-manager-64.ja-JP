---
title: SRP - コミュニティコンテンツストレージ
seo-title: SRP - Community Content Storage
description: AEM Communities 6.1 以降、ユーザー生成コンテンツ (UGC) は、ストレージリソースプロバイダー (SRP) が提供する単一の共通ストアに保存されます
seo-description: As of AEM Communities 6.1, user generated content (UGC) is stored in a single, common store provided by a storage resource provider (SRP)
uuid: 651af1d7-70e8-4b56-8c01-871cb397678e
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.4/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: e975e026-e815-4445-be3e-b1237ed3f6b2
role: Admin
exl-id: 4ff530ae-c676-4259-86f2-a3881843b642
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '932'
ht-degree: 6%

---

# SRP - コミュニティコンテンツストレージ {#srp-community-content-storage}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

## はじめに {#introduction}

AEM Communities 6.1 以降では、ユーザー生成コンテンツ (UGC) は、ストレージリソースプロバイダー (SRP) が提供する単一の共通ストアに保存されます。 ASRP、MSRP、JSRP など、選択できる SRP オプションが複数あります。

以前のリリースとは異なり、AEMインスタンス間での UGC のリバース/フォワードレプリケーションはありません。 代わりに、JSRP の場合を除き、UGC に直接アクセスして、すべてのオーサーインスタンスとパブリッシュインスタンスから作成、読み取り、更新、削除 (CRUD) 操作を行うことができます。

次に、 [各 SRP オプションの特性](#characteristics-of-srp-options)：適切な SRP と [基盤となる展開](topologies.md).

UGC での SRP の使用について詳しくは、 [ストレージリソースプロバイダの概要](srp.md).

>[!NOTE]
>
>SRP はコミュニティコンテンツにのみ適用されます。 サイトコンテンツの保存場所 ([ノードストア](../../help/sites-deploying/data-store-config.md)) や、AEMインスタンス間でのユーザー登録、ユーザープロファイルおよびユーザーグループの安全な処理には影響しません ( [ユーザーデータの管理](#managing-user-data)) をクリックします。

>[!CAUTION]
>
>AEM 6.1 以降、 [UGC はレプリケートされません](#ugc-never-replicated).
>
>デプロイメントに共通ストア（デフォルトなど）が含まれていない場合 [JSRP](topologies.md#jsrp) トポロジの場合、UGC は、その UGC が入力されたAEMパブリッシュインスタンスまたはオーサーインスタンス上でのみ表示されます。 トポロジにパブリッシュクラスターが含まれている場合にのみ、UGC は任意のパブリッシュインスタンスで表示されます。

## SRP オプションの特性 {#characteristics-of-srp-options}

[ASRP - Adobe ストレージリソースプロバイダー](asrp.md)\
このオプションを使用すると、UGC は、Adobeがホストおよび管理するクラウドサービスにリモートで保持されます。 追加のライセンスが必要です。また、アカウント担当者と協力して、その特定のライセンスのアカウントをプロビジョニングする必要があります。

* コミュニティコンテンツを保存するには、Adobeが提供およびサポートする関連クラウドサービスが必要です
* 特定の地域（米国、EMEA、APAC）のデータセンターの選択が必要
* SRP API を介した UGC へのすべてのプログラムによるアクセスが必要です
* TarMK パブリッシュファームに適しています
* ローカル・ストレージに投資する意図がない場合に適している

>[!NOTE]
>
>ASRP 内の投稿（またはコメント）に添付ファイルをアップロードする場合は、制限があります (50 MB)。

[MSRP - MongoDB ストレージリソースプロバイダー](msrp.md)\
このオプションを使用すると、UGC はローカルの MongoDB インスタンスに直接保持されます。

* コミュニティコンテンツを保存するには、MongoDB のローカルのライセンス済みインストールが必要です
* Apache Solr のローカルインストールが必要
* SRP API を介した UGC へのすべてのプログラムによるアクセスが必要です
* 既存の TarMK パブリッシュファームに適しています
* MongoMK または RdbMK クラスターに適しています
* 大量のコミュニティコンテンツを期待する場合に適しています

[DSRP - リレーショナルデータベースストレージリソースプロバイダー](dsrp.md)\
このオプションを使用すると、UGC はローカルの MySQL データベースインスタンスに直接保持されます。

* コミュニティコンテンツを保存するには、MySQL のローカルインストールが必要です
* Apache Solr のローカルインストールが必要
* SRP API を介した UGC へのすべてのプログラムによるアクセスが必要です
* 既存の TarMK パブリッシュファームに適しています
* MongoMK または RdbMK クラスターに適しています
* 大量のコミュニティコンテンツを期待する場合に適しています

[JSRP - JCR ストレージリソースプロバイダー](jsrp.md)\
デフォルトのオプションでは、共通ストアはありません。 UGC は、入力されたAEMインスタンスと同じ JCR リポジトリにのみ保持されます。

* コミュニティコンテンツを、投稿先のAEMオーサーインスタンスまたはパブリッシュインスタンスの JCR リポジトリに格納します。
* SRP API を介した UGC へのすべてのプログラムによるアクセスが必要です
* 複数のパブリッシュインスタンスがデプロイされている場合は、パブリッシュクラスターが必要です（TarMK ファーム内のパブリッシュインスタンス間にレプリケーションメカニズムが存在しません）。
* モデレートは、パブリッシュ環境でのみ実行されます（オーサーとパブリッシュの間にリバース/フォワードのレプリケーションメカニズムはありません）。
* 開発、デモ、トレーニングに一般に最適

## SRP の設定 {#configuring-srp}

デフォルトのストレージオプションを指定するには、基になるデプロイメントに基づいて、 [ストレージ設定コンソール](srp-config.md).

各オプションの設定について詳しくは、次を参照してください。

* [ASRP - Adobe ストレージリソースプロバイダー](asrp.md)
* [MSRP - MongoDB ストレージリソースプロバイダー](msrp.md)
* [DSRP - リレーショナルデータベースストレージリソースプロバイダー](dsrp.md)
* [JSRP - JCR ストレージリソースプロバイダー](jsrp.md)

ストレージオプションがアクティブに選択されていない場合、JSRP はデフォルトで有効になっています。

## 追加情報 {#additional-information}

### UGC がレプリケートされていません {#ugc-never-replicated}

オーサー環境では、オーサーがページコンテンツを作成し、パブリッシュ環境にレプリケートします。 ページにコメント、レビュー、フォーラム、ブログ、Q&amp;A などのインタラクティブなAEM Communities機能が含まれる場合、パブリッシュインスタンス上でのメンバー（サインインしたサイト訪問者）のインタラクションにより、パブリッシュ環境にユーザー生成コンテンツ (UGC) が入力されます。

以前は、このコミュニティコンテンツは、オーサーインスタンスにリバースレプリケートされ、オーサーインスタンスからパブリッシュインスタンスにレプリケートされていました。 リバースレプリケーションとフォワードレプリケーションを使用して、AEMインスタンス間の一貫性を維持することに問題が発生していました。

AEM Communities 6.1 以降、前述のように、UGC 用の共有ストレージを使用することで、UGC のレプリケーションの必要性がなくなりました。

サイトコンテンツはレプリケートされますが、UGC はレプリケートされません。

### ユーザーデータの管理 {#managing-user-data}

また、コミュニティに対する関心も [*ユーザー*, *ユーザーグループ*、および *ユーザープロファイル*](users.md). このユーザー関連データは、パブリッシュ環境で作成および更新されたときに、トポロジが [パブリッシュファーム](../../help/sites-deploying/recommended-deploys.md#tarmk-farm).

AEM Communities 6.1 以降では、ユーザー関連のデータは、レプリケーションではなく Sling 配布を使用して同期されます。 詳しくは、 [ユーザーの同期](sync.md).

### AEM Communities 6.2 へのアップグレード {#upgrading-to-aem-communities}

AEM Communities 6.3 にアップグレードする際に、既存の UGC を保持する必要がある場合は、AEM 5.6.1 またはAEM 6.0 コミュニティでAdobeのオンデマンドストレージを使用したか、オンプレミスストレージを使用したかに応じて、手順を実行する必要があります。

詳しくは、 [AEM Communities 6.3 へのアップグレード](upgrade.md).
