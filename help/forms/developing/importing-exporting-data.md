---
title: データのインポートおよびエクスポート
seo-title: Importing and Exporting Data
description: Form Data Integration サービスを使用して、Java API および Web Service API を使用して、PDFフォームにデータを読み込み、PDFフォームからデータを書き出します。
seo-description: Use the Form Data Integration service to import data into a PDF form and export data from a PDF form using the Java API and Web Service API.
uuid: 94ccb6f2-6e5f-43ea-a954-9a4402871a17
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: operations
discoiquuid: 2e783745-c986-45ba-8e65-7437d114ca38
role: Developer
exl-id: e9d10d35-6a8d-497d-83f7-67ee6c22baed
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '2764'
ht-degree: 6%

---

# データのインポートおよびエクスポート {#importing-and-exporting-data}

## フォームデータ統合サービスについて {#about-the-form-data-integration-service}

Form Data Integration サービスを使用すると、データをPDFフォームに読み込んだり、データフォームからPDFを書き出したりできます。 インポートおよびエクスポート操作では、次の 2 種類のPDF formsがサポートされます。

* Acrobatフォーム (Acrobatで作成 ) は、フォームフィールドを含むPDFドキュメントです。
* AdobeXML フォーム（Designer で作成）は、XMLAdobeXML Formsアーキテクチャ (XFA) に準拠するPDFドキュメントです。

フォームデータは、フォームの種類に応じて、次のいずれかの形式でPDFできます。

* XFDF ファイル。Acrobat フォームデータ形式の XML バージョンです。
* XDP ファイル。フォームフィールド定義を含む XML ファイルです。フォームフィールドデータと埋め込まれた PDF ファイルが含まれる場合もあります。Designer で生成された XDP ファイルは、埋め込まれた base-64 エンコード済みのPDFドキュメントを使用する場合にのみ使用できます。

次のタスクは、Form Data Integration サービスを使用して実行できます。

