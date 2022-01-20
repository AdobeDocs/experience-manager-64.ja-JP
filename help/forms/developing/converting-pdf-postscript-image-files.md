---
title: PDFを Postscript および Image ファイルに変換中
seo-title: Converting PDF to Postscript andImage Files
description: ConvertPDFサービスを使用して、Java API と Web サービス API を使用して、PDFドキュメントを PostScript に、また多数の画像形式 (JPEG、JPEG2000、PNG、TIFF) に変換します。
seo-description: Use the Convert PDF service to convert PDF documents to PostScript and to a number of image formats (JPEG, JPEG 2000, PNG, and TIFF) using the Java API and Web Service API.
uuid: 07da0391-7180-4197-aaa6-ae753d753b84
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: operations
discoiquuid: f8707752-2c83-461a-b83d-708754b0f3f6
role: Developer
exl-id: 4afed537-1694-4187-8968-608f49116c2e
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '2795'
ht-degree: 6%

---

# PDFを Postscript および画像ファイルに変換中 {#converting-pdf-to-postscript-andimage-files}

**Convert Service について**

ConvertPDFサービスは、PDFドキュメントを PostScript および様々な画像形式 (JPEG、JPEG2000、PNG およびTIFF) に変換します。 PDF ドキュメントの PostScript への変換は、PostScript プリンターでの無人のサーバーベース印刷に便利です。PDF ドキュメントをサポートしていないコンテンツ管理システムでドキュメントをアーカイブする場合、PDF ドキュメントをマルチページ TIFF ファイルに変換する方法が実用的です。

Convert タスクサービスを使用して、次のタスクをPDFできます。

* PDF ドキュメントを PostScript に変換します。
* PDFドキュメントを画像形式に変換します。

   >[!NOTE]
   >
   >Convert Convert サービスの詳細については、「PDFの変換」を参照してください。 [AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63).

## PDFドキュメントを PostScript に変換中 {#converting-pdf-documents-to-postscript}

ここでは、ConvertPDFサービス API（Java および Web サービス）を使用して、PDFドキュメントを PostScript ファイルにプログラムで変換する方法について説明します。 PostScript ファイルに変換するPDFドキュメントは、非インタラクティブPDFドキュメントである必要があります。 つまり、インタラクティブPDFドキュメントを PostScript ファイルに変換しようとすると、例外がスローされます。

>[!NOTE]
>
>Convert Convert サービスの詳細については、「PDFの変換」を参照してください。 [AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary-of-steps}

PDFドキュメントを PostScript ファイルに変換するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. Convert Service クライアントをPDFします。
1. PostScript ファイルに変換するPDFドキュメントを参照します。
1. コンバージョン実行時オプションを設定します。
1. PDFドキュメントを PostScript ファイルに変換します。
1. PostScript ファイルを保存します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。 Web サービスを使用している場合は、プロキシファイルを必ず含めてください。

**ConvertPDFクライアントの作成**

プログラムによって ConvertPDFサービスの操作を実行する前に、ConvertPDFサービスクライアントを作成する必要があります。 Java API を使用している場合は、 `ConvertPdfServiceClient` オブジェクト。 Web サービス API を使用している場合、 `ConvertPDFServiceService` オブジェクト。

