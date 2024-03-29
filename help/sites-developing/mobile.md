---
title: モバイルデバイス用サイトの作成
seo-title: Creating Sites for Mobile Devices
description: モバイルサイトの作成は、標準サイトの作成と似ていますが、テンプレートやコンポーネントの作成も含まれます
seo-description: Creating a mobile site is similar to creating a standard site as it also involves creating templates and components
uuid: 28160758-ea2f-46a9-8f52-d1661a467f06
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: mobile-web
content-type: reference
discoiquuid: e6b2de9e-dddc-4987-af2f-cf3477634ea9
legacypath: /content/docs/en/aem/6-0/develop/mobile/mobile
exl-id: 02fbe809-ba02-49f1-82b8-953c0906f9c9
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '3887'
ht-degree: 65%

---

# モバイルデバイス用サイトの作成{#creating-sites-for-mobile-devices}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

>[!NOTE]
>
>Adobeは、単一ページアプリケーションのフレームワークベースのクライアントサイドレンダリング（React など）を必要とするプロジェクトでは、SPA Editor を使用することをお勧めします。 [詳細情報](/help/sites-developing/spa-overview.md)を参照してください。

モバイルサイトの作成は、標準サイトの作成と似ています。また、テンプレートとコンポーネントの作成も含まれます。 テンプレートとコンポーネントの作成について詳しくは、[テンプレート](/help/sites-developing/templates.md)、[コンポーネント](/help/sites-developing/components.md)および [AEM Sites の開発の手引き](/help/sites-developing/getting-started.md)を参照してください。主な違いは、サイト内での AEM の組み込みのモバイル機能の有効化です。そのためには、モバイルページコンポーネントを使用するテンプレートを作成します。

また、 [レスポンシブデザイン](/help/sites-developing/responsive.md)：複数の画面サイズに対応する単一のサイトを作成します。

使い始めるには、 **We.Retail モバイルデモサイト** AEMで使用可能な

モバイルサイトを作成するには、次の手順に従います。

1. ページコンポーネントを作成します。

   * `sling:resourceSuperType` プロパティを `wcm/mobile/components/page` に設定

      このようにして、コンポーネントはモバイルページコンポーネントに依存します。

   * プロジェクトに特有のロジックを使用して `body.jsp` を作成します。

1. ページテンプレートを作成します。

   * `sling:resourceType` プロパティを新しく作成したページコンポーネントに設定します。
   * `allowedPaths` プロパティを設定します。

1. サイト用のデザインページを作成します。
1. `/content` ノードの下にサイトのルートページを作成します。

   * `cq:allowedTemplates` プロパティを設定します。
   * `cq:designPath` プロパティを設定します。

1. サイトのルートページのページプロパティの「**モバイル**」タブで、デバイスグループを設定します。
1. 新しいテンプレートを使用してサイトページを作成します。

モバイルページコンポーネント（`/libs/wcm/mobile/components/page`）：

* ページプロパティダイアログに「**モバイル**」タブを追加します。
* `head.jsp` を使用して、現在のモバイルデバイスグループを要求から取得します。デバイスグループが見つかった場合は、そのグループの `drawHead()` メソッドを使用して、デバイスグループの関連するエミュレーターの init コンポーネント（オーサーモードの場合のみ）とデバイスグループのレンダリング CSS をインクルードします。

>[!NOTE]
>
>モバイルサイトのルートページはノード階層のレベル 1 に位置する必要があります。また、このページを /content ノードの下に配置することをお勧めします。

## マルチサイトマネージャーによるモバイルサイトの作成 {#creating-a-mobile-site-with-the-multi-site-manager}

標準サイトからモバイルのライブコピーを作成するには、マルチサイトマネージャー（MSM）を使用します。標準サイトは自動的にモバイルサイトに変換されます。モバイルサイトには、モバイルサイトのすべての機能（例：エミュレーター内のエディション）が含まれており、標準サイトと同期してサイトを管理できます。マルチサイトマネージャーのページにある[別のチャネル用のライブコピーの作成](/help/sites-administering/msm.md)を参照してください。

## サーバー側モバイル API {#server-side-mobile-api}

モバイルクラスを含む Java パッケージは次のとおりです。

* [com.day.cq.wcm.mobile.api](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/mobile/api/device/capability/package-summary.html) - MobileConstants を定義します。

* [com.day.cq.wcm.mobile.api.device](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/javadoc/com/day/cq/tagging/package-summary.html) - Device、DeviceGroup および DeviceGroupList を定義します。

* [com.day.cq.wcm.mobile.api.device.capability](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/mobile/api/device/capability/package-summary.html) - DeviceCapability を定義します。

* [com.day.cq.wcm.mobile.api.wurfl](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/javadoc/com/day/cq/tagging/package-summary.html) - WurflQueryEngine を定義します。

