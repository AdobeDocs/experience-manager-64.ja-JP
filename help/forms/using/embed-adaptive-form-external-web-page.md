---
title: 外部 Web ページへのアダプティブフォームの埋め込み
seo-title: Embed adaptive form in external web page
description: 外部 Web ページにアダプティブフォームを埋め込む方法について学びましょう
seo-description: Learn how to embed an adaptive form in an external HTML web page
uuid: c612ca3b-62f7-4021-939b-e0c05dbbf0d7
products: SG_EXPERIENCEMANAGER/6.3/FORMS
topic-tags: author
discoiquuid: b99c7b93-ba05-42ee-9ca8-0079e15d8602
feature: Adaptive Forms
exl-id: 84a46197-9933-4b94-a8e3-e7baf9c644b1
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '1034'
ht-degree: 84%

---

# 外部 Web ページへのアダプティブフォームの埋め込み{#embed-adaptive-form-in-external-web-page}

外部 Web ページにアダプティブフォームを埋め込む方法について学びましょう

以下が可能です。 [AEM Sitesにアダプティブフォームを埋め込む](/help/forms/using/embed-adaptive-form-aem-sites.md) ページまたはAEMの外でホストされる Web ページ。 埋め込まれたアダプティブフォームではすべての機能を使用できるため、ユーザーは、ページから移動することなくフォームを記入および送信できます。これにより、ユーザーは Web ページのその他のエレメントから離れることなく、同時にフォームの操作を行うことができます。

## 前提条件 {#prerequisites}

外部 Web サイトにアダプティブフォームを埋め込む前に次の手順を実行します。：

