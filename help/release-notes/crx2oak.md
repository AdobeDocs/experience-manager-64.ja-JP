---
title: CRX2OAK 移行ツール
seo-title: CRX2OAK Migration Tool
description: リリースノート（Adobe Experience Manager 6.4 CRX2OAK 移行ツール）
seo-description: Release notes specific to the Adobe Experience Manager 6.4 CRX2OAK Migration tool.
uuid: 1b582faf-2dc6-41a2-9419-7e82347f9d6c
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.4
topic-tags: release-notes
content-type: reference
discoiquuid: cfdaceac-a5b3-4070-ad4c-f1457b1e2e4b
exl-id: 441c8ba0-f8b2-4c2c-b7be-cfdad9e1e498
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '252'
ht-degree: 63%

---

# CRX2OAK 移行ツール {#crx-oak-migration-tool}

## 変更点と修正点のリスト {#list-of-changes-and-fixes}

### 1.8.6（2018 年 6 月） {#june}

* OAK-7339 LoopbackBlobStore を導入することで、MissingBlobStore での UnsupportedOperationException でのすべてのサイドの障害を修正しました。
* Oak 1.8.4 の使用

### 1.8.4（2018 年 4 月） {#april}

* Oak バージョン 1.8.2 の使用
* GRANITE-18104 6.3 から 6.4 へのリポジトリ移行エラーは、より意味のあるものにする必要がある
* GRANITE-16571 SHA-1 の使用を置き換える

   * —version オプションを使用した場合、ツールチェックサムが SHA-512 になりました。

* GRANITE-17601 CRX2Oak で oak-blob-cloud を使用して oak-upgrade を埋め込む
* GRANITE-18553 crx2oak は、バージョンが移行されていない場合でも、バージョンプロパティをノードに残します。

### バージョン 1.6.8（2017 年 3 月） {#version-march}

* Oak バージョンを 1.6.1 に更新しました。
* CQ-61847 crx2oak-quickstart-extension と crx2oak のマージ（移行プロファイルの追加）
* CQ-97488 AEM 実行モードのプロモートおよびドロップ（sling.options.file の書き直しによる）
* GRANITE-12798/OAK-4260 Oak セグメントから Oak セグメント Tar にサイドグレードする機能

### バージョン 1.4.2（2016 年 3 月） {#version-march-1}

* Oak バージョン 1.4.1 へのアップグレード
* OAK-3846／GRANITE-10748 SNS ノードがノードタイプ制約に違反している場合は名前を変更する
* OAK-3910／GRANITE-10730 バージョン履歴のない `mix:versionable` から継承されるノードの移行
* OAK-4128／GRANITE-11757 `RepositorySidegrade` でルートのノードプロパティがコピーされない

### バージョン 1.3.4（2016 年 1 月） {#version-january}

* Oak バージョン 1.3.16 へのアップグレード
* OAK-3844／GRANITE-10730 バージョン履歴のないバージョン管理可能なノードのサポートの強化
* OAK-3846 SNS ノードがノードタイプ制約に違反している場合は名前を変更する

### バージョン 1.3.2（2015 年 12 月） {#version-december}

* Oak バージョン 1.3.12 へのアップグレード
* 移行後にデータストアディレクトリを移動しないこと（GRANITE-10447）
* crx2oak-quickstart-extension と crx2oak の統合（CQ-61847）
* リポジトリにある重複値が原因で crx2oak がエラーになる（CQ-61906）
* CQ 5.x から移行後に AEM の起動時間が長い（GRANITE-10309）
* crx2oak での複数の LDAP サーバーのサポート（GRANITE-9917）
* ノード名の最大長チェックを適用する（OAK-3111）
* 移行のソースとして S3DataSource をサポート（OAK-3685）
