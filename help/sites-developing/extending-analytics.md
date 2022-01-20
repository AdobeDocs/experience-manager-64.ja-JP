---
title: イベント追跡の拡張
seo-title: Extending Event Tracking
description: AEM Analytics では、Web サイトでのユーザーインタラクションを追跡できます
seo-description: AEM Analytics allows you to track user interaction on your website
uuid: 722798ac-4043-4918-a6df-9eda2c85020b
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: e0372f4a-fe7b-4526-8391-5bb345b51d70
exl-id: 8df6b48f-b1a8-4294-a52e-dc17ab65606c
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '487'
ht-degree: 47%

---

# イベント追跡の拡張{#extending-event-tracking}

AEM Analytics では、Web サイトでのユーザーインタラクションを追跡できます。開発者は次の作業が必要になる場合があります。

* 訪問者がコンポーネントとどのようなやり取りをおこなっているかの追跡。これは、 [カスタムイベント。](#custom-events)
* [ContextHub の値へのアクセス](/help/sites-developing/extending-analytics.md#accessing-values-in-the-contexthub).
* [レコードのコールバックの追加](#adding-record-callbacks)。

>[!NOTE]
>
>この情報は基本的に汎用的ですが、 [Adobe Analytics](/help/sites-administering/adobeanalytics.md) を参照してください。
>
>コンポーネントとダイアログボックスの開発に関する一般的な情報については、[コンポーネントの開発](/help/sites-developing/components.md)を参照してください。

## カスタムイベント {#custom-events}

カスタムイベントはページ内の特定のコンポーネントの可用性に依存する要素を追跡します。これにはテンプレート特有のイベントも含まれます。ページコンポーネントは別のコンポーネントとして扱われています。

### ページの読み込み時のカスタムイベントの追跡 {#tracking-custom-events-on-page-load}

これは、疑似属性 `data-tracking` （古いレコード属性は、後方互換性のために引き続きサポートされます）。 これは任意の HTML タグに追加できます。

の構文 `data-tracking` が

* `data-tracking="{'event': ['eventName'], 'values': {'key': 'value', 'nextKey': 'nextValue'}, componentPath: 'myapp/component/mycomponent'}"`

2 番目のパラメーターとして、任意の数のキーと値のペアを渡すことができます。これはペイロードと呼ばれます。

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

ページの読み込み時、すべて `data-tracking` 属性が収集されて、ContextHub のイベントストアに追加されます。このストアでは、Adobe Analyticsイベントにマッピングできます。 マッピングされていないイベントは、Adobe Analyticsでは追跡されません。 詳しくは、 [Adobe Analyticsへの接続](/help/sites-administering/adobeanalytics.md) イベントのマッピングの詳細については、を参照してください。

### ページの読み込み後のカスタムイベントの追跡 {#tracking-custom-events-after-page-load}

ページの読み込み後に発生するイベント（ユーザーインタラクションなど）を追跡するには、JavaScript 関数 `CQ_Analytics.record` を使用します。

* `CQ_Analytics.record({event: 'eventName', values: { valueName: 'VALUE' }, collect: false, options: { obj: this, defaultLinkType: 'X' }, componentPath: '<%=resource.getResourceType()%>'})`

ここで、

* `events`：文字列、または文字列の配列（イベントが複数の場合）。

* `values`：追跡するすべての値を格納します。
* `collect`：オプションで、イベントおよびデータオブジェクトを格納する配列を返します。
* `options` はオプションで、HTML要素などのリンクトラッキングオプションが含まれます。 `obj` および ` [defaultLinkType](https://microsite.omniture.com/t2/help/en_US/sc/implement/index.html#linkType)`.

* `componentPath` は必要な属性で、 `<%=resource.getResourceType()%>`

例えば、次のように定義した場合、「**Jump to top**」リンクをクリックすると `jumptop` と `headlineclick` の 2 つのイベントが実行されます。

```xml
<h1 data-tracking="{event: 'headline', values: {level:'1'}, componentPath: '<%=resource.getResourceType()%>'}">
  My Headline <a href="#" onclick="CQ_Analytics.record({event: ['jumptop','headlineclick'],  values: {level:'1'}, componentPath: '<%=resource.getResourceType()%>'})">Jump to top</a>
</h1>
```

## ContextHub の値へのアクセス {#accessing-values-in-the-contexthub}

ContextHub JavaScript API には、 `getStore(name)` 関数で指定したストアを返します（使用可能な場合）。 この店には `getItem(key)` 指定したキーの値を返す関数（使用可能な場合）。 の使用 `getKeys()` 関数は、特定のストアに対して定義されたキーの配列を取得できます。

関数をバインドすると、 `ContextHub.getStore(name).eventing.on(ContextHub.Constants.EVENT_STORE_UPDATED, handler, selector, triggerForPastEvents)` 関数に置き換えます。

ContextHub が初期状態であることを通知する最善の方法は、 `ContextHub.eventing.on(ContextHub.Constants.EVENT_ALL_STORES_READY, handler, selector, triggerForPastEvents);` 関数に置き換えます。

**ContextHub の追加イベント：**

すべてのストアに対応：

`ContextHub.eventing.on(ContextHub.Constants.EVENT_ALL_STORES_READY, handler, selector, triggerForPastEvents);`

ストア固有：

`ContextHub.getStore(store).eventing.on(ContextHub.Constants.EVENT_STORE_READY, handler, selector, triggerForPastEvents)`

>[!NOTE]
>
>また、 [ContextHub API リファレンス](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/contexthub-api.html#ContextHubJavascriptAPIReference)

## レコードコールバックの追加 {#adding-record-callbacks}

関数を使用してコールバックを登録する前と後 `CQ_Analytics.registerBeforeCallback(callback,rank)` および `CQ_Analytics.registerAfterCallback(callback,rank)`.

どちらの関数も、先頭の引数では関数を、2 番目の引数ではランクを受け取ります。このランクによって、コールバックの実行順序が決定されます。

コールバックが false を返す場合、実行チェーンの後続のコールバックは実行されません。
