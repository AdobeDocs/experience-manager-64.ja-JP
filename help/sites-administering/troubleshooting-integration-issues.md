---
title: 統合の問題のトラブルシューティング
seo-title: Troubleshooting Integration Issues
description: 統合の問題をトラブルシューティングする方法を学びます。
seo-description: Learn how to troubleshoot integration issues.
uuid: fe080e58-a855-4308-a611-f72eb47ba82d
contentOwner: raiman
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: integration
content-type: reference
discoiquuid: 422ee332-23ae-46bd-8394-a4e0915beaa2
exl-id: 81b8f8c0-7f9d-4748-af07-c550826c19b4
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '1094'
ht-degree: 69%

---

# 統合の問題のトラブルシューティング{#troubleshooting-integration-issues}

## トラブルシューティングに関する一般的なヒント {#general-troubleshooting-tips}

### JavaScript エラーがないことを確認 {#ensure-there-are-no-javascript-errors}

ブラウザの JavaScript コンソールにエラーが表示されていないか確認してください。未処理のエラーにより、後続のコードが正しく実行されない可能性があります。エラーがある場合は、どのスクリプトがどの領域でエラーの原因となっているのか確認してください。スクリプトへのパスにより、そのスクリプトがどの機能に属しているかがわかる場合があります。

### コンポーネントレベルでのログ {#logging-on-component-level}

コンポーネントレベルでステートメントを追加すると便利な場合があります。コンポーネントがレンダリングされることで、一時的なマークアップを追加して変数値を表示し、潜在的な問題を特定するのに役立ちます。次に例を示します。

```
<%
log.info("myVariable={}", myVariable);
%>
  
<!--
<%= myJspVariable %>
-->

<!--
${ myHtlVariable }
-->
```

