---
title: フォームデータの計算
seo-title: Calculating Form Data
description: Formsサービスを使用して、ユーザーがフォームに入力し、結果を表示する値を計算します。 Formsサービスは、Java API および Web サービス API を使用して値を計算します。
seo-description: Use the Forms service to calculate values that a user enters into a form and display the results. Forms service calculates the values using the Java API and Web Service API.
uuid: ccd85bc7-8ccc-44d9-9424-dfc1f603e688
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: operations
discoiquuid: b4f57e42-60a6-407d-9764-15a11615827d
role: Developer
exl-id: 476b1c78-8332-4a79-93dc-a615ec58abbe
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '1853'
ht-degree: 2%

---

# フォームデータの計算 {#calculating-form-data}

Formsサービスでは、ユーザーがフォームに入力した値を計算し、結果を表示することができます。 フォームデータを計算するには、2 つのタスクを実行する必要があります。 まず、フォームデータを計算するフォームデザインスクリプトを作成します。 フォームデザインは、3 種類のスクリプトをサポートしています。 1 つのスクリプトタイプはクライアントで実行され、もう 1 つはサーバーで実行され、3 つ目はサーバーとクライアントの両方で実行されます。 このトピックで説明するスクリプトタイプは、サーバー上で実行されます。 HTML、PDF、フォームガイド（非推奨）の変換では、サーバー側の計算がサポートされています。

フォームデザインプロセスの一環として、演算とスクリプトを使用して、より豊富なユーザーエクスペリエンスを提供できます。 演算とスクリプトは、ほとんどのフォームフィールドとオブジェクトに追加できます。 ユーザーがインタラクティブフォームに入力したデータに対して計算操作を実行するには、フォームデザインスクリプトを作成する必要があります。

ユーザーがフォームに値を入力し、「計算」ボタンをクリックして結果を表示します。 次のプロセスは、ユーザーがデータを計算できるサンプル・アプリケーションを示しています。

