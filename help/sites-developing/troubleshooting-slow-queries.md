---
title: 処理に時間のかかるクエリのトラブルシューティング
seo-title: Troubleshooting Slow Queries
description: 処理に時間のかかるクエリのトラブルシューティング
seo-description: null
uuid: ad09546a-c049-44b2-99a3-cb74ee68f040
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.4/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: c01e42ff-e338-46e6-a961-131ef943ea91
exl-id: edffa86c-a157-45bc-a565-a57200debb37
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '2265'
ht-degree: 69%

---

# 処理に時間のかかるクエリのトラブルシューティング{#troubleshooting-slow-queries}

## 処理に時間のかかるクエリの分類 {#slow-query-classifications}

AEM で処理に時間のかかるクエリは、主に 3 つに分類されます。以下に重大な順に示します。

1. **インデックスのないクエリ**

   * インデックスに解決&#x200B;**されず**、結果を収集するために JCR のコンテンツをトラバースするクエリ

1. **制限（範囲指定）が不十分なクエリ**

   * インデックスには解決されるが、結果を収集するためにすべてのインデックスエントリをトラバースする必要があるクエリ

1. **結果セットが大きいクエリ**

   * 非常に多くの結果を返すクエリ

Oak クエリエンジンに各クエリを強制的に検査させるので、最初の 2 つのクエリの分類（インデックスがなく、制限が不十分）は、時間がかかります **潜在的な** result （コンテンツノードまたはインデックスエントリ）: **実際** 結果セット。

各結果候補を調査する動作をトラバースと呼びます。

結果候補をそれぞれ調査する必要があるので、実際の結果セットを特定するためのコストは、結果候補の数に比例して増大します。

クエリの制限を追加し、インデックスを調整すると、結果を迅速に取得できるように最適化された形式でインデックスデータを格納できます。また、結果候補セットを順次調査する必要性が低減するかなくなります。

AEM 6.3 では、デフォルトでトラバースの回数が 100,000 回に達すると、クエリが失敗し、例外がスローされます。この制限は、AEM 6.3 より前のAEMバージョンにはデフォルトで存在しませんが、Apache Jackrabbit Query Engine Settings OSGi 設定および QueryEngineSettings JMX bean（LimitReads プロパティ）で設定できます。

### インデックスのないクエリの検出 {#detecting-index-less-queries}

#### 開発時 {#during-development}

説明 **すべて** クエリを実行し、クエリプランに含まれていないことを確認します。 **/&amp;ast;traverse** 説明を含む。 クエリプランのトラバースの例：

* **プラン：** `[nt:unstructured] as [a] /* traverse "/content//*" where ([a].[unindexedProperty] = 'some value') and (isdescendantnode([a], [/content])) */`

#### デプロイメント後 {#post-deployment}

* インデックスのないトラバーサルクエリについて、`error.log` を監視します。

   * `*INFO* org.apache.jackrabbit.oak.query.QueryImpl Traversal query (query without index) ... ; consider creating and index`
   * このメッセージがログに記録されるのは、使用できるインデックスがない場合とクエリが多数のノードをトラバースする可能性がある場合のみです。インデックスが使用可能な場合、メッセージはログに記録されませんが、トラバースの量が少ないので処理にかかる時間は短くなります。

