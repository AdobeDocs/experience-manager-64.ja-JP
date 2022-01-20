---
title: インタラクティブ画像
seo-title: Interactive Images
description: Dynamic Media でのインタラクティブ画像の使用方法を学習します
seo-description: Learn how to work with interactive images in dynamic media
uuid: e8f79bc1-fccb-48d0-aca1-7f319c595fe9
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.4/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: d630499d-740d-4979-8a34-9e3fcc3b5a23
exl-id: 4d3299e2-269b-4a41-a979-c884c707666d
feature: Interactive Images
role: User
source-git-commit: cdee53ea75faa2e6d1a1ec6ca7aa8bf8b8840e46
workflow-type: tm+mt
source-wordcount: '4247'
ht-degree: 79%

---

# インタラクティブ画像 {#interactive-images}

「ショッパブル」ホットスポットを画像にドラッグドロップすることで、静的な画像をリッチで魅力的なエクスペリエンスに簡単に変えることができます。ショッパブルホットスポットは、製品やサービスに関する追加情報と、販売に直結する「買い物かごに追加」機能や「購入」機能を組み合わせています。顧客はこれらのホットスポットをタップして、製品やサービスに直接リンクしたり、買い物かごに追加したり、Web ページにリンクしたりできます。 直接的なエクスペリエンス（これらのエクスペリエンスにより、Web サイトでの顧客エンゲージメントとコンバージョンが増加します）。

次に、クイックビューポップアップを含むショッパブルバナーを示します。モデルの上の円（「ホットスポット」）をタップすると、クイックビューがアクティブになります。

![chlimage_1-368](assets/chlimage_1-368.png)

この Web ページの実際のインタラクティブ画像は、次の URL から参照してください。

[https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-banner/we-fashion-QVzoom/index2-shoppable.html?lang=ja](https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-banner/we-fashion-QVzoom/index2-shoppable.html?lang=ja)

## インタラクティブ画像バナーの作成方法 {#watch-how-interactive-image-banners-are-created}

