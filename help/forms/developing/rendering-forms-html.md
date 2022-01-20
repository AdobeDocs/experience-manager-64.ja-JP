---
title: FormsをHTMLとしてレンダリング
seo-title: Rendering Forms as HTML
description: Formsサービスを使用して、Web ブラウザーからの HTTP 要求に応じてフォームをHTMLとしてレンダリングします。 Java API および Web Service API を使用して、フォームをHTMLとしてレンダリングできます。
seo-description: Use the Forms service to render forms as HTML in response to an HTTP request from a web browser. You can use the Java API and Web Service API to render forms as HTML.
uuid: bd8edb6f-333b-4ceb-9877-618f5377f56f
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: operations
discoiquuid: 669ede46-ea55-444b-a23f-23a86e5aff8e
role: Developer
exl-id: 2e8bcdf8-ae57-4ccd-945a-8f3fda4aa3c2
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '4137'
ht-degree: 1%

---

# FormsをHTMLとしてレンダリング {#rendering-forms-as-html}

Formsサービスは、Web ブラウザーからの HTTP 要求に応じて、フォームをHTMLとしてレンダリングします。 フォームをHTMLとしてレンダリングする利点の 1 つは、クライアント Web ブラウザーが配置されているコンピューターには、Adobe Reader、Acrobat、またはFlash Player( フォームガイド（非推奨）用 ) が必要ないことです。

フォームをHTMLとしてレンダリングするには、フォームデザインを XDP ファイルとして保存する必要があります。 PDFファイルとして保存されたフォームデザインは、HTMLとしてレンダリングできません。 Designer でフォームデザインを開発し、HTMLとしてレンダリングする場合は、以下の条件を考慮してください。

* フォームに線、ボックス、グリッドを描画するときに、オブジェクトの境界線プロパティを使用しないでください。ブラウザーによっては、 のプレビューで表示されるとおりに境界線が表示されないことがあります。また、オブジェクトが重なって表示されたり、他のオブジェクトを本来の位置から押しのけたりする場合があります。
* 線、長方形、円を使用して、背景を定義できます。
* テキストを収容するために必要と思われるサイズよりも少し大きいサイズでテキストを描画します。 一部の Web ブラウザーでは、読みやすくテキストが表示されません。

>[!NOTE]
>
>を使用して、画像を含むフォームをTIFFする場合、 `FormServiceClient` オブジェクトの `(Deprecated) renderHTMLForm` および `renderHTMLForm2` メソッドの場合、TIFF画像は、Internet Explorer または Mozilla Firefox ブラウザーに表示されるレンダリングされたHTMLフォームに表示されません。 これらのブラウザーでは、TIFF画像のネイティブサポートは提供されません。

## HTMLページ {#html-pages}

フォームデザインがHTMLフォームとしてレンダリングされる場合、各第 2 レベルサブフォームはHTMLページ（パネル）としてレンダリングされます。 サブフォームの階層は Designer で表示できます。 ルートサブフォームに属する子サブフォーム（ルートサブフォームのデフォルト名は form1）は、パネルのサブフォームです。 次に、フォームデザインのサブフォームの例を示します。

```as3
     form1 
         Master Pages 
         PanelSubform1 
             NestedDynamicSubform 
                 TextEdit1 
         PanelSubform2 
             TextEdit1 
         PanelSubform3 
             TextEdit1 
         PanelSubform4 
             TextEdit1
```

フォームデザインがHTMLフォームとしてレンダリングされる場合、パネルは特定のページサイズに制限されません。 ダイナミックサブフォームがある場合は、パネルサブフォーム内にネストする必要があります。 ダイナミックサブフォームは、無限数のHTMLページに拡張できます。

フォームをHTMLフォームとしてレンダリングする場合、ページサイズ (PDFとしてレンダリングされるフォームのページ番号付けに必要 ) は意味を持ちません。 編集可能なレイアウトを含むフォームはHTMLページを無限数まで拡張できるので、マスターページのフッターを避けることが重要です。 マスターページのコンテンツ領域の下にフッターを配置すると、ページ境界を越えてフローするHTMLコンテンツが上書きされる場合があります。

