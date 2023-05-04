---
title: HTML5 forms 用のフォームテンプレートのレンダリング
seo-title: Rendering form template for HTML5 forms
description: HTML5 フォームプロファイルは、プロファイルレンダーに関連付けられています。 プロファイルレンダーは、Forms OSGi サービスを呼び出してフォームのHTML表現を生成する役割を持つ JSP ページです。
seo-description: HTML5 forms profiles are associated with profile renders. Profile Renders are JSP pages responsible for generating HTML representation of the form by calling the Forms OSGi service.
uuid: 34daed78-0611-4355-9698-0d7f758e6b61
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: hTML5_forms
discoiquuid: cb75b826-d044-44be-b364-790c046513e0
feature: Mobile Forms
exl-id: ccdb2045-9339-4f39-acb5-85999c4667b9
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '571'
ht-degree: 36%

---

# HTML5 forms 用のフォームテンプレートのレンダリング {#rendering-form-template-for-html-forms}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

## レンダリングエンドポイント {#render-endpoint}

HTML5 forms には、フォームテンプレートのモバイルレンダリングを可能にするため、REST エンドポイントとして公開される&#x200B;**プロファイル**&#x200B;の概念があります。これらのプロファイルには関連する&#x200B;**プロファイルレンダラー**&#x200B;があります。それらは Forms OSGi サービスを呼び出すことでフォームの HTML 表現を生成する役割を持つ JSP ページです。Profile ノードの JCR パスによって、レンダーエンドポイントの URL が決まります。 「default」プロファイルを指すフォームのデフォルトのレンダリングエンドポイントは、次のようになります。

https://&lt;*host*>:&lt;*port*>/content/xfaforms/profiles/default.html?contentRoot=&lt;*path of the folder containg form xdp*>&amp;template=&lt;*name of the xdp*>

例：`http://localhost:4502/content/xfaforms/profiles/default.html?contentRoot=c:/xdps&template=sampleForm.xdp`

カスタムプロファイルの場合は、それに応じてエンドポイントが変更されます。 例えば、hrforms という名前のカスタムプロファイルのエンドポイントは次のようになります。

`http://localhost:4502/content/xfaforms/profiles/hrforms.html?contentRoot=c:/xdps&template=sampleForm.xdp`

テンプレートが FormSubmission と呼ばれるアプリケーションの AEM リポジトリにある場合、URI は次のとおりです。

```
http://localhost:4502/content/xfaforms/profiles/default.html?
 contentRoot=crx:///content/dam/formsanddocuments/FormSubmission/1.0
 &template=sampleForm.xdp
```

## レンダリングパラメータ {#render-parameters}

フォームのレンダリング時にサポートされる要求パラメーターは、次のとおりです。HTML:

<table> 
 <tbody> 
  <tr> 
   <th><strong>パラメーター </strong></th> 
   <th><strong>説明</strong></th> 
  </tr> 
  <tr> 
   <td>テンプレート <br /> </td> 
   <td>このパラメータは、テンプレートファイルの名前を指定します。<br /> </td> 
  </tr> 
  <tr> 
   <td>contentRoot<br /> </td> 
   <td>このパラメーターは、テンプレートと関連するリソースが存在するパスを指定します。 このパスは、サーバのファイルシステムパス、リポジトリパス、http、ftp パスのいずれかです。<br /> </td> 
  </tr> 
  <tr> 
   <td>submitUrl<br /> </td> 
   <td>このパラメーターは、フォームデータ xml が投稿される URL を指定します。<br /> </td> 
  </tr> 
 </tbody> 
</table>

### データをフォームテンプレートと結合 {#merge-data-with-form-template}

| パラメーター | 説明 |
|---|---|
| dataRef | このパラメーターはテンプレートと結合されるデータファイルの&#x200B;**絶対パス**&#x200B;を指定します。このパラメーターには XML 形式データを返す REST サービスへの URL を使用できます。 |
| data | このパラメーターは、テンプレートと結合される UTF-8 でエンコードされたデータバイトを指定します。 このパラメーターが指定されている場合、HTML5 フォームでは dataRef パラメーターが無視されます。 |

### レンダーパラメーターを渡す {#passing-the-render-parameter}

HTML5 フォームは、レンダリングパラメーターを渡す 3 つの方法をサポートしています。 URL、キーと値のペア、プロファイルノードを使用してパラメーターを渡すことができます。 レンダリングパラメーターでは、キーと値のペアが最も高い優先順位を保持し、その後にプロファイルノードが続きます。 URL リクエストパラメーターは最低の優先度を持ちます。

* **URL リクエストパラメーター**: レンダリングパラメーターを URL で指定できます。URL リクエストパラメーターでは、パラメーターはエンドユーザーに対して表示されます。 例えば送信 URL `http://localhost:4502/content/xfaforms/profiles/default.html?contentRoot=/Applications/FormSubmission/1.0&template=sampleForm.xdp` には、その中にテンプレートパラメーターが含まれます。

* **SetAttribute リクエストパラメーター**: レンダリングパラメーターをキー値ペアとして指定できます。SetAttribute リクエストパラメーターでは、パラメーターはエンドユーザーには表示されません。 要求を他の JSP からHTML5 フォームのプロファイルレンダラー JSP に転送し、 *setAttribute* すべてのレンダリングパラメーターを渡すリクエストオブジェクトで使用します。 この方法の優先順位が最も高くなります。

* **プロファイルノードリクエストパラメーター：**&#x200B;レンダリングパラメーターをプロファイルノードのノードプロパティとして指定できます。プロファイルノードリクエストパラメーターでは、パラメーターはエンドユーザーには表示されません。 Profile ノードは、要求が送信されるノードです。 パラメーターをノードプロパティとして指定するには、CRXDE lite を使用します。

### 送信パラメーター {#submit-parameters}

HTML5 フォーム送信データ；AEMサーバーでサーバー側スクリプトと web サービスを実行します。 AEMサーバーでサーバー側スクリプトと Web サービスを実行するために使用されるパラメーターについて詳しくは、 [HTML5 forms サービスプロキシ](/help/forms/using/service-proxy.md).
