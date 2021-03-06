---
title: コレクションの管理
seo-title: Managing Collections
description: コレクションは、カバーのテーマに適した記事やバナーなどのコンテンツを集めた、適切に定義されたグループです。このページでは、この機能について詳しく見ていきます。
seo-description: Collections represent a well defined bucket filled with content such as articles or banners that suits the cover's theme. Follow this page to learn more.
uuid: 1d2e9769-d2cc-4d43-a428-e962a51eb5d0
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/MOBILE
topic-tags: authoring-on-demand-services-app
discoiquuid: 64c6d198-983f-4a52-9c83-560206363868
exl-id: fc83cd28-2fd6-4136-839b-b48a69ca75d0
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '797'
ht-degree: 83%

---

# コレクションの管理{#managing-collections}

>[!NOTE]
>
>アドビは、シングルページアプリケーションフレームワークをベースにしたクライアント側のレンダリング（React など）を必要とするプロジェクトには SPA エディターを使用することをお勧めします。[詳細情報](/help/sites-developing/spa-overview.md)

コンテンツ管理アクションは、アプリケーション内でコンテンツを作成および管理するのに役立つ構築ブロックです。アプリケーション内のコンテンツに対して以下のアクションを実行します。

## コレクションの概要 {#collections-overview}

コレクションは適切に定義された *バケット* カバーのテーマに合った記事やバナーなどのコンテンツがいっぱいになっています。

