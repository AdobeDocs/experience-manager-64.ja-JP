---
title: ページへのダイナミックメディアクラシック機能の追加
seo-title: ページへのダイナミックメディアクラシック機能の追加
description: Adobe Dynamic Media Classicは、リッチメディアアセットを管理、拡張、公開、およびWeb、モバイル、電子メールおよびインターネットに接続されたディスプレイや印刷に配信するためのホストソリューションです。
seo-description: Adobe Dynamic Media Classicは、リッチメディアアセットを管理、拡張、公開、およびWeb、モバイル、電子メールおよびインターネットに接続されたディスプレイや印刷に配信するためのホストソリューションです。
uuid: 66b9c150-c482-4a41-9772-fa39c135802c
contentOwner: Alva Ware-Bevacqui
products: SG_EXPERIENCEMANAGER/6.4/ASSETS
topic-tags: authoring
content-type: reference
discoiquuid: 9ba95dce-a801-4a36-8798-45d295371b1b
translation-type: tm+mt
source-git-commit: ea520d6a1b714a21f2b3aeb36932a50d958bd162

---


# ページへのダイナミックメディアクラシック機能の追加{#adding-scene-features-to-your-page}

[Adobe Dynamic Media Classicは](https://help.adobe.com/en_US/scene7/using/WS26AB0D9A-F51C-464e-88C8-580A5A82F810.html) 、Web、モバイル、電子メールおよびインターネットに接続されたディスプレイや印刷でリッチメディアアセットを管理、拡張、公開、配信するためのホストソリューションです。

Dynamic Media Classicで公開されたAEMアセットは、様々なビューアで表示できます。

* ズーム
* フライアウト
* ビデオ
* 画像テンプレート
* 画像

デジタルアセットは、AEMからDynamic Media Classicに直接公開したり、Dynamic Media ClassicからAEMに公開したりできます。

ここでは、デジタルアセットをAEMからDynamic Media Classicに公開する方法と、その逆の方法について説明します。 また、ビューアについても詳しく説明します。AEMをダイナミックメディアクラシック用に設定する方法について詳しくは、『ダイナミ [ックメディアクラシックとAEMの連携』を参照してください](/help/sites-administering/scene7.md)。

[画像マップの追加](/help/assets/image-maps.md)も参照してください。

AEM でのビデオコンポーネントの使用について詳しくは、以下を参照してください。

* [ビデオ](/help/sites-classic-ui-authoring/manage-assets-classic-s7-video.md)

>[!NOTE]
>
>If Dynamic Media Classic assets do not display properly, make sure that Dynamic media is [disabled](/help/assets/config-dynamic.md#disabling-dynamic-media) and then refresh the page.

## アセットからダイナミックメディアクラシックへの手動公開 {#manually-publishing-to-scene-from-assets}

デジタルアセットは、クラシックUIのアセットコンソールから、またはアセットから直接、Dynamic Media Classicに公開できます。

>[!NOTE]
>
>AEMは、Dynamic Media Classicに非同期で公開します。 After you click **[!UICONTROL Publish]**, it may take several seconds for your asset to publish to Dynamic Media Classic.


### アセットコンソールからの公開 {#publishing-from-the-assets-console}

アセットがダイナミックメディアクラシックのターゲットフォルダーにある場合に、アセットコンソールからダイナミックメディアクラシックに公開するには：

1. In the AEM classic UI, click **[!UICONTROL Digital Assets]** to access the digital asset manager.

1. Select the asset (or assets) or folder from within the target folder you want to publish to Dynamic Media Classic and right-click and select **[!UICONTROL Publish to Dynamic Media Classic]**. または、**ツールメニ **[!UICONTROL ューから「ダイナミックメディアクラシック]** 」を選択[!UICONTROL できます] 。

   ![chlimage_1-76](assets/chlimage_1-76.png)

1. Dynamic Media Classicに移動し、アセットが使用可能であることを確認します。

   >[!NOTE]
   >
   >If the assets are not in a Dynamic Media Classic synchronized folder, **[!UICONTROL Publish to Dynamic Media Classic]** in both menus is visible but disabled.

### アセットからの公開 {#publishing-from-an-asset}

同期したDynamic Media Classicフォルダー内にアセットがある限り、手動でアセットを公開できます。

>[!NOTE]
>
>アセットがダイナミックメディアクラシック同期フォルダー内にない場合、「ダイナミックメディ **[!UICONTROL アクラシックに公開]** 」へのリンクは使用できません。

**デジタルアセットから直接Dynamic Media Classicに公開するには**:

1. AEM で、「**[!UICONTROL デジタルアセット]**」をクリックして、Digital Asset Manager にアクセスします。

1. アセットをダブルクリックして開きます。

1. アセットの詳細ペインで、「ダイナミック **[!UICONTROL メディアクラシックに公開」を選択します]**。

   ![screen_shot_2012-02-22at34828pm](assets/screen_shot_2012-02-22at34828pm.png)

1. **[!UICONTROL リンクが「発行中」]**&#x200B;に変わります。その後公 **[!UICONTROL 開]**。 Dynamic Media Classicに移動し、アセットが使用可能であることを確認します。

   >[!NOTE]
   >
   >If the asset does not publish properly to Dynamic Media Classic, the link changes to **[!UICONTROL Publishing Failed]**. アセットが既にダイナミックメディアクラシックに公開されている場合、リンクには「ダ **[!UICONTROL イナミックメディアクラシックに再公開]**」と表示されます。 再公開を使用すると、AEM内のアセットに変更を加えて再公開できます。

### Publishing assets from outside the CQ target folder {#publishing-assets-from-outside-the-cq-target-folder}

アセットは、Dynamic Media Classicのターゲットフォルダー内のアセットからのみ、Dynamic Media Classicに公開することをお勧めします。 However, if you need to upload assets from a folder outside of the target folder, you can still do that by uploading them to an *ad-hoc* folder on Dynamic Media Classic.

これを行うには、アセットを表示するページのクラウド設定を指定します。 次に、ページにDynamic Media Classicコンポーネントを追加し、コンポーネントにアセットをドラッグ&amp;ドロップします。 After the page properties are set for that page, a **[!UICONTROL Publish to Dynamic Media Classic]** link appears that when selected triggers uploading to Dynamic Media Classic.

>[!NOTE]
>
>アドホックフォルダー内のアセットは、Dynamic Media Classicコンテンツブラウザーに表示されません。

**CQターゲットフォルダー外にあるアセットを発行するには**:

1. In AEM in the classic UI, click **[!UICONTROL Websites]** and navigate to the web page that you want to add a digital asset to that is not yet published to Dynamic Media Classic. （通常のページ継承ルールが適用されます）。

1. In the sidekick, click the **[!UICONTROL Page]** icon, then click **[!UICONTROL Page Properties]**.

1. [!UICONTROL **Cloud Services/サービスを追加/Dynamic Media Classic(Scene7)をクリックします**。
1. 「Adobe Dynamic Media Classic」ドロップダウンリストで、必要な設定を選択し、「 **[!UICONTROL OK」をクリックします]**。

   ![chlimage_1-77](assets/chlimage_1-77.png)

1. Webページ上で、Dynamic Media Classic(Scene7)コンポーネントをページ上の目的の場所に追加します。
1. コンテンツファインダーから、デジタルアセットをコンポーネントにドラッグします。 [ダイナミックメディアクラシッ **[!UICONTROL クのパブリケーション状態の確認]**]リンク

   >[!NOTE]
   >
   >デジタルアセットがCQターゲットフォルダーにある場合、「ダイナミックメディアクラシックパブリケーション **[!UICONTROL ステータスを確認」へのリンクは表示されません]** 。 アセットは、単にコンポーネント内に配置されます。

   ![chlimage_1-78](assets/chlimage_1-78.png)

1. 「ダイナミ **[!UICONTROL ックMedia Classicのパブリケーション状態を確認]**」をクリックします。 アセットが公開されていない場合、AEMはアセットをダイナミックメディアクラシックに公開します。 アップロードされたアセットは、アドホックフォルダーに配置されます。By default, the ad-hoc folder is located in the `name_of_the_company/CQ5_adhoc`. [必要に応じて、この場所を設定](#configuringtheadhocfolder)できます。

   >[!NOTE]
   >
   >アセットがダイナミックメディアクラシック同期フォルダー内になく、現在のページに関連付けられたダイナミックメディアクラシッククラウド設定がない場合、アップロードは失敗します。

## ダイナミックメディアクラシック(Scene7)コンポーネント {#scene-components}

AEMでは、次のダイナミックメディアクラシックコンポーネントを使用できます。

* ズーム
* フライアウト（ズーム）
* 画像テンプレート
* 画像
* ビデオ

>[!NOTE]
>
>These components are not available by default and need to be selected in **[!UICONTROL Design]** mode before using.

After they are made available in **[!UICONTROL Design]** mode, you can add the components to your page like any other AEM component. まだDynamic Media Classicに公開されていないアセットは、同期したフォルダー内、ページ上、またはDynamic Media Classicクラウド設定で公開される場合、Dynamic Media Classicに公開されます。

### Flash viewers end-of-life notice {#flash-viewers-end-of-life-notice}

2017年1月31日より、Adobe Dynamic Media ClassicはFlashビューアプラットフォームのサポートを正式に終了しました。

For more information about this important change, see [Flash viewer end-of-life FAQs](https://docs.adobe.com/content/docs/en/aem/6-1/administer/integration/marketing-cloud/scene7/flash-eol.html).

### Adding a Dynamic Media Classic component to a page {#adding-a-scene-component-to-a-page}

ダイナミックメディアクラシックコンポーネントをページに追加するのと、コンポーネントをページに追加するのと同じです。 ダイナミックMedia Classicコンポーネントについては、以下の節で詳しく説明します。

**Dynamic Media Classicコンポーネント/ビューアをクラシックUIのページに追加するには**:

1. AEMで、ダイナミックメディアクラシックコンポーネントを追加するページを開きます。

1. If no Dynamic Media Classic components are available, click the ruler in the sidekick to enter **[!UICONTROL Design]** mode, click **[!UICONTROL Edit]** parsys, and select all the **[!UICONTROL Dynamic Media Classic]** components to make them available.

1. Return to **[!UICONTROL Edit]** mode by clicking the pencil in the sidekick.

1. Drag a component from the **[!UICONTROL Dynamic Media Classic]** group in the sidekick onto the page in the desired location.

1. 「**[!UICONTROL 編集]**」をクリックしてコンポーネントを開きます。

1. コンポーネントの編集を必要に応じておこない、「**[!UICONTROL OK]**」をクリックして変更内容を保存します。

### レスポンシブ Web サイトへのインタラクティブな表示エクスペリエンスの追加 {#adding-interactive-viewing-experiences-to-a-responsive-website}

アセットのレスポンシブデザインとは、アセットが表示される場所に適応することを意味します。レスポンシブデザインでは、同じアセットが複数のデバイスで効果的に表示されます。

**クラシックUIでレスポンシブサイトにインタラクティブな表示エクスペリエンスを追加するには**:

1. Log in to AEM, and ensure that you have [configured Adobe Dynamic Media Classic Cloud Services](/help/sites-administering/scene7.md#configuring-scene-integration) and that Dynamic Media Classic components are available.

   >[!NOTE]
   >
   >Dynamic Media Classic WCMコンポーネントが使用できない場合は、**[!UICONTROL Design] モードを使用して有効にする必要があります。

1. In a website with the Dynamic Media Classic components enabled, drag an **[!UICONTROL Image]** viewer to the page.
1. Edit the component and adjust the breakpoints in the **[!UICONTROL Dynamic Media Classic Settings]** tab.

   ![chlimage_1-79](assets/chlimage_1-79.png)

1. ビューアがレスポンシブにサイズ変更され、すべてのインタラクションがデスクトップ、タブレットおよびモバイル用に最適化されていることを確認します。

### すべてのDynamic Media Classicコンポーネントに共通の設定 {#settings-common-to-all-scene-components}

設定オプションは異なりますが、すべてのDynamic Media Classicコンポーネントに共通のものを次に示します。

* **[!UICONTROL ファイル参照]**- 参照するファイルを探します。ファイル参照は、アセットのURLを表示します。URLコマンドとパラメーターを含む完全なダイナミックメディアクラシックURLとは限りません。 このフィールドには、Dynamic Media Classic URLのコマンドとパラメーターを追加できません。 それらは、コンポーネントの対応する機能を使用して追加する必要があります。
* **[!UICONTROL 幅]** - 幅を設定できます。
* **[!UICONTROL 高さ]** - 高さを設定できます。

You set these configuration options by double-clicking a Dynamic Media Classic component, for example, when you open a **[!UICONTROL Zoom]** component:

![chlimage_1-80](assets/chlimage_1-80.png)

### ズーム {#zoom}

HTML5 ズームコンポーネントでは、+ ボタンをクリックすると画像のサイズが拡大されます。

アセットの下部にはズームツールが用意されています。拡大するには「**[!UICONTROL +]** 」、縮小するには「**[!UICONTROL -]**」をクリックします。Clicking **[!UICONTROL x]** or the reset zoom arrow brings the image back to the original size it was imported as. 全画面表示にするには、斜め矢印をクリックします。コンポーネントを設定するには、「**[!UICONTROL 編集]**」をクリックします。With this component, you can configure [settings common to all Dynamic Media Classic components](#settings-common-to-all-scene-components).

![](do-not-localize/chlimage_1-5.png)

### Flyout {#flyout}

HTML5 フライアウトコンポーネントでは、アセットが分割画面として表示されます。左側には、アセットが指定されたサイズで表示され、右側には、ズーム部分が表示されます。コンポーネントを設定するには、「**[!UICONTROL 編集]**」をクリックします。With this component, you can configure [settings common to all Dynamic Media Classic components](/help/sites-administering/scene7.md#settingscommontoalldynamicmediaclassiccomponents).

>[!NOTE]
>
>フライアウトコンポーネントでカスタムサイズを使用する場合は、そのカスタムサイズが使用され、コンポーネントのレスポンシブ設定は無効になります。
>
>If your Flyout component uses the default size, as set in the [!UICONTROL Design] view, then the default size is used and the component stretches to accomodate the page layout size with responsive setup of the component enabled. Be aware, however, that there is a limitation on responsive setup of the component. When the you use the Flyout component with responsive setup, you should not use it with full page stretch. Otherwise, the Flyout may extend beyond the page&#39;s right border.

![chlimage_1-81](assets/chlimage_1-81.png)

### 画像 {#image}

ダイナミックメディアクラシック画像コンポーネントを使用すると、ダイナミックメディアクラシック修飾子、画像またはビューアプリセット、シャープなどのダイナミックメディアクラシック機能を画像に追加できます。 ダイナミックメディアクラシック画像コンポーネントは、AEMの特別なダイナミックメディアクラシック機能を備えた他の画像コンポーネントと似ています。 この例では、画像にダイナミックメディアクラシックURL修飾子が適用されて `&op_invert=1` います。

![](do-not-localize/chlimage_1-6.png)

**[!UICONTROL タイトル、代替テキスト]** - 「詳細」タブ [!UICONTROL で] 、画像にタイトルを追加し、グラフィックをオフにしているユーザーの代替テキストを追加します。

**[!UICONTROL URL、開く場所]** — からリンクを開くアセットを設定できます。 Set the **[!UICONTROL URL]** and **[!UICONTROL Open in]** to indicate whether you want it to open in the same window or a new window.

![chlimage_1-82](assets/chlimage_1-82.png)

**[!UICONTROL ビューアプリセット]** — ドロップダウンメニューから既存のビューアプリセットを選択します。 探しているビューアプリセットが表示されない場合は、表示できるように設定する必要があります。詳しくは、[ビューアプリセットの管理](/help/assets/managing-viewer-presets.md)を参照してください。画像プリセットを使用している場合は、ビューアプリセットを選択できません。逆の場合も同様です。

**[!UICONTROL Dynamic Media Classic Configuration]** - Scene7 Publishing systemからアクティブな画像プリセットを取得する際に使用するDynamic Media Classic設定を選択します。

**[!UICONTROL 画像プリセット]** — ドロップダウンメニューから既存の画像プリセットを選択します。 探している画像プリセットが表示されない場合は、表示できるように設定する必要があります。[画像プリセットの管理](/help/assets/managing-image-presets.md)を参照してください。画像プリセットを使用している場合は、ビューアプリセットを選択できません。逆の場合も同様です。

**[!UICONTROL 出力形式]** — 画像の出力形式（jpegなど）を選択します。 選択する出力形式によっては、追加の設定オプションが表示される場合があります。[画像プリセットの管理](/help/assets/managing-image-presets.md)を参照してください。

**[!UICONTROL シャープ]** — 画像にシャープを適用する方法を選択します。 シャープの適用について詳しくは、 [*Adobe Dynamic Media Classicの画質とシャープのベストプラクティスを参照してください&#x200B;*](/help/assets/assets/s7_sharpening_images.pdf)。

**[!UICONTROL URL修飾子]** — 追加のDynamic Media Classic画像コマンドを指定して、画像効果を変更できます。 These are described in [Managing Image Presets](/help/assets/managing-image-presets.md) and the [Command reference](https://marketing.adobe.com/resources/help/en_US/s7/is_ir_api/is_api/http_ref/c_command_reference.html).

**[!UICONTROL ブレークポイント]** - webサイトがレスポンシブな場合は、ブレークポイントを調整する必要があります。 Breakpoints must be separated by commas `,`.

### 画像テンプレート {#image-template}

[Dynamic Media Classic画像テンプレートは](https://help.adobe.com/en_US/scene7/using/WS60B68844-9054-4099-BF69-3DC998A04D3C.html) 、Dynamic Media Classicに読み込まれたPhotoshopのレイヤーコンテンツです。コンテンツとプロパティは可変性を考慮してパラメータ化されていました。 **[!UICONTROL 画像テンプレート]**&#x200B;コンポーネントを使用すると、画像を読み込んで、テキストを AEM で動的に変更できます。また、ClientContext の値を使用するように&#x200B;**[!UICONTROL 画像テンプレート]**&#x200B;コンポーネントを設定できます。これにより、各ユーザーが個別に画像を活用できます。

コンポーネントを設定するには、「**[!UICONTROL 編集]**」をクリックします。You can configure [settings common to all Dynamic Media Classic components](/help/sites-administering/scene7.md#settingscommontoalldynamicmediaclassicscomponents) as well as other settings described in this section.

![chlimage_1-83](assets/chlimage_1-83.png)

**[!UICONTROL ファイル参照、幅、高さ]** — すべてのDynamic Media Classicコンポーネントに共通の設定を参照してください。

>[!NOTE]
>
>ダイナミックMedia Classic URLコマンドとパラメーターをファイル参照URLに直接追加することはできません。 これらは、**[!UICONTROL パラメーター]**&#x200B;パネルのコンポーネントの UI でのみ定義できます。

**[!UICONTROL タイトル、代替テキスト]** 「ダイナミック [!UICONTROL メディアクラシック画像テンプレート] 」タブで、画像にタイトルを追加し、グラフィックをオフにしたユーザ用の代替テキストを追加します。

**[!UICONTROL URL、開く場所]** ：リンクを開くアセットの場所を設定できます。 「**[!UICONTROL URL]**」と「**[!UICONTROL 次のウィンドウで開く]**」で、同じウィンドウで開くか新しいウィンドウで開くかを指定します。

![chlimage_1-84](assets/chlimage_1-84.png)

**[!UICONTROL パラメータパネル]** ：画像を読み込むときに、画像からの情報がパラメータに事前入力されます。 動的に変更できるコンテンツがない場合、このウィンドウは空になります。

![chlimage_1-85](assets/chlimage_1-85.png)

#### テキストの動的な変更 {#changing-text-dynamically}

テキストを動的に変更するには、新しいテキストをフィールドに入力して、「**[!UICONTROL OK]**」をクリックします。この例では、「**[!UICONTROL 価格]**」が $50 で、送料が 99 セントです。

![chlimage_1-86](assets/chlimage_1-86.png)

画像内のテキストが変更されます。フィールドの横にある「**[!UICONTROL リセット]**」をクリックすると、テキストを元の値に戻すことができます。

![chlimage_1-87](assets/chlimage_1-87.png)

#### ClientContext の値を反映したテキストの変更 {#changing-text-to-reflect-the-value-of-a-client-context-value}

To link a field to a client context value, click **[!UICONTROL Select]** to open the client-context menu, select the client context, and click **[!UICONTROL OK]**. In this example, the name changes based on linking the Name with the formatted name in the profile.

![chlimage_1-88](assets/chlimage_1-88.png)

現在ログインしているユーザーの名前がテキストに反映されます。フィールドの横にある「**[!UICONTROL リセット]**」をクリックすると、テキストを元の値に戻すことができます。

![chlimage_1-89](assets/chlimage_1-89.png)

#### ダイナミックメディアクラシック画像テンプレートをリンクにする {#making-the-scene-image-template-a-link}

**ダイナミックメディアクラシック画像テンプレートをリンクにするには**:

1. On the page with the Dynamic Media Classic image template component, click **[!UICONTROL Edit]**.
1. 「**[!UICONTROL URL]**」フィールドに、ユーザーが画像をクリックしたときに表示される URL を入力します。「**[!UICONTROL 次のウィンドウで開く]**」フィールドで、ターゲットを新しいウィンドウと同じウィンドウのどちらで開くかを選択します。

   ![chlimage_1-90](assets/chlimage_1-90.png)

1. 「**[!UICONTROL OK]**」をクリックします。

### ビデオコンポーネント {#video-component}

The Dynamic Media Classic **[!UICONTROL Video]** component (available from the Dynamic Media Classic section of the sidekick) uses device and bandwidth detection to serve the right video to each screen. このコンポーネントは HTML5 ビデオプレーヤー（チャネルを超えて使用可能な単一のビューア）です。

このコンポーネントはアダプティブビデオセット（単一の MP4 ビデオまたは単一の F4V ビデオ）で使用できます。

See [Video](/help/sites-classic-ui-authoring/manage-assets-classic-s7-video.md) for more information on how videos work with Dynamic Media Classic integration. In addition, see how [the **Dynamic Media Classic video** component compares to the foundation **video** component](/help/sites-classic-ui-authoring/manage-assets-classic-s7-video.md).

![chlimage_1-91](assets/chlimage_1-91.png)

### ビデオコンポーネントに関する既知の制限事項 {#known-limitations-for-the-video-component}

マスタービデオがアップロードされると、Adobe DAM および WCM が表示されます。次に示すプロキシアセットは表示されません。

* Dynamic Media Classicのエンコードされたレンディション
* ダイナミックMedia Classicアダプティブビデオセット

ダイナミックメディアクラシックビデオコンポーネントでアダプティブビデオセットを使用する場合は、ビデオのサイズに合わせてコンポーネントのサイズを変更する必要があります。

## Dynamic Media Classicコンテンツブラウザー {#scene-content-browser}

Dynamic Media Classicコンテンツブラウザーを使用すると、Dynamic Media ClassicのコンテンツをAEMで直接表示できます。 To access the content browser, in the Content Finder, select **[!UICONTROL Dynamic Media Classic]** in the touch-optimized user interface or the **[!UICONTROL S7]** icon in the classic user interface. どちらの UI を使用しても機能は同じです。

設定が複数ある場合、AEM では既定で[デフォルト設定](/help/sites-administering/scene7.md#configuring-a-default-configuration)が表示されます。ドロップダウンメニューのDynamic Media Classicコンテンツブラウザーで、異なる設定を直接選択できます。

>[!NOTE]
>
>* アドホックフォルダー内のアセットは、Dynamic Media Classicコンテンツブラウザーに表示されません。
>* セキュ [アプレビューを有効にすると](/help/sites-administering/scene7.md#configuring-the-state-published-unpublished-of-assets-pushed-to-scene)、Dynamic Media Classicの公開済みアセットと未公開アセットの両方がDynamic Media Classicコンテンツブラウザーに表示されます。
>* If you do not see **[!UICONTROL Dynamic Media Classic]** or the **[!UICONTROL S7]** icon as an option in the content browser, you need to [configure Dynamic Media Classic to work with AEM](/help/sites-administering/scene7.md).
   >
   >
* ビデオの場合、Dynamic Media Classicコンテンツブラウザーは次の機能をサポートします。
   >
   >
* アダプティブビデオセット：複数の画面でシームレスに再生するために必要なすべてのビデオレンディションのコンテナ
>* 単一の MP4 ビデオ
>* 単一の F4V ビデオ


### クラシック UI でのコンテンツの参照 {#browsing-content-in-the-classic-ui}

Dynamic Media Classicの「 **[!UICONTROL S7]** 」タブをクリックして、コンテンツを参照します。

アクセスしている設定は、設定を選択して変更できます。 フォルダーは、選択した設定に応じて変わります。

![chlimage_1-92](assets/chlimage_1-92.png)

アセット用のコンテンツファインダーと同様に、アセットを検索して、結果にフィルターを適用できます。ただし、アセットファインダーとは異なり、「**[!UICONTROL S7]**」タブでキーワードを入力すると、そのキーワードが&#x200B;*含まれる*&#x200B;ファイル名ではなく、入力した文字列&#x200B;*で始まる*&#x200B;ファイル名が検索されます。

デフォルトでは、アセットはファイル名で表示されます。結果をアセットタイプでフィルタリングすることもできます。

>[!NOTE]
>
>ビデオの場合、WCMのダイナミックメディアクラシックコンテンツブラウザーは次の機能をサポートします。
>
>* アダプティブビデオセット：複数の画面でシームレスに再生するために必要なすべてのビデオレンディションのコンテナ
>* 単一の MP4 ビデオ
>* 単一の F4V ビデオ
>



### コンテンツブラウザーでのダイナミックメディアクラシックアセットの検索 {#searching-for-scene-assets-with-the-content-browser}

ダイナミックメディアクラシックアセットの検索は、AEMアセットの検索と似ていますが、実際に検索すると、AEMに直接読み込むのではなく、Dynamic Media Classicシステムでアセットのリモートビューが表示される点が異なります。

クラシック UI またはタッチ操作向け UI を使用して、アセットを表示および検索できます。インターフェイスによって検索方法は多少異なります。

どちらの UI で検索する場合でも、次の基準でフィルターを適用できます（ここでは、タッチ操作向け UI を示しています）。

**[!UICONTROL キーワードの入力]** — アセットを名前で検索できます。 検索時には、入力したキーワードで始まるファイル名が検索されます。例えば、「swimming」という単語を入力すると、入力した順序どおりの文字列で始まるアセットファイルの名前が検索されます。アセットを検索するには、語句を入力した後に Enter キーを押してください。

![chlimage_1-93](assets/chlimage_1-93.png)

**[!UICONTROL Folder/path]** — 表示されるフォルダーの名前は、選択した設定に基づきます。 下位にドリルダウンするには、フォルダーアイコンをクリックしてサブフォルダーを選択し、チェックマークをクリックして選択します。

キーワードを入力してフォルダーを選択すると、AEM ではそのフォルダーがとすべてのサブフォルダーが検索されます。ただし、検索時にキーワードを入力しない場合は、フォルダーを選択してもそのフォルダー内のアセットしか表示されず、サブフォルダーは含まれません。

デフォルトでは、AEM は、選択したフォルダーとすべてのサブフォルダーを検索します。

![chlimage_1-94](assets/chlimage_1-94.png)

**[!UICONTROL アセットのタイプ]** 「ダイナミックメディアクラシック」を選択して、ダイナミックメディアクラシックコンテンツを参照します。 このオプションは、既にダイナミックメディアクラシックを設定している場合にのみ使用できます。

![chlimage_1-95](assets/chlimage_1-95.png)

**[!UICONTROL 設定]** : [!UICONTROL Cloud Servicesで定義された複数のDynamic Media Classic設定がある場合は]、ここで選択できます。 そのため、選択した設定に基づいてフォルダーが変わります。

![chlimage_1-96](assets/chlimage_1-96.png)

**[!UICONTROL アセットタイプ]** Dynamic Media Classicブラウザー内で、結果をフィルタリングして次のいずれかを含めることができます。画像、テンプレート、ビデオおよびアダプティブビデオセット。 アセットタイプを選択しない場合、AEM ではデフォルトですべてのアセットタイプが検索されます。

![chlimage_1-97](assets/chlimage_1-97.png)

>[!NOTE]
>
>* ビデオを検索するときは、単一のレンディションが検索されています。結果は、元のレンディション（&amp;ast;.mp4のみ）とエンコードされたレンディションを返します。
>* アダプティブビデオセットを検索する場合、検索対象のフォルダとすべてのサブフォルダは検索されますが、検索にキーワードを追加した場合にのみ検索が行われます。 キーワードを追加しない場合、AEM はサブフォルダーを検索しません。
>



**[!UICONTROL 公開ステータス]** ：公開ステータスに基づいてアセットをフィルタリングできます。公開済み [!UICONTROL /未公] 開 。 If you do not select any [!UICONTROL Publish status], AEM by default searches all publish statuses.

![chlimage_1-98](assets/chlimage_1-98.png)

