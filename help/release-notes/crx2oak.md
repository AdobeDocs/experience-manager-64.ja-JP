---
title: CRX2OAK 移行ツール
seo-title: CRX2OAK Migration Tool
description: リリースノート (Adobe Experience Manager 6.4 CRX2OAK 移行ツールに固有 )
seo-description: Release notes specific to the Adobe Experience Manager 6.4 CRX2OAK Migration tool.
uuid: 1b582faf-2dc6-41a2-9419-7e82347f9d6c
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.4
topic-tags: release-notes
content-type: reference
discoiquuid: cfdaceac-a5b3-4070-ad4c-f1457b1e2e4b
exl-id: 441c8ba0-f8b2-4c2c-b7be-cfdad9e1e498
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '288'
ht-degree: 2%

---

# CRX2OAK 移行ツール {#crx-oak-migration-tool}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

## 変更点および修正点の一覧 {#list-of-changes-and-fixes}

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
* CQ-97488 AEM実行モードの昇格と削除（sling.options.file の書き換えによる）
* GRANITE-12798/OAK-4260 Oak セグメントから Oak セグメント Tar にサイドグレードする機能

### バージョン 1.4.2（2016 年 3 月） {#version-march-1}

* Oak バージョンを 1.4.1 にアップグレード
* OAK-3846 / GRANITE-10748 SNS ノードがノードタイプの制約に違反している場合に名前を変更する
* OAK-3910/GRANITE-10730から継承するノードの移行 `mix:versionable` バージョン履歴なし
* OAK-4128 / GRANITE-11757 `RepositorySidegrade` ルートノードのプロパティをコピーしない

### バージョン 1.3.4（2016 年 1 月） {#version-january}

* Oak バージョンを 1.3.16 にアップグレード
* OAK-3844 / GRANITE-10730バージョン履歴のないバージョン管理可能なノードのサポートの向上
* OAK-3846 SNS ノードがノードタイプの制約に違反している場合に名前を変更する

### バージョン 1.3.2（2015 年 12 月） {#version-december}

* Oak バージョンを 1.3.12 にアップグレード
* 移行後にデータストアディレクトリを移動しないでください (GRANITE-10447)
* crx2oak-quickstart-extension と crx2oak のマージ (CQ-61847)
* リポジトリ内の重複値で crx2oak が失敗する (CQ-61906)
* CQ 5.x からの移行後に長いAEMが起動します (GRANITE-10309)
* crx2oak での複数の LDAP サーバーのサポート (GRANITE-9917)
* ノード名の最大長のチェックを実施 (OAK-3111)
* S3DataSource を移行ソースとしてサポート (OAK-3685)
