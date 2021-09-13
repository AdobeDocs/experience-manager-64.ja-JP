---
title: 'AEM 6.4 累積修正パックリリースノート '
description: リリースノート(Adobe Experience Manager 6.4累積修正パック固有)
contentOwner: AK
mini-toc-levels: 1
exl-id: a63e77a3-da48-4072-bc75-c4c41a2f62a3
source-git-commit: 0120fe1303aa3b7f5aa7db39eaf40ff127f2e338
workflow-type: tm+mt
source-wordcount: '4676'
ht-degree: 16%

---

# AEM 6.4 累積修正パックリリースノート  {#aem-cumulative-fix-pack-release-notes}

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

AEM累積修正パック6.4.8.4は、2020年3月のAEM 6.4 Service Pack 8(6.4.8.0)の一般リリース以降に対応された、内部およびお客様向けの修正を含む重要な更新です。

AEM 6.4.8.4は、AEM 6.4 Service Pack 8に依存するCumulative Fix Pack (CFP)です。 AEM 6.4 Service Pack 8をインストールした後にCFPをインストールします。

[!DNL Adobe Experience Manager] 6.4.8.4で導入された主な機能と機能強化は次のとおりです。

* PDFG変換の実行時に[!DNL Experience Manager Forms]レジストリの変更を有効または無効にする機能。

* フォームデータモデルのSOAPベースWebサービス用のX-509証明書ベースの認証。

* 組み込み型のリポジトリ（Apache Jackrabbit Oak）をバージョン 1.8.24 に更新しました。

CFPと他のタイプのリリースについて詳しくは、[AEM Update Release Vehicle Definitions](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-release-vehicle-definitions.html)を参照してください。

Adobe Experience Manager 6.4.8.4では、次の問題が修正されました。

### Sites {#sites-6484}

* Experience Managerサービスパック6.4.8.2のインストール後、ユーザーはコンテンツフラグメントモデルを編集できず、次のエラーが発生します。

   `Uncaught TypeError: Cannot read property 'debounce' of undefined` (NPR-35312)
* ユーザーがログアウトボタンをクリックしても、そのユーザーはパッケージマネージャーからログアウトされません。 (NPR-35161)
* Experience Manager6.4.xからExperience Manager6.4.8.3にアップグレードした後、「公開を管理」を使用してページを公開できない。 （CQ-4312511）
* ブループリントの子ページを元の場所に戻すと、cq:liveSyncConfig設定はライブコピーの子ページから削除されません。 (NPR-35900)
* ライブコピーを含むブループリントを前後に移動すると、最初の移動のみ機能し、失敗してエラーメッセージは表示されません。 (NPR-35899)


### [!DNL Assets] {#assets-6484}

* `IndexWriter.merge` スマートタ `OutOfMemoryError` グ機能で大きいとインデックスが作成さ `/oak:index/lucene` れるの `/oak:index/ntBaseLucene` で、エラーが発生する原因となる。(NPR-35650)
* ユーザーは、[!DNL Adobe InDesign]でアセットを編集した後にチェックインできず、権限の不足に関するエラーが表示される(NPR-35340)。
* 名前の競合を解決した後に既存のアセットの新しいバージョンが作成されると、元のアセットのメタデータが上書きされる(NPR-35939)。
* 自動生成されたプライベートフォルダーのグループは、そのフォルダーを削除する際や、「[!UICONTROL プライベートフォルダーの制限を削除]」オプションを設定してフォルダーを更新する際に、維持および削除されません(NPR-35625)。

#### [!DNL Dynamic Media] {#dynamic-media}

* 断続的なImageServerエラーが発生すると、[!DNL Experience Manager]のいくつかの機能が失敗し、403応答が発生します。 （CQ-4308565）

### 統合 {#integrations-6484}

* Experience Manager6.4.8.3にアップグレードした後にページのプロパティを開くと、JavaScriptエラーがコンソールに表示され始める(NPR-35649)。

### フォーム {#forms-6484}

>[!NOTE]
>
>[!DNL Experience Manager Forms] では、予定されている [!DNL Experience Manager] 累積修正パックリリース日の 1 週間後にアドオンパッケージをリリースします。

**Correspondence Management**

* レターを編集する際、条件を持つモジュールの読み込みに時間がかかる(NPR-35326)。

* レターを編集する際に、コンテンツとデータの連結がユーザーインターフェイスに表示されません(CQ-4312905)。

**ドキュメントサービス**

* [!DNL JAVA]を[!DNL JDK1.8.0_261]にアップグレードした後にPDFをアセンブルできない(NPR-35761、NPR-35848)。

**Foundation JEE**

* [!DNL Forms]ワークフローでタスク通知を編集すると、その通知を保存できなくなります(CQ-4315055)。

