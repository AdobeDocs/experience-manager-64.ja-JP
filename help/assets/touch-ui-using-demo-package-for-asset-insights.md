---
title: アセットインサイト用デモパッケージの使用
description: デモパッケージを使用して、AdobeアセットインサイトでWebページのデータをキャプチャし、インサイトを生成できるようにします。
contentOwner: AG
feature: Asset Insights,Asset Reports
role: User,Admin
exl-id: c6d321f5-4c48-47f2-bff1-c4da988c0e84
source-git-commit: 1e3cd6ce3138113721183439f7cfb9daed6e0e58
workflow-type: tm+mt
source-wordcount: '162'
ht-degree: 41%

---

# アセットインサイト用デモパッケージの使用 {#using-demo-package-for-asset-insights}

デモパッケージを使用して、AdobeアセットインサイトでサンプルWebページのデータをキャプチャし、インサイトを生成できます。

## サンプルWebページでの[!DNL Experience Manager]アセットインサイトの使用  {#using-aem-assets-insights-with-sample-web-page}

1. [アセットインサイトの設定](touch-ui-configuring-asset-insights.md)の手順に従って、アセットインサイトを設定します。
1. サンプルの[!DNL Experience Manager]アセットパッケージを下からダウンロードし、CRXDEパッケージマネージャーからパッケージをインストールします。

[ファイルを入手](assets/insightsdemo.zip)

1. 次に示すサンプル Web ページを含む ZIP ファイルをダウンロードして、ローカルファイルシステムに抽出します。

[ファイルを入手](assets/demosite.zip)

1. Web ページをクリックして Web ブラウザーで開きます。

   >[!CAUTION]
   >
   >Web ページは localhost のサーバーからアセットを読み込むように設定されます。サーバーが別の場所で実行している場合は、localhost のサーバーアドレスを Web ページの HTML コンテンツのサーバーアドレスに変更してください。

   >[!NOTE]
   >
   >外部Webページは、[!DNL Experience Manager]自体に含めることができます。
