---
title: ビデオアセットの管理
description: ビデオアセットをアップロード、プレビュー、注釈付け、公開する方法について説明します。
uuid: 56a8c221-409f-4605-97b1-a054dd2abfab
contentOwner: AG
products: SG_EXPERIENCEMANAGER/6.4/ASSETS
discoiquuid: f341fae1-dda3-4917-b6db-ad02fec63702
feature: アセット管理，ビデオ
role: User
exl-id: eb652414-5b10-45af-a8b6-f1de649994c5
source-git-commit: 1795b0faed0570e8130c1ba60de07bda49db8fde
workflow-type: tm+mt
source-wordcount: '798'
ht-degree: 48%

---

# ビデオアセットの管理 {#managing-video-assets}

Adobe Experience Manager（AEM）Assets でビデオアセットを管理および編集する方法について説明します。また、Dynamic Media のライセンスをお持ちの場合は、[Dynamic Media のビデオに関するドキュメント](video.md)を参照してください。

## ビデオアセットのアップロードとプレビュー {#uploading-and-previewing-video-assets}

AEM Assetsは、拡張子がMP4のビデオアセットのプレビューを生成します。 アセットの形式がMP4でない場合は、FFmpegパックをインストールしてプレビューを生成します。 FFmpegは、OGGタイプとMP4タイプのビデオレンディションを作成します。 これらのレンディションは、AEM Assets ユーザーインターフェイスでプレビューすることができます。