セキュリティ更新について詳しくは、[Experience Managerセキュリティ速報ページ](https://helpx.adobe.com/security/products/experience-manager.html)を参照してください。

## 以前の累積修正パックに含まれていたホットフィックスと機能パック {#hotfixes-and-feature-packs-included-in-previous-cumulative-fix-packs}

### Adobe Experience Manager 6.4.8.3 {#experience-manager-6483}

AEM累積修正パック6.4.8.3は、2020年3月のAEM 6.4 Service Pack 8(6.4.8.0)の一般リリース以降に対応された、内部およびお客様向けの修正を含む重要な更新です。

AEM 6.4.8.3は、AEM 6.4 Service Pack 8に依存するCumulative Fix Pack (CFP)です。 AEM 6.4 Service Pack 8をインストールした後にCFPをインストールします。

AEM 6.4.8.3では、組み込みリポジトリ(Apache Jackrabbit Oak)がバージョン1.8.23に更新されています。

CFPと他のタイプのリリースについて詳しくは、[AEM Update Release Vehicle Definitions](https://docs.adobe.com/content/help/en/experience-manager-65/deploying/deploying/update-release-vehicle-definitions.html)を参照してください。

Adobe Experience Manager 6.4.8.3では、次の問題が修正されました。

#### Sites {#sites-6483}

* コンテンツフラグメントのバリエーションのテキストを更新すると、マスターコンテンツフラグメントのコンテンツがバリエーションではなく更新される(NPR-35080)。

* コンポーネントのString typeラベルプロパティに数値を設定し、そのコンポーネントを削除し、取り消しオプションを使用して元に戻すと、ラベルプロパティのタイプが自動的にStringからLongに変更されます(NPR-34738)。

* ファイルのアップロードコンポーネントをマルチフィールドに追加すると、画像パスはマルチフィールドノードではなくコンポーネントノードに保存されます(NPR-34423)。

* ページの移動ウィザードで、宛先が選択されていない場合でも、次のボタンが有効なままになる(NPR-34460)。

* 親コンポーネントに`cq:isContainer`プロパティが含まれる場合、継承されたコンポーネントにプロパティが自動的に含まれることはありません(CQ-4308409)。

* `calc()`関数を使用してCSSの縮小を使用すると、`+`記号の周囲の空白が削除されます(NPR-34991)。

* AEMインスタンスを起動すると、`com.adobe.granite.maintenance.impl.MaintenanceTaskManagerImpl`と`com.adobe.granite.maintenance.impl.TaskScheduler`のコンポーネントが`Active`状態で表示されない(NPR-34952)。

#### [!DNL Assets] {#assets-6483}

* 既存のアセットのバージョンを作成する際、メタデータプロファイルがフォルダーに適用されていると、ユーザーのメタデータの更新が保持されない(NPR-34833)。
* [!DNL Adobe Asset Link]を[!DNL Adobe InDesign]と共に使用する場合、検索結果にはフォルダーやコレクションは含まれず、アセットのみが含まれる(NPR-34700)。
* フォルダー上でアセットをドラッグして移動すると、ユーザーインターフェイスに「[!UICONTROL Lightboxにドロップ]」および「[!UICONTROL コレクションにドロップ]」のオプションも表示されます。 移動操作がキャンセルされても、ユーザーインターフェイスに後者の2つのオプションが引き続き表示される(NPR-34525)。
* 「公開を管理」インターフェイスを開くと、公開オプションは使用できず、非公開オプションを選択すると、スコープページが空白になります(CQ-4302509)。

##### [!DNL Dynamic Media] {#dynamic-media-6483}

* 画像プリセット設定で、[!DNL Experience Manager]で「JPGクロミナンスダウンサンプリングを有効にする」オプション[!UICONTROL の選択を解除すると、変更は[!DNL Dynamic Media]と同期しません(NPR-34284)。]
* [!UICONTROL ビューアプリセットエディター]で、[!UICONTROL PanoramicImage/PanoramicImage_VR]プリセットを編集する際に、`PanoramicView`コンポーネントで`PANORAMICVIEW_AUTOROTATE`修飾子ラベルを使用できません(CQ-4302043)。
* [!DNL Experience Manager]からビデオを非公開にしても、設定済みのDynamic Media Classic上のアダプティブビデオセットは非公開になりません。 (CQ-4304405).

#### プラットフォーム {#platform-6483}

* `emitUseStrict`フラグは、Google Closure Compiler(GCC)プロセッサ機能`com.adobe.granite.ui.clientlibs.impl.HtmlLibraryManagerImpl`に追加されます。 フラグは、`use strict`命令の出力を抑制する(NPR-34830)。
* 毎日または毎週のメンテナンスタスクの開始時に`NullPointerException`が返される(NPR-34702)。
* [!DNL Apache Sling Health Check]ツールは非推奨です。 代わりに、[パターン検出](https://experienceleague.adobe.com/docs/experience-manager-64/deploying/upgrading/pattern-detector.html)を使用して、コンテンツ違反を検出します(NPR-33929)。

#### 統合 {#integrations-6483}

* フォルダーから[!UICONTROL オーディエンス]ページに移動すると、[!UICONTROL 作成]ボタンが[!UICONTROL オーディエンス]ページに表示されます(NPR-35152)。

#### ユーザーインターフェイス {#ui-6483}

* [!UICONTROL オムニサーチ]ユーザーインターフェイスの[!UICONTROL フィルター]検索パネルでも、検索が実行された場所以外の場所から結果が返されます(NPR-34877)。
* [!UICONTROL オムニサーチ]ユーザーインターフェイスの[!UICONTROL フィルター]パネルを閉じても、左側のレールは[!UICONTROL コンテンツ]選択にリセットされず、[!UICONTROL フィルター]パネルが再び開かない。(NPR-34483)
* ページプロパティにアクセスすると`NullPointerException`が返される(NPR-34509)。

#### Communities {#communities-6483}

<!-- Following fixes of 6483 are documented on Nov 11 20202 by Vishabh. 
-->

* 製品内の不公平な用語のすべてのインスタンスは、受け入れられた同等のものに置き換えられます(NPR-34506)。

#### コマース {#commerce-6483}

* 1つのコレクションに15個を超える製品がある場合、そのコレクションには最初の15個の製品のみが表示されます(NPR-34494)。

#### フォーム {#forms-6483}

>[!NOTE]
>
>[!DNL Experience Manager Forms] では、予定されている [!DNL Experience Manager] 累積修正パックリリース日の 1 週間後にアドオンパッケージをリリースします。

>[!NOTE]
>
>[!DNL Experience Manager] 累積修正パックには、の修正は含まれませ [!DNL Experience Manager Forms]ん。別の[!DNL Forms]アドオンパッケージを使用して配信されます。 さらに、JEE上の[!DNL Experience Manager Forms]の修正を含む累積的なインストーラーがリリースされました。 詳しくは、「 [AEM Formsアドオンパッケージのインストール](#install-aem-forms-add-on-package) 」および「 [AEM Forms JEEインストーラーのインストール](#install-aem-forms-jee-installer) 」を参照してください。

**アダプティブフォーム**

* [!DNL Experience Manager]累積修正パックを適用した後、クラシックUIを使用してアダプティブフォームを編集できない。(NPR-35127)

* キャッシュの無効化が原因で、フラグメントがアダプティブフォームに読み込まれるのに時間がかかる(NPR-34655)。

* アクセシビリティ：アダプティブフォームのスクリーンリーダーに対してタブナビゲーションが適切に機能しない(NPR-34550)。

**Correspondence Management**

* ES3からアセットを移行する場合、アセットには編集不可の2つのデフォルト条件が含まれます(NPR-34971)。

**Foundation JEE**

* [!DNL AEM Forms]ユーザーをFlashからHTMLに移行します(CQ-4304075)。

### Adobe Experience Manager 6.4.8.2 {#experience-manager-6482}

AEM累積修正パック6.4.8.2は、2020年3月のAEM 6.4 Service Pack 8(6.4.8.0)の一般リリース以降に対応された、内部およびお客様向けの修正を含む重要な更新です。

AEM 6.4.8.2は、AEM 6.4 Service Pack 8に依存するCumulative Fix Pack (CFP)です。 AEM 6.4 Service Pack 8をインストールした後にCFPをインストールします。

AEM 6.4.8.2では、組み込みリポジトリ(Apache Jackrabbit Oak)がバージョン1.8.22に更新されました。

CFPと他のタイプのリリースについて詳しくは、[AEM Update Release Vehicle Definitions](https://docs.adobe.com/content/help/en/experience-manager-65/deploying/deploying/update-release-vehicle-definitions.html)を参照してください。

Adobe Experience Manager 6.4.8.2では、次の問題が修正されました。

#### Sites {#sites-6482}

* `RolloutConfigManagerFactoryImpl`がロールアウト設定を読み込めない場合、見つからない設定の読み込みは試みません。 キャッシュされた設定を返します(NPR-34091)。
* テキストコアコンポーネントで、ソースHTML編集オプションを使用した後、`em`タグのクラスが削除される(NPR-34080)。
* Experience Manager6.2からExperience Manager6.5にアップグレードすると、静的テンプレートのParsysコンポーネントが正しく表示されません。 Parsysコンポーネントの高さが0に設定され、その中のコンポーネントが表示されない(NPR-34044)。
* テンプレートエディター内の許可されているコンポーネントに対して、ラベル情報が表示されない(NPR-33908)。

   ![レイアウトコンテナにラベルが見つかりません](assets/33908_missing_labels.png)

* ユーザーが、ネストされたコンポーネントの4番目のレベルの後に、parsysにコンポーネントを追加または編集できない(NPR-33873)。
* 編集可能なテンプレートの初期コンテンツが変更され、その後テンプレートが公開された場合、このテンプレートで作成された新しいページは、ページが公開されなくても、テンプレートの公開日を示します(NPR-33822)。
* コピー&amp;ペースト操作中に、コピー上の`cq:acLinks`および`cq:acUUID`プロパティが削除される(NPR-33793)。[!DNL Adobe Campaign]
* 「[!UICONTROL ライブ使用状況]」タブには、49件の結果のみが表示されます。 コンポーネントのすべての使用状況が表示されるわけではありません(NPR-33710)。
* URLに`/`文字が含まれるWebページが、オーサリング中に応答しなくなる。 オーサリング中にコンポーネントが追加されると、CPU使用率が増加し、ブラウザーが応答を停止する(NPR-33625)。
* [!DNL RTE]のインライン編集モードで、画像をドラッグしてもテキストコンポーネントに対しては機能しない。(NPR-33579)
* ブループリントページ内に、ページ名と同じ名前のコンポーネントを作成できます。 ロールアウト時に、`_msm_moved`のサフィックスを付けて、このようなコンポーネントの名前が変更されます。 ただし、コンポーネントは[!UICONTROL 段落システム]の最後に移動されます(NPR-33534)。
* 最初のコンテンツルートで[!UICONTROL include subpages]プロパティがチェックされていない場合、ローンチの昇格でページが公開されない(NPR-33533)。
* `PageRedirectServlets`はURLフラグメントまたはアンカーの後にクエリー文字列を配置するので、アンカーを含む[!DNL Experience Manager]ページへのリダイレクトはオーサーインスタンスで機能しません。(NPR-34287)
* `PageRedirectServlet` リン `.html` クの失敗につながるSlingマッピングの後にを追加します(NPR-34271)。
* ページの[!DNL Live Copy]を休止すると、エディターモードで確認できるように、で継承が解除されます。 ただし、ページプロパティで、継承を表すアイコンが誤って、継承が存在し、壊れていないことを示す(NPR-34096)。
* テンプレートを編集ページでの許可されたコンポーネントの表示に関する問題(CQ-4297295)。
* ChromeおよびFirefoxをアップグレードした後、ポップアップメニューが期待どおりに動作しない。 ページプロパティの読み込み時に、パネルにデータが含まれている場合、パネルが表示されません(CQ-4292995)。
* [!DNL Experience Manager Sites]コンポーネントの複数のクロスサイトスクリプティングインスタンス(NPR-33926)。
* ユーザ入力は、クライアントに情報を送信する際に、様々なコンポーネントに対して適切にエンコードされない(NPR-33696)。
* `childrenlist.html`で終わるURLは、404応答ではなくHTMLページを表示します。 このようなURLは、クロスサイトスクリプティングに対して脆弱です(NPR-33441)。

#### Assets {#assets-6482}

* アップロードされたPDFファイルのテキスト抽出が機能せず、PDFファイル内の一部の単語の全文検索がそのPDFファイルを取得できない(NPR-34165)。

   >[!NOTE]
   >この修正を機能させるには、Service Pack 6.4.8.2をインストールした後で、Adobe Experience Managerインスタンスを再起動します。

* 名前に特殊文字が含まれるアセットの検索候補の特殊文字の前にバックスラッシュが追加される(NPR-33833)。

* スマートコレクションとして保存されたカスタムフィルターは、アセットに正しく適用されないので、検索結果が正確になりません   (NPR-33725)。

* 並べ替えられたフォルダー内のアセットのタイムラインは、アセットが移動されたことを示している(NPR-33580)。

* [!DNL Brand Portal]から一括でアセットを非公開にすると、`Request-URI Too Long`エラーが発生する(NPR-34158)。

* 列表示で、アセットのセットを選択した後に「[!UICONTROL フィルター]」オプションを選択し（アセットの選択を解除）、移動する別のアセットのセットを選択した場合、以前に選択されたアセットも新しい場所に移動されます(NPR-34018)。

* ページに収まるアセットが多数ある場合でも、リスト表示にスクロールバーが表示されない。(NPR-34156)

* アセットの[!UICONTROL 公開を管理]ページが壊れ、その中のオプションが機能しません(CQ-4302509)。

**Dynamic Media**

* イメージプロファイルが複数（例えば、11）の縦横比を持つフォルダーに追加されると、スマート切り抜き機能がエラーで失敗する(NPR-34083)。

* [!UICONTROL Adobe Experience Manager]での画像プリセットの変更がDynamic Media Classicに同期されない(NPR-34284、CQ-4299713)。

* [!UICONTROL PANORAMICVIEW_AUTOROTATE]修飾子ラベルが[!UICONTROL ビューアプリセットエディター]ページの[!UICONTROL 「ビヘイビアー]」タブに表示されません(CQ-4302043)。

#### プラットフォーム {#platform-6482}

* デフォルトエージェント（パブリッシュ）設定の「 **[!UICONTROL 接続タイムアウト]** 」および「 **[!UICONTROL ソケットタイムアウト]** 」のデフォルト値が指定されていません(NPR-33708)。
* メンテナンスタスクスケジューラは、設定された回数よりも多くメンテナンスタスクを開始および停止します(NPR-33520)。
* アップグレードされたExperience Managerインスタンスで診断ツールを使用してログをダウンロードできない。(NPR-34419)

#### 統合 {#integrations-6482}

* [!DNL Adobe Dynamic Tag Management]から移行されたライブラリの[!DNL Adobe Launch]ライブラリURLを生成する際に、`library_path`の値は考慮されません。 また、移行されたライブラリは、[!DNL Adobe Launch]ライブラリとは異なるプレフィックスを使用します。 (NPR-34238).
* クラウドサービスから継承されたプロパティが、ページプロパティの更新時に保持されない(NPR-33865)。

#### ユーザーインターフェイス {#ui-6482}

* 検索ページで選択されたアセットの数の表示が正しくない(NPR-33540)。

#### コミュニティ {#communities-6482}

* 管理コンソールを通じて追加されたコミュニティグループの既存のユーザーは、コミュニティグループコンソールで変更を行うと、ユーザーリストから削除されます(NPR-34312)。

#### フォーム {#forms-6482}

>[!NOTE]
>
>[!DNL Experience Manager] 累積修正パックには、の修正は含まれませ [!DNL Experience Manager Forms]ん。別の[!DNL Forms]アドオンパッケージを使用して配信されます。 さらに、JEE上の[!DNL Experience Manager Forms]の修正を含む累積的なインストーラーがリリースされました。 詳しくは、「 [AEM Formsアドオンパッケージのインストール](#install-aem-forms-add-on-package) 」および「 [AEM Forms JEEインストーラーのインストール](#install-aem-forms-jee-installer) 」を参照してください。

**アダプティブフォーム**

* 見つからないアダプティブフォームフラグメントがある場合、そのアダプティブフォームがレンダリングに失敗する(NPR-34303)。

* アダプティブフォームフィールドのヘルプコンテンツの説明に段落のHTMLタグが表示される(NPR-34117)。

* [!DNL Experience Manager Sites]ページにFormsコンテナを追加すると、そのページに次のエラーメッセージが表示され、新しいコンポーネントの追加が許可されない。(NPR-33858)

   `DevTools failed to load SourceMap: Could not load content for <Link>. HTTP error: status code 404, net::ERR_HTTP_RESPONSE_CODE_FAILURE`

* 「**[!UICONTROL サーバーで再検証]**」プロパティを選択し、複数の添付ファイルをアップロードすると、アダプティブフォームは送信に失敗する(NPR-33701)。

* **[!UICONTROL ページの「ページ言語]**&#x200B;を使用」と「**[!UICONTROL フォームが[!DNL Experience Manager Sites]ページの[!DNL Experience Manager Forms]コンポーネントのページ]**&#x200B;オプションの幅全体をカバーする」を選択すると、ページの翻訳に失敗します(NPR-33641)。

* [!DNL Experience Manager Sites]ページに埋め込まれた、分析が有効なアダプティブフォームを送信すると、分析が正しく機能しない(NPR-31359)。

* [!DNL Lodash]ライブラリと[!DNL backbone]ライブラリの依存関係を削除しました(NPR-33458)。

* **[!UICONTROL RESTエンドポイントへの送信]**&#x200B;送信アクションがアダプティブフォームに対して機能しない(NPR-34513)。

* アクセシビリティ：必須フィールドの添付ファイルをアップロードせずにアダプティブフォームを送信しようとした場合、フォーカスが自動的に添付フィールドに移動しない(NPR-34511)。

* ユーザー入力は、クライアントに情報を送信する際に、[!DNL Forms]コンポーネントに対して適切にエンコードされない(NPR-33611)。

**ワークフロー**

* [!DNL Experience Manager] ワークフローのパージ操作が失敗し、次のエラーメッセージが表示される(NPR-33576)。

   `java.lang.UnsupportedOperationException: The query read more than 500000 nodes in memory`

* [!DNL Experience Manager] 6.4.8.1をインストールすると、項目の[!UICONTROL To Do]リストはリンクとして表示されません。 [!UICONTROL To Do]項目のテキストには、HTMLタグが含まれます(NPR-34318)。

**BackendIntegration**

* AWSがホストする[!DNL Experience Manager Forms Linux]環境でフォームデータモデルを設定できない(NPR-33617)。

**デザイナー**

* [!DNL Acrobat DC]が[!DNL Experience Manager] Formsサーバーにインストールされている場合、**[!UICONTROL 「フォームを配布」]**&#x200B;オプションは[!DNL Experience Manager Designer]バージョン6.xでは使用できません(NPR-34325)。

**Document Security**

* [!DNL Experience Manager] 6.4.8.0をインストールした後、PDFファイル内のHSMベースの証明書を使用して署名操作を実行できない(NPR-34309)。

**アップグレード**

* [!DNL Linux]環境でDocument Securityを使用して[!DNL Experience Manager Forms]の[!DNL JBoss]バージョンを7.0.9にアップグレードすると、エラーが発生します(CQ-4300546)。

セキュリティ更新について詳しくは、[Experience Managerセキュリティ速報ページ](https://helpx.adobe.com/security/products/experience-manager.html)を参照してください。

### Adobe Experience Manager 6.4.8.1 {#experience-manager-6481}

AEM累積修正パック6.4.8.1は、2020年3月のAEM 6.4 Service Pack 8(6.4.8.0)の一般リリース以降に対応された、内部およびお客様向けの修正を含む重要な更新です。

AEM 累積修正パック 6.4.8.1 は、AEM 6.4 サービスパック 8 に依存しています。したがって、AEM 6.4 Service Pack 8をインストールした後に、AEM Cumulative Fix Pack 6.4.8.1パッケージをインストールする必要があります。

AEM 6.4.8.1の主な特徴は次のとおりです。

* セキュリティを強化するために、CRXDE Liteへの匿名アクセスは許可されていません。 代わりに、ユーザーはログイン画面に移動します。 [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md)を使用した開発を参照してください。
* Adobe Experience Managerとのパッケージ共有の統合を削除しました。
* 組み込み型のリポジトリ（Apache Jackrabbit Oak）をバージョン 1.8.21 に更新しました。

CFPと他のタイプのリリースについて詳しくは、[AEM Update Release Vehicle Definitions](https://docs.adobe.com/content/help/en/experience-manager-65/deploying/deploying/update-release-vehicle-definitions.html)を参照してください。

Adobe Experience Manager 6.4.8.1では、次の問題が修正されました。

#### Sites {#sites-6481}

* 匿名ユーザーは、CRX DE Lite機能にアクセスできます(NPR-33522)。
* ライブコピー内のローカルコンポーネントの名前がブループリント内のコンポーネントの名前と同じで、コンポーネントがブループリントからロールアウトされる場合、ローカルコンポーネントの名前に_msm_movedという用語は追加されません(NPR-33207)。
* 元の要求に追加されたパラメーターは、リダイレクトURLに含まれません(NPR-33174)。
* Coral.SelectオプションでemptyOption=trueが設定されるか、値が「」のデフォルトアイテムが含まれている場合、dropdownshowhide.jsファイルで次のエラーが発生します。キャッチできないTypeError:component.getValueが関数ではない(NPR-33163)。
* コンポーネントにdata-sly-resourceとして別のコンポーネントが含まれる場合、親コンテナコンポーネントのプレースホルダーが内部コンポーネントのプレースホルダーに置き換えられます(NPR-33119)。
* スキーマにコンテンツフラグメントをベースにし、そのフラグメントに必須のテキスト領域またはパスフィールドが含まれている場合、コンテンツフラグメントの保存に失敗する(NPR-33007)
* 標準搭載のエクスペリエンスフラグメントコンポーネントを使用してカスタムコンポーネントを作成し、AEM Sitesページで使用すると、AEMはカスタムコンポーネントの参照（使用状況）を表示しない。(NPR-32852)
* AEM Sitesページが、複数のライブコピーを含む大きなコンテンツセットに含まれている場合、ページバージョン履歴のプレビューを読み込めない(NPR-32772)。
* ローンチを昇格させると、ローンチに追加されたすべてのコンポーネントに「cq:LiveRelationship」mixinが追加されます。 「 — ソースページのライブデータを継承 — 」オプションを選択した場合と選択しない場合とに関係なく、すべてのローンチに影響します。(NPR-32664)
* ページネーションが開始すると、エクスペリエンスフラグメントピッカーがすべての項目を読み込まない(NPR-32605)。
* AEM Sitesページのローンチを作成できない。 ローンチの作成でエラーが発生する(NPR-32544)。
* 「公開を管理」で、アクティベーションワークフローのリクエストに参照されているアセットが含まれない(NPR-32463)。
* Dispatcherヘルスチェックで、ログファイルに`Invalid cookie header`警告メッセージが表示される(NPR-33630)。
* Salesforce統合は、SSRF(NPR-32671)に対して脆弱です。
* PreferencesServletにXSSが反映される(NPR-33439)。

#### Assets {#assets-6481}

* リスト表示での選択内容の変更に従って、アセットの数は変更されない。(NPR-33285)

* 親ノード（単一の子フォルダーが表示される）を選択した後で子フォルダーを選択すると、次のボタンが有効にならない(NPR-33284)。

* DMS7またはハイブリッドモードが有効な場合、リポジトリルートでの読み取りアクセス権を持たないユーザーに対して、タッチUIが（エラー付きで）レンダリングに失敗する(NPR-33175)。

* ダウンロードしたzipファイルで、フォルダー名とアセット名に使用されているGB18030文字が空白に変わる(NPR-33150)。

* 追加のフォルダーが、親フォルダー内にあるアセットのスマート切り抜きで作成され、その名前にドット`.`文字が含まれる(NPR-32755)。

* 遅延読み込みがトリガーされず、通知インボックスからタスクを確認するために選択時に100個以下のアセットが表示される。(NPR-32749)

* coral-infoの変更により、コレクションを共有するリンクページが壊れる(NPR-32510)。

* バルクアップロード中のアセット処理が停止する(CQ-4293916)。

* Experience ManagerのSSRF脆弱性(NPR-33437)。

#### プラットフォーム {#platform-6481}

* `/etc/maps`の下に`sling:match`マップエントリが作成された場合、[!DNL Sling]フィルターは呼び出されません(NPR-33308)。
* ページの非アクティブ化時に、すべてのフラッシュエージェントがトリガーされる(NPR-32941)。
* `ScriptProcessor` APIを使用してJavaScriptライブラリを縮小すると、ログファイルに、JavaScriptコードが厳密モードに準拠していないことを示すエラーメッセージが表示されます。 APIには、厳密モードを有効または無効にするオプションは用意されていません。 (NPR-32746).
* SQLクエリが長時間（例えば7時間）実行されると、AEMは応答を停止する(NPR-33043)。

#### ユーザーインターフェイス {#ui-6481}

* 選択ダイアログを使用してパスを検索または参照する場合、選択ダイアログには、画像のみが表示されるのではなく、選択したJCRノードのすべてのコンテンツが表示されます(NPR-32712)。

#### 翻訳プロジェクト {#tranlation-6481}

* 翻訳ジョブの実行時にログに`NullPointerException`エラーが表示される(NPR-32220)。

#### 統合 {#integrations-6481}

* JSONのクロスサイトスクリプティング(NPR-32745)。

#### コミュニティ {#communities-6481}

* 作成者は、新しいグループを作成した後、 [!DNL Internet Explorer] 11の[!UICONTROL コミュニティグループ]セクションにリダイレクトされない(NPR-33202)。
* [!UICONTROL アクティビティストリーム]ページへのアクセス時にエラーが発生する(NPR-33152)。
* [!DNL Communities]グループを編集し、サムネール画像を変更しても、グループサムネール画像は更新されない(NPR-32603)。
* ユーザー生成コンテンツ(UGC)の通知と購読のバージョンを作成する際に、ソースページの誤ったIDが保存されます(CQ-4289703)。
* クロスサイトスクリプティングの問題(NPR-33212)。

#### ワークフロー {#workflow-6481}

* ユーザーが[!UICONTROL ダイアログ参加者ステップ]を含むワークフローを完了するとポップアップ表示されるダイアログボックスに表示されないコンポーネントがあります(NPR-32989)。

* 左側のレールの「[!UICONTROL タイムライン]」オプションの読み込みに、予想以上の時間がかかる(NPR-32850)。

#### フォーム {#forms-6481}

>[!NOTE]
>
>AEM Cumulative Fix Packには、AEM Formsの修正は含まれていません。 別の Forms アドオンパッケージを使用して配布されます。さらに、JEE上のAEM Formsの修正を含む累積的なインストーラーがリリースされました。 詳しくは、「 [AEM Formsアドオンパッケージのインストール](#install-aem-forms-add-on-package) 」および「 [AEM Forms JEEインストーラーのインストール](#install-aem-forms-jee-installer) 」を参照してください。

* Correspondence Management:ユーザーが[!DNL Word]ドキュメントからコンテンツを貼り付けると、テキストドキュメントフラグメントに書式が保持されない(NPR-33213)。
* アダプティブForms:アダプティブフォームの辞書の文字列に新しい行が`&#xa;`文字を辞書に追加する(NPR-33265)。
* アダプティブForms:ユーザーが複数の添付ファイルを含むアダプティブフォームを保存できない。(NPR-33214)
* アダプティブForms:Instance Managerクラスの`AddInstance`メソッドと`RemoveInstance`メソッドが、[!DNL Internet Explorer 11]に遅延読み込みフラグメントの動的な数のインスタンスを追加しない(NPR-33201)。
* アダプティブForms:[!DNL Sites]ページに埋め込まれたアダプティブフォームで有効になっている分析が、送信および放棄イベントのデータを記録しない(NPR-31359)。
* アダプティブForms:ユーザーが[!DNL Word]ドキュメントの内容をアダプティブフォームに貼り付けて送信すると、送信されたアダプティブフォームにはUnicode文字が含まれます。 また、PDFからPDF/Aへの変換は、Unicode文字が原因で失敗します(NPR-33348)。
* バックエンド統合：不正な非アクティブ状態が原因で更新トークンの有効期限が切れると、フォームデータモデルの要求が失敗する(NPR-33168)。
* ドキュメントサービス：[!DNL Linux]サーバー上の[!DNL WebLogic]のGibson jarが見つからないため、PDF変換サービスがPDFドキュメントをPostScriptに変換できない(NPR-33515、CQ-4292239)。
* ドキュメントサービス：ユーザーがテキストファイルをPDFに変換すると、日本語の文字が正しくレンダリングされない(NPR-33239)。
* GuideSOMProviderServlet(NPR-32701)と共に格納されたXSS。

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
>機能パックをAEM 6.4にインストールしているお客様向け。Adobeが提供するオプションの機能パックは、リリースバージョンとサービスパックに依存します。 機能パックがインストールされている場合は、AEMカスタマーケアチームに連絡して、AEM 6.4用のこの累積修正パックとの互換性を検証してください。

* AEM 6.4.8.4にはAEM 6.4.8.0が必要です。詳細な手順については、[アップグレードのドキュメント](../sites-deploying/upgrade.md)を参照してください。
* MongoDB と複数のインスタンスを含むデプロイメントでは、パッケージマネージャーを使用してオーサーインスタンスの 1 つに AEM 6.4.8.4 をインストールしてください。
* 累積修正パックをインストールする前に、AEMインスタンスのスナップショットまたは新しいバックアップがあることを確認してください。
* インストールする前にインスタンスを再起動してください。これは、インスタンスがまだ更新モードになっている場合（インスタンスが以前のバージョンから更新されたばかりの場合）にのみ必要ですが、インスタンスが長期間実行されている場合は、一般的に推奨されます。

>[!NOTE]
>
>AEM 6.4.8.4 パッケージを削除またはアンインストールすることはお勧めしません。

### 累積修正パックのインストール {#install-cumulative-fix-pack}

既存の AEM 6.4.8.0 インスタンスに累積修正パックをインストールするには、次の手順を実行します。

1. [ソフトウェアの配布](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq640/cumulativefixpack/aem-6.4.8-cfp-4.0.zip)リンクをクリックして、パッケージをダウンロードします。

1. [パッケージマネージャー](http://localhost:4502/crx/packmgr/index.jsp)を開き「**[!UICONTROL パッケージをアップロード]**」をクリックしてパッケージをアップロードします。

1. パッケージ名を選択して、「**[!UICONTROL インストール]**」をクリックします。

>[!NOTE]
>
>**6.4.8.4 のインストール中に、パッケージマネージャー UI のダイアログが途中で終了することがあります。**
>
>そのため、エラーログが安定するのを待ってから、インスタンスにアクセスすることをお勧めします。アップデータバンドルのアンインストールに関連する特定のログが表示されるのを待ってから、インストールが正常に完了するようにする必要があります。 通常は、Safari で発生しますが、任意のブラウザーで断続的に発生する可能性があります。

### 自動インストール {#auto-installation}

実行中のインスタンスに AEM 6.4.8.4 を自動的にインストールするには、次の 2 つの方法があります。

A.サーバーの実行中に、..*/crx-quickstart/install*&#x200B;フォルダーにパッケージを配置します。 パッケージは自動的にインストールされます。

B.パッケージマネージャーの[HTTP APIを使用します。](https://docs.adobe.com/content/docs/en/crx/2-3/how_to/package_manager.html)を使用して、ネストされたパッケージがインストールされるようにしてください。`cmd=install&recursive=true`

>[!NOTE]
>
>AEM 6.4.8.4 では、ブートストラップインストールをサポートしていません。

### インストールの検証 {#validate-install}

1. 製品情報ページ（*/system/console/productinfo*）のインストール済み製品には、更新されたバージョン文字列「Adobe Experience Manager, Version 6.4.8.4」が表示されます。
1. すべての OSGi バンドルは、OSGi コンソール（Web コンソールを使用：/system/console/bundles）で ACTIVE または FRAGMENT です。
1. OSGIバンドルorg.apache.jackrabbit.oak-coreは、バージョン1.8.17以降(Webコンソールを使用：/system/console/bundles)に置き換えます。

このリリースのAEM SitesおよびAssetsでの実行に関する認定済みプラットフォームを確認するには、[技術要件](../sites-deploying/technical-requirements.md)を参照してください。

>[!NOTE]
>パッケージが正常にインストールされると、**「Content Package AEM-6.4-Service-Pack-8 installed successfully.」など、コンテンツパッケージが正常にインストールされたことを示す情報メッセージが表示されます。**

### Dynamic Mediaビューアの更新(5.10.1) {#update-dynamic-media-viewers}

AEM 6.4.8.4には、Dynamic Mediaビューア(5.10.1)の新しいバージョンが含まれています。これにより、画像プリセットページで名前の重複を確認できます。 Dynamic Mediaのお客様は、次のコマンドを実行して、標準のビューアプリセットを最新の状態にすることをお勧めします。

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
1. [AEM Formsリリース](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html#forms-updates)に記載されている、お使いのオペレーティングシステム用の対応するフォームアドオンパッケージをダウンロードします。
1. 「[AEM formsアドオンパッケージのインストール](https://docs.adobe.com/content/help/en/experience-manager-64/forms/install-aem-forms/osgi-installation/installing-configuring-aem-forms-osgi.html#install-aem-forms-add-on-package)」の説明に従って、formsアドオンパッケージをインストールします。

### AEM Forms JEE インストーラーのインストール {#install-aem-forms-jee-installer}

>[!NOTE]
>
>JEE で AEM Forms を使用していない場合はスキップします。AEM Forms JEE の修正は別のインストーラーを介して配布されます。

AEM Forms JEE の累積インストーラーのインストールとデプロイメント後の設定について詳しくは、[AEM Forms JEE パッチインストーラー ](jee-patch-installer-64.md) を参照してください。

>[!NOTE]
>
>JEE上のFormsExperience Manager用の累積インストーラーをインストールしたら、最新のFormsアドオンパッケージをインストールし、`crx-repository\install`フォルダーからFormsアドオンパッケージを削除して、サーバーを再起動します。

### Uber Jar {#uber-jar}

AEM 6.4.8.4のUber Jarは、[Maven Centralリポジトリ](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.4.8.4/)で入手できます。

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
>UberJarおよびその他の関連アーティファクトは、AdobeのパブリックMavenリポジトリ(repo.adobe.com)ではなく、Maven Centralリポジトリで使用できます。 メインのUberJarファイルの名前が`uber-jar-<version>.jar`に変更されます。 その結果、`dependency`タグの値に`apis`を含む`classifier`は存在しません。

## 廃止される機能および削除された機能 {#removed-deprecated-features}

このセクションでは、AEM 6.4 で廃止される機能および削除された機能について説明します。

| 領域 | 機能 | 代替手段 | バージョン |
|---|---|---|---|
| Assets | サブアセットのタグアクションを管理 | 代替機能はありません | AEM 6.4.2.0 |
| Assets と Adobe Creative Cloud の統合 | [AEM／Creative Cloud フォルダー共有](https://docs.adobe.com/content/help/ja/experience-manager-64/assets/administer/aem-cc-folder-sharing-best-practices.html)は、クリエイティブユーザーに AEM のアセットへのアクセスを提供する方法として、AEM 6.2 で導入されました。Creative Cloud アプリケーションでリリースされた新しい機能である Adobe Asset Link では、ユーザーエクスペリエンスが大幅に向上し、Photoshop、InDesign、Illustrator 内から AEM のアセットへの直接アクセスが強化されています。アドビは、このフォルダー共有機能をさらに強化する予定はありません。この機能はAEMに含まれていますが、お客様は（置き換えを使用することを強くお勧めします）。 | Adobeアセットリンクまたはデスクトップアプリケーション。 詳細については、[AEM Creative Cloud の統合](/help/assets/aem-cc-integration-best-practices.md)記事を参照してください。 | AEM 6.4.4.0 |

## 既知の問題 {#known-issues}

* [!DNL Experience Manager] 6.4から[!DNL Experience Manager] 6.5にアップグレードすると、一部のバンドルのステータスが`Active`と表示されない場合があります。 最新の[!DNL Experience Manager] 6.5 Service Packをインストールして問題を解決します。

AEM 6.4.8.0 Service Packの既知の問題については、『AEM 6.4.8.0 Service Packリリースノート](sp-release-notes.md)』を参照してください。[

## OSGi バンドルとコンテンツパッケージが含まれています {#osgi-bundles-and-content-packages-included}

次のテキストドキュメントは、AEM 6.4.8.4に含まれているOSGiバンドルとコンテンツパッケージの一覧です。

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
