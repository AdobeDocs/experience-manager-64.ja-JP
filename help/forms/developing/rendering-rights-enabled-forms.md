---
title: レンダリング権限が有効なForms
seo-title: Rendering Rights-Enabled Forms
description: Formsサービスを使用して、使用権限が適用されているフォームをレンダリングします。 Java API および Web サービス API を使用して、権限が有効なフォームをレンダリングできます。
seo-description: Use the Forms service to render forms that have usage rights applied to them. You can render rights-enabled forms using the Java API and Web Service API.
uuid: ce5e4be6-d9b0-4989-a0e1-a8c3b98aed77
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: operations
discoiquuid: d4c2b2f0-613a-409d-b39b-8e37fdb96eea
role: Developer
exl-id: 0cee94ba-1a72-4021-b606-8fa945312483
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '1463'
ht-degree: 5%

---

# レンダリング権限が有効なForms {#rendering-rights-enabled-forms}

Formsサービスは、使用権限が適用されているフォームをレンダリングできます。 使用権限は、Acrobat ではデフォルトで利用できるが Adobe Reader では利用できない機能（フォームにコメントを追加する機能や、フォームフィールドにデータを入力してフォームを保存する機能など）に関連しています。使用権限が適用されているFormsは、権限が有効なフォームと呼ばれます。 Adobe Readerで権限が付与されたフォームを開いたユーザーは、そのフォームに対して有効な操作を実行できます。

