---
title: REST リクエストを使用したAEM Formsの呼び出し
seo-title: Invoking AEM Forms using REST Requests
description: REST リクエストを使用して、Workbench で作成されたプロセスを呼び出します。
seo-description: Invoke processes created in Workbench using REST requests.
uuid: 3a19a296-f3fe-4e50-9143-b68aed37f9ef
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: coding
discoiquuid: df7b60bb-4897-479e-a05e-1b1e9429ed87
role: Developer
exl-id: 82770ac6-aafc-44b9-82fb-6f193bb3a128
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '2492'
ht-degree: 4%

---

# REST リクエストを使用したAEM Formsの呼び出し {#invoking-aem-forms-using-rest-requests}

Representational State Transfer（REST）要求で呼び出せるように、Workbench で作成したプロセスを設定できます。REST 要求は HTML ページから送信されます。つまり、REST リクエストを使用して、Web ページから直接Formsプロセスを呼び出すことができます。 例えば、Web ページの新しいインスタンスを開くことができます。 次に、Formsプロセスを呼び出し、HTTPPDFリクエストで送信されたデータを含む、レンダリングされたPOSTドキュメントを読み込むことができます。

2 種類のHTML・クライアントが存在します。 最初のHTMLクライアントは、JavaScript で記述されたAJAXクライアントです。 2 つ目のクライアントは、送信HTMLを含むボタンフォームです。 HTMLベースのクライアントアプリケーションは、REST クライアントとして使用できる唯一のクライアントではありません。 HTTP 要求をサポートするクライアントアプリケーションは、REST 呼び出しを使用してサービスを呼び出すことができます。 例えば、サービスフォームから REST 呼び出しを使用して、サービスを呼び出すことがPDFできます。 ( [Acrobatからの MyApplication/EncryptDocument プロセスの呼び出し](#rest-invocation-examples).)

REST リクエストを使用する場合は、Formsサービスを直接呼び出さないことをお勧めします。 代わりに、Workbench で作成されたプロセスを呼び出します。 REST 呼び出し用のプロセスを作成する場合は、プログラム的なスタートポイントを使用します。 この場合、REST エンドポイントは自動的に追加されます。 Workbench でのプロセスの作成について詳しくは、 [Workbench の使用](https://www.adobe.com/go/learn_aemforms_workbench_63).

REST を使用してサービスを呼び出すと、AEM forms のユーザー名とパスワードの入力を求められます。 ただし、ユーザー名とパスワードを指定しない場合は、Service Security を無効にできます。

REST を使用してFormsサービスを呼び出す（プロセスがアクティブになるとプロセスがサービスになります）には、REST エンドポイントを設定します。 (「エンドポイントの管理」( [管理ヘルプ](https://www.adobe.com/go/learn_aemforms_admin_63).)

REST エンドポイントを設定した後、HTTPGETメソッドまたはPOSTメソッドを使用して、Formsサービスを呼び出すことができます。

```as3
 action="https://hiro-xp:8080/rest/services/[ServiceName]/[OperationName]:[ServiceVersion]" method="post" enctype="multipart/form-data"
```

必須 `ServiceName` value は、呼び出すFormsサービスの名前です。 オプション `OperationName` value はサービスの操作の名前です。 この値を指定しない場合、この名前はデフォルトでになります。 `invoke`：プロセスを開始する操作名です。 オプション `ServiceVersion` の値は、X.Y 形式でエンコードされたバージョンです。 この値を指定しない場合は、最新のバージョンが使用されます。 この `enctype` 値も `application/x-www-form-urlencoded`.

## サポートされるデータタイプ {#supported-data-types}

REST 要求を使用してAEM Formsサービスを呼び出す場合、次のデータ型がサポートされます。

* 文字列や整数などの Java プリミティブデータ型
* `com.adobe.idp.Document` データタイプ
* XML データ型（例： ） `org.w3c.Document` および `org.w3c.Element`
* コレクションオブジェクト ( 例： `java.util.List` および `java.util.Map`

   これらのデータ型は、通常、Workbench で作成されるプロセスへの入力値として受け入れられます。

   HTTPPOSTメソッドを使用して Froms サービスが呼び出された場合、引数は HTTP リクエスト本文内に渡されます。 AEM Formsサービスの署名に文字列入力パラメーターがある場合、リクエスト本文には入力パラメーターのテキスト値を含めることができます。 サービスの署名で複数の文字列パラメーターが定義されている場合、要求は HTTP の `application/x-www-form-urlencoded` フォームのフィールド名としてパラメーターの名前を使用した表記。

   Formsサービスが文字列パラメーターを返した場合、結果は出力パラメーターのテキスト表現になります。 サービスが複数の文字列パラメーターを返す場合、結果は、出力パラメーターを次の形式でエンコードする XML ドキュメントになります。
   ` <result> <output-paramater1>output-parameter-value-as-string</output-paramater1> . . . <output-paramaterN>output-parameter-value-as-string</output-paramaterN> </result>`

   >[!NOTE]
   >
   >この `output-paramater1` 値は出力パラメーター名を表します。

   Formsサービスで `com.adobe.idp.Document` パラメーターを渡す場合、サービスは HTTP 呼び出しメソッドのみを使用してPOSTできます。 サービスに必要な場合 `com.adobe.idp.Document` パラメーターを指定した場合、HTTP リクエスト本文は入力 Document オブジェクトの内容になります。

   AEM Formsサービスで複数の入力パラメーターが必要な場合、HTTP リクエスト本文は、RFC 1867 で定義されているマルチパート MIME メッセージである必要があります。 （RFC 1867 は、Web ブラウザーがファイルを Web サイトにアップロードする際に使用する標準です）。 各入力パラメーターは、マルチパートメッセージの個別の部分として送信し、 `multipart/form-data` 形式 各パーツの名前は、パラメータの名前と一致する必要があります。

   リストとマップは、Workbench で作成されるAEM Formsプロセスへの入力値としても使用されます。 その結果、REST リクエストを使用する際に、これらのデータ型を使用できます。 Java 配列は、AEM Formsプロセスの入力値として使用されていないので、サポートされていません。

   入力パラメーターがリストの場合、REST クライアントは、パラメーターを複数回指定して（リスト内の項目ごとに 1 回）送信できます。 たとえば、A がドキュメントのリストの場合、入力は A という名前の複数のパーツで構成されるマルチパートメッセージである必要があります。この場合、A という名前の各パーツは入力リストのアイテムになります。 B が文字列のリストの場合、入力値は `application/x-www-form-urlencoded` B という名前の複数のフィールドで構成されるメッセージ。この場合、B という名前の各フォームフィールドは、入力リストの項目になります。

   入力パラメーターがマップで、それがサービスのみの入力パラメーターの場合、入力メッセージのすべての部分/フィールドがマップ内のキー/値レコードになります。 各パーツまたはフィールドの名前が、レコードのキーになります。 各パーツまたはフィールドの内容が、レコードの値になります。

   入力マップがサービスのみの入力パラメータでない場合、マップに属する各キー/値レコードは、パラメータ名とレコードのキーを連結した名前のパラメータを使用して送信できます。 例えば、 `attributes` は、次のキーと値のペアのリストと共に送信できます。

   `attributesColor=red`

   `attributesShape=box`

   `attributesWidth=5`

   これは、次の 3 つのレコードのマップに変換されます。 `Color=red`, `Shape=box`、および `Width=5`.

   list 型と map 型の出力パラメーターは、結果の XML メッセージの一部になります。 出力リストは、一連の XML 要素として XML で表され、リスト内の項目ごとに 1 つの要素を持ちます。 すべての要素には、出力リストパラメーターと同じ名前が付けられます。 各 XML 要素の値は、次の 2 つのうちの 1 つです。

* リスト内の項目のテキスト表現（リストが文字列型で構成されている場合）
* ドキュメントのコンテンツを指す URL( リストが `com.adobe.idp.Document` オブジェクト )

   次の例は、という名前の出力パラメーターが 1 つあるサービスから返される XML メッセージです。 *リスト*：整数のリストです。
   ` <result>   <list>12345</list>   . . .   <list>67890</list>  </result>`出力マップパラメータは、結果の XML メッセージ内で、マップ内の各レコードに対して 1 つの要素を持つ一連の XML 要素として表されます。 すべての要素には、マップレコードのキーと同じ名前が付けられます。 各要素の値は、マップレコードの値（マップが文字列値を持つレコードで構成される場合）のテキスト表現か、ドキュメントのコンテンツを指す URL( マップが `com.adobe.idp.Document` の値 ) です。 次に、という名前の出力パラメーターが 1 つだけあるサービスが返す XML メッセージの例を示します。 `map`. このパラメータ値は、レターを関連付けるレコードから成るマップです。 `com.adobe.idp.Document` オブジェクト。
   ` <result>   http://localhost:8080/DocumentManager/docm123/4567   . . .   <Z>http://localhost:8080/DocumentManager/docm987/6543</Z>  </result>  `

## 非同期呼び出し {#asynchronous-invocations}

人間中心の長期間有効なプロセスなど、一部のAEM Formsサービスの完了には長い時間が必要です。 これらのサービスは、非ブロッキング方式で非同期で呼び出すことができます。 （[人間中心の長期間有効なプロセスの呼び出し](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes)を参照。）

AEM Formsサービスは、 `services` と `async_invoke` を呼び出し URL に含めることができます。

```as3
 http://localhost:8080/rest/async_invoke/SomeService. SomeOperation?integer_input_variable=123&string_input_variable=abc
```

この URL は、この呼び出しをおこなうジョブの識別子の値（「text/plain」形式）を返します。

非同期呼び出しのステータスは、 `services` ～で置き換えられる `async_status`. URL には、 `job_id` この呼び出しに関連付けられたジョブの識別子の値を指定するパラメーター。 次に例を示します。

```as3
 http://localhost:8080/rest/async_status/SomeService.SomeOperation?job_id=2345353443366564
```

この URL は、ジョブマネージャの仕様に従ってジョブステータスをエンコードする整数値（「text/plain」形式）を返します（例えば、2 は実行、3 は完了、4 は失敗といった意味で）。

ジョブが完了した場合、URL は、サービスが同期的に呼び出された場合と同じ結果を返します。

ジョブが完了し、結果が取得されたら、呼び出し URL を使用してジョブを破棄できます。 `services` は次の値で置き換えられます。 `async_dispose`. URL には、 `job_id` ジョブの識別子の値を指定するパラメーター。 次に例を示します。

```as3
 http://localhost:8080/rest/async_dispose/SomeService.SomeOperation?job_id=2345353443366564
```

ジョブが正常に破棄された場合、この URL は空のメッセージを返します。

## エラーレポート {#error-reporting}

サーバーで例外がスローされているために同期または非同期の呼び出し要求を完了できない場合、HTTP 応答メッセージの一部として例外がレポートされます。 呼び出し URL ( または `async_result` （非同期呼び出しの場合の URL）に.xml サフィックスが付かない場合、REST プロバイダーは HTTP コードを返します `500 Internal Server Error` その後に例外メッセージが続きます。

呼び出し URL ( または `async_result` （非同期呼び出しの場合の URL）に.xml サフィックスが付いている場合、REST プロバイダーは HTTP コードを返します `200 OK`その後に、次の形式の例外を説明する XML ドキュメントが続きます。

```as3
 <exception> 
       <exception_class_name>[ 
       <DSCError> 
          <componentUID>component_UUD</componentUID> 
         <errorCode>error_code</errorCode> 
         <minorCode>minor_code</minorCode> 
         <message>error_message</message> 
       </DSCError> 
 ]  
       <message>exception_message</message> 
     <stackTrace>exception_stack_trace</stackTrace> 
       </exception_class_name> 
     <exception> 
       </exception> 
 </exception>
```

この `DSCError` 要素はオプションで、例外がのインスタンスの場合にのみ存在します。 `com.adobe.idp.dsc.DSCException`.

## セキュリティと認証 {#security-and-authentication}

安全なトランスポートで REST の呼び出しを行うために、AEM forms 管理者は、AEM Formsをホストする J2EE アプリケーションサーバーで HTTPS プロトコルを有効にすることができます。 この設定は、J2EE アプリケーションサーバーに固有です。forms サーバー設定には含まれていません。

>[!NOTE]
>
>REST エンドポイントを介してプロセスを公開する Workbench 開発者は、XSS の脆弱性の問題に注意してください。 XSS 脆弱性は、Cookie の盗用や操作、コンテンツの表示の変更、機密情報の侵害に使用できます。 XSS の脆弱性が問題の場合は、追加の入出力データ検証ルールを使用してプロセスロジックを拡張することをお勧めします。

## REST 呼び出しをサポートするAEM Formsサービス {#aem-forms-services-that-support-rest-invocation}

サービスを直接呼び出すのではなく、Workbench を使用して作成したプロセスを呼び出すことをお勧めしますが、REST 呼び出しをサポートするAEM Formsサービスがいくつかあります。 サービスとは異なり、プロセスを直接呼び出すことをお勧めする理由は、プロセスを呼び出す方がより効率的なためです。 次のシナリオについて考えてみましょう。 REST クライアントからポリシーを作成するとします。 つまり、REST クライアントで、ポリシー名、オフラインリース期間などの値を定義する必要があります。

ポリシーを作成するには、次のような複雑なデータ型を定義する必要があります `PolicyEntry` オブジェクト。 A `PolicyEntry` オブジェクトは、ポリシーに関連付けられた権限などの属性を定義します。 ( [ポリシーの作成](/help/forms/developing/protecting-documents-policies.md#creating-policies).)

ポリシーを作成するために REST リクエストを送信する代わりに ( ポリシーには、 `PolicyEntry` オブジェクトを参照 )、Workbench を使用してポリシーを作成するプロセスを作成します。 プロセス名を定義する文字列値や、オフラインリース期間を定義する整数など、プリミティブ入力変数を受け入れるプロセスを定義します。

この方法では、操作に必要な複雑なデータ型を含む REST 呼び出しリクエストを作成する必要はありません。 プロセスは複雑なデータ型を定義し、REST クライアントから実行する操作は、プロセスを呼び出し、プリミティブデータ型を渡すだけです。 REST を使用したプロセスの呼び出しについて詳しくは、 [REST を使用した MyApplication/EncryptDocument プロセスの呼び出し](#rest-invocation-examples).

次のリストで、直接 REST 呼び出しをサポートするAEM Formsサービスを指定します。

* Distiller サービス[Distiller さーびす]
* Rights Management サービス[Rights Management さーびす]
* GeneratePDF サービス
* Generate3dPDF サービス
* FormDataIntegration

## REST 呼び出しの例 {#rest-invocation-examples}

次の REST 呼び出し例が提供されています。

* AEM Formsプロセスにブール値を渡す
* AEM Formsプロセスに日付値を渡す
* ドキュメントをAEM Formsプロセスに渡す
* AEM Formsプロセスにドキュメントとテキスト値を渡す
* 列挙値をAEM Formsプロセスに渡す
* REST を使用した MyApplication/EncryptDocument プロセスの呼び出し
* Acrobatからの MyApplication/EncryptDocument プロセスの呼び出し

   各例では、様々なデータ型をAEM Formsプロセスに渡す方法を示しています

**プロセスにブール値を渡す**

次のHTMLの例では、2 つの `Boolean` 次の名前のAEM Formsプロセスの値： `RestTest2`. 呼び出しメソッドの名前は、 `invoke` バージョンは 1.0 です。Version Post メソッドが使用されていることに注意してください。

```as3
 <html> 
 <body> 
  
 <form name="input" action="http://localhost:9080/rest/services/RestTest2/invoke/1.0" method="post"> 
  
 Boolean 1: <input type="text" name="inBooleanList" value="true"> 
 Boolean 2: <input type="text" name="inBooleanList" value="false"> 
 <input type="submit" value="Submit"> 
  
 </form> 
  
 </body> 
 </html>
```

**プロセスに日付値を渡す**

次のHTMLの例では、という名前のAEM Formsプロセスに日付値を渡します。 `SOAPEchoService`. 呼び出しメソッドの名前は、 `echoCalendar`. HTML `Post` メソッドが使用されます。

```as3
 <html> 
 <body> 
  
 <form name="input" action="http://localhost:9080/rest/services/SOAPEchoService/echoCalendar" method="post"> 
  
 Date: <input type="text" name="value-to-echo" value="2009-01-02T12:15:30Z"> 
 <input type="submit" value="Submit"> 
  
 </form> 
  
 </body> 
 </html>
```

**プロセスにドキュメントを渡す**

次のHTML例は、という名前のAEM Formsプロセスを呼び出します。 `MyApplication/EncryptDocument` にはPDF文書が必要。 このプロセスについて詳しくは、 [MTOM を使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom).

```as3
 <html> 
 <body> 
  
 <form name="input" action="http://localhost:9080/rest/services/MyApplication/EncryptDocument/invoke" method="post"  
          enctype="multipart/form-data"> 
  
 File: <input type="file" name="value-to-echo"> 
 <input type="submit" value="Submit"/> 
  
 </form> 
  
 </body> 
 </html>
```

**プロセスにドキュメントとテキストの値を渡す**

次のHTML例は、という名前のAEM Formsプロセスを呼び出します。 `RestTest3` ドキュメントと 2 つのテキスト値が必要です。 Post メソッドが使用されていることにHTML。

```as3
 <html> 
 <body> 
  
 <form name="input" action="http://localhost:9080/rest/services/RestTest3" method="post"  
          enctype="multipart/form-data"> 
  
 Doc: <input type="file" name="inDoc"> 
 String 1: <input type="text" name="inListOfStrings" value="hello"> 
 String 2: <input type="text" name="inListOfStrings" value="privet"> 
 <input type="submit" value="Submit"/> 
  
 </form> 
  
 </body> 
 </html>
```

**プロセスに列挙値を渡す**

次のHTML例は、という名前のAEM Formsプロセスを呼び出します。 `SOAPEchoService` 列挙値が必要です。 Post メソッドが使用されていることにHTML。

```as3
 <html> 
 <body> 
  
 <form name="input" action="https://hiro-xp:8080/rest/services/SOAPEchoService/echoEnum" method="post"> 
  
 Color Enum Value: <input type="text" name="value-to-echo" value="green"> 
 <input type="submit" value="Submit"> 
  
 </form> 
  
 </body> 
 </html>
```

**REST を使用した MyApplication/EncryptDocument プロセスの呼び出し**

という名前の短時間のみ有効なAEM Formsプロセスを呼び出すことができます。 *MyApplication/EncryptDocument* REST を使用します。

>[!NOTE]
>
>このプロセスは、既存の AEM Forms プロセスに基づいていません。コード例に従うには、という名前のプロセスを作成します。 `MyApplication/EncryptDocument` workbench の使用 （[Workbench の使用](https://www.adobe.com/go/learn_aemforms_workbench_63)を参照。）

このプロセスを呼び出すと、次のアクションが実行されます。

1. プロセスに渡された保護されていない PDF ドキュメントを取得します。このアクションは `SetValue` 操作に基づいています。このプロセスの入力パラメーターは、`document` という名前の `inDoc` プロセス変数です。
1. PDF ドキュメントをパスワードで暗号化します。このアクションは `PasswordEncryptPDF` 操作に基づいています。パスワードで暗号化された PDF ドキュメントは、`outDoc` という名前のプロセス変数として返されます。

   このプロセスが REST リクエストを使用して呼び出されると、暗号化されたPDFドキュメントが Web ブラウザーに表示されます。 パスワードドキュメントを表示する前に、PDFを指定します（セキュリティが無効になっていない場合）。 次のHTMLコードは、 `MyApplication/EncryptDocument` プロセス。

   ```as3
    <html> 
    <body> 
    <form action="https://hiro-xp:8080/rest/services/MyApplication/EncryptDocument" method="post" enctype="multipart/form-data"> 
         <p>Chose a PDF file (.pdf) to send to the EncryptDocument process.</p> 
         <p>file: 
           <input type="file" name="inDoc" /> 
         </p> 
         <p> 
           <input type="submit"/> 
         </p> 
    </form> 
    </body>
   ```

**Acrobatからの MyApplication/EncryptDocument プロセスの呼び出し** {#invoke-process-acrobat}

REST リクエストを使用して、AcrobatからFormsプロセスを呼び出すことができます。 例えば、 *MyApplication/EncryptDocument* プロセス。 AcrobatからFormsプロセスを呼び出すには、Designer 内の XDP ファイルに送信ボタンを配置します。 （「[Designer ヘルプ](https://www.adobe.com/go/learn_aemforms_designer_63)」を参照）。

ボタンの *URL に送信* フィールドに含まれます。

プロセスを呼び出すための完全な URL はhttps://hiro-xp:8080/rest/services/MyApplication/EncryptDocumentです。

プロセスでPDFドキュメントを入力値として必要とする場合は、前の図に示すように、必ずPDFとしてフォームを送信してください。 また、プロセスを正常に呼び出すには、プロセスがPDFドキュメントを返す必要があります。 そうしないと、Acrobat は戻り値を処理できず、エラーが発生します。 入力プロセス変数の名前を指定する必要はありません。 例えば、MyApplication/EncryptDocument*プロセスには、という名前の入力変数があります。 `inDoc`. フォームがPDFとして送信されている限り、inDoc を指定する必要はありません。

また、フォームデータを XML としてFormsプロセスに送信する場合も、XML データを送信する場合は、 `Submit As` ドロップダウンで XML を指定します。 プロセスの戻り値はPDFドキュメントである必要があるので、PDFドキュメントはAcrobatに表示されます。
