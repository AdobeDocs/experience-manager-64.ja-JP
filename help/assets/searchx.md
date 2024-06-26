---
title: Assets 検索の拡張
description: の検索機能の拡張 [!DNL Experience Manager] 標準搭載のアセット以外は、文字列でアセットを検索します。
contentOwner: AG
feature: Search
role: Developer
exl-id: d68c735f-2699-4923-a7e7-4d1356eae335
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '856'
ht-degree: 47%

---

# Assets 検索の拡張 {#extending-assets-search}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

Adobe Experience Manager Assets の検索機能を拡張できます。 すぐに使える [!DNL Experience Manager] Assets は、文字列でアセットを検索します。

検索は QueryBuilder インターフェイスを介して実行されるので、複数の述語を使用して検索をカスタマイズできます。`/apps/dam/content/search/searchpanel/facets` ディレクトリにあるデフォルトの述語セットをオーバーレイできます。

また、 [!DNL Experience Manager] アセット管理パネル。

>[!CAUTION]
>
>[!DNL Experience Manager] 6.4 以降、クラシック UI は廃止されます。発表については、 [廃止および削除された機能](../release-notes/deprecated-removed-features.md). タッチ操作対応 UI を使用することをお勧めします。 カスタマイズについては、 [検索ファセット](search-facets.md).

## オーバーレイ {#overlaying}

事前設定済みの述語をオーバーレイするには、`facets` ノードを `/libs/dam/content/search/searchpanel` から `/apps/dam/content/search/searchpanel/` にコピーするか、searchpanel 設定に別の `facetURL` プロパティを指定します（デフォルトでは `/libs/dam/content/search/searchpanel/facets.overlay.infinity.json` になります）。

![screen_shot_2012-06-05at113619am](assets/screen_shot_2012-06-05at113619am.png)

>[!NOTE]
>
>デフォルトでは、/の下のディレクトリ構造です。 `apps` が存在しないので、作成する必要があります。 ノードのタイプが、/以下のタイプと一致することを確認します。 `libs`.

## タブの追加 {#adding-tabs}

「検索」タブを追加するには、 [!DNL Experience Manager] アセット管理者。 追加のタブは以下の手順で作成します。

1. フォルダー構造 `/apps/wcm/core/content/damadmin/tabs,` がまだ存在しない場合は作成し、`tabs` ノードを `/libs/wcm/core/content/damadmin` からコピーして貼り付けます。
1. 必要に応じて、2 つ目のタブを作成し設定します。

   >[!NOTE]
   >
   >2 つ目の siteadminsearchpanel を作成する場合は、必ず `id` プロパティを使用して、フォームの競合を防ぎます。

## カスタム述語の作成 {#creating-custom-predicates}