を使用して、パネル間を明示的に移動する必要があります。 `xfa.host.pageUp` および `xfa.host.pageDown` メソッド。 ページを変更するには、フォームをFormsサービスに送信し、Formsサービスでフォームをレンダリングしてクライアントデバイス（通常は Web ブラウザー）に戻す必要があります。

>[!NOTE]
>
>フォームをFormsサービスに送信し、Formsサービスでフォームをレンダリングしてクライアントデバイスに戻すプロセスは、サーバーへのラウンドトリッピングデータと呼ばれます。

>[!NOTE]
>
>HTMLフォーム上のHTMLの電子署名ボタンの外観をカスタマイズする場合は、fscdigsig.css ファイル（ adobe-forms-ds.ear / adobe-forms-ds.war ファイル内）で次のプロパティを変更する必要があります。

**.fsc-ds-ssb**:このスタイルシートは、空白の記号フィールドの場合に適用されます。

**.fsc-ds-ssv**:このスタイルシートは、「有効な記号」フィールドの場合に適用されます。

**.fsc-ds-ssc**:このスタイルシートは、有効な記号フィールドが適用されますが、データが変更された場合に適用されます。

**.fsc-ds-ssi**:このスタイルシートは、無効な記号フィールドの場合に適用されます。

**.fsc-ds-popup-bg**:このスタイルシートのプロパティは使用されていません。

**.fsc-ds-popup-btn**:このスタイルシートのプロパティは使用されていません。

## スクリプトの実行 {#running-scripts}

フォーム作成者は、スクリプトをサーバー上で実行するかクライアント上で実行するかを指定します。 Formsサービスは、フォームインテリジェンスを実行するための分散型イベント処理環境を作成します。この環境は、 `runAt` 属性。 この属性やフォームデザイン内でのスクリプトの作成について詳しくは、 [Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63)

Formsサービスは、フォームのレンダリング中にスクリプトを実行できます。 その結果、データベースに接続するか、クライアント上で使用できない Web サービスに接続することで、フォームにデータを事前入力できます。 また、ボタンの `Click` イベントを設定し、サーバー上で実行します。 これにより、ユーザーがフォームを操作している間に、エンタープライズデータベースなどのサーバーリソースを必要とする可能性のあるスクリプトをクライアントが実行できます。 HTMLフォームの場合、formcalc スクリプトはサーバー上でのみ実行できます。 その結果、次のスクリプトを実行するようにマークする必要があります `server` または `both`.

ページ（パネル）間を移動するフォームは、 `xfa.host.pageUp` および `xfa.host.pageDown` メソッド。 このスクリプトは、ボタンの `Click` イベントと `runAt` 属性が `Both`. 選択した理由 `Both` は、(PDFとしてレンダリングされるフォームの場合 )Adobe ReaderまたはAcrobatがサーバーに移動せずにページを変更でき、HTMLフォームがサーバーにデータを丸めてページを変更できるようにするためです。 つまり、フォームがFormsサービスに送信され、フォームがHTMLとしてレンダリングされ、新しいページが表示されます。

スクリプト変数やフォームフィールドには、item などの同じ名前を付けないことをお勧めします。 Internet Explorer などの一部の Web ブラウザーでは、フォームフィールドと同じ名前の変数が初期化されず、スクリプトエラーが発生する場合があります。 フォームフィールドとスクリプト変数に異なる名前を付けることをお勧めします。

ページナビゲーション機能とフォームスクリプトの両方を含むHTMLフォームをレンダリングする場合（例えば、フォームがレンダリングされるたびにスクリプトがデータベースからフィールドデータを取得すると仮定）、フォームスクリプトが form:readyevent 内ではなく form:calculate イベント内に配置されます。

form:ready イベントにあるフォームスクリプトは、フォームの最初のレンダリング時に 1 回だけ実行され、以降のページ取得時には実行されません。 これに対し、 form:calculate イベントは、フォームがレンダリングされるページナビゲーションごとに実行されます。

>[!NOTE]
複数ページフォームでは、JavaScript によってページに加えられた変更は、別のページに移動しても保持されません。

