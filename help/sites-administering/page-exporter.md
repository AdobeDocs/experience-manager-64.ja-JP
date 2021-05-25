---
title: ページエクスポーター
seo-title: ページエクスポーター
description: AEM ページエクスポーターの使用方法について説明します。
seo-description: AEM ページエクスポーターの使用方法について説明します。
uuid: 2ca2b8f1-c723-4e6b-8c3d-f5886cd0d3f1
contentOwner: Chiradeep Majumdar
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: content
content-type: reference
discoiquuid: 6ab07b5b-ee37-4029-95da-be2031779107
exl-id: a5cb3b7b-d40f-4d86-8473-fb584f1d486c
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '1019'
ht-degree: 37%

---

# ページエクスポーター{#the-page-exporter}

AEM では、画像、.js ファイルおよび .css ファイルを含む完全な Web ページとしてページを書き出すことができます。

書き出しを設定したら、URLの`html`を`export.zip`に置き換えて、ブラウザーでページを要求するだけで、HTML形式でレンダリングされたページと参照元のアセットを含むzipファイルのダウンロードを取得できます。 ページ内のすべてのパス（画像へのパスなど）は、zipファイルに含まれるファイルまたはサーバー上のリソースを指すように書き換えられます。

## ページの書き出し {#exporting-a-page}

