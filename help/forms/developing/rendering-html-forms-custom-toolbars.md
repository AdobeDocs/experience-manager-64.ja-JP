---
title: CustomToolbars を使用したHTMLFormsのレンダリング
seo-title: Rendering HTML Forms with CustomToolbars
description: Formsサービスを使用して、ツールフォームでレンダリングされるツールバーをカスタマイズするHTMLを設定します。 Java API と Web サービス API を使用して、カスタムHTMLーを使用してツールバーフォームをレンダリングできます。
seo-description: Use the Forms service to customize a toolbar that is rendered with an HTML form. You can render an HTML Form with a custom toolbar using the Java API and a Web Service API.
uuid: b9c9464e-ff19-4051-a39b-4ec71c512d10
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: operations
discoiquuid: 7eb0e8a8-d76a-43f7-a012-c21157b14cd4
role: Developer
exl-id: f4711d21-59d3-482e-8059-9ef7c6008d21
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '2331'
ht-degree: 1%

---

# CustomToolbars を使用したHTMLFormsのレンダリング {#rendering-html-forms-with-customtoolbars}

## HTMLFormsとカスタムツールバーのレンダリング {#rendering-html-forms-with-custom-toolbars}

Formsサービスを使用すると、ツールバーフォームでレンダリングされるHTMLをカスタマイズできます。 ツールバーは、デフォルトの CSS スタイルを上書きすることで外観を変更したり、Java スクリプトを上書きして動的な動作を追加したりするように、カスタマイズできます。 ツールバーは、fscmenu.xml という名前の XML ファイルを使用してカスタマイズされます。 デフォルトでは、Formsサービスは内部的に指定された URI の場所からこのファイルを取得します。

>[!NOTE]
>
>この URI の場所は、adobe-forms-core.jar ファイル（ adobe-forms-dsc.jar ファイル）にあります。 adobe-forms-dsc.jar ファイルは、C:\Adobe\Adobe_Experience_Manager_forms\ folder (C:\ is the installation directory) にあります。 Win RAR などのファイル抽出ツールを使用して、アドビを開くことができます。

この場所から fscmenu.xml をコピーし、必要に応じて変更して、カスタム URI の場所に配置できます。 次に、Forms Service API を使用して、指定した場所の fscmenu.xml ファイルを使用してFormsサービスを実行する実行時オプションを設定します。 これらのアクションを実行すると、Formsサービスによって、カスタムHTMLを含むツールバーフォームがレンダリングされます。

fscmenu.xml ファイルに加えて、次のファイルも取得する必要があります。

* fscmenu.js
* fscattachments.js
* fscmenu.css
* fscmenu-v.css
* fscmenu-ie.css
* fscdialog.css

fscJS は、各ノードに関連付けられる Java スクリプトです。 用に供給する必要がある `div#fscmenu` ノードおよび（オプション） `ul#fscmenuItem` ノード。 JS ファイルはコアツールバー機能を実装し、デフォルトファイルが機能します。

fscCSS は、特定のノードに関連付けられているスタイルシートです。 CSS ファイルのスタイルによって、ツールバーの外観が指定されます。 *fscVCSS* は、レンダリングされたツールバーフォームの左側に表示される、縦向きのHTMLのスタイルシートです。 *fscIECSS* は、Internet Explorer でレンダリングされるHTMLフォームに使用されるスタイルシートです。

上記のすべてのファイルが fscmenu.xml ファイルで参照されていることを確認します。 つまり、fscmenu.xml ファイルで、これらのファイルを指す URI の場所を指定し、Formsサービスでそのファイルを検索できるようにします。 デフォルトでは、これらのファイルは、内部キーワードで始まる URI の場所で利用できます `FSWebRoot` または `ApplicationWebRoot`.

ツールバーをカスタマイズするには、外部キーワードを使用してキーワードを置き換えます `FSToolBarURI`. このキーワードは、実行時にFormsサービスに渡される URI を表します（この方法については、この節で後述します）。

