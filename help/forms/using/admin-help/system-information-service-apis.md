---
title: システム情報サービス API
seo-title: System information Service APIs
description: このドキュメントでは、システム情報サービスが提供する API に関する詳細情報を提供します。
seo-description: This document provides detailed information about the APIs provided by the system information service.
uuid: 7f624216-56e6-4d49-b9a1-3c9af045dabe
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/system_information_service
products: SG_EXPERIENCEMANAGER/6.4/FORMS
discoiquuid: 79fccce2-d090-4b50-9c58-3f2a00e651b2
exl-id: 7eee8103-8d6c-4397-acaf-dd662cc09a56
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '374'
ht-degree: 10%

---

# システム情報サービス API {#system-information-service-apis}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

システム情報サービスは、情報を取得するための REST API のセットを提供します。 次の表に、API の詳細情報を示します。

<table>
 <thead>
  <tr>
   <th><p>名前</p></th> 
   <th><p>URL</p></th> 
   <th><p>説明</p></th> 
  </tr> 
 </thead> 
 <tbody>
  <tr>
   <td><p>SystemInfo.properties</p></td> 
   <td><p>https://[server]:[port]/rest/services/SystemInfo.properties</p></td> 
   <td><p>この API は <a href="https://docs.oracle.com/javase/6/docs/api/java/lang/System.html#getProperties()">system.getProperties</a> Java API。 現在の作業環境の設定を取得します。 </p></td> 
  </tr> 
  <tr>
   <td><p>SystemInfo.envVar</p></td> 
   <td><p>https://[server]:[port]/rest/services/ SystemInfo.envVar</p></td> 
   <td><p>ホストオペレーティングシステムのすべての環境変数を取得します。 </p></td> 
  </tr> 
  <tr>
   <td><p>SystemInfo.logs</p></td> 
   <td><p>https://[server]:[port]/rest/services/ SystemInfo.logs</p></td> 
   <td><p>アプリケーションサーバーログを含む zip ファイルをダウンロードします。 </p></td> 
  </tr> 
  <tr>
   <td><p>SystemInfo.config</p></td> 
   <td><p>https://[server]:[port]/rest/services/ SystemInfo.config</p></td> 
   <td><p>config.xml ファイルのすべてのコンテンツを取得します。 </p></td> 
  </tr> 
  <tr>
   <td><p>SystemInfo.services</p></td> 
   <td><p>https://[server]:[port]/rest/services/ SystemInfo.services</p></td> 
   <td><p>AEM forms サービスのステータスおよび設定パラメーターを取得します。</p></td> 
  </tr> 
  <tr>
   <td><p>SystemInfo.vitalDetails</p></td> 
   <td><p>https://[server]:[port]/rest/services/ SystemInfo.vitalDetails</p></td> 
   <td><p>サーバー稼動時間、JVM 引数、システムメモリ、ヒープサイズ、オペレーティングシステム名、アクティブなスレッド数、およびスレッド数を取得します。 </p></td> 
  </tr> 
  <tr>
   <td><p>SystemInfo.coreSettings</p></td> 
   <td><p>https://[server]:[port]/rest/services/ SystemInfo.coreSettings</p></td> 
   <td><p>次のプロパティの値を取得します。</p>
    <ul>
     <li><p>AdobeTempDir</p></li>
     <li><p>AdobeServerFontDir</p></li>
     <li><p>CustomerFontDir</p></li>
     <li><p>GlobalDocumentStorageRootDir</p></li>
     <li><p>DefaultDocumentMaxInlineSize</p></li>
     <li><p>DefaultDocumentDisposalTimeout</p></li>
     <li><p>EnableDocumentDBStorage</p></li>
     <li><p>GlobalDocumentStorageUseNetworkShare</p></li>
     <li><p>EnableFIPS</p></li>
     <li><p>EnableWSDL</p></li>
     <li><p>DataServicesConfigFile </p></li>
     <li><p>EnableRDS</p></li>
    </ul><p></p></td> 
  </tr> 
  <tr>
   <td><p>SystemInfo.database</p></td> 
   <td><p>https://[server]:[port]/rest/services/ SystemInfo.database</p></td> 
   <td><p>データベースに関する詳細な情報を取得します。</p></td> 
  </tr> 
  <tr>
   <td><p>SystemInfo.licenseInfo</p></td> 
   <td><p>https://[server]:[port]/rest/services/ SystemInfo.licenseInfo</p></td> 
   <td><p>インストールされているAEM forms コンポーネントのバージョンおよびライセンス情報を取得します。 </p></td> 
  </tr> 
  <tr>
   <td><p>SystemInfNo.serverConfig</p></td> 
   <td><p>https://[server]:[port]/rest/services/ SystemInfo.serverConfig</p></td> 
   <td><p>ホストアプリケーションサーバーの設定ファイルをダウンロードします。 </p></td> 
  </tr> 
  <tr>
   <td><p>SystemInfo.threads?delay=[n]&amp;iterations=[n]</p></td> 
   <td><p>https://[server]:[port]/rest/services/ SystemInfo.threads?delay=[n]&amp;iterations=[n]</p></td> 
   <td><p>アクティブなスレッドの数とスタックトレースを取得します。 次のパラメーターを受け入れます。</p>
    <ul>
     <li><p>iterations= [n]:繰り返し回数を指定します。 n を数値で置き換えます。 </p></li>
     <li><p>遅延= [n]:次の反復を開始する前に待機する時間（ミリ秒）を指定します。 </p></li>
    </ul><p></p></td> 
  </tr> 
  <tr>
   <td><p>SystemInfo.info</p></td> 
   <td><p>https://[server]:[port]/rest/services/ SystemInfo.info</p></td> 
   <td><p>この API は、すべてのシステム情報サービス API のラッパーです。 内部的には、すべてのシステム情報 API を実行し、情報を zip 形式でダウンロードします。 </p><p><i><strong>注意</strong>：SystemInfo.info はアクティブなスレッドの数とスタックトレースを提供しません。 </i></p></td> 
  </tr> 
 </tbody> 
</table>
