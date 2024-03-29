---
title: クイックビューを使用したカスタムポップアップの作成
seo-title: Using Quickviews to create custom pop-ups
description: e コマースエクスペリエンスではデフォルトのクイックビューが使用され、ポップアップに購入を促す商品情報が表示されます。ポップアップにカスタムコンテンツを表示することもできます。
seo-description: The default Quickview is used in ecommerce experiences whereby a pop-up is displayed with product information to drive a purchase. You can trigger custom content to display in the pop-ups.
uuid: b906cfff-ac44-4989-b6da-8a9bbf02af03
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.4/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: 4bcab3f4-500f-432e-b16b-cdc26b9bab4d
exl-id: 56b070e4-b445-4488-acff-685b7ce5785f
feature: Configuration
role: Admin,User,Developer
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '1046'
ht-degree: 70%

---

# クイックビューを使用したカスタムポップアップの作成 {#using-quickviews-to-create-custom-pop-ups}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

e コマースエクスペリエンスではデフォルトのクイックビューが使用され、ポップアップに購入を促す商品情報が表示されます。ただし、このようなポップアップにカスタムコンテンツが表示されるように設定できます。使用しているビューアに応じて、ユーザーはホットスポット、サムネール画像、画像マップのいずれかをクリックして、情報や関連コンテンツを表示できます。

クイックビューは、Dynamic Media の以下のビューアでサポートされています。

* インタラクティブ画像（クリック可能なホットスポット）
* インタラクティブビデオ（ビデオの再生中にクリック可能なサムネール画像）
* カルーセルバナー（クリック可能なホットスポットまたは画像マップ）

各ビューアの機能は異なりますが、サポートされる 3 つすべてのビューアでクイックビューの作成手順は同じです。

**クイックビューを使用してカスタムポップアップを作成するには：**

1. アップロードしたアセット用にクイックビューを作成します。

   通常、クイックビューは、使用しているビューアで使用するアセットを編集するのと同時に作成します。

   <table> 
    <tbody> 
    <tr> 
    <td><strong>使用しているビューア</strong></td> 
    <td><strong>クイックビューを作成するために実行する手順</strong></td> 
    </tr> 
    <tr> 
    <td>インタラクティブ画像</td> 
    <td><a href="/help/assets/interactive-images.md#adding-hotspots-to-an-image-banner" target="_blank">画像バナーへのホットスポットの追加</a>.</td> 
    </tr> 
    <tr> 
    <td>インタラクティブビデオ</td> 
    <td><a href="/help/assets/interactive-videos.md#adding-interactivity-to-your-video" target="_blank">ビデオへのインタラクティブ機能の追加</a>.</td> 
    </tr> 
    <tr> 
    <td>カルーセルバナー</td> 
    <td><a href="/help/assets/carousel-banners.md#adding-hotspots-or-image-maps-to-an-image-banner" target="_blank">バナーへのホットスポットまたは画像マップの追加</a>.<br /> </td> 
    </tr> 
    </tbody> 
   </table>

1. ビューアの埋め込みコードを取得して、Web サイト内にビューアを統合します。

   <table> 
    <tbody> 
    <tr> 
    <td><strong>使用しているビューア</strong><br /> </td> 
    <td><strong>ビューアを Web サイトに統合するために実行する手順</strong></td> 
    </tr> 
    <tr> 
    <td>インタラクティブ画像</td> 
    <td><a href="/help/assets/interactive-images.md#integrating-an-interactive-image-with-your-website" target="_blank">インタラクティブ画像の Web サイトへの統合</a>.<br /> </td> 
    </tr> 
    <tr> 
    <td>インタラクティブビデオ<br /> </td> 
    <td><a href="/help/assets/interactive-videos.md#integrating-an-interactive-video-with-your-website" target="_blank">インタラクティブビデオの Web サイトへの統合</a>.<br /> </td> 
    </tr> 
    <tr> 
    <td>カルーセルバナー</td> 
    <td><a href="/help/assets/carousel-banners.md#adding-a-carousel-banner-to-your-website-page" target="_blank">Web サイトページへのカルーセルバナーの追加</a>.<br /> </td> 
    </tr> 
    </tbody> 
   </table>

