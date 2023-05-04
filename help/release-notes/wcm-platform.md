---
title: AEM Foundation & Repository
seo-title: AEM Foundation & Repository
description: リリースノート (Adobe Experience Manager 6.3 AEM Platform とリポジトリに固有 )
seo-description: Release notes specific to Adobe Experience Manager 6.3 AEM Platform and Repository.
uuid: 147b38d0-cf87-467c-a52d-3399d4af7e6e
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.4
topic-tags: release-notes
content-type: reference
discoiquuid: e5dd9d0d-6d67-4430-aeb3-2be91356f624
exl-id: 6f131247-d35e-4298-958f-35b94ff08c58
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '755'
ht-degree: 9%

---

# AEM Foundation &amp; Repository {#aem-foundation-repository}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

## 変更について {#list-of-changes}

### リポジトリ {#repository}

* Oak Segment Tar MicroKernel

   * オンラインでのリビジョンクリーンアップの高速コンパクションモード（テールコンパクション）
   * 書き込み率の向上
   * JMXBean を介して公開されたセグメント操作の統計
   * オフラインでのリビジョンクリーンアップの期間の推定値

* Oak Mongo Microkernel

   * MongoMK の継続的なリビジョンクリーンアップは、定期的なクリーンアップメンテナンスに代わるものです

* ドキュメントノードストアでのリビジョンクリーンアップの効率が向上しました。
* 詳しくは、 [Apache Jackrabbit Oak Jira v. 1.8.0](https://archive.apache.org/dist/jackrabbit/oak/1.8.0/RELEASE-NOTES.txt), [Apache Jackrabbit Oak Jira v. 1.8.1](https://archive.apache.org/dist/jackrabbit/oak/1.8.1/RELEASE-NOTES.txt) および [Apache Jackrabbit Oak Jira v. 1.8.2](https://archive.apache.org/dist/jackrabbit/oak/1.8.2/RELEASE-NOTES.txt) 修正された問題の完全な概要を参照してください。

>[!CAUTION]
>
>* AEM 6.3 以降の新しいバージョンの Oak Segment Tar では、リポジトリを移行する必要があります。古いバージョンの TarMK からアップグレードする場合や、別のタイプの永続性から新しいセグメント Tar を切り替える場合は、この手順が必須です。 新しいセグメント Tar の利点について詳しくは、 [Oak Segment Tar への移行に関する FAQ](/help/sites-deploying/revision-cleanup.md#migrating-to-oak-segment-tar).
>


### 検索とインデックス作成 {#search-amp-indexing}

* oak-run(CLI) を使用したインデックス作成操作のサポートが強化されました。

   * インデックスの整合性チェック
   * インデックス作成統計
   * インデックス設定の読み込み/書き出し
   * インデックス再作成

* Lucene 関連のリポジトリの増加が減少し、システム全体のパフォーマンスが向上
* 同期 Lucene プロパティインデックス [（詳細情報）](https://wiki.apache.org/jackrabbit/Synchronous%20Lucene%20Property%20Indexes)
* インデックスマネージャーのクエリの説明を実行で、AEM QueryBuilder 構文がサポートされるようになりました。
* インデックスマネージャはインデックス指標を公開しています：サイズ、最終更新日、整合性チェック

### ユーザーインターフェイス {#user-interface}

* UI に様々な機能強化が加えられ、生産性を高め、使いやすくなりました。
* 新しいコンテンツツリーレールで階層をすばやく移動できるようになりました。 リストビューと組み合わせて、クラシック UI のインタラクションモデルが復元されます。
* 大きなフォルダーのカード表示とリスト表示でのスクロールを改善しました。
* 検索結果とのやり取りが改善されました。「戻る」ボタンをクリックすると、前の検索結果に戻ります。
* 特定のレールを開く、項目を編集、移動および削除する、プロパティを開くなど、ほとんどの一般的なアクションに対するキーボードショートカットが追加されました。
* キーボードショートカットを無効にする機能（環境設定での有効/無効）。
* 7 日後にすべての UI でタイムスタンプの表示を停止します（環境設定でデフォルトに設定）。

>[!CAUTION]
>
>* Adobeは、クラシック UI をさらに強化する予定はありません。 AEM 6.4 にはクラシック UI が含まれており、以前のリリースからアップグレードするお客様はクラシック UI をそのまま使用できます。 クラシック UI は非推奨の間も完全にサポートされ続けます [詳細を表示](/help/sites-deploying/ui-recommendations.md).
>


### コンテンツの配布 {#content-distribution}

* 大量のアセットの公開をサポートするため、レプリケーションパフォーマンスが向上
* 配布トランスポートでの OAuth 2.0 認証をサポート
* VLT パッケージのパフォーマンスの向上

### モニタリング {#monitoring}

* 新しい「システム概要」には、パフォーマンスに関するすべてのシステムステータスとアクティビティのスナップショットが表示されます
* 新しいヘルスチェック：

   * 大きな Lucene インデックスの検出
   * 非同期インデックス作成のヘルス
   * 大きい Lucene インデックス
   * クエリーパフォーマンス
   * クエリトラバーサルの制限
   * 同期済みのクロック
   * システムメンテナンス — リビジョンクリーンアップ
   * システムメンテナンス — DataStore GC
   * システムメンテナンス — 継続的なリビジョン GC

* status.zip ダウンロードの範囲を定義できるようになりました。

### メンテナンス {#maintenance}

* メンテナンスタスクを使用した Lucene バイナリのアクティブな削除
* MongoDB の RevisionGC メンテナンスタスクが無効になり、継続的なリビジョンクリーンアップが優先されました。前述の「リポジトリ」の節を参照してください。
* バージョンのパージ設定により、最小限のバージョン数を保持できます
* バージョンのパージは、メンテナンスウィンドウの終わりに停止します。 また、手動で開始および停止することもでき、次の開始時に段階的に続行します。

### アップグレード {#upgrade}

* 後方互換性：6.4 の後方互換性のある機能により、ほとんどの場合、カスタムコードの互換性を維持し、アップグレードの作業を軽減できます。
* アップグレードの複雑性の評価：新しいパターン検出ツールを使用して、アップグレードの複雑さを評価できます。
* 持続可能なアップグレード：開発サイクル全体を通じて次のバージョンへの効率的かつシームレスなアップグレードを実現するために、ベストプラクティスに簡単に従うために導入された API 表面およびコンテンツ分類。
* リポジトリの再構築：大幅な再構築（主に/etc）により、アップグレードが容易になり、実装のベストプラクティスが促進されます。 [詳細を表示](/help/sites-deploying/repository-restructuring.md)
* 詳しくは、 [アップグレードドキュメント](/help/sites-deploying/upgrade.md) を参照してください。

### Cloud Services {#cloud-services}

* 多くのCloud Servicesは、タッチ UI から設定できるようになりました。残りの設定は、「レガシーCloud Services」カードでおこなえます。
* Sites フォルダーと Assets フォルダーは、コンテキスト対応の方法で読み込まれるCloud Servicesーを使用して設定できます。

### セキュリティ {#security}

* 複数のユーザープロファイルをサポートする、ユーザー作成 UI の強化とシンプル化。
* ユーザーの大きなグループメンバーシップに対するパフォーマンスが向上しました。

### プロジェクトとワークフロー {#projects-and-workflows}

* タッチ操作対応 UI ベースのワークフローエディターを使用して、より効率的な方法でワークフローモデルを管理できます。
* メンテナンスタスクでのプロジェクトタスクのパージのサポート。