次の手順は、ページを書き出す方法と、サイトに書き出し設定テンプレートが存在することを前提としています。設定テンプレートは、ページの書き出し方法を定義し、サイトに固有です。設定テンプレートを作成するには、「[サイト用のページエクスポーター設定の作成](#creating-a-page-exporter-configuration-for-your-site)」の節を参照してください。

ページを書き出すには：

1. ブラウザーで、ページを開きます。次に例を示します。
1. `http://localhost:4502/content/geometrixx/en/products/triangle.html`
1. ページのプロパティダイアログを開き、「**詳細**」タブを選択して、「**書き出し**」フィールドセットを展開します。

1. 虫眼鏡のアイコンをクリックして設定テンプレートを選択します。Geometrixx サイトのデフォルトである **geometrixx** テンプレートを選択します。「**OK**」をクリックします。

1. 「**OK**」をクリックしてページのプロパティダイアログを閉じます。
1. URLの`html`を`export.zip`に置き換えて、ページを要求します。

1. `<page-name>.export.zip`ファイルをファイルシステムにダウンロードします。

1. ファイルシステムで、ファイルを解凍します。

   * ページのhtmlファイル(`<page-name>.html`)は`<unzip-dir>/<page-path>`の下にあります。
   * 書き出しテンプレートの設定に従って、その他のリソース（.jsファイル、.cssファイル、画像など）が配置されます。 この例では、一部のリソースが`<unzip-dir>/etc`以下、一部が`<unzip-dir>/<page-path>`以下にあります。

1. ブラウザーでページHTMLファイル(`<unzip-dir>/<page-path>.html`)を開き、レンダリングを確認します。

## サイト用のページエクスポーター設定の作成 {#creating-a-page-exporter-configuration-for-your-site}

ページエクスポーターは、コンテンツ同期フレームワークに基づいています。ページプロパティダイアログで使用できる設定は、設定テンプレートです。ページに必要な依存関係をすべて定義します。ページの書き出しがトリガーされると、設定テンプレートが使用され、ページパスとデザインパスの両方が設定に動的に適用されます。zipファイルは、標準のコンテンツ同期機能を使用して作成されます。

AEM では、以下を含むいくつかのテンプレートが埋め込まれます。

* `/etc/contentsync/templates/default`のデフォルト値。このテンプレート：

   * リポジトリ内に設定テンプレートが見つからない場合のフォールバックテンプレートです。
   * 新しい設定テンプレートのベースとして使用できます。

* **Geometrixx**&#x200B;サイト専用の1つ(`/etc/contentsync/templates/geometrixx`)。このテンプレートは、新しいテンプレートを作成する例として使用できます。

ページエクスポーター設定テンプレートを作成するには：

1. **CRXDE Lite**&#x200B;で、`/etc/contentsync/templates`の下にノードを作成します。

   * 名前：例：`mysite`.この名前は、ページエクスポーターテンプレートを選択する際に、ページプロパティダイアログに表示されます。
   * 型：`nt:unstructured`

1. テンプレートノード（ここでは `mysite`）の下に、以下で説明する設定ノードを使用してノード構造を作成します。

### ページエクスポーター設定ノード {#page-exporter-configuration-nodes}

設定テンプレートは、ノード構造で構成されます。 各ノードには`type`プロパティがあり、zipファイルの作成プロセスでの特定のアクションを定義します。 typeプロパティの詳細については、コンテンツ同期フレームワークページの設定タイプの概要の節を参照してください。

書き出し設定テンプレートを作成するには、以下のノードを使用できます。

**page** nodeページノードは、ページのhtmlをzipファイルにコピーするために使用します。次の特性があります。

* 必須ノードである。
* `/etc/contentsync/templates/<sitename>`の下にあります。
* 名前は`page`です。
* ノードタイプは`nt:unstructured`です。

`page` ノードには以下のプロパティがあります。

* 値`pages`で設定された`type`プロパティ。

* `path` プロパティはありません。現在のページパスが設定に動的にコピーされます。

* その他のプロパティについては、コンテンツ同期フレームワークの「設定タイプの概要」の節で説明します。

**rewrite** noderewriteノードは、書き出されたページでリンクを書き換える方法を定義します。書き換え後のリンクは、zip ファイルに含まれるファイルまたはサーバー上のリソースを指すことができます。

`rewrite` ノードについて詳しくは、コンテンツ同期ページを参照してください。

**design** nodeデザインノードは、書き出されたページに使用されるデザインをコピーするために使用されます。次の特性があります。

* オプションである。
* `/etc/contentsync/templates/<sitename>`の下にあります。
* 名前は`design`です。
* ノードタイプは`nt:unstructured`です。

`design` ノードには以下のプロパティがあります。

* 値`copy`に設定された`type`プロパティ。

* `path` プロパティはありません。現在のページパスが設定に動的にコピーされます。

**汎用ノ** ード：汎用ノードは、clientlibs .jsや.cssファイルなどのリソースをzipファイルにコピーするために使用します。次の特性があります。

* オプションである。
* `/etc/contentsync/templates/<sitename>`の下にあります。
* 特定の名前を持たない。
* ノードタイプは`nt:unstructured`です。
* コンテンツ同期フレームワークの設定タイプの概要で定義されている`type`プロパティと`type`関連プロパティがあります。

例えば、以下の設定ノードでは、geometrixx クライアントライブラリの .js ファイルを zip ファイルにコピーします。

```xml
"geometrixx.clientlibs.js": {
    "extension": "js",
    "type": "clientlib",
    "path": "/etc/designs/geometrixx/clientlibs",
    "jcr:primaryType": "nt:unstructured"
}
```

**Geometrixx** ページ書き出し設定テンプレートを見ると、ページ書き出しの設定方法がわかります。テンプレートのノード構造をブラウザーで json 形式で表示するには、以下の URL を要求します。

`http://localhost:4502/etc/contentsync/templates/geometrixx.-1.json`

**カスタム設定の実装**

ノード構造に気付いたかもしれませんが、**Geometrixx**&#x200B;ページ書き出し設定テンプレートには、`type`プロパティが`image`に設定された`logo`ノードがあります。 これは、画像のロゴをzipファイルにコピーするために作成された特別な設定タイプです。 特定の要件を満たすには、場合によってはカスタム`type`プロパティを実装する必要があります。そのためには、コンテンツ同期ページの「カスタム更新ハンドラーの実装」の節を参照してください。

## プログラムによるページの書き出し {#programmatically-exporting-a-page}

プログラムによってページを書き出すには、[PageExporter](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/wcm/contentsync/PageExporter.html) OSGI サービスを使用できます。このサービスを使用すると、次のことが可能です。

* ページを書き出して HTTP サーブレット応答に書き込む。
* ページを書き出して zip ファイルを特定の場所に保存する。

`export` セレクターおよび `zip` 拡張子にバインドされているサーブレットは PageExporter サービスを使用します。

## トラブルシューティング {#troubleshooting}

zipファイルのダウンロードで問題が発生した場合は、リポジトリ内の`/var/contentsync`ノードを削除し、書き出しリクエストを再度送信できます。
