---
title: AEM 6.4 累積修正パックのリリースノート
description: Adobe Experience Manager 6.4 Cumulative Fix Packs 固有のリリースノート。
contentOwner: AK
mini-toc-levels: 1
exl-id: a63e77a3-da48-4072-bc75-c4c41a2f62a3
source-git-commit: 1d5d2ef3840a40df7c3b223c7b5835e41553e9f1
workflow-type: tm+mt
source-wordcount: '4693'
ht-degree: 16%

---

# AEM 6.4 累積修正パックのリリースノート {#aem-cumulative-fix-pack-release-notes}

## リリース情報 {#release-information}

<!-- TBD: Update the SD URL. -->

| 製品 | **Adobe Experience Manager（AEM）6.4** |
|---|---|
| バージョン | 6.4.8.4 |
| タイプ | 累積修正パック     |
| 日付 | 2021 年 2 月 25 日（PT） |
| 前提条件 | [AEM 6.4 サービスパック 8（6.4.8.0）](sp-release-notes.md) |
| ダウンロード URL | [ソフトウェア配布](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq640/cumulativefixpack/aem-6.4.8-cfp-4.0.zip) |

## AEM 6.4.8.4 に含まれる機能 {#what-s-included-in-aem}

AEM累積修正パック 6.4.8.4 は、2020 年 3 月のAEM 6.4 Service Pack 8(6.4.8.0) の一般リリース以降に対応された、内部およびお客様向けの修正を含む重要な更新です。

AEM 6.4.8.4 は、AEM 6.4 Service Pack 8 に依存する Cumulative Fix Pack(CFP) です。 AEM 6.4 Service Pack 8 のインストール後に CFP をインストールします。

に導入された主な機能および機能強化 [!DNL Adobe Experience Manager] 6.4.8.4 は次のとおりです。

* を有効または無効にする機能 [!DNL Experience Manager Forms] PDFG 変換の実行時にレジストリが変更されます。

* フォームデータモデルの SOAP ベース Web サービス用の X-509 証明書ベースの認証。

* 組み込み型のリポジトリ（Apache Jackrabbit Oak）をバージョン 1.8.24 に更新しました。

CFP と他のタイプのリリースについて詳しくは、 [AEM Update リリースの提供に関する定義](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-release-vehicle-definitions.html)

Adobe Experience Manager 6.4.8.4 では、次の問題が修正されています。

### Sites {#sites-6484}

* Experience Managerサービスパック 6.4.8.2 のインストール後、ユーザーはコンテンツフラグメントモデルを編集できず、次のエラーが発生します。

   `Uncaught TypeError: Cannot read property 'debounce' of undefined` (NPR-35312)
* ユーザーがログアウトボタンをクリックしても、そのユーザーはパッケージマネージャーからログアウトされません。 (NPR-35161)
* Experience Manager6.4.x からExperience Manager6.4.8.3 にアップグレードした後、「公開を管理」を使用してページを公開できない。 （CQ-4312511）
* ブループリントの子ページを元の場所に戻すと、cq:liveSyncConfig 設定はライブコピーの子ページから削除されません。 (NPR-35900)
* ライブコピーを含むブループリントを前後に移動すると、最初の移動のみが機能し、失敗してエラーメッセージは表示されません。 (NPR-35899)


### [!DNL Assets] {#assets-6484}

* `IndexWriter.merge` 原因 `OutOfMemoryError` スマートタグ機能が大きく作成する際にエラーが発生しました `/oak:index/lucene` および `/oak:index/ntBaseLucene` インデックス (NPR-35650)。
* ユーザーがで編集した後、アセットをチェックインできない [!DNL Adobe InDesign] 権限の欠如に関するエラーを受け取る。(NPR-35340)
* 名前の競合を解決した後に既存のアセットの新しいバージョンが作成されると、元のアセットのメタデータが上書きされる (NPR-35939)。
* 自動生成されたプライベートフォルダーのグループは、フォルダーの削除時や [!UICONTROL プライベートフォルダーの制限を削除] オプションセット (NPR-35625)。

#### [!DNL Dynamic Media] {#dynamic-media}

* 断続的な ImageServer エラーが原因で、403 応答が発生し、その結果、 [!DNL Experience Manager]. （CQ-4308565）

### 統合 {#integrations-6484}

* Experience Manager6.4.8.3 にアップグレードした後にページのプロパティを開くと、JavaScript エラーがコンソールに表示され始める (NPR-35649)。

### Forms {#forms-6484}

>[!NOTE]
>
>[!DNL Experience Manager Forms] では、予定されている [!DNL Experience Manager] 累積修正パックリリース日の 1 週間後にアドオンパッケージをリリースします。

**Correspondence Management**

* レターを編集する際、条件を持つモジュールの読み込みに時間がかかる (NPR-35326)。

* レターを編集する際に、コンテンツとデータの連結がユーザーインターフェイスに表示されません (CQ-4312905)。

**ドキュメントサービス**

* アップグレード後にPDFを組み立てることができません [!DNL JAVA] から [!DNL JDK1.8.0_261] (NPR-35761、NPR-35848)。

**Foundation JEE**

* タスク通知を [!DNL Forms] ワークフローに保存できない場合は、保存できません (CQ-4315055)。

**AEM Forms-6.4.0-0027 で修正された問題**

* （JEE のみ）Apache Log4j2 に対して報告された重大なセキュリティ脆弱性 (CVE-2021-44228および CVE-2021-45046)。

