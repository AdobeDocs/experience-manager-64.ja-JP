---
title: AEM の基盤とリポジトリ
seo-title: AEM Foundation & Repository
description: Adobe Experience Manager 6.3 AEM プラットフォームとリポジトリ固有のリリースノート
seo-description: Release notes specific to Adobe Experience Manager 6.3 AEM Platform and Repository.
uuid: 147b38d0-cf87-467c-a52d-3399d4af7e6e
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.4
topic-tags: release-notes
content-type: reference
discoiquuid: e5dd9d0d-6d67-4430-aeb3-2be91356f624
exl-id: 6f131247-d35e-4298-958f-35b94ff08c58
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '719'
ht-degree: 82%

---

# AEM の基盤とリポジトリ {#aem-foundation-repository}

## 変更について {#list-of-changes}

### リポジトリー {#repository}

* Oak セグメント Tar マイクロカーネル

   * オンラインでのリビジョンクリーンアップの高速コンパクションモード（テールコンパクション）
   * 書き込み速度の向上
   * セグメント操作の統計情報が JMXBean を通じて公開
   * オフラインリビジョンクリーンアップの所要時間の見積もり

* Oak Mongo マイクロカーネル

   * スケジュールに従ったクリーンアップメンテナンスの代わりに、MongoMK の継続的なリビジョンクリーンアップが実行されるようになりました。

