---
title: Postscript からPDF・ドキュメントへの変換
seo-title: Converting Postscript to PDF Documents
description: Distillerサービスを使用して、PostScript®、Encapsulated PostScript(EPS) および PRN ファイルを、ネットワーク経由でコンパクトで信頼性の高い、より安全なPDFファイルに変換します。 Distillerサービスは、Java API および Web Service API を使用して、大量の印刷ドキュメントを請求書や明細書などの電子ドキュメントに変換します。
seo-description: Use the Distiller service to convert PostScript®, Encapsulated PostScript (EPS), and PRN files to compact, reliable, and more secure PDF files over a network. The Distiller service converts large volumes of print documents to electronic documents, such as invoices and statements using the Java API and Web Service API.
uuid: 2143f406-1fdd-4551-a738-1a8388f8d478
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: operations
discoiquuid: 06ad343a-f74d-41f5-b3c8-b85bb723ceeb
role: Developer
exl-id: 8bfbeef8-d211-4e87-8cd5-adccb21a6e05
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '1311'
ht-degree: 7%

---

# Postscript からPDF・ドキュメントへの変換 {#converting-postscript-to-pdf-documents}

## Distiller Service について {#about-the-distiller-service}

Distiller®サービスは、PostScript®、Encapsulated PostScript(EPS) および PRN ファイルを、ネットワーク経由で圧縮、信頼性、より安全なPDFファイルに変換します。 Distiller サービスは、請求書や明細書など、容量の大きい印刷ドキュメントを電子ドキュメントに変換する際によく使用されます。ドキュメントを PDF に変換して、顧客にドキュメントの印刷バージョンと電子バージョンを送付できます。

>[!NOTE]
>
>Distillerサービスについて詳しくは、 [AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63).

## PostScript を変換してPDFドキュメントに {#converting-postscript-to-pdf-documents-inner}

このトピックでは、Distiller Service API（Java および Web サービス）を使用して、PostScript(PS)、Encapsulated PostScript(EPS) および PRN ファイルをプログラムでPDFドキュメントに変換する方法について説明します。