使用権限をフォームに適用するには、 Acrobat Reader DC Extensions サービスがAEM forms インストールに含まれている必要があります。 また、使用権限をPDF・ドキュメントに適用できる有効な資格情報が必要です。 つまり、権限が有効なフォームをレンダリングする前に、Acrobat Reader DC Extensions サービスを適切に設定する必要があります。 ( [Acrobat Reader DC Extensions Service について](/help/forms/developing/assigning-usage-rights.md#about-the-acrobat-reader-dc-extensions-service).)

>[!NOTE]
>
>使用権限を含むフォームをレンダリングするには、XDP ファイルを入力として使用し、PDFファイルを使用しないでください。 PDFファイルを入力として使用した場合、フォームは引き続きレンダリングされます。ただし、権限が有効なフォームにはなりません。

>[!NOTE]
>
>次の使用権限を指定する場合、XML データを使用してフォームに事前入力することはできません。 `enableComments`, `enableCommentsOnline`, `enableEmbeddedFiles`または `enableDigitalSignatures`. ( [編集可能なレイアウトを使用したFormsの事前入力](/help/forms/developing/prepopulating-forms-flowable-layouts.md).)

>[!NOTE]
>
>Formsサービスについて詳しくは、 [AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63).

## 手順の概要 {#summary-of-steps}

権限が有効なフォームをレンダリングするには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. Forms Client API オブジェクトを作成します。
1. 使用権限の実行時オプションを設定します。
1. 権限が有効なフォームをレンダリングします。
1. 権限が有効なフォームをクライアントの Web ブラウザーに書き込みます。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。 Web サービスを使用している場合は、プロキシファイルを必ず含めてください。

**Forms Client API オブジェクトの作成**

Forms Service Client API 操作をプログラムで実行する前に、Formsサービスクライアントを作成する必要があります。

**使用権限の実行時オプションを設定する**

使用権限を有効にしたフォームをレンダリングするには、使用権限の実行時オプションを設定する必要があります。 また、使用権限をフォームに適用するために使用する秘密鍵証明書のエイリアスも指定する必要があります。 エイリアス値を指定したら、フォームに適用する各使用権限を指定します。

**権限が有効なフォームのレンダリング**

権限が有効なフォームをレンダリングする場合は、使用権限のないフォームをレンダリングする場合と同じアプリケーションロジックを使用します。 唯一の違いは、使用権限のランタイムオプションがアプリケーションロジックに含まれていることを確認する必要がある点です。

>[!NOTE]
>
>Forms Web サービス API を使用して権限を付与されたフォームをレンダリングする場合、フォームにファイルを添付することはできません。

**フォームデータストリームをクライアント Web ブラウザーに書き込む**

Formsサービスが権限を付与されたフォームをレンダリングすると、クライアントの Web ブラウザーに書き込む必要があるフォームデータストリームが返されます。 クライアントの Web ブラウザーに書き込まれると、フォームはユーザーに対して表示されます。 Adobe Readerで権限が付与されたフォームを表示しているユーザーは、そのフォームに対して有効な操作を実行できます。

**関連トピック**

[Java API を使用した、権限が有効なフォームのレンダリング](#render-rights-enabled-forms-using-the-java-api)

[Web サービス API を使用した、権限が有効なフォームのレンダリング](#render-rights-enabled-forms-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Forms Service API クイックスタート](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[インタラクティブPDF formsのレンダリング](/help/forms/developing/rendering-interactive-pdf-forms.md)

[Formsをレンダリングする Web アプリケーションの作成](/help/forms/developing/creating-web-applications-renders-forms.md)

### Java API を使用した、権限が有効なフォームのレンダリング {#render-rights-enabled-forms-using-the-java-api}

Forms API(Java) を使用して、権限が有効なフォームをレンダリングします。

1. プロジェクトファイルを含める

   Java プロジェクトのクラスパスに、adobe-forms-client.jar などのクライアント JAR ファイルを含めます。

1. Forms Client API オブジェクトの作成

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * の作成 `FormsServiceClient` オブジェクトのコンストラクタを使用し、 `ServiceClientFactory` オブジェクト。

1. 使用権限の実行時オプションを設定する

   * コンストラクタを使用して `ReaderExtensionSpec` オブジェクトを作成します。
   * を呼び出して、秘密鍵証明書のエイリアスを指定します。 `ReaderExtensionSpec` オブジェクトの `setReCredentialAlias` メソッドを使用してエイリアス値を表す string 値を指定します。
   * に属する対応するメソッドを呼び出して、各使用権限を設定します。 `ReaderExtensionSpec` オブジェクト。 ただし、使用権限を設定できるのは、参照する秘密鍵証明書でその権限が与えられている場合のみです。 つまり、秘密鍵証明書で設定が許可されていない場合は、使用権限を設定できません。 例： ユーザーがフォームフィールドに入力してフォームを保存できる使用権限を設定するには、 `ReaderExtensionSpec` オブジェクトの `setReFillIn` メソッドとパス `true`.

   >[!NOTE]
   >
   >を呼び出す必要はありません。 `ReaderExtensionSpec` オブジェクトの `setReCredentialPassword`*メソッド。 このメソッドは、Formsサービスでは使用されません。*

1. 権限が有効なフォームのレンダリング

   を呼び出す `FormsServiceClient` オブジェクトの `renderPDFFormWithUsageRights` メソッドを使用して、次の値を渡します。

   * ファイル名拡張子を含むフォームデザイン名を指定する string 値。 Formsアプリケーションの一部であるフォームデザインを参照する場合は、必ず次のような完全なパスを指定してください。 `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * A `com.adobe.idp.Document` フォームに結合するデータを含むオブジェクト。 データを結合しない場合は、空の `com.adobe.idp.Document` オブジェクト。
   * A `PDFFormRenderSpec` 実行時オプションを保存するオブジェクト。
   * A `ReaderExtensionSpec` 使用権限の実行時オプションを格納するオブジェクト。
   * A `URLSpec` Formsサービスで必要な URI 値を格納するオブジェクト。

   この `renderPDFFormWithUsageRights` メソッドは、 `FormsResult` クライアントの Web ブラウザーに書き込む必要があるフォームデータストリームを含むオブジェクト。

1. フォームデータストリームをクライアント Web ブラウザーに書き込む

   * の作成 `com.adobe.idp.Document` を呼び出すことによってオブジェクトを取得 `FormsResult` オブジェクト `getOutputContent` メソッド。
   * のコンテンツタイプを取得する `com.adobe.idp.Document` オブジェクトを呼び出す `getContentType` メソッド。
   * を `javax.servlet.http.HttpServletResponse` を呼び出すことによるオブジェクトのコンテンツタイプ `setContentType` メソッドを使用して、 `com.adobe.idp.Document` オブジェクト。
   * の作成 `javax.servlet.ServletOutputStream` オブジェクトを使用します。オブジェクトは、 `javax.servlet.http.HttpServletResponse` オブジェクトの `getOutputStream` メソッド。
   * の作成 `java.io.InputStream` を呼び出すことによってオブジェクトを取得 `com.adobe.idp.Document` オブジェクトの `getInputStream` メソッド。
   * バイト配列を作成し、 `InputStream` オブジェクトの `read` メソッドを使用し、バイト配列を引数として渡す。
   * を呼び出す `javax.servlet.ServletOutputStream` オブジェクトの `write` メソッドを使用して、フォームデータストリームをクライアント Web ブラウザーに送信します。 バイト配列を `write` メソッド。

**関連トピック**

[クイックスタート（SOAP モード）:Java API を使用した権限が有効なフォームのレンダリング](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-a-rights-enabled-form-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Web サービス API を使用した、権限が有効なフォームのレンダリング {#render-rights-enabled-forms-using-the-web-service-api}

Forms API（Web サービス）を使用して、権限が有効なフォームをレンダリングします。

1. プロジェクトファイルを含める

   * Forms Service WSDL を使用する Java プロキシクラスを作成します。
   * Java プロキシクラスをクラスパスに含めます。

1. Forms Client API オブジェクトの作成

   の作成 `FormsService` オブジェクトを選択し、認証値を設定します。

1. 使用権限の実行時オプションを設定する

   * コンストラクタを使用して `ReaderExtensionSpec` オブジェクトを作成します。
   * を呼び出して、秘密鍵証明書のエイリアスを指定します。 `ReaderExtensionSpec` オブジェクトの `setReCredentialAlias` メソッドを使用してエイリアス値を表す string 値を指定します。
   * に属する対応するメソッドを呼び出して、各使用権限を設定します。 `ReaderExtensionSpec` オブジェクト。 ただし、使用権限を設定できるのは、参照する秘密鍵証明書でその権限が与えられている場合のみです。 つまり、秘密鍵証明書で設定が許可されていない場合は、使用権限を設定できません。 ユーザーがフォームフィールドに入力してフォームを保存できる使用権限を設定するには、 `ReaderExtensionSpec` オブジェクトの `setReFillIn` メソッドとパス `true`.

1. 権限が有効なフォームのレンダリング

   を呼び出す `FormsService` オブジェクトの `renderPDFFormWithUsageRights` メソッドを使用して、次の値を渡します。

   * ファイル名拡張子を含むフォームデザイン名を指定する string 値。 Formsアプリケーションの一部であるフォームデザインを参照する場合は、必ず次のような完全なパスを指定してください。 `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * A `BLOB` フォームに結合するデータを含むオブジェクト。 データをフォームと結合しない場合、 `BLOB` 空の XML データソースに基づくオブジェクト。 を渡すことはできません `BLOB` null のオブジェクト；それ以外の場合は、例外がスローされます。
   * A `PDFFormRenderSpec` 実行時オプションを保存するオブジェクト。
   * A `ReaderExtensionSpec` 使用権限の実行時オプションを格納するオブジェクト。
   * A `URLSpec` Formsサービスで必要な URI 値を格納するオブジェクト。

   この `renderPDFFormWithUsageRights` メソッドは、 `FormsResult` クライアントの Web ブラウザーに書き込む必要があるフォームデータストリームを含むオブジェクト。

1. フォームデータストリームをクライアント Web ブラウザーに書き込む

   * の作成 `BLOB` を呼び出してフォームデータを含むオブジェクト `FormsResult` オブジェクトの `getOutputContent` メソッド。
   * のコンテンツタイプを取得する `BLOB` オブジェクトを呼び出す `getContentType` メソッド。
   * を `javax.servlet.http.HttpServletResponse` を呼び出すことによるオブジェクトのコンテンツタイプ `setContentType` メソッドを使用して、 `BLOB` オブジェクト。
   * の作成 `javax.servlet.ServletOutputStream` オブジェクトを使用します。オブジェクトは、 `javax.servlet.http.HttpServletResponse` オブジェクトの `getOutputStream` メソッド。
   * バイト配列を作成し、 `BLOB` オブジェクトの `getBinaryData` メソッド。 このタスクは、 `FormsResult` オブジェクトをバイト配列に変換します。
   * を呼び出す `javax.servlet.http.HttpServletResponse` オブジェクトの `write` メソッドを使用して、フォームデータストリームをクライアント Web ブラウザーに送信します。 バイト配列を `write` メソッド。

**関連トピック**

[レンダリング権限が有効なForms](#rendering-rights-enabled-forms)

[Base64 エンコーディングを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
