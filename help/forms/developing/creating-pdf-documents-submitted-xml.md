---
title: SubmittedXML データを使用したPDFドキュメントの作成
seo-title: Creating PDF Documents with SubmittedXML Data
description: Formsサービスを使用して、ユーザーがインタラクティブフォームに入力したフォームデータを取得します。 フォームデータを別のAEM Formsサービス操作に渡し、そのデータを使用してPDFドキュメントを作成します。
seo-description: Use the Forms service to retrieve the form data that the user entered into an interactive form. Pass the form data to another AEM Forms service operation and create a PDF document using the data.
uuid: 2676c614-8988-451b-ac7c-bd07731a3f5f
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: operations
discoiquuid: 62490230-a24e-419d-95bb-c0bb04a03f96
role: Developer
exl-id: a0d6e4a6-751f-4cab-842b-08719b899060
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '1306'
ht-degree: 4%

---

# 送信済み XMLPDFでのデータ・ドキュメントの作成 {#creating-pdf-documents-with-submittedxml-data}

## 送信済み XMLPDFでのデータ・ドキュメントの作成 {#creating-pdf-documents-with-submitted-xml-data}

ユーザーがインタラクティブフォームに入力できる Web ベースのアプリケーションでは、データをサーバーに送り返す必要があります。 Formsサービスを使用すると、ユーザーがインタラクティブフォームに入力したフォームデータを取得できます。 次に、フォームデータを別のAEM Formsサービス操作に渡し、そのデータを使用してPDFドキュメントを作成します。

>[!NOTE]
>
>この内容を読む前に、送信済みのフォームの処理に関する十分な知識を持っておくことをお勧めします。 フォームデザインと送信済み XML データとの関係などの概念については、送信済みFormsの処理を参照してください。

次の 3 つのAEM Formsサービスを伴うワークフローについて考えてみましょう。

* ユーザーは、Web ベースのアプリケーションからFormsサービスに XML データを送信します。
* Formsサービスは、送信されたフォームの処理とフォームフィールドの抽出に使用されます。 フォームデータは処理できます。 例えば、データをエンタープライズデータベースに送信できます。
* フォームデータは、非インタラクティブデータドキュメントを作成するために Output サービスにPDFされます。
* 非インタラクティブPDFドキュメントは、Content Services（非推奨）に保存されます。

次の図は、このワークフローを視覚的に表したものです。

![cd_cd_finsrv_architecture_xml_pdf1](assets/cd_cd_finsrv_architecture_xml_pdf1.png)

ユーザーがクライアント Web ブラウザーからフォームを送信すると、非インタラクティブPDFドキュメントが Content Services（非推奨）に保存されます。 次の図は、Content Services（非推奨）に保存されたPDFドキュメントを示しています。

![cd_cd_cs_gui](assets/cd_cd_cs_gui.png)

### 手順の概要 {#summary-of-steps}

送信済み XML データを含む非インタラクティブPDFドキュメントを作成し、Content Services（非推奨）のPDFドキュメントに保存するには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. Forms、Output および Document Management オブジェクトを作成します。
1. Formsサービスを使用してフォームデータを取得します。
1. Output サービスを使用して、非インタラクティブPDFドキュメントを作成します。
1. Document Management サービスを使用して、Content Services（非推奨）にPDFフォームを保存します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。 Web サービスを使用している場合は、プロキシファイルを必ず含めてください。

**Forms、Output および Document Management オブジェクトの作成**

プログラムによってForms Service API 操作を実行する前に、Forms Client API オブジェクトを作成します。 同様に、このワークフローは Output サービスと Document Management サービスを呼び出すので、Output Client API オブジェクトと Document Management Client API オブジェクトの両方を作成します。

**Formsサービスを使用してフォームデータを取得する**

Formsサービスに送信されたフォームデータを取得します。 送信されたデータを処理して、ビジネス要件を満たすことができます。 例えば、エンタープライズデータベースにフォームデータを格納できます。 ただし、非インタラクティブPDFドキュメントを作成する場合は、フォームデータが Output サービスに渡されます。

**Output サービスを使用して、非インタラクティブPDFドキュメントを作成します。**

Output サービスを使用して、フォームデザインと XML フォームデータに基づく非インタラクティブPDFドキュメントを作成します。 ワークフローでは、フォームデータはFormsサービスから取得されます。

**Document Management サービスを使用して、PDFフォームを Content Services（非推奨）に格納します**

Content Services（非推奨）にPDFドキュメントを保存するには、Document Management Service API を使用します。

