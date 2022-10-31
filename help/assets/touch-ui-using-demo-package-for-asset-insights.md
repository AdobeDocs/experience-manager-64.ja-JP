---
title: アセットインサイトにデモパッケージを使用する
description: デモパッケージを使用して、アセットインサイトで web ページからデータを取得し、web ページのインサイトを生成できるようにします。
contentOwner: AG
feature: Asset Insights,Asset Reports
role: User,Admin
exl-id: c6d321f5-4c48-47f2-bff1-c4da988c0e84
source-git-commit: 1e3cd6ce3138113721183439f7cfb9daed6e0e58
workflow-type: tm+mt
source-wordcount: '162'
ht-degree: 79%

---

# アセットインサイトにデモパッケージを使用する {#using-demo-package-for-asset-insights}

デモパッケージを使用して、アセットインサイトでサンプル web ページからデータを取得し、サンプル web ページのインサイトを生成できるようにします。

## 使用 [!DNL Experience Manager] サンプル Web ページを使用したアセットインサイト  {#using-aem-assets-insights-with-sample-web-page}

1. [アセットインサイトの設定](touch-ui-configuring-asset-insights.md)の手順を使用してアセットインサイトを設定します。
1. サンプルをダウンロード [!DNL Experience Manager] 下のアセットパッケージから、CRXDE パッケージマネージャーからパッケージをインストールします。

[ファイルを入手](assets/insightsdemo.zip)

1. 次に示すサンプル web ページを含む ZIP ファイルをダウンロードして、ローカルファイルシステムに抽出します。

[ファイルを入手](assets/demosite.zip)

1. Web ページをクリックして Web ブラウザーで開きます。

   >[!CAUTION]
   >
   >Web ページは localhost のサーバーからアセットを読み込むように設定されます。サーバーが別の場所で実行している場合は、localhost のサーバーアドレスを Web ページの HTML コンテンツのサーバーアドレスに変更してください。

   >[!NOTE]
   >
   >外部の web ページは、[!DNL Experience Manager] 自体でホストされたものでもかまいません。
