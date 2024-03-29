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
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '506'
ht-degree: 48%

---

# 検索 {#search-features}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

AEM のオーサー環境は、リソースタイプに応じて、コンテンツを検索するための様々なメカニズムを提供します。

>[!NOTE]
>
>オーサー環境の外部では、検索用のメカニズム ( [Query Builder](/help/sites-developing/querybuilder-api.md) および [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md).

## 検索の基本 {#search-basics}

検索パネルにアクセスするには、該当するコンソールの左側のパネルの上部にある「**検索**」タブをクリックします。

![chlimage_1-140](assets/chlimage_1-140.png)

検索パネルを使用すると、すべての web サイトページにわたって検索できます。次のフィールドとウィジェットが含まれます。

* **Fulltext**:指定したテキストを検索
* **前後に変更**:特定の日付の間に変更されたページのみを検索します
* **テンプレート**:指定したテンプレートに基づくページのみを検索
* **タグ**:指定したタグを持つページのみを検索

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


「 **検索** をクリックします。 クリック **リセット** をクリックして、検索条件をクリアします。

## フィルター {#filter}

様々な場所でフィルターを設定（およびクリア）して、表示をドリルダウンして絞り込むことができます。

![chlimage_1-141](assets/chlimage_1-141.png)

## 検索と置換 {#find-and-replace}

内 **Web サイト** コンソールを **検索と置換** メニューオプションを使用すると、web サイトの特定のセクション内で、1 つの文字列を複数インスタンスで検索および置換できます。

1. 検索および置換アクションを実行するルートページまたはフォルダーを選択します。
1. 選択 **ツール** その後 **検索と置換**:

   ![screen_shot_2012-02-15at120346pm](assets/screen_shot_2012-02-15at120346pm.png)

1. この **検索と置換** ダイアログでは次の操作を実行します。

   * 検索アクションを開始するルートパスを確認します。
   * 見つかる用語を定義します
   * 置き換える用語を定義します。
   * 検索で大文字と小文字を区別する必要があるかどうかを示します
   * 単語全体のみを検出するかどうかを示します（それ以外の場合は、部分文字列も検索されます）。

   「**プレビュー**」リストをクリックすると、語句が見つかった場所が表示されます。特定のインスタンスを選択／選択解除して置換できます。

   ![screen_shot_2012-02-15at120719pm](assets/screen_shot_2012-02-15at120719pm.png)

1. クリック **置換** すべてのインスタンスを実際に置き換える この操作の確認が求められます。

検索と置換のサーブレットのデフォルトスコープには、次のプロパティが含まれています。

* `jcr:title`
* `jcr:description`
* `jcr:text`
* `text`

このスコープは、Apache Felix Web Management Console（例：`http://localhost:4502/system/console/configMgr`）を使用して変更できます。`CQ WCM Find Replace Servlet (com.day.cq.wcm.core.impl.servlets.FindReplaceServlet)` を選択し、必要に応じてスコープを設定します。

>[!NOTE]
>
>標準のAEMインストールでは、検索と置換は Lucene を検索機能に使用します。
>
>Lucene は最大 16 k の文字列プロパティのインデックスを作成します。 これを超える文字列は検索されません。
