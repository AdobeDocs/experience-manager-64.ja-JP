---
title: リソースマッピング
seo-title: Resource Mapping
description: リソースマッピングを使用してリダイレクト、バニティー URL および AEM 用の仮想ホストを定義する方法について説明します。
seo-description: Learn how to define redirects, vanity URLs and virtual hosts for AEM by using resource mapping.
uuid: 33de7e92-8144-431b-badd-e6a667cd78e1
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: configuring
content-type: reference
discoiquuid: ddfacc63-1840-407e-8802-3730009c84f0
feature: Configuring
exl-id: 81dddbab-1a9e-49ee-b2a5-a8e4de3630d1
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '521'
ht-degree: 90%

---

# リソースマッピング{#resource-mapping}

リソースマッピングは、リダイレクト、バニティー URL および AEM 用の仮想ホストを定義するために使用します。

例えば、これらのマッピングを使用すると次のことが可能です。

* すべてのリクエストに `/content` というプレフィックスを付けて、web サイトの訪問者に内部構造が表示されないようにする。
* Web サイトの `/content/en/gateway` ページへのリクエストがすべて `https://gbiv.com/` にリダイレクトされるように、リダイレクトを定義する。

HTTP マッピングの一例として、[localhost:4503 に対するすべての要求に /content](#configuring-an-internal-redirect-to-content) というプレフィックスを指定します。このようなマッピングを使用すると、Web サイトの訪問者に対して内部構造を非表示にすることができます。例えば、次のページにアクセスできます。

`localhost:4503/content/geometrixx/en/products.html`

次の URL を使用してアクセスできます。

`localhost:4503/geometrixx/en/products.html`

マッピングによって、`/content` というプレフィックスが `/geometrixx/en/products.html` に自動的に追加されるからです。

>[!CAUTION]
>
>バニティー URL は regex パターンをサポートしません。

>[!NOTE]
>
>詳しくは、Sling のドキュメントと「[Mappings for Resource Resolution](https://sling.apache.org/site/resources.html)」と「[Resources](https://sling.apache.org/site/mappings-for-resource-resolution.html)」を参照してください。

## マッピング定義の確認 {#viewing-mapping-definitions}

マッピングでは 2 つのリストが作成されます。JCR Resource Resolver は、これらのリストを（トップダウン）評価して一致項目を探します。

これらのリストは、Felix コンソールの **JCR ResourceResolver** オプション（例：`https://<host>:<port>/system/console/jcrresolver`）で（設定情報と一緒に）確認できます。

* 設定

   現在の設定を表示します ( [Apache Sling Resource Resolver](/help/sites-deploying/osgi-configuration-settings.md).

* 設定テスト

   
URL またはリソースパスを入力できます。「**Resolve**」または「**Map**」をクリックして、システムによるエントリの変換方法を確認します。

* **Resolver Map Entries**
URL をリソースにマップするために ResourceResolver.resolve メソッドが使用するエントリのリストです。

* **Mapping Map Entries**
リソースパスを URL にマップするために ResourceResolver.map メソッドが使用するエントリのリストです。

2 つのリストには、アプリケーションでデフォルトとして定義されたエントリを含む様々なエントリが表示されます。これらのエントリの目的は、多くの場合、ユーザーのために URL を簡略化することです。

リストでは、**パターン**（要求に適合する正規表現）と&#x200B;**リプレースメント**（適用するリダイレクトを定義します）がペアになっています。

例えば、次のパターンがあるとします。

**パターン** `^[^/]+/[^/]+/welcome$`

このパターンは次のリプレースメントを呼び出します。

**リプレースメント** `/libs/cq/core/content/welcome.html`.

これにより、次のリクエストがリダイレクトされます。

`http://localhost:4503/welcome`

リダイレクト先は次のとおりです。

`http://localhost:4503/libs/cq/core/content/welcome.html`

新しいマッピング定義がリポジトリ内に作成されます。

>[!NOTE]
>
>正規表現の定義方法について説明したリソースは多数あります（例：[https://www.regular-expressions.info/](https://www.regular-expressions.info/)）。

## AEM でのマッピング定義の作成 {#creating-mapping-definitions-in-aem}

AEM の標準インストールには、次のフォルダーがあります。

`/etc/map/http`

これは、HTTP プロトコル用のマッピングを定義する場合に使用する構造です。マッピングするその他のプロトコル用に別のフォルダー（`sling:Folder`）を `/etc/map` の下に作成できます。

### /content への内部リダイレクトの設定 {#configuring-an-internal-redirect-to-content}

http://localhost:4503/への要求の先頭に「 `/content`:

1. CRXDE を使用して `/etc/map/http` に移動します。

1. 新しいノードを作成します。

   * **型** `sling:Mapping`

      このノードタイプは、このようなマッピングを対象としていますが、使用が必須ではありません。

   * **名前** `localhost_any`

1. 「**すべて保存**」をクリックします。
1. **このノードに次のプロパティを追加します。**

   * **名前** `sling:match`

      * **型** `String`
      * **値** `localhost.4503/`
   * **名前** `sling:internalRedirect`

      * **型** `String`
      * **値** `/content/`


1. 「**すべて保存**」をクリックします。

これは、次のようなリクエストを処理します。\
`localhost:4503/geometrixx/en/products.html`\
次のように：\
`localhost:4503/content/geometrixx/en/products.html`\
が要求されていた

>[!NOTE]
>
>使用可能な Sling のプロパティとその設定方法について詳しくは、Sling のドキュメントの [Resources](https://sling.apache.org/site/mappings-for-resource-resolution.html) を参照してください。

>[!NOTE]
>
>`/etc/map.publish` を使用して、パブリッシュ環境の設定を保持する。これらの設定をレプリケートして、パブリッシュ環境の [Apache Sling Resource Resolver](/help/sites-deploying/osgi-configuration-settings.md#apacheslingresourceresolver) の「**Mapping Location**」用に新しい場所（`/etc/map.publish`）を設定する必要があります。
