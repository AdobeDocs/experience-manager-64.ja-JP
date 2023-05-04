---
title: 廃止される機能および削除された機能
description: リリースノート（Adobe Experience Manager 6.4 の廃止される機能および削除された機能）
exl-id: 2fe0dad7-fc78-4aac-afa3-79a278008453
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '1344'
ht-degree: 24%

---

# 廃止される機能および削除された機能 {#deprecated-and-removed-features}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

アドビでは、製品の機能を絶えず評価して、常に後方互換性を慎重に考慮しながら、古い機能を作成し直したり、より近代的な機能に置き換えて、お客様にとっての全体的な価値を向上させています。

AEM機能の差し迫った削除/置き換えを伝達するために、次の規則が適用されます。

1. まず、非推奨（廃止予定）の発表がおこなわれます。非推奨（廃止予定）の機能は引き続き使用できますが、それ以上の機能強化はおこなわれません。
1. 非推奨（廃止予定）の機能は、以下のメジャーリリースで最も早く削除されます。 削除の実際の目標期日を通知します。

このプロセスにより、機能が実際に削除されるまでに、廃止される機能の新しいバージョンまたは後継機能にお客様が実装を合わせるためのリリースサイクルが少なくとも 1 回あります。

## 非推奨（廃止予定）の機能 {#deprecated-features}

次の表に、AEM 6.4 で非推奨とマークされた機能を示します。通常、将来のリリースで削除される予定の機能は、まず非推奨に設定され、代わりの機能も提供されます。

現在のデプロイメントでその機能を利用しているかどうかを確認し、提示される代替機能を使用するために実装の変更を計画するようにお勧めします。

<!-- TBD: This MD table is a replacement of the HTML table below. However, it generates validation error hence commenting and replacing with inline text. Restore if required. -->

