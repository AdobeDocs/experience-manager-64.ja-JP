---
title: AEM タグ付けフレームワーク
seo-title: AEM Tagging Framework
description: コンテンツのタグ付けとAEM Tagging インフラストラクチャの活用
seo-description: Tag content and leverage the AEM Tagging infrastructure
uuid: 55ba5977-217b-4b0f-a794-ddb9216ee62b
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: platform
content-type: reference
discoiquuid: 4b680d17-383b-4173-a444-0b7bdb24e6c8
feature: Tagging
exl-id: bae592db-dc36-409f-b841-0582c464c3f6
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '1800'
ht-degree: 64%

---

# AEM タグ付けフレームワーク{#aem-tagging-framework}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

コンテンツにタグを付けてAEMタグ付けインフラストラクチャを活用するには：

* タグは、[`cq:Tag`](#tags-cq-tag-node-type) タイプのノードとして[分類階層のルートノード](#taxonomy-root-node)の下に存在する必要があります。
* タグ付けされたコンテンツノードの`NodeType`には、[`cq:Taggable`](#taggable-content-cq-taggable-mixin) Mixin が含まれている必要があります。
* この [タグ ID](#tagid) がコンテンツノードの [`cq:tags`](#tagged-content-cq-tags-property) プロパティを持ち、型のノードに解決されます。 [`cq:Tag`.](#tags-cq-tag-node-type)

## タグ：cq:Tag ノードタイプ  {#tags-cq-tag-node-type}

タグの宣言は、リポジトリーにおける `cq:Tag.` タイプのノードにキャプチャされます。

タグは、単純な単語 ( 例： `fruit`) または階層的な分類 ( 例： `fruit/apple`というのは、果物全般と、より具体的なリンゴの両方を意味している )。

タグは一意のタグ ID で識別されます。

タグには、タイトル、ローカライズされたタイトル、説明など、オプションのメタ情報が含まれます。 ユーザーインターフェイスには、`TagID` ではなくタイトル（存在する場合）が表示されます。

タグ付けフレームワークでは、作成者やサイト訪問者に、特定の事前定義されたタグだけを使用するよう制限を設けることもできます。

### タグの特徴 {#tag-characteristics}

* ノードタイプは `cq:Tag` です。
* ノード名は[`TagID`](#tagid) の構成要素になります。
* [`TagID`](#tagid) には常に[名前空間](#tag-namespace)が含まれています。
* オプション `jcr:title` プロパティ（UI に表示するタイトル）
* オプション `jcr:description` プロパティ
* 子ノードを含む場合、これは [コンテナタグで使用できます。](#container-tags)
* リポジトリ内で、 [分類のルートノード。](#taxonomy-root-node)

### タグ ID {#tagid}

`TagID` は、リポジトリー内のタグノードに解決されるパスを識別します。

通常、 `TagID` は、名前空間で始まる略記法か、 [分類のルートノード](#taxonomy-root-node).

コンテンツがタグ付けされているときに、コンテンツがまだ存在しない場合は、 [`cq:tags`](#tagged-content-cq-tags-property) プロパティがコンテンツノードに追加され、 `TagID` がプロパティの文字列配列値に追加されます。

`TagID` は、[名前空間](#tag-namespace)とそれに続くローカル`TagID` で構成されます。[コンテナタグ](#container-tags)にはサブタグがあり、これは分類における階層順序を表します。サブタグは、任意のローカル`TagID` と同じタグを参照するのに使用できます。例えば、`fruit` というタグが `fruit/apple` や `fruit/banana` などのサブタグを含むコンテナタグであっても、コンテンツにこのタグを付けることができます。

### 分類のルートノード {#taxonomy-root-node}

分類のルートノードは、リポジトリー内にあるすべてのタグの基本パスです。分類のルートノードは、`cq:Tag` タイプのノードにすることができません。

AEM の基本パスは `/content/cq:tags` であり、ルートノードのタイプは `cq:Folder` です。

### タグの名前空間 {#tag-namespace}

名前空間はグループ化を可能にします。 最も一般的な使用例は、サイトごとに名前空間（公開、内部、ポータルなど）を持つ場合、または大規模なアプリケーションごとに名前空間を持つ場合ですが、名前空間は他の様々なニーズに使用できます。 名前空間は、現在のコンテンツに適用されるタグのサブセット（つまり特定の名前空間のタグ）のみを表示するためにユーザーインターフェイスで使用されます。

タグの名前空間は、分類サブツリーの最初のレベルです。これは、[分類のルートノード](#taxonomy-root-node)の直下のノードです。名前空間は `cq:Tag` タイプのノードで、その親は `cq:Tag` ノードタイプではありません。

すべてのタグには名前空間があります。名前空間が指定されていない場合、タグはデフォルトの名前空間 ( `TagID` `default` ( タイトルは `Standard Tags`) を `/content/cq:tags/default`.

### コンテナタグ {#container-tags}

コンテナタグは、任意の数およびタイプの子ノードを含む、`cq:Tag` タイプのノードです。これにより、カスタムメタデータを使用してタグモデルを強化できます。

さらに、分類のコンテナタグ（スーパータグ）は、すべてのサブタグの小計として機能します。例えば、 `fruit/apple` は、 `fruit` 同様に。 つまり、でタグ付けされたコンテンツを検索します `fruit` また、次のタグが付いたコンテンツも見つかります： `fruit/apple`.

### タグ ID の解決 {#resolving-tagids}

タグ ID にコロンが含まれる場合 `:`の場合、コロンでタグまたはサブ分類から名前空間が区切られ、その後通常のスラッシュで区切られます `/`. タグ ID にコロンが含まれていない場合は、デフォルトの名前空間が暗示されます。

タグの標準の場所は `/content/cq:tags` の下のみです。

存在しないパスまたはを指さないパスを参照するタグ `cq:Tag` ノードは無効と見なされ、無視されます。

次の表に、いくつかのサンプルを示します `TagIDs`、要素、および方法 `TagID` リポジトリ内の絶対パスに解決されます。

| `TagID` | 名前空間 | ローカル ID | コンテナタグ | リーフタグ | 絶対リポジトリパス |
|---|---|---|---|---|---|
| `dam:fruit/apple/braeburn` | `dam` | `fruit/apple/braeburn` | `fruit`、`apple` | `braeburn` | `/content/cq:tags/dam/fruit/apple/braeburn` |
| `color/red` | `default` | `color/red` | `color` | `red` | `/content/cq:tags/default/color/red` |
| `sky` | `default` | `sky` | なし | `sky` | `/content/cq:tags/default/sky` |
| `dam:` | `dam` | なし | なし | なし | `/content/cq:tags/dam` |
| `/content/cq:tags/category/car` | `category` | `car` | `car` | `car` | `/content/cq:tags/category/car` |

### タグタイトルのローカリゼーション {#localization-of-tag-title}

タグにオプションのタイトル文字列（`jcr:title`）が含まれている場合は、プロパティ `jcr:title.<locale>` を追加することにより、表示するタイトルをローカライズすることができます。

詳しくは、以下を参照してください。

* [異なる言語のタグ、](/help/sites-developing/building.md#tags-in-different-languages) API の使用を説明するドキュメントです。
* [異なる言語でのタグの管理、](/help/sites-administering/tags.md#managing-tags-in-different-languages) タグ付けコンソールの使用について説明します。

### アクセス制御 {#access-control}

タグは、リポジトリー内で[分類のルートノード](#taxonomy-root-node) 作成者やサイト訪問者に対し、特定の名前空間でタグを作成する機能を許可または拒否するには、リポジトリで適切な ACL を設定します。

また、特定のタグまたは名前空間に対する読み取り権限を拒否すると、特定のコンテンツにタグを適用する機能が制御されます。

典型的な設定は次のとおりです。

* すべての名前空間への書き込みアクセス（`tag-administrators` 下への add／modify）を`/content/cq:tags` グループ／役割に許可する。
   * このグループは、追加設定なしで使用できる AEM に付属しています。
* 読み取り可能にする必要があるすべての名前空間への読み取りアクセスをユーザー／作成者に許可する。
* ユーザー／作成者がタグを自由に定義できる名前空間への書き込みアクセス（`/content/cq:tags/some_namespace` 下への `add_node`）をユーザー／作成者に許可する。

## タグ付け可能なコンテンツ：cq:Taggable Mixin {#taggable-content-cq-taggable-mixin}

アプリケーション開発者がコンテンツタイプにタグ付けを付加するには、ノードの登録（[CND](https://jackrabbit.apache.org/node-type-notation.html)）に `cq:Taggable` Mixin または `cq:OwnerTaggable` Mixin を含める必要があります。

`cq:OwnerTaggable` Mixin は `cq:Taggable` から継承されており、その目的は、所有者または作成者がコンテンツを分類できることを示すことです。AEM では、`cq:PageContent` ノードの属性にすぎません。`cq:OwnerTaggable` Mixin は、タグ付けフレームワークには必要ありません。

>[!NOTE]
>
>集約されたコンテンツアイテムの最上位ノード（またはその `jcr:content` ノード）では、タグの有効化だけを行うことをお勧めします。以下に例を示します。
>
>* ページ ( `cq:Page`) で、 `jcr:content`ノードのタイプは `cq:PageContent` これには `cq:Taggable` mixin.
>* `jcr:content/metadata` ノードに常に `cq:Taggable` Mixin があるアセット（`cq:Asset`）。


### ノードタイプの表記（CND） {#node-type-notation-cnd}

ノードタイプの定義は、リポジトリー内に CND ファイルとして存在します。CND 表記は、[こちら](https://jackrabbit.apache.org/node-type-notation.html)の JCR ドキュメントの一部として定義されています。

AEM に含まれるノードタイプの基本的な定義は、次のようになります。

```text
[cq:Tag] > mix:title, nt:base
    orderable
    - * (undefined) multiple
    - * (undefined)
    + * (nt:base) = cq:Tag version

[cq:Taggable]
    mixin
    - cq:tags (string) multiple

[cq:OwnerTaggable] > cq:Taggable
    mixin
```

## タグ付けされたコンテンツ：cq:tags プロパティ {#tagged-content-cq-tags-property}

この `cq:tags` プロパティは、1 つ以上の `TagID`作成者またはサイト訪問者がコンテンツに適用した場合。 このプロパティは、[`cq:Taggable`](#taggable-content-cq-taggable-mixin) Mixin で定義されているノードに追加した場合にのみ意味があります。

>[!NOTE]
>
>AEM のタグ付け機能を使用するには、カスタムで開発されたアプリケーションで `cq:tags` 以外のタグプロパティを定義しないでください。

## タグの移動と統合 {#moving-and-merging-tags}

次に、[タグ付けコンソール](/help/sites-administering/tags.md)を使用してタグの移動または統合を実行した場合のリポジトリ内での影響について説明します。

* タグ A を `/content/cq:tags` の下のタグ B に移動または統合した場合：

   * タグ A は削除されず、 `cq:movedTo` プロパティ。
   * タグ B が作成され（移動の場合）、 `cq:backlinks` プロパティ。

* `cq:movedTo` はタグ B を指します。

   * このプロパティは、タグ A がタグ B に移動または結合されたことを意味します。
   * タグ B を移動すると、それに応じてこのプロパティが更新されます。したがって、タグ A は非表示になり、タグ A を指すコンテンツノード内のタグ ID を解決するためだけにリポジトリーに保持されます。
   * タグ A のようなタグは、それを指すコンテンツノードがなくなったら、タグのガベージコレクターによって削除されます。
   * `cq:movedTo` プロパティの特殊な値に `nirvana` があります。この値は、タグが削除されたにもかかわらず、保持する必要のある `cq:movedTo` が含まれるサブタブが存在することが原因でそのタグをリポジトリから削除できない場合に適用されます。

      >[!NOTE]
      >
      >`cq:movedTo` プロパティは、次のいずれかの条件を満たす場合にのみ、移動または統合されたタグに追加されます。
      >
      >1. タグがコンテンツで使用されている（つまり、参照が含まれている）。
      >1. タグが、既に移動された子を持っている。


* `cq:backlinks` は、それ以外を指す参照を保持します。つまり、タグ B に移動または結合されたすべてのタグのリストを保持します。

   * これは、タグ B が移動／結合／削除されたとき、またはタグ B がアクティブになったときに、`cq:movedTo` プロパティを最新の状態に保つために通常必要になります。この場合は、すべてのバックリンクタグもアクティブにする必要があります。

>[!NOTE]
>
>`cq:backlinks` プロパティは、次のいずれかの条件を満たす場合にのみ、移動または統合されたタグに追加されます。
>
>1. タグがコンテンツで使用されている（つまり、参照が含まれている）。
>1. タグが、既に移動された子を持っている。


* コンテンツノードの `cq:tags` プロパティを読み取ると、以下のように解決されます。

   1. `/content/cq:tags` 下で一致するものが見つからない場合、タグは返されません。
   1. タグに `cq:movedTo` プロパティが設定されている場合は、参照先のタグ ID が使用されます。

      * これは、その次のタグに `cq:movedTo` プロパティがある限り繰り返されます。
   1. 次のタグに `cq:movedTo` プロパティがない場合は、そのタグが読み取られます。


* タグを移動または結合したときに変更を発行するには、`cq:Tag` ノードとそのすべてのバックリンクを複製する必要があります。
   * これは、タグ管理コンソールでタグがアクティブにされたときに自動的に行われます。

* 後でページの `cq:tags` プロパティに対して更新がおこなわれると、「以前の」参照が自動的にクリーンアップされます。
   * 移動したタグを API で解決すると移動先のタグが戻され、移動先のタグ ID が提供されることから、この処理がトリガーされます。

## タグの移行 {#tags-migration}

Adobe Experience Manager 6.4 以降では、タグは、 `/content/cq:tags`. ただし、Adobe Experience Manager が以前のバージョンからアップグレードされたシナリオでは、タグは古い場所 `/etc/tags` に引き続き存在します。アップグレードされたシステムでは、タグをに移行する必要があります。 `/content/cq:tags`.

>[!NOTE]
>
>タグのページプロパティページでは、タグ ID( 例えば、 `geometrixx-outdoors:activity/biking`) の代わりに、タグの基本パス ( 例えば、 `/etc/tags/geometrixx-outdoors/activity/biking`) をクリックします。
>
>タグを一覧表示するには、`com.day.cq.tagging.servlets.TagListServlet` を使用できます。

>[!NOTE]
>
>タグマネージャー API をリソースとして使用することをお勧めします。

### アップグレードされたAEMインスタンスが TagManager API**をサポートしている場合

1. コンポーネントの開始時に、TagManager API は、コンポーネントがアップグレードされたAEMインスタンスであるかどうかを検出します。 アップグレードされたシステムでは、タグは `/etc/tags` 下に格納されます。

1. その後、TagManager API は後方互換モードで動作します。つまり、API はベースパスとして `/etc/tags` を使用します。そうでない場合は、新しい場所 `/content/cq:tags` を使用します。

1. タグの場所を更新します。

1. 新しい場所にタグを移行した後、次のスクリプトを実行します。

```java
import org.apache.sling.api.resource.*
import javax.jcr.*

ResourceResolverFactory resourceResolverFactory = osgi.getService(ResourceResolverFactory.class);
ResourceResolver resolver = resourceResolverFactory.getAdministrativeResourceResolver(null);
Session session = resolver.adaptTo(Session.class);

def queryManager = session.workspace.queryManager;
def statement = "/jcr:root/content/cq:tags//element(*, cq:Tag)[jcr:contains(@cq:movedTo,\'/etc/tags\') or jcr:contains(@cq:backlinks,\'/etc/tags\')]";
def query = queryManager.createQuery(statement, "xpath");

println "query = ${query.statement}\n";

def tags = query.execute().getNodes();


tags.each { node ->
        def tagPath = node.path;
        println "tag = ${tagPath}";

        if(node.hasProperty("cq:movedTo") && node.getProperty("cq:movedTo").getValue().toString().startsWith("/etc/tags")){

                def movedTo = node.getProperty("cq:movedTo").getValue().toString();

                println "cq:movedTo = ${movedTo} \n";

                movedTo = movedTo.replace("/etc/tags","/content/cq:tags");
                node.setProperty("cq:movedTo",movedTo);
        } else if(node.hasProperty("cq:backlinks")){

               String[] backLinks = node.getProperty("cq:backlinks").getValues();
               int count = 0;

               backLinks.each { value ->
                       if(value.startsWith("/etc/tags")){
                               println "cq:backlinks = ${value}\n";
                               backLinks[count] = value.replace("/etc/tags","/content/cq:tags");
    }
                       count++;
               }

               node.setProperty("cq:backlinks",backLinks);
  }
}
session.save();

println "---------------------------------Success-------------------------------------"
```

スクリプトは、`cq:movedTo/cq:backLinks` プロパティの値に `/etc/tags` が含まれているタグをすべて取得します。その後、取得した結果セットを反復し、 `cq:movedTo` および `cq:backlinks` プロパティ値を `/content/cq:tags` パスに解決します（値に `/etc/tags` が検出された場合 ）。

### アップグレードされたAEMインスタンスがクラシック UI で動作する場合**

>[!NOTE]
>
>クラシック UI は、ダウンタイムなしに準拠しておらず、新しいタグのベースパスをサポートしていません。 クラシック UI を使用する場合は、`/etc/tags` を作成し、その後に `cq-tagging` コンポーネントを再起動する必要があります。

アップグレードされたAEMインスタンスが TagManager API でサポートされ、クラシック UI で実行される場合：

1. 古いタグの基本パスへの参照が 1 回 `/etc/tags` は、tagId または新しいタグの場所を使用して置き換えられます。 `/content/cq:tags`、新しい場所にタグを移行できます `/content/cq:tags` CRX DE でコンポーネントを再起動します。

1. 新しい場所にタグを移行した後、上記のスクリプトを実行します。
