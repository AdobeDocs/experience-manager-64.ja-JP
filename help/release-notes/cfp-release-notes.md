---
title: AEM 6.4累積Fix Packリリースノート
description: Adobe Experience Manager6.4累積Fix Pack固有のリリースノート
contentOwner: AK
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: b698a1348df3ec2ab455c236422784d10cbcf7c2
workflow-type: tm+mt
source-wordcount: '2158'
ht-degree: 24%

---


# AEM 6.4累積Fix Packリリースノート {#aem-cumulative-fix-pack-release-notes}

## リリース情報 {#release-information}

| 製品 | **Adobe Experience Manager（AEM）6.4** |
|---|---|
| バージョン | 6.4.8.1 |
| 型 | 累積修正パック |
| 日付 | 2020年6月4日 |
| 前提条件 | [AEM 6.4 サービスパック 8（6.4.8.0）](sp-release-notes.md) |
| ダウンロード URL | AEM 6.4.8.1( [ソフトウェア配布版)](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq640%2Fcumulativefixpack%2Faem-6.4.8-cfp-1.0.zip) |

## AEM 6.4.8.1 に含まれる機能 {#what-s-included-in-aem}

AEM Cumulative Fix Pack 6.4.8.1は重要なアップデートで、2020年3月のAEM 6.4 Service Pack 8(6.4.8.0)の一般リリース以降の社内およびお客様向けの修正が含まれています。

AEMの累積Fix Pack 6.4.8.1は、AEM 6.4 Service Pack 8に依存します。 そのため、AEM 6.4 Service Pack 8をインストールした後で、AEM Cumulative Fix Pack 6.4.8.1パッケージをインストールする必要があります。

AEM 6.4.8.1の主な特徴は次のとおりです。

* パッケージ共有のAdobe Experience Managerとの統合を削除しました。
* 組み込み型のリポジトリ（Apache Jackrabbit Oak）をバージョン 1.8.21 に更新しました。

For information on CFP and other types of releases, see [AEM Update Release Vehicle Definitions](../sites-deploying/update-release-vehicle-definitions.md)

## 変更点の一覧 {#list-of-changes}

Adobe Experience Manager6.4.8.1では、次の問題が修正されました。

### Sites {#sites-6481}

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

### Assets {#assets-6481}

* リスト表示(NPR-33285)での選択の変更に従って、アセットの数は変わりません。

* 親ノード（子フォルダーが1つ表示される）を選択した後で子フォルダーを選択すると、「次へ」ボタンが有効になりません(NPR-33284)。

* タッチUIは、DMS7またはハイブリッドモードが有効な場合(NPR-33175)、リポジトリルートで読み取りアクセス権を持たないユーザーに表示されません（エラーが発生）。

* ダウンロードしたzipファイル(NPR-33150)で、フォルダー名やアセット名に含まれるGB18030文字が空白に変わります。

* 親フォルダー内にあるアセットの名前にドット `.` 文字が含まれたアセットをスマート切り抜きする際に、追加のフォルダーが作成されます(NPR-32755)。

* 遅延読み込みはトリガーされず、通知インボックス(NPR-32749)からタスクを確認するように選択した場合は、100以下のアセットが表示されます。

* coral-info(NPR-32510)の変更により、コレクションを共有するリンクページが破損しました。

* バルクアップロード中にアセットの処理が停止する(CQ-4293916)。

* Experience ManagerのSSRF脆弱性(NPR-33437)。

### プラットフォーム {#platform-6481}

* マップエントリが [!DNL Sling]`sling:match``/etc/maps` (NPR-33308)の下に作成された場合、フィルターは呼び出されません。
* すべてのフラッシュエージェントは、ページの非アクティブ化時にトリガされます(NPR-32941)。
* APIを使用してJavaScriptライブラリを縮小すると、ログファイルに、JavaScriptコードが厳密なモードに準拠していないことを示すエラーメッセージが表示されます。 `ScriptProcessor` APIには、厳密なモードを有効または無効にするオプションはありません。 (NPR-32746).
* SQLクエリが7時間など長い時間実行されると、AEMは応答を停止します(NPR-33043)。

### ユーザーインターフェイス {#ui-6481}

* 選択ダイアログを使用してパスを検索または参照する場合、選択ダイアログには、画像のみを表示するのではなく、選択したJCRノードのすべてのコンテンツが表示されます(NPR-32712)。

### 翻訳プロジェクト {#tranlation-6481}

* 翻訳ジョブの実行時にログに `NullPointerException` エラーが表示されます(NPR-32220)。

### 統合 {#integrations-6481}

* JSONのクロスサイトスクリプティング(NPR-32745)。

### Communities {#communities-6481}

