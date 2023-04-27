---
title: ページへのDynamic Media Classicコンポーネントの追加
description: Adobe Experience ManagerのページにDynamic Media Classicの機能とコンポーネントを追加する方法。
contentOwner: Alva Ware-Bevacqui
products: SG_EXPERIENCEMANAGER/6.4/ASSETS
content-type: reference
topic-tags: managing-assets
exl-id: b11b19c1-712d-4698-aefc-930ff8cacbc1
feature: Dynamic Media Classic
role: User
source-git-commit: 50b657456d2a0eaaaf681d3902eba38b15d00e12
workflow-type: tm+mt
source-wordcount: '2824'
ht-degree: 46%

---

# ページへのDynamic Media Classicコンポーネントの追加 {#adding-scene-features-to-your-page}

Adobe Dynamic Media Classic は、リッチメディアアセットの管理や拡張のほか、web、モバイル、メールをはじめインターネットに接続されたディスプレイやプリンターにリッチメディアアセットを公開および提供したりするためのホスト型ソリューションです。

Dynamic Media Classicで公開されたAEMアセットは、様々なビューアで表示できます。

* ズーム
* フライアウト
* ビデオ
* 画像テンプレート
* 画像

デジタルアセットをAEMからDynamic Media Classicに直接公開したり、デジタルアセットをDynamic Media ClassicからAEMに公開したりできます。

このドキュメントでは、デジタルアセットをAEMからDynamic Media Classicに公開する方法と、その逆の方法について説明します。 また、ビューアについても詳しく説明します。AEM for Dynamic Media Classicの設定について詳しくは、 [Dynamic Media ClassicとAEMの統合](/help/sites-administering/scene7.md).

関連トピック [画像マップの追加](image-maps.md).

AEMでのビデオコンポーネントの使用について詳しくは、 [ビデオ](video.md).