また、これらの JS ファイルと CSS ファイルの絶対的な場所 ( 例：https://www.mycompany.com/scripts/misc/fscmenu.js) を指定することもできます。 この場合、 `FSToolBarURI` キーワード。

>[!NOTE]
>
>これらのファイルの参照方法を混在させることはお勧めしません。 つまり、すべての URI は、 `FSToolBarURI` キーワードまたは絶対位置。

JS ファイルと CSS ファイルを取得するには、adobe-forms-&lt;appserver>.ear ファイル。 このファイル内で、 adobe-forms-res.war を開きます。 これらのファイルはすべて WAR ファイルに格納されています。 adobe-forms-&lt;appserver>.ear ファイルは、AEM forms のインストールフォルダー (C:\ is the installation directory) にあります。 adobe-forms-&lt;appserver>WinRAR などのファイル抽出ツールを使用して.ear

次の XML 構文は、サンプルの fscmenu.xml ファイルを示しています。

```as3
 <div id="fscmenu" fscJS="FSToolBarURI/scripts/fscmenu.js" fscCSS="FSToolBarURI/fscmenu.css" fscVCSS="FSToolBarURI/fscmenu-v.css" fscIECSS="FSToolBarURI/fscmenu-ie.css"> 
         <ul class="fscmenuItem" id="Home"> 
             <li> 
                 <a href="#" fscTarget="_top" tabindex="1">Home</a> 
             </li> 
         </ul> 
         <ul class="fscmenuItem" id="Upload" fscJS="FSToolBarURI/scripts/fscattachments.js" fscCSS="FSToolBarURI/fscdialog.css"> 
             <li> 
                 <a tabindex="2">Upload Attachments</a> 
                 <ul class="fscmenuPopup" id="fscUploadAttachments"> 
                     <li> 
                         <a href="javascript:doUploadDialog();" tabindex="3">Add ...</a> 
                     </li> 
                     <li> 
                         <a href="javascript:doDeleteDialog();" tabindex="4">Delete ...</a> 
                     </li> 
                 </ul> 
             </li> 
         </ul> 
         <ul class="fscmenuItem" id="Download"> 
             <li> 
                 <a tabindex="100">Download Attachments</a> 
                 <ul class="fscmenuPopup"> 
                     <li> 
                         <a tabindex="101">None available</a> 
                     </li> 
                 </ul> 
             </li> 
         </ul> 
     </div>
```

>[!NOTE]
>
>太字のテキストは、参照する必要がある CSS および JS ファイルへの URI を表します。

次の項目では、ツールバーをカスタマイズする方法を説明します。

* 値の変更 `fscJS`, `fscCSS`, `fscVCSS`, `fscIECSS` 属性（ fscmenu.xml ファイル内）を使用して、このセクションで説明するメソッドの 1 つを使用して、参照されるファイルのカスタムの場所を反映します ( 例： `fscJS="FSToolBarURI/scripts/fscmenu.js"`) をクリックします。
* すべての CSS ファイルと JS ファイルを指定する必要があります。 どのファイルも変更されない場合は、カスタムの場所にデフォルトのファイルを指定します。 デフォルトのファイルを取得するには、この節で説明するように、様々なファイルを開きます。
* 任意のファイルの絶対参照 (https://www.example.com/scripts/custom-vertical-fscmenu.cssなど ) を指定することはできます。
* JS ファイルと CSS ファイル `div#fscmenu` ツールバー機能には、が必要なノードが不可欠です。 個人 `ul#fscmenuItem` ノードには、JS ファイルまたは CSS ファイルをサポートするものと、サポートしないものがあります。

**ローカル値の変更**

ツールバーのカスタマイズの一環として、ツールバーのロケール値を変更できます。 つまり、別の言語で表示できます。 次の図は、フランス語で表示されるカスタムツールバーを示しています。

>[!NOTE]
>
>複数の言語でカスタムツールバーを作成することはできません。 ツールバーは、ロケール設定に基づいて異なる XML ファイルを使用できません。

ツールバーのロケール値を変更するには、fscmenu.xml ファイルに表示する言語が含まれていることを確認します。 次の XML 構文は、フランス語のツールバーを表示するために使用される fscmenu.xml ファイルを示しています。

```as3
 <div id="fscmenu" fscJS="FSToolBarURI/scripts/fscmenu.js" fscCSS="FSToolBarURI/fscmenu.css" fscVCSS="FSToolBarURI/fscmenu-v.css" fscIECSS="FSToolBarURI/fscmenu-ie.css"> 
         <ul class="fscmenuItem" id="Home"> 
             <li> 
                 <a href="#" fscTarget="_top" tabindex="1">Accueil</a> 
             </li> 
         </ul> 
         <ul class="fscmenuItem" id="Upload" fscJS="FSToolBarURI/scripts/fscattachments.js" fscCSS="FSToolBarURI/fscdialog.css"> 
             <li> 
                 <a tabindex="2">Télécharger les pièces jointes</a> 
                 <ul class="fscmenuPopup" id="fscUploadAttachments"> 
                     <li> 
                         <a href="javascript:doUploadDialog();" tabindex="3">Ajouter...</a> 
                     </li> 
                     <li> 
                         <a href="javascript:doDeleteDialog();" tabindex="4">Supprimer...</a> 
                     </li> 
                 </ul> 
             </li> 
         </ul> 
         <ul class="fscmenuItem" id="Download"> 
             <li> 
                 <a tabindex="100">Télécharger les pièces jointes</a> 
                 <ul class="fscmenuPopup"> 
                     <li> 
                         <a tabindex="101">Aucune disponible</a> 
                     </li> 
                 </ul> 
             </li> 
         </ul> 
     </div>
```

>[!NOTE]
>
>このセクションに関連付けられているクイックスタートは、前の図に示すように、この XML ファイルを使用してフランス語のカスタムツールバーを表示します。

また、 `HTMLRenderSpec` オブジェクトの `setLocale` メソッドを使用して、ロケール値を指定する string 値を渡す。 例えば、 `fr_FR` フランス語を指定します。 Formsサービスは、ローカライズされたツールバーにバンドルされています。

>[!NOTE]
>
>カスタムHTMLを使用するツールバーフォームをレンダリングする前に、HTMLフォームのレンダリング方法を知っておく必要があります。 ( [FormsをHTMLとしてレンダリング](/help/forms/developing/rendering-forms-html.md).)

Formsサービスについて詳しくは、 [AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary-of-steps}

カスタムHTMLを含むツールバーフォームをレンダリングするには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. Forms Java API オブジェクトを作成します。
1. カスタム fscmenu XML ファイルを参照します。
1. HTMLフォームをレンダリング
1. フォームデータストリームをクライアントの Web ブラウザーに書き込みます。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。 Web サービスを使用している場合は、プロキシファイルを含めます。

**Forms Java API オブジェクトの作成**

Formsサービスがサポートする操作をプログラムで実行する前に、Formsクライアントオブジェクトを作成する必要があります。

**カスタム fscmenu XML ファイルの参照**

カスタムHTMLを含むツールバーフォームをレンダリングするには、ツールバーを記述する fscmenu XML ファイルを参照します。 （この節では、fscmenu XML ファイルの 2 つの例を示します）。 また、fscmenu.xml ファイルで、参照されるすべてのファイルの場所が正しく指定されていることを確認します。 この節で前述したように、すべてのファイルが `FSToolBarURI` キーワードまたはその絶対位置。

**HTMLフォームをレンダリング**

HTMLフォームをレンダリングするには、Designer で作成され XDP ファイルとして保存されたフォームデザインを指定します。 また、変換タイプとしてHTMLを選択します。 例えば、Internet Explorer 5.0 以降の動的HTMLをレンダリングするHTML変換の種類を指定できます。

また、HTMLフォームのレンダリングには、他のフォームタイプをレンダリングするための URI 値などの値も必要です。

**フォームデータストリームをクライアント Web ブラウザーに書き込む**

FormsサービスがHTMLフォームをレンダリングすると、フォームデータストリームが返されます。このストリームをクライアント Web ブラウザーに書き込み、HTMLフォームをユーザーに表示させる必要があります。

**関連トピック**

[Java API を使用して、カスタムHTMLーでツールバーフォームをレンダリングする](#render-an-html-form-with-a-custom-toolbar-using-the-java-api)

[Web サービス API を使用して、HTMLフォームをカスタムツールバーでレンダリングする](#rendering-an-html-form-with-a-custom-toolbar-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Forms Service API クイックスタート](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[インタラクティブPDF formsのレンダリング](/help/forms/developing/rendering-interactive-pdf-forms.md)

[FormsをHTMLとしてレンダリング](/help/forms/developing/rendering-forms-html.md)

[Formsをレンダリングする Web アプリケーションの作成](/help/forms/developing/creating-web-applications-renders-forms.md)

### Java API を使用して、カスタムHTMLーでツールバーフォームをレンダリングする {#render-an-html-form-with-a-custom-toolbar-using-the-java-api}

Forms Service API(Java) を使用して、カスタムHTMLを含むツールバーフォームをレンダリングします。

1. プロジェクトファイルを含める

   Java プロジェクトのクラスパスに、adobe-forms-client.jar などのクライアント JAR ファイルを含めます。

1. Forms Java API オブジェクトの作成

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用して `FormsServiceClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. カスタム fscmenu XML ファイルの参照

   * の作成 `HTMLRenderSpec` オブジェクトを指定します。
   * ツールバーを使用してHTMLフォームをレンダリングするには、 `HTMLRenderSpec` オブジェクトの `setHTMLToolbar` メソッドと `HTMLToolbar` enum 値。 例えば、縦のHTMLツールバーを表示するには、 `HTMLToolbar.Vertical`.
   * を呼び出して、fscmenu XML ファイルの場所を指定します。 `HTMLRenderSpec` オブジェクトの `setToolbarURI` メソッドを使用して、XML ファイルの URI の場所を指定する string 値を渡す。
   * 該当する場合は、 `HTMLRenderSpec` オブジェクトの `setLocale` メソッドを使用して、ロケール値を指定する string 値を渡す。 デフォルト値は英語です。

   >[!NOTE]
   >
   >このセクションに関連付けられているクイックスタートでは、この値をに設定します。 `fr_FR`*.*

1. HTMLフォームをレンダリング

   を呼び出す `FormsServiceClient` オブジェクトの `renderHTMLForm` メソッドを使用して、次の値を渡します。

   * ファイル名拡張子を含むフォームデザイン名を指定する string 値。 Formsアプリケーションの一部であるフォームデザインを参照する場合は、必ず次のような完全なパスを指定してください。 `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * A `TransformTo` HTMLの環境設定タイプを指定する enum 値。 例えば、Internet Explorer 5.0 以降の動的HTMLと互換性のあるHTMLフォームをレンダリングするには、次のように指定します。 `TransformTo.MSDHTML`.
   * A `com.adobe.idp.Document` フォームに結合するデータを含むオブジェクト。 データを結合しない場合は、空の `com.adobe.idp.Document` オブジェクト。
   * この `HTMLRenderSpec` オブジェクトを指定します。HTMLの実行時オプションが格納されます。
   * 次を指定する string 値 `HTTP_USER_AGENT` ヘッダー値（例： ） `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`.
   * A `URLSpec` オブジェクトを返します。
   * A `java.util.HashMap` 添付ファイルを保存するオブジェクト。 これはオプションのパラメーターで、 `null` フォームにファイルを添付しない場合。

   この `renderHTMLForm` メソッドは、 `FormsResult` クライアントの Web ブラウザーに書き込む必要があるフォームデータストリームを含むオブジェクト。

1. フォームデータストリームをクライアント Web ブラウザーに書き込む

   * の作成 `com.adobe.idp.Document` を呼び出すことによってオブジェクトを取得 `FormsResult` オブジェクト `getOutputContent` メソッド。
   * のコンテンツタイプを取得する `com.adobe.idp.Document` オブジェクトを呼び出す `getContentType` メソッド。
   * を `javax.servlet.http.HttpServletResponse` を呼び出すことによるオブジェクトのコンテンツタイプ `setContentType` メソッドを使用して、 `com.adobe.idp.Document` オブジェクト。
   * の作成 `javax.servlet.ServletOutputStream` オブジェクト。 `javax.servlet.http.HttpServletResponse` オブジェクトの `getOutputStream` メソッド。
   * の作成 `java.io.InputStream` を呼び出すことによってオブジェクトを取得 `com.adobe.idp.Document` オブジェクトの `getInputStream` メソッド。
   * バイト配列を作成し、 `InputStream` オブジェクトの `read` メソッドを使用し、バイト配列を引数として渡す。
   * を呼び出す `javax.servlet.ServletOutputStream` オブジェクトの `write` メソッドを使用して、フォームデータストリームをクライアント Web ブラウザーに送信します。 バイト配列を `write` メソッド。

**関連トピック**

[クイックスタート（SOAP モード）:Java API を使用した、カスタムHTMLでのツールバーでのツールバーフォームのレンダリング](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-an-html-form-with-a-custom-toolbar-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Web サービス API を使用して、HTMLフォームをカスタムツールバーでレンダリングする {#rendering-an-html-form-with-a-custom-toolbar-using-the-web-service-api}

Forms Service API（Web サービス）を使用して、カスタムHTMLを含むツールバーフォームをレンダリングします。

1. プロジェクトファイルを含める

   * Forms Service WSDL を使用する Java プロキシクラスを作成します。
   * クラスパスに Java プロキシクラスを含めます。

1. Forms Java API オブジェクトの作成

   の作成 `FormsService` オブジェクトを選択し、認証値を設定します。

1. カスタム fscmenu XML ファイルの参照

   * の作成 `HTMLRenderSpec` オブジェクトを指定します。
   * ツールバーを使用してHTMLフォームをレンダリングするには、 `HTMLRenderSpec` オブジェクトの `setHTMLToolbar` メソッドと `HTMLToolbar` enum 値。 例えば、縦のHTMLツールバーを表示するには、 `HTMLToolbar.Vertical`.
   * を呼び出して、fscmenu XML ファイルの場所を指定します。 `HTMLRenderSpec` オブジェクトの `setToolbarURI` メソッドを使用して、XML ファイルの URI の場所を指定する string 値を渡す。
   * 該当する場合は、 `HTMLRenderSpec` オブジェクトの `setLocale` メソッドを使用して、ロケール値を指定する string 値を渡す。 デフォルト値は英語です。

   >[!NOTE]
   >
   >このセクションに関連付けられているクイックスタートでは、この値をに設定します。 `fr_FR`*.*

1. HTMLフォームをレンダリング

   を呼び出す `FormsService` オブジェクトの `renderHTMLForm` メソッドを使用して、次の値を渡します。

   * ファイル名拡張子を含むフォームデザイン名を指定する string 値。 Formsアプリケーションの一部であるフォームデザインを参照する場合は、必ず次のような完全なパスを指定してください。 `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * A `TransformTo` HTMLの環境設定タイプを指定する enum 値。 例えば、Internet Explorer 5.0 以降の動的HTMLと互換性のあるHTMLフォームをレンダリングするには、次のように指定します。 `TransformTo.MSDHTML`.
   * A `BLOB` フォームに結合するデータを含むオブジェクト。 データを結合しない場合は、 `null`.
   * この `HTMLRenderSpec` オブジェクトを指定します。HTMLの実行時オプションが格納されます。
   * 次を指定する string 値 `HTTP_USER_AGENT` ヘッダー値（例： ） `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322`) をクリックします。 この値を設定しない場合は、空の文字列を渡すことができます。
   * A `URLSpec` オブジェクトを返します。
   * A `java.util.HashMap` 添付ファイルを保存するオブジェクト。 このパラメーターはオプションで、 `null` フォームにファイルを添付しない場合。
   * 空 `com.adobe.idp.services.holders.BLOBHolder` オブジェクト `renderHTMLForm` メソッド。 このパラメーター値は、レンダリングされたフォームを保存します。
   * 空 `com.adobe.idp.services.holders.BLOBHolder` オブジェクト `renderHTMLForm` メソッド。 このパラメーターは、出力 XML データを格納します。
   * 空 `javax.xml.rpc.holders.LongHolder` オブジェクト `renderHTMLForm` メソッド。 この引数は、フォームのページ数を保存します。
   * 空 `javax.xml.rpc.holders.StringHolder` オブジェクト `renderHTMLForm` メソッド。 この引数はロケール値を格納します。
   * 空 `javax.xml.rpc.holders.StringHolder` オブジェクト `renderHTMLForm` メソッド。 この引数は、使用されるHTMLレンダリング値を格納します。
   * 空 `com.adobe.idp.services.holders.FormsResultHolder` この操作の結果を格納するオブジェクト。

   この `renderHTMLForm` メソッドによって `com.adobe.idp.services.holders.FormsResultHolder` オブジェクト。クライアント Web ブラウザーに書き込む必要があるフォームデータストリームを含む最後の引数値として渡されます。

1. フォームデータストリームをクライアント Web ブラウザーに書き込む

   * の作成 `FormResult` オブジェクトを作成するには、 `com.adobe.idp.services.holders.FormsResultHolder` オブジェクトの `value` データメンバー。
   * の作成 `BLOB` を呼び出してフォームデータを含むオブジェクト `FormsResult` オブジェクトの `getOutputContent` メソッド。
   * のコンテンツタイプを取得する `BLOB` オブジェクトを呼び出す `getContentType` メソッド。
   * を `javax.servlet.http.HttpServletResponse` を呼び出すことによるオブジェクトのコンテンツタイプ `setContentType` メソッドを使用して、 `BLOB` オブジェクト。
   * の作成 `javax.servlet.ServletOutputStream` オブジェクト。 `javax.servlet.http.HttpServletResponse` オブジェクトの `getOutputStream` メソッド。
   * バイト配列を作成し、 `BLOB` オブジェクトの `getBinaryData` メソッド。 このタスクは、 `FormsResult` オブジェクトをバイト配列に変換します。
   * を呼び出す `javax.servlet.http.HttpServletResponse` オブジェクトの `write` メソッドを使用して、フォームデータストリームをクライアント Web ブラウザーに送信します。 バイト配列を `write` メソッド。

**関連トピック**

[Base64 エンコーディングを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
