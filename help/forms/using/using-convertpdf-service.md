---
title: ConvertPDF サービス
seo-title: ConvertPDF Service
description: AEM Forms ConvertPDF サービスを使用して、PDFドキュメントを PostScript または画像ファイルに変換します。
seo-description: Use AEM Forms ConvertPDF service to convert PDF documents to PostScript or image files.
uuid: 7fa94c8c-485b-4a77-bcd3-ed716e3cf316
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: document_services
discoiquuid: 5ec4f0ec-a9fd-4571-9b9a-278f4622c028
exl-id: a6fe7794-3c31-4706-9e23-fe63a506b0bc
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '398'
ht-degree: 21%

---

# ConvertPDF サービス {#convertpdf-service}

## 概要 {#overview}

ConvertPDFサービスは、PDFドキュメントを PostScript または画像ファイル (JPEG、JPEG2000、PNG およびTIFF) に変換します。 PDFドキュメントを PostScript に変換すると、PostScript プリンターでの無人サーバーベースの印刷に便利です。 PDFドキュメントをサポートしていないコンテンツ管理システムでドキュメントをアーカイブする場合、PDFドキュメントを複数ページTIFFファイルに変換すると便利です。

Convert Convert サービスを使用すると、次のことがPDFできます。

* PDF ドキュメントを PostScript に変換します。PostScript に変換する場合は、変換操作を使用して、変換元のドキュメントと、PostScript レベル 2 または 3 のどちらに変換するかを指定できます。 PostScript ファイルに変換するPDFドキュメントは、非インタラクティブである必要があります。
* PDFドキュメントをJPEG、JPEG2000、PNG およびTIFFの画像形式に変換します。 これらの画像形式のいずれかに変換する場合は、変換処理を使用して、ソースドキュメントと画像オプションの仕様を指定できます。 この仕様には、画像変換形式、画像解像度、色変換など、様々な環境設定が含まれます。

## サービスのプロパティを設定   {#properties}

以下を使用して、 **AEMFD ConvertPDF サービス** AEMコンソールで、このサービスのプロパティを設定します。 AEM コンソールのデフォルト URL は `https://[host]:[port]/system/console/configMgr` です。

## サービスの使用 {#using-the-service}

ConvertPDF サービスには次の 2 つの API が用意されています。

