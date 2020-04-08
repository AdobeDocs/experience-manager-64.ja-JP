---
title: 廃止される機能および削除された機能
seo-title: 廃止される機能および削除された機能
description: リリースノート（Adobe Experience Manager 6.4 の廃止される機能および削除された機能）
seo-description: リリースノート（Adobe Experience Manager 6.4 の廃止される機能および削除された機能）
uuid: 2619039b-72b4-4c6c-a813-90eed622b423
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.4
topic-tags: release-notes
content-type: reference
discoiquuid: 15819d42-4897-40fa-a013-e019d1580fa2
translation-type: tm+mt
source-git-commit: 3316dbc8ef268be2b305d22da9003ae40414b4e1

---


# 廃止される機能および削除された機能 {#deprecated-and-removed-features}

アドビでは、製品の機能を絶えず評価して、常に後方互換性を慎重に考慮しながら、古い機能を作成し直したり、より近代的な機能に置き換えて、お客様にとっての全体的な価値を向上させています。

近い将来おこなわれる AEM 機能の削除や置換を通知するため、次のルールが適用されます。

1. まず、非推奨（廃止予定）の発表がおこなわれます。廃止中は、機能はまだ使用可能ですが、それ以上の強化はおこなわれません。
1. 廃止された機能の削除は、早ければ、次のメジャーリリースでおこなわれます。削除の実際の期日が発表されます。

このプロセスにより、機能が実際に削除されるまでに、非推奨（廃止予定）の機能の新しいバージョンまたは後継機能にお客様が実装を合わせるためのリリースサイクルが少なくとも 1 回あります。

## 廃止される機能 {#deprecated-features}

この節では、AEM 6.4 で廃止予定になっている機能について説明します。通常、将来のリリースで削除される予定になっている機能は、まず廃止予定に設定されて代替の機能が提供されます。

現在のデプロイメントでその機能を利用しているかどうかを確認し、提示される代替手段を使用するために実装の変更を計画するようにお勧めします。

