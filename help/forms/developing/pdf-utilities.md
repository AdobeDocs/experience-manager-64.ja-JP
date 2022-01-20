---
title: PDF・ユーティリティの操作
seo-title: Working with PDF Utilities
description: Utilities サービスを使用して、PDFと XDP ファイル形式の間での変換、PDFドキュメントのプロパティの設定と取得、XMPメタデータの操作をおこないます。
seo-description: Use the PDF Utilities service to convert between PDF and XDP file formats, set and retrieve PDF document properties, and manipulate XMP metadata.
uuid: a2ea2359-c547-4f1b-b6ca-f276f816e36a
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: operations
discoiquuid: d816bf2e-5236-4084-b7c4-c32b72cdff97
role: Developer
exl-id: 1fdabd73-ee74-426b-b815-68022ea27c4e
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '2565'
ht-degree: 5%

---

# PDF・ユーティリティの操作 {#working-with-pdf-utilities}

**Utilities サービスについてPDF**

PDFユーティリティサービスは、PDF形式と XDP ファイル形式の変換、PDFドキュメントプロパティの設定と取得、XMPメタデータの操作をおこなうことができます。 例えば、PDFドキュメントを別の形式に変換する前にそのプロパティを調べて、変換用に呼び出すサービス操作を判断すると便利です。

次のタスクは、Experience Utilities サービスを使用してPDFできます。