[!DNL Experience Manager] Assets には、アセット共有ページのカスタマイズに使用できる、事前定義済みの一連の述語が付属しています。この方法でアセット共有をカスタマイズする方法については、[アセット共有ページの作成と設定](assets-finder-editor.md#creating-and-configuring-an-asset-share-page)で説明しています。

[!DNL Experience Manager] デベロッパーは、既存の述語を使用するだけでなく、[Query Builder API](/help/sites-developing/querybuilder-api.md) を使用して独自の述語を作成することもできます。

カスタム述語を作成するには、[ウィジェットフレームワーク](https://helpx.adobe.com/jp/experience-manager/6-4/sites/developing/using/reference-materials/widgets-api/index.html)に関する基本的な知識が必要です。

ベストプラクティスは、既存の述語をコピー後に変更することです。サンプルの述語は、 `/libs/cq/search/components/predicates`.

### 例：単純なプロパティ述語の作成 {#example-build-a-simple-property-predicate}

プロパティの述語を作成するには：

1. プロジェクトディレクトリにコンポーネントフォルダーを作成します。例： `/apps/geometrixx/components/titlepredicate`.
1. 追加 `content.xml`:

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:sling="https://sling.apache.org/jcr/sling/1.0"
    xmlns:cq="https://www.day.com/jcr/cq/1.0"
    xmlns:jcr="https://www.jcp.org/jcr/1.0"
       jcr:primaryType="cq:Component"
       jcr:title="Title Predicate"
       sling:resourceSuperType="foundation/components/parbase"
       allowedParents="[*/parsys]"
       componentGroup="Search"/>
   ```

1. 次の `titlepredicate.jsp`.を追加します。

   ```xml
   <%--
     Sample title predicate component
   
   --%><%@ page import="java.util.Calendar" %><%
   %><%@include file="/libs/foundation/global.jsp"%><%
   
       // A unique id is necessary in case this predicate is inserted multiple times on the same page
       String elemId = "cq-predicate-" +  Long.toString(Calendar.getInstance().getTimeInMillis());
   
   %><div class="predicatebox">
   
       <div class="title">Title</div>
   
       <%-- The wrapper for the form elements. All items will be append to this wrapper. --%>
       <div id="<%= elemId %>" class="content"></div>
   
   </div><script type="text/javascript">
   
       CQ.Ext.onLoad(function() {
   
           var predicateName = "property";
           var propertyName = "jcr:content/metadata/dc:title";
           var elemId = "<%= elemId %>";
   
           // Get the page wide available QueryBuilder.
           var qb = CQ.search.Util.getQueryBuilder();
   
           // createId adds a counter to the predicate name - useful in case this predicate
           // is inserted multiple times on the same page.
           var id = qb.createId(predicateName);
   
           // Hidden field that defines the property to search for; in our case this
           // is the "dc:title" metadata. The name "property" (or "1_property", "2_property" etc.)
           // indicates the server to use the property predicate
           // (com.day.cq.search.eval.JcrPropertyPredicateEvaluator).
           qb.addField({
               "xtype": "hidden",
               "renderTo": elemId,
               "name": id,
               "value": propertyName
           });
   
           // The visible text field. The name has to be like the one of the hidden field above
           // plus the ".value" suffix.
           qb.addField({
               "xtype": "textfield",
               "renderTo": elemId,
               "name": id + ".value"
           });
   
           // Depending on the predicate additional parameters allow to configure the
           // predicate. Here we add an operation parameter to create a "like" query.
           // Again note the name set to the id and a suffix.
           qb.addField({
               "xtype": "hidden",
               "renderTo": elemId,
               "name": id + ".operation",
               "value": "like"
           });
   
       });
   
   </script>
   ```

1. コンポーネントを使用できるようにするには、コンポーネントを編集可能にする必要があります。コンポーネントを編集可能にするには、CRXDE で、ノードを追加します `cq:editConfig` プライマリタイプ `cq:EditConfig`. 段落を削除できるよう、値を複数設定できるプロパティ `cq:actions` を追加し、値として **DELETE** のみを設定します。
1. ブラウザー、およびサンプルページ ( 例： `press.html`) デザインモードに切り替えて、述語段落システム用の新しいコンポーネントを有効にします ( 例： **left**) をクリックします。

1. **編集**&#x200B;モードでは、新しいコンポーネントがサイドキックで使用できるようになります（**検索**&#x200B;グループ内）。コンポーネントを **述語** 列に検索語を入力し、例えば、 **ひし形** 拡大鏡をクリックして検索を開始します。

   >[!NOTE]
   >
   >検索時は、大文字と小文字を含め、語句を正確に入力してください。

### 例：単純なグループ述語の構築 {#example-build-a-simple-group-predicate}

グループ述語を作成するには：

1. プロジェクトディレクトリにコンポーネントフォルダーを作成します。例： `/apps/geometrixx/components/picspredicate`.
1. 追加 `content.xml`:

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:sling="https://sling.apache.org/jcr/sling/1.0"
    xmlns:cq="https://www.day.com/jcr/cq/1.0"
    xmlns:jcr="https://www.jcp.org/jcr/1.0"
       jcr:primaryType="cq:Component"
       jcr:title="Image Formats"
       sling:resourceSuperType="foundation/components/parbase"
       allowedParents="[*/parsys]"
       componentGroup="Search"/>
   ```

1. 追加 `titlepredicate.jsp`:

   ```java
   <%--
   
     Sample group predicate component
   
   --%><%@ page import="java.util.Calendar" %><%
   %><%@include file="/libs/foundation/global.jsp"%><%
   
       // A unique id is necessary in case this predicate is inserted multiple times on the same page.
       String elemId = "cq-predicate-" +  Long.toString(Calendar.getInstance().getTimeInMillis());
   
   %><div class="predicatebox">
   
       <div class="title">Image Formats</div>
   
       <%-- The wrapper for the form elements. All items will be append to this wrapper. --%>
       <div id="<%= elemId %>" class="content"></div>
   
   </div><script type="text/javascript">
   
       CQ.Ext.onLoad(function() {
   
           var predicateName = "property";
           var propertyName = "jcr:content/metadata/dc:format";
           var elemId = "<%= elemId %>";
   
           // Get the page wide available QueryBuilder.
           var qb = CQ.search.Util.getQueryBuilder();
   
           // Create a unique group ID; will return e.g. "1_group".
           var groupId = qb.createGroupId();
   
           // Hidden field that defines the property to search for  - in our case "dc:format" -
           // and declares the group of predicates. "property" in the name ("1_group.property")
           // indicates to the server to use the "property predicate"
           // (com.day.cq.search.eval.JcrPropertyPredicateEvaluator).
           qb.addField({
               "xtype": "hidden",
               "renderTo": "<%= elemId %>",
               "name": groupId + "." + predicateName, // 1_group.property
               "value": propertyName
           });
   
           // Declare to combine the multiple values using OR.
           qb.add(new CQ.Ext.form.Hidden({
               "name": groupId + ".p.or",  // 1_group.p.or
               "value": "true"
           }));
   
           // The options
           var options = [
               { "label":"JPEG", "value":"image/jpeg"},
               { "label":"PNG",  "value":"image/png" },
               { "label":"GIF",  "value":"image/gif" }
           ];
   
           // Build a checkbox for each option.
           for (var i = 0; i < options.length; i++) {
               qb.addField({
                   "xtype": "checkbox",
                   "renderTo": "<%= elemId %>",
                   // 1_group.property.0_value, 1_group.property.1_value etc.
                   "name": groupId + "." +  predicateName + "." + i + "_value",
                   "inputValue": options[i].value,
                   "boxLabel": options[i].label,
                   "listeners": {
                       "check": function() {
                           // Submit the search form when checking/unchecking a checkbox.
                           qb.submit();
                       }
                   }
               });
           }
   
       });
   ```

1. コンポーネントを使用できるようにするには、コンポーネントを編集可能にする必要があります。コンポーネントを編集可能にするには、CRXDE で、ノードを追加します `cq:editConfig` プライマリタイプ `cq:EditConfig`. 段落を削除できるよう、値を複数設定できるプロパティ `cq:actions` を追加し、値として `DELETE` のみを設定します。
1. ブラウザー、およびサンプルページ ( 例： `press.html`) デザインモードに切り替えて、述語段落システム用の新しいコンポーネントを有効にします ( 例： **left**) をクリックします。
1. **編集**&#x200B;モードでは、新しいコンポーネントがサイドキックで使用できるようになります（**検索**&#x200B;グループ内）。「**Predicates**」列にコンポーネントを挿入します。

### インストール済みの述語ウィジェット {#installed-predicate-widgets}

事前設定済みの ExtJS ウィジェットとして、次の述語を使用できます。

### FulltextPredicate {#fulltextpredicate}

| プロパティ | 型 | 説明 |
|---|---|---|
| predicateName | String | 述語の名前。 デフォルトは `fulltext` |
| searchCallback | 関数 | イベント `keyup` で検索をトリガーするためのコールバック。デフォルトは `CQ.wcm.SiteAdmin.doSearch` |

### PropertyPredicate {#propertypredicate}

| プロパティ | 型 | 説明 |
|---|---|---|
| predicateName | String | 述語の名前。 デフォルトは `property` |
| propertyName | String | JCR プロパティの名前。 デフォルトは `jcr:title` |
| defaultValue | String | 事前入力されたデフォルト値。 |

### PathPredicate {#pathpredicate}

| プロパティ | 型 | 説明 |
|---|---|---|
| predicateName | String | 述語の名前。 デフォルトは `path` |
| rootPath | String | 述語のルートパス。 デフォルトは `/content/dam` |
| pathFieldPredicateName | String | デフォルトは `folder` |
| showFlatOption | Boolean | チェックボックス `search in subfolders` を表示するフラグ。デフォルトは true です。 |

### DatePredicate {#datepredicate}

| プロパティ | 型 | 説明 |
|---|---|---|
| predicateName | String | 述語の名前。 デフォルトは `daterange` |
| propertyname | String | JCR プロパティの名前。 デフォルトは `jcr:content/jcr:lastModified` |
| defaultValue | String | 事前入力されたデフォルト値 |

### OptionsPredicate {#optionspredicate}

| プロパティ | 型 | 説明 |
|---|---|---|
| title | String | トップタイトルを追加します |
| predicateName | String | 述語の名前。 デフォルトは `daterange` |
| propertyname | String | JCR プロパティの名前。 デフォルトは `jcr:content/metadata/cq:tags` |
| 折りたたみ | String | 折りたたみのレベル。 デフォルトは `level1` |
| triggerSearch | Boolean | チェック時に検索をトリガーするフラグ。 デフォルトは false です。 |
| searchCallback | 関数 | 検索をトリガーするコールバック。 デフォルトは `CQ.wcm.SiteAdmin.doSearch` |
| searchTimeoutTime | Number | searchCallback が実行される前のタイムアウト。 デフォルトは 800 ms です。 |

## 検索結果のカスタマイズ {#customizing-search-results}

アセット共有ページでの検索結果の表示方法は、選択したレンズによって制御されます。[!DNL Experience Manager] Assets には、アセット共有ページのカスタマイズに使用できる、事前定義済みのレンズのセットが付属しています。 この方法でアセット共有をカスタマイズする方法については、[アセット共有ページの作成と設定](assets-finder-editor.md#creating-and-configuring-an-asset-share-page)で説明しています。

[!DNL Experience Manager] 開発者は、既存のレンズを使用するだけでなく、独自のレンズを作成することもできます。