セキュリティ更新について詳しくは、 [Experience Managerセキュリティ速報ページ](https://helpx.adobe.com/security/products/experience-manager.html).

## 以前の累積修正パックに含まれていたホットフィックスと機能パック {#hotfixes-and-feature-packs-included-in-previous-cumulative-fix-packs}

### Adobe Experience Manager 6.4.8.3 {#experience-manager-6483}

AEM累積修正パック 6.4.8.3 は、2020 年 3 月のAEM 6.4 Service Pack 8(6.4.8.0) の一般リリース以降に対応された、内部およびお客様向けの修正を含む重要な更新です。

AEM 6.4.8.3 は、AEM 6.4 Service Pack 8 に依存する Cumulative Fix Pack (CFP) です。 AEM 6.4 Service Pack 8 のインストール後に CFP をインストールします。

AEM 6.4.8.3 では、組み込みリポジトリ (Apache Jackrabbit Oak) がバージョン 1.8.23 に更新されています。

CFP と他のタイプのリリースについて詳しくは、 [AEM Update リリースの提供に関する定義](https://docs.adobe.com/content/help/en/experience-manager-65/deploying/deploying/update-release-vehicle-definitions.html)

Adobe Experience Manager 6.4.8.3 では、次の問題が修正されています。

#### サイト {#sites-6483}

* コンテンツフラグメントのバリエーションのテキストを更新すると、マスターコンテンツフラグメントのコンテンツが、バリエーションではなく更新される (NPR-35080)。

* コンポーネントの String type ラベルプロパティに数値を設定し、そのコンポーネントを削除し、元に戻すオプションを使用すると、label プロパティのタイプが自動的に String から Long に変わります (NPR-34738)。

* ファイルのアップロードコンポーネントをマルチフィールドに追加すると、画像パスは、マルチフィールドノードではなく、コンポーネントノードに保存されます (NPR-34423)。

* ページの移動ウィザードで、宛先が選択されていない場合でも、次のボタンが有効なままになる (NPR-34460)。

* 親コンポーネントに `cq:isContainer` プロパティを継承した場合、継承されたコンポーネントにプロパティが自動的に含まれるわけではありません (CQ-4308409)。

* を使用して CSS 縮小を使用する場合 `calc()` 関数、 `+` 記号が削除される (NPR-34991)。

* AEMインスタンスを起動すると、 `com.adobe.granite.maintenance.impl.MaintenanceTaskManagerImpl` および `com.adobe.granite.maintenance.impl.TaskScheduler` コンポーネントがに表示されない `Active` 状態 (NPR-34952)。

#### [!DNL Assets] {#assets-6483}

* 既存のアセットのバージョンを作成する際、メタデータプロファイルがフォルダーに適用されている場合、ユーザーがメタデータに対する更新を保持しない (NPR-34833)。
* を使用する場合 [!DNL Adobe Asset Link] と [!DNL Adobe InDesign]の場合、検索結果にはフォルダーやコレクションは含まれず、アセットのみが含まれる。(NPR-34700)
* フォルダー上のアセットをドラッグして移動すると、ユーザーインターフェイスには次のオプションも表示されます。 [!UICONTROL Lightbox にドロップ] および [!UICONTROL コレクションにドロップ]. 移動操作がキャンセルされても、ユーザーインターフェイスには後の 2 つのオプションが引き続き表示される (NPR-34525)。
* 「公開を管理」インターフェイスを開くと、「公開」オプションは使用できず、非公開オプションを選択すると、範囲ページが空白になります (CQ-4302509)。

##### [!DNL Dynamic Media] {#dynamic-media-6483}

* 画像プリセット設定で、オプション [!UICONTROL JPGの色度ダウンサンプリングを有効にする] が [!DNL Experience Manager]の場合、変更は [!DNL Dynamic Media] (NPR-34284)。
* 内 [!UICONTROL ビューアプリセットエディター]（編集時） [!UICONTROL PanoramicImage/PanoramicImage_VR] プリセット、 `PanoramicView` コンポーネント、 `PANORAMICVIEW_AUTOROTATE` 修飾子ラベルは使用できません (CQ-4302043)。
* 次のビデオを非公開にする： [!DNL Experience Manager] では、設定済みのDynamic Media Classicでアダプティブビデオセットを非公開にしません。 (CQ-4304405).

#### Platform {#platform-6483}

* この `emitUseStrict` フラグがGoogle Closure Compiler(GCC) プロセッサ関数に追加されます。 `com.adobe.granite.ui.clientlibs.impl.HtmlLibraryManagerImpl`. このフラグは、 `use strict` 命令 (NPR-34830)。
* A `NullPointerException` は、日次または週次のメンテナンスタスクの開始時に返されます。(NPR-34702)
* この [!DNL Apache Sling Health Check] ツールは非推奨です。 代わりに、 [パターン検出](https://experienceleague.adobe.com/docs/experience-manager-64/deploying/upgrading/pattern-detector.html?lang=ja) コンテンツ違反を検出する (NPR-33929)。

#### 統合 {#integrations-6483}

* この [!UICONTROL 作成] ボタンが [!UICONTROL オーディエンス] フォルダーから [!UICONTROL オーディエンス] ページ (NPR-35152) に表示される。

#### ユーザーインターフェイス {#ui-6483}

* この [!UICONTROL フィルター] の検索パネル [!UICONTROL オムニサーチ] また、検索が実行された場所以外の場所からの結果も返される (NPR-34877)。
* を閉じたとき [!UICONTROL フィルター] パネル [!UICONTROL オムニサーチ] ユーザーインターフェイスの場合、左パネルは [!UICONTROL コンテンツ] 再び開くのを防ぐ選択 [!UICONTROL フィルター] パネル (NPR-34483)。
* A `NullPointerException` が、ページプロパティへのアクセス時に返される。(NPR-34509)

#### Communities {#communities-6483}

<!-- Following fixes of 6483 are documented on Nov 11 20202 by Vishabh. 
-->

* 製品内の不公平な用語のインスタンスは、すべて、受け入れられた同等のものに置き換えられます (NPR-34506)。

#### コマース {#commerce-6483}

* 1 つのコレクションに 15 個を超える製品が存在する場合、そのコレクションには最初の 15 個の製品のみが表示されます (NPR-34494)。

#### Forms {#forms-6483}

>[!NOTE]
>
>[!DNL Experience Manager Forms] では、予定されている [!DNL Experience Manager] 累積修正パックリリース日の 1 週間後にアドオンパッケージをリリースします。

>[!NOTE]
>
>[!DNL Experience Manager] 累積修正パックには、次の修正が含まれていません： [!DNL Experience Manager Forms]. これらは、別の [!DNL Forms] アドオンパッケージ。 さらに、の修正を含む累積インストーラーがリリースされました。 [!DNL Experience Manager Forms] JEE 上で 詳しくは、 [AEM Formsアドオンパッケージのインストール](#install-aem-forms-add-on-package) および [AEM Forms JEE インストーラーのインストール](#install-aem-forms-jee-installer).

**アダプティブフォーム**

* アダプティブフォームをクラシック UI で適用した後に編集できない [!DNL Experience Manager] 累積修正パック (NPR-35127)。

* キャッシュの無効化により、フラグメントのアダプティブフォームへの読み込みに時間がかかる。(NPR-34655)

* アクセシビリティ：アダプティブフォームのスクリーンリーダーに対して、タブナビゲーションが適切に機能しない (NPR-34550)。

**Correspondence Management**

* ES3 からアセットを移行する場合、アセットには編集不可の 2 つのデフォルト条件が含まれます (NPR-34971)。

**Foundation JEE**

* 移行 [!DNL AEM Forms] FlashからHTML(CQ-4304075) のユーザー。

### Adobe Experience Manager 6.4.8.2 {#experience-manager-6482}

AEM累積修正パック 6.4.8.2 は、2020 年 3 月のAEM 6.4 Service Pack 8(6.4.8.0) の一般リリース以降に対応された、内部およびお客様向けの修正を含む重要な更新です。

AEM 6.4.8.2 は、AEM 6.4 Service Pack 8 に依存する Cumulative Fix Pack (CFP) です。 AEM 6.4 Service Pack 8 のインストール後に CFP をインストールします。

AEM 6.4.8.2 では、組み込みリポジトリ (Apache Jackrabbit Oak) がバージョン 1.8.22 に更新されます。

CFP と他のタイプのリリースについて詳しくは、 [AEM Update リリースの提供に関する定義](https://docs.adobe.com/content/help/en/experience-manager-65/deploying/deploying/update-release-vehicle-definitions.html)

Adobe Experience Manager 6.4.8.2 では、次の問題が修正されています。

#### サイト {#sites-6482}

* この `RolloutConfigManagerFactoryImpl` はロールアウト設定を読み込めません。見つからない設定の読み込みは試みません。 キャッシュされた設定を返します (NPR-34091)。
* テキストコアコンポーネントで、ソースHTML編集オプションを使用した後、 `em` タグが削除される (NPR-34080)。
* Experience Manager6.2 からExperience Manager6.5 にアップグレードすると、静的テンプレートの Parsys コンポーネントが正しく表示されません。 Parsys コンポーネントの高さが 0 に設定され、その中のコンポーネントが表示されない (NPR-34044)。
* テンプレートエディター内の許可されたコンポーネントに対して、ラベル情報が表示されない (NPR-33908)。

   ![レイアウトコンテナにラベルがありません](assets/33908_missing_labels.png)

* ユーザーが、ネストされた 4 番目のレベルのコンポーネントの後で、parsys にコンポーネントを追加または編集できない。(NPR-33873)
* 編集可能テンプレートの初期コンテンツが変更され、その後テンプレートが公開された場合、ページが公開されていなくても、このテンプレートで作成された新しいページには、テンプレートの公開日が表示されます (NPR-33822)。
* この `cq:acLinks` および `cq:acUUID` プロパティ [!DNL Adobe Campaign] のコピーが、コピーおよび貼り付け操作中に削除される (NPR-33793)。
* 内 [!UICONTROL ライブ使用状況] 「 」タブに設定すると、49 個の結果のみが表示されます。 コンポーネントのすべての使用状況が表示されるわけではありません (NPR-33710)。
* を含む Web ページ `/` オーサリング中に URL 内の文字が応答しなくなる。 オーサリング中にコンポーネントが追加されると、CPU 使用率が増加し、ブラウザーが応答を停止する (NPR-33625)。
* のインライン編集モードで [!DNL RTE]に設定されている場合、画像をドラッグしても、テキストコンポーネントでは機能しない (NPR-33579)。
* ブループリントページ内に、ページ名と同じ名前のコンポーネントを作成できます。 ロールアウト時に、サフィックスを付けて名前が変更されます `_msm_moved`. ただし、コンポーネントは [!UICONTROL 段落システム] (NPR-33534)。
* 次の場合に、ローンチの昇格でページが公開されません [!UICONTROL サブページを含める] プロパティが最初のコンテンツルートでチェックされない。(NPR-33533)
* へのリダイレクト [!DNL Experience Manager] アンカー付きのページは、オーサーインスタンス上で、 `PageRedirectServlets` は、URL フラグメントまたはアンカーの後にクエリ文字列を配置する (NPR-34287)。
* `PageRedirectServlet` 追加 `.html` Sling マッピング後にリンクエラーが発生する (NPR-34271)。
* 一時停止できる [!DNL Live Copy] ページの継承とは、エディターモードで見たように、で壊れています。 ただし、ページプロパティでは、継承を表すアイコンが誤って、継承が存在し、壊れていないことを示す (NPR-34096)。
* テンプレートを編集ページでの許可されたコンポーネントの表示に関する問題 (CQ-4297295)。
* Chrome および Firefox をアップグレードした後、ポップアップメニューが期待どおりに動作しません。 ページのプロパティを読み込むと、データが含まれている場合、パネルは表示されません (CQ-4292995)。
* での複数のクロスサイトスクリプティングインスタンス [!DNL Experience Manager Sites] コンポーネント (NPR-33926)。
* クライアントに情報を送信する際に、ユーザ入力が様々なコンポーネントに対して適切にエンコードされない (NPR-33696)。
* 次で終わる URL `childrenlist.html` は、404 応答ではなくHTMLページを表示します。 このような URL は、クロスサイトスクリプティングに対して脆弱です (NPR-33441)。

#### Assets {#assets-6482}

* アップロードされたPDFファイルのテキスト抽出が機能せず、PDFファイル内の一部の単語に対する全文検索がそのPDFファイルを取得できない。(NPR-34165)

   >[!NOTE]
   >この修正を機能させるには、Service Pack 6.4.8.2 をインストールした後で、Adobe Experience Managerインスタンスを再起動します。

* 名前に特殊文字が含まれるアセットの検索候補で、特殊文字の前にバックスラッシュが追加される。(NPR-33833)

* スマートコレクションとして保存されたカスタムフィルターがアセットに正しく適用されないので、検索結果が正確でない (NPR-33725)。

* 並べ替えられたフォルダー内のアセットのタイムラインは、そのアセットが移動されたことを示している (NPR-33580)。

* からアセットを一括して非公開にする [!DNL Brand Portal] リード `Request-URI Too Long` エラー (NPR-34158)。

* 列表示で、ユーザーが [!UICONTROL フィルター] オプションを選択した後（アセットの選択を解除）、別のアセットのセットを選択して移動した後、以前に選択したアセットも新しい場所に移動される (NPR-34018)。

* ページに収まるアセットが多数ある場合でも、リスト表示にスクロールバーが表示されない。(NPR-34156)

* この [!UICONTROL 公開を管理] アセットのページが壊れ、そのオプションが機能しない (CQ-4302509)。

**Dynamic Media**

* 画像プロファイルが複数の縦横比（例：11）を持つフォルダーに追加されると、スマート切り抜き機能がエラーで失敗する (NPR-34083)。

* 内の画像プリセットの変更 [!UICONTROL Adobe Experience Manager] Dynamic Media Classicに同期しない (NPR-34284、CQ-4299713)。

* この [!UICONTROL PANORAMICVIEW_AUTOROTATE] 修飾子ラベルが見つかりません [!UICONTROL 動作] タブ [!UICONTROL ビューアプリセットエディター] ページ (CQ-4302043) に表示されます。

#### Platform {#platform-6482}

* のデフォルト値 **[!UICONTROL 接続タイムアウト]** および **[!UICONTROL ソケットタイムアウト]** 「デフォルトエージェント（パブリッシュ） 」設定が指定されていない (NPR-33708)。
* メンテナンスタスクスケジューラーが、設定された回数を超えてメンテナンスタスクを開始および停止する (NPR-33520)。
* アップグレードされたExperience Managerインスタンスの診断ツールを使用してログをダウンロードできない。(NPR-34419)

#### 統合 {#integrations-6482}

* の値 `library_path` 生成時には考慮されません [!DNL Adobe Launch] 移行元のライブラリのライブラリ URL [!DNL Adobe Dynamic Tag Management]. また、移行されたライブラリは、 [!DNL Adobe Launch] ライブラリ。 (NPR-34238).
* クラウドサービスから継承されたプロパティは、ページプロパティの更新時に保持されません (NPR-33865)。

#### ユーザーインターフェイス {#ui-6482}

* 検索ページで選択されたアセットの数が正しく表示されない (NPR-33540)。

#### コミュニティ {#communities-6482}

* 管理コンソールを通じて追加されたコミュニティグループの既存のユーザーは、コミュニティグループコンソールで変更されると、ユーザーリストから削除されます (NPR-34312)。

#### Forms {#forms-6482}

>[!NOTE]
>
>[!DNL Experience Manager] 累積修正パックには、次の修正が含まれていません： [!DNL Experience Manager Forms]. これらは、別の [!DNL Forms] アドオンパッケージ。 さらに、の修正を含む累積インストーラーがリリースされました。 [!DNL Experience Manager Forms] JEE 上で 詳しくは、 [AEM Formsアドオンパッケージのインストール](#install-aem-forms-add-on-package) および [AEM Forms JEE インストーラーのインストール](#install-aem-forms-jee-installer).

**アダプティブフォーム**

* 見つからないアダプティブフォームフラグメントがある場合、そのアダプティブフォームがレンダリングに失敗する (NPR-34303)。

* アダプティブフォームフィールドのヘルプコンテンツの説明に段落HTMLタグが表示される (NPR-34117)。

* Formsコンテナを [!DNL Experience Manager Sites] ページに表示される場合、ページに次のエラーメッセージが表示され、新しいコンポーネントの追加は許可されない (NPR-33858)。

   `DevTools failed to load SourceMap: Could not load content for <Link>. HTTP error: status code 404, net::ERR_HTTP_RESPONSE_CODE_FAILURE`

* を選択し、 **[!UICONTROL サーバーでの再検証]** プロパティを追加して複数の添付ファイルをアップロードした場合に、アダプティブフォームが送信に失敗する (NPR-33701)。

* を選択し、 **[!UICONTROL ページ言語を使用]** および **[!UICONTROL フォームはページの幅全体をカバーします]** オプション [!DNL Experience Manager Forms] 上のコンポーネント [!DNL Experience Manager Sites] ページに含まれている場合、ページが翻訳に失敗する (NPR-33641)。

* Analytics が有効なアダプティブフォームを [!DNL Experience Manager Sites] ページの場合、analytics が正しく機能しない (NPR-31359)。

* 依存関係を削除しました： [!DNL Lodash] および [!DNL backbone] ライブラリ (NPR-33458)。

* この **[!UICONTROL REST エンドポイントに送信]** アダプティブフォームの送信アクションが機能しない (NPR-34513)。

* アクセシビリティ：必須フィールドの添付ファイルをアップロードせずにアダプティブフォームを送信しようとしても、フォーカスが添付フィールドに自動的に移動しない (NPR-34511)。

* ユーザー入力が [!DNL Forms] クライアントに情報を送信する際のコンポーネント (NPR-33611)。

**ワークフロー**

* [!DNL Experience Manager] ワークフローのパージ操作が失敗し、次のエラーメッセージが表示される (NPR-33576)。

   `java.lang.UnsupportedOperationException: The query read more than 500000 nodes in memory`

* インストール時 [!DNL Experience Manager] 6.4.8.1、 [!UICONTROL タスク] 項目のリストはリンクとして表示されません。 のテキスト [!UICONTROL タスク] 項目にはHTMLタグが含まれる (NPR-34318)。

**BackendIntegration**

* AWSでホストされているフォームデータモデルを設定できません [!DNL Experience Manager Forms Linux] 環境 (NPR-33617)。

**デザイナー**

* 条件 [!DNL Acrobat DC] が [!DNL Experience Manager] Formsサーバ **[!UICONTROL フォームを配布]** オプションは、 [!DNL Experience Manager Designer] バージョン 6.x(NPR-34325)。

**Document Security**

* インストール後に、HSM ベースの証明書を使用して署名操作をPDFファイルで実行できません [!DNL Experience Manager] 6.4.8.0(NPR-34309)。

**アップグレード**

* をアップグレードする際に、 [!DNL JBoss] のバージョンを 7.0.9() に変更しました。 [!DNL Experience Manager Forms] Document Security を [!DNL Linux] 環境に問題がある場合、エラーが発生します (CQ-4300546)。

セキュリティ更新について詳しくは、 [Experience Managerセキュリティ速報ページ](https://helpx.adobe.com/security/products/experience-manager.html).

### Adobe Experience Manager 6.4.8.1 {#experience-manager-6481}

AEM累積修正パック 6.4.8.1 は、2020 年 3 月のAEM 6.4 Service Pack 8(6.4.8.0) の一般リリース以降に対応された、内部およびお客様向けの修正を含む重要な更新です。

AEM 累積修正パック 6.4.8.1 は、AEM 6.4 サービスパック 8 に依存しています。そのため、AEM 6.4 Service Pack 8 をインストールした後に、AEM Cumulative Fix Pack 6.4.8.1 パッケージをインストールする必要があります。

AEM 6.4.8.1 の主な特徴は次のとおりです。

* 匿名でCRXDE Liteにアクセスすると、セキュリティが強化されます。 代わりに、ユーザーはログイン画面に移動します。 詳しくは、 [開発，CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md).
* Adobe Experience Managerとのパッケージ共有の統合を削除しました。
* 組み込み型のリポジトリ（Apache Jackrabbit Oak）をバージョン 1.8.21 に更新しました。

CFP と他のタイプのリリースについて詳しくは、 [AEM Update リリースの提供に関する定義](https://docs.adobe.com/content/help/en/experience-manager-65/deploying/deploying/update-release-vehicle-definitions.html)

Adobe Experience Manager 6.4.8.1 では、次の問題が修正されました。

#### サイト {#sites-6481}

* 匿名ユーザーは、CRX DE Lite の機能にアクセスできます (NPR-33522)。
* ライブコピー内のローカルコンポーネントの名前がブループリント内のコンポーネントの名前と同じで、コンポーネントがブループリントからロールアウトされる場合、ローカルコンポーネントの名前に_msm_moved という用語は追加されません (NPR-33207)。
* 元の要求に追加されたパラメーターは、リダイレクト URL に含まれません。(NPR-33174)
* Coral.Select オプションが emptyOption=true に設定された場合、または値が&quot;&quot;のデフォルトの項目が含まれている場合、dropdownshowhide.js ファイルで次のエラーが発生します。キャッチできない TypeError :component.getValue が関数ではありません (NPR-33163)。
* コンポーネントが別のコンポーネントを data-sly-resource として含む場合、親コンテナコンポーネントのプレースホルダーが内部コンポーネントのプレースホルダーに置き換えられます (NPR-33119)。
* スキーマ上のコンテンツフラグメントのベースにして、そのフラグメントに必須のテキスト領域またはパスフィールドが含まれている場合、コンテンツフラグメントの保存に失敗する (NPR-33007)
* 標準搭載のエクスペリエンスフラグメントコンポーネントを使用してカスタムコンポーネントを作成し、AEM Sitesページで使用すると、AEMにカスタムコンポーネントの参照（使用状況）が表示されない。(NPR-32852)
* AEM Sitesページが、複数のライブコピーを含む大きなコンテンツセットに含まれている場合、ページバージョン履歴プレビューの読み込みに失敗する (NPR-32772)。
* ローンチを昇格すると、ローンチに追加されるすべてのコンポーネントに「cq:LiveRelationship」mixin が追加されます。 「 — ソースページのライブデータを継承 — 」オプションを選択した場合と選択しない場合とを問わず、すべてのローンチに影響を与えます。(NPR-32664)
* ページネーションが開始すると、エクスペリエンスフラグメントピッカーはすべての項目を読み込まない (NPR-32605)。
* AEM Sitesページのローンチを作成できません。 ローンチの作成でエラーが発生する (NPR-32544)。
* 「公開を管理」で、アクティベーションワークフローのリクエストに参照されているアセットが含まれない。(NPR-32463)
* Dispatcher ヘルスチェックが表示されます `Invalid cookie header` ログファイルの警告メッセージ (NPR-33630)。
* Salesforce 統合が SSRF(NPR-32671) に対して脆弱である。
* PreferencesServlet に XSS が反映される (NPR-33439)。

#### Assets {#assets-6481}

* リスト表示での選択内容の変更に従って、アセットの数は変化しない (NPR-33285)。

* 親ノード（単一の子フォルダーが表示されている）を選択した後で子フォルダーを選択した場合、次へボタンが有効にならない (NPR-33284)。

* DMS7 またはハイブリッドモードが有効な場合、リポジトリルートでの読み取りアクセス権を持たないユーザーに対して、タッチ UI が（エラーで）レンダリングに失敗する (NPR-33175)。

* ダウンロードした zip ファイルで、フォルダー名とアセット名に使用されているGB18030文字が空白に変わる (NPR-33150)。

* 親フォルダー内のアセットを、ドット付きでスマート切り抜きで追加フォルダーが作成されます `.` 文字を含む。

* 遅延読み込みがトリガーされず、通知インボックスからタスクを確認するために選択時に 100 個以下のアセットが表示される。(NPR-32749)

* coral-info の変更により、コレクションを共有するリンクページが壊れる (NPR-32510)。

* バルクアップロード中のアセット処理が停止する (CQ-4293916)。

* Experience Managerの SSRF 脆弱性 (NPR-33437)。

#### Platform {#platform-6481}

* この [!DNL Sling] フィルターが呼び出されない場合、 `sling:match` マップエントリは、 `/etc/maps` (NPR-33308)。
* ページを非アクティブ化すると、すべてのフラッシュエージェントがトリガーされる (NPR-32941)。
* を使用する場合、 `ScriptProcessor` JavaScript ライブラリを縮小する API。ログファイルに、JavaScript コードが厳密モードに準拠していないことを示すエラーメッセージが表示されます。 API には、厳密モードを有効または無効にするオプションは用意されていません。 (NPR-32746).
* SQL クエリが長時間（例えば 7 時間）実行されると、AEMは応答を停止する (NPR-33043)。

#### ユーザーインターフェイス {#ui-6481}

* 選択ダイアログを使用してパスを検索または参照すると、選択ダイアログに画像のみが表示されるのではなく、選択した JCR ノードのすべてのコンテンツが表示されます (NPR-32712)。

#### 翻訳プロジェクト {#tranlation-6481}

* A `NullPointerException` 翻訳ジョブの実行時にログにエラーが表示される (NPR-32220)。

#### 統合 {#integrations-6481}

* JSON のクロスサイトスクリプティング (NPR-32745)。

#### コミュニティ {#communities-6481}

* 作成者は、新しいグループを作成した後、 [!UICONTROL コミュニティグループ] のセクション [!DNL Internet Explorer] 11(NPR-33202)。
* 次の項目にアクセスするとエラーが発生します： [!UICONTROL アクティビティストリーム] ページ (NPR-33152) に表示される。
* の編集 [!DNL Communities] グループ化し、サムネール画像を変更しても、グループのサムネール画像は更新されない (NPR-32603)。
* ユーザー生成コンテンツ (UGC) の通知および購読のバージョンを作成する際に、ソースページの誤った ID が保存されます (CQ-4289703)。
* クロスサイトスクリプティングの問題 (NPR-33212)。

#### ワークフロー {#workflow-6481}

* 一部のコンポーネントは、 [!UICONTROL ダイアログ参加者ステップ] (NPR-32989)。

* この [!UICONTROL タイムライン] オプションの読み込みに予想以上の時間がかかる (NPR-32850)。

#### Forms {#forms-6481}

>[!NOTE]
>
>AEM Cumulative Fix Pack にはAEM Formsの修正が含まれていません。 別の Forms アドオンパッケージを使用して配布されます。さらに、JEE 上のAEM Formsの修正を含む累積インストーラーがリリースされました。 詳しくは、 [AEM Formsアドオンパッケージのインストール](#install-aem-forms-add-on-package) および [AEM Forms JEE インストーラーのインストール](#install-aem-forms-jee-installer).

* Correspondence Management:ユーザーが [!DNL Word] ドキュメントに書式を設定する場合、テキストドキュメントフラグメントが書式を保持しない (NPR-33213)。
* アダプティブForms:アダプティブフォームディクショナリ内の文字列に新しい行を追加すると、 `&#xa;` 文字を辞書に追加する (NPR-33265)。
* アダプティブForms:ユーザーが複数の添付ファイルを含むアダプティブフォームを保存できない。(NPR-33214)
* アダプティブForms: `AddInstance` および `RemoveInstance` Instance Manager クラスのメソッドは、遅延読み込みフラグメントの動的な数のインスタンスを [!DNL Internet Explorer 11] (NPR-33201)。
* アダプティブForms:Analytics は、 [!DNL Sites] ページは、送信および放棄イベントのデータを記録しない。(NPR-31359)
* アダプティブForms:ユーザーが [!DNL Word] ドキュメントをアダプティブフォームに送信すると、送信後のアダプティブフォームに unicode 文字が含まれます。 また、PDF/A へのPDFは、Unicode 文字が原因で失敗する (NPR-33348)。
* BackendIntegration:非アクティブな状態が正しくないため、更新トークンの期限が切れると、フォームデータモデルのリクエストが失敗する。(NPR-33168)
* ドキュメントサービス：Convert Gibson JAR が見つからないため、PDFサービスがPDFドキュメントを PostScript に変換できません。 [!DNL WebLogic] の [!DNL Linux] サーバー (NPR-33515、CQ-4292239)
* ドキュメントサービス：ユーザーがテキストファイルをPDFに変換すると、日本語の文字が正しく表示されない (NPR-33239)。
* GuideSOMProviderServlet を使用して XSS を格納しました (NPR-32701)。

## 6.4.8.4 のインストール {#install}

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
>機能パックをAEM 6.4 にインストールしているお客様向け。Adobeが提供するオプションの機能パックは、リリースバージョンとサービスパックに依存します。 機能パックがインストールされている場合は、AEMカスタマーケアチームに連絡して、AEM 6.4 用のこの累積修正パックとの互換性を検証してください。

* AEM 6.4.8.4 にはAEM 6.4.8.0 が必要です。 [アップグレードドキュメント](../sites-deploying/upgrade.md) を参照してください。
* MongoDB と複数のインスタンスを含むデプロイメントでは、パッケージマネージャーを使用してオーサーインスタンスの 1 つに AEM 6.4.8.4 をインストールしてください。
* 累積修正パックをインストールする前に、AEMインスタンスのスナップショットまたは新しいバックアップがあることを確認してください。
* インストールする前にインスタンスを再起動してください。これは、インスタンスがまだ更新モードになっている場合（インスタンスが以前のバージョンから更新されたばかりの場合）にのみ必要ですが、インスタンスが長期間実行されている場合は、一般的に推奨されます。

>[!NOTE]
>
>AEM 6.4.8.4 パッケージを削除またはアンインストールすることはお勧めしません。

### 累積修正パックのインストール {#install-cumulative-fix-pack}

既存の AEM 6.4.8.0 インスタンスに累積修正パックをインストールするには、次の手順を実行します。

1. [ソフトウェア配布](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq640/cumulativefixpack/aem-6.4.8-cfp-4.0.zip)リンクをクリックして、パッケージをダウンロードします。

1. [パッケージマネージャー](http://localhost:4502/crx/packmgr/index.jsp)を開き「**[!UICONTROL パッケージをアップロード]**」をクリックしてパッケージをアップロードします。

1. パッケージ名を選択して、「**[!UICONTROL インストール]**」をクリックします。

>[!NOTE]
>
>**6.4.8.4 のインストール中に、パッケージマネージャー UI のダイアログが途中で終了することがあります。**
>
>そのため、エラーログが安定するのを待ってから、インスタンスにアクセスすることをお勧めします。アップデータバンドルのアンインストールに関連する特定のログが表示されるのを待ってから、インストールが正常に完了するようにする必要があります。 通常は、Safari で発生しますが、任意のブラウザーで断続的に発生する可能性があります。

### 自動インストール {#auto-installation}

実行中のインスタンスに AEM 6.4.8.4 を自動的にインストールするには、次の 2 つの方法があります。

A.パッケージをに配置します。*/crx-quickstart/install* フォルダーを使用して、サーバーの実行中に保存します。 パッケージは自動的にインストールされます。

B. [パッケージマネージャーからの HTTP API](https://docs.adobe.com/content/docs/en/crx/2-3/how_to/package_manager.html)  — 必ず `cmd=install&recursive=true`  — ネストされたパッケージがインストールされます。

>[!NOTE]
>
>AEM 6.4.8.4 では、ブートストラップインストールをサポートしていません。

### インストールの検証 {#validate-install}

1. 製品情報ページ（*/system/console/productinfo*）のインストール済み製品には、更新されたバージョン文字列「Adobe Experience Manager, Version 6.4.8.4」が表示されます。
1. すべての OSGi バンドルは、OSGi コンソール（Web コンソールを使用：/system/console/bundles）で ACTIVE または FRAGMENT です。
1. OSGI バンドル org.apache.jackrabbit.oak-core は、バージョン 1.8.17 以降です (Web コンソールを使用：/system/console/bundles) に書き込みます。

このリリースのAEM Sitesおよび Assets での実行に関する認定プラットフォームを決定するには、 [技術要件](../sites-deploying/technical-requirements.md).

>[!NOTE]
>パッケージが正常にインストールされると、コンテンツパッケージが正常にインストールされたことを示す情報メッセージが表示されます。例： **「コンテンツパッケージAEM-6.4-Service-Pack-8 が正常にインストールされました。」**

### Dynamic Media Viewers の更新 (5.10.1) {#update-dynamic-media-viewers}

AEM 6.4.8.4 には、Dynamic Mediaビューア (5.10.1) の新しいバージョンが含まれています。これにより、画像プリセットページの名前の重複を確認できます。 Dynamic Mediaのお客様は、次のコマンドを実行して、標準のビューアプリセットを最新の状態にすることをお勧めします。

`curl -u admin:admin http://localhost:4502/libs/settings/dam/dm/presets/viewer.pushviewerpresets`

新しいビューアプリセットを/conf の場所にコピーします。

### AEM Forms アドオンパッケージのインストール {#install-aem-forms-add-on-package}

>[!NOTE]
>
>[!DNL Experience Manager Forms] では、予定されている [!DNL Experience Manager] 累積修正パックリリース日の 1 週間後にアドオンパッケージをリリースします。

>[!NOTE]
>
>AEM Forms を使用していない場合はスキップしてください。AEM Forms の修正は、個別のアドオンパッケージを介して配信されます。

1. AEM Cumulative Fix Pack がインストールされていることを確認します。
1. 次のリストにある対応する forms アドオンパッケージをダウンロードします。 [AEM Formsリリース](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html#forms-updates) ご使用のオペレーティングシステム用。
1. フォームアドオンパッケージをインストールします。詳しくは、 [AEM forms アドオンパッケージのインストール](https://docs.adobe.com/content/help/en/experience-manager-64/forms/install-aem-forms/osgi-installation/installing-configuring-aem-forms-osgi.html#install-aem-forms-add-on-package).

### AEM Forms JEE インストーラーのインストール {#install-aem-forms-jee-installer}

>[!NOTE]
>
>JEE で AEM Forms を使用していない場合はスキップします。AEM Forms JEE の修正は別のインストーラーを介して配布されます。

AEM Forms JEE の累積インストーラーのインストールとデプロイメント後の設定について詳しくは、[AEM Forms JEE パッチインストーラー ](jee-patch-installer-64.md) を参照してください。

>[!NOTE]
>
>JEE 上のExperience Manager Formsの累積インストーラーをインストールした後、最新のFormsアドオンパッケージをインストールし、次の場所からFormsアドオンパッケージを削除します。 `crx-repository\install` フォルダーを開き、サーバーを再起動します。

### Uber Jar {#uber-jar}

AEM 6.4.8.4 の Uber Jar は、 [Maven 中央リポジトリ](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.4.8.4/).

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
>UberJar およびその他の関連アーティファクトは、Adobeのパブリック Maven リポジトリ (repo.adobe.com) の代わりに、Maven Central リポジトリで使用できます。 メインの UberJar ファイルの名前がに変更されます。 `uber-jar-<version>.jar`. その結果、 `classifier`を `apis` 値として、 `dependency` タグを使用します。

## 廃止される機能および削除された機能 {#removed-deprecated-features}

このセクションでは、AEM 6.4 で廃止される機能および削除された機能について説明します。

| 領域 | 機能 | 代替手段 | バージョン |
|---|---|---|---|
| Assets | サブアセットのタグアクションを管理 | 代替機能はありません | AEM 6.4.2.0 |
| Assets と Adobe Creative Cloud の統合 | [AEM／Creative Cloud フォルダー共有](https://docs.adobe.com/content/help/ja/experience-manager-64/assets/administer/aem-cc-folder-sharing-best-practices.html)は、クリエイティブユーザーに AEM のアセットへのアクセスを提供する方法として、AEM 6.2 で導入されました。Creative Cloud アプリケーションでリリースされた新しい機能である Adobe Asset Link では、ユーザーエクスペリエンスが大幅に向上し、Photoshop、InDesign、Illustrator 内から AEM のアセットへの直接アクセスが強化されています。アドビは、このフォルダー共有機能をさらに強化する予定はありません。この機能はAEMに含まれますが、お客様には代わりの機能を使用することを強くお勧めします。 | AdobeAsset Link またはデスクトップアプリケーション 詳細については、[AEM Creative Cloud の統合](/help/assets/aem-cc-integration-best-practices.md)記事を参照してください。 | AEM 6.4.4.0 |

## 既知の問題 {#known-issues}

* 次の [!DNL Experience Manager] 6.4～ [!DNL Experience Manager] 6.5、一部のバンドルのステータスが「 `Active`. 最新の [!DNL Experience Manager] 6.5 Service Pack を使用して問題を解決。

AEM 6.4.8.0 Service Pack の既知の問題について詳しくは、 [AEM 6.4.8.0 Service Pack リリースノート](sp-release-notes.md).

## 含まれている OSGi バンドルとコンテンツパッケージ {#osgi-bundles-and-content-packages-included}

次のテキストドキュメントは、AEM 6.4.8.4 に含まれている OSGi バンドルとコンテンツパッケージの一覧です。

AEM 6.4.8.4 に含まれている OSGi バンドルの一覧

[ファイルを入手](assets/6.4.8.4_osgi_bundles.txt)

AEM 6.4.8.4 に含まれているコンテンツパッケージの一覧

[ファイルを入手](assets/6.4.8.4_content_packages.txt)

## 役立つリソース {#helpful-resources}

* [AEM 6.4 リリースノート](../release-notes/release-notes.md)
* [AEM 製品ページ](https://www.adobe.com/solutions/web-experience-management.html)
* [AEM 6.4 ドキュメント](https://experienceleague.adobe.com/docs/experience-manager-64.html?lang=ja)
* [Adobe Priority 製品アップデート](https://www.adobe.com/subscription/priority-product-update.html)のサブスクリプションを購入する

## 制限付きサイト {#restricted-sites-new}

以下のサイトは既存ユーザーのみが参照できます。アクセス権が必要な既存ユーザーの方は、アドビのアカウントマネージャーまでお問い合わせください。

* [licensing.adobe.com からの製品ダウンロード](https://licensing.adobe.com/)
* [カスタマーサポートに連絡](https://docs.adobe.com/content/help/en/customer-one/using/home.html)