* PDFドキュメントを XDP ドキュメントに変換します。
* XDP ドキュメントをPDFドキュメントに変換 ( [XDP ドキュメントからPDFドキュメントへの変換](pdf-utilities.md#converting-xdp-documents-into-pdf-documents).)
* PDFドキュメントのプロパティを取得します。 ( [PDFドキュメントのプロパティの取得](pdf-utilities.md#retrieving-pdf-document-properties).)
* PDFドキュメントを保存し、Web 表示用に最適化します。 ( [PDFドキュメントの保存モードの設定](pdf-utilities.md#setting-pdf-document-save-modes).)

>[!NOTE]
>
>Utilities サービスの詳細については、「PDF・ユーティリティ」を参照してください。 [AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63).

## PDFドキュメントの XDP ドキュメントへの変換 {#converting-pdf-documents-into-xdp-documents}

PDFユーティリティ Java および Web サービス API を使用して、PDFドキュメントを XDP ドキュメントにプログラム的に変換できます。

>[!NOTE]
>
>Utilities サービスの詳細については、「PDF・ユーティリティ」を参照してください。 [AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary-of-steps}

PDFドキュメントを XDP ドキュメントに変換するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. PDFUtilityService クライアントを作成します。
1. 「Conversion to XDP conversion」PDFを呼び出します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。 Web サービスを使用している場合は、プロキシファイルを必ず含めてください。

**PDFUtilityService クライアントの作成**

プログラムによって Utilities 操作をPDFする前に、PDFUtilityService クライアントを作成する必要があります。 Java API を使用する場合は、 `PDFUtilityServiceClient` オブジェクト。 Web サービス API では、これは、 `PDFUtilityServiceService` オブジェクト。

**「Invoke to XDP conversion」PDFを呼び出します**

サービスクライアントを作成した後で、このPDFを XDP 変換操作に呼び出すことができます。

**関連トピック**

[Java API を使用したPDFドキュメントの XDP ドキュメントへの変換](pdf-utilities.md#convert-pdf-documents-into-xdp-documents-using-the-java-api)

[Web サービス API を使用してPDFドキュメントを XDP ドキュメントに変換する](pdf-utilities.md#convert-pdf-documents-into-xdp-documents-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Java API を使用したPDFドキュメントの XDP ドキュメントへの変換 {#convert-pdf-documents-into-xdp-documents-using-the-java-api}

PDFユーティリティ API(Java) を使用して、PDFドキュメントを XDP ドキュメントに変換します。

1. プロジェクトファイルを含める

   Java プロジェクトのクラスパスに、adobe-pdfutility-client.jar などのクライアント JAR ファイルを含めます。

1. PDFUtilityService クライアントの作成

   の作成 `PDFUtilityServiceClient` オブジェクトのコンストラクタを使用し、 `ServiceClientFactory` 接続プロパティを含むオブジェクト。

1. 「Invoke to XDP conversion」PDFを呼び出します

   変換を実行するには、 `PDFUtilityServiceClient` オブジェクトの `convertPDFtoXDP` メソッドを使用して `com.adobe.idp.Document` オブジェクトファイルを表すPDF。 このメソッドは、 `com.adobe.idp.Document` 新しく作成された XDP ファイルを表すオブジェクト。

**関連トピック**

[PDFドキュメントの XDP ドキュメントへの変換](pdf-utilities.md#converting-pdf-documents-into-xdp-documents)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Web サービス API を使用してPDFドキュメントを XDP ドキュメントに変換する {#convert-pdf-documents-into-xdp-documents-using-the-web-service-api}

PDFユーティリティ API（Web サービス）を使用して、PDFドキュメントを XDP ドキュメントに変換します。

1. プロジェクトファイルを含める

   * Utilities サービスの WSDL ファイルを使用するMicrosoft .NET クライアントPDFを作成します。
   * Microsoft .NET クライアントアセンブリを参照します。

1. PDFUtilityService クライアントの作成

   の作成 `PDFUtilityServiceService` オブジェクトを指定します。

1. 「Invoke to XDP conversion」PDFを呼び出します

   を呼び出す `PDFUtilityServiceService` オブジェクトの `convertPDFtoXDP` メソッドを使用して `BLOB` オブジェクトファイルを表すPDF。 このメソッドは、 `BLOB` 新しく作成された XDP ファイルを表すオブジェクト。

**関連トピック**

[PDFドキュメントの XDP ドキュメントへの変換](pdf-utilities.md#converting-pdf-documents-into-xdp-documents)

[Base64 エンコーディングを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Base64 エンコーディングを使用する.NET クライアントアセンブリの作成](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## XDP ドキュメントからPDFドキュメントへの変換 {#converting-xdp-documents-into-pdf-documents}

PDFユーティリティ Java および Web サービス API を使用して、XDP ドキュメントをプログラムでPDFドキュメントに変換できます。

>[!NOTE]
>
>Utilities サービスの詳細については、「PDF・ユーティリティ」を参照してください。 [AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary_of_steps-1}

XDP ドキュメントを変換ドキュメントにPDFするには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. PDFUtilityService クライアントを作成します。
1. 「XDP to Conversion」操作を呼び出してPDFを変換します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。 Web サービスを使用している場合は、プロキシファイルを必ず含めてください。

**PDFUtilityService クライアントの作成**

プログラムによって Utilities 操作をPDFする前に、PDFUtilityService クライアントを作成する必要があります。 Java API を使用する場合は、 `PDFUtilityServiceClient` オブジェクト。 Web サービス API では、これは、 `PDFUtilityServiceService` オブジェクト。

**「XDP to Conversion」操作を呼び出してPDFを変換**

サービスクライアントを作成した後で、XDP を呼び出して変換PDFを設定できます。

**関連トピック**

[Java API を使用して XDP ドキュメントをPDFドキュメントに変換する](pdf-utilities.md#convert-xdp-documents-into-pdf-documents-using-the-java-api)

[Web サービス API を使用した XDP ドキュメントのPDFドキュメントへの変換](pdf-utilities.md#converting-xdp-documents-into-pdf-documents-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Java API を使用して XDP ドキュメントをPDFドキュメントに変換する {#convert-xdp-documents-into-pdf-documents-using-the-java-api}

XDP ドキュメントをPDFドキュメントに変換するには、PDFユーティリティ API(Java) を使用します。

1. プロジェクトファイルを含める

   Java プロジェクトのクラスパスに、adobe-pdfutility-client.jar などのクライアント JAR ファイルを含めます。

1. PDFUtilityService クライアントの作成

   の作成 `PDFUtilityServiceClient` オブジェクトのコンストラクタを使用し、 `ServiceClientFactory` 接続プロパティを含むオブジェクト。

1. 「XDP to Conversion」操作を呼び出してPDFを変換

   変換を実行するには、 `PDFUtilityServiceClient` オブジェクトの `convertXDPtoPDF` メソッドを使用して `com.adobe.idp.Document` XDP ファイルを表すオブジェクト。 このメソッドは、 `com.adobe.idp.Document` 新しく作成されたPDFファイルを表すオブジェクト。

**関連トピック**

[XDP ドキュメントからPDFドキュメントへの変換](pdf-utilities.md#converting-xdp-documents-into-pdf-documents)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Web サービス API を使用した XDP ドキュメントのPDFドキュメントへの変換 {#converting-xdp-documents-into-pdf-documents-using-the-web-service-api}

XDP ドキュメントをPDFドキュメントに変換するには、PDFユーティリティ API（Web サービス API）を使用します。

1. プロジェクトファイルを含める

   * Utilities サービスの WSDL ファイルを使用するMicrosoft .NET クライアントPDFを作成します。
   * Microsoft .NET クライアントアセンブリを参照します。

1. PDFUtilityService クライアントの作成

   の作成 `PDFUtilityServiceService` オブジェクトを指定します。

1. 「XDP to Conversion」操作を呼び出してPDFを変換

   変換を実行するには、 `PDFUtilityServiceService` オブジェクトの `convertXDPtoPDF` メソッドを使用して `BLOB` XDP ファイルを表すオブジェクト。 このメソッドは、 `BLOB` 新しく作成されたPDFファイルを表すオブジェクト。

**関連トピック**

[XDP ドキュメントからPDFドキュメントへの変換](pdf-utilities.md#converting-xdp-documents-into-pdf-documents)

[Base64 エンコーディングを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Base64 エンコーディングを使用する.NET クライアントアセンブリの作成](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## PDFドキュメントのプロパティの取得 {#retrieving-pdf-document-properties}

PDFユーティリティ Java および Web サービス API を使用すると、ドキュメントを読むのに必要な入力可能なフォームかAcrobat最小バージョンかなど、PDFドキュメントのプロパティをプログラムで取得できます。

>[!NOTE]
>
>Utilities サービスの詳細については、「PDF・ユーティリティ」を参照してください。 [AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)

### 手順の概要 {#summary_of_steps-2}

PDF・ドキュメントのプロパティを取得するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. PDFUtilityService クライアントを作成します。
1. プロパティ取得操作を呼び出します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。 Web サービスを使用している場合は、プロキシファイルを必ず含めてください。

**PDFUtilityService クライアントの作成**

プログラムによって Utilities 操作をPDFする前に、PDFUtilityService クライアントを作成する必要があります。 Java API を使用する場合は、 `PDFUtilityServiceClient` オブジェクト。 Web サービス API では、これを `PDFUtilityServiceService` オブジェクト。

**プロパティ取得操作を呼び出す**

サービスクライアントを作成した後で、プロパティ取得操作を呼び出すことができます。

**関連トピック**

[Java API を使用してPDFドキュメントのプロパティを取得する](pdf-utilities.md#retrieve-pdf-document-properties-using-the-java-api)

[Web サービス API を使用してPDFドキュメントのプロパティを取得する](pdf-utilities.md#retrieve-pdf-document-properties-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Java API を使用してPDFドキュメントのプロパティを取得する {#retrieve-pdf-document-properties-using-the-java-api}

PDFユーティリティ API(Java) を使用して、PDFドキュメントのプロパティを取得します。

1. プロジェクトファイルを含める

   Java プロジェクトのクラスパスに、adobe-pdfutility-client.jar などのクライアント JAR ファイルを含めます。

1. PDFUtilityService クライアントの作成

   の作成 `PDFUtilityServiceClient` オブジェクトのコンストラクタを使用し、 `ServiceClientFactory` 接続プロパティを含むオブジェクト。

1. プロパティ取得操作を呼び出す

   変換を実行するには、 `PDFUtilityServiceClient` オブジェクトの `getPDFProperties` メソッドを使用して、以下を渡します。

   * A `com.adobe.idp.Document` オブジェクトドキュメントを表すPDF。
   * A `PDFPropertiesOptionSpec` 評価するプロパティを含むオブジェクト。

   このメソッドは、 `PDFPropertiesResult` クエリの結果を格納するオブジェクト。

**関連トピック**

[PDFドキュメントのプロパティの取得](pdf-utilities.md#retrieving-pdf-document-properties)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Web サービス API を使用してPDFドキュメントのプロパティを取得する {#retrieve-pdf-document-properties-using-the-web-service-api}

PDFユーティリティ Web サービス API を使用して、PDFドキュメントのプロパティを取得します。

1. プロジェクトファイルを含める

   * Utilities サービスの WSDL ファイルを使用するMicrosoft .NET クライアントPDFを作成します。
   * Microsoft .NET クライアントアセンブリを参照します。

1. PDFUtilityService クライアントの作成

   の作成 `PDFUtilityServiceService` オブジェクトを指定します。

1. プロパティ取得操作を呼び出す

   変換を実行するには、 `PDFUtilityServiceService` オブジェクトの `getPDFProperties` メソッドを使用して、以下を渡します。

   * A `BLOB` オブジェクトドキュメントを表すPDF。
   * A `PDFPropertiesOptionSpec` 評価するプロパティを含むオブジェクト。

   このメソッドは、 `PDFPropertiesResult` クエリの結果を格納するオブジェクト。

**関連トピック**

[PDFドキュメントのプロパティの取得](pdf-utilities.md#retrieving-pdf-document-properties)

[Base64 エンコーディングを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Base64 エンコーディングを使用する.NET クライアントアセンブリの作成](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## PDFドキュメントの保存モードの設定 {#setting-pdf-document-save-modes}

Utilities サービスの Java および Web サービスの API を使用して、PDFドキュメントの保存モードをプログラムで設定することができます。 PDFUtilities サービスを使用して保存モードを設定する場合、PDFUtilities サービスは保存モードのみを設定し、実際にはPDFドキュメントを保存しません。 PDFドキュメントは、別のサービス操作に渡されたときに保存されます。 たとえば、Encryption Utilities サービスを使用して特定のPDF・モードを設定し、Encryption サービスに渡すことができます。この場合、PDF・ドキュメントは実際に保存および暗号化されます。

>[!NOTE]
>
>Utilities サービスの詳細については、「PDF・ユーティリティ」を参照してください。 [AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary_of_steps-3}

保存オプションをPDF・ドキュメントに設定するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. PDFUtilityService クライアントを作成します。
1. 保存モードを設定します。
1. 保存操作を呼び出します。
1. 別の操作にPDFドキュメントを渡します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。 Web サービスを使用している場合は、プロキシファイルを必ず含めてください。

**PDFUtilityService クライアントの作成**

プログラムによって Utilities 操作をPDFする前に、PDFUtilityService クライアントを作成する必要があります。 Java API を使用する場合は、 `PDFUtilityServiceClient` オブジェクト。 Web サービス API では、これを `PDFUtilityServiceService` オブジェクト。

**保存モードの設定**

次の保存オプションのいずれかを選択できます。

* `INCREMENTAL`:保存に要する時間を減らすために増分的に保存する
* `FAST_WEB_VIEW`:高速な Web 表示用に保存
* `FULL`:完全保存を使用して（最適化を行わずに）保存するには

**「save style」操作を呼び出す**

サービスクライアントを作成した後で、プロパティ取得操作を呼び出すことができます。

**PDFドキュメントを別のAEM Forms操作に渡す**

Save Utilities サービスが指定した保存モードを設定したら、PDFドキュメントを別のAEM Forms操作に渡します。 その操作から返されたPDFドキュメントは、指定されたモードで保存されます。 例えば、Utilities サービスを使用してPDF `FAST_WEB_VIEW` モードにしてから、PDFドキュメントを Encryption サービスの `encryptUsingPassword` を指定した場合、返されたPDFドキュメントはパスワードで暗号化され、 `FAST_WEB_VIEW` モード。

>[!NOTE]
>
>このセクションに関連付けられているクイックスタートでは、 `FAST_WEB_VIEW` モードにしてから、PDFドキュメントを Encryption サービスの `encryptUsingPassword` 操作。

**関連トピック**

[Java API を使用してPDFドキュメントの保存オプションを設定する](pdf-utilities.md#set-pdf-document-save-options-using-the-java-api)

[Web サービス API を使用してPDFドキュメントの保存オプションを設定する](pdf-utilities.md#set-pdf-document-save-options-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[パスワードを使用したPDFドキュメントの暗号化](/help/forms/developing/encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)

### Java API を使用してPDFドキュメントの保存オプションを設定する {#set-pdf-document-save-options-using-the-java-api}

PDFユーティリティ API(Java) を使用して、PDFドキュメントの保存オプションを設定します。

1. プロジェクトファイルを含める

   Java プロジェクトのクラスパスに、adobe-pdfutility-client.jar などのクライアント JAR ファイルを含めます。

1. PDFUtilityService クライアントの作成

   の作成 `PDFUtilityServiceClient` オブジェクトのコンストラクタを使用し、 `ServiceClientFactory` 接続プロパティを含むオブジェクト。

1. 保存モードの設定

   * コンストラクタを使用して `PDFUtilitySaveMode` オブジェクトを作成します。
   * を呼び出して、保存モードを設定します。 `PDFUtilitySaveMode` オブジェクトの `setSaveStyle` メソッドを使用し、保存モードを指定する string 値を渡す。 例えば、Web 表示を高速化するために保存するには、 `FAST_WEB_VIEW`.

1. 「save style」操作を呼び出す

   を呼び出す `PDFUtilityServiceClient` オブジェクトの `setSaveMode` メソッドを使用して、次の値を渡します。

   * A `com.adobe.idp.Document` オブジェクトドキュメントを表すPDF。
   * A `PDFUtilitySaveMode` 使用する保存スタイルを含むオブジェクト。
   * 以前の設定を上書きするかどうかを決定するために使用される Boolean 値です。

   このメソッドは、 `com.adobe.idp.Document` 指定した保存スタイルを使用して書式設定されたオブジェクト。

1. PDFドキュメントを別のAEM Forms操作に渡す

   * 返された `com.adobe.idp.Document` オブジェクトを別のAEM Forms操作に移動します。

**関連トピック**

[PDFドキュメントの保存モードの設定](pdf-utilities.md#setting-pdf-document-save-modes)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Web サービス API を使用してPDFドキュメントの保存オプションを設定する {#set-pdf-document-save-options-using-the-web-service-api}

PDF・ユーティリティ AP（Web サービス）を使用して、PDF・ドキュメントの保存オプションを設定します。

1. プロジェクトファイルを含める

   * Utilities サービスの WSDL ファイルを使用するMicrosoft .NET クライアントPDFを作成します。
   * Microsoft .NET クライアントアセンブリを参照します。

1. PDFUtilityService クライアントの作成

   の作成 `PDFUtilityServiceService` オブジェクトを指定します。

1. 保存モードの設定

   * コンストラクタを使用して `PDFUtilitySaveMode` オブジェクトを作成します。
   * 保存モードを設定するには、 `PDFUtilitySaveMode` オブジェクトの `saveStyle` 保存モードを指定するメソッド。 例えば、Web 表示を高速化するために保存するには、次のように指定します。 `FAST_WEB_VIEW`.

1. 「save style」操作を呼び出す

   を呼び出す `PDFUtilityServiceService` オブジェクトの `setSaveMode` メソッドを使用して、次の値を渡します。

   * A `BLOB` オブジェクトドキュメントを表すPDF。
   * A `PDFUtilitySaveMode` 使用する保存スタイルを含むオブジェクト。
   * 以前の設定を上書きするかどうかを決定するために使用される Boolean 値です。

   このメソッドは、 `BLOB` 指定した保存スタイルを使用して書式設定されたオブジェクト。 その後、そのオブジェクトをPDF文書として保存できます。

1. PDFドキュメントを別のForms操作に渡す

   * 返された `BLOB` オブジェクトを別のAEM Forms操作に移動します。

**関連トピック**

[PDFドキュメントの保存モードの設定](pdf-utilities.md#setting-pdf-document-save-modes)

[Base64 エンコーディングを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Base64 エンコーディングを使用する.NET クライアントアセンブリの作成](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## PDFドキュメントの不要化 {#sanitizing-pdf-documents}

PDFユーティリティ Java API を使用して、プログラムによってPDFドキュメントを XDP ドキュメントに変換できます。

>[!NOTE]
>
>Utilities サービスの詳細については、「PDF・ユーティリティ」を参照してください。 [AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary_of_steps-4}

PDF・ドキュメントの不要部分を削除するには、次の手順に従います。

1. プロジェクトファイルを含めます。
1. PDFUtilityService クライアントを作成します。
1. サニタイズ操作を呼び出します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Java を使用してクライアントアプリケーションを作成するには、必要な JAR ファイルを含めます。

**PDFUtilityService クライアントの作成**

プログラムによってサニタイズ操作を実行する前に、PDFUtilityService クライアントを作成する必要があります。 Java API を使用する場合は、 `PDFUtilityServiceClient` オブジェクト。

**「Invoke to XDP conversion」PDFを呼び出します**

サービスクライアントを作成した後で、サニタイズ化操作を呼び出すことができます。

**関連トピック**

[Java API を使用したPDFドキュメントの XDP ドキュメントへの変換](pdf-utilities.md#convert-pdf-documents-into-xdp-documents-using-the-java-api)

[Web サービス API を使用してPDFドキュメントを XDP ドキュメントに変換する](pdf-utilities.md#convert-pdf-documents-into-xdp-documents-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Java API を使用してPDFドキュメントを不要にする {#sanitize-pdf-documents-using-the-java-api}

Java(Autilities API) を使用して、ドキュメントの不要PDFを削除します。

1. プロジェクトファイルを含める

   Java プロジェクトのクラスパスに、adobe-pdfutility-client.jar などのクライアント JAR ファイルを含めます。

1. PDFUtilityService クライアントの作成

   の作成 `PDFUtilityServiceClient` オブジェクトのコンストラクタを使用し、 `ServiceClientFactory` 接続プロパティを含むオブジェクト。

1. 「Invoke to XDP conversion」PDFを呼び出します

   変換を実行するには、 `PDFUtilityServiceClient` オブジェクトの `convertPDFtoXDP` メソッドを使用して `com.adobe.idp.Document` オブジェクトファイルを表すPDF。 このメソッドは、 `com.adobe.idp.Document` 新しく作成された XDP ファイルを表すオブジェクト。

**関連トピック**

[PDFドキュメントの不要化](/help/forms/developing/pdf-utilities-service-java-api.md#quick-start-soap-mode-sanitizing-pdf-documents)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)
