---
title: ログの使用
seo-title: Working with Logs
description: ログを操作してAEMのトラブルシューティングをおこなう方法を説明します。
seo-description: Learn how to troubleshoot AEM by working with logs.
uuid: b64e0b25-5228-4c2f-9cc1-dde524134026
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: operations
content-type: reference
discoiquuid: b4c1cb82-865b-48dd-b5c0-946e6610ce8e
exl-id: 201e2b57-17c0-4454-9b0e-026e2c95ac63
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '270'
ht-degree: 37%

---

# ログの使用{#working-with-logs}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

この節では、トラブルシューティングに役立つログに関する詳細情報を示します。

CRX は詳細なログを記録します。 クイックスタートを解凍して起動すると、次の場所にログが表示されます。

* crx-quickstart/launchpad/logs
* crx-quickstart/server/logs
* crx-quickstart/logs

## デバッグログレベルのアクティベート {#activating-the-debug-log-level}

デフォルトのログレベルは情報（INFO）であるため、デバッグ（DEBUG）メッセージはログに記録されません。

DEBUG ログレベルをアクティブにするには、CRX Explorer を使用して

```xml
/libs/sling/config/org.apache.sling.commons.log.LogManager/org.apache.sling.commons.log.level
```

このプロパティを debug に設定してください。多くのログが生成されるので、デバッグログレベルのログを不必要に長く残さないでください。

デバッグファイルの行は、通常は DEBUG で始まり、ログレベル、インストーラーのアクション、ログメッセージを示します。 次に例を示します。

```xml
DEBUG 3 WebApp Panel: WebApp successfully deployed
```

ログレベルは次のとおりです。

| 0 | 致命的なエラー | アクションに失敗したので、インストーラーを続行できません。 |
|---|---|---|
| 1 | エラー | アクションが失敗しました。 インストールは続行しますが、CRX の一部が正しくインストールされず、動作しません。 |
| 2 | 警告 | アクションは成功しましたが、問題が発生しました。 CRX が正しく動作する場合と動作しない場合があります。 |
| 3 | 情報 | アクションが成功しました。 |

## トラブルシューティングに使用する詳細オプション {#verbose-option-used-for-troubleshooting}

CRX の起動時には、次に示すように、–v（verbose）オプションをコマンドラインに追加できます。 &quot;

` java -jar crx-<*version*>-<*edition*>.jar -v`

verbose オプションでは quickstart のログ出力の一部がコンソールに表示されるので、このオプションをトラブルシューティングに使用してください。
