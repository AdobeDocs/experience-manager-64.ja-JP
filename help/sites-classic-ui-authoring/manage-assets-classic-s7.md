---
title: ページへのDynamic Media Classic機能の追加
seo-title: ページへのDynamic Media Classic機能の追加
description: AdobeDynamic Media Classicは、Web、モバイル、Eメールおよびインターネットに接続されたディスプレイと印刷を管理、強化、公開、および配信するためのホストソリューションです。
seo-description: AdobeDynamic Media Classicは、Web、モバイル、Eメールおよびインターネットに接続されたディスプレイと印刷を管理、強化、公開、および配信するためのホストソリューションです。
uuid: 66b9c150-c482-4a41-9772-fa39c135802c
contentOwner: Alva Ware-Bevacqui
products: SG_EXPERIENCEMANAGER/6.4/ASSETS
topic-tags: authoring
content-type: reference
discoiquuid: 9ba95dce-a801-4a36-8798-45d295371b1b
exl-id: 93921d23-a2bf-43b6-b002-58a7482b22b0
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '3381'
ht-degree: 30%

---

# Dynamic Media Classic機能のページへの追加{#adding-scene-features-to-your-page}

AdobeDynamic Media Classicは、Web、モバイル、Eメールおよびインターネットに接続されたディスプレイと印刷を管理、強化、公開、および配信するためのホストソリューションです。

Dynamic Media Classicで公開されたAEMアセットは、様々なビューアで表示できます。

* ズーム
* フライアウト
* ビデオ
* 画像テンプレート
* 画像

デジタルアセットをAEMからDynamic Media Classicに直接公開したり、Dynamic Media ClassicからAEMに公開したりできます。

この節では、AEMからDynamic Media Classicにデジタルアセットを公開する方法と、その逆の方法について説明します。 また、ビューアについても詳しく説明します。AEM for Dynamic Media Classicの設定について詳しくは、[Dynamic Media ClassicとAEM](/help/sites-administering/scene7.md)の統合を参照してください。

[画像マップの追加](/help/assets/image-maps.md)も参照してください。

AEM でのビデオコンポーネントの使用について詳しくは、以下を参照してください。

* [ビデオ](/help/sites-classic-ui-authoring/manage-assets-classic-s7-video.md)

