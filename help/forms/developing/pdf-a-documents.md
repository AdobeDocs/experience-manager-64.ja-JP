---
title: PDF/A ドキュメントの操作
seo-title: Working with PDF/A Documents
description: DocConverter サービスを使用して、PDFドキュメントがPDF/A ドキュメントかどうかを判断し、PDFドキュメントをPDF/A ドキュメントに変換します。
seo-description: Use the  DocConverter service to determine if a PDF document is a PDF/A document and convert PDF documents to PDF/A documents.
uuid: c258d253-068a-4412-955a-21d8a4792d6f
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: operations
discoiquuid: 1e6cc554-aef1-463c-906b-634b80a27917
role: Developer
exl-id: fbf6c225-5351-4589-97d3-9faf9c5939bc
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '2358'
ht-degree: 7%

---

# PDF/A ドキュメントの操作 {#working-with-pdf-a-documents}

**DocConverter サービスについて**

DocConverter サービスは、PDFドキュメントを PDA/A ドキュメントに変換できます。 このサービスを使用して、次のタスクを実行できます。

* PDFドキュメントをPDF/A ドキュメントに変換します。 ( [ドキュメントをPDF/A ドキュメントに変換する](pdf-a-documents.md#converting-documents-to-pdf-a-documents).)
* PDFドキュメントがPDF/A ドキュメントかどうかを判断します。 ( [プログラムによるPDF/A 準拠の判断](pdf-a-documents.md#programmatically-determining-pdf-a-compliancy).)

>[!NOTE]
>
>DocConverter サービスの詳細については、 [AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63).

## ドキュメントをPDF/A ドキュメントに変換する {#converting-documents-to-pdf-a-documents}

DocConverter サービスを使用して、PDFドキュメントをPDF/A ドキュメントに変換できます。 PDF/A はドキュメントのコンテンツを長期保存するためのアーカイブ形式なので、すべてのフォントが埋め込まれ、ファイルが非圧縮になります。 その結果、通常、PDF/A ドキュメントは標準の PDF ドキュメントよりも大きくなります。また、PDF/A ドキュメントには、オーディオおよびビデオコンテンツは含まれません。PDFドキュメントをPDF/A ドキュメントに変換する前に、PDFドキュメントがPDF/A ドキュメントでないことを確認してください。

PDF/A-1 仕様は、A と B という 2 つの適合レベルで構成されます。2 つの主な違いは、適合レベル B には必要ない論理構造（アクセシビリティ）のサポートです。適合レベルに関係なく、PDF/A-1 では、生成されたPDF/A 文書にすべてのフォントが埋め込まれます。 現時点では、検証（および変換）ではPDF/A-1b のみがサポートされています。

PDF/A はPDFドキュメントのアーカイブの標準ですが、標準PDFドキュメントが会社の要件を満たす場合に、アーカイブにPDF/A を使用する必要はありません。 PDF/A 規格の目的は、長期的なアーカイブやドキュメント保存のニーズに対応したPDFファイルを構築することです。

>[!NOTE]
>
>DocConverter サービスの詳細については、 [AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary-of-steps}

PDFドキュメントをPDF/A ドキュメントに変換するには、次の手順に従います。

1. プロジェクトファイルを含めます。
1. DocConvert クライアントの作成
1. PDFドキュメントを参照して、PDF/A ドキュメントに変換します。
1. トラッキング情報を設定します。
1. ドキュメントを変換します。
1. PDF/A ドキュメントを保存します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。 Web サービスを使用している場合は、必ずプロキシファイルを含めてください。

次の JAR ファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-docconverter-client.jar
* adobe-utilities.jar(AEM Formsが JBoss Application Server にデプロイされている場合に必要 )
* jbossall-client.jar(AEM Formsが JBoss Application Server にデプロイされている場合に必要 )

これらの JAR ファイルの場所について詳しくは、 [AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**DocConvert クライアントの作成**

DocConverter の操作をプログラムで実行する前に、DocConverter クライアントを作成する必要があります。 Java API を使用している場合は、 `DocConverterServiceClient` オブジェクト。 DocConverter Web サービス API を使用している場合は、 `DocConverterServiceService` オブジェクト。

**PDFドキュメントを参照してPDF/A ドキュメントに変換**

PDFドキュメントを取得してPDF/A ドキュメントに変換します。 AcrobatフォームなどのPDFドキュメントをPDF/A ドキュメントに変換しようとすると、例外が発生します。

**トラッキング情報を設定**

変換処理中に追跡する情報の量を指定する実行時のオプションを設定できます。 つまり、PDFドキュメントをPDF/A ドキュメントに変換する際に DocConverter サービスが追跡する情報の量を指定する 9 つの異なるレベルを設定できます。

**ドキュメントを変換**

DocConverter サービスクライアントを作成した後、変換するPDFドキュメントを参照し、追跡する情報の量を指定するランタイムオプションを設定します。PDFドキュメントをPDF/A ドキュメントに変換できます。

**PDF/A ドキュメントを保存**

PDF/A ドキュメントは、PDFファイルとして保存できます。

**関連トピック**

[Java API を使用して、PDF/A ドキュメントにドキュメントを変換する](pdf-a-documents.md#convert-documents-to-pdf-a-documents-using-the-java-api)

[Web サービス API を使用して、PDF/A ドキュメントにドキュメントを変換する](pdf-a-documents.md#convert-documents-to-pdf-a-documents-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[プログラムによるPDF/A 準拠の判断](pdf-a-documents.md#programmatically-determining-pdf-a-compliancy)

### Java API を使用して、PDF/A ドキュメントにドキュメントを変換する {#convert-documents-to-pdf-a-documents-using-the-java-api}

Java API を使用して、PDFドキュメントをPDF/A ドキュメントに変換します。

1. プロジェクトファイルを含める

   Java プロジェクトのクラスパスに、adobe-docconverter-client.jar などのクライアント JAR ファイルを含めます。

1. DocConvert クライアントの作成

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用して `DocConverterServiceClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. PDFドキュメントを参照してPDF/A ドキュメントに変換

   * の作成 `java.io.FileInputStream` 変換するPDFドキュメントを表すオブジェクト。コンストラクタを使用し、変換ファイルの場所を指定する string 値を渡します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. トラッキング情報を設定

   * コンストラクタを使用して `PDFAConversionOptionSpec` オブジェクトを作成します。
   * を呼び出して、情報トラッキングレベルを設定します。 `PDFAConversionOptionSpec` オブジェクトの `setLogLevel` メソッドを使用して、追跡レベルを指定する string 値を渡す方法と方法を指定します。 例えば、 `FINE`. 様々な値について詳しくは、 `setLogLevel` メソッド [AEM Forms API リファレンス](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

1. ドキュメントを変換

   を呼び出して、PDFドキュメントをPDF/A ドキュメントに変換します。 `DocConverterServiceClient` オブジェクトの `toPDFA` メソッドを使用して、次の値を渡します。

   * この `com.adobe.idp.Document` 変換するPDF文書を含むオブジェクト
   * この `PDFAConversionOptionSpec` 追跡情報を指定するオブジェクト

   この `toPDFA` メソッドは、 `PDFAConversionResult` オブジェクトを返します。PDF/A ドキュメントを含むオブジェクトです。

1. PDF/A ドキュメントを保存

   * を呼び出してPDF/A ドキュメントを取得する `PDFAConversionResult` オブジェクトの `getPDFA` メソッド。 このメソッドは、 `com.adobe.idp.Document` PDF/A ドキュメントを表すオブジェクト。
   * の作成 `java.io.File` PDF/A ファイルを表すオブジェクト。 ファイル名の拡張子が.pdf であることを確認します。
   * を呼び出して、PDF/A データをファイルに入力します。 `com.adobe.idp.Document` オブジェクトの `copyToFile` メソッドおよび `java.io.File` オブジェクト。

**関連トピック**

[PDF/A ドキュメントの操作](pdf-a-documents.md#working-with-pdf-a-documents)

[クイックスタート（SOAP モード）:Java API を使用したPDF/A ドキュメントへのドキュメントの変換](/help/forms/developing/docconverter-service-java-api-quick.md#quick-start-soap-mode-converting-a-document-to-a-pdf-a-document-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Web サービス API を使用して、PDF/A ドキュメントにドキュメントを変換する {#convert-documents-to-pdf-a-documents-using-the-web-service-api}

DocConverter API（Web サービス）を使用して、PDFドキュメントをPDF/A ドキュメントに変換します。

1. プロジェクトファイルを含める

   * DocConverter WSDL を使用するMicrosoft .NET クライアントアセンブリを作成します。
   * Microsoft .NET クライアントアセンブリを参照します。

1. DocConvert クライアントの作成

   * Microsoft .NET クライアントアセンブリを使用して、 `DocConverterServiceService` オブジェクトのデフォルトのコンストラクターを呼び出す。
   * を `DocConverterServiceService` オブジェクトの `Credentials` データメンバーを `System.Net.NetworkCredential` ユーザー名とパスワードの値を指定する値。

1. PDFドキュメントを参照してPDF/A ドキュメントに変換

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。この `BLOB` オブジェクトは、PDF/A ドキュメントに変換されたPDFドキュメントを保存するために使用されます。
   * の作成 `System.IO.FileStream` オブジェクトを指定します。
   * コンテンツを格納するバイト配列を作成します。 `System.IO.FileStream` オブジェクト。 バイト配列のサイズは、 `System.IO.FileStream` オブジェクトの `Length` プロパティ。
   * を呼び出して、バイト配列にストリームデータを入力します。 `System.IO.FileStream` オブジェクトの `Read` メソッドを使用し、読み込むバイト配列、開始位置、ストリーム長を渡す。
   * 次の項目に `BLOB` オブジェクトを割り当てる `binaryData` プロパティにバイト配列の内容を入力します。

1. トラッキング情報を設定

   * コンストラクタを使用して `PDFAConversionOptionSpec` オブジェクトを作成します。
   * トラッキングレベルを指定する値を `PDFAConversionOptionSpec` オブジェクトの `logLevel` データメンバー。 例えば、 `FINE` をこのデータメンバーに追加します。

1. ドキュメントを変換

   を呼び出して、PDFドキュメントをPDF/A ドキュメントに変換します。 `DocConverterServiceService` オブジェクトの `toPDFA` メソッドを使用して、次の値を渡します。

   * この `BLOB` 変換するPDF文書を含むオブジェクト
   * この `PDFAConversionOptionSpec` 追跡情報を指定するオブジェクト

   この `toPDFA` メソッドは、 `PDFAConversionResult` オブジェクトを返します。PDF/A ドキュメントを含むオブジェクトです。

1. PDF/A ドキュメントを保存

   * の作成 `BLOB` オブジェクトを返します。PDF/A ドキュメントを格納する場合は、 `PDFAConversionResult` オブジェクトの `PDFADocument` データメンバー。
   * コンテンツを格納するバイト配列を作成します。 `BLOB` を使用して返されたオブジェクト `PDFAConversionResult` オブジェクト。 バイト配列を生成するには、 `BLOB` オブジェクトの `binaryData` データメンバー。
   * の作成 `System.IO.FileStream` オブジェクトを指定します。
   * の作成 `System.IO.BinaryWriter` オブジェクトのコンストラクタを呼び出し、 `System.IO.FileStream` オブジェクト。
   * を呼び出して、バイト配列の内容をPDFファイルに書き込みます。 `System.IO.BinaryWriter` オブジェクトの `Write` メソッドを使用してバイト配列を渡す。

**関連トピック**

[PDF/A ドキュメントの操作](pdf-a-documents.md#working-with-pdf-a-documents)

[Base64 エンコーディングを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Base64 エンコーディングを使用する.NET クライアントアセンブリの作成](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## プログラムによるPDF/A 準拠の判断 {#programmatically-determining-pdf-a-compliancy}

DocConverter サービスを使用して、PDFドキュメントがPDF/A に準拠しているかどうかを判断できます。 PDF/A ドキュメントおよびPDFドキュメントをPDF/A ドキュメントに変換する方法について詳しくは、 [ドキュメントをPDF/A ドキュメントに変換する](pdf-a-documents.md#converting-documents-to-pdf-a-documents).

>[!NOTE]
>
>DocConverter サービスの詳細については、 [AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary_of_steps-1}

PDF/A の適合性を判断するには、次の手順に従います。

1. プロジェクトファイルを含めます。
1. DocConvert クライアントの作成
1. PDF/A の準拠を判断するために使用されるPDFドキュメントを参照します。
1. 実行時オプションを設定します。
1. PDF・ドキュメントに関する情報を取得します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。 Web サービスを使用している場合は、必ずプロキシファイルを含めてください。

次の JAR ファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-docconverter-client.jar
* adobe-utilities.jar(AEM Formsが JBoss Application Server にデプロイされている場合に必要 )
* jbossall-client.jar(AEM Formsが JBoss Application Server にデプロイされている場合に必要 )

これらの JAR ファイルの場所について詳しくは、 [AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**DocConvert クライアントの作成**

DocConverter の操作をプログラムで実行する前に、DocConverter クライアントを作成する必要があります。 Java API を使用している場合は、 `DocConverterServiceClient` オブジェクト。 DocConverter Web サービス API を使用している場合は、 `DocConverterServiceService` オブジェクト。

**PDF/A 準拠の判断に使用するPDFドキュメントを参照します**

PDFドキュメントがPDF/ A に準拠しているかどうかを判断するには、PDFドキュメントを参照し、DocConverter サービスに渡す必要があります。

**実行時オプションを設定**

変換処理中に追跡する情報の量を指定する実行時のオプションを設定できます。 つまり、PDFドキュメントをPDF/A ドキュメントに変換する際に DocConverter サービスが追跡する情報の量を 9 つの異なるレベルで設定できます。

**PDF文書に関する情報を取得**

DocConverter サービスクライアントを作成し、PDFドキュメントを参照し、実行時のオプションを設定した後、PDFドキュメントがPDF/A 準拠のドキュメントであるかどうかを判断できます。

**関連トピック**

[Java API を使用したPDF/A の準拠の特定](pdf-a-documents.md#determine-pdf-a-compliancy-using-the-java-api)

[Web サービス API を使用したPDF/A の準拠の判断](pdf-a-documents.md#determine-pdf-a-compliancy-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Java API を使用したPDF/A の準拠の特定 {#determine-pdf-a-compliancy-using-the-java-api}

Java API を使用してPDF/A の準拠を判断します。

1. プロジェクトファイルを含める

   Java プロジェクトのクラスパスに、adobe-docconverter-client.jar などのクライアント JAR ファイルを含めます。

1. DocConvert クライアントの作成

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用して `DocConverterServiceClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. PDF/A 準拠の判断に使用するPDFドキュメントを参照します

   * の作成 `java.io.FileInputStream` 変換するPDFドキュメントを表すオブジェクト。コンストラクタを使用し、変換ファイルの場所を指定する string 値を渡します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. 実行時オプションを設定

   * コンストラクタを使用して `PDFAValidationOptionSpec` オブジェクトを作成します。
   * を呼び出して、準拠レベルを設定します。 `PDFAValidationOptionSpec` オブジェクトの `setCompliance` メソッドとパス `PDFAValidationOptionSpec.Compliance.PDFA_1B`.
   * を呼び出して、情報トラッキングレベルを設定します。 `PDFAValidationOptionSpec` オブジェクトの `setLogLevel` メソッドを使用して、追跡レベルを指定する string 値を渡す方法と方法を指定します。 例えば、 `FINE`. 様々な値について詳しくは、 `setLogLevel` メソッド [AEM Forms API リファレンス](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

1. PDF文書に関する情報を取得

   を呼び出してPDF/A の準拠を判断する `DocConverterServiceClient` オブジェクトの `isPDFA` メソッドを使用して、次の値を渡します。

   * この `com.adobe.idp.Document` オブジェクトドキュメントを含むPDF。
   * この `PDFAValidationOptionSpec` 実行時オプションを指定するオブジェクト。

   この `isPDFA` メソッドは、 `PDFAValidationResult` この操作の結果を格納するオブジェクト。

**関連トピック**

[PDF/A ドキュメントの操作](pdf-a-documents.md#working-with-pdf-a-documents)

[クイックスタート（SOAP モード）:Java API を使用したPDF/A の適合性の判断](/help/forms/developing/docconverter-service-java-api-quick.md#quick-start-soap-mode-determining-pdf-a-compliancy-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Web サービス API を使用したPDF/A の準拠の判断 {#determine-pdf-a-compliancy-using-the-web-service-api}

Web サービス API を使用してPDF/A の準拠を判断します。

1. プロジェクトファイルを含める

   * DocConverter WSDL を使用するMicrosoft .NET クライアントアセンブリを作成します。
   * Microsoft .NET クライアントアセンブリを参照します。

1. DocConvert クライアントの作成

   * Microsoft .NET クライアントアセンブリを使用して、 `DocConverterServiceService` オブジェクトのデフォルトのコンストラクターを呼び出す。
   * を `DocConverterServiceService` オブジェクトの `Credentials` データメンバーを `System.Net.NetworkCredential` ユーザー名とパスワードの値を指定する値。

1. PDF/A 準拠の判断に使用するPDFドキュメントを参照します

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。この `BLOB` オブジェクトは、PDF/A ドキュメントに変換されたPDFドキュメントを保存するために使用されます。
   * の作成 `System.IO.FileStream` オブジェクトを指定します。
   * コンテンツを格納するバイト配列を作成します。 `System.IO.FileStream` オブジェクト。 バイト配列のサイズは、 `System.IO.FileStream` オブジェクトの `Length` プロパティ。
   * を呼び出して、バイト配列にストリームデータを入力します。 `System.IO.FileStream` オブジェクトの `Read` メソッドを使用し、読み込むバイト配列、開始位置、ストリーム長を渡す。
   * 次の項目に `BLOB` オブジェクトを割り当てる `binaryData` プロパティにバイト配列の内容を入力します。

1. 実行時オプションを設定

   * コンストラクタを使用して `PDFAValidationOptionSpec` オブジェクトを作成します。
   * コンプライアンスレベルを設定するには、 `PDFAValidationOptionSpec` オブジェクトの `compliance` 値を持つデータメンバー `PDFAConversionOptionSpec_Compliance.PDFA_1B`.
   * 情報トラッキングレベルを設定するには、 `PDFAValidationOptionSpec` オブジェクトの `resultLevel` 値を持つデータメンバー `PDFAValidationOptionSpec_ResultLevel.DETAILED`.

1. PDF文書に関する情報を取得

   を呼び出してPDF/A の準拠を判断する `DocConverterServiceService` オブジェクトの `isPDFA` メソッドを使用して、次の値を渡します。

   * この `BLOB` オブジェクトドキュメントを含むPDF。
   * この `PDFAValidationOptionSpec` 実行時オプションを含むオブジェクト。

   この `isPDFA` メソッドは、 `PDFAValidationResult` この操作の結果を格納するオブジェクト。

**関連トピック**

[PDF/A ドキュメントの操作](pdf-a-documents.md#working-with-pdf-a-documents)

[Base64 エンコーディングを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Base64 エンコーディングを使用する.NET クライアントアセンブリの作成](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)
