---
title: XMP Utilities の操作
seo-title: Working with XMP Utilities
description: XMP Utilities Java および Web Service API を使用して、XMPメタデータをプログラムでPDFドキュメントに読み込み、PDFドキュメントからXMPメタデータを取得して保存します。
seo-description: Use the XMP Utilities Java and Web Service APIs to programmatically import XMP metadata into a PDF document and retrieve and save XMP metadata from a PDF document.
uuid: 90ce6cef-efe1-456a-8e0c-5ba90249dda0
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: operations
discoiquuid: 01d5677f-5c87-4a6e-987b-8eda9acc0b27
role: Developer
exl-id: 00a7989f-0a08-4552-8493-d4d790ed81e9
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '1391'
ht-degree: 3%

---

# XMP Utilities の操作 {#working-with-xmp-utilities}

**XMP Utilities サービスについて**

PDFドキュメントには、メタデータが含まれます。メタデータは、ドキュメントの内容と区別されるドキュメントに関する情報（テキストやグラフィックなど）です。 Adobe拡張メタデータプラットフォーム (XMP) は、ドキュメントのメタデータを処理するための規格です。

XMP Utilities サービスは、XMPメタデータを取得してPDFドキュメントから保存し、XMPメタデータをPDFドキュメントに読み込むことができます。

XMP Utilities サービスを使用して、次のタスクを実行できます。

