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
translation-type: tm+mt
source-git-commit: 8e2bd579e4c5edaaf86be36bd9d81dfffa13a573
workflow-type: tm+mt
source-wordcount: '533'
ht-degree: 48%

---


# URL の外部化{#externalizing-urls}

AEMでは、**Externalizer**&#x200B;はOSGIサービスで、リソースパス(例えば、`/path/to/my/page`)を外部URLや絶対URL（例えば`https://www.mycompany.com/path/to/my/page`）に埋め込みます。

インスタンスが Web レイヤーの背後で実行されている場合、自身の外部向け URL がわかりません。また、リンクをリクエストスコープの範囲外で作成する必要がある場合があります。これらの理由で、このサービスは、そのような外部 URL を設定して組み立てるための一元化された場所を提供します。

このページでは、**Externalizer** サービスの設定方法と使用方法について説明します。詳しくは、関連する [Javadoc](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/Externalizer.html) を参照してください。

## Externalizer サービスの設定  {#configuring-the-externalizer-service}

**Externalizer**&#x200B;サービスを使用すると、プログラム的にリソースパスをプレフィックスするために使用できる複数のドメインを一元的に定義できます。各ドメインは、そのドメインをプログラムで参照する際に使用される一意の名前で識別されます。

**Externalizer** サービスのドメインマッピングを定義するには：

1. **ツール**&#x200B;から&#x200B;**Webコンソール**&#x200B;に移動するか、`https://<host>:<port>/system/console/configMgr.`と入力します。
1. 「**Day CQ Link Externalizer**」をクリックして、設定ダイアログボックスを開きます。

   >[!NOTE]
   >
   >構成への直接リンクは`https://<host>:<port>/system/console/configMgr/com.day.cq.commons.impl.ExternalizerImpl`です

   ![chlimage_1-44](assets/chlimage_1-44.png)

1. ドメインマッピングの定義：マッピングは、ドメイン、スペース、ドメインを参照するコードで使用できる一意の名前で構成されます。

   `<unique-name> [scheme://]server[:port][/contextpath]`, 条件:

   * **** schemeは、通常、httpまたはhttpsですが、ftpなどを指定することもできます。必要に応じてhttpsを使用し、httpsリンクを強制します。URLの外部化を要求する際に、クライアントコードがスキームを上書きしない場合に使用されます。
   * **** serverはホスト名です（ドメイン名またはipアドレスを指定できます）。
   * **port** （オプション）はポート番号です。
   * **contextpath** （オプション）は、AEMがwebアプリとして別のコンテキストパスの下にインストールされている場合にのみ設定されます。

   例：`production https://my.production.instance`

   次のマッピング名は事前に定義されており、AEMがそれらに依存しているため、常に設定する必要があります。

   * **local**  — ローカルインスタンス
   * **author**  — オーサリングシステムのDNS
   * **publish**  — 公開されるWebサイトのDNS

   >[!NOTE]
   >
   >カスタム設定によって、「production」、「staging」などの新しいカテゴリや、「my-internal-webservice」などの AEM 以外の外部システムでも追加できます。このような設定は、プロジェクトのコードベースの様々な場所でそのような URL をハードコーディングするのを避けるために有効です。

1. 「**Save**」をクリックして変更を保存します。

>[!NOTE]
>
>Adobeでは、[リポジトリ](/help/sites-deploying/configuring-osgi.md#adding-a-new-configuration-to-the-repository)に設定を追加することを推奨します。

## Externalizer サービスの使用 {#using-the-externalizer-service}

ここでは、**Externalizer** サービスの使用方法に関するいくつかの例を紹介します。

**JSP で Externalizer サービスを取得する：**

`Externalizer externalizer = resourceResolver.adaptTo(Externalizer.class);`

**「publish」ドメインを付与してパスを外部化する：**

`String myExternalizedUrl = externalizer.publishLink(resolver, "/my/page") + ".html";`

ドメインマッピング「 `publish https://www.website.com` 」を想定すると、myExternalizedUrlは値「 `https://www.website.com/contextpath/my/page.html` 」になります。

**「author」ドメインを付与してパスを外部化するには：**

`String myExternalizedUrl = externalizer.authorLink(resolver, "/my/page") + ".html";`

ドメインマッピング「 `author https://author.website.com` 」を想定すると、myExternalizedUrlは値「 `https://author.website.com/contextpath/my/page.html` 」になります。

**「local」ドメインを付与してパスを外部化するには：**

`String myExternalizedUrl = externalizer.externalLink(resolver, Externalizer.LOCAL, "/my/page") + ".html";`

ドメインマッピング「 `local https://publish-3.internal` 」を想定すると、myExternalizedUrlは値「 `https://publish-3.internal/contextpath/my/page.html` 」になります。

他の例については、関連する [Javadoc](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/Externalizer.html) を参照してください。
