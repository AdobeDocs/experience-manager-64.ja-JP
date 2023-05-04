---
title: Dynamic Media Classic との統合
description: AEMとDynamic Media Classicを統合する方法について説明します。
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: integration
content-type: reference
exl-id: 0bfb05b8-7d10-4984-9e89-f1af88938c03
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '5528'
ht-degree: 66%

---

#  Dynamic Media Classic との統合 {#integrating-with-dynamic-media-classic-scene}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

Adobe Dynamic Media Classic は、リッチメディアアセットの管理や拡張のほか、web、モバイル、メールをはじめインターネットに接続されたディスプレイやプリンターにリッチメディアアセットを公開および提供したりするためのホスト型ソリューションです。

Dynamic Media Classic を使用するには、Dynamic Media Classic と Adobe Experience Manager Assets が相互にやり取りできるようにクラウド設定を指定する必要があります。このドキュメントでは、Experience Manager と Dynamic Media Classic の設定方法について説明します。

ページ上でのすべてのDynamic Media Classicコンポーネントの使用とビデオの操作について詳しくは、 [Dynamic Media Classicの使用](../assets/scene7.md).

>[!NOTE]
>
>* Dynamic Media Classic の DHTML ビューアプラットフォームは、2014年1月31日に正式にサポート終了となりました。詳しくは、[DHTML ビューアのサポート終了 FAQ](../sites-administering/dhtml-viewer-endoflifefaqs.md) を参照してください。
>* Experience Manager と連携するよう Dynamic Media Classic を設定する前に、Dynamic Media Classic と Experience Manager を統合するための[ベストプラクティス](#best-practices-for-integrating-scene-with-aem)を参照してください。
>* Dynamic Media Classicをカスタムプロキシ設定で使用している場合は、Experience Managerの一部の機能で 3.x API を使用し、他の機能で 4.x API を使用するので、両方の HTTP クライアントプロキシ設定を設定します。 3.x は [http://localhost:4502/system/console/configMgr/com.day.commons.httpclient](http://localhost:4502/system/console/configMgr/com.day.commons.httpclient) のように設定し、4.x は [http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator](http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator) のように設定します。
>


## Experience Manager と Dynamic Media Classic との統合または Dynamic Media との統合 {#aem-scene-integration-versus-dynamic-media}

Experience Managerユーザーは、Dynamic Mediaで使用する次の 2 つのソリューションの中から選択できます。

* との統合されたExperience Managerインスタンスの使用 *Dynamic Media Classic*.
* 使用 *Dynamic Media* Experience Manager

次の条件に従って、最適なソリューションを決定します。

* 次の場合、 **既存** Dynamic Media Classicのお客様で、リッチメディアアセットが公開および配信用にDynamic Media Classicに存在し、これらのアセットを Sites(WCM) オーサリングまたはExperience Manager Assets（管理用）と統合する場合は、 [Experience Manager/Dynamic Media Classicのポイントツーポイント統合](#aem-scene-point-to-point-integration) このドキュメントで説明しています。

* リッチメディアを配信する必要がある Experience Manager の&#x200B;**新規の**&#x200B;お客様の場合は、[Dynamic Media オプション](#aem-dynamic-media)を選択します。このオプションは、既存の S7 アカウントを持たず、システムに多くのアセットを保存している場合に最も有用です。

* 場合によっては、両方のソリューションを使用します。そのようなシナリオについては、[両方を利用するシナリオ](/help/sites-administering/scene7.md#dual-use-scenario)で説明しています。

### Experience Manager と Dynamic Media Classic とのポイントツーポイント統合 {#aem-scene-point-to-point-integration}

このソリューションのアセットを使用して作業する場合、次のいずれかの操作をおこないます。

* アセットを Dynamic Media Classic に直接アップロードし、**Dynamic Media Classic** コンテンツブラウザーを利用してアクセスしページオーサリングを行います
* Experience Manager Assets にアップロードしてから、Dynamic Media Classic への自動公開を有効にして、**アセット**&#x200B;コンテンツブラウザーでアクセスしてページオーサリングを行います

この統合に使用するコンポーネントは、 **Dynamic Media Classic** コンポーネント領域 [デザインモード。](/help/sites-authoring/author-environment-tools.md#page-modes)

### Experience Manager Dynamic Media {#aem-dynamic-media}

Experience ManagerDynamic Mediaは、Experience Managerプラットフォーム内で直接Dynamic Media Classic機能を統合する機能です。

このソリューションのアセットを使用して作業する場合、次のワークフローに従います。

1. 1 つの画像とビデオのアセットを直接 Experience Manager にアップロードします。
1. ビデオを Experience Manager 内で直接エンコードします。
1. 画像ベースのセットを Experience Manager 内で直接作成します。
1. 該当する場合は、画像またはビデオにインタラクティビティを追加します。

Dynamic Mediaに使用するコンポーネントは、 **[!UICONTROL Dynamic Media]** コンポーネント領域 [デザインモード](/help/sites-authoring/author-environment-tools.md#page-modes). 次のようなものがあります。

* **[!UICONTROL Dynamic Media]** - **[!UICONTROL Dynamic Media]** コンポーネントはスマートです。追加している画像が画像かビデオかに応じて、様々なオプションを使用できます。 このコンポーネントは画像プリセット、画像ベースのビューア（画像セット、スピンセット、混在メディアセットなど）およびビデオをサポートします。さらに、ビューアはレスポンシブなので、ビューアのサイズは画面サイズに合わせて自動的に変化します。すべてのビューアは HTML5 ビューアです。

* **[!UICONTROL インタラクティブメディア]** - **[!UICONTROL インタラクティブメディア]** コンポーネントは、カルーセルバナー、インタラクティブ画像およびインタラクティブビデオ用で、その中にホットスポットや画像マップなどのインタラクティブ機能が含まれています。 このコンポーネントはスマートです。追加する画像とビデオのどちらに応じて、様々なオプションがあります。 また、ビューアはレスポンシブです。つまり、画面の大きさは、スクリーン上のサイズに応じて自動的に変化します。すべてのビューアは HTML5 ビューアです。

### 二重使用シナリオ {#dual-use-scenario}

標準で、Dynamic Media と Dynamic Media Classic の両方を同時に Experience Manager と統合して、それらの機能を使用することができます。次の使用例の表で、特定の領域をオンまたはオフにするタイミングについて説明します。

Dynamic Media と Dynamic Media Classic を同時に使用するには：

1. Cloud Services で [Dynamic Media Classic](#creating-a-cloud-configuration-for-scene) を設定します。
1. 次の中からお使いのユースケースに合致する手順を実行します。

   <table> 
    <tbody> 
    <tr> 
    <td> </td> 
    <td> </td> 
    <td><strong>Dynamic Media</strong></td> 
    <td> </td> 
    <td><strong>Dynamic Media Classic 統合</strong></td> 
    <td> </td> 
    </tr> 
    <tr> 
    <td><strong>実行する操作...</strong></td> 
    <td><strong>ユースケースのワークフロー</strong></td> 
    <td><strong>画像／ビデオ</strong></td> 
    <td><strong>ダイナミックメディアコンポーネント</strong></td> 
    <td><strong>S7 コンテンツブラウザーとコンポーネント</strong></td> 
    <td><strong>Assets から S7 への自動アップロード</strong></td> 
    </tr> 
    <tr> 
    <td>Sites とダイナミックメディアを初めて使用する</td> 
    <td>アセットを Experience Manager にアップロードし、Experience Manager Dynamic Media コンポーネントを使用して Sites ページにアセットを作成する</td> 
    <td><p>オン</p> <p>（手順 3 を参照）</p> </td> 
    <td><a href="/help/assets/adding-dynamic-media-assets-to-pages.md">オン</a></td> 
    <td>オフ</td> 
    <td>オフ</td> 
    </tr> 
    <tr> 
    <td>小売業界で Sites と Dynamic Media を初めて使用する</td> 
    <td>商品以外のアセットは Experience Manager にアップロードして管理および配信する。商品のアセットは Dynamic Media Classic にアップロードし、Experience Manager の Dynamic Media Classic コンテンツブラウザーとコンポーネントを使用して、Sites に製品詳細ページを作成する。</td> 
    <td><p>オン</p> <p>（手順 3 を参照）</p> </td> 
    <td><a href="/help/assets/adding-dynamic-media-assets-to-pages.md">オン</a></td> 
    <td><a href="/help/assets/scene7.md#scene-content-browser">オン</a></td> 
    <td>オフ</td> 
    </tr> 
    <tr> 
    <td>Assets とDynamic Mediaを使い始める</td> 
    <td>アセットを Experience Manager Assets にアップロードし、公開済み URL または埋め込みコードを Dynamic Media から使用する</td> 
    <td><p>オン</p> <p>（手順 3 を参照）</p> </td> 
    <td>オフ</td> 
    <td>オフ</td> 
    <td>オフ</td> 
    </tr> 
    <tr> 
    <td>Dynamic Mediaとテンプレートを使い始める</td> 
    <td>Dyamic Media を使用して画像とビデオを作成する。Dynamic Media Classic で画像テンプレートを作成し、Dynamic Media Classic コンテンツファインダーを使用して Sites ページにテンプレートを含めます。</td> 
    <td><p>オン</p> <p>（手順 3 を参照）</p> </td> 
    <td><a href="/help/assets/adding-dynamic-media-assets-to-pages.md">オン</a></td> 
    <td><a href="/help/assets/scene7.md#scene-content-browser">オン</a></td> 
    <td>オフ</td> 
    </tr> 
    <tr> 
    <td>Sites を初めて使用する既存の Dynamic Media Classic の顧客</td> 
    <td>Dynamic Media Classic にアセットをアップロードし、Experience Manager Dynamic Media Classic コンテンツブラウザーを使用してアセットを検索し Sites ページでアセットを作成する</td> 
    <td>オフ</td> 
    <td>オフ</td> 
    <td><a href="/help/assets/scene7.md#scene-content-browser">オン</a></td> 
    <td>オフ</td> 
    </tr> 
    <tr> 
    <td>Sites と Assets を初めて使用する既存の Dynamic Media Classic の顧客</td> 
    <td>アセットを DAM にアップロードし、配信のために自動的に Dynamic Media Classic に公開します。Experience Manager Dynamic Media Classic コンテンツブラウザーを使用して、Sites ページ上のアセットを検索およびオーサリングします。</td> 
    <td>オフ</td> 
    <td>オフ</td> 
    <td><a href="/help/assets/scene7.md#scene-content-browser">オン</a></td> 
    <td><p><a href="#configuringautouploadingfromaemassets">オン</a></p> <p>（手順 4 を参照）</p> </td> 
    </tr> 
    <tr> 
    <td>Assets を初めて使用する既存の Dynamic Media Classic の顧客</td> 
    <td><p>アセットを Experience Manager にアップロードし、Dynamic Media を使用してダウンロードや共有のレンディションを生成します。配信用にExperience Manager AssetsをDynamic Media Classicに自動的に公開します。</p> <p><strong>重要：</strong> 重複処理が発生し、Experience Managerで生成されたレンディションがDynamic Media Classicに同期されない</p> </td> 
    <td><p>オン</p> <p>（手順 3 を参照）</p> </td> 
    <td>オフ</td> 
    <td>オフ</td> 
    <td><p><a href="#configuringautouploadingfromaemassets">オン</a></p> <p>（手順 4 を参照）</p> </td> 
    </tr> 
    </tbody> 
    </table>

1. オプション（ユースケーステーブルを参照）- [Dynamic Media のクラウド設定](/help/assets/config-dynamic.md)を設定し、[Dynamic Media サーバーを有効にします](/help/assets/config-dynamic.md)。
1. ( オプション、（使用例の表を参照） — 「 Assets からDynamic Media Classicへの自動アップロード」を有効にする場合は、次の項目を追加する必要があります。

   1. Dynamic Media Classic への自動アップロードを設定します。
   1. すべての Dynamic Media ワークフロー手順の後、**Dam Update Asset**&#x200B;ワークフローの&#x200B;*最後に*、**Dynamic Media Classic のアップロード**&#x200B;手順を追加します（`https://<server>:<host>/cf#/etc/workflow/models/dam/update_asset.html)`）。
   1. （オプション）[https://&lt;server>:&lt;port>/system/console/configMgr/com.day.cq.dam.scene7.impl.Scene7AssetMimeTypeServiceImpl](http://localhost:4502/system/console/configMgr/com.day.cq.dam.scene7.impl.Scene7AssetMimeTypeServiceImpl) で Dynamic Media Classic アセットのアップロードを MIME タイプで制限します。このリストにないアセットの MIME タイプは、Dynamic Media Classic サーバーにアップロードされません。
   1. （オプション） Dynamic Media Classic 設定でビデオを設定します。Dynamic Media または Dynamic Media Classic またはその両方のビデオエンコーディングを同時に有効にできます。動的レンディションは、Experience Manager インスタンスでローカルにプレビューおよび再生するために使用されますが、Dynamic Media Classic ビデオレンディションは、Dynamic Media Classic サーバーで生成および保存されます。Dynamic Media と Dynamic Media Classic の両方にビデオエンコーディングサービスを設定する場合は、[ビデオ処理プロファイル](/help/assets/video-profiles.md)を Dynamic Media Classic アセットフォルダーに適用します。
   1. （オプション）[Dynamic Media Classic でのセキュアプレビューを設定します](/help/sites-administering/scene7.md#configuring-the-state-published-unpublished-of-assets-pushed-to-scene)。

#### 制限事項 {#limitations}

Dynamic Media Classic と Dynamic Media の両方を有効にする際には、次の制限事項があります。

* アセットを選択して Experience Manager ページの Dynamic Media Classic コンポーネントにドラッグして Dynamic Media Classic に手動でアップロードすることはできません。
* Assets でアセットを編集すると、Experience Manager-Dynamic Media Classic 同期アセットが Dynamic Media Classic に自動的に更新されますが、ロールバックアクションによって新しいアップロードがトリガーされることはありません。したがって、Dynamic Media Classic では、ロールバック後すぐに最新バージョンは取得されません。ロールバック完了後に再度編集する必要があります。
* 1 つの使用例でDynamic Mediaを使用し、別の使用例でDynamic Media Classic Assets とDynamic Media Classicシステムとのやり取りをしないようにDynamic Media統合を使用する必要がある場合は、Dynamic Media Classic設定をDynamic Mediaフォルダーに適用しないでください。 また、Dynamic Media 設定（処理プロファイル）を Dynamic Media Classic フォルダーに適用しないでください。

## Dynamic Media Classic と Experience Manager の統合のベストプラクティス {#best-practices-for-integrating-scene-with-aem}

Dynamic Media ClassicをExperience Managerと統合する場合、次の点を考慮すべき重要なベストプラクティスがあります。

* 統合のテストドライブ
* 特定のシナリオで推奨される Dynamic Media Classic からのアセットの直接アップロード

[既知の制限事項](#known-limitations-and-design-implications)を参照してください。

### 統合のテストドライブ {#test-driving-your-integration}

ルートフォルダーが企業全体ではなく、サブフォルダーのみを指すようにすることで、統合をテストドライブすることをお勧めします。

>[!CAUTION]
>
>既存の Dynamic Media Classic 会社アカウントからアセットをインポートすると、Experience Manager に表示されるまでに長い時間がかかる場合があります。アセットが多すぎない Dynamic Media Classic のフォルダーを指定していることを確認してください（例えば、ルートフォルダーではアセットが多すぎて、システムがクラッシュする可能性があります）。

### Experience Manager AssetsからのアセットのアップロードとDynamic Media Classicからのアセットのアップロード {#uploading-assets-from-aem-assets-versus-from-scene}

Assets （デジタルアセット管理）機能を使用するか、Dynamic Media Classic コンテンツブラウザーを介して Experience Manager で Dynamic Media Classic に直接アクセスすることにより、アセットをアップロードできます。どちらを選択するかは、次の要素によって異なります。

* Experience Manager Assets がまだサポートしていない Dynamic Media Classic アセットタイプは、Dynamic Media Classic コンテンツブラウザーを使用して、Dynamic Media Classic から直接 Experience Manager Web サイトに追加する必要があります。例えば、画像テンプレートなどです。
* Experience Manager Assets および Dynamic Media Classic の両方でサポートされているアセットタイプの場合、アップロード方法は次の条件によって決まります。

   * アセットが現在ある場所、および
   * 共有リポジトリでのそれらの管理の重要度

アセットが既にDynamic Media Classicに存在し、共通のリポジトリでそれらを管理することが重要でない場合、アセットをExperience Manager Assetsに書き出して配信用にDynamic Media Classicに同期するだけでは、不要なラウンドトリップになります。 アセットを単一のリポジトリに保持し、配信のためにDynamic Media Classicと同期することをお勧めします。

## Dynamic Media Classic統合の設定 {#configuring-scene-integration}

Dynamic Media Classic にアセットをアップロードするように Experience Manager を設定できます。CQ ターゲットフォルダーからのアセットは、Experience Manager から Dynamic Media Classic 会社アカウントに（自動または手動で）アップロードできます。

>[!NOTE]
>
>Dynamic Media Classic アセットのインポート専用のターゲットフォルダーのみを使用することをお勧めします。ターゲットフォルダーの外部にあるデジタルアセットは、Dynamic Media Classic の設定が有効になっているページの Dynamic Media Classic コンポーネントでのみ使用できます。また、これらは Dynamic Media Classic のオンデマンドフォルダーに配置されます。オンデマンドフォルダーは Experience Manager と同期されません（ただし、Dynamic Media Classic コンテンツブラウザーでアセットは検出可能です）。

Dynamic Media ClassicをExperience Managerと統合するように設定するには、次の手順を実行する必要があります。

1. [クラウド設定を定義](#creating-a-cloud-configuration-for-scene) - Dynamic Media Classic フォルダーと Assets フォルダー間のマッピングを定義します。一方向（Experience Manager Assets から Dynamic Media Classic）の同期のみが必要な場合でも、この手順を完了してください。
1. [**Adobe CQ s7dam Dam Listener**](#enabling-the-adobe-cq-scene-dam-listener) を有効にする - [!UICONTROL OSGi] コンソールで実行します。
1. Experience ManagerアセットをDynamic Media Classicに自動的にアップロードする場合は、「 」オプションをオンにし、DAM アセットの更新ワークフローにDynamic Media Classicを追加します。 また、手動でアセットをアップロードできます。
1. サイドキックに Dynamic Media Classic コンポーネントを追加します。これにより、ユーザーは、Experience ManagerページでDynamic Media Classicコンポーネントを使用できます。
1. [設定を Experience Manager 内のページにマッピングする](#enabling-scene-for-wcm) - この手順は、Dynamic Media Classic で作成したビデオプリセットを表示する場合に必要です。また、CQ ターゲットフォルダーの外部から Dynamic Media Classic にアセットを公開する必要がある場合にも必須です。

ここでは、これらのすべての手順の実行方法を説明し、重要な制限を示します。

### Dynamic Media Classic と Experience Manager Assets 間の同期の仕組み {#how-synchronization-between-scene-and-aem-assets-works}

Experience Manager Assets と Dynamic Media Classic の同期を設定する場合は、次の点を理解することが重要です。

#### Experience Manager AssetsからDynamic Media Classicにアップロード中 {#uploading-to-scene-from-aem-assets}

* Dynamic Media Classic には Dynamic Media Classic のアップロード用に指定された同期フォルダーがあります。
* Dynamic Media Classic へのアップロードは、デジタルアセットが専用同期フォルダーに配置されている場合に自動化できます。
* Experience Manager のフォルダーとサブフォルダーの構造は、Dynamic Media Classic で複製されます。

>[!NOTE]
>
>Experience Manager は、Dynamic Media Classic にアップロードする前にすべてのメタデータを XMP として埋め込むため、メタデータノードのすべてのプロパティを Dynamic Media Classic で XMP として使用できます。

#### 既知の制限および設計の意味 {#known-limitations-and-design-implications}

Experience Manager Assets と Dynamic Media Classic 間の同期により、現在、次の制限／デザイン上の影響があります。

<table> 
 <tbody> 
  <tr> 
   <td><strong>制限／設計の意味</strong></td> 
   <td><strong>説明</strong></td> 
  </tr> 
  <tr> 
   <td>１つの専用同期（ターゲット）フォルダー</td> 
   <td>Dynamic Media Classic のアップロードでは、Experience Manager で会社ごとに指定されたフォルダーを 1 つだけ持つことができます。Dynamic Media Classic で複数の会社アカウントにアクセスする必要がある場合は、複数の設定を作成できます。</td> 
  </tr> 
  <tr> 
   <td>フォルダー構造</td> 
   <td>アセットと共に同期されたフォルダーを削除すると、Dynamic Media Classic のすべてのリモートアセットは削除されますが、フォルダーは残ります。</td> 
  </tr> 
  <tr> 
   <td>アドホックフォルダー</td> 
   <td>WCM でDynamic Media Classicに手動でアップロードしたターゲットフォルダーの外部にあるアセットは、Dynamic Media Classic上の別のアドホックフォルダーに自動的に配置されます。 この機能は、Experience Managerのクラウド設定で設定します。</td> 
  </tr> 
  <tr> 
   <td>混在メディア</td> 
   <td>混在メディアセットは、Experience Manager ではサポートされていませんが、Experience Manager で表示されます。</td> 
  </tr> 
  <tr> 
   <td>PDF</td> 
   <td>Dynamic Media Classic の eCatalog から生成された PDF は、CQ ターゲットフォルダーに読み込まれます。</td> 
  </tr> 
  <tr> 
   <td>UI 更新</td> 
   <td>Experience Manager と Dynamic Media Classic 間で同期を行う場合は、必ずユーザーインターフェイスを更新して変更を表示してください。 </td> 
  </tr> 
  <tr> 
   <td>ビデオサムネール</td> 
   <td>Dynamic Media Classic を使用してエンコードするためにビデオを Experience Manager Assets にアップロードする場合、ビデオサムネールおよびエンコードされたビデオが Experience Manager Assets で使用できるようになるまで、ビデオ処理時間に応じて、ある程度時間がかかることがあります。</td> 
  </tr> 
  <tr> 
   <td>ターゲットサブフォルダー</td> 
   <td><p>ターゲットフォルダー内でサブフォルダーを使用する場合は、場所に関係なく、各アセットに一意の名前を付けるか、（設定領域で）Dynamic Media Classicを設定して、場所に関係なくアセットが上書きされないようにします。</p> <p>そうしないと、Dynamic Media Classic ターゲットサブフォルダーにアップロードされたものと同じ名前を持つアセットはアップロードされますが、ターゲットフォルダー内にある同じ名前のアセットは削除されます。 </p> </td> 
  </tr> 
 </tbody> 
</table>

### Dynamic Media Classicサーバーの設定 {#configuring-scene-servers}

プロキシの背後で Experience Manager を実行するか、特別なファイアウォール設定がある場合、異なる地域のホストを明示的に有効にする必要があります。サーバーは、`/etc/cloudservices/scene7/endpoints`にあるコンテンツで管理され、必要に応じてカスタマイズできます。必要に応じて、URL をタップし、編集して URL を変更します。 Experience Manager の以前のバージョンでは、これらの値はハードコードされていました。

次に移動した場合： `/etc/cloudservices/scene7/endpoints.html`に設定すると、次のサーバーが表示されます（URL をクリックして編集できます）。

![chlimage_1-296](assets/chlimage_1-296.png)

### Dynamic Media Classicのクラウド設定の作成 {#creating-a-cloud-configuration-for-scene}

クラウド設定は、Dynamic Media Classic フォルダーと Experience Manager Assets フォルダー間のマッピングを定義します。Experience Manager Assets と Dynamic Media Classic を同期するように設定する必要があります。詳しくは、同期の仕組みを参照してください。

>[!CAUTION]
>
>既存の Dynamic Media Classic 会社アカウントからアセットをインポートすると、Experience Manager に表示されるまでに長い時間がかかる場合があります。Dynamic Media Classic で指定するフォルダーに、多くのアセットを含まないフォルダーを指定していることを確認してください。例えば、ルートフォルダーのアセットが多すぎる場合があります。
>
>統合をテストする場合は、ルートフォルダーが会社全体ではなく、サブフォルダーのみを指すようにしてください。

>[!NOTE]
>
>複数の設定を持つことができます。1 つのクラウド設定は、 Dynamic Media Classic 会社の 1 名のユーザーを表します。他のDynamic Media Classicの会社またはユーザーにアクセスする場合は、複数の設定を作成します。

Experience ManagerがDynamic Media Classicにアセットを公開できるように設定するには：

1. Experience Managerアイコンをタップし、に移動します。 **[!UICONTROL 導入/Cloud Services]** Adobe Dynamic Media Classicにアクセスするには

1. タップ **[!UICONTROL 今すぐ設定]**.

   ![chlimage_1-297](assets/chlimage_1-297.png)

1. 「**[!UICONTROL タイトル]**」フィールド、およびオプションで「**[!UICONTROL 名前]**」フィールドで、適切な情報を入力します。「**[!UICONTROL 作成]**」をタップします。

   >[!NOTE]
   >
   >追加の設定を作成する場合は、**[!UICONTROL 親設定]**&#x200B;フィールドが表示されます。
   >
   >実行 **not** 親設定を変更します。 親設定を変更すると、統合が解除される場合があります。

1. Dynamic Media Classicアカウントの電子メールアドレス、パスワード、地域を入力して、をタップします。 **[!UICONTROL Dynamic Media Classicに接続]**. Dynamic Media Classic サーバーに接続され、ダイアログにはより多くのオプションが表示され、拡大します。

1. **[!UICONTROL 会社]** 名と&#x200B;**[!UICONTROL ルートパス]**&#x200B;を入力します。この情報は、公開されたサーバ名と指定するパスです。公開先のサーバー名がわからない場合は、Dynamic Media Classicで、に移動します。 **[!UICONTROL 設定/アプリケーション設定]**.

   >[!NOTE]
   >
   >Dynamic Media Classic のルートパスは、Dynamic Media Classic フォルダー Experience Manager が接続する場所です。特定のフォルダーに絞り込むことができます。

   >[!CAUTION]
   >
   >Dynamic Media Classic フォルダーのサイズによっては、ルートフォルダーの読み込みに時間がかかる可能性があります。また、Dynamic Media Classic のデータが Experience Manager のストレージを超える可能性があります。正しいフォルダーをインポートしていることを確認してください。 読み込むデータが多すぎると、システムが停止する場合があります。

   ![chlimage_1-298](assets/chlimage_1-298.png)

1. 「**[!UICONTROL OK]**」をクリックします。Experience Manager で設定が保存されます。

>[!NOTE]
>
>再接続する場合：
>
>* パブリッシュ環境で Dynamic Media Classic に再接続する場合、パブリッシュ環境でパスワードをリセットしないと再接続が正常にできません（オーサーインスタンスの問題ではありません）。
>* 地域、会社名などの値を変更する場合は、 Dynamic Media Classic に再接続する必要があります。設定オプションを変更後、保存していない場合、Experience Manager では引き続き、設定が有効であると誤って表示されます。必ず再接続するようにします。
>


### Adobe CQ Dynamic Media Classic Dam Listener の有効化 {#enabling-the-adobe-cq-scene-dam-listener}

Adobe CQ Dynamic Media Classic Dam Listener を有効にします。このリスナーはデフォルトでは無効になっています。

Adobe CQ Dynamic Media Classic Dam Listener を有効にするには、次の手順に従います。

1. 次をタップします。 [!UICONTROL ツール] アイコンをクリックし、 **[!UICONTROL 操作/Web コンソール]**. Web コンソールが開きます。
1. に移動します。 **[!UICONTROL Adobe CQ Dynamic Media Classic Dam Listener]** をクリックし、 **[!UICONTROL 有効]** チェックボックスをオンにします。

   ![chlimage_1-299](assets/chlimage_1-299.png)

1. 「**[!UICONTROL 保存]**」をタップします。

### Dynamic Media Classic Upload ワークフローへの設定可能なタイムアウトの追加 {#adding-configurable-timeout-to-scene-upload-workflow}

Dynamic Media Classic を使用してビデオエンコーディングを処理するように Experience Manager インスタンスが設定されている場合、アップロードジョブのタイムアウトはデフォルトでは 35 分です。長時間実行される可能性があるビデオエンコーディングジョブに対応するために、次の設定を行います。

1. **http://localhost:4502/system/console/configMgr/com.day.cq.dam.scene7.impl.Scene7UploadServiceImpl** に移動します。

   ![chlimage_1-300](assets/chlimage_1-300.png)

1. 必要に応じて、 **[!UICONTROL アクティブジョブタイムアウト]** フィールドに入力します。 負以外の数は、測定単位（秒）で受け入れられます。 この値は、デフォルトでは 2100 に設定されています。

   >[!NOTE]
   >
   >ベストプラクティス：ほとんどのアセットが長くても数分以内に収集されます（画像など）。ただし、大きなビデオなどの場合は、長い処理時間に対応するために、タイムアウト値を 7200 秒（2 時間）に増やします。 それ以外の場合、このDynamic Media Classicアップロードジョブは **[!UICONTROL UploadFailed]** JCR メタデータ内で使用します。

1. 「**[!UICONTROL 保存]**」をタップします。

### Experience Manager Assetsからの自動アップロード {#autouploading-from-aem-assets}

Experience Manager6.3.2 以降では、Experience Manager Assetsが設定され、Digital Asset Manager にアップロードするデジタルアセットが CQ のターゲットフォルダーにある場合、Dynamic Media Classicに自動的に更新されるようになりました。

アセットを Experience Manager Assets に追加すると、このアセットは Dynamic Media Classic に自動的にアップロードされて公開されます。

>[!NOTE]
>
>Experience Manager Assets から Dynamic Media Classic に自動アップロードできるファイルの最大サイズは 500 MB です。

Experience Manager Assetsからの自動アップロードを設定するには：

1. Experience Managerアイコンをタップし、に移動します。 **[!UICONTROL 導入/Cloud Services]** 次に、「Dynamic Media」見出しの下にある「利用可能な設定」で、をタップします。 **[!UICONTROL dms7 (Dynamic Media)]**)
1. 次をタップします。 **[!UICONTROL 詳細]** タブで、 **[!UICONTROL 自動アップロードを有効にする]** チェックボックスをオンにして、 **[!UICONTROL OK]**. 次に、DAM Asset ワークフローに Dynamic Media Classic へのアップロードが含まれるよう設定する必要があります。

   >[!NOTE]
   >
   >非公開状態での Dynamic Media Classic へのアセットのプッシュについて詳しくは、[Dynamic Media Classic にプッシュしたアセットの状態（公開または非公開）の設定](#configuring-the-state-published-unpublished-of-assets-pushed-to-scene)を参照してください。

   ![screen_shot_2018-03-15at52501pm](assets/screen_shot_2018-03-15at52501pm.jpg)

1. Experience Managerのようこそページに戻り、をタップします。 **[!UICONTROL ワークフロー]**. 次をダブルクリックします。 **DAM アセットの更新** ワークフローを使用して開きます。
1. サイドキックの&#x200B;**[!UICONTROL ワークフロー]**&#x200B;コンポーネントに移動し、「**[!UICONTROL Dynamic Media Classic]**」を選択します。ドラッグ **[!UICONTROL Dynamic Media Classic]** ワークフローに移動して、 **[!UICONTROL 保存]**. ターゲットフォルダーで Experience Manager Assets に追加されたアセットは、自動的に Dynamic Media Classic にアップロードされます。

   ![chlimage_1-301](assets/chlimage_1-301.png)

   >[!NOTE]
   >
   >* 自動化後にアセットを追加する場合、CQ ターゲットフォルダーに配置されていないアセットは、Dynamic Media Classic にアップロードされません。
   >* Experience Manager は、Dynamic Media Classic にアップロードする前にすべてのメタデータを XMP として埋め込むため、メタデータノードのすべてのプロパティを Dynamic Media Classic で XMP として使用できます。


### Dynamic Media Classicにプッシュされたアセットの状態（公開/非公開）の設定 {#configuring-the-state-published-unpublished-of-assets-pushed-to-scene}

Experience Manager Assets から Dynamic Media Classic にアセットをプッシュしている場合、自動的にプッシュするか（デフォルトの動作）、非公開状態で Dynamic Media Classic にプッシュすることができます。

運用開始前にステージング環境でテストするために、Dynamic Media Classic でアセットをただちに公開しないようにすることが必要となる場合があります。Dynamic Media Classic のセキュアテスト環境で Experience Manager を使用すると、Assets から Dynamic Media Classic に非公開状態で直接アセットをプッシュできます。

Dynamic Media Classic のアセットは、セキュアプレビューで引き続き使用できます。Experience Manager 内でアセットが公開された場合にのみ、Dynamic Media Classic アセットも実稼動環境で公開されます。

アセットを Dynamic Media Classic へのプッシュと同時に公開したい場合は、オプションを設定する必要はありません。この動作がデフォルトです。

ただし、Dynamic Media Classic にプッシュしたアセットを自動的に公開しないようにする場合は、Experience Manager と Dynamic Media Classic でこの機能を実行します。このセクションではその設定方法を説明します。

#### Dynamic Media Classic にアセットを未公開でプッシュするための前提条件 {#prerequisites-to-push-assets-to-scene-unpublished}

Dynamic Media Classic にアセットを公開せずにプッシュするには、次のように設定する必要があります。

1. [Admin Console を使用して、サポートケースを作成します。](https://helpx.adobe.com/jp/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html) サポートケースで、Dynamic Media Classicアカウントのセキュアプレビューが有効になっていることをリクエストします。
1. 指示に従う： [Dynamic Media Classicアカウントのセキュアプレビューを設定します。](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/upload-publish/testing-assets-making-them-public.html#upload-publish)

これらの手順は、Dynamic Media Classic で安全なテスト設定を作成する場合と同じです。

>[!NOTE]
>
>インストール環境が UNIX® 64 ビットオペレーティングシステムの場合、追加して指定する必要がある設定オプションについては、[https://helpx.adobe.com/jp/experience-manager/kb/enable-xmp-write-back-64-bit-redhat.html](https://helpx.adobe.com/jp/experience-manager/kb/enable-xmp-write-back-64-bit-redhat.html) を参照してください。

#### 非公開状態のアセットをプッシュする際の既知の制限事項  {#known-limitations-for-pushing-assets-in-unpublished-state}

この機能を使用する場合、次の制限に注意が必要です。

* バージョン管理のサポートはありません。
* アセットが既に Experience Manager で公開されていて、後続バージョンも作成されている場合、その新しいバージョンは、即座に実稼動環境に公開されます。アクティベーションに対する公開は、アセットの最初の公開でのみ動作します。

>[!NOTE]
>
>すぐにアセットを公開するには、「**[!UICONTROL セキュアプレビューを有効にする]**」設定を引き続き「**[!UICONTROL 即時]**」にし、「**[!UICONTROL 自動アップロードを有効にする]**」を使用することをお勧めします。

### Dynamic Media Classicに非公開としてプッシュされたアセットの状態を設定しています {#setting-the-state-of-assets-pushed-to-scene-as-unpublished}

>[!NOTE]
>
>ユーザーが Experience Manager でアセットを公開すると、S7 アセットが実稼働／ライブアセットに自動的にトリガーされます（そのアセットは、セキュアプレビュー／非公開ではなくなります）。

Dynamic Media Classic にプッシュしたアセットの状態を非公開として設定するには：

1. Experience Managerアイコンをタップし、に移動します。 **[!UICONTROL 導入/Cloud Services]**&#x200B;をタップします。 **[!UICONTROL Dynamic Media Classic]**&#x200B;をクリックし、Dynamic Media Classicで設定を選択します。
1. 次をタップします。 **[!UICONTROL 詳細]** タブをクリックします。 アセットを公開せずに Dynamic Media Classic にプッシュするには、「**[!UICONTROL セキュアビューを有効にする]**」ドロップダウンメニューで「**[!UICONTROL AEM 公開アクティベート時]**」を選択します。（デフォルトでは、この値は「**[!UICONTROL 即時]**」に設定されており、Dynamic Media Classic のアセットは即座に公開されます。）

   アセットを公開する前のテストについて詳しくは、[Dynamic Media Classic のドキュメント](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/upload-publish/testing-assets-making-them-public.html?lang=ja#upload-publish)を参照してください。

   ![chlimage_1-302](assets/chlimage_1-302.png)

1. 「**[!UICONTROL OK]**」をタップします。

セキュアビューを有効にすると、アセットがセキュリティで保護されたプレビューサーバーに非公開にプッシュされます。

セキュアプレビューが有効であるかどうかを確認するには、Experience Manager のページで Dynamic Media Classic コンポーネントに移動します。「**[!UICONTROL 編集]**」をタップします。アセットには、URL にリストされたセキュアプレビューサーバーがあります。Experience Manager に公開すると、ファイル参照のサーバードメインがプレビュー URL から実稼働 URL に更新されます。

### WCM でのDynamic Media Classicの有効化 {#enabling-scene-for-wcm}

次の 2 つの理由から、WCM用 Dynamic Media Classic を有効にする必要があります。

* ページオーサリング用のユニバーサルビデオプロファイルのドロップダウンリストを有効にします。このリストがないと、**[!UICONTROL ユニバーサルビデオプリセット]**&#x200B;のドロップダウンが空になって、設定できません。
* デジタルアセットがターゲットフォルダーにない場合、ページプロパティでそのページの Dynamic Media Classic を有効にすると、Dynamic Media Classic にアセットをアップロードできます。次に、アセットを Dynamic Media Classic コンポーネントにドラッグ＆ドロップします。通常の継承ルールが適用されます（子ページが親ページの設定を継承することを意味します）。

WCM の Dynamic Media Classic を有効にすると、他の設定と同様に、継承ルールが適用されます。WCM 用の Dynamic Media Classic は、タッチ操作向け UI とクラシック UI のどちらでも有効にできます。

#### タッチ操作向け UI での WCM 用Dynamic Media Classicの有効化 {#enabling-scene-for-wcm-in-the-touch-optimized-user-interface}

タッチ操作向け UI でDynamic Media Classic for WCM を有効にするには：

1. Experience Managerアイコンをタップし、に移動します。 **[!UICONTROL サイト]** 次に、Web サイトのルートページ（特定言語向けではない）を表示します。

1. ツールバーで、 [!UICONTROL 設定] アイコンとタップ **[!UICONTROL プロパティを開く]**.

1. タップ **[!UICONTROL Cloud Services]** とタップします。 **[!UICONTROL 設定を追加]** を選択し、 **[!UICONTROL Dynamic Media Classic]**.
1. 内 **[!UICONTROL Adobe Dynamic Media Classic]** ドロップダウンリストから目的の設定を選択し、 **[!UICONTROL OK]**.

   ![chlimage_1-303](assets/chlimage_1-303.png)

   Dynamic Media Classic のその設定のビデオプリセットは、そのページと子ページの Dynamic Media Classic ビデオコンポーネントとともに Experience Manager で使用できます。

#### クラシックユーザーインターフェイスでの WCM 用Dynamic Media Classicの有効化 {#enabling-scene-for-wcm-in-the-classic-user-interface}

クラシック UI でDynamic Media Classic for WCM を有効にするには：

1. Experience Managerで、 **[!UICONTROL Web サイト]** また、Web サイトのルートページ（特定言語向けではない）に移動します。

1. サイドキックで、 **[!UICONTROL ページ]** アイコンとタップ **[!UICONTROL ページプロパティ]**.

1. タップ **[!UICONTROL Cloud Services/サービスを追加/ Dynamic Media Classic]**.
1. 内 **[!UICONTROL Adobe Dynamic Media Classic]** ドロップダウンリストから目的の設定を選択し、 **[!UICONTROL OK]**.

   Dynamic Media Classic のその設定のビデオプリセットは、そのページと子ページの Dynamic Media Classic ビデオコンポーネントとともに Experience Manager で使用できます。

### デフォルト設定の指定 {#configuring-a-default-configuration}

複数の Dynamic Media Classic 設定がある場合、そのうちの 1 つを Dynamic Media Classic コンテンツブラウザーのデフォルトとして指定できます。

1 つの Dynamic Media Classic 設定のみが、所定の時点でデフォルトとしてマークできます。デフォルト設定は、Dynamic Media Classic コンテンツブラウザーにデフォルトで表示される会社アセットです。

デフォルトの設定を構成するには：

1. Experience Managerアイコンをタップし、に移動します。 **[!UICONTROL 導入/Cloud Services]**&#x200B;をタップします。 **[!UICONTROL Dynamic Media Classic]**&#x200B;をクリックし、Dynamic Media Classicで設定を選択します。
1. 設定を開くには、をタップします。 **[!UICONTROL 編集]**.

1. 「**[!UICONTROL 一般]**」タブで、「**[!UICONTROL デフォルトの設定]**」チェックボックスを選択して、これを Dynamic Media Classic コンテンツブラウザーに表示されるデフォルトの会社およびルートパスにします。

   ![chlimage_1-304](assets/chlimage_1-304.png)

   >[!NOTE]
   >
   >1 つの設定しかない場合、「**[!UICONTROL デフォルト設定]**」チェックボックスを選択しても、効果はありません。

### アドホックフォルダーの設定 {#configuring-the-ad-hoc-folder}

アセットが CQ ターゲットフォルダーにない場合に、Dynamic Media Classicでアセットのアップロード先のフォルダーを設定できます。 CQ ターゲットフォルダーの外部からのアセットの公開を参照してください。

アドホックフォルダーを設定するには：

1. Experience Managerアイコンをタップし、に移動します。 **[!UICONTROL 導入/Cloud Services]**&#x200B;をタップします。 **[!UICONTROL Dynamic Media Classic]**&#x200B;をクリックし、Dynamic Media Classicで設定を選択します。
1. 設定を開くには、をタップします。 **[!UICONTROL 編集]**.

1. 次をタップします。 **[!UICONTROL 詳細]** タブをクリックします。 「**[!UICONTROL アドホックフォルダー]**」フィールドで、**アドホック**&#x200B;フォルダーを変更できます。デフォルトでは、**name_of_the_company/CQ5_adhoc** です。

   ![chlimage_1-305](assets/chlimage_1-305.png)

### ユニバーサルプリセットの設定 {#configuring-universal-presets}

ビデオコンポーネントのユニバーサルプリセットを設定するには、 [ビデオ](/help/assets/s7-video.md).

## MIME タイプベースの Assets/Dynamic Media Classicアップロードジョブパラメーターサポートの有効化 {#enabling-mime-type-based-assets-scene-upload-job-parameter-support}

Digital Asset Manager／Dynamic Media Classic アセットの同期でトリガーされる、設定可能な Dynamic Media Classic アップロードジョブパラメーターを有効にすることができます。

特に、Experience Manager web コンソール設定パネルの OSGi（Open Service Gateway initiative）領域にある MIME タイプで、受け入れられるファイル形式を設定します。次に、JCR（Java™ コンテンツリポジトリ）の各 MIME タイプで使用される個別のアップロードジョブパラメーターをカスタマイズできます。

**MIME タイプベースのアセットを有効にするには：**

1. Experience Managerアイコンをタップし、に移動します。 **[!UICONTROL ツール/操作/ Web コンソール]**.
1. Adobe Experience Manager Web Console Configuration パネルで、 **[!UICONTROL OSGi]** メニュー、タップ **[!UICONTROL 設定]**.
1. 「名前」列で、を探してタップします。 **[!UICONTROL Adobe CQ Dynamic Media Classic Asset MIME type Service]** 設定を編集します。
1. 「MIME タイプマッピング」領域で、任意のプラス記号 (+) をタップして、MIME タイプを追加します。

   [サポートされる MIME タイプ](/help/assets/assets-formats.md#supported-mime-types)を参照してください。

1. テキストフィールドで、新しい MIME タイプ名を入力します。

   例えば、`EPS=application/postscript`または`PSD=image/vnd.adobe.photoshop`に示すように`<file_extension>=<mime_type>`と入力します。

1. 設定ウィンドウの右下隅で、をタップします。 **[!UICONTROL 保存]**.
1. 「Experience Manager」に戻り、左側のレールで「CRXDE Lite」をタップします。
1. CRXDE Lite ページの左側のレールで、`/etc/cloudservices/scene7/<environment>`（`<environment>` は実際の名前に置き換える）に移動します。
1. `<environment>`（`<environment>`は実際の名前に置き換える）を展開して、`mimeTypes`ノードを表示します。
1. 追加した mimeType をタップします。

   例えば、`mimeTypes > application_postscript` や `mimeTypes > image_vnd.adobe.photoshop` です。

1. CRXDE Liteページの右側で、 **[!UICONTROL プロパティ]** タブをクリックします。
1. **[!UICONTROL jobParam]** 値フィールドの Dynamic Media Classic アップロードジョブパラメーターを指定します。

   （例：`psprocess="rasterize"&psresolution=120`）。

   使用可能な追加のアップロードジョブパラメーターについて詳しくは、[Adobe Dynamic Media Classic 画像実稼働システム API](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/c-overview.html?lang=ja) を参照してください。

   >[!NOTE]
   >
   >PSD ファイルをアップロードしていて、レイヤー抽出のテンプレートとして処理する場合は、**[!UICONTROL jobParam]**&#x200B;値フィールドに次の値を入力します。
   >
   >`process=MaintainLayers&layerNaming=AppendName&createTemplate=true`
   >
   >PSDファイルに「レイヤー」が含まれていることを確認します。 厳密に 1 つの画像またはマスク付きの画像の場合、処理するレイヤーがないので、画像としてのみ処理されます。

1. CRXDE Liteページの左上隅にあるをタップします。 **[!UICONTROL すべて保存]**.

## Dynamic Media ClassicとExperience Managerの統合のトラブルシューティング {#troubleshooting-scene-and-aem-integration}

Dynamic Media Classic と Experience Manager の統合で問題が発生した場合は、次のシナリオを参照して解決してください。

**Dynamic Media Classic へのデジタルアセット公開に失敗した場合：**

* アップロードしようとしているアセットが **[!UICONTROL CQ ターゲット]** フォルダーに保存されます ( このフォルダーはDynamic Media Classicクラウド設定で指定します )。
* 設定されていない場合は、 **[!UICONTROL ページプロパティ]** を設定して、 **[!UICONTROL CQ アドホック]** フォルダー。

* ログで情報を確認します。

**ビデオプリセットが表示されない場合：**

* を通じて、そのページのクラウド設定が設定されていることを確認します。 **[!UICONTROL ページプロパティ]**. ビデオプリセットは、Dynamic Media Classic ビデオコンポーネントで使用できます。

**Experience Manager でビデオアセットが再生されない場合：**

* 正しいビデオコンポーネントを使用していることを確認します。Dynamic Media Classic ビデオコンポーネントは、基盤ビデオコンポーネントとは異なります。詳しくは、[基盤ビデオコンポーネントと Dynamic Media Classic ビデオコンポーネントの比較](/help/assets/s7-video.md)を参照してください。

**Experience Manager 内の新しいアセットや変更されたアセットが Dynamic Media Classic に自動的にアップロードされない場合：**

* アセットが CQ ターゲットフォルダーにあることを確認します。CQ ターゲットフォルダーにあるアセットだけが自動的に更新されます（アセットを自動的にアップロードするように Experience Manager Assets を設定した場合）。
* 自動アップロードを有効にするようにクラウドサービス設定を設定し、DAM Asset ワークフローを更新および保存して Dynamic Media Classic アップロードに含めたことを確認します。
* Dynamic Media Classic ターゲットフォルダーのサブフォルダーに画像をアップロードする場合、次のいずれかの操作を行うようにします。

   * 場所に関係なく、すべてのアセットの名前が一意であることを確認します。 そうしないと、メインターゲットフォルダー内のアセットが削除され、サブフォルダー内のアセットのみが残ります。
   * Dynamic Media Classic アカウントの設定領域で、Dynamic Media Classic によるアセットの上書き方法を変更します。同じ名前のアセットをサブフォルダーで使用する場合、場所に関係なく、アセットを上書きするように Dynamic Media Classic を設定しないでください。

**削除したアセットやフォルダーが Dynamic Media Classic と Experience Manager の間で同期されない場合：**

* Experience Manager Assets で削除されたアセットとフォルダーは、Dynamic Media Classic の同期済みフォルダーに引き続き表示されます。手動で削除します。

**ビデオのアップロードに失敗した場合**

* ビデオのアップロードに失敗し、Experience Managerを使用してDynamic Media Classic統合を通じてビデオをエンコードする場合は、 [Dynamic Media Classic Upload ワークフローへの設定可能なタイムアウトの追加](#adding-configurable-timeout-to-scene-upload-workflow).

>[!CAUTION]
>
>既存の Dynamic Media Classic 会社アカウントからアセットをインポートすると、Experience Manager に表示されるまでに長い時間がかかる場合があります。Dynamic Media Classicで指定するフォルダーに、多くのアセットを含まないようにしてください（例えば、ルートフォルダーに含まれるアセットが多すぎる場合があります）。
>
>統合をテストする場合は、ルートフォルダーが会社全体ではなく、サブフォルダーのみを指すようにしてください。
