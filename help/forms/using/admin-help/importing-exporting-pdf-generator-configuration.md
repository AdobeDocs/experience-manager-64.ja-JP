---
title: PDF Generator 設定ファイルの読み込みおよび書き出し
seo-title: Importing and exporting PDF Generator configuration files
description: Generator 設定ファイルの読み込みと書き出しのPDFについて説明します。
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
ht-degree: 11%

---

# PDF Generator 設定ファイルの読み込みおよび書き出し {#importing-and-exporting-pdf-generator-configuration-files}

設定ファイルには、PDF、ファイルタイプ、セキュリティ設定など、PDFジェネレーターの変換情報が含まれています。

>[!NOTE]
>
>カスタム native2pdfconfig.xml ファイルを読み込むことで、PDFジェネレーターのタイムアウト設定を変更することはできません。 このファイルのタイムアウト設定は、情報提供のみを目的としており、PDFジェネレータに現在の設定が表示されます。 タイムアウト設定を変更するには、「PDF・ジェネレータのパフォーマンス・パラメータの設定」( [AEM forms のインストールおよびデプロイ](https://www.adobe.com/go/learn_aemforms_installJBoss_63_jp).

## 現在の設定ファイルを書き出し {#export-your-current-configuration-file}

1. 管理コンソールで、サービス/PDFジェネレーター/設定ファイル/設定を書き出しをクリックします。
1. 設定を書き出すには、適切なオプションを選択します。

   * すべての名前付き設定を書き出すには、「設定全体をダウンロード」を選択します。
   * 1 つのAdobe PDF設定、セキュリティ設定、またはファイルタイプ設定のみを書き出すには、[ 最小構成のダウンロード ] を選択します。

      最小限の設定を書き出す場合は、書き出すAdobe PDF、セキュリティ、ファイルタイプの設定を選択します。

1. 「ダウンロード」をクリックし、XML ファイルを適切な場所に保存します。

## 設定ファイルのインポート {#import-a-configuration-file}

>[!NOTE]
>
>読み込まれたファイルの情報に基づいて、システムが再設定されます。

1. 管理コンソールで、サービス/PDFジェネレーター/設定ファイル/設定の読み込みをクリックします。
1. 「既存の設定ファイルを読み込む」を選択します。
1. 「設定ファイル」ボックスでファイルの場所を指定するには、「参照」をクリックしてファイルを探して選択し、「 **インポート**.

## AutoCAD ファイル内のすべての画層を変換 {#convert-all-layers-within-autocad-files}

既定では、PDFジェネレータは AutoCAD ファイルの既定の画層のみを、ファイル内のすべての画層ではなくPDFに変換します。 すべての画層を変換するには、次の手順に従います。

1. 管理コンソールで、サービス/PDFジェネレーター/設定ファイル/設定を書き出しをクリックします。
1. 「設定全体をダウンロード」を選択し、「ダウンロード」をクリックします。
1. テキストエディターで、ダウンロードしたファイルを開き、`PDFMaker` タグ内の `AutoCAD` タグの下にテキスト `convertAllPages="true"` を追加します。
1. 管理コンソールで、サービス/PDFジェネレーター/設定ファイル/設定の読み込みをクリックします。
1. 「既存の設定ファイルを読み込む」を選択し、更新したファイルを指定して、「読み込み」をクリックします。

   変更した設定ファイルを使用して変換された AutoCAD ファイルは、すべての画層が変換されます。

## 設定を、Generator でインストールされた元の設定にリセットします。PDF {#reset-your-configuration-to-the-original-settings-installed-with-pdf-generator}

1. 管理コンソールで、サービス/PDFジェネレーター/設定ファイル/設定の読み込みをクリックします。
1. 「設定をデフォルト設定にリセット」を選択し、「読み込み」をクリックします。
