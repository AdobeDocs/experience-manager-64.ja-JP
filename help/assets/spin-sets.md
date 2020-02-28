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

---


# スピンセット {#spin-sets}

スピンセットは、物体を回転させて調べるという現実世界の操作をシミュレートしたものです。スピンセットによって、あらゆる角度からアイテムを表示して、あらゆる角度から重要な細部を目で確認できます。

スピンセットは、360 度の閲覧エクスペリエンスをシミュレートします。Dynamic Media は、ビューアがアイテムを回転できる単一軸のスピンセットを提供します。さらに、ユーザーは「自由形式」のズームを実行し、マウスを数回クリックするだけで任意のビューをパンできます。このようにして、ユーザーは特定の視点からより詳しくアイテムを調べることができます。

Spin Sets are designated by a banner with the word **[!UICONTROL SPINSET]**. In addition, if the Spin Set is published, then the publish date, indicated by the **[!UICONTROL World]** icon is on the banner along with the last modification date, indicated by the **[!UICONTROL Pencil]** icon displays.

![chlimage_1-380](assets/chlimage_1-380.png)

>[!NOTE]
>
>アセットユーザーインターフェイスについて詳しくは、[タッチ UI を使用したアセットの管理](managing-assets-touch-ui.md)を参照してください。

## クイックスタート：スピンセット {#quick-start-spin-sets}

スピンセットをすばやく習得するには、次のワークフローに従います。

