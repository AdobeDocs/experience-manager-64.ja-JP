---
title: ページエクスポーター
seo-title: The Page Exporter
description: AEM ページエクスポーターの使用方法について説明します。
seo-description: Learn how to use the AEM Page Exporter.
uuid: 2ca2b8f1-c723-4e6b-8c3d-f5886cd0d3f1
contentOwner: Chiradeep Majumdar
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: content
content-type: reference
discoiquuid: 6ab07b5b-ee37-4029-95da-be2031779107
exl-id: a5cb3b7b-d40f-4d86-8473-fb584f1d486c
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '1008'
ht-degree: 37%

---

# ページエクスポーター{#the-page-exporter}

AEM では、画像、.js ファイルおよび .css ファイルを含む完全な Web ページとしてページを書き出すことができます。

書き出しを設定したら、次の代わりに `html` と `export.zip` URL 内に、html 形式でレンダリングされたページと参照元のアセットを含む zip ファイルのダウンロードが含まれています。 ページ内のすべてのパス（画像へのパスなど）は、zip ファイルに含まれるファイルまたはサーバー上のリソースを指すように書き換えられます。

## ページの書き出し {#exporting-a-page}

次の手順では、ページを書き出す方法を説明し、サイトに書き出し設定テンプレートが存在すると仮定します。設定テンプレートは、ページの書き出し方法を定義し、サイトに固有のものです。設定テンプレートを作成するには、 [サイト用のページエクスポーター設定の作成](#creating-a-page-exporter-configuration-for-your-site) 」セクションに入力します。

ページを書き出すには：

1. ブラウザーで、ページを開きます。次に例を示します。
1. `http://localhost:4502/content/geometrixx/en/products/triangle.html`
1. ページのプロパティダイアログを開き、「**詳細**」タブを選択して、「**書き出し**」フィールドセットを展開します。

1. 虫眼鏡のアイコンをクリックして設定テンプレートを選択します。Geometrixx サイトのデフォルトである **geometrixx** テンプレートを選択します。「**OK**」をクリックします。

1. 「**OK**」をクリックしてページのプロパティダイアログを閉じます。
1. 次を置き換えてページをリクエスト `html` と `export.zip` 」と入力します。

1. をダウンロードします。 `<page-name>.export.zip` ファイルをファイルシステムに保存します。

1. ファイルシステムで、ファイルを解凍します。

   * ページの html ファイル ( `<page-name>.html`) は、以下で利用できます。 `<unzip-dir>/<page-path>`
   * その他のリソース（.js ファイル、.css ファイル、画像など）は、書き出しテンプレートの設定に従って配置されます。 この例では、一部のリソースが次のようになります。 `<unzip-dir>/etc`の一部 `<unzip-dir>/<page-path>`.

1. ページの html ファイル ( `<unzip-dir>/<page-path>.html`) をブラウザーでクリックして、レンダリングを確認します。

## サイト用のページエクスポーター設定の作成 {#creating-a-page-exporter-configuration-for-your-site}

ページエクスポーターは、コンテンツ同期フレームワークに基づいています。ページのプロパティダイアログで使用できる設定は、設定テンプレートです。ページに必要な依存関係をすべて定義します。ページの書き出しがトリガーされると、設定テンプレートが使用され、ページパスとデザインパスの両方が設定に動的に適用されます。zip ファイルは、その後、標準のコンテンツ同期機能を使用して作成されます。

AEM では、以下を含むいくつかのテンプレートが埋め込まれます。

* デフォルトは `/etc/contentsync/templates/default`.このテンプレート：

   * リポジトリ内に設定テンプレートが見つからない場合のフォールバックテンプレートです。
   * 新しい設定テンプレートのベースとして使用できます。

* 専用の **Geometrixx** サイト、 `/etc/contentsync/templates/geometrixx`.このテンプレートは、新しいテンプレートを作成する例として使用できます。

ページエクスポーター設定テンプレートを作成するには：

1. In **CRXDE Lite**、以下にノードを作成します。 `/etc/contentsync/templates`:

   * 名前：例： `mysite`.この名前は、ページエクスポーターテンプレートを選択する際に、ページのプロパティダイアログに表示されます。
   * 型：`nt:unstructured`

1. テンプレートノード（ここでは `mysite`）の下に、以下で説明する設定ノードを使用してノード構造を作成します。

### ページエクスポーター設定ノード {#page-exporter-configuration-nodes}

設定テンプレートは、ノード構造で構成されます。 各ノードには `type` zip ファイルの作成プロセスで特定のアクションを定義するプロパティ。 type プロパティの詳細については、コンテンツ同期フレームワークページの設定タイプの概要の節を参照してください。

書き出し設定テンプレートを作成するには、以下のノードを使用できます。

**ページノード** ページノードは、ページの html を zip ファイルにコピーするために使用されます。 これには次のような特徴があります。

* 必須ノードである。
* 次の場所にあります。 `/etc/contentsync/templates/<sitename>`.
* 名前は `page`.
* ノードタイプはです。 `nt:unstructured`

`page` ノードには以下のプロパティがあります。

* A `type` プロパティに値を設定 `pages`.

* `path` プロパティはありません。現在のページパスが設定に動的にコピーされます。

* その他のプロパティについては、コンテンツ同期フレームワークの設定タイプの概要の節で説明します。

**書き換えノード** rewrite ノードは、書き出されたページでリンクを書き換える方法を定義します。 書き換え後のリンクは、zip ファイルに含まれるファイルまたはサーバー上のリソースを指すことができます。

`rewrite` ノードについて詳しくは、コンテンツ同期ページを参照してください。

**デザインノード** デザインノードは、書き出したページに使用するデザインをコピーするために使用されます。 これには次のような特徴があります。

* オプションである。
* 次の場所にあります。 `/etc/contentsync/templates/<sitename>`.
* 名前は `design`.
* ノードタイプはです。 `nt:unstructured`.

`design` ノードには以下のプロパティがあります。

* A `type` プロパティを値に設定 `copy`.

* `path` プロパティはありません。現在のページパスが設定に動的にコピーされます。

**汎用ノード** 汎用ノードは、clientlibs .jsや.css ファイルなどのリソースを zip ファイルにコピーするために使用します。 これには次のような特徴があります。

* オプションである。
* 次の場所にあります。 `/etc/contentsync/templates/<sitename>`.
* 特定の名前を持たない。
* ノードタイプはです。 `nt:unstructured`.
* 次を持つ `type` プロパティおよび任意 `type` コンテンツ同期フレームワークの「設定タイプの概要」節で定義される関連プロパティ。

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

ノード構造でご存じのように、 **Geometrixx** ページ書き出し設定テンプレートに `logo` ノード `type` プロパティを `image`. これは、画像のロゴを zip ファイルにコピーするために作成された特別な設定タイプです。 特定の要件を満たすには、カスタム `type` プロパティ：その場合は、コンテンツ同期ページのカスタム更新ハンドラーの実装の節を参照してください。

## プログラムによるページの書き出し {#programmatically-exporting-a-page}

プログラムによってページを書き出すには、[PageExporter](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/wcm/contentsync/PageExporter.html) OSGI サービスを使用できます。このサービスを使用すると、次のことが可能です。

* ページを書き出して HTTP サーブレット応答に書き込む。
* ページを書き出して zip ファイルを特定の場所に保存する。

`export` セレクターおよび `zip` 拡張子にバインドされているサーブレットは PageExporter サービスを使用します。

## トラブルシューティング {#troubleshooting}

zip ファイルのダウンロードで問題が発生した場合は、 `/var/contentsync` ノードを作成し、書き出しリクエストを再度送信します。
