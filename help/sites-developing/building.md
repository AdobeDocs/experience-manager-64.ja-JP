---
title: AEM アプリケーションへのタグの作成
seo-title: Building Tagging into an AEM Application
description: カスタム AEM アプリケーション内のタグまたは拡張タグをプログラムで操作します
seo-description: Programmatically work with tags or extending tags within a custom AEM application
uuid: 0549552e-0d51-4162-b418-babf4ceee046
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: platform
content-type: reference
discoiquuid: 032aea1f-0105-4299-8d32-ba6bee78437f
feature: Tagging
exl-id: b3b0f505-3d7d-493d-a37b-abc8a365f95b
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '875'
ht-degree: 67%

---

# AEM アプリケーションへのタグの作成{#building-tagging-into-an-aem-application}

カスタム AEM アプリケーション内のタグまたは拡張タグをプログラムで操作するために、このページでは、次の使用方法を説明します。

* [タグ付け API](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/javadoc/com/day/cq/tagging/package-summary.html)

これは、次とやり取りします。

* [タグ付けフレームワーク](/help/sites-developing/framework.md)

タグに関する関連情報については、次を参照してください。

* [タグの管理](/help/sites-administering/tags.md) タグの作成と管理、およびタグが適用されるコンテンツについて説明します。
* コンテンツのタグ付けについては、[タグの使用](/help/sites-authoring/tags.md)を参照してください。

## タグ付け API の概要 {#overview-of-the-tagging-api}

AEM の[タグ付けフレームワーク](/help/sites-developing/framework.md)の実装により、JCR API を使用してタグおよびタグコンテンツを管理できます。TagManager は、値として入力されたタグを `cq:tags` 文字列配列プロパティが重複していない場合、存在しないタグを指すタグ ID が削除され、移動したタグまたは結合されたタグの TagID が更新されます。 TagManager は、間違った変更を元に戻す JCR 監視リスナーを使用します。メインクラスは [com.day.cq.tagging](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/tagging/package-summary.html) パッケージ内にあります。

* JcrTagManagerFactory - `TagManager` の JCR ベースの実装を返します。タグ付け API のリファレンス実装です。
* `TagManager` - パスと名前を使用して、タグを解決して作成できます。
* `Tag` - タグオブジェクトを定義します。

### JCR ベースの TagManager の取得 {#getting-a-jcr-based-tagmanager}

TagManager インスタンスを取得するには、JCR `Session` を取得して `getTagManager(Session)` ) を呼び出す必要があります。

```java
@Reference
JcrTagManagerFactory jcrTagManagerFactory;

TagManager tagManager = jcrTagManagerFactory.getTagManager(session);
```

通常の Sling コンテキストでは、`TagManager` を `ResourceResolver` に適合させることもできます。

```java
TagManager tagManager = resourceResolver.adaptTo(TagManager.class);
```

### Tag オブジェクトの取得 {#retrieving-a-tag-object}

`Tag` は、既存のタグを解決するか新しいタグを作成することにより、`TagManager` を介して取得できます。

```java
Tag tag = tagManager.resolve("my/tag"); // for existing tags

Tag tag = tagManager.createTag("my/tag"); // for new tags
```

`Tags` を JCR `Nodes` にマップする JCR ベースの実装の場合、リソースがあれば（例：`/content/cq:tags/default/my/tag`）、Sling の `adaptTo` メカニズムを直接使用できます。

```java
Tag tag = resource.adaptTo(Tag.class);
```

タグは（ノードではなく）リソースからのみ変換できますが、タグはノードとリソースの両方に変換できます。

```java
Node node = tag.adaptTo(Node.class);
Resource node = tag.adaptTo(Resource.class);
```

>[!NOTE]
>
>`Node` は Sling の `Adaptable.adaptTo(Class)` メソッドを実装しないので、`Node` を `Tag` に直接適合させることはできません。

### タグの取得と設定 {#getting-and-setting-tags}

```java
// Getting the tags of a Resource:
Tag[] tags = tagManager.getTags(resource); 

// Setting tags to a Resource:
tagManager.setTags(resource, tags);
```

### タグの検索 {#searching-for-tags}

```java
// Searching for the Resource objects that are tagged with the tag object:
Iterator<Resource> it = tag.find();

// Retrieving the usage count of the tag object:
long count = tag.getCount();

// Searching for the Resource objects that are tagged with the tagID String:
 RangeIterator<Resource> it = tagManager.find(tagID);
```

>[!NOTE]
>
>次の有効な `RangeIterator` を使用できます。
>
>`com.day.cq.commons.RangeIterator`

### タグの削除 {#deleting-tags}

