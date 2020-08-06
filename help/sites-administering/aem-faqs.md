---
title: AEM FAQ
seo-title: AEM 6.4 に関する一般的な質問
description: AEM の一般的なワークフローの理解と設定、または AEM で発生する一般的な問題のトラブルシューティングに役立つ FAQ です。
seo-description: AEM の一般的なワークフローの理解と設定、または AEM で発生する一般的な問題のトラブルシューティングに役立つ FAQ です。
uuid: af197bcc-2c61-4c64-b781-f24d83c27c82
contentOwner: jsyal
discoiquuid: c66b65af-443f-4fc2-b775-9f4e3c60285a
translation-type: tm+mt
source-git-commit: f5b45b2c8bfcf9d82ddc08b05b5fff22937fa9fd
workflow-type: tm+mt
source-wordcount: '1545'
ht-degree: 49%

---


# AEM FAQ{#aem-faqs}

AEMのトラブルシューティングと設定に関する問題の回答を得るには、このページに従ってください。

## Sites {#sites}

### How do I configure binary-less distribution? {#how-do-i-configure-binary-less-distribution}

バイナリレスディストリビューションは、共有データストアにわたる開発でサポートされ、Vault ベースのディストリビューションパッケージエクスポーター（ファクトリ PID：`org.apache.sling.distribution.serialization.impl.vlt.VaultDistributionPackageBuilderFactory`）パッケージビルダーを活用するエージェントが関係します。

バイナリレスモードを有効にすると、ディストリビュートされたコンテンツパッケージに、実際のバイナリではなく、バイナリへの参照が含まれます。

### バイナリレスディストリビューションを有効にする方法を教えてください。 {#how-do-i-enable-binary-less-distribution}

バイナリレスディストリビューションを有効にするには、共有 BLOB ストアと共にデプロイします。\
Check the `useBinaryReferences` property in the OSGI configuration with the factory PID ( `org.apache.sling.distribution.serialization.impl.vlt.VaultDistributionPackageBuilderFactory`*)*that your agent is using.

### How can I customize the error messages while navigating page hierarchy in AEM sites console? {#how-can-i-customize-the-error-messages-while-navigating-page-hierarchy-in-aem-sites-console}

（Chrome ブラウザーの）Network パネルの個人設定を確認します（JS は縮小されていません）。

`Initiator` 列を表示して、リクエストのイニシエーターを判別します。AJAX 呼び出しがおこなわれたファイルおよび行番号がわかります。次に、エラー処理関数をトレースし、要件に応じてエラーメッセージを変更できます。

### 言語コピーを作成する際に AEM で Content-Authors の権限を有効にする方法を教えてください。 {#how-to-enable-permissions-while-creating-language-copy-for-content-authors-in-aem}

To create language copy feature, content-authors need permissions at `/content/projects` location.

If one requires the authors to manage projects as well, then the workaround is to add the author to `project-administrators` group.

### How to change the format while creating Language Copy for a project? {#how-to-change-the-format-while-creating-language-copy-for-a-project}

翻訳プロジェクトを作成する前に、ルート内部に言語ルートおよび言語コピーを作成します。

例：\
Create a language root at `/content/geometrixx` with name as `fr_LU` (and title as French (Luxembourg)). 次に、参照パネルからページの言語コピーを作成し、の `Create structure only` オプションに移動し `Create & Translate`ます。 最後に、翻訳プロジェクトを作成し、言語コピーを翻訳ジョブに追加します。

詳しくは、次の追加リソースを参照してください。

* [翻訳するコンテンツの準備](/help/sites-administering/tc-prep.md)
* [翻訳プロジェクトの管理](/help/sites-administering/tc-manage.md)

### ログイン試行や ACL／権限の変更といった AEM の機能を監査する方法を教えてください。 {#how-to-audit-aem-capabilities-such-as-login-attempts-and-acl-or-permission-changes}

トラブルシューティングと監査の質を高めるために、管理に関係する変更を記録する機能が追加されました。By default, the information is logged in the `error.log` file. 監視を容易にするために、この情報を別のログファイルにリダイレクトすることをお勧めします。\
出力を別のログファイルにリダイレクトする方法については、[AEM でのユーザー管理操作を監査する方法](/help/sites-administering/audit-user-management-operations.md)を参照してください。

### How to enable SSL by default? {#how-to-enable-ssl-by-default}

Adobe Experience Manager（AEM）6.4 には SSL ウィザードが付属し、Jetty および Granite Jetty SSL のサポートを設定するユーザーインターフェイスが備わっています。

デフォルトの SSL を有効にする方法については、[デフォルトの SSL](/help/sites-administering/ssl-by-default.md) を参照してください。

### AEM のコンテンツサービスをモバイルアプリから使用する場合に推奨されるアーキテクチャは何ですか。理想的には React Native ですか。 {#what-is-the-recommended-architecture-when-using-aem-s-content-services-from-a-mobile-app-ideally-react-native}