* [com.day.cq.wcm.mobile.core](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/javadoc/com/day/cq/tagging/package-summary.html) - WCM モバイルに関連するさまざまなユーティリティメソッドを提供する MobileUtil を定義します。

### モバイルコンポーネント {#mobile-components}

**We.Retail モバイルデモサイト** では、`/libs/foundation/components` にある以下のモバイルコンポーネントを使用します。

<table> 
 <tbody> 
  <tr> 
   <td>名前</td> 
   <td>グループ</td> 
   <td>特徴</td> 
  </tr> 
  <tr> 
   <td>mobilefooter</td> 
   <td>hidden</td> 
   <td> — フッター</td> 
  </tr> 
  <tr> 
   <td>mobileimage</td> 
   <td>モバイル</td> 
   <td> — 画像の基盤コンポーネントに基づく<br />  — デバイスが対応している場合に画像をレンダリングします<br /> </td> 
  </tr> 
  <tr> 
   <td>mobilelist</td> 
   <td>モバイル</td> 
   <td> — リストの基盤コンポーネントに基づく<br /> - listitem_teaser.jsp （デバイスが対応している場合）は、画像をレンダリングします。<br /> </td> 
  </tr> 
  <tr> 
   <td>mobilelogo</td> 
   <td>hidden</td> 
   <td> — ロゴの基盤コンポーネントに基づく<br />  — デバイスが対応している場合に画像をレンダリングします<br /> </td> 
  </tr> 
  <tr> 
   <td>mobilereference</td> 
   <td>モバイル</td> 
   <td><p>- reference 基盤コンポーネントと同様</p> <p>- textimage コンポーネントを mobiletextimage コンポーネントに、画像コンポーネントを mobileimage コンポーネントにマッピングします</p> </td> 
  </tr> 
  <tr> 
   <td>mobiletextimage</td> 
   <td>モバイル</td> 
   <td>- textimage 基盤コンポーネントに基づく<br />  — デバイスが対応している場合に画像をレンダリングします</td> 
  </tr> 
  <tr> 
   <td>mobiletopnav</td> 
   <td>hidden</td> 
   <td><p>- topnav 基盤コンポーネントに基づく</p> <p> — テキストのみをレンダリングします</p> </td> 
  </tr> 
 </tbody> 
</table>

#### モバイルコンポーネントの作成 {#creating-a-mobile-component}

AEM モバイルフレームワークを使用すると、要求を発行するデバイスを感知するコンポーネントを開発できます。以降の節のコード例は、コンポーネントの jsp で AEM モバイル API を使用する方法を示しています。具体的には、次に示す処理の方法を示します。

* リクエストからデバイスを取得します。

   `Device device = slingRequest.adaptTo(Device.class);`

* デバイスグループを取得します。

   `DeviceGroup deviceGroup = device.getDeviceGroup();`

* デバイスグループの機能を取得します。

   `Collection<DeviceCapability> capabilities = deviceGroup.getCapabilities();`

* デバイスの属性（WURFL データベースから生の機能のキーと値）を取得します。

   `Map<String,String> deviceAttributes = device.getAttributes();`

* デバイスのユーザーエージェントを取得します。

   `String userAgent = device.getUserAgent();`

* 現在のページからデバイスグループリスト（作成者によってサイトに割り当てられたデバイスグループ）を取得します。

   `DeviceGroupList deviceGroupList = currentPage.adaptTo(DeviceGroupList.class);`

* デバイスグループが画像をサポートしているかどうかを確認

   `if (deviceGroup.hasCapability(DeviceCapability.CAPABILITY_IMAGES)) {`
...
または
   `if MobileUtil.hasCapability(request, DeviceCapability.CAPABILITY_IMAGES) {`
...

>[!NOTE]
>
>jsp では、`slingRequest` は `<sling:defineObjects>`タグ、`currentPage` は `<cq:defineObjects>` タグを通じて利用できます。

### エミュレーター {#emulators}

エミュレーターに基づくオーサリングを使用すると、作成者はモバイルクライアント向けのコンテンツページを作成できます。モバイルコンテンツのオーサリングは、インプレース WYSIWYG 編集の同じ原則に従います。作成者がモバイルデバイスでのページの外観を確認できるように、モバイルコンテンツページはデバイスエミュレーターを使用して編集されます。

モバイルデバイスエミュレーターは汎用のエミュレーターフレームワークに基づいています。詳しくは、[エミュレーター](/help/sites-developing/emulators.md)を参照してください。