この節では、AEM Formsで導入された Web サービス機能を使用します。 新しい機能にアクセスするには、 `lc_version` 属性。 (「Web サービスを使用した新しい機能へのアクセス」( [Web サービスを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-web-services).)

**PostScript ファイルに変換するPDFドキュメントを参照します。**

PostScript ファイルに変換するPDFドキュメントを参照します。 このトピックで前述したように、PDFドキュメントは非インタラクティブPDFドキュメントである必要があります。 インタラクティブPDFドキュメントを PostScript ファイルに変換しようとすると、例外が発生します。

**コンバージョン実行時オプションを設定する**

PDFドキュメントを PostScript ファイルに変換する際に、作成する PostScript タイプを指定するランタイムオプションを定義できます。 例えば、レベル 3 の PostScript ファイルを定義できます。

通常、生成される PostScript ファイルは、入力PDFドキュメントのサイズを反映します。 次を選択した場合、 `ShrinkToFit` オプション（ページに合わせて PostScript ファイルの出力を縮小します）を使用する場合、入力PDFドキュメントと生成された PostScript ファイルの間に違いはありません。 この `ShrinkToFit` 「 」オプションは、入力PDFドキュメントよりも小さいページサイズで印刷することを選択した場合にのみ有効になります。 小さいページサイズを選択するには、 `PageSize` オプション。 また、 `RotateAndCenter` 選択肢 `true` 正しい PostScript 出力を取得するには

同様に、 `ExpandToFit` オプション（ページに合わせて PostScript ファイルの出力を拡張）を使用すると、入力PDFドキュメントよりも大きいページサイズで印刷するように選択した場合にのみ有効になります。 より大きなページサイズを選択するには、 `PageSize` オプション。 また、 `RotateAndCenter` 選択肢 `true` 正しい PostScript 出力を取得するには

>[!NOTE]
>
>設定できる実行時の値について詳しくは、 `ToPSOptionsSpec` のクラス参照 [AEM Forms API リファレンス](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**PDFドキュメントを PostScript ファイルに変換する**

サービスクライアントを作成し、実行時オプションを設定した後、 PostScript 変換操作を呼び出すことができます。 この操作では、変換するドキュメントに関する情報（ターゲットドキュメントに適した PostScript レベルを含む）が必要になります。

**PostScript ファイルを保存します。**

PDFドキュメントを PostScript に変換した後、出力を PostScript ファイルとして保存できます。

**関連トピック**

[Java API を使用したPDFドキュメントの PS への変換](converting-pdf-postscript-image-files.md#convert-a-pdf-document-to-ps-using-the-java-api)

[Web サービス API を使用してPDFドキュメントを PS に変換する](converting-pdf-postscript-image-files.md#convert-a-pdf-document-to-ps-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[ConvertPDFサービス API クイックスタート](/help/forms/developing/convert-pdf-service-java-api.md#convert-pdf-service-java-api-quick-start-soap)

### Java API を使用したPDFドキュメントの PS への変換 {#convert-a-pdf-document-to-ps-using-the-java-api}

ConvertPDFサービス API(Java) を使用して、PDFドキュメントを PostScript に変換します。

1. プロジェクトファイルを含めます。

   Java プロジェクトのクラスパスに、adobe-convertpdf-client.jar などのクライアント JAR ファイルを含めます。

1. ConvertPDFクライアントを作成する。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用して `ConvertPdfServiceClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. PostScript ファイルに変換するPDFドキュメントを参照します。

   * の作成 `java.io.FileInputStream` オブジェクトを指定します。
   * の作成 `com.adobe.idp.Document` を使用してPDFドキュメントを保存するオブジェクト `com.adobe.idp.Document` コンストラクタ。 パス `java.io.FileInputStream` オブジェクトドキュメントを含むPDF。

1. コンバージョン実行時オプションを設定します。

   * の作成 `ToPSOptionsSpec` オブジェクトを指定します。
   * に属する適切なメソッドを呼び出して、実行時オプションを設定する `ToPSOptionsSpec` オブジェクト。 例えば、作成される PostScript レベルを定義するには、 `ToPSOptionsSpec` オブジェクトの `setPsLevel` メソッドと `PSLevel` PostScript レベルを指定する列挙値。 設定できるすべての実行時の値について詳しくは、 `ToPSOptionsSpec` のクラス参照 [AEM Forms API リファレンス](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

1. PDFドキュメントを PostScript ファイルに変換します。

   を呼び出す `ConvertPdfServiceClient`オブジェクトの `toPS2` メソッドを使用して、次の値を渡します。

   * A `com.adobe.idp.Document` PostScript ファイルに変換するPDFドキュメントを表すオブジェクト。
   * A `ToPSOptionsSpec` PostScript の実行時オプションを指定するオブジェクト。

   この `toPS2` メソッドは、 `Document` 新しい PostScript ドキュメントを格納するオブジェクト。

1. PostScript ファイルを保存します。

   * の作成 `java.io.File` オブジェクトを探し、ファイル名の拡張子が.ps であることを確認します。
   * を呼び出す `Document` オブジェクトの `copyToFile` メソッドを使用して、 `Document` オブジェクトをファイルに追加します ( `Document` が返したオブジェクト `toPS2` メソッド )。

**関連トピック**

[手順の概要](converting-pdf-postscript-image-files.md#summary-of-steps)

[クイックスタート（SOAP モード）:Java API を使用したPDFドキュメントの PostScript への変換](/help/forms/developing/convert-pdf-service-java-api.md#quick-start-soap-mode-converting-a-pdf-document-to-postscript-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Web サービス API を使用してPDFドキュメントを PS に変換する {#convert-a-pdf-document-to-ps-using-the-web-service-api}

ConvertPDFサービス API（Web サービス）を使用して、PDFドキュメントを PostScript に変換します。

1. プロジェクトファイルを含めます。

   MTOM を使用するMicrosoft .NET プロジェクトを作成します。 次の WSDL 定義を使用していることを確認します。 `http://localhost:8080/soap/services/ConvertPDFService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >置換 `localhost` を、AEM Formsをホストするサーバーの IP アドレスに設定します。

1. ConvertPDFクライアントを作成する。

   * の作成 `ConvertPdfServiceClient` オブジェクトのデフォルトのコンストラクタを使用します。
   * の作成 `ConvertPdfServiceClient.Endpoint.Address` オブジェクトを `System.ServiceModel.EndpointAddress` コンストラクタ。 WSDL をAEM Formsサービスに渡す文字列値 ( 例： `http://localhost:8080/soap/services/ConvertPDFService?blob=mtom`.) を使用する必要はありません。 `lc_version` 属性。 ただし、 `?blob=mtom`.
   * の作成 `System.ServiceModel.BasicHttpBinding` オブジェクトを作成するには、 `ConvertPdfServiceClient.Endpoint.Binding` フィールドに入力します。 戻り値を `BasicHttpBinding` にキャストします。
   * を `System.ServiceModel.BasicHttpBinding` オブジェクトの `MessageEncoding` ～に向かって `WSMessageEncoding.Mtom`. この値は、MTOM が確実に使用されるようにします。
   * 次のタスクを実行して、基本的な HTTP 認証を有効にします。

      * フィールドにAEM forms ユーザー名を割り当てます。 `ConvertPdfServiceClient.ClientCredentials.UserName.UserName`.
      * 対応するパスワード値をフィールドに割り当てます。 `ConvertPdfServiceClient.ClientCredentials.UserName.Password`.
      * 定数値を割り当て `HttpClientCredentialType.Basic` フィールドに `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 定数値を割り当て `BasicHttpSecurityMode.TransportCredentialOnly` フィールドに `BasicHttpBindingSecurity.Security.Mode`.

1. PostScript ファイルに変換するPDFドキュメントを参照します。

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。この `BLOB` オブジェクトは、PostScript ファイルに変換されたPDFドキュメントを保存するために使用されます。
   * の作成 `System.IO.FileStream` オブジェクトを変換するには、コンストラクタを呼び出し、変換するPDFドキュメントのファイルの場所と、ファイルを開くモードを表す string 値を渡します。
   * コンテンツを格納するバイト配列を作成します。 `System.IO.FileStream` オブジェクト。 バイト配列のサイズは、 `System.IO.FileStream` オブジェクトの `Length` プロパティ。
   * を呼び出して、バイト配列にストリームデータを入力します。 `System.IO.FileStream` オブジェクトの `Read` メソッドを使用し、読み取るバイト配列、開始位置、ストリーム長を渡す。
   * 次の項目に `BLOB` オブジェクトを割り当てる `MTOM` フィールドにバイト配列の内容を入力します。

1. コンバージョン実行時オプションを設定します。

   * の作成 `ToPSOptionsSpec` オブジェクトを指定します。
   * 実行時オプションを設定するには、 `ToPSOptionsSpec` オブジェクトのデータメンバー。 例えば、作成する PostScript レベルを定義するには、 `PSLevel` 列挙値を `ToPSOptionsSpec` オブジェクトの `psLevel` データメンバー。

1. PDFドキュメントを PostScript ファイルに変換します。

   を呼び出す `GeneratePDFServiceService` オブジェクトの `toPS2` メソッドを使用して、次の値を渡します。

   * A `BLOB` PostScript ファイルに変換するPDFドキュメントを表すオブジェクト
   * A `ToPSOptionsSpec` 実行時のオプションを指定するオブジェクト

   変換が完了したら、PostScript ドキュメントを表すバイナリデータを抽出し、そのドキュメントにアクセスします `BLOB` オブジェクトの `MTOM` プロパティ。 PostScript ファイルに書き出すことができるバイト配列を返します。

1. PostScript ファイルを保存します。

   * の作成 `System.IO.FileStream` オブジェクトを指定します。 PS ファイルのファイルの場所を表す string 値を渡します。
   * のデータコンテンツを格納するバイト配列を作成します。 `BLOB` が返したオブジェクト `encryptPDFUsingPassword` メソッド。 バイト配列を生成するには、 `BLOB` オブジェクトの `MTOM` フィールドに入力します。
   * の作成 `System.IO.BinaryWriter` オブジェクトのコンストラクタを呼び出し、 `System.IO.FileStream` オブジェクト。
   * を呼び出して、バイト配列の内容を PostScript ファイルに書き込みます。 `System.IO.BinaryWriter` オブジェクトの `Write` メソッドを使用してバイト配列を渡す。

**関連トピック**

[手順の概要](converting-pdf-postscript-image-files.md#summary-of-steps)

[MTOM を使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRef を使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## PDFドキュメントの画像形式への変換 {#converting-pdf-documents-to-image-formats}

ConvertPDFサービスを使用すると、PDFドキュメントを、JPEG、JPEG2000、TIFF、PNG などの画像形式にプログラムで変換できます。 PDFドキュメントを画像ファイルに変換すると、そのPDFドキュメントを画像ファイルとして使用できます。 例えば、イメージをストレージ用のエンタープライズコンテンツ管理システムに配置できます。

ConvertPDFサービスは、PDFドキュメントを画像に変換する際に、ドキュメント内の各ページに対して個別の画像を作成します。 つまり、ドキュメントに 20 ページが含まれている場合、 ConvertPDFサービスは 20 個の画像ファイルを作成します。 PDFドキュメントをPDF形式に変換する場合、PDFドキュメント内の各ページの個々の画像を作成するか、画像ドキュメント全体の単一の画像ファイルを作成できます。

>[!NOTE]
>
>Convert Convert サービスの詳細については、「PDFの変換」を参照してください。 [AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary_of_steps-1}

PDFドキュメントをサポートされている任意のタイプに変換するには、次の手順に従います。

1. プロジェクトファイルを含めます。
1. Convert Service クライアントをPDFします。
1. 変換するPDFドキュメントを取得します。
1. 実行時オプションを設定します。
1. 画像をPDFに変換します。
1. コレクションから画像ファイルを取得します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。 Web サービスを使用している場合は、プロキシファイルを必ず含めてください。

**ConvertPDFクライアントの作成**

プログラムによって ConvertPDFサービスの操作を実行する前に、ConvertPDFサービスクライアントを作成する必要があります。 Java API を使用している場合は、 `ConvertPdfServiceClient` オブジェクト。 Web サービス API を使用している場合、 `ConvertPDFServiceService` オブジェクト。

**変換するPDFドキュメントを取得**

画像に変換するPDFドキュメントを取得する必要があります。 インタラクティブPDFドキュメントを画像に変換することはできません。 その場合は、例外が発生します。 インタラクティブPDFドキュメントを画像ファイルに変換するには、変換前にPDFドキュメントを統合する必要があります。 ( [PDF文書の統合](/help/forms/developing/creating-document-output-streams.md#flattening-pdf-documents).)

**実行時オプションを設定**

画像形式や解像度の値など、実行時オプションを設定する必要があります。 実行時の値について詳しくは、 `ToImageOptionsSpec` のクラス参照 [AEM Forms API リファレンス](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**画像をPDFに変換する**

サービスクライアントを作成し、実行時オプションを設定した後、PDFドキュメントを画像に変換できます。 画像を含むコレクションオブジェクトが返されます。

**コレクションからの画像ファイルの取得**

Convert Image サービスが返すコレクションオブジェクトからPDFファイルを取得できます。 コレクションの各要素は `com.adobe.idp.Document` インスタンス ( または `BLOB` インスタンス（web サービスを使用している場合）をイメージファイル (JPGファイルなど ) として保存できます。

画像ファイルの形式は、 `ImageConvertFormat` 実行時オプション つまり、 `ImageConvertFormat` 実行時のオプション `ImageConvertFormat.JPEG`を使用する場合、画像ファイルをJPGファイルとして保存できます。

**関連トピック**

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[ConvertPDFサービス API クイックスタート](/help/forms/developing/convert-pdf-service-java-api.md#convert-pdf-service-java-api-quick-start-soap)

### Java API を使用してPDFドキュメントを画像ファイルに変換する {#convert-a-pdf-document-to-image-files-using-the-java-api}

ConvertPDFサービス API(Java) を使用して、PDFドキュメントを画像形式に変換します。

1. プロジェクトファイルを含めます。

   Java プロジェクトのクラスパスに、adobe-convertpdf-client.jar などのクライアント JAR ファイルを含めます。

1. ConvertPDFクライアントを作成する。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用して `ConvertPdfServiceClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. 変換するPDFドキュメントを取得します。

   * の作成 `java.io.FileInputStream` 変換するPDFドキュメントを表すオブジェクト。コンストラクタを使用し、変換ドキュメントの場所を指定する string 値を渡します。PDFドキュメント
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. 実行時オプションを設定します。

   * コンストラクタを使用して `ToImageOptionsSpec` オブジェクトを作成します。
   * 必要に応じて、このオブジェクトに属するメソッドを呼び出します。 例えば、 `setImageConvertFormat` メソッドと `ImageConvertFormat` 形式タイプを指定する enum 値。

   >[!NOTE]
   >
   >の設定 `ImageConvertFormat` 列挙値は必須です。

1. 画像をPDFに変換します。

   を呼び出す `ConvertPdfServiceClient` オブジェクトの `toImage2` メソッドを使用して、次の値を渡します。

   * A `com.adobe.idp.Document` 変換するPDFファイルを表すオブジェクト。
   * A `com.adobe.livecycle.converpdfservice.client.ToImageOptionsSpec` オブジェクトに含まれます。

   この `toImage2` メソッドは、 `java.util.List` 画像を含むオブジェクト。 コレクションの各要素は `com.adobe.idp.Document` インスタンス。

1. コレクションから画像ファイルを取得します。

   反復処理 `java.util.List` オブジェクトを使用して、画像が存在するかどうかを判断します。 各要素は `com.adobe.idp.Document` インスタンス。 を呼び出して画像を保存します。 `com.adobe.idp.Document` オブジェクトの `copyToFile` メソッドと `java.io.File` オブジェクト。

**関連トピック**

[クイックスタート（SOAP モード）:Java API を使用したPDFドキュメントのJPEGファイルへの変換](/help/forms/developing/convert-pdf-service-java-api.md#quick-start-soap-mode-converting-a-pdf-document-to-jpeg-files-using-the-java-api)

### Web サービス API を使用してPDFドキュメントを画像ファイルに変換する {#convert-a-pdf-document-to-image-files-using-the-web-service-api}

ConvertPDFサービス API（Web サービス）を使用して、PDFドキュメントを画像形式に変換します。

1. プロジェクトファイルを含めます。

   MTOM を使用するMicrosoft .NET プロジェクトを作成します。 次の WSDL 定義を使用していることを確認します。 `http://localhost:8080/soap/services/ConvertPDFService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >置換 `localhost` を、AEM Formsをホストするサーバーの IP アドレスに設定します。

1. 変換PDFクライアントを作成する

   * の作成 `ConvertPdfServiceClient` オブジェクトのデフォルトのコンストラクタを使用します。
   * の作成 `ConvertPdfServiceClient.Endpoint.Address` オブジェクトを `System.ServiceModel.EndpointAddress` コンストラクタ。 WSDL をAEM Formsサービスに渡す文字列値 ( 例： `http://localhost:8080/soap/services/ConvertPDFService?blob=mtom`.) を使用する必要はありません。 `lc_version` 属性。 ただし、 `?blob=mtom`.
   * の作成 `System.ServiceModel.BasicHttpBinding` オブジェクトを作成するには、 `ConvertPdfServiceClient.Endpoint.Binding` フィールドに入力します。 戻り値を `BasicHttpBinding` にキャストします。
   * を `System.ServiceModel.BasicHttpBinding` オブジェクトの `MessageEncoding` ～に向かって `WSMessageEncoding.Mtom`. この値は、MTOM が確実に使用されるようにします。
   * 次のタスクを実行して、基本的な HTTP 認証を有効にします。

      * フィールドにAEM forms ユーザー名を割り当てます。 `ConvertPdfServiceClient.ClientCredentials.UserName.UserName`.
      * 対応するパスワード値をフィールドに割り当てます。 `ConvertPdfServiceClient.ClientCredentials.UserName.Password`.
      * 定数値を割り当て `HttpClientCredentialType.Basic` フィールドに `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 定数値を割り当て `BasicHttpSecurityMode.TransportCredentialOnly` フィールドに `BasicHttpBindingSecurity.Security.Mode`.

1. 変換するPDFドキュメントを取得します。

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。この `BLOB` オブジェクトは、PDF・フォームを格納するために使用されます。
   * の作成 `System.IO.FileStream` オブジェクトを指定します。 PDFフォームの場所と、ファイルを開くモードを指定する string 値を渡します。
   * コンテンツを格納するバイト配列を作成します。 `System.IO.FileStream` オブジェクト。 バイト配列のサイズを決定するには、 `System.IO.FileStream` オブジェクトの `Length` プロパティ。
   * を呼び出して、バイト配列にストリームデータを入力します。 `System.IO.FileStream` オブジェクトの `Read` メソッド。 読み取るバイト配列、開始位置、ストリーム長を渡します。
   * 次の項目に `BLOB` オブジェクトを割り当てる `MTOM` フィールドにバイト配列の内容を入力します。

1. 実行時オプションを設定します。

   * コンストラクタを使用して `ToImageOptionsSpec` オブジェクトを作成します。
   * 必要に応じて、このオブジェクトに属するメソッドを呼び出します。 例えば、 `setImageConvertFormat` メソッドと `ImageConvertFormat` 形式タイプを指定する列挙値。

   >[!NOTE]
   >
   >の設定 `ImageConvertFormat` 列挙値は必須です。

1. 画像をPDFに変換します。

   を呼び出す `ConvertPDFServiceService` オブジェクトの `toImage2` メソッドを使用して、次の値を渡します。

   * A `BLOB` 変換するファイルを表すオブジェクト
   * A `ToImageOptionsSpec` ターゲット画像形式に関する様々な環境設定を含むオブジェクト

   この `toImage2` メソッドは、 `MyArrayOfBLOB` 新しく作成された画像ファイルを格納するオブジェクト。

1. コレクションから画像ファイルを取得します。

   * 内の要素数を決定 `MyArrayOfBLOB` オブジェクトの `Count` フィールドに入力します。 各要素は `BLOB` 画像を格納するオブジェクト。
   * 反復処理 `MyArrayOfBLOB` オブジェクトを選択し、各画像ファイルを保存します。

**関連トピック**

[MTOM を使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRef を使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
