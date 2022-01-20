---
title: コミュニティコンポーネントの clientlib
seo-title: Clientlibs for Communities Components
description: Communities 用のクライアント側ライブラリ
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
ht-degree: 62%

---

# コミュニティコンポーネントの clientlib {#clientlibs-for-communities-components}

## はじめに {#introduction}

ドキュメントのこの節では、コミュニティコンポーネント用のクライアント側ライブラリ（clientlib）をページに追加する方法について説明します。

基本情報については、以下を参照してください。

* [クライアント側ライブラリの使用](../../help/sites-developing/clientlibs.md) 使用状況の詳細とデバッグツールを提供します。
* [SCF の clientlibs](client-customize.md#clientlibs) SCF コンポーネントをカスタマイズする際に役立つ情報を提供します。

## clientlib が必要になる理由 {#why-clientlibs-are-required}

コンポーネントを正しく機能させ（JavaScript）、スタイル設定する（CSS）には、clientlib が必要です。

が存在する場合、 [コミュニティ機能](functions.md) 機能の場合、必要な clientlib を含む必要なすべてのコンポーネントと設定がコミュニティサイトに表示されます。 作成者が追加のコンポーネントを使用できる場合にのみ、追加の clientlib を追加する必要があります。

必須の clientlib が欠落していると、[ページにコミュニティコンポーネントを追加](author-communities.md)したときに、JavaScript エラーが発生したり、予期しない外観が生じたりする可能性があります。

### 例：clientlib が欠落している場合のレビューの配置 {#example-placed-reviews-without-clientlibs}

![chlimage_1-244](assets/chlimage_1-244.png)

### 例：clientlib が存在する場合のレビューの配置 {#example-placed-reviews-with-clientlibs}

![chlimage_1-245](assets/chlimage_1-245.png)

## 必須の clientlib の識別 {#identifying-required-clientlibs}

開発者向けの基本機能情報の中で、必須の clientlib が識別されています。

また、AEM インスタンスから[コミュニティコンポーネントガイド](components-guide.md)を参照すると、コンポーネントに必須の clientlib カテゴリのリストにアクセスできます。

例えば、 [レビューページ](http://localhost:4502/content/community-components/en/reviews.html) 以下に、必要な clientlib を示します。

* cq.ckeditor
* cq.social.hbs.reviews

![chlimage_1-246](assets/chlimage_1-246.png)

## 必須の clientlib の追加 {#adding-required-clientlibs}

コミュニティコンポーネントをページに追加する場合、コンポーネントに必須の clientlib がまだ存在しなければ、追加する必要があります。

[CRXDE|Lite](#using-crxde-lite) を使用すると、コミュニティサイトページの既存の clientlibslist を変更できます。

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
      * 「**[!UICONTROL OK]**」を選択します。
   * 「**[!UICONTROL すべて保存]**」を選択します。



>[!NOTE]
>
>コミュニティサイト以外のサイトでは、使用されているクライアントライブラリの有無や場所を調べる必要があります。

ここでは、[AEM Communities 使用の手引き](getting-started.md)の例（`site-name` は *engage*）を引用し、レビューコンポーネントを追加する場合に clientliblist がどのように表示されるかを示しています。

![chlimage_1-247](assets/chlimage_1-247.png)