デバイスエミュレーターのページには、モバイルデバイスが表示されます。一方、通常の編集（parsys、コンポーネント）は、デバイスの画面内でおこなわれます。デバイスエミュレーターは、サイト用に設定されるデバイスグループに依存します。1 つのデバイスグループに複数のエミュレーターを割り当てることができます。これにより、すべてのエミュレーターをコンテンツページで使用できるようになります。デフォルトで表示されるのは、サイトに割り当てた最初のデバイスグループに割り当てられた最初のエミュレーターです。ページ上部にあるエミュレーターのカルーセルまたはサイドキックの編集ボタンを使用してエミュレーターを切り替えることができます。

**エミュレーターの作成**

エミュレーターを作成するには、汎用エミュレーターに関するページの[カスタムモバイルエミュレーターの作成](/help/sites-developing/emulators.md)を参照してください。

**モバイルエミュレーターの主な特徴**

* デバイスグループは、複数のエミュレーターのうちの 1 つで構成されます。デバイスグループ設定ページ（例： /etc/mobile/groups/touch）には、`jcr:content` ノードの下の `emulators` プロパティが含まれます。

   メモ：同じエミュレーターが複数のデバイスグループに属する可能性もありますが、あまり意味がありません。

* デバイスグループの設定ダイアログでは、目的のエミュレーターのパスを使用して `emulators` プロパティが設定されます。（例：`/libs/wcm/mobile/components/emulators/iPhone4`）。

* エミュレーターコンポーネント（例： `/libs/wcm/mobile/components/emulators/iPhone4`）は、基本モバイルエミュレーターコンポーネント ( `/libs/wcm/mobile/components/emulators/base`) を拡張します。

* デバイスグループを設定する際は、基本のモバイルエミュレーターを拡張するすべてのコンポーネントを選択できます。 これにより、カスタムエミュレーターを簡単に作成または拡張できます。
* 編集モードの要求時に、エミュレーターの実装を使用してページがレンダリングされます。
* ページのテンプレートでモバイルページコンポーネントを使用する場合は、エミュレーターの機能が（モバイルページコンポーネントの `head.jsp` を使用して）自動的にページに統合されます。

### Device Groups {#device-groups}

