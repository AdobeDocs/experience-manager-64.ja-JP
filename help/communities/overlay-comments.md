---
title: コメントコンポーネントのオーバーレイ
seo-title: Overlay Comments Component
description: コメントコンポーネントのオーバーレイの概要
seo-description: Overlay Comments component overview
uuid: 634240e2-99bb-4107-89f5-c66d53e2515d
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.4/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 4849da13-518c-40c8-b80e-1b2264d7f8f5
exl-id: 31528814-02bc-4978-87fa-5c8074b454ed
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 10%

---

# コメントコンポーネントのオーバーレイ {#overlay-comments-component}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

次の目的 [重ね](client-customize.md#overlays) デフォルトのコンポーネントでは、コンポーネントに対するすべての相対参照に対して、コンポーネントの外観や動作をグローバルに変更します。 /libs フォルダーで検索する前に/apps フォルダーに解決する Sling の性質に依存します。 したがって、コンポーネントへのパスは、/libs フォルダーではなく/apps フォルダー内にある点を除き、デフォルトコンポーネントへのパスと同じになります。

## 例 {#example}

Web サイトのデザインに合わせてコメント機能を変更する場合は、コメントヘッダーを変更して、コメントのアバターを表示しないようにします。 アバターを非表示にするソリューションは、CSS を使用するか、ここで説明するように、アバターを含むHTMLがクライアントに送信されないように、apps フォルダー内の header.jsp をオーバーレイします。

コメントをオーバーレイするには、次の操作が必要です。

1. [コメントページ](overlay-create-comments-page.md)
1. [ノードの作成](overlay-create-nodes.md)
1. [外観の変更](overlay-alter-appearance.md)
