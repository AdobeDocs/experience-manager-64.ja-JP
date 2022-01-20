---
title: URL の外部化
seo-title: Externalizing URLs
description: Externalizer は、プログラムによってリソースパスを外部 URL および絶対 URL に変換できる OSGi サービスです
seo-description: The Externalizer is an OSGI service that allows you to programmatically transform a resource path into an external and absolute URL
uuid: ea887096-1a48-4bdb-bc5c-e4fe719e5632
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: platform
content-type: reference
discoiquuid: 53342acb-c1a5-443d-8727-cb27cc9d6845
exl-id: 123ef72b-f09b-47eb-9b5a-e0deb38799df
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '510'
ht-degree: 53%

---

# URL の外部化{#externalizing-urls}

AEMで、 **Externalizer** は、リソースパス ( 例えば、 `/path/to/my/page`) を外部 URL や絶対 URL( 例えば、 `https://www.mycompany.com/path/to/my/page`) を追加する必要があります。

インスタンスが Web レイヤーの背後で実行されている場合、自身の外部向け URL がわかりません。また、リンクをリクエストスコープの範囲外で作成する必要がある場合があります。これらの理由で、このサービスは、そのような外部 URL を設定して組み立てるための一元化された場所を提供します。

このページでは、**Externalizer** サービスの設定方法と使用方法について説明します。詳しくは、関連する [Javadoc](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/Externalizer.html) を参照してください。

## Externalizer サービスの設定 {#configuring-the-externalizer-service}

この **Externalizer** サービスを使用すると、リソースパスにプログラム的にプレフィックスを付けるために使用できる複数のドメインを一元的に定義できます。各ドメインは、プログラムによってドメインを参照する際に使用される一意の名前で識別されます。

**Externalizer** サービスのドメインマッピングを定義するには：

1. で設定マネージャーに移動します。 **ツール**&#x200B;を、 **Web コンソール**&#x200B;または、 `https://<host>:<port>/system/console/configMgr.`
1. 「**Day CQ Link Externalizer**」をクリックして設定ダイアログボックスを開きます。

   >[!NOTE]
   >
   >この設定に直接アクセスするためのリンクは `https://<host>:<port>/system/console/configMgr/com.day.cq.commons.impl.ExternalizerImpl` です。

   ![chlimage_1-44](assets/chlimage_1-44.png)

1. ドメインマッピングの定義：マッピングは、ドメイン、スペースおよびドメインを参照するコード内で使用できる一意の名前で構成されます。

   `<unique-name> [scheme://]server[:port][/contextpath]`, 条件:

   * **スキーム** は通常、http または https ですが、ftp などでもかまいません。必要に応じて、https を使用して https リンクを強制します。URL の外部化を要求する際に、クライアントコードがスキームを上書きしない場合に使用されます。
   * **server** はホスト名です（ドメイン名または IP アドレスを指定できます）。
   * **ポート** （オプション）はポート番号です。
   * **contextpath** （オプション）は、AEMが別のコンテキストパスの下に web アプリとしてインストールされている場合にのみ設定されます。

   例：`production https://my.production.instance`

   次のマッピング名は事前定義されており、AEM で使用されるので、常に設定されている必要があります。

   * **ローカル**  — ローカルインスタンス
   * **作成者**  — オーサリングシステムの DNS
   * **公開**  — 公開ウェブサイト DNS

   >[!NOTE]
   >
   >カスタム設定によって、「production」、「staging」などの新しいカテゴリや、「my-internal-webservice」などの AEM 以外の外部システムでも追加できます。このような設定は、プロジェクトのコードベースの様々な場所でそのような URL をハードコーディングするのを避けるために有効です。

1. 「**保存**」をクリックして変更を保存します。

>[!NOTE]
>
>Adobeが推奨する [リポジトリに設定を追加します。](/help/sites-deploying/configuring-osgi.md#adding-a-new-configuration-to-the-repository).

## Externalizer サービスの使用 {#using-the-externalizer-service}

ここでは、**Externalizer** サービスの使用方法に関するいくつかの例を紹介します。

**JSP で Externalizer サービスを取得する：**

`Externalizer externalizer = resourceResolver.adaptTo(Externalizer.class);`

**「publish」ドメインを付与してパスを外部化するには：**

`String myExternalizedUrl = externalizer.publishLink(resolver, "/my/page") + ".html";`

ドメインマッピングが「 `publish https://www.website.com`&quot;, myExternalizedUrl が値&quot; `https://www.website.com/contextpath/my/page.html`&quot;.

**「author」ドメインを付与してパスを外部化するには：**

`String myExternalizedUrl = externalizer.authorLink(resolver, "/my/page") + ".html";`

ドメインマッピングが「 `author https://author.website.com`&quot;, myExternalizedUrl が値&quot; `https://author.website.com/contextpath/my/page.html`&quot;.

**「local」ドメインを付与してパスを外部化するには：**

`String myExternalizedUrl = externalizer.externalLink(resolver, Externalizer.LOCAL, "/my/page") + ".html";`

ドメインマッピングが「 `local https://publish-3.internal`&quot;, myExternalizedUrl が値&quot; `https://publish-3.internal/contextpath/my/page.html`&quot;.

他の例については、関連する [Javadoc](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/Externalizer.html) を参照してください。
