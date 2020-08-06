---
title: コレクション、スニペット、スニペットテンプレートのマルチテナンシー
description: 不正アクセスを防ぐために、顧客組織に基づいてCRXリポジトリ内のコンテンツを分離します。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 0d70a672a2944e2c03b54beb3b5f734136792ab1
workflow-type: tm+mt
source-wordcount: '230'
ht-degree: 33%

---


# Multi-tenancy for collections, snippets, and snippet templates {#multi-tenancy-for-collections-snippets-and-snippet-templates}

マルチテナント機能を使用すると、組織プレフィックスと組織 ID に基づいて CRX のコンテンツを隔離し、他の組織のユーザーによるコンテンツへの不正アクセスを防止できます。

Adobe Experience Manager（AEM）Assets では、組織のデータは、組織ごとに異なるパスに保存されます。各組織固有のパスは、組織のプレフィックスと組織IDで識別されます。これは、異なるタイプのアセットがCRXに保存される従来の場所に含まれています。

For example, if you create a folder named `Demo`, AEM assets by default stores the folder at `../content/dam/Demo` location in CRX. マルチテナンシー機能を有効にすると、にデータを格納でき `../content/dam/<organization prefix>/<organization id>Demo`ます。

For example, for Adobe Marketing Cloud users of AEM Assets (on-demand) that are assigned to `aodpremium` organization, you can use the multi-tenancy feature to configure the following path to `../content/dam/mac/aodpremiumDemo`, segregate the content. この例では、 `mac` が組織のプレフィックスで、 `aodpremium` が組織IDです。

ユーザーの組織と ID に基づくこの修飾パスは、AEM Assets インターフェイスと各種ウィザード（例えば、強制隔離するための移動およびスニペット作成ウィザードなど）に表示されます。

マルチテナンシー機能を使用すると、次のタイプのアセットとコンポーネントを選択できます。

* コレクション
* 公開コレクション
* カタログ(追加ページの選択ウィザードを含む)
* テンプレート
* スニペットテンプレート
* Lightbox
