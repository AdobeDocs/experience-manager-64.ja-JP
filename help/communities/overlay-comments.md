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
translation-type: tm+mt
source-git-commit: 8f169bb9b015ae94b9160d3ebbbd1abf85610465
workflow-type: tm+mt
source-wordcount: '168'
ht-degree: 61%

---


# コメントコンポーネントのオーバーレイ {#overlay-comments-component}

デフォルトのコンポーネントを[オーバーレイ](client-customize.md#overlays)する目的は、コンポーネントのすべての相対参照について、コンポーネントの外観や動作をグローバルに変更することです。これには、/libs フォルダー内で検索する前に、/apps フォルダーに解決するという sling の特性が利用されます。つまり、コンポーネントへのパスは、/apps フォルダーにあり、/libs フォルダーにはない場合を除き、デフォルトのコンポーネントへのパスと同じです。

## 例 {#example}

コメント機能を変更して、Webサイトのデザインと一致するようにし、コメントヘッダーを変更して、どのコメントのアバターも表示されないようにしたいとします。 アバターを非表示にするソリューションは、CSSを使用するか、ここで説明するように、appsフォルダーのheader.jspをオーバーレイして、アバターを含むHTMLがクライアントに送信されないようにします。

コメントをオーバーレイするには、次の手順を実行する必要があります。

1. [コメントページの作成](overlay-create-comments-page.md)
1. [ノードの作成](overlay-create-nodes.md)
1. [外観の変更](overlay-alter-appearance.md)

