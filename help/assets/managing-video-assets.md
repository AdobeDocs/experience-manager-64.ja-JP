---
title: ビデオアセットの管理
description: ビデオアセットをアップロード、プレビュー、注釈付け、公開する方法について説明します。
uuid: 56a8c221-409f-4605-97b1-a054dd2abfab
contentOwner: AG
products: SG_EXPERIENCEMANAGER/6.4/ASSETS
discoiquuid: f341fae1-dda3-4917-b6db-ad02fec63702
translation-type: tm+mt
source-git-commit: 9ced187ddc9bb2d12922fcc734b20ef9767d8fbf
workflow-type: tm+mt
source-wordcount: '797'
ht-degree: 51%

---


# ビデオアセットの管理 {#managing-video-assets}

Adobe Experience Manager（AEM）Assets でビデオアセットを管理および編集する方法について説明します。また、Dynamic Media のライセンスをお持ちの場合は、[Dynamic Media のビデオに関するドキュメント](video.md)を参照してください。

## ビデオアセットのアップロードとプレビュー {#uploading-and-previewing-video-assets}

AEM Assetsは、拡張子がMP4のビデオアセットに関するプレビューを生成します。 アセットの形式がMP4でない場合は、FFmpegパックをインストールしてプレビューを生成します。 FFmpegは、OGGタイプとMP4タイプのビデオレンディションを作成します。 これらのレンディションは、AEM Assets ユーザーインターフェイスでプレビューすることができます。