>[!NOTE]
>
>Distillerサービスについて詳しくは、 [AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>PostScript ファイルをPDFドキュメントに変換するには、AEM Formsをホストするサーバーに次のいずれかをインストールする必要があります。Acrobat 9またはMicrosoft Visual C++ 2005 の再頒布可能パッケージ。

### 手順の概要 {#summary-of-steps}

サポートされているタイプをPDFドキュメントに変換するには、次の手順に従います。

1. プロジェクトファイルを含めます。
1. Distillerサービスクライアントを作成します。
1. 変換するファイルを取得します。
1. 「PDF作成」操作を呼び出します。
1. PDF文書を保存します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。 Web サービスを使用している場合は、プロキシファイルを必ず含めてください。

**Distillerサービスクライアントの作成**

プログラムによってDistillerサービス操作を実行する前に、Distillerサービスクライアントを作成する必要があります。 Java API を使用している場合は、 `DistillerServiceClient` オブジェクト。 Web サービス API を使用している場合、 `DistillerServiceService` オブジェクト。

**変換するファイルを取得します**

変換するファイルを取得する必要があります。 例えば、PS ファイルをPDFドキュメントに変換するには、PS ファイルを取得する必要があります。

**「PDF作成」操作を呼び出す**

サービスクライアントを作成した後で、「PDF作成」操作を呼び出すことができます。 この操作を行うには、変換するドキュメントに関する情報（変換先のドキュメントのパスを含む）が必要です。

**PDF文書を保存**

PDF・ドキュメントは、PDF・ファイルとして保存できます。

**関連トピック**

[Java API を使用した PostScript ファイルのPDFへの変換](converting-postscript-pdf-documents.md#convert-a-postscript-file-to-pdf-using-the-java-api)

[Web サービス API を使用した PostScript ファイルのPDFへの変換](converting-postscript-pdf-documents.md#converting-a-postscript-file-to-pdf-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Output サービス API のクイックスタート](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### Java API を使用した PostScript ファイルのPDFへの変換 {#convert-a-postscript-file-to-pdf-using-the-java-api}

Distiller Service API(Java) を使用して、PostScript ファイルをPDFドキュメントに変換します。

1. プロジェクトファイルを含めます。

   Java プロジェクトのクラスパスに、adobe-distiller-client.jar などのクライアント JAR ファイルを含めます。

1. Distillerサービスクライアントを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * の作成 `DistillerServiceClient` オブジェクトのコンストラクタを使用し、 `ServiceClientFactory` オブジェクト。

1. 変換するファイルを取得します。

   * の作成 `java.io.FileInputStream` コンストラクタを使用し、ファイルの場所を指定する string 値を渡すことによって、変換するファイルを表すオブジェクト。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. 「PDF作成」操作を呼び出します。

   を呼び出す `DistillerServiceClient` オブジェクトの `createPDF` メソッドを使用して、次の値を渡します。

   * この `com.adobe.idp.Document` 変換する PS、EPS、PRN のいずれかのファイルを表すオブジェクト
   * A `java.lang.String` 変換するファイルの名前を格納するオブジェクト
   * A `java.lang.String` 使用するAdobe PDF設定の名前を格納するオブジェクト
   * A `java.lang.String` 使用するセキュリティ設定の名前を含むオブジェクト
   * オプション `com.adobe.idp.Document` オブジェクトドキュメントの生成時に適用されるPDFを含む
   * オプション `com.adobe.idp.Document` オブジェクトドキュメントに適用するメタデータ情報を含むPDF

   この `createPDF` メソッドは、 `CreatePDFResult` 新しいPDF・ドキュメントと生成可能なログ・ファイルを含むオブジェクト。 通常、ログファイルには、変換リクエストによって生成されるエラーメッセージや警告メッセージが含まれます。

1. PDF文書を保存します。

   新しく作成したPDF・ドキュメントを取得するには、次の操作を実行します。

   * を呼び出す `CreatePDFResult` オブジェクトの `getCreatedDocument` メソッド。 これにより、 `com.adobe.idp.Document` オブジェクト。
   * を呼び出す `com.adobe.idp.Document` オブジェクトの `copyToFile` メソッドを使用して、PDFドキュメントを抽出します。

   同様に、ログドキュメントを取得するには、次の操作を実行します。

   * を呼び出す `CreatePDFResult` オブジェクトの `getLogDocument` メソッド。 これにより、 `com.adobe.idp.Document` オブジェクト。
   * を呼び出す `com.adobe.idp.Document` オブジェクトの `copyToFile` メソッドを使用してログドキュメントを抽出します。


**関連トピック**

[手順の概要](converting-postscript-pdf-documents.md#summary-of-steps)

[クイックスタート（SOAP モード）:Java API を使用した PostScript ファイルからPDFドキュメントへの変換](/help/forms/developing/distiller-service-java-api-quick.md#quick-start-soap-mode-converting-a-postscript-file-to-a-pdf-document-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Web サービス API を使用した PostScript ファイルのPDFへの変換 {#converting-a-postscript-file-to-pdf-using-the-web-service-api}

Distiller Service API（Web サービス）を使用して、PostScript ファイルをPDFドキュメントに変換します。

1. プロジェクトファイルを含めます。

   MTOM を使用するMicrosoft .NET プロジェクトを作成します。 次の WSDL 定義を使用していることを確認します。 `http://localhost:8080/soap/services/DistillerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >置換 `localhost` を、AEM Formsをホストするサーバーの IP アドレスに設定します。

1. Distillerサービスクライアントを作成します。

   * の作成 `DistillerServiceClient` オブジェクトのデフォルトのコンストラクタを使用します。
   * の作成 `DistillerServiceClient.Endpoint.Address` オブジェクトを `System.ServiceModel.EndpointAddress` コンストラクタ。 WSDL をAEM Formsサービスに渡す文字列値 ( 例： `http://localhost:8080/soap/services/DistillerService?blob=mtom`.) を使用する必要はありません。 `lc_version` 属性。 この属性は、サービス参照を作成する際に使用されます。 ただし、 `?blob=mtom` MTOM を使用する。
   * の作成 `System.ServiceModel.BasicHttpBinding` オブジェクトを作成するには、 `DistillerServiceClient.Endpoint.Binding` フィールドに入力します。 戻り値を `BasicHttpBinding` にキャストします。
   * を `System.ServiceModel.BasicHttpBinding` オブジェクトの `MessageEncoding` ～に向かって `WSMessageEncoding.Mtom`. この値は、MTOM が確実に使用されるようにします。
   * 次のタスクを実行して、基本的な HTTP 認証を有効にします。

      * フィールドにAEM forms ユーザー名を割り当てます。 `DistillerServiceClient.ClientCredentials.UserName.UserName`.
      * 対応するパスワード値をフィールドに割り当てます。 `DistillerServiceClient.ClientCredentials.UserName.Password`.
      * 定数値を割り当て `HttpClientCredentialType.Basic` フィールドに `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 定数値を割り当て `BasicHttpSecurityMode.TransportCredentialOnly` フィールドに `BasicHttpBindingSecurity.Security.Mode`.

1. 変換するファイルを取得します。

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。この `BLOB` オブジェクトは、PDFドキュメントに変換するファイルを保存するために使用されます。
   * の作成 `System.IO.FileStream` オブジェクトを作成します。
   * コンテンツを格納するバイト配列を作成します。 `System.IO.FileStream` オブジェクト。 バイト配列のサイズは、 `System.IO.FileStream` オブジェクトの `Length` プロパティ。
   * を呼び出して、バイト配列にストリームデータを入力します。 `System.IO.FileStream` オブジェクトの `Read` メソッドを使用し、読み込むバイト配列、開始位置、ストリーム長を渡す。
   * 次の項目に `BLOB` オブジェクトを割り当てる `MTOM` プロパティにバイト配列の内容を入力します。

1. 「PDF作成」操作を呼び出します。

   を呼び出す `DistillerServiceService` オブジェクトの `CreatePDF2` メソッドを使用して、以下の必須値を渡します。

   * この `BLOB` 変換する PS ファイルを表すオブジェクト
   * 変換するファイルのパス名を含む文字列
   * 使用するAdobe PDF設定 ( 例えば、 `Standard`)
   * 使用するセキュリティ設定 ( 例えば、 `No Securit`y)
   * オプション `BLOB` オブジェクトドキュメントの生成時に適用されるPDFを含む
   * オプション `BLOB` オブジェクトドキュメントに適用するメタデータ情報を含むPDF
   * A `BLOB` PDF・ドキュメントの保存に使用する出力パラメータ
   * A `BLOB` ログを保存するために使用する出力パラメーター

1. PDF文書を保存します。

   * の作成 `System.IO.FileStream` オブジェクトを指定します。 署名済みPDFドキュメントのファイルの場所と、ファイルを開くモードを表す string 値を渡します。
   * コンテンツを格納するバイト配列を作成します。 `BLOB` が返したオブジェクト `CreatePDF2` メソッド（出力パラメーター）を使用します。 バイト配列を生成するには、 `BLOB` オブジェクトの `MTOM` データメンバー。
   * の作成 `System.IO.BinaryWriter` オブジェクトのコンストラクタを呼び出し、 `System.IO.FileStream` オブジェクト。
   * を呼び出して、バイト配列の内容をPDFファイルに書き込みます。 `System.IO.BinaryWriter` オブジェクトの `Write` メソッドを使用してバイト配列を渡す。

**関連トピック**

[手順の概要](converting-postscript-pdf-documents.md#summary-of-steps)

<!-- UNRESOLVED LINKS
[Quick Start (MTOM): Converting a PostScript file to a PDF document using the web service API](unresolvedlink-lc-qs-distiller-di.xml#ws624e3cba99b79e12e69a9941333732bac8-7f01.2)

[Quick Start (SwaRef): Converting a PostScript file to a PDF document using the web service API](unresolvedlink-lc-qs-distiller-di.xml#ws624e3cba99b79e12e69a9941333732bac8-7eff.2)
-->

[MTOM を使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRef を使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
