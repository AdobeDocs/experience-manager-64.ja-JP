---
title: 外部 Web ページへのアダプティブフォームの埋め込み
seo-title: 外部 Web ページへのアダプティブフォームの埋め込み
description: 外部 Web ページにアダプティブフォームを埋め込む方法について学びましょう
seo-description: 外部 HTML Web ページにアダプティブフォームを埋め込む方法について学びましょう
uuid: c612ca3b-62f7-4021-939b-e0c05dbbf0d7
products: SG_EXPERIENCEMANAGER/6.3/FORMS
topic-tags: author
discoiquuid: b99c7b93-ba05-42ee-9ca8-0079e15d8602
translation-type: tm+mt
source-git-commit: 61c9abca40007271f1fba49d3d5e3136df91938d
workflow-type: tm+mt
source-wordcount: '1271'
ht-degree: 49%

---


# 外部 Web ページへのアダプティブフォームの埋め込み{#embed-adaptive-form-in-external-web-page}

外部 Web ページにアダプティブフォームを埋め込む方法について学びましょう

You can [Embed adaptive form in AEM Sites](/help/forms/using/embed-adaptive-form-aem-sites.md) page or a web page hosted outside AEM. 埋め込まれたアダプティブフォームではすべての機能を使用できるため、ユーザーは、ページから移動することなくフォームを記入および送信できます。これにより、ユーザーは Web ページのその他のエレメントから離れることなく、同時にフォームの操作を行うことができます。

## 前提条件 {#prerequisites}

アダプティブフォームを外部Webサイトに埋め込む前に、次の手順を実行します。

