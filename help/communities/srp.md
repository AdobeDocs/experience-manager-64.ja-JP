---
title: ストレージリソースプロバイダーの概要
seo-title: Storage Resource Provider Overview
description: コミュニティ用の共通ストレージ
seo-description: Common storage for Communities
uuid: abdf4e5a-767b-428f-9aa4-0dc06819a26e
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.4/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 63abeda4-6ea1-4b45-b188-f9c6b44ca0cd
exl-id: 17105abe-177b-4e73-bb4f-22b208c436ef
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '1189'
ht-degree: 3%

---

# ストレージリソースプロバイダーの概要 {#storage-resource-provider-overview}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

## はじめに {#introduction}

AEM Communities 6.1 以降、コミュニティコンテンツ ( 一般的にユーザー生成コンテンツ (UGC) と呼ばれます ) は、 [ストレージリソースプロバイダー](working-with-srp.md) (SRP)。

複数の SRP オプションがあり、新しいAEM Communitiesインターフェイスを介して UGC にアクセスできます。 [SocialResourceProvider API](srp-and-ugc.md) (SRP API)：すべての作成、読み取り、更新、削除 (CRUD) 操作を含みます。

すべての SCF コンポーネントは SRP API を使用して実装され、 [基盤トポロジ](topologies.md) または UGC の場所。

***SocialResourceProvider API は、AEM Communitiesのライセンスを持つお客様のみが利用できます。***

>[!NOTE]
>
>**カスタムコンポーネント**:AEM Communitiesのライセンスを持つお客様の場合、カスタムコンポーネントの開発者は SRP API を使用して、基になるトポロジに関係なく UGC にアクセスできます。 詳しくは、 [SRP と UGC の基本事項](srp-and-ugc.md).

関連トピック：

* [SRP と UGC の基本事項](srp-and-ugc.md) - SRP ユーティリティメソッドと例
* [SRP を使用した UGC へのアクセス](accessing-ugc-with-srp.md)  — コーディングガイドライン
* [SocialUtils リファクタリング](socialutils.md)  — 廃止されたユーティリティメソッドを現在の SRP ユーティリティメソッドにマッピングする

## リポジトリについて {#about-the-repository}

SRP を理解するには、AEMコミュニティサイトでのAEMリポジトリ (OAK) の役割を理解すると役立ちます。

