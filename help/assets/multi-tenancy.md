---
title: コレクション、スニペット、スニペットテンプレートのマルチテナント機能
description: 不正なアクセスを防ぐため、顧客組織に基づいて CRX リポジトリのコンテンツを分離します。
contentOwner: AG
feature: Collections
role: Architect,Admin,Leader
exl-id: d00a671a-6707-4941-868d-fa13510b7b60
source-git-commit: 5d96c09ef764b02e08dcdf480da1ee18f4d9a30c
workflow-type: tm+mt
source-wordcount: '230'
ht-degree: 33%

---

# コレクション、スニペット、スニペットテンプレートのマルチテナント機能 {#multi-tenancy-for-collections-snippets-and-snippet-templates}

マルチテナント機能を使用すると、組織プレフィックスと組織 ID に基づいて CRX のコンテンツを隔離し、他の組織のユーザーによるコンテンツへの不正アクセスを防止できます。

Adobe Experience Manager（AEM）Assets では、組織のデータは、組織ごとに異なるパスに保存されます。各組織固有のパスは、組織のプレフィックスと組織 ID によって識別されます。これは、異なるタイプのアセットが CRX に保存される従来の場所に含まれます。

例えば、 `Demo`に設定すると、AEM assets はデフォルトでフォルダーを `../content/dam/Demo` の場所を指定します。 マルチテナント機能を有効にすると、次の場所にデータを保存できます。 `../content/dam/<organization prefix>/<organization id>Demo`.

例えば、AEM Assets（オンデマンド）のAdobe Marketing Cloudユーザーが `aodpremium` 組織では、マルチテナント機能を使用して、次のパスを `../content/dam/mac/aodpremiumDemo`、コンテンツを分離します。 この例では、 `mac` は組織のプレフィックスで、 `aodpremium` は組織 ID です。

ユーザーの組織と ID に基づくこの修飾パスは、AEM Assets インターフェイスと各種ウィザード（例えば、強制隔離するための移動およびスニペット作成ウィザードなど）に表示されます。

マルチテナント機能を使用すると、次のタイプのアセットとコンポーネントを切り離すことができます。

* コレクション
* 公開コレクション
* カタログ（ページの追加/選択ウィザードを含む）
* テンプレート
* スニペットテンプレート
* Lightbox
