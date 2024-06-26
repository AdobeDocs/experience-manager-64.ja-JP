---
title: AEM Mobile On-Demand
seo-title: AEM Mobile On-Demand
description: 新しいAEM Mobileアプリエクスペリエンスを開始するには、コンテンツ編集の準備が整う前に、複数の役割を組み合わせる必要があります。 このページでは、AEM Mobile On-Demand サービスの概要について説明します。
seo-description: Starting a new AEM Mobile app experience requires a cohesion of roles before it is ready for content editing. Follow this page to get started with AEM mobile On-Demand services.
uuid: 175c609d-3cb8-4a1b-bfea-278df272e500
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.4/MOBILE
topic-tags: introduction
content-type: reference
discoiquuid: dc6891cd-19cc-4dff-8bda-a41ed8af8bfb
exl-id: 0bd0040d-6890-4b5e-b6bd-5b235408ba23
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '807'
ht-degree: 5%

---

# AEM Mobile On-Demand{#aem-mobile-on-demand}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

>[!NOTE]
>
>Adobeは、単一ページアプリケーションのフレームワークベースのクライアントサイドレンダリング（React など）を必要とするプロジェクトでは、SPA Editor を使用することをお勧めします。 [詳細情報](/help/sites-developing/spa-overview.md)を参照してください。

