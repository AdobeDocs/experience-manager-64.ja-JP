---
title: HTML5 フォームの Form Bridge API
seo-title: Form Bridge APIs for HTML5 forms
description: 外部アプリケーションは FormBridge API を使用して XFA Mobile Form に接続します。API は親ウィンドウで FormBridgeInitialized イベントを送出します。
seo-description: External applications use the FormBridge API to connect to the XFA Mobile Form. The API dispatches a FormBridgeInitialized event on the parent window.
uuid: 0db22649-522b-4857-9ffd-826c52381d15
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: developer-reference
discoiquuid: c05c9911-7c49-4342-89de-61b8b9953c83
exl-id: ad669f3b-2bda-4c41-8032-cf25a192ce12
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '939'
ht-degree: 40%

---

# HTML5 フォームの Form Bridge API {#form-bridge-apis-for-html-forms}

Form Bridge API を使用して、XFA ベースのHTML5 フォームとアプリケーションの間の通信チャネルを開くことができます。 Form Bridge API は **接続** 接続を作成する API。

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

スクリプティングライブラリのバージョン番号を返す

* **入力**：なし
* **出力**:スクリプトライブラリのバージョン番号
* **エラー**：なし

**isConnected()** フォームの状態が初期化されたかどうかを確認します

* **入力**：なし
* **出力**: **True** （XFA フォーム状態が初期化されている場合）

* **エラー**：なし

**connect(handler, context)** FormBridge に接続し、接続が確立され、フォーム状態が初期化された後に関数を実行します

* **必要情報**:

   * **handler**：Form Bridge が接続された後に実行する関数
   * **context**:*handler *関数のコンテキスト (this) が設定されるオブジェクト。

* **出力**：なし
* **エラー**：なし

**getDataXML(options)** 現在のフォームデータを XML 形式で返します

* **必要情報:**

   * **options：**&#x200B;次のプロパティが含まれている JavaScript オブジェクト。

      * **error**：エラーハンドラー関数
      * **success**：サクセスハンドラー関数。 この関数には *data* プロパティに XML が含まれているオブジェクトが渡されます。
      * **context**：*success*&#x200B;関数のコンテキスト（this）の設定対象オブジェクト
      * **validationChecker**:サーバーから受信した検証エラーを確認するためにを呼び出す関数。 検証関数にはエラー文字列の配列が渡されます。
      * **formState**:データ XML を返す必要がある XFA フォームの JSON 状態。 指定されていない場合、現在のレンダリングされているフォームの XML のデータ。

* **出力：**&#x200B;なし
* **エラー**：なし

**registerConfig(configName, config)** ユーザー/ポータル固有の設定を FormBridge に登録します。 これらの設定はデフォルト設定をオーバーライドします。サポートされている設定は config セクションで指定されています。

* **必要情報:**

   * **configName:** 上書きする設定の名前

      * **widgetConfig:** ユーザーがフォーム内のデフォルトのウィジェットをカスタムウィジェットで上書きすることを許可します。 設定は次のようにオーバーライドされます。

         formBridge.registerConfig(&quot;widgetConfig&quot;:{/&amp;ast;configuration&amp;ast;/})

      * **pagingConfig:** 最初のページのみをレンダリングするというデフォルトの動作をユーザーが上書きできるようにします。 設定は次のようにオーバーライドされます。

         window.formBridge.registerConfig(&quot;pagingConfig&quot;:{pagingDisabled: &lt;true | false>, shrinkPageDisabled: &lt;true | false> }).

      * **LoggingConfig:** ユーザーがログのレベルを上書きしたり、カテゴリのログを無効にしたり、ログコンソールを表示するかサーバーに送信するかを指定したりできます。 設定は次のようにオーバーライドできます。

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

      * **SubmitServiceProxyConfig:** ユーザーが送信を登録し、プロキシサービスをロガーすることを許可します。

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

**hideFields(fieldArray)** fieldArray で SOM 式が提供されているフィールドを非表示にします。 指定フィールドの presence プロパティを invisible に設定します

* **必要情報:**

   * **fieldArray:** 非表示にするフィールドの SOM 式の配列

* **出力：**&#x200B;なし
* **エラー**：なし

**showFields(fieldArray)** fieldArray で SOM 式が提供されるフィールドを表示します。 提供されたフィールドの presence プロパティを visible に設定します

* **必要情報:**

   * **fieldArray:** 表示するフィールドの SOM 式の配列

* **出力：**&#x200B;なし
* **エラー**：なし

**hideSubmitButtons()** フォーム内のすべての送信ボタンを非表示にします

* **入力**：なし
* **出力**：なし
* **エラー**：フォーム状態が初期化されていない場合、例外をスローする

**getFormState()** フォームの状態を表す JSON を返します

* **入力：**&#x200B;なし
* **出力：** 現在のフォーム状態を表す JSON を含むオブジェクト ( *データ* プロパティ。

* **エラー**：なし

**restoreFormState(options)** options オブジェクトで指定された JSON 状態からフォーム状態を復元します。 状態が適用され、操作の完了後にサクセスまたはエラーハンドラーが呼び出されます。

* **必要情報:**

   * **オプション：** 次のプロパティを含む JavaScript オブジェクト。

      * **error**：エラーハンドラー関数
      * **success**：サクセスハンドラー関数
      * **context**:のコンテキスト (this) の対象となるオブジェクト *成功* 関数が設定されている
      * **formState**: フォームの JSON ステート。フォームが JSON 状態に復元されます。

* **出力：**&#x200B;なし
* **エラー**：なし

**setFocus (som)** SOM 式で指定されたフィールドにフォーカスを設定

* **入力：** フォーカスを設定するフィールドの SOM 式
* **出力：**&#x200B;なし
* **エラー：** SOM 式が間違っている場合、例外をスローする

**setFieldValue (som, value)** 指定された SOM 式のフィールドの値を設定

* **必要情報:**

   * **som：**&#x200B;フィールドの SOM 式が含まれている配列。フィールドの値を設定する SOM 式。
   * **値：** で提供された SOM 式に対応する値を含む配列 **som** 配列。 値のデータ型が fieldType と異なる場合、値は変更されません。

* **出力：**&#x200B;なし
* **エラー：** SOM 式が正しくない場合に例外をスロー

**getFieldValue (som)** 指定された SOM 式のフィールドの値を返します

* **入力：** 値を取得する必要があるフィールドの SOM 式を含む配列
* **出力：** 結果を配列として含むオブジェクト ( **データ** プロパティ。

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

**getFieldProperties(som, property)** SOM 式で指定されたフィールドの指定されたプロパティの値のリストを取得

* **必要情報:**

   * **som：**&#x200B;フィールドの SOM 式が含まれている配列
   * **property：**&#x200B;値が要求されるプロパティの名前

* **出力：** 結果が配列として*data *property に含まれるオブジェクト

* **エラー**：なし

**setFieldProperties(som, property, values)** SOM 式で指定されたすべてのフィールドの指定されたプロパティの値を設定します

* **必要情報:**

   * **som:** 値を設定する必要があるフィールドの SOM 式を含む配列
   * **property：**&#x200B;値の設定が要求されるプロパティ
   * **値：** SOM 式で指定されたフィールドの指定されたプロパティの値を含む配列

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
