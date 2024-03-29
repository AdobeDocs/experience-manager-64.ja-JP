---
title: HTML5 フォームの Form Bridge API
seo-title: Form Bridge APIs for HTML5 forms
description: 外部アプリケーションは、FormBridge API を使用して XFA Mobile Form に接続します。 API は親ウィンドウで FormBridgeInitialized イベントを発行します。
seo-description: External applications use the FormBridge API to connect to the XFA Mobile Form. The API dispatches a FormBridgeInitialized event on the parent window.
uuid: 0db22649-522b-4857-9ffd-826c52381d15
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: developer-reference
discoiquuid: c05c9911-7c49-4342-89de-61b8b9953c83
exl-id: ad669f3b-2bda-4c41-8032-cf25a192ce12
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '975'
ht-degree: 82%

---

# HTML5 フォームの Form Bridge API {#form-bridge-apis-for-html-forms}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

各種 Form Bridge API を使用すると、XFA ベースの HTML5 フォームとお使いのアプリケーション間の通信チャネルを開くことができます。これらの Form Bridge API では接続作成用の&#x200B;**接続** API を使用できます。

**接続** API はハンドラーを引数として受け入れます。XFA ベースの接続 5 フォームと Form Bridge 間の接続が正常にHTMLされると、ハンドルが呼び出されます。

次のサンプルコードを使用して接続を作成できます。

```
// Example showing how to connect to FormBridge
window.addEventListener("FormBridgeInitialized",
                                function(event) {
                                    var fb = event.detail.formBridge;
                                    fb.connect(function() {
                                           //use form bridge functions 
                         })
                            })
```

>[!NOTE]
>
>必ず接続を作成してから formRuntime.jsp ファイルを追加してください。

## 利用可能な Form Bridge API  {#available-form-bridge-api-nbsp}

**getBridgeVersion()**

スクリプトライブラリのバージョン番号を返します

* **入力**：なし
* **出力**：スクリプティングライブラリのバージョン番号
* **エラー**：なし

**isConnected()** フォーム状態が初期化されたかを確認

* **入力**：なし
* **出力**：XFA フォーム状態が初期化された場合 **true**

* **エラー**：なし

**connect(handler, context)**： FormBridge への接続を確立し、接続を確立してフォーム状態が初期化された後に関数を実行

* **必要情報**:

   * **handler**：Form Bridge が接続された後に実行する関数
   * **context**:*handler *関数のコンテキスト (this) が設定されるオブジェクト。

* **出力**:なし
* **エラー**:なし

**getDataXML(options)**： 現在のフォームデータを XML 形式で返す

* **必要情報:**

   * **options：**&#x200B;次のプロパティが含まれている JavaScript オブジェクト。

      * **error**：エラーハンドラー関数
      * **success**：サクセスハンドラー関数。この関数には、 *データ* プロパティ。
      * **context**:のコンテキスト (this) の対象となるオブジェクト *成功* 関数が設定されている
      * **validationChecker**：サーバーから受信した検証エラーを確認するために呼び出す関数検証関数にはエラー文字列の配列が渡されます。
      * **formState**：XML のデータを返す必要がある XFA フォームの JSON 状態指定されていない場合、現在のレンダリングされているフォームの XML のデータ。

* **出力：**&#x200B;なし
* **エラー**：なし

**registerConfig(configName, config)**： ユーザー / ポータル固有の設定を FormBridge に登録します。 これらの設定は、デフォルトの設定よりも優先されます。 サポートされる設定は、config セクションで指定します。

* **必要情報:**

   * **configName：**&#x200B;オーバーライドする設定の名前

      * **widgetConfig：**&#x200B;フォーム内のデフォルトウィジェットをカスタムウィジェットでオーバーライドするのをユーザーに許可します。設定は次のようにオーバーライドされます。

         formBridge.registerConfig(&quot;widgetConfig&quot;:{/&amp;ast;configuration&amp;ast;/})

      * **pagingConfig：**&#x200B;最初のページのみがレンダリングされるデフォルト動作をオーバーライドするのをユーザーに許可します。設定は次のようにオーバーライドされます。

         window.formBridge.registerConfig(&quot;pagingConfig&quot;:{pagingDisabled: &lt;true | false>, shrinkPageDisabled: &lt;true | false> }).

      * **LoggingConfig：**&#x200B;ユーザーがログのレベル、あるカテゴリのログの無効化、またはログコンソールを表示するかサーバーに送信するかをオーバーライドすることを可能にします。設定は次のようにオーバーライドできます。

      ```css
      formBridge.registerConfig{  
        "LoggerConfig" : {  
      {  
      "on":`<true *| *false>`,  
      "category":`<array of categories>`,  
      "level":`<level of categories>`, "  
      type":`<"console"/"server"/"both">`  
          }  
        }
      ```

      * **SubmitServiceProxyConfig：**&#x200B;ユーザーが送信を登録し、プロキシサービスをロギングできるようにします。

         ```css
         window.formBridge.registerConfig("submitServiceProxyConfig",  
         {  
         "submitServiceProxy" : "`<submitServiceProxy>`",  
         "logServiceProxy": "`<logServiceProxy>`",  
         "submitUrl" : "`<submitUrl>`"  
         });
         ```
   * **config：**&#x200B;設定の値



