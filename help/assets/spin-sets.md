---
title: スピンセット
seo-title: スピンセット
description: Dynamic Media でのスピンセットの操作方法を学習します。
seo-description: Dynamic Media でのスピンセットの操作方法を学習します。
uuid: a80a0491-6500-463a-83c4-ff4b90a88182
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.4/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: afacb3ad-e4ad-4d06-a898-f3f2da8bbb64
translation-type: tm+mt
source-git-commit: 1ebe1e871767605dd4295429c3d0b4de4dd66939
workflow-type: tm+mt
source-wordcount: '1839'
ht-degree: 68%

---


# スピンセット {#spin-sets}

スピンセットは、物体を回転させて調べるという現実世界の操作をシミュレートしたものです。スピンセットによって、あらゆる角度からアイテムを表示して、あらゆる角度から重要な細部を目で確認できます。

スピンセットは、360 度の閲覧エクスペリエンスをシミュレートします。Dynamic Media は、ビューアがアイテムを回転できる単一軸のスピンセットを提供します。さらに、ユーザーは「自由形式」のズームを実行し、マウスを数回クリックするだけで任意のビューをパンできます。このようにして、ユーザーは特定の視点からより詳しくアイテムを調べることができます。

スピンセットのバナーには、「**[!UICONTROL SPINSET]**」と表示されます。また、スピンセットが公開されている場合、公開日が&#x200B;**[!UICONTROL 地球]**&#x200B;アイコン付きでバナーに表示され、最終変更日も&#x200B;**[!UICONTROL 鉛筆]**&#x200B;アイコン付きで表示されます。

![chlimage_1-380](assets/chlimage_1-380.png)

>[!NOTE]
>
>アセットユーザーインターフェイスについて詳しくは、[タッチ UI を使用したアセットの管理](managing-assets-touch-ui.md)を参照してください。

## クイックスタート：スピンセット {#quick-start-spin-sets}

スピンセットをすばやく習得するには、次のワークフローに従います。

