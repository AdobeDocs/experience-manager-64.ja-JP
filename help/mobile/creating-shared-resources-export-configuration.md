---
title: 共有リソースのエクスポート設定の作成
seo-title: Creating Shared Resources Export Configuration
description: このページでは、Adobe Experience Manager(AEM) からAEM Mobileにアップロードする共有リソースを書き出す方法について説明します。
seo-description: Follow this page to learn about exporting shared resources from Adobe Experience Manager (AEM) for upload to AEM Mobile.
uuid: 99b8ff94-8135-4643-a15b-aa6fb91f5401
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/MOBILE
topic-tags: developing-on-demand-services-app
discoiquuid: 1edf6c76-ccb1-40b6-bdf6-924f1461cd28
exl-id: 92ee8c25-9f11-4743-a8e6-1f4986d09a6a
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 6%

---

# 共有リソースのエクスポート設定の作成{#creating-shared-resources-export-configuration}

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

次のリソースでは、Adobe Experience Manager(AEM) から共有リソースを書き出してAEM Mobileにアップロードする方法について説明します。

共有HTMLリソースを使用すると、HTMLリソースを共有できます。記事が共有されていない場合は、すべての記事で複製する必要があります。また、アイコン、フォント、JavaScript、CSS を含めることができます。

コンテンツ同期設定が次の場所に見つかりました： **&lt;dps-exporttemplate>/dps-HTMLResources>** は、デバイス上のプロパティの静的レンダリングに必要なすべてのコンテンツと記事を書き出すように設定する必要があります。

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
1. このパスを参照 *[/etc/contentsync/templates/dps-we-unlimited-app/dps-HTMLResources](http://localhost:4502/crx/de/index.jsp#/etc/contentsync/templates/dps-we-unlimited-app/dps-HTMLResources)*、サンプルの共有リソースを表示します。

   共有リソースの作成に必要なすべてのプロパティを次の図に示すように表示できます。

   ![chlimage_1-145](assets/chlimage_1-145.png)

>[!NOTE]
>
>共有リソースのいずれかが変更された場合は、AEM Mobile On-demand Servicesにアップロードまたは書き出す必要があります。
