---
title: サンプルページへのコメントの追加
seo-title: サンプルページへのコメントの追加
description: ページへのカスタムコメントの追加
seo-description: ページへのカスタムコメントの追加
uuid: 7dbaff4f-9986-435d-9379-7add676ea254
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.4/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 7185fb13-46a2-4fa3-aa21-a51e63cdb9be
exl-id: 96ef7e58-66c9-4985-973b-0c6fc7c39fd5
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '395'
ht-degree: 70%

---

# サンプルページへのコメントの追加  {#add-comment-to-sample-page}

カスタムコメントシステムのコンポーネントをアプリケーションディレクトリ（/apps）に配置したので、拡張されたコンポーネントを使用できるようになりました。影響を受けるWebサイト内のコメントシステムのインスタンスでは、そのresourceTypeをカスタムコメントシステムに設定し、必要なクライアントライブラリをすべて含める必要があります。

## 必要な clientlib の識別 {#identify-required-clientlibs}

デフォルトのコメントのスタイルと機能に必要なクライアントライブラリは、拡張されたコメントにも必要です。

[コミュニティコンポーネントガイド](components-guide.md)は、必要なクライアントライブラリを特定します。 コンポーネントガイドを参照し、コメントコンポーネントを表示します。次に例を示します。

[http://localhost:4502/content/community-components/en/comments.html](http://localhost:4502/content/community-components/en/comments.html)

コメントの正常なレンダリングと機能のためには、3 つのクライアントライブラリが必要です。拡張コメントが参照される場所に、拡張コメントのクライアントライブラリ](extend-create-components.md#create-a-client-library-folder)(`apps.custom.comments`)と共に、拡張コメントが参照される場所にこれらを含める必要があります。[

![chlimage_1-47](assets/chlimage_1-47.png)

## ページへのカスタムコメントの追加 {#add-custom-comments-to-a-page}

1 つのページで使用できるコメントシステムは 1 つだけなので、[サンプルページの作成](create-sample-page.md)のチュートリアルで説明する手順に従ってサンプルページを作成すると簡単です。

作成したら、デザインモードに切り替え、カスタムコンポーネントグループを使用可能にして、`Alt Comments` コンポーネントをページに追加できるようにします。

コメントを正しく表示し、機能させるには、コメントのクライアントライブラリをページの clientlibslist に追加する必要があります（[コミュニティコンポーネントの clientlib](clientlibs.md) を参照）。

### サンプルページでのコメントの clientlib  {#comments-clientlibs-on-sample-page}

![サンプルページでのコメントの clientlib](assets/chlimage_1-48.png)

### オーサー環境：サンプルページでの Alt Comment {#author-alt-comment-on-sample-page}

![サンプルページでの Alt Comment](assets/chlimage_1-49.png)

### オーサー環境：サンプルページでのコメントノード {#author-sample-page-comments-node}

CRXDEでresourceTypeを確認するには、`/content/sites/sample/en/jcr:content/content/primary/comments`にあるサンプルページのcommentsノードのプロパティを確認します。

![chlimage_1-50](assets/chlimage_1-50.png)

### サンプルページの公開 {#publish-sample-page}

カスタムコンポーネントをページに追加した後は、（再度）[ページを公開](sites-console.md#publishing-the-site)する必要もあります。

### パブリッシュ環境：サンプルページでの Alt Comment {#publish-alt-comment-on-sample-page}

カスタムアプリケーションとサンプルページの両方を公開したら、コメントを入力できるようになります。[デモユーザー](tutorials.md#demo-users)または管理者を使用してサインインすると、コメントを投稿できます。

aaron.mcdonald@mailinator.comはコメントを投稿しています。

![chlimage_1-51](assets/chlimage_1-51.png) ![chlimage_1-52](assets/chlimage_1-52.png)

拡張されたコンポーネントがデフォルトの外観で正しく機能していることがわかります。次は外観を変更します。
