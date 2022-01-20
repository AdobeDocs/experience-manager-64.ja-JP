---
title: 複数の XDP フラグメントのアセンブリ
seo-title: Assembling Multiple XDP Fragments
description: Java API と Web Service API を使用して、複数の XDP フラグメントを 1 つの XDP ドキュメントにアセンブリします。
seo-description: Assemble multiple XDP fragments into a single XDP document using the Java API and Web Service API.
uuid: 9e74e0e0-568d-4760-91a8-03dc1362d497
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: operations
discoiquuid: 0ed1f69d-c212-4d47-a572-ae030f2983fc
role: Developer
exl-id: be9db93d-97e1-4d4e-8d07-1c58a4a1a44c
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '1887'
ht-degree: 3%

---

# 複数の XDP フラグメントのアセンブリ {#assembling-multiple-xdp-fragments}

複数の XDP フラグメントを 1 つの XDP ドキュメントにアセンブリできます。 例えば、各 XDP ファイルにヘルスフォームの作成に使用される 1 つ以上のサブフォームが含まれている XDP フラグメントについて考えてみましょう。 次の図に、アウトラインビューを示します ( *複数の XDP フラグメントのアセンブリ* クイックスタート ):

![am_am_forma](assets/am_am_forma.png)

次の図に、patient セクションを示します ( *複数の XDP フラグメントのアセンブリ* クイックスタート ):

![am_am_formb](assets/am_am_formb.png)

次の図に、患者の健康に関する節を示します ( *複数の XDP フラグメントのアセンブリ* クイックスタート ):

![am_am_formc](assets/am_am_formc.png)

このフラグメントには、 *subPatientPhysical* および *subPatientHealth*. これらの両方のサブフォームは、Assembler サービスに渡される DDX ドキュメント内で参照されます。 次の図に示すように、Assembler サービスを使用して、これらの XDP フラグメントをすべて 1 つの XDP ドキュメントに組み合わせることができます。

![am_am_formd](assets/am_am_formd.png)

次の DDX ドキュメントは、複数の XDP フラグメントを XDP ドキュメントにアセンブリします。

```as3
 <?xml version="1.0" encoding="UTF-8"?> 
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/"> 
         <XDP result="tuc018result.xdp"> 
            <XDP source="tuc018_template_flowed.xdp"> 
             <XDPContent insertionPoint="ddx_fragment" source="tuc018_contact.xdp" fragment="subPatientContact" required="false"/> 
               <XDPContent insertionPoint="ddx_fragment" source="tuc018_patient.xdp" fragment="subPatientPhysical" required="false"/> 
               <XDPContent insertionPoint="ddx_fragment" source="tuc018_patient.xdp" fragment="subPatientHealth" required="false"/> 
            </XDP> 
         </XDP>         
 </DDX>
```

DDX ドキュメントに XDP が含まれている `result` 結果の名前を指定するタグ。 この場合、値は `tuc018result.xdp`. この値は、Assembler サービスが結果を返した後に XDP ドキュメントを取得するために使用されるアプリケーションロジックで参照されます。 例えば、アセンブリされた XDP ドキュメントを取得するために使用される次の Java アプリケーションロジックについて考えてみます（値が太字で示されています）。

```as3
 //Iterate through the map object to retrieve the result XDP document 
 for (Iterator i = allDocs.entrySet().iterator(); i.hasNext();) { 
     // Retrieve the Map object’s value 
     Map.Entry e = (Map.Entry)i.next(); 
                  
     //Get the key name as specified in the  
     //DDX document  
     String keyName = (String)e.getKey(); 
     if (keyName.equalsIgnoreCase("tuc018result.xdp")) 
                 {  
         Object o = e.getValue(); 
         outDoc = (Document)o; 
  
         //Save the result PDF file 
         File myOutFile = new File("C:\\AssemblerResultXDP.xdp");  
         outDoc.copyToFile(myOutFile); 
     } 
 }
```

この `XDP source` タグは、XDP フラグメントを追加するためのコンテナとして、または同じ順序で追加される多数のドキュメントの 1 つとして使用できる完全な XDP ドキュメントを表す XDP ファイルを指定します。 この場合、XDP ドキュメントはコンテナとしてのみ使用されます ( 最初の図は *複数の XDP フラグメントのアセンブリ*) をクリックします。 つまり、他の XDP ファイルは XDP コンテナ内に配置されます。

サブフォームごとに、 `XDPContent` 要素（この要素はオプションです）。 上記の例では、次の 3 つのサブフォームがあることに注意してください。 `subPatientContact`, `subPatientPhysical`、および `subPatientHealth`. 両方の `subPatientPhysical` サブフォームおよび `subPatientHealth` サブフォームは、同じ XDP ファイル tuc018_patient.xdp に存在します。 fragment 要素は、Designer で定義されたサブフォームの名前を指定します。

