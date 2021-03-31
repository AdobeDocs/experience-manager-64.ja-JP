---
title: コレクション、スニペット、スニペットテンプレートのマルチテナンシー
description: 不正アクセスを防ぐために、顧客組織に基づいてCRXリポジトリ内のコンテンツを分離します。
contentOwner: AG
feature: コレクション
role: アーキテクト，管理者，リーダー
translation-type: tm+mt
source-git-commit: 29e3cd92d6c7a4917d7ee2aa8d9963aa16581633
workflow-type: tm+mt
source-wordcount: '234'
ht-degree: 33%

---


# コレクション、スニペット、スニペットテンプレートのマルチテナンシー{#multi-tenancy-for-collections-snippets-and-snippet-templates}

マルチテナント機能を使用すると、組織プレフィックスと組織 ID に基づいて CRX のコンテンツを隔離し、他の組織のユーザーによるコンテンツへの不正アクセスを防止できます。

Adobe Experience Manager（AEM）Assets では、組織のデータは、組織ごとに異なるパスに保存されます。組織固有の各パスは、組織のプレフィックスと組織IDで識別されます。
の値は、様々なタイプのアセットがCRXに保存される従来の場所に含まれています。

例えば、`Demo`という名前のフォルダーを作成した場合、AEMアセットは、デフォルトで、CRXの`../content/dam/Demo`の場所にフォルダーを保存します。 マルチテナンシー機能を有効にすると、`../content/dam/<organization prefix>/<organization id>Demo`にデータを保存できます。

例えば、`aodpremium`組織に割り当てられているAEM AssetsのAdobe Marketing Cloudユーザー（オンデマンド）の場合、マルチテナンシー機能を使用して次のパスを`../content/dam/mac/aodpremiumDemo`に設定し、コンテンツを分離できます。 この例では、`mac`が組織のプレフィックス、`aodpremium`が組織IDです。

ユーザーの組織と ID に基づくこの修飾パスは、AEM Assets インターフェイスと各種ウィザード（例えば、強制隔離するための移動およびスニペット作成ウィザードなど）に表示されます。

マルチテナンシー機能を使用すると、次のタイプのアセットとコンポーネントを選択できます。

* コレクション
* 公開コレクション
* カタログ(追加ページの選択ウィザードを含む)
* テンプレート
* スニペットテンプレート
* Lightbox
