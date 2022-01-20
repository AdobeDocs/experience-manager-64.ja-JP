---
title: 組み立てPDFPortfolio
seo-title: Assembling PDF Portfolios
description: PDFポートフォリオを組み立てて、Word ファイル、画像ファイル、PDFドキュメントなど、様々なタイプの複数のドキュメントを組み合わせます。 Java API と WebPDFAPI を使用して、サービスポートフォリオを組み立てることができます。
seo-description: Assemble a PDF portfolio to combine several documents of various types, including word file, image files, and PDF documents. You can assemble a PDF portfolio using a Java API and a Web Service API.
uuid: 1778c90b-9d26-466b-a7c7-401d737395e0
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: operations
discoiquuid: 023f0d9e-bfde-4879-a839-085fadffb48e
role: Developer
exl-id: 767d89bc-d243-46a1-a954-9977f4906566
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '1814'
ht-degree: 3%

---

# 組み立てPDFPortfolio {#assembling-pdf-portfolios}

Assembler Java および Web サービス API を使用してPDFPortfolioをアセンブルできます。 ポートフォリオは、word ファイル、画像ファイル（例えば、jpeg ファイル）、PDFドキュメントなど、様々なタイプの複数のドキュメントを組み合わせることができます。 ポートフォリオのレイアウトは、 *プレビュー付きグリッド*、 *画像上* レイアウトまたは偶数 *回転*.

次の図は、 *画像上* スタイルのレイアウト。

![ap_ap_portfolio](assets/ap_ap_portfolio.png)

PDFPortfolioを作成すると、ドキュメントのコレクションを渡す代わりにペーパーレスを使用できます。 AEM Formsを使用して、構造化 DDX ドキュメントで Assembler サービスを呼び出すことで、ポートフォリオを作成できます。 次の DDX ドキュメントは、PDFPortfolioを作成する DDX ドキュメントの例です。

```as3
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/"> 
     <PDF result="portfolio1.pdf"> 
         <Portfolio>   
             <Navigator source="myNavigator">   
                 <Resource name="navigator/image.xxx" source="myImage.png"/> 
             </Navigator> 
         </Portfolio> 
         <PackageFiles source="dog1"  > 
              <FieldData name="X">72</FieldData> 
             <FieldData name="Y">72</FieldData> 
             <File filename="saint_bernard.jpg" mimetype="image/jpeg"/> 
         </PackageFiles> 
         <PackageFiles source="dog2"  > 
             <FieldData name="X">120</FieldData> 
             <FieldData name="Y">216</FieldData> 
             <File filename="greyhound.pdf"/> 
         </PackageFiles>     
     </PDF> 
 </DDX>
```

DXX ドキュメントには、 `Portfolio` タグにネストされた `Navigator` タグを使用します。 タグをメモします。 `<Resource name="navigator/image.xxx" source="myImage.png"/>` が必要なのは、 `myNavigator` は onImage レイアウトナビゲーターとして割り当てられます。 `AdobeOnImage.nav`. このタグを使用すると、Assembler サービスは、ポートフォリオの背景として使用する画像を選択できます。 次を含む `PackageFiles` および `File` タグを使用して、パッケージ化されたファイルのファイル名と MIME タイプを定義します。

