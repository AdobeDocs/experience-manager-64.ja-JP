---
title: Dynamic Mediaビューアプリセットの管理
seo-title: Managing Dynamic Media viewer presets
description: Dynamic Mediaビューアプリセットの作成方法と管理方法
seo-description: How to create and manage Dynamic Media viewer presets
uuid: 31ef7a4e-2053-43b5-ac6c-cdc4b30c3914
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.4/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: e78bb08a-a923-4399-b3f7-13aa4b7994d5
legacypath: /content/docs/en/aem/6-0/administer/integration/dynamic-media/viewer-presets
exl-id: 53e53cb7-1854-44e9-9516-51bcc99378b4
feature: Viewer Presets
role: Admin,User
source-git-commit: 877eade71c2ec57ff534ba2649275111c5326d75
workflow-type: tm+mt
source-wordcount: '4220'
ht-degree: 67%

---

# Dynamic Mediaビューアプリセットの管理 {#managing-viewer-presets}

Dynamic Mediaのビューアプリセットは、ユーザーがコンピューターの画面やモバイルデバイスでリッチメディアアセットを表示する方法を決定する一連の設定です。 管理者は、ビューアプリセットを作成できます。 設定は、ビューア設定オプションの配列で使用できます。 例えば、ビューアの表示サイズやズームの動作を変更できます。

HTML5 ビューアーのプリセットを独自に作成およびカスタマイズする方法については、Adobe Dynamic Media の *HTML5 Viewer SDK API ドキュメント*&#x200B;を参照してください。SDK は、SDK 自体に組み込まれている IS 公開サーバーで使用できます。各ライブラリバージョンには、独自の SDK ドキュメントが含まれています。

