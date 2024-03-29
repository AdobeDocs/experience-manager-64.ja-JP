---
title: 翻訳するコンテンツの準備
seo-title: Preparing Content for Translation
description: 翻訳するコンテンツを準備する方法を説明します。
seo-description: Learn how to prepare content for translation.
uuid: 369630a8-2ed7-48db-973e-bd8213231d49
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: site-features
content-type: reference
discoiquuid: 8bd67d71-bcb7-4ca0-9751-3ff3ee054011
feature: Language Copy
exl-id: 1a7fe230-093b-4d2b-95cb-f9479c0febe5
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '717'
ht-degree: 59%

---

# 翻訳するコンテンツの準備{#preparing-content-for-translation}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

通常、多言語の Web サイトでは、多言語のコンテンツがいくつか提供されます。 サイトは 1 つの言語で作成され、他の言語に翻訳されます。 一般に、多言語サイトはページのブランチで構成され、各ブランチには異なる言語のサイトのページが含まれます。

サンプルのGeometrixxデモサイトには、複数の言語ブランチが含まれ、次の構造を使用します。

```xml
/content
    |- geometrixx
             |- en
             |- fr
             |- de
             |- es
             |- it
             |- ja
             |- zh
```

サイトの各言語ブランチは、言語コピーと呼ばれます。 言語コピーのルートページ（言語ルート）は、言語コピー内のコンテンツの言語を識別します。 例えば、`/content/geometrixx/fr` は、フランス語の言語コピー用の言語ルートです。ソースサイトの翻訳の実行時に適切な言語がターゲットになるように、言語コピーでは、[正しく設定された言語ルート](/help/sites-administering/tc-prep.md#creating-a-language-root)を使用する必要があります。

サイトのコンテンツを最初にオーサリングするための言語コピーが言語マスターです。言語マスターは、他の言語に翻訳されるソースです。

翻訳するサイトを準備するには、次の手順を使用します。

1. 言語マスターの言語ルートを作成します。例えば、英語の Geometrixx Demo Site の言語ルートは /content/geometrixx/en です。[言語ルートの作成](/help/sites-administering/tc-prep.md#creating-a-language-root)に記載の情報に従って言語ルートが正しく設定されていることを確認してください。
1. 言語マスターのコンテンツをオーサリングします。
1. サイトの各言語コピーの言語ルートを作成します。例えば、Geometrixxサンプルサイトのフランス語の言語コピーは/content/geometrixx/fr です。

翻訳するコンテンツの準備が完了したら、言語コピーおよび関連する翻訳プロジェクトの不足ページを自動的に作成できます（[翻訳プロジェクトの作成](/help/sites-administering/tc-manage.md)を参照）。AEM のコンテンツ翻訳プロセスの概要については、[多言語サイトのコンテンツの翻訳](/help/sites-administering/translation.md)を参照してください。

## 言語ルートの作成 {#creating-a-language-root}

コンテンツの言語を識別する言語コピーのルートページとして言語ルートを作成します。 言語ルートを作成したら、その言語コピーを含む翻訳プロジェクトを作成できます。

言語ルートを作成するには、ページを作成し、「名前」プロパティの値として ISO 言語コードを使用します。言語コードは次のどちらかの形式にしてください。

* `<language-code>`サポートされている言語コードは、ISO-639-1 で定義されている 2 文字のコード（例：`en`）です。

* `<language-code>_<country-code>` または `<language-code>-<country-code>` サポートされている国コードは、ISO 3166 で定義されている小文字または大文字 2 文字のコードです（例：`en_US`、`en_us`、`en_GB`、`en-gb`）。

グローバルサイト用に選択した構造に従って、どちらかの形式を使用できます。例えば、Geometrixx サイトのフランス語の言語コピーのルートページの「名前」プロパティは `fr` になります。Name プロパティはリポジトリ内のページノードの名前として使用されるので、ページのパスを決定します。 (http://localhost:4502/content/geometrixx/fr.html)

次の手順では、タッチ操作向け UI を使用して、Web サイトの言語コピーを作成します。 クラシック UI の使用手順については、 [クラシック UI を使用した言語ルートの作成](/help/sites-administering/tc-lroot-classic.md).

1. Sites に移動します。
1. 言語コピーを作成するサイトをクリックまたはタップします。

   例えば、Geometrixx Outdoorsサイトの言語コピーを作成するには、「Geometrixx Outdoorsサイト」をクリックまたはタップします。

1. 「作成」をクリックまたはタップして、「ページを作成」をクリックまたはタップします。

   ![chlimage_1-21](assets/chlimage_1-21.png)

1. ページテンプレートを選択して、「次へ」をクリックまたはタップします。
1. 「名前」フィールドに言語コードを入力します。言語コードの形式は `<language-code>` または `<language-code>_<country-code>` です。例：`en`、`en_US`、`en_us`、`en_GB`、`en_gb`。ページのタイトルを入力します。

   ![chlimage_1-22](assets/chlimage_1-22.png)

1. 「作成」をクリックまたはタップします。確認のダイアログボックスで、「**完了**」をクリックまたはタップして Sites コンソールに戻ります。または「**開く**」をクリックまたはタップして言語コピーを開きます。

## 言語ルートのステータスの確認 {#seeing-the-status-of-language-roots}

タッチ操作向け UI には参照パネルがあり、作成された言語ルートのリストが表示されます。

![chlimage_1-23](assets/chlimage_1-23.png)

次の手順では、タッチ操作向け UI を使用してページの参照パネルを開きます。

1. サイトコンソールで、サイトのページを選択し、「**参照**」をクリックまたはタップします。

   ![chlimage_1-24](assets/chlimage_1-24.png)

1. 参照パネルで、「**言語コピー**」をクリックまたはタップします。Web サイトの言語コピーが言語コピーパネルに表示されます。
