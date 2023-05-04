---
title: パターン検出を使用したアップグレードの複雑性の評価
seo-title: Assessing the Upgrade Complexity with the Pattern Detector
description: パターン検出を使用して、アップグレードの複雑さを評価する方法を説明します。
seo-description: Learn how to use the Pattern Detector to assess the complexity of your upgrade.
uuid: 4fcfdb16-3183-442a-aa5b-5f9c4fb7e091
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: upgrading
content-type: reference
discoiquuid: 8cdcfd3a-7003-4cce-97f4-da7a1a887d1b
feature: Upgrading
exl-id: 375e202c-21d4-41f1-a2d5-592ac95c8f25
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '536'
ht-degree: 28%

---

# パターン検出を使用したアップグレードの複雑性の評価{#assessing-the-upgrade-complexity-with-the-pattern-detector}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

## 概要 {#overview}

この機能を使用すると、次のパターンを検出することで、既存のAEMインスタンスのアップグレード可能性をチェックできます。

1. 特定のルールに違反し、アップグレードによって影響を受ける領域または上書きされる領域で実行される
1. AEM 6.4 との下位互換性のないAEM 6.x 機能または API を使用しており、アップグレード後に動作しなくなる可能性があります。

これは、AEM 6.4 へのアップグレードに伴う開発作業の評価に役立ちます。

## 設定方法 {#how-to-set-up}