フォームを送信する前にカスタムスクリプトを呼び出すことができます。 この機能は、使用可能なすべてのブラウザーで機能します。 ただし、この変数は、ユーザーが独自の `Output Type` プロパティを `Form Body`. これは、 `Output Type` が `Full HTML`. この機能を設定する手順については、管理ヘルプのフォームの設定を参照してください。

フォームを送信する前に呼び出すコールバック関数を定義する必要があります。関数の名前はです `_user_onsubmit`. この関数は例外をスローしないと想定されます。例外がスローされた場合は無視されます。 JavaScript 関数は、html の head セクションに配置することをお勧めします。ただし、スクリプトタグの終わりより前の任意の場所で宣言することができます。 `xfasubset.js`.

formserver がコンボボックスを含む XDP をレンダリングすると、コンボボックスを作成するだけでなく、2 つの非表示テキストフィールドも作成されます。 これらのテキストフィールドには、ドロップダウンリストのデータが格納されます（一方にはオプションの表示名が格納され、もう一方にはオプションの値が格納されます）。 したがって、ユーザーがフォームを送信するたびに、ドロップダウンリストのデータ全体が送信されます。 毎回それほど多くのデータを送信したくない場合は、それを無効にするカスタムスクリプトを作成できます。 例：ドロップダウンリストの名前は次のとおりです。 `drpOrderedByStateProv` サブフォームヘッダーの下にラップされます。 HTML入力要素の名前は、 `header[0].drpOrderedByStateProv[0]`. ドロップダウンのデータを保存して送信する非表示フィールドの名前には、次の名前が付けられます。 `header[0].drpOrderedByStateProv_DISPLAYITEMS_[0] header[0].drpOrderedByStateProv_VALUEITEMS_[0]`

データを投稿しない場合は、次の方法でこれらの入力要素を無効にできます。 `var __CUSTOM_SCRIPTS_VERSION = 1; //enabling the feature function _user_onsubmit() { var elems = document.getElementsByName("header[0].drpOrderedByStateProv_DISPLAYITEMS_[0]"); elems[0].disabled = true; elems = document.getElementsByName("header[0].drpOrderedByStateProv_VALUEITEMS_[0]"); elems[0].disabled = true; }`

```as3
header[0].drpOrderedByStateProv_DISPLAYITEMS_[0] header[0].drpOrderedByStateProv_VALUEITEMS_[0]
```

```as3
var __CUSTOM_SCRIPTS_VERSION = 1; //enabling the feature 
    function _user_onsubmit() { 
    var elems = document.getElementsByName("header[0].drpOrderedByStateProv_DISPLAYITEMS_[0]"); 
    elems[0].disabled = true; 
    elems = document.getElementsByName("header[0].drpOrderedByStateProv_VALUEITEMS_[0]"); 
    elems[0].disabled = true; 
    }
```

## XFA サブセット {#xfa-subsets}

HTMLとしてレンダリングするフォームデザインを作成する場合は、スクリプトを JavaScript 言語のスクリプトの XFA サブセットに制限する必要があります。

クライアント上で実行される、またはクライアントとサーバーの両方で実行されるスクリプトは、XFA サブセット内で記述する必要があります。 サーバー上で実行されるスクリプトは、完全な XFA スクリプティングモデルを使用でき、FormCalc も使用できます。 JavaScript の使用について詳しくは、 [Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63).

クライアントでスクリプトを実行する場合、表示されている現在のパネルだけがスクリプトを使用できます。例えば、パネル B が表示されている場合に、パネル A にあるフィールドに対してスクリプトを作成することはできません。 サーバーでスクリプトを実行すると、すべてのパネルにアクセスできます。

また、クライアントで実行するスクリプト内で Scripting Object Model(SOM) 式を使用する場合は注意が必要です。 SOM 式のシンプルなサブセットのみが、クライアントで実行されるスクリプトでサポートされます。

## イベントのタイミング {#event-timing}

XFA サブセットは、イベントイベントイベントにマッピングされる XFAHTMLを定義します。 イベントの計算と検証のタイミングでの動作には、若干の違いがあります。 Web ブラウザーでは、フィールドを終了すると、完全な calculate イベントが実行されます。 フィールド値を変更した場合、calculate イベントは自動的には実行されません。 計算イベントを強制的に実行するには、 `xfa.form.execCalculate` メソッド。

