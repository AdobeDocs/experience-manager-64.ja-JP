---
title: HTML5 forms 用のフォームテンプレートのレンダリング
seo-title: Rendering form template for HTML5 forms
description: HTML5 forms のプロファイルは、プロファイルレンダリングに関連付けられています。プロファイルレンダラーは Forms OSGi サービスを呼び出すことでフォームの HTML 表現を生成する役割を持つ JSP ページです。
seo-description: HTML5 forms profiles are associated with profile renders. Profile Renders are JSP pages responsible for generating HTML representation of the form by calling the Forms OSGi service.
uuid: 34daed78-0611-4355-9698-0d7f758e6b61
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: hTML5_forms
discoiquuid: cb75b826-d044-44be-b364-790c046513e0
feature: Mobile Forms
exl-id: ccdb2045-9339-4f39-acb5-85999c4667b9
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '535'
ht-degree: 78%

---

# HTML5 forms 用のフォームテンプレートのレンダリング {#rendering-form-template-for-html-forms}

## レンダリングエンドポイント {#render-endpoint}

HTML5 の形は **プロファイル** フォームテンプレートのモバイルレンダリングを可能にするために、REST エンドポイントとして公開される。 これらのプロファイルは、 **プロファイルレンダラー**. これらは、Forms OSGi サービスを呼び出してフォームのHTML表現を生成する役割を持つ JSP ページです。 Profile ノードの JCR パスがレンダリングエンドポイントの URL を決定します。「default」プロファイルを指す、フォームのデフォルトのレンダリングエンドポイントは次のようになります。

https://&lt;*ホスト*>:&lt;*ポート*>/content/xfaforms/profiles/default.html?contentRoot=&lt;*フォーム xdp を含むフォルダーのパス*>&amp;template=&lt;*xdp の名前*>

例：`http://localhost:4502/content/xfaforms/profiles/default.html?contentRoot=c:/xdps&template=sampleForm.xdp`

カスタムプロファイルでは、それに応じてエンドポイントが変わります。たとえば、hrforms の名前を持つカスタムプロファイルのエンドポイントは：

`http://localhost:4502/content/xfaforms/profiles/hrforms.html?contentRoot=c:/xdps&template=sampleForm.xdp`

テンプレートが FormSubmission と呼ばれるアプリケーションの AEM リポジトリにある場合、URI は次のとおりです。

```
http://localhost:4502/content/xfaforms/profiles/default.html?
 contentRoot=crx:///content/dam/formsanddocuments/FormSubmission/1.0
 &template=sampleForm.xdp
```

## レンダリングパラメーター {#render-parameters}

次に、HTML 形式でフォームをレンダリングする場合にサポートされるリクエストパラメーターを示します。

<table> 
 <tbody> 
  <tr> 
   <th><strong>パラメーター </strong></th> 
   <th><strong>説明</strong></th> 
  </tr> 
  <tr> 
   <td>テンプレート<br /> </td> 
   <td>このパラメーターはテンプレートファイルの名前を指定します。<br /> </td> 
  </tr> 
  <tr> 
   <td>contentRoot<br /> </td> 
   <td>このパラメーターはテンプレートとそれに関連するリソースが存在するパスを指定します。このパスにはサーバーのファイルシステムパス、リポジトリパス、http または ftp パスを使用できます。<br /> </td> 
  </tr> 
  <tr> 
   <td>submitUrl<br /> </td> 
   <td>このパラメーターはフォームのデータ XML がポストされる URL を指定します。<br /> </td> 
  </tr> 
 </tbody> 
</table>

### フォームテンプレートとのデータの結合 {#merge-data-with-form-template}

| パラメーター | 説明 |
|---|---|
| dataRef | このパラメーターはテンプレートと結合されるデータファイルの&#x200B;**絶対パス**&#x200B;を指定します。このパラメーターには、XML 形式のデータを返す REST サービスへの URL を指定できます。 |
| data | このパラメーターはテンプレートと結合される UTF-8 エンコードされたデータバイトを指定します。このパラメーターが指定されている場合、HTML5 form は dataRef パラメーターを無視します。 |

### レンダリングパラメーターの送信 {#passing-the-render-parameter}

HTML5 forms は 3 つの方法によるレンダリングパラメーターの送信をサポートしています。URL、キー値ペア、およびプロファイルノードを使用してパラメーターを渡すことができます。レンダリングパラメーターでは、キー値ペアは最高の優先度を持ち、プロファイルノードがその次に高い優先度を持ちます。URL Request パラメーターは、最も優先順位が低くなります。

* **URL リクエストパラメーター**: レンダリングパラメーターを URL で指定できます。 URL リクエストパラメーターでは、パラメーターはエンドユーザーに対して表示されます。例えば、次の送信 URL の URL には、URL に template パラメーターが含まれています。 `http://localhost:4502/content/xfaforms/profiles/default.html?contentRoot=/Applications/FormSubmission/1.0&template=sampleForm.xdp`

* **SetAttribute リクエストパラメーター**: レンダリングパラメーターをキー値ペアとして指定できます。 SetAttribute リクエストパラメーターでは、パラメーターはエンドユーザーに対して表示されません。リクエストを他の JSP から HTML5 form のプロファイルレンダラ― JSP に転送し、リクエストオブジェクトで *setAttribute* を使用してすべてのレンダリングパラメーターを渡すことができます。この方法は最高の優先度を持ちます。

* **プロファイルノードリクエストパラメーター：** レンダリングパラメーターは、プロファイルノードのノードプロパティとして指定できます。 プロファイルノードリクエストパラメーターでは、パラメーターはエンドユーザーに対して表示されません。プロファイルノードは、リクエストが送信されるノードです。パラメーターをノードプロパティとして指定するには、CRXDE lite を使用します。

### 送信パラメーター {#submit-parameters}

HTML5 forms はデータを送信し、サーバー側スクリプトおよび Web サービスを AEM サーバーで実行します。サーバー側スクリプトと Web サービスを AEM サーバーで実行するために使用するパラメーターについて詳しくは、[HTML5 フォームサービスプロキシ](/help/forms/using/service-proxy.md)を参照してください。
