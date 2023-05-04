---
title: コレクション、スニペットおよびスニペットテンプレートのマルチテナント
description: 不正なアクセスを防ぐため、顧客組織に基づいて CRX リポジトリのコンテンツを分離します。
contentOwner: AG
feature: Collections
role: Architect,Admin,Leader
exl-id: d00a671a-6707-4941-868d-fa13510b7b60
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '266'
ht-degree: 12%

---

# コレクション、スニペットおよびスニペットテンプレートのマルチテナント {#multi-tenancy-for-collections-snippets-and-snippet-templates}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

マルチテナント機能を使用すると、組織のプレフィックスと組織 ID に基づいて CRX 内のコンテンツを区別し、他の組織のユーザーがコンテンツに不正にアクセスするのを防ぐことができます。

Adobe Experience Manager(AEM)Assets では、各組織のデータを異なるパスに保存します。 各組織固有のパスは、組織のプレフィックスと組織 ID によって識別されます。これは、異なるタイプのアセットが CRX に保存される従来の場所に含まれます。

例えば、 `Demo`に設定すると、AEM assets はデフォルトでフォルダーを `../content/dam/Demo` の場所を指定します。 マルチテナント機能を有効にすると、次の場所にデータを保存できます。 `../content/dam/<organization prefix>/<organization id>Demo`.

例えば、AEM Assets（オンデマンド）のAdobe Marketing Cloudユーザーが `aodpremium` 組織では、マルチテナント機能を使用して、次のパスを `../content/dam/mac/aodpremiumDemo`、コンテンツを分離します。 この例では、 `mac` は組織のプレフィックスで、 `aodpremium` は組織 ID です。

ユーザーの組織と ID に基づいて、この修飾パスはAEM Assetsインターフェイスや様々なウィザードに表示されます。このウィザードには、移動やスニペットの作成ウィザードなどが含まれ、セグメント化を実施します。

マルチテナント機能を使用すると、次のタイプのアセットとコンポーネントを切り離すことができます。

* コレクション
* 公開コレクション
* カタログ（ページの追加／選択ウィザードを含む）
* テンプレート
* スニペットテンプレート
* ライトボックス
