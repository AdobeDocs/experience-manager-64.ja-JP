---
title: HTMLとしてのフォームのレンダリング
seo-title: HTMLとしてのフォームのレンダリング
description: 'null'
seo-description: 'null'
uuid: bd8edb6f-333b-4ceb-9877-618f5377f56f
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: operations
discoiquuid: 669ede46-ea55-444b-a23f-23a86e5aff8e
translation-type: tm+mt
source-git-commit: 340c267fc4e142a67ae5be3f1ab11f063417962e

---


# HTMLとしてのフォームのレンダリング {#rendering-forms-as-html}

Formsサービスは、WebブラウザーからのHTTP要求に応じて、フォームをHTMLとしてレンダリングします。 HTML形式でフォームをレンダリングする利点は、クライアントWebブラウザーが配置されているコンピューターで、Adobe Reader、AcrobatまたはFlash Player(フォームガイド（非推奨）用)が不要であることです。

フォームをHTMLとしてレンダリングするには、フォームデザインをXDPファイルとして保存する必要があります。 PDFファイルとして保存されたフォームデザインはHTMLとしてレンダリングできません。 HTMLとしてレンダリングされるDesignerでフォームデザインを開発する場合は、次の条件を考慮します。

* フォームに線、ボックス、グリッドを描画するときに、オブジェクトの境界線プロパティを使用しないでください。ブラウザーによっては、 のプレビューで表示されるとおりに境界線が表示されないことがあります。また、オブジェクトが重なって表示されたり、他のオブジェクトを本来の位置から押しのけたりする場合があります。
* 線、長方形、円を使用して、背景を定義できます。
* テキストを収容するために必要と思われるサイズよりも少し大きなサイズで描画します。 一部のWebブラウザーでは、テキストが見やすく表示されません。

>[!NOTE]
>
>TIFF画像を含むフォームをオブジェクトおよびメソッドを使用し `FormServiceClient``(Deprecated) renderHTMLForm``renderHTMLForm2` てレンダリングする場合、TIFF画像は、Internet ExplorerまたはMozilla Firefoxブラウザーで表示されるレンダリングされたHTMLフォームには表示されません。 これらのブラウザーは、TIFF画像をネイティブでサポートしていません。

## HTMLページ {#html-pages}

フォームデザインがHTMLフォームとしてレンダリングされると、2番目の各サブフォームはHTMLページ（パネル）としてレンダリングされます。 Designerでは、サブフォームの階層を表示できます。 ルートサブフォームに属する子サブフォーム（ルートサブフォームのデフォルト名はform1）は、パネルサブフォームです。 次の例は、フォームデザインのサブフォームを示しています。

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

フォームデザインがHTMLフォームとしてレンダリングされる場合、パネルは特定のページサイズに制限されません。 ダイナミックサブフォームがある場合は、パネルサブフォーム内に階層化する必要があります。 ダイナミックサブフォームは、HTMLページを無限に拡大できます。

フォームをHTMLフォームとしてレンダリングする場合、ページサイズ（PDFとしてレンダリングされたフォームのページ番号付けに必要）は意味を持ちません。 編集可能なレイアウトを含むフォームは、HTMLページを無限に拡大できるので、マスターページのフッターを避けることが重要です。 マスターページのコンテンツ領域の下のフッターは、ページの境界を越えてフローするHTMLコンテンツを上書きする場合があります。

とメソッドを使用して、パネル間を明示的に移動する必 `xfa.host.pageUp` 要があ `xfa.host.pageDown` ります。 ページを変更するには、フォームをFormsサービスに送信し、Formsサービスでフォームをクライアントデバイス（通常はWebブラウザー）にレンダリングし直します。

>[!NOTE]
>
>フォームをFormsサービスに送信し、Formsサービスでフォームをクライアントデバイスにレンダリングして戻すプロセスは、サーバーへのデータのラウンドトリッピングと呼ばれます。

>[!NOTE]
>
>HTMLフォーム上の「HTMLデジタル署名」ボタンの外観をカスタマイズする場合は、fscdigsig.cssファイル（adobe-forms-ds.ear内の「adobe-forms-ds.war」ファイル）で次のプロパティを変更する必要があります。