* **出力：***data* プロパティに設定の元の値が含まれているオブジェクト。

* **エラー**：なし

**hideFields(fieldArray)**：fieldArray で SOM 式が提供されるフィールドを非表示にします。指定フィールドの presence プロパティを invisible に設定します

* **必要情報:**

   * **fieldArray：**&#x200B;非表示にするフィールドの SOM 式の配列

* **出力：**&#x200B;なし
* **エラー**：なし

**showFields(fieldArray)**：fieldArray で SOM 式が提供されるフィールドを表示します。提供されたフィールドの presence プロパティを visible に設定します

* **必要情報:**

   * **fieldArray：**&#x200B;表示するフィールドの SOM 式の配列

* **出力：**&#x200B;なし
* **エラー**：なし

**hideSubmitButtons()**：フォーム内のすべての送信ボタンを非表示にします

* **入力**：なし
* **出力**:なし
* **エラー**:フォームの状態が初期化されていない場合に例外をスローする

**getFormState()**：フォームステートを表す JSON を返します

* **入力：**&#x200B;なし
* **出力：** *data* プロパティに現在のフォームデータを表す JSON が含まれているオブジェクト。

* **エラー**：なし

**restoreFormState(options)**：options オブジェクトに提供された JSON ステートからフォームステートを復元します。状態が適用され、操作の完了後に成功またはエラーハンドラーが呼び出されます

* **必要情報:**

   * **options：**&#x200B;次のプロパティが含まれている JavaScript オブジェクト。

      * **error**：エラーハンドラー関数
      * **success**：サクセスハンドラー関数
      * **context**：*success*&#x200B;関数のコンテキスト（this）の設定対象オブジェクト
      * **formState**: フォームの JSON ステート。フォームは JSON ステートに復元されます。

* **出力：**&#x200B;なし
* **エラー**：なし

**setFocus (som)**：SOM 式で指定されたフィールドにフォーカスを移します。

* **入力：**&#x200B;フォーカスを設定するフィールドの SOM 式
* **出力：**&#x200B;なし
* **エラー：** SOM 式が間違っている場合、例外をスローする

**setFieldValue (som, value)**：提供された SOM 式のフィールドの値を設定します

* **必要情報:**

   * **som：**&#x200B;フィールドの SOM 式が含まれている配列。フィールドの値を設定するための SOM 式。
   * **value：** **SOM** 配列で提供された SOM 式に対応する値が含まれている配列。値のデータタイプが fieldType と同じでない場合、値は変更されません。

* **出力：**&#x200B;なし
* **エラー：** SOM 式が間違っている場合、例外をスローします

**getFieldValue (som)**：提供された SOM 式のフィールドの値を返します

* **入力：**&#x200B;値を取得する必要のあるフィールドの SOM 式が含まれている配列
* **出力：**&#x200B;結果が配列として **data** プロパティに含まれているオブジェクト

* **エラー**：なし

### getFieldValue() API の例 {#example-of-nbsp-getfieldvalue-api}

```JavaScript
var a =  formBridge.getFieldValue(“xfa.form.form1.Subform1.TextField”);
if(a.errors) {
    var err;
     while((err = a.getNextMessage()) != null)
               alert(a.message)
} else {
   alert(a.data[0]) 
}
```

**getFieldProperties(som, property)** SOM 式で指定されたフィールドの提供されたプロパティの値リストを取得

* **必要情報:**

   * **som：**&#x200B;フィールドの SOM 式が含まれている配列
   * **property：**&#x200B;値が要求されるプロパティの名前

* **出力：** 結果が配列として*data *property に含まれるオブジェクト

* **エラー**：なし

**setFieldProperties(som, property, values)**： SOM 式で指定されたすべてのフィールドの提供されたプロパティの値を設定

* **必要情報:**

   * **som：**&#x200B;値の設定が要求されるフィールドの SOM 式が含まれている配列
   * **property：**&#x200B;値の設定が要求されるプロパティ
   * **value：** SOM 式で指定されたフィールドの提供されたプロパティの値が含まれている配列

* **出力：**&#x200B;なし
* **エラー**：なし

## Form Bridge API の使用例 {#sample-usage-of-form-bridge-api}

```JavaScript
// Example 1: FormBridge.restoreFormState
  function loadFormState() {
    var suc = function(obj) {
             //success
            }
    var err = function(obj) {
           while(var t = obj.getNextMessage()) {
         $("#errorDiv").append("<div>"+t.message+"</div>");
           }
           }
        var _formState = // load form state from storage
    formBridge.restoreFormState({success:suc,error:err,formState:_formState}); // not passing a context means that this will be formBridge itself. Validation errors will be checked.
  }

//--------------------------------------------------------------------------------------------------

//Example 2: FormBridge.submitForm
  function SubmitForm() {
    var suc = function(obj) {
             var data = obj.data;
         // submit the data to a url;
            }
    var err = function(obj) {
           while(var t = obj.getNextMessage()) {
         $("#errorDiv").append("<div>"+t.message+"</div>");
           }
           }
    formBridge.submitForm({success:suc,error:err}); // not passing a context means that this will be formBridge itself. Validation errors will be checked.
  }
```
