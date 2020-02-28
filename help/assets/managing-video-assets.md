---
title: ビデオアセットの管理
description: ビデオアセットをアップロード、プレビュー、注釈付け、公開する方法について説明します。
uuid: 56a8c221-409f-4605-97b1-a054dd2abfab
contentOwner: AG
products: SG_EXPERIENCEMANAGER/6.4/ASSETS
discoiquuid: f341fae1-dda3-4917-b6db-ad02fec63702
translation-type: tm+mt
source-git-commit: 9ced187ddc9bb2d12922fcc734b20ef9767d8fbf

---


# ビデオアセットの管理 {#managing-video-assets}

Adobe Experience Manager（AEM）Assets でビデオアセットを管理および編集する方法について説明します。また、Dynamic Media のライセンスをお持ちの場合は、[Dynamic Media のビデオに関するドキュメント](video.md)を参照してください。

## Upload and preview video assets {#uploading-and-previewing-video-assets}

AEM Assetsは、拡張子がMP4のビデオアセットのプレビューを生成します。 アセットの形式がMP4でない場合は、FFmpegパックをインストールしてプレビューを生成します。 FFMPEGは、OGGおよびMP4タイプのビデオレンディションを作成します。 これらのレンディションは、AEM Assets ユーザーインターフェイスでプレビューすることができます。

