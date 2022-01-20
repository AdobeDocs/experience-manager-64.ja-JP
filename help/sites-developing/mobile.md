---
title: モバイルデバイス用サイトの作成
seo-title: Creating Sites for Mobile Devices
description: モバイルサイトの作成は標準サイトの作成と同様ですが、この処理にはテンプレートとコンポーネントの作成も含まれます
seo-description: Creating a mobile site is similar to creating a standard site as it also involves creating templates and components
uuid: 28160758-ea2f-46a9-8f52-d1661a467f06
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: mobile-web
content-type: reference
discoiquuid: e6b2de9e-dddc-4987-af2f-cf3477634ea9
legacypath: /content/docs/en/aem/6-0/develop/mobile/mobile
exl-id: 02fbe809-ba02-49f1-82b8-953c0906f9c9
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '3851'
ht-degree: 62%

---

# モバイルデバイス用サイトの作成{#creating-sites-for-mobile-devices}

>[!NOTE]
>
>単一ページアプリケーションフレームワークを基にしたクライアント側レンダリング（React など）が必要なプロジェクトでは、SPA エディターを使用することをお勧めします。[詳細情報](/help/sites-developing/spa-overview.md)を参照してください。

モバイルサイトの作成は標準サイトの作成と同様ですが、この処理にはテンプレートとコンポーネントの作成も含まれます。テンプレートとコンポーネントの作成について詳しくは、[テンプレート](/help/sites-developing/templates.md)、[コンポーネント](/help/sites-developing/components.md)および [AEM Sites の開発の手引き](/help/sites-developing/getting-started.md)を参照してください。主な違いは、サイト内での AEM の組み込みのモバイル機能の有効化です。そのためには、モバイルページコンポーネントを使用するテンプレートを作成します。

また、[レスポンシブデザイン](/help/sites-developing/responsive.md)を使用して、複数の画面サイズに対応する単一のサイトを作成することも検討してください。

作業を開始する際は、AEM で使用可能な **We.Retail モバイルデモサイト**&#x200B;を確認できます。

モバイルサイトを作成するには、次の手順を実行します。

1. ページコンポーネントを作成します。

   * を `sling:resourceSuperType` プロパティを `wcm/mobile/components/page`

      このようにして、コンポーネントはモバイルページコンポーネントに依存します。

   * プロジェクトに特有のロジックを使用して `body.jsp` を作成します。

1. ページテンプレートを作成します。

   * を `sling:resourceType` プロパティを新しく作成されたページコンポーネントに追加します。
   * を `allowedPaths` プロパティ。

1. サイト用のデザインページを作成します。
1. サイトのルートページを `/content` ノード：

   * を `cq:allowedTemplates` プロパティ。
   * を `cq:designPath` プロパティ。

1. サイトのルートページのページプロパティの「**モバイル**」タブで、デバイスグループを設定します。
1. 新しいテンプレートを使用してサイトページを作成します。

モバイルページコンポーネント ( `/libs/wcm/mobile/components/page`):

* ページプロパティダイアログに「**モバイル**」タブを追加します。
* その `head.jsp`の場合は、現在のモバイルデバイスグループをリクエストから取得し、デバイスグループが見つかった場合は、グループの `drawHead()` メソッドを使用して、デバイスグループに関連付けられているエミュレーターの init コンポーネント（オーサーモードのみ）とデバイスグループのレンダリング CSS を含めます。

>[!NOTE]
>
>モバイルサイトのルートページはノード階層のレベル 1 に位置する必要があります。また、このページを /content ノードの下に配置することをお勧めします。

## マルチサイトマネージャーによるモバイルサイトの作成 {#creating-a-mobile-site-with-the-multi-site-manager}

マルチサイトマネージャー (MSM) を使用して、標準サイトからモバイルライブコピーを作成します。標準サイトは、モバイルサイトに自動的に変換されます。モバイルサイトには、モバイルサイトのすべての機能（エミュレーター内のエディションなど）があり、標準サイトと同期して管理できます。の節を参照してください。 [様々なチャネル用のライブコピーの作成](/help/sites-administering/msm.md) をクリックします。

