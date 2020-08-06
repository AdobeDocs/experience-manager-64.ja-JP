---
title: アセットセレクター
description: アセットセレクターを使用して、Adobe Experience Manager（AEM）Assets 内でアセットの検索、フィルタリングおよび参照をおこなったり、アセットのメタデータを取得したりする方法を学習します。また、アセットセレクターインターフェイスをカスタマイズする方法についても学習します。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 0d70a672a2944e2c03b54beb3b5f734136792ab1
workflow-type: tm+mt
source-wordcount: '480'
ht-degree: 75%

---


# アセットセレクター {#asset-selector}

>[!NOTE]
>
>アセットセレクターは、以前のバージョンの AEM では[アセットピッカー](https://helpx.adobe.com/experience-manager/6-2/assets/using/asset-picker.html)という名前でした。

アセットセレクターを使用すると、Adobe Experience Manager（AEM）Assets 内でアセットを検索、フィルタリングおよび参照できます。また、アセットセレクターを使用して選択したアセットのメタデータを取得できます。アセットセレクターインターフェイスをカスタマイズするには、サポートされたリクエストパラメーターを使用して起動します。これらのパラメーターは、特定のシナリオ向けにアセットセレクターのコンテキストを設定します。

Currently, you can pass the request parameters `Asset Type` (*Image/Video/Text*) and `Selection mode` (*Single/Multiple*) as contextual information for the asset selector, which remains intact throughout the selection.

The asset selector uses the HTML5 **Window.postMessage** message to send data for the selected asset to the recipient.

アセットセレクターは、Granite の基盤ピッカーのボキャブラリに基づいています。デフォルトでは、アセットセレクターは、参照モードで動作します。ただし、Omnisearchエクスペリエンスを使用してフィルターを適用し、特定のアセットを絞り込むことができます。

You can integrate any web page (irrespective of whether it is part of the CQ container) with the asset selector (`https://[AEM_server]:[port]/aem/assetpicker.html`).

## コンテキストパラメーター {#contextual-parameters}

次のリクエストパラメーターを URL で渡して、特定のコンテキストでアセットセレクターを起動できます。

| 名前 | 値 | 例 | 目的 |
|---|---|---|---|
| resource suffix (B) | URL のリソースサフィックスとしてのフォルダーパス：`http://localhost:4502/aem/`<br>`assetpicker.html/<folder_path>` | To launch the asset selector with a particular folder selected, for example with the folder `/content/dam/we-retail/en/activities` selected, the URL should be of the form: `http://localhost:4502/aem/assetpicker.html`<br>`/content/dam/we-retail/en/activities?assettype=images` | アセットセレクターの起動時に特定のフォルダーを選択する必要がある場合、そのフォルダーをリソースサフィックスとして渡します。 |
| mode | single、multiple | `http://localhost:4502/aem/assetpicker.html`<br>`?mode=multiple` <br> `http://localhost:4502/aem/assetpicker.html`<br>`?mode=single` | 複数モードでは、アセットセレクターを使用して、いくつかのアセットを同時に選択できます。 |
| mimetype | アセットの MIME タイプ（`/jcr:content/metadata/dc:format`）（ワイルドカードもサポートされています） | <ul><li>`http://localhost:4502/aem/assetpicker.html`<br>`?mimetype=image/png`</li>  <li>`http://localhost:4502/aem/assetpicker.html`<br>`?mimetype=*png`</li>  <li>`http://localhost:4502/aem/assetpicker.html`<br>`?mimetype=*presentation`</li>  <li>`http://localhost:4502/aem/assetpicker.html`<br>`?mimetype=*presentation&mimetype=*png`</li></ul> | MIME タイプに基づいてアセットをフィルタリングするために使用します |
| dialog | true、false | `http://localhost:4502/aem/assetpicker.html`<br>`?dialog=true` | アセットセレクターを Granite ダイアログとして開くには、これらのパラメーターを使用します。このオプションは、Granite パスフィールドを使用してアセットセレクターを起動し、pickerSrc URL として設定する場合にのみ適用できます。 |
| assettype (S) | images、documents、multimedia、archives | <ul><li>`http://localhost:4502/aem/assetpicker.html`<br>`?assettype=images`</li> <li>`http://localhost:4502/aem/assetpicker.html?assettype=documents`</li> <li>`http://localhost:4502/aem/assetpicker.html?assettype=multimedia`</li> <li>`http://localhost:4502/aem/assetpicker.html?assettype=archives`</li> | 渡された値に基づいてアセットタイプをフィルタリングするには、このオプションを使用します。 |
| root | `<folder_path>` | `http://localhost:4502/aem/`<br>`assetpicker.html?assettype=images`<br>`&root=/content/dam/we-retail/en/activities` | アセットセレクターのルートフォルダーを指定するには、このオプションを使用します。この場合、アセットセレクターを使用すると、ルートフォルダーの下の子アセット（直接／間接）のみを選択できます。 |

## アセットセレクタの使用 {#using-the-asset-selector}

1. アセットセレクターインターフェイスにアクセスするには、`https://[AEM_server]:[port]/aem/assetpicker` に移動します。
1. 目的のフォルダーに移動して、1 つまたは複数のアセットを選択します。

   ![chlimage_1-441](assets/chlimage_1-441.png)

   または、オムニサーチボックスから目的のアセットを検索して選択することもできます。

   ![chlimage_1-442](assets/chlimage_1-442.png)

   オムニサーチボックスを使用してアセットを検索する場合、**[!UICONTROL フィルター]**&#x200B;ウィンドウから様々なフィルターを選択して検索を絞り込むことができます。

   ![chlimage_1-443](assets/chlimage_1-443.png)

1. Tap/click **[!UICONTROL Select]** from the toolbar.
