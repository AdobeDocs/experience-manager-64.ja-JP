---
title: Forms サービスのパフォーマンスの最適化
seo-title: Optimizing the Performance of theForms Service
description: フォームのレンダリング時に実行時オプションを設定し、XDP ファイルをリポジトリに保存して、Formsサービスのパフォーマンスを最適化します。
seo-description: Set run-time options when rendering a form and store XDP files in the repository to optimize the performance of the Forms service.
uuid: 9040c09a-e5d0-432b-b1c5-ad46ab57c4fc
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: operations
discoiquuid: 9f883483-b81e-42c6-a4a1-eb499dd112e7
role: Developer
exl-id: a6d468cd-2b70-4332-8277-15f8b9fc1329
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '1417'
ht-degree: 7%

---

# Forms Service のパフォーマンスの最適化 {#optimizing-the-performance-of-theforms-service}

## Forms Service のパフォーマンスの最適化 {#optimizing-the-performance-of-the-forms-service}

フォームをレンダリングする際に、Formsサービスのパフォーマンスを最適化する実行時のオプションを設定できます。 Formsサービスのパフォーマンスを向上させるために実行できるもう 1 つのタスクは、XDP ファイルをリポジトリに保存することです。 ただし、この節では、このタスクの実行方法については説明しません。 ( [Java クライアントライブラリを使用したサービスの呼び出し](/help/forms/developing/invoking-aem-forms-using-java.md#invoking-a-service-using-a-java-client-library).)

>[!NOTE]
>
>Formsサービスについて詳しくは、 [AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary-of-steps}

フォームのレンダリング中にFormsサービスのパフォーマンスを最適化するには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. Forms Client API オブジェクトを作成します。
1. パフォーマンスの実行時オプションを設定します。
1. フォームをレンダリングします。
1. フォームデータストリームをクライアントの Web ブラウザーに書き込みます。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。 Web サービスを使用している場合は、プロキシファイルを必ず含めてください。

**Forms Client API オブジェクトの作成**

Forms Service Client API 操作をプログラムで実行する前に、Formsサービスクライアントを作成する必要があります。 Java API を使用している場合は、 `FormsServiceClient` オブジェクト。 Forms Web サービス API を使用している場合は、 `FormsService` オブジェクト。

**パフォーマンスの実行時オプションを設定する**

次のパフォーマンスランタイムオプションを設定して、Formsサービスのパフォーマンスを向上させることができます。

* **フォームのキャッシュ**:サーバーキャッシュ内でPDFとしてレンダリングされるフォームをキャッシュできます。 各フォームは、初回生成後にキャッシュされます。それ以降のレンダリング時には、キャッシュされているフォームがフォームデザインのタイムスタンプよりも新しい場合、フォームはキャッシュから取得されます。フォームをキャッシュすると、リポジトリからフォームデザインを取得する必要がなくなるので、Formsサービスのパフォーマンスが向上します。
* フォームガイド（非推奨）は、他の変換タイプよりもレンダリングに時間がかかる場合があります。 パフォーマンスを向上させるために、フォームガイド（非推奨）をキャッシュすることをお勧めします。
* **スタンドアロンオプション**:Formsサービスでサーバー側の計算を実行する必要がない場合、「スタンドアロン」オプションを「 `true`を呼び出すと、フォームは状態情報なしでレンダリングされます。 状態情報は、インタラクティブフォームをエンドユーザーにレンダリングし、そのユーザーがフォームに情報を入力して、そのフォームをFormsサービスに送り返す場合に必要です。 次に、Forms サービスは計算処理を実行し、フォームをレンダリングしてユーザーに戻し、結果がフォームに表示されます。状態情報のないフォームがFormsサービスに送り返された場合、XML データのみが使用可能になり、サーバー側の計算は実行されません。
* **線形化PDF**:線形化されたPDFファイルは、ネットワーク環境で効率的な増分アクセスを可能にするように編成されています。 PDFファイルは、あらゆる点で有効なPDFで、既存のすべてのビューアやその他のPDFアプリケーションと互換性があります。 つまり、線形化されたPDFは、ダウンロード中に表示できます。
* このオプションを選択しても、クライアントでPDFフォームがレンダリングされる際のパフォーマンスは向上しません。
* **GuideRSL オプション**:実行時の共有ライブラリを使用して、フォームガイド（非推奨）の生成を有効にします。 つまり、最初のリクエストでは、小さいSWFファイルと、ブラウザーのキャッシュに保存されている大きい共有ライブラリがダウンロードされます。 詳しくは、 Flexのドキュメントの RSL を参照してください。
* また、クライアントでフォームをレンダリングして、Formsサービスのパフォーマンスを向上させることもできます。 ( [クライアントでのFormsのレンダリング](/help/forms/developing/rendering-forms-client.md).)

**フォームをレンダリング**

パフォーマンスオプションを設定した後にフォームをレンダリングするには、パフォーマンスオプションを指定せずにフォームをレンダリングする場合と同じアプリケーションロジックを使用します。

**フォームデータストリームをクライアント Web ブラウザーに書き込む**

Formsサービスがフォームをレンダリングすると、クライアントの Web ブラウザーに書き込む必要があるフォームデータストリームが返されます。 クライアント Web ブラウザーに書き込まれると、フォームはユーザーに対して表示されます。

**関連トピック**

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Forms Service API クイックスタート](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[インタラクティブPDF formsのレンダリング](/help/forms/developing/rendering-interactive-pdf-forms.md)

[FormsをHTMLとしてレンダリング](/help/forms/developing/rendering-forms-html.md)

[Formsをレンダリングする Web アプリケーションの作成](/help/forms/developing/creating-web-applications-renders-forms.md)

### Java API を使用したパフォーマンスの最適化 {#optimize-the-performance-using-the-java-api}

Forms API(Java) を使用して、最適化されたパフォーマンスでフォームをレンダリングします。

1. プロジェクトファイルを含める

   Java プロジェクトのクラスパスに、adobe-forms-client.jar などのクライアント JAR ファイルを含めます。

1. Forms Client API オブジェクトの作成

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * の作成 `FormsServiceClient` オブジェクトのコンストラクタを使用し、 `ServiceClientFactory` オブジェクト。

1. パフォーマンスの実行時オプションを設定する

   * コンストラクタを使用して `PDFFormRenderSpec` オブジェクトを作成します。
   * を呼び出して、フォームキャッシュオプションを設定します。 `PDFFormRenderSpec` オブジェクトの `setCacheEnabled` メソッドとパス `true`.
   * 線形化オプションを設定するには、 `PDFFormRenderSpec` オブジェクトの `setLinearizedPDF` メソッドとパス `true.`

1. フォームをレンダリング

   を呼び出す `FormsServiceClient` オブジェクトの `renderPDFForm` メソッドを使用して、次の値を渡します。

   * ファイル名拡張子を含むフォームデザイン名を指定する string 値。
   * A `com.adobe.idp.Document` フォームに結合するデータを含むオブジェクト。 データを結合しない場合は、空の `com.adobe.idp.Document` オブジェクト。
   * A `PDFFormRenderSpec` パフォーマンスを向上させるための実行時オプションを保存するオブジェクト。
   * A `URLSpec` Formsサービスで必要な URI 値を格納するオブジェクト。
   * A `java.util.HashMap` 添付ファイルを保存するオブジェクト。 これはオプションのパラメーターで、 `null` フォームにファイルを添付しない場合。

   この `renderPDFForm` メソッドは、 `FormsResult` クライアントの Web ブラウザーに書き込む必要があるフォームデータストリームを含むオブジェクト。

1. フォームデータストリームをクライアント Web ブラウザーに書き込む

   * の作成 `javax.servlet.ServletOutputStream` フォームデータストリームをクライアントの Web ブラウザーに送信するために使用するオブジェクト。
   * の作成 `com.adobe.idp.Document` を呼び出すことによってオブジェクトを取得 `FormsResult` オブジェクト `getOutputContent` メソッド。
   * の作成 `java.io.InputStream` を呼び出すことによってオブジェクトを取得 `com.adobe.idp.Document` オブジェクトの `getInputStream` メソッド。
   * バイト配列を作成し、 `InputStream` オブジェクトの `read`メソッドを使用し、バイト配列を引数として渡す。
   * を呼び出す `javax.servlet.ServletOutputStream` オブジェクトの `write` メソッドを使用して、フォームデータストリームをクライアント Web ブラウザーに送信します。 バイト配列を `write` メソッド。

**関連トピック**

[クイックスタート（SOAP モード）:Java API を使用したパフォーマンスの最適化](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-optimizing-performance-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Web サービス API を使用したパフォーマンスの最適化 {#optimize-the-performance-using-the-web-service-api}

Forms API（Web サービス）を使用して、最適化されたパフォーマンスでフォームをレンダリングします。

1. プロジェクトファイルを含める

   * Forms Service WSDL を使用する Java プロキシクラスを作成します。
   * Java プロキシクラスをクラスパスに含めます。

1. Forms Client API オブジェクトの作成

   の作成 `FormsService` オブジェクトを選択し、認証値を設定します。

1. パフォーマンスの実行時オプションを設定する

   * コンストラクタを使用して `PDFFormRenderSpec` オブジェクトを作成します。
   * を呼び出して、フォームキャッシュオプションを設定します。 `PDFFormRenderSpec` オブジェクトの `setCacheEnabled` メソッドを渡し、true を渡します。
   * を呼び出して、スタンドアロンオプションを設定します。 `PDFFormRenderSpec` オブジェクトの `setStandAlone` メソッドを渡し、true を渡します。
   * 線形化オプションを設定するには、 `PDFFormRenderSpec` オブジェクトの `setLinearizedPDF` メソッドを渡し、true を渡します。

1. フォームをレンダリング

   を呼び出す `FormsService` オブジェクトの `renderPDFForm` メソッドを使用して、次の値を渡します。

   * ファイル名拡張子を含むフォームデザイン名を指定する string 値。
   * A `BLOB` フォームに結合するデータを含むオブジェクト。 データを結合しない場合は、 `null`.
   * A `PDFFormRenderSpecc` 実行時オプションを保存するオブジェクト。
   * A `URLSpec` Formsサービスで必要な URI 値を格納するオブジェクト。
   * A `java.util.HashMap` 添付ファイルを保存するオブジェクト。 これはオプションのパラメーターで、 `null` フォームにファイルを添付しない場合。
   * 空 `com.adobe.idp.services.holders.BLOBHolder` メソッドによって設定されるオブジェクト。 これは、レンダリングされたPDFフォームを保存するために使用されます。
   * 空 `javax.xml.rpc.holders.LongHolder` メソッドによって設定されるオブジェクト。 （この引数は、フォームのページ数を保存します）。
   * 空 `javax.xml.rpc.holders.StringHolder` メソッドによって設定されるオブジェクト。 （この引数はロケール値を格納します）。
   * 空 `com.adobe.idp.services.holders.FormsResultHolder` この操作の結果を格納するオブジェクト。

   この `renderPDFForm` メソッドによって `com.adobe.idp.services.holders.FormsResultHolder` オブジェクト。クライアント Web ブラウザーに書き込む必要があるフォームデータストリームを含む最後の引数値として渡されます。

1. フォームデータストリームをクライアント Web ブラウザーに書き込む

   * の作成 `FormResult` オブジェクトを作成するには、 `com.adobe.idp.services.holders.FormsResultHolder` オブジェクトの `value` データメンバー。
   * の作成 `javax.servlet.ServletOutputStream` フォームデータストリームをクライアントの Web ブラウザーに送信するために使用するオブジェクト。
   * の作成 `BLOB` を呼び出してフォームデータを含むオブジェクト `FormsResult` オブジェクトの `getOutputContent` メソッド。
   * バイト配列を作成し、 `BLOB` オブジェクトの `getBinaryData` メソッド。 このタスクは、 `FormsResult` オブジェクトをバイト配列に変換します。
   * を呼び出す `javax.servlet.http.HttpServletResponse` オブジェクトの `write` メソッドを使用して、フォームデータストリームをクライアント Web ブラウザーに送信します。 バイト配列を `write` メソッド。

**関連トピック**

[Base64 エンコーディングを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
