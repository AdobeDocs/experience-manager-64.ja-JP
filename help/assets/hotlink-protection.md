---
title: Dynamic Media でのホットリンク保護の有効化
seo-title: Activating hotlink protection in Dynamic Media
description: Dynamic Mediaでホットリンク保護を有効にする方法に関する情報です。
seo-description: Information on how to activate hotlink protection in Dynamic Media.
uuid: 5f93bc27-5edd-4143-8701-87896c52f0af
contentOwner: Rick Brough
topic-tags: dynamic-media
products: SG_EXPERIENCEMANAGER/6.4/ASSETS
content-type: reference
discoiquuid: a70aa448-0f58-4ed2-9381-afcc76fa827f
exl-id: 9e27d45e-1d72-4663-a2c5-2ec48f2b23c4
feature: Asset Management
role: Admin,User
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '205'
ht-degree: 47%

---

# Dynamic Media でのホットリンク保護の有効化 {#activating-hotlink-protection-in-dynamic-media}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

ホットリンクは、サードパーティの Web サイトで HTML コードを使用して自社 Web サイト内の画像を表示する場合におこなわれます。訪問者のブラウザーが自社サーバーから画像に直接アクセスするので、画像が要求されるたびに帯域幅が消費されます。ホットリンク&#x200B;*保護*&#x200B;は、自社 web サイト上の画像、CSS、JavaScript などに他の web サイトが直接リンクできないようにするための方法です。このような保護により、Dynamic Media アカウントでの不要な帯域幅使用を減らすことができます。

[Adobeカスタマーサポート](https://experienceleague.adobe.com/?support-solution=Experience+Manager&amp;lang=ja#support) は、CDN レベルでリファラーフィルターを設定し、ドメインに許可された Web サイトにのみDynamic Mediaコンテンツを提供できるようにします。

ホットリンク保護を使用するには、Adobeにバンドルされた CDN を使用する必要があります。 ホットリンク保護を有効にするには、管理者がサポートチケットを作成して、Dynamic Mediaアカウントに対する設定の変更をリクエストする必要があります。 ホットリンク保護を有効にするための追加費用は発生しません。