## サーバー側のモバイル API {#server-side-mobile-api}

モバイルクラスを格納する Java パッケージを次に示します。

* [com.day.cq.wcm.mobile.api](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/mobile/api/device/capability/package-summary.html) - MobileConstants を定義します。

* [com.day.cq.wcm.mobile.api.device](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/mobile/api/device/package-summary.html) - Device、DeviceGroup および DeviceGroupList を定義します。

* [com.day.cq.wcm.mobile.api.device.capability](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/mobile/api/device/capability/package-summary.html) - DeviceCapability を定義します。

* [com.day.cq.wcm.mobile.api.wurfl](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/workflow/api/package-summary.html) - WurflQueryEngine を定義します。

* [com.day.cq.wcm.mobile.core](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/mobile/core/package-summary.html) - WCM Mobile を中心とした様々なユーティリティメソッドを提供する MobileUtil を定義します。

### モバイルコンポーネント {#mobile-components}

この **We.Retail モバイルデモサイト** は、以下にある次のモバイルコンポーネントを使用します。 `/libs/foundation/components`:

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
   <td>- フッター</td> 
  </tr> 
  <tr> 
   <td>mobileimage</td> 
   <td>モバイル</td> 
   <td>- image 基盤コンポーネントに基づく<br />
- 画像をレンダリングする（デバイスが対応している場合）<br /> </td> 
  </tr> 
  <tr> 
   <td>mobilelist</td> 
   <td>モバイル</td> 
   <td>- list 基盤コンポーネントに基づく<br />
- listitem_teaser.jsp が画像をレンダリングする（デバイスが対応している場合）<br /> </td> 
  </tr> 
  <tr> 
   <td>mobilelogo</td> 
   <td>非表示</td> 
   <td>- logo 基盤コンポーネントに基づく<br />
- 画像をレンダリングする（デバイスが対応している場合）<br /> </td> 
  </tr> 
  <tr> 
   <td>mobilereference</td> 
   <td>モバイル</td> 
   <td><p> — 参照基盤コンポーネントと同様</p> <p>- textimage コンポーネントを mobiletextimage コンポーネントにマップし、image コンポーネントを mobileimage コンポーネントにマップする</p> </td> 
  </tr> 
  <tr> 
   <td>mobiletextimage</td> 
   <td>モバイル</td> 
   <td>- textimage 基盤コンポーネントに基づく<br />
- 画像をレンダリングする（デバイスが対応している場合）</td> 
  </tr> 
  <tr> 
   <td>mobiletopnav</td> 
   <td>非表示</td> 
   <td><p>- topnav 基盤コンポーネントに基づく</p> <p>- テキストのみをレンダリングする</p> </td> 
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

* デバイス属性（WURFL データベースから生の機能キー/値）を取得します。

   `Map<String,String> deviceAttributes = device.getAttributes();`

* デバイスの user-agent を取得します。

   `String userAgent = device.getUserAgent();`

* 現在のページから、デバイスグループリスト（作成者によってサイトに割り当てられたデバイスグループ）を取得します。

   `DeviceGroupList deviceGroupList = currentPage.adaptTo(DeviceGroupList.class);`

* デバイスグループが画像をサポートしているかどうかを確認します

   `if (deviceGroup.hasCapability(DeviceCapability.CAPABILITY_IMAGES)) {`
...
または
   `if MobileUtil.hasCapability(request, DeviceCapability.CAPABILITY_IMAGES) {`
...

>[!NOTE]
>
>jsp では、 `slingRequest` は、 `<sling:defineObjects>` タグと `currentPage` から `<cq:defineObjects>` タグを使用します。

### エミュレーター {#emulators}

エミュレーターベースのオーサリングを使用すると、作成者はモバイルクライアント向けのコンテンツページを作成できます。モバイルコンテンツのオーサリングでは、インプレース WYSIWYG 編集と同じ原則に従います。作成者がモバイルデバイスでのページの外観を知覚できるように、モバイルコンテンツページはデバイスエミュレーターを使用して編集されます。