* ユーザーが、WebHTMLの開始ページとして機能する StartLoan.html という名前のアプリケーションページにアクセスします。 このページは、という名前の Java サーブレットを呼び出します `GetLoanForm`.
* この `GetLoanForm` サーブレットは、ローンフォームをレンダリングします。 このフォームには、スクリプト、インタラクティブフィールド、計算ボタンおよび送信ボタンが含まれています。
* ユーザーがフォームのフィールドに値を入力し、「計算」ボタンをクリックします。 フォームが `CalculateData` スクリプトが実行される Java サーブレット。 計算結果がフォームに表示された状態で、フォームがユーザーに送り返されます。
* ユーザは満足のいく結果が表示されるまで値の入力と計算を続けます。 確認が完了したら、ユーザーは「送信」ボタンをクリックしてフォームを処理します。 フォームは、という名前の別の Java サーブレットに送信されます。 `ProcessForm` 送信されたデータを取得する役割を持つ ( [送信済みFormsの処理](/help/forms/developing/rendering-forms.md#handling-submitted-forms).)

次の図に、アプリケーションのロジック・フローを示します。

![cf_cf_finsrv_loancalcapp_v1](assets/cf_cf_finsrv_loancalcapp_v1.png)

次の表に、この図の手順を示します。

<table> 
 <thead>
  <tr> 
   <th><p>手順</p></th> 
   <th><p>説明</p></th> 
  </tr> 
 </thead>
 <tbody>
  <tr> 
   <td><p>1</p></td> 
   <td><p>この <code>GetLoanForm</code> Java サーブレットは、HTML開始ページから呼び出されます。 </p></td> 
  </tr> 
  <tr> 
   <td><p>2</p></td> 
   <td><p>この <code>GetLoanForm</code> Java サーブレットは、Forms service Client API を使用して、ローンフォームをクライアント Web ブラウザーにレンダリングします。 サーバー上で実行するように設定されたスクリプトを含むフォームをレンダリングする場合と、スクリプトを含まないフォームをレンダリングする場合の違いは、スクリプトの実行に使用するターゲットの場所を指定する必要がある点です。 ターゲットの場所が指定されていない場合、サーバー上で実行するように設定されたスクリプトは実行されません。 例えば、この節で紹介するアプリケーションについて考えてみましょう。 この <code>CalculateData</code> Java サーブレットは、スクリプトが実行されるターゲットの場所です。</p></td> 
  </tr> 
  <tr> 
   <td><p>3</p></td> 
   <td><p>ユーザーがインタラクティブフィールドにデータを入力し、「計算」ボタンをクリックします。 フォームが <code>CalculateData</code> Java サーブレット。スクリプトが実行されます。 </p></td> 
  </tr> 
  <tr> 
   <td><p>4</p></td> 
   <td><p>計算結果がフォームに表示された状態で、フォームが Web ブラウザーにレンダリングされます。 </p></td> 
  </tr> 
  <tr> 
   <td><p>5</p></td> 
   <td><p>ユーザーは、値が満足できる場合に「送信」ボタンをクリックします。 フォームは、という名前の別の Java サーブレットに送信されます。 <code>ProcessForm</code>.</p></td> 
  </tr> 
 </tbody> 
</table>

通常、PDFコンテンツとして送信されるフォームには、クライアントで実行されるスクリプトが含まれます。 ただし、サーバー側の計算を実行することもできます。 「送信」ボタンは、スクリプトの計算には使用できません。 この場合、Formsサービスはインタラクションが完了すると見なすので、計算は実行されません。

フォームデザインスクリプトの使用方法を説明するために、この節では、サーバー上で実行するように設定されたスクリプトを含むシンプルなインタラクティブフォームを調べます。 次の図に示すスクリプトを含むフォームデザインを示します。このスクリプトによって、ユーザーが最初の 2 つのフィールドに入力し、その結果を 3 番目のフィールドに表示します。

![cf_cf_caldata](assets/cf_cf_caldata.png)

**A.** NumericField1 という名前のフィールド **B.** NumericField2 という名前のフィールド **C.** NumericField3 という名前のフィールド

このフォームデザインに配置されるスクリプトの構文は次のとおりです。

```as3
     NumericField3 = NumericField2 + NumericField1
```

このフォームデザインでは、「計算」ボタンはコマンドボタンで、スクリプトはこのボタンの `Click` イベント。 ユーザーが最初の 2 つのフィールド（NumericField1 および NumericField2）に値を入力し、「計算」ボタンをクリックすると、フォームがFormsサービスに送信され、スクリプトが実行されます。 Formsサービスは、NumericField3 フィールドに表示された計算結果を使用して、フォームをクライアントデバイスにレンダリングし直します。

>[!NOTE]
>
>フォームデザインスクリプトの作成について詳しくは、 [Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63).

>[!NOTE]
>
>Formsサービスについて詳しくは、 [AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63).

## 手順の概要 {#summary-of-steps}

フォームデータを計算するには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. Forms Client API オブジェクトを作成します。
1. 計算スクリプトを含むフォームを取得します。
1. フォームデータストリームをクライアントの Web ブラウザーに書き戻します

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。 Web サービスを使用している場合は、プロキシファイルを必ず含めてください。

**Forms Client API オブジェクトの作成**

Forms Service Client API 操作をプログラムで実行する前に、Formsサービスクライアントを作成する必要があります。 Java API を使用している場合は、 `FormsServiceClient` オブジェクト。 Forms Web サービス API を使用している場合は、 `FormsServiceService` オブジェクト。

**計算スクリプトを含むフォームの取得**

Forms Service Client API を使用して、サーバー上で実行するように設定されたスクリプトを含むフォームを処理するアプリケーションロジックを作成します。 このプロセスは、送信されたフォームの処理に似ています。 ( [送信済みFormsの処理](/help/forms/developing/handling-submitted-forms.md).)

送信されたフォームに関連付けられている処理状態が `1` `(Calculate)`：つまり、Formsサービスはフォームデータに対して計算操作を実行しており、結果をユーザーに書き戻す必要があります。 この場合、サーバー上で実行するように設定されたスクリプトが自動的に実行されます。

**フォームデータストリームをクライアントの Web ブラウザーに書き戻します**

送信されたフォームに関連付けられている処理状態が `1`の場合は、結果をクライアント Web ブラウザーに書き戻す必要があります。 フォームが表示されると、計算された値が適切なフィールドに表示されます。

**関連トピック**

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Forms Service API クイックスタート](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[インタラクティブPDF formsのレンダリング](/help/forms/developing/rendering-interactive-pdf-forms.md)

[Formsをレンダリングする Web アプリケーションの作成](/help/forms/developing/creating-web-applications-renders-forms.md)

## Java API を使用してフォームデータを計算する {#calculate-form-data-using-the-java-api}

Forms API(Java) を使用してフォームデータを計算します。

1. プロジェクトファイルを含める

   Java プロジェクトのクラスパスに、adobe-forms-client.jar などのクライアント JAR ファイルを含めます。

1. Forms Client API オブジェクトの作成

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * の作成 `FormsServiceClient` オブジェクトのコンストラクタを使用し、 `ServiceClientFactory` オブジェクト。

1. 計算スクリプトを含むフォームの取得

   * 計算スクリプトを含むフォームデータを取得するには、 `com.adobe.idp.Document` オブジェクトのコンストラクタを使用して、 `javax.servlet.http.HttpServletResponse` オブジェクトの `getInputStream` メソッドをコンストラクタ内から呼び出します。
   * を呼び出す `FormsServiceClient` オブジェクトの `processFormSubmission` メソッドを使用して、次の値を渡します。

      * この `com.adobe.idp.Document` フォームデータを格納するオブジェクト。
      * 関連するすべての HTTP ヘッダーを含む環境変数を指定する string 値。 処理するコンテンツタイプを指定するには、 `CONTENT_TYPE` 環境変数。 例えば、XML データとPDFデータを処理するには、このパラメーターに次の文字列値を指定します。 `CONTENT_TYPE=application/xml&CONTENT_TYPE=application/pdf`
      * 次を指定する string 値 `HTTP_USER_AGENT` ヘッダー値；例： `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`.
      * A `RenderOptionsSpec` 実行時オプションを保存するオブジェクト。

      この `processFormSubmission` メソッドは、 `FormsResult` フォーム送信の結果を含むオブジェクト。

   * 送信されたフォームに関連付けられている処理状態が `1` を呼び出すことによって `FormsResult` オブジェクトの `getAction` メソッド。 このメソッドが値を返す場合 `1`を含めると、計算が実行され、データをクライアントの Web ブラウザーに書き戻すことができます。


1. フォームデータストリームをクライアントの Web ブラウザーに書き戻します

   * の作成 `javax.servlet.ServletOutputStream` フォームデータストリームをクライアントの Web ブラウザーに送信するために使用するオブジェクト。
   * の作成 `com.adobe.idp.Document` を呼び出すことによってオブジェクトを取得 `FormsResult` オブジェクト `getOutputContent` メソッド。
   * の作成 `java.io.InputStream` を呼び出すことによってオブジェクトを取得 `com.adobe.idp.Document` オブジェクトの `getInputStream` メソッド。
   * バイト配列を作成し、 `InputStream` オブジェクトの `read` メソッドを使用し、バイト配列を引数として渡す。
   * を呼び出す `javax.servlet.ServletOutputStream` オブジェクトの `write` メソッドを使用して、フォームデータストリームをクライアント Web ブラウザーに送信します。 バイト配列を `write` メソッド。

**関連トピック**

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Web サービス API を使用してフォームデータを計算する {#calculate-form-data-using-the-web-service-api}

Forms API（Web サービス）を使用してフォームデータを計算します。

1. プロジェクトファイルを含める

   * Forms Service WSDL を使用する Java プロキシクラスを作成します。
   * Java プロキシクラスをクラスパスに含めます。

1. Forms Client API オブジェクトの作成

   の作成 `FormsService` オブジェクトを選択し、認証値を設定します。

1. 計算スクリプトを含むフォームの取得

   * Java サーブレットに投稿されたフォームデータを取得するには、 `BLOB` オブジェクトを指定します。
   * の作成 `java.io.InputStream` オブジェクトを `javax.servlet.http.HttpServletResponse` オブジェクトの `getInputStream` メソッド。
   * の作成 `java.io.ByteArrayOutputStream` オブジェクトのコンストラクタを使用し、 `java.io.InputStream` オブジェクト。
   * の内容をコピーします。 `java.io.InputStream` オブジェクトを `java.io.ByteArrayOutputStream` オブジェクト。
   * を呼び出してバイト配列を作成する `java.io.ByteArrayOutputStream` オブジェクトの `toByteArray` メソッド。
   * 次の項目に `BLOB` オブジェクトを呼び出す `setBinaryData` メソッドを使用し、バイト配列を引数として渡す。
   * コンストラクタを使用して `RenderOptionsSpec` オブジェクトを作成します。を呼び出してロケール値を設定します。 `RenderOptionsSpec` オブジェクトの `setLocale` メソッドを使用して、ロケール値を指定する string 値を渡す。
   * を呼び出す `FormsServiceClient` オブジェクトの `processFormSubmission` メソッドを使用して、次の値を渡します。

      * この `BLOB` フォームデータを格納するオブジェクト。
      * 環境変数を指定する string 値に、関連するすべての HTTP ヘッダーが含まれていました。 例えば、次の文字列値を指定できます。 `HTTP_REFERER=referrer&HTTP_CONNECTION=keep-alive&CONTENT_TYPE=application/xml`
      * 次を指定する string 値 `HTTP_USER_AGENT` ヘッダー値；例： `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`.
      * A `RenderOptionsSpec` 実行時オプションを保存するオブジェクト。 その他の情報, .
      * 空 `BLOBHolder` メソッドによって設定されるオブジェクト。
      * 空 `javax.xml.rpc.holders.StringHolder` メソッドによって設定されるオブジェクト。
      * 空 `BLOBHolder` メソッドによって設定されるオブジェクト。
      * 空 `BLOBHolder` メソッドによって設定されるオブジェクト。
      * 空 `javax.xml.rpc.holders.ShortHolder` メソッドによって設定されるオブジェクト。
      * 空 `MyArrayOf_xsd_anyTypeHolder` メソッドによって設定されるオブジェクト。 このパラメーターは、フォームと共に送信される添付ファイルを保存するために使用されます。
      * 空 `FormsResultHolder` 送信されるフォームを使用してメソッドによって入力されるオブジェクト。

      この `processFormSubmission` メソッドによって `FormsResultHolder` パラメーターとフォーム送信の結果。 この `processFormSubmission` メソッドは、 `FormsResult` フォーム送信の結果を含むオブジェクト。

   * 送信されたフォームに関連付けられている処理状態が `1` を呼び出すことによって `FormsResult` オブジェクトの `getAction` メソッド。 このメソッドが値を返す場合 `1`を含めると、計算が実行され、データをクライアントの Web ブラウザーに書き戻すことができます。


1. フォームデータストリームをクライアントの Web ブラウザーに書き戻します

   * の作成 `javax.servlet.ServletOutputStream` フォームデータストリームをクライアントの Web ブラウザーに送信するために使用するオブジェクト。
   * の作成 `BLOB` を呼び出してフォームデータを含むオブジェクト `FormsResult` オブジェクトの `getOutputContent` メソッド。
   * バイト配列を作成し、 `BLOB` オブジェクトの `getBinaryData` メソッド。 このタスクは、 `FormsResult` オブジェクトをバイト配列に変換します。
   * を呼び出す `javax.servlet.http.HttpServletResponse` オブジェクトの `write` メソッドを使用して、フォームデータストリームをクライアント Web ブラウザーに送信します。 バイト配列を `write` メソッド。

**関連トピック**

[Base64 エンコーディングを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