| 領域 | 機能 | 代替手段 |
|---|---|---|
| UI | Adobeは、クラシック UI をさらに強化する予定はありません。 AEM 6.4 にはクラシック UI が含まれており、以前のリリースからアップグレードするお客様はクラシック UI をそのまま使用できます。 クラシック UI は廃止中は引き続き完全にサポートされます。 <ul> <li>`/libs/cq/core/content/welcome.html` </li> <li> `/siteadmin` </li> <li> `/damadmin` </li> <li> `/mcmadmin` </li> <li> `/inbox` </li> <li> `/tagging` </li> <li> `/cf#` (ページエディター) </li><li> `/libs/launches/content/admin.html` </li> <li> `/libs/cq/workflow/content/console.html` </li> </ul> | 新しいAEM UI を使用するように切り替えることをお勧めします。 |
| コンポーネント | Adobeでは、以下に示す基盤コンポーネントの機能強化は予定されていません。 AEM 6.4 には基盤コンポーネントが含まれており、以前のリリースからアップグレードするお客様はクラシック UI をそのまま使用し続けることができます。基盤コンポーネントは、廃止中も引き続き完全にサポートされます。 <ul> <li> foundation/components/account/accountname </li> <li> foundation/components/account/actions </li> <li> foundation/components/account/passwordreset </li> <li> foundation/components/account/requestconfirmation </li> <li> foundation/components/adaptiveimage </li> <li> foundation/components/assetsharepage </li> <li> foundation/components/breadcrumb </li> <li> foundation/components/form/creditcard </li> <li> foundation/components/listchildren </li> <li> foundation/components/login </li> <li> foundation/components/logo </li> <li> foundation/components/mobilefooter </li> <li> foundation/components/mobileimage </li> <li> foundation/components/mobilelist </li> <li> foundation/components/mobilelogo </li> <li> foundation/components/mobilereference </li> <li> foundation/components/mobiletextimage </li> <li> foundation/components/mobiletopnav </li> <li> foundation/components/search </li> <li> foundation/components/sitemap </li> <li> foundation/components/table </li> <li> foundation/components/toolbar </li> <li> foundation/components/topnav </li> <li> foundation/components/userinfo </li> </ul> | 将来のプロジェクトでは、コアコンポーネントを使用することをお勧めします。 既存のサイトを変更する必要はありません。 |
| コンポーネント | Adobeでは、以下に示す基盤コンポーネントの機能強化は予定されていません。 AEM 6.4 には基盤コンポーネントが含まれており、以前のリリースからアップグレードするお客様はクラシック UI をそのまま使用し続けることができます。基盤コンポーネントは、廃止中も引き続き完全にサポートされます。 <ul><li>foundation/components/timing</li></ul> | Adobeは、代替サービスを提供する予定はありません。 |
| ポータルDirector | ポータルDirectorは、ポートレットを介したAEMコンテンツのサードパーティサーバーでのホストを可能にする一連の機能です。 Adobeでは、以下の場所にあるポータルDirector機能をさらに強化する予定はありません。 AEM 6.4 には Portal Directorが含まれており、以前のリリースからアップグレードするお客様は、そのまま使用できます。 ポータルダイレクトは非推奨の間も、引き続き完全にサポートされます。 <ul><li>/libs/portal/director</li></ul> | Adobeは、代替サービスを提供する予定はありません。 |
| ポートレットコンポーネント | /foundation/components/portlet の下のポートレットコンポーネントは、AEM内の JSR ポートレットをコンポーネントとしてホストできます。 Adobeでは、ポートレットコンポーネント機能をさらに強化する予定はありません。 AEM 6.4 にはポートレットコンポーネントが含まれており、以前のリリースからアップグレードしたお客様は、そのまま使用できます。 ポートレットコンポーネントは廃止中も完全にサポートされます。 | Adobeは、代替サービスを提供する予定はありません。 |
| Forms | CentralAdobeはサポートされなくなったので、AdobeCentral Migration Bridge サービスのサポートは廃止されました。 | 代替機能はありません |
| Forms | Query および OperationOptions での JSONObject の使用は廃止されました。 次の API は非推奨（廃止予定）となりました。 <ul><li>`setArguments(JSONObject arguments)`</li><li> `JSONObject getArguments()`</li><li>`OperationOptions(String operationId, JSONObject arguments)`</li><li>`JSONObject getArguments()`</li><li> `void setArguments(JSONObject arguments)`</li></ul> | 以下を使用： `IValueMap` API |
| Forms | 廃止された Central Migration Bridge サービスです。 | 代替機能は提供されていません。 |
| Assets | Assets のオフロードは、AEM 6.4 以降で非推奨となりました。 |  |
| デベロッパー向け | Lodash／underscore クライアントライブラリ。アドビでは今後、配布版（クイックスタート）の一部として含まれている Lodash/underscore クライアントライブラリの保守や更新を行う予定はありません。 | コードに Lodash／underscore が引き続き必要な場合は、このクライアントライブラリをプロジェクトコードベースに追加することをお勧めします。 |

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

次の表に、AEM 6.4 から削除された機能を示します。以前のリリースでは、これらの機能は非推奨とマークされていました。