ログについて詳しくは、 [ログ](/help/sites-deploying/configure-logging.md) および [監査レコードとログファイルの操作](/help/sites-deploying/monitoring-and-maintaining.md#working-with-audit-records-and-log-files) ページ。

## Analytics 統合の問題 {#analytics-integration-issues}

### レポートインポーターが原因で CPU／メモリ使用量が多い {#the-report-importer-causes-high-cpu-memory-usage}

レポートインポーターが原因で CPU／メモリの使用量が多くなる、または `OutOfMemoryError` 例外となる。

#### 解決策 {#solution}

この問題を解決するには、次の方法を試してください。

* 大量の PollingImporter が登録されていないことを確認します（下記の「PollingImporter が原因でシャットダウンに時間がかかる」を参照）。
* `ManagedPollingImporter`OSGi コンソール[で ](/help/sites-deploying/configuring-osgi.md) を設定する CRON 式を使用して、特定の時刻にレポートインポーターを実行します。

AEMでカスタムデータインポーターサービスを作成する方法について詳しくは、次の記事を参照してください [https://helpx.adobe.com/experience-manager/using/polling.html](https://helpx.adobe.com/jp/experience-manager/using/polling.html).

### PollingImporter が原因でシャットダウンに時間がかかる {#shutdown-takes-a-long-time-due-to-the-pollingimporter}

Analytics は継承メカニズムを念頭に置いて設計されています。通常、ページプロパティの「[クラウドサービス](/help/sites-developing/extending-cloud-config.md)」タブ内の Analytics 設定への参照を追加することで、サイトの Analytics を有効にします。ページで別の設定が必要な場合を除き、設定は再度参照する必要はなく、自動的にすべてのサブページに継承されます。サイトへの参照を追加すると、タイプの複数のノード (AEM 6.3 以前の場合は 12、AEM 6.4 の場合は 6) も自動的に作成されます `cq;PollConfig` Analytics データをAEMに読み込むために使用する PollingImporter をインスタンス化します。 そのため、以下のようなことが起こりえます。

* Analytics を参照しているページがたくさんあると、大量の PollingImporter につながります。
* さらに、Analytics 設定への参照とともにページをコピーして貼り付けると、PollingImporters が重複します。

#### 解決策 {#solution-1}

まず、 [error.log](/help/sites-deploying/configure-logging.md) は、アクティブな PollingImporters または登録されている PollingImporters の量に関する情報を提供します。 次に例を示します。

```
# Count PollingImporter entries
$ sed -n "s/.*(aem-analytics-integration-.*).*target=\(.*\),interval.*/\1/p" error.log | wc -l
86415
# Count PollingImporter entries for last30days
$ sed -n "s/.*(aem-analytics-integration-last30Days).*target=\(.*\),interval.*/\1/p" error.log | wc -l
14531
# Count unique paths of PollingImporter registrations
sed -n "s/.*(aem-analytics-integration-.*).*target=\(.*\)\/jcr:content.*/\1/p" error.log | sort | uniq -c
28115
```

次に、トップページ（階層の上位）のみに Analytics 設定が参照されていることを確認します。

AEMでカスタムデータインポーターサービスを作成する方法について詳しくは、次の記事を参照してください [https://helpx.adobe.com/experience-manager/using/polling.html](https://helpx.adobe.com/experience-manager/using/polling.html).

## DTM（レガシー）の問題 {#dtm-legacy-issues}

### DTM スクリプトタグがページソースにレンダリングされない {#the-dtm-script-tag-is-not-rendered-in-the-page-source}

設定がページプロパティの[クラウドサービス](/help/sites-developing/extending-cloud-config.md)タブで参照されているにもかかわらず、[DTM](/help/sites-administering/dtm.md) スクリプトタグがページに正しく含まれていない。

#### 解決策 {#solution-2}

この問題を解決するには、次の方法を試してください。

* 暗号化されたプロパティが復号化できることを確認します（暗号化では各 AEM インスタンスで異なる自動生成キーが使用される可能性があることに注意してください）。詳細については、[構成プロパティの暗号化サポート](/help/sites-administering/encryption-support-for-configuration-properties.md)も参照してください。
* 次の場所で見つかった設定を再公開 `/etc/cloudservices/dynamictagmanagement`
* で ACL をチェック `/etc/cloudservices`. ACL は次のようになります。

   * allow; jcr:read; webservice-support-servicelibfinder
   * 許可する。jcr:read;みんなrep:glob:&amp;ast;/defaults/&amp;ast;
   * 許可する。jcr:read;みんなrep:glob:&amp;ast;/defaults
   * 許可する。jcr:read;みんなrep:glob:&amp;ast;/public/&amp;ast;
   * 許可する。jcr:read;みんなrep:glob:&amp;ast;/public

ACL 管理の詳細については、[ユーザー管理とセキュリティ](/help/sites-administering/security.md#permissions-in-aem)ページを参照してください。

## Target 統合の問題 {#target-integration-issues}

### カスタムページコンポーネントを使用しているときに Target コンテンツがプレビューモードで表示されない {#targeted-content-not-visible-in-preview-mode-when-using-custom-page-components}

この問題は、カスタムページコンポーネントに Target DTM 統合を処理する正しい JSP またはクライアントライブラリが含まれていないために発生します。

#### 解決策 {#solution-3}

次の解決策を試してください。

* カスタム `headlibs.jsp` ( 存在する場合 `/apps/<CUSTOM-COMPONENTS-PATH>/headlibs.jsp`) には、以下が含まれます。

```
<%@include file="/libs/cq/cloudserviceconfigs/components/servicelibs/servicelibs.jsp" %>
<sly data-sly-resource="${'contexthub' @ resourceType='granite/contexthub/components/contexthub'}"/>
```

* カスタム `head.html` ( 存在する場合 `/apps/<CUSTOM-COMPONENTS-PATH>/head.html`) **次の値と等しくない** 次の例のように、特定の統合ヘッドライブを選択的に含めます。

```
<!-- DO NOT MANUALLY INCLUDE SPECIFIC CLOUD SERVICE HEADLIBS LIKE THIS -->
<meta data-sly-include="/libs/cq/dtm/components/dynamictagmanagement/headlibs.jsp" data-sly-unwrap/>
```

この `servicelibs.jsp` によって、必要な分析用 Javascript オブジェクトが追加され、Web サイトに関連付けられているクラウドサービスライブラリが読み込まれます。Target サービスの場合、ライブラリは `/libs/cq/analytics/components/testandtarget/headlibs.jsp`

読み込まれるライブラリのセットは、Target の設定で使用されているターゲットクライアントライブラリのタイプ（`mbox.js` または `at.js`）によって異なります。

`mbox.js` または `at.js` 送信に DTM を使用する場合、コンテンツがレンダリングされる前にライブラリがロードされていることを確認してください。これらのライブラリを非同期的にロードするタグ管理システムを使用すると、ターゲット固有の JavaScript コードの実行に問題が生じる可能性があります。

追加情報については、[ターゲットコンテンツ向けの開発](/help/sites-developing/target.md#understanding-the-target-component)ページを参照してください。

### 「Missing Report Suite ID in AppMeasurement initialization」というエラーがブラウザーコンソールに表示される {#the-error-missing-report-suite-id-in-appmeasurement-initialization-is-displayed-in-the-browser-console}

この問題は、Adobe Analyticsが DTM を使用して Web サイトに実装され、カスタムコードを使用している場合に発生する可能性があります。 原因は `s = new AppMeasurement()` をインスタンス化するには、 `s` オブジェクト。

#### 解決策 {#solution-4}

用途 `s_gi` の代わりに、 `new AppMeasurement` インスタンス化メソッド。 次に例を示します。

```
var s_account="INSERT-RSID-HERE"
var s=s_gi(s_account)
```

### 正しいオファーではなく、デフォルトのオファーがランダムに表示される {#a-default-offer-is-randomly-displayed-instead-of-the-correct-offer}

この問題には複数の原因が考えられます。

* Target クライアントライブラリを読み込み中 ( `mbox.js` または `at.js`) をサードパーティのタグ管理システムを使用して非同期で実行すると、ターゲティングがランダムに解除される場合があります。 ターゲットライブラリはページヘッドに同期的にロードされることになっています。ライブラリが AEM から配信される場合、これは常に当てはまります。

* 2 つの Target クライアントライブラリを読み込み中 ( `at.js`) を同時に使用できます。例えば、1 つは DTM を使用し、もう 1 つはAEMの Target 設定を使用します。 `adobe.target` バージョンが異なる場合、これが原因で `at.js` の定義がクラッシュする可能性があります。

#### 解決策 {#solution-5}

次の解決策を試してください。

* DTM のようなライブラリをロードするカスタムコード（Target ライブラリを順番にロードする）が、[ページヘッド](/help/sites-developing/target.md#enabling-targeting-with-adobe-target-on-your-pages) で同期的に実行されることを確認します。
* サイトが DTM を使用して Target ライブラリを配信するように設定されている場合、 **DTM によって配信される Clientlib** オプションが [Target 設定](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/target-configuring.html) サイトの

### AT.js 1.3 以降を使用すると、正しいオファーではなくデフォルトのオファーが常に表示される {#a-default-offer-is-always-displayed-instead-of-correct-offer-when-using-at-js}

標準の AEM 6.2 および 6.3 は、AT.js バージョン 1.3.0 以降と互換性がありません。AT.js バージョン 1.3.0 では、API に対するパラメーター検証が導入されていますが、 `adobe.target.applyOffer()` には、 `atjs-itegration.js` コード。

#### 解決策 {#solution-6}

この問題を解決するには、編集 `atjs-itegration.js` をクリックし、 `"mbox": mboxName` 次のパラメーターオブジェクトのフィールド： `adobe.target.applyOffer()` 次のように指定します。

```
adobe.target.getOffer({
    "mbox": mboxName,
    "params": params,
    "success": function (response) {
        adobe.target.applyOffer({
            "mbox": mboxName, //<--- ADDED PARAM
            "selector": "#" + mboxName,
            "offer": response
        })
    },
```

### 目標と設定ページにレポートソースセクションが表示されない {#the-goals-settings-page-does-not-show-the-reporting-sources-section}

この問題は、おそらく [A4T Analytics Cloud設定](/help/sites-administering/target-configuring.md) プロビジョニングの問題。

#### 解決策 {#solution-7}

AEM に次の確認要求を発行して、Target アカウントに対して A4T が正しく有効になっていることを確認する必要があります。

```
http://localhost:4502/etc/cloudservices/testandtarget/<YOUR-CONFIG>/jcr:content.a4t.json
 
{
    "a4tEnabled": true,
    "sharedsecret": "SECRET",
    "proxyUrl": "/libs/cq/contentinsight/content/proxy.reportingservices.json",
    "active": "true",
    "pageName": "",
    "url": "https://api5.omniture.com/rs/0.5/",
    "username": "USER@DOMAIN"
}
```

応答に `a4tEnabled:false` という行が含まれている場合、[アドビカスタマーケア](https://helpx.adobe.com/jp/contact.html)に連絡して、アカウントを正しくプロビジョニングするようご依頼ください。

### 参考 Target API {#helpful-target-apis}

Target の問題をトラブルシューティングするときに、以下の 2 つのTarget API が参考になるかもしれません。

* 特定のクライアントコードのTarget エンドポイントを取得する

```
https://admin.testandtarget.omniture.com/rest/v1/endpoint/<CLIENTCODE>.json
 
{"api":"https://admin<N>.testandtarget.omniture.com/admin/rest/v1"}
```

* クライアントのプロファイルを取得する

```
https://admin<N>.testandtarget.omniture.com/admin/rest/v1/clients/<CLIENT>?email=<EMAIL>&password=<PASSWORD>
 
Response for N=4, CLIENT-dayintegrationintern
{
    "clientCode": "dayintegrationintern",
    "companyName": "Day Integration - Internal",
    "omnitureCompanyId": "Day Integration Internal",
    "softTraxId": -1,
    "address1": "XYZ",
    "city": "San Francisco",
    "state": "ca",
    "zip": "94107",
    "country": "UNITED STATES",
    "locale": "de_DE",
    "timeZone": "Europe/Berlin",
    "phone": "XX-XX-XXXX",
    "serviceLevel": "Up to 100,000",
    "privileges": [
        "a4t",
        "hosts",
        "TnT-SC-integration",
        "mvt",
        "steps",
        "testing-campaigns",
        "view-snapshot",
        "on-site-editor",
        "optimizing-campaign",
        "third-party-id-support",
        "landing-page-campaigns",
        "segment",
        "rest-create-user",
        "advanced-targeting",
        "mobile-device-targeting",
        "beta",
        "geolocation"
    ]
}
```
