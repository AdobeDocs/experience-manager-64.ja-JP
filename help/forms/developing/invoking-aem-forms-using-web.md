---
title: Web サービスを使用した AEM Forms の呼び出し
seo-title: Invoking AEM Forms using Web Services
description: WSDL 生成を完全にサポートする Web サービスを使用して、AEM Formsプロセスを呼び出します。
seo-description: Invoke AEM Forms processes using web services with full support for WSDL generation.
uuid: 66bcd010-c476-4b66-831d-a48307d8d67a
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: coding
discoiquuid: d5722281-bea9-4fc7-abdc-e678899e0a15
role: Developer
exl-id: cd4b5e40-afd5-422d-ae2e-cfde0f4d6b1a
source-git-commit: e608249c3f95f44fdc14b100910fa11ffff5ee32
workflow-type: tm+mt
source-wordcount: '9928'
ht-degree: 6%

---

# Web サービスを使用した AEM Forms の呼び出し {#invoking-aem-forms-using-web-services}

サービスコンテナ内のAEM Formsサービスのほとんどは、Web サービスを公開するように設定され、Web サービス定義言語 (WSDL) の生成が完全にサポートされます。 つまり、AEM Formsサービスのネイティブ SOAP スタックを使用するプロキシオブジェクトを作成できます。 その結果、AEM Formsサービスは次の SOAP メッセージを交換して処理できます。

* **SOAP リクエスト**:アクションをリクエストするクライアントアプリケーションによってFormsサービスに送信されます。
* **SOAP 応答**:SOAP リクエストの処理後に、Formsサービスによってクライアントアプリケーションに送信されます。

Web サービスを使用すると、Java API を使用して実行できる操作と同じAEM Forms Services 操作を実行できます。 Web サービスを使用してAEM Formsサービスを呼び出す利点の 1 つは、SOAP をサポートする開発環境でクライアントアプリケーションを作成できることです。 クライアントアプリケーションは、特定の開発環境やプログラミング言語に結び付けられません。 例えば、Microsoft Visual Studio .NET と C#をプログラミング言語として使用して、クライアントアプリケーションを作成できます。