* AEM パブリッシュインスタンスにアダプティブフォームをパブリッシュします。
* Web サイト上で、アダプティブフォームをホストする Web ページを決定するか、新規に作成します。Ensure that the webpage can [read jQuery files from a CDN](https://ajax.googleapis.com/ajax/libs/jquery/3.3.1/jquery.min.js) or has a local copy of the jQuery embeded. アダプティブフォームをレンダリングするには、jQueryが必要です。
* When AEM server and the web page are on different domains, perform the steps listed in sectiion, [enable AEM Forms to serve adaptive forms to a cross domain site](#cross-domain-sites).
* [外部ページとAEM Formsサーバー間の通信を有効にするには、リバースプロキシ](#reveseproxy) を設定します。

## アダプティブフォームの埋め込み {#embed-adaptive-form}

WebページにJavaScriptの数行を挿入することで、アダプティブフォームを埋め込むことができます。 コードの API は AEM サーバーにアダプティブフォームのリソースを求める HTTP リクエストを送信し、指定したフォームコンテナにアダプティブフォームを挿入します。アダプティブフォームを外部ページに埋め込むためのサンプルコードを以下に示します。 実稼働環境ではコードを使用しないでください。 独自のバージョンのjQueryを使用するWebサイト用のiFrameの使用など、Webサイトに合わせてコードをカスタマイズします。 iFrameを使用すると、jQueryバージョン内での競合を回避できます。


1. 次のコードをWebサイト上のWebページに埋め込みます。

   ```
   
   
<!doctype html>
<html>
  <head><meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
    <title>これはWebページのタイトルです！</title>
    <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.3.1/jquery.min.js"></script>
  </head>
  <body>
  <div class="customafsection"/>
    <p>この節は、アダプティブフォームに置き換えられます。</p>


    &lt;script>
    var options = {path:&quot;/content/forms/af/locbasic.html&quot;, dataRef:&quot;&quot;, themepath:&quot;&quot;, CSS_Selector:&quot;.customafsection&quot;};
    alert(options.path);
    var loadAdaptiveForm = function(options){
    ///alert(options.path);if(options.path)が発行url of the adaptive form
    
    
    // For Example: http:myserver:4503/content/forms/af/ABC，ここでABCはアダプティブフォーム
    //注意： AEMサーバーがコンテキストパスで実行されている場合、アダプティブフォームURLには、コンテキスト
    パスvar path = options.path;
    path += &quot;/jcr:content/guideContainer.html&quot;;
    $.ajax({
    url: path ,
    type : &quot;GET&quot;,
    data : {
    // wcmmodeをdisabledwcmmodeに設定し
    ます。 &quot;disabled&quot;
    // Set the data reference, if any
    // &quot;dataRef&quot;: options.dataRef
    // Specify a different theme for the form object
    // &quot;themeOverride&quot; : options.themepath
    },
    async: false,
    success: 関数(data) {
    // jqueryがロードされている場合は、コンテナの内部htmlを設定し
    // jqueryがロードされていない場合は、ドキュメントが提供するAPIを使用して内部HTMLを設定しますが、これらのAPIは、HTML5 spec
    //に従ってHTMLのスクリプトタグを評価しません。 ドキュメント.getElementById().
    innerHTMLif(window.$ &amp;&amp; options.CSS_Selector){
    // jqueryのHTML APIは、タグを抽出し、DOMを更新し、スクリプトタグに埋め込まれたコードを評価します。
    $(options.CSS_Selector).html(data);
    }
    },
    error: function (data) {
    // any error handler
    }
    });
    } else {
    if (typeof(console) !== &quot;undefined&quot;) {
    console.log(&quot;Path of Adaptive Form not specified to loadAdaptiveForm&quot;);
    }
    }
    (options);
    
    &lt;/script>
</body>
</html>
   ```

1. 埋め込まれたコードで：

   * Change value of the `options.path` variable with the path of the publish URL of the adaptive form. AEM サーバーがコンテキストパス上で実行されている場合は、その URL にコンテキストパスが含まれるようにします。例えば、上記のコードとアダプティブフォームは同じaem formsサーバー上に存在するので、例ではアダプティブフォーム/content/forms/af/locbasic.htmlのコンテキストパスを使用します。
   * `options.dataRef` を URL を渡す属性と置き換えます。You can use the dataref variable to [prefill an adaptive form](/help/forms/using/prepopulate-adaptive-form-fields.md).
   * `options.themePath` をアダプティブフォームで設定されたテーマ以外のテーマへのパスと置き換えます。また、リクエストの属性を使用してテーマのパスを指定することができます。
   * `CSS_Selector` は、アダプティブフォームが埋め込まれているフォームコンテナの CSS セレクターです。例えば、.customafsection cssクラスは、上記の例のCSSセレクターです。

アダプティブフォームが Web ページに埋め込まれました。埋め込まれたアダプティブフォームで次を確認します。

* 元のアダプティブフォームにあったヘッダーとフッターは、埋め込まれたフォームには含まれません。
* ドラフトおよび送信済みフォームは、フォームポータル上の「ドラフト」タブと「送信」タブで使用できます。
* 元のアダプティブフォームに構築された送信アクションは、埋め込まれたフォームでも保持されます。
* アダプティブフォームのルールは保持され、埋め込みフォームでも完全に機能します。
* 元のフォームに構築されたのエクスペリエンスのターゲット設定と A/B テストは、埋め込まれたアダプティブフォームでは動作しません。
* 元のフォームに Adobe Analytics が構築されている場合、分析データは Adobe Analytics サーバーで取得されます。ただし、フォームの分析レポートでは使用できません。

## リバースプロキシの設定  {#reveseproxy}

アダプティブフォームを埋め込む外部 Web ページは、プライベートネットワークのファイアウォールの中にある AEM サーバーにリクエストを送信します。リクエストを安全に AEM サーバーに向けるようにするには、リバースプロキシサーバーを設定することをお勧めします。

ディスパッチャーなしで Apache 2.4 リバースプロキシサーバーをセットアップする方法について説明します。In this example, you will host the AEM server with `/forms` context path and map `/forms` for the reverse proxy. It ensures that any request for `/forms` on Apache server are directed to the AEM instance. This topology helps reduces the number of rules at the dispatcher layer as all request prefixed with `/forms` route to the AEM server.

1. `httpd.conf` 設定ファイルを開き、次のコードの行をコメント解除します。または、これらのコードの行をファイルに追加することができます。

   ```
   LoadModule proxy_html_module modules/mod_proxy_html.so 
    LoadModule proxy_http_module modules/mod_proxy_http.so
   ```

1. Set up proxy rules by adding the following lines of code in the `httpd-proxy.conf` configuration file.

   ```
   ProxyPass /forms https://[AEM_Instance]/forms 
    ProxyPassReverse /forms https://[AEM_Instance]/forms
   ```

   Replace `[AEM_Instance`] with the AEM server publish URL in the rules.

AEMサーバーをコンテキストパスにマウントしない場合、Apacheレイヤーのプロキシルールは次のようになります。

```java
ProxyPass /content https://<AEM_Instance>/content
ProxyPass /etc https://<AEM_Instance>/etc
ProxyPass /etc.clientlibs https://<AEM_Instance>/etc.clientlibs
# CSRF Filter
ProxyPass /libs/granite/csrf/token.json https://<AEM_Instance>/libs/granite/csrf/token.json
  
ProxyPassReverse /etc https://<AEM_Instance>/etc
ProxyPassReverse /etc.clientlibs https://<AEM_Instance>/etc.clientlibs
# written for thank you page and other URL present in AF during redirect
ProxyPassReverse /content https://<AEM_Instance>/content
```

>[!NOTE]
>
>その他のトポロジーをセットアップする場合は、ディスパッチャーレイヤーの送信、事前入力、およびその他の URL を必ずホワイトリストに登録してください。

## ベストプラクティス {#best-practices}

Web ページにアダプティブフォームを埋め込む場合、次のベストプラクティスを検討します。

* Web ページの CSS に定義されたスタイルルールが、フォームオブジェクト CSS と衝突しないようにしてください。衝突を避けるため、アダプティブフォームテーマの Web ページ CSS を AEM クライアントライブラリを使用して再利用できます。アダプティブフォームテーマのクライアントライブラリの使用について詳しくは、「[AEM Forms のテーマ](/help/forms/using/themes.md)」を参照してください。
* Web ページのフォームコンテナがウィンドウの幅全体を使用するようにしてください。これにより、モバイルデバイスに設定された CSS ルールが確実に変更なしで動作するようになります。フォームコンテナがウィンドウの幅全体に表示されない場合は、さまざまなモバイルデバイスに適合するようにカスタムの CSS を記述する必要があります。
* Use  [getData](https://helpx.adobe.com/jp/experience-manager/6-4/forms/javascript-api/GuideBridge.html) API to get the XML or JSON representation of form data in client.
* Use [unloadAdaptiveForm](https://helpx.adobe.com/jp/experience-manager/6-4/forms/javascript-api/GuideBridge.html) API to unload the adaptive form from HTML DOM.
* AEMサーバーから応答を送信する際に、access-control-接触チャネルのヘッダーを設定します。

## AEM Forms がクロスドメインサイトに対してアダプティブフォームをサーブできるようにする  {#cross-domain-sites}

1. On AEM author instance, go to AEM Web Console Configuration Manager at `http://[server]:[port]/system/console/configMgr`.
1. **Apache Sling転送者** Filter設定を探して開きます。
1. 「**許可済みホスト**」フィールドで、Web ページが存在するドメインを指定します。これにより、ホストは AEM サーバーに POST リクエストをできるようになります。正規式を使用して、一連の外部アプリケーションドメインを指定することもできます。