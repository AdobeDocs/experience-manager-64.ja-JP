---
title: CRX2OAK 移行ツール
seo-title: CRX2OAK 移行ツール
description: リリースノート（Adobe Experience Manager 6.4 CRX2OAK 移行ツール）
seo-description: リリースノート（Adobe Experience Manager 6.4 CRX2OAK 移行ツール）
uuid: 1b582faf-2dc6-41a2-9419-7e82347f9d6c
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.4
topic-tags: release-notes
content-type: reference
discoiquuid: cfdaceac-a5b3-4070-ad4c-f1457b1e2e4b
exl-id: 441c8ba0-f8b2-4c2c-b7be-cfdad9e1e498
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '268'
ht-degree: 62%

---

# CRX2OAK 移行ツール {#crx-oak-migration-tool}

## 変更点と修正点のリスト {#list-of-changes-and-fixes}

### 1.8.6（2018年6月） {#june}

* OAK-7339 LoopbackBlobStoreを導入することで、MissingBlobStoreでUnsupportedOperationExceptionで障害が発生するすべてのサイドデレイを修正しました。
* Oak 1.8.4の使用

### 1.8.4（2018年4月） {#april}

* Oakバージョン1.8.2の使用
* GRANITE-18104 6.3から6.4へのリポジトリ移行エラーは、より意味のあるものにする必要がある
* GRANITE-16571 SHA-1の使用の置き換え

   * —versionオプションを使用する場合、ツールチェックサムがSHA-512になりました。

* GRANITE-17601 oak-blob-cloudを使用したCRX2Oakでのoak-upgradeの埋め込み
* GRANITE-18553 crx2oakは、バージョンが移行されない場合でも、バージョンプロパティをノードに残します。

### バージョン1.6.8（2017年3月） {#version-march}

* Oakバージョンを1.6.1に更新しました
* CQ-61847 crx2oak-quickstart-extensionとcrx2oakの統合（移行プロファイルの追加）
* CQ-97488 AEM 実行モードのプロモートおよびドロップ（sling.options.file の書き直しによる）
* GRANITE-12798/OAK-4260 OakセグメントからOakセグメントTarへのサイドグレード機能

### バージョン1.4.2（2016年3月）{#version-march-1}

* Oak バージョン 1.4.1 へのアップグレード
* OAK-3846／GRANITE-10748 SNS ノードがノードタイプ制約に違反している場合は名前を変更する
* OAK-3910／GRANITE-10730 バージョン履歴のない `mix:versionable` から継承されるノードの移行
* OAK-4128／GRANITE-11757 `RepositorySidegrade` でルートのノードプロパティがコピーされない

### バージョン1.3.4（2016年1月）{#version-january}

* Oak バージョン 1.3.16 へのアップグレード
* OAK-3844／GRANITE-10730 バージョン履歴のないバージョン管理可能なノードのサポートの強化
* OAK-3846 SNS ノードがノードタイプ制約に違反している場合は名前を変更する

### バージョン1.3.2（2015年12月） {#version-december}

* Oak バージョン 1.3.12 へのアップグレード
* 移行後にデータストアディレクトリを移動しないこと（GRANITE-10447）
* crx2oak-quickstart-extension と crx2oak の統合（CQ-61847）
* リポジトリにある重複値が原因で crx2oak がエラーになる（CQ-61906）
* CQ 5.x から移行後に AEM の起動時間が長い（GRANITE-10309）
* crx2oak での複数の LDAP サーバーのサポート（GRANITE-9917）
* ノード名の最大長チェックを適用する（OAK-3111）
* 移行のソースとして S3DataSource をサポート（OAK-3685）
