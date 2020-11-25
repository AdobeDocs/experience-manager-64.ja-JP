---
title: AEM 6.4累積Fix Packリリースノート
description: Adobe Experience Manager6.4累積Fix Pack固有のリリースノート
contentOwner: AK
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: a969fb6ca6962766b7a69a4f35a9960269dabc86
workflow-type: tm+mt
source-wordcount: '4038'
ht-degree: 13%

---


# AEM 6.4累積Fix Packリリースノート {#aem-cumulative-fix-pack-release-notes}

## リリース情報 {#release-information}

<!-- TBD: Update the SD URL. -->

| 製品 | **Adobe Experience Manager（AEM）6.4** |
|---|---|
| バージョン | 6.4.8.3 |
| 種類 | 累積修正パック |
| 日付 | 2020年11月26日 |
| 前提条件 | [AEM 6.4 サービスパック 8（6.4.8.0）](sp-release-notes.md) |
| ダウンロード URL | AEM 6.4.8.3( [ソフトウェア配布版)](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq640/cumulativefixpack/aem-6.4.8-cfp-3.0.zip) |

## AEM 6.4.8.3 に含まれる機能 {#what-s-included-in-aem}

AEM Cumulative Fix Pack 6.4.8.3は重要なアップデートで、2020年3月のAEM 6.4 Service Pack 8(6.4.8.0)の一般リリース以降の社内およびお客様向けの修正が含まれています。

AEM 6.4.8.3は、AEM 6.4 Service Pack 8に依存するCumulative Fix Pack(CFP)です。 AEM 6.4 Service Pack 8のインストール後にCFPをインストールします。

AEM 6.4.8.3では、組み込みのリポジトリ(Apache Jackrabbit Oak)がバージョン1.8.23に更新されました。

