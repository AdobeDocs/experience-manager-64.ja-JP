---
title: PDF Generator の操作の概要
seo-title: Introduction to working with PDF Generator
description: 様々なファイル形式をPDFに変換する方法を説明します。
seo-description: Learn how to convert various file formats to PDF.
uuid: 1bf3a811-ef8d-481e-8b8d-1a910da8c57d
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.4/FORMS
discoiquuid: 207c6335-f700-48f1-814b-992692534f6c
feature: PDF Generator
exl-id: 217f0f80-fce6-4671-9853-633691d447f5
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '177'
ht-degree: 33%

---

# PDF Generator の操作の概要 {#introduction-to-working-with-pdf-generator}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

PDFジェネレーターは、様々なファイル形式をPDFに変換します。 また、PDF を他のファイル形式に変換し、PDF ドキュメントのサイズを最適化します。サポートされるファイル形式のリストについては、「GeneratePDFサービス」( [サービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63).

**処理するファイルをPDFジェネレーターに送信中**

ファイルを処理するために、次の 3 つの方法でPDFジェネレーターにファイルを送信できます。

* 管理者は、管理コンソールで PDFG ページにアクセスできます。 （[PDF Generator を使用したファイルの変換](/help/forms/using/admin-help/converting-files-using-pdf-generator.md)を参照）。
* ユーザーは、にログインすることで、PDFG エンドユーザーページにアクセスできます `http(s)://[server]:[port]/pdfgui`.ここから、PDFG ネットワークプリンター、PDFの作成、PDFへのHTML、Export PDF、Optimize PDFの各ページにアクセスできます。
* これらのサービスのエンドポイントを設定できます(参照先 <!--Fix broken link Managing Endpoints and --> [Generate PDF サービスの推奨事項](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#generate-pdf-service-recommendations).)