Web ブラウザーでは、検証イベントは、フィールドを終了するかフォームを送信する場合にのみ実行されます。 validate イベントを強制的に実行するには、 `xfa.form.execValidate` メソッド。

Web ブラウザーに表示されるForms(Adobe ReaderやAcrobatとは異なり ) は、必須フィールドの XFA null テスト（エラーまたは警告）に準拠しています。

* null テストでエラーが発生し、値を指定せずにフィールドを終了した場合は、メッセージボックスが表示され、「OK」をクリックした後にそのフィールドに再配置されます。
* null テストで警告が生成され、値を指定せずにフィールドを終了した場合は、[OK] または [ キャンセル ] をクリックすると、値を指定せずに続行するか、値を入力するフィールドに戻るかのオプションが表示されます。

null テストの詳細については、 [Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63).

## フォームボタン {#form-buttons}

送信ボタンをクリックすると、フォームデータがFormsサービスに送信され、フォーム処理の終了を表します。 この `preSubmit` イベントは、クライアントまたはサーバーで実行するように設定できます。 この `preSubmit` イベントは、フォーム送信の前に実行されます（クライアント上で実行するように設定されている場合）。 それ以外の場合は、 `preSubmit` イベントは、フォームの送信中にサーバーで実行されます。 詳しくは、 `preSubmit` イベント： [Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63).

ボタンにクライアント側のスクリプトが関連付けられていない場合、データがサーバーに送信され、計算がサーバー上で実行され、HTMLフォームが再生成されます。 ボタンにクライアント側のスクリプトが含まれている場合、データはサーバーに送信されず、クライアント側のスクリプトが Web ブラウザーで実行されます。

## HTML4.0 Web ブラウザー {#html-4-0-web-browser}

HTML4.0 のみをサポートする Web ブラウザーは、XFA サブセットのクライアント側スクリプティングモデルをサポートできません。 HTML4.0 と MSDHTML または CSS2 の両方のHTMLで動作するフォームデザインを作成する場合、クライアントで実行するようにマークされたスクリプトは、実際にサーバー上で実行されます。 例えば、HTML4.0 Web ブラウザーで表示されているフォーム上のボタンをユーザーがクリックしたとします。 この場合、クライアント側スクリプトが実行されるサーバーにフォームデータが送信されます。

HTML4.0 のサーバーと、MSDHTML または CSS2HTML用のクライアントで実行する calculate イベントに、フォームロジックを配置することをお勧めします。

## プレゼンテーションの変更の管理 {#maintaining-presentation-changes}

HTMLページ（パネル）間を移動すると、データの状態のみが保持されます。 背景色や必須フィールド設定などの設定は維持されません（初期設定と異なる場合）。 プレゼンテーションの状態を維持するには、フィールドのプレゼンテーションの状態を表すフィールド（通常は非表示）を作成する必要があります。 フィールドの `Calculate` イベントを使用して非表示のフィールドの値に基づいてプレゼンテーションを変更する場合、HTMLページ（パネル）間を行ったり来たりする際に、プレゼンテーションの状態を保持することができます。

次のスクリプトでは、 `fillColor` の値に基づくフィールドの `hiddenField`. このスクリプトがフィールドの `Calculate` イベント。

```as3
     If (hiddenField.rawValue == 1) 
         this.fillColor = "255,0,0" 
     else 
         this.fillColor = "0,255,0"
```

>[!NOTE]
テーブルのセル内にネストされている場合、スタティックオブジェクトはレンダリングHTMLフォームに表示されません。 例えば、テーブルのセル内にネストされた円や長方形は、レンダリングHTMLフォーム内に表示されません。 ただし、テーブルの外側に配置されている場合は、同じスタティックオブジェクトが正しく表示されます。

## デジタル署名HTMLフォーム {#digitally-signing-html-forms}

フォームが以下のHTML変換のいずれかとしてレンダリングされる場合、電子署名フィールドを含む署名フォームにはHTMLできません。

* AHTML
* HTML4
* StaticHTML
* NoScriptXHTML

ドキュメントのデジタル署名については、 [ドキュメントのデジタル署名と認証](/help/forms/developing/digitally-signing-certifying-documents.md)