```java
tagManager.deleteTag(tag);
```

### タグの複製 {#replicating-tags}

タグのタイプは `Replicator` なので、タグで複製サービス（`nt:hierarchyNode`）を使用できます。

```java
replicator.replicate(session, replicationActionType, tagPath);
```

## クライアント側でのタグ付け {#tagging-on-the-client-side}

`CQ.tagging.TagInputField` は、タグを入力するためのフォームウィジェットです。既存のタグから選択できるポップアップメニューを備えており、自動入力などの機能もあります。xtype はです。 `tags`.

## タグのガベージコレクター {#the-tag-garbage-collector}

タグのガベージコレクターは、非表示および未使用のタグをクリーンアップするバックグラウンドサービスです。非表示および未使用のタグは以下のタグです `/content/cq:tags` それは `cq:movedTo` プロパティとは異なり、コンテンツノードでは使用されません。このプロパティの数は 0 です。 この遅延削除プロセスを使用すると、移動や結合操作の一環としてコンテンツノード（`cq:tags` プロパティ）をアップデートする必要がありません。`cq:tags` プロパティの参照は、`cq:tags` プロパティがアップデートされると自動的にアップデートされます（例：ページプロパティダイアログを介して）。

タグのガベージコレクターは、デフォルトで 1 日に 1 回実行されます。これは、次の場所で設定できます。

```xml
http://localhost:4502/system/console/configMgr/com.day.cq.tagging.impl.TagGarbageCollector
```

## タグ検索およびタグ一覧 {#tag-search-and-tag-listing}

タグ検索およびタグ一覧は次のように動作します。

* TagID の検索では、プロパティを持つタグを検索します `cq:movedTo` を TagID に設定し、 `cq:movedTo` タグ ID。

* タグタイトルを検索すると、 `cq:movedTo` プロパティ。

## 他の言語のタグ {#tags-in-different-languages}

タグの管理に関するドキュメントの説明に従い、の節を参照してください。 [異なる言語でのタグの管理](/help/sites-administering/tags.md#managing-tags-in-different-languages)、タグ `title`は異なる言語で定義できます。 言語に依存するプロパティがタグノードに追加されます。このプロパティは `jcr:title.<locale>` の形式を持ちます（例：フランス語訳は `jcr:title.fr`）`<locale>` は小文字の ISO ロケール文字列である必要があり、「 — 」の代わりに「_」を使用します。次に例を示します。 `de_ch`.

次の場合に **動物** タグが **製品** ページ、値 `stockphotography:animals` がプロパティに追加される `cq:tags` /content/geometrixx/en/products/jcr:content ノードの 翻訳は、タグノードから参照されます。

サーバーサイド API には、ローカライズされた `title` 関連のメソッドがあります。

* [com.day.cq.tagging.Tag](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/tagging/Tag.html)

   * getLocalizedTitle(Locale locale)
   * getLocalizedTitlePaths()
   * getLocalizedTitles()
   * getTitle(Locale locale)
   * getTitlePath(Locale locale)

* [com.day.cq.tagging.TagManager](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/tagging/TagManager.html)

   * canCreateTagByTitle(String tagTitlePath, Locale locale)
   * createTagByTitle(String tagTitlePath, Locale locale)
   * resolveByTitle(String tagTitlePath, Locale locale)

AEM では、言語はページ言語またはユーザー言語のどちらかから取得できます。

* JSP でページ言語を取得するには：

   * `currentPage.getLanguage(false)`

* JSP でユーザー言語を取得するには：

   * `slingRequest.getLocale()`

`currentPage` および `slingRequest` は、[&lt;cq:definedObjects>](/help/sites-developing/taglib.md) タグを介して JSP で使用できます。

タグ付けの場合、ローカライズはコンテキストに依存します。タグの `titles` はページ言語、ユーザー言語またはそれ以外の任意の言語で表示することができます。

### タグを編集ダイアログへの新しい言語の追加 {#adding-a-new-language-to-the-edit-tag-dialog}

以下の手順では、新しい言語（フィンランド語）を **タグ編集** ダイアログ：

1. **CRXDE** で、ノード `/content/cq:tags` の複数値プロパティ `languages` を編集します。

1. 追加 `fi_fi`  — フィンランド語のロケールを表す — 変更を保存します。

新しい言語（フィンランド語）が、ページプロパティのタグダイアログで、 **タグを編集** ダイアログで **タグ付け** コンソール。

>[!NOTE]
>
>新しい言語は、AEM で認識される言語である必要があります。つまり、`/libs/wcm/core/resources/languages` の下でノードとして使用できる必要があります。
