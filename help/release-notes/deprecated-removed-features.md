---
title: 廃止される機能および削除された機能
description: リリースノート（Adobe Experience Manager 6.4 の廃止される機能および削除された機能）
translation-type: tm+mt
source-git-commit: 5b00783e4471a6b142ab17a7bc4a647ab04aec5f
workflow-type: tm+mt
source-wordcount: '1281'
ht-degree: 45%

---


# 廃止される機能および削除された機能 {#deprecated-and-removed-features}

アドビでは、製品の機能を絶えず評価して、常に後方互換性を慎重に考慮しながら、古い機能を作成し直したり、より近代的な機能に置き換えて、お客様にとっての全体的な価値を向上させています。

近い将来おこなわれる AEM 機能の削除や置換を通知するため、次のルールが適用されます。

1. まず、非推奨（廃止予定）の発表がおこなわれます。非推奨ですが、機能は引き続き利用できますが、これ以上強化されることはありません。
1. 廃止された機能の削除は、早ければ、次のメジャーリリースでおこなわれます。削除の実際の期日が発表されます。

このプロセスにより、機能が実際に削除されるまでに、非推奨（廃止予定）の機能の新しいバージョンまたは後継機能にお客様が実装を合わせるためのリリースサイクルが少なくとも 1 回あります。

## 非推奨（廃止予定）の機能 {#deprecated-features}

次の表は、AEM 6.4で非推奨とマークされたリスト機能と機能を示しています。一般に、将来のリリースで削除される予定の機能は、非推奨となる最初に設定され、代わりの機能が提供されます。

現在のデプロイメントでその機能を利用しているかどうかを確認し、提示される代替手段を使用するために実装の変更を計画するようにお勧めします。

<!-- TBD: This MD table is a replacement of the HTML table below. However, it generates validation error hence commenting and replacing with inline text. Restore if required. -->

| 領域 | 機能 | 代替手段 |
|---|---|---|
| UI | クラシック UI の機能がさらに強化される予定はありません。AEM 6.4 にはクラシック UI が含まれており、以前のリリースからアップグレードするお客様はクラシック UI をそのまま使用し続けることができます。クラシック UI は廃止中は引き続き完全にサポートされます。 <ul> <li>`/libs/cq/core/content/welcome.html` </li> <li> `/siteadmin` </li> <li> `/damadmin` </li> <li> `/mcmadmin` </li> <li> `/inbox` </li> <li> `/tagging` </li> <li> `/cf#` (ページエディター) </li><li> `/libs/launches/content/admin.html` </li> <li> `/libs/cq/workflow/content/console.html` </li> </ul> | 新しい AEM UI に切り替えることをお勧めします。 |
| コンポーネント | 以下の基盤コンポーネントの機能がさらに強化される予定はありません。AEM 6.4にはFoundation Componentsが含まれており、以前のリリースからアップグレードしたお客様は、これらをそのまま使用できます。 非推奨の間も、Foundation Componentsは完全にサポートされたままになります。 <ul> <li> foundation/components/account/accountname </li> <li> foundation/components/account/actions </li> <li> foundation/components/account/passwordreset </li> <li> foundation/components/account/requestconfirmation </li> <li> foundation/components/adaptiveimage </li> <li> foundation/components/assetsharepage </li> <li> foundation/components/breadcrumb </li> <li> foundation/components/form/creditcard </li> <li> foundation/components/listchildren </li> <li> foundation/components/login </li> <li> foundation/components/logo </li> <li> foundation/components/mobilefooter </li> <li> foundation/components/mobileimage </li> <li> foundation/components/mobilelist </li> <li> foundation/components/mobilelogo </li> <li> foundation/components/mobilereference </li> <li> foundation/components/mobiletextimage </li> <li> foundation/components/mobiletopnav </li> <li> foundation/components/search </li> <li> foundation/components/sitemap </li> <li> foundation/components/table </li> <li> foundation/components/toolbar </li> <li> foundation/components/topnav </li> <li> foundation/components/userinfo </li> </ul> | 今後のプロジェクトには、コアコンポーネントを使用することをお勧めします。既存のサイトを変更する必要はありません。 |
| コンポーネント | 以下の基盤コンポーネントの機能がさらに強化される予定はありません。AEM 6.4にはFoundation Componentsが含まれており、以前のリリースからアップグレードしたお客様は、これらをそのまま使用できます。 非推奨の間も、Foundation Componentsは完全にサポートされたままになります。 <ul><li>foundation/components/timing</li></ul> | Adobeは、交換を行う予定はありません。 |
| ポータルDirector | ポータル・Directorは、サード・パーティ・サーバのポートレットを介してAEMコンテンツをホストする機能のセットです。 Adobeは、以下に示す場所で、ポータルDirector機能をさらに強化する予定はありません。 AEM 6.4にはポータルDirectorが含まれており、お客様は以前のリリースからアップグレードした場合もそのまま使用できます。 Portal Directは、非推奨の間も完全にサポートされます。 <ul><li>/libs/portal/director</li></ul> | Adobeは、交換を行う予定はありません。 |
| ポートレットコンポーネント | /foundation/components/portletのポートレットコンポーネントを使用すると、AEMでJSR Portletsをコンポーネントとしてホストできます。 Adobeは、Portlet Component機能をさらに拡張する予定はありません。 AEM 6.4にはPortlet Componentが含まれており、お客様は以前のリリースからアップグレードした場合でも、これをそのまま使用できます。 Portlet Componentは、非推奨の間も完全にサポートされます。 | Adobeは、交換を行う予定はありません。 |
| フォーム | Adobe Central 製品がサポートされなくなったので、Adobe Central Migration Bridge サービスのサポートは廃止されました。 | 代替機能はありません |
| フォーム | クエリおよびOperationOptionsでのJSONObjectの使用を廃止しました。 以下のAPIは廃止されました。 <ul><li>`setArguments(JSONObject arguments)`</li><li> `JSONObject getArguments()`</li><li>`OperationOptions(String operationId, JSONObject arguments)`</li><li>`JSONObject getArguments()`</li><li> `void setArguments(JSONObject arguments)`</li></ul> | `IValueMap` APIを使用する |
| フォーム | Central Migration Bridgeサービスが廃止されました。 | 置き換えは提供されません。 |
| Assets | アセットのオフロードは、AEM 6.4以降で非推奨となりました。 |  |
| 開発者向け | Lodash/underscoreクライアントライブラリ。 Adobeは、配布版(Quickstart)の一部として出荷されるLodash/underscoreクライアントライブラリの保守と更新を今後行う予定はありません | Adobeでは、コードにLodash/underscoreを必要とする場合でも、プロジェクトのコードベースに追加することをお勧めします。 |

