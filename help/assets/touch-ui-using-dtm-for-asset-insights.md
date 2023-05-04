---
title: DTM を使用したアセットインサイトの有効化
description: Adobe Dynamic Tag Management（DTM）を使用して Assets Insights を有効にする方法を学習します。
contentOwner: AG
feature: Asset Insights,Asset Reports
role: User,Admin
exl-id: d19cea4d-5395-479d-b303-4529ae2c0bf2
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '710'
ht-degree: 51%

---

# DTM を使用したアセットインサイトの有効化 {#enabling-asset-insights-through-dtm}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

Adobe Dynamic Tag Management は、デジタルマーケティングツールをアクティベートするツールです。これは Adobe Analytics のユーザーに無償で提供されます。トラッキングコードをカスタマイズして、サードパーティの CMS ソリューションで Assets Insights を使用できるようにするか、DTM を使用して Assets Insights タグを挿入できます。インサイトのサポートおよび提供が行われるのは、画像に対してのみです。

>[!CAUTION]
>
>Adobe DTM は [!DNL Adobe Experience Platform] に置き換わったことにより非推奨のため、まもなく[提供終了](https://medium.com/launch-by-adobe/dtm-plans-for-a-sunset-3c6aab003a6f)となります。Adobeでは、 [!DNL Adobe Experience Platform] アセットインサイト](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/advanced/asset-insights-launch-tutorial.html?lang=ja) には [ を使用することをお勧めします。

DTM を使用して Assets Insights を有効にするには、次の手順を実行します。

1. 次をタップまたはクリックします。 [!DNL Experience Manager] ロゴをクリックし、に移動します。 **[!UICONTROL ツール]** > **[!UICONTROL Assets]** > **[!UICONTROL インサイト設定]**.
1. [設定 [!DNL Experience Manager] DTMCloud Serviceを使用したインスタンス](../sites-administering/dtm.md)

   にログオンすると、API トークンが使用できるようになります。 [https://dtm.adobe.com](https://dtm.adobe.com/) および訪問 **[!UICONTROL アカウント設定]** を「プロファイル」アイコンから選択します。 この手順は、Assets Insights の観点からは必要ありません。これは、 [!DNL Experience Manager Sites] と Assets Insights は、現在も有効です。

1. にログオンします。 [https://dtm.adobe.com](https://dtm.adobe.com/)を選択し、必要に応じて会社を選択します。
1. 既存の Web プロパティを作成または開く

   * を選択します。 **[!UICONTROL Web プロパティ]** 「 」タブをクリックし、次に「 」をタップまたはクリックします。 **[!UICONTROL プロパティを追加]**.
   * 必要に応じてフィールドを更新し、をタップまたはクリックします。 **[!UICONTROL プロパティを作成]** ( [ドキュメント](https://helpx.adobe.com/jp/experience-manager/using/dtm.html)) をクリックします。

   ![chlimage_1-193](assets/chlimage_1-193.png)

1. 内 **[!UICONTROL ルール]** タブ、選択 **[!UICONTROL ページ型ルール]** ナビゲーションウィンドウで、をタップまたはクリックします。 **[!UICONTROL 新規ルールの作成]**.

   ![chlimage_1-194](assets/chlimage_1-194.png)

1. 展開 **[!UICONTROL Javascript /サードパーティタグ]**. 次に、をタップまたはクリックします。 **[!UICONTROL 新しいスクリプトを追加]** 内 **[!UICONTROL 順次HTML]** タブをクリックして、スクリプトダイアログを開きます。

   ![chlimage_1-195](assets/chlimage_1-195.png)

1. 次をタップまたはクリックします。 [!DNL Experience Manager] ロゴをクリックし、に移動します。 **[!UICONTROL ツール/アセット]**.
1. タップまたはクリック **[!UICONTROL インサイトページトラッカー]**&#x200B;トラッカーコードをコピーし、手順 6 で開いたスクリプトダイアログに貼り付けます。 変更を保存します。

   >[!NOTE]
   >
   >* `AppMeasurement.js` が削除されました。 これは、DTM の Adobe Analytics ツールで使用できるはずです。
   >* `assetAnalytics.dispatcher.init()` の呼び出しは削除されました。この関数は、DTM の Adobe Analytics ツールの読み込みが完了すると呼び出されるはずです。
   >* アセットインサイトページトラッカーがホストされている場所 (AEM、CDN など ) に応じて、スクリプトソースのオリジンを変更する必要がある場合があります。
   >* AEMでホストされるページトラッカーの場合、ソースは、Dispatcher インスタンスのホスト名を使用してパブリッシュインスタンスを指す必要があります。


1. 開く [https://dtm.adobe.com](https://dtm.adobe.com). Web プロパティの「概要」をクリックし、「ツールを追加」をクリックするか既存の Adobe Analytics ツールを開きます。ツールを作成する際に、「設定方法」を「自動」に設定できます。

   ![chlimage_1-196](assets/chlimage_1-196.png)

   必要に応じてステージング／実稼動版レポートスイートを選択します。

1. 「**[!UICONTROL ライブラリ管理]**」を展開し、「**[!UICONTROL ライブラリの読み込み先]**」が「**[!UICONTROL ページの先頭へ移動]**」に設定されていることを確認します。

   ![chlimage_1-197](assets/chlimage_1-197.png)

1. 展開 **[!UICONTROL ページコードのカスタマイズ]**&#x200B;をクリックまたはタップします。 **[!UICONTROL 編集画面を開く]**.

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

   * DTM のページ型ルールには、pagetracker.js コードのみが含まれます。 `assetAnalytics` のフィールドはすべて、デフォルト値の上書きと見なされます。これらは、デフォルトでは必要ありません。
   * このコードは、`assetAnalytics.dispatcher.init()` を呼び出す前に、`_satellite.getToolsByType('sc')[0].getS()` が初期化され、`assetAnalytics,dispatcher.init` が使用可能であることを確認します。このため、手順 11 ではこのコードの追加をスキップできます。
   * Insights ページトラッカーコード（**[!UICONTROL ツール／Assets／Insights ページトラッカー]**）内のコメントに記述されているように、ページトラッカーが `AppMeasurement` オブジェクトを作成しないとき、最初の 3 つの引数（RSID、トラッキングサーバー、訪問者の名前空間）は関係ありません。これを示すため代わりに空の文字列が渡されます。

       その他の引数は、インサイト設定ページ（**[!UICONTROL ツール／アセット／インサイト設定]**）で設定された内容に対応しています。

   * AppMeasurement オブジェクトは、すべての使用可能な SiteCatalyst エンジンで `satelliteLib` に対するクエリを実行して取得されます。複数のタグを設定する場合は、配列セレクターのインデックスを適切に変更します。 配列内のエントリは、DTM インターフェイスで使用できるSiteCatalystツールに従って並べ替えられます。

1. 保存して、コードエディターウィンドウを閉じます。その後、変更内容をツール設定で保存します。
1. 「**[!UICONTROL 承認]**」タブで、承認が保留されている両方の項目を承認します。DTM タグを Web ページに挿入する準備ができました。Web ページに DTM タグを挿入する方法について詳しくは、次のアーカイブページを参照してください： [カスタムページテンプレートへの DTM の統合](https://web.archive.org/web/20180816221834/https://blogs.adobe.com/experiencedelivers/experience-management/integrating-dtm-custom-aem6-page-template).