1. 使用しているビューアが、クイックビューの使用方法を認識する必要があります。

   このために、ビューアは `QuickViewActive` というハンドラーを使用します。

   **例** Web ページでインタラクティブ画像用に以下のサンプル埋め込みコードを使用しているとします。

   ![chlimage_1-291](assets/chlimage_1-291.png)

   ハンドラーは `setHandlers` を使用してビューアに読み込まれます。

   `*viewerInstance*.setHandlers({ *handler 1*, *handler 2*}, ...`

   **上記のサンプル埋め込みコードの例を使用すると、以下のようなコードになります。**

   ```xml
   s7interactiveimageviewer.setHandlers({
       quickViewActivate": function(inData) {
           var sku=inData.sku;
           var genericVariable1=inData.genericVariable1;
           var genericVariable2=inData.genericVariable2;
          loadQuickView(sku,genericVariable1,genericVariable2);
       }
   })
   ```

   `setHandlers()` メソッドについて詳しくは、以下を参照してください。

   * インタラクティブ画像ビューア： [setHandlers](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/jsapi-interactive-image/r-html5-aem-int-image-viewer-javascriptapiref-sethandlers.html?lang=ja)
   * インタラクティブビデオビューア： [setHandlers](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-video/jsapi-interactive-video/r-html5-aem-int-video-javascriptapiref-sethandlers.html?lang=ja)

1. 次に、`quickViewActivate` ハンドラーを設定する必要があります。

   quickViewActivate ハンドラーは、ビューアのクイックビューを制御します。 このハンドラーには、クイックビューで使用する変数のリストと関数呼び出しが含まれています。埋め込みコードは、クイックビューの SKU 変数セット用のマッピングと、サンプルの loadQuickView 関数呼び出しを提供しています。

   **変数マッピング** Web ページで使用する変数を SKU 値とクイックビューに含まれる一般変数にマッピングします。

   `var *variable1*= inData.*quickviewVariable*`

   提供された埋め込みコードには、SKU 変数用のサンプルマッピングが含まれています。

   `var sku=inData.sku`

   以下のように、クイックビューからの追加変数もマッピングします。

   ```
   var <i>variable2</i>= inData.<i>quickviewVariable2</i> 
    var <i>variable3</i>= inData.<i>quickviewVariable3</i>
   ```

   **関数呼び出し**&#x200B;ハンドラーには、クイックビューを機能させるために関数呼び出しも必要です。関数は、ホストページからアクセス可能であると想定されます。 埋め込みコードは、次のサンプル関数呼び出しを提供しています。

   `loadQuickView(sku)`

   このサンプル関数呼び出しは、関数 `loadQuickView()` が存在しアクセス可能であることが前提となります。

   quickViewActivate メソッドの詳細については、次を参照してください。

   * インタラクティブ画像ビューア ‐ [イベントコールバック](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/c-html5-aem-interactive-image-event-callbacks.html?lang=ja)
   * インタラクティブビデオビューア ‐ [イベントコールバック](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-video/c-html5-aem-int-video-event-callbacks.html?lang=ja)
   * インタラクティブビデオビューアでのインタラクティブデータのサポート ‐ [インタラクティブデータのサポート](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-video/c-html5-aem-int-video-int-data-support.html?lang=ja)

1. 以下の操作を実行してください。

   * 埋め込みコードの setHandlers セクションのコメントを解除します。
   * クイックビューに含まれる追加の変数をマッピングします。

      * 変数を追加する場合は、`loadQuickView(sku,*var1*,*var2*)` 呼び出しを更新します。
   * ビューア外でページにシンプルな loadQuickView() 関数を作成します。

       例えば、以下により、ブラウザーのコンソールに sku の値が書き込まれます。

   ```xml
   function loadQuickView(sku){
       console.log ("quickview sku value is " + sku);
   }
   ```

   * Web サーバーにテスト HTML ページをアップロードし、開きます。

       クイックビューからの変数がマッピングされ、関数呼び出しが追加された状態で、ブラウザーコンソールは提供されたサンプル関数を使用してブラウザーコンソールに変数値を書き込みます。