>[!NOTE]
>
>Dynamic Media Classicのアセットが正しく表示されない場合は、Dynamic Mediaが[無効](/help/assets/config-dynamic.md#disabling-dynamic-media)であることを確認してから、ページを更新します。

## AssetsからDynamic Media Classicへの手動公開{#manually-publishing-to-scene-from-assets}

クラシックUIのAssetsコンソールから、またはDynamic Media Classicから直接、デジタルアセットを公開できます。

>[!NOTE]
>
>AEMはDynamic Media Classicに非同期で公開します。 「**[!UICONTROL 公開]**」をクリックした後、アセットがDynamic Media Classicに公開されるまでに数秒かかる場合があります。


### アセットコンソールからの公開 {#publishing-from-the-assets-console}

アセットがDynamic Media Classicのターゲットフォルダーにある場合に、AssetsコンソールからDynamic Media Classicに公開するには：

1. AEMクラシックUIで、「**[!UICONTROL デジタルアセット]**」をクリックして、Digital Asset Managerにアクセスします。

1. Dynamic Media Classicに公開するターゲットフォルダー内からアセットまたはフォルダーを選択し、右クリックして「**[!UICONTROL Dynamic Media Classicに公開]**」を選択します。 または、**[!UICONTROL ツール]**&#x200B;メニューから「**[!UICONTROL Dynamic Media Classicに公開]**」を選択します。

   ![chlimage_1-76](assets/chlimage_1-76.png)

1. Dynamic Media Classicに移動し、アセットが使用可能であることを確認します。

   >[!NOTE]
   >
   >アセットがDynamic Media Classic同期フォルダーにない場合は、両方のメニューの「 **[!UICONTROL Dynamic Media Classicに公開]** 」が表示されますが、無効になっています。

### アセットからの公開 {#publishing-from-an-asset}

同期されたDynamic Media Classicフォルダー内にアセットがある限り、手動でアセットを公開できます。

>[!NOTE]
>
>同期されたDynamic Media Classicフォルダーにアセットがない場合、「 **[!UICONTROL Dynamic Media Classicに公開]** 」へのリンクは使用できません。

**デジタルアセットからDynamic Media Classicに直接公開するには**:

1. AEM で、「**[!UICONTROL デジタルアセット]**」をクリックして、Digital Asset Manager にアクセスします。

1. アセットをダブルクリックして開きます。

1. アセットの詳細ウィンドウで、「**[!UICONTROL Dynamic Media Classicに公開]**」を選択します。

   ![screen_shot_2012-02-22at34828pm](assets/screen_shot_2012-02-22at34828pm.png)

1. リンクが「**[!UICONTROL 公開中…」に変わります。]**&#x200B;に続いて&#x200B;**[!UICONTROL 公開済み]**。 Dynamic Media Classicに移動し、アセットが使用可能であることを確認します。

   >[!NOTE]
   >
   >アセットがDynamic Media Classicに適切に公開されない場合、リンクは「**[!UICONTROL 公開失敗]**」に変わります。 アセットが既にDynamic Media Classicに公開されている場合、リンクは「**[!UICONTROL Dynamic Media Classicに再公開]**」となります。 再公開を使用すると、AEM内のアセットに変更を加えて再公開できます。

### CQターゲットフォルダー{#publishing-assets-from-outside-the-cq-target-folder}外からのアセットの公開

Adobeでは、Dynamic Media Classicターゲットフォルダー内のアセットからのみDynamic Media Classicにアセットを公開することをお勧めします。 ただし、ターゲットフォルダー以外のフォルダーからアセットをアップロードする必要がある場合は、Dynamic Media Classicの&#x200B;*アドホック*&#x200B;フォルダーにアセットをアップロードすることで、アセットをアップロードできます。

これをおこなうには、アセットを表示するページのクラウド設定を指定します。 次に、Dynamic Media Classicコンポーネントをページに追加し、そのコンポーネントにアセットをドラッグ&amp;ドロップします。 そのページのトリガーを設定した後、Dynamic Media Classicにアップロードするページを選択すると、「Dynamic Media Classicに公開&#x200B;]**」リンクが表示されます。**[!UICONTROL 

>[!NOTE]
>
>アドホックフォルダー内のアセットは、Dynamic Media Classicコンテンツブラウザーには表示されません。

**CQターゲットフォルダーの外部にあるアセットを公開するには**:

1. クラシックUIのAEMで、「**[!UICONTROL Webサイト]**」をクリックし、Dynamic Media Classicにまだ公開されていないデジタルアセットを追加するWebページに移動します。 （通常のページ継承ルールが適用されます）。

1. サイドキックで、**[!UICONTROL ページ]**&#x200B;アイコンをクリックし、**[!UICONTROL ページのプロパティ]**&#x200B;をクリックします。

1. **[!UICONTROL Cloud Services] / [!UICONTROL サービスを追加] / [!UICONTROL Dynamic Media Classic(Scene7)]**&#x200B;をクリックします。
1. 「Dynamic Media ClassicのAdobe」ドロップダウンリストで目的の設定を選択し、「**[!UICONTROL OK]**」をクリックします。

   ![chlimage_1-77](assets/chlimage_1-77.png)

1. Webページで、Dynamic Media Classic(Scene7)コンポーネントをページ上の目的の場所に追加します。
1. コンテンツファインダーから、デジタルアセットをコンポーネントにドラッグします。 **[!UICONTROL Dynamic Media Classic公開ステータスの確認]**&#x200B;へのリンクが表示されます。

   >[!NOTE]
   >
   >デジタルアセットがCQターゲットフォルダー内にある場合、**[!UICONTROL Dynamic Media Classic公開ステータスを確認]**&#x200B;するリンクは表示されません。 アセットは、単にコンポーネント内に配置されます。

   ![chlimage_1-78](assets/chlimage_1-78.png)

1. 「**[!UICONTROL Dynamic Media Classic公開ステータス]**」をクリックします。 アセットが公開されていない場合、AEMはアセットをDynamic Media Classicに公開します。 アップロードされたアセットは、アドホックフォルダーに配置されます。デフォルトでは、アドホックフォルダーは`name_of_the_company/CQ5_adhoc`にあります。 [必要に応じて、この場所を設定](#configuringtheadhocfolder)できます。

   >[!NOTE]
   >
   >アセットがDynamic Media Classicの同期済みフォルダーになく、現在のページに関連付けられているDynamic Media Classicクラウド設定がない場合、アップロードは失敗します。

## Dynamic Media Classic(Scene7)コンポーネント{#scene-components}

AEMでは、次のDynamic Media Classicコンポーネントを使用できます。

* ズーム
* フライアウト（ズーム）
* 画像テンプレート
* 画像
* ビデオ

>[!NOTE]
>
>これらのコンポーネントはデフォルトでは使用できないので、使用する前に&#x200B;**[!UICONTROL デザイン]**&#x200B;モードで選択する必要があります。

**[!UICONTROL デザイン]**&#x200B;モードで使用可能になったら、他のAEMコンポーネントと同様に、コンポーネントをページに追加できます。 まだDynamic Media Classicに公開されていないアセットは、同期されたフォルダー内、ページ上、またはDynamic Media Classicクラウド設定を使用している場合、Dynamic Media Classicに公開されます。

### Flashビューアのサポート終了に関する通知{#flash-viewers-end-of-life-notice}

2017年1月31日に、AdobeDynamic Media ClassicはFlashビューアプラットフォームのサポートを正式に終了しました。

### Dynamic Media Classicコンポーネントのページへの追加{#adding-a-scene-component-to-a-page}

Dynamic Media Classicコンポーネントをページに追加する操作は、任意のページにコンポーネントを追加する操作と同じです。 Dynamic Media Classicコンポーネントについて、以降の節で詳しく説明します。

**Dynamic Media Classicコンポーネント/ビューアをクラシックUIのページに追加するには**:

1. AEMで、Dynamic Media Classicコンポーネントを追加するページを開きます。

1. 使用可能なDynamic Media Classicコンポーネントがない場合は、サイドキックのルーラーをクリックして&#x200B;**[!UICONTROL デザイン]**&#x200B;モードに切り替え、**[!UICONTROL 編集]** parsysをクリックし、すべての&#x200B;**[!UICONTROL Dynamic Media Classic]**&#x200B;コンポーネントを選択して使用可能にします。

1. サイドキックの鉛筆アイコンをクリックして、**[!UICONTROL 編集]**&#x200B;モードに戻ります。

1. サイドキックの&#x200B;**[!UICONTROL Dynamic Media Classic]**&#x200B;グループからページの目的の場所にコンポーネントをドラッグします。

1. 「**[!UICONTROL 編集]**」をクリックしてコンポーネントを開きます。

1. コンポーネントの編集を必要に応じておこない、「**[!UICONTROL OK]**」をクリックして変更内容を保存します。

### レスポンシブ Web サイトへのインタラクティブな表示エクスペリエンスの追加  {#adding-interactive-viewing-experiences-to-a-responsive-website}

アセットのレスポンシブデザインとは、アセットが表示される場所に適応することを意味します。レスポンシブデザインでは、同じアセットが複数のデバイスで効果的に表示されます。

**クラシックUIでレスポンシブサイトにインタラクティブな表示エクスペリエンスを追加するには**:

1. AEMにログインし、[AdobeDynamic Media ClassicCloud Services](/help/sites-administering/scene7.md#configuring-scene-integration)が設定され、Dynamic Media Classicコンポーネントが使用可能であることを確認します。

   >[!NOTE]
   >
   >Dynamic Media Classic WCMコンポーネントを使用できない場合は、必ず**[!UICONTROL デザイン]モードを使用して有効にしてください。

1. Dynamic Media Classicコンポーネントが有効なWebサイトで、**[!UICONTROL 画像]**&#x200B;ビューアをページにドラッグします。
1. コンポーネントを編集し、「**[!UICONTROL Dynamic Media Classic設定]**」タブでブレークポイントを調整します。

   ![chlimage_1-79](assets/chlimage_1-79.png)

1. ビューアがレスポンシブにサイズ変更され、すべてのインタラクションがデスクトップ、タブレットおよびモバイル用に最適化されていることを確認します。

### すべてのDynamic Media Classicコンポーネントに共通の設定{#settings-common-to-all-scene-components}

設定オプションは異なりますが、次の操作はDynamic Media Classicのすべてのコンポーネントに共通です。

* **[!UICONTROL ファイル参照]**- 参照するファイルを探します。ファイル参照は、アセットのURLを表示しますが、必ずしもURLコマンドやパラメーターを含む完全なDynamic Media Classic URLとは限りません。 このフィールドにDynamic Media Classic URLコマンドおよびパラメーターを追加することはできません。 それらは、コンポーネントの対応する機能を使用して追加する必要があります。
* **[!UICONTROL 幅]** - 幅を設定できます。
* **[!UICONTROL 高さ]** - 高さを設定できます。

これらの設定オプションを設定するには、例えば&#x200B;**[!UICONTROL ズーム]**&#x200B;コンポーネントを開く際に、Dynamic Media Classicコンポーネントをダブルクリックします。

![chlimage_1-80](assets/chlimage_1-80.png)

### ズーム {#zoom}

HTML5 ズームコンポーネントでは、+ ボタンをクリックすると画像のサイズが拡大されます。

アセットの下部にはズームツールが用意されています。拡大するには「**[!UICONTROL +]** 」、縮小するには「**[!UICONTROL -]**」をクリックします。**[!UICONTROL x]**&#x200B;をクリックするか、ズームのリセット矢印をクリックすると、画像が元のサイズに戻ります。 全画面表示にするには、斜め矢印をクリックします。コンポーネントを設定するには、「**[!UICONTROL 編集]**」をクリックします。このコンポーネントを使用すると、すべてのDynamic Media Classicコンポーネント](#settings-common-to-all-scene-components)に共通の[設定を構成できます。

![](do-not-localize/chlimage_1-5.png)

### フライアウト {#flyout}

HTML5 フライアウトコンポーネントでは、アセットが分割画面として表示されます。左側には、アセットが指定されたサイズで表示され、右側には、ズーム部分が表示されます。コンポーネントを設定するには、「**[!UICONTROL 編集]**」をクリックします。このコンポーネントを使用すると、すべてのDynamic Media Classicコンポーネント](/help/sites-administering/scene7.md#settingscommontoalldynamicmediaclassiccomponents)に共通の[設定を構成できます。

>[!NOTE]
>
>フライアウトコンポーネントでカスタムサイズを使用する場合は、そのカスタムサイズが使用され、コンポーネントのレスポンシブ設定は無効になります。
>
>[!UICONTROL デザイン]ビューで設定されたデフォルトサイズをフライアウトコンポーネントで使用する場合は、デフォルトサイズが使用され、コンポーネントが拡大されて、コンポーネントのレスポンシブ設定に合わせてページレイアウトサイズが調整されます。ただし、コンポーネントのレスポンシブ設定には制限があることに注意してください。レスポンシブ設定でフライアウトコンポーネントを使用する場合は、ページ全体を拡大して使用しないでください。そうしないと、フライアウトがページの右の境界線を超えて広がる場合があります。

![chlimage_1-81](assets/chlimage_1-81.png)

### 画像 {#image}

Dynamic Media Classicの画像コンポーネントを使用すると、Dynamic Media Classicの修飾子、画像またはビューアプリセット、シャープニングなどの機能を画像に追加できます。 Dynamic Media Classicの画像コンポーネントは、AEMの他の画像コンポーネントに似ており、特別なDynamic Media Classic機能が備わっています。 この例では、画像にDynamic Media Classic URL修飾子`&op_invert=1`が適用されています。

![](do-not-localize/chlimage_1-6.png)

**[!UICONTROL タイトル、代替テキスト]**  - 「詳細設  定」タブで、グラフィックの表示をオフにしているユーザー向けのタイトルと代替テキストを画像に追加します。

**[!UICONTROL URL、次のウィンドウで開く]**  — からアセットを設定して、リンクを開くことができます。**[!UICONTROL URL]**&#x200B;と&#x200B;**[!UICONTROL Open in]**&#x200B;を設定して、同じウィンドウで開くか、新しいウィンドウで開くかを指定します。

![chlimage_1-82](assets/chlimage_1-82.png)

**[!UICONTROL ビューアプリセット]**  — ドロップダウンメニューから既存のビューアプリセットを選択します。探しているビューアプリセットが表示されない場合は、表示できるように設定する必要があります。詳しくは、[ビューアプリセットの管理](/help/assets/managing-viewer-presets.md)を参照してください。画像プリセットを使用している場合は、ビューアプリセットを選択できません。逆の場合も同様です。

**[!UICONTROL Dynamic Media Classic設定]**  - Scene7 Publishing Systemからアクティブな画像プリセットを取得するために使用するDynamic Media Classic設定を選択します。

**[!UICONTROL 画像プリセット]**  — ドロップダウンメニューから既存の画像プリセットを選択します。探している画像プリセットが表示されない場合は、表示できるように設定する必要があります。[画像プリセットの管理](/help/assets/managing-image-presets.md)を参照してください。画像プリセットを使用している場合は、ビューアプリセットを選択できません。逆の場合も同様です。

**[!UICONTROL 出力形式]**  — 画像の出力形式（例：jpeg）を選択します。選択する出力形式によっては、追加の設定オプションが表示される場合があります。[画像プリセットの管理](/help/assets/managing-image-presets.md)を参照してください。

**[!UICONTROL シャープ]**  — 画像にシャープを適用する方法を選択します。シャープニングについて詳しくは、[*Dynamic Media ClassicのAdobe画質とシャープニングのベストプラクティス*](/help/assets/assets/sharpening_images.pdf)&#x200B;を参照してください。

**[!UICONTROL URL修飾子]**  — 追加のDynamic Media Classic画像コマンドを指定して、画像効果を変更できます。これらは、[画像プリセットの管理](/help/assets/managing-image-presets.md)および[コマンドリファレンス](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/c-command-reference.html)で説明します。

**[!UICONTROL ブレークポイント]**  - Webサイトがレスポンシブな場合は、ブレークポイントを調整する必要があります。ブレークポイントはコンマ`,`で区切る必要があります。

### 画像テンプレート {#image-template}

[Dynamic Media Classic Image Templates](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/template-basics/quick-start-template-basics.html#template-basics) は、Dynamic Media Classicに読み込まれたPhotoshopコンテンツのレイヤーです。コンテンツとプロパティは、可変性を考慮してパラメーター化されています。**[!UICONTROL 画像テンプレート]**&#x200B;コンポーネントを使用すると、；画像を読み込み、AEMでテキストを動的に変更できます。 また、ClientContext の値を使用するように&#x200B;**[!UICONTROL 画像テンプレート]**&#x200B;コンポーネントを設定できます。これにより、各ユーザーが個別に画像を活用できます。

コンポーネントを設定するには、「**[!UICONTROL 編集]**」をクリックします。すべてのDynamic Media Classicコンポーネント](/help/sites-administering/scene7.md#settingscommontoalldynamicmediaclassicscomponents)に共通の[設定や、この節で説明するその他の設定を構成できます。

![chlimage_1-83](assets/chlimage_1-83.png)

**[!UICONTROL ファイル参照、幅、高さ]**  — すべてのDynamic Media Classicコンポーネントに共通の設定を参照してください。

>[!NOTE]
>
>Dynamic Media Classic URLのコマンドとパラメーターは、ファイル参照URLに直接追加できません。 これらは、**[!UICONTROL パラメーター]**&#x200B;パネルのコンポーネントの UI でのみ定義できます。

**[!UICONTROL タイトル、代替テキ]** スト [!UICONTROL Dynamic Media Classic画像テンプレー] トタブで、画像にタイトルを追加し、グラフィックの表示をオフにしているユーザー向けの代替テキストを追加します。

**[!UICONTROL URL、開く：リ]** ンクを開く元のアセットを設定できます。「**[!UICONTROL URL]**」と「**[!UICONTROL 次のウィンドウで開く]**」で、同じウィンドウで開くか新しいウィンドウで開くかを指定します。

![chlimage_1-84](assets/chlimage_1-84.png)

**[!UICONTROL パラメ]** ータPanel画像を読み込むと、画像からの情報があらかじめパラメータに設定されます。動的に変更できるコンテンツがない場合、このウィンドウは空になります。

![chlimage_1-85](assets/chlimage_1-85.png)

#### テキストの動的な変更 {#changing-text-dynamically}

テキストを動的に変更するには、新しいテキストをフィールドに入力して、「**[!UICONTROL OK]**」をクリックします。この例では、「**[!UICONTROL 価格]**」が $50 で、送料が 99 セントです。

![chlimage_1-86](assets/chlimage_1-86.png)

画像内のテキストが変更されます。フィールドの横にある「**[!UICONTROL リセット]**」をクリックすると、テキストを元の値に戻すことができます。

![chlimage_1-87](assets/chlimage_1-87.png)

#### ClientContext の値を反映したテキストの変更 {#changing-text-to-reflect-the-value-of-a-client-context-value}

フィールドをClientContext値にリンクするには、**[!UICONTROL 「]**&#x200B;を選択」をクリックしてClientContextメニューを開き、ClientContextを選択して「**[!UICONTROL OK]**」をクリックします。この例では、名前は、名前とプロファイル内の形式設定された名前のリンクに基づいて変更されます。

![chlimage_1-88](assets/chlimage_1-88.png)

現在ログインしているユーザーの名前がテキストに反映されます。フィールドの横にある「**[!UICONTROL リセット]**」をクリックすると、テキストを元の値に戻すことができます。

![chlimage_1-89](assets/chlimage_1-89.png)

#### Dynamic Media Classic画像テンプレートをリンクにする{#making-the-scene-image-template-a-link}

**Dynamic Media Classic画像テンプレートをリンクにするには**:

1. Dynamic Media Classic画像テンプレートコンポーネントを含むページで、「**[!UICONTROL 編集]**」をクリックします。
1. 「**[!UICONTROL URL]**」フィールドに、ユーザーが画像をクリックしたときに表示される URL を入力します。「**[!UICONTROL 次のウィンドウで開く]**」フィールドで、ターゲットを新しいウィンドウと同じウィンドウのどちらで開くかを選択します。

   ![chlimage_1-90](assets/chlimage_1-90.png)

1. 「**[!UICONTROL OK]**」をクリックします。

### ビデオコンポーネント {#video-component}

Dynamic Media Classicの&#x200B;**[!UICONTROL ビデオ]**&#x200B;コンポーネント(サイドキックのDynamic Media Classicセクションから利用可能)は、デバイスと帯域幅の検出を使用して、適切なビデオを各画面に提供します。 このコンポーネントは HTML5 ビデオプレーヤー（チャネルを超えて使用可能な単一のビューア）です。

このコンポーネントはアダプティブビデオセット（単一の MP4 ビデオまたは単一の F4V ビデオ）で使用できます。

ビデオとDynamic Media Classicの統合の連携について詳しくは、[ビデオ](/help/sites-classic-ui-authoring/manage-assets-classic-s7-video.md)を参照してください。 また、[**Dynamic Media Classicビデオ**&#x200B;コンポーネントと基盤&#x200B;**ビデオ**&#x200B;コンポーネント](/help/sites-classic-ui-authoring/manage-assets-classic-s7-video.md)との比較を参照してください。

![chlimage_1-91](assets/chlimage_1-91.png)

### ビデオコンポーネントに関する既知の制限事項 {#known-limitations-for-the-video-component}

マスタービデオがアップロードされると、Adobe DAM および WCM が表示されます。次に示すプロキシアセットは表示されません。

* Dynamic Media Classicのエンコードされたレンディション
* Dynamic Media Classicアダプティブビデオセット

Dynamic Media Classicビデオコンポーネントでアダプティブビデオセットを使用する場合は、ビデオのサイズに合わせてコンポーネントのサイズを変更する必要があります。

## Dynamic Media Classicコンテンツブラウザー{#scene-content-browser}

Dynamic Media Classicコンテンツブラウザーを使用すると、Dynamic Media ClassicのコンテンツをAEMで直接表示できます。 コンテンツブラウザーにアクセスするには、コンテンツファインダーで、タッチ操作向けUIの&#x200B;**[!UICONTROL Dynamic Media Classic]**&#x200B;またはクラシックUIの&#x200B;**[!UICONTROL S7]**&#x200B;アイコンを選択します。 どちらの UI を使用しても機能は同じです。

設定が複数ある場合、AEM では既定で[デフォルト設定](/help/sites-administering/scene7.md#configuring-a-default-configuration)が表示されます。Dynamic Media Classicのコンテンツブラウザーのドロップダウンメニューで、様々な設定を直接選択できます。

>[!NOTE]
>
>* アドホックフォルダー内のアセットは、Dynamic Media Classicコンテンツブラウザーに表示されません。
>* [セキュアプレビューを有効にすると](/help/sites-administering/scene7.md#configuring-the-state-published-unpublished-of-assets-pushed-to-scene)、Dynamic Media Classicで公開済みと非公開の両方のアセットがDynamic Media Classicコンテンツブラウザーに表示されます。
>* コンテンツブラウザーで&#x200B;**[!UICONTROL Dynamic Media Classic]**&#x200B;や&#x200B;**[!UICONTROL S7]**&#x200B;アイコンがオプションとして表示されない場合は、AEM](/help/sites-administering/scene7.md)と連携するように[Dynamic Media Classicを設定する必要があります。

   >
   >
* ビデオの場合、Dynamic Media Classicコンテンツブラウザーは次の機能をサポートしています。
   >
   >
* アダプティブビデオセット：複数の画面でシームレスに再生するために必要なすべてのビデオレンディションのコンテナ
>* 単一の MP4 ビデオ
>* 単一の F4V ビデオ


### クラシック UI でのコンテンツの参照 {#browsing-content-in-the-classic-ui}

Dynamic Media Classicで「**[!UICONTROL S7]**」タブをクリックして、コンテンツを参照します。

アクセスする設定を変更するには、設定を選択します。 フォルダーは、選択した設定に応じて変わります。

![chlimage_1-92](assets/chlimage_1-92.png)

アセット用のコンテンツファインダーと同様に、アセットを検索して、結果にフィルターを適用できます。ただし、アセットファインダーとは異なり、「**[!UICONTROL S7]**」タブでキーワードを入力すると、そのキーワードが&#x200B;*含まれる*&#x200B;ファイル名ではなく、入力した文字列&#x200B;*で始まる*&#x200B;ファイル名が検索されます。

デフォルトでは、アセットはファイル名で表示されます。結果をアセットタイプでフィルタリングすることもできます。

>[!NOTE]
>
>ビデオの場合、WCMのDynamic Media Classicコンテンツブラウザーは次の機能をサポートしています。
>
>* アダプティブビデオセット：複数の画面でシームレスに再生するために必要なすべてのビデオレンディションのコンテナ
>* 単一の MP4 ビデオ
>* 単一の F4V ビデオ

>



### コンテンツブラウザー{#searching-for-scene-assets-with-the-content-browser}でのDynamic Media Classicアセットの検索

Dynamic Media Classicアセットの検索は、AEMアセットの検索と似ていますが、検索時に、実際にはAEMに直接読み込むのではなく、Dynamic Media Classicシステムにアセットのリモート表示が表示される点が異なります。

クラシック UI またはタッチ操作向け UI を使用して、アセットを表示および検索できます。インターフェイスによって検索方法は多少異なります。

どちらの UI で検索する場合でも、次の基準でフィルターを適用できます（ここでは、タッチ操作向け UI を示しています）。

**[!UICONTROL キーワードを入力]**  — アセットを名前で検索できます。検索時には、入力したキーワードで始まるファイル名が検索されます。例えば、「swimming」という単語を入力すると、入力した順序どおりの文字列で始まるアセットファイルの名前が検索されます。アセットを検索するには、語句を入力した後に Enter キーを押してください。

![chlimage_1-93](assets/chlimage_1-93.png)

**[!UICONTROL フォルダー/パス]**  — 表示されるフォルダーの名前は、選択した設定に基づきます。下位にドリルダウンするには、フォルダーアイコンをクリックしてサブフォルダーを選択し、チェックマークをクリックして選択します。

キーワードを入力してフォルダーを選択すると、AEM ではそのフォルダーがとすべてのサブフォルダーが検索されます。ただし、検索時にキーワードを入力しない場合は、フォルダーを選択してもそのフォルダー内のアセットしか表示されず、サブフォルダーは含まれません。

デフォルトでは、AEM は、選択したフォルダーとすべてのサブフォルダーを検索します。

![chlimage_1-94](assets/chlimage_1-94.png)

**[!UICONTROL AssetのタイプAssetSelect]** Dynamic Media Classicを選択してDynamic Media Classicコンテンツを参照します。このオプションは、Dynamic Media Classicを既に設定している場合にのみ使用できます。

![chlimage_1-95](assets/chlimage_1-95.png)

**** 設定 [!UICONTROL Cloud Services]で複数のDynamic Media Classic設定を定義している場合は、ここで選択できます。そのため、選択した設定に基づいてフォルダーが変わります。

![chlimage_1-96](assets/chlimage_1-96.png)

**[!UICONTROL アセッ]** トタイプDynamic Media Classicブラウザーでは、結果をフィルタリングして、次のいずれかを含めることができます。画像、テンプレート、ビデオおよびアダプティブビデオセットを参照してください。アセットタイプを選択しない場合、AEM ではデフォルトですべてのアセットタイプが検索されます。

![chlimage_1-97](assets/chlimage_1-97.png)

>[!NOTE]
>
>* ビデオを検索するときは、単一のレンディションが検索されています。結果は、元のレンディション（&amp;ast;.mp4のみ）とエンコードされたレンディションを返します。
>* アダプティブビデオセットを検索する場合、検索対象のフォルダーとすべてのサブフォルダーは、検索にキーワードを追加した場合にのみ検索されます。 キーワードを追加しない場合、AEM はサブフォルダーを検索しません。

>



**[!UICONTROL 公開ステ]** ータス公開ステータスに基づいてアセットをフィルタリングできます。  公開または非 [!UICONTROL 公開]。[!UICONTROL 公開ステータス]を選択しない場合、AEMはデフォルトですべての公開ステータスを検索します。

![chlimage_1-98](assets/chlimage_1-98.png)
