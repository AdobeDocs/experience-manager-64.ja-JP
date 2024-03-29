---
title: CSRF 対策フレームワーク
seo-title: The CSRF Protection Framework
description: このフレームワークでは、トークンを使用して、クライアントの要求が正当なものであることを保証します
seo-description: The framework makes use of tokens to guarantee that the client request is legitimate
uuid: 7cb222ba-fc7a-46ee-8b49-a5f39a53580b
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: introduction
content-type: reference
discoiquuid: f453427d-c813-48b7-b2f9-adadea39c67d
exl-id: 533c348e-517f-4d70-a89c-bfc87f71a633
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '318'
ht-degree: 64%

---

# CSRF 対策フレームワーク {#the-csrf-protection-framework}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

Apache Sling Referrer Filter に加えて、Adobeは、この種の攻撃から保護する新しい CSRF 保護フレームワークも提供します。

このフレームワークでは、トークンを使用して、クライアントの要求が正当なものであることを保証します。 トークンは、フォームがクライアントに送信されるときに生成され、フォームがサーバーに送り返されると検証されます。

>[!NOTE]
>
>匿名ユーザーのパブリッシュインスタンスにはトークンがありません。

## 要件 {#requirements}

### 依存関係 {#dependencies}

`granite.jquery` 依存関係を信頼する任意のコンポーネント は、CSRF 保護フレームワークのメリットを自動的に受けます。どのコンポーネントにも当てはまらない場合、このフレームワークを使用するには `granite.csrf.standalone` への依存関係を宣言する必要があります。

### 暗号鍵のレプリケーション {#replicating-crypto-keys}

トークンを利用するには、デプロイメント内のすべてのインスタンスに `/etc/keys/hmac` バイナリをレプリケーションする必要があります。HMAC 鍵をすべてのインスタンスにコピーするには、鍵を格納するパッケージを作成し、パッケージマネージャーを使用してすべてのインスタンスにインストールする方法が便利です。

>[!NOTE]
>
>CSRF 対策フレームワークを使用するには、必要な[ディスパッチャー設定の変更](https://helpx.adobe.com/jp/experience-manager/brand-portal/user-guide.html)を行ってください。

>[!NOTE]
>
>Web アプリケーションでマニフェストキャッシュを使用する場合、トークンがオフラインで CSRF トークンの生成を呼び出さないように、「**&amp;ast;**」をマニフェストに追加してください。詳しくは、こちらの[リンク](https://www.w3.org/TR/offline-webapps/)を参照してください。
>
>CSRF 攻撃とその対策について詳しくは、[クロスサイトリクエストフォージェリに関する OWASP のページ](https://owasp.org/www-community/attacks/csrf)を参照してください。