* 作成者は、新しいグループを作成した後、11の [!UICONTROL コミュニティグループ][!DNL Internet Explorer] (NPR-33202)セクションにリダイレクトされません。
* [!UICONTROL アクティビティストリーム] ページ(NPR-33152)へのアクセス時にエラーが発生します。
* グループを編集してサムネール画像を変更しても、グループサムネール画像は更新されません(NPR-32603)。 [!DNL Communities]
* ユーザー生成コンテンツ(UGC)の通知と購読のバージョンを作成すると、ソースページの誤ったIDが保存されます(CQ-4289703)。
* クロスサイトスクリプティングの問題(NPR-33212)。

### ワークフロー {#workflow-6481}

* 一部のコンポーネントは、ユーザーが [!UICONTROL ダイアログ参加者の手順] (NPR-32989)を含むワークフローを完了するとポップアップするダイアログボックスに表示されません。

* 左側のレールの「 [!UICONTROL タイムライン] 」オプションの読み込みに予想以上に時間がかかります(NPR-32850)。

### フォーム {#forms-6481}

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


## Install 6.4.8.1 {#install}

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

* AEM 6.4.8.1 requires AEM 6.4.8.0. Please visit [upgrade documentation](../sites-deploying/upgrade.md) for detailed instructions.
* MongoDB と複数のインスタンスを含むデプロイメントでは、パッケージマネージャーを使用してオーサーインスタンスの 1 つに AEM 6.4.8.1 をインストールしてください。
* 累積修正パックをインストールする前に、AEMインスタンスのスナップショットまたは新規バックアップが必要です。
* インストールする前にインスタンスを再起動してください。これは、インスタンスがまだ更新モードになっている場合（インスタンスが以前のバージョンから更新されたばかりの場合）にのみ必要ですが、インスタンスが長期間実行されている場合は、一般的に推奨されます。

>[!NOTE]
>
>AEM 6.4.8.1 パッケージを削除またはアンインストールすることはお勧めしません。

### 累積Fix Packのインストール {#install-cumulative-fix-pack}

既存の AEM 6.4.8.0 インスタンスに累積修正パックをインストールするには、次の手順を実行します。

1. 「 [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq640/cumulativefixpack/aem-6.4.8-cfp-1.0.zip) 」リンクをクリックして、パッケージをダウンロードします。