* データをPDF formsに読み込む 詳しくは、 [フォームデータの読み込み](importing-exporting-data.md#importing-form-data).
* データをPDF formsから書き出す 詳しくは、 [フォームデータの書き出し](importing-exporting-data.md#exporting-form-data).

>[!NOTE]
>
>Form Data Integration サービスについて詳しくは、 [AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63).

## フォームデータの読み込み {#importing-form-data}

Form Data Integration サービスを使用して、フォームデータをインタラクティブPDF formsに読み込むことができます。 インタラクティブPDFフォームは、PDFから情報を収集したり、カスタム情報を表示したりするための 1 つ以上のフィールドを含むユーザードキュメントです。 Form Data Integration サービスは、フォームの演算、検証、スクリプティングをサポートしていません。

Designer で作成したフォームにデータを読み込むには、有効な XDP XML データソースを参照する必要があります。 次の住宅ローン申し込みフォームの例を考えてみましょう。

![ie_ie_loanformdata](assets/ie_ie_loanformdata.png)

データ値をこのフォームに読み込むには、フォームに対応する有効な XDP XML データソースが必要です。 任意の XML データソースを使用して、Form Data Integration サービスを使用してデータをフォームに読み込むことはできません。 任意の XML データソースと XDP XML データソースの違いは、XDP データソースが XML Forms Architecture(XFA) に準拠している点です。 次の XML は、サンプルの住宅ローン申し込みフォームに対応する XDP XML データソースを表しています。

```as3
 <?xml version="1.0" encoding="UTF-8" ?>  
 - <xfa:datasets xmlns:xfa="https://www.xfa.org/schema/xfa-data/1.0/"> 
 - <xfa:data> 
 - <data> 
     - <Layer> 
         <closeDate>1/26/2007</closeDate>  
         <lastName>Johnson</lastName>  
         <firstName>Jerry</firstName>  
         <mailingAddress>JJohnson@NoMailServer.com</mailingAddress>  
         <city>New York</city>  
         <zipCode>00501</zipCode>  
         <state>NY</state>  
         <dateBirth>26/08/1973</dateBirth>  
         <middleInitials>D</middleInitials>  
         <socialSecurityNumber>(555) 555-5555</socialSecurityNumber>  
         <phoneNumber>5555550000</phoneNumber>  
     </Layer> 
     - <Mortgage> 
         <mortgageAmount>295000.00</mortgageAmount>  
         <monthlyMortgagePayment>1724.54</monthlyMortgagePayment>  
         <purchasePrice>300000</purchasePrice>  
         <downPayment>5000</downPayment>  
         <term>25</term>  
         <interestRate>5.00</interestRate>  
     </Mortgage> 
 </data> 
 </xfa:data> 
 </xfa:datasets>
```

>[!NOTE]
>
>Form Data Integration サービスについて詳しくは、 [AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary-of-steps}

フォームデータをPDFフォームに読み込むには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. フォームデータ統合サービスクライアントを作成します。
1. PDFフォームを参照する。
1. XML データソースを参照します。
1. データをPDF・フォームにインポートします。
1. PDFフォームをPDFファイルとして保存します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。 Web サービスを使用している場合は、プロキシファイルを必ず含めてください。

次の JAR ファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-formdataintegration-client.jar
* adobe-utilities.jar(AEM Formsを JBoss にデプロイする場合に必須 )
* jbossall-client.jar(AEM Formsが JBoss にデプロイされている場合に必須 )

これらの JAR ファイルの場所について詳しくは、 [AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**フォームデータ統合サービスクライアントの作成**

プログラムによってデータをクライアント API からPDFに読み込む前に、Data Integration Service クライアントを作成する必要があります。 サービスクライアントを作成する場合、サービスを呼び出すために必要な接続設定を定義します。 詳しくは、 [接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).

**PDFフォームの参照**

データをPDFフォームに読み込むには、Designer で作成した XML フォームまたはAcrobatで作成したAcrobatフォームを参照する必要があります。

**XML データソースの参照**

フォームデータを読み込むには、有効なデータソースを参照する必要があります。 Designer で作成した XFA XML フォームにデータを読み込むには、XDP XML データソースを使用する必要があります。 Acrobatフォームを参照する場合は、XFDF データソースを使用する必要があります。 データのインポート先のフィールドごとに、値を指定する必要があります。 XML データソース内の要素がフォーム内のフィールドに対応していない場合、その要素は無視されます。

**データをPDFフォームに読み込む**

PDFフォームと有効な XML データソースを参照した後、データをPDFフォームに読み込むことができます。

**PDFフォームをPDFファイルとして保存**

データをフォームに読み込んだ後、フォームをPDFファイルとして保存できます。 ユーザーは、PDFファイルとして保存したフォームをAdobe ReaderまたはAcrobatで開き、読み込んだデータを含むフォームを確認できます。

**関連トピック**

[Java API を使用したフォームデータの読み込み](importing-exporting-data.md#import-form-data-using-the-java-api)

[Web サービス API を使用したフォームデータの読み込み](importing-exporting-data.md#import-form-data-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[フォームデータ統合サービス API クイックスタート](/help/forms/developing/form-data-integration-service-java.md#form-data-integration-service-java-api-quick-start-soap)

[フォームデータの書き出し](importing-exporting-data.md#exporting-form-data)

### Java API を使用したフォームデータの読み込み {#import-form-data-using-the-java-api}

フォームデータ統合 API(Java) を使用してフォームデータを読み込みます。

1. プロジェクトファイルを含めます。

   Java プロジェクトのクラスパスに、adobe-formdataintegration-client.jar などのクライアント JAR ファイルを含めます。

1. フォームデータ統合サービスクライアントを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用して `FormDataIntegrationClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. PDFフォームを参照する。

   * コンストラクタを使用して `java.io.FileInputStream` オブジェクトを作成します。PDF・フォームの場所を指定する string 値を渡します。
   * の作成 `com.adobe.idp.Document` オブジェクトを選択し、PDFフォームを `com.adobe.idp.Document` コンストラクタ。 パス `java.io.FileInputStream` コンストラクタに対するPDF・フォームを含むオブジェクト。

1. XML データソースを参照します。

   * の作成 `java.io.FileInputStream` オブジェクトを指定する必要があります。
   * の作成 `com.adobe.idp.Document` を使用してフォームデータを保存するオブジェクト `com.adobe.idp.Document` コンストラクタ。 パス `java.io.FileInputStream` コンストラクタに対するフォームデータを含むオブジェクト。

1. データをPDF・フォームにインポートします。

   を呼び出して、PDFフォームにデータを読み込む `FormDataIntegrationClient` オブジェクトの `importData` メソッドを使用して、次の値を渡します。

   * この `com.adobe.idp.Document` オブジェクトを設定します。PDFフォームを保存します。
   * この `com.adobe.idp.Document` オブジェクトを指定します。

   この `importData` メソッドは、 `com.adobe.idp.Document` XML データソースにあるPDFを含むデータフォームを保存するオブジェクト。

1. PDFフォームをPDFファイルとして保存します。

   * の作成 `java.io.File` オブジェクトに置き換えて、ファイル拡張子が「。PDF」であることを確認します。
   * を呼び出す `Document` オブジェクトの `copyToFile` メソッドを使用して、 `Document` オブジェクトをファイルに追加します ( `Document` が返したオブジェクト `importData` メソッド )。

**関連トピック**

[手順の概要](importing-exporting-data.md#summary-of-steps)

[クイックスタート（SOAP モード）:Java API を使用したフォームデータの読み込み](/help/forms/developing/form-data-integration-service-java.md#quick-start-soap-mode-importing-form-data-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Web サービス API を使用したフォームデータの読み込み {#import-form-data-using-the-web-service-api}

フォームデータ統合 API（Web サービス）を使用してフォームデータを読み込みます。

1. プロジェクトファイルを含めます。

   MTOM を使用するMicrosoft .NET プロジェクトを作成します。 次の WSDL 定義を使用していることを確認します。 `http://localhost:8080/soap/services/FormDataIntegration?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >置換 `localhost` を、AEM Formsをホストするサーバーの IP アドレスに設定します。

1. フォームデータ統合サービスクライアントを作成します。

   * の作成 `FormDataIntegrationClient` オブジェクトのデフォルトのコンストラクタを使用します。
   * の作成 `FormDataIntegrationClient.Endpoint.Address` オブジェクトを `System.ServiceModel.EndpointAddress` コンストラクタ。 WSDL をAEM Formsサービスに渡す文字列値 ( 例： `http://localhost:8080/soap/services/FormDataIntegration?blob=mtom`.) を使用する必要はありません。 `lc_version` 属性。 この属性は、サービス参照を作成する際に使用されます。 ただし、 `?blob=mtom` MTOM を使用する。
   * の作成 `System.ServiceModel.BasicHttpBinding` オブジェクトを作成するには、 `FormDataIntegrationClient.Endpoint.Binding` フィールドに入力します。 戻り値を `BasicHttpBinding` にキャストします。
   * を `System.ServiceModel.BasicHttpBinding` オブジェクトの `MessageEncoding` ～に向かって `WSMessageEncoding.Mtom`. この値は、MTOM が確実に使用されるようにします。
   * 次のタスクを実行して、基本的な HTTP 認証を有効にします。

      * フィールドにAEM forms ユーザー名を割り当てます。 `FormDataIntegrationClient.ClientCredentials.UserName.UserName`.
      * 対応するパスワード値をフィールドに割り当てます。 `FormDataIntegrationClient.ClientCredentials.UserName.Password`.
      * 定数値を割り当て `HttpClientCredentialType.Basic` フィールドに `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 定数値を割り当て `BasicHttpSecurityMode.TransportCredentialOnly` フィールドに `BasicHttpBindingSecurity.Security.Mode`.

1. PDFフォームを参照する。

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。この `BLOB` オブジェクトは、PDF・フォームを格納するために使用されます。
   * の作成 `System.IO.FileStream` オブジェクトを指定します。 PDFフォームの場所とファイルを開くモードを指定する string 値を渡します。
   * コンテンツを格納するバイト配列を作成します。 `System.IO.FileStream` オブジェクト。 バイト配列のサイズは、 `System.IO.FileStream` オブジェクトの `Length` プロパティ。
   * を呼び出して、バイト配列にストリームデータを入力します。 `System.IO.FileStream` オブジェクトの `Read` メソッド。 読み取るバイト配列、開始位置、ストリーム長を渡します。
   * 次の項目に `BLOB` オブジェクトを割り当てる `MTOM` フィールドにバイト配列の内容を入力します。

1. XML データソースを参照します。

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。この `BLOB` オブジェクトは、フォームに読み込まれるデータを保存するために使用されます。
   * の作成 `System.IO.FileStream` オブジェクトを指定します。 読み込むデータが含まれる XML ファイルの場所と、ファイルを開くモードを指定する string 値を渡します。
   * コンテンツを格納するバイト配列を作成します。 `System.IO.FileStream` オブジェクト。 バイト配列のサイズは、 `System.IO.FileStream` オブジェクトの `Length` プロパティ。
   * を呼び出して、バイト配列にストリームデータを入力します。 `System.IO.FileStream` オブジェクトの `Read` メソッド。 読み取るバイト配列、開始位置、ストリーム長を渡します。
   * 次の項目に `BLOB` オブジェクトを割り当てる `MTOM` フィールドにバイト配列の内容を入力します。

1. データをPDF・フォームにインポートします。

   を呼び出して、PDFフォームにデータを読み込む `FormDataIntegrationClient` オブジェクトの `importData` メソッドを使用して、次の値を渡します。

   * この `BLOB` オブジェクトを設定します。PDFフォームを保存します。
   * この `BLOB` オブジェクトを指定します。

   この `importData` メソッドは、 `BLOB` XML データソースにあるPDFを含むデータフォームを保存するオブジェクト。

1. PDFフォームをPDFファイルとして保存します。

   * の作成 `System.IO.FileStream` オブジェクトを指定します。
   * のデータコンテンツを格納するバイト配列を作成します。 `BLOB` が返したオブジェクト `importData` メソッド。 バイト配列を生成するには、 `BLOB` オブジェクトの `MTOM` フィールドに入力します。
   * の作成 `System.IO.BinaryWriter` オブジェクトのコンストラクタを呼び出し、 `System.IO.FileStream` オブジェクト。
   * を呼び出して、バイト配列の内容をPDFファイルに書き込みます。 `System.IO.BinaryWriter` オブジェクトの `Write` メソッドを使用してバイト配列を渡す。

**関連トピック**

[手順の概要](importing-exporting-data.md#summary-of-steps)

[MTOM を使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

## フォームデータの書き出し {#exporting-form-data}

Form Data Integration サービスを使用して、インタラクティブPDFフォームからフォームデータを書き出すことができます。 書き出されるデータの形式は、フォームタイプによって異なります。 フォームタイプがAcrobatで作成されたAcrobatフォームの場合、書き出されるデータは XFDF になります。 フォームタイプが Designer で作成された XML フォームの場合、書き出されるデータは XDP になります。

>[!NOTE]
>
>Form Data Integration サービスについて詳しくは、 [AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary_of_steps-1}

フォームフォームからフォームデータをPDFするには、次の手順を実行します。

1. プロジェクトファイルを含める
1. フォームデータ統合サービスクライアントを作成します。
1. PDFフォームを参照する。
1. 「PDF」フォームからデータを書き出します。
1. 書き出したデータを XML ファイルとして保存します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。 Web サービスを使用している場合は、プロキシファイルを必ず含めてください。

次の JAR ファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-formdataintegration-client.jar
* adobe-utilities.jar(AEM Formsを JBoss にデプロイする場合に必須 )
* jbossall-client.jar(AEM Formsが JBoss にデプロイされている場合に必須 )

**フォームデータ統合サービスクライアントの作成**

プログラムによってデータをPDFformClient API に読み込む前に、Data Integration Service クライアントを作成する必要があります。 サービスクライアントを作成する場合、サービスを呼び出すために必要な接続設定を定義します。 詳しくは、 [接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).

**PDFフォームの参照**

PDFフォームからデータを書き出すには、Designer またはAcrobatで作成され、フォームデータを含むPDFフォームを参照する必要があります。 空のスキーマフォームからデータを書き出そうとすると、空のPDFが生成されます。

**データ・フォームからのPDFのエクスポート**

フォームデータを含むPDFフォームを参照した後で、フォームからデータを書き出すことができます。 データは、フォームに基づく XML スキーマ内で書き出されます。

**フォームデータを XML ファイルとして保存する**

フォームデータを書き出した後は、データを XML ファイルとして保存できます。 XML ファイルとして保存した XML ファイルを XML ビューアで開くと、フォームデータを表示できます。

**関連トピック**

[Java API を使用したフォームデータの書き出し](importing-exporting-data.md#export-form-data-using-the-java-api)

[Web サービス API を使用したフォームデータの書き出し](importing-exporting-data.md#export-form-data-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[フォームデータ統合サービス API クイックスタート](/help/forms/developing/form-data-integration-service-java.md#form-data-integration-service-java-api-quick-start-soap)

[フォームデータの読み込み](importing-exporting-data.md#importing-form-data)

### Java API を使用したフォームデータの書き出し {#export-form-data-using-the-java-api}

フォームデータ統合 API(Java) を使用してフォームデータを書き出すには、次の手順を実行します。

1. プロジェクトファイルを含めます。

   Java プロジェクトのクラスパスに、adobe-formdataintegration-client.jar などのクライアント JAR ファイルを含めます。

1. フォームデータ統合サービスクライアントを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用して `FormDataIntegrationClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. PDFフォームを参照する。

   * の作成 `java.io.FileInputStream` オブジェクトを指定します。
   * の作成 `com.adobe.idp.Document` オブジェクトを選択し、PDFフォームを `com.adobe.idp.Document` コンストラクタ。 パス `java.io.FileInputStream` コンストラクタに対するPDF・フォームを含むオブジェクト。

1. 「PDF」フォームからデータを書き出します。

   を呼び出してフォームデータを書き出す `FormDataIntegrationClient` オブジェクトの `exportData` メソッドを使用して、 `com.adobe.idp.Document` オブジェクトを設定します。PDFフォームを保存します。 このメソッドは、 `com.adobe.idp.Document` オブジェクトを作成します。

1. PDFフォームをPDFファイルとして保存します。

   * の作成 `java.io.File` オブジェクトに置き換え、ファイル拡張子が XML であることを確認します。
   * を呼び出す `Document` オブジェクトの `copyToFile` メソッドを使用して、 `Document` オブジェクトをファイルに追加します ( `Document` が返したオブジェクト `exportData` メソッド )。

**関連トピック**

[手順の概要](importing-exporting-data.md#summary-of-steps)

[クイックスタート（SOAP モード）:Java API を使用したフォームデータの書き出し](/help/forms/developing/form-data-integration-service-java.md#quick-start-soap-mode-exporting-form-data-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Web サービス API を使用したフォームデータの書き出し {#export-form-data-using-the-web-service-api}

フォームデータ統合 API（Web サービス）を使用してフォームデータを書き出すには、次の手順を実行します。

1. プロジェクトファイルを含めます。

   MTOM を使用するMicrosoft .NET プロジェクトを作成します。 次の WSDL 定義を使用していることを確認します。 `http://localhost:8080/soap/services/FormDataIntegration?WSDL&lc_version=9.0.1`.

   * 置換 `localhost` を、AEM Formsをホストするサーバーの IP アドレスに設定します。

1. フォームデータ統合サービスクライアントを作成します。

   * の作成 `FormDataIntegrationClient` オブジェクトのデフォルトのコンストラクタを使用します。
   * の作成 `FormDataIntegrationClient.Endpoint.Address` オブジェクトを `System.ServiceModel.EndpointAddress` コンストラクタ。 WSDL をAEM Formsサービスに渡す文字列値 ( 例： `http://localhost:8080/soap/services/FormDataIntegration?blob=mtom`.) を使用する必要はありません。 `lc_version` 属性。 この属性は、サービス参照を作成する際に使用されます。 ただし、 `?blob=mtom` MTOM を使用する。
   * の作成 `System.ServiceModel.BasicHttpBinding` オブジェクトを作成するには、 `FormDataIntegrationClient.Endpoint.Binding` フィールドに入力します。 戻り値を `BasicHttpBinding` にキャストします。
   * を `System.ServiceModel.BasicHttpBinding` オブジェクトの `MessageEncoding` ～に向かって `WSMessageEncoding.Mtom`. この値は、MTOM が確実に使用されるようにします。
   * 次のタスクを実行して、基本的な HTTP 認証を有効にします。

      * フィールドにAEM forms ユーザー名を割り当てます。 `FormDataIntegrationClient.ClientCredentials.UserName.UserName`.
      * 対応するパスワード値をフィールドに割り当てます。 `FormDataIntegrationClient.ClientCredentials.UserName.Password`.
      * 定数値を割り当て `HttpClientCredentialType.Basic` フィールドに `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 定数値を割り当て `BasicHttpSecurityMode.TransportCredentialOnly` フィールドに `BasicHttpBindingSecurity.Security.Mode`.

1. PDFフォームを参照する。

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。この `BLOB` オブジェクトは、データの書き出し元のPDF・フォームを保存するために使用されます。
   * の作成 `System.IO.FileStream` オブジェクトを指定します。 PDFフォームの場所とファイルを開くモードを指定する string 値を渡します。
   * コンテンツを格納するバイト配列を作成します。 `System.IO.FileStream` オブジェクト。 バイト配列のサイズは、 `System.IO.FileStream` オブジェクトの `Length` プロパティ。
   * を呼び出して、バイト配列にストリームデータを入力します。 `System.IO.FileStream` オブジェクトの `Read` メソッドを使用し、読み込むバイト配列、開始位置、ストリーム長を渡す。
   * 次の項目に `BLOB` オブジェクトを割り当てる `MTOM` フィールドにバイト配列の内容を入力します。

1. 「PDF」フォームからデータを書き出します。

   を呼び出して、PDFフォームにデータを読み込む `FormDataIntegrationClient` オブジェクトの `exportData` メソッドを使用して、 `BLOB` オブジェクトを設定します。PDFフォームを保存します。 このメソッドは、 `BLOB` オブジェクトを作成します。

1. PDFフォームをPDFファイルとして保存します。

   * の作成 `System.IO.FileStream` オブジェクトを作成します。
   * のデータコンテンツを格納するバイト配列を作成します。 `BLOB` が返したオブジェクト `exportData` メソッド。 バイト配列を生成するには、 `BLOB` オブジェクトの `MTOM` フィールドに入力します。
   * の作成 `System.IO.BinaryWriter` オブジェクトのコンストラクタを呼び出し、 `System.IO.FileStream` オブジェクト。
   * を呼び出して、バイト配列の内容を XML ファイルに書き込みます。 `System.IO.BinaryWriter` オブジェクトの `Write` メソッドを使用してバイト配列を渡す。

**関連トピック**

[手順の概要](importing-exporting-data.md#summary-of-steps)

[MTOM を使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRef を使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
