---
title: アダプティブフォームからフォームデータモデルサービスを呼び出すための API
seo-title: API to invoke form data model service from adaptive forms
description: アダプティブフォームフィールド内から WSDL で記述された Web サービスを呼び出すために使用できる invokeWebServices API について説明します。
seo-description: Explains the invokeWebServices API that you can use to invoke web services written in WSDL from within an adaptive form field.
uuid: 40561086-e69d-4e6a-9543-1eb2f54cd836
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: develop
discoiquuid: aa3e50f1-8f5a-489d-a42e-a928e437ab79
feature: Adaptive Forms
exl-id: 0653b0e4-a697-472a-8093-5ed48ede3c75
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '351'
ht-degree: 55%

---

# アダプティブフォームからフォームデータモデルサービスを呼び出すための API {#api-to-invoke-form-data-model-service-from-adaptive-forms}

## 概要 {#overview}

AEM Formsを使用すると、フォーム作成者は、フォームデータモデルで設定されたサービスをアダプティブフォームフィールド内から呼び出すことで、フォームの入力操作をさらに簡素化し、強化することができます。 データモデルサービスを呼び出すには、ビジュアルエディターでルールを作成するか、[ルールエディター](/help/forms/using/rule-editor.md)のコードエディターの `guidelib.dataIntegrationUtils.executeOperation` API を使用して JavaScript を指定します。

このドキュメントでは、`guidelib.dataIntegrationUtils.executeOperation` API を使用して JavaScript を記述してサービスを呼び出す方法に焦点を当てています。

## API の使用 {#using-the-api}

`guidelib.dataIntegrationUtils.executeOperation` API は、アダプティブフォームのフィールド内から サービスを呼び出します。API 構文は以下のとおりです。

```
guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs)
```

API には次のパラメーターが必要です。

| パラメーター | 説明 |
|---|---|
| `operationInfo` | フォームデータモデルの識別子、操作タイトル、操作名を指定する構造 |
| `inputs` | サービス操作に値が入力されるフォームオブジェクトを指定する構造 |
| `outputs` | サービス操作によって返される値を使用して入力されるフォームオブジェクトを指定する構造 |

`guidelib.dataIntegrationUtils.executeOperation` API の構造は、サービス操作の詳細を指定します。構造の構文は次のとおりです。

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

API 構造では、サービス操作に関する次の詳細を指定します。

<table> 
 <tbody> 
  <tr> 
   <th>パラメーター</th> 
   <th>説明</th> 
  </tr> 
  <tr> 
   <td><code>forDataModelId</code></td> 
   <td>名前を含むフォームデータモデルのリポジトリパスを指定します</td> 
  </tr> 
  <tr> 
   <td><code>operationName</code></td> 
   <td>実行するサービス操作の名前を指定します</td> 
  </tr> 
  <tr> 
   <td><code>input</code></td> 
   <td>1 つ以上のフォームオブジェクトをサービス操作の入力引数にマッピングする</td> 
  </tr> 
  <tr> 
   <td>出力</td> 
   <td>1 つ以上のフォームオブジェクトをサービス操作からの出力値にマップして、フォームフィールドに入力します<br /> </td> 
  </tr> 
 </tbody> 
</table>

## サービスを呼び出すスクリプトのサンプル {#sample-script-to-invoke-a-service}

以下のサンプルスクリプトでは、`guidelib.dataIntegrationUtils.executeOperation` API を使用して、`employeeAccount` フォームデータモデルで構成された `getAccountById` サービス操作を呼び出しています。

`getAccountById` 操作は、`empId` 引数の入力値として `employeeID` フォームフィールドにある値を使用し、該当する従業員の名前、口座番号、口座残高を戻します。この出力値は指定されたフォームフィールドに入力されます。例えば、`name` 引数の値は `fullName` フォーム要素に入力され、`accountNumber` 引数の値は `account` フォーム要素に入力されます。

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