>[!NOTE]
>
>AEM Mobile アプリの以下のトピックについては、オンラインヘルプの以下のリソースを参照してください。
>
>* [デザインに関する考慮事項](https://helpx.adobe.com/jp/digital-publishing-solution/help/design-app.html)
>
>* [コレクションの管理](https://helpx.adobe.com/jp/digital-publishing-solution/help/creating-collections.html)

>


## コレクションの作成 {#creating-a-collection}

コレクションを作成する一般的なワークフローは以下のとおりです。

1. サイドレールから「**モバイル**」を選択します。
1. モバイルで、カタログから Mobile On-Demand アプリを選択します。
1. **コレクションを管理**&#x200B;タイルの右上隅にある下矢印をクリックします。
1. ウィザードの各ステップで必要な情報を入力して、新しいコレクションの作成を続行します。
1. 準備ができたら、「**作成**」をクリックします。
1. **コレクションを管理**&#x200B;タイルに新しいコレクションが表示されます。

![chlimage_1-1](assets/chlimage_1-1.gif)

## 新しいコレクションの読み込み {#importing-a-new-collection}

既存の Mobile On-Demand コンテンツを Mobile On-Demand から AEM にダウンロードする（読み込む）ことができます。これにより、ローカルのコンテンツを編集および表示できます。

>[!NOTE]
>
>読み込みには画像は含まれません。

新しいコレクションを読み込むワークフローは以下のとおりです。

1. Mobile から、カタログから Mobile On-Demand アプリを選択します。
1. **コレクションを管理**&#x200B;タイルの右上隅にある下矢印をクリックして、「コレクションを読み込む」を選択します。
1. ダイアログで「**コレクションを読み込む**」をクリックし、「閉じる」をクリックします。
1. Mobile On-Demand コレクションが **コレクションを管理** タイル。

>[!CAUTION]
>
>最初に Mobile On-Demand の接続を関連付ける必要があります。

## コレクションの編集 {#editing-a-collection}

記事を追加または変更するには、組み込みの AEM ドラッグ＆ドロップエディターを使用します。テキストや画像などのコンポーネントを追加したり、削除したりすることができます。DAM アセットの画像を挿入することもできます。

コレクションを編集するワークフローは以下のとおりです。

1. モバイルで、カタログから Mobile On-Demand アプリを選択します。
1. 次の場所からAEMソースの記事を選択 **コレクションを管理** タイル。
1. リスト表示で、ハイライトされたコレクションをクリックし、コンテンツエディターで開きます。
1. コンテンツエディターを使用して、コレクションの内容（原稿、画像、テキストなど）をドラッグします。

### コレクション内のメタデータの表示および編集 {#viewing-and-editing-the-metadata-within-a-collection}

コレクションには、タイトル、説明、画像など多くのプロパティがあります。このようなプロパティを表示および変更するには、この操作を使用します。オプションで、保存時に Mobile On-Demand に変更内容をアップロードすることもできます。

コレクションを表示／編集する一般的なワークフローは以下のとおりです。

1. モバイルで、カタログから Mobile On-Demand アプリを選択します。
1. 次の場所からコレクションを選択： **コレクションを管理** タイル。

1. アクションバーから「**プロパティ**」を選択します。
1. コレクションの使用可能なすべてのメタデータを確認します。
1. 必要に応じてメタデータを編集し、終わったら「**保存**」をクリックします。
1. オプションで、変更内容を直ちに Mobile On-Demand にアップロードします。

## コレクションのアップロード {#uploading-a-collection}

アップロード操作では、選択したコンテンツがコピーされ、 Mobile On-Demand プロジェクトに追加されます。既存の Mobile On-Demand コンテンツは新しいバージョンに置き換えられます。

コレクションをアップロードする一般的なワークフローは以下のとおりです。

1. 送信者 **モバイル**」で、カタログから Mobile On-Demand アプリを選択します。
1. 内 **コレクションを管理** タイルで、Mobile On-Demand にアップロードする記事を選択します。
1. 必要に応じて、リスト表示からさらにコレクションを追加します。
1. アクションバーから「**アップロード**」を選択し、ダイアログで「アップロード」をクリックします。
1. コレクションが Mobile On-Demand にアップロードされました。

## コレクションの削除 {#deleting-a-collection}

この操作を実行すると、選択したコレクションが Mobile On-Demand から削除され、必要に応じてローカルのAEMインスタンスからも削除されます。

コレクションを削除する一般的なワークフローは以下のとおりです。

1. モバイルで、カタログから Mobile On-Demand アプリを選択します。
1. **コレクションを管理**&#x200B;タイルで、削除するコレクションを選択します。
1. 削除するコレクションがリスト内で選択されていることを確認します（必要に応じて、削除する他のコレクションを選択します）。
1. アクションバーから「**削除**」をクリックします。
1.  Mobile On-Demand だけでなく、AEM からも削除するかどうかを確認します。
1. 「**削除**」をクリックします。
1. コレクションがリストから削除されます。

## コレクションへのコンテンツの追加 {#adding-content-to-collections}

コレクションは基本的に、関連するコンテンツのカテゴリです。コレクションによって、アプリケーションのナビゲーション構造を定義するパッケージに記事やバナーなどのコンテンツが収集されます。コレクションはネスト可能です。

>[!NOTE]
>
>コンテンツをコレクションに追加する前に、Mobile On-Demand にアップロードする必要があります。

コレクションは基本的に、関連するコンテンツのカテゴリです。コレクションによって、アプリケーションのナビゲーション構造を定義するパッケージに記事やバナーなどのコンテンツが収集されます。コレクションはネスト可能です。

1. モバイルで、カタログから Mobile On-Demand アプリを選択します。
1. 以前にアップロードした記事（またはバナー／コレクション）を選択します。
1. アクションバーから「追加」を選択します。
1. 以前にアップロードしたコレクションをダイアログから選択します。
1. 「**更新**」をクリックして、コレクションにコンテンツを追加します。

![chlimage_1-2](assets/chlimage_1-2.gif)

### 次の手順 {#the-next-steps}

コレクションの管理について学習したら、以下を参照してください。

* [バナーの管理](/help/mobile/mobile-on-demand-managing-banners.md)
* [記事の管理](/help/mobile/mobile-on-demand-managing-articles.md)
* [共有リソースのアップロード](/help/mobile/mobile-on-demand-shared-resources.md)
* [コンテンツの公開／非公開](/help/mobile/mobile-on-demand-publishing-unpublishing.md)
* [プリフライトによるプレビュー](/help/mobile/aem-mobile-manage-ondemand-services.md)