* **[toPS](https://helpx.adobe.com/jp/experience-manager/6-4/forms/javadocs/com/adobe/fd/cpdf/api/ConvertPdfService.html#toPS)**：PDF ドキュメントを PostScript ファイルに変換します。

* **[toImage](https://helpx.adobe.com/jp/experience-manager/6-4/forms/javadocs/com/adobe/fd/cpdf/api/ConvertPdfService.html#toImage)**：PDF ドキュメントを画像ファイルに変換します。サポートされている画像形式は、JPEG、JPEG2000、PNG および TIFF です。

### JSP またはサーブレットでの toPS API の使用 {#using-tops-api-with-a-jsp-or-servlets}

```java
<%@ page import="java.util.List, java.io.File,

                com.adobe.fd.cpdf.api.ConvertPdfService,
                com.adobe.fd.cpdf.api.ToPSOptionsSpec,
                com.adobe.fd.cpdf.api.enumeration.PSLevel,

                com.adobe.aemfd.docmanager.Document" %><%
%><%@taglib prefix="sling" uri="https://sling.apache.org/taglibs/sling/1.0" %><%
%><sling:defineObjects/><%

 // Get reference to ConvertPdfService OSGi service.
 // Within an OSGi bundle @Reference annotation 
 // can be used to retrieve service reference

 ConvertPdfService cpdfService = sling.getService(ConvertPdfService.class);

 // path to input document in AEM repository
 // please replace this with path to your document
String documentPath = "/content/dam/formsanddocuments/ExpenseClaimFlat.pdf";

 // Create a Docmanager Document object for 
 // the flat PDF file which needs to be converted 
 // to PostScript

 Document inputPDF = new Document(documentPath);

 // options object to pass to toPS API
 ToPSOptionsSpec toPSOptions = new ToPSOptionsSpec();

 // mandatory option to pass, sets PostScript langauge
 toPSOptions.setPsLevel(PSLevel.LEVEL_3);

 // invoke toPS method to convert inputPDF to PostScript
 Document convertedPS = cpdfService.toPS(inputPDF, toPSOptions);

 // save converted PostScript file to disk
 convertedPS.copyToFile(new File("C:/temp/out.ps"));

%>
```

### JSP またはサーブレットでの toImage API の使用 {#using-toimage-api-with-a-jsp-or-servlets}

```java
<%@ page import="java.util.List, java.io.File,

                com.adobe.fd.cpdf.api.ConvertPdfService,
                com.adobe.fd.cpdf.api.ToImageOptionsSpec,
                com.adobe.fd.cpdf.api.enumeration.ImageConvertFormat,

                com.adobe.aemfd.docmanager.Document" %><%
%><%@taglib prefix="sling" uri="https://sling.apache.org/taglibs/sling/1.0" %><%
%><sling:defineObjects/><%

 // Get reference to ConvertPdfService OSGi service.
 // Within an OSGi bundle @Reference annotation 
 // can be used to retrieve service reference

 ConvertPdfService cpdfService = sling.getService(ConvertPdfService.class);

 // path to input document in AEM repository
 // please replace this with path to your document
 String documentPath = "/content/dam/formsanddocuments/ExpenseClaimFlat.pdf";

 // Create a Docmanager Document object for 
 // the flat PDF file which needs to be converted 
 // to image

 Document inputPDF = new Document(documentPath);

 // options object to pass to toImage API
 ToImageOptionsSpec toImageOptions = new ToImageOptionsSpec();

 // mandatory option to pass, image format
 toImageOptions.setImageConvertFormat(ImageConvertFormat.JPEG);

 // invoke toImage method to convert inputPDF to Image
 List<Document> convertedImages = cpdfService.toImage(inputPDF, toImageOptions);

 // save converted image files to disk
 for(int i=0;i<convertedImages.size();i++){
     Document pageImage = convertedImages.get(i);
     pageImage.copyToFile(new File("C:/temp/out_"+(i+1)+".jpeg"));
 }

%>
```

### AEMワークフローでの ConvertPDF サービスの使用 {#using-convertpdf-service-with-aem-workflows}

ワークフローから ConvertPDF サービスを実行することは、JSP/Servlet から実行する場合と似ています。

唯一の違いは、JSP/Servlet からサービスを実行する場合、ドキュメントオブジェクトは ResourceResolverHelper オブジェクトから ResourceResolver オブジェクトのインスタンスを自動的に取得する点です。 この自動メカニズム\
は、コードがワークフローから呼び出された場合、機能しません。 ワークフローの場合、ResourceResolver オブジェクトのインスタンスを Document クラスのコンストラクタに明示的に渡します。次に、Document オブジェクトが\
リポジトリからコンテンツを読み取るための ResourceResolver オブジェクトが提供されました。

以下のサンプルワークフロープロセスでは、入力ドキュメントを PostScript ドキュメントに変換します。 コードは ECMAScript で記述され、ドキュメントはワークフローペイロードとして渡されます。

```
/*
 * Imports 
 */
var ConvertPdfService = Packages.com.adobe.fd.cpdf.api.ConvertPdfService;
var ToPSOptionsSpec = Packages.com.adobe.fd.cpdf.api.ToPSOptionsSpec;
var PSLevel = Packages.com.adobe.fd.cpdf.api.enumeration.PSLevel;
var Document = Packages.com.adobe.aemfd.docmanager.Document;
var File = Packages.java.io.File;
var ResourceResolverFactory = Packages.org.apache.sling.api.resource.ResourceResolverFactory;

// get reference to ConvertPdfService
var cpdfService = sling.getService(ConvertPdfService);

/*
 * workflow payload and path to it
 */
var payload = graniteWorkItem.getWorkflowData().getPayload();
var payload_path = payload.toString();

/* Create resource resolver using current session 
 * this resource resolver needs to be passed to Document
 * object constructor when file is to be read from 
 * crx repository. 
 */

/* get ResourceResolverFactory service reference , used 
 * to construct resource resolver
 */
var resourceResolverFactory = sling.getService(ResourceResolverFactory);

var authInfo = {
    "user.jcr.session":graniteWorkflowSession.getSession()
};

var resourceResolver = resourceResolverFactory.getResourceResolver(authInfo);

// Create Document object from payload_path 
var inputDocument = new Document(payload_path, resourceResolver);

// options object to be passed to toPS operation
var toPSOptions = new ToPSOptionsSpec();

// Set PostScript Language Three
toPSOptions.setPsLevel(PSLevel.LEVEL_3);

// invoke toPS operation to convert inputDocument to PS
var convertedPS = cpdfService.toPS(inputDocument, toPSOptions);

// save converted PostScript file to disk
convertedPS.copyToFile(new File("C:/temp/out.ps"));
```