パス：`<scene7_domain>/s7sdk/<library_version>/docs/jsdocs/index.html`\
たとえば、3.10 SDK の場合：[https://s7d1.scene7.com/s7sdk/3.10/docs/jsdoc/index.html](https://s7d1.scene7.com/s7sdk/3.10/docs/jsdoc/index.html)

[Adobe Dynamic Media ビューアリファレンスガイド](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/homeviewers.html?lang=ja)も参照してください。

このセクションでは、ビューアのプリセットを作成、編集、管理する方法について説明します。ビューアのプリセットは、アセットをプレビューする際にいつでも適用できます。詳しくは、「[ビューアのプリセットの適用](viewer-presets.md)」を参照してください。

>[!NOTE]
>
>*事前に定義された標準提供ビューアプリセット*&#x200B;を編集するシナリオはサポートされていません。標準提供のビューアのプリセットを編集しようとすると、ビューアのプリセットに新しい名前を付けて保存するよう求められます。

## 閲覧者のキーボードアクセシビリティ {#keyboard-accessibility-for-viewers}

すべての標準提供ビューアでキーボードアクセシビリティがサポートされています。

[キーボードアクセシビリティとナビゲーション](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/c-keyboard-accessibility.html?lang=ja)に関するページも参照してください。

## Dynamic Mediaビューアプリセットの管理 {#managing-presets}

AEMでビューアプリセットの追加、編集、削除、公開、非公開およびプレビューを実行するには、次の操作をタップします **[!UICONTROL ツール/アセット/ビューアプリセット]**.

![tools-assets](assets/tools-assets.png)

>[!NOTE]
>
>アセットの詳細表示で「閲覧者」を選択すると、デフォルトでビューアのプリセットが 15 個表示されます。この制限は増やすことができます。[表示されるビューアプリセットの数を増やす](#increasing-the-number-of-viewer-presets-that-display)を参照してください。

## レスポンシブデザイン Web ページのビューアサポート {#viewer-support-for-responsive-designed-web-pages}

Web ページによってニーズは異なります。例えば、HTML5 ビューアが別のブラウザーウィンドウで 開くリンクを提供する web ページが必要な場合があります。ホスティングページに直接 HTML5 ビューアを埋め込む必要が生じる場合があります。後者の場合は、web ページのレイアウトが静的な場合や、または、 *レスポンシブ* およびの表示は、デバイスごと、またはブラウザーウィンドウのサイズごとに異なります。 これらのニーズに対応するために、Dynamic Media に付属する事前定義済みの標準提供 HTML5 ビューアはすべて、静的な Web ページとレスポンシブデザイン Web ページの両方をサポートしています。

詳しくは、 [レスポンシブ画像ライブラリ](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/responsive-static-image-library/c-about-responsive-static-image-library.html?lang=ja) 内 *画像サービング API ヘルプ* レスポンシブビューアを web ページに埋め込む方法について詳しくは、こちらを参照してください。

>[!NOTE]
>
>標準提供ビューアを使用するには、まずすべて公開する必要があります。\
>[ビューアプリセットの公開](#publishing-viewer-presets)を参照してください。

## ビューアプリセットのシステム互換性  {#viewer-preset-system-compatibility}

Dynamic Media に付属するすべての標準提供のビューアのプリセットは、次のシステムと完全に互換性があります。

* デスクトップ
* Apple iPhone
* Apple iPad
* Android スマートフォン
* Android タブレット
* ビデオの場合、MP4 再生の追加サポートが [Blackberry](https://developer.blackberry.com/devzone/develop/supported_media/bb_media_support_at_a_glance.html#kba1328730952678) および [Windows Phone 8](https://msdn.microsoft.com/library/windows/apps/ff462087%28v=vs.105%29.aspx).

### ビューアプリセットのリッチメディアタイプ {#rich-media-types-for-viewer-presets}

管理者は、新しいビューアプリセットの作成時に次のリッチメディアタイプを追加してカスタマイズすることができます。

| リッチメディアタイプ | 説明 |
|:---|:---|
| **カルーセルセット** | ホットスポットや画像マップ、またはその両方が 2 つ以上の一連の画像に追加されます。お客様は画像を左右にパンし、画像のホットスポットをクリックして追加の詳細情報を入力したり、Web サイトのカテゴリ、ホームまたはランディングページから直接購入したりできます。 |
| **フライアウトズーム** | ズームされた領域の 2 つ目の画像を元の画像の横に表示します。使用できるコントロールはありません。表示する領域に選択範囲を移動します。 |
|  | このビューアの完全な帯域幅使用量を判断する際には、メイン画像とフライアウト画像の両方がビューアに提供されることを考慮してください。 メイン画像のサイズ（ステージの幅と高さ）とズーム率によって、フライアウト画像のサイズが決まります。フライアウトのファイルサイズが大きくなりすぎないようにするには、次の 2 つの値のバランスを取ります。メイン画像のサイズが大きい場合は、ズーム率の値を小さくします。（フライアウトの幅と高さによってフライアウトウィンドウのサイズが決まりますが、ビューアに提供されるフライアウト画像のサイズは決まりません。） |
|  | 例えば、メイン画像のサイズが 350 x 350 ピクセルで、ズーム率が 3 の場合、生成されるフライアウト画像は 1050 x 1050 ピクセルになります。メイン画像のサイズが 300 x 300 ピクセルで、ズーム率が 4 の場合、フライアウト画像は 1200 x 1200 ピクセルになります。 JPEG 品質の設定（推奨設定は 80～90）によって、ファイルサイズを大幅に小さくすることができます。推奨ズーム率は、メイン画像のサイズに応じて 2.5～4 です。 |
| **インラインズーム** | 元のビューア内でズームされた領域の画像を表示します。使用するコントロールはありません。つまり、ユーザーは表示したい領域に選択範囲を移動します。 |
| **画像セット** | 画像セットビューアでは、サムネール画像をクリックして、項目の様々なビューやカラーを表示できます。 このビューアは、画像を接近して確認するためのズームツールも提供しています。 |
| **インタラクティブ画像** | ユーザーがクリックして追加の詳細情報を入力したり、Web サイトのカテゴリ、ホームまたはランディングページから直接購入したりするためのホットスポットを画像の一部に追加します。 |
| **インタラクティブビデオ** | ユーザーがクリックして追加の詳細情報を入力したり、Web サイトのカテゴリ、ホームまたはランディングページから直接購入したりするためのサムネールをビデオ内のタイムラインセグメントに追加します。 |
| **混在メディア** | 1 つのビューアで異なる複数のタイプのメディアを表示します。スピンセット、画像セット、画像、ビデオを使用できます。 |
| **パノラマ画像** | パノラマ画像およびパノラマ VR ビューアでは球状のパノラマ画像をレンダリングして、部屋、プロパティ、場所、風景などの 360° の視聴エクスペリエンスにユーザーを没入させます。 |
|  | アップロードした画像が球パノラマと見なされるには、次のいずれかまたは両方を満たす必要があります。 <ul><li>アスペクト比が 2:1 です。</li><li>キーワードがエクイレクタングラー、球状とパノラマ、または球状とパノラマでタグ付けされています。 [タグの使用](../sites-authoring/tags.md)を参照してください。</li></ul> |
|  | アスペクト比とキーワードの両方の条件が、アセットの詳細ページと「パノラマメディア」WCM コンポーネントのパノラマアセットに適用されます。 |
|  | 重要：このビューアを使用できるのは、Dynamic Media - Scene7 モードのみです。 |
| **スピンセット** | ユーザーがオブジェクトを回転させて、様々な面や角度を確認できるように、複数の画像ビューを提供します。 |
| **ビデオ** | プログレッシブまたはアダプティブビットレートストリーミングを使用してビデオを再生します。アダプティブビットレートストリーミングはデバイスと帯域幅を自動的に検出し、適切な形式で適切な品質のビデオを配信します。 |
| **垂直方向ズーム** | 垂直ズームビューアでは、製品画像の視聴エクスペリエンスを最大化して、ユーザーに製品を最適に表示できます。スウォッチの垂直方向の位置では、次の操作を行います。 <ul><li>スウォッチがフォールドの上に表示されます。 水平スウォッチの場合、ユーザーのデスクトップ画面のサイズに応じて、スウォッチは、ユーザーがページを下にスクロールするまで表示されませんでした。 ビューアにスウォッチを垂直方向に配置すると、ユーザの画面サイズに関係なくスウォッチが表示されます。</li><li>メイン画像のサイズを最大化する。 水平方向のスウォッチの場合、確実に表示されるようにページ上にスペースを確保しておく必要があります。この配置によって、メイン画像のサイズが小さくなります。ただし、垂直方向のスウォッチレイアウトの場合は、こうしたスペースを確保する必要がありません。そのため、メイン画像のサイズを最大化できます。</li></ul> |
| **ズーム** | ユーザーが領域をクリックしてズームインできます。 ユーザーは、コントロールをクリックして、画像をズームイン、ズームアウトおよびデフォルトサイズにリセットできます。 |

## 標準提供ビューアプリセットのリスト {#list-of-out-of-the-box-viewer-presets}

次の表に、Dynamic Mediaに付属する事前定義済みの標準提供ビューアプリセットを示します。

[ライブデモ](https://landing.adobe.com/en/na/dynamic-media/ctir-2755/live-demos.html)も参照してください。

ビューアでサポートされている Web ブラウザーとオペレーティングシステムのバージョンについては、ビューアのリリースノートに記載されています。

詳しくは、 *ビューアリリースノート* の目次に [ビューアリファレンスガイド](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/homeviewers.html?lang=ja).

>[!NOTE]
>
>Dynamic Mediaの標準提供ビューアプリセットはすべて既にアクティベート済みです（オン）。ただし、公開する必要があります。\
>[ビューアプリセットの公開](#publishing-viewer-presets)を参照してください。
>
>作成および追加した新しいビューアプリセットは、すべてアクティベートされている必要があります *および* 公開済み。\
>[ビューアプリセットのアクティベートとアクティベート解除](#activating-or-deactivating-viewer-presets)と[ビューアプリセットの公開](#publishing-viewer-presets)を参照してください。

| ビューアプリセットのタイトル | タイプ | CSS ファイル名 |
|:---|:---|:---|
| Carousel_Dotted_dark | Carousel_Set | html5_carouselviewer_dotted_dark.css |
| Carousel_Dotted_light | Carousel_Set | html5_carouselviewer_dotted_light.css |
| Carousel_Numeric_dark | Carousel_Set | html5_carouselviewer_numeric_dark.css |
| Carousel_Numeric_light | Carousel_Set | html5_carouselviewer_numeric_light.css |
| フライアウト | Flyout_Zoom | html5_flyoutviewer.css |
| ImageSet_dark | 画像セット | html5_zoomviewer_dark.css |
| ImageSet_light | 画像セット | html5_zoomviewer_light.css |
| InlineMixedMedia_dark | Mixed_Media | html5_inlinemixedmediaviewer_dark.css |
| InlineMixedMedia_light | Mixed_Media | html5_inlinemixedmediaviewer_light.css |
| InlineZoom | Flyout_Zoom | html5_inlinezoomviewer.css |
| MixedMedia_dark | Mixed_Media | html5_mixedmediaviewer_dark.css |
| MixedMedia_light | Mixed_Media | html5_mixedmediaviewer_light.css |
| PanoramicImage | Panoramic_Image | html5_panoramicimage.css |
| PanoramicImageVR | Panoramic_Image | html5_panoramicimage.css |
| Shoppable_Banner | Interactive_Image | html5_interactiveimage.css |
| Shoppable_Video_dark | Interactive_Video | html5_interactivevideoviewer_dark.css |
| Shoppable_Video_light | Interactive_Video | html5_interactivevideovewer_light.css |
| SpinSet_dark | Spin_Set | html5_spinviewer_dark.css |
| SpinSet_light | Spin_Set | html5_spinviewer_light.css |
| ビデオ（クローズドキャプションのサポートを含む） | ビデオ | html5_videoviewer.css |
| Video_social （クローズドキャプションおよびソーシャルメディアのサポートを含む） | ビデオ | html5_videoviewersocial.css |
| Zoom_dark | ズーム | html5_basiczoomviewer_dark.css |
| Zoom_light | ズーム | html5_basiczoomviewer_light.css |
| ZoomVertical_dark | Vertical_Zoom | html5_zoomverticalviewer_dark.css |
| ZoomVertical_light | Vertical_Zoom | html5_zoomverticalviewer_light.css |

### サポートされているモバイルビューアのジェスチャーに関する表 {#supported-mobile-viewers-gestures-matrix}

次の表に、iOS、Android 2.x および Android 3.x デバイスでサポートされているモバイルビューアのジェスチャーを示します。

| ジェスチャー | フライアウトズーム | ズーム | スピン |
|---|---|---|---|
| **ドラッグ** | パン | パン | パン |
| **タップ** | フライアウトウィンドウを表示 | ユーザインターフェイスを表示または非表示 | ユーザインターフェイスを表示または非表示 |
| **ダブルタップ** | 適用なし | ズームインまたはリセット | ズームインまたはリセット |
| **ピンチオープン** | 適用なし | ズームイン (iOSおよび Android 3x のみ ) | ズームイン (iOSおよび Android 3x のみ ) |
| **ピンチクローズ** | 適用なし | ズームアウト (iOSおよび Android 3x のみ ) | ズームアウト (iOSおよび Android 3x のみ ) |
| **スワイプ** | スウォッチバーをスクロール | 画像をスクロール | スピン |
| **フリック** | スウォッチバーをスクロール | 画像をスクロール | スピン |

## 表示されるDynamic Mediaビューアプリセットの数の増加 {#increasing-the-number-of-viewer-presets-that-display}

**[!UICONTROL 詳細ビュー／ビューア]**&#x200B;でアセットを表示したとき、AEM には様々なビューアプリセットが表示されます。表示されるビューアの数を増減できます。

**表示されるDynamic Mediaビューアプリセットの数を増やすには：**:

1. に移動します。 **[!UICONTROL CRXDE Lite]** ([http://localhost:4502/crx/de](http://localhost:4502/crx/de)) をクリックします。
1. ビューアプリセットリストノード（`/libs/dam/gui/coral/content/commons/sidepanels/viewerpresets/viewerpresetslist`）に移動します。

   ![chlimage_1-221](assets/chlimage_1-221.png)

1. 「**[!UICONTROL limit]**」プロパティで、「**[!UICONTROL 値]**」（デフォルトで 15 に設定されています）を目的の数に変更します。
1. ビューアプリセットデータソース（`/libs/dam/gui/coral/content/commons/sidepanels/viewerpresets/viewerpresetslist/datasource`）に移動します。

   ![chlimage_1-222](assets/chlimage_1-222.png)

1. 内 **[!UICONTROL 制限]** プロパティの数を、目的の数（例： ）に変更します。 `{empty requestPathInfo.selectors[1] ? "20" : requestPathInfo.selectors[1]}`
1. 「**[!UICONTROL すべて保存]**」をタップします。

## 新しいDynamic Mediaビューアプリセットの作成 {#creating-a-new-viewer-preset}

ビューアプリセットを作成しておくと、アセットの表示やアセットとの対話のための様々な設定を適用できます。ただし、新しいビューアプリセットを作成する必要はありません。 デフォルトの、すぐに使えるビューアプリセットが既に AEM Assets に付属していますので、これを使用できます。

新しいビューアプリセットを作成することを選んだ場合、ビューアプリセットを保存すると、ビューアプリセットページのそのビューアの状態が自動的にアクティベート済みになります（「**オン**」に設定されます）。****&#x200B;この状態は、 **[!UICONTROL Dynamic Media]** コンポーネントと **[!UICONTROL インタラクティブメディア]** コンポーネントを使用し、画像またはビデオをプレビューする際に使用できます。

一部のビューアプリセットには、ビューアの全体的な動作に影響する専用の設定があります。作成するビューアプリセットによっては、これらの特別な考慮事項について注意する必要があります。

[インタラクティブなビューアのプリセットを作成するための特別な考慮事項](#special-considerations-for-creating-an-interactive-viewer-preset)を参照してください。

[カルーセルバナーのビューアプリセットの作成に関する考慮事項](#special-considerations-for-creating-a-carousel-banner-viewer-preset)を参照してください。

**新しいDynamic Mediaビューアプリセットを作成するには：**:

1. AEMの左上隅にあるAEMロゴをタップし、左側のレールでをタップします。 **[!UICONTROL ツール/アセット/ビューアプリセット]**.

   ![viewerpresets](assets/viewerpresets.png)

1. の **[!UICONTROL ビューアプリセット]** ページで、ツールバーの **[!UICONTROL 作成]**.
1. 内 **[!UICONTROL 新しいビューアプリセット]** ダイアログボックス、 **[!UICONTROL プリセット名]** 「 」フィールドに、新しいプリセットの名前を入力します。名前は慎重に選択してください。タップした後は編集できません **[!UICONTROL 作成]**.

   後の手順でプリセットを保存すると、その名前がビューアプリセットページの **[!UICONTROL プリセットのタイトル]** 列ヘッダー。

1. の **[!UICONTROL リッチメディアタイプ]** ドロップダウンメニューで、作成するビューアプリセットのタイプを選択し、ページの右上隅にあるをタップします。 **[!UICONTROL 作成]**.

   [ビューアプリセットのリッチメディアタイプ](#rich-media-types-for-viewer-presets)を参照してください。

1. の **ビューアプリセットを編集** ページで、 **[!UICONTROL 外観]** タブをクリックします。
1. 次のいずれかの操作を行います。

   * 「**[!UICONTROL 選択したタイプ]**」プルダウンメニューで、ビジュアルデザインをカスタマイズするコンポーネントを選択します。または、設定するビジュアル要素をビューアでタップして選択することもできます。

        Visual Editor を使用すると、特定のプロパティがスタイルに与える効果を確認できます。プロパティを設定または調整するだけで、Visual Editor の左にあるサンプルを使用して、ビューア上での効果を瞬時に確認できます。

      ビューアプリセットタイプごとの CSS スタイル設定プロパティについては、「カスタマイズ」を参照してください。 *&lt;viewer_name>* Viewer」ヘルプトピック ( [ビューアリファレンスガイド](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/homeviewers.html?lang=ja).

      例えば、`Mixed_Media` タイプのビューアプリセットを作成している場合、プロパティのリストと各プロパティの説明については、[混在メディアビューアのカスタマイズ](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/mixed-media/customing-mixed-media/c-html5-mixedmedia-viewer-customizingviewer.html?lang=ja)を参照してください。

   * スタイル設定を別個の CSS ファイルで定義している場合は、その CSS ファイルを AEM Assets にアップロードできます。「**[!UICONTROL 選択したタイプ]**」プルダウンメニュー（表示するには Visual Editor を上にスクロールする必要が生じる場合があります）の下の「**[!UICONTROL CSS を読み込み]**」をタップし、アップロードした CSS ファイルを探してビューアプリセットと関連付けます。

        CSS ファイルを読み込むと、Visual Editor は、その CSS に正しいビューアマーカーが使用されているかを確認します。例えば、ズームビューアを作成している場合、読み込むすべての CSS ルールが、親のビューアエレメントに定義されているズームビューアのクラス名 `.s7mixedmediaviewer` を使用して定義されている必要があります。

      指定ビューアの CSS マーカーが正しく定義された CSS であれば、自作した任意の CSS を読み込むことができます（CSS マーカーについては、『[ビューアリファレンスガイド](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/homeviewers.html?lang=ja)』の「*&lt;viewer name>* ビューアのカスタマイズ」のヘルプトピックを参照してください。例えば、ズームビューアの CSS マーカーについては、[ズームビューアのカスタマイズ](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/zoom/customizing-zoom/c-html5-20-zoom-viewer-customizingviewer.html?lang=ja)を参照してください）。ただし、Visual Editor が一部の CSS 値を理解できないこともありえます。そのような場合、Visual Editor は、CSS が正常に機能するように、エラーを上書きしようとします。
   >[!NOTE]
   >
   >RAW 形式で CSS を直接編集する場合は、「選択したタイプ」プルダウンメニュー（表示するには Visual Editor を上にスクロールする必要が生じる場合があります）の下の「**[!UICONTROL CSS を表示／非表示]**」をタップします。****
   >
   >Visual Editor と同様に、CSS でプロパティを直接変更すると、ビューアのサンプルに対する効果を即座に確認できます。 また、ビジュアルエディターでは、同じプロパティが同時に自動的に更新されます。そのため、生の CSS エディターまたはビジュアルエディターを使用することも、両方を区別なく使用することもできます。

   >[!NOTE]
   >
   >ボタンのアートワークの場合は、2 倍の画像を選択し、高解像度のアートワークをアップロードします。 インタラクティブ画像やショッパブルバナーを操作する場合は、あらかじめ用意されている様々なホットスポットボタンから選択することもできます。

1. （オプション） **[!UICONTROL ビューアプリセットを編集]** ページ、タップ **[!UICONTROL デスクトップ]**, **[!UICONTROL タブレット]**&#x200B;または **[!UICONTROL 電話]** 異なるデバイスや画面の種類に対して表示スタイルを一意に定義する。
1. の **[!UICONTROL ビューアプリセットを編集]** ページで、 **動作** タブをクリックします。 または、設定するビジュアル要素をビューアでタップまたはクリックして選択することもできます。
1. 「**[!UICONTROL 選択したタイプ]**」プルダウンメニューで、動作を変更するコンポーネントを選択します。

   ビジュアルエディターの多くのコンポーネントには、詳細な説明が関連付けられています。これらの説明は、コンポーネントを展開して関連するパラメーターを表示したときに、青いボックス内に表示されます。

   一部のビューアタイプには、「**IS コマンド**」テキストフィールドに画像サービングコマンドを指定できるコンポーネントがあります。使用できるコマンドのリストについては、[画像サービング API リファレンス（英語）](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/c-is-home.html?lang=ja)を参照してください。

   >[!NOTE]
   >
   >**スマートフォンやタブレットなどのタッチデバイスを使用している場合**
   >
   >テキストフィールドに値を入力した後、ユーザーインターフェイスの別の場所をタップして変更を送信し、仮想キーボードを閉じます。 次をタップした場合： **[!UICONTROL 入力]**&#x200B;を呼び出した場合、アクションは発生しません。

1. ページの右上隅にある「**[!UICONTROL 保存]**」をタップします。
1. 新しいビューアプリセットを公開します。プリセットを Web サイトで使用するには、事前に公開する必要があります。

   [ビューアプリセットの公開](#publishing-viewer-presets)を参照してください。

## インタラクティブなビューアのプリセットを作成するための特別な考慮事項 {#special-considerations-for-creating-an-interactive-viewer-preset}

**パネル内の画像サムネールのディスプレイモードについて**

インタラクティブビデオのビューアプリセットを作成または編集する際に、どのビューアプリセットを選択するかを指定できます **[!UICONTROL ディスプレイモード]** 選択時に使用する設定 `InteractiveSwatches` から **[!UICONTROL 選択したコンポーネント]** 下のプルダウンメニュー **[!UICONTROL 動作]** タブをクリックします。 選択するディスプレイモードは、ビデオの再生中にサムネールを表示する方法とタイミングに影響します。`segment`ディスプレイモード（デフォルト）または `continuous` ディスプレイモードを選択できます。

| ディスプレイモード | 説明 |
|---|---|
| [!UICONTROL セグメント] | [!UICONTROL セグメント] は、既製のインタラクティブビデオビューアプリセット Shoppable_Video_light と Shoppable_Video_dark および自分で作成するすべてのインタラクティブビデオビューアプリセットのデフォルトのディスプレイモードです。 |
|  | このモードでは、ビデオセグメントに割り当てられているサムネールの数がディスプレイパネル内に表示されるスポットの数よりも少ない場合、次または前のサブセグメントがパネル内の空のスポットを満たすように引っ張り込まれることはありません。つまり、特定のビデオセグメントに割り当てられたスウォッチの表示が保持されます。 |
| [!UICONTROL 連続] | In [!UICONTROL 連続] ディスプレイモード：セグメント内のサムネールの数がパネルに表示される数より少ない場合、最後のサムネールが表示されている場合は、次のセグメントまたは前のセグメントのサムネールの表示が自動的に含まれます。 |

**インタラクティブビデオビューアの自動スクロール動作について**

インタラクティブなビデオビューアのサムネイルの自動スクロールは、選択した表示モードとは関係なく機能します。

インタラクティブビデオのビューアプリセットを作成または編集する際は、 **[!UICONTROL 自動スクロール]** から **[!UICONTROL 動作]** タブをクリックします。 **[!UICONTROL 選択したコンポーネント]**&#x200B;ドロップダウンメニューの「ビヘイビアー」タブで、「**[!UICONTROL InteractiveSwatches]**」をタップします。この **[!UICONTROL 自動スクロール]** 「IS コマンド」テキストフィールドの下にチェックボックスがリストされます。

ビューアプリセットで「**[!UICONTROL 自動スクロール」]**&#x200B;を無効（チェックボックスをオフ）にした場合、ユーザーによるビデオの再生中、パネルにはビデオの全長につき最初のサムネール画像のみが表示されます。ただし、ユーザーは必要に応じて上下の矢印アイコンを使用してサムネール間を手動でスクロールできます。

ビューアプリセットで「**[!UICONTROL 自動スクロール]**」を有効（チェックボックスをオン）にすると、ビデオの再生中、セグメントの開始時に、ビデオセグメントに割り当てられたサムネール画像まで表示がスクロールされます。ただし、セグメントによっては特定のサムネールが前後のサムネールの 2 倍の時間表示されることもあります。この動作は、セグメント内のサムネールの数がパネルに表示される数よりも多く、均等に分割できないことが原因で発生します。

例えば、30 秒のビデオセグメントが 1 つあるとします。 また、30 秒間に表示されるサムネイルは合計 9 個です。ブラウザーのサイズは、ディスプレイパネルの 4 つの位置でサムネイルが表示されるように設定されます。30 秒のビデオ時間セグメントは、3 つのサブセグメントに分割されます。 次の表に、特定の時間サブセグメントに対して表示されるサムネールの分類を示します。

| **ビデオサブセグメント** | **サブセグメントの時間（秒）** | **パネルに表示されるサムネイル** |
|---|---|---|
| 1 | 0～10 | 1、2、3、4 |
| 2 | 10～20 | 4、5、6、7 |
| 3 | 20～30 | 6、7、8、9 |

ビデオサブセグメント 3 が、割り当てられているサムネールを超えて拡張されることはありません。また、サムネール 4、6、7 は、他のサムネールの 2 倍の長さでパネルに表示されます。

ビューアが、表示できる位置の数に基づいて、パネルに表示するサムネイルの数を決定するロジックは次のとおりです。

* サブセグメントの数 = 次のサブセグメントに切り上げ（サムネールの数／サムネールパネル内に表示されるスロットの数（ブラウザー画面のサイズに基づく））

   前述の表の例では、「9 サムネール / 4 スロット = 2.25 サブセグメント」（ビューアのロジックにより 2.25 を 3 に切り上げ）になります。

* サムネールの数 = 次のサムネールに切り上げ（サムネールの数／ビデオサブセグメントの数）

   前述の表の例では、「9 サムネール / 3 ビデオサブセグメント = 3 サムネール」になります。

* サブセグメントの表示時間 = ビデオの合計再生時間／ビデオサブセグメントの数

   前述の表の例では、「30 秒 / 3 ビデオサブセグメント = 各ビデオサブセグメントで 10 秒」の再生時間になります。

### カルーセルバナーのビューアプリセットの作成に関する特別な考慮事項 {#special-considerations-for-creating-a-carousel-banner-viewer-preset}

カルーセルバナーのビューアプリセットを作成するときに、ホットスポットのスタイル変更は次のように実行できます。

|  | **説明** | **アクション** |
|---|---|---|
| **ホットスポットアイコン** | ホットスポットに使用するアイコンを変更する | ホットスポットアイコンの画像を変更するには、「**[!UICONTROL 外観]**」タブで、「**[!UICONTROL 選択したコンポーネント]**」の「**[!UICONTROL ImageMapEffect]**」をタップします。「**[!UICONTROL アイコン]**」で「**[!UICONTROL 背景]**」を選択し、「**[!UICONTROL 画像]**」フィールドで目的に背景画像に移動します。 |

## Dynamic Mediaビューアプリセットのアクティベートとアクティベート解除 {#activating-or-deactivating-viewer-presets}

ユーザーインターフェイスで使用できるビューアのプリセットは、どれがオーサーモードでアクティブになっているかによって異なります。デフォルトでは、ビューアプリセットは *オン* 作成後 プリセットをオフに切り替えた場合、オーサーモードでは表示されません。 プリセットが公開されている場合。 オン/オフを切り替えても、常に公開されます。 リストが不十分になった場合や、ビューアプリセットを使用できなくしたい場合は、ビューアプリセットを非アクティブ化できます。

**Dynamic Mediaビューアプリセットをアクティベートまたはアクティベート解除するには：**:

1. AEMの左上隅にあるAEMロゴをタップし、左側のレールでをタップします。 **[!UICONTROL ツール/アセット/ビューアプリセット]**.
1. の **[!UICONTROL ビューアプリセット]** ページの **[!UICONTROL 都道府県]** 列ヘッダーで、切り替えをタップして、ビューアプリセットをアクティベートまたはアクティベート解除します。

   アクティベートされたビューアプリセットには、右側の青いボックスに切替スイッチが表示されます。アクティベート解除されたビューアプリセットには、左側の薄いグレーのボックスに切替スイッチが表示されます。

## Dynamic Mediaビューアプリセットの公開 {#publishing-viewer-presets}

有効化（または回転） *オン*) ビューアプリセットの状態とは、Dynamic Mediaコンポーネントとインタラクティブメディアコンポーネントに、またアセットを表示する際には常に表示されることを意味します。

ただし、ビューアプリセットを使用しているアセットを配信するには、そのビューアプリセットも公開する必要があります。URL を取得したりアセットのコードを埋め込むには、すべてのビューアプリセットをアクティベートし、*かつ*&#x200B;公開する必要があります。Dynamic Media に付属しているすべての既製ビューアプリセットをアクティベートして公開する必要があります。自分で作成して追加したカスタムビューアプリセットは自動的にアクティベートされますが、やはり手動で公開する必要があります。

「[ビューアのプリセットのアクティベートとアクティベート解除](#activating-or-deactivating-viewer-presets)」を参照してください。

「[アセットのプレビュー](previewing-assets.md)」も参照してください。

**Dynamic Mediaビューアプリセットを公開するには：**:

1. AEMの左上隅にあるAEMロゴをタップし、左側のレールでをタップします。 **[!UICONTROL ツール/アセット/ビューアプリセット]**.
1. 公開するビューアプリセットを 1 つ以上選択します。
1. ツールバーで、 **[!UICONTROL 公開]** アイコン

## Dynamic Mediaビューアプリセットの並べ替え {#sorting-viewer-presets}

**Dynamic Mediaビューアプリセットを並べ替えるには：**:

1. AEM の左上隅にある AEM ロゴをタップし、左側のパネルで&#x200B;**ツール**（ハンマーアイコン）／**[!UICONTROL Assets／ビューアプリセット]**&#x200B;をタップします。
1. 「**[!UICONTROL プリセットのタイトル]**」、「**[!UICONTROL タイプ]**」、「**[!UICONTROL 公開]**」または「**[!UICONTROL 状態]**」をクリックして、その見出しの列でソートします。例えば、「**[!UICONTROL タイプ]**」をクリックすると、ビューアプリセットのタイプが、アルファベット順で、またはアルファベットの逆の順序でソートされます。

## Dynamic Mediaビューアプリセットの編集 {#editing-viewer-presets}

*事前に定義された標準提供ビューアプリセット*&#x200B;を編集するシナリオはサポートされていません。標準提供ビューアプリセットを編集すると、新しい名前で保存するように指示されます。

**Dynamic Mediaビューアプリセットを編集するには：**:

1. AEMの左上隅にあるAEMロゴをタップし、左側のレールでをタップします。 **[!UICONTROL ツール/アセット/ビューアプリセット]**.
1. ビューアプリセットのタイトルの左側にあるチェックボックスをオンにして、プリセットを選択します。
1. ツールバーの「**[!UICONTROL 編集]**」をタップします。
1. の **[!UICONTROL ビューアプリセットを編集]** ページで、必要な変更をビューアプリセットに加えます。
1. 次のいずれかの操作を行います。

   * 「**[!UICONTROL 保存]**」をタップして変更内容を保存し、ビューアプリセットページに戻ります。****
   * 「**[!UICONTROL キャンセル]**」をタップして変更内容をキャンセルし、ビューアプリセットページに戻ります。****

## カスタムDynamic Mediaビューアプリセットの削除 {#deleting-custom-viewer-presets}

作成して Dynamic Media に追加したビューアプリセットを削除できます。

**カスタムDynamic Mediaビューアプリセットを削除するには：**:

1. AEMの左上隅にあるAEMロゴをタップし、左側のレールでをタップします。 **[!UICONTROL ツール/アセット/ビューアプリセット]**.
1. の **[!UICONTROL ビューアプリセット]** ページ、チェック **[!UICONTROL プリセットのタイトル]**&#x200B;次に、 **[!UICONTROL ごみ箱]** アイコン
1. 「**[!UICONTROL 削除]**」をタップします。

## アセットへの Dynamic Media ビューアプリセットの適用 {#applying-a-viewer-preset-to-an-asset}

アセットと選択したビューアを既に公開している場合は、ビューアプリセットの選択後に「**[!UICONTROL URL]**」ボタンと「**[!UICONTROL 埋め込み]**」ボタンが表示されます。

**アセットにDynamic Mediaビューアプリセットを適用するには：**:

1. アセットを開き、ページの左上隅付近にあるドロップダウンメニュータップして、「**[!UICONTROL ビューア]**」を選択します。

   >[!NOTE]
   >
   >アセットと選択したビューアを既に公開している場合は、ビューアプリセットの選択後に「**[!UICONTROL URL]**」ボタンと「**[!UICONTROL 埋め込み]**」ボタンが表示されます。

1. 左側のウィンドウからビューアプリセットを選択して、アセットに適用します。

   [この URL をコピー](linking-urls-to-yourwebapplication.md)して、他のユーザーと共有できます。

## Dynamic Mediaビューアプリセットを使用するアセットの配信 {#delivering-assets-with-viewer-presets}

ビューアプリセットの URL を取得する方法については、[Web アプリケーションへの URL のリンク](linking-urls-to-yourwebapplication.md)を参照してください。[Web ページへのビデオビューアの埋め込み](embed-code.md)も参照してください。

AEMを WCM として使用している場合は、ページ上でビューアプリセットを使用してアセットを直接追加できます。 [ページへの Dynamic Media アセットの追加](adding-dynamic-media-assets-to-pages.md)を参照してください。