パターン検出は、 [1 つのパッケージ](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/compatpack/pd-all-aem65)  6.1 から 6.5 への任意のソースAEMバージョンでAEM 6.5 のアップグレードをターゲットとして作業する インストールするには、 [パッケージマネージャー](https://helpx.adobe.com/jp/experience-manager/6-5/sites/administering/using/package-manager.html).

## 使用方法 {#how-to-use}

>[!NOTE]
>
>パターン検出は、環境インスタンスを含む、あらゆるローカル開発で実行できます。 ただし、次の目的で使用します。
>
>* 検出率を上げる
>* ビジネスにとって重大なインスタンスの減速を避ける\
   >ユーザーアプリケーション、コンテンツ、設定の分野において、実稼働環境にできるだけ近い&#x200B;**ステージング環境で**&#x200B;実行することをお勧めします。


いくつかの方法を使用して、パターン検出の出力をチェックできます。

* **Felix Inventory コンソールを使用：**

1. 次の場所を参照してAEM Web コンソールに移動します。https://<i></i>serveraddress:serverport/system/console/configMgr
1. 次の図に示すように、**ステータス - パターン検出**&#x200B;を選択します。

   ![screenshot-2018-2-5pattern-detector](assets/screenshot-2018-2-5pattern-detector.png)

* **事後対応テキストベースまたは通常の JSON インターフェイスを使用**

* **反応性の高い JSON 行インターフェイスを使用**&#x200B;を生成します。これは各行に個別の JSON ドキュメントを生成します。

次に、これらの両方の方法について説明します。

## リアクティブインターフェイス {#reactive-interface}

リアクティブインターフェイスを使用すると、疑いが検出されたらすぐに違反レポートを処理できます。

出力は現在、次の 2 つの URL で使用できます。

1. プレーンテキストインターフェイス
1. JSON インターフェイス

## プレーンテキストインターフェイスの処理 {#handling-the-plain-text-interface}

出力内の情報は、一連のイベントエントリの形式で表示されます。 違反を公開するチャネルと、現在の進行状況を公開するチャネルの 2 つがあります。

これらは、次のコマンドを使用して取得できます。

```shell
curl -Nsu 'admin:admin' http://localhost:4502/system/console/status-pattern-detector.txt | tee patterns-report.log | grep SUSPICION
```

出力は次のようになります。

```
2018-02-13T14:18:32.071+01:00 [SUSPICION] The pattern=ECU/extraneous.content.usage was found by detector=ContentAccessDetector with id=a07fd94318f12312c165e06d890cbd3c2c8b8dad0c030663db8b4c800dd7c33f message="Cross-boundary overlay of internal marked path /libs/granite/operations/components/commons/commons.jsp/jcr:content referenced at /apps/granite/operations/components/commons/commons.jsp/jcr:content with properties redefined: jcr:lastModifiedBy, jcr:mimeType, jcr:data, jcr:lastModified, jcr:uuid". More info at=https://www.adobe.com/go/aem6_EC
```

進行状況は、`grep` コマンドを使用してフィルタリングできます。

```shell
curl -Nsu 'admin:admin' http://localhost:4502/system/console/status-pattern-detector.txt | tee patterns-report.log | grep PROGRESS
```

これにより、次の出力が得られます。

```
2018-02-13T14:19:26.909+01:00 [PROGRESS] emitted=127731/52 MB patterns (from=6.4), analysed=45780/16 MB items, found=0 suspicions so far in period=PT5.005S (throughput=34667 items/sec)
2018-02-13T14:19:31.904+01:00 [PROGRESS] emitted=127731/52 MB patterns (from=6.4), analysed=106050/39 MB items, found=0 suspicions so far in period=PT10S (throughput=23378 items/sec)
2018-02-13T14:19:35.685+01:00 [PROGRESS] Finished in period=PT13.782
```

## JSON インターフェイスの処理 {#handling-the-json-interface}

同様に、JSON も [jq ツール](https://stedolan.github.io/jq/) 公開され次第

```shell
curl -Nsu 'admin:admin' http://localhost:4502/system/console/status-pattern-detector.json | tee patterns-report.json | jq --unbuffered -C 'select(.suspicion == true)'
```

出力を次に示します。

```
{
  "timestamp": "2018-02-13T14:20:18.894+01:00",
  "suspicion": true,
  "pattern": {
    "code": "ECU",
    "type": "extraneous.content.usage",
    "detective": "ContentAccessDetector",
    "moreInfo": "https://www.adobe.com/go/aem6_ECU"
  },
  "item": {
    "id": "a07fd94318f12312c165e06d890cbd3c2c8b8dad0c030663db8b4c800dd7c33f",
    "message": "Cross-boundary overlay of internal marked path /libs/granite/operations/components/commons/commons.jsp/jcr:content referenced at /apps/granite/operations/components/commons/commons.jsp/jcr:content with properties redefined: jcr:lastModifiedBy, jcr:mimeType, jcr:data, jcr:lastModified, jcr:uuid"
  }
}
```

進行状況は 5 秒ごとにレポートされ、疑わしいメッセージとしてマークされている以外のメッセージを除外することで、取得できます。

```shell
curl -Nsu 'admin:admin' http://localhost:4502/system/console/status-pattern-detector.json | tee patterns-report.json | jq --unbuffered -C 'select(.suspicion == false)'
```

出力を次に示します。

```
{
  "suspicion": false,
  "timestamp": "2018-02-13T14:21:17.279+01:00",
  "type": "PROGRESS",
  "database": {
    "patternsEmitted": 127731,
    "patternsEmittedSize": "52 MB",
    "databasesEmitted": [
      "6.4"
    ]
  },
  "state": {
    "itemsAnalysed": 57209,
    "itemsAnalysedSize": "26 MB",
    "suspicionsFound": 0
  },
  "progress": {
    "elapsedTime": "PT5.003S",
    "elapsedTimeMilliseconds": 5003,
    "itemsPerSecond": 36965
  }
}
{
  "suspicion": false,
  "timestamp": "2018-02-13T14:21:22.276+01:00",
  "type": "PROGRESS",
  "database": {
    "patternsEmitted": 127731,
    "patternsEmittedSize": "52 MB",
    "databasesEmitted": [
      "6.4"
    ]
  },
  "state": {
    "itemsAnalysed": 113194,
    "itemsAnalysedSize": "46 MB",
    "suspicionsFound": 0
  },
  "progress": {
    "elapsedTime": "PT10S",
    "elapsedTimeMilliseconds": 10000,
    "itemsPerSecond": 24092
  }
}
{
  "suspicion": false,
  "timestamp": "2018-02-13T14:21:25.762+01:00",
  "type": "FINISHED",
  "database": {
    "patternsEmitted": 127731,
    "patternsEmittedSize": "52 MB",
    "databasesEmitted": [
      "6.4"
    ]
  },
  "state": {
    "itemsAnalysed": 140744,
    "itemsAnalysedSize": "63 MB",
    "suspicionsFound": 1
  },
  "progress": {
    "elapsedTime": "PT13.486S",
    "elapsedTimeMilliseconds": 13486,
    "itemsPerSecond": 19907
  }
}
{
  "suspicion": false,
  "type": "SUMMARY",
  "suspicionsFound": 1,
  "totalTime": "PT13.487S"
}
```

>[!NOTE]
>
>curl からの出力全体をファイルに保存した後、`jq` または `grep` を使用して情報タイプをフィルタリングする方法をお勧めします。

## 検出範囲 {#scope}

現在、パターン検出では次の項目を確認できます。

* OSGi バンドルの書き出しと読み込みの不一致
* Sling リソースタイプとスーパータイプ（検索パスコンテンツオーバーレイを使用）のオーバー使用状況
* Oak インデックスの定義（互換性）
* VLT パッケージ（過剰使用）
* rep:User nodes の互換性（OAuth 設定のコンテキスト内）
