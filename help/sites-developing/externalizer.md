---
title: URL の外部化
seo-title: URL の外部化
description: Externalizer は、プログラムによってリソースパスを外部 URL および絶対 URL に変換できる OSGi サービスです
seo-description: Externalizer は、プログラムによってリソースパスを外部 URL および絶対 URL に変換できる OSGi サービスです
uuid: ea887096-1a48-4bdb-bc5c-e4fe719e5632
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: platform
content-type: reference
discoiquuid: 53342acb-c1a5-443d-8727-cb27cc9d6845
exl-id: 123ef72b-f09b-47eb-9b5a-e0deb38799df
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '533'
ht-degree: 48%

---

# URL の外部化{#externalizing-urls}

AEMの&#x200B;**Externalizer**&#x200B;は、リソースパス(例えば、`/path/to/my/page`)を外部URLと絶対URL（例えば、`https://www.mycompany.com/path/to/my/page`）に埋め込みます。

インスタンスが Web レイヤーの背後で実行されている場合、自身の外部向け URL がわかりません。また、リンクをリクエストスコープの範囲外で作成する必要がある場合があります。これらの理由で、このサービスは、そのような外部 URL を設定して組み立てるための一元化された場所を提供します。

このページでは、**Externalizer** サービスの設定方法と使用方法について説明します。詳しくは、関連する [Javadoc](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/Externalizer.html) を参照してください。

## Externalizer サービスの設定  {#configuring-the-externalizer-service}

**Externalizer**&#x200B;サービスを使用すると、リソースパスにプログラム的にプレフィックスを付けるために使用できる複数のドメインを一元的に定義できます。各ドメインは、プログラムでドメインを参照する際に使用される一意の名前で識別されます。

**Externalizer** サービスのドメインマッピングを定義するには：

1. **ツール**&#x200B;から設定マネージャーに移動し、**Webコンソール**&#x200B;を開くか、`https://<host>:<port>/system/console/configMgr.`と入力します。
1. **Day CQ Link Externalizer**&#x200B;をクリックして、設定ダイアログボックスを開きます。

   >[!NOTE]
   >
   >設定への直接リンクは`https://<host>:<port>/system/console/configMgr/com.day.cq.commons.impl.ExternalizerImpl`です。

   ![chlimage_1-44](assets/chlimage_1-44.png)

1. ドメインマッピングの定義：マッピングは、ドメイン、スペースおよびドメインを参照するコードで使用できる一意の名前で構成されます。

   `<unique-name> [scheme://]server[:port][/contextpath]`, 条件:

   * **** スキーマは通常、httpまたはhttpsですが、ftpなどでもかまいません。必要に応じて、httpsを使用してhttpsリンクを強制します。URLの外部化を要求する際にクライアントコードがスキームを上書きしない場合に使用されます。
   * **** serverはホスト名です（ドメイン名またはipアドレスを使用できます）。
   * **port** （オプション）はポート番号です。
   * **contextpath** （オプション）は、AEMが別のコンテキストパスの下にwebアプリとしてインストールされている場合にのみ設定されます。

   例：`production https://my.production.instance`

   次のマッピング名は事前に定義されており、AEMがこれらを利用するため常に設定する必要があります。

   * **local**  — ローカルインスタンス
   * **author**  — オーサリングシステムのDNS
   * **publish**  — 公開されるWebサイトのDNS

   >[!NOTE]
   >
   >カスタム設定によって、「production」、「staging」などの新しいカテゴリや、「my-internal-webservice」などの AEM 以外の外部システムでも追加できます。このような設定は、プロジェクトのコードベースの様々な場所でそのような URL をハードコーディングするのを避けるために有効です。

1. 「**Save**」をクリックして変更を保存します。

>[!NOTE]
>
>Adobeでは、リポジトリに[設定を追加することをお勧めします。](/help/sites-deploying/configuring-osgi.md#adding-a-new-configuration-to-the-repository)

## Externalizer サービスの使用 {#using-the-externalizer-service}

ここでは、**Externalizer** サービスの使用方法に関するいくつかの例を紹介します。

**JSP で Externalizer サービスを取得する：**

`Externalizer externalizer = resourceResolver.adaptTo(Externalizer.class);`

**「publish」ドメインを付与してパスを外部化する：**

`String myExternalizedUrl = externalizer.publishLink(resolver, "/my/page") + ".html";`

ドメインマッピング「 `publish https://www.website.com` 」と仮定すると、myExternalizedUrlは「 `https://www.website.com/contextpath/my/page.html` 」という値になります。

**「author」ドメインを付与してパスを外部化するには：**

`String myExternalizedUrl = externalizer.authorLink(resolver, "/my/page") + ".html";`

ドメインマッピング「 `author https://author.website.com` 」と仮定すると、myExternalizedUrlは「 `https://author.website.com/contextpath/my/page.html` 」という値になります。

**「local」ドメインを付与してパスを外部化するには：**

`String myExternalizedUrl = externalizer.externalLink(resolver, Externalizer.LOCAL, "/my/page") + ".html";`

ドメインマッピング「 `local https://publish-3.internal` 」と仮定すると、myExternalizedUrlは「 `https://publish-3.internal/contextpath/my/page.html` 」という値になります。

他の例については、関連する [Javadoc](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/Externalizer.html) を参照してください。