* ドキュメントノードストアに対するリビジョンクリーンアップの効率が向上しました。
* 詳しくは、 [Apache Jackrabbit Oak Jira v. 1.8.0](https://archive.apache.org/dist/jackrabbit/oak/1.8.0/RELEASE-NOTES.txt), [Apache Jackrabbit Oak Jira v. 1.8.1](https://archive.apache.org/dist/jackrabbit/oak/1.8.1/RELEASE-NOTES.txt) および [Apache Jackrabbit Oak Jira v. 1.8.2](https://archive.apache.org/dist/jackrabbit/oak/1.8.2/RELEASE-NOTES.txt) 修正された問題の完全な概要を参照してください。

>[!CAUTION]
>
>* AEM 6.3 以降の新しいバージョンの Oak Segment Tar では、リポジトリを移行する必要があります。この手順は、古いバージョンの TarMK からアップグレードする場合、または別のタイプの格納機能から新しい Segment Tar に切り替える場合に必須です。新しい Segment Tar のメリットについて詳しくは、[Oak Segment Tar への移行に関する FAQ](/help/sites-deploying/revision-cleanup.md#migrating-to-oak-segment-tar) を参照してください。
>


### 検索とインデックス作成 {#search-amp-indexing}

* oak-run（CLI）を使用したインデックス作成操作のサポートが強化されました。

   * インデックスの整合性チェック
   * インデックス作成に関する統計情報の提供
   * インデックス設定の読み込み／書き出し
   * インデックス再作成

* Lucene 関連リポジトリのサイズの増大を抑えることで、システム全体のパフォーマンスが向上しました。
* 同期 Lucene プロパティインデックス[（詳細情報）](https://wiki.apache.org/jackrabbit/Synchronous%20Lucene%20Property%20Indexes)
* インデックスマネージャーの「クエリの説明を実行」で AEM QueryBuilder 構文がサポートされるようになりました。
* インデックスマネージャーでインデックス指標（サイズ、最終更新日時、整合性チェック）が公開されるようになりました。

### ユーザーインターフェイス {#user-interface}

* UI に対して様々な機能強化がおこなわれ、生産性と使いやすさが向上しました。
* 新しいコンテンツツリーレールで階層内をすばやく移動できます。これをリスト表示と組み合わせれば、クラシック UI インタラクションモデルに戻すことができます。
* 大きいフォルダーのカード表示とリスト表示でスクロール操作が向上しました。
* 検索結果の操作性が向上しました - 「戻る」ボタンをクリックすると、前の検索結果に戻ります。
* 最もよく使用されるアクション（特定のレールを開く、項目を編集、移動、削除する、プロパティを開くなど）のキーボードショートカットが追加定義されました。
* キーボードショートカットを無効にできます（環境設定で有効／無効を切り替えます）。
* すべての UI で 7 日後にタイムスタンプが非表示になります（環境設定でデフォルトを設定します）。

>[!CAUTION]
>
>* クラシック UI の機能がさらに強化される予定はありません。AEM 6.4 にはクラシック UI が含まれており、以前のリリースからアップグレードするお客様はクラシック UI をそのまま使用し続けることができます。クラシック UI は非推奨の間も完全にサポートされ続けます [詳細を表示](/help/sites-deploying/ui-recommendations.md).
>


### コンテンツの配布 {#content-distribution}

* レプリケーションのパフォーマンスが向上し、大量アセットの公開に対応できるようになりました。
* 配布トランスポートでの OAuth 2.0 認証をサポートしています。
* VLT パッケージの場合のパフォーマンスが向上しました。

### モニタリング {#monitoring}

* 新しい「システム概要」には、パフォーマンスに関するすべてのシステムステータスとアクティビティのスナップショットが表示されます
* 以下の新しいヘルスチェックが用意されています。

   * 大きい Lucene インデックスの検出
   * 非同期インデックス作成のヘルス
   * 大きい Lucene インデックス
   * クエリーパフォーマンス
   * クエリトラバーサルの制限
   * 同期済みのクロック
   * システムメンテナンス - リビジョンクリーンアップ
   * システムメンテナンス - データストア GC
   * システムメンテナンス - 連続リビジョン GC

* status.zip のダウンロードの範囲をユーザーが指定できるようになりました。

### メンテナンス {#maintenance}

* メンテナンスタスクでの Lucene バイナリのアクティブ削除
* MongoDB の RevisionGC メンテナンスタスクは無効になり、代わりに連続リビジョンクリーンアップが使用されます。上記の「リポジトリ」の節を参照してください。
* バージョンのパージ設定により、保持するバージョンの数を最小限に抑えることができます。
* バージョンのパージはメンテナンスウィンドウの終了時に停止します。手動で開始および停止することもでき、次回開始したときには、増分的に続行されます。

### アップグレード {#upgrade}

* 下位互換性：AEM 6.4の機能には下位互換性があるので、カスタムコードはほとんどの場合そのまま動作し、アップグレードの労力を削減できます。
* アップグレードの複雑さの評価：新しいパターン検出ツールにより、アップグレードの複雑さを評価することができます。
* 持続可能なアップグレード：API サーフェスとコンテンツ分類が導入され、開発サイクル全体を通して次のバージョンに効率的かつシームレスにアップグレードするためのベストプラクティスに容易に従えるようになりました。
* リポジトリの再構築：大幅な再構築（主に/etc）により、アップグレードが容易になり、実装のベストプラクティスが促進されます。 （[詳細情報](/help/sites-deploying/repository-restructuring.md)）。
* 詳しくは、 [アップグレードドキュメント](/help/sites-deploying/upgrade.md) を参照してください。

### Cloud Services {#cloud-services}

* 多くのCloud Servicesは、タッチ UI から設定できるようになりました。残りの設定は、「レガシーCloud Services」カードでおこなえます。
* Sites フォルダーと Assets フォルダーは、コンテキスト対応の方法で読み込まれるCloud Servicesーを使用して設定できます。

### セキュリティ {#security}

* ユーザー作成 UI が機能強化および簡素化され、複数のユーザープロファイルをサポートするようになりました。
* ユーザーのグループメンバーシップが多数ある場合のパフォーマンスが向上しました。

### プロジェクトとワークフロー {#projects-and-workflows}

* タッチ UI ベースのワークフローエディターで、より効率的にワークフローモデルを管理できるようになりました。
* メンテナンスタスクでプロジェクトタスクのパージをサポートするようになりました。
