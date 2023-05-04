---
title: 記事のエクスポート設定の作成
seo-title: Creating Article Export Configuration
description: このページでは、Adobe Experience Manager(AEM) からAEM Mobileにアップロードするコンテンツを書き出す方法について説明します。
seo-description: Follow this page to learn about exporting content from Adobe Experience Manager (AEM) for upload to AEM Mobile.
uuid: 089bc15b-669e-4623-bdbb-fd9abf46e098
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/MOBILE
topic-tags: developing-on-demand-services-app
discoiquuid: bc681589-5d46-44cd-888d-b0722a2fd006
exl-id: d6e8412d-09d4-4cac-a691-71703ebaa374
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '335'
ht-degree: 5%

---

# 記事のエクスポート設定の作成{#creating-article-export-configuration}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

>[!NOTE]
>
>Adobeは、単一ページアプリケーションのフレームワークベースのクライアントサイドレンダリング（React など）を必要とするプロジェクトでは、SPA Editor を使用することをお勧めします。 [詳細情報](/help/sites-developing/spa-overview.md)を参照してください。

>[!CAUTION]
>
>**前提条件**:
>
>共有リソースの作成と変更について詳しくは、 [コンテンツ同期](/help/mobile/mobile-ondemand-contentsync.md) を参照してください。

AEM Mobileのユーザーは、コンテンツ同期を使用して、ライブコンテンツをモバイルアプリで使用する静的コンテンツに書き出します。この書き出しは、AEM Mobileから Mobile On-Demand Services にコンテンツがアップロードされたときに発生します。

プロパティ ***dps-exportTemplate*** 上記の表で、アプリの書き出し設定へのパスを定義します。 共有リソースを作成および変更するには、このプロパティを設定します。

次のリソースでは、Adobe Experience Manager(AEM) からコンテンツを書き出してAEM Mobileにアップロードする方法について説明します。

記事には、書き出しとアップロードが必要なコンテンツが含まれています。 このコンテンツの一部は、記事間で共有できます。

用途 [コンテンツ同期](/help/mobile/mobile-ondemand-contentsync.md) コンテンツをまとめて ***共有リソース*** パッケージ。

次の場所に ContentSync 設定が見つかりました： **&lt;dps-exporttemplate>/dps-article>** は、デバイス上のプロパティの静的レンダリングに必要なすべてのコンテンツと記事を書き出すように設定する必要があります。

>[!CAUTION]
>
>以下の手順を実行して、以下の場合に限り、サンプルの共有リソースを表示できます。
>
>* サンプルコンテンツをインストール済み
>* 実行中のAEMインスタンス
>* カスタムコンテキストが設定されていないか、別のポートがありません
>


サンプルの共有リソースを表示するには、以下の手順を参照してください。

1. AEMサーバーのCRXDE Liteを開きます。
1. このパスを参照 [/etc/contentsync/templates/dps-we-unlimited-app/dps-article](http://localhost:4502/crx/de/index.jsp#/etc/contentsync/templates/dps-we-unlimited-app/dps-article)、サンプルの共有リソースを表示します。

   共有リソースの作成に必要なすべてのプロパティを次の図に示すように表示できます。

   ![chlimage_1-134](assets/chlimage_1-134.png)

>[!NOTE]
>
>記事のコンテンツが変更された場合は、AEM Mobile On-demand Servicesに記事をアップロードまたは書き出す必要があります。