| 領域 | 機能 | 代替手段 |
|---|---|---|
| [!DNL Experience Cloud] との統合 | [!DNL Adobe I/O] 経由での設定を使用して、アセットを [!DNL Experience Cloud] と同期できます。[!DNL Adobe Experience Cloud] は、以前は [!DNL Adobe Marketing Cloud] と呼ばれていました。 | クエリがある場合は、 [Adobeカスタマーサポート](https://experienceleague.adobe.com/?support-solution=General&amp;lang=ja#support). |
| AnalyticsActivity Map | AEMに含まれるActivity Mapのバージョン。 | Adobe Analytics API 内のセキュリティ変更により、AEM に含まれているバージョンの Activity Map は使用できなくなりました。この [Adobe Analyticsが提供する ActivityMap プラグイン](https://experienceleague.adobe.com/docs/analytics/analyze/activity-map/getting-started/get-started-users/activitymap-install.html?lang=ja) 現在はを使用する必要があります。 |
| Components-Forms | フォームキャプチャ (foundation/components/form/captcha) | 代わりに、Googleによる ReCaptcha コンポーネントを使用します。 |
| コンポーネント | スライドショー (foundation/components/slideshow) | 代替機能はありません |
| コンポーネント | Flash(foundation/components/flash) | 代替機能はありません |
| コンポーネント | ビデオコンポーネントでのSWFファイルの再生のサポートを削除しました (foundation/components/video) | Flash ベースでないビデオ形式を使用します。 |
| コンポーネント | 製品テーブル (commerce/components/product_table) | 代替機能はありません |
| タスク管理 | クラシック UI タスク管理 (/libs/cq/taskmanagement/content/taskmanager.html) | 6.0 以降で廃止されました。ワークフロー UI と組み合わされた新しいタスク管理を使用してください。 |
| ワークフロー | 5.6 ～ 6.2 の間で使用される通知 UI (/libs/cq/workflow/content/notifications.html) | ワークフローインボックス/aem/inbox |
| Forms | PDFジェネレーターを使用したPDF/E-1 形式へのExport PDFは削除されました。 | PDFジェネレーターは、PDF/A-1a/b、PDF/A-2a/b、PDF/A-3a/b 形式へのPDFの書き出しを引き続きサポートしています。 |
| Forms | ドキュメントフラグメント内の画像のサポートが削除されました。 | インタラクティブ通信には、印刷チャネルと Web チャネルで画像を直接使用する機能が用意されています。 |
| Forms | アウトオブプレースアップグレード | アウトオブプレースアップグレードを実行するサポートは利用できません |
| Forms | TarMK から DocumentMK への移行のサイドグレード | 古いシステムからデータを書き出し、新しいセットアップシステムに読み込むことができます。 詳しい手順については、 JEE 上のAEM Formsのアップグレードドキュメントを参照してください |
| Forms | JEE 上のAEM Forms 32 ビット版のインストーラーは使用できません。 | Adobeは、JEE 32 ビット版のインストーラーでAEM Formsの出荷を停止しました。 64 ビットインストーラーを引き続き使用して、JEE 上のAEM Formsをインストールできます。 |
| Forms | ドキュメントフラグメントコンポーネントでの DAM 画像の使用のサポートを削除しました。 | インタラクティブ通信の印刷チャネルで、画像コンポーネントとグラフコンポーネントを使用できます。 アダプティブフォームでアダプティブドキュメントのドキュメントフラグメントコンポーネントを使用している場合、AEM 6.4 Formsにアップグレードした後、コンポーネントが機能しなくなります。 |
| Forms | アダプティブドキュメント機能を削除しました。 | インタラクティブ通信機能を使用して、印刷用と Web ベースの通信を作成できます。 アダプティブドキュメントを使用している場合は、互換性パッケージをインストールして既存のアダプティブドキュメントを引き続き使用してください |
| Forms | JEE 上のAEM Forms固有のランディングページを削除しました。 | JEE 上のAEM Formsのランディングページは、AEMのランディングページ (/aem/start.html) に置き換えられます。 |
| Forms | デフォルトの Captcha のサポートを削除しました。 | Googleの reCAPTCHA サービスを使用する。 |
| Forms | AEM Designer での Flash フィールドのサポートを削除しました。 AEM Designer では、フォームで使用される Flash フィールドを編集できません。 | 以前のバージョンでリリースされたAEM Designer を使用して、このようなフォームを編集できます。 |
| Communities | Captcha 検証のサポートが削除されました。 | 検証には、カスタム Captcha 統合 (Googleによる reCAPTCHA など ) を使用します。 |

## 次期リリースの事前発表 {#pre-announcement-for-next-release}

次の表は、非推奨（廃止予定）ではないが、お客様に影響を与える可能性のある、将来のリリースに関する変更のリストを示しています。 これらは、計画のために提供されます。

| 領域 | 機能 | お知らせ |
|---|---|---|
| ブラウザーのサポート | Microsoft Internet Explorer | AEM 6.4 は、Microsoft Internet Explorer 11 をサポートする最後のリリースです。 |
| 基盤 | UI フレームワーク | Adobeは、2019 年に Coral UI 2 コンポーネントを廃止します。 AEM 6.4 は、(AEM 6.2 で導入された )Coral UI 3 に完全に基づいています。 Adobeでは、Coral 2 でカスタム UI を構築したお客様およびパートナーに対し、Coral 3 にリファクタリングすることをお勧めします。 Adobeは、Coral 2 のダイアログを Coral 3 に変換するツールを提供します。 [詳細を表示](/help/sites-developing/modernization-tools.md) |
