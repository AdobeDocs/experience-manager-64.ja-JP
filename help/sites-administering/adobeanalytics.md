---
title: Adobe Analytics との統合
seo-title: Adobe Analytics との統合
description: AEM と Adobe Analytics を統合する方法について説明します。
seo-description: AEM と Adobe Analytics を統合する方法について説明します。
uuid: 8329d891-1897-46f6-80ee-40244b079c0e
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: integration
content-type: reference
discoiquuid: 0089394f-0107-49eb-ad73-52e9cabe71b1
translation-type: tm+mt
source-git-commit: ee380780bb7b62d348051b29edb9d13e14407377

---


# Adobe Analytics との統合{#integrating-with-adobe-analytics}

Adobe Analytics と AEM の統合により、Web ページのアクティビティを追跡できます。

* Adobe Analytics 設定により、AEM で Adobe Analytics を認証できます。
* フレームワークは、Adobe Analyticsレポートスイートに送信されるデータを識別します。

データには、次のようなページおよびユーザーデータが含まれます。

* AEM コンポーネントが収集するデータ
* リンククリック数
* ビデオ使用量情報
* Adobe Analytics から訪問するページ数

統合の設定に役立つ情報は、次のページにあります。

* [Adobe Analytics への接続とフレームワークの作成](/help/sites-administering/adobeanalytics-connect.md)
* [Adobe Analytics のリンクトラッキングの設定](/help/sites-administering/adobeanalytics-link.md)
* [コンポーネントデータと Adobe Analytics プロパティとのマッピング](/help/sites-administering/adobeanalytics-mapping.md)
* [Adobe Analytics のビデオトラッキングの設定](/help/sites-administering/adobeanalytics-video.md)

また、[オプトインウィザード](/help/sites-administering/opt-in.md)を使用して簡単に統合を実行できます。

>[!NOTE]
>
>方法については、[DTM を使用した AEM と Adobe Target および Adobe Analytics の統合（英語）](https://helpx.adobe.com/experience-manager/using/integrate-digital-marketing-solutions.html)も参照してください。

## その他の情報 {#further-information}

次のページを参照してください。

* [Adobe Analytics統合の拡張を参照してください](/help/sites-developing/extending-analytics.md) 。
* The knowledge base article, [Adobe Analytics integration - troubleshooting issues](https://helpx.adobe.com/experience-manager/kb/sitecatalystintegrationtroubleshooting.html), for information about troubleshooting your Adobe Analytics integration.

>[!NOTE]
>
>Adobe Analytics をカスタムプロキシ設定で使用している場合、（例えば、Web コンソールで）**Apache HTTP Client** プロキシ設定に必要な [2 つの OSGi バンドルを設定](/help/sites-deploying/configuring-osgi.md)する必要があります。AEM の一部の機能では 3.x API を使用し、他の機能では 4.x API を使用するので、両方とも必要です。次の設定をおこないます。
>
>* **Day Commons HTTP Client 3.1** to configure the 3.x API;\
   >  for example, [http://localhost:4502/system/console/configMgr/com.day.commons.httpclient](http://localhost:4502/system/console/configMgr/com.day.commons.httpclient)
   >
   >
* **Apache HTTPコンポーネントプロキシ設定** （4.x APIを設定）\
   >  for example, [http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator](http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator)
>