<!-- Original HTML table that came from helpx during migration.

<table> 
 <tbody>
  <tr>
   <td>Area</td> 
   <td>Feature</td> 
   <td>Replacement</td> 
  </tr>
  <tr>
   <td>UI</td> 
   <td><p>Adobe does not plan to make further enhancements to the Classic UI. AEM 6.4 has the Classic UI included, and customers upgrading from earlier releases can keep using it as is. Note that Classic UI remains fully supported while being deprecated. </p> 
    <ul> 
     <li>/libs/cq/core/content/welcome.html</li> 
     <li>/siteadmin</li> 
     <li>/damadmin</li> 
     <li>/mcmadmin</li> 
     <li>/inbox</li> 
     <li>/tagging</li> 
     <li>/cf# (Page Editor)</li> 
     <li>/libs/launches/content/admin.html</li> 
     <li>/libs/cq/workflow/content/console.html</li> 
    </ul> </td> 
   <td><p>Customers are advised to switch to use the new AEM UI.</p> <p> </p> </td> 
  </tr>
  <tr>
   <td>Components</td> 
   <td><p>Adobe does not plan to make further enhancements to the Foundation Components listed below. AEM 6.4 has the Foundation Components included, and customers upgrading from earlier releases can keep using them as is. Note that Foundation Components remain fully supported while being deprecated. </p> 
    <ul> 
     <li>foundation/components/account/accountname</li> 
     <li>foundation/components/account/actions</li> 
     <li>foundation/components/account/passwordreset</li> 
     <li>foundation/components/account/requestconfirmation</li> 
     <li>foundation/components/adaptiveimage</li> 
     <li>foundation/components/assetsharepage</li> 
     <li>foundation/components/breadcrumb</li> 
     <li>foundation/components/form/creditcard</li> 
     <li>foundation/components/listchildren</li> 
     <li>foundation/components/login</li> 
     <li>foundation/components/logo</li> 
     <li>foundation/components/mobilefooter</li> 
     <li>foundation/components/mobileimage</li> 
     <li>foundation/components/mobilelist</li> 
     <li>foundation/components/mobilelogo</li> 
     <li>foundation/components/mobilereference</li> 
     <li>foundation/components/mobiletextimage</li> 
     <li>foundation/components/mobiletopnav</li> 
     <li>foundation/components/search</li> 
     <li>foundation/components/sitemap</li> 
     <li>foundation/components/table</li> 
     <li>foundation/components/toolbar</li> 
     <li>foundation/components/topnav</li> 
     <li>foundation/components/userinfo</li> 
    </ul> </td> 
   <td>Customers are advised to use the Core Components for future projects. Existing sites do not need to be changed.</td> 
  </tr>
  <tr>
   <td>Components</td> 
   <td><p>Adobe does not plan to make further enhancements to the Foundation Components listed below. AEM 6.4 has the Foundation Components included, and customers upgrading from earlier releases can keep using them as is. Note that Foundation Components remain fully supported while being deprecated.</p> 
    <ul> 
     <li>foundation/components/timing</li> 
    </ul> </td> 
   <td>At the point of writing, it's not planned to provide a replacement.</td> 
  </tr>
  <tr>
   <td>Portal Director</td> 
   <td><p>The Portal Director is a set of features, that enables the hosting of AEM content via Portlet in 3rd party servers.</p> <p>Adobe does not plan to make further enhancements to the Portal Director feature under the location listed below. AEM 6.4 has the Portal Director included, and customers upgrading from earlier releases can keep using it as is. Note that Portal Direct remains fully supported while being deprecated.</p> 
    <ul> 
     <li>/libs/portal/director</li> 
    </ul> </td> 
   <td>At the point of writing, it's not planned to provide a replacement.</td> 
  </tr>
  <tr>
   <td>Portlet Component</td> 
   <td><p>Portlet Components under /foundation/components/portlet enables the hosting of JSR Portlets in AEM as components.</p> <p>Adobe does not plan to make further enhancements to the Portlet Component feature. AEM 6.4 has the Portlet Component included, and customers upgrading from earlier releases can keep using it as is. Note that Portlet Component remains fully supported while being deprecated.</p> </td> 
   <td>At the point of writing, it's not planned to provide a replacement.</td> 
  </tr>
  <tr>
   <td>Forms</td> 
   <td><p>Support for Adobe Central Migration Bridge service has been deprecated as Adobe Central product is no longer supported.</p> </td> 
   <td>No replacement </td> 
  </tr>
    <tr>
   <td>Forms</td> 
   <td><p>Deprecated use of JSONObject in Query and OperationOptions. The following APIs are deprecated:
   <ul><li>setArguments(JSONObject arguments)</li><li>JSONObject getArguments()</li><li>OperationOptions(String operationId, JSONObject arguments</li><li>JSONObject getArguments()</li><li>void setArguments(JSONObject arguments)</li></ul>
   </p> </td> 
   <td>Use the IValueMap API </td> 
  </tr>
  <tr>
   <td>Forms</td> 
   <td><p>Deprecated Central Migration Bridge service</p> </td> 
   <td> No replacement </td> 
  </tr>
  <tr>
   <td>Assets</td> 
   <td><p>Assets Offloading has been deprecated starting with AEM 6.4</p> </td> 
   <td> </td> 
  </tr>
 </tbody>
</table>
-->

## 削除された機能 {#removed-features}

次の表に、AEM 6.4から削除されたリスト機能と機能を示します。以前のリリースでは、これらの機能が
非推奨です。

| 領域 | 機能 | 代替手段 |
|---|---|---|
| Analytics の Activity Map | AEM に組み込まれている Activity Map のバージョン。 | Adobe Analytics API 内のセキュリティ変更により、AEM に含まれているバージョンの Activity Map は使用できなくなりました。現在は、Adobe Analytics](https://docs.adobe.com/content/help/ja/analytics/analyze/activity-map/getting-started/get-started-users/activitymap-install.translate.html)が提供する[ActivityMapプラグインを使用する必要があります。 |
| コンポーネント —Forms | フォームキャプチャ（foundation/components/form/captcha） | Google の ReCaptcha コンポーネントを代わりに使用します。 |
| コンポーネント | Slideshow（foundation/components/slideshow） | 代替機能はありません。 |
| コンポーネント | Flash（foundation/components/flash） | 代替機能はありません。 |
| コンポーネント | ビデオコンポーネントでの SWF ファイルの再生はサポートされなくなりました。 （foundation/components/video） | Flash ベースでないビデオ形式を使用します。 |
| コンポーネント | 製品テーブル（commerce/components/product_table） | 代替機能はありません。 |
| タスク管理 | クラシック UI タスク管理（/libs/cq/taskmanagement/content/taskmanager.html） | 6.0 以降、廃止されました。ワークフロー UI に統合されている新しいタスク管理機能を使用します。 |
| ワークフロー | 5.6 から 6.2 までで使用された通知 UI （/libs/cq/workflow/content/notifications.html） | ワークフローインボックス（/aem/inbox） |
| フォーム | PDF Generator を使用して PDF を PDF/E-1 形式に書き出す機能は削除されました。 | PDF Generatorでは、引き続きPDFからPDF/A-1a/b、PDF/A-2a/bおよびPDF/A-3a/b形式への書き出しがサポートされます。 |
| フォーム | ドキュメントフラグメント内では画像がサポートされなくなりました。 | インタラクティブコミュニケーションでは、印刷および Web チャネルで画像を直接使用できます。 |
| フォーム | アウトオブザプレースアップグレード | アウトオブプレースアップグレードの実行のサポートは利用できません |
| フォーム | TarMKからDocumentMKへの移行のサイドグレード | 古いシステムからデータを書き出し、新しいセットアップシステムで読み込むことができます。 手順について詳しくは、JEE上のAEM Formsのアップグレードドキュメントを参照してください |
| フォーム | JEE上のAEM Forms32ビット版のインストーラーは使用できません。 | Adobeは、JEE 32ビットインストーラーでAEM Formsの出荷を停止しました。 引き続き64ビット版のインストーラーを使用して、JEE上のAEM Formsをインストールできます。 |
| フォーム | ドキュメントフラグメントコンポーネントでのDAM画像の使用のサポートを削除しました。 | インタラクティブな通信の印刷チャネルで、画像とグラフコンポーネントを使用できます。 アダプティブフォームでアダプティブドキュメントのドキュメントフラグメントコンポーネントを使用している場合、AEM 6.4Formsへのアップグレード後に機能が停止します。 |
| フォーム | アダプティブドキュメント機能を削除しました。 | インタラクティブな通信機能を使用して、印刷およびWebベースの通信を作成できます。 アダプティブドキュメントを使用する場合、既存のアダプティブドキュメントを引き続き使用するには、互換性パッケージをインストールします |
| フォーム | JEE固有のランディングページ上のAEM Formsを削除しました。 | JEE上のAEM FormsランディングページはAEMランディングページ(/aem/start.html)に置き換えられます。 |
| フォーム | デフォルトのCaptchaのサポートを削除しました。 | GoogleのreCAPTCHAサービスを使用します。 |
| フォーム | AEM DesignerでFlashフィールドのサポートが削除されました。 AEM Designerでは、フォームで使用されるFlashフィールドの編集は許可されていません。 | 以前のバージョン用にリリースされたAEM Designerを使用して、このようなフォームを編集できます。 |
| Communities | Captcha検証のサポートが削除されました。 | 検証には、カスタムcaptcha統合（GoogleによるreCAPTCHAなど）を使用します。 |

## 次期リリースに関する予告 {#pre-announcement-for-next-release}

次の表に、今後のリリースに関する変更点のリストを示します。この変更点は非推奨ではありませんが、お客様に影響を与える可能性があります。 計画を立てる際の参考情報としてご覧ください。

| 領域 | 機能 | お知らせ |
|---|---|---|
| ブラウザーのサポート | Microsoft Internet Explorer | AEM 6.4 は、Microsoft Internet Explorer 11 をサポートする最後のリリースです。 |
| 基盤 | UI フレームワーク | Adobeでは、2019年にCoral UI 2コンポーネントが非推奨となります。 AEM 6.4は、完全にCoral UI 3に基づいています(AEM 6.2で導入)。 Adobeでは、Coral 2を使用してカスタムUIを構築した顧客およびパートナーに、Coral 3にリファクタリングすることを推奨しています。 Adobeオファーは、Coral 2の対話をCoral 3に変換するツールです — [詳細を読みます。](/help/sites-developing/modernization-tools.md) |