1. Open [Package Manager](http://localhost:4502/crx/packmgr/index.jsp) and click **[!UICONTROL Upload Package]** to upload the package.

1. Select the package name and click **[!UICONTROL Install]**.

>[!NOTE]
>
>**6.4.8.1 のインストール中に、パッケージマネージャー UI のダイアログが途中で終了することがあります。**
>
>そのため、エラーログが安定するのを待ってから、インスタンスにアクセスすることをお勧めします。ユーザーは、アップデーターバンドルのアンインストールに関連する特定のログを待ってから、インストールが正常に行われることを確認する必要があります。 通常は、Safari で発生しますが、任意のブラウザーで断続的に発生する可能性があります。

### 自動インストール {#auto-installation}

実行中のインスタンスに AEM 6.4.8.1 を自動的にインストールするには、次の 2 つの方法があります。

A. Place the package into ..*/crx-quickstart/install* folder while the server is running. パッケージは自動的にインストールされます。

B. Use the [HTTP API from Package Manager](https://docs.adobe.com/content/docs/en/crx/2-3/how_to/package_manager.html) - make sure you use `cmd=install&recursive=true` - so the nested package are installed.

>[!NOTE]
>
>AEM 6.4.8.1 では、ブートストラップインストールをサポートしていません。

### インストールの検証 {#validate-install}

1. 製品情報ページ（*/system/console/productinfo*）のインストール済み製品には、更新されたバージョン文字列「Adobe Experience Manager, Version 6.4.8.1」が表示されます。
1. すべての OSGI バンドルは、OSGI コンソール（Web コンソールを使用：/system/console/bundles）で ACTIVE または FRAGMENT です。
1. OSGIバンドルorg.apache.jackrabbit.oak-coreがバージョン1.8.17以降に搭載されています(Webコンソールを使用：/system/console/bundles)。

To determine the certified platform for running with this release of AEM Sites and Assets, see [Technical Requirements](../sites-deploying/technical-requirements.md).

>[!NOTE]
>On successful installation of the package, an informational message appears indicating that the content package has installed successfully, such as **&quot;Content Package AEM-6.4-Service-Pack-7 installed successfully.&quot;**

### ダイナミックメディアビューアの更新(5.10.1) {#update-dynamic-media-viewers}

AEM 6.4.8.1には、画像プリセットページの重複名のチェックを有効にする、新しいバージョンのダイナミックメディアビューア(5.10.1)が含まれています。 ダイナミックメディアのお客様には、次のコマンドを実行して、初期設定のビューアプリセットを最新の状態にすることをお勧めします。

`curl -u admin:admin http://localhost:4502/libs/settings/dam/dm/presets/viewer.pushviewerpresets`

新しいビューアプリセットを/confの場所にコピーします。

### AEM Forms アドオンパッケージのインストール {#install-aem-forms-add-on-package}

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

AEM Forms JEE の累積インストーラーのインストールとデプロイメント後の設定について詳しくは、[AEM Forms JEE パッチインストーラー 0016](https://helpx.adobe.com/jp/aem-forms/quick-fixes/6-4/jee-patch-0016.html) を参照してください。

### Uber Jar {#uber-jar}

The Uber Jar for AEM 6.4.8.1 is available in the [Adobe Public Maven repository](https://repo.adobe.com/nexus/content/groups/public/com/adobe/aem/uber-jar/6.4.8.1/).

To use Uber Jar in a Maven project, refer to the article, [How to use Uber jar](../sites-developing/ht-projects-maven.md) and include the following dependency in your project POM:

```shell
<dependency>
      <groupId>com.adobe.aem</groupId>
      <artifactId>uber-jar</artifactId>
      <version>6.4.8.1</version>
      <classifier>apis</classifier>
      <scope>provided</scope>
</dependency>
```

## 廃止される機能および削除された機能 {#removed-deprecated-features}

このセクションでは、AEM 6.4 で廃止される機能および削除された機能について説明します。

| 領域 | 機能 | 代替手段 | バージョン |
|---|---|---|---|
| Assets | サブアセットのタグアクションの管理 | 代替機能はありません | AEM 6.4.2.0 |
| Assets と Adobe Creative Cloud の統合 | [AEM 6.2では、クリエイティブユーザーにAEMのアセットへのアクセスを許可する方法として、AEMからCreative Cloudへのフォルダ共有が導入されました。](https://docs.adobe.com/content/help/en/experience-manager-64/assets/administer/aem-cc-folder-sharing-best-practices.html) Creative Cloud アプリケーションでリリースされた新しい機能である Adobe Asset Link では、ユーザーエクスペリエンスが大幅に向上し、Photoshop、InDesign、Illustrator 内から AEM のアセットへの直接アクセスが強化されています。アドビは、このフォルダー共有機能をさらに強化する予定はありません。この機能はAEMに含まれていますが、お客様には交換の使用を強くお勧めします。 | Adobeアセットリンクまたはデスクトップアプリ 詳細については、[AEM Creative Cloud の統合](/help/assets/aem-cc-integration-best-practices.md)記事を参照してください。 | AEM 6.4.4.0 |

## 既知の問題 {#known-issues}

* AEM 6.4.8.1のインストール時に、バージョン83のアップデートが原因でパッケージの構築に問題が発生して [!DNL Chrome] います。 問題を解決するには、 [!DNL Internet Explorer] およびなどの他の利用可能なブラウザー、 [!DNL Firefox]またはAEM標準のパッケージインストールオプションを使用します。 この問題はAEM 6.4.8.1のインストール後に解決されます。

* AEMの既定のメール送信者を使用してリモートSMTPサーバーに電子メールを送信できません。TLS v1.2を使用した通信のみが可能です。バンドルを削除し、更新して問題 `javax.mail:mail:1.5.0-b01` を解決し `system/console` てください。

AEM 6.4.8.0 Service Packの既知の問題については、『 [AEM 6.4.8.0 Service Packリリースノート](sp-release-notes.md)』を参照してください。

## OSGi バンドルとコンテンツパッケージが含まれています {#osgi-bundles-and-content-packages-included}

次のテキストドキュメントリストは、AEM 6.4.8.1に含まれるOSGiバンドルとコンテンツパッケージを示します。

AEM 6.4.8.1 に含まれている OSGi バンドルの一覧

[ファイルを入手](assets/6.4.8.1_osgi_bundles.txt)

AEM 6.4.8.1 に含まれているコンテンツパッケージの一覧

[ファイルを入手](assets/6.4.8.1_content_packages.txt)

## 参考リソース {#helpful-resources}

* [AEM 6.4 リリースノート](../release-notes/release-notes.md)
* [AEM 製品ページ](https://www.adobe.com/solutions/web-experience-management.html)
* [AEM 6.4 ドキュメント](https://helpx.adobe.com/jp/support/experience-manager/6-4.html)
* [Adobe優先度の製品アップデートの購読](https://www.adobe.com/subscription/priority-product-update.html)

## 制限付きサイト {#restricted-sites-new}

以下のサイトは既存ユーザーのみが参照できます。アクセス権が必要な既存ユーザーの方は、アドビのアカウントマネージャーまでお問い合わせください。

* [licensing.adobe.com からの製品ダウンロード](https://licensing.adobe.com/)
* [カスタマーサポートに連絡](https://docs.adobe.com/content/help/en/customer-one/using/home.html)