<table> 
 <tbody>
  <tr>
   <td>領域</td> 
   <td>機能</td> 
   <td>代替手段</td> 
  </tr>
  <tr>
   <td>UI</td> 
   <td><p>クラシック UI の機能がさらに強化される予定はありません。AEM 6.4 にはクラシック UI が含まれており、以前のリリースからアップグレードするお客様はクラシック UI をそのまま使用し続けることができます。クラシック UI は廃止中は引き続き完全にサポートされます。 </p> 
    <ul> 
     <li>/libs/cq/core/content/welcome.html</li> 
     <li>/siteadmin</li> 
     <li>/damadmin</li> 
     <li>/mcmadmin</li> 
     <li>/inbox</li> 
     <li>/tagging</li> 
     <li>/cf#（ページエディター）</li> 
     <li>/libs/launches/content/admin.html</li> 
     <li>/libs/cq/workflow/content/console.html</li> 
    </ul> </td> 
   <td><p>新しい AEM UI に切り替えることをお勧めします。</p> <p> </p> </td> 
  </tr>
  <tr>
   <td>コンポーネント</td> 
   <td><p>以下の基盤コンポーネントの機能がさらに強化される予定はありません。AEM 6.4にはFoundation Componentsが含まれており、以前のリリースからアップグレードしたお客様は、引き続きそのまま使用できます。 Foundation Componentsは、非推奨の間も完全にサポートされたままです。 </p> 
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
   <td>今後のプロジェクトには、コアコンポーネントを使用することをお勧めします。既存のサイトを変更する必要はありません。</td> 
  </tr>
  <tr>
   <td>コンポーネント</td> 
   <td><p>以下の基盤コンポーネントの機能がさらに強化される予定はありません。AEM 6.4にはFoundation Componentsが含まれており、以前のリリースからアップグレードしたお客様は、引き続きそのまま使用できます。 Foundation Componentsは、非推奨の間も完全にサポートされたままです。</p> 
    <ul> 
     <li>foundation/components/timing</li> 
    </ul> </td> 
   <td>書き換えの予定はありません。</td> 
  </tr>
  <tr>
   <td>ポータル・ディレクター</td> 
   <td><p>ポータルディレクターは、サードパーティサーバーのポートレットを介してAEMコンテンツをホストする機能のセットです。</p> <p>アドビでは、以下に示す場所で、Portal Directorの機能をさらに強化する予定はありません。 AEM 6.4にはPortal Directorが含まれており、以前のリリースからアップグレードしたお客様は、引き続きそのまま使用できます。 非推奨の間も、Portal Directは引き続き完全にサポートされます。</p> 
    <ul> 
     <li>/libs/portal/director</li> 
    </ul> </td> 
   <td>書き換えの予定はありません。</td> 
  </tr>
  <tr>
   <td>ポートレットコンポーネント</td> 
   <td><p>/foundation/components/portletの下のポートレットコンポーネントを使用すると、AEM内のJSRポートレットをコンポーネントとしてホストできます。</p> <p>アドビでは、ポートレットコンポーネント機能をさらに強化する予定はありません。 AEM 6.4にはポートレットコンポーネントが含まれており、以前のリリースからアップグレードしたお客様は、このコンポーネントをそのまま使用し続けることができます。 ポートレットコンポーネントは、非推奨の間も完全にサポートされます。</p> </td> 
   <td>書き換えの予定はありません。</td> 
  </tr>
  <tr>
   <td>Forms</td> 
   <td><p>Adobe Central 製品がサポートされなくなったので、Adobe Central Migration Bridge サービスのサポートは廃止されました。</p> </td> 
   <td>代替手段はありません。 </td> 
  </tr>
    <tr>
   <td>Forms</td> 
   <td><p>OptionとOperationOptionsでのJSONObjectの使用が廃止されました。クエリとOptionsを参照してください。 次のAPIは廃止されました。
   <ul><li>setArguments（JSONObject引数）</li><li>JSONObject getArguments()</li><li>OperationOptions(String operationId, JSONObject引数</li><li>JSONObject getArguments()</li><li>void setArguments（JSONObject引数）</li></ul>
   </p> </td> 
   <td>IValueMap APIの使用 </td> 
  </tr>
  <tr>
   <td>Assets</td> 
   <td><p>AEM 6.4以降では、アセットのオフロードは非推奨となりました。</p> </td> 
   <td> </td> 
  </tr>
 </tbody>
</table>

## 削除された機能 {#removed-features}

この節では、AEM 6.4から削除された機能に関するリストを説明します。以前のリリースでは、これらの機能は非推奨としてマークされていました。

<table> 
 <tbody>
  <tr>
   <td><strong>領域</strong></td> 
   <td><strong>機能</strong></td> 
   <td><strong>代替手段</strong></td> 
  </tr>
  <tr>
   <td>Analyticsアクティビティマップ</td> 
   <td>AEMに含まれるアクティビティマップのバージョン。</td> 
   <td>Adobe Analytics API 内のセキュリティ変更により、AEM に含まれているバージョンの Activity Map は使用できなくなりました。<br><br>Adobe Analyticsが提 <a href="https://docs.adobe.com/content/help/ja-JP/analytics/analyze/activity-map/getting-started/get-started-users/activitymap-install.translate.html">供するActivityMapプラグインを使用する</a> 。</td> 
  </tr>
  <tr>
   <td>コンポーネント</td> 
   <td>フォームキャプチャ<br />（foundation/components/form/captcha）</td> 
   <td>Google の ReCaptcha コンポーネントを代わりに使用します。</td> 
  </tr>
  <tr>
   <td>コンポーネント</td> 
   <td>Slideshow<br />（foundation/components/slideshow）</td> 
   <td>代替機能はありません。</td> 
  </tr>
  <tr>
   <td>コンポーネント</td> 
   <td>Flash<br />（foundation/components/flash）</td> 
   <td>代替機能はありません。</td> 
  </tr>
  <tr>
   <td>コンポーネント</td> 
   <td>ビデオコンポーネントでの SWF ファイルの再生はサポートされなくなりました。<br /> （foundation/components/video）</td> 
   <td>Flash ベースでないビデオ形式を使用します。</td> 
  </tr>
  <tr>
   <td>コンポーネント</td> 
   <td>製品テーブル<br />（commerce/components/product_table）</td> 
   <td>代替機能はありません。</td> 
  </tr>
  <tr>
   <td>タスク管理</td> 
   <td>クラシック UI タスク管理<br />（/libs/cq/taskmanagement/content/taskmanager.html）</td> 
   <td>6.0 以降、廃止されました。ワークフロー UI に統合されている新しいタスク管理機能を使用します。</td> 
  </tr>
  <tr>
   <td>ワークフロー</td> 
   <td>5.6 から 6.2 までで使用された通知 UI<br /> （/libs/cq/workflow/content/notifications.html）</td> 
   <td>ワークフローインボックス（/aem/inbox）</td> 
  </tr>
  <tr>
   <td>Forms</td> 
   <td>PDF Generator を使用して PDF を PDF/E-1 形式に書き出す機能は削除されました。</td> 
   <td>PDF Generatorでは、引き続きPDFのPDF/A-1a/b、PDF/A-2a/bおよびPDF/A-3a/b形式への書き出しがサポートされます。</td> 
  </tr>
  <tr>
   <td>Forms</td> 
   <td>アダプティブフォームでのデフォルトのAEM Captchaサービスのサポートが削除されました。 </td> 
   <td>Google の ReCaptcha を代わりに使用します。</td> 
  </tr>
  <tr>
   <td>Forms</td> 
   <td>ドキュメントフラグメント内では画像がサポートされなくなりました。 </td> 
   <td>インタラクティブコミュニケーションでは、印刷および Web チャネルで画像を直接使用できます。<br /> </td> 
  </tr>
    <tr>
   <td>Forms</td> 
   <td> アウトオブプレースアップグレード </td> 
   <td>アウトオブプレースアップグレードのサポートは利用できません <br/> </td> 
  </tr>
  <tr>
   <td>Forms</td> 
   <td> TarMKからDocumentMKへの移行のサイドグレード </td> 
   <td> 古いシステムからデータを書き出し、新しいセットアップシステムで読み込むことができます。 詳しい手順については、「JEE上のAEM Formsアップグレードドキュメント」を参照してください。 <br/> </td> 
  </tr>
    <tr>
   <td>Forms</td> 
 <td>JEE上のAEM Forms 32ビット版のインストーラーは使用できません。</td> 
   <td>アドビは、JEE 32ビット版のAEM Formsインストーラーの出荷を停止しました。 引き続き64ビットインストーラーを使用して、JEE上のAEM Formsをインストールできます。 </td>  
  </tr>
    <tr>
    <td>Forms</td> 
    <td>DAM画像を使用するためのサポートをドキュメントフラグメントコンポーネントで削除。</td> 
    <td> インタラクティブな通信の印刷チャネルで、画像とグラフコンポーネントを使用できます。 アダプティブフォームでアダプティブドキュメントのドキュメントフラグメントコンポーネントを使用している場合、AEM 6.4 Formsにアップグレードすると機能しなくなります。 </td>  
  </tr>
  <tr>
   <td>Forms</td> 
   <td> アダプティブドキュメント機能の削除</td> 
   <td> インタラクティブな通信機能を使用して、印刷およびWebベースの通信を作成できます。 アダプティブドキュメントを使用する場合は、互換性パッケージをインストールして、既存のアダプティブドキュメントの使用を継続します<br/> </td> 
  </tr>
    <tr>
    <td>Forms</td> 
    <td>JEE上のAEM Forms固有のランディングページを削除。</td> 
    <td>「JEE上のAEM Forms」ランディングページはAEMランディングページ(/aem/start.html)に置き換えられます。 </td>  
  </tr>
   <tr>
   <td>Forms</td> 
   <td>デフォルトのCaptchaのサポートを削除しました。</td> 
   <td>GoogleのreCAPTCHAサービスを使用します。</td> 
  </tr>
   <tr>
   <td>Forms</td> 
   <td>デフォルトのCaptchaのサポートを削除しました。</td> 
   <td>GoogleのreCAPTCHAサービスを使用します。</td> 
  </tr>
  <tr>
   <td>Communities</td> 
   <td>Captcha検証のサポートが削除されました。</td> 
   <td>検証には、カスタムcaptcha統合（GoogleによるreCAPTCHAなど）を使用します。</td> 
  </tr>
 </tbody>
</table>

## 次期リリースに関する予告 {#pre-announcement-for-next-release}

このセクションで予告する将来のリリースの変更内容は、廃止ではありませんが、お客様に影響します。計画を立てる際の参考情報としてご覧ください。

<table> 
 <tbody>
  <tr>
   <td>領域<br /> </td> 
   <td>機能<br /> </td> 
   <td>予告</td> 
  </tr>
  <tr>
   <td>ブラウザーのサポート</td> 
   <td>Microsoft Internet Explorer</td> 
   <td>AEM 6.4 は、Microsoft Internet Explorer 11 をサポートする最後のリリースです。</td> 
  </tr>
  <tr>
   <td>Foundation</td> 
   <td>UI フレームワーク</td> 
   <td>2019年には、Coral UI 2コンポーネントを非推奨とします。 AEM 6.4は、Coral UI 3（AEM 6.2で導入）に完全に基づいています。 Coral 2を使用してカスタムUIを構築した顧客およびパートナーは、Coral 3にリファクタリングすることをお勧めします。 Adobe offers a tool to convert Coral 2 dialogs to Coral 3 - <a href="/help/sites-developing/dialog-conversion.md">Read more</a>.</td> 
  </tr>
 </tbody>
</table>
