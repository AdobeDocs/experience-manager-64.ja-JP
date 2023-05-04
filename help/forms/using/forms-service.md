---
title: Forms サービス
seo-title: Forms Service
description: ここでは、Formsサービスと、Formsサービスを使用して実行できるフォーム関連のタスクについて説明します。
seo-description: The article describes Forms service and the form-related tasks you can perform using Forms service.
uuid: 3258d3c2-8755-4815-8c97-b2cfb9a9dfd4
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: document_services
discoiquuid: a9695d10-43ec-40eb-942f-7720abaa0973
exl-id: a1c7c90f-6b50-4bc1-9972-1d3bdf8887ce
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '721'
ht-degree: 45%

---

# Forms サービス {#forms-service}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

## 概要 {#overview}

Formsサービスを使用すると、通常 Designer で作成されるフォームを検証、処理、変換および配信する、インタラクティブなデータキャプチャクライアントアプリケーションを作成できます。 Formsサービスは、開発したフォームデザインをPDFドキュメントとしてレンダリングします。

また、Formsサービスを使用すると、組織は、電子フォームをAdobePDFとしてデプロイすることで、インテリジェントデータキャプチャプロセスを拡張できます。 また、このサービスを使用して、既存のデータをそれぞれインポートしたり、既存のPDF formsからデータをエクスポートしたりすることもできます。

Forms サービスの使用目的：

* テンプレートと XMLPDF formsに基づいてテンプレートをレンダリングします。
* フォームデータの統合を有効にして、データの読み込みとPDF formsからのデータの抽出を行います。
* フラグメントに基づいた Forms のレンダリング

## 作成PDF forms  {#creating-pdf-forms-nbsp}

Form サービスを使用して、データキャプチャ用のPDF formsを作成します。 通常は、AEM Forms Designer テンプレートから開始します。 Forms サービスの `renderPDFForm`（Javadoc にリンク）操作を使用して、このテンプレートを PDF フォームに変換します。

`renderPDFForm` 操作の最初のパラメーターはテンプレートファイルの名前（`ExpenseClaim.xdp` など）になります。テンプレートファイルはローカルのファイルシステム、CRX リポジトリー、HTTP ロケーション、FTP ロケーションのいずれかに保存できます。`renderPDFForm` 操作の `PDFFormRenderOptions` パラメーターのコンテンツルートを設定すると、テンプレートファイルの場所を指定できます。`PDFFormRenderOptions` パラメーターに対して指定できる他のオプションについて詳しくは、Javadoc を参照してください。

`renderPDFForm` 操作は XML データを受け取ることもできます。PDF フォームを作成する際、指定したデータがその PDF フォームに含まれるようにするため、XML データはテンプレートと結合されます。`renderPDFForm` 操作の 2 番目のパラメーターは、XML データを含むドキュメント（Javadoc）オブジェクトを受け取ることができます。

## PDF フォームからのデータ抽出 {#extracting-data-from-pdf-forms-nbsp}

Forms サービスの `exportData`（Javadoc）操作を使用して、PDF フォームから XML データを抽出します。この操作は、ドキュメントを最初のパラメーターとして受け入れます。 データは、XDP ドキュメントまたは XML ファイルとして書き出すことができます。 データを XML ファイルとして書き出すと、書き出されたデータは XDP エンベロープを削除し、プレーン XML ファイルを返します。 この配置は、2 番目のパラメーターを使用して指定できます。

## データのインポートPDF forms {#importing-data-into-pdf-forms}

Forms サービスを使用すると、AEM Forms Designer または `renderPDFForm` 操作を使用して作成された PDF フォームを XML データと統合することもできます。Forms サービスの `importData`（Javadoc）操作は PDF フォームと XML データを受け取り、XML データを含んだ PDF フォームを返します。

## フラグメントに基づいたフォームのレンダリング {#rendering-forms-based-on-fragments}

Formsサービスでは、AEM Forms Designer で作成したフラグメントに基づいてフォームをレンダリングできます。 フラグメントは、フォームの再使用可能な部分です。複数のフォームデザインに挿入できる個別の XDP ファイルとして保存されます。 例えば、フラグメントには住所ブロックや法律文を含めることができます。

フラグメントを使用すると、大量のフォームを簡単に作成し、管理することができます。 フォームを作成するときに必要なフラグメントへの参照を挿入すると、そのフラグメントがフォームに表示されます。フラグメント参照には、物理 XDP ファイルを指すサブフォームが含まれます。

フラグメントを使用する利点は次のとおりです。

* **コンテンツの再利用**:複数のフォームデザインでコンテンツを再利用できます。 複数のフォームで同じコンテンツの一部をすばやく再利用するには、フラグメントを作成します。 コンテンツのコピーまたは再作成に時間がかかります。 フラグメントを使用し、それをフォームで参照することで、フォームデザインの中で頻繁に使用する部分を一貫性のあるコンテンツと外観ですべてのフォームに表示できます。
* **グローバル更新**:1 つのファイルで 1 回だけ、複数のフォームに対してグローバルな変更を行うことができます。 フラグメント内のコンテンツ、スクリプトオブジェクト、データバインディング、レイアウトまたはスタイルを変更できます。 フラグメントを参照するすべての XDP フォームに変更が反映されます。
* **共有フォームの作成**:フォームの作成を複数のリソースで共有できます。 スクリプトなどといった AEM Forms Designer の高度な機能に精通しているフォーム開発者は、スクリプトや動的プロパティを使用するフラグメントを作成、共有することができます。フォームデザイナーは、フラグメントを使用してフォームをデザインできます。 また、フラグメントを使用することで、複数のフォーム間でフォームのすべての部分の外観と機能が一貫していることを確認できます。
