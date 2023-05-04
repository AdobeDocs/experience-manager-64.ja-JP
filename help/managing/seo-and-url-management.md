---
title: SEO と URL 管理のベストプラクティス
seo-title: SEO and URL Management Best Practices
description: AEMの実装でこれらを達成するための SEO のベストプラクティスと推奨事項について説明します。
seo-description: Learn about SEO best practices and recommendations for achieving these on an AEM implementation.
uuid: 7fffbe30-7cf8-44ce-b275-e128732577dd
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.4/MANAGING
topic-tags: managing
content-type: reference
discoiquuid: 150b43e3-9fb3-4c1c-b1cd-ccfd162974ad
exl-id: d45fe856-4709-437b-b193-e8243a695d2c
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '3133'
ht-degree: 65%

---

# SEO と URL 管理のベストプラクティス{#seo-and-url-management-best-practices}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

検索エンジン最適化（SEO）は、多くのマーケターにとって重要な関心事となっています。したがって、多くの AEM プロジェクトで SEO の懸念に対処する必要があります。

このドキュメントでは、まず、AEM の実装でこうした目的を達成するための [SEO のベストプラクティス](#seo-best-practices)および推奨事項を説明します。その次に、最初の節で提示するより[複雑な実装手順](#aem-configurations)のいくつかについて詳しく説明していきます。

## SEO のベストプラクティス {#seo-best-practices}

この節では、一般的な SEO のベストプラクティスをいくつか説明します。

### URL {#urls}

URL に関しては、一般に認められたいくつかのベストプラクティスがあります。

AEM プロジェクトで URL を評価するときには、次のことを確認してください。

* 「ユーザーが URL を目にしたときに、ページのコンテンツを見なくても、そのページの内容を説明できますか。」

回答が「はい」の場合、URL は検索エンジンで適切に機能する可能性が高くなります。

SEO 用の URL を作成する方法に関する一般的なヒントを以下に示します。

* ハイフンを使用して単語を区切ります。

   * ページにハイフン (-) を区切り文字として使用する名前を付けます。
   * キャメルケース、アンダースコアおよびスペースの使用は避けます。

* 可能な場合、クエリパラメーターの使用は避けます。必要に応じて、2 つ以下に制限します。

   * ディレクトリ構造を使用して、情報アーキテクチャを示します（使用可能な場合）。
   * ディレクトリ構造を使用できない場合は、クエリ文字列の代わりに、Sling セレクターを URL で使用します。Sling セレクターを使用すると、提供される SEO 値に加えて、Dispatcher でページをキャッシュできるようになります。

* URL が人間が読み取りやすいほど、より良い結果が得られます。URL にキーワードが存在すると、値がブーストされます。

   * ページでセレクターを使用する場合は、セマンティックな値を提供するセレクターをお勧めします。
   * 人が URL を読み取れない場合、検索エンジンも読み取れません。
   * 例： `mybrand.com/products/product-detail.product-category.product-name.html` を選択します。 `mybrand.com/products/product-detail.1234.html`

* 可能な限りサブドメインを避けます。サブドメインは、検索エンジンによって異なるエンティティとして扱われ、サイトの SEO 値がフラグメント化されます。

   * 代わりに、第 1 レベルのサブパスを使用します。例えば、`es.mybrand.com/home.html` の代わりに、`www.mybrand.com/es/home.html` を使用します。
   * このガイドラインに従って、コンテンツの表示方法に合わせてコンテンツ階層を計画します。

* URL の長さとキーワードの位置が増えると、URL でのキーワードの有効性が低下します。 つまり、短い方が良いのです。

   * 不要な URL を削除するには、AEMが提供する URL 短縮手法と機能を使用します。
   * 例えば、`mybrand.com/content/my-brand/en/myPage.html` より `mybrand.com/en/myPage.html` を選択します。

* 正規 URL を使用します。

   * 複数のパスから、または複数のパラメーターやセレクターで 1 つの URL を提供できない場合は必ず、ページで `rel=canonical` タグを使用します。
   * これは、AEMテンプレートのコードに含めることができます。

* 可能な限り、URL をページタイトルに一致させます。

   * コンテンツ作成者は、この方法に従うことをお勧めします。

* URL リクエストで大文字と小文字を区別しないようサポートします。

   * すべての受信要求を小文字として書き換えるように Dispatcher を設定します。
   * 小文字を使用してすべてのページを作成するようにコンテンツ作成者をトレーニングします。

* 各ページが 1 つのプロトコルからのみ提供されていることを確認します。

   * サイトが `http` 経由で提供され、ユーザーがチェックアウトまたはログインフォームを使用してページに到達した時点で、`https` に切り替わることがあります。このページからリンクするときに、ユーザーが `http` ページに戻り、`https` 経由でそれらのページにアクセスできる場合、検索エンジンでは、2 つの異なるページとして追跡されます。
   * Google では現在、`https` ページの方が `http` ページよりも推奨されています。こうした理由から、多くの場合、サイト全体を `https` 経由で提供する方が便利です。

### サーバーの設定 {#server-configuration}

サーバーの設定に関しては、次の手段を講じることで、適切なコンテンツのみがクロールされるようにすることができます。

* `robots.txt` ファイルを使用して、インデックスを作成する必要がないコンテンツのクローリングをブロックします。

   * ブロック **すべて** テスト環境でのクロール。

* 更新された URL を持つ新しいサイトを開始する際には、301 リダイレクトを実装して、既存の SEO ランキングが失われないようにします。
* サイトの favicon を含めます。
* XML サイトマップを実装して、検索エンジンがコンテンツをより簡単にクロールできるようにします。 モバイルサイトやレスポンシブサイト用のモバイルサイトマップを必ず含めてください。

## AEM の設定 {#aem-configurations}

ここでは、SEO に関する前述の推奨事項に従って AEM を設定するために必要な実装手順を説明します。

### Sling セレクターの使用 {#using-sling-selectors}

これまで、エンタープライズ Web アプリケーションを構築する場合、クエリパラメーターを使用するのが一般的に認められた手法でした。

近年は、URL をよりわかりやすくするために、クエリパラメーターを削除する傾向にあります。多くのプラットフォームでは、Web サーバーやコンテンツ配信ネットワーク（CDN）へのリダイレクトの実装などが行われますが、Sling を使用すると簡単です。Sling セレクター：

* URL の読みやすさを向上させます。
* Dispatcher でページをキャッシュでき、多くの場合、セキュリティが強化されます。
* 汎用サーブレットを使用してコンテンツを取得する代わりに、コンテンツを直接アドレス指定できます。これにより、リポジトリーに適用する ACL や、ディスパッチャーで適用するフィルターを活用できます。

#### サーブレット用のセレクターの使用 {#using-selectors-for-servlets}

AEMでは、サーブレットを記述する際に 2 つのオプションが用意されています。

* bin サーブレット
* Sling サーブレット

次の例では、これらのパターンの両方に従うサーブレットの登録方法と、Sling サーブレットを使用することで得られるメリットを示します。

#### bin サーブレット（1 レベル下） {#bin-servlets-one-level-down}

bin サーブレットは、多くの開発者が使い慣れている J2EE プログラミングのパターンに準拠しています。このサーブレットは、特定のパスに登録されます。AEM の場合は通常 `/bin` に登録され、必要な要求パラメーターをクエリ文字列から抽出します。

このタイプのサーブレットの SCR 注釈は、次のようになります。

```
@SlingServlet(paths = "/bin/myApp/myServlet", extensions = "json", methods = "GET")
```

続いて、`SlingHttpServletRequest` メソッドに含まれる `doGet` オブジェクトを使用して、クエリ文字列からパラメーターを抽出します。次に例を示します。

```
String myParam = req.getParameter("myParam");
```

使用される結果の URL は次のようになります。

`https://www.mydomain.com/bin/myApp/myServlet.json?myParam=myValue`

この方法では、次の点に注意してください。

* URL 自体が SEO 値を失います。 検索エンジンを含むサイトにアクセスするユーザーは、URL はコンテンツ階層ではなくプログラム的パスを表すので、URL からセマンティック値を受け取りません。
* URL にクエリパラメーターが含まれていることは、Dispatcher で応答をキャッシュできないことを意味します。
* このサーブレットを保護するには、独自のカスタムセキュリティロジックをサーブレットに実装する必要があります。
* `/bin/myApp/myServlet` を公開するように Dispatcher を（慎重に）設定する必要があります。単に `/bin` を公開すると、サイト訪問者に公開してはいけない特定のサーブレットへのアクセスが許可されます。

#### Sling サーブレット（1 レベル下） {#sling-servlets-one-level-down}

Sling サーブレットを使用すると、逆の方法でサーブレットを登録できます。 サーブレットをアドレス指定し、クエリパラメーターに基づいてサーブレットでレンダリングするコンテンツを指定するのではなく、目的のコンテンツをアドレス指定し、Sling セレクターに基づいてコンテンツをレンダリングするサーブレットを指定します。

このタイプのサーブレットの SCR 注釈は、次のようになります。

```
@SlingServlet(resourceTypes = "myBrand/components/pages/myPageType", selectors = "myRenderer", extensions = "json”, methods=”GET”)
```

この場合、URL によってアドレス指定されるリソース（`myPageType` リソースのインスタンス）にサーブレットで自動的にアクセスできます。アクセスするには、次の呼び出しをおこないます。

```
Resource myPage = req.getResource();
```

使用される結果の URL は次のようになります。

`https://www.mydomain.com/content/my-brand/my-page.myRenderer.json`

このアプローチの利点は次のとおりです。

* サイト階層とページ名に存在するセマンティクスで取得した SEO 値でベイク処理できます。
* クエリパラメーターがないので、Dispatcher で応答をキャッシュできます。さらに、アドレス指定されたページに対して行われた更新により、ページがアクティベートされると、このキャッシュが無効になります。
* ユーザーがこのサーブレットにアクセスしようとすると、`/content/my-brand/my-page` に適用されているすべての ACL が有効になります。
* Dispatcher は、Web サイトを提供する機能の 1 つとしてこのコンテンツを提供するようにあらかじめ設定されます。追加の設定は必要ありません。

### URL の書き換え {#url-rewriting}

AEM では、すべての Web ページが `/content/my-brand/my-content` に保存されます。これは、リポジトリーデータ管理の観点では便利な場合がありますが、必ずしもこの方法で顧客にサイトを表示するわけではなく、URL をできるだけ短くするという SEO のガイダンスと矛盾する可能性があります。さらに、同じ AEM インスタンスや異なるドメイン名から複数の Web サイトを提供している場合もあります。

この節では、AEMでこれらの URL を管理し、より読みやすく SEO に適した方法でユーザーに提示するために使用できるオプションについて説明します。

#### バニティ URL {#vanity-urls}

作成者が、プロモーション目的で別の場所からアクセス可能なページを作成する場合、ページごとに定義される AEM のバニティー URL が役立つことがあります。ページのバニティー URL を追加するには、 **[!UICONTROL Sites]** コンソールで該当するページに移動し、ページのプロパティを編集します。「**[!UICONTROL 基本]**」タブの下部に、バニティー URL を追加できるセクションが表示されます。複数の URL を使用してページにアクセスできるようにすると、ページの SEO 値が分断されるので、正規 URL タグをページに追加して、この問題を回避する必要があることに留意してください。

#### ページ名のローカライズ {#localized-page-names}

翻訳済みコンテンツのユーザーにローカライズされたページ名を表示したい場合があります。 次に例を示します。

* スペイン語を話すユーザーが次のページにアクセスするとします。

   `www.mydomain.com/es/home.html`

* この場合、URL を次のように表示した方が効果的です。

   `www.mydomain.com/es/casa.html`。

ページ名のローカライズに伴う課題は、AEM プラットフォームで使用可能なローカリゼーションツールの多くでは、コンテンツを同期しておくためには、ロケール間でページ名を一致させる必要があるという点です。

`sling:alias` プロパティを使用すると、両方を同時に実現できます。`sling:alias` を任意のリソースにプロパティとして追加すると、リソースのエイリアス名を使用することができます。前述の例では、次のようになります。

* JCR の次の場所にページがあるとします。

   `…/es/home`

* プロパティを追加します。

   `sling:alias` = `casa`

これにより、マルチサイトマネージャーなどの AEM 翻訳ツールでは、次のページ間の関係を引き続き維持できます。

* `/en/home`

* `/es/home`

また、エンドユーザーもページ名を母国語で操作できます。

>[!NOTE]
>
> この `sling:alias` プロパティは、 [ページプロパティ編集時のエイリアスプロパティ](/help/sites-authoring/editing-page-properties.md#advanced)

#### /etc/map {#etc-map}

標準 AEM インストールでは、

* OSGi 設定には:

   **Apache Sling Resource Resolver Factory**

   (`org.apache.sling.jcr.resource.internal.JcrResourceResolverFactoryImpl`)

* プロパティ:

   **マッピング場所**

   (`resource.resolver.map.location`)

* デフォルト：

   `/etc/map`

AEM で受信要求のマッピングまたはページ上の URL の書き換え、あるいはその両方を行うために、この場所にマッピング定義を追加できます。

新しいマッピングを作成するには、この場所の `sling:Mapping` または `/http` の下に新しい `/https` ノードを作成します。このノードで設定された `sling:match` および `sling:internalRedirect` プロパティに基づいて、AEM は、一致した URL のすべてのトラフィックを `internalRedirect` プロパティで指定された値にリダイレクトします。

これは、AEM および Sling の正式なドキュメントに記載されているアプローチですが、この実装で提供される正規表現のサポートは、`SlingResourceResolver` を直接使用することによって利用可能なオプションと比べると、範囲が限られています。また、この方法でマッピングを実装すると、Dispatcher のキャッシュの無効化に関する問題が生じることがあります。

次に、この問題がどのように生じるかについて例を示します。

1. ユーザーが Web サイトを訪問し、`https://www.mydomain.com/my-page.html` を要求します。
1. Dispatcher が、この要求を公開サーバーに転送します。
1. 公開サーバーが `/etc/map` を使用して、この要求を `/content/my-brand/my-page` に解決し、ページをレンダリングします。

1. Dispatcher が `/my-page.html` に応答をキャッシュし、応答をユーザーに返します。
1. コンテンツの作成者がこのページを変更し、アクティベートします。
1. Dispatcher フラッシュエージェントが `/content/my-brand/my-page`**の無効化要求を送信します。** Dispatcher はこのパスにページをキャッシュしていないので、古いコンテンツがキャッシュされたままになり、更新されません。

キャッシュの無効化の目的で、短い URL を長い URL にマッピングするカスタムディスパッチフラッシュルールを設定する方法があります。

ただし、これをより簡単に管理する方法もあります。

1. **SlingResourceResolver ルール**

   Web コンソール（例えば、localhost:4502/system/console/configMgr）を使用して、Sling Resource Resolver を設定できます。

   * **Apache Sling Resource Resolver Factory**

      `(org.apache.sling.jcr.resource.internal.JcrResourceResolverFactoryImpl)`。
   URL を短縮するために必要なマッピングを正規表現として構築した後、ビルドに含まれている OsgiConfignode の `config.publish` でこれらの設定を定義することをお勧めします。

   `/etc/map`マッピングを定義する代わりに、プロパティ **URL Mappings**（`resource.resolver.mapping`）に直接割り当てることができます。

   ```xml
   resource.resolver.mapping="[/content/my-brand/(.*)</$1]"
   ```

   この簡単な例では、URL に `/content/my-brand/` が存在する場合、URL の先頭から削除されます。

   これにより、URL は次のように変換されます。

   * `/content/my-brand/my-page.html` から
   * ただの `/my-page.html`

   これは、URL をできるだけ短く保つことをお勧めします。

1. **ページへの URL 出力のマッピング**

   Apache Sling Resource Resolver でマッピングを定義したら、ページに出力する URL が短く、適切になるように、それらのマッピングをコンポーネントで使用する必要があります。そのためには、`ResourceResolver` のマッピング関数を使用します。

   例えば、現在のページの子をリストアウトするカスタムナビゲーションコンポーネントを実装している場合、次のようなマッピングメソッドを使用できます。

   ```
   for (Page child : children) {
     String childUrl = resourceResolver.map(request, child.getPath());
     //Output the childUrl on the page here
   }
   ```

#### Apache HTTP サーバ mod_rewrite {#apache-http-server-mod-rewrite}

これまでに、URL をページに出力するときに、定義したマッピングを使用するために、マッピングをロジックとともにコンポーネントに実装しました。

最後の手順は、短縮された URL の Dispatcher での処理です。ここでは、`mod_rewrite` を使用します。`mod_rewrite` を使用する最大の利点は、URL が、Dispatcher モジュールに送信される&#x200B;*前に*&#x200B;長い形式に再びマッピングされる点です。つまり、Dispatcher は公開サーバーに長い URL を要求し、それに応じて URL をキャッシュします。したがって、公開サーバーからの Dispatcher フラッシュ要求により、そのコンテンツを正常に無効にすることができます。

このようなルールを実装するには、Apache HTTP Server の設定で仮想ホストに `RewriteRule` 要素を追加します。前の例の短縮 URL を展開する場合は、次のようなルールを実装できます。

```
<VirtualHost *:80>
  ServerName www.mydomain.com
  RewriteEngine on
  RewriteRule ^/(.*)$ /content/my-brand/$1 [PT,L]
  …
</VirtualHost>
```

### 正規 URL タグ {#canonical-url-tags}

正規 URL タグは、コンテンツのインデックス作成時に検索エンジンでページがどのように処理されるかを明確にするために、HTMLドキュメントの先頭に配置されるリンクタグです。 ページの URL に違いが含まれている場合でも、ページのインデックスが同じ（異なるバージョンの）ページになるようにするのがメリットです。

例えば、ページのプリンターフレンドリーなバージョンをサイトで提供する場合、検索エンジンでは、通常のバージョンのページとは別に、このページのインデックスが作成される可能性があります。正規タグは、同じであることを検索エンジンに通知します。

例：

* `https://www.mydomain.com/my-brand/my-page.html`
* `https://www.mydomain.com/my-brand/my-page.print.html`

両方について、ページの先頭に次のタグを適用します。

```xml
<link rel=”canonical” href=”my-brand/my-page.html”/>
```

`href` は、相対パスとして指定することも、絶対パスとして指定することもできます。ページの正規 URL を確認し、このタグを出力するには、このコードをページマークアップに挿入する必要があります。

### 大文字と小文字を区別しないための Dispatcher の設定 {#configuring-the-dispatcher-for-case-insensitivity}

すべてのページに小文字を使用して表示することをお勧めします。 ただし、URL に大文字を使用して Web サイトにアクセスする際に、ユーザーに 404 を返さないようにする必要があります。 こうした理由から、すべての受信 URL を小文字にマッピングするように、Apache HTTP Server の設定に書き換えルールを追加することをお勧めします。さらに、小文字の名前を使用してページを作成するようコンテンツの作成者をトレーニングする必要があります。

すべての受信トラフィックを強制的に小文字に変換するように Apache を設定するには、次のコードを `vhost` の設定に追加します。

```xml
RewriteEngine On
RewriteMap lowercase int:tolower
```

さらに、次のコードを `htaccess` ファイルの最上部に追加します。

```xml
RewriteCond $1 [A-Z]
RewriteRule ^(.*)$ /${lowercase:$1} [R=301,L]
```

### 開発環境を保護するための robots.txt の実装 {#implementing-robots-txt-to-protect-development-environments}

検索エンジンは、サイトをクロールする前に、サイトのルートに *ファイルがあるかどうかをチェック*&#x200B;するはずです`robots.txt`。ただし、Google、Yahoo、Bing などの主要な検索エンジンではすべてこの点が考慮されるのに対し、なじみのない検索エンジンの中には、この点が考慮されないものもあります。

サイト全体へのアクセスをブロックするための最も簡単な方法は、`robots.txt` というファイルに次の内容を指定して、サイトのルートに配置することです。

```xml
User-agent: *
Disallow: /
```

また、実稼働環境では、インデックスが作成されないように特定のパスを禁止することもできます。

ただし、`robots.txt` ファイルをサイトのルートに配置すると、Dispatcher フラッシュ要求によって、このファイルが除去されることがあり、URL マッピングによって、Apache HTTP Server の設定で定義された `DOCROOT` とは異なる場所にサイトのルートが置かれる可能性があります。このため、このファイルをオーサーインスタンスのサイトルートに配置し、パブリッシュインスタンスにレプリケートするのが一般的です。

### AEMでの XML サイトマップの作成 {#building-an-xml-sitemap-on-aem}

クローラーは、Web サイトの構造をより深く理解するために XML サイトマップを使用します。 サイトマップを提供することで SEO ランキングが向上する保証はありませんが、これは合意に基づくベストプラクティスです。 Web サーバー上で XML ファイルを手動で維持してサイトマップとして使用できますが、サイトマップをプログラムで生成することをお勧めします。これにより、作成者が新しいコンテンツを作成すると、サイトマップに変更が自動的に反映されます。

プログラムによってサイトマップを生成するには、`sitemap.xml` の呼び出しをリスンする Sling サーブレットを登録します。次に、サーブレットは、サーブレット API を介して提供されたリソースを使用して、現在のページとその子を参照し、XML を出力します。 XML はその後、Dispatcher でキャッシュされます。`robots.txt` ファイルのサイトマッププロパティで、この場所を参照する必要があります。さらに、新しいページがアクティベートされたときには必ず、このファイルがフラッシュされるように、カスタムフラッシュルールを実装する必要があります。

>[!NOTE]
>
>Sling サーブレットを登録すると、拡張子 `sitemap` のセレクター `xml` をリスンできます。これにより、末尾が以下のようになっている URL が要求されると、サーブレットによってリクエストが処理されます。
>
>`/<*path-to*>/page.sitemap.xml`
>
>その後、JCR API を使用して、リクエストからリクエストされたリソースを取得し、コンテンツツリー内のその時点からサイトマップを生成できます。
>
>このようなアプローチの利点は、同じインスタンスから複数のサイトを提供する場合です。 `/content/siteA.sitemap.xml` に対するリクエストでは `siteA` 用のサイトマップが生成され、`/content/siteB.sitemap.xml` のリクエストでは `siteB` 用のサイトマップが生成されます。コードを追加する必要はありません。

### レガシー URL の 301 リダイレクトの作成 {#creating-redirects-for-legacy-urls}

新しい構造でサイトの運用を開始するときには、次の 2 つの理由から、Apache HTTP Server で 301 リダイレクトを実装し、テストすることが重要です。

* レガシー URL は、時間の経過と共に SEO 値を構築しています。 リダイレクトを実装することで、検索エンジンはこの値を新しい URL に適用できます。
* サイトのユーザーが、これらのページにブックマークを作成している場合があります。 リダイレクトを実装すると、古いサイトでの取得を試みていた場所に最も近い新しいサイトのページに、ユーザーを確実に誘導できます。

301 リダイレクトの実装手順と、リダイレクトが期待どおりに動作しているかをテストするためのツールについては、以下の追加のリソースの節を必ず確認してください。

## その他のリソース {#additional-resources}

詳しくは、以下のその他のリソースを参照してください。

* [リソースマッピング](/help/sites-deploying/resource-mapping.md)
* [https://moz.com/blog/seo-cheat-sheet-anatomy-of-a-url](https://moz.com/blog/seo-cheat-sheet-anatomy-of-a-url)
* [https://moz.com/blog/15-seo-best-practices-for-structuring-urls](https://moz.com/blog/15-seo-best-practices-for-structuring-urls)
* [https://mysiteauditor.com/blog/top-10-most-important-seo-tips-for-url-optimization/](https://mysiteauditor.com/blog/top-10-most-important-seo-tips-for-url-optimization/)
* [https://sling.apache.org/documentation/the-sling-engine/servlets.html](https://sling.apache.org/documentation/the-sling-engine/servlets.html)
* [https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html)
* [https://httpd.apache.org/docs/current/mod/mod_rewrite.html](https://httpd.apache.org/docs/current/mod/mod_rewrite.html)
* [https://moz.com/blog/canonical-url-tag-the-most-important-advancement-in-seo-practices-since-sitemaps](https://moz.com/blog/canonical-url-tag-the-most-important-advancement-in-seo-practices-since-sitemaps)
* [https://en.wikipedia.org/wiki/Robots_exclusion_standard](https://en.wikipedia.org/wiki/Robots_exclusion_standard)
* [https://www.internetmarketingninjas.com/blog/search-engine-optimization/301-redirects/](https://www.internetmarketingninjas.com/blog/search-engine-optimization/301-redirects/)
* [https://github.com/Adobe-Marketing-Cloud/tools/tree/master/dispatcher/redirectTester](https://github.com/Adobe-Marketing-Cloud/tools/tree/master/dispatcher/redirectTester)
* [https://adobe-consulting-services.github.io/](https://adobe-consulting-services.github.io/)
