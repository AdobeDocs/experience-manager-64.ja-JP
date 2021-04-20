---
title: アダプティブフォームからフォームデータモデルサービスを呼び出すための API
seo-title: アダプティブフォームからフォームデータモデルサービスを呼び出すための API
description: 'アダプティブフォームフィールド内から WSDL で記述された、Web サービスを呼び出す API について説明します。 '
seo-description: 'アダプティブフォームフィールド内から WSDL で記述された、Web サービスを呼び出す API について説明します。 '
uuid: 40561086-e69d-4e6a-9543-1eb2f54cd836
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: develop
discoiquuid: aa3e50f1-8f5a-489d-a42e-a928e437ab79
feature: Adaptive Forms
translation-type: tm+mt
source-git-commit: 75312539136bb53cf1db1de03fc0f9a1dca49791
workflow-type: tm+mt
source-wordcount: '384'
ht-degree: 60%

---


# アダプティブフォームからフォームデータモデルサービスを呼び出すための API {#api-to-invoke-form-data-model-service-from-adaptive-forms}

## 概要 {#overview}

AEM Forms を使用すると、アダプティブフォームフィールド内からフォームデータモデルで構成されたサービスを呼び出すことで、フォーム作成者はフォームへの記入作業を簡略化および強化することができます。データモデルサービスを呼び出すには、ビジュアルエディターでルールを作成するか、[ルールエディター](/help/forms/using/rule-editor.md)のコードエディターで`guidelib.dataIntegrationUtils.executeOperation` APIを使用してJavaScriptを指定します。

このドキュメントでは、`guidelib.dataIntegrationUtils.executeOperation` APIを使用してサービスを呼び出すJavaScriptの作成に重点を置いています。

## API の使用 {#using-the-api}

`guidelib.dataIntegrationUtils.executeOperation` API は、アダプティブフォームのフィールド内から サービスを呼び出します。API 構文は以下のとおりです。

```
guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs)
```

この API には以下のパラメーターが必要です。

| パラメーター | 説明 |
|---|---|
| `operationInfo` | フォームデータモデルの識別子、操作タイトル、操作名を指定する構造 |
| `inputs` | サービス操作に値が入力されるフォームオブジェクトを指定するための構造 |
| `outputs` | サービス操作が返す値を使用して入力されるフォームオブジェクトを指定する構造 |

`guidelib.dataIntegrationUtils.executeOperation` APIの構造はサービス操作の詳細を指定します。 この構造の構文は以下のとおりです。

```
var operationInfo = {
formDataModelId,
operationTitle,
operationName
};
var inputs = {
inputField1,
inputFieldN
};
var outputs = {
outputField1,
outputFieldN
}
```

API 構造は、サービス操作の以下の詳細を指定します。

<table> 
 <tbody> 
  <tr> 
   <th>パラメーター</th> 
   <th>説明</th> 
  </tr> 
  <tr> 
   <td><code>forDataModelId</code></td> 
   <td>フォームデータモデルへのリポジトリパスをその名前も含めて指定する</td> 
  </tr> 
  <tr> 
   <td><code>operationName</code></td> 
   <td>実行するサービス操作の名前を指定する</td> 
  </tr> 
  <tr> 
   <td><code>input</code></td> 
   <td>1 つ以上のフォームオブジェクトをサービス操作の入力引数にマップする</td> 
  </tr> 
  <tr> 
   <td>出力</td> 
   <td>1 つ以上のフォームオブジェクトをサービス操作からの出力値にマップしてフォームフィールドを埋め込む<br /> </td> 
  </tr> 
 </tbody> 
</table>

## サービスを呼び出すスクリプトのサンプル  {#sample-script-to-invoke-a-service}

次のサンプルスクリプトでは、`guidelib.dataIntegrationUtils.executeOperation` APIを使用して、`employeeAccount`フォームデータモデルで設定された`getAccountById`サービス操作を呼び出します。

`getAccountById`演算は、`empId`引数の入力として`employeeID`フォームフィールドの値を受け取り、対応する従業員の従業員名、口座番号、口座残高を返します。 この出力値は指定されたフォームフィールドに入力されます。例えば、`name`引数の値が`fullName`フォーム要素に入力され、`account`フォーム要素の`accountNumber`引数の値が入力されます。

```
var operationInfo = {
"formDataModelId": "/content/dam/formsanddocuments-fdm/employeeAccount",
"operationName": "getAccountDetails"
};
var inputs = {
"empid" : employeeID
};
var outputs = {
"name" : fullName,
"accountNumber" : account,
"balance" : balance
};
guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs);
```

