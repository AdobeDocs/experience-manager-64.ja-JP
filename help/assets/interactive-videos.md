---
title: インタラクティブビデオ
seo-title: Interactive Videos
description: Dynamic Media でのインタラクティブビデオの操作方法を説明します。
seo-description: Learn how to work with interactive video in dynamic media
uuid: 5de8844f-d5d0-4fda-b59e-74682eda949f
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.4/ASSETS
discoiquuid: 2f254541-6f9b-4f8a-9201-6c70f2d4f3b9
exl-id: 3adae6da-e148-4670-86ae-27d83008ec66
feature: Interactive Videos,Video
role: User
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '6008'
ht-degree: 76%

---

# インタラクティブビデオ {#interactive-videos}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

ビデオから直接変換を促すインタラクティブビデオを簡単に作成できます。 ビデオに対する顧客エンゲージメントは、ビデオプレーヤーの隣のパネルで行われ、関連するサービス、情報または製品のサムネールが、ビデオの特集に基づいてスクロール表示されます。顧客はサムネールをタップして、サービスを直接参照したり、買い物かごに商品を追加して即時に購入したり、Web ページを参照して詳細を確認したりできます。

ビデオが終了すると、コールトゥアクション（CTA）を促すために、画像を使用して、すべてのサービスの概要が表示されます。顧客は、ここで欲しい商品をタップすることもできます。このような実用的で具体的なエクスペリエンスにより、顧客エンゲージメントとコンバージョンが向上します。

[インタラクティブ画像](interactive-images.md) も参照してください。

## 実際のインタラクティブビデオ {#interactive-video-in-action}

