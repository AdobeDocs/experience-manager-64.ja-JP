---
title: リモートエンドポイントの設定
seo-title: Configuring Remoting endpoints
description: リモートエンドポイントを設定する方法を説明します。
seo-description: Learn how to configure remoting endpoints.
uuid: 4d4f9274-dcae-4b9f-975a-575376c2f89c
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_endpoints
products: SG_EXPERIENCEMANAGER/6.4/FORMS
discoiquuid: aab9d622-d76b-4100-9ca6-e5b86f543381
exl-id: d8e31f99-0558-4634-ae35-f4a09f34ad6d
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 37%

---

# リモートエンドポイントの設定 {#configuring-remoting-endpoints}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

リモートエンドポイントを使用すると、Flexで構築されたアプリケーションで、(AEM forms では廃止されています )AEM forms Remoting を使用してサービスを呼び出すことができます。 リモートエンドポイントは、アクティブ化された各サービスに対して自動的に作成されます。 エンドポイントと同じ名前のFlex宛先が作成され、Flexクライアントは、この宛先を指すリモートオブジェクトを作成して、関連するサービスの操作を呼び出すことができます。

## リモートエンドポイントの設定 {#remoting-endpoint-settings}

**Flex Client Authentication Method：**&#x200B;呼び出されたサービスでセキュリティが有効になっており、呼び出された操作で匿名の呼び出しがサポートされていないとき、クライアントから秘密鍵証明書が渡されないか無効な場合に、サーバーがクライアントに送り返す応答の種類を特定します。