モバイルデバイスエミュレーターは汎用のエミュレーターフレームワークに基づいています。詳しくは、[エミュレーター](/help/sites-developing/emulators.md)を参照してください。

デバイスエミュレーターのページには、モバイルデバイスが表示されます。一方、通常の編集（parsys、コンポーネント）は、デバイスの画面内でおこなわれます。デバイスエミュレーターは、サイト用に設定されるデバイスグループに依存します。1 つのデバイスグループに複数のエミュレーターを割り当てることができます。これにより、すべてのエミュレーターをコンテンツページで使用できるようになります。デフォルトで表示されるのは、サイトに割り当てた最初のデバイスグループに割り当てられた最初のエミュレーターです。ページ上部にあるエミュレーターのカルーセルまたはサイドキックの編集ボタンを使用してエミュレーターを切り替えることができます。

**エミュレーターの作成**

エミュレーターを作成するには、汎用エミュレーターに関するページの[カスタムモバイルエミュレーターの作成](/help/sites-developing/emulators.md)を参照してください。

**モバイルエミュレーターの主な特徴**

* デバイスグループは、次のエミュレーターの 1 つで構成されます。デバイスグループ設定ページ（例： ）/etc/mobile/groups/touch には、 `emulators` 以下のプロパティ `jcr:content` ノード。

   注意：同じエミュレーターが複数のデバイスグループに属している可能性がありますが、あまり意味がありません。

* デバイスグループの設定ダイアログから、 `emulators` プロパティに目的のエミュレーターのパスを設定します。 （例：`/libs/wcm/mobile/components/emulators/iPhone4`）。

* エミュレーターコンポーネント ( 例： `/libs/wcm/mobile/components/emulators/iPhone4`) 基本モバイルエミュレーターコンポーネントを拡張する ( `/libs/wcm/mobile/components/emulators/base`) をクリックします。

* 基本のモバイルエミュレーターを拡張する各コンポーネントは、デバイスグループの設定時に選択できます。これにより、カスタムエミュレーターを簡単に作成または拡張できます。
* 編集モードでの要求時には、エミュレーターの実装を使用してページをレンダリングします。
* ページのテンプレートでモバイルページコンポーネントを使用する場合は、エミュレーターの機能が（モバイルページコンポーネントの `head.jsp` を使用して）自動的にページに統合されます。

### Device Groups {#device-groups}

