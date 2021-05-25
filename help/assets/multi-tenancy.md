---
title: コレクション、スニペット、スニペットテンプレートのマルチテナント機能
description: CRXリポジトリ内のコンテンツを顧客組織に基づいて分離し、不正アクセスを防ぎます。
contentOwner: AG
feature: コレクション
role: Architect,Administrator,Leader
exl-id: d00a671a-6707-4941-868d-fa13510b7b60
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 34%

---

# コレクション、スニペット、およびスニペットテンプレートのマルチテナント機能{#multi-tenancy-for-collections-snippets-and-snippet-templates}

マルチテナント機能を使用すると、組織プレフィックスと組織 ID に基づいて CRX のコンテンツを隔離し、他の組織のユーザーによるコンテンツへの不正アクセスを防止できます。

Adobe Experience Manager（AEM）Assets では、組織のデータは、組織ごとに異なるパスに保存されます。各組織固有のパスは、組織のプレフィックスと組織IDで識別されます。
異なるタイプのアセットがCRXに保存される従来の場所に含まれます。

例えば、`Demo`という名前のフォルダーを作成した場合、AEM assetsはデフォルトでCRXの`../content/dam/Demo`の場所にフォルダーを保存します。 マルチテナント機能を有効にすると、`../content/dam/<organization prefix>/<organization id>Demo`にデータを保存できます。

例えば、AEM Assets（オンデマンド）のAdobe Marketing Cloudユーザーが`aodpremium`組織に割り当てられている場合、マルチテナント機能を使用して、次のパスを`../content/dam/mac/aodpremiumDemo`に設定し、コンテンツを分離できます。 この例では、 `mac`は組織のプレフィックスで、 `aodpremium`は組織IDです。

ユーザーの組織と ID に基づくこの修飾パスは、AEM Assets インターフェイスと各種ウィザード（例えば、強制隔離するための移動およびスニペット作成ウィザードなど）に表示されます。

マルチテナント機能を使用すると、次のタイプのアセットとコンポーネントを切り離すことができます。

* コレクション
* 公開コレクション
* カタログ（ページの追加/選択ウィザードを含む）
* テンプレート
* スニペットテンプレート
* Lightbox