1. デジタルアセットフォルダーまたはサブフォルダーで、デジタルアセットを追加する場所に移動します。
1. アセットをアップロードするには、ツールバーの「**[!UICONTROL 作成]**」をクリックまたはタップして、「**[!UICONTROL ファイル]**」を選択します。または、アセット領域に直接ドロップします。See [Uploading assets](managing-assets-touch-ui.md#uploading-assets) for details around the upload operation.
1. To preview a video in the Card view, tap the **[!UICONTROL Play]** button on the video asset.

   ![chlimage_1-201](assets/chlimage_1-201.png)

   You can pause or play video in the **[!UICONTROL Card]** view only. The Play/Pause button is not available in the **[!UICONTROL List]** view.

1. カード上の **[!UICONTROL 編集]** ( **[!UICONTROL Edit]** )アイコンをタップして、詳細ビューでビデオをプレビューします。

   ビデオは、ブラウザーのネイティブなビデオプレーヤーで再生されます。再生、一時停止、音量の調節およびビデオの全画面表示を行うことができます。

   ![chlimage_1-202](assets/chlimage_1-202.png)

## Configuration to upload assets that are larger than 2 GB {#configuration-to-upload-video-assets-that-are-larger-than-gb}

デフォルトでは、ファイルサイズの制限により、AEM Assetsでは2 GBを超えるアセットをアップロードできません。 However, you can overwrite this limit by going into CRXDE Lite and creating a node under the `/apps` directory. ノードには、同じノード名とディレクトリ構造および類似した順序のノードプロパティが必要です。

AEM Assets設定に加えて、次の設定を変更し、大きなアセットをアップロードします。

* トークンの有効期限を長くします。 Web Consoleの [!UICONTROL Adobe Granite CSRF Servlet] ()を参照してくださ `https://[aem_server]:[port]/system/console/configMgr`い。 詳しくは、 [CSRF保護を参照してください](/help/sites-developing/csrf-protection.md)。
* ディスパッチャ `receiveTimeout` ー設定のを増やします。 詳しくは、 [Experience Manager Dispatcherの設定を参照してください](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#renders-options)。

>[!NOTE]
>
>AEM Classicユーザーインターフェイスには、2 GBのファイルサイズ制限はありません。 また、サイズの大きなビデオでは、エンドツーエンドのワークフローが完全にはサポートされません。

To configure a higher file size limit, perform the following steps in the `/apps` directory.

1. AEM で、**[!UICONTROL ツール／一般／CRXDE Lite]** をタップします。
1. In the **[!UICONTROL CRXDE Lite]** page, in the directory window on the left, navigate to `/libs/dam/gui/content/assets/jcr:content/actions/secondary/create/items/fileupload`. To see the directory window, touch `>>` icon.
1. From the toolbar, tap **[!UICONTROL Overlay Node]**. または、コンテキストメニューから「**[!UICONTROL ノードをオーバーレイ]**」を選択します。
1. **[!UICONTROL ノードをオーバーレイ]**&#x200B;ダイアログで「**[!UICONTROL OK]**」をタップします。

   ![chlimage_1-203](assets/chlimage_1-203.png)

1. ブラウザーを更新します。オーバーレイノードが `/jcr_root/apps/dam/gui/content/assets/jcr:content/actions/secondary/create/items/fileupload` 選択されます。
1. In the **[!UICONTROL Properties]** tab, enter the appropriate value in bytes to increase the size limit to the desired size. 例えば、サイズ上限を 30 GB に増やすには、以下の値を入力します。

   `{sizeLimit : "32212254720"}`

1. From the toolbar, tap **[!UICONTROL Save All]**.
1. AEM で、**[!UICONTROL ツール／操作／Web コンソール]**&#x200B;をタップします。
1. **[!UICONTROL Adobe Experience Manager Web Console Bundlesページの表の]** Name **[!UICONTROL 列の下で、「]** Adobe Granite Workflow External Process Job Handler」を探してタップします ****。
1. In the **[!UICONTROL Adobe Granite Workflow External Process Job Handler]** page, set the seconds for both **[!UICONTROL Default Timeout]** and **[!UICONTROL Max Timeout]** fields to `18000` (five hours).
1. 「**[!UICONTROL 保存]**」をタップします。
1. AEM で、**[!UICONTROL ツール／ワークフロー／モデル]**&#x200B;をタップします。
1. On the **[!UICONTROL Workflow Models]** page, select **[!UICONTROL Dynamic Media Encode Video]**, then tap **[!UICONTROL Edit]**.
1. On the **[!UICONTROL Workflow]** page, double-tap the **[!UICONTROL Dynamic Media Video Service Process]** component.
1. **[!UICONTROL ステップのプロパティ]**&#x200B;ダイアログボックスの「**[!UICONTROL 共通]**」タブにある「**[!UICONTROL 詳細設定]**」を展開します。
1. 「]**タイムアウト**[!UICONTROL 」フィールドの値を `18000` に指定し、「**[!UICONTROL OK]**」をタップして&#x200B;**[!UICONTROL Dynamic Media エンコーディングビデオ]**&#x200B;ワークフローページに戻ります。
1. Near the top of the page, below the **[!UICONTROL Dynamic Media Encode Video]** page title, tap **[!UICONTROL Save]**.

## ビデオアセットを公開する {#publishing-video-assets}

ビデオアセットを公開すると、URL として Web ページに含めることや、Web ページに埋め込むことができます。詳しくは、ア [セットの公開を参照してくださ](publishing-dynamicmedia-assets.md)い。

## ビデオアセットに注釈を付ける {#annotating-video-assets}

1. From the Assets console, tap the **[!UICONTROL Edit]** icon on the asset card to display the asset details page.
1. Tap the **[!UICONTROL Preview]** icon to play the video.
1. To annotate the video, tap the **[!UICONTROL Annotate]** button. 注釈がビデオ内の特定の時点（フレーム）に追加されます。

   注釈の作成中に、キャンバスに描画し、図面にコメントを含めることができます。コメントはAdobe Experience Manager Assetsに自動的に保存されます。

   ![chlimage_1-204](assets/chlimage_1-204.png)

   To exit the annotation wizard, tap **[!UICONTROL Close]**.

1. To jump to a specific point in the video, specify the time in seconds in the text field and click **[!UICONTROL Jump]**. 例えば、ビデオの最初の 秒をスキップするには、`20`テキストフィールドに 10 と入力します。

   ![chlimage_1-205](assets/chlimage_1-205.png)

1. 注釈をクリックすると、タイムラインに注釈が表示されます。 Tap **[!UICONTROL Delete]** to remove the annotation from the timeline.

   ![chlimage_1-206](assets/chlimage_1-206.png)
