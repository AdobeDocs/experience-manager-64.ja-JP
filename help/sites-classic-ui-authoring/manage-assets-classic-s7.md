---
title: ページへの Dynamic Media Classic 機能の追加
seo-title: Adding Dynamic Media Classic features to your page
description: Adobe Dynamic Media Classic は、リッチメディアアセットの管理や拡張のほか、web、モバイル、電子メールをはじめインターネットに接続されたディスプレイやプリンターにリッチメディアアセットを公開および提供したりするためのホスト型ソリューションです。
seo-description: Adobe Dynamic Media Classic is a hosted solution for managing, enhancing, publishing, and delivering rich media assets to Web, mobile, email, and Internet-connected displays and print.
uuid: 66b9c150-c482-4a41-9772-fa39c135802c
contentOwner: Alva Ware-Bevacqui
products: SG_EXPERIENCEMANAGER/6.4/ASSETS
topic-tags: authoring
content-type: reference
discoiquuid: 9ba95dce-a801-4a36-8798-45d295371b1b
exl-id: 93921d23-a2bf-43b6-b002-58a7482b22b0
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '3347'
ht-degree: 50%

---

# ページへの Dynamic Media Classic 機能の追加{#adding-scene-features-to-your-page}

Adobe Dynamic Media Classic は、リッチメディアアセットの管理や拡張のほか、web、モバイル、電子メールをはじめインターネットに接続されたディスプレイやプリンターにリッチメディアアセットを公開および提供したりするためのホスト型ソリューションです。

Dynamic Media Classicで公開されたAEMアセットは、様々なビューアで表示できます。

* ズーム
* フライアウト
* ビデオ
* 画像テンプレート
* 画像

デジタルアセットをAEMからDynamic Media Classicに直接公開したり、デジタルアセットをDynamic Media ClassicからAEMに公開したりできます。

この節では、デジタルアセットをAEMからDynamic Media Classicに公開する方法と、その逆の方法について説明します。 また、ビューアについても詳しく説明します。AEM for Dynamic Media Classicの設定について詳しくは、 [Dynamic Media ClassicとAEMの統合](/help/sites-administering/scene7.md).

[画像マップの追加](/help/assets/image-maps.md)も参照してください。

AEM でのビデオコンポーネントの使用について詳しくは、以下を参照してください。

* [ビデオ](/help/sites-classic-ui-authoring/manage-assets-classic-s7-video.md)

