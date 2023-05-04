---
title: ページエクスポーター
seo-title: The Page Exporter
description: AEM Page Exporter の使用方法を説明します。
seo-description: Learn how to use the AEM Page Exporter.
uuid: 2ca2b8f1-c723-4e6b-8c3d-f5886cd0d3f1
contentOwner: Chiradeep Majumdar
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: content
content-type: reference
discoiquuid: 6ab07b5b-ee37-4029-95da-be2031779107
exl-id: a5cb3b7b-d40f-4d86-8473-fb584f1d486c
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '1044'
ht-degree: 27%

---

# ページエクスポーター{#the-page-exporter}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

AEMでは、画像、.js、.css ファイルを含む完全な Web ページとしてページを書き出すことができます。

書き出しを設定したら、次の代わりに `html` と `export.zip` URL 内に、html 形式でレンダリングされたページと参照元のアセットを含む zip ファイルのダウンロードが含まれています。 ページ内のすべてのパス（画像へのパスなど）は、zip ファイルに含まれるファイルまたはサーバー上のリソースを指すように書き換えられます。

## ページのエクスポート {#exporting-a-page}

次の手順では、ページを書き出す方法を説明し、サイトに書き出し設定テンプレートが存在すると仮定します。 設定テンプレートは、ページの書き出し方法を定義し、サイトに固有のものです。 設定テンプレートを作成するには、 [サイト用のページエクスポーター設定の作成](#creating-a-page-exporter-configuration-for-your-site) 」セクションに入力します。

ページをエクスポートするには：

1. ブラウザーで、ページを開きます。 次に例を示します。
1. `http://localhost:4502/content/geometrixx/en/products/triangle.html`
1. ページプロパティダイアログを開き、「 **詳細** タブをクリックし、 **書き出し** フィールドセット。

1. 虫めがねアイコンをクリックし、設定テンプレートを選択します。 を選択します。 **geometrixx** テンプレートに含まれます。Geometrixxサイトのデフォルトのテンプレートです。 「**OK**」をクリックします。

1. クリック **OK** をクリックして、ページプロパティダイアログを閉じます。
1. 次を置き換えてページをリクエスト `html` と `export.zip` 」と入力します。

1. をダウンロードします。 `<page-name>.export.zip` ファイルをファイルシステムに保存します。

1. ファイルシステムで、ファイルを解凍します。

   * ページの html ファイル ( `<page-name>.html`) は、以下で利用できます。 `<unzip-dir>/<page-path>`
   * その他のリソース（.js ファイル、.css ファイル、画像など）は、書き出しテンプレートの設定に従って配置されます。 この例では、一部のリソースが次のようになります。 `<unzip-dir>/etc`の一部 `<unzip-dir>/<page-path>`.

1. ページの HTML ファイル（`<unzip-dir>/<page-path>.html`）をブラウザーで開き、レンダリングを確認します。

## サイト用のページエクスポーター設定の作成 {#creating-a-page-exporter-configuration-for-your-site}

ページエクスポーターは、コンテンツ同期フレームワークに基づいています。ページのプロパティダイアログで使用できる設定は、設定テンプレートです。 ページに必要な依存関係をすべて定義します。 ページの書き出しがトリガーされると、設定テンプレートが使用され、ページパスとデザインパスの両方が設定に動的に適用されます。 その後、標準のコンテンツ同期機能を使用して、zip ファイルが作成されます。

AEMには、次のようないくつかのテンプレートが埋め込まれます。

* デフォルトは `/etc/contentsync/templates/default`. このテンプレート：

   * リポジトリに設定テンプレートが見つからない場合のフォールバックテンプレートです。
   * 新しい設定テンプレートのベースとして使用できます。

* 専用の **Geometrixx** サイト、 `/etc/contentsync/templates/geometrixx`. このテンプレートは、新しいテンプレートを作成する例として使用できます。

ページエクスポーター設定テンプレートを作成するには：

1. **CRXDE Lite** で、`/etc/contentsync/templates` の下にノードを作成します。

   * 名前：例： `mysite`. ページエクスポーターテンプレートを選択すると、この名前がページプロパティのダイアログボックスに表示されます。
   * 型：`nt:unstructured`

1. テンプレートノード（ここでは `mysite`）の下に、次で説明する設定ノードを使用してノード構造を作成します。

### ページエクスポーター設定ノード {#page-exporter-configuration-nodes}

設定テンプレートは、ノード構造で構成されます。 各ノードには、zip ファイルの作成プロセスで特定のアクションを定義する `type` プロパティが含まれています。type プロパティの詳細については、コンテンツ同期フレームワークページの設定タイプの概要の節を参照してください。

書き出し設定テンプレートを作成するには、次のノードを使用できます。

**ページノード** ページノードは、ページの html を zip ファイルにコピーするために使用されます。 次のような特徴があります。

* 必須ノードです。
* `/etc/contentsync/templates/<sitename>` にあります。
* 名前は `page`.
* ノードタイプはです。 `nt:unstructured`

`page` ノードには以下のプロパティがあります。

* 値 `pages` が設定された `type` プロパティ。

* `path` プロパティはありません。現在のページパスが設定に動的にコピーされます。

* その他のプロパティについては、コンテンツ同期フレームワークの設定タイプの概要の節で説明します。

**書き換えノード** rewrite ノードは、書き出されたページでリンクを書き換える方法を定義します。 書き換えられたリンクは、zip ファイルに含まれるファイルまたはサーバー上のリソースを指す場合があります。

詳しくは、コンテンツ同期ページを参照してください。 `rewrite` ノード。

**デザインノード** デザインノードは、書き出したページに使用するデザインをコピーするために使用されます。 次のような特徴があります。

* オプションです。
* `/etc/contentsync/templates/<sitename>` にあります。
* 名前は `design`.
* ノードタイプはです。 `nt:unstructured`.

`design` ノードには次のプロパティがあります。

* 値 `copy` に設定された `type` プロパティ。

* `path` プロパティはありません。現在のページパスが設定に動的にコピーされます。

**汎用ノード** 汎用ノードは、clientlibs .jsや.css ファイルなどのリソースを zip ファイルにコピーするために使用します。 次のような特徴があります。

* オプションです。
* `/etc/contentsync/templates/<sitename>` にあります。
* 特定の名前がありません。
* ノードタイプはです。 `nt:unstructured`.
* 次を持つ `type` プロパティおよび任意 `type` コンテンツ同期フレームワークの「設定タイプの概要」節で定義される関連プロパティ。

例えば、次の設定ノードでは、geometrixx clientlibs .js ファイルを zip ファイルにコピーします。

```xml
"geometrixx.clientlibs.js": {
    "extension": "js",
    "type": "clientlib",
    "path": "/etc/designs/geometrixx/clientlibs",
    "jcr:primaryType": "nt:unstructured"
}
```

この **Geometrixx** ページ書き出し設定テンプレートで、ページの書き出しを設定する方法を確認できます。 テンプレートのノード構造を json 形式でブラウザーに表示するには、次の URL を要求します。

`http://localhost:4502/etc/contentsync/templates/geometrixx.-1.json`

**カスタム設定の実装**

ノード構造でご存じのように、 **Geometrixx** ページ書き出し設定テンプレートに `logo` ノード `type` プロパティを `image`. これは、画像のロゴを zip ファイルにコピーするために作成された特別な設定タイプです。 特定の要件を満たすには、カスタム `type` プロパティ：その場合は、コンテンツ同期ページのカスタム更新ハンドラーの実装の節を参照してください。

## プログラムによるページのエクスポート {#programmatically-exporting-a-page}

プログラムによってページを書き出すには、 [PageExporter](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/wcm/contentsync/PageExporter.html) OSGi サービス。 このサービスを使用すると、次のことができます。

* ページを書き出し、HTTP サーブレット応答に書き込みます。
* ページを書き出し、zip ファイルを特定の場所に保存します。

`export` セレクターおよび `zip` 拡張子にバインドされているサーブレットは PageExporter サービスを使用します。

## トラブルシューティング {#troubleshooting}

Zip ファイルのダウンロードで問題が発生した場合は、リポジトリで `/var/contentsync` ノードを削除して、エクスポートリクエストを再度送信できます。
