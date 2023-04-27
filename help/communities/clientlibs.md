---
title: コミュニティコンポーネントの clientlib
seo-title: Clientlibs for Communities Components
description: コミュニティ用のクライアント側ライブラリ
seo-description: Client-side libraries for Communities
uuid: 0a62f629-e6af-4269-862e-0595824c329f
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.4/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 7d423dff-8710-4f43-ad55-8863169946e2
exl-id: 9b4ed16f-3c7c-478a-a897-9b4be086988b
source-git-commit: 9178c3a01e7f450d3794f41605fb3788231c88c0
workflow-type: tm+mt
source-wordcount: '382'
ht-degree: 4%

---

# コミュニティコンポーネントの clientlib {#clientlibs-for-communities-components}

## はじめに {#introduction}

この節では、コミュニティコンポーネント用のページにクライアント側ライブラリ (clientlibs) を追加する方法について説明します。

基本情報については、以下を参照してください。

* [クライアント側ライブラリの使用](../../help/sites-developing/clientlibs.md) 使用状況の詳細とデバッグツールを提供します。
* [SCF の clientlibs](client-customize.md#clientlibs) SCF コンポーネントをカスタマイズする際に役立つ情報を提供します。

## clientlibs が必要な理由 {#why-clientlibs-are-required}

コンポーネントが適切に機能し (JavaScript)、スタイル設定 (CSS) されるには、clientlibs が必要です。

が存在する場合、 [コミュニティ機能](functions.md) 機能の場合、必要な clientlib を含む必要なすべてのコンポーネントと設定がコミュニティサイトに表示されます。 作成者が追加のコンポーネントを使用できる場合にのみ、追加の clientlib を追加する必要があります。

必要な clientlib が見つからない場合、 [ページへのコミュニティコンポーネントの追加](author-communities.md) により、javascript エラーが発生し、予期しない外観が発生する可能性がありました。

### 例：Clientlibs を使用しない場合のレビューの配置 {#example-placed-reviews-without-clientlibs}

![chlimage_1-244](assets/chlimage_1-244.png)

### 例：Clientlibs でのレビューの配置 {#example-placed-reviews-with-clientlibs}

![chlimage_1-245](assets/chlimage_1-245.png)

## 必要な clientlib の識別 {#identifying-required-clientlibs}

開発者向けの基本的な機能情報は、必要な clientlib を特定します。

さらに、AEMインスタンスから [コミュニティコンポーネントガイド](components-guide.md) では、コンポーネントに必要な clientlib カテゴリのリストにアクセスできます。

例えば、 [レビューページ](http://localhost:4502/content/community-components/en/reviews.html) 以下に、必要な clientlib を示します。

* cq.ckeditor
* cq.social.hbs.reviews

![chlimage_1-246](assets/chlimage_1-246.png)

## 必要な clientlib の追加 {#adding-required-clientlibs}

コミュニティコンポーネントをページに追加する場合は、そのコンポーネントに必要な clientlib を追加する必要があります（まだ追加していない場合）。

用途 [CRXDE|Lite](#using-crxde-lite) コミュニティサイトページの既存の clientlibslist を変更する場合。

を使用してコミュニティサイトに clientlib を追加するには [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md):

* 参照先 [https://&lt;server>:&lt;port>/crx/de](http://localhost:4502/crx/de)
* を `clientlibslist` コンポーネントを追加するページのノード

   * `/content/sites/sample/en/page/jcr:content/clientlibslist`

* を使用 `clientlibslist` 選択されたノード

   * 文字列[] プロパティ `scg:requiredClientLibs`
   * 選択 `Value` 「文字列配列」ダイアログにアクセスするには

      * 必要に応じて下にスクロールします。
      * 選択 `+` 新しいクライアントライブラリに入るには

         * 繰り返してクライアントライブラリをさらに追加します
      * 選択 **[!UICONTROL OK]**
   * 選択 **[!UICONTROL すべて保存]**



>[!NOTE]
>
>サイトがコミュニティサイトでない場合は、そのサイトで使用されているクライアントライブラリの存在または場所を検出する必要があります。

の使用 [AEM Communitiesの概要](getting-started.md) 例： `site-name` が *エンゲージ*&#x200B;レビューコンポーネントを追加すると、clientliblist は次のように表示されます。

![chlimage_1-247](assets/chlimage_1-247.png)
