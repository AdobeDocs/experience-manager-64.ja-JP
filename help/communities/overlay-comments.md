---
title: コメントコンポーネントのオーバーレイ
seo-title: コメントコンポーネントのオーバーレイ
description: コメントコンポーネントのオーバーレイの概要
seo-description: コメントコンポーネントのオーバーレイの概要
uuid: 634240e2-99bb-4107-89f5-c66d53e2515d
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.4/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 4849da13-518c-40c8-b80e-1b2264d7f8f5
exl-id: 31528814-02bc-4978-87fa-5c8074b454ed
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '168'
ht-degree: 61%

---

# コメントコンポーネントのオーバーレイ  {#overlay-comments-component}

デフォルトのコンポーネントを[オーバーレイ](client-customize.md#overlays)する目的は、コンポーネントのすべての相対参照について、コンポーネントの外観や動作をグローバルに変更することです。これには、/libs フォルダー内で検索する前に、/apps フォルダーに解決するという sling の特性が利用されます。つまり、コンポーネントへのパスは、/apps フォルダーにあり、/libs フォルダーにはない場合を除き、デフォルトのコンポーネントへのパスと同じです。

## 例 {#example}

コメント機能を変更してWebサイトのデザインに合わせ、コメントヘッダーを変更して、コメントのアバターが表示されないようにするとします。 アバターを非表示にするソリューションは、CSSを使用するか、ここで説明するように、アバターを含むHTMLがクライアントに送信されないように、appsフォルダー内のheader.jspをオーバーレイします。

コメントをオーバーレイするには、次の手順を実行する必要があります。

1. [コメントページ](overlay-create-comments-page.md)
1. [ノードの作成](overlay-create-nodes.md)
1. [外観の変更](overlay-alter-appearance.md)
