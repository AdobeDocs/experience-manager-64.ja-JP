---
title: アダプティブフォームの標準検証エラーメッセージ
seo-title: Standard validation error messages for adaptive forms
description: カスタムエラーハンドラーを使用して、アダプティブフォームの検証エラーメッセージを標準形式に変換する
seo-description: Transform the validation error messages for adaptive forms into standard format using custom error handlers
uuid: 0d1f9835-3e28-41d3-a3b1-e36d95384328
contentOwner: anujkapo
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_managing_domains
discoiquuid: ec062567-1c6b-497b-a1e7-1dbac2d60852
feature: Adaptive Forms
exl-id: 864e6b0d-178b-4b91-85d3-34b90e999ee3
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '1108'
ht-degree: 10%

---

# アダプティブフォームの標準検証エラーメッセージ {#standard-validation-error-messages}

アダプティブフォームは、事前設定された検証条件に基づいて、フィールドに入力した入力を検証します。 検証条件は、アダプティブフォーム内のフィールドに指定できる入力値を指します。 アダプティブフォームで使用するデータソースに基づいて、検証条件を設定できます。 例えば、RESTful Web サービスをデータソースとして使用する場合、Swagger 定義ファイルで検証条件を定義できます。

入力値が検証条件を満たす場合、値がデータソースに送信されます。 それ以外の場合は、アダプティブフォームにエラーメッセージが表示されます。

この方法と同様に、アダプティブフォームをカスタムサービスと統合して、データ検証を実行できるようになりました。 入力値が検証条件を満たさず、サーバーが返す検証エラーメッセージが標準メッセージ形式の場合、エラーメッセージはフォームのフィールドレベルに表示されます。

入力値が検証条件を満たさず、サーバーの検証エラーメッセージが標準メッセージ形式でない場合、アダプティブフォームは検証エラーメッセージを標準形式に変換し、フォームのフィールドレベルで表示するメカニズムを提供します。 次の 2 つの方法のいずれかを使用して、エラーメッセージを標準形式に変換できます。

* アダプティブフォーム送信時にカスタムエラーハンドラーを追加する
* ルールエディターを使用して「Invoke Service」アクションにカスタムハンドラーを追加する

この記事では、検証エラーメッセージの標準形式と、エラーメッセージをカスタム形式から標準形式に変換する手順について説明します。

## 標準検証エラーメッセージ形式 {#standard-validation-message-format}

サーバー検証エラーメッセージが次の標準形式の場合、アダプティブフォームはフィールドレベルでエラーを表示します。

```javascript
   {
    errorCausedBy : "SERVER_SIDE_VALIDATION/SERVICE_INVOCATION_FAILURE"
    errors : [
        {
             somExpression  : <somexpr>
             errorMessage / errorMessages : <validationMsg> / [<validationMsg>, <validationMsg>]

        }
    ]
    originCode : <target error Code>
    originMessage : <unstructured error message returned by service>
}
```

ここで、

* `errorCausedBy` 失敗の理由を説明します
* `errors` 検証エラーメッセージと共に、検証条件に失敗したフィールドの SOM 式に言及する
* `originCode` 外部サービスから返されたエラーコードが含まれます
* `originMessage` 外部サービスから返された生のエラーデータが含まれます

## カスタムハンドラーを追加するためのアダプティブフォームの送信設定 {#configure-adaptive-form-submission}

サーバーの検証エラーメッセージが標準形式で表示されない場合は、非同期送信を有効にし、アダプティブフォーム送信にカスタムエラーハンドラーを追加して、メッセージを標準形式に変換できます。

### 非同期アダプティブフォーム送信の設定 {#configure-asynchronous-adaptive-form-submission}

カスタムハンドラーを追加する前に、非同期送信用にアダプティブフォームを設定する必要があります。 以下の手順を実行します。

