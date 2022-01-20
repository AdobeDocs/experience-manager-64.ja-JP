---
title: リクエスト分析スクリプト
seo-title: Request Analysis Script
description: このリクエスト分析スクリプトは、access.log ファイルの分析を簡易化し、後の処理で役立つようにわかりやすいレポートを生成します。
seo-description: The request analysis script is made to ease the analysis of the access.log files producing a readable report for later processing
uuid: 24eff3c6-5748-46f3-a30c-4a3a6427ce1d
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: testing
content-type: reference
discoiquuid: 1b5e0ccf-4157-45e3-8caf-1d6739d7d9d2
exl-id: 8582bbca-c11a-4880-88ba-da22e0301dba
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '171'
ht-degree: 27%

---

# リクエスト分析スクリプト{#request-analysis-script}

## ダウンロード {#download}

このスクリプトは、 `access.log` 後で処理するための読み取り可能なレポートを生成するファイル。

[ファイルを入手](assets/analyse-access.sh)

## 説明 {#description}

このスクリプトは、 `access.log` 後で処理するための読み取り可能なレポートを生成するファイル。

このスクリプトは、リクエストの全体番号、GET 対 POST、リクエスト配信の推移など多くのデータを生成します。

出力は Markdown 構文になっているので、pandoc などのツールを使用してPDFに変換したり、Markdown ビューアなどのプラグインを使用してブラウザーに表示したりすると、より簡単になります。

コマンドラインで提供されたカスタムパスを分析できます。

ファイル内のコメントから、その実行方法を示すコメントを取得します。

CQ を分析 `access.log` 様々な情報を推定し、Markdown の出力を生成する `stdout`.

## 使用方法 {#usage}

`./analyse-access.sh access.log.2013-&ast;`

コマンドラインで分析する追加のカスタムパスを指定できます。

`/analyse-access.sh access.log.2013-&ast; /my/custom/path/1 /my/custom/path/2`

出力は、単純な配管で保存できます

`./analyse-access.sh access.log.2013-&ast; | tee yr2013.md`
