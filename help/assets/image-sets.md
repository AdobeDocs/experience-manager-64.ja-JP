---
title: 画像セット
seo-title: 画像セット
description: Dynamic Media の画像セットの操作方法を学習します。
seo-description: Dynamic Media の画像セットの操作方法を学習します。
uuid: 16008278-f59f-4fa8-90e9-19c78f132439
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.4/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: e00e7cc9-b777-4f9e-906d-824bcb2bbd41
translation-type: tm+mt
source-git-commit: 1ebe1e871767605dd4295429c3d0b4de4dd66939

---


# 画像セット {#image-sets}

画像セットは、ユーザーに対して統一された閲覧エクスペリエンスを提供します。ユーザーはこのエクスペリエンスで、サムネール画像をクリックしてアイテムの様々なビューを表示できます。画像セットによって、アイテムの代替的なビューを表示でき、ビューアでは画像をより近くで確認するためのズームツールを利用できます。

画像セットのバナーには、「**[!UICONTROL IMAGESET]**」と表示されます。また、画像セットが公開されている場合、公開日が&#x200B;**[!UICONTROL 地球]**&#x200B;アイコン付きでバナーに表示され、最終変更日も&#x200B;**[!UICONTROL 鉛筆]**&#x200B;アイコン付きで表示されます。

![chlimage_1-339](assets/chlimage_1-339.png)

画像セット内でスウォッチを作成するには、画像セットを作成し、サムネールを追加します。

この使い方は、アイテムを異なる色、パターンまたは仕上がりで表示する場合に特に便利です。カラースウォッチを含む画像セットを作成するには、ユーザーに表示する色、パターンまたは仕上がりごとに画像を 1 つずつ用意する必要があります。また、色、パターンまたは仕上がりごとに 1 つのカラースウォッチ、パターンスウォッチまたは仕上がりスウォッチを用意する必要もあります。

例として、つばの色が異なる帽子の画像を表示します。つばの色は、赤、緑、青です。この場合、同じ帽子について 3 つの写真が必要になります。赤のつばの写真、緑のつばの写真、青のつばの写真が必要です。また、赤のカラースウォッチ、緑のカラースウォッチ、青のカラースウォッチも必要になります。カラースウォッチは、ユーザーがスウォッチセットビューアでクリックして、赤のつばの帽子、緑のつばの帽子または青のつばの帽子を表示するためのサムネールとして機能します。

>[!NOTE]
>
>アセットユーザーインターフェイスについて詳しくは、[タッチ UI を使用したアセットの管理](managing-assets-touch-ui.md)を参照してください。

## クイックスタート：画像セット {#quick-start-image-sets}

すぐに使い始めるには：