**関連トピック**

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Forms Service API クイックスタート](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

### Java API を使用して、送信された XML データを含むPDFドキュメントを作成します {#create-a-pdf-document-with-submitted-xml-data-using-the-java-api}

Forms、Output、および Document Management API(Java) を使用して、送信された XML データを含むPDFドキュメントを作成します。

1. プロジェクトファイルを含める

   Java プロジェクトのクラスパスに、adobe-forms-client.jar、adobe-output-client.jar、adobe-contentservices-client.jar などのクライアント JAR ファイルを含めます。

1. Forms、Output および Document Management オブジェクトの作成

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用して `FormsServiceClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。
   * の作成 `OutputClient` オブジェクトのコンストラクタを使用し、 `ServiceClientFactory` オブジェクト。
   * コンストラクタを使用して `DocumentManagementServiceClientImpl` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. Formsサービスを使用してフォームデータを取得する

   * を呼び出す `FormsServiceClient` オブジェクトの `processFormSubmission` メソッドを使用して、次の値を渡します。

      * この `com.adobe.idp.Document` フォームデータを格納するオブジェクト。
      * 関連するすべての HTTP ヘッダーを含む環境変数を指定する string 値。 処理するコンテンツタイプを指定するには、 `CONTENT_TYPE` 環境変数。 例えば、XML データを処理するには、このパラメーターに次の文字列値を指定します。 `CONTENT_TYPE=text/xml`.
      * 次を指定する string 値 `HTTP_USER_AGENT` ヘッダー値（例： ） `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`.
      * A `RenderOptionsSpec` 実行時オプションを保存するオブジェクト。

      この `processFormSubmission` メソッドは、 `FormsResult` フォーム送信の結果を含むオブジェクト。

   * を呼び出して、Formsサービスがフォームデータの処理を完了したかどうかを判断します。 `FormsResult` オブジェクトの `getAction` メソッド。 このメソッドが値を返す場合 `0`に設定すると、データを処理する準備が整います。
   * フォームデータを取得するには、 `com.adobe.idp.Document` を呼び出すことによってオブジェクトを取得 `FormsResult` オブジェクトの `getOutputContent` メソッド。 （このオブジェクトには、Output サービスに送信できるフォームデータが含まれています）。
   * の作成 `java.io.InputStream` を呼び出すことによってオブジェクトを取得 `java.io.DataInputStream` コンストラクタと `com.adobe.idp.Document` オブジェクト。
   * の作成 `org.w3c.dom.DocumentBuilderFactory` オブジェクトの `org.w3c.dom.DocumentBuilderFactory` オブジェクトの `newInstance` メソッド。
   * の作成 `org.w3c.dom.DocumentBuilder` を呼び出すことによってオブジェクトを取得 `org.w3c.dom.DocumentBuilderFactory` オブジェクトの `newDocumentBuilder` メソッド。
   * の作成 `org.w3c.dom.Document` を呼び出すことによってオブジェクトを取得 `org.w3c.dom.DocumentBuilder` オブジェクトの `parse` メソッドおよび `java.io.InputStream` オブジェクト。
   * XML ドキュメント内の各ノードの値を取得します。 このタスクを実行する 1 つの方法は、次の 2 つのパラメーターを受け入れるカスタムメソッドを作成することです。の `org.w3c.dom.Document` オブジェクトおよび値を取得するノードの名前。 このメソッドは、ノードの値を表す文字列値を返します。 このプロセスに続くコード例では、このカスタムメソッドをと呼び出します。 `getNodeText`. このメソッドの本文を示します。


1. Output サービスを使用して、非インタラクティブPDFドキュメントを作成します。

   を呼び出してPDFドキュメントを作成する `OutputClient` オブジェクトの `generatePDFOutput` メソッドを使用して、次の値を渡します。

   * A `TransformationFormat` enum 値。 PDF・ドキュメントを生成するには、 `TransformationFormat.PDF`.
   * フォームデザイン名を指定する string 値。フォームデザインに、Formsサービスから取得したフォームデータとの互換性があることを確認します。
   * フォームデザインが配置されているコンテンツルートを指定する string 値です。
   * A `PDFOutputOptionsSpec` PDFの実行時オプションを含むオブジェクト。
   * A `RenderOptionsSpec` レンダリングの実行時オプションを含むオブジェクト。
   * この `com.adobe.idp.Document` フォームデザインとマージするデータが含まれる XML データソースを含むオブジェクト。 このオブジェクトが `FormsResult` オブジェクトの `getOutputContent` メソッド。
   * この `generatePDFOutput` メソッドは、 `OutputResult` 操作の結果を格納するオブジェクト。
   * を呼び出して、非インタラクティブPDFドキュメントを取得する `OutputResult` オブジェクトの `getGeneratedDoc` メソッド。 このメソッドは、 `com.adobe.idp.Document` 非インタラクティブPDFドキュメントを表すインスタンス。

1. Document Management サービスを使用して、PDFフォームを Content Services（非推奨）に格納します

   を呼び出して、コンテンツを追加します。 `DocumentManagementServiceClientImpl` オブジェクトの `storeContent` メソッドを使用して、次の値を渡します。

   * コンテンツが追加されるストアを指定する string 値です。 デフォルトのストアは `SpacesStore`. この値は必須のパラメータです。
   * コンテンツが追加されるスペースの完全修飾パスを指定する string 値 ( 例： `/Company Home/Test Directory`) をクリックします。 この値は必須のパラメータです。
   * 新しいコンテンツを表すノード名 ( 例： `MortgageForm.pdf`) をクリックします。 この値は必須のパラメータです。
   * ノードタイプを指定する string 値。 新しいコンテンツ (PDFファイルなど ) を追加するには、次のように指定します。 `{https://www.alfresco.org/model/content/1.0}content`. この値は必須のパラメータです。
   * A `com.adobe.idp.Document` コンテンツを表すオブジェクト。 この値は必須のパラメータです。
   * エンコーディング値 ( 例えば、 `UTF-8`) をクリックします。 この値は必須のパラメータです。
   * An `UpdateVersionType` バージョン情報の処理方法を指定する列挙値 ( 例： `UpdateVersionType.INCREMENT_MAJOR_VERSION` コンテンツのバージョンを増分します。 ) この値は必須のパラメータです。
   * A `java.util.List` コンテンツに関連する要素を指定するインスタンス。 この値はオプションのパラメーターで、 `null`.
   * A `java.util.Map` コンテンツ属性を格納するオブジェクト。

   この `storeContent` メソッドは、 `CRCResult` コンテンツを表すオブジェクト。 の使用 `CRCResult` オブジェクトを使用すると、例えば、コンテンツの一意の識別子値を取得できます。 このタスクを実行するには、 `CRCResult` オブジェクトの `getNodeUuid` メソッド。

**関連トピック**

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)