>[!NOTE]
>
>AEMをコンテンツ管理ソースとして使用していない場合は、 [AEM Mobile On-demand Services Help](https://helpx.adobe.com/digital-publishing-solution/topics.html).

AEMには、コンテンツをモバイルアプリケーションに統合するためのツールがいくつか用意されています。

次の図は、AEM Mobileと On-Demand Services の様々なコンポーネントがどのように組み合わされて、モバイルアプリにコンテンツを配信するかを示しています。

AEM Preflight アプリは、公開前にアプリとコンテンツをプレビューするテスト環境と見なすことができます。一方、AEM Mobile App は、配布用に構築された最終的なアプリです。

>[!NOTE]
>
>プリフライトアプリについて詳しくは、 [AEM Preflight アプリの使用](https://helpx.adobe.com/digital-publishing-solution/help/preflight-app.html) (AEM Mobile On-demand Servicesヘルプ )

![chlimage_1-171](assets/chlimage_1-171.png)

>[!NOTE]
>
>上の図では、AEM Mobile On-demand Servicesへの一般的なデプロイメントシナリオには、AEM パブリッシュインスタンスは必要ありません。

## 新しいモバイルアプリの開始 {#starting-a-new-mobile-app}

AEM Mobileは、AEMプラットフォーム全体を構成する 1 つの柱に過ぎません。

新しいAEM Mobileアプリエクスペリエンスを開始するには、コンテンツ編集の準備が整う前に、複数の役割を組み合わせる必要があります。 新しいAEM Mobileアプリケーションを作成する出発点となる役割は次のとおりです。

* **管理者**
* **開発者**
* **作成者**

>[!NOTE]
>
>AEM Mobileを操作し、この入門ガイドの手順に従う前に、AEMに関する知識が必要です。 AEMの基本を学ぶ [ここ](/help/sites-deploying/deploy.md).

### AEM Mobile Application Dashboard について {#understanding-the-aem-mobile-application-dashboard}

役割と責任を理解する前に、ユーザーは **AEM Mobile Control Center** または **アプリケーションダッシュボード**. クリック [ここ](/help/mobile/mobile-apps-ondemand-application-dashboard.md) を参照してください。

### AEM 管理者 {#aem-administrator}

An ***AEM administrator*** は、作成ウィザードを使用して新しいアプリを作成するか、既存のアプリを読み込むことで、AEM Mobileカタログに新しいアプリを追加します。 AEM Mobileを使用して新しいアプリを作成するAEM管理者 *作成ウィザード* 通常は、あらかじめ用意されている参照サンプルから目的のアプリテンプレートを 1 つ選択するか、（ほとんどの場合は） *AEM開発者。*

AEM管理者は、AEM Mobile On-demand Servicesを使用してアプリを作成する際に、次のタスクを実行します。

* [AEM Mobileの設定](/help/mobile/aem-mobile-setup.md)
* [ユーザーおよびユーザーグループの設定](/help/mobile/aem-mobile-configure-users.md)
* [プリフライトによるプレビュー](/help/mobile/aem-mobile-manage-ondemand-services.md)
* [コンテンツサービスの管理](/help/mobile/developing-content-services.md)

管理者の役割と責任の使用を開始するには、 [AEM Mobile On-demand Servicesを使用するコンテンツの管理](/help/mobile/aem-mobile.md).

## AEM Developer {#aem-developer}

An **AEM developer** は、カスタムの Web テンプレートおよびコンポーネントを拡張して作成することで、AEM オーサーインスタンスを活用して美しく魅力的なモバイルエクスペリエンスを作成できます。 これらのテンプレートとコンポーネントは、モバイルアプリの世界に最適化されているだけではありません。ただし、デバイスとAEMサーバー（任意のリモートサーバー）の両方をオムニチャネルサービスエンドポイントに通信します。 AEMの組み込みコンテンツエディターは、 *AEM 作成者* ：アプリ内で、他のAdobe Marketing Cloudとの統合を含む、豊富で関連性の高いエクスペリエンスを作成します。

AEM開発者は、AEM Mobile On-demand Servicesを使用してアプリを作成する際に、次のタスクを実行します。

* [アプリのテンプレートとコンポーネント](/help/mobile/app-templates-and-components1.md)
* [モバイルとコンテンツ同期](/help/mobile/mobile-ondemand-contentsync.md)
* [コンテンツプロパティとコンテンツの書き出し](/help/mobile/on-demand-content-properties-exporting.md)
* [AEM Mobile Content Services の開発](/help/mobile/developing-content-services.md)

開発者の役割と責務の概要については、 [AEM Mobile On-demand Services向けAEMコンテンツの開発](/help/mobile/aem-mobile-on-demand.md).

>[!NOTE]
>
>An *AEM developer&#39;s* の役割は、テンプレートとコンポーネントの開発で始まったり終わったりしません。 An *AEM developer* では、標準の参照実装サンプルを単に拡張するのではなく、まったく新しいアプリを作成できます。

## AEM オーサー {#aem-author}

An ***AEM オーサー* ( または *マーケター*)**は、カスタムで開発または標準搭載のテンプレートおよびコンポーネントを使用して、ページの追加と編集、コンポーネントのドラッグ&amp;ドロップ、DAM からのすべてのタイプのメディア（画像、ビデオ、テキストフラグメント）の追加をおこないます。 AEMの組み込みコンテンツエディターは、 *AEM 作成者* ：アプリ内で、他のAdobe Marketing Cloudとの統合を含む、豊富で関連性の高いエクスペリエンスを作成します。

AEMの作成者は、AEM Mobile On-demand Servicesを使用してアプリを作成する際に、次のトピックを理解する必要があります。

* [AEM Mobile アプリケーションのダッシュボード](/help/mobile/mobile-apps-ondemand-application-dashboard.md)
* [アプリケーションの作成および設定アクション](/help/mobile/mobile-apps-ondemand-application-create-configure-action.md)
* [クラウド設定](/help/mobile/mobile-on-demand-associating-an-on-demand-app-to-cloud-configuration.md)
* [コンテンツ管理](/help/mobile/mobile-apps-ondemand-manage-content-ondemand.md)
* [コンテンツサービスの概要](/help/mobile/develop-content-as-a-service.md)

作成者の役割と責務の概要については、 [AEM Mobile On-demand Servicesアプリ用AEMコンテンツのオーサリング](/help/mobile/mobile-apps-ondemand.md).

>[!NOTE]
>
>また、AEM 作成者は、権限の設定、カードとレイアウトの作成、プッシュ通知の送信も担当します。 また、コンテンツのオーサリング方法の詳細については、記事とコレクションの管理AEM Mobileでのバナー、カード、レイアウトの作成 ( [AEM Mobile On-Demand Portal](https://helpx.adobe.com/digital-publishing-solution/topics.html#dynamicpod_reference_2).