1. アダプティブフォームのオーサリングモードで、フォームコンテナオブジェクトを選択し、 ![アダプティブフォームのプロパティ](assets/configure_icon.png) をクリックしてプロパティを開きます。
1. 「**[!UICONTROL 送信]**」プロパティセクションで、「**[!UICONTROL 非同期送信を使用]**」を有効にします。
1. 選択 **[!UICONTROL サーバーで再検証]** ：送信前にサーバー上の入力フィールド値を検証します。
1. 送信アクションを選択します。

   * 選択 **[!UICONTROL フォームデータモデルを使用して送信]** RESTful Web サービスベースを使用している場合は、適切なデータモデルを選択します。 [フォームデータモデル](work-with-form-data-model.md) をデータソースとして使用する。
   * 選択 **[!UICONTROL REST エンドポイントに送信]** をクリックし、 **[!UICONTROL リダイレクト URL/パス]**&#x200B;データソースとして RESTful Web サービスを使用している場合は、を選択します。

   ![アダプティブフォーム送信プロパティ](assets/af_submission_properties.png)

1. 「![保存](assets/save_icon.png)」をタップして、プロパティを保存します。

### アダプティブフォーム送信時にカスタムエラーハンドラーを追加する {#add-custom-error-handler-af-submission}

AEM Forms には、フォーム送信が成功した場合と失敗した場合の処理を実行するハンドラーが用意されています。これらのハンドラーは、すぐに使用することができます。ハンドラーは、サーバー応答に基づいて実行されるクライアントサイド関数です。フォームが送信されると、データが検証のためにサーバーに転送され、送信の成功またはエラーイベントに関する情報と共に、応答がクライアントに返されます。この情報は、関連するハンドラーにパラメーターとして渡され、関数が実行されます。

アダプティブフォームの送信時にカスタムエラーハンドラーを追加するには、以下の手順を実行します。

1. アダプティブフォームをオーサリングモードで開き、任意のフォームオブジェクトを選択して、をタップします。 <!--![Rule Editor](assets/af_edit_rules.png)--> をクリックして、ルールエディターを開きます。
1. フォームオブジェクトツリーで「**[!UICONTROL フォーム]**」選択し、「**[!UICONTROL 作成]**」をタップします。
1. 選択 **[!UICONTROL 送信中にエラーが発生しました]** を選択します。
1. カスタムエラー構造を標準エラー構造に変換するルールを作成し、をタップします。 **[!UICONTROL 完了]** 」と入力してルールを保存します。

カスタムエラー構造を標準エラー構造に変換するサンプルコードを以下に示します。

```javascript
var data = $event.data;
var som_map = {
    "id": "guide[0].guide1[0].guideRootPanel[0].Pet[0].id_1[0]",
    "name": "guide[0].guide1[0].guideRootPanel[0].Pet[0].name_2[0]",
    "status": "guide[0].guide1[0].guideRootPanel[0].Pet[0].status[0]"
};

var errorJson = {};
errorJson.errors = [];

if (data) {
    if (data.originMessage) {
        var errorData;
        try {
            errorData = JSON.parse(data.originMessage);
        } catch (err) {
            // not in json format
        }

        if (errorData) {
            Object.keys(errorData).forEach(function(key) {
                var som_key = som_map[key];
                if (som_key) {
                    var error = {};
                    error.somExpression = som_key;
                    error.errorMessage = errorData[key];
                    errorJson.errors.push(error);
                }
            });
        }
        window.guideBridge.handleServerValidationError(errorJson);
    } else {
        window.guideBridge.handleServerValidationError(data);
    }
}
```

この `var som_map` 標準形式に変換するアダプティブフォームフィールドの SOM 式を一覧表示します。 アダプティブフォーム内の任意のフィールドの SOM 式を表示するには、フィールドをタップして、 **[!UICONTROL SOM 式を表示]**.

アダプティブフォームは、このカスタムエラーハンドラーを使用して、 `var som_map` を標準のエラーメッセージ形式に変更します。 その結果、検証エラーメッセージは、アダプティブフォームのフィールドレベルに表示されます。

## 「サービスを呼び出し」アクションを使用してカスタムハンドラーを追加する

