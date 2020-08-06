---
title: AEM AssetsとAEMメディアライブラリの機能の比較
description: AEM AssetsとAEMメディアライブラリに関する、相違点を含むよくある質問(FAQ)です。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 6a1013715c538c39eaf40a22dbffc7f2df36f968
workflow-type: tm+mt
source-wordcount: '551'
ht-degree: 79%

---


# AEM Assets と AEM Media Library との比較 {#aem-assets-vs-aem-medialibrary}

Adobe Experience Manager (AEM) Assets は、AEM プラットフォームの不可欠な構成要素です。このスムーズな統合は AEM の大きなメリットとしてとらえられており、これによってコンテンツ管理における整合性とコンテンツ作成者の高い生産性が確保されます。

## よくある質問 {#frequently-asked-questions}

### AEM Assets とは何ですか。 {#what-is-aem-assets}

AEM Assets は、AEM プラットフォーム上のアプリケーションです。お客様はこのアプリケーションを使用して、Web ベースのリポジトリ内でデジタルアセット（画像、ビデオ、ドキュメントおよびオーディオクリップ）を管理できます。AEM Assets には、メタデータサポート、レンディション、デジタルアセット管理ファインダーおよび AEM Assets 管理 UI が含まれています。

### AEM Media Library とは何ですか。 {#what-is-the-aem-media-library}

AEM Media Library は、画像やその他の共有リソースの保存専用に設けられた、AEM WCM コンテンツリポジトリ内の構成要素です。Media Library は、AEM WCM のデジタルアセット管理機能を使用します。

### AEM WCM にはない AEM Assets の機能 {#what-do-i-get-from-aem-assets-that-is-not-part-of-aem-wcm}

AEM Assets のお客様だけが使用できる独自の機能は次のとおりです。

1. タイトル、タグ、説明以外のメタデータを抽出および編集する機能。
1. the AEM Assets Admin, available from the welcome screen by clicking the second button next to the `siteadmin`.
1. Digital Asset Managementに関連するすべてのワークフロー手順、つまり、AEMアセットの取り込み、AEM Assetsの削除、AEM Assetsのサブアセット処理、AEM Assetsのメタデータ抽出です。
1. libraries including `dam` im package space.

これらの機能を使用するには、AEM Assets の有効なライセンスが必要です。

### AEM Assets は個別のパッケージとして使用できますか。 {#is-aem-assets-available-as-a-separate-package}

いいえ。インストールとデプロイメントを簡単にするために、すべての AEM アプリケーションとアドオンは、機能がすべて含まれる 1 つのパッケージで配布されます。これは、パッケージに含まれるすべての機能の使用権がユーザーにあることを表すわけではありません。

#### デジタルアセットのメタデータを編集したいのですが、その場合 AEM Assets は必要ですか。 {#i-want-to-edit-metadata-of-digital-assets-do-i-need-aem-assets}

タイトル、説明およびタグ以外のメタデータを編集する場合は、AEM Assets のライセンスが必要です。

#### 画像を読み込むときに自動的にサイズ変更したいのですが、その場合 AEM Assets は必要ですか。 {#i-want-to-automatically-resize-images-upon-import-do-i-need-aem-assets}

いいえ。静的な画像のサイズ変更とワークフローに基づく自動変換、およびレンディションの管理機能は、AEM Media Library の一部です。これらの機能には、AEM Assets のライセンスは必要ありません。

### カスタマイズされた画像コンポーネントを使用して画像をサイズ変更したいのですが、その場合 AEM Assets は必要ですか。 {#i-want-to-resize-images-using-a-customized-image-component-do-i-need-aem-assets}

画像コンポーネントは AEM WCM に含まれています。画像コンポーネントに（さらに AEM Assets にも）使用されているグラフィックライブラリは AEM プラットフォームに含まれており、AEM Assets ライセンスは必要ありません。

### 自分が AEM Assets のライセンスを所持していない場合、ユーザーが AEM Assets を使用しないようにする方法はありますか。 {#how-can-i-prevent-my-users-from-using-aem-assets-if-i-did-not-license-aem-assets}

すべての AEM Assets 固有ワークフロー、コンポーネント、分類、オプション、AEM Assets 管理機能を AEM から削除できます。これにより、ライセンスを取得していないAEM Assets機能を誤って使用するのを防ぐことができます。

### ページに画像を追加し、その画像の切り抜きやサイズ変更を実行したいのですが、その場合 AEM Assets は必要ですか。 {#i-want-to-add-images-to-a-page-and-want-to-crop-and-resize-these-images-do-i-need-aem-assets}

このような使用法では、AEM Assets を購入する必要はありません。Web サイト上で画像を使用する目的では、Media Library も使用する必要はありません。画像コンポーネントを使用すると、ページに画像を直接アップロードできるからです。

>[!MORELIKETHIS]
>
>* [機能の違いの詳細リスト](https://docs.adobe.com/content/help/en/experience-manager-65/assets/administer/medialibrary.html#listoffeatures)

