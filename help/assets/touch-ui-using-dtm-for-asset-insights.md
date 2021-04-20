---
title: DTM でのアセットインサイトの有効化
description: Adobe Dynamic Tag Management（DTM）を使用してアセットインサイトを有効にする方法を学習します。
contentOwner: AG
feature: Asset Insights,Asset Reports
role: Business Practitioner,Administrator
translation-type: tm+mt
source-git-commit: 29e3cd92d6c7a4917d7ee2aa8d9963aa16581633
workflow-type: tm+mt
source-wordcount: '685'
ht-degree: 50%

---


# DTM でのアセットインサイトの有効化 {#enabling-asset-insights-through-dtm}

Adobe Dynamic Tag Management は、デジタルマーケティングツールをアクティベートするツールです。これは Adobe Analytics のユーザーに無償で提供されます。トラッキングコードをカスタマイズしてサードパーティのCMSソリューションでアセットインサイトを使用できるようにするか、DTMを使用してアセットインサイトタグを挿入できます。 インサイトのサポートおよび提供がおこなわれるのは、画像に対してのみです。

>[!CAUTION]
>
>AdobeDTMはAdobe Experience Platform Launchの支援のために廃止され、間もなく[提供終了](https://medium.com/launch-by-adobe/dtm-plans-for-a-sunset-3c6aab003a6f)に達する予定です。 Adobeでは、「アセットのインサイト](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/advanced/asset-insights-launch-tutorial.html)に対して起動」を[使用することを推奨します。

DTM を使用してアセットインサイトを有効にするには、次の手順を実行します。

1. AEM のロゴをタップまたはクリックし、**[!UICONTROL ツール／アセット／インサイト設定]**&#x200B;に移動します。
1. [DTM クラウドサービスを使用して AEM インスタンスを設定します](../sites-administering/dtm.md)。

   APIトークンは、[https://dtm.adobe.com](https://dtm.adobe.com/)にログオンし、プロファイルアイコンから&#x200B;**[!UICONTROL アカウント設定]**&#x200B;にアクセスしたら、使用できるはずです。 この手順はアセットインサイトの観点からは必要ありません。AEM Sites とアセットインサイトの統合は現在準備中であるからです。

1. [https://dtm.adobe.com](https://dtm.adobe.com/) にログオンし、必要に応じて会社を選択します。
1. Web プロパティを作成するか既存の Web プロパティを開きます。

   * 「**[!UICONTROL Webプロパティ]**」タブを選択し、「**[!UICONTROL 追加プロパティ]**」をタップまたはクリックします。
   * 必要に応じてフィールドを更新し、「**[!UICONTROL プロパティを作成]**」をタップまたはクリックします（[ドキュメント](https://helpx.adobe.com/jp/experience-manager/using/dtm.html)を参照）。

   ![chlimage_1-193](assets/chlimage_1-193.png)

1. 「**[!UICONTROL ルール]**」タブで、ナビゲーションウィンドウから「**[!UICONTROL ページ型ルール]**」を選択し、「**[!UICONTROL 新しいルールを作成]**」をタップまたはクリックします。

   ![chlimage_1-194](assets/chlimage_1-194.png)

1. **[!UICONTROL Javascript /サードパーティタグ]**&#x200B;を展開します。 次に、「**[!UICONTROL 順次HTML]**」タブの「追加新しいスクリプト&#x200B;**[!UICONTROL 」をタップまたはクリックして、スクリプトダイアログを開きます。]**

   ![chlimage_1-195](assets/chlimage_1-195.png)

1. AEMロゴをタップまたはクリックし、**[!UICONTROL ツール/アセット]**&#x200B;に移動します。
1. 「**[!UICONTROL インサイトページトラッカー]**」をタップまたはクリックし、トラッカーコードをコピーして、手順6で開いたスクリプトダイアログに貼り付けます。 変更内容を保存します。

   >[!NOTE]
   >
   >* `AppMeasurement.js` は削除されました。これは、DTM の Adobe Analytics ツールで使用できるはずです。
   >* `assetAnalytics.dispatcher.init()`への呼び出しは削除されます。 この関数は、DTM の Adobe Analytics ツールの読み込みが完了すると呼び出されるはずです。
   >* アセットインサイトページトラッカーがホストされる場所（例えば、AEM や CDN など）によっては、スクリプトソースのオリジナルを変更する必要があります。
   >* AEMがホストするページトラッカーの場合、ソースは、ディスパッチャーインスタンスのホスト名を使用して、発行インスタンスを指し示す必要があります。


1. [https://dtm.adobe.com](https://dtm.adobe.com) を開きます。Web プロパティの「概要」をクリックし、「ツールを追加」をクリックするか既存の Adobe Analytics ツールを開きます。ツールの作成時に、「設定方法」を「自動」に設定できます。

   ![chlimage_1-196](assets/chlimage_1-196.png)

   必要に応じてステージング／実稼動版レポートスイートを選択します。

1. **[!UICONTROL ライブラリ管理]**&#x200B;を展開し、****&#x200B;のライブラリを読み込みが&#x200B;**[!UICONTROL ページのトップ]**&#x200B;に設定されていることを確認します。

   ![chlimage_1-197](assets/chlimage_1-197.png)

1. 「**[!UICONTROL ページコードをカスタマイズ]**」を展開し、「**[!UICONTROL エディターを開く]**」をクリックまたはタップします。

   ![chlimage_1-198](assets/chlimage_1-198.png)

1. 次のコードをウィンドウに貼り付けます。

   ```java
   var sObj;
   
   if (arguments.length > 0) {
     sObj = arguments[0];
   } else {
     sObj = _satellite.getToolsByType('sc')[0].getS();
   }
   _satellite.notify('in assetAnalytics customInit');
   (function initializeAssetAnalytics() {
     if ((!!window.assetAnalytics) && (!!assetAnalytics.dispatcher)) {
       _satellite.notify('assetAnalytics ready');
       /** NOTE:
           Copy over the call to 'assetAnalytics.dispatcher.init()' from Assets Pagetracker
           Be mindful about changing the AppMeasurement object as retrieved above.
       */
       assetAnalytics.dispatcher.init(
             "",  /** RSID to send tracking-call to */
             "",  /** Tracking Server to send tracking-call to */
             "",  /** Visitor Namespace to send tracking-call to */
             "",  /** listVar to put comma-separated-list of Asset IDs for Asset Impression Events in tracking-call, e.g. 'listVar1' */
             "",  /** eVar to put Asset ID for Asset Click Events in, e.g. 'eVar3' */
             "",  /** event to include in tracking-calls for Asset Impression Events, e.g. 'event8' */
             "",  /** event to include in tracking-calls for Asset Click Events, e.g. 'event7' */
             sObj  /** [OPTIONAL] if the webpage already has an AppMeasurement object, please include the object here. If unspecified, Pagetracker Core shall create its own AppMeasurement object */
             );
       sObj.usePlugins = true;
       sObj.doPlugins = assetAnalytics.core.updateContextData;
       assetAnalytics.core.optimizedAssetInsights();
     }
     else {
       _satellite.notify('assetAnalytics not available. Consider updating the Custom Page Code', 4);
     }
   })();
   ```

   * DTMのページ型ルールには、pagetracker.jsコードのみが含まれます。 `assetAnalytics` のフィールドはすべて、デフォルト値の上書きと見なされます。これらは、デフォルトでは必要ありません。
   * コードは、`_satellite.getToolsByType('sc')[0].getS()`が初期化され、`assetAnalytics,dispatcher.init`が使用可能であることを確認した後、`assetAnalytics.dispatcher.init()`を呼び出します。 このため、手順 11 ではこのコードの追加をスキップできます。
   * インサイトページトラッカーコード（**[!UICONTROL ツール/アセット/インサイトページトラッカー]**）内のコメントに示されているように、ページトラッカーが`AppMeasurement`オブジェクトを作成しない場合、最初の3つの引数(RSID、トラッキングサーバー、訪問者名前空間)は無関係です。 これを示すため代わりに空の文字列が渡されます。

       その他の引数は、インサイト設定ページ（**[!UICONTROL ツール／アセット／インサイト設定]**）で設定された内容に対応しています。

   * AppMeasurement オブジェクトは、すべての使用可能な SiteCatalyst エンジンで `satelliteLib` に対するクエリを実行して取得されます。複数のタグが設定されている場合は、配列セレクターのインデックスをそれに応じて変更します。配列のエントリは、DTM インターフェイスで使用可能な SiteCatalyst ツールの順に並んでいます。

1. コードエディターウィンドウを保存して閉じ、変更をツール設定に保存します。
1. 「**[!UICONTROL 承認]**」タブで、承認待ちの両方を承認します。 DTM タグを Web ページに挿入する準備ができました。DTM タグを Web ページに挿入する方法について詳しくは、[カスタムページテンプレートへの DTM の統合（英語）](https://blogs.adobe.com/experiencedelivers/experience-management/integrating-dtm-custom-aem6-page-template/)を参照してください。
