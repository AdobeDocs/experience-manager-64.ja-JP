---
title: PDF Generator 設定ファイルの読み込みおよび書き出し
seo-title: Importing and exporting PDF Generator configuration files
description: PDF Generator 設定ファイルの読み込みおよび書き出し方法について説明します。
seo-description: Learn how to import and export PDF Generator configuration files.
uuid: 3367253b-d222-4c5f-9455-a1810d96112e
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.4/FORMS
discoiquuid: e25c1b35-73eb-4353-8e39-a2d4cdccd101
feature: PDF Generator
exl-id: 57673410-b8f1-494e-b4a0-c6724bab643c
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '378'
ht-degree: 100%

---

# PDF Generator 設定ファイルの読み込みおよび書き出し {#importing-and-exporting-pdf-generator-configuration-files}

設定ファイルには、PDF、ファイルタイプおよびセキュリティの設定を含む PDF Generator の変換情報が格納されます。

>[!NOTE]
>
>カスタムの native2pdfconfig.xml ファイルを読み込むことによって PDF Generator のタイムアウト設定を変更することはできません。このファイルのタイムアウト設定は情報提供のみを目的としており、PDF Generator の現在の設定が表示されます。タイムアウト設定を変更するには、『[AEM forms のインストールおよびデプロイ](https://www.adobe.com/go/learn_aemforms_installJBoss_63_jp)』の「PDF Generator のパフォーマンスパラメーターの設定」を参照してください。

## 現在の設定ファイルの書き出し {#export-your-current-configuration-file}

1. 管理コンソールで、サービス／PDF Generator／設定ファイル／設定を書き出すをクリックします。
1. 設定を書き出すには、適切なオプションを選択します。

   * 名前付き設定をすべて書き出すには、「設定全体のダウンロード」を選択します。
   * 1 つの Adobe PDF 設定、セキュリティ設定またはファイルタイプの設定のみを書き出すには、「最低限の設定のダウンロード」を選択します。

      最低限の設定を書き出す場合、Adobe PDF、セキュリティおよびファイルタイプの設定を選択します。

1. 「ダウンロード」をクリックし、XML ファイルを適切な場所に保存します。

## 設定ファイルのインポート {#import-a-configuration-file}

>[!NOTE]
>
>読み込んだファイルの情報に基づいてシステムが再設定されます。

1. 管理コンソールで、サービス／PDF Generator／設定ファイル／設定の読み込みをクリックします。
1. 「既存の設定ファイルの読み込み」を選択します。
1. 「設定ファイル」ボックスでファイルの場所を指定するには、「参照」をクリックしてファイルを探して選択し、「**読み込み**」をクリックします。

## AutoCAD ファイル内のすべてのレイヤーの変換 {#convert-all-layers-within-autocad-files}

デフォルトで、PDF Generator は、AutoCAD ファイル内のすべてのレイヤーではなく、デフォルトレイヤーだけを PDF に変換します。すべてのレイヤーを変換するには、以下の手順に従います。

1. 管理コンソールで、サービス／PDF Generator／設定ファイル／設定を書き出すをクリックします。
1. 「設定全体のダウンロード」を選択して「ダウンロード」をクリックします。
1. テキストエディターで、ダウンロードしたファイルを開き、`PDFMaker` タグ内の `AutoCAD` タグの下にテキスト `convertAllPages="true"` を追加します。
1. 管理コンソールで、サービス／PDF Generator／設定ファイル／設定の読み込みをクリックします。
1. 「既存の設定ファイルの読み込み」を選択し、更新したファイルを指定して、「読み込み」をクリックします。

   修正された設定ファイルを使用して変換された任意の AutoCAD ファイルでは、すべてのレイヤーが変換されます。

## PDF Generator でインストールした元の設定へのリセット {#reset-your-configuration-to-the-original-settings-installed-with-pdf-generator}

1. 管理コンソールで、サービス／PDF Generator／設定ファイル／設定の読み込みをクリックします。
1. 「設定をデフォルトにリセット」を選択して、「読み込み」をクリックします。
