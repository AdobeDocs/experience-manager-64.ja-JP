---
title: Output サービス
seo-title: Output Service
description: AEM Document Services の一部である Output Service を記述します
seo-description: Describes Output Service, which is part of AEM Document Services
uuid: acd64bbb-91df-49bc-9216-2e860812bbe9
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: document_services
discoiquuid: 8b96ba2d-007e-472a-875f-2caedd35ecf4
exl-id: ccc291fc-f4c5-4d14-816a-c57f56a95663
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '548'
ht-degree: 62%

---

# Output サービス {#output-service}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

## 概要 {#overview}

出力サービスは、AEM ドキュメントサービスの一部を成す OSGi サービスです。出力サービスは、様々な出力形式や、AEM Forms Designer の出力設計機能をサポートしています。出力サービスでは、XFA テンプレートと XML データを変換して、様々な形式の印刷ドキュメントを生成することができます。

出力サービスを使用すると、次のことを可能にするアプリケーションを作成できます。

* テンプレートファイルに XML データを格納することで、最終形式のドキュメントを生成する。
* 非インタラクティブPDF、ポストスクリプト、PCL、ZPL の印刷ストリームなど、様々な形式で出力フォームを生成します。
* XFA フォームの PDF ファイルから印刷用 PDF を生成する。
* 付属のテンプレートを用いて複数のデータセットを結合することにより、PDF、ポストスクリプト、PCL および ZPL の形式のドキュメントを一括生成する

>[!NOTE]
>
>出力サービスは 32 ビットアプリケーションです。 Microsoft Windows では、32 ビットアプリケーションで最大 2 GB のメモリを使用できます。 この制限は、出力サービスにも適用されます。

## 非インタラクティブ形式のドキュメントを作成する {#creating-non-interactive-form-documents}

![usingoutput_modified](assets/usingoutput_modified.png)

通常、テンプレートは AEM Forms Designer を使用して作成します。これらのテンプレートは、出力サービスの `generatePDFOutput` と `generatePrintedOutput` の各 API により、PDF、ポストスクリプト、ZPL や PCL などの様々な形式に直接変換することができます。

`generatePDFOutput` 操作は PDF を生成する一方で、`generatePrintedOutput` 操作は、PostScript、ZPL、および PCL の形式でドキュメントを生成します。各演算の最初のパラメーターは、テンプレートファイルの名前（例えば、`ExpenseClaim.xdp`）、またはテンプレートが含まれているドキュメントオブジェクトのいずれかを受け取ります。テンプレートファイルの名前を指定した場合は、テンプレートを含むフォルダへのパスとしてのコンテンツルートも指定します。コンテンツルートの指定には、`PDFOutputOptions` または `PrintedOutputOptions` パラメータのいずれかを使用します。これらのパラメータを使用して指定できる他のオプションの詳細は、Javadoc を参照してください。

2 番目のパラメーターは、出力ドキュメントの生成中にテンプレートと結合される XML ドキュメントを受け取ります。

`generatePDFOutput` 演算では、XFA ベースの PDF フォームを入力として受け取り、出力として非インタラクティブの PDF フォームを返すこともできます。

## 非インタラクティブフォームドキュメントの生成 {#generating-non-interactive-form-documents}

例えば、1 つ以上のテンプレートが存在しており、各テンプレートには XML データの複数のレコードがあるシナリオを考えてみましょう。

各レコードの印刷文書を生成するために、出力サービスの `generatePDFOutputBatch` と `generatePrintedOutputBatch` の演算を使用します。

また、レコードを 1 つのドキュメントに組み合わせることもできます。 どちらの演算も 4 つのパラメータを取ります。

最初のパラメータは、任意の文字列をキーとし、テンプレートファイルの名前を値として含むマップです。

2 番目のパラメータは別のマップです。この値は、XML データを含む Document オブジェクトです。 キーは、最初のパラメーターに指定したキーと同じです。

`generatePDFOutputBatch` または `generatePrintedOutputBatch` の 3 番目のパラメーターは、それぞれ `PDFOutputOptions` タイプまたは `PrintedOutputOptions` タイプです。

パラメータータイプは `generatePDFOutput` と `generatePrintedOutput` 演算のためのパラメーターのタイプと同じで、効果も同じです。

第 4 のパラメーターはタイプ `BatchOptions` です。これは、レコードごとに別のファイルを生成するかどうかを指定するために使用します。このパラメータのデフォルト値は false です。

`generatePrintedOutputBatch` と `generatePDFOutputBatch` は、共にタイプ `BatchResult` の値を返します。値には、生成されたドキュメントのリストが含まれます。 また、XML 形式のメタデータドキュメントも含まれ、この中には、生成される各ドキュメントに関する情報が格納されます。