>[!NOTE]
>
>Dynamic Media Classicのアセットが正しく表示されない場合は、Dynamic Media が [無効](/help/assets/config-dynamic.md#disabling-dynamic-media) ページを更新します。

## Assets からDynamic Media Classicへの手動公開 {#manually-publishing-to-scene-from-assets}

クラシック UI の Assets コンソールから、またはDynamic Media Classicから直接、デジタルアセットをに公開できます。

>[!NOTE]
>
>AEMはDynamic Media Classicに非同期で公開します。 次をクリックした後： **[!UICONTROL 公開]**( アセットがDynamic Media Classicに公開されるまで数秒かかる場合があります )。

### Assets コンソールからの公開 {#publishing-from-the-assets-console}

アセットがDynamic Media Classicのターゲットフォルダー内にある場合に、アセットコンソールからDynamic Media Classicに公開するには：

1. AEMクラシック UI で、 **[!UICONTROL デジタルアセット]** digital asset manager にアクセスする

1. Dynamic Media Classicに公開するターゲットフォルダー内からアセット（またはアセット）またはフォルダーを選択し、右クリックして「 」を選択します。 **[!UICONTROL Dynamic Media Classicに公開]**. または、 **[!UICONTROL Dynamic Media Classicに公開]** から **[!UICONTROL ツール]** メニュー

   ![chlimage_1-76](assets/chlimage_1-76.png)

1. Dynamic Media Classicに移動し、アセットが使用可能であることを確認します。

   >[!NOTE]
   >
   >アセットがDynamic Media Classicの同期済みフォルダーにない場合、 **[!UICONTROL Dynamic Media Classicに公開]** は、どちらのメニューも表示されますが、無効です。

### アセットからの公開 {#publishing-from-an-asset}

同期されたDynamic Media Classicフォルダー内にアセットがある限り、手動でアセットを公開できます。

>[!NOTE]
>
>同期されたDynamic Media Classicフォルダーにアセットがない場合、へのリンク **[!UICONTROL Dynamic Media Classicに公開]** は使用できません。

**デジタルアセットからDynamic Media Classicに直接公開するには**:

1. AEM で、「**[!UICONTROL デジタルアセット]**」をクリックして、Digital Asset Manager にアクセスします。

1. アセットをダブルクリックして開きます。

1. アセットの詳細ウィンドウで、「 」を選択します。 **[!UICONTROL Dynamic Media Classicに公開]**.

   ![screen_shot_2012-02-22at34828pm](assets/screen_shot_2012-02-22at34828pm.png)

1. リンクが「**[!UICONTROL 公開中…]**」となった後、「**[!UICONTROL 公開済み]**」に変わります。Dynamic Media Classicに移動し、アセットが使用可能であることを確認します。

   >[!NOTE]
   >
   >アセットがDynamic Media Classicに正しく公開されない場合、リンクはに変わります。 **[!UICONTROL 公開に失敗しました]**. アセットが既にDynamic Media Classicに公開されている場合、リンクは次のようになります。 **[!UICONTROL Dynamic Media Classicに再公開]**. 再公開を使用すると、AEM内のアセットに変更を加えて再公開できます。

### CQ のターゲットフォルダー外からのアセットの公開 {#publishing-assets-from-outside-the-cq-target-folder}

Adobeでは、Dynamic Media Classicのターゲットフォルダー内のアセットからのみDynamic Media Classicにアセットを公開することをお勧めします。 ただし、ターゲットフォルダー以外のフォルダーからアセットをアップロードする必要がある場合は、アセットを *アドホック* Dynamic Media Classicのフォルダー。

これをおこなうには、アセットを表示するページのクラウド設定を指定します。 次に、ページにDynamic Media Classicコンポーネントを追加し、そのコンポーネントにアセットをドラッグ&amp;ドロップします。 そのページのページプロパティを設定した後、 **[!UICONTROL Dynamic Media Classicに公開]** 「Dynamic Media Classicにアップロード中のトリガー」を選択すると、このリンクが表示されます。

>[!NOTE]
>
>アドホックフォルダー内のアセットは、Dynamic Media Classicコンテンツブラウザーに表示されません。

**CQ ターゲットフォルダーの外部に存在するアセットを公開するには**:

1. クラシック UI のAEMで、 **[!UICONTROL Web サイト]** まだDynamic Media Classicに公開されていないデジタルアセットを追加する Web ページに移動します。 （通常のページ継承ルールが適用されます）。

1. サイドキックで、 **[!UICONTROL ページ]** アイコンをクリックし、 **[!UICONTROL ページプロパティ]**.

1. クリック **[!UICONTROL Cloud Services] > [!UICONTROL サービスを追加] > [!UICONTROL Dynamic Media Classic(Scene7)]**.
1. 「 Adobe Dynamic Media Classic 」ドロップダウンリストで、目的の設定を選択し、「 **[!UICONTROL OK]**.

   ![chlimage_1-77](assets/chlimage_1-77.png)

1. Web ページで、ページの目的の場所に Dynamic Media Classic（Scene7）コンポーネントを追加します。
1. コンテンツファインダーから、デジタルアセットをコンポーネントにドラッグします。 次へのリンクが表示されます： **[!UICONTROL Dynamic Media Classic Publication ステータスの確認]**.

   >[!NOTE]
   >
   >デジタルアセットが CQ ターゲットフォルダー内にある場合、 **[!UICONTROL Dynamic Media Classic Publication ステータスの確認]** が表示されます。 アセットは、単にコンポーネント内に配置されるだけです。

   ![chlimage_1-78](assets/chlimage_1-78.png)

1. クリック **[!UICONTROL Dynamic Media Classic Publication ステータスの確認]**. アセットが公開されていない場合、AEMはアセットをDynamic Media Classicに公開します。 アップロードされたアセットは、アドホックフォルダーに配置されます。デフォルトでは、アドホックフォルダーは、 `name_of_the_company/CQ5_adhoc`. [必要に応じて、この場所を設定](#configuringtheadhocfolder)できます。

   >[!NOTE]
   >
   >アセットがDynamic Media Classicの同期されたフォルダーになく、現在のページにDynamic Media Classicクラウド設定が関連付けられていない場合、アップロードは失敗します。

## Dynamic Media Classic (Scene7) コンポーネント {#scene-components}

AEMでは、次のDynamic Media Classicコンポーネントを使用できます。

* ズーム
* フライアウト（ズーム）
* 画像テンプレート
* 画像
* ビデオ

>[!NOTE]
>
>これらのコンポーネントはデフォルトでは使用できないので、で選択する必要があります。 **[!UICONTROL デザイン]** モードを使用してください。

これらが **[!UICONTROL デザイン]** モードでは、他のAEMコンポーネントと同様に、コンポーネントをページに追加できます。 同期済みフォルダー内、ページ上、または Dynamic Media Classic クラウド設定を使用している場合、まだ Dynamic Media Classic に公開されていないアセットは Dynamic Media Classic に公開されます。

### Flashビューアのサポート終了に関する通知 {#flash-viewers-end-of-life-notice}

2017 年 1 月 31 日、Adobe Dynamic Media ClassicはFlashビューアプラットフォームのサポートを正式に終了しました。

### ページへのDynamic Media Classicコンポーネントの追加 {#adding-a-scene-component-to-a-page}

Dynamic Media Classicコンポーネントをページに追加する操作は、任意のページにコンポーネントを追加する操作と同じです。 Dynamic Media Classic コンポーネントについて、以降の節で詳しく説明します。

**クラシック UI でDynamic Media Classicコンポーネント/ビューアをページに追加するには**:

1. AEMで、Dynamic Media Classicコンポーネントを追加するページを開きます。

1. 使用可能なDynamic Media Classicコンポーネントがない場合は、サイドキックのルーラーをクリックして、 **[!UICONTROL デザイン]** モード、クリック **[!UICONTROL 編集]** parsys を選択し、 **[!UICONTROL Dynamic Media Classic]** コンポーネントを使用できるようにします。

1. 戻る **[!UICONTROL 編集]** モードを切り替えるには、サイドキックの鉛筆アイコンをクリックします。

1. コンポーネントを **[!UICONTROL Dynamic Media Classic]** を、目的の場所のページ上にサイドキックでグループ化します。

1. 「**[!UICONTROL 編集]**」をクリックしてコンポーネントを開きます。

1. コンポーネントの編集を必要に応じておこない、「**[!UICONTROL OK]**」をクリックして変更内容を保存します。

### レスポンシブ Web サイトへのインタラクティブな表示エクスペリエンスの追加 {#adding-interactive-viewing-experiences-to-a-responsive-website}

アセットのレスポンシブデザインとは、アセットが表示される場所に適応することを意味します。レスポンシブデザインでは、同じアセットを複数のデバイスで効果的に表示できます。

**クラシック UI でレスポンシブサイトにインタラクティブな表示エクスペリエンスを追加するには**:

1. AEMにログインし、 [設定済みのAdobe Dynamic Media ClassicCloud Services](/help/sites-administering/scene7.md#configuring-scene-integration) Dynamic Media Classicコンポーネントを使用できます。

   >[!NOTE]
   >
   >Dynamic Media Classic WCM コンポーネントを使用できない場合は、必ず[!UICONTROL デザイン] モード。

1. Web サイトで、Dynamic Media Classicコンポーネントを有効にして、 **[!UICONTROL 画像]** 閲覧者をページに追加します。
1. コンポーネントを編集し、 **[!UICONTROL Dynamic Media Classic Settings]** タブをクリックします。

   ![chlimage_1-79](assets/chlimage_1-79.png)

1. ビューアがレスポンシブにサイズ変更され、すべてのインタラクションがデスクトップ、タブレットおよびモバイル用に最適化されていることを確認します。

### すべての Dynamic Media Classic コンポーネントに共通の設定 {#settings-common-to-all-scene-components}

様々な設定オプションがありますが、次のオプションはすべての Dynamic Media Classic コンポーネントに共通です。

* **[!UICONTROL ファイル参照]** - 参照するファイルを探します。ファイル参照には、アセットの URL が表示されます。これは必ずしも、URL コマンドおよびパラメーターを含む Dynamic Media Classic の完全な URL ではありません。このフィールドに Dynamic Media Classic の URL コマンドおよびパラメーターを追加することはできません。それらは、コンポーネントの対応する機能を使用して追加する必要があります。
* **[!UICONTROL 幅]** - 幅を設定できます。
* **[!UICONTROL 高さ]** - 高さを設定できます。

これらの設定オプションを設定するには、例えば、Dynamic Media Classicコンポーネントをダブルクリックします。 **[!UICONTROL ズーム]** コンポーネント：

![chlimage_1-80](assets/chlimage_1-80.png)

### ズーム {#zoom}

HTML5 ズームコンポーネントでは、「+」ボタンをクリックすると画像のサイズが拡大されます。

アセットの下部にはズームツールが用意されています。拡大するには「**[!UICONTROL +]** 」、縮小するには「**[!UICONTROL -]**」をクリックします。クリック **[!UICONTROL x]** または「ズームをリセット」矢印を使用すると、画像は読み込み時の元のサイズに戻ります。 全画面表示にするには、斜め矢印をクリックします。コンポーネントを設定するには、「**[!UICONTROL 編集]**」をクリックします。このコンポーネントを使用すると、[Dynamic Media Classic のすべてのコンポーネントに共通の設定](#settings-common-to-all-scene-components)を指定できます。

![](do-not-localize/chlimage_1-5.png)

### フライアウト {#flyout}

HTML5 フライアウトコンポーネントでは、アセットが分割画面として表示されます。左側には、アセットが指定されたサイズで表示され、右側には、ズーム部分が表示されます。コンポーネントを設定するには、「**[!UICONTROL 編集]**」をクリックします。このコンポーネントを使用すると、[Dynamic Media Classic のすべてのコンポーネントに共通の設定](/help/sites-administering/scene7.md#settingscommontoalldynamicmediaclassiccomponents)を指定できます。

>[!NOTE]
>
>フライアウトコンポーネントでカスタムサイズを使用する場合は、そのカスタムサイズが使用され、コンポーネントのレスポンシブ設定は無効になります。
>
>フライアウトコンポーネントでデフォルトのサイズを使用する場合は、 [!UICONTROL デザイン] ビューを開くと、デフォルトのサイズが使用され、コンポーネントがストレッチされ、コンポーネントのレスポンシブ設定でページレイアウトのサイズに合わせて調整されます。ただし、コンポーネントのレスポンシブ設定には制限があることに注意してください。レスポンシブ設定でフライアウトコンポーネントを使用する場合は、フルページで拡大して使用しないでください。そうしないと、フライアウトがページの右の境界線を越えて拡大する場合があります。

![chlimage_1-81](assets/chlimage_1-81.png)

### 画像 {#image}

Dynamic Media Classic の画像コンポーネントを使用すると、Dynamic Media Classic の修飾子、画像またはビューアのプリセット、シャープニングなどといった Dynamic Media Classic 機能を画像に追加できます。Dynamic Media Classicの画像コンポーネントは、AEMの他の画像コンポーネントと似ており、特別なDynamic Media Classic機能が備わっています。 この例では、画像に Dynamic Media Classic の URL 修飾子である `&op_invert=1` が適用されています。

![](do-not-localize/chlimage_1-6.png)

**[!UICONTROL タイトル、代替テキスト]** - 「[!UICONTROL 詳細]」タブでは画像にタイトルを追加し、グラフィックの表示をオフにしているユーザー向けに代替テキストを追加します。

**[!UICONTROL URL、次のウィンドウで開く]** - アセットを設定してリンクを開くことができます。「**[!UICONTROL URL]**」と「**[!UICONTROL 次のウィンドウで開く]**」で、同じウィンドウで開くか新しいウィンドウで開くかを指定します。

![chlimage_1-82](assets/chlimage_1-82.png)

**[!UICONTROL ビューアプリセット]** - ドロップダウンメニューから既存のビューアプリセットを選択します。探しているビューアプリセットが表示されない場合は、表示できるように設定する必要があります。詳しくは、[ビューアプリセットの管理](/help/assets/managing-viewer-presets.md)を参照してください。画像プリセットを使用している場合は、ビューアプリセットを選択できません。逆の場合も同様です。

**[!UICONTROL Dynamic Media Classic Configuration]** - Scene7 Publishing System からアクティブな画像プリセットを取得するために使用するDynamic Media Classic設定を選択します。

**[!UICONTROL 画像プリセット]** - ドロップダウンメニューから既存の画像プリセットを選択します。探している画像プリセットが表示されない場合は、表示できるように設定する必要があります。[画像プリセットの管理](/help/assets/managing-image-presets.md)を参照してください。画像プリセットを使用している場合は、ビューアプリセットを選択できません。逆の場合も同様です。

**[!UICONTROL 出力形式]** - 画像の出力形式（例：jpeg）を選択します。選択する出力形式によっては、追加の設定オプションが表示される場合があります。[画像プリセットの管理](/help/assets/managing-image-presets.md)を参照してください。

**[!UICONTROL シャープニング]** - 画像にシャープニングを適用する方法を選択します。シャープニングについて詳しくは、 [*Adobe Dynamic Media Classicの画質とシャープのベストプラクティス*](/help/assets/assets/sharpening_images.pdf).

**[!UICONTROL URL 修飾子]** — 追加の Dynamic Media Classic 画像コマンドを指定して、画像エフェクトを変更できます。詳しくは、 [画像プリセットの管理](/help/assets/managing-image-presets.md) そして [コマンドリファレンス](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/c-command-reference.html?lang=ja).

**[!UICONTROL ブレークポイント]** - レスポンシブ web サイトでは、ブレークポイントの調整が必要な場合があります。ブレークポイントはコンマで区切る必要があります `,`.

### 画像テンプレート {#image-template}

[Dynamic Media Classic 画像テンプレート](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/template-basics/quick-start-template-basics.html?lang=ja#template-basics) は、Dynamic Media Classic にインポートされたレイヤー化された Photoshop コンテンツで、可変性を考慮してコンテンツとプロパティがパラメーター化されています。この **[!UICONTROL 画像テンプレート]** コンポーネントを使用すると、 AEMで画像を読み込んでテキストを動的に変更できます。 また、ClientContext の値を使用するように&#x200B;**[!UICONTROL 画像テンプレート]**&#x200B;コンポーネントを設定できます。これにより、各ユーザーが個別に画像を活用できます。

コンポーネントを設定するには、「**[!UICONTROL 編集]**」をクリックします。次の項目を設定できます。 [すべてのDynamic Media Classicコンポーネントに共通の設定](/help/sites-administering/scene7.md#settingscommontoalldynamicmediaclassicscomponents) と、この節で説明するその他の設定。

![chlimage_1-83](assets/chlimage_1-83.png)

**[!UICONTROL ファイル参照、幅、高さ]**  — すべてのDynamic Media Classicコンポーネントに共通の設定を参照してください。

>[!NOTE]
>
>Dynamic Media Classic の URL コマンドおよびパラメーターを「ファイル参照」の URL に直接追加することはできません。これらは、**[!UICONTROL パラメーター]**&#x200B;パネルのコンポーネントの UI でのみ定義できます。

**[!UICONTROL タイトル、代替テキスト]** 内 [!UICONTROL Dynamic Media Classic画像テンプレート] 「 」タブで、グラフィックの表示をオフにしているユーザー向けのタイトルと代替テキストを画像に追加します。

**[!UICONTROL URL、で開く]** からアセットを設定して、リンクを開くことができます。 「**[!UICONTROL URL]**」と「**[!UICONTROL 次のウィンドウで開く]**」で、同じウィンドウで開くか新しいウィンドウで開くかを指定します。

![chlimage_1-84](assets/chlimage_1-84.png)

**[!UICONTROL パラメータパネル]** 画像を読み込む際に、画像からの情報がパラメーターに事前に設定されます。 動的に変更できるコンテンツがない場合、このウィンドウは空になります。

![chlimage_1-85](assets/chlimage_1-85.png)

#### テキストの動的な変更 {#changing-text-dynamically}

テキストを動的に変更するには、新しいテキストをフィールドに入力して、「**[!UICONTROL OK]**」をクリックします。この例では、「**[!UICONTROL 価格]**」が 50 ドルで、送料が 99 セントです。

![chlimage_1-86](assets/chlimage_1-86.png)

画像内のテキストが変更されます。フィールドの横にある「**[!UICONTROL リセット]**」をクリックすると、テキストを元の値に戻すことができます。

![chlimage_1-87](assets/chlimage_1-87.png)

#### ClientContext の値を反映したテキストの変更 {#changing-text-to-reflect-the-value-of-a-client-context-value}

フィールドを ClientContext 値にリンクするには、 **[!UICONTROL 選択]** client-context メニューを開くには、clientcontext を選択し、 **[!UICONTROL OK]**.この例では、名前は、名前とプロファイル内の形式設定された名前とのリンクに基づいて変更されます。

![chlimage_1-88](assets/chlimage_1-88.png)

現在ログインしているユーザーの名前がテキストに反映されます。フィールドの横にある「**[!UICONTROL リセット]**」をクリックすると、テキストを元の値に戻すことができます。

![chlimage_1-89](assets/chlimage_1-89.png)

#### Dynamic Media Classicの画像テンプレートをリンクにする {#making-the-scene-image-template-a-link}

**Dynamic Media Classicの画像テンプレートをリンクにするには**:

1. Dynamic Media Classic画像テンプレートコンポーネントを含むページで、 **[!UICONTROL 編集]**.
1. 「**[!UICONTROL URL]**」フィールドに、ユーザーが画像をクリックしたときに表示される URL を入力します。「**[!UICONTROL 次のウィンドウで開く]**」フィールドで、ターゲットを新しいウィンドウと同じウィンドウのどちらで開くかを選択します。

   ![chlimage_1-90](assets/chlimage_1-90.png)

1. 「**[!UICONTROL OK]**」をクリックします。

### ビデオコンポーネント {#video-component}

Dynamic Media Classic **[!UICONTROL ビデオ]**&#x200B;コンポーネント（サイドキックの「Dynamic Media Classic」セクションから使用可能）では、デバイスと帯域幅の検出を使用して、適切なビデオをそれぞれの画面に提供します。このコンポーネントは HTML5 ビデオプレーヤー（チャネルを超えて使用可能な単一のビューア）です。

このコンポーネントはアダプティブビデオセット（単一の MP4 ビデオまたは単一の F4V ビデオ）で使用できます。

ビデオが Dynamic Media Classic 統合でどのように機能するかに関する詳細は、[ビデオ](/help/sites-classic-ui-authoring/manage-assets-classic-s7-video.md)を参照してください。また、 [の **Dynamic Media Classicビデオ** 基盤との比較 **ビデオ** コンポーネント](/help/sites-classic-ui-authoring/manage-assets-classic-s7-video.md).

![chlimage_1-91](assets/chlimage_1-91.png)

### ビデオコンポーネントに関する既知の制限事項 {#known-limitations-for-the-video-component}

マスタービデオがアップロードされると、Adobe DAM および WCM が表示されます。次に示すプロキシアセットは表示されません。

* Dynamic Media Classic のエンコードされたレンディション
* Dynamic Media Classic アダプティブビデオセット

Dynamic Media Classic ビデオコンポーネントでアダプティブビデオセットを使用する場合、ビデオのサイズに合わせてコンポーネントのサイズを変更する必要があります。

## Dynamic Media Classic コンテンツブラウザー {#scene-content-browser}

Dynamic Media Classicのコンテンツブラウザーを使用すると、Dynamic Media ClassicのコンテンツをAEMで直接表示できます。 コンテンツブラウザーにアクセスするには、コンテンツファインダーで、タッチ操作向けユーザーインターフェイスの「**[!UICONTROL Dynamic Media Classic]**」またはクラシックインターフェイスの&#x200B;**[!UICONTROL S7]**&#x200B;アイコンを選択します。どちらのユーザーインターフェイスを使用しても、機能は同じです。

設定が複数ある場合、AEM では既定で[デフォルト設定](/help/sites-administering/scene7.md#configuring-a-default-configuration)が表示されます。 Dynamic Media Classic コンテンツブラウザーのドロップダウンメニューで、別の設定を直接選択できます。

>[!NOTE]
>
>* アドホックフォルダーにあるアセットは、Dynamic Media Classicコンテンツブラウザーに表示されません。
>* [セキュアプレビューが有効](/help/sites-administering/scene7.md#configuring-the-state-published-unpublished-of-assets-pushed-to-scene)に設定されている場合、Dynamic Media Classic 上の公開済みアセットと未公開アセットの両方が Dynamic Media Classic コンテンツブラウザーに表示されます。
>* 表示されない **[!UICONTROL Dynamic Media Classic]** または **[!UICONTROL S7]** アイコンをコンテンツブラウザーのオプションとして使用する場合は、 [AEMと連携するDynamic Media Classicの設定](/help/sites-administering/scene7.md).
>
>* ビデオの場合、Dynamic Media Classic コンテンツブラウザーは次の項目をサポートしています。
>
>* アダプティブビデオセット：複数の Screens でシームレスに再生するために必要なすべてのビデオレンディションのコンテナ
>* 単一の MP4 ビデオ
>* 単一の F4V ビデオ


### クラシック UI でのコンテンツの参照 {#browsing-content-in-the-classic-ui}

Dynamic Media Classicでコンテンツを参照するには、 **[!UICONTROL S7]** タブをクリックします。

設定を選択することで、現在アクセスしている設定を変更することができます。 フォルダーは、選択する設定に応じて変わります。

![chlimage_1-92](assets/chlimage_1-92.png)

アセット用のコンテンツファインダーと同様に、アセットを検索して、結果にフィルターを適用できます。ただし、アセットファインダーとは異なり、「**[!UICONTROL S7]**」タブでキーワードを入力すると、そのキーワードが&#x200B;*含まれる*&#x200B;ファイル名ではなく、入力した文字列&#x200B;*で始まる*&#x200B;ファイル名が検索されます。

デフォルトでは、アセットはファイル名で表示されます。結果をアセットタイプでフィルタリングすることもできます。

>[!NOTE]
>
>ビデオの場合、WCM のDynamic Media Classicコンテンツブラウザーは次の機能をサポートしています。
>
>* アダプティブビデオセット：複数の Screens でシームレスに再生するために必要なすべてのビデオレンディションのコンテナ
>* 単一の MP4 ビデオ
>* 単一の F4V ビデオ
>


### コンテンツブラウザーでのDynamic Media Classicアセットの検索 {#searching-for-scene-assets-with-the-content-browser}

Dynamic Media Classicアセットの検索は、AEMアセットの検索と似ていますが、検索時に、実際にはAEMに直接読み込むのではなく、Dynamic Media Classicシステムにアセットのリモートビューが表示される点が異なります。

クラシック UI またはタッチ操作向け UI を使用して、アセットを表示および検索できます。インターフェイスによって検索方法は多少異なります。

どちらの UI で検索する場合でも、次の基準でフィルターを適用できます（ここでは、タッチ操作向け UI を示しています）。

**[!UICONTROL キーワードを入力]** - アセットを名前で検索できます。検索時には、入力したキーワードで始まるファイル名が検索されます。例えば、「swimming」という単語を入力すると、入力した順序どおりの文字列で始まるアセットファイルの名前が検索されます。アセットを検索するには、語句を入力した後に Enter キーを押してください。

![chlimage_1-93](assets/chlimage_1-93.png)

**[!UICONTROL フォルダー/パス]**  — 表示されるフォルダーの名前は、選択した設定に基づいています。 下位にドリルダウンするには、フォルダーアイコンをクリックしてサブフォルダーを選択し、チェックマークをクリックして選択します。

キーワードを入力してフォルダーを選択すると、AEM ではそのフォルダーがとすべてのサブフォルダーが検索されます。ただし、検索時にキーワードを入力しない場合は、フォルダーを選択してもそのフォルダー内のアセットしか表示されず、サブフォルダーは含まれません。

デフォルトでは、AEM は、選択したフォルダーとすべてのサブフォルダーを検索します。

![chlimage_1-94](assets/chlimage_1-94.png)

**[!UICONTROL アセットのタイプ]** 「 Dynamic Media Classic 」を選択してDynamic Media Classicコンテンツを参照します。 このオプションは、Dynamic Media Classicを設定済みの場合にのみ使用できます。

![chlimage_1-95](assets/chlimage_1-95.png)

**[!UICONTROL 設定]** 複数のDynamic Media Classic設定を [!UICONTROL Cloud Services]を選択する場合は、ここで選択できます。 そのため、選択した設定に基づいてフォルダーが変わります。

![chlimage_1-96](assets/chlimage_1-96.png)

**[!UICONTROL アセットタイプ]** Dynamic Media Classicブラウザー内で、結果をフィルタリングして、次のいずれかを含めることができます。画像、テンプレート、ビデオおよびアダプティブビデオセットを参照してください。 アセットタイプを選択しない場合、AEM ではデフォルトですべてのアセットタイプが検索されます。

![chlimage_1-97](assets/chlimage_1-97.png)

>[!NOTE]
>
>* ビデオを検索するときは、単一のレンディションが検索されています。結果には、元のレンディション（&amp;ast;.mp4 のみ）と、エンコードされたレンディションが返されます。
>* アダプティブビデオセットを検索する場合、検索にキーワードを追加した場合にのみ、フォルダーとすべてのサブフォルダーを検索します。 キーワードを追加しない場合、AEM はサブフォルダーを検索しません。
>


**[!UICONTROL 公開ステータス]** 公開ステータスに基づいてアセットをフィルタリングできます。 [!UICONTROL 公開済み] または [!UICONTROL 非公開]. 選択しない場合は、 [!UICONTROL 公開ステータス]、AEMはデフォルトで、すべての公開ステータスを検索します。

![chlimage_1-98](assets/chlimage_1-98.png)
