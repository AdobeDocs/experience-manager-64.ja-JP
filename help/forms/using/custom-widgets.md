---
title: HTML5 フォームのカスタム外観の作成
seo-title: Create custom appearances in HTML5 forms
description: カスタムウィジェットを Mobile Formsにプラグインできます。 既存の jQuery ウィジェットを拡張したり、独自のカスタムウィジェットを開発したりできます。
seo-description: You can plug in custom widgets to a Mobile Forms. You can extend existing jQuery Widgets or develop your own custom widgets.
uuid: afb16f42-e404-478b-82dd-4b5b59c4f184
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: hTML5_forms
discoiquuid: 5d860f05-3257-4cf7-93dd-77d226d59b39
feature: Mobile Forms
exl-id: e9e53b6d-6403-4d37-bac1-efaff0317f34
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '676'
ht-degree: 43%

---

# HTML5 フォームのカスタム外観の作成 {#create-custom-appearances-in-html-forms}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

カスタムウィジェットを Mobile Formsにプラグインできます。 既存の jQuery ウィジェットを拡張したり、外観フレームワークを使用して独自のカスタムウィジェットを開発したりできます。 XFA エンジンは様々なウィジェットを使用します。詳しくは、[アダプティブフォームおよび HTML5 フォームの外観フレームワーク](/help/forms/using/introduction-widgets.md)を参照してください。

![デフォルトおよびカスタムウェジェットの例](assets/custom-widgets.jpg)
**図：** *デフォルトとカスタムウィジェットの例*

## カスタムウィジェットとHTML5 フォームの統合 {#integrating-custom-widgets-with-html-forms}

### プロファイルの作成  {#create-a-profile-nbsp}

プロファイルを作成するか、既存のプロファイルを選択してカスタムウィジェットを追加することができます。 プロファイルの作成について詳しくは、 [カスタムプロファイルの作成](/help/forms/using/custom-profile.md).

### ウィジェットの作成 {#create-a-widget}

HTML5 Forms には、新しいウィジェットを作成するために拡張可能なウィジェットフレームワークの実装が提供されています。実装は jQuery ウィジェットです。 *abstractWidget* 新しいウィジェットを書くために拡張できます。 新しいウィジェットは、以下に示す関数を拡張または上書きすることによってのみ、機能させることができます。

<table> 
 <tbody> 
  <tr> 
   <td>関数/クラス</td> 
   <td>説明</td> 
  </tr> 
  <tr> 
   <td>render</td> 
   <td>レンダリング関数は、ウィジェットのデフォルトのHTML要素の jQuery オブジェクトを返します。 デフォルトのHTML要素は、フォーカス可能なタイプである必要があります。 例： &lt;a&gt;, &lt;input&gt;、および &lt;li&gt;. 返された要素は、 $userControl として使用されます。 $userControl は上記の制約を指定し、次に AbstractWidget クラスの関数が期待通りに機能します。そうでない場合、一部の一般的な API（フォーカス、クリック）は変更を必要とします。 </td> 
  </tr> 
  <tr> 
   <td>getEventMap</td> 
   <td>HTML イベントを XFA イベントに変換するマップを返します。<br /> {<br /> blur: XFA_EXIT_EVENT,<br /> }<br /> この例は、blur が HTML イベントであり、XFA_EXIT_EVENT が対応する XFA イベントであることを示しています。 </td> 
  </tr> 
  <tr> 
   <td>getOptionsMap</td> 
   <td>オプションの変更時に実行するアクションの詳細を示すマップを返します。 キーはウィジェットに提供されるオプションです。値はそのオプションの変更が検出されたときに毎回呼び出される関数です。ウィジェットは、すべての一般的なオプション（value と displayValue を除く）のハンドラーを提供します</td> 
  </tr> 
  <tr> 
   <td>getCommitValue</td> 
   <td>ウィジェットフレームワークは、ウィジェットの値が XFAModel に保存されるたびに（例えば、textField の exit イベント時に）関数を読み込みます。 実装は、ウィジェットに保存された値を返す必要があります。ハンドラーには、オプションの新しい値が与えられます。</td> 
  </tr> 
  <tr> 
   <td>showValue</td> 
   <td>デフォルトでは、XFA では enter イベント時に、フィールドの rawValue が表示されます。 この関数は、rawValue をユーザーに表示するために呼び出されます。 </td> 
  </tr> 
  <tr> 
   <td>showDisplayValue</td> 
   <td>デフォルトでは、XFA の exit イベントでは、フィールドの formattedValue が表示されます。 この関数は、formattedValue をユーザーに表示するために呼び出されます。 </td> 
  </tr> 
 </tbody> 
</table>

独自のウィジェットを作成するには、上記で作成されたプロファイルに、上書きされた関数と新しく追加された関数を含む JavaScript ファイルの参照を含めます。例えば、*sliderNumericFieldWidget* は数値フィールドのためのウィジェットです。ヘッダーセクションのプロファイルでウィジェットを使用するには、次の行を含めます。

```
window.formBridge.registerConfig("widgetConfig" , widgetConfigObject);
```

### カスタムウィジェットを XFA スクリプティングエンジンに登録  {#register-custom-widget-with-xfa-scripting-engine-nbsp}

カスタムウィジェットのコードが準備されたら、[Form Bridge](/help/forms/using/form-bridge-apis.md) の `registerConfig` API を使用して、スクリプトエンジンにウィジェットを登録します。widgetConfigObject を入力として受け取ります。

```
window.formBridge.registerConfig("widgetConfig",
        {
        ".<field-identifier>":"<name-of-the-widget>"
        }
    );
```

#### widgetConfigObject {#widgetconfigobject}

ウィジェットの設定は JSON オブジェクト（キーと値のペアのコレクション）として提供されます。キーはフィールドを識別し、値はこれらのフィールドで使用するウィジェットを表します。 設定例を次に示します。

```
*{*

*“identifier1” : “customwidgetname”,  
“identifier2” : “customwidgetname2”,  
..  
}*
```

ここで「identifier」は、特定のフィールド、特定のタイプの一連のフィールド、またはすべてのフィールドを現す jQuery CSS セレクターです。以下には、さまざまなケースでの識別子の値が記載されています。

| 識別子のタイプ | 識別子 | 説明 |
|---|---|---|
| fieldname という名前の特定のフィールド | 識別子：&quot;div.fieldname&quot; | 「fieldname」という名前のフィールドはすべて、ウィジェットを使用してレンダリングされます。 |
| 「type」タイプのすべてのフィールド（ここで type は NumericField、DateField などです。）： | 識別子：&quot;div.type&quot; | Timefield と DateTimeField の場合、これらのフィールドはまだサポートされていないため、タイプは textfield です。 |
| すべてのフィールド | 識別子：「div.field」 |  |
