---
title: CSRF 対策フレームワーク
seo-title: The CSRF Protection Framework
description: このフレームワークでは、トークンを利用して、クライアントの要求が正当なものであることを保証します
seo-description: The framework makes use of tokens to guarantee that the client request is legitimate
uuid: 7cb222ba-fc7a-46ee-8b49-a5f39a53580b
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: introduction
content-type: reference
discoiquuid: f453427d-c813-48b7-b2f9-adadea39c67d
exl-id: 533c348e-517f-4d70-a89c-bfc87f71a633
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '282'
ht-degree: 60%

---

# CSRF 対策フレームワーク{#the-csrf-protection-framework}

アドビでは、Apache Sling Referrer Filter 以外にも、この種の攻撃を防ぐための新しい CSRF 対策フレームワークを用意しています。

このフレームワークでは、トークンを利用して、クライアントの要求が正当なものであることを保証します。トークンは、フォームがクライアントに送信されるときに生成され、フォームがサーバーに返されるときに検証されます。

>[!NOTE]
>
>パブリッシュインスタンスでは、匿名ユーザーのトークンはありません。

## 要件 {#requirements}

### 依存関係 {#dependencies}

に依存する任意のコンポーネント `granite.jquery` 依存関係は、CSRF 保護フレームワークのメリットを自動的に受けます。 どのコンポーネントでも該当しない場合は、 `granite.csrf.standalone` このフレームワークを使用する前に、

### 暗号鍵のレプリケーション {#replicating-crypto-keys}

トークンを利用するには、 `/etc/keys/hmac` バイナリをデプロイメント内のすべてのインスタンスに追加します。 HMAC 鍵をすべてのインスタンスにコピーするには、鍵を格納するパッケージを作成し、パッケージマネージャーを使用してすべてのインスタンスにインストールする方法が便利です。

>[!NOTE]
>
>CSRF 対策フレームワークを使用するには、必要な[ディスパッチャー設定の変更](https://helpx.adobe.com/experience-manager/dispatcher/user-guide.html)をおこなってください。

>[!NOTE]
>
>Web アプリケーションでマニフェストキャッシュを使用する場合は、必ず「**&amp;ast;**」がマニフェストに追加されます。 詳しくは、こちらの[リンク](https://www.w3.org/TR/offline-webapps/)を参照してください。
>
>CSRF 攻撃とその軽減方法について詳しくは、[OWASP のクロスサイトリクエストフォージェリに関するページ](https://owasp.org/www-community/attacks/csrf)を参照してください。