[インタラクティブ画像バナーの作成方法](https://s7d5.scene7.com/s7viewers/html5/VideoViewer.html?videoserverurl=https://s7d5.scene7.com/is/content/&amp;emailurl=https://s7d5.scene7.com/s7/emailFriend&amp;serverUrl=https://s7d5.scene7.com/is/image/&amp;config=Scene7SharedAssets/Universal_HTML5_Video_social&amp;contenturl=https://s7d5.scene7.com/skins/&amp;asset=S7tutorials/InteractiveCarouselBanner)を示す 10 分 33 秒のガイドをご覧ください。ここでは、インタラクティブ画像バナーのプレビュー、編集、配信方法も説明します。

## クイックスタート：インタラクティブ画像 {#quick-start-interactive-images}

次のワークフローの手順説明は、AEM Assets 内のインタラクティブ画像をすぐに使い始めることを目的としたものです。

一部のクイックスタートタスク内には「**例**」という見出しがあります。これには、まだインタラクティブ画像が追加されていない次のサンプル Web ページに基づく簡単なチュートリアルが含まれています。

[https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-banner/we-fashion/landing-0.html?lang=ja](https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-banner/we-fashion/landing-0.html?lang=ja)

このチュートリアルでは、Web サイトにインタラクティブ画像を統合する手順が説明されています。

**インタラクティブ画像のワークフロー**:

1. **（オプション）ホットスポットの変数の識別** - AEM Assets と Dynamic Media をスタンドアロンで使用している場合は、まず、既存のクイックビュー実装で使用される動的変数を特定し、インタラクティブ画像を作成するときにホットスポットデータを入力できるようにします。[（オプション）ホットスポットの変数の識別](#optional-identifying-hotspot-variables)を参照してください。

   ただし、AEM Sites または AEM eCommerce（あるいは両方）を使用している場合、この手順は必要ありません。

   [AEM Assets での eCommerce の概念](/help/sites-administering/concepts.md)を参照してください。

1. **（オプション）インタラクティブ画像ビューアプリセットの作成** - ホットスポットを表すために使用するグラフィック画像をカスタマイズします。独自のインタラクティブ画像ビューアプリセットの作成は、標準提供のインタラクティブ画像ビューアプリセット `Shoppable_Banner` を使用する場合には必要ありません。

   [（オプション）インタラクティブ画像ビューアプリセットの作成](managing-viewer-presets.md#creating-a-new-viewer-preset)を参照してください。

1. **画像バナーのアップロード**  — インタラクティブにする画像バナーをアップロードします。

   [画像バナーのアップロード](#uploading-an-image-banner)を参照してください。

1. **画像バナーへのホットスポットの追加**  — 画像バナーに 1 つ以上のホットスポットを追加し、それぞれにアクション（ハイパーリンク、クイックビュー、エクスペリエンスフラグメントなど）を関連付けます。 ホットスポットを追加した後は、インタラクティブ画像を公開するとタスクが終了します。

   * [画像バナーへのホットスポットの追加](#adding-hotspots-to-an-image-banner)を参照してください。
   * [（オプション）インタラクティブ画像のプレビュー](#optional-previewing-interactive-images)を参照してください。必要に応じて、ショッパブルバナーの表示を確認して、インタラクティビティをテストすることができます。
   * インタラクティブ画像アセットの公開方法について詳しくは、[アセットの公開](publishing-dynamicmedia-assets.md)を参照してください。

1. **AEMで Web サイトまたは Web サイトにインタラクティブ画像を追加する**

   * AEM Sites、AEM e コマース、またはその両方を使用する場合は、インタラクティブメディアコンポーネントをページにドラッグすることで、インタラクティブ画像をAEMの Web ページに直接追加できます。 [ページへの Dynamic Media アセットの追加](adding-dynamic-media-assets-to-pages.md)を参照してください。
   * を参照してください。AEM Assets と Dynamic Media をスタンドアロンで使用している場合は、埋め込みコードを Web サイトにコピーしてから、既存のクイックビューに統合する必要があります。[インタラクティブ画像の Web サイトへの統合](#integrating-an-interactive-image-with-your-website)を参照してください。
   * サードパーティの WCM（Web Content Manager）を使用している場合は、新しいインタラクティブビデオを、Web サイトで使用されている既存のクイックビュー実装に統合する必要があります。[インタラクティブ画像の既存のクイックビューへの統合](#integrating-an-interactive-image-with-an-existing-quickview)を参照してください。

## （オプション）ホットスポットの変数の識別  {#optional-identifying-hotspot-variables}

>[!NOTE]
>
>このタスクが必要になるのは次に該当する場合のみです。
>
>* クイックビューをトリガーして、画像にインタラクティブ機能を追加する。
>* eコマースソリューション&#x200B;*（* IBM Websphere Commerce、Elastic Path、hybris、Intershop など）から AEM に製品データを取り出すために、AEM の実装が eコマース統合フレームワークを使用していない。[AEM Assets での eCommerce の概念](/help/sites-administering/concepts.md)を参照してください。

>
>AEM の実装で AEM eCommerce を使用している場合は、このタスクをスキップして次のタスクに進みます。

まず、既存のクイックビュー実装で使用されている動的変数を識別します。こうすることで、ホットスポットデータを入力してインタラクティブ画像を作成できます。

AEM Assets 内でバナー画像にホットスポットを追加する場合は、各ホットスポットに SKU（Stock Keeping Unit。提供される個々の異なる製品やサービス用の一意の識別子）とオプションの追加変数を割り当てる必要があります。そのようなホットスポットの変数は、後でホットスポットとクイックビューコンテンツを対応付けるために使用されます。

重要なのは、ホットスポットデータに関連付けられる変数の数とタイプを正しく識別することです。バナー画像に追加するそれぞれのホットスポットに、既存のバックエンドシステム内で製品を一意に識別するための十分な情報がある必要があります。

ホットスポットデータに使用する一連の変数を識別するには、様々な方法があります。

既存のクイックビュー実装を担当する IT スペシャリストに相談するだけで十分な場合もあります（通常、そのような IT スペシャリストは、システム内のクイックビューを識別するために必要な最小データセットを理解しています）。ただし、ほとんどの場合は、フロントエンドコードの既存の動作を分析するだけでもかまいません。

クイックビュー実装の大部分では、次の枠組みが使用されています。

* ユーザーは Web サイト上の特定のユーザーインターフェイス要素をアクティベートします。例えば、 **[!UICONTROL クイックビュー]** 」ボタンをクリックします。
* Web サイトでは、必要に応じて、クイックビューのデータまたはコンテンツを読み込むための Ajax リクエストをバックエンドに送信します。
* クイックビューのデータは、Web ページでのレンダリングに備えて、コンテンツに変換されます。
* 最後に、フロントエンドコードによってそのコンテンツが画面上に視覚的にレンダリングされます。

次に、クイックビュー機能が実装されている既存の Web サイトの各領域にアクセスしてクイックビューをトリガーし、そのクイックビューのデータまたはコンテンツを読み込むために Web ページから送信される Ajax URL をキャプチャします。

通常、専門のデバッグツールを使用する必要はありません。最新の Web ブラウザーには、十分なタスクを実行できる Web インスペクターが備わっています。Web インスペクターが搭載されている Web ブラウザーの例を次に示します。

* Google Chrome で、送信されるすべての HTTP リクエストを表示するには、F12 キーを押して、 **[!UICONTROL 開発者ツール]** パネルを開き、 **[!UICONTROL ネットワーク]** タブをクリックします。

   Macで、 **[!UICONTROL Command+Option+I]** 開く **[!UICONTROL 開発者ツール]** パネルをクリックし、「ネットワーク」タブをクリックします。

* Firefox では、F12 キーを押して Firebug プラグインを有効にし、「Net」タブを使用するか、組み込みの **[!UICONTROL 検査官]** ツールとその **[!UICONTROL ネットワーク]** タブをクリックします。

   Macで、 **[!UICONTROL Command+Option+I]** 開く **[!UICONTROL 開発者ツール]** パネルを開き、 **[!UICONTROL 検査官]** タブをクリックします。

ブラウザーでネットワーク監視をオンにして、ページ上でクイックビューをトリガーします。

次に、ネットワークログ内でクイックビューの Ajax URL を見つけ、記録された URL を今後の分析のためにコピーします。クイックビューをトリガーするとほとんどの場合、大量のリクエストがサーバーに送信されます。クイックビューの Ajax URL は通常、そのリスト内の最初のほうにあります。この URL には複雑なクエリ文字列部分またはパスが含まれ、その応答の MIME タイプは `text/html`、`text/xml`、`text/javascript` のいずれかになります。

このプロセスの実行中は、様々な製品カテゴリや製品タイプが含まれる Web サイトの様々な領域にアクセスすることが重要です。なぜなら、クイックビュー URL には、ある特定の Web サイトカテゴリに共通するが、Web サイトの異なる領域にアクセスした場合にのみ変化する部分が存在する場合があるからです。

単純なケースでは、クイックビュー URL 内で変化する唯一の部分が製品 SKU となります。その場合、SKU の値が、ホットスポットをバナー画像に追加するために必要になる唯一のデータです。

一方、複雑なケースでは、クイックビュー URL に SKU 以外の様々な要素が含まれます（カテゴリ ID、カラーコード、サイズコードなど）。その場合、各要素は AEM Assets のショッパブルインタラクティブ画像機能において、ホットスポットデータ定義内の個別の変数になります。

次のクイックビュー URL の例と、その結果となるホットスポットの変数について見てみましょう。

<table> 
     <tbody> 
      <tr> 
       <td><p>単一の SKU（クエリ文字列内）</p> </td> 
       <td><p>記録されたクイックビューの URL：</p> 
        <ul> 
         <li><p><code>https://server/json?productId=866558&amp;source=100</code></p> </li> 
         <li><p><code>https://server/json?productId=1196184&amp;source=100</code></p> </li> 
         <li><p><code>https://server/json?productId=1081492&amp;source=100</code></p> </li> 
         <li><p><code>https://server/json?productId=1898294&amp;source=100</code></p> </li> 
        </ul> <p>この URL で変化する唯一の部分は productId= というクエリ文字列パラメーターの値であり、これが SKU 値であることは明白です。したがって、ホットスポットでは、<strong><code>866558</code></strong>、<strong><code>1196184</code></strong>、<strong><code>1081492</code></strong>、<strong><code>1898294</code></strong> などの値が入力された SKU フィールドのみが必要になります。</p> </td> 
      </tr> 
      <tr> 
       <td><p>単一の SKU（URL パス内）</p> </td> 
       <td><p>記録されたクイックビューの URL：</p> 
        <ul> 
         <li><p><code>https://server/product/6422350843</code></p> </li> 
         <li><p><code>https://server/product/1607745002</code></p> </li> 
         <li><p><code>https://server/product/0086724882</code></p> </li> 
        </ul> <p>パスの最後の要素が変化する部分であり、これがホットスポットの SKU 値（<strong><code>6422350843</code></strong>、<strong><code>1607745002</code></strong>、<strong><code>0086724882</code></strong>）になります。</p> </td> 
      </tr> 
      <tr> 
       <td><p>SKU とカテゴリ ID（クエリ文字列内）</p> </td> 
       <td><p>記録されたクイックビューの URL：</p> 
        <ul> 
         <li><p><code>https://server/quickView/product/?category=1100004&amp;prodId=305466</code></p> </li> 
         <li><p><code>https://server/quickView/product/?category=1100004&amp;prodId=310181</code></p> </li> 
         <li><p><code>https://server/quickView/product/?category=1740148&amp;prodId=308706</code></p> </li> 
        </ul> <p>この場合、URL には変化する部分が 2 つあります。SKU は <code>prodId</code> パラメーターとカテゴリ ID</p><p><code>categoryId</code></p><ul><li><p><code>305466</code><code>categoryId</code><code>1100004</code></p></li><li><p><code>310181</code><code>categoryId</code><code>1100004</code></p></li><li><p><code>308706</code><code>categoryId</code><code>1740148</code></p></li></ul><p></p></td></tr></tbody></table></td></tr><tr></tr></table>

**例**

この 3 つの例で使用されているものと同じアプローチを次のデモ Web ページに適用できます。

[https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-banner/we-fashion/landing-0.html?lang=ja](https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-banner/we-fashion/landing-0.html)

デモ Web ページには複数の製品サムネールがあり、それぞれにクイックビューボタンのラベルが付いています **[!UICONTROL 詳細を見る]**. Web ブラウザーのデバッグツールをアクティブにしたまま各ボタンをクリックし、記録されたクイックビュー URL に注目してください。そのページの 4 つの製品クイックビューのすべてをアクティベートすると、バックエンドに対して次のリストのクイックビューリクエストが作成されます。

* `/datafeed/Men-Windbreaker.json`
* `/datafeed/Men-SimpleHenley.json`
* `/datafeed/Men-CamoPullover.json`
* `/datafeed/Women-QuiltedDownJacket.json`

これらのサーバーコールを見ると、製品固有の情報がリクエストパスのみに含まれることがわかります。また、クエリ文字列がまったく使用されていないこと、2 つの異なるタイプのデータが含まれることもわかります。

* 最初のタイプは Men または Women です。これは「製品カテゴリ」と呼ばれます。
* 2 つ目のタイプは製品名（CamoPullover など）です。これは製品 SKU と考えることができます。

この情報に基づいて、全体的なクイックビュー URL は次のようなパターンであることがわかります。

`/datafeed/$categoryId$-$SKU$.json`

このような分析に基づいて、ホットスポットに対して `categoryId` と `SKU` を使用することになります。

これで、画像バナーをアップロードし、AEM Assets のショッパブルインタラクティブ画像機能を使用して画像バナーにホットスポットを追加する準備ができました。

## （オプション）インタラクティブ画像ビューアプリセットの作成 {#optional-creating-an-interactive-image-viewer-preset}

デフォルトの標準提供インタラクティブ画像ビューアプリセット ( ) であるを使用するように選択できます。 **[!UICONTROL Shoppable_Banner]** それはAEM Assetsに付属しています。 または、インタラクティブ画像で使用するために独自のカスタムビューアプリセットを作成できます。

カスタムインタラクティブ画像ビューアプリセットを作成する場合は、画像バナーのホットスポットの外観を決定できます。ビューアプリセットの作成中に、事前定義済みの画像ギャラリーからホットスポットのグラフィックを選択して使用できます。

ビューアプリセットを保存すると、 **[!UICONTROL ビューアプリセット]** AEM Assetsのリストページ つまり、そのビューアプリセットは、インタラクティブメディアコンポーネントで、アセットを表示するときに常に表示されます。ただし、 *配信* このビューアプリセットを含むインタラクティブバナー *公開* ビューアプリセットも同様に使用できます（これは、カスタムビューアプリセットまたは標準提供ビューアプリセットの場合に当てはまります）。

**インタラクティブ画像ビューアプリセットを作成するには：**:

1. 左側のパネルで、**[!UICONTROL ツール／Assetss／ビューアプリセット]**&#x200B;をタップします。
1. ページの右上隅にある「**[!UICONTROL 作成]**」をタップします。
1. 内 **[!UICONTROL 新しいビューアプリセット]** ダイアログボックスに、インタラクティブバナーのビューアプリセットを説明する名前を入力します。

   これは、 **[!UICONTROL ビューアプリセット]** リストページに表示されます。
1. 内 **[!UICONTROL リッチメディアタイプ]** プルダウンメニューで、「 **[!UICONTROL インタラクティブ画像]**.
1. 「**作成**」をタップします。
1. の **[!UICONTROL ビューアプリセットを編集]** ページで、 **[!UICONTROL 外観]** タブをクリックします。
1. 次のいずれかの操作を行います。

   * 画像で使用する独自のホットスポット画像をアップロードするには、 **[!UICONTROL アセットピッカー]** アイコン内 **[!UICONTROL コンテンツを選択]** ページで、使用するホットスポット画像の場所に移動して選択し、 **[!UICONTROL チェックマーク]** アイコンが表示されます。
   * 定義済みのホットスポット画像を選択するには、 **[!UICONTROL ホットスポットギャラリー]** アイコンホットスポットギャラリーパレットで、使用するホットスポット画像をタップします。

1. ページの右上隅にある「**[!UICONTROL 保存]**」をタップします。

   新しいビューアプリセットを忘れずに公開してください。

   [追加したビューアプリセットの公開](managing-viewer-presets.md#publishing-viewer-presets)を参照してください。

   これで、画像バナーをアップロードできるようになりました。

## 画像バナーのアップロード   {#uploading-an-image-banner}

使用する画像を既にアップロードしている場合は、次の手順（[画像バナーへのホットスポットの追加](#adding-hotspots-to-an-image-banner)）に進んでください。

**画像バナーをアップロードするには：**:

1. インタラクティブにする画像バナーをアップロードします。

   [アセットのアップロード](managing-assets-touch-ui.md#uploading-assets)を参照してください。

   これで、画像バナーにホットスポットを追加する準備が整いました。この後のタスクを参照してください。

## 画像バナーへのホットスポットの追加 {#adding-hotspots-to-an-image-banner}

画像バナーにホットスポットを追加するには、 **[!UICONTROL ホットスポット管理]** ページ。

ホットスポットを追加する際に、クイックビューポップアップ表示、ハイパーリンクまたはエクスペリエンスフラグメントとして定義することができます。

[エクスペリエンスフラグメント](/help/sites-authoring/experience-fragments.md)を参照してください。

>[!NOTE]
>
>ビューアをエクスペリエンスフラグメントに埋め込む場合、インタラクティブ画像のソーシャルメディア共有ツールはサポートされないことに注意してください。この問題を回避するには、ソーシャルメディア共有ツールのないビューアプリセットを使用または作成します。このようなビューアプリセットを使用すると、ビューアをエクスペリエンスフラグメントに正常に埋め込むことができます。

**[!UICONTROL ページの右上隅にある「取り消し」および「やり直し」オプションは、現在の作成／編集セッションの間で有効です。]******

インタラクティブ画像の作成が完了したら、 **[!UICONTROL プレビュー]** を使用して、インタラクティブ画像が顧客にどのように表示されるかを確認できます。

[（オプション）インタラクティブ画像のプレビュー](#optional-previewing-interactive-images)を参照してください。

>[!NOTE]
>
>インタラクティブ画像またはカルーセルバナーの画像にホットスポットを追加すると、インタラクティブ画像かカルーセルバナーかにかかわらず、ホットスポット情報が同じメタデータの場所（画像に対して相対的な場所）に格納されます。つまり、どちらのビューアでも、同じ画像を定義済みのホットスポットデータと一緒に簡単に再利用できます。
>
>ただし、カルーセルバナーでは、画像上の画像マップ（ホットスポットを含むことができる）がサポートされることに注意してください。インタラクティブ画像ではサポートされません。同じ画像を使用するインタラクティブ画像またはカルーセルバナーを作成する場合には、このことに注意してください。同じ画像の別のコピーを使用してインタラクティブ画像とカルーセルバナーを作成することをお勧めします。
>
>[カルーセルバナー](carousel-banners.md)も参照してください。

>[!NOTE]
>
>ホットスポットを含むインタラクティブ画像を編集しているときに、画像を切り取ると、ホットスポットは削除されます。

**画像バナーにホットスポットを追加するには：**：

1. Assets ビューで、インタラクティブにする画像バナーに移動します。
1. 次のいずれかの操作を行います。

   * 画像の上にマウスポインターを置き、**[!UICONTROL 選択]**（チェックマークアイコン）をタップします。ツールバーの「**[!UICONTROL 編集]**」をタップします。
   * 画像の上にマウスポインターを置き、**[!UICONTROL その他のアクション]**（3 つのドットのアイコン）／**[!UICONTROL 編集]**&#x200B;をタップします。
   * 画像をタップして、 **[!UICONTROL 詳細ビュー]** ページ。 ツールバーの「**[!UICONTROL 編集]**」をタップします。

1. ページの左上隅付近にあるをタップします。 **[!UICONTROL ホットスポットを追加]** （指でタップするアイコン） **[!UICONTROL ホットスポット管理]** ページ。
1. ページの左上隅にある「**[!UICONTROL ホットスポット]**」をタップします。
1. a.の左上隅付近 **ホットスポット管理** ページ、タップ **[!UICONTROL ホットスポット]**.
b.画像上で、ホットスポットを表示する場所をタップします。 必要に応じて、ホットスポットをドラッグして場所を調整します。c.必要に応じて、手順 a および b を繰り返して、他のホットスポットを追加します。d.（オプション）ホットスポットを削除するには、画像上でそのホットスポットを選択して、をタップします **[!UICONTROL 削除]** （ごみ箱アイコン）を **[!UICONTROL ホットスポット]** 見出し。

1. 内 **[!UICONTROL 名前]** テキストフィールドに、ホットスポットの名前を入力します。 この名前は、 **[!UICONTROL 選択したホットスポット]** 」ドロップダウンリストから選択できます。
1. 次のいずれかの操作をおこないます。

   * 「**[!UICONTROL クイックビュー]**」をタップします。

      * AEM Sitesまたは e コマースのユーザーである場合は、 **[!UICONTROL 製品ピッカー]** アイコン（虫眼鏡）を使用して **[!UICONTROL 製品を選択]** ページ。 使用する製品をタップし、 **[!UICONTROL 選択]** ページの右上隅に **[!UICONTROL ホットスポット管理]** ページ。
      * AEM Sites または AEM eCommerce *のユーザーではない場合は次のようにします*。

         * [ホットスポットの変数の識別](#optional-identifying-hotspot-variables)を参照してください。これらの変数を定義する必要があります。
         * 次に、SKU 値を手動で入力します。内 **[!UICONTROL SKU 値]** 「 」テキストフィールドに、製品の SKU(Stock Keeping Unit) を入力します。SKU は、提供する個々の製品またはサービスの一意の識別子です。 入力した SKU 値によってクイックビューテンプレートの変数部分が自動的に入力され、タップされたホットスポットが特定の SKU のクイックビューに関連付けられます。
         * （オプション）クイックビュー内で製品をさらに識別するために必要になる他の変数がある場合は、「**[!UICONTROL 汎用変数を追加]**」をタップします。テキストフィールドに追加の変数を指定します。例えば、追加の変数として `category=Mens` などと指定します。
   * 「**ハイパーリンク**」をタップします。

      * AEM Sitesのユーザーである場合は、 **[!UICONTROL サイトセレクター]** アイコン（フォルダー）を使用して URL に移動します。 インタラクティブコンテンツに相対 URL のリンク（特に AEM Sites ページへのリンク）がある場合、URL ベースのリンク方法は使用できません。
      * スタンドアロンのユーザーの場合は、 **[!UICONTROL HREF]** テキストフィールドで、リンクされた Web ページへの完全な URL パスを指定します。

      このリンクを新しいブラウザータブで開く（推奨のデフォルト）か同じタブで開くかを指定してください。

      詳しくは、[セレクターの操作](working-with-selectors.md)を参照してください。

   * 「**エクスペリエンスフラグメント**」をタップします。

      * AEM Sitesのユーザーである場合は、 **[!UICONTROL 検索]** アイコン（虫眼鏡）を使用して **[!UICONTROL エクスペリエンスフラグメント]** ページ。 使用するエクスペリエンスフラグメントをタップし、 **[!UICONTROL 選択]** をクリックして、ホットスポット管理ページに戻ります。

         [エクスペリエンスフラグメント](/help/sites-authoring/experience-fragments.md)を参照してください。
         >[!NOTE]
         >ビューアをエクスペリエンスフラグメントに埋め込む場合、インタラクティブ画像のソーシャルメディア共有ツールはサポートされないことに注意してください。この問題を回避するには、ソーシャルメディア共有ツールのないビューアプリセットを使用または作成します。このようなビューアプリセットを使用すると、ビューアをエクスペリエンスフラグメントに正常に埋め込むことができます。

      * エクスペリエンスフラグメントがバナーに表示されるときの幅と高さを指定します。



1. 「**[!UICONTROL 保存]**」をタップして作業内容を保存し、参照ページに戻ります。****
1. インタラクティブ画像を公開します。公開すると、バナーをクラウドで配信できるようになり、サードパーティの Web サイトに統合する必要がある場合は埋め込みコードが生成されます。

   [アセットの公開](managing-assets-touch-ui.md#publishing-assets)を参照してください。

   ホットスポットを追加してインタラクティブ画像を公開したら、次に既存の Web サイトにその画像を追加できます。

   [インタラクティブ画像の Web サイトへの統合](#integrating-an-interactive-image-with-your-website)を参照してください。

   >[!NOTE]
   >
   >ホットスポットを含むインタラクティブ画像を編集しているときに、画像を切り取ると、ホットスポットは削除されます。

### （オプション）インタラクティブ画像のプレビュー {#optional-previewing-interactive-images}

プレビューを使用して、顧客に対して示されるインタラクティブ画像の表示方法を確認し、画像のホットスポットをテストして動作が期待どおりであるかを確認することができます。

インタラクティブ画像の設定が完了したら、この画像を公開できます。\
[Web ページへのビデオビューアまたは画像ビューアの埋め込み](embed-code.md)を参照してください。\
[Web アプリケーションへの URL のリンク](linking-urls-to-yourwebapplication.md)を参照してください。インタラクティブコンテンツに相対 URL のリンク（特に AEM Sites ページへのリンク）がある場合、URL ベースのリンク方法は使用できません。\
[ページへの Dynamic Media アセットの追加](adding-dynamic-media-assets-to-pages.md)を参照してください。

**インタラクティブ画像をプレビューするには：**:

1. Assets ビューで、作成した既存のインタラクティブ画像の場所に移動し、タップしてプレビューで表示します。
1. プレビューページの左上隅付近にある **[!UICONTROL コンテンツ]** ドロップダウンリストから、 **[!UICONTROL ビューア]**.
1. 内 **[!UICONTROL ビューア]** リスト、タップ **[!UICONTROL Shoppable_Banner]** または作成したインタラクティブ画像ビューアプリセットの名前。
1. 画像上のホットスポットをタップし、関連付けられたアクションをテストします。

## インタラクティブ画像アセットの公開 {#publishing-interactive-image-assets}

インタラクティブ画像アセットの公開方法について詳しくは、[アセットの公開](publishing-dynamicmedia-assets.md)を参照してください。

## インタラクティブ画像の Web サイトへの統合 {#integrating-an-interactive-image-with-your-website}

バナー画像をアップロードし、ホットスポットを画像に追加してインタラクティブ画像を公開したら、次に Web サイトページにその画像を追加できます。

AEM Sites のユーザーである場合は、インタラクティブメディアコンポーネントをページにドラッグすることによりインタラクティブ画像を追加できます。[ページへの Dynamic Media アセットの追加](adding-dynamic-media-assets-to-pages.md)を参照してください。

スタンドアロン AEM Assets のユーザーである場合は、この節で説明するようにインタラクティブ画像を手動で Web サイトに追加できます。

1. 公開済みのインタラクティブ画像の埋め込みコードをコピーします。

   [Web ページへのビデオビューアまたは画像ビューアの埋め込み](embed-code.md)を参照してください。

1. コピーした埋め込みコードを、Web ページ内の必要な場所に追加します。

   コピーされた埋め込みコードはレスポンシブ環境向けに設定されているので、追加された場所に自動的に適応します。

**例**

次のデモ Web サイトを例として使用します。

[https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-banner/we-fashion/landing-0.html?lang=ja](https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-banner/we-fashion/landing-0.html)

3 人の男性の写真には次のような静的 `IMG` タグが使用されています。

```xml
<img class="img-responsive" width="100%" title="Hero Image 2" alt="Hero Image 2" src="images/shoppable-banner.jpg">
```

統合は、`IMG` タグを削除して AEM Assets からコピーした埋め込みコードに置き換えるだけで簡単にできます。次の URL で結果を確認できます。これは、3 つの円のホットスポットを含むページ上でショッパブルインタラクティブ画像を表示します。

[https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-banner/we-fashion/landing-1.html?lang=ja](https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-banner/we-fashion/landing-1.html?lang=ja)

>[!NOTE]
>
>この時点では、デモ Web サイトのショッパブルインタラクティブ画像上のホットスポットは表示用のみで、まだ既存のクイックビューと統合されていません。

レスポンシブ環境用のショッパブルインタラクティブ画像に切り抜きを適用するには、インタラクティブ画像設定属性を含めます `ZoomView.iscommand` 道へ `ZoomView` は呼び出すコンポーネントで、は `iscommand` は、適用する crop 画像サービングコマンドです。

[ZoomView.iscommand](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/command-reference-configuration-attributes-interactive-images/r-html5-aem-interactive-image-config-attrib-zoomview-iscommand.html?lang=ja) 設定属性を参照してください。

[crop](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-crop.html?lang=ja) 画像サービングコマンドを参照してください。

これで、インタラクティブ画像を Web サイト上の既存のクイックビューに統合できるようになりました。

## インタラクティブ画像の既存のクイックビューへの統合 {#integrating-an-interactive-image-with-an-existing-quickview}

>[!NOTE]
>
>このタスクはスタンドアロン AEM Assets のユーザーのみに適用されます。

このプロセスの最後の手順は、インタラクティブ画像を Web サイトの既存のクイックビュー実装に統合することです。すべてのケースで機能する統合のソリューションはありません。すべてのクイックビュー実装は固有であり、フロントエンド IT 担当者の支援を受けた特別なアプローチが必要になります。

既存のクイックビュー実装は一般的に、Web ページ上で以下の順に発生する、相互に関連するアクションの連鎖となっています。

1. ユーザーは、Web サイトのユーザーインターフェイス内で、特定の要素を起動します。
1. フロントエンドコードは、手順 1 で起動されたユーザーインターフェイス要素に基づいてクイックビュー URL を取得します。
1. フロントエンドコードは、手順 2 で取得した URL を使用して Ajax リクエストを送信します。
1. バックエンドロジックは、対応するクイックビューのデータまたはコンテンツをフロントコードに送り返します。
1. フロントエンドコードは、そのクイックビューのデータまたはコンテンツを読み込みます。
1. （オプション）フロントエンドコードは、読み込んだクイックビューのデータを HTML 表現に変換します。
1. フロントエンドコードは、モーダルダイアログボックスまたはパネルを表示し、エンドユーザー向けに、画面上に HTML コンテンツをレンダリングします。

これらの呼び出しは、必ずしもそれぞれ独立した、Web ページのロジックから任意の手順で呼び出すことができるパブリックな API 呼び出しを表すわけではありません。むしろ、次の手順が前の手順の最後のフェーズ（コールバック）に隠されているような連鎖的な呼び出しになっています。

ショッパブルインタラクティブ画像が手順 1 と（部分的に）手順 2 を置き換えるのと同時に、ユーザーがショッパブル画像内のホットスポットをクリックしたときに、そのユーザー操作がビューアによって処理されます。ビューアは、AEM Assets に以前に追加されたすべてのホットスポットデータを含む Web ページに、イベントを返します。

そのようなイベントハンドラーでは、フロントエンドコードは次の処理を実行します。

* ショッパブルインタラクティブ画像から送出されるイベントをリッスンします。
* ホットスポットデータに基づいてクイックビュー URL を作成します。
* バックエンドからクイックビューを読み込み、画面上の表示用にレンダリングするプロセスを起動します。

AEM Assets によって返される埋め込みコードには、次のハイライトされたコードのように、既にすぐに使用可能なイベントハンドラーがコメントアウトされた状態で含まれています。

```xml
        var s7interactiveimageviewer = new s7viewers.InteractiveImage({
            "containerId" : "s7interactiveimage_div",
            "params" : { 
                "serverurl" : "https://aodmarketingna.assetsadobe.com/is/image",
                "contenturl" : "https://aodmarketingna.assetsadobe.com/", 
                "config" : "/etc/dam/presets/viewer/Shoppable_Media",
                "asset" : "/content/dam/mac/aodmarketingna/shoppable-banner/shoppable-banner.jpg" }
        })
        /* // Example of interactive image event for Quickview.
             s7interactiveimageviewer.setHandlers({ 
                "quickViewActivate": function(inData) {
                    var sku=inData.sku; //SKU for product ID
                    //To pass other parameter from the hotspot, you will need to add custom parameter during the hotspot setup as parameterName=value
                    loadQuickView(sku); //Replace this call with your Quickview plugin
                    //Please refer to your Quickviewer plugin for the Quickview call
                 }, 
             });
        */
        s7interactiveimageviewer.init();
```

そのため、必要な処理は、このコードのコメントアウトを解除し、ダミーのハンドラー本体を、特定の Web ページ専用のコードに置き換えることだけです。

クイックビュー URL の作成プロセスは、基本的に先ほど説明したホットスポットの変数を識別するためのプロセスとは逆のプロセスになります。

[ホットスポットの変数の識別](#optional-identifying-hotspot-variables)を参照してください。

以前のクイックビュー URL の例を使用した場合、クイックビュー URL の各ケースでの作成方法は次の例のようになります。

<table> 
 <tbody> 
  <tr> 
   <td><p>単一の SKU（クエリ文字列内）</p> </td> 
   <td><code class="code">s7interactiveimageviewer.setHandlers({
      "quickViewActivate": function(inData) {
      var quickViewUrl = "https://server/json?productId=" + inData.sku + "&amp;amp;source=100";
      },
      });</code></td> 
  </tr> 
  <tr> 
   <td><p>単一の SKU（URL パス内）</p> </td> 
   <td><code class="code">s7interactiveimageviewer.setHandlers({
      "quickViewActivate": function(inData) {
      var quickViewUrl = "https://server/product/" + inData.sku;
      },
      });</code></td> 
  </tr> 
  <tr> 
   <td><p>SKU とカテゴリ ID（クエリ文字列内）</p> </td> 
   <td><code class="code">s7interactiveimageviewer.setHandlers({
      "quickViewActivate": function(inData) {
      var quickViewUrl = "https://server/quickView/product/?category=" + inData.categoryId + "&amp;amp;prodId=" + inData.sku;
      },
      });</code></td> 
  </tr> 
 </tbody> 
</table>

クイックビュー URL をトリガーしてクイックビューパネルをアクティベートするための最後の手順では、おそらく IT 部門のフロントエンド IT 担当者の支援が必要になります。フロントエンド IT 担当者は、すぐに使用できるクイックビュー URL を含め、クイックビュー実装を適切な手順から正しくトリガーするための最適な方法について理解しています。

これらの手順をデモ Web サイトに適用してショッパブルインタラクティブ画像をクイックビューのコードに統合する方法を確認できます。先ほど、クイックビュー URL の構造を次のように識別しました。

```xml
/datafeed/$categoryId$-$SKU$.json
```

この URL を `quickViewActivate` ハンドラー内で再構成するために、ビューアのコードからハンドラーに渡される `inData` オブジェクト内の `categoryId` フィールドと `SKU` フィールドを使用できます。

```xml
var sku=inData.sku;
var categoryId=inData.categoryId;
var quickViewUrl = "datafeed/" + categoryId + "-" + sku + ".json";
```

このデモ Web サイトは、単純な `loadQuickView()` 関数呼び出しを使用してクイックビューダイアログボックスを起動しています。この関数は、1 つの引数（クイックビューデータの URL）のみを受け取ります。したがって、ショッパブルインタラクティブ画像を統合するために必要な最後の手順は、`quickViewActivate` ハンドラーに次のコード行を追加することです。

```xml
loadQuickView(quickViewUrl);
```

次に、ソースコード全体を示します。

```xml
 var s7interactiveimageviewer = new s7viewers.InteractiveImage({
  "containerId" : "s7interactiveimage_div",
  "params" : { 
   "serverurl" : "https://aodmarketingna.assetsadobe.com/is/image",
   "contenturl" : "https://aodmarketingna.assetsadobe.com/", 
   "config" : "/etc/dam/presets/viewer/Shoppable_Media",
   "asset" : "/content/dam/mac/aodmarketingna/shoppable-banner/shoppable-banner.jpg" }
 })
   s7interactiveimageviewer.setHandlers({ 
   "quickViewActivate": function(inData) {
     var sku=inData.sku;
     var categoryId=inData.categoryId;
    var quickViewUrl = "datafeed/" + categoryId + "-" + sku + ".json";
    loadQuickView(quickViewUrl);
    }, 
   });
 s7interactiveimageviewer.init();
```

インタラクティブ画像が完全に統合された最終的なデモ Web サイトは次のようになります。

[https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-banner/we-fashion/landing-3.html?lang=ja](https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-banner/we-fashion/landing-3.html?lang=ja)

## クイックビューを使用したカスタムポップアップの作成 {#using-quickviews-to-create-custom-pop-ups}

詳しくは、 [クイックビューを使用したカスタムポップアップの作成](custom-pop-ups.md).
