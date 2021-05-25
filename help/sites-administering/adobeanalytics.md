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
exl-id: ca11bfcd-06d1-4ca9-9069-afa91d8a6610
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '302'
ht-degree: 94%

---

# Adobe Analytics との統合{#integrating-with-adobe-analytics}

Adobe Analytics と AEM の統合により、Web ページのアクティビティを追跡できます。

* Adobe Analytics 設定により、AEM で Adobe Analytics を認証できます。
* Adobe Analytics レポートスイートに送信されたデータはフレームワークで特定されます。

データには、次のようなページおよびユーザーデータが含まれます。

* AEM コンポーネントで収集されるデータ
* リンククリック数
* ビデオ使用量情報
* Adobe Analytics から訪問されるページの数

統合の設定に役立つ情報は、次のページにあります。

* [Adobe Analytics への接続とフレームワークの作成](/help/sites-administering/adobeanalytics-connect.md)
* [Adobe Analytics のリンクトラッキングの設定](/help/sites-administering/adobeanalytics-link.md)
* [コンポーネントデータと Adobe Analytics プロパティとのマッピング](/help/sites-administering/adobeanalytics-mapping.md)
* [Adobe Analytics のビデオトラッキングの設定](/help/sites-administering/adobeanalytics-video.md)

また、[オプトインウィザード](/help/sites-administering/opt-in.md)を使用して簡単に統合を実行できます。

>[!NOTE]
>
>方法については、[DTM を使用した AEM と Adobe Target および Adobe Analytics の統合（英語）](https://helpx.adobe.com/jp/experience-manager/using/integrate-digital-marketing-solutions.html)も参照してください。

## その他の情報 {#further-information}

次のページを参照してください。

* ユーザーデータを収集するコンポーネントの開発と Adobe Analytics フレームワークのカスタマイズに関する情報については、[Adobe Analytics 統合の拡張](/help/sites-developing/extending-analytics.md)を参照してください。
* Adobe Analytics 統合のトラブルシューティングに関する情報については、[Adobe Analytics 統合 - 問題のトラブルシューティング](https://helpx.adobe.com/jp/experience-manager/kb/sitecatalystintegrationtroubleshooting.html)に関するナレッジベースの記事を参照してください。

>[!NOTE]
>
>Adobe Analytics をカスタムプロキシ設定で使用している場合、（例えば、Web コンソールで）**Apache HTTP Client** プロキシ設定に必要な [2 つの OSGi バンドルを設定](/help/sites-deploying/configuring-osgi.md)する必要があります。AEM の一部の機能では 3.x API を使用し、他の機能では 4.x API を使用するので、両方とも必要です。設定：
>
>* **Day Commons HTTP Client 3.1**（3.x API を設定）。\
   >  例： [http://localhost:4502/system/console/configMgr/com.day.commons.httpclient](http://localhost:4502/system/console/configMgr/com.day.commons.httpclient)
   >
   >
* **Apache HTTP コンポーネントプロキシ設定**（4.x API を設定）。
>
>  
例： [http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator](http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator)
