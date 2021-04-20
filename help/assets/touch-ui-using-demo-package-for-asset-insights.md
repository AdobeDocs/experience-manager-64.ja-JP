---
title: アセットインサイトでのデモパッケージの使用
description: デモパッケージを使用して、アセットインサイトで Web ページからデータを取得し、Web ページのインサイトを生成できるようにします。
contentOwner: AG
feature: Asset Insights,Asset Reports
role: Business Practitioner,Administrator
translation-type: tm+mt
source-git-commit: 29e3cd92d6c7a4917d7ee2aa8d9963aa16581633
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 91%

---


# アセットインサイトでのデモパッケージの使用 {#using-demo-package-for-asset-insights}

デモパッケージを使用して、アセットインサイトでサンプル Web ページからデータを取得し、サンプル Web ページのインサイトを生成できるようにします。

## サンプル Web ページに対する AEM アセットインサイトの使用   {#using-aem-assets-insights-with-sample-web-page}

1. [アセットインサイトの設定](touch-ui-configuring-asset-insights.md)の手順に従って、アセットインサイトを設定します。
1. 次に示すサンプル AEM Assets パッケージをダウンロードして、CRXDE パッケージマネージャーでインストールします。

   [ファイルを入手](assets/insightsdemo.zip)

1. 次に示すサンプル Web ページを含む ZIP ファイルをダウンロードして、ローカルファイルシステムに抽出します。

   [ファイルを入手](assets/demosite.zip)

1. Web ページをクリックして Web ブラウザーで開きます。

   >[!CAUTION]
   >
   >Web ページは localhost のサーバーからアセットを読み込むように設定されます。サーバーが別の場所で実行している場合は、localhost のサーバーアドレスを Web ページの HTML コンテンツのサーバーアドレスに変更してください。

   >[!NOTE]
   >
   >外部の Web ページは、AEM 自体でホストされたものでもかまいません。