* AEM [クエリパフォーマンス](/help/sites-administering/operations-dashboard.md#query-performance) 操作コンソールおよび [説明](/help/sites-administering/operations-dashboard.md#explain-query) トラバーサルを探すクエリが遅いか、インデックスクエリの説明がない。

### 制限が不十分なクエリの検出 {#detecting-poorly-restricted-queries}

#### 開発時 {#during-development-1}

すべてのクエリの説明を実行し、クエリのプロパティ制限に一致するよう調整されたインデックスに解決されることを確認します。

* 理想的なクエリプランの範囲では、すべてのプロパティ制限、および少なくともクエリで最も厳密なプロパティ制限に `indexRules` を持ちます。
* 結果を並べ替えるクエリは、Lucene プロパティインデックスに解決される必要があります。このインデックスには、`orderable=true.` を設定するプロパティによる並べ替えに関するインデックスルールがあります。

#### 例えば、デフォルトの `cqPageLucene` には次のインデックスルールがありません： `jcr:content/cq:tags` {#for-example-the-default-cqpagelucene-does-not-have-an-index-rule-for-jcr-content-cq-tags}

cq:tags インデックスルールを追加する前

* **cq:tags インデックスルール**

   * デフォルトでは存在しません。

* **Query Builder クエリ**

   ```
   type=cq:Page
    property=jcr:content/cq:tags
    property.value=my:tag
   ```

* **クエリプラン**

   * `[cq:Page] as [a] /* lucene:cqPageLucene(/oak:index/cqPageLucene) *:* where [a].[jcr:content/cq:tags] = 'my:tag' */`

このクエリは `cqPageLucene` インデックスに解決されます。ただし、`jcr:content` または `cq:tags` のプロパティインデックスルールは存在しないので、この制限を評価する際に、`cqPageLucene` インデックス内のすべてのレコードが一致するかどうかを判断するためにチェックされます。つまり、インデックスに 100 万個の `cq:Page` ノードが含まれている場合は、結果セットを特定するために 100 万件のレコードがチェックされます。

cq:tags インデックスルールを追加した後

* **cq:tags インデックスルール**

   ```
   /oak:index/cqPageLucene/indexRules/cq:Page/properties/cqTags
    @name=jcr:content/cq:tags
    @propertyIndex=true
   ```

* **Query Builder クエリ**

   ```
   type=cq:Page
    property=jcr:content/cq:tags
    property.value=myTagNamespace:myTag
   ```

* **クエリプラン**

   * `[cq:Page] as [a] /* lucene:cqPageLucene(/oak:index/cqPageLucene) jcr:content/cq:tags:my:tag where [a].[jcr:content/cq:tags] = 'my:tag' */`

の indexRule の追加 `jcr:content/cq:tags` 内 `cqPageLucene` index allows `cq:tags` 最適化された方法で保存するデータ。

クエリが `jcr:content/cq:tags` 制限が実行された場合、インデックスは値で結果を検索できます。 つまり、100 個の `cq:Page` ノードに値として `myTagNamespace:myTag` が設定されている場合は、この 100 件の結果だけが返され、他の 999,000 件は制限チェックから除外されるので、パフォーマンスは 10,000 倍向上します。

  当然ながら、さらにクエリを制限すると、対象となる結果セットが少なくなり、クエリはさらに最適化されます。

同様に、 `cq:tags` プロパティ、制限付きのフルテキストクエリも含む `cq:tags` インデックスの結果はすべての全文一致を返すので、パフォーマンスが低下します。 cq:tags に対する制限は、その後にフィルタリングされます。

インデックス後にフィルタリングされるもう 1 つの原因は、開発中に見落とされることがよくあるアクセス制御リストです。ユーザーがアクセスできない可能性のあるパスがクエリによって返されていないかどうかを確認してみます。これをおこなうには、通常、コンテキスト構造を改良すると共に、クエリに適切なパス制限を指定します。

Lucene インデックスが多数の結果を返し、非常に小さなサブセットを返しているかどうかを識別するのに便利な方法は、クエリ結果での DEBUG ログを有効にすることです。 `org.apache.jackrabbit.oak.plugins.index.lucene.LucenePropertyIndex` また、インデックスから読み込まれるドキュメントの数を確認します。 最終結果の数と読み込まれたドキュメントの数を比較すると釣り合うはずです。詳しくは、[ログ](/help/sites-deploying/configure-logging.md)を参照してください。

#### デプロイメント後 {#post-deployment-1}

* の監視 `error.log` トラバーサルクエリの場合：

   * `*WARN* org.apache.jackrabbit.oak.spi.query.Cursors$TraversingCursor Traversed ### nodes ... consider creating an index or changing the query`

* AEM [クエリパフォーマンス](/help/sites-administering/operations-dashboard.md#query-performance) 操作コンソールおよび [説明](/help/sites-administering/operations-dashboard.md#explain-query) クエリプロパティの制限をインデックスプロパティルールに解決しないクエリプランを探すのに時間がかかるクエリ

### 結果セットが大きいクエリの検出 {#detecting-large-result-set-queries}

#### 開発時 {#during-development-2}

oak.queryLimitInMemory とoak.queryLimitReads のしきい値を低く設定し（例えば、それぞれ 10000 と 5000）、UnsupportedOperationException にヒットして「The query read more than x nodes...」と表示されたときに高負荷のクエリを最適化します。

これにより、リソースを集中的に使用するクエリ（つまり、インデックスのないクエリまたは対応するインデックスが少ないクエリ）を回避することができます。例えば、100 万個のノードを読み取るクエリでは、大量の IO が発生し、アプリケーション全体のパフォーマンスに悪影響を及ぼします。このため、上述の制限が原因で失敗するクエリは、分析して最適化する必要があります。

#### デプロイメント後 {#post-deployment-2}

* 大量のノードのトラバーサルまたは大量のヒープメモリの消費を引き起こすクエリについてログを監視します。

   * `*WARN* ... java.lang.UnsupportedOperationException: The query read or traversed more than 100000 nodes. To avoid affecting other tasks, processing was stopped.`
   * クエリを最適化して、走査するノードの数を減らします。

* ログを監視して、ヒープメモリを大量に消費しているクエリがないかどうかを調べます。

   * `*WARN* ... java.lang.UnsupportedOperationException: The query read more than 500000 nodes in memory. To avoid running out of memory, processing was stopped`
   * クエリを最適化して、ヒープメモリの使用量を減らします。

AEM 6.0 ～ 6.2 バージョンの場合は、AEM開始スクリプトの JVM パラメーターを使用してノードトラバーサルのしきい値を調整し、大きなクエリが環境をオーバーロードしないようにすることができます。 推奨される値は次のとおりです。

* `-Doak.queryLimitInMemory=500000`
* `-Doak.queryLimitReads=100000`

AEM 6.3 では、デフォルトで上述の 2 つのパラメーターが事前設定されており、OSGi QueryEngineSettings を使用して変更できます。

詳しくは、以下を参照してください。 [https://jackrabbit.apache.org/oak/docs/query/query-engine.html#Slow_Queries_and_Read_Limits](https://jackrabbit.apache.org/oak/docs/query/query-engine.html#Slow_Queries_and_Read_Limits)

## クエリパフォーマンスのチューニング {#query-performance-tuning}

AEM におけるクエリパフォーマンス最適化のモットーは次のとおりです。

**「制限は多いほどよい」**

以下に、クエリのパフォーマンスを確保するために推奨される調整の概要を示します。まずクエリ、次にあまり目立たないアクティビティ、その後必要に応じてインデックス定義をチューニングします。

### クエリステートメントの調整 {#adjusting-the-query-statement}

AEM では、以下のクエリ言語がサポートされています。

* Query Builder
* JCR-SQL2
* XPath

以下の例では、AEM 開発者が最もよく使用する Query Builder を使用していますが、JCR-SQL2 および XPath にも同じ原則が当てはまります。

1. クエリが既存の Lucene プロパティインデックスに解決されるようにノードタイプの制限を追加します。

   * **最適化されていないクエリ**

      ```
       property=jcr:content/contentType
       property.value=article-page
      ```

   * **最適化されたクエリ**

      ```
       type=cq:Page 
       property=jcr:content/contentType 
       property.value=article-page
      ```
   ノードタイプの制限がないクエリにより、AEM では `nt:base` ノードタイプが想定されます。これは、AEM のすべてのノードのサブタイプなので、実質上ノードタイプの制限は存在しません。

   設定 `type=cq:Page` は、このクエリのみを制限します `cq:Page` ノードに解決し、クエリをAEM cqPageLucene に解決し、結果をノードのサブセットに制限します（ノードのみ）。 `cq:Page` ノード ) をAEMで使用します。

1. クエリが既存の Lucene プロパティインデックスに解決されるようにクエリのノードタイプの制限を調整します。

   * **最適化されていないクエリ**

      ```
      type=nt:hierarchyNode
      property=jcr:content/contentType
      property.value=article-page
      ```

   * **最適化されたクエリ**

      ```
      type=cq:Page
      property=jcr:content/contentType
      property.value=article-page
      ```
   `nt:hierarchyNode` は、 `cq:Page`と仮定して `jcr:content/contentType=article-page` が適用されるのは次の場合のみです。 `cq:Page` カスタムアプリケーションを介したノードの場合、このクエリは `cq:Page` ノード `jcr:content/contentType=article-page`. ただしこれは、以下の理由から、次善策としての制限となります。

   * 他のノードは次から継承 `nt:hierarchyNode` ( 例： `dam:Asset`) 結果のセットに不必要な追加を行う。
   * 次に対してAEMが提供したインデックスが存在しません： `nt:hierarchyNode`しかし、 `cq:Page`.
   `type=cq:Page` を設定すると、このクエリは `cq:Page` ノードのみに限定され、AEM の cqPageLucene に解決されます。これにより、結果は AEM のノードのサブセット（cq:Page ノードのみ）に限定されます。

1. または、クエリが既存のプロパティインデックスに解決されるようにプロパティの制限を調整します。

   * **最適化されていないクエリ**

      ```
        property=jcr:content/contentType
        property.value=article-page
      ```

   * **最適化されたクエリ**

      ```
      property=jcr:content/sling:resourceType
      property.value=my-site/components/structure/article-page
      ```
   プロパティ制限の変更元 `jcr:content/contentType` （カスタム値）を既知のプロパティに追加する `sling:resourceType` プロパティインデックスに解決するクエリを許可します `slingResourceType` を使用して、すべてのコンテンツを `sling:resourceType`.

   （Lucene プロパティインデックスではなく）プロパティインデックスの使用が最も適しているのは、クエリがノードタイプを認識せず、単一のプロパティ制限によって結果セットが決まる場合です。

1. クエリに可能な限り厳密なパス制限を追加します。例： `/content/my-site/us/en` over `/content/my-site`または `/content/dam` over `/`.

   * **最適化されていないクエリ**

      ```
      type=cq:Page
      path=/content
      property=jcr:content/contentType
      property.value=article-page
      ```

   * **最適化されたクエリ**

      ```
      type=cq:Page
      path=/content/my-site/us/en
      property=jcr:content/contentType
      property.value=article-page
      ```
   次のパス制限の範囲を設定 `path=/content`から `path=/content/my-site/us/en` を使用すると、検査する必要のあるインデックスエントリの数を減らすことができます。 クエリがパスを非常に適切に制限できる場合 ( 単に `/content` または `/content/dam`を使用する場合、インデックスにが含まれていることを確認します。 `evaluatePathRestrictions=true`.

   注意： `evaluatePathRestrictions` インデックスのサイズを増やします。

1. 可能な場合は、`LIKE` や `fn:XXXX` などのクエリの関数や操作を避けます。これらのコストは、制限に基づいた結果の数に伴って増減するからです。

   * **最適化されていないクエリ**

      ```
      type=cq:Page
      property=jcr:content/contentType
      property.operation=like
      property.value=%article%
      ```

   * **最適化されたクエリ**

      ```
      type=cq:Page
      fulltext=article
      fulltext.relPath=jcr:content/contentType
      ```
   テキストがワイルドカード (「%...」) で始まる場合は、インデックスを使用できないので、LIKE 条件の評価には時間がかかります。 jcr:contains 条件は、フルテキストのインデックスの使用を可能にするので、推奨されています。これには、解決された Lucene プロパティインデックスに indexRule が必要です。 `jcr:content/contentType` と `analayzed=true`.

   のようなクエリ関数の使用 `fn:lowercase(..)` は、より複雑で目立ちにくいインデックスアナライザ構成の外では、より高速な同等物が存在しないので、最適化が困難になる場合があります。 他の範囲制限を指定し、クエリ全体のパフォーマンスを向上させることをお勧めします。これには、関数の操作対象となる結果候補のセットをできるだけ小さくする必要があります。

1. この調整は、Query Builder 固有であり、JCR-SQL2 または XPath には当てはまりません。******

   用途 [Query Builder の guessTotal](/help/sites-developing/querybuilder-api.md#using-p-guesstotal-to-return-the-results) 結果の完全なセットがすぐに必要**な**場合。

   * **最適化されていないクエリ**

      ```
      type=cq:Page
      path=/content
      ```

   * **最適化されたクエリ**

      ```
      type=cq:Page
      path=/content
      p.guessTotal=100
      ```
   クエリの実行が速いが結果の数が多い場合、p. `guessTotal` は、Query Builder クエリの重要な最適化です。

   `p.guessTotal=100` を指定すると、Query Builder は最初の 100 件の結果だけを収集し、さらに 1 つ以上の結果が存在するかどうかを示すブール値フラグを設定します（ただしカウントすると処理に時間がかかるので、残りの数は示されません）。この最適化は、ページネーションまたは無限ロードの使用例よりも優れており、結果のサブセットだけが増分的に表示されます。

## 既存のインデックスのチューニング {#existing-index-tuning}

1. 最適なクエリがプロパティインデックスに解決される場合、プロパティインデックスで可能なチューニングは最小限なので、できることはありません。
1. それ以外の場合は、クエリは Lucene プロパティインデックスに解決する必要があります。 解決できるインデックスがない場合は、「新しいインデックスの作成」に進んでください。
1. 必要に応じて、クエリを XPath または JCR-SQL2 に変換します。

   * **Query Builder クエリ**

      ```
      query type=cq:Page
      path=/content/my-site/us/en
      property=jcr:content/contentType
      property.value=article-page
      orderby=@jcr:content/publishDate
      orderby.sort=desc
      ```

   * **Query Builder クエリから生成された XPath**

      ```
      /jcr:root/content/my-site/us/en//element(*, cq:Page)[jcr:content/@contentType = 'article-page'] order by jcr:content/@publishDate descending
      ```

1. この XPath（または JCR-SQL2）を [Oak Index Definition Generator](https://oakutils.appspot.com/generate/index) に提供して、最適化された Lucene プロパティインデックス定義を生成します。

   **生成された Lucene プロパティインデックス定義**

   ```xml
   - evaluatePathRestrictions = true
   - compatVersion = 2
   - type = "lucene"
   - async = "async"
   - jcr:primaryType = oak:QueryIndexDefinition
       + indexRules 
       + cq:Page 
           + properties 
           + contentType 
               - name = "jcr:content/contentType"
               - propertyIndex = true
           + publishDate 
               - ordered = true
               - name = "jcr:content/publishDate"
   ```

1. 生成された定義を、追加的な方法で既存の Lucene プロパティインデックスに手動で結合します。 その他のクエリを満たすために使用される可能性があるので、既存の設定を削除しないよう注意してください。

   1. cq:Page を対象とする既存の Lucene プロパティインデックスを探します（インデックスマネージャーを使用）。この場合、 `/oak:index/cqPageLucene`.
   1. 最適化したインデックス定義（手順 4）と既存のインデックス（/oak:index/cqPageLucene）の設定の差分を特定し、欠けている設定を最適化したインデックスから既存のインデックス定義に追加します。
   1. AEM のインデックス再作成のベストプラクティスにより、このインデックス設定の変更が既存コンテンツに影響するかどうかに基づいて、更新または再インデックス付けのいずれかが必要になります。

## 新しいインデックスの作成 {#create-a-new-index}

1. クエリが既存の Lucene プロパティインデックスに解決されないことを確認します。解決される場合は、前述の既存インデックスのチューニングに関する節を参照してください。
1. 必要に応じて、クエリを XPath または JCR-SQL2 に変換します。

   * **Query Builder クエリ**

      ```
      type=myApp:Author
      property=firstName
      property.value=ira
      ```

   * **Query Builder クエリから生成された XPath**

      ```
      //element(*, myApp:Page)[@firstName = 'ira']
      ```

1. この XPath（または JCR-SQL2）を [Oak Index Definition Generator](https://oakutils.appspot.com/generate/index) に提供して、最適化された Lucene プロパティインデックス定義を生成します。

   **生成された Lucene プロパティインデックス定義**

   ```xml
   - compatVersion = 2
   - type = "lucene"
   - async = "async"
   - jcr:primaryType = oak:QueryIndexDefinition
       + indexRules 
       + myApp:AuthorModel 
           + properties 
           + firstName 
               - name = "firstName"
               - propertyIndex = true
   ```

1. 生成された Lucene プロパティインデックス定義をデプロイします。

   Oak Index Definition Generator によって新しいインデックスに提供された XML 定義を、Oak インデックス定義を管理する AEM プロジェクトに追加します（コードは Oak インデックス定義に依存するので、これらの定義はコードとして扱うことを忘れないでください）。

   通常の AEM ソフトウェア開発ライフサイクルに従って新しいインデックスをデプロイしてテストし、クエリがインデックスに解決され、効率よく実行されることを確認します。

   このインデックスを初めてデプロイしたときに、AEM によってインデックスに必要なデータが追加されます。

## インデックスレスクエリとトラバーサルクエリが正常なのはいつですか？ {#when-index-less-and-traversal-queries-are-ok}

AEM のコンテンツアーキテクチャは柔軟です。そのため、コンテンツ構造のトラバーサルが時間の経過と共に受け入れられないほど大きくならないことを予測したり保証したりすることは困難です。

したがって、パス制限とノードタイプ制限の組み合わせによってクエリが確実に満たされる場合を除き、インデックスがクエリを確実に満たすようにします。 **20 個未満のノードがトラバースされます。**

## クエリ開発ツール {#query-development-tools}

### アドビでのサポート {#adobe-supported}

* **Query Builder Debugger**

   * Query Builder クエリを実行するための Web UI。対応する XPath（クエリの説明を実行または Oak Index Definition Generator で使用）を生成します。
   * AEMの [/libs/cq/search/content/querydebug.html](http://localhost:4502/libs/cq/search/content/querydebug.html)

* **CRXDE Lite - クエリツール**

   * XPath および JCR-SQL2 クエリを実行するための Web UI。
   * AEMの [/crx/de/index.jsp](http://localhost:4502/crx/de/index.jsp) /ツール/クエリ…

* **[クエリの説明を実行](/help/sites-administering/operations-dashboard.md#explain-query)**

   * 任意の XPATH または JCR-SQL2 クエリの詳しい説明（クエリプラン、クエリ時間、結果数）が表示される AEM 操作ダッシュボード。

* **[処理に時間のかかるクエリ／一般的なクエリ](/help/sites-administering/operations-dashboard.md#query-performance)**

   * AEM で最近実行された処理に時間のかかるクエリおよび一般的なクエリが一覧表示される AEM 操作ダッシュボード。

* **[インデックスマネージャー](/help/sites-administering/operations-dashboard.md#the-index-manager)**

   * AEM インスタンスのインデックスを表示する AEM 操作 Web UI。既存のインデックス、ターゲットにできるインデックス、または増強できるインデックスの把握に役立ちます。

* **[ログ](/help/sites-administering/operations-dashboard.md#log-messages)**

   * Query Builder のログ記録

      * `DEBUG @ com.day.cq.search.impl.builder.QueryImpl`
   * Oak クエリ実行のログ記録

      * `DEBUG @ org.apache.jackrabbit.oak.query`


* **Apache Jackrabbit クエリエンジンの OSGi 設定**

   * トラバースクエリの失敗動作を設定する OSGi 設定。
   * AEMの [/system/console/configMgr#org.apache.jackrabbit.oak.query.QueryEngineSettingsService](http://localhost:4502/system/console/configMgr#org.apache.jackrabbit.oak.query.QueryEngineSettingsService)

* **NodeCounter JMX Mbean**

   * AEM のコンテンツツリーのノード数を推定するのに使用する JMX MBean。
   * AEMの [/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3DnodeCounter%2Ctype%3DNodeCounter](http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3DnodeCounter%2Ctype%3DNodeCounter)

### コミュニティによるサポート {#community-supported}

* **[Oak Index Definition Generator](https://oakutils.appspot.com/generate/index)**

   * XPath または JCR-SQL2 クエリステートメントから最適な Lucence プロパティインデックスを生成します。

* **[AEM Chrome Plug-in](https://chrome.google.com/webstore/detail/aem-chrome-plug-in/ejdcnikffjleeffpigekhccpepplaode?hl=ja-JP)**

   * Google Chrome Web ブラウザーの拡張機能で、実行されたクエリとそのクエリプランなど、リクエストごとのログデータをブラウザーの開発ツールコンソールに公開します。
   * [Sling Log Tracer 1.0.2 以上](https://sling.apache.org/downloads.cgi)がインストールされ、AEM で有効になっている必要があります。