次の手順を実行して、エラーハンドラーを追加し、を使用してカスタムエラー構造を標準エラー構造に変換します。 [ルールエディターの](rule-editor.md) サービス呼び出しアクション：

1. アダプティブフォームをオーサリングモードで開き、任意のフォームオブジェクトを選択して、をタップします。 ![ルールエディター](assets/rule_editor_icon.png) をクリックして、ルールエディターを開きます。
1. 「**[!UICONTROL 作成]**」をタップします。
1. 条件を **[!UICONTROL 条件]** 」セクションに表示されます。 例：[フィールド名] が変更されました。 選択 **[!UICONTROL 変更済み]** から **[!UICONTROL 状態を選択]** 」ドロップダウンリストを使用して、この条件を設定できます。
1. 「**[!UICONTROL Then]**」セクションの「**[!UICONTROL アクションの選択]**」ドロップダウンリストで「**[!UICONTROL サービスの呼び出し]**」を選択します。
1. 次の中から、Post サービスと対応するデータバインディングを選択します。 **[!UICONTROL 入力]** 」セクションに入力します。 例えば、検証する場合は、 **名前**, **ID**、および **ステータス** アダプティブフォームのフィールドで、「ポストサービス (pet) 」を選択し、「 **[!UICONTROL 入力]** 」セクションに入力します。

このルールの結果、に入力した値 **名前**, **ID**、および **ステータス** 手順 2 で定義したフィールドが変更され、フォームのフィールドからタブを離すと、フィールドが検証されます。

1. 選択 **[!UICONTROL コードエディター]** を選択します。
1. タップ **[!UICONTROL コードを編集]**.
1. 既存のコードから次の行を削除します。

   ```javascript
   guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs);
   ```

1. カスタムエラー構造を標準エラー構造に変換するルールを作成し、をタップします。 **[!UICONTROL 完了]** 」と入力してルールを保存します。
例えば、カスタムのエラー構造を標準のエラー構造に変換するには、末尾に次のサンプルコードを追加します。

   ```javascript
   var errorHandler = function(jqXHR, data) {
   var som_map = {
       "id": "guide[0].guide1[0].guideRootPanel[0].Pet[0].id_1[0]",
       "name": "guide[0].guide1[0].guideRootPanel[0].Pet[0].name_2[0]",
       "status": "guide[0].guide1[0].guideRootPanel[0].Pet[0].status[0]"
   };
   
   
   var errorJson = {};
   errorJson.errors = [];
   
   if (data) {
       if (data.originMessage) {
           var errorData;
           try {
               errorData = JSON.parse(data.originMessage);
           } catch (err) {
               // not in json format
           }
   
           if (errorData) {
               Object.keys(errorData).forEach(function(key) {
                   var som_key = som_map[key];
                   if (som_key) {
                       var error = {};
                       error.somExpression = som_key;
                       error.errorMessage = errorData[key];
                       errorJson.errors.push(error);
                   }
               });
           }
           window.guideBridge.handleServerValidationError(errorJson);
       } else {
           window.guideBridge.handleServerValidationError(data);
       }
     }
   };
   
   guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs, null, errorHandler);
   ```

   この `var som_map` 標準形式に変換するアダプティブフォームフィールドの SOM 式を一覧表示します。 アダプティブフォーム内の任意のフィールドの SOM 式を表示するには、フィールドをタップして、 **[!UICONTROL SOM 式を表示]** から **[!UICONTROL その他のオプション]** (...) メニューを使用します。

   次のサンプルコード行をカスタムエラーハンドラーにコピーしてください。

   ```javascript
   guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs, null, errorHandler);
   ```

   executeOperation API には、 `null` および `errorHandler` 新しいカスタムエラーハンドラーに基づくパラメーター。

   アダプティブフォームは、このカスタムエラーハンドラーを使用して、 `var som_map` を標準のエラーメッセージ形式に変更します。 その結果、検証エラーメッセージは、アダプティブフォームのフィールドレベルに表示されます。