インタラクティブでショッパブルなビデオを実際に表示するには、 [ライブデモ](https://landing.adobe.com/en/na/dynamic-media/ctir-2755/live-demos.html)、にスクロールします。 **[!UICONTROL ショッパブルメディア]** 」見出しをクリックし、ショッパブルビデオをクリックします。

* 再生中にビデオ内で製品が使用されると、同じ製品のサムネール画像が右側に表示されます。

* ビデオを一時停止し、製品のクイックビューを開く場合は、サムネールをクリックします。 例えば、ビデオ内の KitchenAid のサムネール画像をクリックすると、このミキサーの 360 度のスピンビューを見たり、細部を拡大表示したりすることができます。

<!-- There was a link here that showed the video frame of an interactive video and when the reader clicked the frame the video would play https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-video/AXIS/index.html. This now needs to call a new interactive video-->

![インタラクティブなショッパブルビデオのフレーム](assets/chlimage_1-126.png) *インタラクティブなショッパブルビデオからのビデオフレームキャプチャ。*

>[!NOTE]
>
>ユーザーがサムネール画像をクリックしたときに Web ページを起動するインタラクティブビデオを作成した場合、一部のデバイスでは、ポップアップ Web ページがブロックされて開きません。 そのようなケースでは、デバイスのポップアップブロック機能の設定を変更する必要があります。例えば、Apple iPhone 6 で、 **[!UICONTROL 設定]** > **Safari** > **ポップアップのブロック**&#x200B;をクリックし、次の場所にコントロールをスライドさせます。 **[!UICONTROL オフ]**. これで、インタラクティブビデオを再生してサムネールをクリックすると、ポップアップを開くかどうかを尋ねるプロンプトが表示されます。 同意すると Web ページが開きます。

## インタラクティブビデオの作成方法を見る {#watch-how-interactive-videos-are-created}

のウォークスルーを再生する [インタラクティブビデオの作成方法](https://s7d5.scene7.com/s7viewers/html5/VideoViewer.html?videoserverurl=https://s7d5.scene7.com/is/content/&amp;emailurl=https://s7d5.scene7.com/s7/emailFriend&amp;serverUrl=https://s7d5.scene7.com/is/image/&amp;config=Scene7SharedAssets/Universal_HTML5_Video_social&amp;contenturl=https://s7d5.scene7.com/skins/&amp;asset=S7tutorials/InteractiveVideo) [](https://outv.omniture.com?v=s4NHQ2dzqd7hIqWjeG2sIdyNWsTWyupA). （7 分 30 秒）このビデオガイドの対象は Assets on Demand ですが、原則や手順はAdobe Experience Manager Assets のインタラクティブビデオにも対応しています。

## アドビカスタマーサクセスウェビナー {#adobe-customer-success-webinar}

「Experience Manager Assets でのインタラクティブビデオの使用、リンク共有および YouTube での共有」ウェビナーでは、インタラクティブビデオなどの機能を使用して、コンバージョン誘導イベントをビデオマーケティングコンテンツと連動させる方法を解説しています。

>[!NOTE]
[Experience Manager Assets でのインタラクティブビデオ、リンク共有、YouTube 共有の使用](https://adobecustomersuccess.adobeconnect.com/p1yxzdo4aec/)。

## クイックスタート：インタラクティブビデオ {#quick-start-interactive-videos}

次の詳しいワークフローの説明は、Dynamic Media でインタラクティブビデオをすぐに開始することを目的としたものです。

一部のクイックスタートタスク内には「**例**」という見出しがあります。これには、まだインタラクティブ機能が追加&#x200B;*されていない*&#x200B;最初のデモ web ページに基づいた、簡単なチュートリアルが含まれています。

[https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-video/john-lewis/landing-0.html?lang=ja](https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-video/john-lewis/landing-0.html?lang=ja)

「**例**」では、Web サイトにインタラクティブビデオを統合する手順が説明されています。

最後の「例」セクションでチュートリアルを終えると、完全に統合されたインタラクティブビデオを含む最終的なデモ web ページの表示は次のようになります。

[https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-video/john-lewis/landing-3.html?lang=ja](https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-video/john-lewis/landing-3.html?lang=ja)

**インタラクティブビデオのワークフロー：**

1. **（オプション）クイックビュー変数の識別**  — 最初に、既存のクイックビュー実装で使用される動的変数を識別します。 これらの変数を使用して、インタラクティブビデオを作成するときに、製品のサムネールを対応する製品のクイックビューにマッピングします。詳しくは、 [（オプション）クイックビュー変数の識別](#optional-identifying-quickview-variables).

   *このタスクが必要になるのは、以下のすべてに該当する場合のみです*。

   * クイックビューをトリガーして、ビデオにインタラクティビティを追加する。
   * e コマースソリューション（IBM WebSphere® Commerce、Elastic Path、hybris、Intershop など）から Adobe Experience Manager に製品データを取り出すために、Adobe Experience Manager の実装が e コマース統合フレームワークを使用して&#x200B;*いない*。[Experience Manager Assetsの e コマースの概念](/help/sites-administering/concepts.md)を参照してください。

1. **（オプション）インタラクティブビデオのビューアプリセットの作成** - プレーヤーを構成する様々なコンポーネント（ビデオスクラバーやインタラクティブサムネールなど）の外観と動作をカスタマイズします。

   独自のインタラクティブビデオビューアプリセットの作成は、標準提供のインタラクティブビデオビューアプリセット（`Shoppable_Video_Light` または `Shoppable_Video_Dark`）を使用する場合には必要ありません。[新しいビューアプリセットの作成](managing-viewer-presets.md#creating-a-new-viewer-preset)（オプション）と[インタラクティブビューアプリセットの作成に関する注意事項](managing-viewer-presets.md#special-considerations-for-creating-an-interactive-viewer-preset)を参照してください。

1. **ビデオおよび関連する画像アセットのアップロード** - インタラクティブにするビデオと関連する画像をアップロードします。

   [ビデオおよび関連するサムネールアセットのアップロード](#uploading-a-video-and-its-associated-thumbnail-assets)を参照してください。

1. **ビデオへのインタラクティビティの追加** - 1 つ以上の時間セグメントをビデオに追加します。 次に、それらの時間セグメント内で画像サムネールを関連付けます。各画像サムネールを、ハイパーリンク、クイックビュー、エクスペリエンスフラグメントなどのアクションに割り当てます

   （インタラクティブコンテンツに相対 URL のリンク（特に Adobe Experience Manager Sites ページへのリンク）がある場合、URL ベースのリンク方法は使用できません）。

   インタラクティブビデオアセットを公開して作業は完了です。公開によって埋め込みコードまたは URL が生成されます。最終的には、このコードまたは URL をコピーして、Web サイトのランディングページに適用します。[ビデオへのインタラクティビティの追加](#adding-interactivity-to-your-video)を参照してください。

   [アセットの公開](publishing-dynamicmedia-assets.md)を参照してください。

1. **Web サイトまたは Web サイトへのインタラクティブビデオのExperience Manager**

   Experience Manager Sites、Experience Managerー e コマース、またはその両方を使用する場合は、インタラクティブメディアコンポーネントをページにドラッグすることで、Experience Managerで Web ページにインタラクティブビデオを直接追加できます。 [ページへの Dynamic Media アセットの追加](adding-dynamic-media-assets-to-pages.md)を参照してください。

   埋め込みコードまたは URL を使用して、インタラクティブビデオを Web サイトエクスペリエンスに統合します。[インタラクティブビデオの Web サイトへの統合](#integrating-an-interactive-video-with-your-website)を参照してください。

   サードパーティの WCM（Web Content Manager）を使用している場合は、新しいインタラクティブビデオを、Web サイトで使用されている既存のクイックビュー実装に統合する必要があります。[インタラクティブビデオの既存のクイックビューへの統合](#integrating-an-interactive-video-with-an-existing-quickview)を参照してください。

## （オプション）クイックビュー変数の特定  {#optional-identifying-quickview-variables}

>[!NOTE]
このタスクが必要になるのは次に該当する場合のみです。
* クイックビューをトリガーして、ビデオにインタラクティビティを追加する。
* e コマースソリューション（IBM WebSphere® Commerce、Elastic Path、hybris、Intershop など）から Adobe Experience Manager に製品データを取り出すために、Adobe Experience Manager の実装が e コマース統合フレームワークを使用して&#x200B;*いない*。[Experience Manager Assetsの e コマースの概念](/help/sites-administering/concepts.md)を参照してください。
>
Experience Manager の実装で eCommerce を使用している場合は、このタスクをスキップして次のタスクに進みます。

最初に、インタラクティブビデオの作成プロセス中に製品サムネールを対応する製品クイックビューにマッピングできるように、既存のクイックビューの実装で使用している動的変数を特定します。

ビデオに時間セグメントを追加する際に、セグメントに追加する各サムネールに SKU（Stock Keeping Unit）と任意の追加の変数を割り当てます。こうした変数は、適切な製品クイックビューを表示するために後で使用されます。

製品クイックビューを一意にトリガーするために必要な変数を適切に特定することが重要です。

既存のクイックビューの実装を担当する IT 担当者に相談するだけで十分な場合があります。 システム内のクイックビューを識別するために必要な最小データセットを把握している可能性が高くなります。 ただし、フロントエンドコードの既存の動作を分析するだけでもかまいません。

ほとんどのクイックビュー実装では、次のような枠組みが使用されています。

* ユーザーは Web サイト上の特定のユーザーインターフェイス要素をアクティベートします。例えば、 **[!UICONTROL クイックビュー]** 」ボタンをクリックします。
* Web サイトでは、必要に応じて、クイックビューのデータまたはコンテンツを読み込むための Ajax リクエストをバックエンドに送信します。
* クイックビューのデータは、Web ページでのレンダリングに備えて、コンテンツに変換されます。
* 最後に、フロントエンドコードによってそのコンテンツが画面上に視覚的にレンダリングされます。

そのため、このアプローチでは、クイックビューが実装されている既存の Web サイトの様々な部分にアクセスし、クイックビューをトリガーして、クイックビューのデータまたはコンテンツを読み込むために Web ページから送信された Ajax URL をキャプチャします。

通常は、特別なデバッグツールを使用する必要はありません。最新の Web ブラウザーには、十分なタスクを実行できる Web インスペクターが備わっています。Web インスペクターが搭載されている Web ブラウザーの例を次に示します。

* Google Chrome で、送信されるすべての HTTP リクエストを表示するには、キーボードショートカットを使用します `F12` (Windows) または `Command + Options + I` (Mac) **[!UICONTROL 開発者ツール]** パネルを開き、 **[!UICONTROL ネットワーク]** タブをクリックします。

* Mozilla Firefox では、キーボードショートカットを使用して Firebug プラグインをアクティベートできます `F12` (Windows) または `Command + Options + I` (Mac) **[!UICONTROL ネット]** 」タブをクリックするか、組み込みのインスペクターツールとその「ネットワーク」タブを使用できます。

* Internet Explorer では、`F12` キーを押してデバッガーツールを起動します。

ブラウザーでネットワーク監視をオンにして、ページ上でクイックビューをトリガーします。

次に、ネットワークログ内でクイックビューの Ajax URL を見つけ、記録された URL を今後の分析のためにコピーします。通常、クイックビューをトリガーすると、多数のリクエストがサーバーに送信されます。クイックビューの Ajax URL は通常、そのリスト内の最初のほうにあります。この URL には複雑なクエリ文字列部分またはパスが含まれ、その応答の MIME タイプは `text/html`、`text/xml`、`text/javascript` のいずれかになります。

このプロセスの実行中は、製品カテゴリや製品タイプが異なる、Web サイトの様々な領域にアクセスすることが重要です。なぜなら、クイックビュー URL には、ある特定の Web サイトカテゴリに共通するが、Web サイトの異なる領域にアクセスした場合にのみ変化する部分が存在する場合があるからです。

単純なケースでは、クイックビュー URL 内で変化する唯一の部分が製品 SKU となります。この場合、Adobe Experience Manager でサムネールをインタラクティブビデオの時間セグメントに追加するのに必要なデータは製品の SKU 値のみです。

ただし、複雑なケースでは、クイックビュー URL に製品 SKU 以外の様々な要素が含まれます（カテゴリ ID やカラーコードなど）。 その場合は、それぞれの要素が Adobe Experience Manager のサムネールデータ定義で個別の変数になります。

次のクイックビュー URL と、その結果のサムネイルの変数の例を考えてみます。

<table> 
     <tbody> 
      <tr> 
       <td><p>単一の SKU（クエリ文字列内）</p> </td> 
       <td><p>記録されたクイックビューの URLとしては以下が挙げられます。</p> 
        <ul> 
         <li><p><code>https://server/json?productId=866558&amp;source=100</code></p> </li> 
         <li><p><code>https://server/json?productId=1196184&amp;source=100</code></p> </li> 
         <li><p><code>https://server/json?productId=1081492&amp;source=100</code></p> </li> 
         <li><p><code>https://server/json?productId=1898294&amp;source=100</code></p> </li> 
        </ul> <p>この URL で変化する唯一の部分は <code>productId=</code> というクエリ文字列パラメーターの値であり、これが SKU 値であることは明白です。したがって、サムネールでは、<strong><code>866558</code></strong>、<strong><code>1196184</code></strong>、<strong><code>1081492</code></strong>、<strong><code>1898294</code></strong> などの値が設定された SKU フィールドのみが必要になります。</p> </td> 
      </tr> 
      <tr> 
       <td><p>単一の SKU（URL パス内）</p> </td> 
       <td><p>記録されたクイックビューの URLとしては以下が挙げられます。</p> 
        <ul> 
         <li><p><code>https://server/product/6422350843</code></p> </li> 
         <li><p><code>https://server/product/1607745002</code></p> </li> 
         <li><p><code>https://server/product/0086724882</code></p> </li> 
        </ul> <p>パスの最後の要素が変化する部分であり、これが Adobe Experience Manager サムネールの SKU 値（<strong><code>6422350843</code></strong>、<strong><code>1607745002</code></strong>、<strong><code>0086724882</code></strong>）になります。</p> </td> 
      </tr> 
      <tr> 
       <td><p>SKU とカテゴリ ID（クエリ文字列内）</p> </td> 
       <td><p>記録されたクイックビューの URLとしては以下が挙げられます。</p> 
        <ul> 
         <li><p><code>https://server/quickView/product/?category=1100004&amp;prodId=305466</code></p> </li> 
         <li><p><code>https://server/quickView/product/?category=1100004&amp;prodId=310181</code></p> </li> 
         <li><p><code>https://server/quickView/product/?category=1740148&amp;prodId=308706</code></p> </li> 
        </ul> <p>この場合、URL には変化する部分が 2 つあります。SKU が <code>prodId</code> パラメーターに、カテゴリ ID が <code>category=</code> パラメーターに格納されています。</p> <p>そのため、サムネール定義はペアになります。つまり、SKU 値と、<code>categoryId</code> という追加の変数です。結果のペアは次のようになります。</p> 
        <ul> 
         <li>SKU が <code>305466</code>、<code>categoryId</code> が <code>1100004</code></li> 
         <li>SKU が <code>310181</code>、<code>categoryId</code> が <code>1100004</code></li> 
         <li>SKU が <code>308706</code>、<code>categoryId</code> が <code>1740148</code></li> 
        </ul> <p> </p> </td> 
      </tr> 
     </tbody> 
    </table> </td> 
  </tr> 
  <tr>
</table>

**例**

上記の方法を例の Web サイトに適用すると、いくつかの製品サムネールを含む Web ページが作成され、それぞれに **[!UICONTROL 詳細を見る]** ボタン：

[https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-video/john-lewis/landing-0.html?lang=ja](https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-video/john-lewis/landing-0.html?lang=ja)

ページで使用可能なすべての製品クイックビューをアクティベートした後、バックエンドに対しておこなわれたクイックビューリクエストの次のリストが取得されます。

* datafeed/candles-233396346.json
* datafeed/candles-233978050.json
* datafeed/candles-234024346.json
* datafeed/candles-234024356.json
* datafeed/candles-234024359.json
* datafeed/cushions-233939848.json
* datafeed/cushions-234019477.json
* datafeed/cushions-234019483.json
* datafeed/furniture-231747479.json
* datafeed/furniture-232625621.json
* datafeed/furniture-232625626.json
* datafeed/furniture-233939810.json
* datafeed/furniture-233939825.json
* datafeed/furniture-233939828.json
* datafeed/furniture-233939853.json
* datafeed/furniture-233940334.json
* datafeed/glassware-000064007.json
* datafeed/glassware-230722193.json
* datafeed/glassware-233916550.json
* datafeed/glassware-233916597.json

これらのサーバーコールを見ると、製品固有の情報はリクエストパスにしか存在しないことがわかります。また、クエリ文字列がまったく使用されていないことと、2 つの異なるタイプのデータが含まれることもわかります。

* 1 つ目のタイプはキャンドル、クッション、家具、ガラス製品です。これは「製品カテゴリ」と呼ばれます。
* 2 つ目のタイプは製品コード（233916597 など）です。これは「製品 SKU」と見なすことができます。

この情報に基づいて、全体的なクイックビュー URL は次のようなパターンであることがわかります。

`/datafeed/$categoryId$-$SKU$.json`

こうした分析に基づいて、サムネールには `categoryId` と `SKU` の 2 つの変数を使用できるという結論が得られます。

これで、ビデオおよび関連するサムネールアセットをアップロードできます。

## （オプション）インタラクティブビデオのビューアプリセットの作成 {#optional-creating-an-interactive-video-viewer-preset}

標準提供のインタラクティブビデオビューアプリセットタイプ ( `Shoppable_Video_dark` または `Shoppable_Video_light`.

オーサリング環境でサムネールをクリックすると、 **[!UICONTROL クイックビュー]** ダイアログボックスが表示されます。

![chlimage_1-127](assets/chlimage_1-127.png)

オプションで、独自のカスタムインタラクティブビデオのビューアプリセットを作成できます。 特に、ビデオプレーヤーのスタイル、インタラクティブサムネイル、ビデオの最後に表示されるサムネイルのグリッド表示を指定できます。

インタラクティブビデオのビューアプリセットは、ビデオと追加したすべてのタイムラインセグメントを適切にレンダリングします。また、で製品のサムネールをクリックしたときに、デフォルトのクイックビューの例も使用されます。 **[!UICONTROL プレビュー]** モードを使用して、公開前にインタラクティビティをテストできます。

ビューアプリセットを保存すると、ビューアプリセットページでそのプリセットのステータスが自動的に&#x200B;**[!UICONTROL オン]**&#x200B;に設定されます。このステータスは、そのプリセットが Dynamic Media コンポーネントに表示され、ビデオのプレビュー時に必ず使用されることを意味します。****&#x200B;また、新しいビューアプリセットも忘れずに手動で公開してください。

[新しいビューアプリセットの作成](managing-viewer-presets.md#creating-a-new-viewer-preset)を参照して、独自のインタラクティブビデオのビューアプリセットを作成します。

## ビデオおよび関連するサムネールアセットのアップロード {#uploading-a-video-and-its-associated-thumbnail-assets}

ビデオとサムネールアセットを既にアップロードしている場合は、[ビデオへのインタラクティブ機能の追加](#adding-interactivity-to-your-video)に進んでください。

間違ったビデオや画像をアップロードした場合、またはアップロードしたビデオや不要になった画像を削除する場合は、「 [アセットの削除](managing-assets-touch-ui.md#deleting-assets).

**ビデオおよび関連するサムネイルアセットのアップロード**

1. ビデオおよび関連するサムネイルのアセットを、目的のフォルダー（1 つまたは複数）にアップロードします。

   [アセットのアップロード](managing-assets-touch-ui.md)を参照してください。

   詳しくは、 [FTP ジョブスケジューリングを使用したアセットのアップロード](managing-assets-touch-ui.md).

   これで、ビデオにインタラクティブ機能を追加できます。

## ビデオへのインタラクティブ機能の追加 {#adding-interactivity-to-your-video}

「インタラクティブビデオを作成」ページのインプレースビジュアルエディターを使用して、ビデオにタイムラインセグメントを追加します。

タイムラインセグメントを追加した後、各セグメント内にサムネイル画像を追加します。 追加したサムネイルごとに、アクションを適用します。例えば、サムネイルにクイックビューを適用したり、サムネイルにハイパーリンクやエクスペリエンスフラグメントを割り当てたりすることができます。

[エクスペリエンスフラグメント](/help/sites-authoring/experience-fragments.md)を参照してください。

>[!NOTE]
インタラクティブコンテンツに相対 URL のリンク（特に Experience Manager Sites ページへのリンク）がある場合、URL ベースのリンク方法は使用できません。

**[!UICONTROL ページの右上隅にある「取り消し」および「やり直し」オプションは、現在の作成／編集セッションの間で有効です。]******

インタラクティブビデオを保存すると、ビデオがすぐにプレビューで開きます。そこから、インタラクティブビデオのビューアプリセットを選択し、ビデオを再生して、顧客にどのように表示されるかを大まかに確認できます。

**ビデオにインタラクティブ機能を追加するには：**

1. Assets ビューで、インタラクティブにするアップロード済みのビデオに移動します。
1. 次のいずれかの操作を行います。

   * 画像の上にマウスポインターを置き、**[!UICONTROL 選択]**（チェックマークアイコン）をタップします。ツールバーの「**[!UICONTROL 編集]**」をタップします。
   * 画像の上にマウスポインターを置いて、をタップします。 **[!UICONTROL その他のアクション]** （3 つのドットのアイコン） > **[!UICONTROL 編集]**.
   * 画像をタップして、詳細ビューページで開くことができます。 ツールバーの「**[!UICONTROL 編集]**」をタップします。

1. の **[!UICONTROL インタラクティブビデオを作成]** ページで、次のいずれかの操作をおこないます。

   * 次をタップします。 **[!UICONTROL 再生]** ボタンをクリックして、ビデオを再生できます。 取り上げたい特定の製品、サービスまたは詳細が表示されたら、ツールバーの「**[!UICONTROL セグメントを追加]**」をタップします。ビデオの最後に達するまで繰り返します。

      追加した各時間セグメントに 1 つまたは複数のサムネール画像を割り当て、それらのサムネールにリンクを設定し、顧客が購入するためのクイックビュー製品ページや詳細情報のための web ページにアクセスできるようにします。

   * 次をタップします。 **[!UICONTROL 再生]** ボタンをクリックして、ビデオを再生できます。 取り上げたい特定の製品、サービスまたは詳細が表示されたら、「**[!UICONTROL 一時停止]**」をタップします。「**[!UICONTROL セグメントを追加]**」をタップします。

      ビデオの最後に達するまで、セグメントを追加するタイムラインのポイントで、ビデオの再生と停止を続けます。

1. （オプション）**[!UICONTROL タイムラインスケールスライダー]**&#x200B;のバーを左にドラッグしてズームインするか、右にドラッグしてズームアウトします。この方法で、追加したセグメントの表示レベルを制御できます。

   ![chlimage_1-128](assets/chlimage_1-128.png)

   ビデオの長さに応じて、 **[!UICONTROL セグメントの期間]** デフォルト値は次のとおりです。

   <table> 
    <tbody> 
      <tr> 
      <td><strong>ビデオの長さ</strong></td> 
      <td><strong>「セグメントの期間」のデフォルト値</strong></td> 
      </tr> 
      <tr> 
      <td>3 分以上</td> 
      <td>60 秒</td> 
      </tr> 
      <tr> 
      <td>2～3 分</td> 
      <td>30 秒</td> 
      </tr> 
      <tr> 
      <td>1～2 分</td> 
      <td>20 秒<br /> </td> 
      </tr> 
      <tr> 
      <td>30～60 秒</td> 
      <td>10 秒</td> 
      </tr> 
      <tr> 
      <td>30 秒以下</td> 
      <td>5 秒</td> 
      </tr> 
    </tbody> 
   </table>

   ビデオタイムラインは、使用可能になったものと同じ量の画面領域を使用します。したがって、ブラウザーのサイズを変更しても、追加したセグメントの幅は正しく維持されます。

   説明するために、次の 3 つのスクリーンショットでは同じビデオを使用しています。各セグメントの幅は **[!UICONTROL タイムラインスケール]** 設定。

   ![chlimage_1-129](assets/chlimage_1-129.png)

   スクリーンショット A

   上記のスクリーンショット A は 29 秒の製品ビデオのデフォルト表示です。この **[!UICONTROL タイムラインスケール]** がデフォルトの 5 秒に設定されている。

   ![chlimage_1-130](assets/chlimage_1-130.png)

   スクリーンショット B

   上のスクリーンショット B では、 **[!UICONTROL タイムラインスケール]** スライダがデフォルトの 5 秒から 3 秒にドラッグされました。 個人 **[!UICONTROL タイムラインスケール]** タイムスタンプがすべて 3 秒間隔で設定されるようになりました。

   ![chlimage_1-131](assets/chlimage_1-131.png)

   スクリーンショット C

   上のスクリーンショット C では、 **[!UICONTROL タイムラインスケール]** 設定が 8 秒に移動されました。 製品サムネイルを含むセグメントが縮小されたことに注意してください。この方法でズームアウトすると、長いビデオでページの幅に合う追加セグメントの概要を確認したい場合に便利です。

1. （オプション）次のいずれかの操作を行います。

   * セグメントの開始時間と終了時間の調整

      セグメントを選択し、先頭または末尾の青い楕円形をドラッグして、開始時刻または終了時刻をそれぞれ調整します。表示されたビデオフレームは、調整内容に応じてビデオ内の適切な時間に移動します。タイムラインセグメントの移動は、タイムライン内の隣接するセグメントに基づいて制限されます。最小許容セグメント時間は 1 秒です。

      次のナビゲーションショートカットを使用すると、ビデオのセグメントを簡単にチェックして微調整することができます。

      * そのセグメントの先頭に直接ビデオをシークする場合は、先頭の青い楕円形をタップします。
      * そのセグメントの最後まで直接ビデオをシークする場合は、末尾の青い楕円形をタップします。
      * ビデオの再生をそのセグメントの最初に戻す場合は、セグメント全体をタップします

   ![chlimage_1-132](assets/chlimage_1-132.png)

   タイムラインセグメントの末尾の再配置

   * セグメントを削除するには

      タイムライン上にある最後のセグメントを選択し、ツールバーの「**[!UICONTROL セグメントを削除]**」をタップします。2 つ以上のセグメントが選択されている場合、 **[!UICONTROL セグメントを削除]** 機能は無効です。

      削除できるのは最後のセグメントのみです。例えば、タイムライン上のすべてのセグメントを削除したい場合、常に最後のセグメントを選択して「**[!UICONTROL セグメントを削除]**」をタップします。


1. 1 つまたは複数のサムネール画像を関連付ける時間セグメントを選択します。
1. ビデオの右側にある **[!UICONTROL コンテンツ]** タブをクリックします。
1. 以下 **[!UICONTROL コンテンツ]** タブ、タップ **[!UICONTROL アセットを選択]**&#x200B;を参照し、ビデオで使用するすべての画像アセットを参照して選択します。 選択したアセットが **[!UICONTROL アセットセレクター]** パネル **[!UICONTROL コンテンツ]** タブをクリックします。

1. 「コンテンツ」タブの下にあるアセットセレクターで、次のいずれかの操作を行います。

   <table> 
    <tbody> 
      <tr> 
      <td>選択したタイムラインセグメントへのサムネイルの関連付け</td> 
      <td><p>右側のアセットセレクターパネルで画像をタップします。</p> <p>1 つのタイムラインセグメントに好きなだけサムネールを追加できます。選択した各画像について、アセットセレクターの画像の上にチェックマークが表示されます。</p> </td> 
      </tr> 
      <tr> 
      <td>選択したタイムラインセグメントからのサムネイルの削除</td> 
      <td><p>次のいずれかの操作を行います。</p> 
        <ul> 
        <li>アセットセレクターパネルで、チェックマークの付いた画像をタップして選択を解除します。 画像アセットがタイムラインセグメントから削除されます。<br /> </li> 
        <li>選択したタイムラインセグメントで、画像をタップし、ツールバーでをタップします。 <strong>製品を削除</strong>.</li> 
        </ul> </td> 
      </tr> 
    </tbody> 
   </table>

   ![アセットピッカー](assets/chlimage_1-133.png)

   アセットセレクターパネルで画像をタップすると、選択したタイムラインセグメントに画像が追加されます。

1. いずれかのタイムラインセグメント内で 1 つのサムネール画像を選択し、 **[!UICONTROL アクション]** タブをクリックします。
1. 次のいずれかの操作を行います。
   <table> 
    <tbody> 
      <tr> 
      <td>選択したサムネイル画像のハイパーリンクへの関連付け</td> 
      <td><p>「アクションタイプ」で、をタップします。 <strong>クイックビュー</strong>.</p> <p>Adobe Experience Manager Sites または eCommerce のユーザーである場合：</p> 
       <ul> 
       <li>「SKU 値」テキストフィールドには、選択した製品の SKU(Stock Keeping Unit) が事前に入力されています。SKU は、提供する製品またはサービスごとの一意の識別子です。 このフィールドは、Adobe Experience Manager Commerce で画像が製品に関連付けられると自動的に設定されます。</li> 
       <li>設定済みの SKU が正しくない場合は、製品ピッカーアイコン（虫眼鏡）をタップまたはクリックして製品を選択ページを開きます。使用する製品をタップまたはクリックし、ページの右上隅にあるチェックマークをタップして、インタラクティブビデオエディターに戻ることができます。</li> 
       </ul> <p> Adobe Experience Manager Sites または eCommerce のユーザーで<em>ない</em>場合は、次のようにします。</p> 
       <ul> 
       <li>詳しくは、 <a href="/help/assets/carousel-banners.md#identifying-hotspot-and-image-map-variables">ホットスポットの変数の識別</a>.これらの変数を定義する必要があります。 </li> 
       <li>デフォルトでは、この SKU フィールドでは画像アセットのファイル名を拡張子を付けずに使用します。SKU に基づくファイルの標準的な命名規則に従っている場合、通常はファイルを編集する必要はありません。 </li> 
       <li>それ以外の場合は、デフォルト値を編集して、正しい SKU 値を入力します。「SKU 値」テキストフィールドに、製品の SKU（Stock Keeping Unit）を入力します。SKU は、提供している製品またはサービスごとの一意の識別子です。入力した SKU 値によってクイックビューテンプレートの変数部分が自動的に入力され、タップされた画像が特定の SKU のクイックビューに関連付けられます。</li> 
       </ul> <p>（オプション）クイックビュー内で製品をさらに識別するために使用する必要がある他の変数がある場合は、 <strong>汎用変数を追加</strong>. テキストフィールドに追加の変数を指定します。例えば、追加の変数として <code>category=Womens</code> などと指定します。</p> <p> </p> </td> 
      </tr> 
      <tr> 
      <td>選択したサムネール画像をハイパーリンクに関連付けるには</td> 
      <td><p>「アクションタイプ」で、をタップします。 <strong>ハイパーリンク</strong>次のいずれかの操作を行います。</p> 
       <ul> 
       <li>Adobe Experience Manager Sites のユーザーである場合は、サイトセレクターアイコン（フォルダー）をタップして Web ページに移動します。インタラクティブコンテンツに相対 URL のリンク（特に Experience Manager Sites ページへのリンク）がある場合、URL ベースのリンク方法は使用できません。</li> 
       <li>スタンドアロンの Dynamic Media ユーザーである場合は、「HREF」テキストフィールドに、リンクされる Web ページへの完全な URL パスを指定します。</li> 
       </ul> <p>このリンクを新しいブラウザータブで開くか、現在のタブで開くかを必ず指定します。</p> </td> 
      </tr> 
      <tr> 
      <td>選択したサムネイル画像のエクスペリエンスフラグメントへの関連付け</td> 
      <td><p>「アクションタイプ」で、をタップします。 <strong>エクスペリエンスフラグメント</strong>、次の操作を実行します。<p> 
       <ul> 
       <li>Adobe Experience Manager Sites のユーザーである場合は、検索アイコン（虫眼鏡）をタップまたはクリックしてエクスペリエンスフラグメントページを開きます。使用するエクスペリエンスフラグメントをタップまたはクリックし、次にをタップします。 <strong>選択 </strong>前のページのアクションパネルに戻れるように、ページの右上隅。<br /><a href="/help/sites-authoring/experience-fragments.md">エクスペリエンスフラグメント</a>を参照してください。</li> 
      </ul> 
       <ul> 
       <li>エクスペリエンスフラグメントがビデオに表示されるときの幅と高さを指定します。</li>
       </ul><strong>注意</strong>：インタラクティブビデオのソーシャルメディア共有ツールは、エクスペリエンスフラグメントにビューアを埋め込む場合はサポートされません。この問題を回避するには、ソーシャルメディアでの共有ツールを持たないビューアプリセットを使用または作成します。このようなビューアプリセットを使用すると、ビューアをエクスペリエンスフラグメントに正常に埋め込むことができます。</p></tr>&lt; 
      <tr> 
      <td>既にサムネール画像に割り当てられているアクションを編集するには</td> 
      <td>タイムラインセグメント内で、テキストラベルの右側にチェーンリンクが表示されているサムネール画像をタップします。チェーンリンクは、アクションが割り当てられていることを示します。次をタップします。 <strong>アクション</strong> 」タブをクリックして、変更を加えることができます。</td> 
      </tr> 
      <tr> 
      <td>サムネール画像のテキストラベルを変更するには</td> 
      <td><p>デフォルトでは、テキストラベルはサムネール画像の <code>Title</code> メタデータフィールドを使用します。<code>Title</code>がない場合は、代わりにサムネール画像のファイル名が使用されますが、拡張子は付きません。</p> <p>サムネール画像のテキストラベルを変更するには、「<strong>アクション</strong>」タブで、表示される画像アセットのすぐ下に目的のテキストを入力します。以下のスクリーンショットを参照してください。</p> <p>新しいテキストラベルは、ビデオプレーヤー自体と、タイムラインセグメントに表示されているサムネールテキストでのみ使用されています。ラベルの変更は、サムネール画像の「タイトル」メタデータフィールドとファイル名には影響しません。</p> </td> 
      </tr> 
      <tr> 
      <td>行った変更を元に戻す場合は、</td> 
      <td>ページの右上隅にある「<strong>取り消し</strong>」または「<strong>元に戻す</strong>」をタップします。</td> 
      </tr> 
    </tbody> 
   </table>

   ![experiencefragment_interactivevideos](assets/experiencefragment_interactivevideos.png)

   新しいテキストラベルがサムネイル画像に追加されます。

1. 次のいずれかの操作を行います。

   * 手順 6～11 を繰り返して、ビデオのタイムラインセグメントにさらにサムネイル画像を追加します。
   * オプションの手順 13 を行います。

1. （オプション）次のいずれかの操作を行います。

   * **[!UICONTROL セグメントの結合]**：製品サムネイルが割り当てられているかどうかにかかわらず、隣接する 2 つのセグメントは 1 つのセグメントに結合することができます。

      タイムライン上で、1 つのセグメントに統合する 2 つ以上の連続したセグメントをタップします。以下のスクリーンショットでは、選択した 2 つのセグメントに青い楕円形のドラッグハンドルが表示されていません。

      ツールバーの「**[!UICONTROL セグメントを統合]**」をタップします。
   ![chlimage_1-134](assets/chlimage_1-134.png)

   選択した 5 秒のセグメント 2 つを 10 秒のセグメント 1 つに統合。

   * **[!UICONTROL セグメントの分割]**：1 つのセグメントを 2 つの等しい時間のセグメントに分割できます。セグメントに既に製品サムネイルが割り当てられている場合、サムネイルは左側のセグメントに結合されます。

      タイムラインで、半分に分割したいセグメントをタップし、ツールバーで「**[!UICONTROL セグメントを分割]**」をタップします。

      2 つ以上のセグメントを選択すると、「**[!UICONTROL セグメントを分割]**」オプションは無効になります。
   ![chlimage_1-135](assets/chlimage_1-135.png)

   選択した 10 秒のセグメントを 5 秒ずつのセグメント 2 つに分割。

1. **[!UICONTROL インタラクティブビデオを作成]**&#x200B;ページの右上隅付近に、現在選択されてビデオで使用されているビューアプリセットの名前が表示されます。別のビューアプリセットを選択する場合は、この名前をタップします。

   例えば、`Shoppable_Video_light` ビューアプリセットでは、ビデオが再生されるときに横に白い表示領域が現れます。この表示領域には、クリック可能なサムネール画像が再生中に表示されます。`Shoppable_Video_dark` ビューアプリセットでは、ビデオが再生されるときに横に黒い表示領域が現れます。

   インタラクティブビデオの独自のビューアプリセットを作成した場合は、そのプリセットもリストに表示され、そこから選択できます。

   完了したら、「**[!UICONTROL 保存]**」をタップします。

   >[!NOTE]
   インタラクティブビデオを保存すると、関連付けられた `.vtt` ファイルも自動的に保存されます。`.vtt` ファイルは、**[!UICONTROL アセット]**&#x200B;のルートにある `_VTT` フォルダーに保存されます。インタラクティブビデオが Web サイト上で正しく再生されるには、それらのファイルとフォルダーが必要です。したがって、`_VTT` フォルダーやフォルダーのコンテンツを移動したり、編集したり削除しないでください。

1. インタラクティブビデオを公開します。公開によって埋め込みコードまたは URL が生成されます。最終的には、このコードまたは URL を Web サイトのエクスペリエンスにコピー＆ペーストします。

   クイックビューを使用したインタラクティビティを追加した場合は、埋め込みコードのみを使用します。ハイパーリンクされた Web ページを使用したインタラクティビティを追加した場合は、公開された URL を使用することもできます。ただし、インタラクティブコンテンツに相対 URL のリンク（特に Adobe Experience Manager Sites ページへのリンク）がある場合、URL ベースのリンク方法は使用できません。

   [アセットの公開](publishing-dynamicmedia-assets.md)を参照してください。

   >[!NOTE]
   クイックビューを含むショッパブルビデオを公開するには、各ビデオの関連する画像アセットもコマース領域から個別に公開してください。

   タイムラインセグメントを追加し、インタラクティブビデオを公開したので、既存の Web サイトのランディングページにビデオを追加する準備が整いました。[インタラクティブビデオの Web サイトへの統合](#integrating-an-interactive-video-with-your-website)を参照してください。

## インタラクティブビデオアセットの公開 {#publishing-interactive-video-assets}

インタラクティブビデオアセットの公開方法について詳しくは、[アセットの公開](publishing-dynamicmedia-assets.md)を参照してください。

## インタラクティブビデオの Web サイトへの統合 {#integrating-an-interactive-video-with-your-website}

ビデオをアップロードし、タイムラインセグメントを追加して、インタラクティブビデオを公開したら、既存の Web サイトにビデオを追加する準備は完了です。

Adobe Experience Manager Sites のユーザーである場合は、インタラクティブメディアコンポーネントをページにドラッグしてインタラクティブビデオを追加できます。[ページへの Dynamic Media アセットの追加](adding-dynamic-media-assets-to-pages.md)を参照してください。

スタンドアロンの Adobe Experience Manager Assets のユーザーである場合は、この節で説明するようにインタラクティブビデオを手動で Web サイトに追加できます。

**インタラクティブビデオを Web サイトに統合するには：**

1. 公開済みのインタラクティブビデオの埋め込みコードまたは URL をコピーします。

   [Web ページへのビデオビューアまたは画像ビューアの埋め込み](embed-code.md)を参照してください。

   クイックビューを使用したインタラクティビティを追加した場合は、埋め込みコードのみを使用します。ハイパーリンクされた Web ページを使用したインタラクティビティを追加した場合は、公開された URL を使用することもできます。ただし、インタラクティブコンテンツに相対 URL のリンク（特に Adobe Experience Manager Sites ページへのリンク）がある場合、URL ベースのリンク方法は使用できません。

1. ターゲットの Web ページのコードで、静的なビデオの場所を特定します。
1. 静的なビデオを削除し、Adobe Experience Manager Assets からコピーした埋め込みコードまたは URL でそのままコードを置き換えます。

   コピーされた埋め込みコードはレスポンシブ環境用に設定されているので、以前静的ビデオが占有していた領域に自動的に適応します。

>[!NOTE]
そのため、ハイパーリンクされた Web ページのみを使用したインタラクティビティを追加した場合は、これで完了です。
ただし、クイックビューのトリガーにインタラクティビティを追加した場合、インタラクティブビデオの横のサムネールは表示専用です。既存のクイックビューとまだ統合されていません。 その場合は、インタラクティブビデオを Web サイト上の既存のクイックビューに統合する必要があります。

**例**

次のデモ Web サイトを例として使用します。

[https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-video/john-lewis/landing-0.html?lang=ja](https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-video/john-lewis/landing-0.html?lang=ja)

標準のビデオ埋め込みコードを確認します。

```xml
<style type="text/css">
 #s7video_div.s7videoviewer{
   width:100%; 
   height:auto;
 }
</style>

<script type="text/javascript" src="https://demos-pub.assetsadobe.com/etc/dam/viewers/s7viewers/html5/js/VideoViewer.js"></script>
<div id="s7video_div"></div>
<script type="text/javascript">
 var s7videoviewer = new s7viewers.VideoViewer({
  "containerId" : "s7video_div",
  "params" : { 
   "serverurl" : "https://adobedemo62-h.assetsadobe.com/is/image",
   "contenturl" : "https://demos-pub.assetsadobe.com/", 
   "config" : "/etc/dam/presets/viewer/Video",
   "config2": "/etc/dam/presets/analytics",
   "videoserverurl": "https://gateway-na.assetsadobe.com/DMGateway/public/demoCo",
   "posterimage": "/content/dam/marketing/shoppable-video/john-lewis/shoppable-video-john-lewis-2014.mp4",
   "asset" : "/content/dam/marketing/shoppable-video/john-lewis/shoppable-video-john-lewis-2014.mp4" }
 }).init();
</script>
```

統合は、ビデオ埋め込みコードを削除して、Adobe Experience Manager のインタラクティブビデオ埋め込みコードで置き換えるだけで簡単にできます。次の URL で結果を確認できます。ページにインタラクティブビデオが表示されますが、既存のクイックビューとはまだ統合されていません。

[https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-video/john-lewis/landing-1.html?lang=ja](https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-video/john-lewis/landing-1.html?lang=ja)

## インタラクティブビデオの既存のクイックビューへの統合 {#integrating-an-interactive-video-with-an-existing-quickview}

>[!NOTE]
このタスクはスタンドアロン Adobe Experience Manager Assets のユーザーにのみ当てはまります。

このプロセスの最後の手順は、Web サイトで使用されている既存のクイックビュー実装にインタラクティブビデオを統合することです。すべてのケースで機能する統合のソリューションはありません。クイックビューの実装はすべて一意です。そのため、フロントエンド IT 担当者の支援を受けた個別のアプローチが必要になります。

既存のクイックビュー実装は一般的に、Web ページ上で以下の順に発生する、相互に関連するアクションの連鎖となっています。

1. ユーザーは、Web サイトのユーザーインターフェイス内で、特定の要素を起動します。
1. フロントエンドコードは、手順 1 で起動されたユーザーインターフェイスの要素に基づいてクイックビュー URL を取得します。
1. フロントエンドコードは、手順 2 で取得した URL を使用して AJAX リクエストを送信します。
1. バックエンドロジックは、対応するクイックビューのデータまたはコンテンツをフロントエンドコードに返します。
1. フロントエンドコードは、クイックビューのデータまたはコンテンツを読み込みます。
1. （オプション）フロントエンドコードは、読み込んだクイックビューのデータを HTML 表現に変換します。
1. フロントエンドコードは、モーダルダイアログボックスまたはパネルを表示し、エンドユーザー向けに、画面上に HTML コンテンツをレンダリングします。

これらの呼び出しは、必ずしもそれぞれ独立した、Web ページのロジックから任意の手順で呼び出すことができるパブリックな API 呼び出しを表すわけではありません。むしろ、次の手順が前の手順の最後のフェーズ（コールバック）に隠されているような連鎖的な呼び出しになっています。

インタラクティブビデオが手順 1 と部分的な手順 2 を置き換えるのと同時に、ユーザーがインタラクティブビデオ内のサムネールをクリックすると、そのようなユーザー操作がビューアによって処理されます。 ビューアは、Adobe Experience Manager に以前に追加されたすべてのサムネールデータを含む Web ページに、イベントを返します。

そのようなイベントハンドラーでは、フロントエンドコードは次の処理を実行します。

* インタラクティブビデオから送出されるイベントをリッスンします。
* サムネイルデータに基づいてクイックビュー URL を作成します。
* バックエンドからクイックビューを読み込み、表示用に画面にレンダリングするプロセスをトリガーします。

また、インタラクティブビデオビューアでは、全画面操作モードもサポートされます。エンドユーザーは、フルスクリーンのままサムネールをクリックすることでクイックビューをトリガーします。 この機能を実現するには、クイックビューのモーダルダイアログボックスがビューアのコンテナにアタッチされるようにフロントエンドコードを変更します。ドキュメントの Body またはビューアが全画面モードになっているときに使用できないその他の Web ページ要素を追加しないでください。このジョブを実行するコードは、ビューアがページに読み込まれた後で送信されるもう 1 つのビューアコールバックをリッスンします。

Adobe Experience Manager によって返される埋め込みコードには、そのまま使用可能なイベントハンドラーが既に含まれています。次のハイライトされたコードスニペットのように、コメントアウトされています。

```xml
<style type="text/css">
 #s7interactivevideo_div.s7interactivevideoviewer{
   width:100%; 
   height:auto;
 }
</style>
<script type="text/javascript" src="https://demos-pub.assetsadobe.com/etc/dam/viewers/s7viewers/html5/js/InteractiveVideoViewer.js"></script>

<div id="s7interactivevideo_div"></div>
<script type="text/javascript">
 var s7interactivevideoviewer = new s7viewers.InteractiveVideoViewer({
  "containerId" : "s7interactivevideo_div",
  "params" : { 
   "serverurl" : "https://adobedemo62-h.assetsadobe.com/is/image",
   "contenturl" : "https://demos-pub.assetsadobe.com/", 
   "config" : "/etc/dam/presets/viewer/Shoppable_Video_light",
   "config2": "/etc/dam/presets/analytics",
   "videoserverurl": "https://gateway-na.assetsadobe.com/DMGateway/public/demoCo",
   "interactivedata": "content/dam/_VTT/marketing/shoppable-video/john-lewis/shoppable-video-john-lewis-2014.mp4.svideo.vtt",
   "VideoPlayer.contenturl": "https://adobedemo62-h.assetsadobe.com/is/content",
   "asset" : "/content/dam/marketing/shoppable-video/john-lewis/shoppable-video-john-lewis-2014.mp4" }
 })
 /* // Example of interactive video event for quickview.
   s7interactivevideoviewer.setHandlers({ 
   "quickViewActivate": function(inData) {
     var sku=inData.sku; //SKU for product ID
    //To pass other parameter from the hotspot, you need to add custom parameter during the hotspot setup as parameterName=value
    loadQuickView(sku); //Replace this call with your quickview plugin
    //Please refer to your quickviewer plugin for the quickview call
    }, 
"initComplete":function() { 
    //--- Attach quickview popup to viewer container so popup will work in fullscreen mode ---
    var popup = document.getElementById('quickview_div'); // get custom quickview container
    popup.parentNode.removeChild(popup); // remove it from current DOM
    var sdkContainerId = s7interactivevideoviewer.getComponent("container").getInnerContainerId(); // get viewer container component
    var inner_container = document.getElementById(sdkContainerId); 
    inner_container.appendChild(popup); //Attach custom quickview container to viewer
    } 
   });
 */
 s7interactivevideoviewer.init();
</script>
```

そのため、必要な処理は、このハイライトされたコードスニペットのコメントアウトを解除し、ダミーのハンドラー本体を、特定の Web ページ専用のコードに置き換えることだけです。

標準の埋め込みコードには、2 つのデフォルトコールバックハンドラー、`quickViewActivate` と `initComplete` が含まれています。`quickViewActivate` ハンドラーがトリガーされるのは、ビューアでサムネールがクリックされるときです。これを使用して、ビューアをクイックビューのアクティベートロジックに統合します。`initComplete` ハンドラーは、ビューアがページに読み込まれるときに 1 回だけトリガーされます。このハンドラーは、Web ページ DOM でのクイックビューダイアログボックスの位置を調整するために使用されます。

クイックビュー URL の作成プロセスは、このトピックで既に説明したサムネイルの変数を識別するためのプロセスと逆になります。前に特定したクイックビュー URL の例を使用して、クイックビュー URL の各ケースでの作成方法を確認できます。

<table> 
     <tbody> 
      <tr> 
       <td><p>単一の SKU（クエリ文字列内）</p> </td> 
       <td><code class="code">s7interactivevideoviewer.setHandlers({
          "quickViewActivate": function(inData) {
          var quickViewUrl = "https://server/json?productId=" + inData.sku + "&amp;source=100";
          },
          });</code></td> 
      </tr> 
      <tr> 
       <td>単一の SKU（URL パス内）</td> 
       <td><code class="code">s7interactivevideoviewer.setHandlers({
          "quickViewActivate": function(inData) {
          var quickViewUrl = "https://server/product/" + inData.sku;
          },
          });</code></td> 
      </tr> 
      <tr> 
       <td><p>SKU とカテゴリ ID（クエリ文字列内）</p> </td> 
       <td><code class="code">s7interactivevideoviewer.setHandlers({
          "quickViewActivate": function(inData) {
          var quickViewUrl = "https://server/quickView/product/?category=" + inData.categoryId + "&amp;prodId=" + inData.sku;
          },
          });</code></td> 
      </tr> 
     </tbody> 
    </table> </td> 
  </tr> 
  <tr></tr> 
 </tbody> 
</table>

クイックビュー URL をトリガーしてクイックビューパネルをアクティベートするための最後の手順では、フロントエンドの IT 担当者のサポートが必要になる可能性が高くなります。フロントエンド IT 担当者は、すぐに使用できるクイックビュー URL を用意し、クイックビューを適切な手順で正しく実装するための最適な方法を知っています。

これらの手順をデモ Web サイトに適用してインタラクティブビデオをクイックビューのコードに統合する方法を確認できます。このトピックでは先ほど、クイックビュー URL の構造を次のように特定しました。

```xml
/datafeed/$CategoryId$-$SKU$.json
```

この URL は `quickViewActivate` ハンドラー内で簡単に再構成できます。次のように、ビューアのコードを介してハンドラーに渡される `categoryId` オブジェクト内の `sku` フィールドと `inData` フィールドを使用します。

```xml
var sku=inData.sku;
var categoryId=inData.categoryId;
var quickViewUrl = "datafeed/" + categoryId + "-" + sku + ".json";
```

このデモ Web サイトは、単純な `loadQuickView()` 関数呼び出しを使用してクイックビューダイアログボックスを起動しています。この関数は、1 つの引数（クイックビューデータの URL）のみを受け取ります。最後の手順は、インタラクティブビデオを統合する場合に、次のコード行を `quickViewActivate` ハンドラー：

```xml
loadQuickView(quickViewUrl);
```

最後に、 **[!UICONTROL クイックビュー]** ダイアログボックスが、ビューアのコンテナ要素にアタッチされています。 デフォルトの埋め込みコードは、この機能を実現するためのサンプル手順を提供します。 ビューアのコンテナ要素への参照を取得するには、次のコード行を使用できます。

```xml
var sdkContainerId = s7interactivevideoviewer.getComponent("container").getInnerContainerId(); // get viewer container component
var inner_container = document.getElementById(sdkContainerId);
```

ここで、`inner_container` が、ビューアによって管理される `DIV` 要素への参照です。ダイアログボックスをこの `DIV` の子にしようとしています。

実際にモーダルダイアログボックス要素を探して前述のコンテナにアタッチする手順は、ケースごとに異なります。ここでも、必要なクイックビュー実装に詳しいフロントエンド開発者の助けを借りることをお勧めします。

サンプル Web サイトの場合、クイックビューモーダルダイアログボックスは `DIV` として実装され、クイックビューモーダル ID がドキュメント `BODY` に直接アタッチされています。したがって、このダイアログボックスをビューアのコンテナに移動するコードは、次のように簡単です。

```xml
var sdkContainerId = s7interactivevideoviewer.getComponent("container").getInnerContainerId(); // get viewer container component
var inner_container = document.getElementById(sdkContainerId);
inner_container.appendChild(document.getElementById("quickview-modal"));
```

完全なソースコードは次のとおりです。

```xml
<style type="text/css">
 #s7interactivevideo_div.s7interactivevideoviewer{
   width:100%; 
   height:auto;
 }
</style>
<script type="text/javascript" src="https://demos-pub.assetsadobe.com/etc/dam/viewers/s7viewers/html5/js/InteractiveVideoViewer.js"></script>

<div id="s7interactivevideo_div"></div>
<script type="text/javascript">
 var s7interactivevideoviewer = new s7viewers.InteractiveVideoViewer({
  "containerId" : "s7interactivevideo_div",
  "params" : { 
   "serverurl" : "https://adobedemo62-h.assetsadobe.com/is/image",
   "contenturl" : "https://demos-pub.assetsadobe.com/", 
   "config" : "/etc/dam/presets/viewer/Shoppable_Video_light",
   "videoserverurl": "https://gateway-na.assetsadobe.com/DMGateway/public/demoCo",
   "interactivedata": "content/dam/_VTT/marketing/shoppable-video/john-lewis/shoppable-video-john-lewis-2014.mp4.svideo.vtt",
   "VideoPlayer.contenturl": "https://adobedemo62-h.assetsadobe.com/is/content",
   "asset" : "/content/dam/marketing/shoppable-video/john-lewis/shoppable-video-john-lewis-2014.mp4" }
 })
 // Example of interactive video event for quickview.
   s7interactivevideoviewer.setHandlers({ 
   "quickViewActivate": function(inData) {
     var sku=inData.sku; //SKU for product ID
     var categoryId=inData.categoryId; //categoryId
    var quickViewUrl = "datafeed/" + categoryId + "-" + sku + ".json";
    loadQuickView(quickViewUrl);
    },
   "initComplete":function() { 
    //--- Attach quickview popup to viewer container so popup will work in fullscreen mode ---
    var sdkContainerId = s7interactivevideoviewer.getComponent("container").getInnerContainerId(); // get viewer container component
    var inner_container = document.getElementById(sdkContainerId);
    inner_container.appendChild(document.getElementById("quickview-modal"));
    } 
   });
 s7interactivevideoviewer.init();
</script>
```

インタラクティブビデオが完全に統合された最終的なデモ Web サイトは次のようになります。

[https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-video/john-lewis/landing-3.html?lang=ja](https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-video/john-lewis/landing-3.html?lang=ja)

## クイックビューを使用したカスタムポップアップの作成 {#using-quickviews-to-create-custom-pop-ups}

詳しくは、 [クイックビューを使用したカスタムポップアップの作成](custom-pop-ups.md).
