---
title: バーコードフォームの操作
seo-title: Working with barcoded forms
description: Java API および Web Service API を使用して、PDFフォームまたはバーコードを含む画像からデータをデコードします。
seo-description: Decode data from a PDF form or an image that contains a barcode using the Java API and Web Service API.
uuid: e56c3c94-384d-401f-b418-dd34cdc57eda
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: operations
discoiquuid: eb28ac30-265c-4611-8247-1f4bc826f254
role: Developer
exl-id: 9d459939-a311-4770-84db-f2a4b7869072
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '1906'
ht-degree: 2%

---

# バーコードフォームの操作 {#working-with-barcoded-forms}

## バーコードフォームサービスについて {#about-the-barcoded-forms-service}

バーコードフォームサービスは、入力および印刷フォームからのデータのキャプチャを自動化し、取り込んだ情報を組織の主要な IT システムに統合します。

バーコードフォームサービスを使用すると、1 次元および 2 次元のバーコードをインタラクティブPDF formsに追加できます。 その後、バーコードフォームを Web サイトに公開したり、電子メールまたは CD で配布したりできます。 ユーザーがAdobe Reader、Acrobat Professional、Acrobat Standardを使用してバーコードフォームに入力すると、ユーザーが指定したフォームデータがエンコードされるようにバーコードが自動的に更新されます。 ユーザーは、フォームを電子的に送信したり、紙に印刷して、メール、FAX、または手で送信したりできます。 後で、自動化されたワークフローの一部として、ユーザーが指定したデータを抽出し、承認プロセスやビジネスシステム間でデータをルーティングできます。

バーコードフォームサービスについて詳しくは、 [AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63).

## バーコードフォームデータのデコード {#decoding-barcoded-form-data}

バーコードフォームサービス API を使用して、バーコードを含むPDFフォームまたは画像からデータをデコードできます。 フォームデータのデコードとは、バーコード内のデータを抽出することを意味します。 データをPDFフォーム（または画像）からデコードする前に、ユーザーはフォームにデータを入力する必要があります。

>[!NOTE]
>
>バーコードフォームサービスについて詳しくは、 [AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary-of-steps}

データをデコードフォームからPDFするには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. Barcoded FormsClient API オブジェクトを作成します。
1. バーコードPDFを含むデータフォームを取得します。
1. データをデコードフォームからPDFします。
1. データを XML データソースに変換します。
1. デコードされたデータを処理します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。 Web サービスを使用している場合は、プロキシファイルを必ず含めてください。

次の JAR ファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-barcodedforms-client.jar
* adobe-utilities.jar(AEM Formsを JBoss にデプロイする場合に必須 )
* jbossall-client.jar(AEM Formsが JBoss にデプロイされている場合に必須 )
* xercesImpl.jar( &lt;install directory=&quot;&quot;>/Adobe/Adobe_Experience_Manager_forms/sdk/client-libs\thirdparty)