AEM Formsサービスは、SOAP プロトコルで公開され、WSI Basic Profile 1.1 に準拠しています。 Web Services Interoperability(WSI) は、プラットフォーム間での Web サービスの相互運用性を促進するオープンスタンダード組織です。 詳しくは、 [https://www.ws-i.org/](https://www.ws-i.org).

AEM Formsは、次の Web サービス標準をサポートしています。

* **エンコード**:ドキュメントおよびリテラルエンコーディングのみがサポートされます（WSI 基本プロファイルに従った推奨のエンコーディングです）。 ( [Base64 エンコーディングを使用したAEM Formsの呼び出し](#invoking-aem-forms-using-base64-encoding).)
* **MTOM**:SOAP 要求で添付ファイルをエンコードする方法を表します。 ( [MTOM を使用したAEM Formsの呼び出し](#invoking-aem-forms-using-mtom).)
* **SwaRef**:SOAP 要求で添付ファイルをエンコードする別の方法を表します。 ( [SwaRef を使用したAEM Formsの呼び出し](#invoking-aem-forms-using-swaref).)
* **添付ファイル付き SOAP**:MIME と DIME(Direct Internet Message Encapsulation) の両方をサポートします。 これらのプロトコルは、SOAP 経由で添付ファイルを送信する標準的な方法です。 Microsoft Visual Studio .NET アプリケーションは DIME を使用します。 ( [Base64 エンコーディングを使用したAEM Formsの呼び出し](#invoking-aem-forms-using-base64-encoding).)
* **WS-Security**:ユーザー名パスワードトークンプロファイルをサポートします。これは、WS セキュリティ SOAP ヘッダーの一部としてユーザー名とパスワードを送信する標準的な方法です。 AEM Formsは、HTTP 基本認証もサポートしています。

Web サービスを使用してAEM Formsサービスを呼び出すには、通常、サービス WSDL を使用するプロキシライブラリを作成します。 この *Web サービスを使用したAEM Formsの呼び出し* セクションは、JAX-WS を使用して Java プロキシクラスを作成し、サービスを呼び出します。 ( [JAX-WS を使用した Java プロキシクラスの作成](#creating-java-proxy-classes-using-jax-ws).)

次の URL 定義を指定して、サービス WDSL を取得できます（角括弧で囲まれた項目はオプションです）。

```as3
 https://<your_serverhost>:<your_port>/soap/services/<service_name>?wsdl[&version=<version>][&async=true|false][lc_version=<lc_version>]
```

各パラメーターの意味は次のとおりです。

* *your_serverhost* は、AEM Formsをホストする J2EE アプリケーションサーバーの IP アドレスを表します。
* *your_port* は、J2EE アプリケーションサーバーが使用する HTTP ポートを表します。
* *service_name* は、サービス名を表します。
* *version* は、サービスの対象バージョンを表します（デフォルトでは最新のサービスバージョンが使用されます）。
* `async` 値を指定します `true` 非同期呼び出しの追加操作を有効にするには ( `false` （デフォルト）。
* *lc_version* は、呼び出すAEM Formsのバージョンを表します。

次の表に、サービスの WSDL 定義を示します (AEM Formsがローカルホストにデプロイされ、投稿が 8080 である場合 )。

<table> 
 <thead> 
  <tr> 
   <th><p>Service</p></th> 
   <th><p>WSDL 定義</p></th> 
  </tr> 
 </thead> 
 <tbody>
  <tr> 
   <td><p>Assembler</p></td> 
   <td><p><code>http://localhost:8080/soap/services/ AssemblerService?wsdl</code></p></td> 
  </tr> 
  <tr> 
   <td><p>戻る/復元</p></td> 
   <td><p><code>http://localhost:8080/soap/services/BackupService?wsdl</code></p></td> 
  </tr> 
  <tr> 
   <td><p>barcoded forms[barcoded forms]</p></td> 
   <td><p><code>http://localhost:8080/soap/services/ BarcodedFormsService?wsdl</code></p></td> 
  </tr> 
  <tr> 
   <td><p>Convert PDF</p></td> 
   <td><p><code>http://localhost:8080/soap/services/ ConvertPDFService?wsdl</code></p></td> 
  </tr> 
  <tr> 
   <td><p>Distiller</p></td> 
   <td><p><code>http://localhost:8080/soap/services/ DistillerService?wsdl</code></p></td> 
  </tr> 
  <tr> 
   <td><p>DocConverter </p></td> 
   <td><p><code>http://localhost:8080/soap/services/DocConverterService?WSDL</code></p></td> 
  </tr> 
  <tr> 
   <td><p>DocumentManagement</p></td> 
   <td><p><code>http://localhost:8080/soap/services/DocumentManagementService?WSDL</code></p></td> 
  </tr> 
  <tr> 
   <td><p>Encryption </p></td> 
   <td><p><code>http://localhost:8080/soap/services/EncryptionService?wsdl</code></p></td> 
  </tr> 
  <tr> 
   <td><p>Forms</p></td> 
   <td><p><code>http://localhost:8080/soap/services/FormsService?wsdl</code></p></td> 
  </tr> 
  <tr> 
   <td><p>Form Data Integration</p></td> 
   <td><p><code>http://localhost:8080/soap/services/FormDataIntegration?wsdl</code></p></td> 
  </tr> 
  <tr> 
   <td><p>Generate PDF</p></td> 
   <td><p><code>http://localhost:8080/soap/services/ GeneratePDFService?wsdl</code></p></td> 
  </tr> 
  <tr> 
   <td><p>Generate 3D PDF</p></td> 
   <td><p><code>http://localhost:8080/soap/services/Generate3dPDFService?WSDL</code></p></td> 
  </tr> 
  <tr> 
   <td><p>出力</p></td> 
   <td><p><code>http://localhost:8080/soap/services/ OutputService?wsdl</code></p></td> 
  </tr> 
  <tr> 
   <td><p>PDF Utilities </p></td> 
   <td><p><code>http://localhost:8080/soap/services/ PDFUtilityService?wsdl</code></p></td> 
  </tr> 
  <tr> 
   <td><p>Acrobat Reader DC エクステンション</p></td> 
   <td><p><code>http://localhost:8080/soap/services/ ReaderExtensionsService?wsdl</code></p></td> 
  </tr> 
  <tr> 
   <td><p>リポジトリ</p></td> 
   <td><p><code>http://localhost:8080/soap/services/ RepositoryService?wsdl</code></p></td> 
  </tr> 
  <tr> 
   <td><p>Rights Management </p></td> 
   <td><p><code>http://localhost:8080/soap/services/ RightsManagementService?wsdl</code></p></td> 
  </tr> 
  <tr> 
   <td><p>シグネチャ </p></td> 
   <td><p><code>http://localhost:8080/soap/services/ SignatureService?wsdl</code></p></td> 
  </tr> 
  <tr> 
   <td><p>XMP Utilities</p></td> 
   <td><p><code>http://localhost:8080/soap/services/ XMPUtilityService?wsdl</code></p></td> 
  </tr> 
 </tbody> 
</table>

**AEM Forms Process WSDL の定義**

Workbench で作成されたプロセスに属する WSDL にアクセスするには、WSDL 定義内でアプリケーション名とプロセス名を指定する必要があります。 アプリケーションの名前が `MyApplication` プロセスの名前は `EncryptDocument`. この場合は、次の WSDL 定義を指定します。

```as3
 http://localhost:8080/soap/services/MyApplication/EncryptDocument?wsdl
```

>[!NOTE]
>
>例について詳しくは、 `MyApplication/EncryptDocument` 短時間のみ有効なプロセス ( [短時間のみ有効なプロセスの例](/help/forms/developing/aem-forms-processes.md).

>[!NOTE]
>
>アプリケーションには、フォルダーを含めることができます。 この場合、WSDL 定義でフォルダー名を指定します。

```as3
 http://localhost:8080/soap/services/MyApplication/[<folderA>/.../<folderZ>/]EncryptDocument?wsdl
```

**Web サービスを使用した新しい機能へのアクセス**

新しいAEM Formsサービス機能には、Web サービスを使用してアクセスできます。 例えば、AEM Formsでは、MTOM を使用して添付ファイルをエンコードする機能が導入されました。 ( [MTOM を使用したAEM Formsの呼び出し](#invoking-aem-forms-using-mtom).)

AEM Formsで導入された新機能にアクセスするには、 `lc_version` 属性を設定します。 例えば、新しいサービス機能（MTOM のサポートを含む）にアクセスするには、次の WSDL 定義を指定します。

```as3
 http://localhost:8080/soap/services/MyApplication/EncryptDocument?wsdl&lc_version=9.0.1
```

>[!NOTE]
>
>設定時に `lc_version` 属性の場合は、必ず 3 桁の数字を使用します。 例えば、9.0.1 はバージョン 9.0 と等しくなります。

**Web サービス BLOB データ型**

AEM Formsサービス WSDL は、多くのデータ型を定義します。 Web サービスで公開される最も重要なデータ型の 1 つは、 `BLOB` タイプ。 このデータタイプは、 `com.adobe.idp.Document` クラスを使用して、AEM Forms Java API を操作する場合に使用します。 ( [Java API を使用してAEM Formsサービスにデータを渡す](/help/forms/developing/invoking-aem-forms-using-java.md#passing-data-to-aem-forms-services-using-the-java-api).)

A `BLOB` オブジェクトは、AEM Formsサービスとの間でバイナリデータ (PDFファイル、XML データなど ) を送受信します。 この `BLOB` type は、サービス WSDL で次のように定義されます。

```as3
 <complexType name="BLOB"> 
     <sequence> 
         <element maxOccurs="1" minOccurs="0" name="contentType" 
             type="xsd:string"/> 
         <element maxOccurs="1" minOccurs="0" name="binaryData" 
             type="xsd:base64Binary"/> 
         <element maxOccurs="1" minOccurs="0" name="attachmentID" 
             type="xsd:string"/> 
         <element maxOccurs="1" minOccurs="0" name="remoteURL" 
             type="xsd:string"/> 
         <element maxOccurs="1" minOccurs="0" name="MTOM"  
             type="xsd:base64Binary" 
             xmime:expectedContentTypes="*/*" 
             xmlns:xmime="https://www.w3.org/2005/05/xmlmime"/> 
         <element maxOccurs="1" minOccurs="0" name="swaRef"  
             type="tns1:swaRef"/> 
         <element maxOccurs="1" minOccurs="0" name="attributes" 
             type="impl:MyMapOf_xsd_string_To_xsd_anyType"/> 
     </sequence> 
 </complexType>
```

この `MTOM` および `swaRef` フィールドは、AEM Formsでのみサポートされます。 これらの新しいフィールドは、 `lc_version` プロパティ。

**サービスリクエストでの BLOB オブジェクトの指定**

AEM Formsサービス操作に `BLOB` 入力値としてを入力し、 `BLOB` アプリケーションロジックを入力します。 ( 多くの Web サービスのクイックスタートは、 *AEM forms によるプログラミング* BLOB データ型の操作方法を示します。)

値を `BLOB` インスタンスを次のように指定します。

* **Base64**:データを Base64 形式でエンコードされたテキストとして渡すには、 `BLOB.binaryData` フィールドに値を入力し、MIME 形式でデータタイプを設定します ( 例： `application/pdf`) を `BLOB.contentType` フィールドに入力します。 ( [Base64 エンコーディングを使用したAEM Formsの呼び出し](#invoking-aem-forms-using-base64-encoding).)
* **MTOM**:MTOM 添付ファイルにバイナリデータを渡すには、 `BLOB.MTOM` フィールドに入力します。 この設定は、Java JAX-WS フレームワークまたは SOAP フレームワークのネイティブ API を使用して、SOAP リクエストにデータを添付します。 ( [MTOM を使用したAEM Formsの呼び出し](#invoking-aem-forms-using-mtom).)
* **SwaRef**:WS-I SwaRef 添付ファイルにバイナリデータを渡すには、 `BLOB.swaRef` フィールドに入力します。 この設定は、Java JAX-WS フレームワークを使用して SOAP リクエストにデータを添付します。 ( [SwaRef を使用したAEM Formsの呼び出し](#invoking-aem-forms-using-swaref).)
* **MIME または DIME 添付ファイル**:MIME または DIME 添付ファイルにデータを渡すには、SOAP フレームワークのネイティブ API を使用して、SOAP リクエストにデータを添付します。 添付ファイル識別子を `BLOB.attachmentID` フィールドに入力します。 ( [Base64 エンコーディングを使用したAEM Formsの呼び出し](#invoking-aem-forms-using-base64-encoding).)
* **リモート URL**:データが Web サーバーでホストされ、HTTP URL 経由でアクセス可能な場合は、 `BLOB.remoteURL` フィールドに入力します。 ( [HTTP 経由での BLOB データを使用したAEM Formsの呼び出し](#invoking-aem-forms-using-blob-data-over-http).)

**サービスから返された BLOB オブジェクト内のデータへのアクセス**

返されるの送信プロトコル `BLOB` オブジェクトは、いくつかの要因に依存します。次の順序で考慮されます。主な条件が満たされた場合に停止します。

1. **ターゲット URL は送信プロトコルを指定します**. SOAP 呼び出しで指定されたターゲット URL に `blob="`*BLOB_TYPE*「では *BLOB_TYPE* 送信プロトコルを決定します。 *BLOB_TYPE* は、base64、dime、mime、http、mtom または swaref のプレースホルダーです。
1. **サービス SOAP エンドポイントがスマートです**. 次の条件が true の場合、出力ドキュメントは入力ドキュメントと同じ送信プロトコルを使用して返されます。

   * サービスの SOAP エンドポイントパラメータ出力 BLOB オブジェクトのデフォルトプロトコルが「スマート」に設定されています。

      SOAP エンドポイントを持つ各サービスについて、管理コンソールを使用して、返された BLOB の送信プロトコルを指定できます。 ( [管理ヘルプ](https://www.adobe.com/go/learn_aemforms_admin_63).)

   * AEM Formsサービスは、1 つ以上のドキュメントを入力として取得します。

1. **サービス SOAP エンドポイントがスマートではありません**. 設定されたプロトコルがドキュメント送信プロトコルを決定し、データは対応する `BLOB` フィールドに入力します。 例えば、SOAP エンドポイントが DIME に設定されている場合、返される BLOB は `blob.attachmentID` フィールドに関係なく、入力ドキュメントの送信プロトコルに関係なく、
1. **それ以外の場合**. サービスがドキュメントタイプを入力として取らない場合、出力ドキュメントは `BLOB.remoteURL` HTTP プロトコルのフィールド。

最初の条件で説明したように、次のようなサフィックスを付けて SOAP エンドポイント URL を拡張することで、返されるドキュメントの送信タイプを確認できます。

```as3
     https://<your_serverhost>:<your_port>/soap/services/<service 
     name>?blob=base64|dime|mime|http|mtom|swaref
```

次に、送信タイプとデータの取得元のフィールドとの相関関係を示します。

* **Base64 形式**:を `blob` サフィックス `base64` データを `BLOB.binaryData` フィールドに入力します。
* **MIME または DIME 添付ファイル**:を `blob` サフィックス `DIME` または `MIME` データを対応する添付ファイルタイプとして返し、添付ファイルの識別子を `BLOB.attachmentID` フィールドに入力します。 SOAP フレームワーク独自の API を使用して、添付ファイルからデータを読み取ります。
* **リモート URL**:を `blob` サフィックス `http` アプリケーションサーバー上のデータを保持し、 `BLOB.remoteURL` フィールドに入力します。
* **MTOM または SwaRef**:を `blob` サフィックス `mtom` または `swaref` データを対応する添付ファイルタイプとして返し、添付ファイルの識別子を `BLOB.MTOM` または `BLOB.swaRef` フィールド。 SOAP フレームワークのネイティブ API を使用して、添付ファイルからデータを読み取ります。

>[!NOTE]
>
>を `BLOB` オブジェクトを呼び出す `setBinaryData` メソッド。 そうでない場合、 `OutOfMemory`*例外が発生しました。*

>[!NOTE]
>
>MTOM 送信プロトコルを使用する JAX WS ベースのアプリケーションは、送受信データが 25 MB に制限されています。 この制限は、JAX-WS のバグが原因です。 送受信ファイルの合計サイズが 25 MB を超える場合は、MTOM の代わりに SwaRef 送信プロトコルを使用します。 そうでない場合、 `OutOfMemory`* exception.*

**base64 でエンコードされたバイト配列の MTOM 送信**

また、 `BLOB` オブジェクトの場合、MTOM プロトコルは、任意の byte-array パラメータまたは byte-array フィールドを複合型でサポートします。 つまり、MTOM をサポートするクライアント SOAP フレームワークは、 `xsd:base64Binary` 要素を MTOM 添付ファイル（base64 エンコードされたテキストではなく）として使用する。 AEM Forms SOAP エンドポイントは、この種のバイト配列エンコーディングを読み取ることができます。 ただし、AEM Formsサービスは常に、base64 エンコードされたテキストとしてバイト配列型を返します。 出力バイト配列パラメータは MTOM をサポートしていません。

大量のバイナリデータを返すAEM Formsサービスでは、バイト配列型ではなく Document/BLOB 型を使用します。 ドキュメントタイプは、大量のデータを送信する場合に、より効率的です。

## Web サービスのデータ型 {#web-service-data-types}

次の表に、Java データ型と、対応する Web サービスデータ型を示します。

<table> 
 <thead> 
  <tr> 
   <th><p>Java データタイプ</p></th> 
   <th><p>Web サービスのデータタイプ</p></th> 
  </tr> 
 </thead> 
 <tbody>
  <tr> 
   <td><p><code>java.lang.byte[]</code></p></td> 
   <td><p><code>xsd:base64Binary</code></p></td> 
  </tr> 
  <tr> 
   <td><p><code>java.lang.Boolean</code></p></td> 
   <td><p><code>xsd:boolean</code></p></td> 
  </tr> 
  <tr> 
   <td><p><code>java.util.Date</code></p></td> 
   <td><p>この <code>DATE</code> サービス WSDL で次のように定義された型</p><p><code>&lt;complexType name="DATE"&gt;</code></p><p><code>&lt;sequence&gt;</code></p><p><code>&lt;element maxOccurs="1" minOccurs="0" name="date" </code><code>type="xsd:dateTime" /&gt; </code></p><p><code>&lt;element maxOccurs="1" minOccurs="0" name="calendar" </code><code>type="xsd:dateTime" /&gt; </code></p><p><code>&lt;/sequence&gt;</code></p><p><code>&lt;/complexType&gt;</code></p><p>AEM Formsのサービス操作で <code>java.util.Date</code> 値を入力として指定する場合、SOAP クライアントアプリケーションは <code>DATE.date</code> フィールドに入力します。 の設定 <code>DATE.calendar</code> この場合、フィールドによって実行時例外が発生します。 サービスが <code>java.util.Date</code>の場合、日付は <code>DATE.date</code> フィールドに入力します。</p></td> 
  </tr> 
  <tr> 
   <td><p><code>java.util.Calendar</code></p></td> 
   <td><p>この <code>DATE</code> サービス WSDL で次のように定義された型</p><p><code>&lt;complexType name="DATE"&gt;</code></p><p><code>&lt;sequence&gt;</code></p><p><code>&lt;element maxOccurs="1" minOccurs="0" name="date" </code><code>type="xsd:dateTime" /&gt; </code></p><p><code>&lt;element maxOccurs="1" minOccurs="0" name="calendar" </code><code>type="xsd:dateTime" /&gt; </code></p><p><code>&lt;/sequence&gt;</code></p><p><code>&lt;/complexType&gt;</code></p><p>AEM Formsのサービス操作で <code>java.util.Calendar</code> 値を入力として指定する場合、SOAP クライアントアプリケーションは <code>DATE.caledendar</code> フィールドに入力します。 の設定 <code>DATE.date</code> この場合、フィールドは実行時例外を引き起こします。 サービスが <code>java.util.Calendar</code>の場合、日付が <code>DATE.calendar</code> フィールドに入力します。 </p></td> 
  </tr> 
  <tr> 
   <td><p><code>java.math.BigDecimal</code></p></td> 
   <td><p><code>xsd:decimal</code></p></td> 
  </tr> 
  <tr> 
   <td><p><code>com.adobe.idp.Document</code></p></td> 
   <td><p><code>BLOB</code></p></td> 
  </tr> 
  <tr> 
   <td><p><code>java.lang.Double</code></p></td> 
   <td><p><code>xsd:double</code></p></td> 
  </tr> 
  <tr> 
   <td><p><code>java.lang.Float</code></p></td> 
   <td><p><code>xsd:float</code></p></td> 
  </tr> 
  <tr> 
   <td><p><code>java.lang.Integer</code></p></td> 
   <td><p><code>xsd:int</code></p></td> 
  </tr> 
  <tr> 
   <td><p><code>java.util.List</code></p></td> 
   <td><p><code>MyArrayOf_xsd_anyType</code></p></td> 
  </tr> 
  <tr> 
   <td><p><code>java.lang.Long</code></p></td> 
   <td><p><code>xsd:long</code></p></td> 
  </tr> 
  <tr> 
   <td><p><code>java.util.Map</code></p></td> 
   <td><p>この <code>apachesoap:Map</code>：サービス WSDL で次のように定義されます。</p><p><code>&lt;schema elementFormDefault="qualified" targetNamespace="https://xml.apache.org/xml-soap" xmlns="https://www.w3.org/2001/XMLSchema"&gt;</code></p><p><code>&lt;complexType name="mapItem"&gt;</code></p><p><code>&lt;sequence&gt;</code></p><p><code>&lt;element name="key" nillable="true" type="xsd:anyType"/&gt;</code></p><p><code>&lt;element name="value" nillable="true" type="xsd:anyType"/&gt;</code></p><p><code>&lt;/sequence&gt;</code></p><p><code>&lt;/complexType&gt;</code></p><p><code>&lt;complexType name="Map"&gt;</code></p><p><code>&lt;sequence&gt;</code></p><p><code>&lt;element maxOccurs="unbounded" minOccurs="0" name="item" </code><code>type="apachesoap:mapItem"/&gt;</code></p><p><code>&lt;/sequence&gt;</code></p><p><code>&lt;/complexType&gt;</code></p><p><code>&lt;/schema&gt;</code></p><p>マップは、キーと値のペアのシーケンスとして表されます。</p></td> 
  </tr> 
  <tr> 
   <td><p><code>java.lang.Object</code></p></td> 
   <td><p><code>$1</code></p></td> 
  </tr> 
  <tr> 
   <td><p><code>java.lang.Short</code></p></td> 
   <td><p><code>xsd:short</code></p></td> 
  </tr> 
  <tr> 
   <td><p><code>java.lang.String</code></p></td> 
   <td><p><code>xsd:string</code></p></td> 
  </tr> 
  <tr> 
   <td><p><code>org.w3c.dom.Document</code></p></td> 
   <td><p>サービス WSDL で次のように定義される XML 型です。</p><p><code>&lt;complexType name="XML"&gt;</code></p><p><code>&lt;sequence&gt;</code></p><p><code>&lt;element maxOccurs="1" minOccurs="0" name="document" </code><code>type="xsd:string" /&gt; </code></p><p><code>&lt;element maxOccurs="1" minOccurs="0" name="element" </code><code>type="xsd:string" /&gt; </code></p><p><code>&lt;/sequence&gt;</code></p><p><code>&lt;/complexType&gt;</code></p><p>AEM Formsサービス操作が <code>org.w3c.dom.Document</code> の値を指定し、XML データを <code>XML.document</code> フィールドに入力します。</p><p>の設定 <code>XML.element</code> フィールドを指定すると、実行時例外が発生します。 サービスが <code>org.w3c.dom.Document</code>を指定した場合、XML データが <code>XML.document</code> フィールドに入力します。</p></td> 
  </tr> 
  <tr> 
   <td><p><code>org.w3c.dom.Element</code></p></td> 
   <td><p>サービス WSDL で次のように定義される XML 型です。</p><p><code>&lt;complexType name="XML"&gt;</code></p><p><code>&lt;sequence&gt;</code></p><p><code>&lt;element maxOccurs="1" minOccurs="0" name="document" </code><code>type="xsd:string" /&gt; </code></p><p><code>&lt;element maxOccurs="1" minOccurs="0" name="element" </code><code>type="xsd:string" /&gt; </code></p><p><code>&lt;/sequence&gt;</code></p><p><code>&lt;/complexType&gt;</code></p><p>AEM Formsのサービス操作が <code>org.w3c.dom.Element</code> XML データを <code>XML.element</code> フィールドに入力します。</p><p>の設定 <code>XML.document</code> フィールドを指定すると、実行時例外が発生します。 サービスが <code>org.w3c.dom.Element</code>に値を指定しない場合、XML データは <code>XML.element</code> フィールドに入力します。</p></td> 
  </tr> 
 </tbody> 
</table>

>[!NOTE]
>
>カスタムコンポーネントを使用した Web サービスの呼び出しでは、サードパーティの Web サービスを呼び出すAEM Formsコンポーネントを作成する方法について説明します。

## JAX-WS を使用した Java プロキシクラスの作成 {#creating-java-proxy-classes-using-jax-ws}

JAX-WS を使用して、Forms Service WSDL を Java プロキシクラスに変換できます。 これらのクラスを使用して、AEM Formsサービス操作を呼び出すことができます。 Apache Ant では、AEM Forms Service WSDL を参照して Java プロキシクラスを生成するビルドスクリプトを作成できます。 次の手順を実行して、JAX-WS プロキシファイルを生成できます。

1. クライアントコンピューターに Apache Ant をインストールします。 ( [https://ant.apache.org/bindownload.cgi](https://ant.apache.org/bindownload.cgi).)

   * bin ディレクトリをクラスパスに追加します。
   * を `ANT_HOME` 環境変数を、Ant をインストールしたディレクトリに設定します。

1. JDK 1.6 以降をインストールします。

   * JDK bin ディレクトリをクラスパスに追加します。
   * JRE bin ディレクトリをクラスパスに追加します。 この bin は、 [*JDK_INSTALL_LOCATION*]/jre ディレクトリ。
   * を `JAVA_HOME` 環境変数を、JDK をインストールしたディレクトリに設定します。

   JDK 1.6 には、build.xml ファイルで使用される wsimport プログラムが含まれています。 JDK 1.5 には、このプログラムは含まれていません。

1. JAX-WS をクライアントコンピューターにインストールします。 ( [XML Web サービス用 Java API](https://jax-ws.dev.java.net/jax-ws-ea3/docs/mtom-swaref.html).)
1. JAX-WS と Apache Ant を使用して Java プロキシクラスを生成します。 このタスクを実行する Ant ビルドスクリプトを作成します。 次のスクリプトは、build.xml という名前の Ant ビルドスクリプトのサンプルです。

   ```as3
    <?xml version="1.0" encoding="UTF-8"?> 
     
    <project basedir="." default="compile"> 
     
    <property name="port" value="8080" /> 
    <property name="host" value="localhost" /> 
    <property name="username" value="administrator" /> 
    <property name="password" value="password" /> 
    <property name="tests" value="all" /> 
     
    <target name="clean" > 
           <delete dir="classes" /> 
    </target> 
     
    <target name="wsdl" depends="clean"> 
           <mkdir dir="classes"/> 
           <exec executable="wsimport" failifexecutionfails="false" failonerror="true" resultproperty="foundWSIMPORT"> 
               <arg line="-keep -d classes https://${host}:${port}/soap/services/EncryptionService?wsdl&lc_version=9.0.1"/> 
           </exec> 
           <fail unless="foundWSIMPORT"> 
              !!! Failed to execute JDK's wsimport tool. Make sure that JDK 1.6 (or later) is on your PATH !!! 
           </fail> 
    </target> 
     
    <target name="compile" depends="clean, wsdl" > 
         <javac destdir="./classes" fork="true" debug="true"> 
            <src path="./src"/> 
         </javac> 
    </target> 
     
    <target name="run"> 
         <java classname="Client" fork="yes" failonerror="true" maxmemory="200M"> 
            <classpath> 
              <pathelement location="./classes"/> 
            </classpath> 
            <arg value="${port}"/> 
            <arg value="${host}"/> 
            <arg value="${username}"/> 
            <arg value="${password}"/> 
            <arg value="${tests}"/> 
         </java> 
    </target> 
    </project>
   ```

   この Ant ビルドスクリプト内で、 `url` プロパティは、localhost で実行されている Encryption サービス WSDL を参照するように設定されます。 この `username` および `password` プロパティは、有効なAEM forms のユーザー名とパスワードに設定する必要があります。 URL には `lc_version` 属性。 指定しない `lc_version` 」オプションを使用する場合、新しいAEM Formsサービス操作を呼び出すことはできません。

   >[!NOTE]
   >
   >置換 `EncryptionService`* Java プロキシクラスを使用して呼び出すAEM Formsサービス名 例えば、プロキシサービスの JavaRights Managementクラスを作成するには、次のように指定します。*

   ```as3
    http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1
   ```

1. BAT ファイルを作成して、Ant ビルドスクリプトを実行します。 次のコマンドは、Ant ビルドスクリプトの実行を担当する BAT ファイル内に配置できます。

   ```as3
    ant -buildfile "build.xml" wsdl
   ```

   ANT ビルドスクリプトをC:\Program Files\Java\jaxws-ri\bin directoryフォルダに配置します。 スクリプトは JAVA ファイルをに書き込みます。/classes フォルダー このスクリプトは、サービスを呼び出すことのできる JAVA ファイルを生成します。

1. JAVA ファイルを JAR ファイルにパッケージ化します。 Eclipse を使用する場合は、次の手順に従います。

   * プロキシ JAVA ファイルを JAR ファイルにパッケージ化するために使用する新しい Java プロジェクトを作成します。
   * プロジェクトにソースフォルダーを作成します。
   * の作成 `com.adobe.idp.services` パッケージをソースフォルダーに保存します。
   * を選択します。 `com.adobe.idp.services` パッケージ化してから、JAVA ファイルを adobe/idp/services フォルダーからパッケージにインポートします。
   * 必要に応じて、 `org/apache/xml/xmlsoap` パッケージをソースフォルダーに保存します。
   * ソースフォルダーを選択し、 org/apache/xml/xmlsoap フォルダーから JAVA ファイルを読み込みます。
   * Java コンパイラのコンプライアンスレベルを 5.0 以上に設定します。
   * プロジェクトを構築します。
   * プロジェクトを JAR ファイルとして書き出します。
   * この JAR ファイルをクライアントプロジェクトのクラスパスにインポートします。 さらに、にあるすべての JAR ファイルをインポートします。 &lt;install directory=&quot;&quot;>\Adobe\Adobe_Experience_Manager_forms\sdk\client-libs\thirdparty.

   >[!NOTE]
   >
   >「 AEM forms によるプログラミング」にあるすべての Java Web サービスのクイックスタート (Formsサービスを除く ) は、JAX-WS を使用して Java プロキシファイルを作成します。 また、すべての Java Web サービスのクイックスタートには、SwaRef を使用します。 ( [SwaRef を使用したAEM Formsの呼び出し](#invoking-aem-forms-using-swaref).)

**関連トピック**

[Apache Axis を使用した Java プロキシクラスの作成](#creating-java-proxy-classes-using-apache-axis)

[Base64 エンコーディングを使用したAEM Formsの呼び出し](#invoking-aem-forms-using-base64-encoding)

[HTTP 経由での BLOB データを使用したAEM Formsの呼び出し](#invoking-aem-forms-using-blob-data-over-http)

[SwaRef を使用したAEM Formsの呼び出し](#invoking-aem-forms-using-swaref)

## Apache Axis を使用した Java プロキシクラスの作成 {#creating-java-proxy-classes-using-apache-axis}

Apache Axis WSDL2Java ツールを使用して、Formsサービスを Java プロキシクラスに変換できます。 これらのクラスを使用して、Formsサービス操作を呼び出すことができます。 Apache Ant を使用して、サービス WSDL から Axis ライブラリファイルを生成できます。 Apache Axis は URL でダウンロードできます [https://ws.apache.org/axis/](https://ws.apache.org/axis/).

>[!NOTE]
>
>Formsサービスに関連付けられた Web サービスのクイックスタートでは、Apache Axis を使用して作成された Java プロキシクラスを使用します。 Forms Web サービスのクイックスタートでは、エンコーディングの種類として Base64 も使用します。 ( [Forms Service API クイックスタート](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts).)

次の手順を実行して、Axis Java ライブラリファイルを生成できます。

1. クライアントコンピューターに Apache Ant をインストールします。 次の場所で利用できます。 [https://ant.apache.org/bindownload.cgi](https://ant.apache.org/bindownload.cgi).

   * bin ディレクトリをクラスパスに追加します。
   * を `ANT_HOME` 環境変数を、Ant をインストールしたディレクトリに設定します。

1. Apache Axis 1.4 をクライアントコンピューターにインストールします。 次の場所で利用できます。 [https://ws.apache.org/axis/](https://ws.apache.org/axis/).
1. Web サービスクライアントで Axis JAR ファイルを使用するクラスパスを設定します。詳しくは、 [https://ws.apache.org/axis/java/install.html](https://ws.apache.org/axis/java/install.html).
1. Axis の Apache WSDL2Java ツールを使用して、Java プロキシクラスを生成します。 このタスクを実行する Ant ビルドスクリプトを作成します。 次のスクリプトは、build.xml という名前の Ant ビルドスクリプトのサンプルです。

   ```as3
    <?xml version="1.0"?> 
    <project name="axis-wsdl2java"> 
     
    <path id="axis.classpath"> 
    <fileset dir="C:\axis-1_4\lib" > 
        <include name="**/*.jar" /> 
    </fileset> 
    </path> 
     
    <taskdef resource="axis-tasks.properties" classpathref="axis.classpath" /> 
     
    <target name="encryption-wsdl2java-client" description="task"> 
    <axis-wsdl2java 
        output="C:\JavaFiles" 
        testcase="false" 
        serverside="false" 
        verbose="true" 
        username="administrator" 
        password="password" 
        url="http://localhost:8080/soap/services/EncryptionService?wsdl&lc_version=9.0.1" > 
    </axis-wsdl2java> 
    </target> 
     
    </project>
   ```

   この Ant ビルドスクリプト内で、 `url` プロパティは、localhost で実行されている Encryption サービス WSDL を参照するように設定されます。 この `username` および `password` プロパティは、有効なAEM forms のユーザー名とパスワードに設定する必要があります。

1. BAT ファイルを作成して、Ant ビルドスクリプトを実行します。 次のコマンドは、Ant ビルドスクリプトの実行を担当する BAT ファイル内に配置できます。

   ```as3
    ant -buildfile "build.xml" encryption-wsdl2java-client
   ```

   JAVA ファイルは、C:\JavaFiles folder as specified by the `output` プロパティ。 Formsサービスを正常に呼び出すには、次の JAVA ファイルをクラスパスに読み込みます。

   デフォルトでは、これらのファイルは、 `com.adobe.idp.services`. これらの JAVA ファイルは、JAR ファイルに配置することをお勧めします。 次に、JAR ファイルをクライアントアプリケーションのクラスパスにインポートします。

   >[!NOTE]
   >
   >.JAVA ファイルを JAR に配置する方法は異なります。 1 つの方法は、Eclipse のような Java IDE を使用する方法です。 Java プロジェクトの作成と `com.adobe.idp.services`*パッケージ（すべての.JAVA ファイルはこのパッケージに属しています） 次に、すべての.JAVA ファイルをパッケージにインポートします。 最後に、プロジェクトを JAR ファイルとしてエクスポートします。*

1. URL を `EncryptionServiceLocator` クラスを使用してエンコーディングタイプを指定します。 例えば、base64 を使用するには、次のように指定します。 `?blob=base64` 確実に `BLOB` オブジェクトはバイナリデータを返します。 つまり、 `EncryptionServiceLocator` クラスで、次のコード行を探します。

   ```as3
    http://localhost:8080/soap/services/EncryptionService;
   ```

   次のように変更します。

   ```as3
    http://localhost:8080/soap/services/EncryptionService?blob=base64;
   ```

1. 次の Axis JAR ファイルを Java プロジェクトのクラスパスに追加します。

   * activation.jar
   * axis.jar
   * commons-codec-1.3.jar
   * commons-collections-3.1.jar
   * commons-discovery.jar
   * commons-logging.jar
   * dom3-xml-apis-2.5.0.jar
   * jai_imageio.jar
   * jaxen-1.1-beta-9.jar
   * jaxrpc.jar
   * log4j.jar
   * mail.jar
   * saaj.jar
   * wsdl4j.jar
   * xalan.jar
   * xbean.jar
   * xercesImpl.jar

   これらの JAR ファイルは、 *[インストールディレクトリ]*/Adobe/Adobe Experience Manager Forms/sdk/lib/thirdparty ディレクトリ

**関連トピック**

[JAX-WS を使用した Java プロキシクラスの作成](#creating-java-proxy-classes-using-jax-ws)

[Base64 エンコーディングを使用したAEM Formsの呼び出し](#invoking-aem-forms-using-base64-encoding)

[HTTP 経由での BLOB データを使用したAEM Formsの呼び出し](#invoking-aem-forms-using-blob-data-over-http)

## Base64 エンコーディングを使用したAEM Formsの呼び出し {#invoking-aem-forms-using-base64-encoding}

Base64 エンコーディングを使用してAEM Formsサービスを呼び出すことができます。 Base64 エンコードは、Web サービスの呼び出し要求で送信される添付ファイルをエンコードします。 つまり `BLOB` データは Base64 でエンコードされ、SOAP メッセージ全体ではありません。

「Base64 エンコーディングを使用したAEM Formsの呼び出し」では、次のAEM Formsの短時間のみ有効なプロセス ( `MyApplication/EncryptDocument` Base64 エンコーディングを使用します。

>[!NOTE]
>
>このプロセスは、既存の AEM Forms プロセスに基づいていません。このコードの例の流れを追うには、Workbench を使用して `MyApplication/EncryptDocument` という名前のプロセスを作成します。（[Workbench の使用](https://www.adobe.com/go/learn_aemforms_workbench_63)を参照。）

このプロセスを呼び出すと、次のアクションが実行されます。

1. プロセスに渡された保護されていない PDF ドキュメントを取得します。このアクションは `SetValue` 操作に基づいています。このプロセスの入力パラメーターは、`document` という名前の `inDoc` プロセス変数です。
1. PDF ドキュメントをパスワードで暗号化します。このアクションは `PasswordEncryptPDF` 操作に基づいています。パスワードで暗号化された PDF ドキュメントは、`outDoc` という名前のプロセス変数として返されます。

### Base64 エンコーディングを使用する.NET クライアントアセンブリの作成 {#creating-a-net-client-assembly-that-uses-base64-encoding}

.NET クライアントアセンブリを作成して、Microsoft Visual Studio .NET プロジェクトからFormsサービスを呼び出すことができます。 base64 エンコーディングを使用する.NET クライアントアセンブリを作成するには、次の手順を実行します。

1. AEM Forms呼び出し URL に基づいてプロキシクラスを作成します。
1. .NET クライアントアセンブリを生成するMicrosoft Visual Studio .NET プロジェクトを作成します。

**プロキシクラスの作成**

Microsoft Visual Studio に付属するツールを使用して、.NET クライアントアセンブリの作成に使用するプロキシクラスを作成できます。 このツールの名前は wsdl.exe で、Microsoft Visual Studio のインストールフォルダーにあります。 プロキシクラスを作成するには、コマンドプロンプトを開き、wsdl.exe ファイルを含むフォルダーに移動します。 wsdl.exe ツールの詳細については、 *MSDN ヘルプ*.

コマンドプロンプトで次のコマンドを入力します。

```as3
 wsdl https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?WSDL&lc_version=9.0.1
```

デフォルトでは、このツールは WSDL の名前に基づくのと同じフォルダに CS ファイルを作成します。 この場合、という名前の CS ファイルが作成されます。 *EncryptDocumentService.cs*. この CS ファイルを使用してプロキシオブジェクトを作成し、呼び出し URL で指定されたサービスを呼び出すことができます。

プロキシクラスの URL を修正して、 `?blob=base64` 確実に `BLOB` オブジェクトはバイナリデータを返します。 プロキシクラスで、次のコード行を探します。

```as3
 "https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument";
```

次のように変更します。

```as3
 "https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=base64";
```

この *Base64 エンコーディングを使用したAEM Formsの呼び出し* セクションを使用 `MyApplication/EncryptDocument` を例として示します。 別のFormsサービス用に.NET クライアントアセンブリを作成する場合は、 `MyApplication/EncryptDocument` をサービスの名前に置き換えます。

**.NET クライアントアセンブリの開発**

.NET クライアントアセンブリを生成する Visual Studio クラスライブラリプロジェクトを作成します。 wsdl.exe を使用して作成した CS ファイルを、このプロジェクトに読み込むことができます。 このプロジェクトは、DLL ファイル（.NET クライアントアセンブリ）を生成し、他の Visual Studio .NET プロジェクトで使用してサービスを呼び出すことができます。

1. Microsoft Visual Studio .NET を起動します。
1. クラスライブラリプロジェクトを作成し、DocumentService という名前を付けます。
1. wsdl.exe を使用して作成した CS ファイルを読み込みます。
1. 内 **プロジェクト** メニュー、選択 **参照を追加**.
1. [ 参照を追加 ] ダイアログボックスで、 **System.Web.Services.dll**.
1. クリック **選択** 次に、 **OK**.
1. プロジェクトをコンパイルしてビルドします。

>[!NOTE]
>
>この手順では、DocumentService.dll という名前の.NET クライアントアセンブリが作成され、SOAP 要求をに送信する際に使用できます。 `MyApplication/EncryptDocument` サービス。

>[!NOTE]
>
>次を追加したことを確認します。 `?blob=base64` を.NET クライアントアセンブリの作成に使用されるプロキシクラスの URL に追加します。 そうしないと、 `BLOB` オブジェクト。

**.NET クライアントアセンブリの参照**

新しく作成した.NET クライアントアセンブリを、クライアントアプリケーションを開発するコンピューターに配置します。 .NET クライアントアセンブリをディレクトリに配置した後、プロジェクトから参照できます。 また、 `System.Web.Services` ライブラリをプロジェクトから削除します。 このライブラリを参照しない場合、.NET クライアントアセンブリを使用してサービスを呼び出すことはできません。

1. 内 **プロジェクト** メニュー、選択 **参照を追加**.
1. 次をクリック： **.NET** タブをクリックします。
1. クリック **参照** DocumentService.dll ファイルを探します。
1. クリック **選択** 次に、 **OK**.

**Base64 エンコーディングを使用する.NET クライアントアセンブリを使用したサービスの呼び出し**

を呼び出すことができます。 `MyApplication/EncryptDocument` （Workbench で構築された）サービス（Base64 エンコーディングを使用する.NET クライアントアセンブリを使用）。 を呼び出すには、以下を実行します。 `MyApplication/EncryptDocument` サービスで、次の手順を実行します。

1. を使用するMicrosoft .NET クライアントアセンブリを作成します。 `MyApplication/EncryptDocument` サービス WSDL。
1. クライアントMicrosoft .NET プロジェクトを作成します。 クライアントプロジェクトでMicrosoft .NET クライアントアセンブリを参照します。 参照 `System.Web.Services`.
1. Microsoft .NET クライアントアセンブリを使用して、 `MyApplication_EncryptDocumentService` オブジェクトのデフォルトのコンストラクターを呼び出す。
1. を `MyApplication_EncryptDocumentService` オブジェクトの `Credentials` プロパティに `System.Net.NetworkCredential` オブジェクト。 内 `System.Net.NetworkCredential` コンストラクタ。AEM forms ユーザー名と対応するパスワードを指定します。 認証値を設定して、.NET クライアントアプリケーションがAEM Formsと SOAP メッセージを正常に交換できるようにします。
1. コンストラクタを使用して `BLOB` オブジェクトを作成します。この `BLOB` オブジェクトは、 `MyApplication/EncryptDocument` プロセス。
1. の作成 `System.IO.FileStream` オブジェクトを指定します。 PDFドキュメントのファイルの場所と、ファイルを開くモードを表す string 値を渡します。
1. コンテンツを格納するバイト配列を作成します。 `System.IO.FileStream` オブジェクト。 バイト配列のサイズは、 `System.IO.FileStream` オブジェクトの `Length` プロパティ。
1. を呼び出して、バイト配列にストリームデータを入力します。 `System.IO.FileStream` オブジェクトの `Read` メソッド。 読み取るバイト配列、開始位置、ストリーム長を渡します。
1. 次の項目に `BLOB` オブジェクトを割り当てる `binaryData` プロパティにバイト配列の内容を入力します。
1. を呼び出す `MyApplication/EncryptDocument` を呼び出して処理 `MyApplication_EncryptDocumentService` オブジェクトの `invoke` メソッドおよび `BLOB` オブジェクトドキュメントを含むPDF。 このプロセスは、暗号化されたPDFドキュメントを `BLOB` オブジェクト。
1. の作成 `System.IO.FileStream` オブジェクトを指定します。
1. のデータコンテンツを格納するバイト配列を作成します。 `BLOB` が返すオブジェクト `MyApplicationEncryptDocumentService` オブジェクトの `invoke` メソッド。 バイト配列を生成するには、 `BLOB` オブジェクトの `binaryData` データメンバー。
1. の作成 `System.IO.BinaryWriter` オブジェクトのコンストラクタを呼び出し、 `System.IO.FileStream` オブジェクト。
1. を呼び出して、バイト配列の内容をPDFファイルに書き込みます。 `System.IO.BinaryWriter` オブジェクトの `Write` メソッドを使用してバイト配列を渡す。

### Java プロキシクラスと Base64 エンコーディングを使用したサービスの呼び出し {#invoking-a-service-using-java-proxy-classes-and-base64-encoding}

Java プロキシクラスと Base64 を使用して、AEM Formsサービスを呼び出すことができます。 を呼び出すには、以下を実行します。 `MyApplication/EncryptDocument` Java プロキシクラスを使用するサービスで、次の手順を実行します。

1. JAX-WS を使用して、 `MyApplication/EncryptDocument` サービス WSDL。 次の WSDL エンドポイントを使用します。

   `https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?WSDL&lc_version=9.0.1`

   >[!NOTE]
   >
   >置換 `hiro-xp`* AEM Formsをホストする J2EE アプリケーションサービスの IP アドレス*

1. JAX-WS を使用して作成した Java プロキシクラスを JAR ファイルにパッケージ化します。
1. 次のパスにある Java プロキシ JAR ファイルと JAR ファイルを含めます。

   &lt;install directory=&quot;&quot;>\Adobe\Adobe_Experience_Manager_forms\sdk\client-libs\thirdparty

   を Java クライアントプロジェクトのクラスパスに追加します。

1. コンストラクタを使用して `MyApplicationEncryptDocumentService` オブジェクトを作成します。
1. の作成 `MyApplicationEncryptDocument` を呼び出すことによってオブジェクトを取得 `MyApplicationEncryptDocumentService` オブジェクトの `getEncryptDocument` メソッド。
1. 次のデータメンバーに値を割り当てて、AEM Formsを呼び出すのに必要な接続値を設定します。

   * WSDL エンドポイントとエンコーディングの種類を `javax.xml.ws.BindingProvider` オブジェクトの `ENDPOINT_ADDRESS_PROPERTY` フィールドに入力します。 を呼び出すには、以下を実行します。 `MyApplication/EncryptDocument` Base64 エンコーディングを使用するサービスで、次の URL 値を指定します。

      `https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=base64`

   * AEM forms ユーザーを `javax.xml.ws.BindingProvider` オブジェクトの `USERNAME_PROPERTY` フィールドに入力します。
   * 対応するパスワード値を `javax.xml.ws.BindingProvider` オブジェクトの `PASSWORD_PROPERTY` フィールドに入力します。

   次のコード例に、このアプリケーションロジックを示します。

   ```as3
    //Set connection values required to invoke AEM Forms 
    String url = "https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=base64"; 
    String username = "administrator"; 
    String password = "password"; 
    ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.ENDPOINT_ADDRESS_PROPERTY, url); 
    ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.USERNAME_PROPERTY, username); 
    ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.PASSWORD_PROPERTY, password);
   ```

1. に送信するPDFドキュメントを取得します `MyApplication/EncryptDocument` プロセス（作成による） `java.io.FileInputStream` オブジェクトを指定します。 PDFドキュメントの場所を指定する string 値を渡します。
1. バイト配列を作成し、 `java.io.FileInputStream` オブジェクト。
1. コンストラクタを使用して `BLOB` オブジェクトを作成します。
1. 次の項目に `BLOB` オブジェクトを呼び出す `setBinaryData` メソッドを使用してバイト配列を渡す。 この `BLOB` オブジェクトの `setBinaryData` は、Base64 エンコーディングを使用する場合に呼び出すメソッドです。 サービス・リクエストでの BLOB オブジェクトの供給を参照してください。
1. を呼び出す `MyApplication/EncryptDocument` を呼び出して処理 `MyApplicationEncryptDocument` オブジェクトの `invoke` メソッド。 パス `BLOB` オブジェクトドキュメントを含むPDF。 invoke メソッドは、 `BLOB` 暗号化されたPDF・ドキュメントを含むオブジェクト。
1. を呼び出して、暗号化されたPDFドキュメントを含むバイト配列を作成します。 `BLOB` オブジェクトの `getBinaryData` メソッド。
1. 暗号化されたPDFドキュメントをPDFファイルとして保存します。 バイト配列をファイルに書き込みます。

**関連トピック**

[クイックスタート：Java プロキシファイルと Base64 エンコーディングを使用したサービスの呼び出し](/help/forms/developing/invocation-api-quick-starts.md#quick-start-invoking-a-service-using-java-proxy-files-and-base64-encoding)

[Base64 エンコーディングを使用する.NET クライアントアセンブリの作成](#creating-a-net-client-assembly-that-uses-base64-encoding)

## MTOM を使用したAEM Formsの呼び出し {#invoking-aem-forms-using-mtom}

Web サービス標準の MTOM を使用して、AEM Formsサービスを呼び出すことができます。 この規格では、バイナリデータ (PDFドキュメントなど ) がインターネットやイントラネット経由で送信される方法を定義します。 MTOM の特徴は、 `XOP:Include` 要素。 この要素は、SOAP メッセージのバイナリ添付を参照する XML Binary Optimized Packaging(XOP) 仕様で定義されます。

ここでは、MTOM を使用して、以下のAEM Formsの短時間のみ有効なプロセス ( `MyApplication/EncryptDocument`.

>[!NOTE]
>
>このプロセスは、既存の AEM Forms プロセスに基づいていません。このコードの例の流れを追うには、Workbench を使用して `MyApplication/EncryptDocument` という名前のプロセスを作成します。（[Workbench の使用](https://www.adobe.com/go/learn_aemforms_workbench_63)を参照。）

このプロセスを呼び出すと、次のアクションが実行されます。

1. プロセスに渡された保護されていない PDF ドキュメントを取得します。このアクションは `SetValue` 操作に基づいています。このプロセスの入力パラメーターは、`document` という名前の `inDoc` プロセス変数です。
1. PDF ドキュメントをパスワードで暗号化します。このアクションは `PasswordEncryptPDF` 操作に基づいています。パスワードで暗号化された PDF ドキュメントは、`outDoc` という名前のプロセス変数として返されます。

>[!NOTE]
>
>MTOM サポートは、AEM Forms、バージョン 9 で追加されました。

>[!NOTE]
>
>MTOM 送信プロトコルを使用する JAX WS ベースのアプリケーションは、送受信データが 25 MB に制限されています。 この制限は、JAX-WS のバグが原因です。 送受信ファイルの合計サイズが 25 MB を超える場合は、MTOM の代わりに SwaRef 送信プロトコルを使用します。 そうでない場合、 `OutOfMemory`* exception.*


ここでは、Microsoft .NET プロジェクト内で MTOM を使用してAEM Formsサービスを呼び出す方法について説明します。 使用される.NET フレームワークは 3.5 で、開発環境は Visual Studio 2008 です。 Web Service Enhancements(WSE) が開発用コンピューターにインストールされている場合は、削除します。 .NET 3.5 フレームワークは、Windows Communication Foundation (WCF) という名前の SOAP フレームワークをサポートしています。 MTOM を使用してAEM Formsを呼び出す場合、WCF（WSE ではない）のみがサポートされます。

### MTOM を使用してサービスを呼び出す.NET プロジェクトの作成 {#creating-a-net-project-that-invokes-a-service-using-mtom}

Web サービスを使用してAEM Formsサービスを呼び出すことができるMicrosoft .NET プロジェクトを作成できます。 まず、Visual Studio 2008 を使用してMicrosoft .NET プロジェクトを作成します。 AEM Formsサービスを呼び出すには、プロジェクト内で呼び出すAEM Formsサービスへのサービス参照を作成します。 サービス参照を作成する際に、AEM Formsサービスの URL を指定します。

```as3
 http://localhost:8080/soap/services/MyApplication/EncryptDocument?WSDL&lc_version=9.0.1
```

置換 `localhost` AEM Formsをホストする J2EE アプリケーションサーバーの IP アドレスを使用する 置換 `MyApplication/EncryptDocument` を呼び出すAEM Formsサービスの名前に置き換えます。 例えば、「Rights Management」操作を呼び出すには、次のように指定します。

`http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`

この `lc_version` オプションを使用すると、MTOM などのAEM Forms機能が使用可能になります。 指定しない `lc_version` 」オプションを使用する場合、MTOM を使用してAEM Formsを呼び出すことはできません。

サービス参照を作成したら、AEM Formsサービスに関連付けられているデータタイプを.NET プロジェクト内で使用できるようになります。 AEM Formsサービスを呼び出す.NET プロジェクトを作成するには、次の手順を実行します。

1. Microsoft Visual Studio 2008 を使用して.NET プロジェクトを作成します。
1. 内 **プロジェクト** メニュー、選択 **サービス参照を追加**.
1. 内 **住所** ダイアログボックスで、AEM Formsサービスへの WSDL を指定します。 例：

   ```as3
    http://localhost:8080/soap/services/MyApplication/EncryptDocument?WSDL&lc_version=9.0.1
   ```

1. クリック **移動**&#x200B;次に、**OK**.

### .NET プロジェクトでの MTOM を使用したサービスの呼び出し {#invoking-a-service-using-mtom-in-a-net-project}

次の点を考慮してください。 `MyApplication/EncryptDocument` 保護されていないパスワードドキュメントを受け入れ、PDFで暗号化されたパスワードドキュメントを返すPDF。 を呼び出すには、以下を実行します。 `MyApplication/EncryptDocument` MTOM を使用して（Workbench に組み込まれていた）プロセスは、次の手順で実行します。

1. Microsoft .NET プロジェクトを作成します。
1. の作成 `MyApplication_EncryptDocumentClient` オブジェクトのデフォルトのコンストラクタを使用します。
1. の作成 `MyApplication_EncryptDocumentClient.Endpoint.Address` オブジェクトを `System.ServiceModel.EndpointAddress` コンストラクタ。 WSDL をAEM Formsサービスに渡す string 値とエンコードの種類を指定します。

   ```as3
    https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=mtom
   ```

   を使用する必要はありません。 `lc_version` 属性。 この属性は、サービス参照を作成する際に使用されます。 ただし、次の項目を指定する必要があります。 `?blob=mtom`.

   >[!NOTE]
   >
   >置換 `hiro-xp`* AEM Formsをホストする J2EE アプリケーションサービスの IP アドレス*

1. の作成 `System.ServiceModel.BasicHttpBinding` オブジェクトを作成するには、 `EncryptDocumentClient.Endpoint.Binding` データメンバー。 戻り値を `BasicHttpBinding` にキャストします。
1. を `System.ServiceModel.BasicHttpBinding` オブジェクトの `MessageEncoding` データメンバー `WSMessageEncoding.Mtom`. この値は、MTOM が確実に使用されるようにします。
1. 次のタスクを実行して、基本的な HTTP 認証を有効にします。

   * AEM forms ユーザー名をデータメンバーに割り当てる `MyApplication_EncryptDocumentClient.ClientCredentials.UserName.UserName`.
   * 対応するパスワード値をデータメンバーに割り当てます。 `MyApplication_EncryptDocumentClient.ClientCredentials.UserName.Password`.
   * 定数値を割り当て `HttpClientCredentialType.Basic` データメンバーに `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * 定数値を割り当て `BasicHttpSecurityMode.TransportCredentialOnly` データメンバーに `BasicHttpBindingSecurity.Security.Mode`.

   次のコードの例に、これらのタスクを示します。

   ```as3
    //Enable BASIC HTTP authentication 
    encryptProcess.ClientCredentials.UserName.UserName = "administrator"; 
    encryptProcess.ClientCredentials.UserName.Password = "password"; 
    b.Security.Transport.ClientCredentialType = HttpClientCredentialType.Basic; 
    b.Security.Mode = BasicHttpSecurityMode.TransportCredentialOnly; 
    b.MaxReceivedMessageSize = 4000000; 
    b.MaxBufferSize = 4000000; 
    b.ReaderQuotas.MaxArrayLength = 4000000;
   ```

1. コンストラクタを使用して `BLOB` オブジェクトを作成します。この `BLOB` オブジェクトは、 `MyApplication/EncryptDocument` プロセス。
1. の作成 `System.IO.FileStream` オブジェクトを指定します。 PDFドキュメントのファイルの場所と、ファイルを開くモードを表す string 値を渡します。
1. コンテンツを格納するバイト配列を作成します。 `System.IO.FileStream` オブジェクト。 バイト配列のサイズは、 `System.IO.FileStream` オブジェクトの `Length` プロパティ。
1. を呼び出して、バイト配列にストリームデータを入力します。 `System.IO.FileStream` オブジェクトの `Read` メソッド。 読み取るバイト配列、開始位置、ストリーム長を渡します。
1. 次の項目に `BLOB` オブジェクトを割り当てる `MTOM` データメンバーにバイト配列の内容を入力します。
1. を呼び出す `MyApplication/EncryptDocument` を呼び出して処理 `MyApplication_EncryptDocumentClient` オブジェクトの `invoke` メソッド。 パス `BLOB` オブジェクトドキュメントを含むPDF。 このプロセスは、暗号化されたPDFドキュメントを `BLOB` オブジェクト。
1. の作成 `System.IO.FileStream` オブジェクトを指定します。
1. のデータコンテンツを格納するバイト配列を作成します。 `BLOB` が返したオブジェクト `invoke` メソッド。 バイト配列を生成するには、 `BLOB` オブジェクトの `MTOM` データメンバー。
1. の作成 `System.IO.BinaryWriter` オブジェクトのコンストラクタを呼び出し、 `System.IO.FileStream` オブジェクト。
1. を呼び出して、バイト配列の内容をPDFファイルに書き込みます。 `System.IO.BinaryWriter` オブジェクトの `Write` メソッドを使用してバイト配列を渡す。

>[!NOTE]
>
>ほとんどのAEM Formsサービス操作は、MTOM のクイックスタートを備えています。 これらのクイックスタートは、サービスの対応するクイックスタートセクションに表示されます。 例えば、Output のクイックスタートの節を見るには、 [Output サービス API のクイックスタート](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap).

**関連トピック**

[クイックスタート：.NET プロジェクトでの MTOM を使用したサービスの呼び出し](/help/forms/developing/invocation-api-quick-starts.md#quick-start-invoking-a-service-using-mtom-in-a-net-project)

[Web サービスを使用した複数のサービスへのアクセス](#accessing-multiple-services-using-web-services)

[人間中心の長期間有効なプロセスを呼び出す ASP.NET Web アプリケーションの作成](/help/forms/developing/invoking-human-centric-long-lived.md#creating-an-asp-net-web-application-that-invokes-a-human-centric-long-lived-process)

## SwaRef を使用したAEM Formsの呼び出し {#invoking-aem-forms-using-swaref}

SwaRef を使用してAEM Formsサービスを呼び出すことができます。 のコンテンツ `wsi:swaRef` XML 要素は、添付ファイルへの参照を保存する SOAP 本文内の添付ファイルとして送信されます。 SwaRef を使用してFormsサービスを呼び出す場合、XML Web Services 用 Java API(JAX-WS) を使用して Java プロキシクラスを作成します。 ( [XML Web サービス用 Java API](https://jax-ws.dev.java.net/jax-ws-ea3/docs/mtom-swaref.html).)

ここでは、以下のFormsの短時間有効なプロセスを呼び出す方法について説明します。 `MyApplication/EncryptDocument` SwaRef を使用して

>[!NOTE]
>
>このプロセスは、既存の AEM Forms プロセスに基づいていません。このコードの例の流れを追うには、Workbench を使用して `MyApplication/EncryptDocument` という名前のプロセスを作成します。（[Workbench の使用](https://www.adobe.com/go/learn_aemforms_workbench_63)を参照。）

このプロセスを呼び出すと、次のアクションが実行されます。

1. プロセスに渡された保護されていない PDF ドキュメントを取得します。このアクションは `SetValue` 操作に基づいています。このプロセスの入力パラメーターは、`document` という名前の `inDoc` プロセス変数です。
1. PDF ドキュメントをパスワードで暗号化します。このアクションは `PasswordEncryptPDF` 操作に基づいています。パスワードで暗号化された PDF ドキュメントは、`outDoc` という名前のプロセス変数として返されます。

>[!NOTE]
>
>AEM Formsでの SwaRef のサポートの追加

以下では、Java クライアントアプリケーション内で SwaRef を使用してFormsサービスを呼び出す方法について説明します。 Java アプリケーションは、JAX-WS を使用して作成されたプロキシクラスを使用します。

### SwaRef を使用する JAX-WS ライブラリファイルを使用してサービスを呼び出す {#invoke-a-service-using-jax-ws-library-files-that-use-swaref}

を呼び出すには、以下を実行します。 `MyApplication/EncryptDocument` JAX-WS と SwaRef を使用して作成された Java プロキシファイルを使用して、次の手順を実行します。

1. JAX-WS を使用して、 `MyApplication/EncryptDocument` サービス WSDL。 次の WSDL エンドポイントを使用します。

   ```as3
    https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?WSDL&lc_version=9.0.1
   ```

   詳しくは、 [JAX-WS を使用した Java プロキシクラスの作成](#creating-java-proxy-classes-using-jax-ws).

   >[!NOTE]
   >
   >置換 `hiro-xp`* AEM Formsをホストする J2EE アプリケーションサーバーの IP アドレス*

1. JAX-WS を使用して作成した Java プロキシクラスを JAR ファイルにパッケージ化します。
1. 次のパスにある Java プロキシ JAR ファイルと JAR ファイルを含めます。

   &lt;install directory=&quot;&quot;>\Adobe\Adobe_Experience_Manager_forms\sdk\client-libs\thirdparty

   を Java クライアントプロジェクトのクラスパスに追加します。

1. コンストラクタを使用して `MyApplicationEncryptDocumentService` オブジェクトを作成します。
1. の作成 `MyApplicationEncryptDocument` を呼び出すことによってオブジェクトを取得 `MyApplicationEncryptDocumentService` オブジェクトの `getEncryptDocument` メソッド。
1. 次のデータメンバーに値を割り当てて、AEM Formsを呼び出すのに必要な接続値を設定します。

   * WSDL エンドポイントとエンコーディングの種類を `javax.xml.ws.BindingProvider` オブジェクトの `ENDPOINT_ADDRESS_PROPERTY` フィールドに入力します。 を呼び出すには、以下を実行します。 `MyApplication/EncryptDocument` SwaRef エンコーディングを使用するサービスでは、次の URL 値を指定します。

      ` https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=swaref`

   * AEM forms ユーザーを `javax.xml.ws.BindingProvider` オブジェクトの `USERNAME_PROPERTY` フィールドに入力します。
   * 対応するパスワード値を `javax.xml.ws.BindingProvider` オブジェクトの `PASSWORD_PROPERTY` フィールドに入力します。

   次のコード例に、このアプリケーションロジックを示します。

   ```as3
    //Set connection values required to invoke AEM Forms 
    String url = "https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=swaref"; 
    String username = "administrator"; 
    String password = "password"; 
    ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.ENDPOINT_ADDRESS_PROPERTY, url); 
    ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.USERNAME_PROPERTY, username); 
    ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.PASSWORD_PROPERTY, password);
   ```

1. に送信するPDFドキュメントを取得します `MyApplication/EncryptDocument` プロセス（作成による） `java.io.File` オブジェクトを指定します。 PDFドキュメントの場所を指定する string 値を渡します。
1. の作成 `javax.activation.DataSource` オブジェクトを `FileDataSource` コンストラクタ。 パス `java.io.File` オブジェクト。
1. コンストラクタを使用して `javax.activation.DataHandler` オブジェクトを渡すことによって、`javax.activation.DataSource` オブジェクトを作成します。
1. コンストラクタを使用して `BLOB` オブジェクトを作成します。
1. 次の項目に `BLOB` オブジェクトを呼び出す `setSwaRef` メソッドおよび `javax.activation.DataHandler` オブジェクト。
1. を呼び出す `MyApplication/EncryptDocument` を呼び出して処理 `MyApplicationEncryptDocument` オブジェクトの `invoke` メソッドおよび `BLOB` オブジェクトドキュメントを含むPDF。 invoke メソッドは、 `BLOB` 暗号化されたPDF・ドキュメントを含むオブジェクト。
1. の `javax.activation.DataHandler` を呼び出すことによってオブジェクトを取得 `BLOB` オブジェクトの `getSwaRef` メソッド。
1. を `javax.activation.DataHandler` オブジェクトを `java.io.InputSteam` を呼び出すことによるインスタンス `javax.activation.DataHandler` オブジェクトの `getInputStream` メソッド。
1. を書く `java.io.InputSteam` インスタンスを、暗号化されたPDFドキュメントを表すPDFファイルに追加します。

>[!NOTE]
>
>ほとんどのAEM Formsサービス操作には、SwaRef クイックスタートが用意されています。 これらのクイックスタートは、サービスの対応するクイックスタートセクションに表示されます。 例えば、Output のクイックスタートの節を見るには、 [Output サービス API のクイックスタート](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap).

**関連トピック**

[クイックスタート：Java プロジェクトでの SwaRef を使用したサービスの呼び出し](/help/forms/developing/invocation-api-quick-starts.md#quick-start-invoking-a-service-using-swaref-in-a-java-project)

## HTTP 経由での BLOB データを使用したAEM Formsの呼び出し {#invoking-aem-forms-using-blob-data-over-http}

Web サービスを使用し、HTTP 経由で BLOB データを渡すことで、AEM Formsサービスを呼び出すことができます。 HTTP 経由で BLOB データを渡す方法は、base64 エンコーディング、DIME、MIME を使用する代わりに、別の方法です。 例えば、DIME や MIME をサポートしていない Web Service Enhancement 3.0 を使用するMicrosoft .NET プロジェクトで、HTTP 経由でデータを渡すことができます。 HTTP 経由で BLOB データを使用する場合は、AEM Formsサービスが呼び出される前に入力データがアップロードされます。

「BLOB Data over HTTP を使用したAEM Formsの呼び出し」では、次のAEM Formsの短時間のみ有効なプロセスの呼び出しについて説明します。 `MyApplication/EncryptDocument` HTTP 経由で BLOB データを渡す方法を使用する場合。

>[!NOTE]
>
>このプロセスは、既存の AEM Forms プロセスに基づいていません。このコードの例の流れを追うには、Workbench を使用して `MyApplication/EncryptDocument` という名前のプロセスを作成します。（[Workbench の使用](https://www.adobe.com/go/learn_aemforms_workbench_63)を参照。）

このプロセスを呼び出すと、次のアクションが実行されます。

1. プロセスに渡された保護されていない PDF ドキュメントを取得します。このアクションは `SetValue` 操作に基づいています。このプロセスの入力パラメーターは、`document` という名前の `inDoc` プロセス変数です。
1. PDF ドキュメントをパスワードで暗号化します。このアクションは `PasswordEncryptPDF` 操作に基づいています。パスワードで暗号化された PDF ドキュメントは、`outDoc` という名前のプロセス変数として返されます。

>[!NOTE]
>
>SOAP を使用したAEM Formsの呼び出しについて詳しく理解しておくことをお勧めします。 ( [Web サービスを使用したAEM Formsの呼び出し](#invoking-aem-forms-using-web-services).)

### HTTP 経由のデータを使用する.NET クライアントアセンブリの作成 {#creating-a-net-client-assembly-that-uses-data-over-http}

HTTP 経由でデータを使用するクライアントアセンブリを作成するには、 [Base64 エンコーディングを使用したAEM Formsの呼び出し](#invoking-aem-forms-using-base64-encoding). ただし、プロキシクラスの URL を修正して、 `?blob=http` の代わりに `?blob=base64`. このアクションにより、データが HTTP 経由で渡されます。 プロキシクラスで、次のコード行を探します。

```as3
 "http://localhost:8080/soap/services/MyApplication/EncryptDocument";
```

次のように変更します。

```as3
 "http://localhost:8080/soap/services/MyApplication/EncryptDocument?blob=http";
```

**.NET clientMyApplication/EncryptDocument アセンブリの参照**

新しい.NET クライアントアセンブリを、クライアントアプリケーションを開発するコンピューターに配置します。 .NET クライアントアセンブリをディレクトリに配置した後、プロジェクトから参照できます。 参照先 `System.Web.Services` ライブラリをプロジェクトから削除します。 このライブラリを参照しない場合、.NET クライアントアセンブリを使用してサービスを呼び出すことはできません。

1. 内 **プロジェクト** メニュー、選択 **参照を追加**.
1. 次をクリック： **.NET** タブをクリックします。
1. クリック **参照** DocumentService.dll ファイルを探します。
1. クリック **選択** 次に、 **OK**.

**HTTP 経由で BLOB データを使用する.NET クライアントアセンブリを使用したサービスの呼び出し**

を呼び出すことができます。 `MyApplication/EncryptDocument` HTTP 経由のデータを使用する.NET クライアントアセンブリを使用するサービス（Workbench で構築）。 を呼び出すには、以下を実行します。 `MyApplication/EncryptDocument` サービスで、次の手順を実行します。

1. .NET クライアントアセンブリを作成します。
1. Microsoft .NET クライアントアセンブリを参照します。 クライアントMicrosoft .NET プロジェクトを作成します。 クライアントプロジェクトでMicrosoft .NET クライアントアセンブリを参照します。 参照 `System.Web.Services`.
1. Microsoft .NET クライアントアセンブリを使用して、 `MyApplication_EncryptDocumentService` オブジェクトのデフォルトのコンストラクターを呼び出す。
1. を `MyApplication_EncryptDocumentService` オブジェクトの `Credentials` プロパティに `System.Net.NetworkCredential` オブジェクト。 内 `System.Net.NetworkCredential` コンストラクタ。AEM forms ユーザー名と対応するパスワードを指定します。 認証値を設定して、.NET クライアントアプリケーションがAEM Formsと SOAP メッセージを正常に交換できるようにします。
1. コンストラクタを使用して `BLOB` オブジェクトを作成します。この `BLOB` オブジェクトは、データを `MyApplication/EncryptDocument` プロセス。
1. 文字列値を `BLOB` オブジェクトの `remoteURL` に渡すPDFドキュメントの URI の場所を指定するデータメンバー `MyApplication/EncryptDocument`サービス。
1. を呼び出す `MyApplication/EncryptDocument` を呼び出して処理 `MyApplication_EncryptDocumentService` オブジェクトの `invoke` メソッドおよび `BLOB` オブジェクト。 このプロセスは、暗号化されたPDFドキュメントを `BLOB` オブジェクト。
1. の作成 `System.UriBuilder` オブジェクトのコンストラクタを使用し、返された `BLOB` オブジェクトの `remoteURL` データメンバー。
1. を `System.UriBuilder` オブジェクトを `System.IO.Stream` オブジェクト。 （このリストの後に続く C#クイックスタートは、このタスクの実行方法を示しています）。
1. バイト配列を作成し、 `System.IO.Stream` オブジェクト。
1. の作成 `System.IO.BinaryWriter` オブジェクトのコンストラクタを呼び出し、 `System.IO.FileStream` オブジェクト。
1. を呼び出して、バイト配列の内容をPDFファイルに書き込みます。 `System.IO.BinaryWriter` オブジェクトの `Write` メソッドを使用してバイト配列を渡す。

### HTTP 経由での Java プロキシクラスと BLOB データを使用したサービスの呼び出し {#invoking-a-service-using-java-proxy-classes-and-blob-data-over-http}

Java プロキシクラスと BLOB データを HTTP 経由で使用して、AEM Formsサービスを呼び出すことができます。 を呼び出すには、以下を実行します。 `MyApplication/EncryptDocument` Java プロキシクラスを使用するサービスで、次の手順を実行します。

1. JAX-WS を使用して、 `MyApplication/EncryptDocument` サービス WSDL。 次の WSDL エンドポイントを使用します。

   ```as3
    https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?WSDL&lc_version=9.0.1
   ```

   詳しくは、 [JAX-WS を使用した Java プロキシクラスの作成](#creating-java-proxy-classes-using-jax-ws).

   >[!NOTE]
   >
   >置換 `hiro-xp`* AEM Formsをホストする J2EE アプリケーションサーバーの IP アドレス*

1. JAX-WS を使用して作成した Java プロキシクラスを JAR ファイルにパッケージ化します。
1. 次のパスにある Java プロキシ JAR ファイルと JAR ファイルを含めます。

   &lt;install directory=&quot;&quot;>\Adobe\Adobe_Experience_Manager_forms\sdk\client-libs\thirdparty

   を Java クライアントプロジェクトのクラスパスに追加します。

1. コンストラクタを使用して `MyApplicationEncryptDocumentService` オブジェクトを作成します。
1. の作成 `MyApplicationEncryptDocument` を呼び出すことによってオブジェクトを取得 `MyApplicationEncryptDocumentService` オブジェクトの `getEncryptDocument` メソッド。
1. 次のデータメンバーに値を割り当てて、AEM Formsを呼び出すのに必要な接続値を設定します。

   * WSDL エンドポイントとエンコーディングの種類を `javax.xml.ws.BindingProvider` オブジェクトの `ENDPOINT_ADDRESS_PROPERTY` フィールドに入力します。 を呼び出すには、以下を実行します。 `MyApplication/EncryptDocument` BLOB over HTTP エンコーディングを使用するサービスでは、次の URL 値を指定します。

      `https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=http`

   * AEM forms ユーザーを `javax.xml.ws.BindingProvider` オブジェクトの `USERNAME_PROPERTY` フィールドに入力します。
   * 対応するパスワード値を `javax.xml.ws.BindingProvider` オブジェクトの `PASSWORD_PROPERTY` フィールドに入力します。

   次のコード例に、このアプリケーションロジックを示します。

   ```as3
    //Set connection values required to invoke AEM Forms 
    String url = "https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=http"; 
    String username = "administrator"; 
    String password = "password"; 
    ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.ENDPOINT_ADDRESS_PROPERTY, url); 
    ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.USERNAME_PROPERTY, username); 
    ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.PASSWORD_PROPERTY, password);
   ```

1. コンストラクタを使用して `BLOB` オブジェクトを作成します。
1. 次の項目に `BLOB` オブジェクトを呼び出す `setRemoteURL` メソッド。 に渡すPDFドキュメントの URI 位置を指定する string 値を渡します。 `MyApplication/EncryptDocument` サービス。
1. を呼び出す `MyApplication/EncryptDocument` を呼び出して処理 `MyApplicationEncryptDocument` オブジェクトの `invoke` メソッドおよび `BLOB` オブジェクトドキュメントを含むPDF。 このプロセスは、暗号化されたPDFドキュメントを `BLOB` オブジェクト。
1. 暗号化されたPDF・ドキュメントを表すデータ・ストリームを格納するバイト・アレイを作成します。 を呼び出す `BLOB` オブジェクトの `getRemoteURL` メソッド ( `BLOB` が返すオブジェクト `invoke` メソッド )。
1. コンストラクタを使用して `java.io.File` オブジェクトを作成します。このオブジェクトは、暗号化されたPDF・ドキュメントを表します。
1. コンストラクタを使用して `java.io.FileOutputStream` オブジェクトを渡すことによって、`java.io.File` オブジェクトを作成します。
1. を呼び出す `java.io.FileOutputStream` オブジェクトの `write` メソッド。 暗号化されたPDF・ドキュメントを表すデータ・ストリームを含むバイト配列を渡します。

## DIME を使用したAEM Formsの呼び出し {#invoking-aem-forms-using-dime}

添付ファイル付きの SOAP を使用して、AEM Formsサービスを呼び出すことができます。 AEM Formsは、MIME と DIME Web サービスの両方の標準をサポートしています。 DIME を使用すると、添付ファイルをエンコードする代わりに、呼び出し要求と共に、PDFドキュメントなどのバイナリ添付ファイルを送信できます。 この *DIME を使用したAEM Formsの呼び出し* の節では、以下のAEM Formsの短時間のみ有効なプロセスの呼び出しについて説明します。 `MyApplication/EncryptDocument` DIME を使用して。

このプロセスを呼び出すと、次のアクションが実行されます。

1. プロセスに渡された保護されていない PDF ドキュメントを取得します。このアクションは `SetValue` 操作に基づいています。このプロセスの入力パラメーターは、`document` という名前の `inDoc` プロセス変数です。
1. PDF ドキュメントをパスワードで暗号化します。このアクションは `PasswordEncryptPDF` 操作に基づいています。パスワードで暗号化された PDF ドキュメントは、`outDoc` という名前のプロセス変数として返されます。

このプロセスは、既存の AEM Forms プロセスに基づいていません。コード例に従うには、 `MyApplication/EncryptDocument`**Workbench の使用 （[Workbench の使用](https://www.adobe.com/go/learn_aemforms_workbench_63)を参照。）

>[!NOTE]
>
>DIME を使用したAEM Formsサービス操作の呼び出しは非推奨（廃止予定）となりました。 MTOM を使用することをお勧めします。 ( [MTOM を使用したAEM Formsの呼び出し](#invoking-aem-forms-using-mtom).)

### DIME を使用する.NET プロジェクトの作成 {#creating-a-net-project-that-uses-dime}

DIME を使用してFormsサービスを呼び出すことのできる.NET プロジェクトを作成するには、次のタスクを実行します。

* 開発用コンピュータに Web Services Enhancements 2.0 をインストールします。
* .NET プロジェクト内から、FormsAEM Formsサービスへの Web 参照を作成します。

**Web サービス拡張機能 2.0 のインストール**

Web Services Enhancements 2.0 を開発用コンピューターにインストールし、Microsoft Visual Studio .NET と統合します。 Web Services Enhancements 2.0 は、 [Microsoftダウンロードセンター](https://www.microsoft.com/downloads/search.aspx)

この Web ページから、Web Services Enhancements 2.0 を検索し、開発用コンピューターにダウンロードします。 このダウンロードにより、Microsoft WSE 2.0 SPI.msi という名前のファイルがコンピューターに配置されます。 インストールプログラムを実行し、オンラインの指示に従います。

>[!NOTE]
>
>Web Services Enhancements 2.0 は DIME をサポートしています。 Microsoft Visual Studio のサポート対象バージョンは、Web Services Enhancements 2.0 を操作する場合の 2003 年です。Web Services Enhancements 3.0 は、DIME をサポートしていません。しかし、MTOM をサポートしています。

**AEM Formsサービスへの Web 参照の作成**

Web Services Enhancements 2.0 を開発コンピューターにインストールし、Microsoft .NET プロジェクトを作成したら、Formsサービスへの Web 参照を作成します。 例えば、 `MyApplication/EncryptDocument` プロセスを実行し、Formsがローカルコンピューターにインストールされている場合は、次の URL を指定します。

```as3
     http://localhost:8080/soap/services/MyApplication/EncryptDocument?WSDL
```

Web 参照を作成した後、次の 2 つのプロキシデータ型を.NET プロジェクト内で使用できます。 `EncryptDocumentService` および `EncryptDocumentServiceWse`. を呼び出すには、以下を実行します。 `MyApplication/EncryptDocument` DIME を使用したプロセスでは、 `EncryptDocumentServiceWse` タイプ。

>[!NOTE]
>
>Formsサービスへの Web 参照を作成する前に、プロジェクトで Web Services Enhancements 2.0 を参照していることを確認してください。 （「Web Services Enhancements 2.0 のインストール」を参照）。

**WSE ライブラリの参照**

1. プロジェクトメニューで、「参照を追加」を選択します。
1. [ 参照を追加 ] ダイアログボックスで、[ Microsoft.Web.Services2.dll ] を選択します。
1. System.Web.Services.dll を選択します。
1. 「選択」をクリックし、「OK」をクリックします。

**Formsサービスへの Web 参照の作成**

1. プロジェクトメニューで、「Web 参照を追加」を選択します。
1. URL ダイアログボックスで、Formsサービスの URL を指定します。
1. 「移動」をクリックし、「参照を追加」をクリックします。

>[!NOTE]
>
>.NET プロジェクトで WSE ライブラリを使用できるようにします。 プロジェクトエクスプローラ内で、プロジェクト名を右クリックし、「WSE 2.0 を有効にする」を選択します。表示されるダイアログボックスのチェックボックスがオンになっていることを確認します。

**.NET プロジェクトでの DIME を使用したサービスの呼び出し**

DIME を使用してFormsサービスを呼び出すことができます。 次の点を考慮してください。 `MyApplication/EncryptDocument` 保護されていないパスワードドキュメントを受け入れ、PDFで暗号化されたパスワードドキュメントを返すPDF。 を呼び出すには、以下を実行します。 `MyApplication/EncryptDocument` DIME を使用してプロセスを実行するには、次の手順を実行します。

1. DIME を使用してFormsサービスを呼び出せるようにするMicrosoft .NET プロジェクトを作成します。 Web Services Enhancements 2.0 を含め、AEM Formsサービスへの Web 参照を作成します。
1. Web 参照を `MyApplication/EncryptDocument` プロセス、作成 `EncryptDocumentServiceWse` オブジェクトのデフォルトのコンストラクタを使用します。
1. を `EncryptDocumentServiceWse` オブジェクトの `Credentials` データメンバーを `System.Net.NetworkCredential` AEM forms のユーザー名とパスワードの値を指定する値。
1. の作成 `Microsoft.Web.Services2.Dime.DimeAttachment` オブジェクトを作成するには、コンストラクタを使用し、次の値を渡します。

   * GUID 値を指定する string 値。 GUID 値は、 `System.Guid.NewGuid.ToString` メソッド。
   * コンテンツタイプを指定する string 値。 このプロセスにはPDF文書が必要なので、 `application/pdf`.
   * A `TypeFormat` 列挙値。 以下のように `TypeFormat.MediaType`.
   * AEM Formsプロセスに渡すPDFドキュメントの場所を指定する string 値。

1. コンストラクタを使用して `BLOB` オブジェクトを作成します。
1. DIME 添付ファイルを `BLOB` オブジェクトを割り当てる `Microsoft.Web.Services2.Dime.DimeAttachment` オブジェクトの `Id` データメンバーの値を `BLOB` オブジェクトの `attachmentID` データメンバー。
1. を呼び出す `EncryptDocumentServiceWse.RequestSoapContext.Attachments.Add` メソッドを使用して、 `Microsoft.Web.Services2.Dime.DimeAttachment` オブジェクト。
1. を呼び出す `MyApplication/EncryptDocument` を呼び出して処理 `EncryptDocumentServiceWse` オブジェクトの `invoke` メソッドおよび `BLOB` DIME 添付ファイルを含むオブジェクト。 このプロセスは、暗号化されたPDFドキュメントを `BLOB` オブジェクト。
1. 返される `BLOB` オブジェクトの `attachmentID` データメンバー。
1. 次の場所にある添付ファイルを繰り返し処理します。 `EncryptDocumentServiceWse.ResponseSoapContext.Attachments` およびを使用して、暗号化された添付ファイルドキュメントを取得し、PDF識別子の値を使用します。
1. の取得 `System.IO.Stream` オブジェクトを作成するには、 `Attachment` オブジェクトの `Stream` データメンバー。
1. バイト配列を作成し、そのバイト配列を `System.IO.Stream` オブジェクトの `Read` メソッド。 このメソッドは、暗号化されたPDF・ドキュメントを表すデータ・ストリームをバイト・アレイに入力します。
1. の作成 `System.IO.FileStream` オブジェクトを指定します。 このオブジェクトは、暗号化されたPDF・ドキュメントを表します。
1. の作成 `System.IO.BinaryWriter` オブジェクトのコンストラクタを呼び出し、 `System.IO.FileStream` オブジェクト。
1. を呼び出して、バイト配列の内容をPDFファイルに書き込みます。 `System.IO.BinaryWriter` オブジェクトの `Write` メソッドを使用してバイト配列を渡す。

### DIME を使用する Apache Axis Java プロキシクラスの作成 {#creating-apache-axis-java-proxy-classes-that-use-dime}

Apache Axis WSDL2Java ツールを使用してサービス WSDL を Java プロキシクラスに変換し、サービス操作を呼び出すことができます。 Apache Ant を使用すると、サービスを呼び出すAEM Formsサービス WSDL から Axis ライブラリファイルを生成できます。 ( [Apache Axis を使用した Java プロキシクラスの作成](#creating-java-proxy-classes-using-apache-axis).)

Apache Axis WSDL2Java ツールは、SOAP 要求をサービスに送信するために使用されるメソッドを含む JAVA ファイルを生成します。 サービスが受け取った SOAP リクエストは、Axis が生成したライブラリによってデコードされ、メソッドと引数に戻されます。

を呼び出すには、以下を実行します。 `MyApplication/EncryptDocument` Axis 生成のライブラリファイルと DIME を使用して、（Workbench で構築された）サービスを次の手順で実行します。

1. を使用する Java プロキシクラスの作成 `MyApplication/EncryptDocument` Apache Axis を使用したサービス WSDL ( [Apache Axis を使用した Java プロキシクラスの作成](#creating-java-proxy-classes-using-apache-axis).)
1. Java プロキシクラスをクラスパスに含めます。
1. コンストラクタを使用して `MyApplicationEncryptDocumentServiceLocator` オブジェクトを作成します。
1. の作成 `URL` オブジェクトを指定します。 次の項目を指定してください。 `?blob=dime` SOAP エンドポイント URL の末尾に配置されます。 例えば、

   ```as3
    https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=dime.
   ```

1. の作成 `EncryptDocumentSoapBindingStub` オブジェクトのコンストラクタを呼び出し、 `MyApplicationEncryptDocumentServiceLocator`オブジェクトと `URL` オブジェクト。
1. を呼び出して、AEM forms のユーザー名とパスワードの値を設定します。 `EncryptDocumentSoapBindingStub` オブジェクトの `setUsername` および `setPassword` メソッド。

   ```as3
    encryptionClientStub.setUsername("administrator"); 
    encryptionClientStub.setPassword("password");
   ```

1. に送信するPDFドキュメントを取得します `MyApplication/EncryptDocument` サービスを作成する `java.io.File` オブジェクト。 PDFドキュメントの場所を指定する string 値を渡します。
1. の作成 `javax.activation.DataHandler` オブジェクトのコンストラクタを使用し、 `javax.activation.FileDataSource` オブジェクト。 この `javax.activation.FileDataSource` オブジェクトは、コンストラクタを使用して `java.io.File` オブジェクトドキュメントを表すPDF。
1. の作成 `org.apache.axis.attachments.AttachmentPart` オブジェクトのコンストラクタを使用し、 `javax.activation.DataHandler` オブジェクト。
1. を呼び出して添付ファイルを添付 `EncryptDocumentSoapBindingStub` オブジェクトの `addAttachment` メソッドおよび `org.apache.axis.attachments.AttachmentPart` オブジェクト。
1. コンストラクタを使用して `BLOB` オブジェクトを作成します。次の項目に `BLOB` を呼び出すことにより、attachment identifier 値を持つオブジェクト `BLOB` オブジェクトの `setAttachmentID` メソッドを使用して添付ファイル識別子の値を渡す方法を参照してください。 この値は、 `org.apache.axis.attachments.AttachmentPart` オブジェクトの `getContentId` メソッド。
1. を呼び出す `MyApplication/EncryptDocument` を呼び出して処理 `EncryptDocumentSoapBindingStub` オブジェクトの `invoke` メソッド。 パス `BLOB` DIME 添付ファイルを含むオブジェクト。 このプロセスは、暗号化されたPDFドキュメントを `BLOB` オブジェクト。
1. 返された `BLOB` オブジェクトの `getAttachmentID` メソッド。 このメソッドは、返される添付ファイルの識別子の値を表す string 値を返します。
1. を呼び出して添付ファイルを取得する `EncryptDocumentSoapBindingStub` オブジェクトの `getAttachments` メソッド。 このメソッドは、 `Objects` 添付ファイルを表す。
1. 添付ファイル ( `Object` 配列 ) を参照し、添付ファイル識別子の値を使用して、暗号化されたPDFドキュメントを取得します。 各要素は `org.apache.axis.attachments.AttachmentPart` オブジェクト。
1. の取得 `javax.activation.DataHandler` を呼び出すことで添付ファイルに関連付けられたオブジェクト `org.apache.axis.attachments.AttachmentPart` オブジェクトの `getDataHandler` メソッド。
1. の取得 `java.io.FileStream` を呼び出すことによってオブジェクトを取得 `javax.activation.DataHandler` オブジェクトの `getInputStream` メソッド。
1. バイト配列を作成し、そのバイト配列を `java.io.FileStream` オブジェクトの `read` メソッド。 このメソッドは、暗号化されたPDF・ドキュメントを表すデータ・ストリームをバイト・アレイに入力します。
1. コンストラクタを使用して `java.io.File` オブジェクトを作成します。このオブジェクトは、暗号化されたPDF・ドキュメントを表します。
1. コンストラクタを使用して `java.io.FileOutputStream` オブジェクトを渡すことによって、`java.io.File` オブジェクトを作成します。
1. を呼び出す `java.io.FileOutputStream` オブジェクトの `write` メソッドを使用して、暗号化されたPDF・ドキュメントを表すデータ・ストリームを含むバイト配列を渡します。

**関連トピック**

[クイックスタート：Java プロジェクトでの DIME を使用したサービスの呼び出し](/help/forms/developing/invocation-api-quick-starts.md#quick-start-invoking-a-service-using-dime-in-a-java-project)

## SAML ベースの認証の使用 {#using-saml-based-authentication}

AEM Formsは、サービスを呼び出す際に、様々な web サービス認証モードをサポートします。 1 つの認証モードでは、Web サービス呼び出しの基本認証ヘッダーを使用してユーザー名とパスワードの値の両方を指定します。 AEM Formsは、SAML アサーションベースの認証もサポートしています。 クライアントアプリケーションが Web サービスを使用してAEM Formsサービスを呼び出すと、クライアントアプリケーションは次のいずれかの方法で認証情報を提供できます。

* 基本認証の一部として資格情報を渡す
* WS-Security ヘッダーの一部としてユーザー名トークンを渡す
* WS-Security ヘッダーの一部として SAML アサーションを渡す
* WS-Security ヘッダーの一部として Kerberos トークンを渡す

AEM Formsは、標準の証明書ベースの認証をサポートしていませんが、別の形式の証明書ベースの認証をサポートしています。

>[!NOTE]
>
>「 AEM Formsでのプログラミング」の Web サービスのクイックスタートでは、認証を実行するユーザー名とパスワードの値を指定します。

AEM forms ユーザーの ID は、秘密鍵を使用して署名された SAML アサーションを通じて表すことができます。 次の XML コードは、SAML アサーションの例を示しています。

```as3
 <Assertion xmlns="urn:oasis:names:tc:SAML:1.0:assertion" 
     xmlns:saml="urn:oasis:names:tc:SAML:1.0:assertion" 
     xmlns:samlp="urn:oasis:names:tc:SAML:1.0:protocol" 
     AssertionID="fd4bd0c87302780e0d9bbfa8726d5bc0" IssueInstant="2008-04-17T13:47:00.720Z" Issuer="LiveCycle" 
     MajorVersion="1" MinorVersion="1"> 
     <Conditions NotBefore="2008-04-17T13:47:00.720Z" NotOnOrAfter="2008-04-17T15:47:00.720Z"> 
     </Conditions> 
     <AuthenticationStatement 
         AuthenticationInstant="2008-04-17T13:47:00.720Z" 
         AuthenticationMethod="urn:oasis:names:tc:SAML:1.0:am:unspecified"> 
         <Subject> 
             <NameIdentifier NameQualifier="DefaultDom">administrator</NameIdentifier> 
             <SubjectConfirmation> 
                 <ConfirmationMethod>urn:oasis:names:tc:SAML:1.0:cm:sender-vouches</ConfirmationMethod> 
             </SubjectConfirmation> 
         </Subject> 
     </AuthenticationStatement> 
     <ds:Signature > 
         <ds:SignedInfo> 
             <ds:CanonicalizationMethod Algorithm="https://www.w3.org/2001/10/xml-exc-c14n#"></ds:CanonicalizationMethod> 
             <ds:SignatureMethod    Algorithm="https://www.w3.org/2000/09/xmldsig#hmac-sha1"></ds:SignatureMethod> 
             <ds:Reference URI="#fd4bd0c87302780e0d9bbfa8726d5bc0"> 
                 <ds:Transforms> 
                     <ds:Transform Algorithm="https://www.w3.org/2000/09/xmldsig#enveloped-signature"></ds:Transform> 
                     <ds:Transform Algorithm="https://www.w3.org/2001/10/xml-exc-c14n#"> 
                         <ec:InclusiveNamespaces     
                             PrefixList="code ds kind rw saml samlp typens #default"> 
                         </ec:InclusiveNamespaces> 
                     </ds:Transform> 
                 </ds:Transforms> 
                 <ds:DigestMethod Algorithm="https://www.w3.org/2000/09/xmldsig#sha1"></ds:DigestMethod> 
                 <ds:DigestValue>hVrtqjWr+VzaVUIpQx0YI9lIjaY=</ds:DigestValue> 
             </ds:Reference> 
         </ds:SignedInfo> 
         <ds:SignatureValue>UMbBb+cUcPtcWDCIhXes4n4FxfU=</ds:SignatureValue> 
     </ds:Signature> 
 </Assertion>
```

この例のアサーションは、管理者ユーザーに対して発行されます。 このアサーションには、次の目に見える項目が含まれます。

* 一定期間有効です。
* 特定のユーザーに対して発行されます。
* デジタル署名されています。 したがって、変更を加えると署名が壊れます。
* ユーザー名やパスワードと同様に、ユーザーの ID のトークンとしてAEM Formsに表示できます。

クライアントアプリケーションは、 `AuthResult` オブジェクト。 以下を取得すると、 `AuthResult` インスタンスを作成するには、次の 2 つの方法のいずれかを実行します。

* AuthenticationManager API で公開されている認証メソッドのいずれかを使用して、ユーザーを認証する。 通常は、ユーザー名とパスワードを使用します。ただし、証明書認証を使用することもできます。
* の使用 `AuthenticationManager.getAuthResultOnBehalfOfUser` メソッド。 このメソッドを使用すると、クライアントアプリケーションは `AuthResult` 任意のAEM forms ユーザー用のオブジェクト。

AEM forms ユーザーは、取得した SAML トークンを使用して認証できます。 この SAML アサーション（xml フラグメント）は、ユーザー認証用の Web サービス呼び出しで WS-Security ヘッダーの一部として送信できます。 通常、クライアントアプリケーションはユーザーを認証しましたが、ユーザー資格情報は保存されていません。 （または、ユーザー名とパスワード以外のメカニズムを使用してそのクライアントにログオンした。） この場合、クライアントアプリケーションはAEM Formsを呼び出し、AEM Formsの呼び出しを許可されている特定のユーザーとして動作する必要があります。

特定のユーザーを装うには、 `AuthenticationManager.getAuthResultOnBehalfOfUser` メソッドを使用して web サービスを使用します。 このメソッドは、 `AuthResult` そのユーザーの SAML アサーションを含むインスタンス。

次に、その SAML アサーションを使用して、認証を必要とするサービスを呼び出します。 このアクションでは、SOAP ヘッダーの一部としてアサーションを送信します。 このアサーションで Web サービスが呼び出されると、AEM Formsはユーザーをそのアサーションで表されるユーザーとして識別します。 つまり、アサーションで指定されたユーザーは、サービスを呼び出すユーザーです。

### Apache Axis クラスと SAML ベースの認証の使用 {#using-apache-axis-classes-and-saml-based-authentication}

Axis ライブラリを使用して作成された Java プロキシクラスによってAEM Formsサービスを呼び出すことができます。 ( [Apache Axis を使用した Java プロキシクラスの作成](#creating-java-proxy-classes-using-apache-axis).)

SAML ベースの認証を使用する AXIS を使用する場合は、Axis にリクエストと応答ハンドラーを登録します。 Apache Axis は、呼び出し要求をAEM Formsに送信する前にハンドラーを呼び出します。 ハンドラーを登録するには、を拡張する Java クラスを作成します `org.apache.axis.handlers.BasicHandler`.

**軸を持つ AssertionHandler の作成**

次の Java クラス ( `AssertionHandler.java`に、を拡張する Java クラスの例を示します `org.apache.axis.handlers.BasicHandler`.

```as3
 public class AssertionHandler extends BasicHandler { 
        public void invoke(MessageContext ctx) throws AxisFault { 
            String assertion = (String) ctx.getProperty(LC_ASSERTION); 
  
            //no assertion hence nothing to insert 
            if(assertion == null) return;  
      
            try { 
                MessageElement samlElement = new MessageElement(convertToXML(assertion)); 
                SOAPHeader header = (SOAPHeader) ctx.getRequestMessage().getSOAPHeader(); 
                //Create the wsse:Security element which would contain the SAML element 
                SOAPElement wsseHeader = header.addChildElement("Security", "wsse", WSSE_NS); 
                wsseHeader.appendChild(samlElement); 
                //remove the actor attribute as in LC we do not specify any actor. This would not remove the actor attribute though 
                //it would only remove it from the soapenv namespace 
                wsseHeader.getAttributes().removeNamedItem("actor"); 
            } catch (SOAPException e) { 
                throw new AxisFault("Error occured while adding the assertion to the SOAP Header",e); 
            } 
        } 
 }
```

**ハンドラーを登録**

Axis にハンドラーを登録するには、 client-config.wsdd ファイルを作成します。 既定では、Axis はこの名前のファイルを検索します。 次の XML コードは client-config.wsdd ファイルの例です。 詳しくは、軸のドキュメントを参照してください。

```as3
 <deployment xmlns="https://xml.apache.org/axis/wsdd/" xmlns:java="https://xml.apache.org/axis/wsdd/providers/java"> 
     <transport name="http" pivot="java:org.apache.axis.transport.http.HTTPSender"/> 
      <globalConfiguration > 
       <requestFlow > 
        <handler type="java:com.adobe.idp.um.example.AssertionHandler" /> 
       </requestFlow > 
      </globalConfiguration > 
 </deployment> 
 
```

**AEM Formsサービスを呼び出す**

次のコード例は、SAML ベースの認証を使用してAEM Formsサービスを呼び出します。

```as3
 public class ImpersonationExample { 
        . . . 
        public void  authenticateOnBehalf(String superUsername,String password,  
                String canonicalName,String domainName) throws UMException, RemoteException{ 
            ((org.apache.axis.client.Stub) authenticationManager).setUsername(superUsername); 
            ((org.apache.axis.client.Stub) authenticationManager).setPassword(password); 
      
            //Step 1 - Invoke the Auth manager api to get an assertion for the user to be impersonated 
            AuthResult ar = authenticationManager.getAuthResultOnBehalfOfUser(canonicalName, domainName, null); 
            String assertion = ar.getAssertion(); 
            //Step 2 - Setting the assertion here to be picked later by the AssertionHandler. Note that stubs are not threadSafe 
            //hence should not be reused. For this simple example we have made them instance variable but care should be taken 
            //regarding the thread safety 
            ((javax.xml.rpc.Stub) authorizationManager)._setProperty(AssertionHandler.LC_ASSERTION, assertion); 
        } 
      
        public Role findRole(String roleId) throws UMException, RemoteException{ 
            //This api would be invoked under bob's user rights 
            return authorizationManager.findRole(roleId); 
        } 
      
        public static void main(String[] args) throws Exception { 
            ImpersonationExample ie = new ImpersonationExample("http://localhost:5555"); 
            //Get the SAML assertion for the user to impersonate and store it in stub 
            ie.authenticateOnBehalf( 
                    "administrator", //The Super user which has the required impersonation permission 
                    "password", // Password of the super user as referred above 
                    "bob", //Cannonical name of the user to impersonate 
                    "testdomain" //Domain of the user to impersonate 
                    ); 
      
            Role r = ie.findRole("BASIC_ROLE_ADMINISTRATOR"); 
            System.out.println("Role "+r.getName()); 
        } 
 }
```

### .NET クライアントアセンブリと SAML ベースの認証の使用 {#using-a-net-client-assembly-and-saml-based-authentication}

.NET クライアントアセンブリと SAML ベースの認証を使用して、Formsサービスを呼び出すことができます。 そのためには、Web Service Enhancements 3.0(WSE) を使用する必要があります。 WSE を使用する.NET クライアントアセンブリの作成については、 [DIME を使用する.NET プロジェクトの作成](#creating-a-net-project-that-uses-dime).

>[!NOTE]
>
>DIME セクションでは WSE 2.0 を使用します。SAML ベースの認証を使用するには、DIME のトピックで指定されているのと同じ手順に従います。 ただし、WSE 2.0 を WSE 3.0 に置き換えます。開発用コンピューターに Web Services Enhancements 3.0 をインストールし、Microsoft Visual Studio .NET に統合します。 Web Services Enhancements 3.0 は、 [Microsoftダウンロードセンター](https://www.microsoft.com/downloads/search.aspx).

WSE アーキテクチャは、ポリシー、アサーション、および SecurityToken データ型を使用します。 Web サービスの呼び出しで、ポリシーを指定します。 1 つのポリシーに複数のアサーションを設定できます。 各アサーションには、フィルターを含めることができます。 フィルターは、Web サービス呼び出しの特定のステージで呼び出され、その時点で、SOAP 要求を変更できます。 詳しくは、 Web サービス拡張機能 3.0 のドキュメントを参照してください。

**アサーションとフィルターの作成**

次の C#コードの例では、filter クラスと assertion クラスを作成します。 このコードの例では、SamlAssertionOutputFilter を作成します。 このフィルターは、SOAP 要求がAEM Formsに送信される前に、WSE フレームワークによって呼び出されます。

```as3
 class LCSamlPolicyAssertion : Microsoft.Web.ServicES4.Design.PolicyAssertion 
 { 
        public override Microsoft.Web.ServicES4.SoapFilter CreateClientOutputFilter(FilterCreationContext context) 
        { 
           return new SamlAssertionOutputFilter(); 
        } 
        . . . 
 } 
  
      
 class SamlAssertionOutputFilter : SendSecurityFilter 
 { 
        public override void SecureMessage(SoapEnvelope envelope, Security security) 
        { 
           // Get the SamlToken from the SessionState 
           SamlToken samlToken = envelope.Context.Credentials.UltimateReceiver.GetClientToken<SamlToken>(); 
           security.Tokens.Add(samlToken); 
        } 
 }
```

**SAML トークンの作成**

SAML アサーションを表すクラスを作成します。 このクラスが実行する主なタスクは、データ値を文字列から xml に変換し、空白を保持することです。 このアサーション xml は、後で SOAP リクエストに読み込まれます。

```as3
 class SamlToken : SecurityToken 
 { 
        public const string SAMLAssertion = "https://docs.oasis-open.org/wss/oasis-wss-saml-token-profile-1.1#SAMLV1.1"; 
        private XmlElement _assertionElement; 
  
        public SamlToken(string assertion) 
             : base(SAMLAssertion) 
        { 
           XmlDocument xmlDoc = new XmlDocument(); 
           //The white space has to be preserved else the digital signature would get broken 
           xmlDoc.PreserveWhitespace = true; 
           xmlDoc.LoadXml(assertion); 
           _assertionElement = xmlDoc.DocumentElement; 
         } 
      
         public override XmlElement GetXml(XmlDocument document) 
         { 
            return (XmlElement)document.ImportNode(_assertionElement, true); 
         } 
        . . .  
 }
```

**AEM Formsサービスを呼び出す**

次の C#コードの例では、SAML ベースの認証を使用してFormsサービスを呼び出します。

```as3
 public class ImpersonationExample 
 { 
        . . . 
        public void AuthenticateOnBehalf(string superUsername, string password, string canonicalName, string domainName) 
        { 
            //Create a policy for UsernamePassword Token 
            Policy usernamePasswordPolicy = new Policy(); 
            usernamePasswordPolicy.Assertions.Add(new UsernameOverTransportAssertion()); 
      
            UsernameToken token = new UsernameToken(superUsername, password, PasswordOption.SendPlainText); 
            authenticationManager.SetClientCredential(token); 
            authenticationManager.SetPolicy(usernamePasswordPolicy); 
  
            //Get the SAML assertion for impersonated user 
            AuthClient.AuthenticationManagerService.AuthResult ar  
                = authenticationManager.getAuthResultOnBehalfOfUser(canonicalName, domainName, null); 
            System.Console.WriteLine("Received assertion " + ar.assertion); 
  
            //Create a policy for inserting SAML assertion 
            Policy samlPolicy = new Policy(); 
            samlPolicy.Assertions.Add(new LCSamlPolicyAssertion()); 
            authorizationManager.SetPolicy(samlPolicy); 
            //Set the SAML assertion obtained previously as the token 
            authorizationManager.SetClientCredential(new SamlToken(ar.assertion)); 
        } 
  
        public Role findRole(string roleId) 
        { 
            return authorizationManager.findRole(roleId); 
        } 
  
        static void Main(string[] args) 
        { 
            ImpersonationExample ie = new ImpersonationExample("http://localhost:5555"); 
            ie.AuthenticateOnBehalf( 
                 "administrator", //The Super user which has the required impersonation permission 
                 "password", // Password of the super user as referred above 
                 "bob", //Cannonical name of the user to impersonate 
                 "testdomain" //Domain of the user to impersonate 
                 ); 
          
         Role r = ie.findRole("BASIC_ROLE_ADMINISTRATOR"); 
            System.Console.WriteLine("Role "+r.name); 
     } 
 }
```

## Web サービスを使用する際の関連事項 {#related-considerations-when-using-web-services}

Web サービスを使用して特定のAEM Forms Services 操作を呼び出すと、問題が発生することがあります。 このディスカッションの目的は、問題を特定し、解決策がある場合は提供することです。

### サービス操作を非同期で呼び出しています {#invoking-service-operations-asynchronously}

GeneratePDFの `htmlToPDF` 操作， `SoapFaultException` 発生します。 この問題を解決するには、 `ExportPDF_Result` 要素と他の要素を異なるクラスに分割します。 次の XML は、カスタムバインディングファイルを表します。

```as3
 <bindings     
        xmlns:xsd="https://www.w3.org/2001/XMLSchema" 
        xmlns:jxb="https://java.sun.com/xml/ns/jaxb" jxb:version="1.0" 
        xmlns:wsdl="https://schemas.xmlsoap.org/wsdl/" 
      wsdlLocation="http://localhost:8080/soap/services/GeneratePDFService?wsdl&async=true&lc_version=9.0.0" 
        xmlns="https://java.sun.com/xml/ns/jaxws"> 
        <enableAsyncMapping>false</enableAsyncMapping> 
        <package name="external_customize.client"/> 
        <enableWrapperStyle>true</enableWrapperStyle> 
        <bindings node="/wsdl:definitions/wsdl:types/xsd:schema[@targetNamespace='https://adobe.com/idp/services']/xsd:element[@name='ExportPDF_Result']">            
            <jxb:class name="ExportPDFAsyncResult">             
            </jxb:class> 
        </bindings> 
        <bindings node="/wsdl:definitions/wsdl:types/xsd:schema[@targetNamespace='https://adobe.com/idp/services']/xsd:element[@name='CreatePDF_Result']">            
            <jxb:class name="CreatePDFAsyncResult">             
            </jxb:class> 
        </bindings> 
        <bindings node="/wsdl:definitions/wsdl:types/xsd:schema[@targetNamespace='https://adobe.com/idp/services']/xsd:element[@name='HtmlToPDF_Result']">            
            <jxb:class name="HtmlToPDFAsyncResult">             
            </jxb:class> 
        </bindings> 
        <bindings node="/wsdl:definitions/wsdl:types/xsd:schema[@targetNamespace='https://adobe.com/idp/services']/xsd:element[@name='OptimizePDF_Result']">            
            <jxb:class name="OptimizePDFAsyncResult">             
            </jxb:class> 
        </bindings> 
        <!--bindings node="//wsdl:portType[@name='GeneratePDFService']/wsdl:operation[@name='HtmlToPDF_Result']">               
            <jxb:class name="HtmlToPDFAsyncResult"/>             
        </bindings--> 
 </bindings>
```

JAX-WS を使用して Java プロキシファイルを作成する場合は、この XML ファイルを使用します。 ( [JAX-WS を使用した Java プロキシクラスの作成](#creating-java-proxy-classes-using-jax-ws).)

JAX-WS ツール (wsimport.exe) を実行する際に、 — を使用してこの XML ファイルを参照します。 `b` コマンドラインオプション。 を更新します。 `wsdlLocation` 要素を使用して、AEM Formsの URL を指定します。

非同期呼び出しが確実に機能するようにするには、エンドポイント URL の値を変更し、 `async=true`. 例えば、JAX-WS で作成される Java プロキシファイルの場合、 `BindingProvider.ENDPOINT_ADDRESS_PROPERTY`.

`https://server:port/soap/services/ServiceName?wsdl&async=true&lc_version=9.0.0`

次のリストは、非同期で呼び出された場合にカスタムバインディングファイルを必要とする他のサービスを指定します。

* PDFG 3D
* タスクマネージャー
* Application Manager
* ディレクトリマネージャー
* Distiller
* Rights Management
* Document Management

### J2EE アプリケーションサーバーの違い {#differences-in-j2ee-application-servers}

特定の J2EE アプリケーションサーバーを使用して作成されたプロキシライブラリが、別の J2EE アプリケーションサーバーでホストされているAEM Formsを正常に呼び出さない場合があります。 WebSphere にデプロイされるAEM Formsを使用して生成されるプロキシライブラリについて考えてみましょう。 このプロキシライブラリは、JBoss Application Server にデプロイされているAEM Formsサービスを正常に呼び出せません。

一部のAEM Formsの複雑なデータ型（など） `PrincipalReference`WebSphere にAEM Formsをデプロイする場合の定義は、JBoss Application Server とは異なります。 異なる J2EE アプリケーションサービスで使用される JDK の違いが、WSDL 定義に違いがある理由です。 その結果、同じ J2EE アプリケーションサーバーから生成されたプロキシライブラリを使用します。

### Web サービスを使用した複数のサービスへのアクセス {#accessing-multiple-services-using-web-services}

名前空間の競合により、複数のサービス WSDL 間でデータオブジェクトを共有することはできません。 様々なサービスでデータ型を共有できるので、サービスは WSDL 内でこれらの型の定義を共有します。 たとえば、 `BLOB` 同じ.NET クライアントプロジェクトに対するデータ型。 この場合、コンパイルエラーが発生します。

次のリストは、複数のサービス WSDL 間で共有できないデータ型を指定します。

* `User`
* `Principals`
* `PrincipalReference`
* `Groups`
* `Roles`
* `BLOB`

この問題を回避するには、データタイプを完全に修飾することをお勧めします。 例えば、サービス参照を使用してFormsサービスと Signature サービスの両方を参照する.NET アプリケーションについて考えてみましょう。 両方のサービス参照には、 `BLOB` クラス。 次の手順で `BLOB` インスタンスを完全修飾 `BLOB` オブジェクトを宣言する際に使用します。 この方法を次のコード例に示します。 このコード例について詳しくは、 [インタラクティブFormsのデジタル署名](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-interactive-forms).

次の C#コードの例は、Formsサービスによってレンダリングされるインタラクティブフォームに署名します。 クライアントアプリケーションには 2 つのサービス参照があります。 この `BLOB` Formsサービスに関連付けられているインスタンスは、 `SignInteractiveForm.ServiceReference2` 名前空間。 同様に、 `BLOB` Signature サービスに関連付けられているインスタンスは、 `SignInteractiveForm.ServiceReference1` 名前空間。 署名済みのインタラクティブフォームは、という名前のPDFファイルとして保存されます *LoanXFASigned.pdf*.

```as3
 ???/** 
     * Ensure that you create a .NET project that uses  
     * MS Visual Studio 2008 and version 3.5 of the .NET 
     * framework. This is required to invoke a  
     * AEM Forms service using MTOM. 
     * 
     * For information, see "Invoking AEM Forms using MTOM" in Programming with AEM forms   
     */ 
 using System; 
 using System.Collections.Generic; 
 using System.Linq; 
 using System.Text; 
 using System.ServiceModel; 
 using System.IO; 
  
 //A reference to the Signature service  
 using SignInteractiveForm.ServiceReference1; 
  
 //A reference to the Forms service  
 using SignInteractiveForm.ServiceReference2; 
  
 namespace SignInteractiveForm 
 { 
        class Program 
        { 
            static void Main(string[] args) 
            { 
                try 
                { 
                    //Because BLOB objects are used in both service references 
                    //it is necessary to fully-qualify the BLOB objects 
  
                    //Retrieve the form -- invoke the Forms service 
                    SignInteractiveForm.ServiceReference2.BLOB formData = GetForm(); 
  
                    //Create a BLOB object associated with the Signature service 
                    SignInteractiveForm.ServiceReference1.BLOB sigData = new SignInteractiveForm.ServiceReference1.BLOB(); 
  
                    //Transfer the byte stream from one Forms BLOB object to the  
                    //Signature BLOB object 
                    sigData.MTOM = formData.MTOM; 
  
                    //Sign the Form -- invoke the Signature service 
                    SignForm(sigData); 
                } 
                catch (Exception ee) 
                { 
                    Console.WriteLine(ee.Message); 
                } 
            } 
  
            //Creates an interactive PDF form based on a XFA form - invoke the Forms service 
            private static SignInteractiveForm.ServiceReference2.BLOB GetForm() 
            { 
  
                try 
                { 
                    //Create a FormsServiceClient object 
                    FormsServiceClient formsClient = new FormsServiceClient(); 
                    formsClient.Endpoint.Address = new System.ServiceModel.EndpointAddress("https://hiro-xp:8080/soap/services/FormsService?blob=mtom"); 
  
                    //Enable BASIC HTTP authentication 
                    BasicHttpBinding b = (BasicHttpBinding)formsClient.Endpoint.Binding; 
                    b.MessageEncoding = WSMessageEncoding.Mtom; 
                    formsClient.ClientCredentials.UserName.UserName = "administrator"; 
                    formsClient.ClientCredentials.UserName.Password = "password"; 
                    b.Security.Transport.ClientCredentialType = HttpClientCredentialType.Basic; 
                    b.Security.Mode = BasicHttpSecurityMode.TransportCredentialOnly; 
                    b.MaxReceivedMessageSize = 2000000; 
                    b.MaxBufferSize = 2000000; 
                    b.ReaderQuotas.MaxArrayLength = 2000000; 
  
                    //Create a BLOB to store form data 
                    SignInteractiveForm.ServiceReference2.BLOB formData = new SignInteractiveForm.ServiceReference2.BLOB(); 
                    SignInteractiveForm.ServiceReference2.BLOB pdfForm = new SignInteractiveForm.ServiceReference2.BLOB(); 
  
                    //Specify a XML form data 
                    string path = "C:\\Adobe\Loan.xml"; 
                    FileStream fs = new FileStream(path, FileMode.Open); 
  
                    //Get the length of the file stream  
                    int len = (int)fs.Length; 
                    byte[] ByteArray = new byte[len]; 
  
                    fs.Read(ByteArray, 0, len); 
                    formData.MTOM = ByteArray; 
  
                    //Specify a XML form data 
                    string path2 = "C:\\Adobe\LoanSigXFA.pdf"; 
                    FileStream fs2 = new FileStream(path2, FileMode.Open); 
  
                    //Get the length of the file stream  
                    int len2 = (int)fs2.Length; 
                    byte[] ByteArray2 = new byte[len2]; 
  
                    fs2.Read(ByteArray2, 0, len2); 
                    pdfForm.MTOM = ByteArray2; 
  
                    PDFFormRenderSpec renderSpec = new PDFFormRenderSpec(); 
                    renderSpec.generateServerAppearance = true; 
  
                    //Set out parameter values 
                    long pageCount = 1; 
                    String localValue = "en_US"; 
                    FormsResult result = new FormsResult(); 
  
                    //Render an interactive PDF form 
                    formsClient.renderPDFForm2( 
                        pdfForm, 
                        formData, 
                        renderSpec, 
                        null, 
                        null, 
                        out pageCount, 
                        out localValue, 
                        out result); 
  
                    //Write the data stream to the BLOB object 
                    SignInteractiveForm.ServiceReference2.BLOB outForm = result.outputContent; 
                    return outForm; 
                } 
                catch (Exception ee) 
                { 
                    Console.WriteLine(ee.Message); 
                } 
                return null; 
            } 
  
            //Sign the form -- invoke the Signature service 
            private static void SignForm(SignInteractiveForm.ServiceReference1.BLOB inDoc) 
            { 
  
                try 
                { 
                    //Create a SignatureServiceClient object 
                    SignatureServiceClient signatureClient = new SignatureServiceClient(); 
                    signatureClient.Endpoint.Address = new System.ServiceModel.EndpointAddress("https://hiro-xp:8080/soap/services/SignatureService?blob=mtom"); 
  
                    //Enable BASIC HTTP authentication 
                    BasicHttpBinding b = (BasicHttpBinding)signatureClient.Endpoint.Binding; 
                    b.MessageEncoding = WSMessageEncoding.Mtom; 
                    signatureClient.ClientCredentials.UserName.UserName = "administrator"; 
                    signatureClient.ClientCredentials.UserName.Password = "password"; 
                    b.Security.Transport.ClientCredentialType = HttpClientCredentialType.Basic; 
                    b.Security.Mode = BasicHttpSecurityMode.TransportCredentialOnly; 
                    b.MaxReceivedMessageSize = 2000000; 
                    b.MaxBufferSize = 2000000; 
                    b.ReaderQuotas.MaxArrayLength = 2000000; 
  
                    //Specify the name of the signature field 
                    string fieldName = "form1[0].grantApplication[0].page1[0].SignatureField1[0]"; 
  
                    //Create a Credential object 
                    Credential myCred = new Credential(); 
                    myCred.alias = "secure"; 
  
                    //Specify the reason to sign the document 
                    string reason = "The document was reviewed"; 
  
                    //Specify the location of the signer 
                    string location = "New York HQ"; 
  
                    //Specify contact information 
                    string contactInfo = "Tony Blue"; 
  
                    //Create a PDFSignatureAppearanceOptions object  
                    //and show date information 
                    PDFSignatureAppearanceOptionSpec appear = new PDFSignatureAppearanceOptionSpec(); 
                    appear.showDate = true; 
  
                    //Sign the PDF document 
                    SignInteractiveForm.ServiceReference1.BLOB signedDoc = signatureClient.sign( 
                        inDoc, 
                        fieldName, 
                        myCred, 
                        HashAlgorithm.SHA1, 
                        reason, 
                        location, 
                        contactInfo, 
                        appear, 
                        true, 
                        null, 
                        null, 
                        null); 
  
                    //Populate a byte array with BLOB data that represents the signed form 
                    byte[] outByteArray = signedDoc.MTOM; 
  
                    //Save the signed PDF document 
                    string fileName = "C:\\Adobe\LoanXFASigned.pdf"; 
                    FileStream fs2 = new FileStream(fileName, FileMode.OpenOrCreate); 
  
                    //Create a BinaryWriter object 
                    BinaryWriter w = new BinaryWriter(fs2); 
                    w.Write(outByteArray); 
                    w.Close(); 
                    fs2.Close(); 
                } 
  
                catch (Exception ee) 
                { 
                    Console.WriteLine(ee.Message); 
                } 
            } 
        } 
 } 
  
 
```

### 文字で始まるサービスは無効なプロキシファイルを生成します {#services-starting-with-the-letter-i-produce-invalid-proxy-files}

Microsoft .Net 3.5 および WCF を使用する際に、AEM Formsで生成された一部のプロキシクラスの名前が正しくありません。 この問題は、IBMFilenetContentRepositoryConnector、IDPSchedulerService、または名前が文字 I で始まる他のサービスに対してプロキシクラスが作成された場合に発生します。例えば、IBMFileNetContentRepositoryConnector の場合、生成されたクライアントの名前などです `BMFileNetContentRepositoryConnectorClient`. 生成されたプロキシクラスに文字 I がありません。
