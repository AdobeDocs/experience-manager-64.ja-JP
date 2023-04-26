---
title: デプロイのベストプラクティス
seo-title: Deploying Best Practices
description: ベストプラクティスのデプロイと保守。
seo-description: Deploying and maintaining best practices.
uuid: 4546ed2c-43d5-40f3-874f-567b324e78c2
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.4/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 4b5c0677-c630-4fae-867e-4f4583ac8507
exl-id: 0c8fefb5-6fa0-4fab-a890-9f5ae7508459
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '430'
ht-degree: 73%

---

# デプロイのベストプラクティス{#deploying-best-practices}

デプロイのベストプラクティスでは、AEM を可能な限り効率的かつ効果的にデプロイまたは保守する方法を説明しています。AEM の様々な領域を対象としたトピックが順次追加されています。

次の領域について、ベストプラクティスのデプロイと保守、および推奨事項に関するドキュメントが提供されています。

* [Oak](#oak)
* [Communities](#communities)
* [UI](#ui)
* [パフォーマンス](#performance)

管理、開発、オーサリングのベストプラクティスについては、次のページを参照してください。

* [管理のベストプラクティス](/help/sites-administering/administer-best-practices.md)
* [開発のベストプラクティス](/help/sites-developing/best-practices.md)
* [オーサリングのベストプラクティス](/help/sites-authoring/best-practices.md)

以下の表では、特定のドキュメントについて説明し、リンクします。

## Oak {#oak}

[Oak](/help/sites-deploying/platform.md) は、AEM の基礎となっている、拡張性の高い高性能の階層コンテンツリポジトリです。

<table> 
 <tbody>
  <tr>
   <td><p>スケーラビリティ、パフォーマンスおよびディザスタリカバリ</p> </td> 
   <td><a href="/help/sites-deploying/performance.md">パフォーマンスとスケーラビリティ</a></td> 
   <td>技術的な俊敏性、高いパフォーマンス、および健全な災害復旧機能について説明するホワイト・ペーパー</td> 
  </tr>
  <tr>
   <td>推奨される OAK デプロイメント</td> 
   <td><a href="/help/sites-deploying/recommended-deploys.md">推奨されるデプロイメント</a></td> 
   <td>デプロイメントシナリオを説明します</td> 
  </tr>
  <tr>
   <td>Mongo トポロジ</td> 
   <td><a href="/help/sites-deploying/recommended-deploys.md">Mongo トポロジのベストプラクティス</a></td> 
   <td>Mongo トポロジを説明します。使用するトポロジはいつかを示します。</td> 
  </tr>
  <tr>
   <td>データストアオプション</td> 
   <td><a href="/help/sites-deploying/data-store-config.md">ノードストアとデータストアの設定</a></td> 
   <td>このドキュメントでは、バイナリデータとコンテンツノードの保存に関するベストプラクティスを説明します。 Amazon S3 データストアの使用に関する情報が含まれます。</td> 
  </tr>
  <tr>
   <td>OAK で検索</td> 
   <td><a href="/help/sites-deploying/best-practices-for-queries-and-indexing.md">クエリとインデックス作成のベストプラクティス</a><br /> </td> 
   <td>コンテンツのインデックス作成方法に関するベストプラクティスについて説明します。</td> 
  </tr>
 </tbody>
</table>

## Communities {#communities}

AEM Communities を使用すると、オンプレミスのコミュニティの作成と管理が容易になります。AEM Communities のベストプラクティスは、こちらで説明しています。

[コミュニティコンテンツストア](/help/communities/working-with-srp.md) - ユーザー生成コンテンツ（UGC）のための新しい共有ストレージ機能と、基盤となる[ トポロジー](/help/communities/topologies.md)の選択に関する考察について説明しています。

[コミュニティの推奨デプロイメント](/help/sites-deploying/recommended-deploys.md#considerations-for-aem-communities) - Communities の推奨されるデプロイメントについて説明します。|

## UI {#ui}

ユーザーインターフェイスに関するベストプラクティスは、こちらで説明しています。

[顧客向けのユーザーインターフェイスの推奨事項](/help/sites-deploying/ui-recommendations.md)

AEM には現在、クラシック UI とタッチ操作向け UI の 2 つが同じリリースに含まれています。そのため、どちらを使用するかを、プロジェクトの実装時にユーザーが決断する必要があります。このドキュメントは、適切な選択肢を見つける際に役立ちます。

## パフォーマンス {#performance}

パフォーマンスに関するベストプラクティスを次に示します。

<table> 
 <tbody>
  <tr>
   <td>品質保証のベストプラクティス</td> 
   <td><a href="/help/sites-deploying/configuring-performance.md#best-practices-for-quality-assurance">品質保証のベストプラクティス</a></td> 
   <td>特に<em>パブリッシュ</em>環境のパフォーマンステストのテストコンセプトを定義する際の問題を標準的な観点から概説します。これは主に、QA エンジニア、プロジェクトマネージャー、システム管理者が関心を持ちます。</td> 
  </tr>
  <tr>
   <td>CDN での Dispatcher の使用</td> 
   <td><a href="https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=ja#using-dispatcher-with-a-cdn">CDN での Dispatcher の使用</a></td> 
   <td>Akamai Edge Delivery または Amazon Cloud Front などのコンテンツ配信ネットワーク（CDN）は、エンドユーザーに近い場所からコンテンツを配信します。</td> 
  </tr>
  <tr>
   <td>パフォーマンスの最適化</td> 
   <td><a href="/help/sites-deploying/configuring-performance.md">パフォーマンスの最適化</a></td> 
   <td>主な問題は、Web サイトが訪問者のリクエストに応えるのに要する時間です。</td> 
  </tr>
  <tr>
   <td>パフォーマンステスト</td> 
   <td><a href="/help/sites-deploying/best-practices-for-performance-testing.md">パフォーマンステストのベストプラクティス</a></td> 
   <td>AEM のデプロイメントのパフォーマンステストを実行する際のベストプラクティスについて説明します。<br /> </td> 
  </tr>
 </tbody>
</table>
