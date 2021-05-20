---
title: アセットインサイトに対するデモパッケージの使用
description: デモパッケージを使用して、Adobeアセットインサイトを有効にし、Webページのデータを取り込んでインサイトを生成します。
contentOwner: AG
feature: アセットインサイト，アセットレポート
role: Business Practitioner,Administrator
exl-id: c6d321f5-4c48-47f2-bff1-c4da988c0e84
source-git-commit: edba9586711ee5c0e5549dbe374226e878803178
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 59%

---

# アセットインサイトにデモパッケージを使用する{#using-demo-package-for-asset-insights}

デモパッケージを使用すると、Adobeアセットインサイトを有効にして、サンプルWebページのデータを取り込み、インサイトを生成できます。

## サンプル Web ページに対する AEM アセットインサイトの使用  {#using-aem-assets-insights-with-sample-web-page}

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
