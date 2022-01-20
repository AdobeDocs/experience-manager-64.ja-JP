---
title: ベイツナンバリングを使用したドキュメントのアセンブリ
seo-title: Assembling Documents Using Bates Numbering
description: 'ベイツナンバリングを使用して、Java および Web サービス API を使用してPDFドキュメントをアセンブリします。 '
seo-description: Use Bates numbering to assemble PDF documents using the Java and Web Service API.
uuid: 28d5faeb-6915-41a2-b6a0-78d255df024f
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: operations
discoiquuid: 77e9b895-1313-4a5b-a2d5-cdb65bdc1966
role: Developer
exl-id: 902fc62b-262e-4eb4-b580-dbfbf4344fa6
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '1908'
ht-degree: 5%

---

# ベイツナンバリングを使用したドキュメントのアセンブリ {#assembling-documents-using-bates-numbering}

ベイツ番号付けを使用すると、一意のPDFID を含むページドキュメントを組み立てることができます。 *通し番号* は、関連するドキュメントのバッチに一意の ID を適用する方法です。 ドキュメント内の各ページ（またはドキュメントのセット）に、ページを一意に識別するベイツ番号が割り当てられます。 例えば、原材料情報を含む、1 つの組立部品の製造に関する生産ドキュメントに、1 つの識別子が割り当てられます。ベイツナンバリングの数値は連続した増分値で、オプションでプレフィックスやサフィックスが付きます。プレフィックス+数値+サフィックスは、 *ベイツパターン*.

次の例は、ドキュメントのヘッダに一意の識別子を含む PDF ドキュメントを示しています。

![au_au_batesnumber](assets/au_au_batesnumber.png)

このディスカッションの目的で、一意のページ識別子がドキュメントのヘッダーに配置されます。 次の DDX ドキュメントが使用されているとします。

```as3
 <?xml version="1.0" encoding="UTF-8"?> 
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/"> 
        <PDF result="out.pdf"> 
        <Header> 
         <Center> 
             <StyledText> 
                 <p font-size="20pt"><BatesNumber/></p> 
             </StyledText> 
         </Center> 
     </Header> 
           <PDF source="map.pdf" /> 
          <PDF source="directions.pdf" /> 
          </PDF> 
 </DDX>
```

この DDX ドキュメントは、名前が付いた 2 つのPDFドキュメントを結合します *map.pdf* および* directions.pdf*を単一のPDF文書に 結果のPDFドキュメントには、一意のページ識別子で構成されるヘッダーが含まれます。 例えば、上の図のドキュメントは000016です。

>[!NOTE]
>
>この節を読む前に、Assembler サービスを使用したPDFドキュメントの組み立てに関する知識を身に付けておくことをお勧めします。 このセクションでは、入力ドキュメントを含むコレクションオブジェクトの作成や、返されたコレクションオブジェクトからの結果の抽出など、概念については説明しません。 ( [プログラムによるPDF文書の作成](/help/forms/developing/programmatically-assembling-pdf-documents.md).)