モバイルデバイスグループは、デバイスの機能に基づいてモバイルデバイスをセグメント化します。 デバイスグループは、オーサーインスタンス上のエミュレーターベースのオーサリングと、パブリッシュインスタンス上での正しいコンテンツレンダリングに必要な情報を提供します。作成者がモバイルページにコンテンツを追加して公開したら、そのページをパブリッシュインスタンスでリクエストできます。 そこで、エミュレーターの編集ビューの代わりに、設定済みのデバイスグループの 1 つを使用してコンテンツページがレンダリングされます。 デバイスグループの選択は、 [モバイルデバイス検出](#client-side-device-detection). 次に、対応するデバイスグループが、必要なスタイル設定情報を提供します。

デバイスグループは、`/etc/mobile/devices` の下のコンテンツページとして定義され、**モバイルデバイスグループ** テンプレートを使用します。デバイスグループテンプレートは、コンテンツページのフォームでデバイスグループ定義用の設定テンプレートとして機能します。このダイアログの主な特徴を次に示します。

* 場所: `/libs/wcm/mobile/templates/devicegroup`
* 許可されたパス： `/etc/mobile/groups/*`
* ページコンポーネント: `wcm/mobile/components/devicegroup`

#### サイトへのデバイスグループの割り当て {#assigning-device-groups-to-your-site}

モバイルサイトを作成する場合は、サイトにデバイスグループを割り当てる必要があります。 AEMは、デバイスのHTMLおよび JavaScript レンダリング機能に応じて、次の 3 つのデバイスグループを提供します。

* **機能** 携帯電話、Sony Ericsson W800 などの機能デバイス ( 基本HTMLはサポートされますが、画像や JavaScript はサポートされません )。
* **スマート**&#x200B;フォン、Blackberry などのデバイス用。基本的な HTML と画像はサポートされますが、JavaScript はサポートされません。

* **タッチ**&#x200B;フォン：iPad などのデバイス用。HTML、画像、JavaScript およびデバイスの回転が完全にサポートされます。

エミュレーターをデバイスグループに関連付けることができます（[デバイスグループの作成](#creating-a-device-group) を参照）。デバイスグループをサイトに割り当てると、作成者は、ページの編集用にデバイスグループに関連付けられている複数のエミュレーターの中から選択できます。

サイトにデバイスグループを割り当てるには：

1. ブラウザーで、 **Siteadmin** コンソール。
1. 以下のモバイルサイトのルートページを開きます。 **Web サイト**.
1. ページのプロパティを開きます。
1. を選択します。 **モバイル** タブ：

   * デバイスグループを定義します。
   * 「**OK**」をクリックします。

>[!NOTE]
>
>デバイスグループがサイトに対して定義されている場合、それらはサイトのすべてのページに継承されます。

#### デバイスグループフィルター {#device-group-filters}

デバイスグループフィルターは、デバイスがグループに属するかどうかを指定するための、機能に基づく条件を定義します。デバイスグループの作成時には、デバイスの評価に使用するフィルターを選択できます。

AEMがデバイスから HTTP リクエストを受け取ると、実行時に、グループに関連付けられている各フィルターが、デバイスの機能と特定の条件を比較します。 フィルターが必要とするすべての機能を持つデバイスは、グループに属していると見なされます。 機能は WURFL™ データベースから取得されます。

デバイスグループは、機能検出に 0 個以上のフィルターを使用できます。 また、1 つのフィルターを複数のデバイスグループで使用することもできます。 AEMには、グループに対して選択された機能をデバイスに含めるかどうかを決定するデフォルトのフィルターが用意されています。

* CSS
* JPG 画像と PNG 画像
* JavaScript
* デバイスの回転

デバイスグループでフィルターを使用しない場合、デバイスが要求するのは、グループ用に設定された選択済みの機能のみです。

詳しくは、[デバイスグループフィルターの作成](/help/sites-developing/groupfilters.md)を参照してください。

#### デバイスグループの作成 {#creating-a-device-group}

AEMがインストールするグループが要件を満たさない場合は、デバイスグループを作成します。

1. ブラウザーで、 **ツール** コンソール。
1. **ツール**／**モバイル**／**デバイスグループ**&#x200B;の下に新しいページを作成します。**ページを作成**&#x200B;ダイアログで、次の操作を実行します。

   * **タイトル** に「`Special Phones`」と入力します。
   * **名前**&#x200B;に「`special`」と入力します。
   * を選択します。 **モバイルデバイスグループテンプレート**.
   * 「**作成**」をクリックします。

1. CRXDE で、デバイスグループ用のスタイルを格納する **static.css** ファイルを `/etc/mobile/groups/special` ノードの下に追加します。

1. **Special Phones** ページを開きます。
1. デバイスグループを設定するには、 **編集** 隣のボタン **設定**.

   の **一般** タブ：

   * **タイトル**：モバイルデバイスグループの名前
   * **説明**:グループの説明。
   * **User-Agent**:デバイスを照合するユーザーエージェント文字列。 これはオプションで、正規表現にすることができます。 例：`BlackBerryZ10`
   * **機能**:グループが画像、CSS、JavaScript、デバイスの回転を処理できるかどうかを定義します。
   * **画面の最小の幅**&#x200B;および&#x200B;**高さ**
   * **エミュレーターを無効にする**:：コンテンツ編集中にエミュレーターを有効/無効にします。

   の **エミュレーター** タブ：

   * **エミュレーター**：デバイスグループに割り当てられたエミュレーターを選択します。

   の **フィルター** タブ：

   * フィルターを追加するには、「項目を追加」をクリックし、ドロップダウンリストからフィルターを選択します。
   * フィルターは、表示順に評価されます。 デバイスがフィルターの条件を満たさない場合、リスト上の後続のフィルターは評価されません。



1. 「OK」をクリックします。

モバイルデバイスグループの設定ダイアログは、次のように表示されます。

![screen_shot_2012-02-01at22043pm](assets/screen_shot_2012-02-01at22043pm.png)

#### デバイスグループごとのカスタム CSS {#custom-css-per-device-group}

前述のように、カスタム CSS をデザインページの CSS と同様に、デバイスグループページに関連付けることができます。この CSS は、オーサー環境およびパブリッシュ環境で、デバイスグループに特有のページコンテンツのレンダリングに影響します。

* このデバイスグループで使用されるすべてのエミュレーターのオーサーインスタンス上のページ。
* パブリッシュインスタンスのページ（要求のユーザーエージェントがこの特定のデバイスグループ内のモバイルデバイスに一致する場合）

## サーバー側デバイス検出 {#server-side-device-detection}

HTTP 要求を実行するデバイスの機能を決定するには、フィルターとデバイス仕様のライブラリを使用します。

### デバイスグループフィルターの開発 {#develop-device-group-filters}

デバイスグループフィルターを作成して、一連のデバイス機能要件を定義します。 必要なデバイス機能のグループをターゲットにするために必要な数のフィルターを作成します。

組み合わせを使用して機能のグループを定義できるようにフィルターをデザインします。 通常、異なるデバイスグループの機能が重複します。 したがって、複数のデバイスグループ定義で一部のフィルターを使用する場合があります。

作成したフィルターは、グループ設定で使用できます。

詳しくは、を参照してください。 [デバイスグループフィルターの作成](/help/sites-developing/groupfilters.md).

### WURFL™データベースの使用 {#using-the-wurfl-database}

AEM ではサポート対象外のバージョンの [WURFL](http://wurfl.sourceforge.net/index.php)™ データベースを使用して、デバイスのユーザーエージェントに基づいてデバイスの機能（画面の解像度、JavaScript のサポートなど）を照会します。

WURFL™ データベースの XML コードは、`wurfl.xml` ファイル（`/libs/wcm/mobile/devicespecs/wurfl.xml.`）を解析することによって、`/var/mobile/devicespecs` の下にあるノードとして表されます。ノードに対する拡張は `cq-mobile-core` バンドルの初回起動時に行われます。

デバイスの機能はノードのプロパティとして保存され、ノードはデバイスモデルを表します。 クエリを使用して、デバイスまたはユーザーエージェントの機能を取得できます。

WURFL™データベースが進化しているので、カスタマイズまたは置き換えが必要になる場合があります。 モバイルデバイスデータベースを更新するには、次のオプションがあります。

* この使用を許可するライセンスをお持ちの場合は、ファイルを最新バージョンに置き換えます。 「別の WURFL データベースのインストール」を参照してください。
* AEM で使用可能なバージョンを使用して、ユーザーエージェント文字列を照合し、既存の WURFL™ デバイスを指定する正規表現を設定します。[正規表現に基づくユーザーエージェント照合の追加](#adding-a-regexp-based-user-agent-matching)を参照してください。

#### WURFL™機能へのユーザーエージェントのマッピングのテスト {#testing-the-mapping-of-a-user-agent-to-wurfl-capabilities}

デバイスがモバイルサイトにアクセスすると、AEMはデバイスを検出し、その機能に従ってデバイスグループにマッピングし、デバイスグループに対応するページのビューを送信します。 対応するデバイスグループが、必要なスタイル設定情報を提供します。 このマッピングをモバイルのユーザーエージェントテストページでテストできます。

`http://localhost:4502/etc/mobile/useragent-test.html`

#### 別の WURFL™ データベースのインストール {#installing-a-different-wurfl-database}

AEMと共にインストールされる切り捨てられた WURFL™データベースは、\
2011 年 8 月 31 日。 お使いのバージョンの WURFL が 2011 年 8 月 30 日以降にリリースされた場合は、使用状況がライセンスに準拠していることを確認してください。

WURFL™ データベースをインストールするには：

1. CRXDE Lite で、`/apps/wcm/mobile/devicespecs` フォルダーを参照します。
1. WURFL™ ファイルをそのフォルダーにコピーします。
1. ファイル名を `wurfl.xml` に変更します。

AEM は `wurfl.xml` ファイルを自動的に解析して、`/var/mobile/devicespecs` の下にあるノードを更新します。

>[!NOTE]
>
>WURFL™データベース全体が有効になっている場合、解析とアクティベーションに数分かかる場合があります。 ログで進行状況を確認できます。

#### 正規表現に基づくユーザーエージェントの照合の追加 {#adding-a-regexp-based-user-agent-matching}

ユーザーエージェントを /apps/wcm/mobile/devicespecs/wurfl/regexp に正規表現として追加して、既存の WURFL™ デバイスタイプを指定します。

1. In **CRXDE Lite**/apps/wcm/mobile/devicespecs/regexp の下にノード（例：apple_ipad_ver1）を作成します。
1. ノードに次のプロパティを追加します。

   * **正規表現**:ユーザーエージェントを定義する正規表現。例：.&amp;ast;Mozilla。&amp;ast;iPad.&amp;ast;AppleWebKit。&amp;ast;Safari。&amp;ast;
   * **deviceId**：wurfl.xml で定義されるデバイス ID（例：apple_ipad_ver1）

上記の設定によって、ユーザーエージェントが指定の正規表現に一致するデバイスが、WURFL™ デバイス ID である apple_ipad_ver1（存在する場合）にマップされます。

## クライアント側のデバイス検出 {#client-side-device-detection}

この節では、ページのレンダリングを最適化したり、クライアントに代替の web サイトバージョンを提供したりするために、AEM のデバイスのクライアントサイド検出を使用する方法について説明します。

AEM は `BrowserMap` に基づくデバイスのクライアントサイド検出をサポートしています。`BrowserMap` は、`/etc/clientlibs/browsermap` 下のクライアントライブラリとして AEM に同梱されています。

`BrowserMap` では、次の 3 つの方法を使用して、代替 web サイトをクライアントに提供できます。この方法は、次の順序で使用されます。

1. [代替リンク](#providing-alternate-links)

1. [デバイスグループ専用の URL](#defining-a-device-group-specific-url)
1. [セレクターベースの URL](#defining-selector-based-urls)

>[!NOTE]
>
>クライアントライブラリの統合について詳しくは、[クライアント側 HTML ライブラリの使用](/help/sites-developing/clientlibs.md)を参照してください。

### 代替リンクの設定 {#providing-alternate-links}

`PageVariantsProvider` OSGi サービスは、同じファミリーに属するサイトに対して代替リンクを生成できます。サービスが考慮するサイトを設定するには、サイトのルートから `jcr:content` ノードに `cq:siteVariant` ノードを追加する必要があります。

`cq:siteVariant` ノードには以下のプロパティが必要です。

* `cq:childNodesMapTo` - 子ノードのマップ先のリンク要素の属性を指定します。ルートノードの子がグローバル web サイトの言語バリアント用のルートを表すように web サイトのコンテンツを構成することをお勧めします（例：`/content/mysite/en`、`/content/mysite/de`）。この場合、`cq:childNodesMapTo`の値を`hreflang`にする必要があります。

* `cq:variantDomain` - ページバリアントの絶対 URL を生成するために使用する `Externalizer` ドメインを示します。この値が設定されていない場合は、相対リンクを使用してページバリアントが生成されます。

* `cq:variantFamily` - このサイトが属する Web サイトのファミリーを示します。同じ Web サイトのデバイス特有の複数の表現は同じファミリーに属している必要があります。
* `media` - リンク要素のメディア属性の値を格納します。`BrowserMap` が登録した `DeviceGroups` の名前を使用することをお勧めします。これにより、`BrowserMap` ライブラリは、クライアントを Web サイトの適切なバリアントに自動的に転送できます。

#### PageVariantsProvider と Externalizer {#pagevariantsprovider-and-externalizer}

`cq:siteVariant`ノードの`cq:variantDomain`プロパティの値が空でない場合、`PageVariantsProvider`サービスはこの値を`Externalizer`サービスの設定ドメインとして使用して絶対リンクを生成します。使用する設定を反映させるために、`Externalizer`サービスの設定を確認します。

>[!NOTE]
>
>AEM を操作しているときは、このようなサービスの設定を管理する方法がいくつかあります。詳細および推奨事項については、[OSGi の設定](/help/sites-deploying/configuring-osgi.md)を参照してください。

### デバイスグループ固有の URL の定義 {#defining-a-device-group-specific-url}

代替リンクを使用しない場合は、各 `DeviceGroup` にグローバル URL を設定できます。`browsermap.standard`クライアントライブラリを組み込み、デバイスグループを再定義する独自のクライアントライブラリを作成することをお勧めします。

 は、カスタマイズされたクライアントライブラリから同名の新しいデバイスグループを作成して `BrowserMap`BrowserMap オブジェクトに追加することで、デバイスグループ定義を上書きできるように設計されます。

>[!NOTE]
>
>詳しくは、 [カスタマイズされた BrowserMap](#using-browsermap-on-your-pages) 」セクションに入力します。

### セレクターベースの URL の定義 {#defining-selector-based-urls}

`BrowserMap` 用の代替サイトを指定するために以前のメカニズムを採用していない場合は、`DeviceGroups` の名前を使用するセレクターが `URL` に追加されます。この場合、要求を処理する独自のサーブレットを指定する必要があります。

例えば、`www.example.com/index.html` を閲覧するデバイスが BrowserMap によって `smartphone` と識別された場合、そのデバイスは `www.example.com/index.smartphone.html.` に転送されます。

### ページでの BrowserMap の使用 {#using-browsermap-on-your-pages}

標準の BrowserMap クライアントライブラリをページで使用するには、ページの `head` セクションで `cq:include` タグを使用して `/libs/wcm/core/browsermap/browsermap.jsp` ファイルを含める必要があります。

```xml
<cq:include script="/libs/wcm/core/browsermap/browsermap.jsp" />
```

`JSP` ファイルで `BrowserMap` クライアントライブラリを追加する以外にも、`client-side` に設定した `cq:deviceIdentificationMode` 文字列プロパティを web サイトのルートの下にある `jcr:content` ノードに追加する必要があります。

### BrowserMap のデフォルト動作の上書き {#overriding-browsermap-s-default-behavior}

（`BrowserMap` を上書きするか、またはプローブを追加して）`DeviceGroups` をカスタマイズする場合は、`browsermap.standard` クライアント側ライブラリを埋め込む独自のクライアント側ライブラリを作成する必要があります。

さらに、`JavaScript` コードで `BrowserMap.forwardRequest()` メソッドを手動で呼び出す必要があります。

>[!NOTE]
>
>クライアントライブラリの統合について詳しくは、[クライアント側 HTML ライブラリの使用](/help/sites-developing/clientlibs.md)を参照してください。

カスタマイズされた `BrowserMap` クライアントライブラリの作成が完了したら、次の手順を実行することをお勧めします。

1. アプリケーションで `browsermap.jsp` ファイルを作成します。

   ```xml
   <%@include file="/libs/foundation/global.jsp" %>
   <%@ taglib prefix="c" uri="https://java.sun.com/jsp/jstl/core" %>
   <%@ page import="
       com.day.cq.wcm.api.variants.PageVariant,
       com.day.cq.wcm.api.variants.PageVariantsProvider,
       com.day.cq.wcm.api.devicedetection.DeviceIdentificationMode,
       com.day.cq.wcm.api.WCMMode"
   %>
   <%
       final PageVariantsProvider p = sling.getService(PageVariantsProvider.class);
       if(p == null) {
           throw new IllegalStateException("Missing PageVariantsProvider service");
       }
       for(PageVariant v : p.getVariants(currentPage, slingRequest)) {
           final String curVar = v.getAttributes().get("data-current-variant");
           String media = v.getAttributes().get("media");
           if (media != null) {
               media = media.replaceAll(" ", "");
           }
   %>
       <link
           rel="alternate"
           data-cq-role="site.variant"
           title="<%= xssAPI.encodeForHTMLAttr(v.getTitle()) %>"
           hreflang="<%= xssAPI.encodeForHTMLAttr(v.getAttributes().get("hreflang")) %>"
           media="<%= xssAPI.encodeForHTMLAttr(media) %>"
           href="<%= xssAPI.getValidHref(v.getURL()) %>"
           <% if(curVar != null) { %> data-current-variant="<%= curVar %>"<% } %>
       />
   <%
       }
       Boolean browserMapEnabled = true;
       final DeviceIdentificationMode dim = sling.getService(DeviceIdentificationMode.class);
       String[] selectors  = slingRequest.getRequestPathInfo().getSelectors();
       boolean isPortletRequest = false;
       for (int i = 0; i < selectors.length; i++) {
           if ("portlet".equals(selectors[i])) {
               isPortletRequest = true;
               break;
           }
       }
       if (isPortletRequest) {
           log.debug("Request was made by a portlet container - BrowserMap will not be embedded");
       } else {
           final WCMMode wcmMode = WCMMode.fromRequest(slingRequest);
           boolean shouldIncludeClientLib = false;
           if (WCMMode.EDIT != wcmMode && WCMMode.PREVIEW != wcmMode && WCMMode.DESIGN != wcmMode) {
               if (dim != null) {
                   final String mode = dim.getDeviceIdentificationModeForPage(currentPage);
                   shouldIncludeClientLib = DeviceIdentificationMode.CLIENT_SIDE.equals(mode);
                   if (shouldIncludeClientLib) {
                       browserMapEnabled = (Boolean) request.getAttribute("browsermap.enabled");
                       if (browserMapEnabled == null) {
                           browserMapEnabled = true;
                       }
                   }
               }
           }
   %>
           <c:if test="<%= !browserMapEnabled %>">
               <meta name="browsermap.enabled" content="false">
           </c:if>
           <c:if test="<%= shouldIncludeClientLib %>">
               <meta name="viewport" content="width=device-width, initial-scale=1.0">
               <cq:includeClientLib categories="browsermap.custom"/>
           </c:if>
   <%
       }
   %>
   ```

1. head セクションに `broswermap.jsp` ファイルをインクルードします。

   ```xml
   <cq:include script="browsermap.jsp" />
   ```

### 特定のページからの BrowserMap の除外 {#excluding-browsermap-from-certain-pages}

クライアント検出を必要としない一部のページから BrowserMap ライブラリを除外する場合は、request 属性を追加できます。

```xml
<%
request.setAttribute("browsermap.enabled", false);
%>
```

これにより、`/libs/wcm/core/browsermap/browsermap.jsp` スクリプトは、`BrowserMap` が検出を行わないようにする meta タグをページに追加するようになります。

```xml
<meta name="browsermap.enabled" content="false">
```

### Web サイトの特定のバージョンのテスト {#testing-a-specific-version-of-a-web-site}

通常、BrowserMap スクリプトは常に最適なバージョンの Web サイトに訪問者をリダイレクトします。通常、必要に応じて、訪問者をデスクトップまたはモバイルサイトにリダイレクトします。

特定のバージョンの Web サイトをテストするために、`device` パラメーターを URL に追加して、要求のデバイスを強制することができます。次の URL は、モバイルバージョンの Geometrixx Outdoors Web サイトをレンダリングします。

`http://localhost:4502/content/geometrixx-outdoors/en.html?wcmmode=disabled&device=smartphone`

>[!NOTE]
>
>パブリッシュインスタンスの動作をシミュレートするために、`wcmmode` パラメーターは `disabled` に設定されます。

上書きされた の値は Cookie に格納されるので、`device`device パラメーターを各 `URL` に追加せずに Web サイトを閲覧できます。

その結果、デスクトップバージョンの Web サイトに戻るには、`URL` が `device` に設定された同じ `browser` を呼び出す必要があります。

>[!NOTE]
>
>BrowserMap は、上書きされた device の値を `BMAP_device` という Cookie に格納します。この Cookie を削除すると、CQ は現在のデバイス（デスクトップまたはモバイル）に従って適切なバージョンの Web サイトを提供します。

## モバイルの要求の処理 {#mobile-request-processing}

AEM は、タッチデバイスグループに属するモバイルデバイスが発行した要求を次のように処理します。

1. iPad が AEM パブリッシュインスタンスにリクエストを送ります（例：`http://localhost:4503/content/geometrixx_mobile/en/products.html`）。
1. （最初のレベルのページである `/content/geometrixx_mobile` がモバイルページコンポーネントを拡張するかどうかを確認することにより）要求されたページのサイトがモバイルサイトであるかどうかを AEM が判断します。モバイルサイトである場合は、次の処理が行われます。
1. AEM が要求ヘッダーのユーザーエージェントに基づいてデバイスの機能を検出します。
1. AEM がデバイスの機能をデバイスグループにマップし、デバイスグループセレクターとして`touch`を設定します。

1. AEM がリクエストを `http://localhost:4503/content/geometrixx_mobile/en/products.touch.html.` にリダイレクト 
1. AEM が応答を iPad に送信します。

   * `products.touch.html` は通常の方法でレンダリングされます。このページはキャッシュ可能です。
   * レンダリングコンポーネントでは、セレクターを使用してプレゼンテーションを変更します。
   * AEM では、ページ内のすべての内部リンクにモバイルセレクターを自動的に追加します。

### 統計 {#statistics}

モバイルデバイスから AEM サーバーに対して行われたリクエスト数に関する一部の統計を取得できます。リクエスト数は次のように分類できます。

* デバイスグループごと、およびデバイス
* 年、月、日

統計を表示するには：

1. 次に移動： **ツール** コンソール。
1. を開きます。 **デバイス統計** 下のページ **ツール** > **モバイル**.

1. リンクをクリックすると、特定の年、月または日の統計を表示できます。

この **統計** ページは次のようになります。

![screen_shot_2012-02-01at24353pm](assets/screen_shot_2012-02-01at24353pm.png)

>[!NOTE]
>
>**統計**&#x200B;ページは、モバイルデバイスが初めて AEM にアクセスし、そのデバイスが検出されると作成されます。それ以前にこのページを使用することはできません。

統計内にエントリを生成する必要がある場合は、次の手順を実行できます。

1. モバイルデバイスまたはエミュレーター（例えば、Firefox の場合は https://chrispederick.com/work/user-agent-switcher/）を使用します。
1. オーサリングモードを無効にして、オーサーインスタンスでモバイルページをリクエストします。次に例を示します。

   `http://localhost:4502/content/geometrixx_mobile/en/products.html?wcmmode=disabled`

これで、**統計**&#x200B;ページを使用できるようになります。

### 「友人にリンクを送信」リンク用のページキャッシュのサポート {#supporting-page-caching-for-send-link-to-a-friend-links}

デバイスグループ用にレンダリングされたページは、ページURLの中でデバイスグループセレクタ、例えば `/content/mobilepage.touch.html` によって区別されるため、モバイルページは通常 Dispatcher でキャッシュすることができます。セレクタのないモバイルページへのリクエストは、決してキャッシュされません。この場合、デバイス検出が動作し、最終的に一致するデバイスグループ（またはその点では「nomatch」）にリダイレクトされるからです。デバイスグループセレクターを使用してレンダリングされたモバイルページは、リンクリライターによって処理されます。このリンクは、ページ内のすべてのリンクを書き換え、デバイスグループセレクターも含みます。

したがって、次のシナリオが発生する可能性があります。

Alice というユーザーが `coolpage.feature.html` にリダイレクトされ、その URL を友人の Bob に送信します。Bob は `touch` デバイスグループに分類される別のクライアントを使用してその URL にアクセスします。

`coolpage.feature.html` がフロントエンドキャッシュから提供される場合、要求を分析して、モバイルセレクターが新しいユーザーエージェントに一致しないことを確認する機会が AEM にはありません。そのため、Bob は誤った表現を取得することになります。

この問題を解決するために、単純な選択の UI をページにインクルードできます。このようなページでは、AEM で選択されたデバイスグループをエンドユーザーが上書きできます。上記の例では、エンドユーザーが自分のデバイスで十分だと思う場合、ページ上に表示されたリンク（またはアイコン）により、`coolpage.touch.html` に切り替えることができます。
