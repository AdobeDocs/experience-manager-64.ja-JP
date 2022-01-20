---
title: フラグメントに基づくFormsのレンダリング
seo-title: Rendering Forms Based on Fragments
description: Formsサービスを使用して、Designer で作成されたフラグメントに基づくフォームをレンダリングします。
seo-description: Use the Forms service to render forms that are based on fragments created using Designer.
uuid: 9c9a730d-f970-41f8-afed-4e6b6d3d393d
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: operations
discoiquuid: a65c5303-0ebd-43a9-a777-401042d8fcad
role: Developer
exl-id: 49c4af9a-5797-468c-b3ad-f3140d445ff2
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '2195'
ht-degree: 9%

---

# フラグメントに基づくFormsのレンダリング {#rendering-forms-based-on-fragments}

## フラグメントに基づくFormsのレンダリング {#rendering-forms-based-on-fragments-inner}

Formsサービスでは、Designer を使用して作成したフラグメントに基づくフォームをレンダリングできます。 A *フラグメント* はフォームの再利用可能な部分で、複数のフォームデザインに挿入できる個別の XDP ファイルとして保存されます。 例えば、フラグメントには住所ブロックや法律文を含めることができます。

フラグメントの使用により、大量のフォームの作成とメンテナンスを簡単に、短時間で実行できます。新しいフォームを作成する際に、必要なフラグメントへの参照を挿入すると、そのフラグメントがフォームに表示されます。 フラグメント参照には、物理 XDP ファイルを指すサブフォームが含まれます。フラグメントを基にしたフォームデザインの作成について詳しくは、 [Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63)

フラグメントには、選択サブフォームセットに含める複数のサブフォームを含めることができます。 選択サブフォームセットは、データ接続からのデータのフローに基づいてサブフォームの表示を制御します。 条件ステートメントを使用して、配信するフォームに表示するサブフォームをそのセットから指定します。例えば、セット内の各サブフォームには、特定の地理的な場所に関する情報を含めることができ、表示されるサブフォームは、ユーザーの場所に基づいて決定できます。

A *スクリプトフラグメント* には、日付パーサーや Web サービス呼び出しなど、特定のオブジェクトとは別に保存される再利用可能な JavaScript 関数や値が含まれています。 このようなフラグメントには、階層パレットに変数の子として表示される単独のスクリプトオブジェクトがあります。フラグメントは、他のオブジェクトのプロパティとなっているスクリプトからは作成できません。このようなスクリプトとして、検証、計算、初期化などのイベントスクリプトがあります。

フラグメントを使用する利点は次のとおりです。

* **コンテンツの再利用**:フラグメントを使用すると、複数のフォームデザインでコンテンツを再利用できます。 複数のフォームで同じコンテンツの一部を使用する必要がある場合は、コンテンツをコピーまたは再作成するよりも、フラグメントを使用する方が速くて簡単です。 フラグメントを使用し、それをフォームで参照することで、フォームデザインの中で頻繁に使用する部分を一貫性のあるコンテンツと外観ですべてのフォームに表示できます。
* **グローバル更新**:フラグメントを使用すると、1 つのファイルで 1 回だけ複数のフォームにグローバルな変更を加えることができます。 フラグメント内のコンテンツ、スクリプトオブジェクト、データバインディング、レイアウトまたはスタイルを変更すると、その変更がフラグメントを参照するすべての XDP フォームに反映されます。
* 例えば、多くのフォームで共通する要素は、国のコンボボックスオブジェクトを含む住所ブロックです。 コンボボックスオブジェクトの値を更新する必要がある場合は、多数のフォームを開いて変更を加える必要があります。 フラグメントにアドレスブロックを含める場合は、1 つのフラグメントファイルを開くだけで変更を加えることができます。
* PDFフォーム内のフラグメントを更新するには、Designer でそのフォームを再保存する必要があります。
* **共有フォームの作成**:フラグメントを使用して、複数のリソースでフォームの作成を共有できます。 スクリプトまたは Designer のその他の高度な機能に精通しているフォーム開発者は、スクリプトまたは動的プロパティを活用するフラグメントを作成、共有することができます。フォーム作成者がこれらのフラグメントを使用してフォームデザインをレイアウトすれば、複数の担当者が作成した複数のフォームの各部分で一貫性のある外観と機能を実現できます。

### フラグメントを使用してアセンブリされたフォームデザインのアセンブリ {#assembling-a-form-design-assembled-using-fragments}