1. デジタルアセットフォルダー（またはサブフォルダー）で、デジタルアセットを追加する場所に移動します。
1. アセットをアップロードするには、ツールバーの「**[!UICONTROL 作成]**」をクリックまたはタップして、「**[!UICONTROL ファイル]**」を選択します。または、アセット領域に直接ドロップします。アップロード操作について詳しくは、[アセットのアップロード](managing-assets-touch-ui.md#uploading-assets)を参照してください。
1. カード表示でビデオをプレビューするには、ビデオアセットの&#x200B;**[!UICONTROL 再生]**&#x200B;ボタンをタップします。

   ![chlimage_1-201](assets/chlimage_1-201.png)

   ビデオの一時停止や再生は、**[!UICONTROL カード]**&#x200B;表示でのみ可能です。 **[!UICONTROL リスト]**&#x200B;ビューでは、再生/一時停止ボタンは使用できません。

1. カードの&#x200B;**[!UICONTROL 編集]**&#x200B;アイコンをタップして、**[!UICONTROL 詳細]**&#x200B;ビューでビデオをプレビューします。

   ビデオは、ブラウザーのネイティブなビデオプレーヤーで再生されます。再生、一時停止、音量の調節およびビデオの全画面表示を行うことができます。

   ![chlimage_1-202](assets/chlimage_1-202.png)

## 2 GB を超えるアセットをアップロードするための設定 {#configuration-to-upload-video-assets-that-are-larger-than-gb}

デフォルトでは、ファイルサイズの上限により、AEM Assetsでは2 GBを超えるアセットをアップロードできません。 ただし、この上限は CRXDE Lite を開き、`/apps` ディレクトリ配下にノードを作成することで上書きできます。ノードには、同じノード名とディレクトリ構造および類似した順序のノードプロパティが必要です。

大きなアセットをアップロードするには、AEM Assets設定に加えて、次の設定を変更します。

* トークンの有効期間を増やします。`https://[aem_server]:[port]/system/console/configMgr`のWebコンソールの[!UICONTROL AdobeGranite CSRF Servlet]を参照してください。 詳しくは、[CSRF保護](/help/sites-developing/csrf-protection.md)を参照してください。
* Dispatcher の設定で `receiveTimeout` を増やします。詳しくは、[Adobe Experience Manager Dispatcher の設定](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=en#renders-options)を参照してください。

>[!NOTE]
>
>AEM Classicユーザーインターフェイスには、2 GBのファイルサイズ制限はありません。 また、サイズの大きなビデオでは、エンドツーエンドのワークフローが完全にはサポートされません。

ファイルサイズの制限を高めに設定するには、`/apps` ディレクトリで次の手順を実行します。

1. AEM で、**[!UICONTROL ツール／一般／CRXDE Lite]** をタップします。
1. **[!UICONTROL CRXDE Lite]**&#x200B;ページの左側にあるディレクトリウィンドウで、`/libs/dam/gui/content/assets/jcr:content/actions/secondary/create/items/fileupload`に移動します。 ディレクトリウィンドウを表示するには、`>>`アイコンをタッチします。
1. ツールバーの「**[!UICONTROL ノードをオーバーレイ]**」をタップします。 または、コンテキストメニューの「**[!UICONTROL ノードをオーバーレイ]**」を選択します。
1. **[!UICONTROL ノードをオーバーレイ]**&#x200B;ダイアログで「**[!UICONTROL OK]**」をタップします。

   ![chlimage_1-203](assets/chlimage_1-203.png)

1. ブラウザーを更新します。オーバーレイノード `/apps/dam/gui/content/assets/jcr:content/actions/secondary/create/items/fileupload` が選択されます。
1. サイズ上限を必要なサイズに増やすには、「**[!UICONTROL プロパティ]**」タブで適切な値をバイト単位で入力します。例えば、`32212254720`と入力して、サイズ制限を30 GBに増やします。

1. ツールバーの「**[!UICONTROL すべて保存]**」をタップします。
1. AEM で、**[!UICONTROL ツール／操作／Web コンソール]**&#x200B;をタップします。
1. **[!UICONTROL Adobe Experience Manager Web Console Bundles]**&#x200B;ページの表の&#x200B;**[!UICONTROL Name]**&#x200B;列で、**[!UICONTROL Workflow External Process Job Handler]**&#x200B;を探してタップします。
1. **[!UICONTROL AdobeGranite Workflow External Process Job Handler]**&#x200B;ページで、「**[!UICONTROL Default Timeout]**」と「**[!UICONTROL Max Timeout]**」の両方のフィールドの秒数を`18000`（5時間）に設定します。
1. 「**[!UICONTROL 保存]**」をタップします。
1. AEM で、**[!UICONTROL ツール／ワークフロー／モデル]**&#x200B;をタップします。
1. **[!UICONTROL ワークフローモデル]**&#x200B;ページで、「**[!UICONTROL Dynamic Media Encode Video]**」を選択し、「**[!UICONTROL 編集]**」をタップします。
1. **[!UICONTROL ワークフロー]**&#x200B;ページで、**[!UICONTROL Dynamic Mediaビデオサービスプロセス]**&#x200B;コンポーネントをダブルタップします。
1. **[!UICONTROL ステップのプロパティ]**&#x200B;ダイアログボックスの「**[!UICONTROL 共通]**」タブにある「**[!UICONTROL 詳細設定]**」を展開します。
1. 「**[!UICONTROL タイムアウト]**」フィールドの値を `18000` に指定し、「**[!UICONTROL OK]**」をタップして **[!UICONTROL Dynamic Media エンコーディングビデオ]**&#x200B;ワークフローページに戻ります。
1. ページ上部付近の&#x200B;**[!UICONTROL Dynamic Media Encode Video]**&#x200B;ページタイトルの下にある「**[!UICONTROL 保存]**」をタップします。

## ビデオアセットを公開する {#publishing-video-assets}

ビデオアセットを公開すると、URL として Web ページに含めることや、Web ページに埋め込むことができます。[アセットの公開](publishing-dynamicmedia-assets.md)を参照してください。

## ビデオアセットに注釈を付ける {#annotating-video-assets}

1. アセットコンソールで、アセットカードの&#x200B;**[!UICONTROL 編集]**&#x200B;アイコンをタップして、アセットの詳細ページを表示します。
1. **[!UICONTROL プレビュー]**&#x200B;アイコンをタップしてビデオを再生します。
1. ビデオに注釈を付けるには、「**[!UICONTROL 注釈]**」ボタンをタップします。 注釈がビデオ内の特定の時点（フレーム）に追加されます。

   注釈を付ける際に、キャンバスに描画して、その描画を使用してコメントを含めることができます。コメントはAdobe Experience Manager Assetsに自動的に保存されます。

   ![chlimage_1-204](assets/chlimage_1-204.png)

   注釈ウィザードを終了するには、「**[!UICONTROL 閉じる]**」をタップします。

1. ビデオ内の特定のポイントにジャンプするには、テキストフィールドに時間（秒）を指定し、「**[!UICONTROL ジャンプ]**」をクリックします。 例えば、ビデオの最初の 秒をスキップするには、`20`テキストフィールドに 20 と入力します。

   ![chlimage_1-205](assets/chlimage_1-205.png)

1. 注釈をクリックすると、タイムラインに表示されます。 **[!UICONTROL 削除]**&#x200B;をタップして、注釈をタイムラインから削除します。

   ![chlimage_1-206](assets/chlimage_1-206.png)