>[!NOTE]
>
>Assembler サービスについて詳しくは、 [AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>DDX ドキュメントについて詳しくは、 [Assembler サービスと DDX リファレンス](https://www.adobe.com/go/learn_aemforms_ddx_63).

## 手順の概要 {#summary-of-steps}

一意のページ識別子（通し番号）を含むPDFドキュメントを組み立てるには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. Assembler クライアントをPDFします。
1. 既存の DDX ドキュメントを参照します。
1. 参照入力PDF文書。
1. 初期通し番号の値を設定します。
1. 入力アセンブリドキュメントをPDFします。
1. 結果を抽出します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。 Web サービスを使用している場合は、プロキシファイルを必ず含めてください。

次の JAR ファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar(AEM Formsを JBoss にデプロイする場合に必要 )
* jbossall-client.jar(AEM Formsが JBoss にデプロイされている場合に必要 )

AEM Formsが JBoss 以外のサポート対象の J2EE アプリケーションサーバーにデプロイされている場合は、adobe-utilities.jar ファイルと jbossall-client.jar ファイルを、AEM Formsがデプロイされている J2EE アプリケーションサーバーに固有の JAR ファイルに置き換える必要があります。 すべてのAEM Forms JAR ファイルの場所について詳しくは、 [AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Assembler クライアントのPDF**

Assembler 操作をプログラムで実行する前に、Assembler サービスクライアントを作成する必要があります。

**既存の DDX ドキュメントの参照**

DDX ドキュメントを参照して、アセンブリドキュメントをPDFする必要があります。 例えば、この節で紹介した DDX ドキュメントについて考えてみましょう。 一意のページPDFを含む識別子ドキュメントを組み立てるには、DDX ドキュメントに `BatesNumber` 要素。

**参照入力PDFドキュメント**

入力PDFドキュメントを参照して、アセンブリドキュメントをPDFする必要があります。 例えば、map.pdf ドキュメントと directions.pdf ドキュメントを参照して、これらのPDFドキュメントを 1 つのPDFドキュメントにアセンブリする必要があります。

**初期通し番号の値を設定**

ビジネス要件に合わせて、初期の通し番号の値を設定できます。 例えば、初期値を000100に設定する必要があるとします。 初期値を設定しない場合、最初のページの値は000000になります。

**入力アセンブリドキュメントのPDF**

Assembler サービスクライアントを作成したら、を含む DDX ドキュメントを参照します `BatesNumber` 要素情報、入力PDFドキュメントの参照、実行時オプションの設定を行うには、 `invokeDDX` 一意のページ識別子を含むPDFドキュメントを組み立てる Assembler サービスの結果として発生する操作。

**結果を抽出**

Assembler サービスは、ジョブの結果を含むコレクションオブジェクトを返します。 結果の例外ドキュメントと、スローされたPDFを抽出できます。 この場合、暗号化されたPDFドキュメントは、収集オブジェクト内に配置されます。

>[!NOTE]
>
>コレクションオブジェクトが返されるのは、 `invokeDDX` 操作。 この操作は、2 つ以上の入力PDFドキュメントを Assembler サービスに渡す場合に使用します。 ただし、1 つの入力PDFドキュメントのみを Assembler サービスに渡す場合は、 `invokeOneDocument` 操作。 この操作の使用方法については、 [暗号化されたPDF文書の作成](/help/forms/developing/assembling-encrypted-pdf-documents.md).

**関連トピック**

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[プログラムによるPDF文書の作成](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Java API を使用したベイツナンバリングを使用したドキュメントのアセンブリ {#assemble-documents-with-bates-numbering-using-the-java-api}

Assembler Service API(Java) を使用して、一意のページPDF（通し番号）を使用する識別子ドキュメントを組み立てます。

1. プロジェクトファイルを含めます。

   Java プロジェクトのクラスパスに、adobe-assembler-client.jar などのクライアント JAR ファイルを含めます。

1. Assembler クライアントをPDFします。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * の作成 `AssemblerServiceClient` オブジェクトのコンストラクタを使用し、 `ServiceClientFactory` オブジェクト。

1. 既存の DDX ドキュメントを参照します。

   * の作成 `java.io.FileInputStream` コンストラクターを使用して DDX ファイルの場所を指定する string 値を渡すことによって DDX ドキュメントを表すオブジェクト。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. 参照入力PDF文書。

   * の作成 `java.util.Map` を使用して入力PDF・ドキュメントを格納するために使用されるオブジェクト `HashMap` コンストラクタ。
   * 入力PDFドキュメントごとに、 `java.io.FileInputStream` オブジェクトのコンストラクタを使用し、入力PDF・ドキュメントの場所を渡す。 この場合、保護されていないPDFドキュメントの場所を渡します。
   * 入力PDFドキュメントごとに、 `com.adobe.idp.Document` オブジェクトを選択し、 `java.io.FileInputStream` オブジェクトドキュメントを含むPDF。
   * エントリを `java.util.Map` オブジェクトを呼び出す `put` メソッドを使用し、次の引数を渡す。

      * キー名を表す string 値です。 この値は、DDX ドキュメントで指定されたPDFソース要素の値と一致する必要があります。 例えば、この節で紹介する DDX ドキュメントで指定されたPDFソースファイルの名前は Loan.pdf です。
      * A `com.adobe.idp.Document` 保護されていないPDFドキュメントを含むオブジェクト。

1. 初期通し番号の値を設定します。

   * の作成 `AssemblerOptionSpec` コンストラクタを使用して実行時オプションを格納するオブジェクト。
   * を呼び出して、初期の通し番号を設定します。 `AssemblerOptionSpec` オブジェクトの `setFirstBatesNumber` 初期値を指定する数値を渡す

1. 入力アセンブリドキュメントをPDFします。

   を呼び出す `AssemblerServiceClient` オブジェクトの `invokeDDX` メソッドを使用して、以下の必須値を渡します。

   * A `com.adobe.idp.Document` DDX ドキュメントを表すオブジェクト。
   * A `java.util.Map` 入力のセキュリティで保護されていないPDFファイルを含むオブジェクト。
   * A `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` デフォルトのフォントやジョブログレベルを含む、実行時のオプションを指定するオブジェクト。

   この `invokeDDX` メソッドは、 `com.adobe.livecycle.assembler.client.AssemblerResult` パスワードで暗号化されたPDF・ドキュメントを含むオブジェクト。

1. 結果を抽出します。

   新しく作成したPDF・ドキュメントを取得するには、次の操作を実行します。

   * を呼び出す `AssemblerResult` オブジェクトの `getDocuments` メソッド。 このアクションは、 `java.util.Map` オブジェクト。
   * 反復処理 `java.util.Map` オブジェクトを `com.adobe.idp.Document` オブジェクト。
   * を呼び出す `com.adobe.idp.Document` オブジェクトの `copyToFile` メソッドを使用して、PDFドキュメントを抽出します。

**関連トピック**

[クイックスタート（SOAP モード）:Java API を使用したPDFドキュメントのベイト番号付きアセンブリ](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-a-pdf-document-with-bates-numbering-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Web サービス API を使用して、ベイツナンバリングを使用してドキュメントをアセンブリする {#assemble-documents-with-bates-numbering-using-the-web-service-api}

Assembler Service API（Web サービス）を使用して、一意のページ識別子（通し番号）を使用するPDFドキュメントを組み立てます。

1. プロジェクトファイルを含めます。

   MTOM を使用するMicrosoft .NET プロジェクトを作成します。 次の WSDL 定義を使用していることを確認します。 `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

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
   * の作成 `System.IO.FileStream` オブジェクトを作成するには、コンストラクターを呼び出し、DDX ドキュメントのファイルの場所とファイルを開くモードを表す string 値を渡します。
   * コンテンツを格納するバイト配列を作成します。 `System.IO.FileStream` オブジェクト。 バイト配列のサイズは、 `System.IO.FileStream` オブジェクトの `Length` プロパティ。
   * を呼び出して、バイト配列にストリームデータを入力します。 `System.IO.FileStream` オブジェクトの `Read` メソッド。 読み取るバイト配列、開始位置、ストリーム長を渡します。
   * 次の項目に `BLOB` オブジェクトを割り当てる `MTOM` フィールドにバイト配列の内容を入力します。

1. 参照入力PDF文書。

   * 入力PDFドキュメントごとに、 `BLOB` オブジェクトを指定します。 この `BLOB` オブジェクトは、入力PDF・ドキュメントを格納するために使用します。
   * の作成 `System.IO.FileStream` オブジェクトを指定します。 入力PDFドキュメントのファイルの場所と、ファイルを開くモードを表す string 値を渡します。
   * コンテンツを格納するバイト配列を作成します。 `System.IO.FileStream` オブジェクト。 バイト配列のサイズは、 `System.IO.FileStream` オブジェクトの `Length` プロパティ。
   * を呼び出して、バイト配列にストリームデータを入力します。 `System.IO.FileStream` オブジェクトの `Read` メソッド。 読み取るバイト配列、開始位置、ストリーム長を渡します。
   * 次の項目に `BLOB` オブジェクトを割り当てる `MTOM` プロパティにバイト配列の内容を入力します。
   * の作成 `MyMapOf_xsd_string_To_xsd_anyType` オブジェクト。 このコレクションオブジェクトは、入力コレクションドキュメントをPDFするために使用されます。
   * 入力PDFドキュメントごとに、 `MyMapOf_xsd_string_To_xsd_anyType_Item` オブジェクト。 例えば、2 つの入力PDFドキュメントを使用する場合、 `MyMapOf_xsd_string_To_xsd_anyType_Item` オブジェクト。
   * キー名を表す string 値を `MyMapOf_xsd_string_To_xsd_anyType_Item` オブジェクトの `key` フィールドに入力します。 この値は、DDX ドキュメントで指定されたPDFソース要素の値と一致する必要があります。 ( このタスクは、入力タスクドキュメントごとにPDFします )。
   * を `BLOB` オブジェクトを指定し、PDFドキュメントを `MyMapOf_xsd_string_To_xsd_anyType_Item` オブジェクトの `value` フィールドに入力します。 ( このタスクは、入力タスクドキュメントごとにPDFします )。
   * を `MyMapOf_xsd_string_To_xsd_anyType_Item` オブジェクトを `MyMapOf_xsd_string_To_xsd_anyType` オブジェクト。 を呼び出す `MyMapOf_xsd_string_To_xsd_anyType` オブジェクトの `Add` メソッドを使用して、 `MyMapOf_xsd_string_To_xsd_anyType` オブジェクト。 ( このタスクは、入力タスクドキュメントごとにPDFします )。

1. 初期通し番号の値を設定します。

   * の作成 `AssemblerOptionSpec` コンストラクタを使用して実行時オプションを格納するオブジェクト。
   * 最初の通し番号を設定するには、 `firstBatesNumber` に属するデータメンバー `AssemblerOptionSpec` オブジェクト。

1. 入力アセンブリドキュメントをPDFします。

   を呼び出す `AssemblerServiceClient` オブジェクトの `invoke` メソッドを使用して、次の値を渡します。

   * A `BLOB` DDX ドキュメントを表すオブジェクト。
   * この `MyMapOf_xsd_string_To_xsd_anyType` 入力PDF・ドキュメントを格納するオブジェクト。 キーはPDFソースファイルの名前と一致する必要があり、値は `BLOB` これらのファイルに対応するオブジェクト。
   * An `AssemblerOptionSpec` 実行時オプションを指定するオブジェクト。

   この `invoke` メソッドは、 `AssemblerResult` ジョブの結果と発生した例外を含むオブジェクト。

1. 結果を抽出します。

   新しく作成したPDF・ドキュメントを取得するには、次の操作を実行します。

   * 次にアクセス： `AssemblerResult` オブジェクトの `documents` フィールド ( `Map` 結果PDF文書を含むオブジェクト。
   * 反復処理 `Map` オブジェクトを閉じます。 次に、その配列メンバの `value` から `BLOB`.
   * PDFドキュメントを表すバイナリデータを、そのドキュメントにアクセスして抽出します `BLOB` オブジェクトの `MTOM` プロパティ。 これは、バイトの配列を返し、PDF・ファイルに書き出すことができます。

**関連トピック**

[MTOM を使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
