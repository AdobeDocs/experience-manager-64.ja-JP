---
title: Adobe Analytics への接続とフレームワークの作成
seo-title: Connecting to Adobe Analytics and Creating Frameworks
description: SiteCatalyst への AEM の接続とフレームワークの作成について説明します。
seo-description: Learn about connecting AEM to SiteCatalyst and creating frameworks.
uuid: 04325409-435c-4394-9ab7-c9022e19e085
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: integration
content-type: reference
discoiquuid: 88dbfd34-1f8d-47a2-893d-20faf1a80f95
exl-id: 654387e3-d837-4bde-a9e4-962862ad69e9
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '1540'
ht-degree: 62%

---

# Adobe Analytics への接続とフレームワークの作成{#connecting-to-adobe-analytics-and-creating-frameworks}

Adobe AnalyticsでAEMページから Web データを追跡するには、Adobe Analytics Cloud Services 設定とAdobe Analyticsフレームワークを作成します。

* **Adobe Analytics設定：** Adobe Analyticsアカウントに関する情報。 Adobe Analytics設定を使用すると、AEMはAdobe Analyticsに接続できます。 使用するアカウントごとに Adobe Analytics 設定を作成します。
* **Adobe Analytics Framework:** Adobe Analyticsレポートスイートプロパティと CQ 変数間の一連のマッピング。 フレームワークを使用して、Web サイトデータを Adobe Analytics レポートにどのように入力するかを設定します。フレームワークは、Adobe Analytics設定に関連付けられます。 設定ごとに複数のフレームワークを作成できます。

Web ページをフレームワークに関連付けると、フレームワークがそのページおよび子ページの追跡を実行します。ページビューは、Adobe Analytics から取得され、Sites コンソールに表示されます。

## 前提条件 {#prerequisites}

### Adobe Analytics アカウント {#adobe-analytics-account}

Adobe AnalyticsでAEMデータを追跡するには、有効なAdobe Marketing Cloud Adobe Analyticsアカウントが必要です。

Adobe Analyticsアカウントでは、次の操作が必要です。

* **管理者** 権限がある
* **Web サービスアクセス**&#x200B;ユーザーグループに割り当てられている

>[!CAUTION]
>
>（Adobe Analytics 内の）**管理者**&#x200B;権限を持っているだけでは、AEM から Adobe Analytics に接続するのに十分ではありません。アカウントは、**Web サービスアクセス**&#x200B;権限も持っている必要があります。

![chlimage_1-316](assets/chlimage_1-316.png)

先に進む前に、資格情報で次のいずれかの方法を使用してAdobe Analyticsにログインできることを確認してください。