For information on CFP and other types of releases, see [AEM Update Release Vehicle Definitions](https://docs.adobe.com/content/help/en/experience-manager-65/deploying/deploying/update-release-vehicle-definitions.html)

Adobe Experience Manager6.4.8.3には、次の問題の修正が含まれています。

### Sites {#sites-6483}

* コンテンツフラグメントのバリエーションのテキストを更新すると、そのバリエーションの代わりにマスターコンテンツフラグメントのコンテンツが更新されます(NPR-35080)。

* コンポーネントの「String type label」プロパティに数値を設定した場合は、コンポーネントを削除し、「元に戻す」オプションを使用して元に戻すと、labelプロパティのタイプが自動的に「String」から「Long」に変更されます(NPR-34738)。

* 複数フィールドにファイルアップロードコンポーネントを追加する場合、画像パスは、複数フィールドノード(NPR-34423)ではなく、コンポーネントノードに保存されます。

* ページの移動ウィザードで、移動先が選択されていない場合でも、次のボタンは有効なままです(NPR-34460)。

* 親コンポーネントにプロパティが含まれる場合、継承されたコンポーネントにはプロパティが自動的に含まれません(CQ-4308409)。 `cq:isContainer`

* 関数を使用してCSSの縮小を使用すると、 `calc()` 記号の周りの空白 `+` が削除されます(NPR-34991)。

* AEMインスタンスを開始すると、 `com.adobe.granite.maintenance.impl.MaintenanceTaskManagerImpl` および `com.adobe.granite.maintenance.impl.TaskScheduler` コンポーネントは `Active` 状態(NPR-34952)で表示されません。

### [!DNL Assets] {#assets-6483}

* 既存のアセットのバージョンを作成する場合、メタデータプロファイルがフォルダーに適用されていると、メタデータに対する更新は保持されません(NPR-34833)。
* ととを使用 [!DNL Adobe Asset Link][!DNL Adobe InDesign]する場合、検索結果にはフォルダーとコレクションは含まれず、アセットのみが含まれます(NPR-34700)。
* フォルダー上でアセットをドラッグして移動する場合、ユーザーインターフェイスには、「ライトボックスに [!UICONTROL ドロップ」および「コレクションに] ドロップ 」オプションも表示されます。 移動操作がキャンセルされた場合でも、ユーザインターフェイスは後者の2つのオプション(NPR-34525)を引き続き表示する。
* 「パブリケーションの管理」インターフェイスを開いた場合、「公開」オプションは使用できず、「非公開」オプションを選択した場合、スコープページが空白になります。(CQ-4302509)

#### [!DNL Dynamic Media] {#dynamic-media}

* 「画像プリセット」設定で、で「JPGクロミナンスダウンサンプリングを [!UICONTROL 有効にする] 」オプションの選択が解除され [!DNL Experience Manager]ている場合、変更は [!DNL Dynamic Media] (NPR-34284)と同期されません。
* ビ [!UICONTROL ューアプリセットエディタ](Viewer Presets Editor [!UICONTROL )で] PanoramicImage/PanoramicImage_VRプリセットを編集する場合、コンポーネント内の `PanoramicView``PANORAMICVIEW_AUTOROTATE` 修飾子ラベルは使用できません(CQ-4302043)。
* からビデオを非公開にしても、設定され [!DNL Experience Manager] たScene7でアダプティブビデオセットの公開は取り消されません。 (CQ-4304405).

### プラットフォーム {#platform-6483}

* この `emitUseStrict` フラグは、Google Closure Compiler(GCC)のプロセッサ関数に追加され `com.adobe.granite.ui.clientlibs.impl.HtmlLibraryManagerImpl`ます。 フラグは、 `use strict` 命令(NPR-34830)の出力を抑制する。
* A `NullPointerException` が、毎日または毎週のメンテナンスタスクの開始時に返されます(NPR-34702)。
* この [!DNL Apache Sling Health Check] ツールは非推奨です。 代わりに、「 [パターン検出」を使用してコンテンツ違反を検出します](https://experienceleague.adobe.com/docs/experience-manager-64/deploying/upgrading/pattern-detector.html) (NPR-33929)。

### 統合 {#integrations-6483}

* 「 [!UICONTROL 作成] 」ボタンは、フォルダーから [!UICONTROL オーディエンスページ(NPR-35152)に移動すると、オーディエンス] ページに表示されます。

### ユーザーインターフェイス {#ui-6483}

* また、 [!UICONTROL Omnisearch] フィルターインターフェイスの  ユーザー検索パネルは、検索を実行する場所以外の場所からの結果も返します(NPR-34877)。
* [!UICONTROL フィルターパネル] Omnisearch [!UICONTROL インターフェイスを閉じると、左側のレールは] Content [!UICONTROL selectionにリセットされず、これによりパネル(NPR-34483)上の] フィルターが再び開くのを妨げます。
* ページプロパティ `NullPointerException` にアクセスすると、が返されます(NPR-34509)。

### Communities {#communities-6483}

<!-- Following fixes of 6483 are documented on Nov 11 20202 by Vishabh. 
-->

* 製品内の不公平な用語の例はすべて、受け入れられた等価語(NPR-34506)に置き換えられる。

### Commerce {#commerce-6483}

* コレクションに15を超える製品がある場合、コレクションには最初の15の製品のみが表示されます(NPR-34494)。

### フォーム {#forms-6483}

>[!NOTE]
>
>[!DNL Experience Manager Forms] 予定されている [!DNL Experience Manager] 累積Fix Packのリリース日から1週間後に、アドオンパッケージをリリースします。

セキュリティ更新について詳しくは、「 [Experience Managerセキュリティ速報ページ](https://helpx.adobe.com/security/products/experience-manager.html)」を参照してください。

## 以前の累積修正パックに含まれていたホットフィックスと機能パック {#hotfixes-and-feature-packs-included-in-previous-cumulative-fix-packs}

### Adobe Experience Manager 6.4.8.2 {#experience-manager-6482}

AEM Cumulative Fix Pack 6.4.8.2は重要なアップデートで、2020年3月のAEM 6.4 Service Pack 8(6.4.8.0)の一般リリース以降の社内およびお客様向けの修正が含まれています。

AEM 6.4.8.2は、AEM 6.4 Service Pack 8に依存するCumulative Fix Pack(CFP)です。 AEM 6.4 Service Pack 8のインストール後にCFPをインストールします。

AEM 6.4.8.2では、組み込みのリポジトリ(Apache Jackrabbit Oak)がバージョン1.8.22に更新されました。

For information on CFP and other types of releases, see [AEM Update Release Vehicle Definitions](https://docs.adobe.com/content/help/en/experience-manager-65/deploying/deploying/update-release-vehicle-definitions.html)

Adobe Experience Manager6.4.8.2には、次の問題の修正が含まれています。

#### Sites {#sites-6482}

* ロールアウト設定 `RolloutConfigManagerFactoryImpl` をロードできない場合、ロードは行われない設定をロードしません。 キャッシュされた設定(NPR-34091)を返します。
* Textコアコンポーネントでは、ソースHTML編集オプションを使用した後、 `em` タグからのクラスが削除されます(NPR-34080)。
* Experience Manager6.2からExperience Manager6.5にアップグレードした場合、静的テンプレートのParsysコンポーネントが正しく表示されません。 Parsysコンポーネントの高さは0に設定され、その中のコンポーネントは表示されません(NPR-34044)。
* テンプレートエディター(NPR-33908)内の許可されたコンポーネントについては、ラベル情報は表示されません。

   ![レイアウトコンテナにラベルが見つかりません](assets/33908_missing_labels.png)

* ユーザは、ネストされたコンポーネントの4番目のレベル(NPR-33873)の後で、parsysにコンポーネントを追加または編集できません。
* 編集可能なテンプレートの初期コンテンツが変更され、その後テンプレートが公開された場合、このテンプレートで作成された新しいページには、ページが公開されていなくても、テンプレートの公開日が表示されます(NPR-33822)。
* コピー `cq:acLinks` および貼り付け操作中に、コピー `cq:acUUID`[!DNL Adobe Campaign] 上のプロパティとプロパティが削除されます(NPR-33793)。
* 「 [!UICONTROL 使用状況] 」タブには、49件の結果のみが表示されます。 コンポーネントの使用状況の一部が表示されるわけではありません(NPR-33710)。
* URLに `/` 文字が含まれるWebページは、オーサリング中に応答しなくなります。 オーサリング中にコンポーネントが追加されると、CPU使用量が増加し、ブラウザーは応答を停止します(NPR-33625)。
* のインライン編集モードで [!DNL RTE]は、画像のドラッグがテキストコンポーネント(NPR-33579)で動作しません。
* Blueprintページ内に、ページ名と同じ名前のコンポーネントを作成できます。 ロールアウト時に、このようなコンポーネントの名前はサフィックスによって変更され `_msm_moved`ます。 ただし、コンポーネントは [!UICONTROL Paragraph System] (NPR-33534)の末尾に移動されます。
* 最初のコンテンツルートで「サブページを [!UICONTROL 含む] 」プロパティがチェックされていない場合、「開始」プロモーションでページが公開されません(NPR-33533)。
* アンカーを含む [!DNL Experience Manager] ページへのリダイレクトは、URLフラグメントまたはアンカーの後にクエリ文字列を `PageRedirectServlets` 配置するオーサーインスタンスでは機能しません(NPR-34287)。
* `PageRedirectServlet` リンクの失敗を引き起こすSlingマッピングの `.html` 後に追加します(NPR-34271)。
* ページ [!DNL Live Copy] の操作を中止すると、エディターモードで表示されるように、継承が中断されます。 ただし、Pageプロパティでは、継承を表すアイコンは誤って継承が存在し、壊れていないことを示します(NPR-34096)。
* テンプレートを編集ページでの許可されたコンポーネントの表示に関する問題が発生します。(CQ-4297295)
* ChromeおよびFirefoxをアップグレードした後、ポップアップメニューが期待どおりに機能しない。 ページのプロパティを読み込むと、パネルにデータが含まれている場合はパネルが表示されません(CQ-4292995)。

#### Assets {#assets-6482}

* アップロードされたPDFファイルのテキスト抽出が機能せず、PDFファイル内の一部の単語に対するフルテキスト検索がそのPDFファイルの取得に失敗します(NPR-34165)。

   >[!NOTE]
   >この修正を有効にするには、Service Pack 6.4.8.2をインストールした後で、Adobe Experience Managerインスタンスを再起動します。

* アセットの検索候補の中で、バックスラッシュは特殊文字の前に追加されます。アセットの名前には特殊文字が含まれます(NPR-33833)。

* スマートコレクションとして保存されたカスタムフィルターはアセットに正しく適用されないので、検索結果は正確ではありません(NPR-33725)。

* 並べ替えられたフォルダー内のアセットのタイムラインは、アセットが移動されたことを示します(NPR-33580)。

* アセットを一括して公開解除すると、 [!DNL Brand Portal]`Request-URI Too Long` エラーが発生します(NPR-34158)。

* 列表示で、アセットのセットを選択した後に [!UICONTROL Filter] （フィルター）オプションを選択し、別のアセットを選択して移動すると、以前に選択したアセットも新しい場所(NPR-34018)に移動されます。

* ページに収まるアセットが多数ある場合でも、リスト表示ではスクロールバーが表示されません(NPR-34156)。

* アセットのパブリケーション [!UICONTROL の管理] ページが壊れ、そのオプションが機能しません。(CQ-4302509)

**Dynamic Media**

* 画像プロファイルが複数（例えば11）の縦横比を持つフォルダー(NPR-34083)に追加されると、スマート切り抜き機能がエラーで失敗します。

* [!UICONTROL Adobe Experience Manager] での画像プリセットに対する変更が、Scene7パブリッシングシステム(NPR-34284、CQ-4299713)と同期されません。

* [!UICONTROL PANORAMICVIEW_AUTOROTATE] 修飾子のラベルが、 [!UICONTROL ビューアプリセットエディタ] ーページの「動作  」タブに表示されません(CQ-4302043)。

#### プラットフォーム {#platform-6482}

* デフォルトエージェント（公開）設定の「 **[!UICONTROL 接続タイムアウト]** 」と「 **[!UICONTROL ソケットタイムアウト]** 」のデフォルト値は指定されていません(NPR-33708)。
* メンテナンスタスクスケジューラー開始は、設定されたタスクよりも頻繁にメンテナンスを停止します(NPR-33520)。
* アップグレードしたExperience Managerインスタンス(NPR-34419)で、診断ツールを使用してログをダウンロードできません。

#### 統合 {#integrations-6482}

* 移行元のライブラリの `library_path` ライブラリURLを生成する場合、の値は考慮され [!DNL Adobe Launch][!DNL Adobe Dynamic Tag Management]ません。 また、移行されたライブラリは、ライブラリとは異なるプレフィックスを使用し [!DNL Adobe Launch] ます。 (NPR-34238).
* クラウドサービスから継承されたプロパティは、ページプロパティの更新時に保持されません(NPR-33865)。

#### ユーザーインターフェイス {#ui-6482}

* 検索ページ上で選択されたアセットの数の表示が正しくありません(NPR-33540)。

#### Communities {#communities-6482}

* 管理コンソールを介して追加されたコミュニティグループの既存のユーザは、コミュニティグループコンソール(NPR-34312)で変更が行われると、ユーザリストから削除される。

#### フォーム {#forms-6482}

>[!NOTE]
>
>[!DNL Experience Manager] 累積Fix Packにはの修正が含まれていません [!DNL Experience Manager Forms]。 They are delivered using a separate [!DNL Forms] add-on package. In addition, a cumulative installer is released that includes fixes for [!DNL Experience Manager Forms] on JEE. For more information, see [Install AEM Forms add-on package](#install-aem-forms-add-on-package) and [Install AEM Forms JEE installer](#install-aem-forms-jee-installer).

**アダプティブフォーム**

* アダプティブフォームフラグメントが見つからない場合、アダプティブフォームはレンダリングに失敗します(NPR-34303)。

* アダプティブフォームのフィールドのヘルプコンテンツの説明には、段落HTMLタグ(NPR-34117)が表示されます。

* Formsコンテナを [!DNL Experience Manager Sites] ページに追加すると、ページに次のエラーメッセージが表示され、新しいコンポーネントの追加は許可されません。(NPR-33858)

   `DevTools failed to load SourceMap: Could not load content for <Link>. HTTP error: status code 404, net::ERR_HTTP_RESPONSE_CODE_FAILURE`

* 「サーバーで **[!UICONTROL 再検証]** 」プロパティを選択し、複数の添付ファイルをアップロードすると、アダプティブフォームは送信に失敗します(NPR-33701)。

* 「 **[!UICONTROL Use Page Language]** and **[!UICONTROL Form」を選択した場合、ページ上のコンポーネント内の「Page]**[!DNL Experience Manager Forms][!DNL Experience Manager Sites] （ページ言語およびフォーム）」オプションの幅全体がカバーされると、ページは翻訳に失敗します(NPR-33641)。

* ページに埋め込まれたAnalyticsが有効なアダプティブフォームを送信すると、 [!DNL Experience Manager Sites] 解析が正しく動作しません(NPR-31359)。

* ライブラリ [!DNL Lodash][!DNL backbone] とライブラリに対する依存関係を削除しました(NPR-33458)。

* 「 **[!UICONTROL RESTエンドポイントへの送信]** 」の送信アクションが、アダプティブフォーム(NPR-34513)では機能しません。

* アクセシビリティ：必須フィールドの添付ファイルをアップロードせずにアダプティブフォームを送信しようとすると、フォーカスが自動的に添付フィールドに移動することはありません(NPR-34511)。

**ワークフロー**

* [!DNL Experience Manager] ワークフローの削除操作が失敗し、次のエラーメッセージが表示されます(NPR-33576)。

   `java.lang.UnsupportedOperationException: The query read more than 500000 nodes in memory`

* 6.4.8.1をインストール [!DNL Experience Manager] すると、項目 [!UICONTROL のTo Do] リストはリンクとして表示されません。 「 [!UICONTROL To Do] 」項目のテキストには、HTMLタグ(NPR-34318)が含まれます。

**BackendIntegration**

* AWSがホストする [!DNL Experience Manager Forms Linux] 環境(NPR-33617)でフォームデータモデルを設定できません。

**デザイナー**

* が [!DNL Acrobat DC] Formsサーバーにインストールさ [!DNL Experience Manager] れている場合、 **[!UICONTROL 「フォームを配布]**[!DNL Experience Manager Designer] 」オプションはバージョン6.xでは使用できません(NPR-34325)。

**Document Security**

* 6.4.8.0をインストールした後、PDFファイル内のHSMベースの証明書を使用して署名操作を実行できない( [!DNL Experience Manager] NPR-34309)。

**アップグレード**

* 環境でドキュメントセキュリティ [!DNL JBoss] を使用する場合は、バージョン7.0.9にアップグレードすると [!DNL Experience Manager Forms][!DNL Linux] 、エラーが発生します(CQ-4300546)。

セキュリティ更新について詳しくは、「 [Experience Managerセキュリティ速報ページ](https://helpx.adobe.com/security/products/experience-manager.html)」を参照してください。

### Adobe Experience Manager 6.4.8.1 {#experience-manager-6481}

AEM Cumulative Fix Pack 6.4.8.1は重要なアップデートで、2020年3月のAEM 6.4 Service Pack 8(6.4.8.0)の一般リリース以降の社内およびお客様向けの修正が含まれています。

AEMの累積Fix Pack 6.4.8.1は、AEM 6.4 Service Pack 8に依存します。 そのため、AEM 6.4 Service Pack 8をインストールした後で、AEM Cumulative Fix Pack 6.4.8.1パッケージをインストールする必要があります。

AEM 6.4.8.1の主な特徴は次のとおりです。

* CRXDE Liteへの匿名アクセスは、セキュリティを強化するために許可されていません。 代わりに、ユーザーはログイン画面に誘導されます。 See [developing with CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md).
* パッケージ共有のAdobe Experience Managerとの統合を削除しました。
* 組み込み型のリポジトリ（Apache Jackrabbit Oak）をバージョン 1.8.21 に更新しました。

For information on CFP and other types of releases, see [AEM Update Release Vehicle Definitions](https://docs.adobe.com/content/help/en/experience-manager-65/deploying/deploying/update-release-vehicle-definitions.html)

Adobe Experience Manager6.4.8.1では、次の問題が修正されました。

#### Sites {#sites-6481}

* 匿名ユーザーはCRX DE Lite機能(NPR-33522)にアクセスできます。
* LiveCopyのローカルコンポーネントの名前が、設計図のコンポーネントの名前と同じで、そのコンポーネントが設計図からロールアウトされる場合、ローカルコンポーネントの名前に_msm_movedという用語は追加されません(NPR-33207)。
* 元の要求に追加されたパラメーターは、リダイレクトURL(NPR-33174)には含まれません。
* Coral.SelectオプションでemptyOption=trueが設定されるか、値= &quot;&quot;のデフォルト項目が含まれている場合、dropdownshowide.jsファイルで次のエラーが発生します。Uncaught TypeError:component.getValueが関数ではありません(NPR-33163)。
* コンポーネントがデータを含む別のコンポーネントをデータを含む場合、親コンテナコンポーネントプレースホルダは内部コンポーネントプレースホルダ(NPR-33119)に置き換えられる。
* スキーマに基づくコンテンツフラグメントの基本で、そのコンテンツに必須のテキスト領域またはパスフィールドが含まれている場合、コンテンツフラグメントの保存は失敗します(NPR-33007)。
* 既製のエクスペリエンスフラグメントコンポーネントを使用してカスタムコンポーネントを作成し、それをAEM Sitesページで使用する場合、AEMはカスタムコンポーネントの参照（使用）を表示しません(NPR-32852)。
* AEM Sitesページが複数のライブコピーが設定された大きなコンテンツセットに含まれている場合、ページバージョン履歴プレビューの読み込みに失敗します(NPR-32772)。
* 起動をプロモートすると、「cq:LiveRelationship」ミックスインが起動に追加されたすべてのコンポーネントに追加されます。 「 —Inherit source page live data — 」オプションを選択して（または選択せずに）起動が作成された場合には関係なく、すべての起動に影響します。(NPR-32664)
* ページ番号の開始では、エクスペリエンスフラグメントピッカーはすべての項目を読み込みません(NPR-32605)。
* AEM Sitesページの開始を作成できません。 起動の作成の結果、エラーが発生します(NPR-32544)。
* 「パブリケーションを管理」では、アクティベーションワークフローの要求に参照先のアセットが含まれません(NPR-32463)。
* ディスパッチャーの正常性チェックで、ログファイルに `Invalid cookie header` 警告メッセージが表示されます(NPR-33630)。
* Salesforce統合はSSRF(NPR-32671)に対して脆弱です。
* PreferencesServlet(NPR-33439)でXSSが反映されている。

#### Assets {#assets-6481}

* リスト表示(NPR-33285)での選択の変更に従って、アセットの数は変わりません。

* 親ノード（子フォルダーが1つ表示される）を選択した後で子フォルダーを選択すると、「次へ」ボタンが有効になりません(NPR-33284)。

* タッチUIは、DMS7またはハイブリッドモードが有効な場合(NPR-33175)、リポジトリルートで読み取りアクセス権を持たないユーザーに表示されません（エラーが発生）。

* ダウンロードしたzipファイル(NPR-33150)で、フォルダー名やアセット名に含まれるGB18030文字が空白に変わります。

* 親フォルダー内にあるアセットの名前にドット `.` 文字が含まれたアセットをスマート切り抜きする際に、追加のフォルダーが作成されます(NPR-32755)。

* 遅延読み込みはトリガーされず、通知インボックス(NPR-32749)からタスクを確認するように選択した場合は、100以下のアセットが表示されます。

* coral-info(NPR-32510)の変更により、コレクションを共有するリンクページが破損しました。

* バルクアップロード中にアセットの処理が停止する(CQ-4293916)。

* Experience ManagerのSSRF脆弱性(NPR-33437)。

#### プラットフォーム {#platform-6481}

* マップエントリが [!DNL Sling]`sling:match``/etc/maps` (NPR-33308)の下に作成された場合、フィルターは呼び出されません。
* すべてのフラッシュエージェントは、ページの非アクティブ化時にトリガされます(NPR-32941)。
* APIを使用してJavaScriptライブラリを縮小すると、ログファイルに、JavaScriptコードが厳密なモードに準拠していないことを示すエラーメッセージが表示されます。 `ScriptProcessor` APIには、厳密なモードを有効または無効にするオプションはありません。 (NPR-32746).
* SQLクエリが7時間など長い時間実行されると、AEMは応答を停止します(NPR-33043)。

#### ユーザーインターフェイス {#ui-6481}

* 選択ダイアログを使用してパスを検索または参照する場合、選択ダイアログには、画像のみを表示するのではなく、選択したJCRノードのすべてのコンテンツが表示されます(NPR-32712)。

#### 翻訳プロジェクト {#tranlation-6481}

* 翻訳ジョブの実行時にログに `NullPointerException` エラーが表示されます(NPR-32220)。

#### 統合 {#integrations-6481}

* JSONのクロスサイトスクリプティング(NPR-32745)。

#### Communities {#communities-6481}

* 作成者は、新しいグループを作成した後、11の [!UICONTROL コミュニティグループ][!DNL Internet Explorer] (NPR-33202)セクションにリダイレクトされません。
* [!UICONTROL アクティビティストリーム] ページ(NPR-33152)へのアクセス時にエラーが発生します。
* グループを編集してサムネール画像を変更しても、グループサムネール画像は更新されません(NPR-32603)。 [!DNL Communities]
* ユーザー生成コンテンツ(UGC)の通知と購読のバージョンを作成すると、ソースページの誤ったIDが保存されます(CQ-4289703)。
* クロスサイトスクリプティングの問題(NPR-33212)。

#### ワークフロー {#workflow-6481}

* 一部のコンポーネントは、ユーザーが [!UICONTROL ダイアログ参加者の手順] (NPR-32989)を含むワークフローを完了するとポップアップするダイアログボックスに表示されません。

* 左側のレールの「 [!UICONTROL タイムライン] 」オプションの読み込みに予想以上に時間がかかります(NPR-32850)。

#### フォーム {#forms-6481}

>[!NOTE]
>
>AEM Cumulative Fix Packには、AEM Formsの修正は含まれていません。 別の Forms アドオンパッケージを使用して配布されます。さらに、JEE上のAEM Formsの修正を含む累積インストーラーがリリースされました。 For more information, see [Install AEM Forms add-on package](#install-aem-forms-add-on-package) and [Install AEM Forms JEE installer](#install-aem-forms-jee-installer).

* Correspondence Management:ユーザが [!DNL Word] ドキュメントからコンテンツを貼り付けると、テキストドキュメントフラグメントは書式を保持しません(NPR-33213)。
* アダプティブForms:アダプティブフォームの辞書の文字列に対する新しい行で、 `&#xa;` 文字が辞書(NPR-33265)に追加されます。
* アダプティブForms:複数の添付ファイルが含まれるアダプティブフォームを保存できません(NPR-33214)。
* アダプティブForms: `AddInstance` と、Instance Managerクラスの `RemoveInstance` メソッドは、遅延読み込みフラグメントの動的な数のインスタンスを [!DNL Internet Explorer 11] (NPR-33201)に追加しません。
* アダプティブForms:ページに埋め込まれたアダプティブフォームで有効にされている解析で、送信イベントおよび放棄のデータが記録されません(NPR-31359)。 [!DNL Sites]
* アダプティブForms:ユーザーがドキュメントのコンテンツをアダプティブフォームに貼り付けて送信すると、送信されたアダプティブフォームにはUnicode文字が含まれます。 [!DNL Word] また、PDFからPDF/Aへの変換は、Unicode文字(NPR-33348)のため失敗します。
* BackendIntegration:非アクティブな状態が正しくないために更新トークンの期限が切れると、フォームデータモデルの要求は失敗します(NPR-33168)。
* ドキュメントサービス：Convert PDFサービスで、サー [!DNL WebLogic][!DNL Linux] バー上のGibson jarが見つからないため、PDFドキュメントをPostScriptに変換できません(NPR-33515、CQ-4292239)。
* ドキュメントサービス：ユーザーがテキストファイルをPDFに変換すると、日本語の文字は正しくレンダリングされません(NPR-33239)。
* GuideSOMProviderServlet(NPR-32701)に格納されたXSS。

## Install 6.4.8.3 {#install}

### セットアップ要件 {#setup-requirements}

<!--

>[!NOTE]
>
>For successful installation of AEM 6.4.6.0 on the instance, it is strongly recommended to upgrade the version of com.adobe.granite.oak.s3connector to 1.8.4 for the customers who are on the older version of s3 connector.
>The process of upgrading the com.adobe.granite.oak.s3connector is available at [https://helpx.adobe.com/in/experience-manager/6-4/sites/deploying/using/data-store-config.html](https://helpx.adobe.com/in/experience-manager/6-4/sites/deploying/using/data-store-config.html).
>Download the latest version of com.adobe.granite.oak.s3connector from: [https://repo.adobe.com/nexus/content/groups/public/com/adobe/granite/com.adobe.granite.oak.s3connector/](https://repo.adobe.com/nexus/content/groups/public/com/adobe/granite/com.adobe.granite.oak.s3connector/)

-->

>[!CAUTION]
>
>AEM 6.4にFeature Packをインストールしているお客様の場合。Adobeが提供するオプションのFeature Packは、リリースバージョンとサービスパックに依存しています。 機能パックがインストールされている場合は、AEMカスタマーケアチームに問い合わせて、AEM 6.4用の累積的な修正パックとこれらの機能パックの互換性を検証してください。

* AEM 6.4.8.3 requires AEM 6.4.8.0. Please visit [upgrade documentation](../sites-deploying/upgrade.md) for detailed instructions.
* MongoDB と複数のインスタンスを含むデプロイメントでは、パッケージマネージャーを使用してオーサーインスタンスの 1 つに AEM 6.4.8.3 をインストールしてください。
* 累積修正パックをインストールする前に、AEMインスタンスのスナップショットまたは新規バックアップが必要です。
* インストールする前にインスタンスを再起動してください。これは、インスタンスがまだ更新モードになっている場合（インスタンスが以前のバージョンから更新されたばかりの場合）にのみ必要ですが、インスタンスが長期間実行されている場合は、一般的に推奨されます。

>[!NOTE]
>
>AEM 6.4.8.3 パッケージを削除またはアンインストールすることはお勧めしません。

### 累積Fix Packのインストール {#install-cumulative-fix-pack}

既存の AEM 6.4.8.0 インスタンスに累積修正パックをインストールするには、次の手順を実行します。

1. 「 [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq640/cumulativefixpack/aem-6.4.8-cfp-3.0.zip) 」リンクをクリックして、パッケージをダウンロードします。

1. Open [Package Manager](http://localhost:4502/crx/packmgr/index.jsp) and click **[!UICONTROL Upload Package]** to upload the package.

1. Select the package name and click **[!UICONTROL Install]**.

>[!NOTE]
>
>**6.4.8.3 のインストール中に、パッケージマネージャー UI のダイアログが途中で終了することがあります。**
>
>そのため、エラーログが安定するのを待ってから、インスタンスにアクセスすることをお勧めします。ユーザーは、アップデーターバンドルのアンインストールに関連する特定のログを待ってから、インストールが正常に行われることを確認する必要があります。 通常は、Safari で発生しますが、任意のブラウザーで断続的に発生する可能性があります。

### 自動インストール {#auto-installation}

実行中のインスタンスに AEM 6.4.8.3 を自動的にインストールするには、次の 2 つの方法があります。

A. Place the package into ..*/crx-quickstart/install* folder while the server is running. パッケージは自動的にインストールされます。

B. Use the [HTTP API from Package Manager](https://docs.adobe.com/content/docs/en/crx/2-3/how_to/package_manager.html) - make sure you use `cmd=install&recursive=true` - so the nested package are installed.

>[!NOTE]
>
>AEM 6.4.8.3 では、ブートストラップインストールをサポートしていません。

### インストールの検証 {#validate-install}

1. 製品情報ページ（*/system/console/productinfo*）のインストール済み製品には、更新されたバージョン文字列「Adobe Experience Manager, Version 6.4.8.3」が表示されます。
1. すべての OSGI バンドルは、OSGI コンソール（Web コンソールを使用：/system/console/bundles）で ACTIVE または FRAGMENT です。
1. OSGIバンドルorg.apache.jackrabbit.oak-coreがバージョン1.8.17以降に搭載されています(Webコンソールを使用：/system/console/bundles)。

To determine the certified platform for running with this release of AEM Sites and Assets, see [Technical Requirements](../sites-deploying/technical-requirements.md).

>[!NOTE]
>On successful installation of the package, an informational message appears indicating that the content package has installed successfully, such as **&quot;Content Package AEM-6.4-Service-Pack-8 installed successfully.&quot;**

### ダイナミックメディアビューアの更新(5.10.1) {#update-dynamic-media-viewers}

AEM 6.4.8.3には、画像プリセットページの重複名のチェックを有効にする、新しいバージョンのダイナミックメディアビューア(5.10.1)が含まれています。 ダイナミックメディアのお客様には、次のコマンドを実行して、初期設定のビューアプリセットを最新の状態にすることをお勧めします。

`curl -u admin:admin http://localhost:4502/libs/settings/dam/dm/presets/viewer.pushviewerpresets`

新しいビューアプリセットを/confの場所にコピーします。

### AEM Forms アドオンパッケージのインストール {#install-aem-forms-add-on-package}

>[!NOTE]
>
>[!DNL Experience Manager Forms] 予定されている [!DNL Experience Manager] 累積Fix Packのリリース日から1週間後に、アドオンパッケージをリリースします。

>[!NOTE]
>
>AEM Forms を使用していない場合はスキップしてください。AEM Forms の修正は、個別のアドオンパッケージを介して配信されます。

1. AEM Cumulative Fix Packがインストールされていることを確認します。
1. Download the corresponding forms add-on package listed at [AEM Forms releases](https://helpx.adobe.com/jp/aem-forms/kb/aem-forms-releases.html) for your operating system.
1. Install the forms add-on package as described in [Installing AEM forms add-on packages](https://docs.adobe.com/content/help/en/experience-manager-64/forms/install-aem-forms/osgi-installation/installing-configuring-aem-forms-osgi.html#install-aem-forms-add-on-package).

### AEM Forms JEE インストーラーのインストール {#install-aem-forms-jee-installer}

>[!NOTE]
>
>JEE で AEM Forms を使用していない場合はスキップします。AEM Forms JEE の修正は別のインストーラーを介して配布されます。

AEM Forms JEE の累積インストーラーのインストールとデプロイメント後の設定について詳しくは、[AEM Forms JEE パッチインストーラー ](jee-patch-installer-64.md) を参照してください。

### Uber Jar {#uber-jar}

The Uber Jar for AEM 6.4.8.3 is available in the [Maven Central repository](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.4.8.3/).

To use Uber Jar in a Maven project, refer to the article, [How to use Uber jar](../sites-developing/ht-projects-maven.md) and include the following dependency in your project POM:

```shell
<dependency>
      <groupId>com.adobe.aem</groupId>
      <artifactId>uber-jar</artifactId>
      <version>6.4.8.3</version>
      <scope>provided</scope>  
</dependency>
```

>[!NOTE]
>
>UberJarおよびその他の関連アーティファクトは、AdobeのパブリックMavenリポジトリ(repo.adobe.com)ではなく、Maven Centralリポジトリで使用できます。 メインのUberJarファイルの名前がに変更され `uber-jar-<version>.jar`ます。 その結果、 `classifier`タグに値 `apis``dependency` はありません。

## 廃止される機能および削除された機能 {#removed-deprecated-features}

このセクションでは、AEM 6.4 で廃止される機能および削除された機能について説明します。

| 領域 | 機能 | 代替手段 | バージョン |
|---|---|---|---|
| Assets | サブアセットのタグアクションの管理 | 代替機能はありません | AEM 6.4.2.0 |
| Assets と Adobe Creative Cloud の統合 | [AEM 6.2では、クリエイティブユーザーにAEMのアセットへのアクセスを許可する方法として、AEMからCreative Cloudへのフォルダ共有が導入されました。](https://docs.adobe.com/content/help/en/experience-manager-64/assets/administer/aem-cc-folder-sharing-best-practices.html) Creative Cloud アプリケーションでリリースされた新しい機能である Adobe Asset Link では、ユーザーエクスペリエンスが大幅に向上し、Photoshop、InDesign、Illustrator 内から AEM のアセットへの直接アクセスが強化されています。アドビは、このフォルダー共有機能をさらに強化する予定はありません。この機能はAEMに含まれていますが、お客様には交換の使用を強くお勧めします。 | Adobeアセットリンクまたはデスクトップアプリ 詳細については、[AEM Creative Cloud の統合](/help/assets/aem-cc-integration-best-practices.md)記事を参照してください。 | AEM 6.4.4.0 |

## 既知の問題 {#known-issues}

* 6.4から [!DNL Experience Manager] 6.5にアップグレードすると、一部のバンドルのステータスが「として表示されない場合があり [!DNL Experience Manager]`Active`ます。 最新の [!DNL Experience Manager] 6.5 Service Packをインストールして問題を解決します。

AEM 6.4.8.0 Service Packの既知の問題については、『 [AEM 6.4.8.0 Service Packリリースノート](sp-release-notes.md)』を参照してください。

## OSGi バンドルとコンテンツパッケージが含まれています {#osgi-bundles-and-content-packages-included}

次のテキストドキュメントリストは、AEM 6.4.8.3に含まれるOSGiバンドルとコンテンツパッケージを示します。

AEM 6.4.8.3 に含まれている OSGi バンドルの一覧

[ファイルを入手](assets/6.4.8.3_osgi_bundles.txt)

AEM 6.4.8.3 に含まれているコンテンツパッケージの一覧

[ファイルを入手](assets/6.4.8.3_content_packages.txt)

## 参考リソース {#helpful-resources}

* [AEM 6.4 リリースノート](../release-notes/release-notes.md)
* [AEM 製品ページ](https://www.adobe.com/solutions/web-experience-management.html)
* [AEM 6.4 ドキュメント](https://helpx.adobe.com/jp/support/experience-manager/6-4.html)
* [Adobe優先度の製品アップデートの購読](https://www.adobe.com/subscription/priority-product-update.html)

## 制限付きサイト {#restricted-sites-new}

以下のサイトは既存ユーザーのみが参照できます。アクセス権が必要な既存ユーザーの方は、アドビのアカウントマネージャーまでお問い合わせください。

* [licensing.adobe.com からの製品ダウンロード](https://licensing.adobe.com/)
* [カスタマーサポートに連絡](https://docs.adobe.com/content/help/en/customer-one/using/home.html)
