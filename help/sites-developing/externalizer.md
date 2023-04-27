---
title: URL の外部化
seo-title: Externalizing URLs
description: Externalizer は、プログラムによってリソースパスを外部および絶対 URL に変換できる OSGi サービスです
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
ht-degree: 47%

---

# URL の外部化{#externalizing-urls}

AEM の **Externalizer** は、プログラムによってリソースパス（例：`/path/to/my/page`）を外部の絶対 URL（例：`https://www.mycompany.com/path/to/my/page`）に変換できるようにする OSGi サービスであり、その変換はパスに事前設定済みの DNS をプレフィックスとして付けることで実現します。

Web レイヤーの背後で実行されている場合、インスタンスは外部から表示される URL を認識できないので、リクエスト範囲外でリンクを作成する必要がある場合があるので、このサービスを使用して、外部 URL を設定して作成できます。

このページでは、 **Externalizer** サービスとその使用方法について説明します。 詳しくは、 [Javadocs](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/Externalizer.html).

## Externalizer サービスの設定 {#configuring-the-externalizer-service}

**Externalizer** サービスでは、プログラムによってリソースパスにプレフィックスを付けるために使用可能な複数のドメインを一元的に定義できます。各ドメインは一意の名前によって識別され、その名前を使用して、プログラムからそのドメインを参照できます。

**Externalizer** サービスのドメインマッピングを定義するには：

1. で設定マネージャーに移動します。 **ツール**&#x200B;を、 **Web コンソール**&#x200B;または、 `https://<host>:<port>/system/console/configMgr.`
1. 「**Day CQ Link Externalizer**」をクリックして設定ダイアログボックスを開きます。

   >[!NOTE]
   >
   >この設定に直接アクセスするためのリンクは `https://<host>:<port>/system/console/configMgr/com.day.cq.commons.impl.ExternalizerImpl` です。

   ![chlimage_1-44](assets/chlimage_1-44.png)

1. ドメインマッピングの定義：マッピングは、ドメイン、スペースおよびドメインを参照するコード内で使用できる一意の名前で構成されます。

   `<unique-name> [scheme://]server[:port][/contextpath]`, 条件:

   * **スキーム** は通常、http または https ですが、ftp などでもかまいません。;必要に応じて、https を使用して https リンクを強制します。URL の外部化を要求する際に、クライアントコードがスキームを上書きしない場合に使用されます。
   * **server** はホスト名です（ドメイン名または IP アドレス）。
   * **port**（オプション）はポート番号です。
   * **contextpath**（オプション）は、AEM が異なるコンテキストパスの下の Web アプリケーションとしてインストールされている場合に限り設定します。

   例：`production https://my.production.instance`

   次のマッピング名は事前定義されており、AEM で使用されるので、常に設定されている必要があります。

   * **ローカル**  — ローカルインスタンス
   * **作成者**  — オーサリングシステムの DNS
   * **公開**  — 公開ウェブサイト DNS

   >[!NOTE]
   >
   >カスタム設定を使用すると、「production」、「staging」、または「my-internal-webservice」などの外部のAEM以外のシステムでさえ新しいカテゴリを追加でき、プロジェクトのコードベースの様々な場所に URL をハードコーディングするのを避けるのに役立ちます。

1. 「**保存**」をクリックして変更を保存します。

>[!NOTE]
>
>アドビでは、[この設定をリポジトリに追加する](/help/sites-deploying/configuring-osgi.md#adding-a-new-configuration-to-the-repository)ことをお勧めします。

## Externalizer サービスの使用 {#using-the-externalizer-service}

この節では、 **Externalizer** サービスを使用できます。

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
