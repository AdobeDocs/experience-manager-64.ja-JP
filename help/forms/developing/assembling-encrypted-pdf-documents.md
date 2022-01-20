---
title: 暗号化されたPDF文書の作成
seo-title: Assembling Encrypted PDF Documents
description: Java API および Web サービス API を使用して、暗号化されたPDFドキュメントをアセンブリします。
seo-description: Assemble encrypted PDF documents using the Java API and Web Service API.
uuid: d0948ec9-ab67-4fe4-9062-1c4938460b43
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: operations
discoiquuid: 6d75c7b1-9c0e-47f3-bdb1-61acf16b97f9
role: Developer
exl-id: fa543e13-f920-4b77-9762-36f115261e8c
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '1645'
ht-degree: 6%

---

# 暗号化されたPDF文書の作成 {#assembling-encrypted-pdf-documents}

Assembler サービスを使用して、PDFドキュメントをパスワードで暗号化できます。 PDF ドキュメントがパスワードを使用して暗号化されている場合、Adobe Reader または Acrobat で PDF ドキュメントを表示するには、パスワードを指定する必要があります。パスワードを使用して PDF ドキュメントを暗号化するには、PDF ドキュメントの暗号化に必要な暗号化要素の値を DDX ドキュメントに含める必要があります。

この説明では、次の DDX ドキュメントが使用されていると仮定します。

```as3
 <?xml version="1.0" encoding="UTF-8"?> 
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/"> 
        <PDF result="EncryptLoan.pdf" encryption="userProtect"> 
         <PDF source="inDoc" /> 
     </PDF> 
     <PasswordEncryptionProfile name="userProtect" compatibilityLevel="Acrobat7"> 
         <OpenPassword>AdobeOpen</OpenPassword> 
        </PasswordEncryptionProfile> 
 </DDX>
```

この DDX ドキュメント内では、 source 属性に値が割り当てられています `inDoc`. 1 つの入力PDFドキュメントのみが Assembler サービスに渡され、1 つのPDFドキュメントが返された場合、 `invokeOneDocument` 操作、値の割り当て `inDoc` をPDFソース属性に追加します。 を呼び出すとき `invokeOneDocument` 操作 `inDoc` 値は、DDX ドキュメントで指定する必要がある事前定義済みのキーです。

これに対し、2 つ以上の入力PDFドキュメントを Assembler サービスに渡す場合は、 `invokeDDX` 操作。 この場合、 `source` 属性。

PDFドキュメントをパスワードで暗号化する場合、AEM forms のインストールに Encryption サービスを含める必要はありません。 詳しくは、 [暗号化および復号化PDF・ドキュメント](/help/forms/developing/encrypting-decrypting-pdf-documents.md).