**.fsc-ds-ssb**:このスタイルシートは、空白の記号フィールドの場合に適用されます。

**.fsc-ds-ssv**:このスタイルシートは、有効な記号フィールドの場合に適用されます。

**.fsc-ds-ssc**:このスタイルシートは、有効な符号フィールドが適用されるが、データが変更された場合に適用されます。

**.fsc-ds-ssi**:このスタイルシートは、無効な記号フィールドの場合に適用されます。

**.fsc-ds-popup-bg**:このスタイルシートのプロパティは使用されていません。

**.fsc-ds-popup-btn**:このスタイルシートのプロパティは使用されていません。

## スクリプトの実行 {#running-scripts}

フォーム作成者は、スクリプトをサーバー上で実行するか、クライアント上で実行するかを指定します。 Formsサービスは、属性を使用してクライアントとサーバーの間で配布できるフォームインテリジェンスを実行する、分散されたイベント処理環境を作成 `runAt` します。 この属性やフォームデザイン内でのスクリプトの作成について詳しくは、「 [Forms Designer」を参照してください](https://www.adobe.com/go/learn_aemforms_designer_63)

Formsサービスは、フォームのレンダリング中にスクリプトを実行できます。 その結果、データベースまたはクライアントで使用できないWebサービスに接続して、フォームにデータを事前入力できます。 また、サーバー上で実行するボタンの `Click` イベントを設定して、クライアントがサーバーに旅行データを丸めるようにすることもできます。 これにより、ユーザーがフォームを操作している間に、エンタープライズデータベースなどのサーバーリソースを必要とする可能性のあるスクリプトをクライアントが実行できます。 HTMLフォームの場合、formcalcスクリプトはサーバー上でのみ実行できます。 その結果、またはで実行するスクリプトをマークする必要が `server` ありま `both`す。

メソッドとメソッドを呼び出して、ページ（パネル）間を移動するフォームをデザ `xfa.host.pageUp` インで `xfa.host.pageDown` きます。 このスクリプトはボタンの `Click` イベントに配置さ `runAt` れ、属性はに設定されま `Both`す。 選択した理由は、Adobe Readerま `Both` たはAcrobat（PDFとしてレンダリングされるフォームの場合）がサーバーに移動せずにページを変更でき、HTMLフォームがデータをサーバーに丸めてトリッピングすることでページを変更できるようにするためです。 つまり、フォームがFormsサービスに送信され、フォームがHTMLとしてレンダリングされ、新しいページが表示されます。

スクリプト変数とフォームフィールドには、itemなどの同じ名前を付けないことをお勧めします。 Internet Explorerなどの一部のWebブラウザーでは、フォームフィールドと同じ名前の変数が初期化されず、スクリプトエラーが発生する場合があります。 フォームフィールドとスクリプト変数には異なる名前を付けることをお勧めします。

ページナビゲーション機能とフォームスクリプトの両方を含むHTMLフォームをレンダリングする場合（例えば、フォームをレンダリングするたびにスクリプトがデータベースからフィールドデータを取得する場合）、フォームスクリプトがform:readyeventではなくform:calculateイベントーに配置されていることを確認します。

form:readyイベントにあるフォームスクリプトは、フォームの最初のレンダリング時に1回だけ実行され、以降のページ取得時には実行されません。 これに対し、form:calculateイベントは、フォームがレンダリングされるページナビゲーションごとに実行されます。

>[!NOTE]
複数ページのフォームでは、JavaScriptによってページに加えられた変更は、別のページに移動しても保持されません。

フォームを送信する前に、カスタムスクリプトを呼び出すことができます。 この機能は、使用可能なすべてのブラウザーで機能します。 ただし、この変数は、プロパティがに設定されたHTMLフォームをユーザーがレンダリングする場合にの `Output Type` み使用できま `Form Body`す。 が有効な場合は機能しま `Output Type` せん `Full HTML`。 この機能を設定する手順については、管理ヘルプの「フォームの設定」を参照してください。

フォームを送信する前に呼び出されるコールバック関数を定義する必要があります。この関数の名前はで `_user_onsubmit`す。 関数が例外をスローしないと見なされます。例外の場合は無視されます。 JavaScript関数は、htmlのheadセクションに配置することをお勧めします。ただし、を含むスクリプトタグの末尾より前の任意の場所で宣言できま `xfasubset.js`す。

formserverがコンボボックスを含むXDPをレンダリングする場合、コンボボックスの作成に加えて、2つの非表示テキストフィールドも作成されます。 これらのテキストフィールドには、ドロップダウンリストのデータが格納されます（一方にはオプションの表示名が格納され、もう一方にはオプションの値が格納されます）。 したがって、ユーザーがフォームを送信するたびに、ドロップダウンリストのデータ全体が送信されます。 毎回それほど多くのデータを送信したくない場合は、それを無効にするカスタムスクリプトを作成できます。 例：ドロップダウンリストの名前は、サ `drpOrderedByStateProv` ブフォームヘッダーの下に含まれます。 HTML入力要素の名前は、次のようになります `header[0].drpOrderedByStateProv[0]`。 ドロップダウンのデータを保存して送信する非表示フィールドの名前は、次のような名前になります。 `header[0].drpOrderedByStateProv_DISPLAYITEMS_[0] header[0].drpOrderedByStateProv_VALUEITEMS_[0]`

データをポストしない場合は、次の方法でこれらの入力要素を無効にできます。 `var __CUSTOM_SCRIPTS_VERSION = 1; //enabling the feature function _user_onsubmit() { var elems = document.getElementsByName("header[0].drpOrderedByStateProv_DISPLAYITEMS_[0]"); elems[0].disabled = true; elems = document.getElementsByName("header[0].drpOrderedByStateProv_VALUEITEMS_[0]"); elems[0].disabled = true; }`

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

## XFAサブセット {#xfa-subsets}

HTMLとしてレンダリングするフォームデザインを作成する場合は、JavaScript言語のスクリプトのXFAサブセットに制限する必要があります。

クライアント上で実行するスクリプト、またはクライアントとサーバーの両方で実行するスクリプトは、XFAサブセット内に記述する必要があります。 サーバー上で実行するスクリプトは、完全なXFAスクリプティングモデルを使用でき、FormCalcも使用できます。 JavaScriptの使用に関する詳細は、「 [Forms Designer」を参照してください](https://www.adobe.com/go/learn_aemforms_designer_63)。

クライアント上でスクリプトを実行する場合、現在表示されているパネルのみがスクリプトを使用できます。例えば、パネルBが表示されている場合に、パネルAにあるフィールドに対してスクリプトを実行することはできません。 サーバー上でスクリプトを実行すると、すべてのパネルにアクセスできます。

また、クライアント上で実行するスクリプト内でスクリプティングオブジェクトモデル(SOM)式を使用する場合は、注意が必要です。 クライアント上で実行されるスクリプトでは、SOM式の簡単なサブセットのみがサポートされます。

## イベント時期 {#event-timing}

XFAサブセットは、HTMLサブセットにマッピングされるXFAイベントを定義します。イベント 計算と検証のタイミングに関する動作にわずかな違いがあります。イベント Webブラウザーでは、フィールドを終了すると、完全な計算イベントが実行されます。 計算イベントは、フィールド値を変更しても自動的には実行されません。 メソッドを呼び出すことで、強制的にイベントを計算することが `xfa.form.execCalculate` できます。

Webブラウザーでは、検証イベントはフィールドを終了するか、フォームを送信する場合にのみ実行されます。 この方法を使用して、validateイベントを強制的に実行で `xfa.form.execValidate` きます。

（Adobe ReaderやAcrobatとは対照的に）Webブラウザーに表示されるフォームは、必須フィールドのXFAのnullテスト（エラーまたは警告）に準拠しています。

* nullテストでエラーが発生し、値を指定せずにフィールドを終了すると、メッセージボックスが表示され、「OK」をクリックした後にフィールドの位置が変更されます。
* nullテストで警告が表示され、値を指定せずにフィールドを終了した場合は、「OK」または「キャンセル」をクリックするよう求められ、値を指定せずに続行するか、フィールドに戻って値を入力するかを選択できます。

nullテストについて詳しくは、「 [Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63)」を参照してください。

## フォームボタン {#form-buttons}

送信ボタンをクリックすると、フォームデータがFormsサービスに送信され、フォーム処理の終わりを表します。 この `preSubmit` イベントは、クライアントまたはサーバーで実行するように設定できます。 イベント `preSubmit` がクライアント上で実行するように設定されている場合、フォームの送信前に実行されます。 それ以外の場合は、 `preSubmit` イベントはフォームの送信中にサーバー上で実行されます。 このイベントについて詳しくは、「 `preSubmit`[Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63)」を参照してください。

ボタンにクライアントサイドのスクリプトが関連付けられていない場合、データはサーバーに送信され、計算がサーバー上で実行され、HTMLフォームが再生成されます。 ボタンにクライアントサイドのスクリプトが含まれる場合、データはサーバーに送信されず、クライアントサイドのスクリプトがWebブラウザーで実行されます。

## HTML 4.0 Webブラウザー {#html-4-0-web-browser}

HTML 4.0のみをサポートするWebブラウザーは、XFAサブセットのクライアント側スクリプティングモデルをサポートできません。 HTML 4.0とMSDHTML、またはCSS2HTMLの両方で動作するフォームデザインを作成する場合、クライアントで実行するようにマークされたスクリプトが実際にサーバー上で実行されます。 例えば、HTML 4.0 Webブラウザーに表示されているフォーム上のボタンをユーザーがクリックしたとします。 この場合、フォームデータはクライアントサイドのスクリプトが実行されるサーバーに送信されます。

フォームロジックは、HTML 4.0のサーバーで実行され、MSDHTMLまたはCSS2HTMLのクライアントで実行されるcalculateイベントーに配置することをお勧めします。

## プレゼンテーションの変更の管理 {#maintaining-presentation-changes}

HTMLページ（パネル）間を移動すると、データの状態のみが保持されます。 背景色や必須フィールドの設定などの設定は維持されません（初期設定と異なる場合）。 プレゼンテーションの状態を維持するには、フィールドのプレゼンテーションの状態を表すフィールド（通常は非表示）を作成する必要があります。 フィールドのイベントに、非表示のフィールド値に基づいてプレゼンテーションを変更するスクリプトを追加すると、HTMLページ（パネル）間を移動しながらプレゼンテーションの状態を保持できます。 `Calculate`

次のスクリプトでは、の値 `fillColor` に基づいてフィールドの内容を管理しま `hiddenField`す。 このスクリプトがフィールドのイベント内にあると `Calculate` します。

```as3
     If (hiddenField.rawValue == 1) 
         this.fillColor = "255,0,0" 
     else 
         this.fillColor = "0,255,0"
```

>[!NOTE]
テーブルのセル内にネストされている場合、スタティックオブジェクトはレンダリングされたHTMLフォームに表示されません。 例えば、テーブルセル内にネストされた円と長方形は、レンダリングHTMLフォーム内に表示されません。 ただし、テーブルの外側に配置した場合は、これらの同じスタティックオブジェクトが正しく表示されます。

## HTMLフォームへの電子署名 {#digitally-signing-html-forms}

電子署名フィールドを含むHTMLフォームを、次のHTML変換のいずれかとしてレンダリングする場合は、署名を行うことはできません。

* AHTML
* HTML4
* StaticHTML
* NoScriptXHTML

電子署名の詳細については、「ドキュメントの電子署名と [認証ドキュメント」を参照してください](/help/forms/developing/digitally-signing-certifying-documents.md)

## アクセシビリティガイドライン準拠のXHTMLフォームのレンダリング {#rendering-an-accessibility-guidelines-compliant-xhtml-form}

アクセシビリティガイドラインに準拠した完全なHTMLフォームをレンダリングできます。 つまり、フォームは完全なHTMLタグ内でレンダリングされ、HTMLフォームはbodyタグ内（完全なHTMLページではない）でレンダリングされます。

## フォームデータの検証 {#validating-form-data}

フォームをHTMLフォームとしてレンダリングする場合は、フォームフィールドの検証ルールの使用を制限することをお勧めします。 一部の検証ルールは、HTMLフォームでサポートされていない場合があります。 例えば、HTMLフォームとしてレンダリングされるフォームデザイン内のフィールドにMM-DD-YYYYの検証パターンを適用した場合、日付が正しく入力されていても、正しく機能しません。 `Date/Time` ただし、この検証パターンは、PDFとしてレンダリングされるフォームに対して正しく機能します。

>[!NOTE]
For more information about the Forms service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## 手順の概要 {#summary-of-steps}

HTMLフォームをレンダリングするには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. フォームクライアントAPIオブジェクトを作成します。
1. HTML実行時オプションを設定します。
1. HTMLフォームのレンダリング
1. フォームデータストリームをクライアントのWebブラウザーに書き込みます。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、必ずプロキシファイルを含めてください。

**フォームクライアントAPIオブジェクトの作成**

プログラムによってデータをPDF formClient APIに読み込む前に、Form Data Integrationサービスクライアントを作成する必要があります。 サービスクライアントを作成する場合、サービスの呼び出しに必要な接続設定を定義します。

**HTML実行時オプションの設定**

HTMLフォームのレンダリング時に、HTML実行時オプションを設定します。 例えば、HTMLフォームにツールバーを追加して、クライアントコンピューター上の添付ファイルを選択したり、HTMLフォームと共にレンダリングされる添付ファイルを取得したりできます。 デフォルトでは、HTMLツールバーは無効です。 HTMLフォームにツールバーを追加するには、プログラムによって実行時のオプションを設定する必要があります。 デフォルトでは、HTMLツールバーは次のボタンで構成されます。

* `Home`:アプリケーションのWebルートへのリンクを提供します。
* `Upload`:現在のフォームに添付するファイルを選択するためのユーザーインターフェイスを提供します。
* `Download`:添付ファイルを表示するユーザインターフェイスを提供します。

HTMLツールバーがHTMLフォームに表示される場合、ユーザーはフォームデータと共に送信するファイルを最大10個まで選択できます。 ファイルが送信されると、Formsサービスはファイルを取得できます。

フォームをHTMLとしてレンダリングする場合は、user-agentの値を指定できます。 user-agent値は、ブラウザーとシステムの情報を提供します。 これはオプションの値で、空の文字列値を渡すことができます。 Java APIを使用したHTMLフォームのレンダリングのクイック開始では、ユーザーエージェントの値を取得し、それを使用してフォームをHTMLとしてレンダリングする方法を示します。

フォームデータの投稿先となるHTTP URLは、Forms Service Client APIを使用してターゲットURLを設定することで指定するか、XDPフォームデザインに含まれる「送信」ボタンで指定することができます。 ターゲットURLがフォームデザインで指定されている場合は、Forms Service Client APIを使用して値を設定しないでください。

>[!NOTE]
ツールバーを使用したHTMLフォームのレンダリングはオプションです。

>[!NOTE]
AHTMLフォームをレンダリングする場合は、ツールバーをフォームに追加しないことをお勧めします。

**HTMLフォームのレンダリング**

HTMLフォームをレンダリングするには、Designerで作成し、XDPファイルとして保存するフォームデザインを指定する必要があります。 また、HTML変換タイプを選択する必要があります。 例えば、Internet Explorer 5.0以降用の動的HTMLをレンダリングするHTML変換タイプを指定できます。

HTMLフォームのレンダリングには、他のフォームタイプをレンダリングするために必要なURI値などの値も必要です。

**フォームデータストリームをクライアントWebブラウザーに書き込む**

Formsサービスは、HTMLフォームをレンダリングする際に、クライアントのWebブラウザーに書き込む必要のあるフォームデータストリームを返します。 クライアントWebブラウザーに書き込むと、HTMLフォームがユーザーに表示されます。

**関連トピック**

[Java APIを使用してフォームをHTMLとしてレンダリングする](#render-a-form-as-html-using-the-java-api)

[WebサービスAPIを使用してフォームをHTMLとしてレンダリングする](#render-a-form-as-html-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[FormsサービスAPIのクイック開始](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[インタラクティブPDFフォームのレンダリング](/help/forms/developing/rendering-interactive-pdf-forms.md)

[カスタムツールバーを使用したHTMLフォームのレンダリング](/help/forms/developing/rendering-html-forms-custom-toolbars.md)

[フォームをレンダリングするWeb アプリケーションの作成](/help/forms/developing/creating-web-applications-renders-forms.md)

## Java APIを使用してフォームをHTMLとしてレンダリングする {#render-a-form-as-html-using-the-java-api}

Forms API(Java)を使用してHTMLフォームをレンダリングします。

1. プロジェクトファイルを含める

   Javaプロジェクトのクラスパスに、adobe-forms-client.jarなどのクライアントJARファイルを含めます。

1. フォームクライアントAPIオブジェクトの作成

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * Create an `FormsServiceClient` object by using its constructor and passing the `ServiceClientFactory` object.

1. HTML実行時オプションの設定

   * Create an `HTMLRenderSpec` object by using its constructor.
   * ツールバーを使用してHTMLフォームをレンダリングするには、オ `HTMLRenderSpec` ブジェクトのメソッ `setHTMLToolbar` ドを呼び出し、列挙値を渡 `HTMLToolbar` します。 例えば、垂直方向のHTMLツールバーを表示するには、を渡しま `HTMLToolbar.Vertical`す。
   * HTMLフォームのロケール値を設定するには、オブジェクトのメ `HTMLRenderSpec` ソッドを呼び出 `setLocale` し、ロケール値を指定する文字列値を渡します。 （これはオプションの設定です）。
   * 完全なHTMLタグ内でHTMLフォームをレンダリングするには、オブジェクトの `HTMLRenderSpec` メソッドを呼び出 `setOutputType` し、渡してくださ `OutputType.FullHTMLTags`い。 （これはオプションの設定です）。
   >[!NOTE]
   このオプションを選択し、AEM FormsをホストするJ2EEアプリケーションサーバー以外のサーバーを参照している場合、フォームはHTMLで正常にレンダリングされません( `StandAlone` 値は、オブジェクトのメソッドに渡される `true` オブジェクトを使用して指定 `ApplicationWebRoot``ApplicationWebRoot``URLSpec``FormsServiceClient``(Deprecated) renderHTMLForm` されます)。 *がAEM Formsをホストする別のサーバーの場合、管理コンソールのWebルートURIの値をフォームのWebアプリケーションのURI値として設定する必要があります。 `ApplicationWebRoot`これは、管理コンソールにログインし、サービス/Formsをクリックし、WebルートURIをhttps://server-name:port/FormServerに設定することで実行できます。 次に、設定を保存します。*

1. HTMLフォームのレンダリング

   オブジェクト `FormsServiceClient` のメソッドを `(Deprecated) renderHTMLForm` 呼び出し、次の値を渡します。

   * ファイル名の拡張子を含む、フォームデザイン名を指定するstring値。 Formsアプリケーションの一部であるフォームデザインを参照する場合、などの完全なパスを必ず指定してくださ `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`い。
   * HTMLの `TransformTo` 環境設定の種類を指定する列挙値です。 例えば、Internet Explorer 5.0以降用の動的HTMLと互換性のあるHTMLフォームをレンダリングするには、を指定しま `TransformTo.MSDHTML`す。
   * フォーム `com.adobe.idp.Document` とマージするデータを含むオブジェクトです。 データを結合しない場合は、空のオブジェクトを渡し `com.adobe.idp.Document` ます。
   * HTML実行 `HTMLRenderSpec` 時オプションを格納するオブジェクトです。
   * ヘッダー値を指定す `HTTP_USER_AGENT` るstring値。例えば、 `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`.
   * HTMLフォ `URLSpec` ームのレンダリングに必要なURI値を格納するオブジェクト。
   * 添付ファ `java.util.HashMap` イルを格納するオブジェクト。 これはオプションのパラメーターで、フォームにフ `null` ァイルを添付しないかどうかを指定できます。
   このメソ `(Deprecated) renderHTMLForm` ッドは、クラ `FormsResult` イアントのWebブラウザーに書き込み可能なフォームデータストリームを含むオブジェクトを返します。

1. フォームデータストリームをクライアントWebブラウザーに書き込む

   * オブジェクトの `com.adobe.idp.Document` メソッドを呼び出して、オ `FormsResult` ブジェクトを作成 `getOutputContent` します。
   * メソッドを呼び出して、オブジェ `com.adobe.idp.Document` クトのコンテンツタイプを取 `getContentType` 得します。
   * メソッドを呼 `javax.servlet.http.HttpServletResponse` び出し、オブジェクトのコンテ `setContentType` ンツタイプを渡して、オブジェクトのコンテンツタイプを設定 `com.adobe.idp.Document` します。
   * オブジェクトの `javax.servlet.ServletOutputStream` メソッドを呼び出して、フォームデータストリームをクライアントのWebブラウザーに書き込むために使用す `javax.servlet.http.HttpServletResponse` るオブジェクトを作成 `getOutputStream` します。
   * オブジェクトの `java.io.InputStream` メソッドを呼び出して、オ `com.adobe.idp.Document` ブジェクトを作成 `getInputStream` します。
   * バイト配列を作成し、オブジェクトのメソッドを呼び出し、バイト配列を引 `InputStream` 数として渡すこ `read` とで、フォームデータストリームを設定します。
   * オブジェクト `javax.servlet.ServletOutputStream` のメソッドを呼 `write` び出して、フォームデータストリームをクライアントWebブラウザーに送信します。 バイト配列をメソッドに渡し `write` ます。

**関連トピック**

[HTMLとしてのフォームのレンダリング](#rendering-forms-as-html)

[クイック開始（SOAPモード）:Java APIを使用したHTMLフォームのレンダリング](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-an-html-form-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## WebサービスAPIを使用してフォームをHTMLとしてレンダリングする {#render-a-form-as-html-using-the-web-service-api}

Forms API（Webサービス）を使用してHTMLフォームをレンダリングします。

1. プロジェクトファイルを含める

   * FormsサービスのWSDLを使用するJavaプロキシクラスを作成します。
   * クラスパスにJavaプロキシクラスを含めます。

1. フォームクライアントAPIオブジェクトの作成

   オブジェクトを `FormsService` 作成し、認証値を設定します。

1. HTML実行時オプションの設定

   * Create an `HTMLRenderSpec` object by using its constructor.
   * ツールバーを使用してHTMLフォームをレンダリングするには、オ `HTMLRenderSpec` ブジェクトのメソッ `setHTMLToolbar` ドを呼び出し、列挙値を渡 `HTMLToolbar` します。 例えば、垂直方向のHTMLツールバーを表示するには、を渡しま `HTMLToolbar.Vertical`す。
   * HTMLフォームのロケール値を設定するには、オブジェクトのメ `HTMLRenderSpec` ソッドを呼び出 `setLocale` し、ロケール値を指定する文字列値を渡します。 For more information, see [AEM Forms API Reference](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).
   * 完全なHTMLタグ内でHTMLフォームをレンダリングするには、オブジェクトの `HTMLRenderSpec` メソッドを呼び出 `setOutputType` し、渡してくださ `OutputType.FullHTMLTags`い。
   >[!NOTE]
   このオプションを選択し、AEM FormsをホストするJ2EEアプリケーションサーバー以外のサーバーを参照している場合、フォームはHTMLで正常にレンダリングされません( `StandAlone` 値は、オブジェクトのメソッドに渡される `true` オブジェクトを使用して指定 `ApplicationWebRoot``ApplicationWebRoot``URLSpec``FormsServiceClient``(Deprecated) renderHTMLForm` されます)。 *がAEM Formsをホストする別のサーバーの場合、管理コンソールのWebルートURIの値をフォームのWebアプリケーションのURI値として設定する必要があります。 `ApplicationWebRoot`これは、管理コンソールにログインし、サービス/Formsをクリックし、WebルートURIをhttps://server-name:port/FormServerに設定することで実行できます。 次に、設定を保存します。*

1. HTMLフォームのレンダリング

   オブジェクト `FormsService` のメソッドを `(Deprecated) renderHTMLForm` 呼び出し、次の値を渡します。

   * ファイル名の拡張子を含む、フォームデザイン名を指定するstring値。 Formsアプリケーションの一部であるフォームデザインを参照する場合、などの完全なパスを必ず指定してくださ `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`い。
   * HTMLの `TransformTo` 環境設定の種類を指定する列挙値です。 例えば、Internet Explorer 5.0以降用の動的HTMLと互換性のあるHTMLフォームをレンダリングするには、を指定しま `TransformTo.MSDHTML`す。
   * フォーム `BLOB` とマージするデータを含むオブジェクトです。 データを結合しない場合は、を渡します `null`。 (編集可能な [レイアウトでのフォームの自動埋め込みを参照](/help/forms/developing/prepopulating-forms-flowable-layouts.md#prepopulating-forms-with-flowable-layouts))。
   * HTML実行 `HTMLRenderSpec` 時オプションを格納するオブジェクトです。
   * ヘッダー値を指定す `HTTP_USER_AGENT` るstring値。例えば、 `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`. この値を設定しない場合は、空の文字列を渡すことができます。
   * HTMLフォ `URLSpec` ームのレンダリングに必要なURI値を格納するオブジェクト。 (URI値の指 [定を参照](/help/forms/developing/rendering-interactive-pdf-forms.md))。
   * 添付ファ `java.util.HashMap` イルを格納するオブジェクト。 これはオプションのパラメーターで、フォームにフ `null` ァイルを添付しないかどうかを指定できます。 (フォーム [へのファイルの添付を参照](/help/forms/developing/rendering-interactive-pdf-forms.md))。
   * メソッドに `com.adobe.idp.services.holders.BLOBHolder` よって入力される空のオブジェクトです。 このパラメーター値は、レンダリングされたフォームを保存します。
   * メソッドに `com.adobe.idp.services.holders.BLOBHolder` よって入力される空のオブジェクトです。 このパラメーターは、出力XMLデータを格納します。
   * メソッドに `javax.xml.rpc.holders.LongHolder` よって入力される空のオブジェクトです。 この引数は、フォームのページ数を格納します。
   * メソッドに `javax.xml.rpc.holders.StringHolder` よって入力される空のオブジェクトです。 この引数はロケールの値を格納します。
   * メソッドに `javax.xml.rpc.holders.StringHolder` よって入力される空のオブジェクトです。 この引数には、使用されるHTMLレンダリング値が格納されます。
   * この操作の `com.adobe.idp.services.holders.FormsResultHolder` 結果を含む空のオブジェクトです。
   メソッド `(Deprecated) renderHTMLForm` は、最後の引 `com.adobe.idp.services.holders.FormsResultHolder` 数として渡されたオブジェクトに、クライアントWebブラウザーに書き込む必要のあるフォームデータストリームを設定します。

1. フォームデータストリームをクライアントWebブラウザーに書き込む

   * オブジェクト `FormResult` のデータメンバーの値を取得して、オ `com.adobe.idp.services.holders.FormsResultHolder` ブジェクトを `value` 作成します。
   * オブジェクトの `BLOB` メソッドを呼び出して、フォームデータを含む `FormsResult` オブジェクトを作成 `getOutputContent` します。
   * メソッドを呼び出して、オブジェ `BLOB` クトのコンテンツタイプを取 `getContentType` 得します。
   * メソッドを呼 `javax.servlet.http.HttpServletResponse` び出し、オブジェクトのコンテ `setContentType` ンツタイプを渡して、オブジェクトのコンテンツタイプを設定 `BLOB` します。
   * オブジェクトの `javax.servlet.ServletOutputStream` メソッドを呼び出して、フォームデータストリームをクライアントのWebブラウザーに書き込むために使用す `javax.servlet.http.HttpServletResponse` るオブジェクトを作成 `getOutputStream` します。
   * バイト配列を作成し、オブジェクトのメソッドを呼び出 `BLOB` して値を設定 `getBinaryData` します。 このタスクは、オブジェクトの内容をバ `FormsResult` イト配列に割り当てます。
   * オブジェクト `javax.servlet.http.HttpServletResponse` のメソッドを呼 `write` び出して、フォームデータストリームをクライアントWebブラウザーに送信します。 バイト配列をメソッドに渡し `write` ます。

**関連トピック**

[HTMLとしてのフォームのレンダリング](#rendering-forms-as-html)

[Base64エンコーディングを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