* メタデータをPDFドキュメントに読み込みます。 ( [メタデータのPDFドキュメントへの読み込み](xmp-utilities.md#importing-metadata-into-pdf-documents).)
* メタデータをPDFドキュメントから書き出し ( [メタデータドキュメントからのPDFの書き出し](xmp-utilities.md#exporting-metadata-from-pdf-documents).)

>[!NOTE]
>
>XMP Utilities サービスについて詳しくは、 [AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63).

## メタデータのPDFドキュメントへの読み込み {#importing-metadata-into-pdf-documents}

XMP Utilities Java および Web サービス API を使用して、XMPメタデータをプログラムでPDFドキュメントに読み込むことができます。 メタデータは、ドキュメントの作成者やPDFに関連するキーワードなど、キーワードドキュメントに関する情報を提供します。 メタデータは、次の図に示すように、ドキュメントのドキュメントのプロパティダイアログに配置できます。

![ww_ww_metadatadialog](assets/ww_ww_metadatadialog.png)

プログラムによってメタデータをPDFドキュメントに読み込むには、メタデータ値を指定する既存の XML ドキュメントを使用するか、型のオブジェクトを使用します `XMPUtilityMetadata`. ( [AEM Forms API リファレンス](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).)

>[!NOTE]
>
>この節では、XML ドキュメントを使用してメタデータをPDF・ドキュメントに読み込む方法を説明します。

次の XML コードには、前の図に対応するメタデータ値が含まれています。 例えば、キーワードを指定する太字の項目に注意してください。

```as3
 <?xpacket begin="?" id="W5M0MpCehiHzreSzNTczkc9d"?> 
 <x:xmpmeta xmlns:x="adobe:ns:meta/" x:xmptk="Adobe XMP Core 4.2-jc015 52.349034, 2008 Jun 20 00:30:39-PDT (debug)"> 
       <rdf:RDF xmlns:rdf="https://www.w3.org/1999/02/22-rdf-syntax-ns#"> 
          <rdf:Description rdf:about="" 
                xmlns:xmp="https://ns.adobe.com/xap/1.0/"> 
             <xmp:MetadataDate>2008-10-22T10:52:21-04:00</xmp:MetadataDate> 
             <xmp:CreatorTool>AEM Forms</xmp:CreatorTool> 
             <xmp:ModifyDate>2008-10-22T10:52:21-04:00</xmp:ModifyDate> 
             <xmp:CreateDate>2008-02-13T11:00:18-05:00</xmp:CreateDate> 
          </rdf:Description> 
          <rdf:Description rdf:about="" 
                xmlns:pdf="https://ns.adobe.com/pdf/1.3/"> 
             <pdf:Producer>AEM Forms</pdf:Producer> 
             <pdf:Keywords>keyword1, keyword2, keyword3,keyword4</pdf:Keywords> 
          </rdf:Description> 
          <rdf:Description rdf:about="" 
                xmlns:xmpMM="https://ns.adobe.com/xap/1.0/mm/"> 
             <xmpMM:DocumentID>uuid:1cce1f84-331e-4d8d-8538-15441c271dd7</xmpMM:DocumentID> 
             <xmpMM:InstanceID>uuid:cdda0ca6-7c91-4771-9dc9-796c8fe59350</xmpMM:InstanceID> 
          </rdf:Description> 
          <rdf:Description rdf:about="" 
                > 
             <dc:format>application/pdf</dc:format> 
             <dc:description> 
                <rdf:Alt> 
                   <rdf:li xml:lang="x-default">Adobe Designer Sample</rdf:li> 
                </rdf:Alt> 
             </dc:description> 
             <dc:title> 
                <rdf:Alt> 
                   <rdf:li xml:lang="x-default">Grant Application</rdf:li> 
                </rdf:Alt> 
             </dc:title> 
             <dc:creator> 
                <rdf:Seq> 
                   <rdf:li>Tony Blue</rdf:li> 
                </rdf:Seq> 
             </dc:creator> 
             <dc:subject> 
                <rdf:Bag> 
                   <rdf:li>keyword1</rdf:li> 
                   <rdf:li>keyword2</rdf:li> 
                   <rdf:li>keyword3</rdf:li> 
                   <rdf:li>keyword4</rdf:li> 
                </rdf:Bag> 
             </dc:subject> 
          </rdf:Description> 
          <rdf:Description rdf:about="" 
                xmlns:desc="https://ns.adobe.com/xfa/promoted-desc/"> 
             <desc:version rdf:parseType="Resource"> 
                <rdf:value>1.0</rdf:value> 
                <desc:ref>/template/subform[1]</desc:ref> 
             </desc:version> 
             <desc:contact rdf:parseType="Resource"> 
                <rdf:value>Adobe Systems Incorporated</rdf:value> 
                <desc:ref>/template/subform[1]</desc:ref> 
             </desc:contact> 
          </rdf:Description> 
       </rdf:RDF> 
 </x:xmpmeta>
```

>[!NOTE]
>
>XMP Utilities サービスについて詳しくは、 [AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary-of-steps}

XMPメタデータをPDFドキュメントに読み込むには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. XMPUtilityService クライアントを作成します。
1. XMPメタデータの読み込み操作を呼び出します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。 Web サービスを使用している場合は、プロキシファイルを必ず含めてください。

**XMPUtilityService クライアントを作成します**

XMP Utilities の操作をプログラムで実行する前に、XMPUtilityService クライアントを作成する必要があります。 Java API を使用すると、これは `XMPUtilityServiceClient` オブジェクト。 Web サービス API では、これは `XMPUtilityServiceService` オブジェクト。

**「XMP metadata import」操作を呼び出す**

サービスクライアントを作成したら、XMPのメタデータの読み込み操作の 1 つを呼び出して、XMPのメタデータを指定したPDFドキュメントに読み込むことができます。

**関連トピック**

[Java API を使用したXMPメタデータの読み込み](xmp-utilities.md#import-xmp-metadata-using-the-java-api)

[Web サービス API を使用したXMPメタデータの読み込み](xmp-utilities.md#importing-xmp-metadata-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Java API を使用したXMPメタデータの読み込み {#import-xmp-metadata-using-the-java-api}

XMP Utilities API(Java) を使用してXMPメタデータを読み込みます。

1. プロジェクトファイルを含める

   Java プロジェクトのクラスパスに、adobe-pdfutility-client.jar などのクライアント JAR ファイルを含めます。

   >[!NOTE]
   >
   >adobe-pdfutility-client.jar ファイルには、XMP Utilities サービスをプログラムで呼び出すことを可能にするクラスが含まれています。

1. XMPUtilityService クライアントを作成します

   の作成 `XMPUtilityServiceClient` オブジェクトのコンストラクタを使用し、 `ServiceClientFactory` 接続プロパティを含むオブジェクト。

1. 「XMP metadata import」操作を呼び出す

   XMPメタデータを変更するには、 `XMPUtilityServiceClient` オブジェクトの `importMetadata` メソッドまたはその `importXMP` メソッド。

   次の `importMetadata` メソッドで、次の値を渡します。

   * A `com.adobe.idp.Document` オブジェクトファイルを表すPDF。
   * An `XMPUtilityMetadata` 読み込むメタデータを含むオブジェクト。

   次の `importXMP` メソッドで、次の値を渡します。

   * A `com.adobe.idp.Document` オブジェクトファイルを表すPDF。
   * A `com.adobe.idp.Document` 読み込むメタデータが含まれる XML ファイルを表すオブジェクト。

   どちらの場合も、返される値は `com.adobe.idp.Document` 新しく読み込まれたメタPDFを含むメタデータファイルを表すオブジェクト。 このオブジェクトをディスクに保存できます。

**関連トピック**

[メタデータのPDFドキュメントへの読み込み](xmp-utilities.md#importing-metadata-into-pdf-documents)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Web サービス API を使用したXMPメタデータの読み込み {#importing-xmp-metadata-using-the-web-service-api}

XMP Utilities Web サービス API を使用してプログラムでXMPメタデータを読み込むには、次のタスクを実行します。

1. プロジェクトファイルを含める

   * XMP Utilities サービスの WSDL ファイルを使用するMicrosoft .NET クライアントアセンブリを作成します。 ( [Base64 エンコーディングを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding).)
   * Microsoft .NET クライアントアセンブリを参照します。 ( [Base64 エンコーディングを使用する.NET クライアントアセンブリの作成](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding).)

1. XMPUtilityService クライアントを作成します

   の作成 `XMPUtilityServiceService` オブジェクトを指定します。

1. 「XMP metadata import」操作を呼び出す

   XMPメタデータを変更するには、 `XMPUtilityServiceService` オブジェクトの `importMetadata` メソッドまたはその `importXMP` メソッド。

   次の `importMetadata` メソッドで、次の値を渡します。

   * A `BLOB` オブジェクトファイルを表すPDF。
   * An `XMPUtilityMetadata` 読み込むメタデータを含むオブジェクト。

   次の `importXMP` メソッドで、次の値を渡します。

   * A `BLOB` オブジェクトファイルを表すPDF。
   * A `BLOB` 読み込むメタデータが含まれる XML ファイルを表すオブジェクト。

   どちらの場合も、返される値は `BLOB` 新しく読み込まれたメタPDFを含むメタデータファイルを表すオブジェクト。 このオブジェクトをディスクに保存できます。

**関連トピック**

[メタデータのPDFドキュメントへの読み込み](xmp-utilities.md#importing-metadata-into-pdf-documents)

<!--REVIEW: [Quick Start (Base64): Importing XMP metadata using the web service API](unresolvedlink-lc-qs-xmp-utilities-xu.xml#ws624e3cba99b79e12e69a9941333732bac8-7be8.2)-->

[Base64 エンコーディングを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Base64 エンコーディングを使用する.NET クライアントアセンブリの作成](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## メタデータドキュメントからのPDFの書き出し {#exporting-metadata-from-pdf-documents}

XMP Utilities Java および Web サービス API を使用して、プログラムによってPDFドキュメントからXMPメタデータを取得し、保存することができます。

>[!NOTE]
>
>XMP Utilities サービスについて詳しくは、 [AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary_of_steps-1}

XMPドキュメントからPDFメタデータを書き出すには、次の手順に従います。

1. プロジェクトファイルを含めます。
1. XMPUtilityService クライアントを作成します。
1. XMPのメタデータ書き出し操作を呼び出します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。 Web サービスを使用している場合は、プロキシファイルを必ず含めてください。

**XMPUtilityService クライアントを作成します**

XMP Utilities の操作をプログラムで実行する前に、XMPUtilityService クライアントを作成する必要があります。 Java AP を使用すると、これは `XMPUtilityServiceClient` オブジェクト。 Web サービス API では、これを `XMPUtilityServiceService` オブジェクト。

**「XMP metadata export」操作を呼び出します。**

サービスクライアントを作成したら、XMPのメタデータの書き出し操作の 1 つを呼び出すことができます。これは、XMPのメタデータを調べたり、ディスクに保存したりするために使用できます。

**関連トピック**

[Java API を使用したXMPメタデータの読み込み](xmp-utilities.md#import-xmp-metadata-using-the-java-api)

[Web サービス API を使用したXMPメタデータの読み込み](xmp-utilities.md#importing-xmp-metadata-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Java API を使用したXMPメタデータの書き出し {#export-xmp-metadata-using-the-java-api}

XMP Utilities API(Java) を使用してXMPメタデータを書き出します。

1. プロジェクトファイルを含める

   Java プロジェクトのクラスパスに、adobe-pdfutility-client.jar などのクライアント JAR ファイルを含めます。

   >[!NOTE]
   >
   >adobe-pdfutility-client.jar ファイルには、XMP Utility サービスをプログラムで呼び出すことを可能にするクラスが含まれています。

1. XMPUtilityService クライアントを作成します

   の作成 `XMPUtilityServiceClient` オブジェクトのコンストラクタを使用し、 `ServiceClientFactory` 接続プロパティを含むオブジェクト。

1. 「XMP metadata import」操作を呼び出す

   XMPメタデータを検査するには、 `XMPUtilityServiceClient` オブジェクトの `exportMetadata` メソッドを使用して `com.adobe.idp.Document` オブジェクトファイルを表すPDF。 メソッドは、 `XMPUtilityMetadata` 取得したメタデータを含むオブジェクト。

   XMPメタデータを取得して保存するには、 `XMPUtilityServiceClient` オブジェクトの `exportXMP` メソッドを使用して `com.adobe.idp.Document` オブジェクトファイルを表すPDF。 このメソッドは、 `com.adobe.idp.Document` 取得したメタデータを含むオブジェクト。このオブジェクトは、XML ファイルとしてディスクに保存できます。

**関連トピック**

[メタデータドキュメントからのPDFの書き出し](xmp-utilities.md#exporting-metadata-from-pdf-documents)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Web サービス API を使用したXMPメタデータの書き出し {#export-xmp-metadata-using-the-web-service-api}

XMP Utilities API（Web サービス）を使用してXMPメタデータを書き出します。

1. プロジェクトファイルを含める

   * XMP Utilities サービスの WSDL ファイルを使用するMicrosoft .NET クライアントアセンブリを作成します。
   * Microsoft .NET クライアントアセンブリを参照します。

1. XMPUtilityService クライアントを作成します

   の作成 `XMPUtilityServiceService` オブジェクトを指定します。

1. 「XMP metadata import」操作を呼び出す

   XMPメタデータを検査するには、 `XMPUtilityServiceClient` オブジェクトの `exportMetadata` メソッドを使用して `BLOB` オブジェクトファイルを表すPDF。 メソッドは、 `XMPUtilityMetadata` 取得したメタデータを含むオブジェクト。

   XMPメタデータを取得して保存するには、 `XMPUtilityServiceClient` オブジェクトの `exportXMP` メソッドを使用して `BLOB` オブジェクトファイルを表すPDF。 このメソッドは、 `BLOB` 取得したメタデータを含むオブジェクト。このオブジェクトは、XML ファイルとしてディスクに保存できます。

**関連トピック**

[メタデータドキュメントからのPDFの書き出し](xmp-utilities.md#exporting-metadata-from-pdf-documents)

[Base64 エンコーディングを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Base64 エンコーディングを使用する.NET クライアントアセンブリの作成](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)