Content ServicesはSlingモデルに基づいており、AEMの開発者は、エクスポートされる各コンポーネントに対してSlingモデルのポジションを提供する必要があります。

AEM コンテンツサービスを React アプリケーションから使用する方法については、[AEM コンテンツサービスの使用準備](https://helpx.adobe.com/jp/experience-manager/kt/sites/using/content-services-tutorial-use.html)のチュートリアルを参照してください。

Also, if the developers want to export a tree of components they can also implement the `ComponentExporter` and `ContainerExporter` interfaces as well as use the `ModelFactory` to iterate over the child components and return their model representation. 以下のリソースを参照してください。

[1] Adobe- [Marketing-Cloud/aem-core-wcm-components](https://github.com/Adobe-Marketing-Cloud/aem-core-wcm-components/blob/master/bundles/core/src/main/java/com/adobe/cq/wcm/core/components/internal/models/v1/PageImpl.java#L245)

[2] [Apache Sling :: Slingモデル](https://sling.apache.org/documentation/bundles/models.html)

### How to disable AEM 6.4 survey pop-up? {#how-to-disable-aem-survey-pop-up}

使用状況に関する統計情報の収集をオプトインするには、タッチ UI または Web コンソールを使用します。詳しくは、[集計した使用状況の統計の収集をオプトインする方法](/help/sites-deploying/opt-in-aggregated-usage-statistics.md)を参照してください。

### AEM 6.4 にアップグレードするための主な機能を説明しているリソースを教えてください。 {#is-there-a-good-resource-that-highlights-the-key-features-for-upgrading-to-aem}

Refer to [Understanding Reasons to Upgrade AEM](https://helpx.adobe.com/experience-manager/kt/platform-repository/using/upgrade-aem-article-understand.html) that describes high-level breakdown of key features for customers considering upgrading to the latest version of Adobe Experience Manager.

### PorterStemフィルタを使用するAEMインスタンスを設定する方法を教えてください。 {#how-to-configure-an-aem-instance-to-use-the-porterstem-filter}

PorterStemフィルターは、英語用のPorter Stemming Algorithmを適用します。 結果は、Snowball Porter Stemmerを *language=&quot;English&quot;引数と共に使用した場合と似ています* 。 ただし、このステマーはJavaで直接コード化され、Snowballに基づいているわけではありません。 保護された単語のリストは受け入れられず、英語のテキストにのみ適しています。

Oakは、AEMで使用するLucene提供のアナライザ構成要素のセットを公開します。 フィルターの使用方法については、『 **シンプル検索導入ガイド** 』の「 [Apache Oak Analyzers](https://helpx.adobe.com/experience-manager/kt/sites/using/search-tutorial-develop.html)」を参照してください。

### 完全な再インデックスの実行方法 {#how-to-perform-a-full-re-indexing}

再インデックスに着手する前には必ず、AEM の全体的なパフォーマンスに対する影響を適切に検討し、アクティビティが少ない期間やメンテナンスウィンドウ中に再インデックスを実行する必要があります。

再インデックスの理由については、 [クエリとインデックス作成のベストプラクティス](/help/sites-deploying/best-practices-for-queries-and-indexing.md) （英語）を参照してください。

### デザインインポーターで縮小JSライブラリをサポートしていますか？ {#do-we-support-minified-js-libs-in-design-importer}

AdobeGranite HTML Library ManagerのJSプロセッサのデフォルトの設定プロパティを ***min:gccに変更する必要があります***。 デザインパッケージを正常に読み込むには、クライアント側ライブラリに縮小済みのサードパーティライブラリを含めることをお勧めします。

## Assets {#assets}

### Why the Assets workflow repeats itself while uploading MP4 files (for example, using drag-and-drop method)? {#why-the-assets-workflow-repeats-itself-while-uploading-mp-files-for-example-using-drag-and-drop-method}

ムービーファイルをアップロードするユーザーが asset ノード以下の削除権限を持っていない場合、削除チャンクノードは失敗し、アップロードが再開します。

### AEM 6.4 で一度に操作できるデジタルアセットの最大数を教えてください。 {#what-is-the-maximum-number-of-digital-assets-that-can-be-operated-with-aem-at-a-time}

Adobe Experience Manager（AEM）6.4 では現在、一度に 2 GB のアセットをアップロードできます。

AEM 6.4 で操作できるアセットの最大数について詳しくは、[Assets サイジングガイド](/help/assets/assets-sizing-guide.md)を参照してください。

### 言語コピーを作成する際の OOTB 設定のデフォルト設定を教えてください。 {#what-are-the-default-settings-for-ootb-configurations-while-creating-language-copy}

クラシック UI を利用して言語コピーを作成するときは、Assets は新しい言語階層下に移動されるのではなく、言語マスターから使用されます。

一方で、タッチ UI を利用して言語コピーを作成するときは（**参照**／**言語コピーを更新**）、新しい DAM フォルダーが新しい言語下に作成され、アセットはそのフォルダーから参照されます。

これは OOTB 設定のデフォルト設定です。翻訳設定で「**ページのアセットを翻訳**」を「**翻訳しない**」に設定できます。\
AEM 6.4 の場合は、**ツール**／**クラウドサービス**／**翻訳クラウドサービス**&#x200B;を選択して設定します。

### How to disable an AEM component causing exponential growth for the AEM SegmentStore (AEM 6.3.1.1)? {#how-to-disable-an-aem-component-causing-exponential-growth-for-the-aem-segmentstore-aem}

OSGi Component Disabler を無効にできます。このサービスの使用方法については、[OSGi Component Disabler](https://adobe-consulting-services.github.io/acs-aem-commons/features/osgi-disablers/component-disabler/index.html) を参照してください。

回避策として、AEM が再開するたびに、UI または `curl` コマンド（以下の例を参照）を使用して、このコンポーネントを手動で無効にすることもできます。

`curl -u admin:$(pass CQ_Admin) 'http://localhost:4502/system/console/components/com.day.cq.analytics.sitecatalyst.impl.importer.ReportImporter' --data 'action=disable'`

### How to configure Asset Insights with AEM 6.4 instance? {#how-to-configure-asset-insights-with-aem-instance}

To setup and configure Asset Insights for Experience Manager deployed via Adobe Activation (DTM), refer to [Set up Asset Insights with AEM Assets](https://helpx.adobe.com/experience-manager/kt/assets/using/asset-insights-tutorial-setup.html).

### How to customize admin consoles? {#how-to-customize-admin-consoles}

AEMには様々なメカニズムが用意されており、オーサリングインスタンスのコンソールとページオーサリング機能をカスタマイズできます。
To learn how to create a custom console and customize a default view for a console, refer to [Customizing the Consoles](/help/sites-developing/customizing-consoles-touch.md).

### What is the difference between CoralUI 2 and CoralUI 3-based components? {#what-is-the-difference-between-coralui-and-coralui-based-components}

A new set of Sling components of Granite UI Foundation is created for Coral3 and is located under [/libs/granite/ui/components/coral/foundation.](https://helpx.adobe.com/jp/experience-manager/6-4/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/components/coral/foundation/server.html)CoralUI 2 ベースのコンポーネント用と CoralUI 3 ベースのコンポーネント用のセットが1 つずつあります。新しいセットは、古いセットをただコピーして貼り付けたものではなく、（合理化、廃止予定の機能を削除するなど）クリーンアップしたものです。そのため、ページは CoralUI 3 ベースまたは CoralUI 2 ベースのいずれかのセットのみを使用することをお勧めします。

To learn more in detail, refer to [Migration Guide to CoralUI 3-based](https://helpx.adobe.com/jp/experience-manager/6-4/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/components/legacy/coral2/migration.html).

### How to customize the search component in AEM Assets? {#how-to-customize-the-search-component-in-aem-assets}

To learn about search boost/ranking and further implementation information, refer to [Simple search implementation guide.](https://helpx.adobe.com/experience-manager/kt/sites/using/search-tutorial-develop.html)

簡易検索の実装は、2017 Summit lab AEM Search Demystified の資料です。

### お客様がAEMでサイトライセンスのみを購入した場合、アセットにアクセスできますか。 {#if-a-customer-buys-only-sites-license-in-aem-do-they-still-have-access-to-assets}

いいえ。お客様はアセット（またはサイト以外）にアクセスできません。 すべてのAdobe Experience Manager(AEM)オンプレミスがJARに含まれている場合でも、お客様は、契約でライセンスを受けるJAR内のコンポーネントに対してのみアクセスを許可されます。 他のコンポーネントを調査する場合は、AEMの体験版プログラムを最大45日間使用するか、$0の販売注文に署名して、Assetsなどの名前付きコンポーネントを評価（実稼働での使用なし）することを承認できます。

AEMオンプレミスソフトウェアとAdobe Managed Servicesについて詳しくは、次のリソースを参照してください。

* [Adobe Experience Managerオンプレミスソフトウェア](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-on-premise.html)

* [Adobe Experience ManagerManaged Services](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-managed-services.html)

### 顧客は、ページやアセットのデフォルトのプロパティをどのように拡張できるか。 {#how-to-extend-default-properties-page-or-asset}

ページまたはアセットのデフォルトプロパティの拡張については、次のリソースを参照してください。

* [アセット内のメタデータスキーマ](/help/assets/metadata-schemas.md)
* [ページプロパティのビューのカスタマイズ](/help/sites-developing/page-properties-views.md)