モバイルデバイスグループを使用すると、デバイスの機能に基づくモバイルデバイスのセグメント化が可能になります。デバイスグループは、オーサーインスタンスでのエミュレーターベースのオーサリングおよびパブリッシュインスタンスに適したコンテンツのレンダリングに必要な情報を提供します。作成者がモバイルページにコンテンツを追加して公開すると、そのページをパブリッシュインスタンスで要求できます。その場合、エミュレーターの編集ビューではなく、設定済みのいずれかのデバイスグループを使用してコンテンツページがレンダリングされます。デバイスグループの選択は[モバイルデバイスの検出](#client-side-device-detection)に基づいておこなわれます。一致するデバイスグループが必要なスタイル設定情報を提供します。

デバイスグループは、次のコンテンツページとして定義されます。 `/etc/mobile/devices` また、 **モバイルデバイスグループ** テンプレート。 デバイスグループテンプレートは、コンテンツページのフォームでデバイスグループ定義用の設定テンプレートとして機能します。このダイアログの主な特徴を次に示します。

* 場所: `/libs/wcm/mobile/templates/devicegroup`
* 許可されたパス： `/etc/mobile/groups/*`
* ページコンポーネント: `wcm/mobile/components/devicegroup`

#### サイトへのデバイスグループの割り当て {#assigning-device-groups-to-your-site}

モバイルサイトを作成する場合は、デバイスグループをサイトに割り当てる必要があります。AEM には、デバイスの HTML および JavaScript のレンダリング機能に対応した 3 つのデバイスグループが用意されています。

* **フィーチャー**&#x200B;フォン：Sony Ericsson W800 などのフィーチャーデバイス用。基本的な HTML はサポートされますが、画像と JavaScript はサポートされません。
* **スマート** 携帯電話、Blackberry などのデバイス ( 基本的なHTMLと画像はサポートされますが、JavaScript はサポートされません )。

* **タッチ**&#x200B;フォン：iPad などのデバイス用。HTML、画像、JavaScript およびデバイスの回転が完全にサポートされます。

エミュレーターはデバイスグループに関連付けることができます ( [デバイスグループの作成](#creating-a-device-group)) をクリックし、デバイスグループをサイトに割り当てると、作成者はデバイスグループに関連付けられているエミュレーターを選択して、ページを編集できます。

デバイスグループをサイトに割り当てるには：

1. ブラウザーで、**サイト管理者コンソール**&#x200B;に移動します。
1. 「**Web サイト**」の下にあるモバイルサイトのルートページを開きます。
1. ページプロパティを開きます。
1. 「**モバイル**」タブを選択します。

   * デバイスグループを定義します。
   * 「**OK**」をクリックします。

>[!NOTE]
>
>サイト用のデバイスグループが定義済みの場合は、そのグループがサイトのすべてのページによって継承されます。

#### デバイスグループフィルター {#device-group-filters}

デバイスグループフィルターは、デバイスがグループに属するかどうかを指定するための、機能に基づく条件を定義します。デバイスグループの作成時には、デバイスの評価に使用するフィルターを選択できます。

実行時に AEM がデバイスから HTTP 要求を受信すると、グループに関連付けられている各フィルターはデバイスの機能を特定の条件と比較します。フィルターが要求するすべての機能を備えたデバイスは、グループに属していると見なされます。機能は WURFL™ データベースから取得されます。

デバイスグループでは、0 個以上のフィルターを使用して機能を検出できます。また、複数のデバイスグループで 1 つのフィルターを使用することもできます。AEM には、グループ用に選択された機能がデバイスにあるかどうかを判断するデフォルトのフィルターが用意されています。

* CSS
* JPG 画像と PNG 画像
* JavaScript
* デバイスの回転

デバイスグループでフィルターを使用しない場合、デバイスが要求するのは、グループ用に設定された選択済みの機能のみです。

詳しくは、[デバイスグループフィルターの作成](/help/sites-developing/groupfilters.md)を参照してください。

#### デバイスグループの作成 {#creating-a-device-group}

AEM がインストールするグループが要件を満たさない場合は、デバイスグループを作成します。

1. ブラウザーで、**ツール**&#x200B;コンソールに移動します。
1. 以下に新しいページを作成します **ツール** > **モバイル** > **デバイスグループ**.内 **ページを作成** ダイアログ：

   * 形式 **タイトル** 入力 `Special Phones`.
   * 形式 **名前** 入力 `special`.
   * 「**モバイルデバイスグループテンプレート**」を選択します。
   * 「**作成**」をクリックします。

1. CRXDE で、 **static.css** 次の `/etc/mobile/groups/special` ノード。

1. を開きます。 **スペシャルフォン** ページ。
1. デバイスグループを設定するには、「**設定**」の横にある「**編集**」ボタンをクリックします。

   「**一般**」タブで、次の設定を行います。

   * **タイトル**:モバイルデバイスグループの名前。
   * **説明**：グループの説明
   * **ユーザーエージェント**：デバイスを照合するユーザーエージェント文字列。省略可能です。正規表現を使用できます。例：`BlackBerryZ10`
   * **機能**：グループで画像、CSS、JavaScript またはデバイスの回転を処理できるかどうかを定義します。
   * 「**画面の最小の幅**」と「**画面の最小の高さ**」
   * **エミュレーターを無効にする**：コンテンツの編集時にエミュレーターを有効または無効にします。

   「**エミュレーター**」タブで、次の設定をおこないます。

   * **エミュレーター**：デバイスグループに割り当てられたエミュレーターを選択します。

   「**フィルター**」タブで、次の設定をおこないます。

   * フィルターを追加するには、「項目を追加」をクリックして、ドロップダウンリストからフィルターを選択します。
   * フィルターは表示順に評価されます。デバイスがフィルターの条件を満たしていない場合、リスト内の後続のフィルターは評価されません。



1. 「OK」をクリックします。

モバイルデバイスグループ設定ダイアログを次に示します。

![screen_shot_2012-02-01at22043pm](assets/screen_shot_2012-02-01at22043pm.png)

#### デバイスグループ別のカスタム CSS {#custom-css-per-device-group}

前述のとおり、デザインページの CSS と同様に、カスタム CSS をデバイスグループページに関連付けることができます。この CSS はオーサーインスタンスおよびパブリッシュインスタンスでページコンテンツのデバイスグループ固有のレンダリングに影響を与えるために使用されます。この CSS は次のページに自動的にインクルードされます。

* このデバイスグループで使用する各エミュレーターのオーサーインスタンスのページ
* パブリッシュインスタンスのページ（要求のユーザーエージェントがこの特定のデバイスグループ内のモバイルデバイスに一致する場合）

## サーバー側のデバイス検出 {#server-side-device-detection}

HTTP 要求を実行するデバイスの機能を特定するには、フィルターおよびデバイス仕様のライブラリを使用します。

### デバイスグループフィルターの開発 {#develop-device-group-filters}

デバイスグループフィルターを作成して、一連のデバイスの機能の要件を定義します。デバイスの機能の必要なグループをターゲットとして指定するのに必要な数のフィルターを作成してください。

フィルターを組み合わせて機能のグループを定義できるようにフィルターを設計します。通常、異なるデバイスグループの機能は重複します。そのため、一部のフィルターを複数のデバイスグループ定義と共に使用できます。

作成したフィルターはグループ設定で使用できます。

詳しくは、[デバイスグループフィルターの作成](/help/sites-developing/groupfilters.md)を参照してください。

### WURFL™ データベースの使用 {#using-the-wurfl-database}

AEMは、 [WURFL](http://wurfl.sourceforge.net/index.php)™デバイスの User-Agent に基づいて、デバイスの機能（画面の解像度や javascript のサポートなど）を問い合わせるデータベース。

WURFL™データベースの XML コードは、以下のノードで表されます。 `/var/mobile/devicespecs` を解析することによって `wurfl.xml`～にファイルを送る `/libs/wcm/mobile/devicespecs/wurfl.xml.` ノードへの拡張は、 `cq-mobile-core` バンドルが開始されます。

デバイスの機能はノードプロパティとして格納されます。ノードはデバイスのモデルを表します。クエリを使用して、デバイスまたはユーザーエージェントの機能を取得できます。

WURFL™ データベースは進化しているので、データベースのカスタマイズまたは置き換えが必要になる場合があります。モバイルデバイスデータベースを更新するためのオプションは次のとおりです。

* この使用方法を許可するライセンスを所有している場合は、ファイルを最新バージョンに置き換えます。別の WURFL データベースのインストールを参照してください。
* AEMで使用可能なバージョンを使用して、User-Agent 文字列に一致し、既存の WURFL™デバイスを指す正規表現を設定します。詳しくは、 [正規表現に基づくユーザーエージェントの照合の追加](#adding-a-regexp-based-user-agent-matching).

#### WURFL™ の機能へのユーザーエージェントのマッピングのテスト {#testing-the-mapping-of-a-user-agent-to-wurfl-capabilities}

デバイスがモバイルサイトにアクセスすると、AEM はそのデバイスを検出し、機能に従ってデバイスグループにマップします。また、デバイスグループに対応するページのビューを送信します。一致するデバイスグループが必要なスタイル設定情報を提供します。マッピングは、モバイルユーザーエージェントのテストページでテストできます。

`http://localhost:4502/etc/mobile/useragent-test.html`

#### 別の WURFL™ データベースのインストール {#installing-a-different-wurfl-database}

AEMと共にインストールされる切り捨てられた WURFL™データベースは、\
2011 年 8 月 31 日。 お使いのバージョンの WURFL が 2011 年 8 月 30 日以降にリリースされた場合は、使用状況がライセンスに準拠していることを確認してください。

WURFL™ データベースをインストールするには：

1. CRXDE Liteで、次のフォルダーを作成します。 `/apps/wcm/mobile/devicespecs`
1. WURFL™ ファイルをそのフォルダーにコピーします。
1. ファイル名をに変更します。 `wurfl.xml`.

AEMが自動的に解析する `wurfl.xml` ファイルを作成し、以下のノードを更新します。 `/var/mobile/devicespecs`.

>[!NOTE]
>
>WURFL™ データベース全体が有効な場合は、解析とアクティブ化に数分かかることがあります。進行状況の情報については、ログで確認できます。

#### 正規表現に基づくユーザーエージェント照合の追加 {#adding-a-regexp-based-user-agent-matching}

/apps/wcm/mobile/devicespecs/wurfl/regexp の下に、既存の WURFL™デバイスタイプを指すように、user-agent を正規表現として追加します。

1. **CRXDE Lite** で、/apps/wcm/mobile/devicespecs/regexp の下にノード（例：apple_ipad_ver1）を作成します。
1. この  ノードに次のプロパティを追加します。

   * **正規表現**:ユーザーエージェントを定義する正規表現。例：.&amp;ast;Mozilla。&amp;ast;iPad.&amp;ast;AppleWebKit。&amp;ast;Safari。&amp;ast;
   * **deviceId**:wurfl.xml で定義されているデバイス ID。例：apple_ipad_ver1

上記の設定により、指定された正規表現と User-Agent が一致するデバイスが、apple_ipad_ver1 WURFL™デバイス ID（存在する場合）にマッピングされます。

## クライアント側のデバイス検出 {#client-side-device-detection}

この節では、ページのレンダリングを最適化したり、クライアントに代替の Web サイトバージョンを提供したりするために、AEMのデバイスクライアント側検出を使用する方法について説明します。

AEMは、 `BrowserMap`. `BrowserMap` は、次のクライアントライブラリとしてAEMに出荷されます。 `/etc/clientlibs/browsermap`.

`BrowserMap` では、次の 3 つの方法を使用して、代替 Web サイトをクライアントに提供できます。この方法は、次の順序で使用されます。

1. [代替リンク](#providing-alternate-links)

1. [デバイスグループ専用の URL](#defining-a-device-group-specific-url)
1. [セレクターベースの URL](#defining-selector-based-urls)

>[!NOTE]
>
>クライアントライブラリの統合について詳しくは、[クライアント側 HTML ライブラリの使用](/help/sites-developing/clientlibs.md)を参照してください。

### 代替リンクの設定 {#providing-alternate-links}

この `PageVariantsProvider` OSGi サービスは、同じファミリに属するサイトに対して代替リンクを生成できます。 サービスで考慮するサイトを設定するには、 `cq:siteVariant` ノードを `jcr:content` ノードをサイトのルートから削除します。

この `cq:siteVariant` ノードには次のプロパティが必要です。

* `cq:childNodesMapTo`  — 子ノードをマッピングするリンク要素の属性を決定します。ルートノードの子がグローバル web サイトの言語バリアントのルートを表すように、web サイトのコンテンツを整理することをお勧めします ( 例： `/content/mysite/en`, `/content/mysite/de`) の場合、 `cq:childNodesMapTo` は、 `hreflang`;

* `cq:variantDomain` - ページバリアントの絶対 URL を生成するために使用する `Externalizer` ドメインを示します。この値が設定されていない場合は、相対リンクを使用してページバリアントが生成されます。

* `cq:variantFamily` - このサイトが属する Web サイトのファミリーを示します。同じ Web サイトのデバイス特有の複数の表現は同じファミリーに属している必要があります。
* `media` - リンク要素のメディア属性の値を格納します。`BrowserMap` が登録した `DeviceGroups` の名前を使用することをお勧めします。これにより、`BrowserMap` ライブラリは、クライアントを Web サイトの適切なバリアントに自動的に転送できます。

#### PageVariantsProvider と Externalizer {#pagevariantsprovider-and-externalizer}

When the value of `cq:variantDomain` プロパティ `cq:siteVariant` ノードが空でない場合、 `PageVariantsProvider` この値を `Externalizer` サービス。 必ず `Externalizer` 設定を反映するサービス。

>[!NOTE]
>
>AEM を操作しているときは、このようなサービスの設定を管理する方法がいくつかあります。詳細および推奨事項については、[OSGi の設定](/help/sites-deploying/configuring-osgi.md)を参照してください。

### デバイスグループ専用の URL の定義 {#defining-a-device-group-specific-url}

代替リンクを使用しない場合は、各 `DeviceGroup` にグローバル URL を設定できます。独自のクライアントライブラリを作成して、 `browsermap.standard` クライアントライブラリを作成しますが、デバイスグループは再定義されます。

 は、カスタマイズされたクライアントライブラリから同名の新しいデバイスグループを作成して `BrowserMap`BrowserMap オブジェクトに追加することで、デバイスグループ定義を上書きできるように設計されます。

>[!NOTE]
>
>詳しくは、[カスタマイズされた BrowserMap](#using-browsermap-on-your-pages) に関する節を参照してください。

### セレクターベースの URL の定義 {#defining-selector-based-urls}

`BrowserMap` 用の代替サイトを指定するために以前のメカニズムを採用していない場合は、`DeviceGroups` の名前を使用するセレクターが `URL` に追加されます。この場合、要求を処理する独自のサーブレットを指定する必要があります。

例えば、デバイスが `www.example.com/index.html` ～と識別される `smartphone` （BrowserMap による）が次に転送されます： `www.example.com/index.smartphone.html.`

### ページでの BrowserMap の使用 {#using-browsermap-on-your-pages}

ページで標準の BrowserMap クライアントライブラリを使用するには、 `/libs/wcm/core/browsermap/browsermap.jsp` ファイルを `cq:include`タグをページの `head` 」セクションに入力します。

```xml
<cq:include script="/libs/wcm/core/browsermap/browsermap.jsp" />
```

さらに、 `BrowserMap` クライアントライブラリを `JSP` ファイルを追加する場合は、 `cq:deviceIdentificationMode` 文字列プロパティをに設定 `client-side` から `jcr:content` Web サイトのルートの下のノード。

### BrowserMap のデフォルト動作の上書き {#overriding-browsermap-s-default-behavior}

（`BrowserMap` を上書きするか、またはプローブを追加して）`DeviceGroups` をカスタマイズする場合は、`browsermap.standard` クライアント側ライブラリを埋め込む独自のクライアント側ライブラリを作成する必要があります。

さらに、 `BrowserMap.forwardRequest()` メソッド内で `JavaScript` コード。

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

クライアント検出が不要な一部のページから BrowserMap ライブラリを除外する場合は、request 属性を追加できます。

```xml
<%
request.setAttribute("browsermap.enabled", false);
%>
```

これにより、 `/libs/wcm/core/browsermap/browsermap.jsp` 作成するページにメタタグを追加するスクリプト `BrowserMap` 検出を実行しない場合：

```xml
<meta name="browsermap.enabled" content="false">
```

### 特定のバージョンの Web サイトのテスト {#testing-a-specific-version-of-a-web-site}

通常、BrowserMap スクリプトは常に訪問者を最適なバージョンの Web サイト（デスクトップ、または必要に応じてモバイルサイト）にリダイレクトします。

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

1. iPadがAEMパブリッシュインスタンスにリクエストを送信します ( 例： `http://localhost:4503/content/geometrixx_mobile/en/products.html`
1. AEMは、リクエストされたページのサイトがモバイルサイトかどうかを判断します（最初のレベルのページかどうかを調べます）。 `/content/geometrixx_mobile` は、モバイルページコンポーネントを拡張したものです )。 該当する場合：
1. AEMは、リクエストヘッダー内の User-Agent に基づいてデバイス機能を検索します。
1. AEMはデバイス機能をデバイスグループにマッピングし、 `touch` をデバイスグループセレクターとして使用します。

1. AEMがリクエストをにリダイレクト `http://localhost:4503/content/geometrixx_mobile/en/products.touch.html.`
1. AEMがiPadに応答を送信します。

   * `products.touch.html` は通常の方法でレンダリングされます。このページはキャッシュ可能です。
   * レンダリングコンポーネントでは、セレクターを使用してプレゼンテーションを変更します。
   * AEMは、ページ内のすべての内部リンクにモバイルセレクターを自動的に追加します。

### 統計 {#statistics}

モバイルデバイスによってAEMサーバーに対しておこなわれたリクエスト数に関する統計を取得できます。リクエストの数は、次のように分類できます。

* デバイスグループ別およびデバイス別
* 年別、月別、日別

統計を表示するには：

1. **ツール**&#x200B;コンソールに移動します。
1. **ツール**／**モバイル**&#x200B;から&#x200B;**デバイスの統計**&#x200B;ページを開きます。

1. リンクをクリックして、特定の年、月または日の統計を表示します。

**統計**&#x200B;ページを次に示します。

![screen_shot_2012-02-01at24353pm](assets/screen_shot_2012-02-01at24353pm.png)

>[!NOTE]
>
>この **統計** ページは、モバイルデバイスがAEMに初めてアクセスし、が検出されたときに作成されます。それ以前は利用不可。

統計内にエントリを生成する必要がある場合は、次の手順を実行できます。

1. モバイルデバイスまたはエミュレーター ( 例：Firefox のhttps://chrispederick.com/work/user-agent-switcher/) を使用します。
1. オーサリングモードを無効にして、オーサーインスタンス上のモバイルページをリクエストします。次に例を示します。

   `http://localhost:4502/content/geometrixx_mobile/en/products.html?wcmmode=disabled`

これで、**統計**&#x200B;ページを使用できるようになります。

### 「友人にリンクを送信」リンク用のページキャッシュのサポート {#supporting-page-caching-for-send-link-to-a-friend-links}

通常、モバイルページは Dispatcher でキャッシュできます。これは、デバイスグループ用にレンダリングされるページは、デバイスグループセレクターによってページ URL 内で識別されるからです。 `/content/mobilepage.touch.html`.セレクターのないモバイルページへのリクエストはキャッシュされないので、この場合、デバイス検出が動作し、最終的に一致するデバイスグループ（またはその件に関しては「一致しない」）にリダイレクトされます。 デバイスグループセレクターを使用してレンダリングされるモバイルページは、リンクリライターで処理されます。リンクリライターは、デバイスグループセレクターも含めるようにページ内のすべてのリンクを書き換えて、既に要件を満たしているページをクリックするたびにデバイスの検出が再実行されないようにします。

そのため、次のような状況が発生する可能性があります。

Alice というユーザーが `coolpage.feature.html` にリダイレクトされ、その URL を友人の Bob に送信します。Bob は `touch` デバイスグループに分類される別のクライアントを使用してその URL にアクセスします。

`coolpage.feature.html` がフロントエンドキャッシュから提供される場合、要求を分析して、モバイルセレクターが新しいユーザーエージェントに一致しないことを確認する機会が AEM にはありません。そのため、Bob は誤った表現を取得することになります。

この問題を解決するために、単純な選択の UI をページにインクルードできます。このようなページでは、AEM で選択されたデバイスグループをエンドユーザーが上書きできます。上記の例では、ページ上のリンク（またはアイコン）により、エンドユーザーは `coolpage.touch.html` もし彼が自分のデバイスがそれに十分な良いと思うなら