1. これで、関数を使用してクイックビューでシンプルなポップアップを起動できるようになりました。以下の例では、ポップアップに `DIV` を使用しています。
1. ポップアップの `DIV` を以下のようなスタイルにします。必要に応じて独自のスタイルを追加します。

   ```xml
   <style type="text/css">
       #quickview_div{
           position: absolute;
           z-index: 99999999;
           display: none;
       }
   </style>
   ```

1. HTML ページのボディにポップアップの `DIV` を配置します。

   要素の 1 つに、ユーザーがクイックビューを起動したときに sku 値で更新される ID が設定されます。 この例には、ポップアップを表示後に再び隠すための簡単なボタンも含まれています。

   ```xml
   <div id="quickview_div" >
       <table>
           <tr><td><input id="btnClosePopup" type="button" value="Close"        onclick='document.getElementById("quickview_div").style.display="none"' /><br /></td></tr>
           <tr><td>SKU</td><td><input type="text" id="txtSku" name="txtSku"></td></tr>
       </table>
   </div>
   ```

1. ポップアップの sku 値を更新する関数を追加します。手順 5 で作成したシンプルな関数を置き換えて、ポップアップを表示できるようにします。 を次のように設定します。

   ```xml
   <script type="text/javascript">
       function loadQuickView(sku){
           document.getElementById("txtSku").setAttribute("value",sku); // write sku value
           document.getElementById("quickview_div").style.display="block"; // show popup
       }
   </script>
   ```

1. Web サーバーにテスト用の HTML ページをアップロードして開きます。ユーザーがクイックビューを起動すると、ビューアにポップアップの `DIV` が表示されます。
1. **全画面表示モードでカスタムポップアップを表示する方法**

   インタラクティブビデオビューアなどの一部のビューアでは、全画面表示モードでの表示をサポートしています。ただし、前の手順で説明したポップアップを使用すると、全画面表示モード中はビューアの背後に表示されるようになります。

   標準モードと全画面表示モードの両方でポップアップを表示させるには、ビューアのコンテナにポップアップをアタッチします。それには、2 つ目のハンドラーメソッド `initComplete` を使用できます。

   `initComplete` ハンドラーは、ビューアの初期化後に起動します。

   ```xml
   "initComplete":function() { code block }
   ```

   `init()` メソッドについて詳しくは、以下を参照してください。

   * インタラクティブ画像ビューア ‐ [init](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/jsapi-interactive-image/r-html5-aem-int-image-viewer-javascriptapiref-init.html?lang=ja)
   * インタラクティブビデオビューア ‐ [init](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-video/jsapi-interactive-video/r-html5-aem-int-video-javascriptapiref-init.html?lang=ja)

1. 前の手順で言及したように、ビューアにポップアップをアタッチするには、以下のコードを使用します。

   ```xml
   "initComplete":function() {
       var popup = document.getElementById('quickview_div');
       popup.parentNode.removeChild(popup);
       var sdkContainerId = s7interactivevideoviewer.getComponent("container").getInnerContainerId();
       var inner_container = document.getElementById(sdkContainerId);
       inner_container.appendChild(popup);
   }
   ```

   上記のコードでは、次の操作をおこないました。

   * カスタムポップアップを特定しました。
   * DOM から削除しました。
   * ビューアのコンテナを識別しました。
   * ビューアのコンテナにポップアップをアタッチしました。

1. setHandlers コード全体は、次のようになります（インタラクティブビデオビューアを使用していました）。

   ```xml
   s7interactivevideoviewer.setHandlers({
       "quickViewActivate": function(inData) {
           var sku=inData.sku;
           loadQuickView(sku);
   
       },
       "initComplete":function() {
           var popup = document.getElementById('quickview_div'); // get custom quick view container
           popup.parentNode.removeChild(popup); // remove it from current DOM
           var sdkContainerId = s7interactivevideoviewer.getComponent("container").getInnerContainerId();
           var inner_container = document.getElementById(sdkContainerId);
           inner_container.appendChild(popup);
       }
   });
   ```

1. ハンドラーを読み込んだ後で、ビューアを初期化します。

   `*viewerInstance.*init()`

   **例**：この例では、インタラクティブ画像ビューアを使用します。

   `s7interactiveimageviewer.init()`

   ホストページにビューアを埋め込んだ後で、`init()` を使用してビューアを起動する前に、ビューアインスタンスが作成され、ハンドラーが読み込まれていることを確認してください。