* [Adobe Experience Cloudログイン](https://login.experiencecloud.adobe.com/exc-content/login.html)

* [Adobe Analyticsログイン](https://sc.omniture.com/login/)

### Adobe Analytics データセンターを使用するように AEM を設定 {#configuring-aem-to-use-your-adobe-analytics-data-centers}

Adobe Analytics [データセンター](https://developer.omniture.com/en_US/content_page/concepts-terminology/c-how-is-data-stored) Adobe Analyticsレポートスイートに関連付けられているデータを収集、処理および保存します。 Adobe Analyticsレポートスイートをホストするデータセンターを使用するようにAEMを設定する必要があります。 次の表に、使用可能なデータセンターとその URL を示します。

| データセンター | URL |
|---|---|
| San Jose | https://api.omniture.com/admin/1.4/rest/ |
| ダラス | https://api2.omniture.com/admin/1.4/rest/ |
| ロンドン | https://api3.omniture.com/admin/1.4/rest/ |
| シンガポール | https://api4.omniture.com/admin/1.4/rest/ |
| オレゴン | https://api5.omniture.com/admin/1.4/rest/ |

AEM は、デフォルトではサンノゼのデータセンター（https://api.omniture.com/admin/1.4/rest/）を使用します。

[Web コンソールを使用して OSGi バンドルを設定](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console)してください（**Adobe AEM Analytics HTTP Client**）。を **データセンター URL** AEMページでデータを収集するレポートスイートをホストするデータセンターの場合。

![aa-07](assets/aa-07.png)

1. Web コンソールを Web ブラウザーで開きます（[http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr)）。
1. コンソールにアクセスするための資格情報を入力します。

   >[!NOTE]
   >
   >このコンソールへのアクセス権があるかどうかを確認するには、サイト管理者にお問い合わせください。

1. **Adobe AEM Analytics HTTP Client** という設定項目を選択します。
1. データセンターの URL を追加するには、 **データセンター URL** リストを表示し、ボックスに URL を入力します。

1. リストから URL を削除するには、URL の横の「-」ボタンをクリックします。
1. 「保存」をクリックします。

## Adobe Analytics への接続の設定 {#configuring-the-connection-to-adobe-analytics}

>[!CAUTION]
>
>Adobe Analytics API 内のセキュリティ変更により、AEM に含まれているバージョンの Activity Map は使用できなくなりました。
>
>この [Adobe Analyticsが提供する ActivityMap プラグイン](https://docs.adobe.com/content/help/ja/analytics/analyze/activity-map/getting-started/get-started-users/activitymap-install.translate.html) 現在はを使用する必要があります。

## Activity Map の設定 {#configuring-for-the-activity-map}

>[!CAUTION]
>
>Adobe Analytics API 内のセキュリティ変更により、AEM に含まれているバージョンの Activity Map は使用できなくなりました。
>
>この [Adobe Analyticsが提供する ActivityMap プラグイン](https://docs.adobe.com/content/help/en/analytics/analyze/activity-map/getting-started/get-started-users/activitymap-install.html) 現在はを使用する必要があります。

## Adobe Analytics フレームワークの作成 {#creating-a-adobe-analytics-framework}

使用するレポートスイート ID（RSID）に関して、レポートスイートにデータを入力するサーバーインスタンス（作成者、発行または両方）を制御できます。

* **すべて**：オーサーインスタンスとパブリッシュインスタンスの両方からの情報がレポートスイートに入力されます。
* **オーサー**：オーサーインスタンスからの情報のみがレポートスイートに入力されます。
* **パブリッシュ**：パブリッシュインスタンスからの情報のみがレポートスイートに入力されます。

>[!NOTE]
>
>サーバーインスタンスのタイプを選択することによって、Adobe Analytics への呼び出しは制限されません。RSID を含める呼び出しを制御するだけです。
>
>例えば、*diiweretail* レポートスイートを使用するようにフレームワークを設定し、サーバーインスタンスとして作成者を選択します。ページをフレームワークと共に公開すると、引き続き Adobe Analytics に対して呼び出しがおこなわれますが、その呼び出しに RSID は含まれません。作成者インスタンスからの呼び出しにのみ RSID が含まれます。

1. **ナビゲーション**&#x200B;を使用して、**ツール**、**クラウドサービス**&#x200B;を選択し、**従来のクラウドサービス**&#x200B;を選択します。
2. スクロールして **Adobe Analytics** をクリックし、 **[+]** 次の **利用可能な設定**.
3. 次をクリック： **[+]** Adobe Analytics設定の横にあるリンクをクリックします。

4. **フレームワークを作成**&#x200B;ダイアログで、次の操作を実行します。

   * 「**タイトル**」を指定します。
   * オプションで、リポジトリにフレームワークの詳細を保存するノードの&#x200B;**名前**&#x200B;を指定できます。
   * 選択 **Adobe Analytics Framework**

   「**作成**」をクリックします。

   フレームワークが編集用に開きます。

5. サイドポッド（メインパネルの右側）の「**レポートスイート**」セクションで、「**項目を追加**」をクリックします。次に、ドロップダウンを使用して、レポートスイート ID( 例： `geometrixxauth`) を使用して、フレームワークがやり取りする際に使用します。

   >[!NOTE]
   >
   >左側のコンテンツファインダーでは、レポートスイート ID を選択する際に、Adobe Analytics変数 (SiteCatalyst変数 ) が入力されます。

6. 次に、**実行モード**&#x200B;ドロップダウン（レポートスイート ID の横）を使用して、レポートスイートに情報を送信するサーバーインスタンスを選択します。

   ![aa-framework-01](assets/aa-framework-01.png)

7. サイトのパブリッシュインスタンスでフレームワークを使用できるようにするには、 **ページ** サイドキックのタブで、をクリックします。 **フレームワークをアクティベートします。**

### Adobe Analytics のサーバー設定の設定 {#configuring-server-settings-for-adobe-analytics}

フレームワークシステムを使用すると、各Adobe Analyticsフレームワーク内のサーバー設定を変更できます。

>[!CAUTION]
>
>これらの設定は、データの送信先と送信方法を決定するので、必ず *これらの設定を変更しない* 代わりにAdobe Analyticsの担当者に設定してもらいます。

まず、パネルを開きます。「**サーバー**」の横の下向き矢印を押します。

![server_001](assets/server_001.png)

* **トラッキングサーバー**

   * には、Adobe Analytics呼び出しの送信に使用する URL が含まれます

      * cname — デフォルトはAdobe Analyticsアカウントの「会社名」です。
      * d1 - 情報が送信されるデータセンターに対応しています（d1、d2 または d3 ）。
      * sc.omtrdc.net — ドメイン名

* **トラッキングサーバーを保護**

   * トラッキングサーバーと同じセグメントが格納されています。
   * セキュリティ保護されているページ（https://）からのデータ送信に使用されます。

* **訪問者の名前空間**

   * 名前空間は、トラッキング URL の最初の部分を決定します。
   * 例：名前空間をに変更する **CNAME** を指定すると、Adobe Analyticsに対する呼び出しは次のようになります。 **CNAME.d1.omtrdc.net** デフォルトの代わりに。

## Adobe Analytics フレームワークへのページの関連付け {#associating-a-page-with-a-adobe-analytics-framework}

ページがAdobe Analyticsフレームワークに関連付けられている場合、ページの読み込み時にページはデータをAdobe Analyticsに送信します。 ページに設定される変数は、フレームワークの Adobe Analytics 変数からマッピングされ、取得されます。例えば、ページビューは Adobe Analytics から取得されます。

ページの子は、フレームワークとの関連付けを継承します。例えば、サイトのルートページをフレームワークに関連付けると、サイトのすべてのページがそのフレームワークに関連付けられます。

1. 次の **サイト** コンソールで、トラッキングを設定するページを選択します。
1. コンソールから直接、またはページエディターから&#x200B;**[ページのプロパティ](/help/sites-authoring/editing-page-properties.md)**&#x200B;を開きます。
1. 「**クラウドサービス**」タブを開きます。

1. 以下を使用： **設定を追加** ドロップダウンして選択 **Adobe Analytics** を選択します。 継承が設定されている場合、セレクターが使用可能になる前に無効にする必要があります。

1. **Adobe Analytics** のドロップダウンセレクターに、利用可能なオプションが追加されます。これを使用して、必要なフレームワーク設定を選択します。

1. 「**保存して閉じる**」を選択します。
1. ページを&#x200B;**[公開](/help/sites-authoring/publishing-pages.md)**&#x200B;して、ページおよび接続された設定／ファイルをアクティベートします。
1. 最後に、パブリッシュインスタンス上のページを訪問し、**検索**&#x200B;コンポーネントを使用してキーワード（例：aubergine）を検索します。
1. その後、適切なツールを使用して、Adobe Analyticsに対する呼び出しを確認できます。例： [Adobe Experience Cloud Debugger](https://docs.adobe.com/content/help/en/debugger/using/experience-cloud-debugger.html).
1. 提供されている呼び出しの例では、入力された値（例：aubergine）が eVar7 に格納され、イベントリストが event3 に格納されます。

### ページビュー {#page-views}

ページがAdobe Analyticsフレームワークに関連付けられている場合、ページビュー数を Sites コンソールのリスト表示に表示できます。

詳しくは、[ページ分析データの表示](/help/sites-authoring/pa-using.md)を参照してください。

### 読み込み間隔の設定 {#configuring-the-import-interval}

**Adobe AEM ポーリング設定管理**&#x200B;サービスの適切なインスタンスを設定します。

* **ポーリング間隔**:

   サービスがAdobe Analyticsからページビューデータを取得する間隔（秒）。

   デフォルトの間隔は 43200000 ms（12 時間）です。

* **Enable（有効）**:

   サービスを有効または無効にします。 デフォルトでは、このサービスは有効です。

この OSGi サービスを設定するには、 [Web コンソール](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console) または [リポジトリ内の osgiConfig ノード](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository) ( サービス PID は `com.day.cq.polling.importer.impl.ManagedPollConfigImpl`) をクリックします。

## Adobe Analytics 設定やフレームワークの編集 {#editing-adobe-analytics-configurations-and-or-frameworks}

Adobe Analytics 設定またはフレームワークを作成する場合のように、（従来の）**クラウドサービス**&#x200B;画面に移動します。「**設定を表示**」を選択して、更新する特定の設定へのリンクをクリックします。

Adobe Analytics設定の編集時に、 **編集** ボタンをクリックし、 **コンポーネントを編集** ダイアログ。

## Adobe Analytics フレームワークの削除 {#deleting-adobe-analytics-frameworks}

Adobe Analytics フレームワークを削除するには、まず、[編集するためにフレームワークを開きます](#editing-adobe-analytics-configurations-and-or-frameworks)。

次に、サイドキックの「**ページ**」タブから、「**フレームワークを削除**」を選択します。