**Java コンテンツリポジトリ (JCR)**
この標準は、データモデルとアプリケーションプログラミングインターフェイス ([JCR API](https://jackrabbit.apache.org/jcr/jcr-api.html)) をコンテンツリポジトリーに追加します。 従来のファイル・システムの特性とリレーショナル・データベースの特性を組み合わせ、コンテンツ・アプリケーションが頻繁に必要とする機能を多数追加します。

JCR の実装の 1 つはAEMリポジトリ OAK です。

**Apache Jackrabbit Oak(OAK)**
[OAK](../../help/sites-deploying/platform.md) は、コンテンツ中心のアプリケーション向けに特別に設計されたデータストレージシステムである JCR 2.0 の実装です。 これは、非構造化データと半構造化データ用に設計された階層データベースの一種です。 リポジトリには、ユーザーに表示されるコンテンツだけでなく、アプリケーションで使用されるすべてのコード、テンプレート、内部データも保存されます。コンテンツにアクセスするための UI は次のとおりです。 [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md).

通常、JCR と OAK の両方がAEMリポジトリを参照するために使用されます。

非公開のオーサー環境でサイトコンテンツを開発した後は、公開パブリッシュ環境にコピーする必要があります。 これは、多くの場合、 *[複製](deploy-communities.md#replication-agents-on-author)*. これは、作成者、開発者、管理者の管理下で発生します。

UGC の場合、コンテンツは公開パブリッシュ環境で登録されたサイト訪問者（コミュニティメンバー）によって入力されます。 これはランダムに発生します。

管理とレポートの目的で、プライベートオーサー環境から UGC にアクセスできると便利です。 SRP では、パブリッシュからオーサーへのリバースレプリケーションは不要なので、オーサーから UGC にアクセスする方が一貫性が高く、パフォーマンスも向上します。

## SRP について {#about-srp}

UGC を共有ストレージに保存すると、メンバーコンテンツのインスタンスが 1 つになり、ほとんどのデプロイメントで、オーサー環境とパブリッシュ環境の両方からアクセスできます。 SRP の選択 (MSRP、ASRP、JSRP) に関係なく、すべての SRP API を使用してプログラムからアクセスする必要があります。

>[!NOTE]
>
>詳しくは、 [SRP と UGC の基本事項](srp-and-ugc.md) を参照してください。
>
>詳しくは、 [SRP を使用した UGC へのアクセス](accessing-ugc-with-srp.md) を参照してください。

### ASRP {#asrp}

ASRP の場合、UGC は JCR に格納されず、Adobeがホストおよび管理するクラウドサービスに格納されます。 ASRP に保存された UGC は、CRXDE Liteで表示したり、JCR API を使用してアクセスしたりすることはできません。

詳しくは、 [ASRP -Adobeストレージリソースプロバイダ](asrp.md).

開発者が UGC に直接アクセスすることはできません。

ASRP は、クエリにAdobeクラウドを使用します。

### MSRP {#msrp}

MSRP の場合、UGC は JCR には格納されず、MongoDB に格納されます。 MSRP に格納された UGC は、CRXDE Liteで表示したり、JCR API を使用してアクセスしたりすることはできません。

詳しくは、 [MSRP - MongoDB ストレージリソースプロバイダー](msrp.md).

MSRP は ASRP と同等ですが、すべてのAEMサーバーインスタンスが同じ UGC にアクセスするので、共通のツールを使用して MongoDB に格納された UGC に直接アクセスできます。

MSRP はクエリに Solr を使用します。

### JSRP {#jsrp}

JSRP は、1 つのAEMインスタンス上のすべての UGC にアクセスするためのデフォルトのプロバイダーです。 MSRP や ASRP を設定しなくても、AEM Communities 6.1 をすばやく体験できます。

詳しくは、 [JSRP - JCR ストレージリソースプロバイダー](jsrp.md).

JSRP の場合、UGC は JCR に格納され、CRXDE Liteと JCR API の両方からアクセスできますが、JCR API を使用しないことを強くお勧めします。そうしないと、今後の変更がカスタムコードに影響を与える可能性があります。

さらに、オーサー環境とパブリッシュ環境用のリポジトリは共有されません。 パブリッシュインスタンスのクラスターが共有パブリッシュリポジトリになりますが、パブリッシュ時に入力された UGC はオーサーに表示されないので、オーサーから UGC を管理することはできません。 UGC は、入力されたインスタンスのAEMリポジトリ (JCR) にのみ保持されます。

JSRP は、クエリに Oak インデックスを使用します。

## JCR のシャドウノードについて {#about-shadow-nodes-in-jcr}

UGC へのパスを模倣するシャドウノードは、ローカルリポジトリ内に存在し、次の 2 つの目的を果たします。

1. [アクセス制御 (ACL)](#for-access-control-acls))
1. [存在しないリソース (NER)](#for-non-existing-resources-ners)

SRP の実装に関係なく、実際の UGC はシャドウノードと同じ場所に表示されません。

### アクセス制御 (ACL) の場合 {#for-access-control-acls}

ASRP や MSRP などの一部の SRP 実装では、ACL 検証を提供しないデータベースにコミュニティコンテンツを格納します。 シャドウノードは、ACL を適用できるローカルリポジトリ内の場所を提供します。

SRP API を使用すると、すべての SRP オプションで、すべての CRUD 操作の前に、シャドウの場所が同じにチェックされます。

ACL チェックでは、リソースの UGC に適用される権限の確認に適したパスを返すユーティリティメソッドを使用します。

詳しくは、 [SRP と UGC の基本事項](srp-and-ugc.md) を参照してください。

### 存在しないリソース (NER) の場合 {#for-non-existing-resources-ners}

一部のコミュニティコンポーネントは、スクリプト内にインクルードできるので、コミュニティ機能をサポートするには Sling アドレス可能ノードが必要です。 [含まれるコンポーネント](scf.md#add-or-include-a-communities-component) は、存在しないリソース (NER) と呼ばれます。

シャドウノードは、リポジトリ内の Sling アドレス可能な場所を提供します。

>[!CAUTION]
>
>シャドウノードには複数の用途があるので、シャドウノードが存在すると、 *not* コンポーネントが NER であることを示します。

### ストレージの場所 {#storage-location}

次に、 [コメントコンポーネント](http://localhost:4502/content/community-components/en/comments.html) 内 [コミュニティコンポーネントガイド](components-guide.md):

* コンポーネントは次の場所にあるローカルリポジトリに存在します。

   /content/community-components/en/comments/jcr:content/content/includable/comments

* 対応するシャドウノードが、次の場所にあるローカルリポジトリに存在します。

   /content/usergenerated/content/community-components/en/comments/jcr:content/content/includable/comments

シャドウノードの下に UGC は見つかりません。

デフォルトの動作では、関連するサブツリーが読み取りまたは書き込み用に参照されるたびに、パブリッシュインスタンス上にシャドウノードを設定します。

例えば、デプロイメントが [MSRP](msrp.md) TarMK パブリッシュファームを使用します。

When a [メンバー](users.md) pub1（MongoDB に格納）に UGC を投稿し、pub1 の JCR にシャドウノードを作成します。

UGC が pub2 で初めて読み取られる場合、何も設定されていないと、デフォルトの動作ではシャドウノードが作成されます。

デフォルト動作以外の動作が必要な場合は、オーサーインスタンスで設定し、すべてのパブリッシュインスタンス（通常は手動プロセス）にロールフォワードする必要があります。
