---
title: アセットインサイト機能を使用して画像の使用状況を追跡する
description: アセットインサイト機能を使用すると、サードパーティWebサイト、マーケティングキャンペーンおよびアドビのクリエイティブソリューションで使用される画像のユーザー評価と使用状況統計を追跡できます。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 0e0e2aa693c30c8e1ef1033b936b82d83e5b348e

---


# アセットインサイト {#asset-insights}

アセットインサイト機能を使用して、サードパーティの Web サイト、マーケティングキャンペーン、アドビのクリエイティブソリューションで使用されるアセットのユーザーのレーティングと使用状況統計を追跡する方法について説明します。

アセットインサイト機能では、サードパーティの Web サイト、マーケティングキャンペーン、アドビのクリエイティブソリューションで使用されるアセットのユーザーのレーティングと使用状況統計を追跡して、アセットのパフォーマンスと人気に関するインサイトを導き出すことができます。

アセットインサイトでは、アセットの評価回数、クリック数、インプレッション数（アセットが Web サイトに読み込まれた回数）など、ユーザーのアクティビティの詳細を取得します。これらの統計情報に基づいてアセットにスコアを割り当てます。スコアとパフォーマンス統計を使用して、人気が高いアセットをカタログやマーケティングキャンペーンなどに含めるために選ぶことができます。このような統計に基づいて、アセットのアーカイブやライセンスの更新ポリシーを策定することさえできます。

アセットインサイトがアセットの使用状況統計を Web サイトから取得するためには、アセットの埋め込みコードを Web サイトのコードに組み込む必要があります。

To let Asset Insights display usage statistics for assets, first configure the feature to fetch reporting data from [!DNL Adobe Analytics]. 詳しくは、[アセットインサイトの設定](touch-ui-configuring-asset-insights.md)を参照してください。

>[!NOTE]
>
>インサイトは画像に対してのみサポートされ、提供されます。

## View statistics for an asset {#viewing-statistics-for-an-asset}

メタデータページでアセットインサイトのスコアを確認できます。

1. Assets ユーザーインターフェイス（UI）から、アセットを選択し、ツールバーの「**[!UICONTROL プロパティ]**」アイコンをタップまたはクリックします。
1. プロパティページで、「**[!UICONTROL インサイト]**」タブをタップまたはクリックします。
1. 「**[!UICONTROL インサイト]**」タブで、アセットの使用状況の詳細を確認します。「**[!UICONTROL スコア]**」セクションには、アセットの全体的な使用状況とパフォーマンスのスコアが表示されます。

   使用状況のスコアは、アセットが様々なソリューションで使用された回数です。

   「**[!UICONTROL インプレッション数]**」のスコアは、アセットが Web サイトに読み込まれた回数です。「**[!UICONTROL クリック数]**」の下に表示される数値は、アセットがクリックされた回数です。

1. Review the **[!UICONTROL Usage Statistics]** section to know which entities the asset was part of and which creative solutions recently used it. 使用率が高いほど、ユーザーの間で人気のあるアセットであることを意味します。使用状況データは、次の見出しの下に表示されます。

   * **[!UICONTROL アセット]**：アセットが、コレクションまたは複合アセットに含まれた回数
   * **[!UICONTROL Webおよびモバイル]**:アセットがWebサイトやアプリの一部であった回数
   * **[!UICONTROL ソーシャル]**：アセットが Adobe Social や Adobe Campaign などのソリューションで使用された回数
   * **[!UICONTROL 電子メール]**：アセットが電子メールキャンペーンで使用された回数
   ![usage_statistics](assets/usage_statistics.png)

   >[!NOTE]
   >
   >通常、アセットインサイト機能は、Adobe Analyticsからソリューションデータを定期的に取得するので、「ソリューション」セクションには最新のデータが表示されない場合があります。 表示されるデータが対応する期間は、アセットインサイトが Analytics のデータを取得するために実行するフェッチ操作のスケジュールによって決まります。

1. 特定の期間のアセットのパフォーマンス統計をグラフィカルに表示するには、「**[!UICONTROL パフォーマンス統計]**」セクションで期間を選択します。クリック数やインプレッション数などの詳細がグラフの傾向線として表示されます。

   ![chlimage_1-3](assets/chlimage_1-3.jpeg)

   >[!NOTE]
   >
   >「ソリューション」セクションのデータとは異なり、「パフォーマンス統計」セクションには最新データが表示されます。

1. To obtain the embed code for the asset that you include in websites to gets performance data, tap/click **[!UICONTROL Get Embed Code]** below the asset thumbnail. For more information on how to include your Embed code in third-party web pages, see [Using Page Tracker and Embed code in web pages](touch-ui-using-page-tracker.md).

   ![chlimage_1-303](assets/chlimage_1-303.png)

## View aggregate statistics for assets {#viewing-aggregate-statistics-for-assets}

**[!UICONTROL インサイト表示]**&#x200B;を使用すると、フォルダー内のすべてのアセットのスコアを同時に表示できます。

1. Assets UI で、インサイトを表示するアセットを含むフォルダーに移動します。
1. ツールバーの「レイアウト」アイコンをタップまたはクリックして、「**[!UICONTROL インサイト表示]**」オプションを選択します。
1. このページには、アセットの使用状況スコアが表示されます。様々なアセットのレーティングを比較して、洞察を導きます。

## バックグラウンドジョブのスケジュール {#scheduling-background-job}

アセットインサイトは、Adobe Analytics レポートスイートから定期的にアセットの使用状況データをフェッチします。デフォルトでは、アセットインサイトはデータをフェッチするためのバックグラウンドジョブを 24 時間おきに午前 2 時に実行します。この間隔と時刻は、「**[!UICONTROL Adobe CQ DAM Asset Performance Report Sync Job]**」サービスを Web コンソールで設定して変更できます。

1. AEM のロゴをタップし、**[!UICONTROL ツール／操作／Web コンソール]**&#x200B;に移動します。
1. Open the **[!UICONTROL Adobe CQ DAM Asset Performance Report Sync Job]** service configuration.

   ![chlimage_1-304](assets/chlimage_1-304.png)

1. プロパティスケジューラーの式にスケジューラーの目的の頻度とジョブの開始時間を指定します。変更内容を保存します。