* AEM パブリッシュインスタンスにアダプティブフォームをパブリッシュします。
* Web サイト上で、アダプティブフォームをホストする Web ページを作成するか、特定してください。その Web ページが [CDN から送信される jQuery ファイルを読み取ることができること](https://ajax.googleapis.com/ajax/libs/jquery/3.3.1/jquery.min.js)、または web ページに jQuery のローカルコピーが埋め込まれていることを確認してください。jQuery は、アダプティブフォームのレンダリングに必要です。
* AEM サーバーと web ページが異なるドメイン上に存在する場合、[AEM Forms がクロスドメインサイトに対してアダプティブフォームをサーブできるようにする](#cross-domain-sites)節に記載された手順を実行してください。
* [リバースプロキシの設定](#reveseproxy) 外部ページとAEM Formsサーバとの間の通信を可能にする。

## アダプティブフォームの埋め込み {#embed-adaptive-form}

Web ページに数行の JavaScript を挿入することで、アダプティブフォームを埋め込むことができます。コードの API は AEM サーバーにアダプティブフォームのリソースを求める HTTP リクエストを送信し、指定したフォームコンテナにアダプティブフォームを挿入します。アダプティブフォームを外部ページに埋め込むためのサンプルコードを以下に示します。 コードは実稼動環境では使用しないでください。 独自のバージョンの jQuery を使用する Web サイト用に iFrame を使用するなど、Web サイトに合わせてコードをカスタマイズします。 iFrame を使用すると、jQuery バージョン内での競合を回避できます。


1. 次のコードを Web サイトの Web ページに埋め込みます。

   ```html
   <!doctype html>
   <html>
   <head>
    <title>This is the title of the webpage!</title>
    <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.3.1/jquery.min.js"></script>
   </head>
   <body>
   <div class="customafsection"/>
   <p>This section is replaced with the adaptive form.</p>
   
    <script>
    var options = {path:"/content/forms/af/locbasic.html", dataRef:"", themepath:"", CSS_Selector:".customafsection"};
    alert(options.path);
    var loadAdaptiveForm = function(options){
    //alert(options.path);
    if(options.path) {
        // options.path refers to the publish URL of the adaptive form
        // For Example: http:myserver:4503/content/forms/af/ABC, where ABC is the adaptive form
        // Note: If AEM server is running on a context path, the adaptive form URL must contain the context path 
        var path = options.path;
        path += "/jcr:content/guideContainer.html";
        $.ajax({
            url  : path ,
            type : "GET",
            data : {
                // Set the wcmmode to be disabled
                wcmmode : "disabled"
                // Set the data reference, if any
               // "dataRef": options.dataRef
                // Specify a different theme for the form object
              //  "themeOverride" : options.themepath
            },
            async: false,
            success: function (data) {
                // If jquery is loaded, set the inner html of the container
                // If jquery is not loaded, use APIs provided by document to set the inner HTML but these APIs would not evaluate the script tag in HTML as per the HTML5 spec
                // For example: document.getElementById().innerHTML
                if(window.$ && options.CSS_Selector){
                    // HTML API of jquery extracts the tags, updates the DOM, and evaluates the code embedded in the script tag.
                    $(options.CSS_Selector).html(data);
                }
            },
            error: function (data) {
                // any error handler
            }
        });
    } else {
        if (typeof(console) !== "undefined") {
            console.log("Path of Adaptive Form not specified to loadAdaptiveForm");
        }
    }
    }(options);
   
    </script>
   </body>
   </html>
   ```

1. 埋め込まれたコードで、

   * `options.path` 変数の値をアダプティブフォームのパブリッシュ URL のパスに変更します。AEM サーバーがコンテキストパス上で実行されている場合は、その URL にコンテキストパスが含まれるようにします。例えば、上記のコードとアダプティブフォームは同じ aem forms サーバー上に存在するので、この例ではアダプティブフォーム/content/forms/af/locbasic.htmlのコンテキストパスを使用します。
   * `options.dataRef` を URL と一緒に渡す属性に置き換えます。dataRef 変数を使用して、[アダプティブフォームに事前にデータを取り込む](/help/forms/using/prepopulate-adaptive-form-fields.md)ことができます。  
   * `options.themePath` をアダプティブフォームで設定されたテーマ以外のテーマへのパスと置き換えます。また、リクエストの属性を使用してテーマのパスを指定することができます。
   * `CSS_Selector` は、アダプティブフォームが埋め込まれているフォームコンテナの CSS セレクターです。例えば、上の例では、.customafsection CSS クラスが CSS セレクターです。

アダプティブフォームが Web ページに埋め込まれました。埋め込まれたアダプティブフォームで次を確認します。

* 元のアダプティブフォームにあったヘッダーとフッターは、埋め込まれたフォームには含まれません。
* ドラフトおよび送信済みフォームは、フォームポータル上の「ドラフト」タブと「送信」タブで使用できます。
* 元のアダプティブフォームに構築された送信アクションは、埋め込まれたフォームでも保持されます。
* アダプティブフォームのルールは保持され、埋め込みフォームでも完全に機能します。
* 元のフォームに構築されたのエクスペリエンスのターゲット設定と A/B テストは、埋め込まれたアダプティブフォームでは動作しません。
* 元のフォームに Adobe Analytics が構築されている場合、分析データは Adobe Analytics サーバーで取得されます。ただし、フォームの分析レポートでは使用できません。

## リバースプロキシの設定  {#reveseproxy}

アダプティブフォームを埋め込む外部 Web ページは、プライベートネットワークのファイアウォールの中にある AEM サーバーにリクエストを送信します。リクエストを安全に AEM サーバーに向けるようにするには、リバースプロキシサーバーを設定することをお勧めします。

ディスパッチャーなしで Apache 2.4 リバースプロキシサーバーをセットアップする方法について説明します。この例では、AEM サーバーを `/forms` コンテキストパスでホストし、リバースプロキシの `/forms` をマッピングします。これで、Apache サーバーの `/forms` へのすべてのリクエストは、AEM インスタンスにダイレクトされます。このトポロジにより、前に `/forms` の付いたすべてのリクエストが AEM サーバー経由になるため、ディスパッチャーレイヤーのルールの数を低減することができます。

1. `httpd.conf` 設定ファイルを開き、次のコードの行をコメント解除します。または、これらのコードの行をファイルに追加することができます。

   ```
   LoadModule proxy_html_module modules/mod_proxy_html.so 
    LoadModule proxy_http_module modules/mod_proxy_http.so
   ```

1. 次のコードの行を `httpd-proxy.conf` 設定ファイルに追加して、プロキシルールをセットアップします。

   ```
   ProxyPass /forms https://[AEM_Instance]/forms 
    ProxyPassReverse /forms https://[AEM_Instance]/forms
   ```

   `[AEM_Instance]` を、ルールの AEM サーバーパブリッシュ URL で置き換えます。

コンテキストパスに AEM サーバーをマウントしない場合、Apache レイヤーのプロキシルールは次のようになります。

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
>その他のトポロジーをセットアップする場合は、ディスパッチャーレイヤーの送信、事前入力、およびその他の URL を必ず許可リストに登録してください。

## ベストプラクティス {#best-practices}

Web ページにアダプティブフォームを埋め込む場合、次のベストプラクティスを検討します。

* Web ページの CSS に定義されたスタイルルールが、フォームオブジェクト CSS と衝突しないようにしてください。衝突を避けるため、アダプティブフォームテーマの Web ページ CSS を AEM クライアントライブラリを使用して再利用できます。アダプティブフォームテーマのクライアントライブラリの使用について詳しくは、「[AEM Forms のテーマ](/help/forms/using/themes.md)」を参照してください。
* Web ページのフォームコンテナがウィンドウの幅全体を使用するようにしてください。これにより、モバイルデバイスに設定された CSS ルールが確実に変更なしで動作するようになります。フォームコンテナがウィンドウの幅全体に表示されない場合は、さまざまなモバイルデバイスに適合するようにカスタムの CSS を記述する必要があります。
* 用途  [getData](https://helpx.adobe.com/jp/experience-manager/6-4/forms/javascript-api/GuideBridge.html) クライアントでフォームデータの XML または JSON 表現を取得する API。
* 用途 [unloadAdaptiveForm](https://helpx.adobe.com/experience-manager/6-4/forms/javascript-api/GuideBridge.html) アダプティブフォームをHTMLDOM からアンロードする API。
* AEM サーバーから応答を送信するときは、access-control-origin ヘッダーを設定してください。

## AEM Forms がクロスドメインサイトに対してアダプティブフォームをサーブできるようにする  {#cross-domain-sites}

1. AEM パブリッシュインスタンスで、AEM Web Console Configuration Manager（`http://[server]:[port]/system/console/configMgr`）に移動します。
1. を探して開きます。 **Apache Sling Referrer** フィルター設定。
1. 「**許可済みホスト**」フィールドで、Web ページが存在するドメインを指定します。これにより、ホストは AEM サーバーに POST リクエストをできるようになります。また、正規表現を使用して、一連の外部アプリケーションドメインを指定することもできます。
