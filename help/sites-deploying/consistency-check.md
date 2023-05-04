---
title: 整合性チェックとトラバーサルチェック
seo-title: Consistency and Traversal Checks
description: 整合性チェックとトラバーサルチェックの実行方法を説明します。
seo-description: Learn how to perform consistency and traversal checks.
uuid: 0304e378-7c60-4bf5-9052-d01149d2a6df
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.4/SITES
content-type: reference
discoiquuid: af9a3e9d-194a-42e5-be28-b238e0c1e55e
feature: Configuring
exl-id: 67dfa0f7-24ac-41ae-83c9-3bb1a8656502
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '192'
ht-degree: 81%

---

# 整合性チェックとトラバーサルチェック{#consistency-and-traversal-checks}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

アップグレード中に、ワークスペースの不整合による問題が発生することがあります。テストアップグレードを実行して不整合の問題が発生するかを確認できます。または、予防策として整合性チェックを実行できます。

テストアップグレードを実行した結果、ワークスペースの不整合によって失敗した場合は、crx-quickstart/logs/crx/error.log に次のようなエントリが表示されます。

```xml
*ERROR* TarPersistenceManager: No bundle found for uuid 'deadbeef-cafe-babe-cafe-babecafebabe'
 ...
*ERROR* RepositoryImpl: Failed to initialize workspace 'crx.default'
javax.jcr.RepositoryException: Error indexing workspace: Error indexing workspace: Error indexing workspace
...
```

## 整合性チェックの実行 {#perform-a-consistency-check}

整合性チェックを実行するには、JMX Mbean** com.adobe.granite (Repository)** の管理ページに移動します。AEM メイン画面から、次のように移動してください。

**ツール／web コンソール／メイン（メニューバー）／JMX／com.adobe.granite（リポジトリ）**

デフォルトのインストールでは、このページは次の場所にあります。**[|表示|](http://localhost:4502/system/console/jmx/com.adobe.granite%3Atype%3DRepository)**

ページの&#x200B;**操作**&#x200B;セクションには、**`traversalCheck`** と **`consistencyCheck`** の 2 つのメソッドがあります。チェックを実行するには、この操作をクリックして必要なパラメーターを入力します。

![chlimage_1-117](assets/chlimage_1-117.png)