>[!NOTE]
>
>Assembler サービスについて詳しくは、 [AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>DDX ドキュメントについて詳しくは、 [Assembler サービスと DDX リファレンス](https://www.adobe.com/go/learn_aemforms_ddx_63).

## 手順の概要 {#summary-of-steps}

複数の XDP フラグメントをアセンブリするには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. Assembler クライアントをPDFします。
1. 既存の DDX ドキュメントを参照します。
1. XDP ドキュメントを参照します。
1. 実行時オプションを設定します。
1. 複数の XDP ドキュメントをアセンブリします。
1. アセンブリされた XDP ドキュメントを取得します。

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

複数の XDP ドキュメントをアセンブリするには、DDX ドキュメントを参照する必要があります。 この DDX ドキュメントには `XDP result`, `XDP source`、および `XDPContent` 要素。

**XDP ドキュメントの参照**

複数の XDP ドキュメントをアセンブリするには、結果の XDP ドキュメントをアセンブリするために使用されるすべての XDP ファイルを参照します。 XDP ドキュメントに含まれるサブフォームの名前が、 `source` 属性が `fragment` 属性。 サブフォームは Designer で定義されます。 例えば、次の XML について考えてみます。

```as3
 <XDPContent insertionPoint="ddx_fragment" source="tuc018_contact.xdp" fragment="subPatientContact" required="false"/>
```

次の名前のサブフォーム： *subPatientContact* は、 *tuc018_contact.xdp*.

**実行時オプションを設定**

ジョブの実行中に Assembler サービスの動作を制御する実行時オプションを設定できます。 例えば、エラーが発生した場合にジョブの処理を続行するよう Assembler サービスに指示するオプションを設定できます。

**複数の XDP ドキュメントのアセンブリ**

複数の XDP ファイルをアセンブリするには、 `invokeDDX` 操作。 Assembler サービスは、コレクションオブジェクト内でアセンブリされた XDP ドキュメントを返します。

**アセンブリされた XDP ドキュメントの取得**

アセンブリされた XDP ドキュメントがコレクションオブジェクト内で返されます。 コレクションオブジェクトを繰り返し処理し、XDP ドキュメントを XDP ファイルとして保存します。 また、XDP ドキュメントを別のAEM Formsサービス（Output など）に渡すこともできます。

**関連トピック**

[Java API を使用した複数の XDP フラグメントのアセンブリ](assembling-multiple-xdp-fragments.md#assemble-multiple-xdp-fragments-using-the-java-api)

[Web サービス API を使用した複数の XDP フラグメントのアセンブリ](assembling-multiple-xdp-fragments.md#assemble-multiple-xdp-fragments-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[プログラムによるPDF文書の作成](/help/forms/developing/programmatically-assembling-pdf-documents.md)

[フラグメントを使用したPDFドキュメントの作成](/help/forms/developing/creating-document-output-streams.md)

## Java API を使用した複数の XDP フラグメントのアセンブリ {#assemble-multiple-xdp-fragments-using-the-java-api}

Assembler Service API(Java) を使用して、複数の XDP フラグメントをアセンブリします。

1. プロジェクトファイルを含めます。

   Java プロジェクトのクラスパスに、adobe-assembler-client.jar などのクライアント JAR ファイルを含めます。

1. Assembler クライアントをPDFします。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * の作成 `AssemblerServiceClient` オブジェクトのコンストラクタを使用し、 `ServiceClientFactory` オブジェクト。

1. 既存の DDX ドキュメントを参照します。

   * の作成 `java.io.FileInputStream` コンストラクターを使用して DDX ファイルの場所を指定する string 値を渡すことによって DDX ドキュメントを表すオブジェクト。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. XDP ドキュメントを参照します。

   * の作成 `java.util.Map` オブジェクトを使用して入力 XDP ドキュメントを保存するために使用します `HashMap` コンストラクタ。
   * の作成 `com.adobe.idp.Document` オブジェクトを選択し、 `java.io.FileInputStream` 入力 XDP ファイルを含むオブジェクト（各 XDP ファイルに対してこのタスクを繰り返します）。
   * エントリを `java.util.Map` オブジェクトを呼び出す `put` メソッドを使用し、次の引数を渡す。

      * キー名を表す string 値です。 この値は `source` DDX ドキュメントで指定された element 値（XDP ファイルごとにこのタスクを繰り返します）
      * A `com.adobe.idp.Document` に対応する XDP ドキュメントを格納するオブジェクト `source` 要素（XDP ファイルごとにこのタスクを繰り返します）

1. 実行時オプションを設定します。

   * の作成 `AssemblerOptionSpec` コンストラクタを使用して実行時オプションを格納するオブジェクト。
   * に属するメソッドを呼び出して、ビジネス要件を満たすように実行時オプションを設定する `AssemblerOptionSpec` オブジェクト。 例えば、エラーが発生したときにジョブの処理を続行するように Assembler サービスに指示するには、 `AssemblerOptionSpec` オブジェクトの `setFailOnError` メソッドとパス `false`.

1. 複数の XDP ドキュメントをアセンブリします。

   を呼び出す `AssemblerServiceClient` オブジェクトの `invokeDDX` メソッドを使用して、以下の必須値を渡します。

   * A `com.adobe.idp.Document` 使用する DDX ドキュメントを表すオブジェクト
   * A `java.util.Map` 入力 XDP ファイルを格納するオブジェクト
   * A `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` デフォルトのフォントやジョブログレベルを含む、実行時のオプションを指定するオブジェクト

   この `invokeDDX` メソッドは、 `com.adobe.livecycle.assembler.client.AssemblerResult` アセンブリされた XDP ドキュメントを格納するオブジェクト。

1. アセンブリされた XDP ドキュメントを取得します。

   アセンブリされた XDP ドキュメントを取得するには、次の操作を実行します。

   * を呼び出す `AssemblerResult` オブジェクトの `getDocuments` メソッド。 このメソッドは、 `java.util.Map` オブジェクト。
   * 反復処理 `java.util.Map` 結果が見つかるまでオブジェクトを閉じます。 `com.adobe.idp.Document` オブジェクト。
   * を呼び出す `com.adobe.idp.Document` オブジェクトの `copyToFile` メソッドを使用して、アセンブリされた XDP ドキュメントを抽出します。

**関連トピック**

[複数の XDP フラグメントのアセンブリ](assembling-multiple-xdp-fragments.md#assembling-multiple-xdp-fragments)

[クイックスタート（SOAP モード）:Java API を使用した複数の XDP フラグメントのアセンブリ](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-multiple-xdp-fragments-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Web サービス API を使用した複数の XDP フラグメントのアセンブリ {#assemble-multiple-xdp-fragments-using-the-web-service-api}

Assembler Service API（Web サービス）を使用して、複数の XDP フラグメントをアセンブリします。

1. プロジェクトファイルを含めます。

   MTOM を使用するMicrosoft .NET プロジェクトを作成します。 サービス参照を設定する際は、次の WSDL 定義を必ず使用してください。

   ```as3
    http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1.
   ```

   >[!NOTE]
   >
   >置換 `localhost` を、AEM Formsをホストするサーバーの IP アドレスに設定します。

1. Assembler クライアントをPDFします。

   * の作成 `AssemblerServiceClient` オブジェクトのデフォルトのコンストラクタを使用します。
   * の作成 `AssemblerServiceClient.Endpoint.Address` オブジェクトを `System.ServiceModel.EndpointAddress` コンストラクタ。 WSDL をAEM Formsサービスに指定する string 値 ( 例えば、 `http://localhost:8080/soap/services/AssemblerService?blob=mtom`) をクリックします。 を使用する必要はありません。 `lc_version` 属性。 この属性は、サービス参照を作成する際に使用されます。
   * の作成 `System.ServiceModel.BasicHttpBinding` オブジェクトを作成するには、 `AssemblerServiceClient.Endpoint.Binding` フィールドに入力します。 戻り値を `BasicHttpBinding` にキャストします。
   * を `System.ServiceModel.BasicHttpBinding` オブジェクトの `MessageEncoding` ～に向かって `WSMessageEncoding.Mtom`. この値は、MTOM が確実に使用されるようにします。
   * 次のタスクを実行して、基本的な HTTP 認証を有効にします。

      * AEM forms ユーザー名を `AssemblerServiceClient.ClientCredentials.UserName.UserName` フィールドに入力します。
      * 対応するパスワード値を `AssemblerServiceClient.ClientCredentials.UserName.Password`フィールドに入力します。
      * を `HttpClientCredentialType.Basic` 定数値 `BasicHttpBindingSecurity.Transport.ClientCredentialType`フィールドに入力します。
      * を `BasicHttpSecurityMode.TransportCredentialOnly` 定数値 `BasicHttpBindingSecurity.Security.Mode`フィールドに入力します。

1. 既存の DDX ドキュメントを参照します。

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。この `BLOB` オブジェクトは、DDX ドキュメントを保存するために使用されます。
   * の作成 `System.IO.FileStream` オブジェクトを開くには、コンストラクターを呼び出し、DDX ドキュメントのファイルの場所とファイルを開くモードを表す string 値を渡します。
   * コンテンツを格納するバイト配列を作成します。 `System.IO.FileStream` オブジェクト。 バイト配列のサイズは、 `System.IO.FileStream` オブジェクトの `Length` プロパティ。
   * を呼び出して、バイト配列にストリームデータを入力します。 `System.IO.FileStream` オブジェクトの `Read` メソッド。 読み取るバイト配列、開始位置、ストリーム長を渡します。
   * 次の項目に `BLOB` オブジェクトを割り当てる `MTOM` プロパティにバイト配列の内容を入力します。

1. XDP ドキュメントを参照します。

   * 入力 XDP ファイルごとに、 `BLOB` オブジェクトを指定します。 この `BLOB` オブジェクトは、入力ファイルを保存するために使用されます。
   * の作成 `System.IO.FileStream` オブジェクトを指定します。
   * コンテンツを格納するバイト配列を作成します。 `System.IO.FileStream` オブジェクト。 バイト配列のサイズは、 `System.IO.FileStream` オブジェクトの `Length` プロパティ。
   * を呼び出して、バイト配列にストリームデータを入力します。 `System.IO.FileStream` オブジェクトの `Read` メソッド。 読み取るバイト配列、開始位置、ストリーム長を渡します。
   * 次の項目に `BLOB` オブジェクトを割り当てる `MTOM` フィールドにバイト配列の内容を入力します。
   * の作成 `MyMapOf_xsd_string_To_xsd_anyType` オブジェクト。 このコレクションオブジェクトは、アセンブリされた XDP ドキュメントの作成に必要な入力ファイルを格納するために使用されます。
   * 入力ファイルごとに、 `MyMapOf_xsd_string_To_xsd_anyType_Item` オブジェクト。
   * キー名を表す string 値を `MyMapOf_xsd_string_To_xsd_anyType_Item` オブジェクトの `key` フィールドに入力します。 この値は、DDX ドキュメントで指定された要素の値と一致する必要があります。 （このタスクは入力 XDP ファイルごとに実行します）。
   * を `BLOB` 入力ファイルを `MyMapOf_xsd_string_To_xsd_anyType_Item` オブジェクトの `value` フィールドに入力します。 （このタスクは入力 XDP ファイルごとに実行します）。
   * を `MyMapOf_xsd_string_To_xsd_anyType_Item` オブジェクトを `MyMapOf_xsd_string_To_xsd_anyType` オブジェクト。 を呼び出す `MyMapOf_xsd_string_To_xsd_anyType` オブジェクトの `Add` メソッドを使用して、 `MyMapOf_xsd_string_To_xsd_anyType` オブジェクト。 （このタスクは入力 XDP ドキュメントごとに実行します）。

1. 実行時オプションを設定します。

   * の作成 `AssemblerOptionSpec` コンストラクタを使用して実行時オプションを格納するオブジェクト。
   * に属するデータメンバーに値を割り当てて、ビジネス要件を満たすようにランタイムオプションを設定する `AssemblerOptionSpec` オブジェクト。 例えば、エラーが発生した場合にジョブの処理を続行するように Assembler サービスに指示するには、 `false` から `AssemblerOptionSpec` オブジェクトの `failOnError` データメンバー。

1. 複数の XDP ドキュメントをアセンブリします。

   を呼び出す `AssemblerServiceClient` オブジェクトの `invokeDDX` メソッドを使用して、次の値を渡します。

   * A `BLOB` DDX ドキュメントを表すオブジェクト
   * この `MyMapOf_xsd_string_To_xsd_anyType` 必要なファイルを含むオブジェクト
   * An `AssemblerOptionSpec` 実行時のオプションを指定するオブジェクト

   この `invokeDDX` メソッドは、 `AssemblerResult` ジョブの結果と発生した例外を含むオブジェクト。

1. アセンブリされた XDP ドキュメントを取得します。

   新しく作成した XDP ドキュメントを取得するには、次の操作を実行します。

   * 次にアクセス： `AssemblerResult` オブジェクトの `documents` フィールド ( `Map` 結果のPDF・ドキュメントを格納するオブジェクト。
   * 反復処理 `Map` オブジェクトを使用して各結果ドキュメントを取得します。 次に、その配列メンバの `value` から `BLOB`.
   * PDFドキュメントを表すバイナリデータを、そのドキュメントにアクセスして抽出します `BLOB` オブジェクトの `MTOM` プロパティ。 XDP ファイルに書き出すことができるバイトの配列を返します。

**関連トピック**

[複数の XDP フラグメントのアセンブリ](assembling-multiple-xdp-fragments.md#assembling-multiple-xdp-fragments)

[MTOM を使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