1. [複数ビュー用のマスター画像をアップロードします。](#uploading-assets-in-image-sets)

   まずは画像セット用の画像をアップロードします。ユーザーは画像セットビューアで画像をズームできるので、画像を選択する際にはズームを考慮します。最大サイズで 2,000 ピクセル以上の画像を使用してください。AEM Assets では多くの画像ファイル形式がサポートされますが、可逆圧縮 TIFF、PNG および EPS 画像の使用が推奨されます。

1. [画像セットを作成します。](#creating-image-sets)

   画像セットで、画像セットビューア内のサムネール画像をクリックします。

   To create an Image Set in Assets, tap **[!UICONTROL Create > Image Sets]**. Then, add images and tap **[!UICONTROL Save]**.

   [バッチセットプリセット](/help/assets/config-dms7.md#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets)を使用して画像セットを自動的に作成することもできます。

   **重要** —バッチセットは、アセット取り込みの一部としてIPS(Image Production System)によって作成され、ダイナミックメディア — Scene7モードでのみ使用できます。

   See [Preparing Image Set assets for upload and Uploading your files](#uploading-assets-in-image-sets).

   [セレクターの操作](working-with-selectors.md)を参照してください。

1. Add [Image Set Viewer presets](managing-viewer-presets.md), as needed.

   Administrators can create or modify Image **[!UICONTROL Set Viewer Presets]**. To see your image set with a viewer preset, select the image set, and in the left-rail drop-down menu, select **[!UICONTROL Viewers]**.

   See **[!UICONTROL Tools > Assets > Viewer Presets]** to create or edit viewer presets.

1. (Optional) [Viewing Image Sets](image-sets.md#viewing-image-sets) that were created using batch set presets.
1. [画像セットをプレビューします。](previewing-assets.md)

   画像セットを選択すると、プレビューできます。サムネールアイコンをタップして、選択したビューアで画像セットを確認します。 You can choose different viewers from the **[!UICONTROL Viewers]** menu, available from the left rail drop-down menu.

1. [画像セットを公開します。](publishing-dynamicmedia-assets.md)

   画像セットを公開すると、URL と埋め込み文字列がアクティベートされます。In addition, you must [publish any custom viewer preset](managing-viewer-presets.md) that you have created. 既製のビューアプリセットが既に公開されています。

1. [URL を Web アプリケーションにリンクする](linking-urls-to-yourwebapplication.md)か、[ビデオビューアまたは画像ビューアを埋め込みます](embed-code.md)。

   画像セットの URL コールが作成され、画像セットの公開後にそれらの URL コールがアクティベートされます。アセットをプレビューする際に、これらの URL をコピーできます。または、URL を Web サイトに埋め込むこともできます。

   画像セットを選択し、左パネルのドロップダウンメニューで「**[!UICONTROL ビューア]**」を選択します。

   詳しくは、[Web ページへの画像セットのリンク](linking-urls-to-yourwebapplication.md)および[ビデオビューアまたは画像ビューアの埋め込み](embed-code.md)を参照してください。

To edit Image Sets, see [editing Image Sets.](#editing-image-sets) また、画像セットのプロパティを表示および編 [集することもできます](managing-assets-touch-ui.md#editing-properties)。

セットの作成で問題が発生した場合は、[Dynamic Media - Scene7 モードのトラブルシューティング](troubleshoot-dms7.md#images-and-sets)の「画像とセット」を参照してください。

## Uploading assets in Image Sets {#uploading-assets-in-image-sets}

まずは画像セット用の画像をアップロードします。ユーザーは画像セットビューアで画像をズームできるので、画像を選択する際にはズームを考慮します。最大サイズで 2,000 ピクセル以上の画像を使用してください。画像セットでは多くの画像ファイル形式がサポートされますが、可逆圧縮 TIFF、PNG および EPS 画像の使用が推奨されます。

画像セット用の画像のアップロードは、[AEM アセットでの他のアセットのアップロード](managing-assets-touch-ui.md#uploading-assets)と同様に実行できます。

### アップロード用の画像セットアセットの準備 {#preparing-image-set-assets-for-upload}

画像セットを作成する前に、画像が適切なサイズと形式であることを確認します。

複数ビューの画像セットを作成するには、異なる視点からアイテムを表示するための画像、または同じアイテムの異なる面を表示するための画像が必要になります。目標は、閲覧者がアイテムの見た目や機能について全体的に把握できるように、アイテムの重要な特徴を際立たせることです。

ユーザーは画像セット内で画像をズームできるので、最大サイズで 2,000 ピクセル以上の画像を使用してください。AEM アセットでは多くの画像ファイル形式がサポートされますが、可逆圧縮 TIFF、PNG および EPS 画像の使用が推奨されます。

>[!NOTE]
>
>さらに、製品スウォッチを示すサムネールを使用する場合は、次のことをおこなう必要があります。
>
>同じ画像を異なる色、パターンまたは仕上がりで表示するためのビネットまたは異なる写真が必要になります。また、それぞれの色、パターンまたは仕上がりに対応するサムネールファイルも必要です。例えば、同じジャケットをブラック、ブラウン、グリーンで表示する画像セットのサムネールを表示するには、次の項目が必要です。
>
>* 同じジャケットのブラック、ブラウンおよびグリーンの写真。
>* ブラック、ブラウンおよびグリーンの色のサムネール。
>



## 画像セットの作成 {#creating-image-sets}

画像セットは、ユーザーインターフェイスまたはAPIを使用して作成できます。 ここでは、ユーザインターフェイスで画像セットを作成する方法について説明します。

>[!NOTE]
>
>[バッチセットプリセット](/help/assets/config-dms7.md#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets)を使用して画像セットを自動的に作成することもできます。

**重要：**&#x200B;バッチセットは IPS（Image Production System）によってアセット取り込みの一環として作成され、Dynamic Media - Scene7 モードでのみ使用できます。

画像セットに追加したアセットは、自動的に英数字順で追加されます。追加後に、手動でアセットの順番を変更したり、並べ替えたりすることができます。

>[!NOTE]
>
>Image sets are not supported for assets with `,` (comma) in the file name.

**画像セットを作成するには**:

1. In **Assets**, navigate to where you want to create an image set, tap **[!UICONTROL Create]**, and select **[!UICONTROL Image Set]**. また、アセットを格納しているフォルダー内からセットを作成することもできます。

   ![chlimage_1-340](assets/chlimage_1-340.png)

1. On the Image Set Editor page, in the **[!UICONTROL Title]** field, enter a name for the Image Set. この名前は、画像セット全般のバナーに表示されます。オプションで、説明を入力します。

   ![chlimage_1-341](assets/chlimage_1-341.png)

   >[!NOTE]
   >
   >画像セットを作成するときに、画像セットのサムネールを変更したり、画像セット内のアセットに基づいて AEM がサムネールを自動的に選択するように設定したりできます。To select a thumbnail, tap **[!UICONTROL Change thumbnail]** and select any image (you can navigate to other folders to find images as well). サムネールを選択した状態で、画像セットからサムネールを自動的に生成することにした場合は、「自動サムネール&#x200B;****&#x200B;に切り替え」を選択します。

1. 次のいずれかの操作をおこないます。

   * Near the upper-left corner of the **[!UICONTROL Image Set Editor]** page, tap **[!UICONTROL Add Asset]**.
   * Near the middle of the **[!UICONTROL Image Set Editor]** page, tap **[!UICONTROL Tap to open Asset Selector]**.
   をタップして、画像セットに含めるアセットを選択します。 選択済みのアセットにはチェックマークアイコンが付いています。作業が完了したら、ページの右上隅付近にある「**[!UICONTROL 選択]**」をタップします。

   アセットセレクターでは、キーワードを入力して **[!UICONTROL Enter]** キーをタップすることで、アセットを検索することができます。フィルターを適用して、検索結果を絞り込むこともできます。パス、コレクション、ファイルタイプおよびタグでフィルタリングできます。フィルターを選択してから、ツールバーの&#x200B;**[!UICONTROL フィルター]**&#x200B;アイコンをタップします。Change the view by tapping the **[!UICONTROL View]** icon and selecting **[!UICONTROL Column View]**, **[!UICONTROL Card View]**, or **[!UICONTROL List View]**.

   [セレクターの操作](working-with-selectors.md)を参照してください。

   ![chlimage_1-342](assets/chlimage_1-342.png)

1. 画像セットに追加したアセットは、自動的に英数字順で追加されます。追加後に、手動でアセットの順番を変更したり、並べ替えたりすることができます。

   If necessary, drag an asset&#39;s **[!UICONTROL Reorder]** icon to the right of the asset&#39;s file name to re-order images up or down the set list.

   ![spin_set_assets](assets/spin_set_assets.png)

   If you want to change a thumbnail or swatch, tap the **[!UICONTROL Thumbnail]** icon next to the image and navigate to the thumbnail or swatch you want. When done selecting all the images tap **[!UICONTROL Save]**.

1. （オプション）次のいずれかの操作をおこないます。

   * To delete an image, select the image, then tap **[!UICONTROL Delete Asset]**.
   * ページの右上隅付近にプリセットを適用するには、「]**プリセット**[!UICONTROL 」をタップした後、すべてのアセットに一度に適用するプリセットを選択します。

1. 「**[!UICONTROL 保存]**」をタップします。新しく作成した画像セットが、作成先のフォルダーに表示されます。

## 画像セットの表示 {#viewing-image-sets}

画像セットは、ユーザーインターフェイスで作成することも、[バッチセットプリセット](/help/assets/config-dms7.md#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets)を使用して自動的に作成することもできます。

**重要** —バッチセットは、IPS [Image Production Systemによってアセット取り込みの一部として作成され] 、ダイナミックメディア — Scene7モードでのみ使用できます。

However, sets created using batch set presets, do *not* appear in the user interface. これらのセットは、3つの方法で表示できます。 （これらの方法は、画像セットをユーザーインターフェイスで作成した場合も使用できます）。

* 個々のアセットのプロパティを開きます。（「**[!UICONTROL セットのメンバー]**」の下に）選択したアセットがメンバーとして含まれるセットが表示されます。セット全体を表示するには、セットの名前をタップします。

   ![chlimage_1-343](assets/chlimage_1-343.png)

* 任意のセットのメンバー画像で、Select the **[!UICONTROL Sets]** menu to display the sets that the asset is a member of.

   ![chlimage_1-344](assets/chlimage_1-344.png)

* From search, you can select **[!UICONTROL Filters]**, then expand **[!UICONTROL Dynamic Media]** and select **[!UICONTROL Sets]**.

   検索結果として、ユーザーインターフェイスで手動で作成した一致するセットか、バッチセットプリセットを使用して自動的に作成した一致するセットが返されます。自動セットの場合、検索クエリは、AEM での検索とは異なる「次の値で始まる」検索条件を使用して実行されます。AEM での検索は、「次を含む」検索条件に基づいて実行されます。Setting the filter to **[!UICONTROL Sets]** is the only way to search automated sets.

   ![chlimage_1-345](assets/chlimage_1-345.png)

>[!NOTE]
>
>[画像セットの編集](#editing-image-sets)の説明に従って、ユーザーインターフェイスを通じて画像セットを表示できます。

## 画像セットの編集 {#editing-image-sets}

画像セットには、次のような様々な編集タスクを実行できます。

* 画像セットへの画像の追加
* 画像セット内の画像の並べ替え
* 画像セットのアセットの削除
* ビューアプリセットの適用
* 画像セットの削除

**画像セットを編集するには**:

1. 次のいずれかの操作をおこないます。

   * 画像セットアセット上にマウスポインターを置き、]**編集**[!UICONTROL （鉛筆アイコン）をタップします。
   * 画像セットアセット上にマウスポインターを置き、**[!UICONTROL 選択]**（チェックマークアイコン）をタップした後、ツールバーの「**[!UICONTROL 編集]**」をタップします。
   * 画像セットアセットをタップしてから、ツールバーの&#x200B;]**編集**[!UICONTROL （鉛筆アイコン）をタップします。

1. 画像セット内の画像を編集するには、次のいずれかの操作をおこないます。

   * アセットを並べ替えるには、画像を新しい位置までドラッグします（並べ替えアイコンを選択して項目を移動します）。
   * 項目を昇順または降順に並べ替えるには、列見出しをタップします。
   * To add an asset or update an existing asset, tap the **[!UICONTROL Add Asset]**. アセットに移動して選択し、ページの右上隅にある「]**選択**[!UICONTROL 」をタップしますページ。
   >[!NOTE]
   >AEMがサムネールに使用する画像を削除し、別の画像に置き換えても、元のアセットは表示されたままになります。

   * To delete an asset, select it, then tap **[!UICONTROL Delete Asset]**.
   * プリセットを適用するには、ページの右上隅付近にある「**[!UICONTROL プリセット]**」をタップ し、ビューアプリセットを選択します。
   * サムネールを追加または変更するには、該当するアセットの右横にあるサムネールアイコンを選択します。新しいサムネールまたはスウォッチアセットに移動して選択し、「**[!UICONTROL 選択]**」をタップします。
   * 画像セット全体を削除するには、画像セットの場所に移動して画像セットを選択し、「**[!UICONTROL 削除]**」をタップします。
   >[!NOTE]
   >
   >画像セットの画像を編集するにはセットに移動し、左パネルの「**[!UICONTROL メンバーを設定]**」をタップしてから、個々のアセットの鉛筆アイコンをタップして編集ウィンドウを開きます。****

1. 編集が完了したら、「**[!UICONTROL 保存]**」をタップします。

## 画像セットのプレビュー {#previewing-image-sets}

詳しくは、[アセットのプレビュー](previewing-assets.md)を参照してください。

## 画像セットの公開 {#publishing-image-sets}

[アセットの公開](publishing-dynamicmedia-assets.md)を参照してください。