## アクセシビリティガイドラインに準拠した XHTML フォームのレンダリング {#rendering-an-accessibility-guidelines-compliant-xhtml-form}

アクセシビリティガイドラインに準拠するHTMLフォームを完全にレンダリングできます。 つまり、フォームはフルHTMLタグ内でレンダリングされます。これは、HTMLフォームが ( 完全なHTMLページではなく )body タグ内でレンダリングされるのとは異なります。

## フォームデータの検証 {#validating-form-data}

フォームをHTMLフォームとしてレンダリングする場合、フォームフィールドに対する検証ルールの使用を制限することをお勧めします。 一部の検証ルールは、検証フォームでサポートされていない可能性がHTMLされます。 例えば、MM-DD-YYYY という検証パターンが `Date/Time` HTMLフォームとしてレンダリングされるフォームデザインにあるフィールド。日付が正しく入力されている場合でも、正しく機能しません。 ただし、この検証パターンは、PDFとしてレンダリングされたフォームに対して適切に機能します。

>[!NOTE]
Formsサービスについて詳しくは、 [AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63).

## 手順の概要 {#summary-of-steps}

HTMLフォームをレンダリングするには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. Forms Client API オブジェクトを作成します。
1. HTMLの実行時オプションを設定します。
1. HTMLフォームをレンダリング
1. フォームデータストリームをクライアントの Web ブラウザーに書き込みます。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。 Web サービスを使用している場合は、プロキシファイルを必ず含めてください。

**Forms Client API オブジェクトの作成**

プログラムによってデータをPDFformClient API に読み込む前に、Form Data Integration サービスクライアントを作成する必要があります。 サービスクライアントを作成する場合、サービスを呼び出すために必要な接続設定を定義します。

**HTML実行時オプションを設定**

HTMLフォームのレンダリング時に、HTML実行時オプションを設定します。 例えば、HTMLフォームにツールバーを追加して、クライアントコンピューター上の添付ファイルを選択したり、HTMLフォームでレンダリングされる添付ファイルを取得したりできます。 デフォルトでは、HTMLツールバーは無効です。 ツールバーをHTMLフォームに追加するには、プログラムによって実行時オプションを設定する必要があります。 デフォルトでは、HTMLツールバーは次のボタンで構成されています。

* `Home`:アプリケーションの Web ルートへのリンクを提供します。
* `Upload`:現在のフォームに添付するファイルを選択するためのユーザーインターフェイスを提供します。
* `Download`:添付ファイルを表示するユーザインタフェースを提供します。

HTMLフォーム上にHTMLツールバーが表示されている場合、ユーザーは最大 10 個のファイルを選択して、フォームデータと共に送信できます。 ファイルが送信されると、Formsサービスはファイルを取得できます。

フォームをHTMLとしてレンダリングする際に、user-agent 値を指定できます。 user-agent 値は、ブラウザーとシステムの情報を提供します。 これはオプションの値で、空の文字列値を渡すことができます。 Java API を使用したHTMLフォームのレンダリングクイックスタートでは、ユーザーエージェントの値を取得し、それを使用してフォームをHTMLとしてレンダリングする方法を示しています。

フォームデータの投稿先となる HTTP URL は、Forms Service Client API を使用してターゲット URL を設定することで指定できます。また、XDP フォームデザインに含まれる「送信」ボタンで指定することもできます。 ターゲット URL がフォームデザインで指定されている場合は、Forms Service Client API を使用して値を設定しないでください。

>[!NOTE]
ツールバーを含むHTMLフォームのレンダリングはオプションです。

>[!NOTE]
AHTML フォームをレンダリングする場合は、ツールバーをフォームに追加しないことをお勧めします。

**HTMLフォームをレンダリング**

HTMLフォームをレンダリングするには、Designer で作成し、XDP ファイルとして保存したフォームデザインを指定する必要があります。 また、変換タイプを選択する必要があるHTMLもあります。 例えば、Internet Explorer 5.0 以降の動的HTMLをレンダリングするHTML変換の種類を指定できます。

HTMLフォームのレンダリングには、他のフォームタイプのレンダリングに必要な URI 値などの値も必要です。

