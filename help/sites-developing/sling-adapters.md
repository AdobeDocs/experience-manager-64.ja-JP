---
title: Sling アダプターの使用
seo-title: Sling アダプターの使用
description: Sling には、Adaptable インターフェイスを実装するオブジェクトを適切に変換するアダプターパターンが用意されています
seo-description: Sling には、Adaptable インターフェイスを実装するオブジェクトを適切に変換するアダプターパターンが用意されています
uuid: 07f66a33-072d-49e1-8e67-8b80a6a9072a
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: platform
content-type: reference
discoiquuid: c081b242-67e4-4820-9bd3-7e4495df459e
exl-id: 7780d04d-418e-494c-85c3-76bef5f35690
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '1747'
ht-degree: 89%

---

# Sling アダプターの使用{#using-sling-adapters}

[Sling](https://sling.apache.org) は、[Adaptable](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/adapter/Adaptable.html#adaptTo%28java.lang.Class%29) インターフェイスを実装するオブジェクトを簡単に変換するための [Adapter パターン](https://sling.apache.org/site/adapters.html)を提供します。このインターフェイスは、汎用の [adaptTo()](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/adapter/Adaptable.html#adaptTo%28java.lang.Class%29) メソッドを提供しており、このメソッドによってオブジェクトは引数として渡されるクラス型に変換されます。

例えば、次のように実行するだけで、Resource オブジェクトを対応する Node オブジェクトに変換できます。

```java
Node node = resource.adaptTo(Node.class);
```

## ユースケース {#use-cases}

次のようなユースケースがあります。

* 実装用のオブジェクトの取得

   例えば、汎用の [`Resource`](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/resource/Resource.html) インターフェイスの JCR ベース実装では、基盤の JCR [`Node`](https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html) にアクセスできます。

* 内部的なコンテキストオブジェクトを渡す必要があるオブジェクトのショートカット作成。

   例えば、JCR ベースの [`ResourceResolver`](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/resource/ResourceResolver.html) では、要求の [`JCR Session`](https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Session.html) への参照を保持しています。この JCR セッションは、その要求セッションに基づいて動作する多くのオブジェクト（[`PageManager`](https://helpx.adobe.com/jp/experience-manager/6-4/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/PageManager.html) や [`UserManager`](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/javadoc/com/day/cq/security/UserManager.html) など）を取得するために必要になります。

* サービスへのショートカット。

   稀なケース - `sling.getService()` も簡単に使用できます。

### 戻り値 Null {#null-return-value}

`adaptTo()` は null を返す場合があります。

これには様々な理由がありますが、その一部は次のとおりです。

* 実装がターゲットタイプをサポートしていない
* このケースを処理するアダプターファクトリがアクティブでない（サービスの参照が見つからないなどの理由で）
* 内部的な条件が合わなかった
* サービスを利用できない

null のケースを問題なく処理することが重要です。JSP レンダリングでは、JSP の問題によってコンテンツの一部が空になる場合に、その問題が受容されることもあります。

### キャッシュ {#caching}

パフォーマンスを改善する目的で、各実装では `obj.adaptTo()` 呼び出しから返されたオブジェクトを自由にキャッシュできます。`obj` が同じであれば、返されるオブジェクトも同じです。

このキャッシュ処理は、すべての `AdapterFactory` ベースのケースで実行されます。

ただし、汎用的なルールは存在せず、オブジェクトが新しいインスタンスである場合も既存のインスタンスである場合もあります。したがって、いずれの動作にも依存することはできません。重要なのは、特に `AdapterFactory` 内部において、このシナリオでオブジェクトが再利用可能であるということです。

### 仕組み {#how-it-works}

`Adaptable.adaptTo()` の実装には、様々な方法があります。

* オブジェクト自体による実装（このメソッド自体を実装して特定のオブジェクトにマッピングします）。
* [`AdapterFactory`](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/adapter/AdapterFactory.html)&#39;を使用して、任意のオブジェクトをマッピングできます。

   オブジェクトは、引き続き `Adaptable` インターフェイスを実装し、[`SlingAdaptable`](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/javadoc/org/apache/sling/adapter/SlingAdaptable.html) を拡張する必要があります（これは、Central Adapter Manager の `adaptTo` 呼び出しを渡します）。

   これにより、`Resource` などの既存クラスの `adaptTo` メカニズムにフックを組み込むことができます。

* これら 2 つの組み合わせ。

最初の例では、javadocs に何の `adaptTo-targets` が可能かが示されます。ただし、JCR ベースのリソースなどの特定のサブクラスでは、多くの場合、これは不可能です。後者の場合、`AdapterFactory` の実装は通常、バンドルのプライベートクラスの一部なので、クライアント API で公開されず、Javadoc にも表示されません。理論的には、[OSGi](/help/sites-deploying/configuring-osgi.md) サービスランタイムからすべての `AdapterFactory` 実装にアクセスし、「アダプタブル」（ソースとターゲット）の設定を調べることは可能ですが、相互にマッピングすることはできません。最終的には、これは内部ロジックに依存し、ドキュメントに記載する必要があります。従って、参照はこちらです。

## 参照 {#reference}

### Sling {#sling}

[**Resource**](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/Resource.html) は次の項目に適応します。

<table> 
 <tbody> 
  <tr> 
   <td><a href="https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html">Node</a></td> 
   <td>このリソースが JCR ノードベースのリソースまたはノードを参照する JCR プロパティの場合。</td> 
  </tr> 
  <tr> 
   <td><a href="https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Property.html">Property</a></td> 
   <td>このリソースが JCR プロパティベースのリソースである場合。</td> 
  </tr> 
  <tr> 
   <td><a href="https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Item.html">Item</a></td> 
   <td>このリソースが JCR ベースのリソース（ノードまたはプロパティ）の場合。</td> 
  </tr> 
  <tr> 
   <td><a href="https://java.sun.com/j2se/1.5.0/docs/api//java/util/Map.html">Map</a></td> 
   <td>このリソースが JCR ノードベースのリソース（または値マップをサポートするその他のリソース）の場合、プロパティのマップを返します。</td> 
  </tr> 
  <tr> 
   <td><a href="https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/ValueMap.html">ValueMap</a></td> 
   <td>このリソースが JCR ノードベースのリソース（または値マップをサポートするその他のリソース）の場合、プロパティの使用しやすいマップを返します。また、<br /> <code><a href="https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/ResourceUtil.html#getvaluemap%28org.apache.sling.api.resource.resource%29">ResourceUtil.getValueMap(Resource)</a></code> を使用（null ケースを処理するなど）して達成することもできます。</td> 
  </tr> 
  <tr> 
   <td><a href="https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/inherit/InheritanceValueMap.html">InheritanceValueMap</a></td> 
   <td><a href="https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/ValueMap.html">ValueMap</a> の拡張。プロパティを探すときにリソースの階層を考慮することができます。</td> 
  </tr> 
  <tr> 
   <td><a href="https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/PersistableValueMap.html">PersistableValueMap</a></td> 
   <td>このリソースが JCR ノードベースのリソースであり、ユーザーがそのノードのプロパティを変更する権限を持っている場合。<br />
注意：複数の永続化可能マップでは値は共有されません。</td> 
  </tr> 
  <tr> 
   <td><a href="https://java.sun.com/j2se/1.5.0/docs/api/java/io/InputStream.html">InputStream</a></td> 
   <td>「ファイル」のバイナリコンテンツを返します<code>nt:resource</code></td></tr><tr><td></td><td></td></tr><tr><td></td><td></td></tr><tr><td></td><td></td></tr><tr><td></td><td></td></tr><tr><td></td><td><code>AuthorizableResourceProvider</code><code>org.apache.sling.jackrabbit.usermanager</code><code>/system/userManager</code></td></tr><tr><td></td><td></td></tr><tr><td></td><td></td></tr><tr><td></td><td><code>cq:Page</code><code>cq:PseudoPage</code></td></tr><tr><td></td><td><code>cq:Component</code></td></tr><tr><td></td><td><code>cq:Page</code></td></tr><tr><td></td><td><code>cq:Template</code></td></tr><tr><td></td><td><code>cq:Page</code></td></tr><tr><td></td><td></td></tr><tr><td></td><td></td></tr><tr><td></td><td><code>cq:Tag</code></td></tr><tr><td></td><td><code>cq:Preferences</code></td></tr><tr><td></td><td></td></tr><tr><td></td><td></td></tr><tr><td></td><td></td></tr><tr><td></td><td></td></tr><tr><td></td><td></td></tr><tr><td></td><td></td></tr><tr><td></td><td></td></tr><tr><td></td><td></td></tr><tr><td></td><td></td></tr><tr><td></td><td><code>cq:ContentSyncConfig</code></td></tr><tr><td></td><td><code>cq:ContentSyncConfig</code></td></tr></tbody></table>

[**ResourceResolver**](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/ResourceResolver.html) は次の項目に適応します。

<table> 
 <tbody> 
  <tr> 
   <td><a href="https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Session.html">Session</a></td> 
   <td>このリソースリゾルバーが JCR ベースのリソースリゾルバー（デフォルト）である場合の、要求の JCR セッション。</td> 
  </tr> 
  <tr> 
   <td><a href="https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/PageManager.html">PageManager</a></td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td><a href="https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/components/ComponentManager.html">ComponentManager</a></td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td><a href="https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/designer/Designer.html">デザイナー</a></td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td><a href="https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/javadoc/com/day/cq/dam/api/AssetManager.html">AssetManager</a></td> 
   <td>このリソースリゾルバーが JCR ベースのリソースリゾルバーである場合の、JCR セッションに基づいたもの。</td> 
  </tr> 
  <tr> 
   <td><a href="https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/javadoc/com/day/cq/tagging/TagManager.html">TagManager</a></td> 
   <td>このリソースリゾルバーが JCR ベースのリソースリゾルバーである場合の、JCR セッションに基づいたもの。</td> 
  </tr> 
  <tr> 
   <td><a href="https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/javadoc/com/day/cq/security/UserManager.html">UserManager</a></td> 
   <td>このリソースリゾルバーが JCR ベースのリソースリゾルバーであり、ユーザーが UserManager へのアクセス権限を持っている場合の、JCR セッションに基づいたもの。</td> 
  </tr> 
  <tr> 
   <td><a href="https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/javadoc/org/apache/jackrabbit/api/security/user/Authorizable.html">Authorizable</a> </td> 
   <td>現在のユーザー。</td> 
  </tr> 
  <tr> 
   <td><a href="https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/javadoc/org/apache/jackrabbit/api/security/user/User.html">User</a><br /> </td> 
   <td>現在のユーザー。</td> 
  </tr> 
  <tr> 
   <td><a href="https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/javadoc/com/day/cq/security/privileges/PrivilegeManager.html">PrivilegeManager</a></td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td><a href="https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/javadoc/com/day/cq/preferences/Preferences.html">環境設定</a></td> 
   <td>現在のユーザーの環境設定（このリソースリゾルバーが JCR ベースのリソースリゾルバーである場合、JCR セッションに基づいたもの）。</td> 
  </tr> 
  <tr> 
   <td><a href="https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/javadoc/com/day/cq/preferences/PreferencesService.html">PreferencesService</a></td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td><a href="https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/javadoc/com/day/cq/auth/pin/PinManager.html">PinManager</a></td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td><a href="https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/javadoc/com/day/cq/search/QueryBuilder.html">QueryBuilder</a></td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td><a href="https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/Externalizer.html">Externalizer</a></td> 
   <td>要求オブジェクトがない場合でも、絶対 URL を外部化するためのもの。<br /> </td> 
  </tr> 
 </tbody> 
</table>

[**SlingHttpServletRequest**](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/SlingHttpServletRequest.html) は次の項目に適応します。

現時点ではターゲットはありませんが、Adaptable を実装し、カスタムの AdapterFactory 内でソースとして使用することは可能です。

[**SlingHttpServletResponse**](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/SlingHttpServletResponse.html) は次の項目に適応します。

<table> 
 <tbody> 
  <tr> 
   <td><a href="https://java.sun.com/j2se/1.5.0/docs/api/org/xml/sax/ContentHandler.html">ContentHandler</a><br />
（XML）</td> 
   <td>この応答が Sling リライター応答である場合。</td> 
  </tr> 
 </tbody> 
</table>

#### WCM {#wcm}

[**Page**](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/Page.html) は次の項目に適応します。

<table> 
 <tbody> 
  <tr> 
   <td><a href="https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/Resource.html">Resource</a><br /> </td> 
   <td>ページのリソース。</td> 
  </tr> 
  <tr> 
   <td><a href="https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/LabeledResource.html">LabeledResource</a></td> 
   <td>ラベル付きリソース（== this）。</td> 
  </tr> 
  <tr> 
   <td><a href="https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html">ノード</a></td> 
   <td>ページのノード。</td> 
  </tr> 
  <tr> 
   <td>...</td> 
   <td>ページのリソースが適応可能なすべての項目。</td> 
  </tr> 
 </tbody> 
</table>

[**Component**](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/components/Component.html) は次の項目に適応します。

| [リソース](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/Resource.html) | コンポーネントのリソース。 |
|---|---|
| [LabeledResource](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/LabeledResource.html) | ラベル付きリソース（== this）。 |
| [Node](https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html) | コンポーネントのノード。 |
| ... | コンポーネントのリソースが適応可能なすべての項目。 |

[**Template**](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/Template.html) は次の項目に適応します。

<table> 
 <tbody> 
  <tr> 
   <td><a href="https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/Resource.html">Resource</a><a href="https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html"><br /> </a></td> 
   <td>テンプレートのリソース。</td> 
  </tr> 
  <tr> 
   <td><a href="https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/LabeledResource.html">LabeledResource</a></td> 
   <td>ラベル付きリソース（== this）。</td> 
  </tr> 
  <tr> 
   <td><a href="https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html">ノード</a></td> 
   <td>このテンプレートのノード。</td> 
  </tr> 
  <tr> 
   <td>...</td> 
   <td>テンプレートのリソースが適応可能なすべての項目。</td> 
  </tr> 
 </tbody> 
</table>

#### セキュリティ {#security}

[**Authorizable**](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/javadoc/com/day/cq/security/Authorizable.html)、[**User**](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/javadoc/com/day/cq/security/User.html) および [**Group**](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/javadoc/com/day/cq/security/Group.html) は次の項目に適応します。

| [ノード](https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html) | ユーザーまたはグループのホームノードを返します。 |
|---|---|
| [ReplicationStatus](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/javadoc/com/day/cq/replication/ReplicationStatus.html) | ユーザーまたはホームノードのレプリケーションステータスを返します。 |

#### DAM {#dam}

[**Asset**](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/javadoc/com/day/cq/dam/api/Asset.html) は次の項目に適応します。

| [リソース](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/Resource.html) | アセットのリソース。 |
|---|---|
| [ノード](https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html) | アセットのノード。 |
| ... | アセットのリソースが適応可能なすべての項目。 |

#### タグ付け {#tagging}

[**Tag**](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/javadoc/com/day/cq/tagging/Tag.html) は次の項目に適応します。

| [リソース](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/Resource.html) | タグのリソース。 |
|---|---|
| [ノード](https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html) | タグのノード。 |
| ... | タグのリソースが適応可能なすべての項目。 |

#### その他 {#other}

さらに、Sling、JCR、OCM では、カスタム OCM（` [AdapterFactory](https://sling.apache.org/site/adapters.html#Adapters-AdapterFactory)`Object Content Mapping）オブジェクト用の [](https://jackrabbit.apache.org/object-content-mapping.html) も提供しています。
