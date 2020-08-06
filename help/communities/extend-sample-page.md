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
translation-type: tm+mt
source-git-commit: 44c56ec5de6e9a832aaa52ab4a6c4978af7a9865
workflow-type: tm+mt
source-wordcount: '395'
ht-degree: 70%

---


# サンプルページへのコメントの追加 {#add-comment-to-sample-page}

カスタムコメントシステムのコンポーネントをアプリケーションディレクトリ（/apps）に配置したので、拡張されたコンポーネントを使用できるようになりました。影響を受けるWebサイト内のコメントシステムのインスタンスでは、そのresourceTypeをカスタムコメントシステムに設定し、必要なすべてのクライアントライブラリを含める必要があります。

## 必要な clientlib の識別 {#identify-required-clientlibs}

デフォルトのコメントのスタイルと機能に必要なクライアントライブラリは、拡張されたコメントにも必要です。

The [Community Components Guide](components-guide.md) identifies the required client libraries. コンポーネントガイドを参照し、コメントコンポーネントの表示を表示します。例：

[http://localhost:4502/content/community-components/en/comments.html](http://localhost:4502/content/community-components/en/comments.html)

コメントの正常なレンダリングと機能のためには、3 つのクライアントライブラリが必要です。These will need to be included where the extended Comments is referenced, as well as the [extended Comments&#39; client library](extend-create-components.md#create-a-client-library-folder) ( `apps.custom.comments`).

![chlimage_1-47](assets/chlimage_1-47.png)

## ページへのカスタムコメントの追加 {#add-custom-comments-to-a-page}

1 つのページで使用できるコメントシステムは 1 つだけなので、[サンプルページの作成](create-sample-page.md)のチュートリアルで説明する手順に従ってサンプルページを作成すると簡単です。

作成したら、デザインモードに切り替え、カスタムコンポーネントグループを使用可能にして、`Alt Comments` コンポーネントをページに追加できるようにします。

コメントを正しく表示し、機能させるには、コメントのクライアントライブラリをページの clientlibslist に追加する必要があります（[コミュニティコンポーネントの clientlib](clientlibs.md) を参照）。

### サンプルページでのコメントの clientlib {#comments-clientlibs-on-sample-page}

![サンプルページでのコメントの clientlib](assets/chlimage_1-48.png)

### オーサー環境：サンプルページでの Alt Comment {#author-alt-comment-on-sample-page}

![サンプルページでの Alt Comment](assets/chlimage_1-49.png)

### オーサー環境：サンプルページでのコメントノード {#author-sample-page-comments-node}

You can verify the resourceType in CRXDE by viewing the properties of the comments node for the sample page at `/content/sites/sample/en/jcr:content/content/primary/comments`.

![chlimage_1-50](assets/chlimage_1-50.png)

### サンプルページの公開 {#publish-sample-page}

カスタムコンポーネントをページに追加した後は、（再度）[ページを公開](sites-console.md#publishing-the-site)する必要もあります。

### パブリッシュ環境：サンプルページでの Alt Comment {#publish-alt-comment-on-sample-page}

カスタムアプリケーションとサンプルページの両方を公開したら、コメントを入力できるようになります。When signed in, either with a [demo user](tutorials.md#demo-users) or admin, it should be possible to post a comment.

aaron.mcdonald@mailinator.comコメントの投稿を次に示します。

![chlimage_1-51](assets/chlimage_1-51.png) ![chlimage_1-52](assets/chlimage_1-52.png)

拡張されたコンポーネントがデフォルトの外観で正しく機能していることがわかります。次は外観を変更します。