>[!NOTE]
>
>Assembler サービスについて詳しくは、 [AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>DDX ドキュメントについて詳しくは、 [Assembler サービスと DDX リファレンス](https://www.adobe.com/go/learn_aemforms_ddx_63).

## 手順の概要 {#summary-of-steps}

PDFPortfolioを作成するには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. Assembler クライアントをPDFします。
1. 既存の DDX ドキュメントを参照します。
1. 必要なドキュメントを参照します。
1. 実行時オプションを設定します。
1. ポートフォリオを組み立てます。
1. 組み立てられたポートフォリオを保存します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。 Web サービスを使用している場合は、プロキシファイルを必ず含めてください。

次の JAR ファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar(AEM Formsを JBoss にデプロイする場合に必要 )
* jbossall-client.jar(AEM Formsが JBoss にデプロイされている場合に必要 )

**Assembler クライアントのPDF**

Assembler 操作をプログラムで実行する前に、Assembler サービスクライアントを作成します。

**既存の DDX ドキュメントの参照**

DDX ドキュメントを参照して、アセンブリPortfolioをPDFします。 この DDX ドキュメントには `Portfolio`, `Navigator` そして `PackageFiles` 要素。

**必要なドキュメントの参照**

PDFPortfolioをアセンブリするには、アセンブリ対象のドキュメントを表すすべてのファイルを参照します。 例えば、DDX ドキュメントで指定されているすべての画像ファイルを Assembler サービスに渡します。 これらのファイルは、この節で指定した DDX ドキュメント内で参照されています。 *myImage.png* および *saint_bernard.jpg*.

PDFPortfolioをアセンブルする際に、NAV ファイル（ナビゲーターファイル）を Assembler サービスに渡します。 Assembler サービスに渡す NAV ファイルは、作成するPDFPortfolioの種類に応じて異なります。 例えば、 *画像上* レイアウトでは、 AdobeOnImage.nav ファイルを渡します。 NAV ファイルは次のフォルダーにあります。

`<Install folder>\Acrobat 9.0\Acrobat\Navigators`

NAV ファイルをAcrobat 9（またはそれ以降）のインストールディレクトリからコピーします。 NAV ファイルは、クライアントアプリケーションがアクセスできる場所に配置します。 すべてのファイルは、Map コレクションオブジェクト内の Assembler サービスに渡されます。

>[!NOTE]
>
>組み立てPDFPortfolioに関連するクイックスタートでは、AdobeOnImage.nav を使用します。

**実行時オプションを設定**

ジョブの実行中に Assembler サービスの動作を制御する実行時オプションを設定できます。 例えば、エラーが発生した場合にジョブの処理を続行するよう Assembler サービスに指示するオプションを設定できます。

**ポートフォリオの組み立て**

PDFPortfolioを組み立てるには、 `invokeDDX` 操作。 Assembler サービスは、コレクションオブジェクト内のPDFPortfolioを返します。

**組み立てられたポートフォリオを保存**

PDFPortfolioがコレクションオブジェクト内で返されます。 コレクションオブジェクトを繰り返し処理し、PDFPortfolioをPDFファイルとして保存します。

**関連トピック**

[Java API を使用したPDFPortfolioのアセンブリ](#assemble-a-pdf-portfolio-using-the-java-api)

[Web サービス API を使用したPDFPortfolioのアセンブリ](#assemble-a-pdf-portfolio-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[プログラムによるPDF文書の作成](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Java API を使用したPDFPortfolioのアセンブリ {#assemble-a-pdf-portfolio-using-the-java-api}

Assembler Service API(Java) を使用してPDFPortfolioをアセンブリします。

1. プロジェクトファイルを含めます。

   Java プロジェクトのクラスパスに、adobe-assembler-client.jar などのクライアント JAR ファイルを含めます。

1. Assembler クライアントをPDFします。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * の作成 `AssemblerServiceClient` オブジェクトのコンストラクタを使用し、 `ServiceClientFactory` オブジェクト。

1. 既存の DDX ドキュメントを参照します。

   * の作成 `java.io.FileInputStream` コンストラクターを使用して DDX ファイルの場所を指定する string 値を渡すことによって DDX ドキュメントを表すオブジェクト。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. 必要なドキュメントを参照します。

   * の作成 `java.util.Map` オブジェクトを使用して入力PDFドキュメントを格納する `HashMap` コンストラクタ。
   * コンストラクタを使用して `java.io.FileInputStream` オブジェクトを作成します。必要な NAV ファイルの場所を渡します（ポートフォリオの作成に必要な各ファイルに対して、このタスクを繰り返します）。
   * の作成 `com.adobe.idp.Document` オブジェクトを選択し、 `java.io.FileInputStream` NAV ファイルを含むオブジェクト（ポートフォリオの作成に必要なファイルごとに、このタスクを繰り返します）。
   * エントリを `java.util.Map` オブジェクトを呼び出す `put` メソッドを使用し、次の引数を渡す。

      * キー名を表す string 値です。 この値は、DDX ドキュメントで指定されたソース要素の値と一致する必要があります。 （ポートフォリオの作成に必要なファイルごとに、このタスクを繰り返します）。
      * A `com.adobe.idp.Document` オブジェクトドキュメントを含むPDF。 （ポートフォリオの作成に必要なファイルごとに、このタスクを繰り返します）。

1. 実行時オプションを設定します。

   * の作成 `AssemblerOptionSpec` コンストラクタを使用して実行時オプションを格納するオブジェクト。
   * に属するメソッドを呼び出して、ビジネス要件を満たすように実行時オプションを設定する `AssemblerOptionSpec` オブジェクト。 例えば、エラーが発生したときにジョブの処理を続行するように Assembler サービスに指示するには、 `AssemblerOptionSpec` オブジェクトの `setFailOnError` メソッドとパス `false`.

1. ポートフォリオを組み立てます。

   を呼び出す `AssemblerServiceClient` オブジェクトの `invokeDDX` メソッドを使用して、以下の必須値を渡します。

   * A `com.adobe.idp.Document` 使用する DDX ドキュメントを表すオブジェクト
   * A `java.util.Map` オブジェクトPortfolioを構築するために必要なファイルを含むPDF。
   * A `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` デフォルトのフォントやジョブログレベルを含む、ランタイムオプションを指定するオブジェクト

   この `invokeDDX` メソッドは、 `com.adobe.livecycle.assembler.client.AssemblerResult` アセンブリ済みのPDFPortfolioと発生した例外を含むオブジェクト。

1. 組み立てられたポートフォリオを保存します。

   PDFPortfolioを取得するには、次の操作を実行します。

   * を呼び出す `AssemblerResult` オブジェクトの `getDocuments` メソッド。 このメソッドは、 `java.util.Map` オブジェクト。
   * 反復処理 `java.util.Map` 結果が見つかるまでオブジェクトを閉じます。 `com.adobe.idp.Document` オブジェクト。
   * を呼び出す `com.adobe.idp.Document` オブジェクトの `copyToFile` メソッドを使用してPDFPortfolioを抽出します。

**関連トピック**

[クイックスタート（SOAP モード）:Java API を使用したPDFPortfolioのアセンブリ](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-pdf-portfolios-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Web サービス API を使用したPDFPortfolioのアセンブリ {#assemble-a-pdf-portfolio-using-the-web-service-api}

Assembler Service API（Web サービス）を使用してPDFPortfolioをアセンブリします。

1. プロジェクトファイルを含めます。

   MTOM を使用するMicrosoft .NET プロジェクトを作成します。 サービス参照を設定する際は、次の WSDL 定義を必ず使用してください。 `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >置換 `localhost` を、AEM Formsをホストするサーバーの IP アドレスに設定します。

1. Assembler クライアントをPDFします。

   * の作成 `AssemblerServiceClient` オブジェクトのデフォルトのコンストラクタを使用します。
   * の作成 `AssemblerServiceClient.Endpoint.Address` オブジェクトを `System.ServiceModel.EndpointAddress` コンストラクタ。 WSDL をAEM Formsサービスに渡す文字列値 ( 例： `http://localhost:8080/soap/services/AssemblerService?blob=mtom`) をクリックします。 を使用する必要はありません。 `lc_version` 属性。 この属性は、サービス参照を作成する際に使用されます。
   * の作成 `System.ServiceModel.BasicHttpBinding` オブジェクトを作成するには、 `AssemblerServiceClient.Endpoint.Binding` フィールドに入力します。 戻り値を `BasicHttpBinding` にキャストします。
   * を `System.ServiceModel.BasicHttpBinding` オブジェクトの `MessageEncoding` ～に向かって `WSMessageEncoding.Mtom`. この値は、MTOM が確実に使用されるようにします。
   * 次のタスクを実行して、基本的な HTTP 認証を有効にします。

      * フィールドにAEM forms ユーザー名を割り当てます。 `AssemblerServiceClient.ClientCredentials.UserName.UserName`.
      * 対応するパスワード値をフィールドに割り当てます。 `AssemblerServiceClient.ClientCredentials.UserName.Password`.
      * 定数値を割り当て `HttpClientCredentialType.Basic` フィールドに `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 定数値を割り当て `BasicHttpSecurityMode.TransportCredentialOnly` フィールドに `BasicHttpBindingSecurity.Security.Mode`.

1. 既存の DDX ドキュメントを参照します。

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。この `BLOB` オブジェクトは、DDX ドキュメントを保存するために使用されます。
   * の作成 `System.IO.FileStream` オブジェクトを開くには、コンストラクターを呼び出し、DDX ドキュメントのファイルの場所とファイルを開くモードを表す string 値を渡します。
   * コンテンツを格納するバイト配列を作成します。 `System.IO.FileStream` オブジェクト。 バイト配列のサイズは、 `System.IO.FileStream` オブジェクトの `Length` プロパティ。
   * を呼び出して、バイト配列にストリームデータを入力します。 `System.IO.FileStream` オブジェクトの `Read` メソッド。 読み取るバイト配列、開始位置、ストリーム長を渡します。
   * 次の項目に `BLOB` オブジェクトを割り当てる `MTOM` プロパティにバイト配列の内容を入力します。

1. 必要なドキュメントを参照します。

   * 入力ファイルごとに、 `BLOB` オブジェクトを指定します。 この `BLOB` オブジェクトは、入力ファイルを保存するために使用されます。
   * の作成 `System.IO.FileStream` オブジェクトを指定します。
   * コンテンツを格納するバイト配列を作成します。 `System.IO.FileStream` オブジェクト。 バイト配列のサイズは、 `System.IO.FileStream` オブジェクトの `Length` プロパティ。
   * を呼び出して、バイト配列にストリームデータを入力します。 `System.IO.FileStream` オブジェクトの `Read` メソッド。 読み取るバイト配列、開始位置、ストリーム長を渡します。
   * 次の項目に `BLOB` オブジェクトを割り当てる `MTOM` フィールドにバイト配列の内容を入力します。
   * の作成 `MyMapOf_xsd_string_To_xsd_anyType` オブジェクト。 このコレクションオブジェクトは、PDFPortfolioの作成に必要な入力ファイルの格納に使用されます。
   * 入力ファイルごとに、 `MyMapOf_xsd_string_To_xsd_anyType_Item` オブジェクト。
   * キー名を表す string 値を `MyMapOf_xsd_string_To_xsd_anyType_Item` オブジェクトの `key` フィールドに入力します。 この値は、DDX ドキュメントで指定された要素の値と一致する必要があります。 （入力ファイルごとにこのタスクを実行します）。
   * を `BLOB` 入力ファイルを `MyMapOf_xsd_string_To_xsd_anyType_Item` オブジェクトの `value` フィールドに入力します。 ( このタスクは、入力タスクドキュメントごとにPDFします )。
   * を `MyMapOf_xsd_string_To_xsd_anyType_Item` オブジェクトを `MyMapOf_xsd_string_To_xsd_anyType` オブジェクト。 を呼び出す `MyMapOf_xsd_string_To_xsd_anyType` オブジェクトの `Add` メソッドを使用して、 `MyMapOf_xsd_string_To_xsd_anyType` オブジェクト。 ( このタスクは、入力タスクドキュメントごとにPDFします )。

1. 実行時オプションを設定します。

   * の作成 `AssemblerOptionSpec` コンストラクタを使用して実行時オプションを格納するオブジェクト。
   * に属するデータメンバーに値を割り当てて、ビジネス要件を満たすようにランタイムオプションを設定する `AssemblerOptionSpec` オブジェクト。 例えば、エラーが発生した場合にジョブの処理を続行するように Assembler サービスに指示するには、 `false` から `AssemblerOptionSpec` オブジェクトの `failOnError` データメンバー。

1. ポートフォリオを組み立てます。

   を呼び出す `AssemblerServiceClient` オブジェクトの `invokeDDX` メソッドを使用して、次の値を渡します。

   * A `BLOB` DDX ドキュメントを表すオブジェクト
   * この `MyMapOf_xsd_string_To_xsd_anyType` 必要なファイルを含むオブジェクト
   * An `AssemblerOptionSpec` 実行時のオプションを指定するオブジェクト

   この `invokeDDX` メソッドは、 `AssemblerResult` ジョブの結果と発生した例外を含むオブジェクト。

1. 組み立てられたポートフォリオを保存します。

   新しく作成されたPDFPortfolioを取得するには、次の操作を実行します。

   * 次にアクセス： `AssemblerResult` オブジェクトの `documents` フィールド ( `Map` 結果のPDF・ドキュメントを格納するオブジェクト。
   * 反復処理 `Map` オブジェクトを使用して各結果ドキュメントを取得します。 次に、その配列メンバの `value` から `BLOB`.
   * PDFドキュメントを表すバイナリデータを、そのドキュメントにアクセスして抽出します `BLOB` オブジェクトの `MTOM` プロパティ。 これは、バイトの配列を返し、PDF・ファイルに書き出すことができます。

**関連トピック**

[MTOM を使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRef を使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
