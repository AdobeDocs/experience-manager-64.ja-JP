---
title: AEM AssetsとAEM Media Libraryで使用できる機能の比較
description: AEM AssetsとAEM Media Libraryに関する、相違点を含むよくある質問(FAQ)です。
contentOwner: AG
translation-type: tm+mt
source-git-commit: c5862cce4a061f076486a00685c37326bb4b21d9

---


# AEM Assets と AEM Media Library との比較 {#aem-assets-vs-aem-medialibrary}

Adobe Experience Manager（AEM） Assets は、AEM プラットフォームの不可欠な構成要素です。このスムーズな統合は AEM の大きなメリットとしてとらえられており、これによってコンテンツ管理における整合性とコンテンツ作成者の高い生産性が確保されます。

## よくある質問 {#frequently-asked-questions}

### What is AEM Assets? {#what-is-aem-assets}

AEM Assets は、AEM プラットフォーム上のアプリケーションです。お客様はこのアプリケーションを使用して、Web ベースのリポジトリ内でデジタルアセット（画像、ビデオ、ドキュメントおよびオーディオクリップ）を管理できます。AEM Assets には、メタデータサポート、レンディション、デジタルアセット管理ファインダーおよび AEM Assets 管理 UI が含まれています。

### AEM Media Library とは {#what-is-the-aem-media-library}

AEM Media Library は、画像やその他の共有リソースの保存専用に設けられた、AEM WCM コンテンツリポジトリ内の構成要素です。Media Library は、AEM WCM のデジタルアセット管理機能を使用します。

### AEM WCM にはない AEM Assets の機能 {#what-do-i-get-from-aem-assets-that-is-not-part-of-aem-wcm}

AEM Assets のお客様だけが使用できる独自の機能は次のとおりです。

1. タイトル、タグ、説明以外のメタデータを抽出および編集する機能。
1. the AEM Assets Admin, available from the welcome screen by clicking the second button next to the `siteadmin`.
1. Digital Asset Managementに関連するすべてのワークフロー手順、つまり、AEM Assetsの取り込み、AEM Assetsの削除、AEM Assetsのサブアセット処理、AEM Assetsのメタデータの抽出。
1. libraries including `dam` im package space.

これらの機能を使用するには、AEM Assets の有効なライセンスが必要です。

### AEM Assets は個別のパッケージとして使用できますか。 {#is-aem-assets-available-as-a-separate-package}

いいえ. インストールとデプロイメントを簡単にするために、すべての AEM アプリケーションとアドオンは、機能がすべて含まれる 1 つのパッケージで配布されます。これは、パッケージに含まれるすべての機能の使用権がユーザーあることを表すわけではありません。

#### デジタルアセットのメタデータを編集したいのですが、その場合 AEM Assets は必要ですか。 {#i-want-to-edit-metadata-of-digital-assets-do-i-need-aem-assets}

タイトル、説明およびタグ以外のメタデータを編集する場合は、AEM Assets のライセンスが必要です。

#### Web サイトでカテゴリ述語を使用したいのですが、その場合 AEM Assets は必要ですか。 {#i-want-to-use-the-category-predicate-on-my-website-do-i-need-aem-assets}

はい。カテゴリ述語は、Geometrixx Press Center で使用されるその他すべてのコンポーネントと共に AEM Assets に含まれており、AEM Assets ライセンスが必要です。

#### 画像を読み込むときに自動的にサイズ変更したいのですが、その場合 AEM Assets は必要ですか。 {#i-want-to-automatically-resize-images-upon-import-do-i-need-aem-assets}

いいえ. 静的な画像のサイズ変更とワークフロー主導の自動変換、およびレンディションの管理機能は、AEM Media Libraryの一部です。 これらの機能にはAEM Assetsライセンスは必要ありません。

### カスタマイズされた画像コンポーネントを使用して画像をサイズ変更したいのですが、その場合 AEM Assets は必要ですか。 {#i-want-to-resize-images-using-a-customized-image-component-do-i-need-aem-assets}

画像コンポーネントは AEM WCM に含まれています。画像コンポーネントに（さらに AEM Assets にも）使用されているグラフィックライブラリは AEM プラットフォームに含まれており、AEM Assets ライセンスは必要ありません。

### How can I prevent my users from using AEM Assets if I did not license AEM Assets? {#how-can-i-prevent-my-users-from-using-aem-assets-if-i-did-not-license-aem-assets}

すべての AEM Assets 固有ワークフロー、コンポーネント、分類、オプションおよび AEM Assets 管理機能を AEM から削除できます。これによって、ライセンスを所持していない AEM Assets 機能をユーザーが誤って使用することを防ぐことができます。

### ページに画像を追加し、その画像の切り抜きやサイズ変更を実行したいのですが、その場合 AEM Assets は必要ですか。 {#i-want-to-add-images-to-a-page-and-want-to-crop-and-resize-these-images-do-i-need-aem-assets}

このような使用法では、AEM Assets を購入する必要はありません。Web サイト上で画像を使用する目的では、Media Library も使用する必要はありません。画像コンポーネントを使用すると、ページに画像を直接アップロードできるからです。

>[!MORELIKETHIS]
>
>* [機能の違いの詳細リスト](https://docs.adobe.com/content/help/en/experience-manager-65/assets/administer/medialibrary.html#listoffeatures)