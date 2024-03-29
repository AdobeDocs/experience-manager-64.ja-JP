---
title: イベント追跡の拡張
seo-title: Extending Event Tracking
description: AEM Analytics を使用すると、Web サイトでのユーザーのインタラクションを追跡できます
seo-description: AEM Analytics allows you to track user interaction on your website
uuid: 722798ac-4043-4918-a6df-9eda2c85020b
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: e0372f4a-fe7b-4526-8391-5bb345b51d70
exl-id: 8df6b48f-b1a8-4294-a52e-dc17ab65606c
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '523'
ht-degree: 70%

---

# イベント追跡の拡張{#extending-event-tracking}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

AEM Analytics を使用すると、Web サイトでのユーザーのインタラクションを追跡できます。 開発者は、次の作業が必要になる場合があります。

* 訪問者がコンポーネントとどのようにやり取りしているかを追跡します。 これを行うには、[カスタムイベント](#custom-events)を使用します。
* [ContextHub の値へのアクセス](/help/sites-developing/extending-analytics.md#accessing-values-in-the-contexthub)。
* [レコードのコールバックの追加](#adding-record-callbacks)。

>[!NOTE]
>
>この情報は基本的には全体に適用されますが、一部の例では [Adobe Analytics](/help/sites-administering/adobeanalytics.md) が使用されています。
>
>コンポーネントとダイアログボックスの開発に関する一般的な情報については、[コンポーネントの開発](/help/sites-developing/components.md)を参照してください。

## カスタムイベント {#custom-events}

カスタムイベントは、ページ上の特定のコンポーネントの可用性に依存するあらゆるものを追跡します。 また、ページコンポーネントは別のコンポーネントとして扱われるので、テンプレートに固有のイベントも含まれます。

### ページ読み込み時のカスタムイベントの追跡 {#tracking-custom-events-on-page-load}

これを行うには、疑似属性 `data-tracking`（下位互換性のために、古いレコード属性がまだサポートされています）を使用します。これは任意の HTML タグに追加できます。

`data-tracking` の構文は次のとおりです。

* `data-tracking="{'event': ['eventName'], 'values': {'key': 'value', 'nextKey': 'nextValue'}, componentPath: 'myapp/component/mycomponent'}"`

2 番目のパラメーターとして、任意の数のキーと値のペアを渡すことができます。これをペイロードと呼びます。

次に例を示します。

```xml
<span data-tracking="{event:'blogEntryView', 
                                values:{
                                   'blogEntryContentType': 'blog', 
                                   'blogEntryUniqueID': '<%= xssAPI.encodeForJSString(entry.getId()) %>',
                                   'blogEntryTitle': '<%= xssAPI.encodeForJSString(entry.getTitle()) %>',
                                   'blogEntryAuthor':'<%= xssAPI.encodeForJSString(entry.getAuthor()) %>',
                                   'blogEntryPageLanguage':'<%= currentPage.getLanguage(true) %>'
                                },
                                componentPath:'myapp/component/mycomponent'}">
</span>
```

ページの読み込み時に、すべての `data-tracking` 属性が収集されて ContextHub のイベントストアに追加され、Adobe Analytics イベントにマッピングできるようになります。マッピングされないイベントは Adobe Analytics では追跡されません。マッピングイベントについて詳しくは、[Adobe Analytics への接続](/help/sites-administering/adobeanalytics.md)を参照してください。

### ページの読み込み後のカスタムイベントの追跡 {#tracking-custom-events-after-page-load}

ページの読み込み後に発生するイベント（ユーザーインタラクションなど）を追跡するには、JavaScript 関数 `CQ_Analytics.record` を使用します。

* `CQ_Analytics.record({event: 'eventName', values: { valueName: 'VALUE' }, collect: false, options: { obj: this, defaultLinkType: 'X' }, componentPath: '<%=resource.getResourceType()%>'})`

ここで、

* `events`：文字列、または文字列の配列（イベントが複数の場合）。

* `values`：追跡するすべての値を格納します。
* `collect`：オプションで、イベントおよびデータオブジェクトを格納する配列を返します。
* `options`：オプションであり、HTML 要素 `obj` および ` [defaultLinkType](https://microsite.omniture.com/t2/help/en_US/sc/implement/index.html#linkType)` などのリンク追跡オプションが含まれます。

* `componentPath`：必須の属性。`<%=resource.getResourceType()%>` に設定することを推奨します。

例えば、次のように定義した場合、「**Jump to top**」リンクをクリックすると `jumptop` と `headlineclick` の 2 つのイベントが実行されます。

```xml
<h1 data-tracking="{event: 'headline', values: {level:'1'}, componentPath: '<%=resource.getResourceType()%>'}">
  My Headline <a href="#" onclick="CQ_Analytics.record({event: ['jumptop','headlineclick'],  values: {level:'1'}, componentPath: '<%=resource.getResourceType()%>'})">Jump to top</a>
</h1>
```

## ContextHub の値へのアクセス {#accessing-values-in-the-contexthub}

ContextHub JavaScript API には、指定したストアを返す `getStore(name)` 関数があります（使用可能な場合）。このストアには、指定したキーの値を返す `getItem(key)` 関数があります（使用可能な場合）。`getKeys()` 関数を使用すると、特定のストアに対して定義されたキーの配列を取得できます。

`ContextHub.getStore(name).eventing.on(ContextHub.Constants.EVENT_STORE_UPDATED, handler, selector, triggerForPastEvents)` 関数を使用して関数をバインドすると、ストアの値が変更されたことを知らせる通知を受けることができます。

ContextHub の利用開始の通知を受けるには、`ContextHub.eventing.on(ContextHub.Constants.EVENT_ALL_STORES_READY, handler, selector, triggerForPastEvents);` 関数を使用するのが最適です。

**ContextHub のその他のイベント：**

すべてのストアに対応：

`ContextHub.eventing.on(ContextHub.Constants.EVENT_ALL_STORES_READY, handler, selector, triggerForPastEvents);`

ストア固有：

`ContextHub.getStore(store).eventing.on(ContextHub.Constants.EVENT_STORE_READY, handler, selector, triggerForPastEvents)`

>[!NOTE]
>
>完全な [ContextHub API リファレンス](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/contexthub-api.html#ContextHubJavascriptAPIReference)も参照してください

## レコードコールバックの追加 {#adding-record-callbacks}

関数 `CQ_Analytics.registerBeforeCallback(callback,rank)` と `CQ_Analytics.registerAfterCallback(callback,rank)` を使用して、before コールバックと after コールバックを登録します。

両方の関数は、最初の引数として関数を取り、2 番目の引数としてランクを取ります。この関数は、コールバックの実行順序を示します。

コールバックが false を返した場合、実行チェーン内の以降のコールバックは実行されません。