**フォームデータストリームをクライアント Web ブラウザーに書き込む**

FormsサービスがHTMLフォームをレンダリングすると、クライアントの Web ブラウザーに書き込む必要があるフォームデータストリームが返されます。 クライアント Web ブラウザーに書き込まれると、HTMLフォームがユーザーに対して表示されます。

**関連トピック**

[Java API を使用してフォームをHTMLとしてレンダリングする](#render-a-form-as-html-using-the-java-api)

[Web サービス API を使用してフォームをHTMLとしてレンダリングする](#render-a-form-as-html-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Forms Service API クイックスタート](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[インタラクティブPDF formsのレンダリング](/help/forms/developing/rendering-interactive-pdf-forms.md)

[HTMLFormsとカスタムツールバーのレンダリング](/help/forms/developing/rendering-html-forms-custom-toolbars.md)

[Formsをレンダリングする Web アプリケーションの作成](/help/forms/developing/creating-web-applications-renders-forms.md)

## Java API を使用してフォームをHTMLとしてレンダリングする {#render-a-form-as-html-using-the-java-api}

Forms API(Java) を使用してHTMLフォームをレンダリングします。

1. プロジェクトファイルを含める

   Java プロジェクトのクラスパスに、adobe-forms-client.jar などのクライアント JAR ファイルを含めます。

1. Forms Client API オブジェクトの作成

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * の作成 `FormsServiceClient` オブジェクトのコンストラクタを使用し、 `ServiceClientFactory` オブジェクト。

1. HTML実行時オプションを設定

   * の作成 `HTMLRenderSpec` オブジェクトを指定します。
   * ツールバーを使用してHTMLフォームをレンダリングするには、 `HTMLRenderSpec` オブジェクトの `setHTMLToolbar` メソッドと `HTMLToolbar` enum 値。 例えば、縦のHTMLツールバーを表示するには、 `HTMLToolbar.Vertical`.
   * ロケールフォームのロケール値を設定するには、HTMLフォームで `HTMLRenderSpec` オブジェクトの `setLocale` メソッドを使用し、ロケール値を指定する string 値を渡します。 （これはオプションの設定です）。
   * 完全なHTMLタグ内でHTMLフォームをレンダリングするには、 `HTMLRenderSpec` オブジェクトの `setOutputType` メソッドとパス `OutputType.FullHTMLTags`. （これはオプションの設定です）。

   >[!NOTE]
   Formsは、 `StandAlone` オプションは `true` そして `ApplicationWebRoot` は、AEM Forms( `ApplicationWebRoot` 値が `URLSpec` オブジェクト `FormsServiceClient` オブジェクトの `(Deprecated) renderHTMLForm` メソッド )。 次の場合に `ApplicationWebRoot`*は、AEM Formsをホストしている別のサーバーです。管理コンソールの Web ルート URI の値を、フォームの Web アプリケーションの URI 値として設定する必要があります。 これをおこなうには、管理コンソールにログインして、サービス/Formsをクリックし、「 Web ルート URI 」をhttps://server-name:port/FormServerに設定します。 次に、設定を保存します。*

1. HTMLフォームをレンダリング

   を呼び出す `FormsServiceClient` オブジェクトの `(Deprecated) renderHTMLForm` メソッドを使用して、次の値を渡します。

   * ファイル名拡張子を含むフォームデザイン名を指定する string 値。 Formsアプリケーションの一部であるフォームデザインを参照する場合は、必ず次のような完全なパスを指定してください。 `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * A `TransformTo` HTMLの環境設定タイプを指定する enum 値。 例えば、Internet Explorer 5.0 以降の動的HTMLと互換性のあるHTMLフォームをレンダリングするには、次のように指定します。 `TransformTo.MSDHTML`.
   * A `com.adobe.idp.Document` フォームに結合するデータを含むオブジェクト。 データを結合しない場合は、空の `com.adobe.idp.Document` オブジェクト。
   * この `HTMLRenderSpec` オブジェクトを指定します。HTMLの実行時オプションが格納されます。
   * 次を指定する string 値 `HTTP_USER_AGENT` ヘッダー値；例： `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`.
   * A `URLSpec` オブジェクトフォームのレンダリングに必要な URI 値をHTMLするオブジェクト。
   * A `java.util.HashMap` 添付ファイルを保存するオブジェクト。 これはオプションのパラメーターで、 `null` フォームにファイルを添付しない場合。

   この `(Deprecated) renderHTMLForm` メソッドは、 `FormsResult` クライアントの Web ブラウザーに書き込むことができるフォームデータストリームを含むオブジェクト。

1. フォームデータストリームをクライアント Web ブラウザーに書き込む

   * の作成 `com.adobe.idp.Document` を呼び出すことによってオブジェクトを取得 `FormsResult` オブジェクト `getOutputContent` メソッド。
   * のコンテンツタイプを取得する `com.adobe.idp.Document` オブジェクトを呼び出す `getContentType` メソッド。
   * を `javax.servlet.http.HttpServletResponse` を呼び出すことによるオブジェクトのコンテンツタイプ `setContentType` メソッドを使用して、 `com.adobe.idp.Document` オブジェクト。
   * の作成 `javax.servlet.ServletOutputStream` オブジェクトを使用します。オブジェクトは、 `javax.servlet.http.HttpServletResponse` オブジェクトの `getOutputStream` メソッド。
   * の作成 `java.io.InputStream` を呼び出すことによってオブジェクトを取得 `com.adobe.idp.Document` オブジェクトの `getInputStream` メソッド。
   * バイト配列を作成し、 `InputStream` オブジェクトの `read` メソッドを使用し、バイト配列を引数として渡す。
   * を呼び出す `javax.servlet.ServletOutputStream` オブジェクトの `write` メソッドを使用して、フォームデータストリームをクライアント Web ブラウザーに送信します。 バイト配列を `write` メソッド。

**関連トピック**

[FormsをHTMLとしてレンダリング](#rendering-forms-as-html)

[クイックスタート（SOAP モード）:Java API を使用したHTMLフォームのレンダリング](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-an-html-form-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Web サービス API を使用してフォームをHTMLとしてレンダリングする {#render-a-form-as-html-using-the-web-service-api}

Forms API（Web サービス）を使用してHTMLフォームをレンダリングします。

1. プロジェクトファイルを含める

   * Forms Service WSDL を使用する Java プロキシクラスを作成します。
   * Java プロキシクラスをクラスパスに含めます。

1. Forms Client API オブジェクトの作成

   の作成 `FormsService` オブジェクトを選択し、認証値を設定します。

1. HTML実行時オプションを設定

   * の作成 `HTMLRenderSpec` オブジェクトを指定します。
   * ツールバーを使用してHTMLフォームをレンダリングするには、 `HTMLRenderSpec` オブジェクトの `setHTMLToolbar` メソッドと `HTMLToolbar` enum 値。 例えば、縦のHTMLツールバーを表示するには、 `HTMLToolbar.Vertical`.
   * ロケールフォームのロケール値を設定するには、HTMLフォームで `HTMLRenderSpec` オブジェクトの `setLocale` メソッドを使用し、ロケール値を指定する string 値を渡します。 詳しくは、 [AEM Forms API リファレンス](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).
   * 完全なHTMLタグ内でHTMLフォームをレンダリングするには、 `HTMLRenderSpec` オブジェクトの `setOutputType` メソッドとパス `OutputType.FullHTMLTags`.

   >[!NOTE]
   Formsは、 `StandAlone` オプションは `true` そして `ApplicationWebRoot` は、AEM Forms( `ApplicationWebRoot` 値が `URLSpec` オブジェクト `FormsServiceClient` オブジェクトの `(Deprecated) renderHTMLForm` メソッド )。 次の場合に `ApplicationWebRoot`*は、AEM Formsをホストしている別のサーバーです。管理コンソールの Web ルート URI の値を、フォームの Web アプリケーションの URI 値として設定する必要があります。 これをおこなうには、管理コンソールにログインして、サービス/Formsをクリックし、「 Web ルート URI 」をhttps://server-name:port/FormServerに設定します。 次に、設定を保存します。*

1. HTMLフォームをレンダリング

   を呼び出す `FormsService` オブジェクトの `(Deprecated) renderHTMLForm` メソッドを使用して、次の値を渡します。

   * ファイル名拡張子を含むフォームデザイン名を指定する string 値。 Formsアプリケーションの一部であるフォームデザインを参照する場合は、必ず次のような完全なパスを指定してください。 `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * A `TransformTo` HTMLの環境設定タイプを指定する enum 値。 例えば、Internet Explorer 5.0 以降の動的HTMLと互換性のあるHTMLフォームをレンダリングするには、次のように指定します。 `TransformTo.MSDHTML`.
   * A `BLOB` フォームに結合するデータを含むオブジェクト。 データを結合しない場合は、 `null`. ( [編集可能なレイアウトを使用したFormsの事前入力](/help/forms/developing/prepopulating-forms-flowable-layouts.md#prepopulating-forms-with-flowable-layouts).)
   * この `HTMLRenderSpec` オブジェクトを指定します。HTMLの実行時オプションが格納されます。
   * 次を指定する string 値 `HTTP_USER_AGENT` ヘッダー値；例： `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`. この値を設定しない場合は、空の文字列を渡すことができます。
   * A `URLSpec` オブジェクトフォームのレンダリングに必要な URI 値をHTMLするオブジェクト。 ( [URI 値の指定](/help/forms/developing/rendering-interactive-pdf-forms.md).)
   * A `java.util.HashMap` 添付ファイルを保存するオブジェクト。 これはオプションのパラメーターで、 `null` フォームにファイルを添付しない場合。 ( [フォームにファイルを添付する](/help/forms/developing/rendering-interactive-pdf-forms.md).)
   * 空 `com.adobe.idp.services.holders.BLOBHolder` メソッドによって設定されるオブジェクト。 このパラメーター値は、レンダリングされたフォームを保存します。
   * 空 `com.adobe.idp.services.holders.BLOBHolder` メソッドによって設定されるオブジェクト。 このパラメーターは出力 XML データを格納します。
   * 空 `javax.xml.rpc.holders.LongHolder` メソッドによって設定されるオブジェクト。 この引数は、フォームのページ数を保存します。
   * 空 `javax.xml.rpc.holders.StringHolder` メソッドによって設定されるオブジェクト。 この引数はロケール値を格納します。
   * 空 `javax.xml.rpc.holders.StringHolder` メソッドによって設定されるオブジェクト。 この引数は、使用されるHTMLレンダリング値を格納します。
   * 空 `com.adobe.idp.services.holders.FormsResultHolder` この操作の結果を格納するオブジェクト。

   この `(Deprecated) renderHTMLForm` メソッドによって `com.adobe.idp.services.holders.FormsResultHolder` オブジェクト。クライアント Web ブラウザーに書き込む必要があるフォームデータストリームを含む最後の引数値として渡されます。

1. フォームデータストリームをクライアント Web ブラウザーに書き込む

   * の作成 `FormResult` オブジェクトを作成するには、 `com.adobe.idp.services.holders.FormsResultHolder` オブジェクトの `value` データメンバー。
   * の作成 `BLOB` を呼び出してフォームデータを含むオブジェクト `FormsResult` オブジェクトの `getOutputContent` メソッド。
   * のコンテンツタイプを取得する `BLOB` オブジェクトを呼び出す `getContentType` メソッド。
   * を `javax.servlet.http.HttpServletResponse` を呼び出すことによるオブジェクトのコンテンツタイプ `setContentType` メソッドを使用して、 `BLOB` オブジェクト。
   * の作成 `javax.servlet.ServletOutputStream` オブジェクトを使用します。オブジェクトは、 `javax.servlet.http.HttpServletResponse` オブジェクトの `getOutputStream` メソッド。
   * バイト配列を作成し、 `BLOB` オブジェクトの `getBinaryData` メソッド。 このタスクは、 `FormsResult` オブジェクトをバイト配列に変換します。
   * を呼び出す `javax.servlet.http.HttpServletResponse` オブジェクトの `write` メソッドを使用して、フォームデータストリームをクライアント Web ブラウザーに送信します。 バイト配列を `write` メソッド。

**関連トピック**

[FormsをHTMLとしてレンダリング](#rendering-forms-as-html)

[Base64 エンコーディングを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
