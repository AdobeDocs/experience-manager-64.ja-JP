---
title: リモートエンドポイントの設定
seo-title: Configuring Remoting endpoints
description: リモートエンドポイントの設定方法について説明します。
seo-description: Learn how to configure remoting endpoints.
uuid: 4d4f9274-dcae-4b9f-975a-575376c2f89c
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_endpoints
products: SG_EXPERIENCEMANAGER/6.4/FORMS
discoiquuid: aab9d622-d76b-4100-9ca6-e5b86f543381
exl-id: d8e31f99-0558-4634-ae35-f4a09f34ad6d
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '120'
ht-degree: 65%

---

# リモートエンドポイントの設定 {#configuring-remoting-endpoints}

リモートエンドポイントを使用すると、Flex で作成されたアプリケーションから AEM Forms Remoting（AEM Forms では廃止されています）を使用してサービスを呼び出せるようにします。リモートエンドポイントは、アクティブ化された各サービスに対して自動的に作成されます。エンドポイントと同じ名前を持つ Flex の宛先が作成され、Flex クライアントは、関連するサービスの操作を呼び出すために、この宛先を指すリモートオブジェクトを作成できます。

## リモートエンドポイントの設定 {#remoting-endpoint-settings}

**Flexクライアント認証方法：** 呼び出されたサービスがセキュリティが有効になっている場合、呼び出された操作が匿名の呼び出しをサポートせず、クライアントが無効または無効な資格情報を渡した場合に、サーバーがクライアントに返す応答の種類を決定します。
