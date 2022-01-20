---
title: 検索
seo-title: Search
description: AEM のオーサー環境は、リソースタイプに応じて、コンテンツを検索するための様々なメカニズムを提供します。
seo-description: The author environment of AEM provides various mechanisms for searching for content, dependent on the resource type.
uuid: b50c8144-1993-441d-8303-fcb6b0f24376
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: introduction
content-type: reference
discoiquuid: b20e0f78-9ae4-47ba-8e9a-452a0a78b663
exl-id: 9c1d8969-6aa6-41b9-a797-3e6431475fc6
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '470'
ht-degree: 87%

---

# 検索{#search-features}

AEM のオーサー環境は、リソースタイプに応じて、コンテンツを検索するための様々なメカニズムを提供します。

>[!NOTE]
>
>オーサー環境外では、[Query Builder](/help/sites-developing/querybuilder-api.md) や [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md) など、他の検索メカニズムも使用できます。

## 検索の基本 {#search-basics}

検索パネルにアクセスするには、該当するコンソールの左側のパネルの上部にある「**検索**」タブをクリックします。

![chlimage_1-140](assets/chlimage_1-140.png)

検索パネルを使用すると、Web サイトのすべてのページに対して検索を実行できます。次のフィールドとウィジェットが含まれます。

* **フルテキスト**：指定したテキストを検索します。
* **前後に変更**：特定の日付の期間に変更されたページのみを検索します。
* **テンプレート**：指定したテンプレートに基づいたページのみを検索します。
* **タグ**：指定したタグを持つページのみを検索します。

>[!NOTE]
>
>インスタンスが [Lucene 検索](/help/sites-deploying/queries-and-indexing.md)用に設定されていると、次を&#x200B;**フルテキスト**&#x200B;で使用できます。
>
>* [ワイルドカード](https://lucene.apache.org/core/5_3_1/queryparser/org/apache/lucene/queryparser/classic/package-summary.html#Wildcard_Searches)
>* [ブール演算子](https://lucene.apache.org/core/5_3_1/queryparser/org/apache/lucene/queryparser/classic/package-summary.html#Boolean_operators)
>
>* [正規表現](https://lucene.apache.org/core/5_3_1/queryparser/org/apache/lucene/queryparser/classic/package-summary.html#Regexp_Searches)
>* [フィールドグループ](https://lucene.apache.org/core/5_3_1/queryparser/org/apache/lucene/queryparser/classic/package-summary.html#Field_Grouping)
>* [ブースト](https://lucene.apache.org/core/5_3_1/queryparser/org/apache/lucene/queryparser/classic/package-summary.html#Boosting_a_Term)

>


検索を実行するには、ペイン下部にある「**検索**」をクリックします。検索基準を消去するには、「**リセット**」をクリックします。

## フィルター {#filter}

様々な場所でフィルターを設定（およびクリア）してビューのドリルダウンおよび洗練をおこなうことができます。

![chlimage_1-141](assets/chlimage_1-141.png)

## 検索および置換 {#find-and-replace}

**Web サイト**&#x200B;コンソールの「**検索と置換**」メニューオプションでは、Web サイトの特定のセクション内で特定の文字列を持つ複数のインスタンスを検索して置換できます。

1. 検索と置換操作を実行するルートページまたはフォルダーを選択します。
1. **ツール**／**検索と置換**&#x200B;を選択します。

   ![screen_shot_2012-02-15at120346pm](assets/screen_shot_2012-02-15at120346pm.png)

1. **検索と置換**&#x200B;ダイアログでは、次の操作を実行できます。

   * 検索操作を開始するルートパスを確認します。
   * 検索する語句を指定します。
   * 置換後の語句を指定します。
   * 検索で大文字と小文字を区別するかどうかを指定します。
   * 完全に一致する語句のみを検索するかどうかを指定します（指定しなければ、サブ文字列も検索されます）。

   クリック **プレビュー** に、語句が見つかった場所を示します。置き換える特定のインスタンスを選択またはクリアできます。

   ![screen_shot_2012-02-15at120719pm](assets/screen_shot_2012-02-15at120719pm.png)

1. 「**置換**」をクリックすると、すべてのインスタンスが置換されます。この操作の確認が求められます。

検索と置換サーブレットのデフォルトのスコープには、以下のプロパティが含まれます。

* `jcr:title`
* `jcr:description`
* `jcr:text`
* `text`

スコープは、Apache Felix Web Management Console( 例： `http://localhost:4502/system/console/configMgr`) をクリックします。 選択 `CQ WCM Find Replace Servlet (com.day.cq.wcm.core.impl.servlets.FindReplaceServlet)` 必要に応じて、範囲を設定します。

>[!NOTE]
>
>標準の AEM インストールでは、検索と置換の検索機能に Lucene が使用されます。
>
>Lucene では長さが 16 K までの文字列プロパティにインデックスが作成されます。この長さを超える文字列は検索されません。
