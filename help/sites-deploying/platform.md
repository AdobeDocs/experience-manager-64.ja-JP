---
title: AEM プラットフォームの概要
seo-title: Introduction to the AEM Platform
description: この記事では、AEMプラットフォームとその最も重要なコンポーネントの概要を説明します。
seo-description: This article provides a general overview of the AEM platform and its most important components.
uuid: 214d4c49-1f5c-432c-a2c0-c1fbdceee716
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: platform
content-type: reference
discoiquuid: fccf9a0f-ebab-45ab-8460-84c86b3c4192
legacypath: /content/docs/en/aem/6-0/deploy/upgrade/introduction-to-oak
exl-id: afd8f9ab-ae44-4845-9cb4-f6e28a35ad27
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '805'
ht-degree: 30%

---

# AEM プラットフォームの概要{#introduction-to-the-aem-platform}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

AEM 6 の AEM プラットフォームは、Apache Jackrabbit Oak に基づいています。

Apache Jackrabbit Oak は、昨今の世界規模の web サイトや、要求の厳しいその他のコンテンツアプリケーションの基盤として使用する、スケーラビリティとパフォーマンスに優れた階層構造のコンテンツリポジトリを実装するための取り組みです。

これは Jackrabbit 2 の後継であり、コンテンツリポジトリである CRX のデフォルトのバックエンドとして AEM 6 で使用しています。

## 設計の原則と目的 {#design-principles-and-goals}

Oak が [JSR-283](https://www.day.com/day/en/products/jcr/jsr-283.html) (JCR 2.0) 仕様。 主な設計目標は次のとおりです。

* 大きなリポジトリのサポートの向上
* 高可用性を実現する複数の分散クラスタノード
* パフォーマンスの向上
* 多数の子ノードおよびアクセス制御レベルのサポート

## アーキテクチャの概念 {#architecture-concept}

![chlimage_1-84](assets/chlimage_1-84.png)

### ストレージ {#storage}

ストレージ層の目的は次のとおりです。

* ツリーモデルの実装
* ストレージをプラグ可能にする
* クラスタリングメカニズムの提供

### Oak Core {#oak-core}

Oak Core は、ストレージレイヤーに複数のレイヤーを追加します。

* アクセスレベル制御
* 検索およびインデックス作成
* 監視

### Oak JCR {#oak-jcr}

Oak JCR の主な目的は、JCR セマンティクスをツリー操作に変換することです。また、次の役割も果たします。

* JCR API の実装
* JCR 制約を実装するコミットフックの格納

また、Oak JCR の概念の一環として、Java 以外の実装も可能になりました。

## ストレージの概要 {#storage-overview}

Oak ストレージレイヤーは、コンテンツの実際のストレージの抽象化レイヤーを提供します。

現在、AEM6 では 2 つのストレージ実装（**Tar ストレージ**&#x200B;と **MongoDB ストレージ**）を使用できます。

### Tar ストレージ {#tar-storage}

Tar ストレージは tar ファイルを使用します。 これにより、大きなセグメント内の様々なタイプのレコードとしてコンテンツが保存されます。 ジャーナルは、リポジトリの最新の状態を追跡するために使用されます。

デザインに関する主要な原則は、次のとおりです。

* **不変セグメント**

コンテンツは、最大 256 KiB のサイズのセグメントに保存されます。 このセグメントは不変であり、そのため、頻繁にアクセスされるセグメントを簡単にキャッシュして、リポジトリの破損につながるシステムエラーを削減できます。

各セグメントは、一意の識別子 (UUID) で識別され、コンテンツツリーの連続したサブセットを含みます。 また、セグメントは他のコンテンツを参照できます。 各セグメントには、参照先の他のセグメントの UUID のリストが保持されます。

* **市区町村**

ノードやその直近の子などの関連レコードは、通常、同じセグメントに保存されます。 これにより、リポジトリの検索が非常に高速になり、セッションごとに複数の関連ノードにアクセスする一般的なクライアントのキャッシュミスのほとんどが回避されます。

* **コンパクト**

レコードのフォーマットは、IO コストを削減し、キャッシュにできるだけ多くのコンテンツを収めるために、サイズに合わせて最適化されます。

### Mongo ストレージ {#mongo-storage}

MongoDB ストレージは、MongoDB を利用して、シャーディングとクラスタリングをおこないます。 リポジトリツリーは、1 つの MongoDB データベースに保存されます。各ノードは別々のドキュメントです。

これにはいくつかの特殊性があります。

* 改訂

コンテンツの更新（コミット）ごとに、新しいリビジョンが作成されます。 リビジョンは、基本的に次の 3 つの要素で構成される文字列です。

1. 生成されたマシンのシステム時刻から得られるタイムスタンプ。
1. 同じタイムスタンプで作成されたリビジョンを区別するためのカウンター
1. リビジョンが作成されたクラスターノード ID

* ブランチ

ブランチがサポートされ、クライアントは複数の変更をステージングし、1 回の結合呼び出しで表示できるようになります。

* 前のドキュメント

MongoDB ストレージは、変更のたびにドキュメントにデータを追加します。 ただし、クリーンアップが明示的にトリガーされた場合にのみ、データが削除されます。 特定のしきい値に達すると、古いデータが移動されます。 以前のドキュメントには不変データのみが含まれています。つまり、コミットおよびマージされたリビジョンのみが含まれています。

* クラスターノードのメタデータ

クラスタの操作を容易にするため、アクティブなクラスタノードと非アクティブなクラスタノードに関するデータは、データベースに保持されます。

MongoDB ストレージを使用した一般的な AEM クラスターのセットアップは次のようになります。

![chlimage_1-85](assets/chlimage_1-85.png)

## Jackrabbit 2 との違いは何ですか。 {#what-is-different-from-jackrabbit}

Oak は JCR 1.0 標準との後方互換性を保つように設計されているので、ユーザーレベルではほとんど変更されません。 ただし、Oak ベースのAEMのインストールを設定する際に考慮する必要がある顕著な違いがいくつかあります。

* Oak ではインデックスが自動的に作成されません。そのため、必要に応じてカスタムインデックスを作成する必要があります。
* セッションは常にリポジトリの最新の状態を反映する Jackrabbit 2 とは異なり、Oak を使用すると、セッションは、セッションが取得された時点からのリポジトリの安定した表示を反映します。 これは、Oak が基にしている MVCC モデルが原因です。
* 同じ名前の兄弟（SNS）は Oak ではサポートしていません。

## その他の Platform 関連ドキュメント {#other-platform-related-documentation}

AEMプラットフォームの詳細については、以下の記事も参照してください。

* [AEM 6 でのノードストアとデータストアの設定](/help/sites-deploying/data-store-config.md)
* [Oak クエリとインデックス作成](/help/sites-deploying/queries-and-indexing.md)
* [AEM 6 のストレージ要素](/help/sites-deploying/storage-elements-in-aem-6.md)
* [MongoDB を備えた AEM](/help/sites-deploying/aem-with-mongodb.md)
