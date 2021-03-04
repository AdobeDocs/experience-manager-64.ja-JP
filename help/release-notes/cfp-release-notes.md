---
title: 'AEM 6.4 累積修正パックリリースノート '
description: Adobe Experience Manager6.4累積Fix Pack固有のリリースノート
contentOwner: AK
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: 7c19ef4a56fbfaa2f43b71e4dc48c79f797f32a8
workflow-type: tm+mt
source-wordcount: '4680'
ht-degree: 16%

---


# AEM 6.4 累積修正パックリリースノート {#aem-cumulative-fix-pack-release-notes}

## リリース情報 {#release-information}

<!-- TBD: Update the SD URL. -->

| 製品 | **Adobe Experience Manager（AEM）6.4** |
|---|---|
| バージョン | 6.4.8.4 |
| タイプ | 累積修正パック     |
| 日付 | 2021 年 2 月 25 日 |
| 前提条件 | [AEM 6.4 サービスパック 8（6.4.8.0）](sp-release-notes.md) |
| ダウンロード URL | [ソフトウェア配布](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq640/cumulativefixpack/aem-6.4.8-cfp-4.0.zip) |

## AEM 6.4.8.4 に含まれる機能 {#what-s-included-in-aem}

AEM Cumulative Fix Pack 6.4.8.4は重要なアップデートで、2020年3月のAEM 6.4 Service Pack 8(6.4.8.0)の一般リリース以降の社内およびお客様向けの修正が含まれています。

AEM 6.4.8.4は、AEM 6.4 Service Pack 8に依存するCumulative Fix Pack(CFP)です。 AEM 6.4 Service Pack 8のインストール後にCFPをインストールします。

[!DNL Adobe Experience Manager] 6.4.8.4で導入された主な機能と拡張機能は次のとおりです。

* PDFG変換の実行時に[!DNL Experience Manager Forms]レジストリ変更を有効または無効にする機能。

* フォームデータモデルのSOAPベースWebサービス用のX-509証明書ベースの認証。

* 組み込み型のリポジトリ（Apache Jackrabbit Oak）をバージョン 1.8.24 に更新しました。

CFPと他のタイプのリリースについて詳しくは、[AEM Update Release Vehicle Definitions](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-release-vehicle-definitions.html?lang=en)を参照してください。

Adobe Experience Manager6.4.8.4には、次の問題の修正が含まれています。

### Sites {#sites-6484}

* Experience Managerサービスパック6.4.8.2をインストールした後は、コンテンツフラグメントモデルを編集できず、次のエラーが発生します。

   `Uncaught TypeError: Cannot read property 'debounce' of undefined` (NPR-35312)
* ユーザーが「ログアウト」ボタンをクリックしても、ユーザーはPackage Managerからログアウトされません。 (NPR-35161)
* Experience Manager6.4.xからExperience Manager6.4.8.3にアップグレードした後、「パブリケーションの管理」を使用してページを公開できなくなります。 (CQ-4312511)
* BluePrintの子ページを元の場所に戻すと、cq:liveSyncConfig設定はライブコピーの子ページから削除されません。 (NPR-35900)
* ライブコピーを持つBluePrintを前後に移動する場合、最初の移動のみが機能し、失敗してエラーメッセージは表示されません。 (NPR-35899)


### [!DNL Assets] {#assets-6484}

* `IndexWriter.merge` を指定すると、スマートタグ機能によって大き `OutOfMemoryError` い `/oak:index/lucene` インデックスとインデックスが作成されるので、 `/oak:index/ntBaseLucene` エラーが発生します(NPR-35650)。
* ユーザーは、[!DNL Adobe InDesign]でアセットを編集した後にチェックインできず、権限がないことに関するエラーを受け取ることができません(NPR-35340)。
* 名前の競合を解決した後に既存のアセットの新しいバージョンが作成されると、元のアセットのメタデータが上書きされます(NPR-35939)。
* 自動生成されたプライベートフォルダーグループは、フォルダーの削除時や[!UICONTROL 「プライベートフォルダーの制限を削除]」オプションを設定してフォルダーを更新する際には、維持されず、削除されません(NPR-35625)。

#### [!DNL Dynamic Media] {#dynamic-media}

* 断続的なImageServerエラーが発生すると、[!DNL Experience Manager]のいくつかの機能に対する403応答が発生し、その結果、が失敗します。 (CQ-4308565)

### 統合 {#integrations-6484}

* Experience Manager6.4.8.3にアップグレードした後にページのプロパティを開くと、JavaScriptエラー開始がコンソールに表示されます(NPR-35649)。

### Forms {#forms-6484}

>[!NOTE]
>
>[!DNL Experience Manager Forms] では、予定されている [!DNL Experience Manager] 累積修正パックリリース日の 1 週間後にアドオンパッケージをリリースします。

**Correspondence Management**

* レターを編集する場合、条件が指定されたモジュールの読み込みには時間がかかります(NPR-35326)。

* レターを編集する場合、コンテンツとデータ連結がユーザーインターフェイスに表示されません(CQ-4312905)。

**ドキュメントサービス**

* [!DNL JAVA]を[!DNL JDK1.8.0_261]にアップグレードした後にPDFをアセンブルできない(NPR-35761、NPR-35848)。

**Foundation JEE**

* [!DNL Forms]ワークフローでタスク通知を編集すると、その通知を保存できません。(CQ-4315055)