1. デジタルアセットフォルダーまたはサブフォルダー内で、デジタルアセットを追加する場所に移動します。
1. アセットをアップロードするには、ツールバーの「**[!UICONTROL 作成]**」をクリックまたはタップして、「**[!UICONTROL ファイル]**」を選択します。または、アセット領域に直接ドロップします。アップロード操作について詳しくは、[アセットのアップロード](managing-assets-touch-ui.md#uploading-assets)を参照してください。
1. カード表示でビデオをプレビューするには、ビデオアセットの&#x200B;**[!UICONTROL 再生]**&#x200B;ボタンをタップします。

   ![chlimage_1-201](assets/chlimage_1-201.png)

   You can pause or play video in the **[!UICONTROL Card]** view only. The Play/Pause button is not available in the **[!UICONTROL List]** view.

1. カードの **[!UICONTROL 編集]** アイコンをタップして、ビデオを **[!UICONTROL 詳細]** 表示にプレビューします。

   ビデオは、ブラウザーのネイティブなビデオプレーヤーで再生されます。再生、一時停止、音量の調節およびビデオの全画面表示をおこなうことができます。

   ![chlimage_1-202](assets/chlimage_1-202.png)

## 2 GB を超えるアセットをアップロードするための設定 {#configuration-to-upload-video-assets-that-are-larger-than-gb}

デフォルトでは、ファイルサイズの制限により、2 GBを超えるアセットはAEM Assetsにアップロードされません。 ただし、この上限は CRXDE Lite を開き、`/apps` ディレクトリ配下にノードを作成することで上書きできます。ノードには、同じノード名とディレクトリ構造および類似した順序のノードプロパティが必要です。

AEM Assetsの設定に加えて、次の設定を変更して大きなアセットをアップロードします。

* トークンの有効期間を増やします。Webコンソールの「 [!UICONTROL AdobeGranite CSRF Servlet] 」()を参照し `https://[aem_server]:[port]/system/console/configMgr`てください。 詳しくは、「 [CSRF保護](/help/sites-developing/csrf-protection.md)」を参照してください。
* Dispatcher の設定で `receiveTimeout` を増やします。詳しくは、[Adobe Experience Manager Dispatcher の設定](https://docs.adobe.com/content/help/ja-JP/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#renders-options)を参照してください。

>[!NOTE]
>
>AEM Classicユーザーインターフェイスには、2 GBのファイルサイズ制限はありません。 また、サイズの大きなビデオでは、エンドツーエンドのワークフローが完全にはサポートされません。

ファイルサイズの制限を高めに設定するには、`/apps` ディレクトリで次の手順を実行します。

1. AEM で、**[!UICONTROL ツール／一般／CRXDE Lite]** をタップします。
1. **[!UICONTROL CRXDE Lite]** ページの左側のディレクトリウィンドウで、に移動し `/libs/dam/gui/content/assets/jcr:content/actions/secondary/create/items/fileupload`ます。 To see the directory window, touch `>>` icon.
1. From the toolbar, tap **[!UICONTROL Overlay Node]**. または、コンテキストメニューの「**[!UICONTROL ノードをオーバーレイ]**」を選択します。
1. **[!UICONTROL ノードをオーバーレイ]**&#x200B;ダイアログで「**[!UICONTROL OK]**」をタップします。

   ![chlimage_1-203](assets/chlimage_1-203.png)

1. ブラウザーを更新します。オーバーレイノード `/jcr_root/apps/dam/gui/content/assets/jcr:content/actions/secondary/create/items/fileupload` が選択されます。
1. サイズ上限を必要なサイズに増やすには、「**[!UICONTROL プロパティ]**」タブで適切な値をバイト単位で入力します。例えば、サイズ上限を 30 GB に増やすには、以下の値を入力します。

   `{sizeLimit : "32212254720"}`

1. From the toolbar, tap **[!UICONTROL Save All]**.
1. AEM で、**[!UICONTROL ツール／操作／Web コンソール]**&#x200B;をタップします。
1. On the **[!UICONTROL Adobe Experience Manager Web Console Bundles]** page, under the **[!UICONTROL Name]** column of the table, locate and tap **[!UICONTROL Adobe Granite Workflow External Process Job Handler]**.
1. In the **[!UICONTROL Adobe Granite Workflow External Process Job Handler]** page, set the seconds for both **[!UICONTROL Default Timeout]** and **[!UICONTROL Max Timeout]** fields to `18000` (five hours).
1. 「**[!UICONTROL 保存]**」をタップします。
1. AEM で、**[!UICONTROL ツール／ワークフロー／モデル]**&#x200B;をタップします。
1. On the **[!UICONTROL Workflow Models]** page, select **[!UICONTROL Dynamic Media Encode Video]**, then tap **[!UICONTROL Edit]**.
1. **[!UICONTROL ワークフロー]** ページで、 **** ダイナミックメディアビデオサービスプロセスコンポーネントを重複タップします。
1. **[!UICONTROL ステップのプロパティ]**&#x200B;ダイアログボックスの「**[!UICONTROL 共通]**」タブにある「**[!UICONTROL 詳細設定]**」を展開します。
1. 「**[!UICONTROL タイムアウト]**」フィールドの値を `18000` に指定し、「**[!UICONTROL OK]**」をタップして **[!UICONTROL Dynamic Media エンコーディングビデオ]**&#x200B;ワークフローページに戻ります。
1. Near the top of the page, below the **[!UICONTROL Dynamic Media Encode Video]** page title, tap **[!UICONTROL Save]**.

## ビデオアセットを公開する {#publishing-video-assets}

ビデオアセットを公開すると、URL として Web ページに含めることや、Web ページに埋め込むことができます。詳しくは、アセット [の公開を参照してください](publishing-dynamicmedia-assets.md)。

## ビデオアセットに注釈を付ける {#annotating-video-assets}

1. From the Assets console, tap the **[!UICONTROL Edit]** icon on the asset card to display the asset details page.
1. Tap the **[!UICONTROL Preview]** icon to play the video.
1. To annotate the video, tap the **[!UICONTROL Annotate]** button. 注釈がビデオ内の特定の時点（フレーム）に追加されます。

   注釈を付けているときは、キャンバスに描画して、図面にコメントを含めることができます。 コメントは自動的にAdobe Experience Managerアセットに保存されます。

   ![chlimage_1-204](assets/chlimage_1-204.png)

   To exit the annotation wizard, tap **[!UICONTROL Close]**.

1. To jump to a specific point in the video, specify the time in seconds in the text field and click **[!UICONTROL Jump]**. 例えば、ビデオの最初の 秒をスキップするには、`20`テキストフィールドに 10 と入力します。

   ![chlimage_1-205](assets/chlimage_1-205.png)

1. 注釈をクリックして、タイムラインに表示します。 Tap **[!UICONTROL Delete]** to remove the annotation from the timeline.

   ![chlimage_1-206](assets/chlimage_1-206.png)
