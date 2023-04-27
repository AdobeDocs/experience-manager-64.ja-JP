---
title: コミュニティコンポーネントの基本
seo-title: Communities Components Basics
description: 編集モードでコミュニティ機能をAEMサイトに追加し、コンポーネントを設定する
seo-description: Add Communities features to AEM sites in edit mode and configure components
uuid: c017a7c5-40d1-4592-9317-96fd727dac86
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.4/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 21714581-7645-4b47-a9b0-9f1424013240
exl-id: 17fbee1c-5657-442a-8c9d-1456b853f666
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '365'
ht-degree: 6%

---

# コミュニティコンポーネントの基本 {#communities-components-basics}

## 概要 {#overview}

ドキュメントのオーサリングの節では、オーサー編集モードでAEMサイトにコミュニティ機能を追加する方法と、コンポーネント設定を説明する方法について説明します。

コンポーネントは、AEMインスタンスとインタラクティブを使用して確認できます [コミュニティコンポーネントガイド](components-guide.md).

## コミュニティコンポーネントへのアクセス {#accessing-communities-components}

ページコンテンツのオーサリング時に、基になるテンプレートがページのデザインに対する変更を許可している場合は、サイトデザインの一部としてコンポーネントブラウザーでまだ使用できないコンポーネントを有効にできます。

使用可能なコミュニティコンポーネントが一覧表示されます [ここ](author-communities.md#available-communities-components).

>[!NOTE]
>
>オーサリングに関する一般的な情報については、 [ページのオーサリングのクイックガイド](../../help/sites-authoring/qg-page-authoring.md).
>
>AEMに詳しくない場合は、 [基本操作](../../help/sites-authoring/basic-handling.md).

### デザインモードに入ります {#entering-design-mode}

次の場合、 **コミュニティ** コンポーネントがコンポーネントブラウザー（サイドキック）に見つからない場合は、 `Design Mode` をクリックして、他のコミュニティコンポーネントを追加します。 [必要なクライアント側ライブラリ](#required-clientlibs) (clientlibs) の追加も必要になる場合があります。

詳しくは、 [デザインモードでのコンポーネントの設定](../../help/sites-authoring/default-components-designmode.md).

次に、いくつかのコミュニティコンポーネントを選択し、コンポーネントブラウザーで表示する画像を示します。

![chlimage_1-424](assets/chlimage_1-424.png)

選択したコンポーネントがコンポーネントブラウザーで使用できるようになります。

![chlimage_1-425](assets/chlimage_1-425.png)

## 必須の clientlib {#required-clientlibs}

[クライアント側ライブラリ](../../help/sites-developing/clientlibs.md) (clientlibs) は、コンポーネントが適切に機能し (JavaScript)、スタイル設定 (CSS) されるために必要です。

コミュニティコンポーネントをページに追加する際に、エラーや予期しない外観が発生した場合は、最初に、コミュニティコンポーネントに必要な clientlib を追加します。 詳しくは、 [コミュニティコンポーネントの clientlib](clientlibs.md).

### 例：最初にクライアントライブラリのないレビューを配置… {#example-initially-placed-reviews-without-client-libraries}

![chlimage_1-426](assets/chlimage_1-426.png)

### ...およびクライアントライブラリ {#and-with-client-libraries}

![chlimage_1-427](assets/chlimage_1-427.png)

## タグ付け {#tagging}

多くのコミュニティ機能は、パブリッシュ環境で入力（投稿）されたコンテンツにメンバーがタグ付けできるように設定できます。

タグ付けが許可されている場合は、コミュニティサイトの設定で、パブリッシュ環境でメンバーに表示する名前空間を制限できます。 詳しくは、 [コミュニティサイトコンソール](sites-console.md#tagging).

タグ付けを許可する機能： [ブログ](blog-feature.md), [カレンダー](calendar.md), [ファイルライブラリ](file-library.md), [フォーラム](forum.md)

タグを使用する機能： [カタログ](catalog.md), [検索](search.md), [social タグクラウド](tagcloud.md)

オーサリング情報の場合：

* [タグの使用 ](../../help/sites-authoring/tags.md)

管理情報の場合：

* タグ名前空間（分類）の作成： [タグの管理](../../help/sites-administering/tags.md)
* コミュニティサイトの設定：参照 [タグ付け](sites-console.md#tagging)
* [ユーザー生成コンテンツのタグ付け](../../help/sites-authoring/tags.md)
* [イネーブルメントリソースのタグ付け](tag-resources.md)

開発者向けの情報：

* [AEM タグ付けフレームワーク](../../help/sites-developing/framework.md)
* [タグ付けの基本事項](tag.md)