セキュリティ更新について詳しくは、[Experience Managerのセキュリティ速報ページ](https://helpx.adobe.com/security/products/experience-manager.html)を参照してください。

## 以前の累積修正パックに含まれていたホットフィックスと機能パック {#hotfixes-and-feature-packs-included-in-previous-cumulative-fix-packs}

### Adobe Experience Manager 6.4.8.3 {#experience-manager-6483}

AEM Cumulative Fix Pack 6.4.8.3は重要なアップデートで、2020年3月のAEM 6.4 Service Pack 8(6.4.8.0)の一般リリース以降の社内およびお客様向けの修正が含まれています。

AEM 6.4.8.3は、AEM 6.4 Service Pack 8に依存するCumulative Fix Pack(CFP)です。 AEM 6.4 Service Pack 8のインストール後にCFPをインストールします。

AEM 6.4.8.3では、組み込みのリポジトリ(Apache Jackrabbit Oak)がバージョン1.8.23に更新されました。

CFPと他のタイプのリリースについて詳しくは、[AEM Update Release Vehicle Definitions](https://docs.adobe.com/content/help/en/experience-manager-65/deploying/deploying/update-release-vehicle-definitions.html)を参照してください。

Adobe Experience Manager6.4.8.3には、次の問題の修正が含まれています。

#### サイト{#sites-6483}

* コンテンツフラグメントのバリエーションのテキストを更新すると、そのバリエーションの代わりにマスターコンテンツフラグメントのコンテンツが更新されます(NPR-35080)。

* コンポーネントの「String type label」プロパティに数値を設定した場合は、コンポーネントを削除し、「元に戻す」オプションを使用して元に戻すと、labelプロパティのタイプが自動的に「String」から「Long」に変更されます(NPR-34738)。

* 複数フィールドにファイルアップロードコンポーネントを追加する場合、画像パスは、複数フィールドノード(NPR-34423)ではなく、コンポーネントノードに保存されます。

* ページの移動ウィザードで、移動先が選択されていない場合でも、次のボタンは有効なままです(NPR-34460)。

* 親コンポーネントに`cq:isContainer`プロパティが含まれる場合、継承されたコンポーネントにはプロパティが自動的に含まれません(CQ-4308409)。

* `calc()`関数を使用してCSS縮小を使用すると、`+`記号の周りの空白が削除されます(NPR-34991)。

* AEMインスタンスを開始すると、`com.adobe.granite.maintenance.impl.MaintenanceTaskManagerImpl`および`com.adobe.granite.maintenance.impl.TaskScheduler`コンポーネントは`Active`状態(NPR-34952)では表示されません。

#### [!DNL Assets] {#assets-6483}

* 既存のアセットのバージョンを作成する場合、メタデータプロファイルがフォルダーに適用されていると、メタデータに対する更新は保持されません(NPR-34833)。
* [!DNL Adobe Asset Link]を[!DNL Adobe InDesign]と共に使用する場合、検索結果にはフォルダーやコレクションは含まれず、アセットのみが含まれます(NPR-34700)。
* フォルダー上のアセットをドラッグして移動すると、ユーザーインターフェイスには、「[!UICONTROL ライトボックスにドロップ]」および「[!UICONTROL コレクションにドロップ]」のオプションも表示されます。 移動操作がキャンセルされた場合でも、ユーザインターフェイスは後者の2つのオプション(NPR-34525)を引き続き表示する。
* 「パブリケーションの管理」インターフェイスを開いた場合、「公開」オプションは使用できず、「非公開」オプションを選択した場合、スコープページが空白になります。(CQ-4302509)

##### [!DNL Dynamic Media] {#dynamic-media-6483}

* 画像プリセット設定で、[!DNL Experience Manager]で「[!UICONTROL JPGクロミナンスダウンサンプリングを有効にする]」オプションの選択が解除されている場合、変更は[!DNL Dynamic Media](NPR-34284)と同期されません。
* [!UICONTROL ビューアプリセットエディター]で、[!UICONTROL PanoramicImage/PanoramicImage_VR]プリセットを編集する場合、`PanoramicView`コンポーネントで`PANORAMICVIEW_AUTOROTATE`修飾子のラベルを使用できません(CQ-4302043)。
* [!DNL Experience Manager]からビデオを非公開にしても、設定済みのDynamic Mediaクラシックにあるアダプティブビデオセットの公開は取り消されません。 (CQ-4304405).

#### Platform {#platform-6483}

* `emitUseStrict`フラグは、Google Closure Compiler(GCC)プロセッサ関数`com.adobe.granite.ui.clientlibs.impl.HtmlLibraryManagerImpl`に追加されます。 フラグは`use strict`命令(NPR-34830)の出力を抑制する。
* 毎日または毎週のメンテナンスタスクを開始すると`NullPointerException`が返されます(NPR-34702)。
* [!DNL Apache Sling Health Check]ツールは廃止されました。 代わりに、[パターンディテクター](https://experienceleague.adobe.com/docs/experience-manager-64/deploying/upgrading/pattern-detector.html)を使用して、コンテンツ違反を検出します(NPR-33929)。

#### 統合 {#integrations-6483}

* [!UICONTROL 「作成]」ボタンは、オーディエンスーから[!UICONTROL オーディエンスー]ページ(NPR-35152)に移動すると、[!UICONTROL フォルダー]ページに表示されます。

#### ユーザーインターフェイス {#ui-6483}

* [!UICONTROL Omnisearch]フィルターインターフェイスの[!UICONTROL ユーザー]検索パネルでも、検索が実行された場所以外の場所からの結果が返されます(NPR-34877)。
* [!UICONTROL Omnisearch]ユーザーインターフェイスの[!UICONTROL フィルター]パネルを閉じても、左側のレールは[!UICONTROL コンテンツ]選択にリセットされず、[!UICONTROL フィルター]パネル(NPR-34483)を再び開けません。
* ページプロパティにアクセスすると`NullPointerException`が返されます(NPR-34509)。

#### Communities {#communities-6483}

<!-- Following fixes of 6483 are documented on Nov 11 20202 by Vishabh. 
-->

* 製品内の不公平な用語の例はすべて、受け入れられた等価語(NPR-34506)に置き換えられる。

#### Commerce {#commerce-6483}

* コレクションに15を超える製品がある場合、コレクションには最初の15の製品のみが表示されます(NPR-34494)。

#### Forms{#forms-6483}

>[!NOTE]
>
>[!DNL Experience Manager Forms] では、予定されている [!DNL Experience Manager] 累積修正パックリリース日の 1 週間後にアドオンパッケージをリリースします。

>[!NOTE]
>
>[!DNL Experience Manager] 累積Fix Packにはの修正が含まれていません [!DNL Experience Manager Forms]。これらは、別の[!DNL Forms]アドオンパッケージを使用して配信されます。 さらに、JEE上の[!DNL Experience Manager Forms]の修正を含む累積インストーラーがリリースされました。 詳しくは、「[AEM Formsアドオンパッケージのインストール](#install-aem-forms-add-on-package)」および「[AEM FormsJEEインストーラーのインストール](#install-aem-forms-jee-installer)」を参照してください。

**アダプティブフォーム**

* [!DNL Experience Manager]累積修正パック(NPR-35127)を適用した後、Classic UIを使用してアダプティブフォームを編集できない。

* キャッシュの無効化(NPR-34655)が原因で、フラグメントのアダプティブフォームへの読み込みに時間がかかります。

* アクセシビリティ：アダプティブフォームのスクリーンリーダーでタブナビゲーションが適切に機能しない(NPR-34550)。

**Correspondence Management**

* ES3からアセットを移行する場合、アセットには編集不可の2つのデフォルト条件(NPR-34971)が含まれます。

**財団法人JEE**

* [!DNL AEM Forms]ユーザーをFlashからHTMLに移行します(CQ-4304075)。

### Adobe Experience Manager 6.4.8.2 {#experience-manager-6482}

AEM Cumulative Fix Pack 6.4.8.2は重要なアップデートで、2020年3月のAEM 6.4 Service Pack 8(6.4.8.0)の一般リリース以降の社内およびお客様向けの修正が含まれています。

AEM 6.4.8.2は、AEM 6.4 Service Pack 8に依存するCumulative Fix Pack(CFP)です。 AEM 6.4 Service Pack 8のインストール後にCFPをインストールします。

AEM 6.4.8.2では、組み込みのリポジトリ(Apache Jackrabbit Oak)がバージョン1.8.22に更新されました。

CFPと他のタイプのリリースについて詳しくは、[AEM Update Release Vehicle Definitions](https://docs.adobe.com/content/help/en/experience-manager-65/deploying/deploying/update-release-vehicle-definitions.html)を参照してください。

Adobe Experience Manager6.4.8.2には、次の問題の修正が含まれています。

#### サイト{#sites-6482}

* `RolloutConfigManagerFactoryImpl`がロールアウト設定を読み込めない場合は、見つからない設定を読み込もうとしません。 キャッシュされた設定(NPR-34091)を返します。
* Textコアコンポーネントでは、ソースHTML編集オプションを使用した後、`em`タグからのクラスが削除されます(NPR-34080)。
* Experience Manager6.2からExperience Manager6.5にアップグレードした場合、静的テンプレートのParsysコンポーネントが正しく表示されません。 Parsysコンポーネントの高さは0に設定され、その中のコンポーネントは表示されません(NPR-34044)。
* テンプレートエディター(NPR-33908)内の許可されたコンポーネントについては、ラベル情報は表示されません。

   ![レイアウトコンテナにラベルが見つかりません](assets/33908_missing_labels.png)

* ユーザーは、ネストされたコンポーネントの4番目のレベル(NPR-33873)の後で、parsysにコンポーネントを追加または編集できません。
* 編集可能なテンプレートの初期コンテンツが変更され、その後テンプレートが公開された場合、このテンプレートで作成された新しいページには、ページが公開されていなくても、テンプレートの公開日が表示されます(NPR-33822)。
* コピー&amp;ペースト操作(NPR-33793)中に、コピー上の`cq:acLinks`と[!DNL Adobe Campaign]のプロパティが削除されます。`cq:acUUID`
* 「[!UICONTROL 使用状況]」タブには、49件の結果のみが表示されます。 コンポーネントの使用状況の一部が表示されるわけではありません(NPR-33710)。
* オーサリング中に、URLに`/`文字が含まれるWebページが応答しなくなります。 オーサリング中にコンポーネントが追加されると、CPU使用量が増加し、ブラウザーは応答を停止します(NPR-33625)。
* [!DNL RTE]のインライン編集モードでは、画像のドラッグがテキストコンポーネント(NPR-33579)で動作しません。
* Blueprintページ内に、ページ名と同じ名前のコンポーネントを作成できます。 ロールアウト時に、`_msm_moved`のサフィックスを付けることで、このようなコンポーネントの名前が変更されます。 ただし、コンポーネントは[!UICONTROL 段落システム]の末尾に移動されます(NPR-33534)。
* 最初のコンテンツルート(NPR-33533)で[!UICONTROL include subpages]プロパティがチェックされていない場合、「プロモーションを起動」はページを公開しません。
* `PageRedirectServlets`がURLフラグメントまたはアンカーの後にクエリ文字列を配置するので、アンカーを含む[!DNL Experience Manager]ページへのリダイレクトは作成者インスタンスでは機能しません(NPR-34287)。
* `PageRedirectServlet` リンクの失敗を引き起こすSlingマッピングの `.html` 後に追加します(NPR-34271)。
* ページの[!DNL Live Copy]を中断すると、エディタモードのように継承が中断されます。 ただし、Pageプロパティでは、継承を表すアイコンは誤って継承が存在し、壊れていないことを示します(NPR-34096)。
* テンプレートを編集ページでの許可されたコンポーネントの表示に関する問題が発生します。(CQ-4297295)
* ChromeおよびFirefoxをアップグレードした後、ポップアップメニューが期待どおりに機能しない。 ページのプロパティを読み込むと、パネルにデータが含まれている場合はパネルが表示されません(CQ-4292995)。
* [!DNL Experience Manager Sites]コンポーネントの複数のクロスサイトスクリプティングインスタンス(NPR-33926)。
* ユーザ入力は、情報をクライアントに送信する際に、様々なコンポーネントに対して適切にエンコードされません(NPR-33696)。
* `childrenlist.html`で終わるURLは、404応答ではなくHTMLページを表示します。 このようなURLは、クロスサイトスクリプティング(NPR-33441)に対して脆弱です。

#### Assets {#assets-6482}

* アップロードされたPDFファイルのテキスト抽出が機能せず、PDFファイル内の一部の単語に対するフルテキスト検索がそのPDFファイルの取得に失敗します(NPR-34165)。

   >[!NOTE]
   >この修正を有効にするには、Service Pack 6.4.8.2をインストールした後で、Adobe Experience Managerインスタンスを再起動します。

* アセットの検索候補の中で、バックスラッシュは特殊文字の前に追加されます。アセットの名前には特殊文字が含まれます(NPR-33833)。

* スマートコレクションとして保存されたカスタムフィルターは、アセットに正しく適用されないので、検索結果は正確ではありません   (NPR-33725)

* 並べ替えられたフォルダー内のアセットのタイムラインは、アセットが移動されたことを示します(NPR-33580)。

* [!DNL Brand Portal]からアセットを一括して非公開にすると、`Request-URI Too Long`エラーが発生します(NPR-34158)。

* 列表示で、アセットのセットを選択した後に「[!UICONTROL フィルター]」を選択し、別のアセットを選択して移動すると、以前に選択したアセットも新しい場所(NPR-34018)に移動されます。

* ページに収まるアセットが多数ある場合でも、リスト表示ではスクロールバーが表示されません(NPR-34156)。

* アセットの[!UICONTROL パブリケーションの管理]ページが壊れており、その中のオプションが機能しません。(CQ-4302509)

**Dynamic Media**

* 画像プロファイルが複数（例えば11）の縦横比を持つフォルダー(NPR-34083)に追加されると、スマート切り抜き機能がエラーで失敗します。

* [!UICONTROL Adobe Experience Manager]の画像プリセットに対する変更がDynamic Mediaクラシック(NPR-34284、CQ-4299713)と同期されません。

* [!UICONTROL PANORAMICVIEW_AUTOROTATE]修飾子のラベルが[!UICONTROL ビューアプリセットエディター]ページ(CQ-4302043)の[!UICONTROL 「動作]」タブにありません。

#### プラットフォーム{#platform-6482}

* デフォルトエージェント（公開）設定の&#x200B;**[!UICONTROL 接続タイムアウト]**&#x200B;および&#x200B;**[!UICONTROL ソケットタイムアウト]**&#x200B;のデフォルト値は指定されていません(NPR-33708)。
* メンテナンスタスクスケジューラー開始は、設定されたタスクよりも頻繁にメンテナンスを停止します(NPR-33520)。
* アップグレードしたExperience Managerインスタンス(NPR-34419)で、診断ツールを使用してログをダウンロードできません。

#### 統合 {#integrations-6482}

* `library_path`の値は、[!DNL Adobe Dynamic Tag Management]から移行されたライブラリの[!DNL Adobe Launch]ライブラリURLを生成する際に考慮されません。 また、移行されたライブラリは[!DNL Adobe Launch]ライブラリとは異なるプレフィックスを使用します。 (NPR-34238).
* クラウドサービスから継承されたプロパティは、ページプロパティの更新時に保持されません(NPR-33865)。

#### ユーザーインターフェイス {#ui-6482}

* 検索ページ上で選択されたアセットの数の表示が正しくありません(NPR-33540)。

#### コミュニティ{#communities-6482}

* 管理コンソールを介して追加されたコミュニティグループの既存のユーザは、コミュニティグループコンソール(NPR-34312)で変更が行われると、ユーザリストから削除される。

#### Forms{#forms-6482}

>[!NOTE]
>
>[!DNL Experience Manager] 累積Fix Packにはの修正が含まれていません [!DNL Experience Manager Forms]。これらは、別の[!DNL Forms]アドオンパッケージを使用して配信されます。 さらに、JEE上の[!DNL Experience Manager Forms]の修正を含む累積インストーラーがリリースされました。 詳しくは、「[AEM Formsアドオンパッケージのインストール](#install-aem-forms-add-on-package)」および「[AEM FormsJEEインストーラーのインストール](#install-aem-forms-jee-installer)」を参照してください。

**アダプティブフォーム**

* アダプティブフォームフラグメントが見つからない場合、アダプティブフォームはレンダリングに失敗します(NPR-34303)。

* アダプティブフォームのフィールドのヘルプコンテンツの説明には、段落HTMLタグ(NPR-34117)が表示されます。

* [!DNL Experience Manager Sites]ページにFormsコンテナを追加すると、そのページには次のエラーメッセージが表示され、新しいコンポーネントの追加は許可されません。(NPR-33858)

   `DevTools failed to load SourceMap: Could not load content for <Link>. HTTP error: status code 404, net::ERR_HTTP_RESPONSE_CODE_FAILURE`

* 「**[!UICONTROL サーバー]**&#x200B;で再検証」プロパティを選択し、複数の添付ファイルをアップロードすると、アダプティブフォームは送信に失敗します(NPR-33701)。

* 「**[!UICONTROL ページの言語を使用]**」および「**[!UICONTROL フォーム」を選択した場合、[!DNL Experience Manager Sites]ページの[!DNL Experience Manager Forms]コンポーネントのページ]**&#x200B;オプションの幅全体がカバーされ、そのページは翻訳に失敗します(NPR-33641)。

* [!DNL Experience Manager Sites]ページに埋め込まれた、解析が有効なアダプティブフォームを送信すると、解析が正しく動作しません(NPR-31359)。

* [!DNL Lodash]ライブラリと[!DNL backbone]ライブラリに対する依存関係を削除しました(NPR-33458)。

* **[!UICONTROL RESTエンドポイントへの送信]**&#x200B;送信アクションは、アダプティブフォーム(NPR-34513)では動作しません。

* アクセシビリティ：必須フィールドの添付ファイルをアップロードせずにアダプティブフォームを送信しようとすると、フォーカスが自動的に添付フィールドに移動することはありません(NPR-34511)。

* ユーザー入力は、クライアントに情報を送信する際に、[!DNL Forms]コンポーネントに対して適切にエンコードされません(NPR-33611)。

**ワークフロー**

* [!DNL Experience Manager] ワークフローの削除操作が失敗し、次のエラーメッセージが表示されます(NPR-33576)。

   `java.lang.UnsupportedOperationException: The query read more than 500000 nodes in memory`

* [!DNL Experience Manager] 6.4.8.1をインストールすると、[!UICONTROL To Do]リストの項目はリンクとして表示されません。 [!UICONTROL To Do]項目のテキストには、HTMLタグ(NPR-34318)が含まれます。

**BackendIntegration**

* AWSがホストする[!DNL Experience Manager Forms Linux]環境(NPR-33617)でフォームデータモデルを設定できません。

**デザイナー**

* [!DNL Acrobat DC]が[!DNL Experience Manager]Formsサーバーにインストールされている場合、**[!UICONTROL バージョン6.x(NPR-34325)では「フォーム]**&#x200B;を配布」オプションを使用できません。[!DNL Experience Manager Designer]

**Document Security**

* [!DNL Experience Manager] 6.4.8.0 (NPR-34309)をインストールした後、PDFファイルでHSMベースの証明書を使用して署名操作を実行できません。

**アップグレード**

* [!DNL Linux]環境でドキュメントセキュリティを使用して[!DNL Experience Manager Forms]の[!DNL JBoss]バージョンを7.0.9にアップグレードすると、エラーが発生します(CQ-4300546)。

セキュリティ更新について詳しくは、[Experience Managerのセキュリティ速報ページ](https://helpx.adobe.com/security/products/experience-manager.html)を参照してください。

### Adobe Experience Manager 6.4.8.1 {#experience-manager-6481}

AEM Cumulative Fix Pack 6.4.8.1は重要なアップデートで、2020年3月のAEM 6.4 Service Pack 8(6.4.8.0)の一般リリース以降の社内およびお客様向けの修正が含まれています。

AEM 累積修正パック 6.4.8.1 は、AEM 6.4 サービスパック 8 に依存しています。そのため、AEM 6.4 Service Pack 8をインストールした後で、AEM Cumulative Fix Pack 6.4.8.1パッケージをインストールする必要があります。

AEM 6.4.8.1の主な特徴は次のとおりです。

* CRXDE Liteへの匿名アクセスは、セキュリティを強化するために許可されていません。 代わりに、ユーザーはログイン画面に誘導されます。 [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md)を使用した開発を参照してください。
* パッケージ共有のAdobe Experience Managerとの統合を削除しました。
* 組み込み型のリポジトリ（Apache Jackrabbit Oak）をバージョン 1.8.21 に更新しました。

CFPと他のタイプのリリースについて詳しくは、[AEM Update Release Vehicle Definitions](https://docs.adobe.com/content/help/en/experience-manager-65/deploying/deploying/update-release-vehicle-definitions.html)を参照してください。

Adobe Experience Manager6.4.8.1では、次の問題が修正されました。

#### サイト{#sites-6481}

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
* ディスパッチャーの正常性チェックで、ログファイルに`Invalid cookie header`警告メッセージが表示されます(NPR-33630)。
* Salesforce統合はSSRF(NPR-32671)に対して脆弱です。
* PreferencesServlet(NPR-33439)でXSSが反映されている。

#### アセット{#assets-6481}

* リスト表示(NPR-33285)での選択の変更に従って、アセットの数は変わりません。

* 親ノード（子フォルダーが1つ表示される）を選択した後で子フォルダーを選択すると、「次へ」ボタンが有効になりません(NPR-33284)。

* タッチUIは、DMS7またはハイブリッドモードが有効な場合(NPR-33175)、リポジトリルートで読み取りアクセス権を持たないユーザーに表示されません（エラーが発生）。

* ダウンロードしたzipファイル(NPR-33150)で、フォルダー名やアセット名に含まれるGB18030文字が空白に変わります。

* 親フォルダー内にあるアセットの名前にドット`.`が含まれるアセットをスマート切り抜きで追加のフォルダーが作成されます(NPR-32755)。

* 遅延読み込みはトリガーされず、通知インボックス(NPR-32749)からタスクを確認するように選択した場合は、100以下のアセットが表示されます。

* coral-info(NPR-32510)の変更により、コレクションを共有するリンクページが破損しました。

* バルクアップロード中にアセットの処理が停止する(CQ-4293916)。

* Experience ManagerのSSRF脆弱性(NPR-33437)。

#### プラットフォーム{#platform-6481}

* `/etc/maps`の下に`sling:match`マップエントリが作成された場合、[!DNL Sling]フィルターは呼び出されません(NPR-33308)。
* すべてのフラッシュエージェントは、ページの非アクティブ化時にトリガされます(NPR-32941)。
* `ScriptProcessor` APIを使用してJavaScriptライブラリを縮小すると、ログファイルにエラーメッセージが表示され、JavaScriptコードが厳密なモードに準拠していないことを示します。 APIには、厳密なモードを有効または無効にするオプションはありません。 (NPR-32746).
* SQLクエリが7時間など長い時間実行されると、AEMは応答を停止します(NPR-33043)。

#### ユーザーインターフェイス {#ui-6481}

* 選択ダイアログを使用してパスを検索または参照する場合、選択ダイアログには、画像のみを表示するのではなく、選択したJCRノードのすべてのコンテンツが表示されます(NPR-32712)。

#### 翻訳プロジェクト {#tranlation-6481}

* 翻訳ジョブの実行時にログに`NullPointerException`エラーが表示されます(NPR-32220)。

#### 統合 {#integrations-6481}

* JSONのクロスサイトスクリプティング(NPR-32745)。

#### コミュニティ{#communities-6481}

* 作成者は、新しいグループを作成した後、[!DNL Internet Explorer] 11の[!UICONTROL コミュニティグループ]セクション(NPR-33202)にリダイレクトされません。
* [!UICONTROL アクティビティストリーム]ページへのアクセス時にエラーが発生します(NPR-33152)。
* [!DNL Communities]グループを編集してサムネール画像を変更しても、グループサムネール画像は更新されません(NPR-32603)。
* ユーザー生成コンテンツ(UGC)の通知と購読のバージョンを作成すると、ソースページの誤ったIDが保存されます(CQ-4289703)。
* クロスサイトスクリプティングの問題(NPR-33212)。

#### ワークフロー {#workflow-6481}

* [!UICONTROL ダイアログ参加者の手順](NPR-32989)を含むワークフローをユーザーが完了すると、ダイアログボックスがポップアップ表示されないコンポーネントがあります。

* 左側のレールの[!UICONTROL タイムライン]オプションの読み込みに予想以上の時間がかかります(NPR-32850)。

#### Forms{#forms-6481}

>[!NOTE]
>
>AEM Cumulative Fix Packには、AEM Formsの修正は含まれていません。 別の Forms アドオンパッケージを使用して配布されます。さらに、JEE上のAEM Formsの修正を含む累積インストーラーがリリースされました。 詳しくは、「[AEM Formsアドオンパッケージのインストール](#install-aem-forms-add-on-package)」および「[AEM FormsJEEインストーラーのインストール](#install-aem-forms-jee-installer)」を参照してください。

* Correspondence Management:ユーザーが[!DNL Word]ドキュメントからコンテンツを貼り付けると、テキストドキュメントフラグメントは書式を保持しません(NPR-33213)。
* アダプティブForms:アダプティブフォームの辞書の文字列に対する新しい行で、`&#xa;`文字が辞書(NPR-33265)に追加されます。
* アダプティブForms:複数の添付ファイルが含まれるアダプティブフォームを保存できません(NPR-33214)。
* アダプティブForms:Instance Managerクラスの`AddInstance`メソッドと`RemoveInstance`メソッドは、遅延読み込みフラグメントの動的な数のインスタンスを[!DNL Internet Explorer 11]に追加しません(NPR-33201)。
* アダプティブForms:[!DNL Sites]ページに埋め込まれたアダプティブフォームで有効にされた解析で、送信および放棄イベントのデータが記録されません(NPR-31359)。
* アダプティブForms:ユーザーが[!DNL Word]ドキュメントの内容をアダプティブフォームに貼り付けて送信すると、送信されたアダプティブフォームにはUnicode文字が含まれます。 また、PDFからPDF/Aへの変換は、Unicode文字(NPR-33348)のため失敗します。
* BackendIntegration:非アクティブな状態が正しくないために更新トークンの期限が切れると、フォームデータモデルの要求は失敗します(NPR-33168)。
* ドキュメントサービス：[!DNL Linux]サーバー(NPR-33515、CQ-4292239)に[!DNL WebLogic]のギブソンjarがないため、Convert PDFサービスでPDFドキュメントをPostScriptに変換できません。
* ドキュメントサービス：ユーザーがテキストファイルをPDFに変換すると、日本語の文字は正しくレンダリングされません(NPR-33239)。
* GuideSOMProviderServlet(NPR-32701)に格納されたXSS。

## 6.4.8.4 {#install}のインストール

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

* AEM 6.4.8.4ではAEM 6.4.8.0が必要です。詳細な手順については、[アップグレードドキュメント](../sites-deploying/upgrade.md)を参照してください。
* MongoDB と複数のインスタンスを含むデプロイメントでは、パッケージマネージャーを使用してオーサーインスタンスの 1 つに AEM 6.4.8.4 をインストールしてください。
* 累積修正パックをインストールする前に、AEMインスタンスのスナップショットまたは新規バックアップが必要です。
* インストールする前にインスタンスを再起動してください。これは、インスタンスがまだ更新モードになっている場合（インスタンスが以前のバージョンから更新されたばかりの場合）にのみ必要ですが、インスタンスが長期間実行されている場合は、一般的に推奨されます。

>[!NOTE]
>
>AEM 6.4.8.4 パッケージを削除またはアンインストールすることはお勧めしません。

### 累積Fix Packのインストール{#install-cumulative-fix-pack}

既存の AEM 6.4.8.0 インスタンスに累積修正パックをインストールするには、次の手順を実行します。

1. [ソフトウェアの配布](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq640/cumulativefixpack/aem-6.4.8-cfp-4.0.zip)リンクをクリックして、パッケージをダウンロードします。

1. [パッケージマネージャー](http://localhost:4502/crx/packmgr/index.jsp)を開き「**[!UICONTROL パッケージをアップロード]**」をクリックしてパッケージをアップロードします。

1. パッケージ名を選択して、「**[!UICONTROL インストール]**」をクリックします。

>[!NOTE]
>
>**6.4.8.4 のインストール中に、パッケージマネージャー UI のダイアログが途中で終了することがあります。**
>
>そのため、エラーログが安定するのを待ってから、インスタンスにアクセスすることをお勧めします。ユーザーは、アップデーターバンドルのアンインストールに関連する特定のログを待ってから、インストールが正常に行われることを確認する必要があります。 通常は、Safari で発生しますが、任意のブラウザーで断続的に発生する可能性があります。

### 自動インストール {#auto-installation}

実行中のインスタンスに AEM 6.4.8.4 を自動的にインストールするには、次の 2 つの方法があります。

A.サーバーの実行中に、パッケージを。.*/crx-quickstart/install*&#x200B;フォルダーに配置します。 パッケージは自動的にインストールされます。

B. Package Managerの[HTTP APIを使用します。](https://docs.adobe.com/content/docs/en/crx/2-3/how_to/package_manager.html)を使用していることを確認します。`cmd=install&recursive=true`を使用していることを確認してください。そうすると、ネストされたパッケージがインストールされます。

>[!NOTE]
>
>AEM 6.4.8.4 では、ブートストラップインストールをサポートしていません。

### インストールの検証 {#validate-install}

1. 製品情報ページ（*/system/console/productinfo*）のインストール済み製品には、更新されたバージョン文字列「Adobe Experience Manager, Version 6.4.8.4」が表示されます。
1. すべての OSGi バンドルは、OSGi コンソール（Web コンソールを使用：/system/console/bundles）で ACTIVE または FRAGMENT です。
1. OSGIバンドルorg.apache.jackrabbit.oak-coreがバージョン1.8.17以降に搭載されています(Webコンソールを使用：/system/console/bundles)。

このリリースのAEM Sitesとアセットでの運用に適した認定プラットフォームを確認するには、[技術要件](../sites-deploying/technical-requirements.md)を参照してください。

>[!NOTE]
>パッケージが正常にインストールされると、**&quot;Content Package AEM-6.4-Service-Pack-8が正常にインストールされたなど、コンテンツパッケージが正常にインストールされたことを示す情報メッセージが表示されます。&quot;**

### Dynamic Mediaビューアの更新(5.10.1) {#update-dynamic-media-viewers}

AEM 6.4.8.4には、新しいバージョンのDynamic Mediaビューア(5.10.1)が含まれています。このビューアを使用すると、画像プリセットページで重複名を確認できます。 Dynamic Mediaのお客様には、次のコマンドを実行して、初期設定のビューアプリセットを最新の状態にするようお勧めします。

`curl -u admin:admin http://localhost:4502/libs/settings/dam/dm/presets/viewer.pushviewerpresets`

新しいビューアプリセットを/confの場所にコピーします。

### AEM Forms アドオンパッケージのインストール {#install-aem-forms-add-on-package}

>[!NOTE]
>
>[!DNL Experience Manager Forms] では、予定されている [!DNL Experience Manager] 累積修正パックリリース日の 1 週間後にアドオンパッケージをリリースします。

>[!NOTE]
>
>AEM Forms を使用していない場合はスキップしてください。AEM Forms の修正は、個別のアドオンパッケージを介して配信されます。

1. AEM Cumulative Fix Packがインストールされていることを確認します。
1. [AEM Formsリリース](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=en#forms-updates)に記載されている、お使いのオペレーティングシステム用の対応するフォームアドオンパッケージをダウンロードします。
1. [AEM formsアドオンパッケージのインストール](https://docs.adobe.com/content/help/en/experience-manager-64/forms/install-aem-forms/osgi-installation/installing-configuring-aem-forms-osgi.html#install-aem-forms-add-on-package)の説明に従って、formsアドオンパッケージをインストールします。

### AEM Forms JEE インストーラーのインストール {#install-aem-forms-jee-installer}

>[!NOTE]
>
>JEE で AEM Forms を使用していない場合はスキップします。AEM Forms JEE の修正は別のインストーラーを介して配布されます。

AEM Forms JEE の累積インストーラーのインストールとデプロイメント後の設定について詳しくは、[AEM Forms JEE パッチインストーラー ](jee-patch-installer-64.md) を参照してください。

>[!NOTE]
>
>JEE上のExperience ManagerFormsの累積インストーラーをインストールした後、最新のFormsアドオンパッケージをインストールし、`crx-repository\install`フォルダーからFormsアドオンパッケージを削除して、サーバーを再起動します。

### Uber Jar {#uber-jar}

AEM 6.4.8.4用のUber Jarは、[Maven Centralリポジトリ](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.4.8.4/)で入手できます。

Maven プロジェクトで Uber Jar を使用するには、[Uber Jar の使用方法](../sites-developing/ht-projects-maven.md)を参照して、プロジェクト POM に以下の依存関係を追加します。

```shell
<dependency>
      <groupId>com.adobe.aem</groupId>
      <artifactId>uber-jar</artifactId>
      <version>6.4.8.4</version>
      <scope>provided</scope>  
</dependency>
```

>[!NOTE]
>
>UberJarおよびその他の関連アーティファクトは、AdobeのパブリックMavenリポジトリ(repo.adobe.com)ではなく、Maven Centralリポジトリで使用できます。 メインのUberJarファイルの名前が`uber-jar-<version>.jar`に変更されます。 その結果、`dependency`タグの値として`apis`を持つ`classifier`はありません。

## 廃止される機能および削除された機能 {#removed-deprecated-features}

このセクションでは、AEM 6.4 で廃止される機能および削除された機能について説明します。

| 領域 | 機能 | 代替手段 | バージョン |
|---|---|---|---|
| Assets | サブアセットのタグアクションの管理 | 代替機能はありません | AEM 6.4.2.0 |
| Assets と Adobe Creative Cloud の統合 | [AEM／Creative Cloud フォルダー共有](https://docs.adobe.com/content/help/ja/experience-manager-64/assets/administer/aem-cc-folder-sharing-best-practices.html)は、クリエイティブユーザーに AEM のアセットへのアクセスを提供する方法として、AEM 6.2 で導入されました。Creative Cloud アプリケーションでリリースされた新しい機能である Adobe Asset Link では、ユーザーエクスペリエンスが大幅に向上し、Photoshop、InDesign、Illustrator 内から AEM のアセットへの直接アクセスが強化されています。アドビは、このフォルダー共有機能をさらに強化する予定はありません。この機能はAEMに含まれていますが、お客様には交換の使用を強くお勧めします。 | Adobeアセットリンクまたはデスクトップアプリ 詳細については、[AEM Creative Cloud の統合](/help/assets/aem-cc-integration-best-practices.md)記事を参照してください。 | AEM 6.4.4.0 |

## 既知の問題 {#known-issues}

* [!DNL Experience Manager] 6.4から[!DNL Experience Manager] 6.5にアップグレードした場合、一部のバンドルのステータスが`Active`と表示されない場合があります。 最新の[!DNL Experience Manager] 6.5 Service Packをインストールして問題を解決します。

AEM 6.4.8.0 Service Packの既知の問題については、「[AEM 6.4.8.0 Service Packリリースノート](sp-release-notes.md)」を参照してください。

## OSGi バンドルとコンテンツパッケージが含まれています {#osgi-bundles-and-content-packages-included}

次のテキストドキュメントリストは、AEM 6.4.8.4に含まれるOSGiバンドルとコンテンツパッケージを示します。

AEM 6.4.8.4 に含まれている OSGi バンドルの一覧

[ファイルを入手](assets/6.4.8.4_osgi_bundles.txt)

AEM 6.4.8.4 に含まれているコンテンツパッケージの一覧

[ファイルを入手](assets/6.4.8.4_content_packages.txt)

## 参考リソース {#helpful-resources}

* [AEM 6.4 リリースノート](../release-notes/release-notes.md)
* [AEM 製品ページ](https://www.adobe.com/solutions/web-experience-management.html)
* [AEM 6.4 ドキュメント](https://experienceleague.adobe.com/docs/experience-manager-64.html?lang=ja)
* [Adobe Priority 製品アップデート](https://www.adobe.com/subscription/priority-product-update.html)のサブスクリプションを購入する

## 制限付きサイト {#restricted-sites-new}

以下のサイトは既存ユーザーのみが参照できます。アクセス権が必要な既存ユーザーの方は、アドビのアカウントマネージャーまでお問い合わせください。

* [licensing.adobe.com からの製品ダウンロード](https://licensing.adobe.com/)
* [カスタマーサポートに連絡](https://docs.adobe.com/content/help/en/customer-one/using/home.html)
