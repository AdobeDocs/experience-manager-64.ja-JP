---
title: FormsService にドキュメントを渡す
seo-title: Passing Documents to the FormsService
description: フォームデザインを含む com.adobe.idp.Document オブジェクトをFormsサービスに渡します。 Formsサービスは、com.adobe.idp.Document オブジェクトにあるフォームデザインをレンダリングします。
seo-description: Pass a com.adobe.idp.Document object that contains the form design to the Forms service. The Forms service renders the form design located in the com.adobe.idp.Document object.
uuid: 841e97f3-ebb8-4340-81a9-b6db11f0ec82
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: operations
discoiquuid: e23de3c3-f8a0-459f-801e-a0942fb1c6aa
role: Developer
exl-id: fe19e9b3-d662-4df2-b372-5006b794cde8
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '1670'
ht-degree: 3%

---

# Forms Service にドキュメントを渡す {#passing-documents-to-the-formsservice}

AEM Formsサービスは、ユーザーから情報を収集するために、インタラクティブPDF formsをクライアントデバイス（通常は Web ブラウザー）にレンダリングします。 インタラクティブPDFフォームは、通常 XDP ファイルとして保存され、Designer で作成されるフォームデザインに基づいています。 AEM Forms以降、 `com.adobe.idp.Document` フォームデザインを含むFormsサービスへのオブジェクト。 次に、Formsサービスは、 `com.adobe.idp.Document` オブジェクト。

を通過する利点 `com.adobe.idp.Document` Formsサービスに対するオブジェクトは、他のサービス操作が `com.adobe.idp.Document` インスタンス。 つまり、 `com.adobe.idp.Document` インスタンスを別のサービス操作から削除し、レンダリングします。 例えば、XDP ファイルがという名前の Content Services（非推奨）ノードに格納されているとします。 `/Company Home/Form Designs`（次の図に示すように）

プログラムによって Content Services（非推奨）（非推奨）から Loan.xdp を取得し、XDP ファイルを `com.adobe.idp.Document` オブジェクト。

>[!NOTE]
>
>Formsサービスについて詳しくは、 [AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63).

## 手順の概要 {#summary-of-steps}

Content Services（非推奨）から取得したドキュメントをFormsサービスに渡すには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. Formsと Document Management Client API オブジェクトを作成します。
1. Content Services（非推奨）からフォームデザインを取得します。
1. インタラクティブPDFフォームをレンダリング
1. フォームデータストリームを使用してアクションを実行します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。 Web サービスを使用している場合は、プロキシファイルを含めます。

**Formsと Document Management Client API オブジェクトの作成**

プログラムによってForms Service API 操作を実行する前に、Forms Client API オブジェクトを作成します。 また、このワークフローは Content Services（非推奨）から XDP ファイルを取得するので、Document Management API オブジェクトを作成します。

**Content Services（非推奨）からフォームデザインを取得する**