>[!NOTE]
>
>Dynamic Media Classicのアセットが正しく表示されない場合は、Dynamic Media が [無効](config-dynamic.md#disabling-dynamic-media) ページを更新します。

## アセットから Dynamic Media Classic への手動公開 {#manually-publishing-to-scene-from-assets}

デジタルアセットは、次の手順で Dynamic Media Classic に公開できます。

* [クラシックユーザーインターフェイスを使用して Assets コンソールから](/help/sites-classic-ui-authoring/manage-assets-classic-s7.md#publishing-from-the-assets-console)
* [クラシックユーザーインターフェイスを使用してアセットから](/help/sites-classic-ui-authoring/manage-assets-classic-s7.md#publishing-from-an-asset)
* [CQ Target フォルダーの外部からのクラシックユーザーインターフェイス](/help/sites-classic-ui-authoring/manage-assets-classic-s7.md#publishing-assets-from-outside-the-cq-target-folder)

>[!NOTE]
>
>AEMはDynamic Media Classicに非同期で公開します。 次をクリックした後： **[!UICONTROL 公開]**( アセットがDynamic Media Classicに公開されるまで数秒かかる場合があります )。

## Dynamic Media Classic コンポーネント {#scene-components}

AEMでは、次のDynamic Media Classicコンポーネントを使用できます。

* ズーム
* フライアウト (ズーム)
* 画像テンプレート
* 画像
* ビデオ

>[!NOTE]
>
>これらのコンポーネントはデフォルトでは使用できないので、で選択する必要があります。 **[!UICONTROL デザイン]** モードを使用してください。

これらが **[!UICONTROL デザイン]** モードでは、他のAEMコンポーネントと同様に、コンポーネントをページに追加できます。 同期済みフォルダー内、ページ上、または Dynamic Media Classic クラウド設定を使用している場合、まだ Dynamic Media Classic に公開されていないアセットは Dynamic Media Classic に公開されます。

>[!NOTE]
>
>カスタムビューアを作成および開発し、コンテンツファインダーを使用する場合は、 **[!UICONTROL allowfullscreen]** パラメーター。

### Flash ビューアのサポート終了に関するお知らせ {#flash-viewers-end-of-life-notice}

2017年1月31日（PT）をもって、Adobe Dynamic Media Classic は Flash ビューアプラットフォームのサポートを終了しました。

### ページへのDynamic Media Classicコンポーネント (Scene7) の追加 {#adding-a-scene-component-to-a-page}

ページに Dynamic Media Classic（Scene7）コンポーネントを追加する手順は、任意のページにコンポーネントを追加する手順と同様です。Dynamic Media Classic コンポーネントについて、以降の節で詳しく説明します。

**ページにDynamic Media Classic(Scene7) コンポーネントを追加するには**:

1. AEMで、Dynamic Media Classic(Scene7) コンポーネントを追加するページを開きます。

1. 使用できるDynamic Media Classicコンポーネントがない場合は、 **[!UICONTROL デザイン]** モード、青い境界線の付いた任意のコンポーネントをタップ、 **[!UICONTROL 親]** アイコン、 **[!UICONTROL 設定]** アイコン In **[!UICONTROL Parsys （デザイン）]**&#x200B;をクリックし、使用可能にするDynamic Media Classicのすべてのコンポーネントを選択して、 **[!UICONTROL OK]**.

   ![chlimage_1-224](assets/chlimage_1-224.png)

1. クリック **[!UICONTROL 編集]** 戻る **[!UICONTROL 編集]** モード。

1. コンポーネントをサイドキックの Dynamic Media Classic グループから目的の場所のページにドラッグします。

1. 次をクリック： **[!UICONTROL 設定]** アイコンをクリックして、コンポーネントを開きます。

1. 必要に応じてコンポーネントを編集し、 **[!UICONTROL OK]** 変更を保存します。
1. コンテンツブラウザーから画像やビデオを、ページに追加した Dynamic Media Classic コンポーネントにドラッグします。

   >[!NOTE]
   >
   >タッチ UI に限り、画像やビデオを、ページに配置した Dynamic Media Classic コンポーネントにドラッグ＆ドロップする必要があります。Dynamic Media Classic コンポーネントを選択して編集した後にアセットを選択する操作はサポートされていません。

### レスポンシブサイトへのインタラクティブな表示エクスペリエンスの追加 {#adding-interactive-viewing-experiences-to-a-responsive-website}

アセットのレスポンシブデザインとは、アセットが表示される場所に応じて適応することを意味します。 レスポンシブデザインを使用すると、同じアセットを複数のデバイスで効果的に表示できます。

関連トピック [Web ページ用レスポンシブデザイン](/help/sites-developing/responsive.md).

**レスポンシブサイトにインタラクティブな表示エクスペリエンスを追加するには**:

1. AEMにログインし、 [設定済みのAdobe Dynamic Media ClassicCloud Services](/help/sites-administering/scene7.md#configuring-scene-integration) Dynamic Media Classicコンポーネントを使用できます。

   >[!NOTE]
   >
   >Dynamic Media Classic コンポーネントが使用可能になっていない場合は、[デザインモードで有効に](/help/sites-authoring/default-components-designmode.md)してください。

1. **[!UICONTROL Dynamic Media Classic]** コンポーネントが有効になっている web サイトで、**[!UICONTROL 画像]**&#x200B;コンポーネントをページにドラッグします。
1. コンポーネントを選択し、設定アイコンをタップします。
1. 「**[!UICONTROL Dynamic Media Classic の設定]**」タブで、ブレークポイントを調整します。

   ![chlimage_1-225](assets/chlimage_1-225.png)

1. ビューアがレスポンシブにサイズ変更され、すべてのインタラクションがデスクトップ、タブレットおよびモバイル用に最適化されていることを確認します。

### すべての Dynamic Media Classic コンポーネントに共通の設定 {#settings-common-to-all-scene-components}

様々な設定オプションがありますが、次のオプションはすべての [!UICONTROL Dynamic Media Classic] コンポーネントに共通です。

* **[!UICONTROL ファイル参照]**
参照するファイルを参照します。 ファイル参照には、アセットの URL が表示されます。これは必ずしも、URL コマンドおよびパラメーターを含む Dynamic Media Classic の完全な URL ではありません。このフィールドに Dynamic Media Classic の URL コマンドおよびパラメーターを追加することはできません。コンポーネントの対応する機能を使用して追加する必要があります。
* **[!UICONTROL 幅]**
幅を設定できます。
* **[!UICONTROL 高さ]**
高さを設定できます。

これらの設定オプションは、Dynamic Media Classic コンポーネントを開く（ダブルクリックする）ことで設定できます。例えば、**[!UICONTROL ズーム]**&#x200B;コンポーネントを開いた場合は、次のようになります。

![chlimage_1-226](assets/chlimage_1-226.png)

### ズーム {#zoom}

HTML5 ズームコンポーネントでは、「**[!UICONTROL +]**」ボタンをクリックすると画像のサイズが拡大されます。

アセットの下部にはズームツールが用意されています。タップ **[!UICONTROL +]** を拡大します。 タップ **[!UICONTROL -]** 減らす。 「**[!UICONTROL x]**」またはズームのリセット矢印をタップすると、画像が元の（読み込み時の）サイズに戻ります。斜めの矢印をタップして、全画面表示にします。 タップ **[!UICONTROL 編集]** コンポーネントを設定する場合。 このコンポーネントを使用すると、[[!UICONTROL Dynamic Media Classic] のすべてのコンポーネントに共通の設定](#settings-common-to-all-scene-components)を指定できます。

![chlimage_1-227](assets/chlimage_1-227.png)

### フライアウト {#flyout}

HTML5 **[!UICONTROL フライアウト]**&#x200B;コンポーネントでは、アセットが分割画面として表示されます。左側にはアセットが指定されたサイズで表示され、右側にはズーム部分が表示されます。タップ **[!UICONTROL 編集]** コンポーネントを設定する場合。 このコンポーネントを使用すると、[Dynamic Media Classic のすべてのコンポーネントに共通の設定](#settings-common-to-all-scene-components)を指定できます。

>[!NOTE]
>
>**[!UICONTROL フライアウト]**&#x200B;コンポーネントでカスタムサイズを使用している場合は、そのカスタムサイズが使用され、コンポーネントのレスポンシブ設定は無効になります。
>
>次に、 **[!UICONTROL フライアウト]** コンポーネントは、 **[!UICONTROL デザインビュー]**&#x200B;を指定した場合は、デフォルトのサイズが使用され、コンポーネントが拡張され、コンポーネントのレスポンシブ設定に応じてページレイアウトのサイズに調整されます。 ただし、コンポーネントのレスポンシブ設定には制限があります。を **[!UICONTROL フライアウト]** レスポンシブ設定のコンポーネント。フルページで拡大して使用しないでください。 それ以外の場合は、 **[!UICONTROL フライアウト]** は、ページの右の境界線を越えて拡大する場合があります。

![chlimage_1-228](assets/chlimage_1-228.png)

### 画像 {#image}

Dynamic Media Classic の&#x200B;**[!UICONTROL 画像]**&#x200B;コンポーネントを使用すると、Dynamic Media Classic の修飾子、画像またはビューアのプリセット、シャープニングなどといった Dynamic Media Classic 機能を画像に追加できます。ザDynamic Media Classic **[!UICONTROL 画像]** コンポーネントは、AEMの特別なDynamic Media Classic機能を備えた他の画像コンポーネントと似ています。 この例では、画像にDynamic Media Classic URL 修飾子が含まれています。 **&amp;op_invert=1** 適用済み

![chlimage_1-229](assets/chlimage_1-229.png)

* **[!UICONTROL タイトル、代替テキスト]**
内 **[!UICONTROL 詳細]** 「 」タブで、グラフィックの表示をオフにしているユーザー向けのタイトルと代替テキストを画像に追加します。

* **[!UICONTROL URL、で開く]**
からアセットを設定して、リンクを開くことができます。 「**[!UICONTROL URL]**」と「**[!UICONTROL 次のウィンドウで開く]**」で、同じウィンドウで開くか新しいウィンドウで開くかを指定します。

![chlimage_1-230](assets/chlimage_1-230.png)

* **[!UICONTROL ビューアプリセット]**
ドロップダウンメニューから既存のビューアプリセットを選択します。 探しているビューアプリセットが表示されない場合は、表示できるように設定する必要があります。詳しくは、[ビューアプリセットの管理](/help/assets/managing-viewer-presets.md)を参照してください。画像プリセットを使用している場合はビューアプリセットを選択できません。また、その逆の場合も選択できません。

* **[!UICONTROL Dynamic Media Classic Configuration]**
SPS からアクティブな画像プリセットを取得するために使用するDynamic Media Classic設定を選択します。

* **[!UICONTROL 画像プリセット]**
ドロップダウンメニューから既存の画像プリセットを選択します。 探している画像プリセットが表示されない場合は、表示できるように設定する必要があります。[画像プリセットの管理](/help/assets/managing-image-presets.md)を参照してください。画像プリセットを使用している場合はビューアプリセットを選択できません。また、その逆の場合も選択できません。

* **[!UICONTROL 出力形式]**
画像の出力形式（例：jpeg）を選択します。 選択する出力形式によっては、追加の設定オプションが表示される場合があります。[画像プリセットのベストプラクティス](/help/assets/managing-image-presets.md#image-preset-options)を参照してください。

* **[!UICONTROL シャープ]**
画像にシャープを適用する方法を選択します。 シャープニングについて詳しくは、[画像プリセットのベストプラクティス](/help/assets/managing-image-presets.md#image-preset-options)および[シャープニングのベストプラクティス](/help/assets/assets/sharpening_images.pdf)を参照してください。

* **[!UICONTROL URL 修飾子]**
追加のDynamic Media Classic画像コマンドを指定すると、画像エフェクトを変更できます。 詳しくは、 [画像プリセット](/help/assets/managing-image-presets.md) そして [コマンドリファレンス](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/c-command-reference.html?lang=ja).

* **[!UICONTROL ブレークポイント]**
レスポンシブ Web サイトの場合は、ブレークポイントを調整する必要があります。 ブレークポイントはコンマ（,）で区切る必要があります。

### 画像テンプレート {#image-template}

[Dynamic Media Classic 画像テンプレート](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/template-basics/creating-template.html#creating-the-initial-template) は、Dynamic Media Classic にインポートされたレイヤー化された Photoshop コンテンツで、可変性を考慮してコンテンツとプロパティがパラメーター化されています。この **[!UICONTROL 画像テンプレート]** コンポーネントを使用すると、画像を読み込み、AEMでテキストを動的に変更できます。 また、ClientContext の値を使用するように&#x200B;**[!UICONTROL 画像テンプレート]**&#x200B;コンポーネントを設定できます。これにより、各ユーザーが個別に画像を活用できます。

タップ **[!UICONTROL 編集]** コンポーネントを設定する場合。 次の項目を設定できます。 [すべてのDynamic Media Classicコンポーネントに共通の設定](#settings-common-to-all-scene-components) と、この節で説明するその他の設定。

![chlimage_1-231](assets/chlimage_1-231.png)

* **[!UICONTROL ファイル参照、幅、高さ]**
すべてのDynamic Media Classicコンポーネントに共通の設定を参照してください。

   >[!NOTE]
   >
   >Dynamic Media Classic の URL コマンドおよびパラメーターを「ファイル参照」の URL に直接追加することはできません。これらは、**[!UICONTROL パラメーター]**&#x200B;パネルのコンポーネントの UI でのみ定義できます。

* **[!UICONTROL タイトル、代替テキスト]**
「 Dynamic Media Classic画像テンプレート」タブで、グラフィックの表示をオフにしているユーザー向けのタイトルと代替テキストを画像に追加します。

* **[!UICONTROL URL、で開く]**
からアセットを設定して、リンクを開くことができます。 「URL」と「次のウィンドウで開く」で、同じウィンドウで開くか新しいウィンドウで開くかを指定します。

![chlimage_1-232](assets/chlimage_1-232.png)

* **[!UICONTROL パラメータパネル]**
画像を読み込む際に、画像からの情報がパラメーターに事前に設定されます。 動的に変更できるコンテンツがない場合、このウィンドウは空になります。

![chlimage_1-233](assets/chlimage_1-233.png)

#### テキストの動的な変更 {#changing-text-dynamically}

テキストを動的に変更するには、フィールドに新しいテキストを入力し、 **[!UICONTROL OK]**. この例では、「**[!UICONTROL 価格]**」が 50 ドルで、送料が 99 セントです。

![chlimage_1-234](assets/chlimage_1-234.png)

画像内のテキストが変更されます。フィールドの横にある「**[!UICONTROL リセット]**」をタップすると、テキストを元の値に戻すことができます。

![chlimage_1-235](assets/chlimage_1-235.png)

#### ClientContext 値の値を反映するテキストの変更 {#changing-text-to-reflect-the-value-of-a-client-context-value}

フィールドを ClientContext の値にリンクするには、 **[!UICONTROL 選択]** client-context メニューを開くには、clientcontext を選択し、 **[!UICONTROL OK]**. この例では、「名前」フィールドとプロファイル内の書式設定された名前とのリンクに基づいて名前が変わります。

![chlimage_1-236](assets/chlimage_1-236.png)

現在ログインしているユーザーの名前がテキストに反映されます。フィールドの横にある「**[!UICONTROL リセット]**」をクリックすると、テキストを元の値に戻すことができます。

![chlimage_1-237](assets/chlimage_1-237.png)

#### Dynamic Media Classic画像テンプレートをリンクにする {#making-the-scene-image-template-a-link}

1. Dynamic Media Classicを含むページ上 **[!UICONTROL 画像テンプレート]** コンポーネント、タップ **[!UICONTROL 編集]**.
1. 「**[!UICONTROL URL]**」フィールドに、ユーザーが画像をタップしたときに表示される URL を入力します。「**[!UICONTROL 次のウィンドウで開く]**」フィールドで、ターゲットを新しいウィンドウと同じウィンドウのどちらで開くかを選択します。

   ![chlimage_1-238](assets/chlimage_1-238.png)

1. 「**[!UICONTROL OK]**」をタップします。

### ビデオコンポーネント {#video-component}

Dynamic Media Classic **[!UICONTROL ビデオ]**&#x200B;コンポーネント（サイドキックの「Dynamic Media Classic」セクションから使用可能）では、デバイスと帯域幅の検出を使用して、適切なビデオをそれぞれの画面に提供します。このコンポーネントは HTML5 ビデオプレーヤー（チャネルを超えて使用可能な単一のビューア）です。

このコンポーネントはアダプティブビデオセット（単一の MP4 ビデオまたは単一の F4V ビデオ）で使用できます。

ビデオが Dynamic Media Classic 統合でどのように機能するかに関する詳細は、[ビデオ](s7-video.md)を参照してください。また、 [Dynamic Media Classicビデオコンポーネントと基盤ビデオコンポーネントの比較](s7-video.md)も参照してください。

![chlimage_1-239](assets/chlimage_1-239.png)

### ビデオコンポーネントに関する既知の制限事項 {#known-limitations-for-the-video-component}

AdobeDAM と WCM に、マスタービデオがアップロードされたかどうかを示します。 次に示すプロキシアセットは表示されません。

* Dynamic Media Classic のエンコードされたレンディション
* Dynamic Media Classic アダプティブビデオセット

Dynamic Media Classicビデオコンポーネントでアダプティブビデオセットを使用する場合、ビデオのサイズに合わせてコンポーネントのサイズを変更する必要があります。

## Dynamic Media Classic コンテンツブラウザー {#scene-content-browser}

Dynamic Media Classicのコンテンツブラウザーを使用すると、Dynamic Media ClassicのコンテンツをAEMで直接表示できます。 コンテンツブラウザーにアクセスするには、**[!UICONTROL コンテンツファインダー]**&#x200B;で、タッチ操作向けユーザーインターフェイスの「**[!UICONTROL Dynamic Media Classic]**」またはクラシックインターフェイスの&#x200B;**[!UICONTROL S7]**&#x200B;アイコンを選択します。どちらのユーザーインターフェイスを使用しても、機能は同じです。

複数の設定がある場合、AEMにはデフォルトで「 [デフォルト設定](/help/sites-administering/scene7.md#configuring-a-default-configuration). Dynamic Media Classic コンテンツブラウザーのドロップダウンメニューで、別の設定を直接選択できます。

>[!NOTE]
>
>* アドホックフォルダーにあるアセットは、Dynamic Media Classicコンテンツブラウザーに表示されません。
>* [セキュアプレビューが有効](/help/sites-administering/scene7.md#configuring-the-state-published-unpublished-of-assets-pushed-to-scene)に設定されている場合、Dynamic Media Classic 上の公開済みアセットと未公開アセットの両方が Dynamic Media Classic コンテンツブラウザーに表示されます。
>* 表示されない **[!UICONTROL Dynamic Media Classic]** または **[!UICONTROL S7]** アイコンをコンテンツブラウザーのオプションとして使用する場合は、 [AEMと連携するDynamic Media Classicの設定](/help/sites-administering/scene7.md).
>* ビデオの場合、Dynamic Media Classic コンテンツブラウザーは次の項目をサポートしています。
   >   * アダプティブビデオセット：複数の Screens でシームレスに再生するために必要なすべてのビデオレンディションのコンテナ
   >   * 単一の MP4 ビデオ
   >   * 単一の F4V ビデオ


### タッチ操作向け UI でのコンテンツの参照 {#browsing-content-in-the-touch-optimized-ui}

コンテンツブラウザーには、タッチ操作向け UI またはクラシック UI でアクセスできます。 現在、タッチ操作向けには次の制限があります。

* Dynamic Media Classic の FXG および Flash のアセットはサポートされていません。

3 番目のドロップダウンメニューから「**[!UICONTROL Dynamic Media Classic]**」を選択して、Dynamic Media Classic アセットを参照します。Dynamic Media Classic/AEMの統合を設定していない場合、Dynamic Media Classicはリストに表示されません。

>[!NOTE]
>
>* Dynamic Media Classic コンテンツブラウザーは、約 100 個のアセットを読み込んで、名前順に並べ替えます。
>* 安全なプレビューサーバーが設定されている場合、ブラウザーはそのプレビューサーバーを使用してサムネールとアセットをレンダリングします。
>


![chlimage_1-240](assets/chlimage_1-240.png)

また、ブラウザー内でアセットの上にマウスポインターを置くと、解像度の情報、サイズ、変更後の日数およびファイル名を参照できます。

![chlimage_1-241](assets/chlimage_1-241.png)

* アダプティブビデオセットおよびテンプレートの場合、サムネールのサイズ情報は生成されません。
* アダプティブビデオセットの場合、サムネールの解像度は生成されません。

### コンテンツブラウザーでのDynamic Media Classicアセットの検索 {#searching-for-scene-assets-with-the-content-browser}

Dynamic Media Classicアセットの検索は、AEMアセットの検索と似ていますが、検索時に、実際にはAEMに直接読み込むのではなく、Dynamic Media Classicシステムにアセットのリモートビューが表示される点が異なります。

クラシック UI またはタッチ操作向け UI を使用して、アセットの表示と検索の両方を行うことができます。 インターフェイスによって、検索方法が少し異なります。

どちらの UI で検索する場合でも、次の基準でフィルターを適用できます（ここでは、タッチ操作向け UI を示しています）。

* **[!UICONTROL キーワードを入力]**
アセットを名前で検索できます。 検索時に入力したキーワードが、ファイル名の先頭に表示されます。 例えば、「swimming」という単語を入力すると、入力した順序どおりの文字列で始まるアセットファイルの名前が検索されます。アセットを検索するには、キーワードを入力した後、必ず Enter キーを押してください。

![chlimage_1-242](assets/chlimage_1-242.png)

* **[!UICONTROL フォルダー/パス]**
表示されるフォルダーの名前は、選択した設定に基づいています。 フォルダーアイコンをタップしてサブフォルダーを選択し、チェックマークをタップして選択すると、下位レベルまでドリルダウンできます。

キーワードを入力してフォルダーを選択すると、AEMはそのフォルダーとサブフォルダーを検索します。 ただし、検索時にキーワードを入力しない場合、フォルダーを選択した場合はそのフォルダー内のアセットのみが表示され、サブフォルダーは含まれません。

デフォルトでは、AEMは選択したフォルダーとすべてのサブフォルダーを検索します。

![chlimage_1-243](assets/chlimage_1-243.png)

* **[!UICONTROL アセットのタイプ]**
選択 **[!UICONTROL Dynamic Media Classic]** Dynamic Media Classicコンテンツを参照します。 このオプションは、Dynamic Media Classic が設定されている場合にのみ使用できます。

![chlimage_1-244](assets/chlimage_1-244.png)

* **[!UICONTROL 設定]**
複数のDynamic Media Classic設定を [!UICONTROL Cloud Services]を選択する場合は、ここで選択できます。 その結果、選択した設定に基づいてフォルダーが変更されます。

![chlimage_1-245](assets/chlimage_1-245.png)

* **[!UICONTROL アセットタイプ]**
Dynamic Media Classicブラウザー内で、結果をフィルタリングして、次のいずれかを含めることができます。画像、テンプレート、ビデオおよびアダプティブビデオセットを参照してください。 アセットタイプを選択しない場合、AEMはデフォルトですべてのアセットタイプを検索します。

![chlimage_1-246](assets/chlimage_1-246.png)

>[!NOTE]
>
>* クラシック UI では、**Flash** と **FXG** も検索できます。現在、タッチ操作向け UI でのこれらのフィルタリングはサポートされていません。
>
>* ビデオを検索するときは、単一のレンディションが検索されています。結果には、元のレンディション（&amp;ast;.mp4 のみ）と、エンコードされたレンディションが返されます。
>* アダプティブビデオセットを検索する場合、検索にキーワードを追加した場合にのみ、フォルダーとすべてのサブフォルダーを検索します。 キーワードを追加していない場合、AEMはサブフォルダーを検索しません。
>


* **[!UICONTROL 公開ステータス]**
公開ステータスに基づいてアセットをフィルタリングできます。 **[!UICONTROL 非公開]** または **[!UICONTROL 公開済み]**. 選択しない場合は、 **[!UICONTROL 公開ステータス]**、AEMはデフォルトで、すべての公開ステータスを検索します。

![chlimage_1-247](assets/chlimage_1-247.png)