1. [複数ビュー用の画像をアップロードします。](#uploading-assets-for-spin-sets)

   1次元スピンセットには少なくとも8 ～ 12枚の写真が必要で、2次元スピンセットには16 ～ 24枚の写真が必要です。アイテムが回転して反転しているように見せるには、一定の間隔でアイテムを撮影する必要があります。例えば、1次元スピンセットに12枚の写真が含まれる場合、アイテムを30°(360°/12)単位で回転させます。

1. [スピンセットを作成します。](#creating-spin-sets)

   スピンセットを作成するには、作成/スピ **[!UICONTROL ンセットを選択し]** 、セットに名前を付け、アセットを選択して、画像を表示される順序で並べ替えます。

   [セレクターの操作](working-with-selectors.md)を参照してください。

   >[!NOTE]
   >
   >You can also create Spin Sets automatically through [batch set presets](/help/assets/config-dms7.md#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets).
   *バッチセットは、アセット取り込みの一部としてIPS(Image Production System)によって作成され、ダイナミックメディア — Scene7モードでのみ使用できます*。

1. 必要に応じて[スピンセットビューアプリセット](managing-viewer-presets.md)を設定します。

   管理者は、スピンセットビューアのプリセットを作成または変更できます。 To see your Spin Set with a Viewer preset, select the Spin Set, and in the left-rail drop-down menu, select **[!UICONTROL Viewers]**.

   See **[!UICONTROL Tools > Assets > Viewer Presets]** to create or edit viewer presets.

   See [Adding and editing viewer presets.](managing-viewer-presets.md)

1. [スピンセットを表示します。](#viewing-spin-sets)

   バッチセットプリセットを使用して作成したセットを表示したり、それらのセットにアクセスしたりするには、3 つの方法があります(Sets created using batch set presets, do *not* appear in the user interface.)

1. [スピンセットをプレビューします。](previewing-assets.md)

   スピンセットを選択すると、プレビューできます。スピンセットを回転します。You can choose different viewers from the **[!UICONTROL Viewers]** menu, available from the left rail drop-down menu.

1. [スピンセットを公開します。](publishing-dynamicmedia-assets.md)

   スピンセットを公開すると、スピンセット内で画像が表示される順序がアクティブになります。 スピンがスムーズに 360 度のビューを描けるように画像を並べてください。**[!UICONTROL URLと埋め込]** み文字列 **** 。 In addition, you must [publish the viewer preset](managing-viewer-presets.md).

1. [URL を Web アプリケーションにリンクする](linking-urls-to-yourwebapplication.md)か、[ビデオビューアまたは画像ビューアを埋め込みます](embed-code.md)。

   AEM Assetsは、スピンセットを公開した後に、スピンセットのURL呼び出しを作成し、アクティブにします。これらのURLは、アセットのプレビュー時にコピーできます。または、それらをWebサイトに埋め込むこともできます。

   「スピンセット」を選択し、左パネルのドロップダウンメニューで「**[!UICONTROL ビューア]**」を選択します。

   詳しくは、[Web ページへのスピンセットのリンク](linking-urls-to-yourwebapplication.md)と[ビデオビューアまたは画像ビューアの埋め込み](embed-code.md)を参照してください。

If you need to, you can [edit Spin Sets](#editing-spin-sets). In addition, you can view and edit [Spin Set properties](managing-assets-touch-ui.md#editing-properties).

## スピンセット用のアセットのアップロード {#uploading-assets-for-spin-sets}

1次元スピンセットには少なくとも8 ～ 12枚の写真が必要で、2次元スピンセットには16 ～ 24枚の写真が必要です。アイテムが回転して反転しているように見せるには、一定の間隔でアイテムを撮影する必要があります。例えば、1次元スピンセットに12枚の写真が含まれる場合、アイテムを30°(360°/12)単位で回転させます。

スピンセット用の画像のアップロードは、[AEM Assets での他のアセットのアップロード](managing-assets-touch-ui.md)と同様に実行できます。

### スピンセット画像の撮影に関するガイドライン {#guidelines-for-shooting-spin-set-images}

ここでは、スピンセット画像に関するベストプラクティスを説明します。一般に、スピンセット内の画像が多いほど、画像のスピン効果が向上します。ただし、セット内に多くの画像を追加すると、画像の読み込みにかかる時間も長くなります。AEM では、スピンセットで使用する画像の撮影について、次のガイドラインに従うことを推奨します。

* 1次元スピンセットでは少なくとも8 ～ 12枚の画像を使用し、2次元スピンセットでは16 ～ 24枚の画像を使用します。360度回転するには、最低8枚の画像が必要です。2次元スピンセットの作成には労力が必要なので、1次元スピンセットの方が一般的です。
* 可逆圧縮形式を使用します。TIFF および PNG が推奨されます。
* 真っ白または他の高コントラストの背景上にアイテムが表示されるように、すべての画像をマスクします。オプションで、シャドウを追加します。
* 製品の細部に十分に光を当て、ピントを合わせるようにします。
* ファッション衣料の場合は、マネキンやモデルに着せてスピン画像を撮影します。多くの場合、ガラス製のマネキンを使用してマネキンを完全にマスクするか、画像内に定型化されたマネキンを表示します。角度を定義することで、モデルによるスピンセットを作成できます。床にテープを貼って角度をマークし、モデルが撮影ごとに動いて向きを変えるための手助けをします。

## スピンセットの作成 {#creating-spin-sets}

スピンセット内での画像の表示順は重要です。スピンがスムーズに 360 度のビューを描けるように画像を並べてください。

>[!NOTE]
>
>また、[バッチセットプリセット](/help/assets/config-dms7.md#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets)を使用してスピンセットを自動的に作成することもできます。バッチセットは、アセット取り込みの一部としてIPS(Image Production System)によって作成され、ダイナミックメディア — Scene7モードでのみ使用できます。
>
>[Dynamic Media - Scene7 モードの設定](/help/assets/config-dms7.md#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets)の「画像セットおよびスピンセットを自動生成するためのバッチセットプリセットの作成」を参照してください。

**スピンセットを作成するには：**

1. In Assets, navigate to where you want to create a spin set, tap **[!UICONTROL Create]**, and select **[!UICONTROL Spin Set**. また、アセットを格納しているフォルダー内からセットを作成することもできます。

   ![chlimage_1-381](assets/chlimage_1-381.png)

1. On the **[!UICONTROL Spin Set Editor]** page, in the **[!UICONTROL Title]** field, enter a name for the Spin Set. この名前は、スピンセット全般のバナーに表示されます。オプションで、説明を入力します。

   ![chlimage_1-382](assets/chlimage_1-382.png)

   スピンセットを作成する際に、スピンセットのサムネールを変更したり、スピンセット内のアセットに基づいてAEMが自動的にサムネールを選択できるようにしたりできます。 To select a thumbnail, tap **[!UICONTROL Change thumbnail]**. Select any image (you can navigate to other folders to find images as well). If you have selected a thumbnail and then decide that you want AEM to generate one from the spin set, select **[!UICONTROL Switch to Automatic thumbnail]**.

1. 次のいずれかの操作をおこないます。

   * Near the upper-left corner of the **[!UICONTROL Spin Set Editor]** page, tap **[!UICONTROL Add Asset]**.
   * Near the middle of the **[!UICONTROL Spin Set Editor]** page, tap **[!UICONTROL Tap to open Asset Selector]**.
   スピンセットに含めるアセットをタップして選択しします。選択済みのアセットにはチェックマークアイコンが付いています。作業が完了したら、ページの右上隅付近にある「**[!UICONTROL 選択]**」をタップします。

   アセットセレクターでは、キーワードを入力して **[!UICONTROL Enter]** キーをタップすることで、アセットを検索することができます。フィルターを適用して、検索結果を絞り込むこともできます。パス、コレクション、ファイルタイプおよびタグでフィルタリングできます。フィルターを選択してから、ツールバーの&#x200B;**[!UICONTROL フィルター]**&#x200B;アイコンをタップします。表示を変更するには、ページの右上隅近くにある **[!UICONTROL View]** （表示）アイコンをタップし、「列表示」、「カード表示 **[!UICONTROL 」]**、「リスト表示」をタップ ********&#x200B;します。

   [セレクターの操作](working-with-selectors.md)を参照してください。

   ![chlimage_1-383](assets/chlimage_1-383.png)

1. 画像セットに追加したアセットは、自動的に英数字順で追加されます。追加後に、手動でアセットの順番を変更したり、並べ替えたりすることができます。If necessary, drag an asset&#39;s **[!UICONTROL Reorder]** icon to the right of the asset&#39;s file name to re-order images up or down the set list.

   ![spin_set_assets6-4](assets/spin_set_assets6-4.png)

1. （オプション）次のいずれかの操作をおこないます。

   * To delete an image, select the image, then tap **[!UICONTROL Delete Asset]**.
   * ページの右上隅付近にプリセットを適用するには、「]**プリセット**[!UICONTROL 」をタップした後、すべてのアセットに一度に適用するプリセットを選択します。

1. 「**[!UICONTROL 保存]**」をタップします。新しく作成したスピンセットは、作成したフォルダに表示されます。

## スピンセットの表示 {#viewing-spin-sets}

スピンセットは、ユーザーインターフェイスで作成することも、[バッチセットプリセット](/help/assets/config-dms7.md#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets)を使用して自動的に作成することもできます。However, sets created using batch set presets, do *not* appear in the user interface. バッチセットプリセットを使用して作成されたセットには、3つの方法でアクセスできます。 （これらの方法は、ユーザインターフェイスでスピンセットを作成した場合でも使用できます）。

You can also view sets by way of the user interface as described in [Editing Spin Sets](#editing-spin-sets).

**スピンセットを表示するには：**

1. 個々のアセットのプロパティを開きます。（「**[!UICONTROL セットのメンバー]**」の下に）選択したアセットがメンバーとして含まれるセットが表示されます。セット全体を表示するには、セットの名前をタップします。

   ![chlimage_1-384](assets/chlimage_1-384.png)

1. 任意のセットのメンバー画像で、Select the **[!UICONTROL Sets]** menu to display the sets that the asset is a member of.

   ![chlimage_1-385](assets/chlimage_1-385.png)

1. From search, you can select **[!UICONTROL Filters]**, then expand **[!UICONTROL Dynamic Media]** and select **[!UICONTROL Sets]**.

   ユーザインターフェイスで手動で作成された、またはバッチセットプリセットを使用して自動的に作成された、一致するセットが返されます。 For automated sets, the search query is conducted using **[!UICONTROL Starts with]** search criteria which is different from AEM search which is based on using **[!UICONTROL Contains]** search criteria. Setting the filter to **[!UICONTROL Sets]** is the only way to search automated sets.

   ![chlimage_1-386](assets/chlimage_1-386.png)

## スピンセットの編集 {#editing-spin-sets}

スピンセットには、次のような様々な編集タスクを実行できます。

* スピンセットへの画像の追加
* スピンセット内の画像の並べ替え
* スピンセットのアセットの削除
* ビューアプリセットの適用
* スピンセットの削除

**スピンセットを編集するには：**

1. 次のいずれかの操作をおこないます。

   * スピンセットアセット上にマウスポインターを置き、]**編集**[!UICONTROL （鉛筆アイコン）をタップします。
   * スピンセットアセット上にマウスポインターを置き、**[!UICONTROL 選択]**（チェックマークアイコン）をタップした後、ツールバーの「**[!UICONTROL 編集]**」をタップします。
   * スピンセットアセットをタップしてから、ツールバーの&#x200B;]**編集**[!UICONTROL （鉛筆アイコン）をタップします。

1. スピンセットを編集するには、次のいずれかの操作をおこないます。

   * 画像を並べ替えるには、画像を新しい位置までドラッグします（並べ替えアイコンを選択して項目を移動します）。
   * 項目を昇順または降順に並べ替えるには、列見出しをタップします。
   * To add an asset or update an existing asset, tap **[!UICONTROL Add Asset]**. アセットに移動して選択し、右上隅の「]**選択**[!UICONTROL 」をタップします。AEMがサムネールに使用する画像を削除し、別の画像に置き換えても、元のアセットは表示されたままになります。
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