複数のフラグメントに基づいてFormsサービスに渡すフォームデザインを組み立てることができます。 複数のフラグメントをアセンブリするには、Assembler サービスを使用します。 Assemble サービスを使用して別のFormsサービス（Output サービス）で使用されるフォームデザインを作成する例については、 [フラグメントを使用したPDFドキュメントの作成](/help/forms/developing/creating-document-output-streams.md#creating-pdf-documents-using-fragments). Output サービスを使用する代わりに、Formsサービスを使用して同じワークフローを実行できます。

Assembler サービスを使用する場合、フラグメントを使用してアセンブルされたフォームデザインを渡します。 作成されたフォームデザインは、他のフラグメントを参照していません。 これに対し、このトピックでは、他のフラグメントを参照するフォームデザインをFormsサービスに渡す方法について説明します。 ただし、フォームデザインは Assembler によってアセンブルされていません。 Designer で作成されました。

>[!NOTE]
>
>Formsサービスについて詳しくは、 [AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>フラグメントに基づいてフォームをレンダリングする Web ベースのアプリケーションの作成について詳しくは、 [Formsをレンダリングする Web アプリケーションの作成](/help/forms/developing/creating-web-applications-renders-forms.md).

### 手順の概要 {#summary-of-steps}

フラグメントに基づいてフォームをレンダリングするには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. Forms Client API オブジェクトを作成します。
1. URI 値を指定します。
1. フォームをレンダリングします。
1. フォームデータストリームをクライアントの Web ブラウザーに書き込みます。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。 Web サービスを使用している場合は、プロキシファイルを必ず含めてください。

**Forms Client API オブジェクトの作成**

Forms Service Client API 操作をプログラムで実行する前に、Formsサービスクライアントを作成する必要があります。

**URI 値の指定**

フラグメントに基づいてフォームを正常にレンダリングするには、Formsサービスで、フォームデザインが参照するフォームとフラグメント（XDP ファイル）の両方を検索できるようにする必要があります。 例えば、フォームの名前が PO.xdp で、このフォームが FooterUS.xdp および FooterCanada.xdp という 2 つのフラグメントを使用しているとします。 このような状況では、Formsサービスは 3 つの XDP ファイルをすべて見つけることができる必要があります。

フォームとそのフラグメントは、ある場所に配置し、別の場所に配置することで整理できます。また、すべての XDP ファイルを同じ場所に配置することもできます。 この節の目的では、すべての XDP ファイルがAEM Formsリポジトリ内にあると仮定します。 XDP ファイルをAEM Formsリポジトリに配置する方法について詳しくは、 [リソースの書き込み](/help/forms/developing/aem-forms-repository.md#writing-resources).

フラグメントに基づいてフォームをレンダリングする場合は、フォーム自体のみを参照し、フラグメントは参照しないでください。 例えば、FooterUS.xdp や FooterCanada.xdp ではなく、PO.xdp を参照する必要があります。 フラグメントは、Formsサービスで見つけられる場所に配置してください。

**フォームをレンダリング**

フラグメントに基づくフォームは、フラグメント化されていないフォームと同じ方法でレンダリングできます。 つまり、フォームをPDF、HTML、またはフォームガイド（非推奨）としてレンダリングできます。 この節の例では、フラグメントに基づいたフォームをインタラクティブなPDFフォームとしてレンダリングします。 ( [インタラクティブPDF formsのレンダリング](/help/forms/developing/rendering-interactive-pdf-forms.md).)

**フォームデータストリームをクライアント Web ブラウザーに書き込む**

Formsサービスがフォームをレンダリングすると、クライアントの Web ブラウザーに書き込む必要があるフォームデータストリームが返されます。 クライアント Web ブラウザーに書き込まれると、フォームはユーザーに対して表示されます。

**関連トピック**

[Java API を使用してフラグメントに基づいてフォームをレンダリングする](#render-forms-based-on-fragments-using-the-java-api)

[Web サービス API を使用してフラグメントに基づいてフォームをレンダリングする](#render-forms-based-on-fragments-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Forms Service API クイックスタート](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[インタラクティブPDF formsのレンダリング](/help/forms/developing/rendering-interactive-pdf-forms.md)

[Formsをレンダリングする Web アプリケーションの作成](/help/forms/developing/creating-web-applications-renders-forms.md)

### Java API を使用してフラグメントに基づいてフォームをレンダリングする {#render-forms-based-on-fragments-using-the-java-api}

Forms API(Java) を使用して、フラグメントに基づいてフォームをレンダリングします。

1. プロジェクトファイルを含める

   Java プロジェクトのクラスパスに、adobe-forms-client.jar などのクライアント JAR ファイルを含めます。

1. Forms Client API オブジェクトの作成

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * の作成 `FormsServiceClient` オブジェクトのコンストラクタを使用し、 `ServiceClientFactory` オブジェクト。

1. URI 値の指定

   * の作成 `URLSpec` コンストラクターを使用して URI 値を格納するオブジェクト。
   * を呼び出す `URLSpec` オブジェクトの `setApplicationWebRoot` メソッドを使用して、アプリケーションの Web ルートを表す string 値を渡します。
   * を呼び出す `URLSpec` オブジェクトの `setContentRootURI` メソッドを使用して、コンテンツルート URI 値を指定する string 値を渡します。 フォームデザインとフラグメントがコンテンツルート URI に配置されていることを確認します。 そうでない場合、Formsサービスは例外をスローします。 リポジトリを参照するには、次を指定します。 `repository://`.
   * を呼び出す `URLSpec` オブジェクトの `setTargetURL` メソッドを使用してターゲット URL 値を指定し、フォームデータの投稿先となる文字列値を渡します。 フォームデザインでターゲット URL を定義する場合、空の文字列を渡すことができます。 また、計算を実行するためのフォームの送信先の URL を指定することもできます。

1. フォームをレンダリング

   を呼び出す `FormsServiceClient` オブジェクトの `renderPDFForm` メソッドを使用して、次の値を渡します。

   * ファイル名拡張子を含むフォームデザイン名を指定する string 値。 Formsアプリケーションの一部であるフォームデザインを参照する場合は、必ず次のような完全なパスを指定してください。 `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * A `com.adobe.idp.Document` フォームに結合するデータを含むオブジェクト。 データを結合しない場合は、空の `com.adobe.idp.Document` オブジェクト。
   * A `PDFFormRenderSpec` 実行時オプションを保存するオブジェクト。
   * A `URLSpec` フラグメントに基づいてフォームをレンダリングするためにFormsサービスで必要な URI 値を含むオブジェクト。
   * A `java.util.HashMap` 添付ファイルを保存するオブジェクト。 これはオプションのパラメーターで、 `null` フォームにファイルを添付しない場合。

   この `renderPDFForm` メソッドは、 `FormsResult` クライアントの Web ブラウザーに書き込む必要があるフォームデータストリームを含むオブジェクト。

1. フォームデータストリームをクライアント Web ブラウザーに書き込む

   * の作成 `com.adobe.idp.Document` を呼び出すことによってオブジェクトを取得 `FormsResult` オブジェクト `getOutputContent` メソッド。
   * のコンテンツタイプを取得する `com.adobe.idp.Document` オブジェクトを呼び出す `getContentType` メソッド。
   * を `javax.servlet.http.HttpServletResponse` を呼び出すことによるオブジェクトのコンテンツタイプ `setContentType` メソッドを使用して、 `com.adobe.idp.Document` オブジェクト。
   * の作成 `javax.servlet.ServletOutputStream` オブジェクトを使用します。オブジェクトは、 `javax.servlet.http.HttpServletResponse` オブジェクトの `getOutputStream` メソッド。
   * の作成 `java.io.InputStream` を呼び出すことによってオブジェクトを取得 `com.adobe.idp.Document` オブジェクトの `getInputStream` メソッド。
   * バイト配列を作成し、 `InputStream` オブジェクトの `read`メソッドを使用し、バイト配列を引数として渡す。
   * を呼び出す `javax.servlet.ServletOutputStream` オブジェクトの `write` メソッドを使用して、フォームデータストリームをクライアント Web ブラウザーに送信します。 バイト配列を `write` メソッド。

**関連トピック**

[フラグメントに基づくFormsのレンダリング](#rendering-forms-based-on-fragments)

[クイックスタート（SOAP モード）:Java API を使用したフラグメントに基づくフォームのレンダリング](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-a-form-based-on-fragments-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Web サービス API を使用してフラグメントに基づいてフォームをレンダリングする {#render-forms-based-on-fragments-using-the-web-service-api}

Forms API（Web サービス）を使用して、フラグメントに基づいてフォームをレンダリングします。

1. プロジェクトファイルを含める

   * Forms Service WSDL を使用する Java プロキシクラスを作成します。
   * Java プロキシクラスをクラスパスに含めます。

1. Forms Client API オブジェクトの作成

   の作成 `FormsService` オブジェクトを選択し、認証値を設定します。

1. URI 値の指定

   * の作成 `URLSpec` コンストラクターを使用して URI 値を格納するオブジェクト。
   * を呼び出す `URLSpec` オブジェクトの `setApplicationWebRoot` メソッドを使用して、アプリケーションの Web ルートを表す string 値を渡します。
   * を呼び出す `URLSpec` オブジェクトの `setContentRootURI` メソッドを使用して、コンテンツルート URI 値を指定する string 値を渡します。 フォームデザインがコンテンツルート URI に配置されていることを確認します。 そうでない場合、Formsサービスは例外をスローします。 リポジトリを参照するには、次を指定します。 `repository://`.
   * を呼び出す `URLSpec` オブジェクトの `setTargetURL` メソッドを使用してターゲット URL 値を指定し、フォームデータの投稿先となる文字列値を渡します。 フォームデザインでターゲット URL を定義する場合、空の文字列を渡すことができます。 また、計算を実行するためのフォームの送信先の URL を指定することもできます。

1. フォームをレンダリング

   を呼び出す `FormsService` オブジェクトの `renderPDFForm` メソッドを使用して、次の値を渡します。

   * ファイル名拡張子を含むフォームデザイン名を指定する string 値。 Formsアプリケーションの一部であるフォームデザインを参照する場合は、必ず次のような完全なパスを指定してください。 `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * A `BLOB` フォームに結合するデータを含むオブジェクト。 データを結合しない場合は、 `null`.
   * A `PDFFormRenderSpec` 実行時オプションを保存するオブジェクト。 入力ドキュメントがPDFドキュメントの場合、「タグ付きPDF」オプションは設定できません。 入力ファイルが XDP ファイルの場合は、タグ付きPDFオプションを設定できます。
   * A `URLSpec` Formsサービスで必要な URI 値を含むオブジェクト。
   * A `java.util.HashMap` 添付ファイルを保存するオブジェクト。 これはオプションのパラメーターで、 `null` フォームにファイルを添付しない場合。
   * 空 `com.adobe.idp.services.holders.BLOBHolder` メソッドによって設定されるオブジェクト。 このパラメーターは、レンダリングされたフォームを保存するために使用されます。
   * 空 `javax.xml.rpc.holders.LongHolder` メソッドによって設定されるオブジェクト。 この引数は、フォームのページ数を保存します。
   * 空 `javax.xml.rpc.holders.StringHolder` メソッドによって設定されるオブジェクト。 この引数はロケール値を格納します。
   * 空 `com.adobe.idp.services.holders.FormsResultHolder` この操作の結果を格納するオブジェクト。

   この `renderPDFForm` メソッドによって `com.adobe.idp.services.holders.FormsResultHolder` オブジェクト。クライアント Web ブラウザーに書き込む必要があるフォームデータストリームを含む最後の引数値として渡されます。

1. フォームデータストリームをクライアント Web ブラウザーに書き込む

   * の作成 `FormResult` オブジェクトを作成するには、 `com.adobe.idp.services.holders.FormsResultHolder` オブジェクトの `value` データメンバー。
   * の作成 `BLOB` を呼び出してフォームデータを含むオブジェクト `FormsResult` オブジェクトの `getOutputContent` メソッド。
   * のコンテンツタイプを取得する `BLOB` オブジェクトを呼び出す `getContentType` メソッド。
   * を `javax.servlet.http.HttpServletResponse` を呼び出すことによるオブジェクトのコンテンツタイプ `setContentType` メソッドを使用して、 `BLOB` オブジェクト。
   * の作成 `javax.servlet.ServletOutputStream` オブジェクトを使用します。オブジェクトは、 `javax.servlet.http.HttpServletResponse` オブジェクトの `getOutputStream` メソッド。
   * バイト配列を作成し、 `BLOB` オブジェクトの `getBinaryData` メソッド。 このタスクは、 `FormsResult` オブジェクトをバイト配列に変換します。
   * を呼び出す `javax.servlet.http.HttpServletResponse` オブジェクトの `write` メソッドを使用して、フォームデータストリームをクライアント Web ブラウザーに送信します。 バイト配列を `write` メソッド。

**関連トピック**

[フラグメントに基づくFormsのレンダリング](#rendering-forms-based-on-fragments)

[Base64 エンコーディングを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