1. [複数ビュー用の画像をアップロードします。](#uploading-assets-for-spin-sets)

   アイテムの写真は最低でも、1 次元スピンセットで 8～12 個、2 次元スピンセットで 16～24 個必要になります。アイテムが回転および反転している印象を与えるためには、写真を一定の間隔で撮影する必要があります。例えば、1 次元スピンセットに 12 個の写真を含める場合、写真を撮影するごとに 30 度ずつ（360/12）アイテムを回転します。

1. [スピンセットを作成します。](#creating-spin-sets)

   スピンセットを作成するには、 **[!UICONTROL 作成/スピンセットを選択し]** 、セットに名前を付け、アセットを選択し、画像を表示される順に並べ替えます。

   [セレクターの操作](working-with-selectors.md)を参照してください。

   >[!NOTE]
   >
   >You can also create Spin Sets automatically through [batch set presets](/help/assets/config-dms7.md#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets).
   *バッチセットは、アセット取り込みの一環としてIPS(Image Production System)によって作成され、ダイナミックメディア —Scene7モードでのみ使用できます*。

1. 必要に応じて[スピンセットビューアプリセット](managing-viewer-presets.md)を設定します。

   管理者は、スピンセットビューアのプリセットを作成または変更できます。 To see your Spin Set with a Viewer preset, select the Spin Set, and in the left-rail drop-down menu, select **[!UICONTROL Viewers]**.

   **[!UICONTROL ツール／アセット／ビューアプリセット]**&#x200B;を選択して、ビューアプリセットを作成または編集します。

   詳しくは、[ビューアプリセットの追加と編集](managing-viewer-presets.md)を参照してください。

1. [スピンセットを表示します。](#viewing-spin-sets)

   バッチセットプリセットを使用して作成したセットを表示したり、それらのセットにアクセスしたりするには、3 つの方法があります（バッチセットプリセットを使用して作成したセットは、ユーザーインターフェイスに表示&#x200B;*されません*）。

1. [スピンセットをプレビューします。](previewing-assets.md)

   スピンセットを選択すると、プレビューできます。スピンセットを回転します。**[!UICONTROL ビューア]**&#x200B;メニューから様々なビューアを選択できます。このメニューは左側のレールのドロップダウンメニューにあります。

1. [スピンセットを公開します。](publishing-dynamicmedia-assets.md)

   スピンセットを公開すると、スピンセット内の画像の表示順序がアクティブになります。 スピンがスムーズに 360 度のビューを描けるように画像を並べてください。**[!UICONTROL URL]** と **** 埋め込み文字列。 また、[ビューアプリセットを公開](managing-viewer-presets.md)する必要があります。

1. [URL を Web アプリケーションにリンクする](linking-urls-to-yourwebapplication.md)か、[ビデオビューアまたは画像ビューアを埋め込みます](embed-code.md)。

   スピンセットを公開すると、AEM AssetsはスピンセットのURL呼び出しを作成し、アクティブにします。 これらのURLは、アセットをプレビューするときにコピーできます。 または、それらをWebサイトに埋め込むこともできます。

   スピンセットを選択し、左側のレールのドロップダウンメニューで「**[!UICONTROL ビューア]**」を選択します。

   詳しくは、[Web ページへのスピンセットのリンク](linking-urls-to-yourwebapplication.md)と[ビデオビューアまたは画像ビューアの埋め込み](embed-code.md)を参照してください。

If you need to, you can [edit Spin Sets](#editing-spin-sets). In addition, you can view and edit [Spin Set properties](managing-assets-touch-ui.md#editing-properties).

## スピンセット用のアセットのアップロード {#uploading-assets-for-spin-sets}

アイテムの写真は最低でも、1 次元スピンセットで 8～12 個、2 次元スピンセットで 16～24 個必要になります。アイテムが回転および反転している印象を与えるためには、写真を一定の間隔で撮影する必要があります。例えば、1 次元スピンセットに 12 個の写真を含める場合、写真を撮影するごとに 30 度ずつ（360/12）アイテムを回転します。

スピンセット用の画像のアップロードは、[AEM Assets での他のアセットのアップロード](managing-assets-touch-ui.md)と同様に実行できます。

### スピンセット画像の撮影に関するガイドライン {#guidelines-for-shooting-spin-set-images}

ここでは、スピンセット画像に関するベストプラクティスを説明します。一般に、スピンセット内の画像が多いほど、画像のスピン効果が向上します。ただし、セット内に多くの画像を追加すると、画像の読み込みにかかる時間も長くなります。AEM では、スピンセットで使用する画像の撮影について、次のガイドラインに従うことを推奨します。

* 最低でも、1 次元スピンセットで 8～12 個、2 次元スピンセットで 16～24 個の画像を使用するようにします。360 度回転できるようにするには、最小で 8 個の画像が必要になります。2 次元スピンセットの作成には多大な労力がかかるので、1 次元スピンセットのほうが一般的です。
* 可逆圧縮形式を使用します。TIFF および PNG が推奨されます。
* 真っ白または他の高コントラストの背景上にアイテムが表示されるように、すべての画像をマスクします。オプションで、シャドウを追加します。
* 製品の細部に十分に光を当て、ピントを合わせるようにします。
* ファッション衣料の場合は、マネキンやモデルに着せてスピン画像を撮影します。多くの場合、ガラス製のマネキンを使用してマネキンを完全にマスクするか、画像内に定型化されたマネキンを表示します。角度を定義することで、モデルによるスピンセットを作成できます。床にテープを貼って角度をマークし、モデルが撮影ごとに動いて向きを変えるための手助けをします。

## スピンセットの作成 {#creating-spin-sets}

スピンセット内での画像の表示順は重要です。スピンがスムーズに 360 度のビューを描けるように画像を並べてください。

>[!NOTE]
>
>[バッチセットプリセット](/help/assets/config-dms7.md#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets)を使用してスピンセットを自動的に作成することもできます。バッチセットは、アセット取り込みの一環としてIPS(Image Production System)によって作成され、ダイナミックメディア —Scene7モードでのみ使用できます。
>
>[Dynamic Media - Scene7 モードの設定](/help/assets/config-dms7.md#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets)の「画像セットおよびスピンセットを自動生成するためのバッチセットプリセットの作成」を参照してください。

**スピンセットを作成するには:**

1. In Assets, navigate to where you want to create a spin set, tap **[!UICONTROL Create]**, and select **[!UICONTROL Spin Set**. アセットを格納しているフォルダー内からセットを作成することもできます。

   ![chlimage_1-381](assets/chlimage_1-381.png)

1. On the **[!UICONTROL Spin Set Editor]** page, in the **[!UICONTROL Title]** field, enter a name for the Spin Set. この名前は、スピンセット全般のバナーに表示されます。オプションで、説明を入力します。

   ![chlimage_1-382](assets/chlimage_1-382.png)

   スピンセットを作成する場合は、スピンセットのサムネールを変更するか、AEMがスピンセット内のアセットに基づいて自動的にサムネールを選択できるようにします。 To select a thumbnail, tap **[!UICONTROL Change thumbnail]**. Select any image (you can navigate to other folders to find images as well). サムネールを選択した状態で、スピンセットからサムネールを自動的に生成する場合は、「**[!UICONTROL 自動サムネールに切り替え]**」を選択します。

1. 次のいずれかの操作をおこないます。

   * Near the upper-left corner of the **[!UICONTROL Spin Set Editor]** page, tap **[!UICONTROL Add Asset]**.
   * Near the middle of the **[!UICONTROL Spin Set Editor]** page, tap **[!UICONTROL Tap to open Asset Selector]**.

   スピンセットに含めるアセットをタップして選択しします。選択済みのアセットにはチェックマークアイコンが付いています。作業が完了したら、ページの右上隅付近にある「**[!UICONTROL 選択]**」をタップします。

   アセットセレクターでは、キーワードを入力して **[!UICONTROL Enter]** キーをタップすることで、アセットを検索することができます。フィルターを適用して、検索結果を絞り込むこともできます。パス、コレクション、ファイルタイプおよびタグでフィルタリングできます。フィルターを選択してから、ツールバーの&#x200B;**[!UICONTROL フィルター]**&#x200B;アイコンをタップします。ページの右上隅近くにある表示を変更するには、 **[!UICONTROL 表示]** アイコンをタップし、次に **[!UICONTROL 列表示]**、カード表示 **[!UICONTROL 、またはリスト表示のをタップしま]******&#x200B;す。

   [セレクターの操作](working-with-selectors.md)を参照してください。

   ![chlimage_1-383](assets/chlimage_1-383.png)

1. 画像セットに追加したアセットは、自動的に英数字順で追加されます。追加後に、手動でアセットの順番を変更したり、並べ替えたりすることができます。If necessary, drag an asset&#39;s **[!UICONTROL Reorder]** icon to the right of the asset&#39;s file name to re-order images up or down the set list.

   ![spin_set_assets6-4](assets/spin_set_assets6-4.png)

1. （オプション）次のいずれかの操作をおこないます。

   * To delete an image, select the image, then tap **[!UICONTROL Delete Asset]**.
   * ページの右上隅付近にプリセットを適用するには、「]**プリセット**[!UICONTROL 」をタップした後、すべてのアセットに一度に適用するプリセットを選択します。

1. 「**[!UICONTROL 保存]**」をタップします。新しく作成したスピンセットは、作成元のフォルダに表示されます。

## スピンセットの表示 {#viewing-spin-sets}

スピンセットは、ユーザーインターフェイスで作成することも、[バッチセットプリセット](/help/assets/config-dms7.md#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets)を使用して自動的に作成することもできます。ただし、バッチセットプリセットを使用して作成したセットは、ユーザーインターフェイスに表示&#x200B;*されません*。バッチセットプリセットを使用して作成されたセットには、3つの方法でアクセスできます。 （これらの方法は、ユーザインターフェイスでスピンセットを作成した場合でも使用できます）。

[スピンセットの編集](#editing-spin-sets)の説明に従って、ユーザーインターフェイスを使用してセットを表示することもできます。

**スピンセットを表示するには:**

1. 個々のアセットのプロパティを開きます。（「**[!UICONTROL セットのメンバー]**」の下に）選択したアセットがメンバーとして含まれるセットが表示されます。セット全体を表示するには、セット名をタップします。

   ![chlimage_1-384](assets/chlimage_1-384.png)

1. 任意のセットのメンバー画像で、**[!UICONTROL セット]**&#x200B;メニューを選択して、アセットがメンバーとして含まれているセットを表示します。

   ![chlimage_1-385](assets/chlimage_1-385.png)

1. From search, you can select **[!UICONTROL Filters]**, then expand **[!UICONTROL Dynamic Media]** and select **[!UICONTROL Sets]**.

   ユーザインターフェイスで手動で作成したか、バッチセットプリセットを使用して自動的に作成した一致セットが返されます。 For automated sets, the search query is conducted using **[!UICONTROL Starts with]** search criteria which is different from AEM search which is based on using **[!UICONTROL Contains]** search criteria. フィルターを「**[!UICONTROL セット]**」に設定するのが、自動セットを検索する唯一の方法です。

   ![chlimage_1-386](assets/chlimage_1-386.png)

## スピンセットの編集 {#editing-spin-sets}

スピンセットには、次のような様々な編集タスクを実行できます。

* スピンセットへの画像の追加
* スピンセット内の画像の並べ替え
* スピンセットのアセットの削除
* ビューアプリセットの適用
* スピンセットの削除

**スピンセットを編集するには:**

1. 次のいずれかの操作をおこないます。

   * スピンセットアセット上にマウスポインターを置き、]**編集**[!UICONTROL （鉛筆アイコン）をタップします。
   * スピンセットアセット上にマウスポインターを置き、**[!UICONTROL 選択]**（チェックマークアイコン）をタップした後、ツールバーの「**[!UICONTROL 編集]**」をタップします。
   * スピンセットアセットをタップしてから、ツールバーの&#x200B;]**編集**[!UICONTROL （鉛筆アイコン）をタップします。

1. スピンセットを編集するには、次のいずれかの操作をおこないます。

   * 画像を並べ替えるには、画像を新しい位置までドラッグします（並べ替えアイコンを選択して項目を移動します）。
   * 項目を昇順または降順で並べ替えるには、列見出しをタップします。
   * To add an asset or update an existing asset, tap **[!UICONTROL Add Asset]**. アセットに移動して選択し、右上隅の「]**選択**[!UICONTROL 」をタップします。AEM でサムネール用に使用されている画像を別の画像に置き換えて削除しても、元のアセットは表示されたままになります。
   * To delete an asset, select it and tap **[!UICONTROL Delete Asset]**.
   * To apply a preset, tap the **[!UICONTROL Preset]** icon and select a preset.
   * スピンセット全体を削除するには、スピンセットに移動して選択し、「**[!UICONTROL 削除]**」を選択します

      >[!NOTE]
      >* You can edit the images in a Spin Set by navigating to the set, tap **[!UICONTROL Set Members]** in the left rail, and then tap the **[!UICONTROL Edit]** (pencil icon) on an individual asset to open the editing window.


1. 編集が完了したら、「**[!UICONTROL 保存]**」をクリックします。

## スピンセットのプレビュー {#previewing-spin-sets}

詳しくは、[アセットのプレビュー](previewing-assets.md)を参照してください。

## スピンセットの公開 {#publishing-spin-sets}

[アセットの公開](publishing-dynamicmedia-assets.md)を参照してください。