Java または Web サービス API を使用して、Content Services（非推奨）から XDP ファイルを取得します。 XDP ファイルは、 `com.adobe.idp.Document` インスタンス ( または `BLOB` インスタンス（web サービスを使用する場合）。 その後、 `com.adobe.idp.Document` Formsサービスのインスタンス。

**インタラクティブPDFフォームのレンダリング**

インタラクティブフォームをレンダリングするには、 `com.adobe.idp.Document` Content Services（非推奨）からFormsサービスに返されたインスタンス。

>[!NOTE]
>
>次の条件を満たす場合に、 `com.adobe.idp.Document` フォームデザインを含んだFormsサービスへの 次の 2 つの新しいメソッド： `renderPDFForm2` および `renderHTMLForm2` 受け入れる `com.adobe.idp.Document` フォームデザインを含むオブジェクト。

**フォームデータストリームを使用してアクションを実行します**

クライアントアプリケーションの種類に応じて、フォームをクライアント Web ブラウザーに書き込んだり、フォームをPDFファイルとして保存したりできます。 通常、Web ベースのアプリケーションは、フォームを Web ブラウザーに書き込みます。 ただし、デスクトップアプリケーションは通常、フォームをPDFファイルとして保存します。

**関連トピック**

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Forms Service API クイックスタート](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

## Java API を使用してForms Service にドキュメントを渡す {#pass-documents-to-the-forms-service-using-the-java-api}

Formsサービスおよび Content Services（非推奨）API(Java) を使用して Content Services（非推奨）から取得したドキュメントを渡します。

1. プロジェクトファイルを含める

   Java プロジェクトのクラスパスに、adobe-forms-client.jar や adobe-contentservices-client.jar などのクライアント JAR ファイルを含めます。

1. Formsと Document Management Client API オブジェクトの作成

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。（[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)を参照。）
   * の作成 `FormsServiceClient` オブジェクトのコンストラクタを使用し、 `ServiceClientFactory` オブジェクト。
   * コンストラクタを使用して `DocumentManagementServiceClientImpl` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. Content Services（非推奨）からフォームデザインを取得する

   を呼び出す `DocumentManagementServiceClientImpl` オブジェクトの `retrieveContent` メソッドを使用して、次の値を渡します。

   * コンテンツが追加されるストアを指定する string 値です。 デフォルトのストアは `SpacesStore`. この値は必須のパラメータです。
   * 取得するコンテンツの完全修飾パスを指定する string 値 ( 例： `/Company Home/Form Designs/Loan.xdp`) をクリックします。 この値は必須のパラメータです。
   * バージョンを指定する string 値。 この値はオプションのパラメーターで、空の文字列を渡すことができます。 この場合、最新バージョンが取得されます。

   この `retrieveContent` メソッドは、 `CRCResult` XDP ファイルを格納するオブジェクト。 の取得 `com.adobe.idp.Document` を呼び出すことによるインスタンス `CRCResult` オブジェクトの `getDocument` メソッド。

1. インタラクティブPDFフォームのレンダリング

   を呼び出す `FormsServiceClient` オブジェクトの `renderPDFForm2` メソッドを使用して、次の値を渡します。

   * A `com.adobe.idp.Document` Content Services（非推奨）から取得したフォームデザインを含むオブジェクト。
   * A `com.adobe.idp.Document` フォームに結合するデータを含むオブジェクト。 データを結合しない場合は、空の `com.adobe.idp.Document` オブジェクト。
   * A `PDFFormRenderSpec` 実行時オプションを保存するオブジェクト。 この値はオプションのパラメータで、 `null` 実行時のオプションを指定しない場合。
   * A `URLSpec` URI 値を格納するオブジェクト。 この値はオプションのパラメータで、 `null`.
   * A `java.util.HashMap` 添付ファイルを保存するオブジェクト。 この値はオプションのパラメータで、 `null` フォームにファイルを添付しない場合。

   この `renderPDFForm` メソッドは、 `FormsResult` クライアントの Web ブラウザーに書き込む必要があるフォームデータストリームを含むオブジェクト。

1. フォームデータストリームを使用してアクションを実行します

   * の作成 `com.adobe.idp.Document` を呼び出すことによってオブジェクトを取得 `FormsResult` オブジェクト `getOutputContent` メソッド。
   * のコンテンツタイプを取得する `com.adobe.idp.Document` オブジェクトを呼び出す `getContentType` メソッド。
   * を `javax.servlet.http.HttpServletResponse` を呼び出すことによるオブジェクトのコンテンツタイプ `setContentType` メソッドを使用して、 `com.adobe.idp.Document` オブジェクト。
   * の作成 `javax.servlet.ServletOutputStream` オブジェクトを使用します。オブジェクトは、 `javax.servlet.http.HttpServletResponse` オブジェクトの `getOutputStream` メソッド。
   * の作成 `java.io.InputStream` を呼び出すことによってオブジェクトを取得 `com.adobe.idp.Document` オブジェクトの `getInputStream` メソッド。
   * バイト配列を作成し、 `InputStream` オブジェクトの `read` メソッド。 バイト配列を引数として渡します。
   * を呼び出す `javax.servlet.ServletOutputStream` オブジェクトの `write` メソッドを使用して、フォームデータストリームをクライアント Web ブラウザーに送信します。 バイト配列を `write` メソッド。

**関連トピック**

[クイックスタート（SOAP モード）:Java API を使用してForms Service にドキュメントを渡す](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-passing-documents-to-the-forms-service-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Web サービス API を使用してForms Service にドキュメントを渡す {#pass-documents-to-the-forms-service-using-the-web-service-api}

Formsサービスおよび Content Services（非推奨） API（Web サービス）を使用して Content Services（非推奨）から取得したドキュメントを渡します。

1. プロジェクトファイルを含める

   MTOM を使用するMicrosoft .NET プロジェクトを作成します。 このクライアントアプリケーションは 2 つのAEM Formsサービスを呼び出すので、2 つのサービス参照を作成します。 Formsサービスに関連付けられたサービス参照に、次の WSDL 定義を使用します。 `http://localhost:8080/soap/services/FormsService?WSDL&lc_version=9.0.1`.

   Document Management サービスに関連付けられたサービス参照に対して、次の WSDL 定義を使用します。 `http://localhost:8080/soap/services/DocumentManagementService?WSDL&lc_version=9.0.1`.

   これは、 `BLOB` データタイプは、両方のサービス参照に共通で、完全に修飾されます `BLOB` データタイプを使用する場合。 対応する Web サービスのクイックスタートで、 `BLOB` インスタンスは完全に選定されています。

   >[!NOTE]
   >
   >置換 `localhost`* AEM Formsをホストするサーバーの IP アドレス*

1. Formsと Document Management Client API オブジェクトの作成

   * の作成 `FormsServiceClient` オブジェクトのデフォルトのコンストラクタを使用します。
   * の作成 `FormsServiceClient.Endpoint.Address` オブジェクトを `System.ServiceModel.EndpointAddress` コンストラクタ。 WSDL をAEM Formsサービスに渡す文字列値 ( 例： `http://localhost:8080/soap/services/FormsService?WSDL`) をクリックします。 を使用する必要はありません。 `lc_version` 属性。 この属性は、サービス参照を作成する際に使用されます )。
   * の作成 `System.ServiceModel.BasicHttpBinding` オブジェクトを作成するには、 `FormsServiceClient.Endpoint.Binding` フィールドに入力します。 戻り値を `BasicHttpBinding` にキャストします。
   * を `System.ServiceModel.BasicHttpBinding` オブジェクトの `MessageEncoding` ～に向かって `WSMessageEncoding.Mtom`. この値は、MTOM が確実に使用されるようにします。
   * 次のタスクを実行して、基本的な HTTP 認証を有効にします。

      * フィールドにAEM forms ユーザー名を割り当てます。 `FormsServiceClient.ClientCredentials.UserName.UserName`.
      * 対応するパスワード値をフィールドに割り当てます。 `FormsServiceClient.ClientCredentials.UserName.Password`.
      * 定数値を割り当て `HttpClientCredentialType.Basic` フィールドに `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * 定数値を割り当て `BasicHttpSecurityMode.TransportCredentialOnly` フィールドに `BasicHttpBindingSecurity.Security.Mode`.

   >[!NOTE]
   >
   >以下の手順を `DocumentManagementServiceClient`*サービスクライアント。*

1. Content Services（非推奨）からフォームデザインを取得する

   を呼び出して、コンテンツを取得する `DocumentManagementServiceClient` オブジェクトの `retrieveContent` メソッドを使用して、次の値を渡します。

   * コンテンツが追加されるストアを指定する string 値です。 デフォルトのストアは `SpacesStore`. この値は必須のパラメータです。
   * 取得するコンテンツの完全修飾パスを指定する string 値 ( 例： `/Company Home/Form Designs/Loan.xdp`) をクリックします。 この値は必須のパラメータです。
   * バージョンを指定する string 値。 この値はオプションのパラメーターで、空の文字列を渡すことができます。 この場合、最新バージョンが取得されます。
   * 参照リンクの値を格納する文字列出力パラメーター。
   * A `BLOB` コンテンツを格納する出力パラメーター。 この出力パラメーターを使用して、コンテンツを取得できます。
   * A `ServiceReference1.MyMapOf_xsd_string_To_xsd_anyType` コンテンツ属性を格納する出力パラメーター。
   * A `CRCResult` 出力パラメーター。 このオブジェクトを使用する代わりに、 `BLOB` 出力パラメーターを使用して、コンテンツを取得します。

1. インタラクティブPDFフォームのレンダリング

   を呼び出す `FormsServiceClient` オブジェクトの `renderPDFForm2` メソッドを使用して、次の値を渡します。

   * A `BLOB` Content Services（非推奨）から取得したフォームデザインを含むオブジェクト。
   * A `BLOB` フォームに結合するデータを含むオブジェクト。 データを結合しない場合は、空の `BLOB` オブジェクト。
   * A `PDFFormRenderSpec` 実行時オプションを保存するオブジェクト。 この値はオプションのパラメータで、 `null` 実行時のオプションを指定しない場合。
   * A `URLSpec` URI 値を格納するオブジェクト。 この値はオプションのパラメータで、 `null`.
   * A `Map` 添付ファイルを保存するオブジェクト。 この値はオプションのパラメータで、 `null` フォームにファイルを添付しない場合。
   * ページ数の保存に使用される長い出力パラメーター。
   * ロケール値の格納に使用される文字列出力パラメーターです。
   * A `FormsResult` インタラクティブPDFフォームの保存に使用する出力パラメーター `.`

   この `renderPDFForm2` メソッドは、 `FormsResult` インタラクティブPDFフォームを含むオブジェクト。

1. フォームデータストリームを使用してアクションを実行します

   * の作成 `BLOB` オブジェクトの `FormsResult` オブジェクトの `outputContent` フィールドに入力します。
   * の作成 `System.IO.FileStream` オブジェクトを指定します。 インタラクティブPDFドキュメントのファイルの場所と、ファイルを開くモードを表す string 値を渡します。
   * コンテンツを格納するバイト配列を作成します。 `BLOB` から取得したオブジェクト `FormsResult` オブジェクト。 バイト配列を生成するには、 `BLOB` オブジェクトの `MTOM` データメンバー。
   * の作成 `System.IO.BinaryWriter` オブジェクトのコンストラクタを呼び出し、 `System.IO.FileStream` オブジェクト。
   * を呼び出して、バイト配列の内容をPDFファイルに書き込みます。 `System.IO.BinaryWriter` オブジェクトの `Write` メソッドを使用してバイト配列を渡す。

**関連トピック**

[MTOM を使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