>[!NOTE]
>
>Assembler サービスについて詳しくは、 [AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>DDX ドキュメントについて詳しくは、 [Assembler サービスと DDX リファレンス](https://www.adobe.com/go/learn_aemforms_ddx_63).

## 手順の概要 {#summary-of-steps}

暗号化されたPDF・ドキュメントを組み立てるには、次の手順に従います。

1. プロジェクトファイルを含めます。
1. Assembler クライアントをPDFします。
1. 既存の DDX ドキュメントを参照します。
1. 保護されていないPDF文書を参照します。
1. 実行時オプションを設定します。
1. ドキュメントを暗号化します。
1. 暗号化されたPDF文書を保存します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。 Web サービスを使用している場合は、プロキシファイルを必ず含めてください。

次の JAR ファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar(AEM Formsを JBoss にデプロイする場合に必要 )
* jbossall-client.jar(AEM Formsが JBoss にデプロイされている場合に必要 )

AEM Formsが JBoss 以外のサポート対象の J2EE アプリケーションサーバーにデプロイされている場合は、adobe-utilities.jar ファイルと jbossall-client.jar ファイルを、AEM Formsがデプロイされている J2EE アプリケーションサーバーに固有の JAR ファイルに置き換える必要があります。 すべてのAEM Forms JAR ファイルの場所について詳しくは、 [AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Assembler クライアントの作成**

Assembler 操作をプログラムで実行する前に、Assembler サービスクライアントを作成する必要があります。

**既存の DDX ドキュメントの参照**

DDX ドキュメントを参照して、アセンブリドキュメントをPDFする必要があります。 例えば、この節で紹介した DDX ドキュメントについて考えてみましょう。 PDFドキュメントを暗号化するには、DDX ドキュメントに `PasswordEncryptionProfile` 要素。

**保護されていないPDF文書の参照**

セキュリティで保護されていないPDFドキュメントを暗号化するには、ドキュメントを参照し、Assembler サービスに渡す必要があります。 既に暗号化されているPDF・ドキュメントを参照する場合は、例外がスローされます。

**実行時オプションを設定**

ジョブの実行中に Assembler サービスの動作を制御する実行時オプションを設定できます。 例えば、エラーが発生した場合にジョブの処理を続行するよう Assembler サービスに指示するオプションを設定できます。 設定できる実行時オプションについて詳しくは、 `AssemblerOptionSpec` のクラス参照 [AEM Forms API リファレンス](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**ドキュメントを暗号化**

Assembler サービスクライアントを作成し、暗号化情報を含む DDX ドキュメントを参照し、セキュリティで保護されていないPDFドキュメントを参照し、実行時オプションを設定したら、 `invokeOneDocument` 操作。 入力PDFドキュメントが 1 つだけ Assembler サービスに渡される（そして 1 つのドキュメントが返される）ので、 `invokeOneDocument` の代わりに操作 `invokeDDX` 操作。

**暗号化されたPDF文書を保存**

Assembler サービスに渡されるPDFドキュメントが 1 つだけの場合、Assembler サービスは、コレクションオブジェクトではなく 1 つのドキュメントを返します。 つまり、 `invokeOneDocument` を指定すると、1 つのドキュメントが返されます。 この節で参照する DDX ドキュメントには暗号化情報が含まれているので、Assembler サービスはPDFで暗号化されたパスワードドキュメントを返します。

**関連トピック**

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[プログラムによるPDF文書の作成](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Java API を使用した暗号化PDFドキュメントのアセンブリ {#assemble-an-encrypted-pdf-document-using-the-java-api}

1. プロジェクトファイルを含めます。

   Java プロジェクトのクラスパスに、adobe-assembler-client.jar などのクライアント JAR ファイルを含めます。

1. Assembler クライアントを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * の作成 `AssemblerServiceClient` オブジェクトのコンストラクタを使用し、 `ServiceClientFactory` オブジェクト。

1. 既存の DDX ドキュメントを参照します。

   * の作成 `java.io.FileInputStream` コンストラクターを使用して DDX ファイルの場所を指定する string 値を渡すことによって DDX ドキュメントを表すオブジェクト。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. 保護されていないPDF文書を参照します。

   * の作成 `java.io.FileInputStream` オブジェクトのコンストラクタを使用し、保護されていないPDFドキュメントの場所を渡す。
   * の作成 `com.adobe.idp.Document` オブジェクトを選択し、 `java.io.FileInputStream` オブジェクトドキュメントを含むPDF。 この `com.adobe.idp.Document` オブジェクトが `invokeOneDocument` メソッド。

1. 実行時オプションを設定します。

   * の作成 `AssemblerOptionSpec` コンストラクタを使用して実行時オプションを格納するオブジェクト。
   * に属するメソッドを呼び出して、ビジネス要件を満たすように実行時オプションを設定する `AssemblerOptionSpec` オブジェクト。 例えば、エラーが発生したときにジョブの処理を続行するように Assembler サービスに指示するには、 `AssemblerOptionSpec` オブジェクトの `setFailOnError` メソッドとパス `false`.

1. ドキュメントを暗号化します。

   を呼び出す `AssemblerServiceClient` オブジェクトの `invokeOneDocument` メソッドを使用して、次の値を渡します。

   * A `com.adobe.idp.Document` DDX ドキュメントを表すオブジェクト。 この DDX ドキュメントに値が含まれていることを確認してください `inDoc` (PDFソース要素用 )
   * A `com.adobe.idp.Document` 保護されていないPDFドキュメントを含むオブジェクト。
   * A `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` デフォルトのフォントやジョブログレベルを含む、実行時のオプションを指定するオブジェクト。

   この `invokeOneDocument` メソッドは、 `com.adobe.idp.Document` パスワードで暗号化されたPDF・ドキュメントを含むオブジェクト。

1. 暗号化されたPDF文書を保存します。

   * の作成 `java.io.File` オブジェクトにマッピングされ、ファイル名の拡張子が.pdf であることを確認します。
   * を呼び出す `Document` オブジェクトの `copyToFile` メソッドを使用して、 `Document` オブジェクトをファイルに追加します。 必ず `Document` オブジェクト `invokeOneDocument` メソッドが返されました。

**関連トピック**

[クイックスタート（SOAP モード）:Java API を使用した暗号化されたPDFドキュメントのアセンブリ](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-an-encrypted-pdf-document-using-the-java-api)

## Web サービス API を使用した暗号化PDFドキュメントのアセンブリ {#assemble-an-encrypted-pdf-document-using-the-web-service-api}

1. プロジェクトファイルを含めます。

   MTOM を使用するMicrosoft .NET プロジェクトを作成します。 サービス参照を設定する際は、次の WSDL 定義を必ず使用してください。 `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >置換 `localhost` を、AEM Formsをホストするサーバーの IP アドレスに設定します。

1. Assembler クライアントを作成します。

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
   * を呼び出して、バイト配列にストリームデータを入力します。 `System.IO.FileStream` オブジェクトの `Read` メソッドを使用し、読み込むバイト配列、開始位置、ストリーム長を渡す。
   * 次の項目に `BLOB` オブジェクトを割り当てる `MTOM` フィールドにバイト配列の内容を入力します。

1. 保護されていないPDF文書を参照します。

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。この `BLOB` オブジェクトは、入力PDF・ドキュメントを格納するために使用します。 この `BLOB` オブジェクトが `invokeOneDocument` を引数として。
   * の作成 `System.IO.FileStream` オブジェクトを指定します。
   * コンテンツを格納するバイト配列を作成します。 `System.IO.FileStream` オブジェクト。 バイト配列のサイズは、 `System.IO.FileStream` オブジェクトの `Length` プロパティ。
   * を呼び出して、バイト配列にストリームデータを入力します。 `System.IO.FileStream` オブジェクトの `Read` メソッドを使用し、読み込むバイト配列、開始位置、ストリーム長を渡す。
   * 次の項目に `BLOB` オブジェクトを割り当てる `MTOM` フィールドにバイト配列の内容を入力します。

1. 実行時オプションを設定します。

   * の作成 `AssemblerOptionSpec` コンストラクタを使用して実行時オプションを格納するオブジェクト。
   * に属するデータメンバーに値を割り当てて、ビジネス要件を満たすようにランタイムオプションを設定する `AssemblerOptionSpec` オブジェクト。 例えば、エラーが発生した場合にジョブの処理を続行するように Assembler サービスに指示するには、 `false` から `AssemblerOptionSpec` オブジェクトの `failOnError` データメンバー。

1. ドキュメントを暗号化します。

   を呼び出す `AssemblerServiceClient` オブジェクトの `invokeOneDocument` メソッドを使用して、次の値を渡します。

   * A `BLOB` DDX ドキュメントを表すオブジェクト
   * A `BLOB` 保護されていないPDF文書を表すオブジェクト
   * An `AssemblerOptionSpec` 実行時のオプションを指定するオブジェクト

   この `invokeOneDocument` メソッドは、 `BLOB` 暗号化されたPDF・ドキュメントを含むオブジェクト。

1. 暗号化されたPDF文書を保存します。

   * の作成 `System.IO.FileStream` オブジェクトを作成するには、コンストラクターを呼び出し、暗号化されたPDFドキュメントのファイルの場所と、ファイルを開くモードを表す string 値を渡します。
   * コンテンツを格納するバイト配列を作成します。 `BLOB` オブジェクト `invokeOneDocument` メソッドが返されました。 バイト配列を生成するには、 `BLOB` オブジェクトの `MTOM` データメンバー。
   * の作成 `System.IO.BinaryWriter` オブジェクトのコンストラクタを呼び出し、 `System.IO.FileStream` オブジェクト。
   * を呼び出して、バイト配列の内容をPDFファイルに書き込みます。 `System.IO.BinaryWriter` オブジェクトの `Write` メソッドを使用してバイト配列を渡す。

**関連トピック**

[MTOM を使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
