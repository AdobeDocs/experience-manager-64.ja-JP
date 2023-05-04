---
title: パフォーマンスガイドライン
seo-title: Performance Guidelines
description: この記事では、AEMデプロイメントのパフォーマンスを最適化する方法に関する一般的なガイドラインを示します。
seo-description: This article provides general guidelines on how to optimize the performance of your AEM deployment.
uuid: 38cf8044-9ff9-48df-a843-43f74b0c0133
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.4/SITES
content-type: reference
topic-tags: configuring
discoiquuid: 9ccbc39e-aea7-455e-8639-9193abc1552f
feature: Configuring
exl-id: ee86b1b9-68fb-4311-bf5f-6151dd94d3b0
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '3012'
ht-degree: 36%

---

# パフォーマンスガイドライン{#performance-guidelines}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

このページでは、AEMデプロイメントのパフォーマンスを最適化する方法に関する一般的なガイドラインを示します。 AEMを初めて使用する場合は、パフォーマンスガイドラインを読む前に、次のページを参照してください。

* [AEM の基本概念](/help/sites-deploying/deploy.md#basic-concepts)
* [AEM のストレージの概要](/help/sites-deploying/storage-elements-in-aem-6.md#overview-of-storage-in-aem)
* [推奨されるデプロイメント](/help/sites-deploying/recommended-deploys.md)
* [技術要件](/help/sites-deploying/technical-requirements.md)

以下に AEM で使用できるデプロイメントオプションを示します（すべてのオプションを表示するにはスクロールしてください）。

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>AEM</strong></p> <p><strong>製品</strong></p> </td> 
   <td><p><strong>トポロジ</strong></p> </td> 
   <td><p><strong>オペレーティングシステム</strong></p> </td> 
   <td><p><strong>アプリケーションサーバー</strong></p> </td> 
   <td><p><strong>JRE</strong></p> </td> 
   <td><p><strong>セキュリティ</strong></p> </td> 
   <td><p><strong>マイクロカーネル</strong></p> </td> 
   <td><p><strong>データストア</strong></p> </td> 
   <td><p><strong>インデックス作成</strong></p> </td> 
   <td><p><strong>Web サーバー</strong></p> </td> 
   <td><p><strong>ブラウザー</strong></p> </td> 
   <td><p><strong>Marketing Cloud</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>Sites</p> </td> 
   <td><p>非 HA</p> </td> 
   <td><p>Windows</p> </td> 
   <td><p>CQSE</p> </td> 
   <td><p>Oracle</p> </td> 
   <td><p>LDAP</p> </td> 
   <td><p>Tar</p> </td> 
   <td><p>セグメント</p> </td> 
   <td><p>プロパティ</p> </td> 
   <td><p>Apache</p> </td> 
   <td><p>Edge</p> </td> 
   <td><p>ターゲット</p> </td> 
  </tr> 
  <tr> 
   <td><p>Assets</p> </td> 
   <td><p>Publish-HA</p> </td> 
   <td><p>Solaris</p> </td> 
   <td><p>WebLogic</p> </td> 
   <td><p>IBM</p> </td> 
   <td><p>SAML</p> </td> 
   <td><p>MongoDB</p> </td> 
   <td><p>File</p> </td> 
   <td><p>Lucene</p> </td> 
   <td><p>IIS</p> </td> 
   <td><p>IE</p> </td> 
   <td><p>Analytics</p> </td> 
  </tr> 
  <tr> 
   <td><p>Communities</p> </td> 
   <td><p>Author-CS</p> </td> 
   <td><p>Red Hat</p> </td> 
   <td><p>WebSphere</p> </td> 
   <td><p>HP</p> </td> 
   <td><p>OAuth</p> </td> 
   <td><p>RDB/Oracle</p> </td> 
   <td><p>S3/Azure</p> </td> 
   <td><p>Solr</p> </td> 
   <td><p>iPlanet</p> </td> 
   <td><p>FireFox</p> </td> 
   <td><p>Campaign</p> </td> 
  </tr> 
  <tr> 
   <td><p>Forms</p> </td> 
   <td><p>オーサー — オフロード</p> </td> 
   <td><p>HP-UX</p> </td> 
   <td><p>Tomcat</p> </td> 
   <td><p> </p> </td> 
   <td><p> </p> </td> 
   <td><p>RDB/DB2</p> </td> 
   <td><p>MongoDB</p> </td> 
   <td><p> </p> </td> 
   <td><p> </p> </td> 
   <td><p>Chrome</p> </td> 
   <td><p>ソーシャル</p> </td> 
  </tr> 
  <tr> 
   <td><p>モバイル</p> </td> 
   <td><p>オーサー — クラスター</p> </td> 
   <td><p>IBM AIX</p> </td> 
   <td><p>JBoss</p> </td> 
   <td><p> </p> </td> 
   <td><p> </p> </td> 
   <td><p>RDB/MySQL</p> </td> 
   <td><p>RDBMS</p> </td> 
   <td><p> </p> </td> 
   <td><p> </p> </td> 
   <td><p>Safari</p> </td> 
   <td><p>対象読者</p> </td> 
  </tr> 
  <tr> 
   <td><p>マルチサイト</p> </td> 
   <td><p>ASRP</p> </td> 
   <td><p>SUSE</p> </td> 
   <td><p> </p> </td> 
   <td><p> </p> </td> 
   <td><p> </p> </td> 
   <td><p>RDB／SQLServer</p> </td> 
   <td><p> </p> </td> 
   <td><p> </p> </td> 
   <td><p> </p> </td> 
   <td><p> </p> </td> 
   <td><p>Assets</p> </td> 
  </tr> 
  <tr> 
   <td><p>コマース</p> </td> 
   <td><p>MSRP</p> </td> 
   <td><p>Apple OS</p> </td> 
   <td><p> </p> </td> 
   <td><p> </p> </td> 
   <td><p> </p> </td> 
   <td><p> </p> </td> 
   <td><p> </p> </td> 
   <td><p> </p> </td> 
   <td><p> </p> </td> 
   <td><p> </p> </td> 
   <td><p>アクティベーション</p> </td> 
  </tr> 
  <tr> 
   <td><p>Dynamic Media</p> </td> 
   <td><p>JSRP</p> </td> 
   <td><p> </p> </td> 
   <td><p> </p> </td> 
   <td><p> </p> </td> 
   <td><p> </p> </td> 
   <td><p> </p> </td> 
   <td><p> </p> </td> 
   <td><p> </p> </td> 
   <td><p> </p> </td> 
   <td><p> </p> </td> 
   <td><p>モバイル</p> </td> 
  </tr> 
  <tr> 
   <td><p>Brand Portal</p> </td> 
   <td><p>J2E</p> </td> 
   <td><p> </p> </td> 
   <td><p> </p> </td> 
   <td><p> </p> </td> 
   <td><p> </p> </td> 
   <td><p> </p> </td> 
   <td><p> </p> </td> 
   <td><p> </p> </td> 
   <td><p> </p> </td> 
   <td><p> </p> </td> 
   <td><p> </p> </td> 
  </tr> 
  <tr> 
   <td><p>AoD</p> </td> 
   <td><p> </p> </td> 
   <td><p> </p> </td> 
   <td><p> </p> </td> 
   <td><p> </p> </td> 
   <td><p> </p> </td> 
   <td><p> </p> </td> 
   <td><p> </p> </td> 
   <td><p> </p> </td> 
   <td><p> </p> </td> 
   <td><p> </p> </td> 
   <td><p> </p> </td> 
  </tr> 
  <tr> 
   <td><p>LiveFyre</p> </td> 
   <td><p> </p> </td> 
   <td><p> </p> </td> 
   <td><p> </p> </td> 
   <td><p> </p> </td> 
   <td><p> </p> </td> 
   <td><p> </p> </td> 
   <td><p> </p> </td> 
   <td><p> </p> </td> 
   <td><p> </p> </td> 
   <td><p> </p> </td> 
   <td><p> </p> </td> 
  </tr> 
  <tr> 
   <td><p>スクリーン</p> </td> 
   <td><p> </p> </td> 
   <td><p> </p> </td> 
   <td><p> </p> </td> 
   <td><p> </p> </td> 
   <td><p> </p> </td> 
   <td><p> </p> </td> 
   <td><p> </p> </td> 
   <td><p> </p> </td> 
   <td><p> </p> </td> 
   <td><p> </p> </td> 
   <td><p> </p> </td> 
  </tr> 
  <tr> 
   <td><p>Doc Security</p> </td> 
   <td><p> </p> </td> 
   <td><p> </p> </td> 
   <td><p> </p> </td> 
   <td><p> </p> </td> 
   <td><p> </p> </td> 
   <td><p> </p> </td> 
   <td><p> </p> </td> 
   <td><p> </p> </td> 
   <td><p> </p> </td> 
   <td><p> </p> </td> 
   <td><p> </p> </td> 
  </tr> 
  <tr> 
   <td><p>Process Mgt</p> </td> 
   <td><p> </p> </td> 
   <td><p> </p> </td> 
   <td><p> </p> </td> 
   <td><p> </p> </td> 
   <td><p> </p> </td> 
   <td><p> </p> </td> 
   <td><p> </p> </td> 
   <td><p> </p> </td> 
   <td><p> </p> </td> 
   <td><p> </p> </td> 
   <td><p> </p> </td> 
  </tr> 
  <tr> 
   <td><p>デスクトップアプリケーション</p> </td> 
   <td><p> </p> </td> 
   <td><p> </p> </td> 
   <td><p> </p> </td> 
   <td><p> </p> </td> 
   <td><p> </p> </td> 
   <td><p> </p> </td> 
   <td><p> </p> </td> 
   <td><p> </p> </td> 
   <td><p> </p> </td> 
   <td><p> </p> </td> 
   <td><p> </p> </td> 
  </tr> 
 </tbody> 
</table>

>[!NOTE]
>
>パフォーマンスガイドラインは主にAEM Sitesに適用されます。

## パフォーマンスガイドラインを使用するタイミング {#when-to-use-the-performance-guidelines}

次の状況では、パフォーマンスガイドラインを使用する必要があります。

* **初めてのデプロイメント**:AEM Sitesまたは Assets の初めてのデプロイを計画する場合は、（デフォルト設定と比べて）マイクロカーネル、ノードストア、データストアを設定する際に使用できるオプションを理解しておくことが重要です。 例えば、TarMK のデータストアのデフォルト設定をファイルデータストアに変更します。
* **新しいバージョンへのアップグレード**:新しいバージョンにアップグレードする場合は、実行中の環境と比較したパフォーマンスの違いを理解することが重要です。 例えば、AEM 6.1 から 6.2 へ、またはAEM 6.0 CRX2 から 6.2 OAK へのアップグレードです。
* **応答時間が遅い**:選択したノードストアアーキテクチャが要件を満たしていない場合は、他のトポロジオプションと比較してパフォーマンスの違いを理解することが重要です。 例えば、MongoMK の代わりに TarMK をデプロイしたり、Amazon S3 またはMicrosoft Azure Data Store の代わりにファイルデータストアを使用したりします。
* **作成者の追加**:推奨される TarMK トポロジがパフォーマンス要件を満たさず、オーサーノードのアップサイズが最大容量に達した場合は、3 つ以上のオーサーノードで MongoMK を使用する場合と比較して、パフォーマンスの違いを理解することが重要です。 例えば、TarMK の代わりに MongoMK をデプロイします。
* **コンテンツの追加**：推奨データストアアーキテクチャが要件を満たさない場合は、他のデータストアオプションと比較してパフォーマンスの違いを理解することが重要です。例えば、ファイルデータストアの代わりに Amazon S3 または Microsoft Azure データストアを使用する場合などです。

## はじめに {#introduction}

この章では、AEMのアーキテクチャと最も重要なコンポーネントの概要を説明します。 また、開発ガイドラインを提供し、TarMK および MongoMK ベンチマークテストで使用されるテストシナリオについて説明します。

### AEM Platform {#the-aem-platform}

AEMプラットフォームは、次のコンポーネントで構成されています。

![chlimage_1](assets/chlimage_1.png)

AEM のプラットフォームについて詳しくは、[AEM とは](/help/sites-deploying/deploy.md#what-is-aem)を参照してください。

### AEMアーキテクチャ {#the-aem-architecture}

AEMデプロイメントには、3 つの重要な構築要素があります。 この **オーサーインスタンス** コンテンツ作成者、編集者および承認者がコンテンツの作成とレビューに使用する コンテンツが承認されると、コンテンツは、 **発行インスタンス** エンドユーザーがアクセスする場所から。 3 番目のビルディングブロックは **Dispatcher** で、これはキャッシュおよび URL フィルタリングを処理するモジュールとして、web サーバーにインストールされます。AEM のアーキテクチャについて詳しくは、[典型的なデプロイメントシナリオ](/help/sites-deploying/deploy.md#typical-deployment-scenarios)を参照してください。

![chlimage_1-1](assets/chlimage_1-1.png)

### マイクロカーネル {#micro-kernels}

マイクロカーネルは、AEMの永続性マネージャーとして機能します。 AEM で使用されるマイクロカーネルには、TarMK、MongoDB、リレーショナルデータベース（制限付きサポート）の 3 つのタイプがあります。インスタンスの目的と検討しているデプロイメントタイプによって、ニーズに合うマイクロカーネルを選択します。マイクロカーネルについて詳しくは、[推奨されるデプロイメント](/help/sites-deploying/recommended-deploys.md)のページを参照してください。

![chlimage_1-2](assets/chlimage_1-2.png)

### ノードストア {#nodestore}

AEMでは、バイナリデータをコンテンツノードとは独立して保存できます。 バイナリデータが保存される場所は、 **データストア**&#x200B;コンテンツノードとプロパティの場所は **ノードストア**.

>[!NOTE]
>
>Adobeでは、AEM オーサーインスタンスとパブリッシュインスタンスの両方で顧客が使用するデフォルトの永続化テクノロジーとして TarMK を推奨します。

>[!CAUTION]
>
>リレーショナルデータベースマイクロカーネルは制限付きでサポートされています。 連絡先 [Adobeカスタマーケア](https://helpx.adobe.com/jp/marketing-cloud/contact-support.html) このタイプのマイクロカーネルを使用する前に。

![chlimage_1-3](assets/chlimage_1-3.png)

### データストア {#data-store}

多数のバイナリを処理する場合は、最大限のパフォーマンスを確保するために、デフォルトのノードストアではなく外部のデータストアを使用することをお勧めします。例えば、プロジェクトで多数のメディアアセットが必要な場合は、それらをファイルデータストアまたは Azure／S3 データストアに格納すると、MongoDB 内に直接格納するよりも迅速にアセットにアクセスできます。

使用可能な設定オプションについて詳しくは、[ノードストアとデータストアの設定](/help/sites-deploying/data-store-config.md)を参照してください。

>[!NOTE]
>
>AEM を Azure または Amazon Web Services（AWS）にデプロイする場合は、Adobe Managed Services を使用することをお勧めします。このサービスでは、これらのクラウドコンピューティング環境での AEM のデプロイと運用の経験とスキルを持つチームのサポートを受けられます。[Adobe Managed Services に関するドキュメント](https://www.adobe.com/jp/marketing-cloud/enterprise-content-management/managed-services-cloud-platform.html?aemClk=t)も参照してください。
>
>Adobe Managed Services 以外の Azure またはAWSにAEMをデプロイする方法に関する推奨事項については、クラウドプロバイダー、または選択したクラウド環境でのAEMのデプロイをサポートするパートナーと直接連携することを強くお勧めします。 選択したクラウドプロバイダーまたはパートナーは、特定のパフォーマンス、負荷、拡張性、セキュリティ要件を満たすためにサポートするアーキテクチャのサイズ設定、設計、実装を担当します。
>
>詳細については、[技術要件](/help/sites-deploying/technical-requirements.md#supported-platforms)ページも参照してください。

### 検索 {#search-features}

この節では AEM で使用されるカスタムインデックスプロバイダーを示します。インデックス作成について詳しくは、[Oak クエリとインデックス作成](/help/sites-deploying/queries-and-indexing.md)を参照してください。

>[!NOTE]
>
>ほとんどのデプロイメントでは、Adobeは Lucene インデックスを使用することをお勧めします。 Solr は、特殊で複雑なデプロイメントのスケーラビリティにのみ使用してください。

![chlimage_1-4](assets/chlimage_1-4.png)

### 開発のガイドライン {#development-guidelines}

目指すAEMの開発が必要 **パフォーマンスと拡張性**. 以下に、従うことのできるベストプラクティスをいくつか示します。

**実行**

* プレゼンテーション、ロジック、コンテンツの分離を適用
* 既存のAEM API を使用 ( 例：Sling) とツール ( 例：レプリケーション )
* 実際のコンテンツのコンテキストで開発
* 最適なキャッシュ性を実現する開発
* 保存数を最小限に抑える ( 例：一時的なワークフローの使用
* すべての HTTP エンドポイントが RESTful であることを確認します。
* JCR 監視の範囲の制限
* 非同期スレッドに注意する

**DON&#39;T**

* 可能な場合は、JCR API を直接使用しないでください
* /libs を変更せず、オーバーレイを使用
* 可能な限りクエリを使用しない
* Java コードで OSGi サービスを取得する際には Sling バインディングを使用せず、次のように使用します。

   * @Reference in DS component
   * @Inject in a Sling Model
   * Sightly 使用クラスの sling.getService()
   * JSP の sling.getService()
   * ServiceTracker
   * OSGi サービスレジストリへの直接アクセス

AEMでの開発について詳しくは、 [開発 — 基本](/help/sites-developing/the-basics.md). その他のベストプラクティスについては、 [開発のベストプラクティス](/help/sites-developing/best-practices.md).

### ベンチマークのシナリオ {#benchmark-scenarios}

>[!NOTE]
>
>このページに表示されるすべてのベンチマークテストは、ラボ設定で実行されています。

以下に説明するテストシナリオは、TarMK、MongoMk、TarMK と MongoMk の各章のベンチマークセクションで使用されます。 特定のベンチマークテストで使用されているシナリオを確認するには、[技術仕様](/help/sites-deploying/performance-guidelines.md#tarmk-performance-benchmark)表のシナリオフィールドを参照してください。

**単一製品シナリオ**

AEM Assets：

* ユーザーインタラクション：アセットの参照/アセットの検索/アセットのダウンロード/アセットメタデータの読み込み/アセットメタデータの更新/アセットのアップロード/アセットのアップロードアップロードワークフローの実行
* 実行モード：同時ユーザー数、ユーザーごとの単一インタラクション数

**製品の混在シナリオ**

AEM Sites + Assets：

* Sites のユーザーインタラクション：記事ページを読む/ページを読む/段落を作成/段落を編集/コンテンツページを作成/コンテンツページをアクティベート/検索を作成
* Assets のユーザーインタラクション：アセットの参照/アセットの検索/アセットのダウンロード/アセットメタデータの読み込み/アセットメタデータの更新/アセットのアップロード/アセットのアップロードアップロードワークフローの実行
* 実行モード：同時ユーザー、ユーザーごとの混合インタラクション

**垂直方向の使用例のシナリオ**

メディア：

* 記事ページを読む (27.4%)、ページを読む (10.9%)、セッションを作成 (2.6%)、コンテンツページをアクティベート (1.7%)、コンテンツページを作成 (0.4%)、段落を作成 (4.3%)、段落を編集 (0.9%)、参照 (0.9%)、アセット (20%)、アセットメタデータ読み込み (8.5%)、アセットのダウンロード (4.2%)、アセットの検索 (0.2%)、アセットメタデータの更新 (2.4%)、アセットをアップロード (1.2%)、プロジェクトを参照 (4.9%)、プロジェクトを読み込み (6.6%)、アセットを追加 (1.2%)、プロジェクト追加サイト (1.2%)、プロジェクトを作成 (0.1%)、作成者検索 (0.4%)
* 実行モード：同時ユーザー、ユーザーごとの混合インタラクション

## TarMK {#tarmk}

この章では、TarMK の一般的なパフォーマンスガイドラインで、アーキテクチャの最小要件と設定設定を指定します。 さらに明確化するために、ベンチマークテストも提供されています。

アドビでは、すべてのデプロイメントシナリオにおいて、AEM オーサーインスタンスとパブリッシュインスタンスの両方に対し TarMK をデフォルトの優先使用する技術とすることを顧客に推奨します。

TarMK について詳しくは、[デプロイメントのシナリオ](/help/sites-deploying/recommended-deploys.md#deployment-scenarios)および [Tar ストレージ](/help/sites-deploying/storage-elements-in-aem-6.md#tar-storage)を参照してください。

### TarMK 最小アーキテクチャガイドライン {#tarmk-minimum-architecture-guidelines}

>[!NOTE]
>
>以下に示す最小アーキテクチャガイドラインは、実稼動環境および高トラフィックサイト向けです。 これらのガイドラインは、AEM を実行するために必要な[最小仕様](/help/sites-deploying/technical-requirements.md#prerequisites)では&#x200B;**ありません**。

TarMK を使用する際に優れたパフォーマンスを確立するには、次のアーキテクチャから始める必要があります。

* 1 つのオーサーインスタンス
* 2 つのパブリッシュインスタンス
* 2 つの Dispatcher

次に、AEM Sites とAEM Assetsのアーキテクチャガイドラインを示します。

>[!NOTE]
>
>ファイルデータストアを共有する場合は、バイナリなしのレプリケーションを&#x200B;**オン**&#x200B;にする必要があります。

**AEM Sitesの Tar アーキテクチャのガイドライン**

![chlimage_1-5](assets/chlimage_1-5.png)

**AEM Assets での Tar アーキテクチャガイドライン**

![chlimage_1-6](assets/chlimage_1-6.png)

### TarMK 設定ガイドライン {#tarmk-settings-guideline}

パフォーマンスを高めるには、次に示す設定ガイドラインに従う必要があります。 設定を変更する手順については、[このページを参照してください](https://helpx.adobe.com/experience-manager/kb/performance-tuning-tips.html)。

<table> 
 <tbody> 
  <tr> 
   <td><strong>設定</strong></td> 
   <td><strong>パラメーター</strong></td> 
   <td><strong>値</strong></td> 
   <td><strong>説明</strong></td> 
  </tr> 
  <tr> 
   <td>Sling ジョブキュー</td> 
   <td><code>queue.maxparallel</code></td> 
   <td>CPU コア数の半分の値に設定します。 </td> 
   <td>デフォルトでは、ジョブキューあたりの同時スレッド数は、CPU コア数と同じです。</td> 
  </tr> 
  <tr> 
   <td>Granite 一時的なワークフローキュー</td> 
   <td><code>Max Parallel</code></td> 
   <td>CPU コア数の半分の値に設定します。</td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>JVM パラメーター</td> 
   <td><p><code>Doak.queryLimitInMemory</code></p> <p><code>Doak.queryLimitReads</code></p> <p><code>Dupdate.limit</code></p> <p><code>Doak.fastQuerySize</code></p> </td> 
   <td><p>500000</p> <p>100000</p> <p>250000</p> <p>True</p> </td> 
   <td>AEMの起動スクリプトにこれらの JVM パラメーターを追加して、拡張クエリがシステムをオーバーロードしないようにします。</td> 
  </tr> 
  <tr> 
   <td>Lucene インデックスの設定</td> 
   <td><p><code>CopyOnRead</code></p> <p><code>CopyOnWrite</code></p> <p><code>Prefetch Index Files</code></p> </td> 
   <td><p>Enabled</p> <p>Enabled</p> <p>Enabled</p> </td> 
   <td>使用可能なパラメーターの詳細については、 <a href="https://jackrabbit.apache.org/oak/docs/query/lucene.html">このページ</a>.</td> 
  </tr> 
  <tr> 
   <td>データストア= S3 データストア</td> 
   <td><p><code>maxCachedBinarySize</code></p> <p><code>cacheSizeInMB</code></p> </td> 
   <td><p>1048576(1 MB) 以下</p> <p>最大ヒープサイズの 2～10%</p> </td> 
   <td>関連トピック <a href="/help/sites-deploying/data-store-config.md#data-store-configurations">データストアの設定</a>.</td> 
  </tr> 
  <tr> 
   <td>DAM アセットの更新ワークフロー</td> 
   <td><code>Transient Workflow</code></td> 
   <td>チェック済み</td> 
   <td>このワークフローではアセットの更新を管理します.</td> 
  </tr> 
  <tr> 
   <td>DAM メタデータの書き戻し</td> 
   <td><code>Transient Workflow</code></td> 
   <td>チェック済み</td> 
   <td>このワークフローは、元のバイナリへのXMPの書き戻しを管理し、JCR で最終変更日を設定します。</td> 
  </tr> 
 </tbody> 
</table>

### TarMK パフォーマンスベンチマーク {#tarmk-performance-benchmark}

#### 技術仕様 {#technical-specifications}

ベンチマークテストは以下の仕様に基づいて行われた。

|  | **オーサーノード** |
|---|---|
| サーバー | ベアメタルハードウェア（HP） |
| オペレーティングシステム | RedHat Linux |
| CPU／コア | Intel(R) Xeon(R) CPU E5-2407 @2.40GHz、8 コア |
| RAM | 32 GB |
| ディスク | 磁気 |
| Java | Oracle JRE バージョン 8 |
| JVM ヒープ | 16 GB |
| 製品 | AEM 6.2 |
| ノードストア | TarMK |
| データストア | ファイル DS |
| シナリオ | 単一の製品：アセット／30 個の同時スレッド |

#### パフォーマンスベンチマークの結果 {#performance-bechmark-results}

>[!NOTE]
>
>以下に示す数値は、ベースラインとして 1 に正規化されており、実際のスループット数ではありません。

![chlimage_1-7](assets/chlimage_1-7.png) ![chlimage_1-8](assets/chlimage_1-8.png)

## MongoMK {#mongomk}

TarMK よりも MongoMK 永続性バックエンドを選択する主な理由は、インスタンスを水平方向にスケールすることです。 つまり、2 つ以上のアクティブなオーサーインスタンスが常に実行され、MongoDB を永続性ストレージシステムとして使用します。 複数のオーサーインスタンスを実行する必要があるのは、通常、すべての同時オーサリングアクティビティをサポートする単一のサーバーの CPU とメモリの容量が持続不可能になったためです。

TarMK について詳しくは、[デプロイメントのシナリオ](/help/sites-deploying/recommended-deploys.md#deployment-scenarios)および [Mongo ストレージ](/help/sites-deploying/storage-elements-in-aem-6.md#mongo-storage)を参照してください。

### MongoMK 最小アーキテクチャのガイドライン {#mongomk-minimum-architecture-guidelines}

MongoMK を使用する際に優れたパフォーマンスを確立するには、次のアーキテクチャから始める必要があります。

* 3 つのオーサーインスタンス
* 2 つのパブリッシュインスタンス
* 3 つの MongoDB インスタンス
* 2 つの Dispatcher

>[!NOTE]
>
>実稼動環境では、MongoDB は常に、プライマリと 2 つのセカンダリを持つレプリカセットとして使用されます。 読み取りと書き込みはプライマリに送られ、読み取りはセカンダリに送られます。 ストレージが使用できない場合、セカンダリの 1 つをアービターに置き換えることができますが、MongoDB レプリカセットは常に奇数のインスタンスで構成する必要があります。

>[!NOTE]
>
>ファイルデータストアを共有する場合は、バイナリなしのレプリケーションを&#x200B;**オン**&#x200B;にする必要があります。

![chlimage_1-9](assets/chlimage_1-9.png)

### MongoMK 設定のガイドライン {#mongomk-settings-guidelines}

パフォーマンスを高めるには、次に示す設定ガイドラインに従う必要があります。 設定を変更する手順については、[このページを参照してください](https://helpx.adobe.com/experience-manager/kb/performance-tuning-tips.html)。

<table> 
 <tbody> 
  <tr> 
   <td><strong>設定</strong></td> 
   <td><strong>パラメーター</strong></td> 
   <td><strong>値（デフォルト）</strong></td> 
   <td><strong>説明</strong></td> 
  </tr> 
  <tr> 
   <td>Sling ジョブキュー</td> 
   <td><code>queue.maxparallel</code></td> 
   <td>CPU コア数の半分の値に設定します。 </td> 
   <td>デフォルトでは、ジョブキューあたりの同時スレッド数は、CPU コア数と同じです。</td> 
  </tr> 
  <tr> 
   <td>Granite 一時的なワークフローキュー</td> 
   <td><code>Max Parallel</code></td> 
   <td>CPU コア数の半分の値に設定します。</td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>JVM パラメーター</td> 
   <td><p><code>Doak.queryLimitInMemory</code></p> <p><code>Doak.queryLimitReads</code></p> <p><code>Dupdate.limit</code></p> <p><code>Doak.fastQuerySize</code></p> <p><code>Doak.mongo.maxQueryTimeMS</code></p> </td> 
   <td><p>500000</p> <p>100000</p> <p>250000</p> <p>True</p> <p>60000</p> </td> 
   <td>AEMの起動スクリプトにこれらの JVM パラメーターを追加して、拡張クエリがシステムをオーバーロードしないようにします。</td> 
  </tr> 
  <tr> 
   <td>Lucene インデックスの設定</td> 
   <td><p><code>CopyOnRead</code></p> <p><code>CopyOnWrite</code></p> <p><code>Prefetch Index Files</code></p> </td> 
   <td><p>Enabled</p> <p>Enabled</p> <p>Enabled</p> </td> 
   <td>使用可能なパラメーターについて詳しくは、 <a href="https://jackrabbit.apache.org/oak/docs/query/lucene.html">このページ</a>.</td> 
  </tr> 
  <tr> 
   <td>データストア= S3 データストア</td> 
   <td><p><code>maxCachedBinarySize</code></p> <p><code>cacheSizeInMB</code></p> </td> 
   <td><p>1048576(1 MB) 以下</p> <p>最大ヒープサイズの 2～10%</p> </td> 
   <td>関連トピック <a href="/help/sites-deploying/data-store-config.md#data-store-configurations">データストアの設定</a>.</td> 
  </tr> 
  <tr> 
   <td>DocumentNodeStoreService</td> 
   <td><p><code>cache</code></p> <p><code>nodeCachePercentage</code></p> <p><code>childrenCachePercentage</code></p> <p><code>diffCachePercentage</code></p> <p><code>docChildrenCachePercentage</code></p> <p><code>prevDocCachePercentage</code></p> <p><code>persistentCache</code></p> </td> 
   <td><p>2048</p> <p>35 (25)</p> <p>20 (10)</p> <p>30 (5)</p> <p>10 (3)</p> <p>4 (4)</p> <p>。/cache,size=2048,binary=0,-compact,-compress</p> </td> 
   <td><p>キャッシュのデフォルトのサイズは 256 MB に設定されています。</p> <p>キャッシュの無効化の実行に要する時間に影響を与えます。</p> </td> 
  </tr> 
  <tr> 
   <td>oak-observation</td> 
   <td><p><code>thread pool</code></p> <p><code>length</code></p> </td> 
   <td><p>最小値と最大値= 20</p> <p>50000</p> </td> 
   <td> </td> 
  </tr> 
 </tbody> 
</table>

### MongoMK パフォーマンスベンチマーク {#mongomk-performance-benchmark}

### 技術仕様 {#technical-specifications-1}

ベンチマークテストは以下の仕様に基づいて行われた。

|  | **オーサーノード** | **MongoDB ノード** |
|---|---|---|
| サーバー | ベアメタルハードウェア（HP） | ベアメタルハードウェア（HP） |
| オペレーティングシステム | RedHat Linux | RedHat Linux |
| CPU／コア | Intel(R) Xeon(R) CPU E5-2407 @2.40GHz、8 コア | Intel(R) Xeon(R) CPU E5-2407 @2.40GHz、8 コア |
| RAM | 32 GB | 32 GB |
| ディスク | 磁気 - 1,000 IOPS を超える | 磁気 - 1,000 IOPS を超える |
| Java | Oracle JRE バージョン 8 | 該当なし |
| JVM ヒープ | 16 GB | 該当なし |
| 製品 | AEM 6.2 | MongoDB 3.2 WiredTiger |
| ノードストア | MongoMK | 該当なし |
| データストア | ファイル DS | 該当なし |
| シナリオ | 単一の製品：アセット／30 個の同時スレッド | 単一の製品：アセット／30 個の同時スレッド |

### パフォーマンスベンチマーク結果 {#performance-benchmark-results}

>[!NOTE]
>
>以下に示す数値は、ベースラインとして 1 に正規化されており、実際のスループット数ではありません。

![chlimage_1-10](assets/chlimage_1-10.png) ![chlimage_1-11](assets/chlimage_1-11.png)

## TarMK と MongoMK {#tarmk-vs-mongomk}

この 2 つのいずれかを選択する際には、TarMK はパフォーマンスを重視して設計されているのに対して、MongoMK はスケーラビリティを重視して使用されるという基本ルールを考慮する必要があります。アドビでは、すべてのデプロイメントシナリオにおいて、AEM オーサーインスタンスとパブリッシュインスタンスの両方に対し TarMK をデフォルトの優先使用する技術とすることを顧客に推奨します。

TarMK よりも MongoMK 永続性バックエンドを選択する主な理由は、インスタンスを水平方向にスケールすることです。 つまり、2 つ以上のアクティブなオーサーインスタンスが常に実行され、MongoDB を永続性ストレージシステムとして使用します。 通常、複数のオーサーインスタンスを実行する必要があるのは、同時に実行するすべてのオーサリングアクティビティをサポートする単一のサーバーの CPU とメモリの容量が維持できなくなったためです。

TarMK と MongoMK の詳細については、 [推奨されるデプロイメント](/help/sites-deploying/recommended-deploys.md#microkernels-which-one-to-use).

### TarMK と MongoMk のガイドライン {#tarmk-vs-mongomk-guidelines}

**TarMK のメリット**

* コンテンツ管理アプリケーション向けに設計
* ファイルは常に一貫性があり、任意のファイルベースのバックアップ・ツールを使用してバックアップできます。
* フェイルオーバーメカニズムを備えています。詳しくは、[コールドスタンバイ](/help/sites-deploying/tarmk-cold-standby.md)を参照してください。
* 運用上のオーバーヘッドを最小限に抑え、高パフォーマンスで信頼性の高いデータストレージを提供
* TCO（総所有コスト）の削減

**MongoMK を選択するための条件**

* 1 日に接続した名前付きユーザーの数：何千もの間
* 同時ユーザー数：数百以上の
* 1 日あたりのアセット取り込みの量：何十万以上で
* 1 日あたりのページ編集の量：何十万以上で
* 1 日あたりの検索数：数十万以上で

### TarMK と MongoMK のベンチマーク {#tarmk-vs-mongomk-benchmarks}

>[!NOTE]
>
>以下に示す数値は、ベースラインとして 1 に正規化されており、実際のスループット数ではありません。

### シナリオ 1 技術仕様 {#scenario-technical-specifications}

<table> 
 <tbody> 
  <tr> 
   <td><strong> </strong></td> 
   <td><strong>OAK オーサーノード</strong></td> 
   <td><strong>MongoDB ノード</strong></td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>サーバー</td> 
   <td>ベアメタルハードウェア（HP）</td> 
   <td>ベアメタルハードウェア（HP）</td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>オペレーティングシステム</td> 
   <td>RedHat Linux</td> 
   <td>RedHat Linux</td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>CPU／コア</td> 
   <td>Intel(R) Xeon(R) CPU E5-2407 @2.40GHz、8 コア</td> 
   <td>Intel(R) Xeon(R) CPU E5-2407 @2.40GHz、8 コア</td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>RAM</td> 
   <td>32 GB</td> 
   <td>32 GB</td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>ディスク</td> 
   <td>磁気 - 1,000 IOPS を超える</td> 
   <td>磁気 - 1,000 IOPS を超える</td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>Java</td> 
   <td>Oracle JRE バージョン 8</td> 
   <td>該当なし</td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>JVM ヒープ 16 GB</td> 
   <td>16 GB</td> 
   <td>該当なし</td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>製品 </td> 
   <td>AEM 6.2</td> 
   <td>MongoDB 3.2 WiredTiger</td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>ノードストア</td> 
   <td>TarMK または MongoMK</td> 
   <td>該当なし</td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>データストア</td> 
   <td>ファイル DS </td> 
   <td>該当なし</td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>シナリオ</td> 
   <td><p><br /> 単一の製品：Assets／実行あたり 30 個の同時スレッド</p> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
 </tbody> 
</table>

### シナリオ 1 パフォーマンスベンチマークの結果 {#scenario-performance-benchmark-results}

![chlimage_1-12](assets/chlimage_1-12.png)

### シナリオ 2 技術仕様 {#scenario-technical-specifications-1}

>[!NOTE]
>
>1 つの TarMK システムと同数の MongoDB を使用して作成者を有効にするには、2 つのAEMノードを持つクラスターが必要です。 4 ノードの MongoDB クラスターは、1 つの TarMK インスタンスの 1.8 倍のオーサー数を処理できます。 8 ノードの MongoDB クラスターは、1 つの TarMK インスタンスの 2.3 倍のオーサー数を処理できます。

<table> 
 <tbody> 
  <tr> 
   <td><strong> </strong></td> 
   <td><strong>TarMK オーサーノード</strong></td> 
   <td><strong>MongoMK オーサーノード</strong></td> 
   <td><strong>MongoDB ノード</strong></td> 
  </tr> 
  <tr> 
   <td>サーバー</td> 
   <td>AWS c3.8xlarge</td> 
   <td>AWS c3.8xlarge</td> 
   <td>AWS c3.8xlarge</td> 
  </tr> 
  <tr> 
   <td>オペレーティングシステム</td> 
   <td>RedHat Linux</td> 
   <td>RedHat Linux</td> 
   <td>RedHat Linux</td> 
  </tr> 
  <tr> 
   <td>CPU／コア</td> 
   <td>32</td> 
   <td>32</td> 
   <td>32</td> 
  </tr> 
  <tr> 
   <td>RAM</td> 
   <td>60 GB</td> 
   <td>60 GB</td> 
   <td>60 GB</td> 
  </tr> 
  <tr> 
   <td>ディスク</td> 
   <td>SSD - 10k IOPS</td> 
   <td>SSD - 10k IOPS</td> 
   <td>SSD - 10k IOPS</td> 
  </tr> 
  <tr> 
   <td>Java</td> 
   <td>Oracle JRE バージョン 8</td> 
   <td><br /> Oracle JRE バージョン 8</td> 
   <td>該当なし</td> 
  </tr> 
  <tr> 
   <td>JVM ヒープ 16 GB</td> 
   <td>30 GB</td> 
   <td>30 GB</td> 
   <td>該当なし</td> 
  </tr> 
  <tr> 
   <td>製品 </td> 
   <td>AEM 6.2</td> 
   <td>AEM 6.2</td> 
   <td><br /> MongoDB 3.2 WiredTiger</td> 
  </tr> 
  <tr> 
   <td>ノードストア</td> 
   <td>TarMK </td> 
   <td>MongoMK</td> 
   <td><br /> 該当なし</td> 
  </tr> 
  <tr> 
   <td>データストア</td> 
   <td>ファイル DS </td> 
   <td><br /> ファイル DS</td> 
   <td><br /> 該当なし</td> 
  </tr> 
  <tr> 
   <td>シナリオ</td> 
   <td><p><br /> <br /> 垂直方向の使用例：メディア／2000 の同時スレッド</p> </td>
   <td></td>
   <td></td>
  </tr> 
 </tbody> 
</table>

### シナリオ 2 パフォーマンスベンチマークの結果 {#scenario-performance-benchmark-results-1}

![chlimage_1-13](assets/chlimage_1-13.png)

### AEM Sites および AEM Assets のアーキテクチャスケーラビリティのガイドライン {#architecture-scalability-guidelines-for-aem-sites-and-assets}

![chlimage_1-14](assets/chlimage_1-14.png)

## パフォーマンスガイドラインの概要  {#summary-of-performance-guidelines}

このページで説明するガイドラインの概要を次に示します。

* **ファイルデータストアを使用する TarMK** は、ほとんどのお客様にとって推奨されるアーキテクチャです。

   * 最小トポロジ：1 つのオーサーインスタンス、2 つのパブリッシュインスタンス、2 つの Dispatcher
   * ファイルデータストアが共有されている場合、バイナリレスレプリケーションはオンになります

* **ファイルデータストアを使用する MongoMK** は、オーサー層の水平方向の拡張性を実現するための推奨アーキテクチャです。

   * 最小トポロジ：3 つのオーサーインスタンス、3 つの MongoDB インスタンス、2 つのパブリッシュインスタンス、2 つの Dispatcher
   * ファイルデータストアが共有されている場合、バイナリレスレプリケーションはオンになります

* **ノードストア** は、NAS（ネットワーク接続型ストレージ）ではなく、ローカルディスクに保存する必要があります。
* **Amazon S3** を使用する場合：

   * Amazon S3 データストアは、オーサー層とパブリッシュ層の間で共有されます
   * バイナリレスレプリケーションを有効にする必要があります
   * データストアのガベージコレクションを使用するには、最初にすべてのオーサーノードとパブリッシュノードで実行し、次にオーサーノードで 2 回目に実行する必要があります

* **標準提供のインデックスに加えて、カスタムインデックスを作成する必要があります** 最も一般的な検索に基づく

   * Lucene インデックスは、カスタムインデックスに使用する必要があります

* **ワークフローをカスタマイズすると、パフォーマンスが大幅に向上する場合があります**。例えば、「アセットの更新」ワークフローのビデオ手順を削除したり、使用されないリスナーを削除したりします。

詳しくは、[推奨されるデプロイメント](/help/sites-deploying/recommended-deploys.md)のページも参照してください。