AEM Formsが、JBOSS 以外のサポート対象の J2EE アプリケーションサーバー上にデプロイされている場合は、adobe-utilities.jar と jbossall-client.jar を、AEM Formsがデプロイされている J2EE アプリケーションサーバー専用の JAR ファイルに置き換える必要があります。 すべてのAEM Forms JAR ファイルの場所について詳しくは、 [AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**バーコードフォームクライアント API オブジェクトの作成**

プログラムによってバーコードフォームサービスの操作を実行する前に、Barcoded Formsサービスクライアントを作成する必要があります。 Java API を使用している場合は、 `BarcodedFormsServiceClient` オブジェクト。 バーコードフォーム Web サービス API を使用している場合は、 `BarcodedFormsServiceService` オブジェクト。

**バーコードPDFを含むデータフォームを取得する**

ユーザーデータがPDFされたバーコードフォームを取得する必要があります。

**データをPDF・フォームからデコード**

バーコードを含むPDFフォーム（または画像）を取得したら、データをデコードできます。 Barcoded Formsサービスは、次の種類のバーコードをサポートします。

* PDF417 バーコード。
* データ・マトリックス・バーコード。
* QR コードのバーコード。
* Codabar バーコード。
* Code 128 バーコード。
* Code 39 バーコード。
* EAN-13 バーコード。
* EAN-8 バーコード。

デコード API で 16 進数の文字セットを入力した場合は、バーコードの内容が 16 進文字列としてエンコードされます。 例えば、フォームで文字エンコーディングに UTF-8 を指定し、デコード操作で Hex を指定した場合、バーコードのコンテンツは &lt; `xb:content`> 要素を含める必要があります。 クライアントアプリケーションでアプリケーションロジックを作成することで、この 16 進数値を変換して元のコンテンツを取得できます。

**データを XML データソースに変換する**

フォームデータをデコードした後、XDP または XFDF データに変換できます。 例えば、別のフォームにデータを読み込むとします。 データを XFA フォームに読み込むには、そのデータを XDP データに変換する必要があります。 詳しくは、 [フォームデータの読み込み](/help/forms/developing/importing-exporting-data.md#importing-form-data).

**デコードされたデータを処理**

変換後のデータを処理して、ビジネス要件を満たすことができます。 例えば、データをデコードして変換した後に、ファイルに保存し、エンタープライズデータベースに保存し、別のフォームに入力することができます。 この節では、変換後のデータを XML ファイルとして保存する方法について説明します。

>[!NOTE]
>
>行区切り文字パラメーターとフィールド区切り文字パラメーターの値が同じ場合、バーコードフォームサービスはバーコードデータをデコードできません

**関連トピック**

[Java API を使用したバーコードフォームデータのデコード](barcoded-forms.md#decode-barcoded-form-data-using-the-java-api)

[Web サービス API を使用したバーコードフォームデータのデコード](barcoded-forms.md#decode-barcoded-form-data-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Java API を使用したバーコードフォームデータのデコード {#decode-barcoded-form-data-using-the-java-api}

Barcoded Forms API(Java) を使用してフォームデータをデコードします。

1. プロジェクトファイルを含める

   クライアント JAR ファイルを Java プロジェクトのクラスパスに含めます。

1. バーコードフォームクライアント API オブジェクトの作成

   の作成 `BarcodedFormsServiceClient` オブジェクトのコンストラクタを使用し、 `ServiceClientFactory` 接続プロパティを含むオブジェクト。

1. バーコードPDFを含むデータフォームを取得する

   * の作成 `java.io.FileInputStream` コンストラクタを使用し、PDFドキュメントの場所を指定する string 値を渡すことによって、バーコードデータを含むPDFフォームを表すオブジェクト。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. データをPDF・フォームからデコード

   を呼び出してフォームデータをデコードする `BarcodedFormsServiceClient` オブジェクトの `decode` メソッドを使用して、次の値を渡します。

   * この `com.adobe.idp.Document` オブジェクトを作成します。PDF・フォームが含まれます。
   * A `java.lang.Boolean` オブジェクトを返します。このオブジェクトは、PDF417 バーコードをデコードするかどうかを指定します。
   * A `java.lang.Boolean` データマトリクスバーコードをデコードするかどうかを指定するオブジェクト。
   * A `java.lang.Boolean` QR コードバーコードをデコードするかどうかを指定するオブジェクト。
   * A `java.lang.Boolean` codabar バーコードをデコードするかどうかを指定するオブジェクト。
   * A `java.lang.Boolean` コード 128 バーコードをデコードするかどうかを指定するオブジェクト。
   * A `java.lang.Boolean` コード 39 バーコードをデコードするかどうかを指定するオブジェクト。
   * A `java.lang.Boolean` EAN-13 バーコードをデコードするかどうかを指定するオブジェクト。
   * A `java.lang.Boolean` EAN-8 バーコードをデコードするかどうかを指定するオブジェクト。
   * A `com.adobe.livecycle.barcodedforms.CharSet` バーコードで使用される文字セットエンコーディング値を指定する列挙値。

   この `decode` メソッドは、 `org.w3c.dom.Document` デコードされたフォームデータを含むオブジェクト。

1. データを XML データソースに変換する

   デコードされたデータを、 `BarcodedFormsServiceClient` オブジェクトの `extractToXML` メソッドを使用して、次の値を渡します。

   * この `org.w3c.dom.Document` デコードされたデータを含むオブジェクト ( `decode` メソッドの戻り値 )。
   * A `com.adobe.livecycle.barcodedforms.Delimiter` 行の区切り文字を指定する列挙値。 次を指定することをお勧めします。 `Delimiter.Carriage_Return`.
   * A `com.adobe.livecycle.barcodedforms.Delimiter` フィールド区切り文字を指定する列挙値。 例えば、次のように指定します。 `Delimiter.Tab`.
   * A `com.adobe.livecycle.barcodedforms.XMLFormat` バーコードデータを XDP または XFDF XML データに変換するかどうかを指定する列挙値。 例えば、次のように指定します。 `XMLFormat.XDP` をクリックしてデータを XDP データに変換します。

   >[!NOTE]
   >
   >行区切り文字パラメーターとフィールド区切り文字パラメーターに同じ値を指定しないでください。

   この `extractToXML` メソッドは、 `java.util.List` 各要素が `org.w3c.dom.Document` オブジェクト。 フォーム上のバーコードごとに別々の要素があります。 つまり、フォームに 4 つのバーコードがある場合、返されるには 4 つの要素が含まれます `java.util.List` オブジェクト。

1. デコードされたデータを処理

   * 反復処理 `java.util.List` 各 `org.w3c.dom.Document` オブジェクトを指定します。
   * リストの各要素に対して、 `org.w3c.dom.Document` オブジェクトを `com.adobe.idp.Document` オブジェクト。 ( `org.w3c.dom.Document` オブジェクトを `com.adobe.idp.Document` オブジェクトは、「 Java API を使用したバーコード化されたフォームデータのデコード」の例に示されています )。
   * を呼び出して、XML データを XML ファイルとして保存します。 `com.adobe.idp.Document` オブジェクトの `copyToFile`、および XML ファイルを表す File オブジェクトを渡す

**関連トピック**

[クイックスタート（SOAP モード）:Java API を使用したバーコードされたフォームデータのデコード](/help/forms/developing/barcoded-forms-service-java-api.md#quick-start-soap-mode-decoding-barcoded-form-data-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Web サービス API を使用したバーコードフォームデータのデコード {#decode-barcoded-form-data-using-the-web-service-api}

Barcoded Forms API（Web サービス）を使用してフォームデータをデコードする：

1. プロジェクトファイルを含める

   * Barcoded Forms サービス WSDL を使用するMicrosoft .NET クライアントアセンブリを作成します。 詳しくは、 [Base64 エンコーディングを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding).
   * Microsoft .NET クライアントアセンブリを参照します。 詳しくは、 [Base64 エンコーディングを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding).

1. バーコードフォームクライアント API オブジェクトの作成

   Barcoded Forms サービス WSDL を使用するMicrosoft .NET クライアントアセンブリを使用して、 `BarcodedFormsServiceService` オブジェクトのデフォルトのコンストラクターを呼び出す。

1. バーコードPDFを含むデータフォームを取得する

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。この `BLOB` オブジェクトは、バーコードを含むPDFドキュメントを保存するために使用されます。
   * の作成 `System.IO.FileStream` オブジェクトを指定します。
   * コンテンツを格納するバイト配列を作成します。 `System.IO.FileStream` オブジェクト。 バイト配列のサイズは、 `System.IO.FileStream` オブジェクトの `Length` プロパティ。
   * を呼び出して、バイト配列にストリームデータを入力します。 `System.IO.FileStream` オブジェクトの `Read` メソッドを使用し、読み込むバイト配列、開始位置、ストリーム長を渡す。
   * 次の項目に `BLOB` オブジェクトを割り当てる `binaryData` プロパティにバイト配列の内容を入力します。

1. データをPDF・フォームからデコード

   を呼び出してフォームデータをデコードする `BarcodedFormsServiceService` オブジェクトの `decode` メソッドを使用して、次の値を渡します。

   * この `BLOB` オブジェクトを作成します。PDF・フォームが含まれます。
   * A `Boolean` オブジェクトを返します。このオブジェクトは、PDF417 バーコードをデコードするかどうかを指定します。
   * A `Boolean` データマトリクスバーコードをデコードするかどうかを指定するオブジェクト。
   * A `Boolean` QR コードバーコードをデコードするかどうかを指定するオブジェクト。
   * A `Boolean` codabar バーコードをデコードするかどうかを指定するオブジェクト。
   * A `Boolean` コード 128 バーコードをデコードするかどうかを指定するオブジェクト。
   * A `Bolean` コード 39 バーコードをデコードするかどうかを指定するオブジェクト。
   * A `Boolean` EAN-13 バーコードをデコードするかどうかを指定するオブジェクト。
   * A `Boolean` EAN-8 バーコードをデコードするかどうかを指定するオブジェクト。
   * A `CharSet` バーコードで使用される文字セットエンコーディング値を指定する列挙値。

   この `decode` メソッドは、デコードされたフォームデータを含む文字列値を返します。

1. データを XML データソースに変換する

   デコードされたデータを、 `BarcodedFormsServiceService` オブジェクトの `extractToXML` メソッドを使用して、次の値を渡します。

   * デコードされたデータを含む string 値 ( `decode` メソッドの戻り値 )。
   * A `Delimiter` 行の区切り文字を指定する列挙値。 次を指定することをお勧めします。 `Delimiter.Carriage_Return`.
   * A `Delimiter` フィールド区切り文字を指定する列挙値。 例えば、次のように指定します。 `Delimiter.Tab`.
   * A `XMLFormat` バーコードデータを XDP または XFDF XML データに変換するかどうかを指定する列挙値。 例えば、次のように指定します。 `XMLFormat.XDP` をクリックしてデータを XDP データに変換します。

   >[!NOTE]
   >
   >行区切り文字パラメーターとフィールド区切り文字パラメーターに同じ値を指定しないでください。

   この `extractToXML` メソッドは、 `Object` 各要素が `BLOB` インスタンス。 フォーム上のバーコードごとに別々の要素があります。 つまり、フォームに 4 つのバーコードがある場合、返されるには 4 つの要素が含まれます `Object` 配列。

1. デコードされたデータを処理

   * の作成 `System.IO.FileStream` オブジェクトを指定します。
   * のデータコンテンツを格納するバイト配列を作成します。 `BLOB` が返したオブジェクト `encryptPDFUsingPassword` メソッド。 バイト配列を生成するには、 `BLOB` オブジェクトの `binaryData` データメンバー。
   * の作成 `System.IO.BinaryWriter` オブジェクトのコンストラクタを呼び出し、 `System.IO.FileStream` オブジェクト。
   * を呼び出して、バイト配列の内容をPDFファイルに書き込みます。 `System.IO.BinaryWriter` オブジェクトの `Write` メソッドを使用してバイト配列を渡す。

**関連トピック**

[Base64 エンコーディングを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
