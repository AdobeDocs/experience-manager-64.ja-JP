---
title: ContextHub の拡張
seo-title: Extending ContextHub
description: 提供される ContextHub ストアやモジュールがソリューションの要件を満たさない場合は、新しいタイプの ContextHub ストアやモジュールを定義する
seo-description: Define new types of ContextHub stores and modules when the ones provided do not meet your solution requirements
uuid: 1d80c01d-ec5d-4e76-849d-bec0e1c3941a
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: personalization
content-type: reference
discoiquuid: 13a908ae-6965-4438-96d0-93516b500884
exl-id: 15b17bed-3422-43cf-b1af-91d9e0c5dfcb
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '686'
ht-degree: 74%

---

# ContextHub の拡張{#extending-contexthub}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

提供される ContextHub ストアやモジュールがソリューションの要件を満たさない場合は、新しいタイプの ContextHub ストアやモジュールを定義します。

## カスタムストア候補の作成 {#creating-custom-store-candidates}

ContextHub ストアは、登録されたストア候補から作成されます。 カスタムストアを作成するには、ストア候補を作成して登録する必要があります。

ストア候補を作成して登録するコードを含む JavaScript ファイルは、 [クライアントライブラリフォルダー](/help/sites-developing/clientlibs.md#creating-client-library-folders). フォルダーのカテゴリは、次のパターンに一致しなければなりません。

```xml
contexthub.store.[storeType]
```

カテゴリの `[storeType]` 部分は、ストア候補と一緒に登録されている `storeType` です（「[ContextHub ストア候補の登録](/help/sites-developing/ch-extend.md#registering-a-contexthub-store-candidate)」を参照）。例えば、storeType が `contexthub.mystore` の場合、クライアントライブラリフォルダーのカテゴリは `contexthub.store.contexthub.mystore` でなければなりません。

### ContextHub ストア候補の作成 {#creating-a-contexthub-store-candidate}

ストア候補を作成するには、[`ContextHub.Utils.inheritance.inherit`](/help/sites-developing/contexthub-api.md#inherit-child-parent) 関数を使用して、次のいずれかのベースストアを拡張します。

* [`ContextHub.Store.PersistedStore`](/help/sites-developing/contexthub-api.md#contexthub-store-persistedstore)
* [`ContextHub.Store.SessionStore`](/help/sites-developing/contexthub-api.md#contexthub-store-sessionstore)
* [`ContextHub.Store.JSONPStore`](/help/sites-developing/contexthub-api.md#contexthub-store-jsonpstore)
* [`ContextHub.Store.PersistedJSONPStore`](/help/sites-developing/contexthub-api.md#contexthub-store-persistedjsonpstore)

各ベースストアは、[`ContextHub.Store.Core`](/help/sites-developing/contexthub-api.md#contexthub-store-core) ストアを拡張したものです。

次の例では、`ContextHub.Store.PersistedStore` ストア候補の最もシンプルな拡張を作成しています。

```
myStoreCandidate = function(){};
ContextHub.Utils.inheritance.inherit(myStoreCandidate,ContextHub.Store.PersistedStore);
```

実際には、カスタムストア候補は追加の関数を定義するか、ストアの初期設定を上書きします。いくつかの[サンプルストア候補](/help/sites-developing/ch-samplestores.md)が、`/libs/granite/contexthub/components/stores` の下にあるリポジトリにインストールされています。これらのサンプルから学ぶには、CRXDE Liteを使用して JavaScript ファイルを開きます。

### ContextHub ストア候補の登録 {#registering-a-contexthub-store-candidate}

ストア候補を登録して ContextHub フレームワークに統合し、ストア候補からストアを作成できるようにします。ストア候補を登録するには、[`registerStoreCandidate`](/help/sites-developing/contexthub-api.md#registerstorecandidate-store-storetype-priority-applies) クラスの `ContextHub.Utils.storeCandidates` 関数を使用します。

ストア候補を登録する際に、ストアタイプの名前を指定します。候補からストアを作成するときは、ストアタイプを使用してベースとする候補を識別します。

ストア候補を登録する際に、優先度を指定します。既に登録済みのストア候補と同じストアタイプを使用してストア候補を登録した場合、優先度の高い候補が使用されます。そのため、新しいストア候補を既存のストア候補に優先させることができます。

```
ContextHub.Utils.storeCandidates.registerStoreCandidate(myStoreCandidate,
                                'contexthub.mystorecandidate', 0);
```

ほとんどの場合、1 つの候補のみが必要で優先度を `0` に設定できますが、[より高度な登録](/help/sites-developing/contexthub-api.md#registerstorecandidate-store-storetype-priority-applies)について学ぶことができます。これにより、少数のストア実装のうちの 1 つを javascript 条件（`applies`）と優先度の候補に基づいて選択できます。

## ContextHub UI モジュールタイプの作成 {#creating-contexthub-ui-module-types}

[ContextHub に付属してインストールされる](/help/sites-developing/ch-samplemodules.md) UI モジュールタイプが要件を満たさない場合は、カスタム UI モジュールタイプを作成できます。UI モジュールタイプを作成するには、`ContextHub.UI.BaseModuleRenderer` クラスを拡張して `ContextHub.UI` に登録し、新しい UI モジュールレンダラーを作成します。

UI モジュールレンダラーを作成するには、UI モジュールをレンダリングするロジックを格納している `Class` オブジェクトを作成します。少なくとも、このクラスは次のアクションを実行する必要があります。

* `ContextHub.UI.BaseModuleRenderer` クラスを拡張します。このクラスは、すべての UI モジュールレンダラーのベースとなる実装です。`Class` オブジェクトは、このクラスが拡張されていることを示すために使用する `extend` というプロパティを定義します。

* デフォルトの設定を指定します。`defaultConfig` プロパティを作成します。このプロパティは、[`contexthub.base`](/help/sites-developing/ch-samplemodules.md#contexthub-base-ui-module-type) UI モジュール用に定義されているプロパティと、必要なその他すべてのプロパティを含むオブジェクトです。

`ContextHub.UI.BaseModuleRenderer` のソースは、/libs/granite/contexthub/code/ui/container/js/ContextHub.UI.BaseModuleRenderer.js にあります。レンダラーを登録するには、[`registerRenderer`](/help/sites-developing/contexthub-api.md#registerrenderer-moduletype-renderer-dontrender) クラスの `ContextHub.UI` メソッドを使用します。モジュールタイプの名前を指定する必要があります。 管理者がこのレンダラーに基づいて UI モジュールを作成する場合は、この名前を指定します。

レンダラークラスを作成し、自己実行する匿名関数に登録します。 次の例は、contexthub.browserinfo UI モジュールのソースコードをベースとしています。 この UI モジュールは、`ContextHub.UI.BaseModuleRenderer` クラスのシンプルな拡張です。

```xml
;(function() {

    var SurferinfoRenderer = new Class({
        extend: ContextHub.UI.BaseModuleRenderer,

        defaultConfig: {
            icon: 'coral-Icon--globe',
            title: 'Browser/OS Information',

            storeMapping: {
                surferinfo: 'surferinfo'
            },

            template:
                '<p>{{surferinfo.browser.family}} {{surferinfo.browser.version}}</p>' +
                '<p>{{surferinfo.os.name}} {{surferinfo.os.version}}</p>'
        }
    });

    ContextHub.UI.registerRenderer('contexthub.browserinfo', new SurferinfoRenderer());

}());
```

レンダラーを作成して登録するコードを含む JavaScript ファイルは、[クライアントライブラリフォルダー](/help/sites-developing/clientlibs.md#creating-client-library-folders)に含める必要があります。フォルダーのカテゴリは、次のパターンに一致しなければなりません。

```xml
contexthub.module.[moduleType]
```

カテゴリの `[moduleType]` 部分は、モジュールレンダラーの登録に使用されている `moduleType` です。例えば、`moduleType` が `contexthub.browserinfo` の場合、クライアントライブラリフォルダーのカテゴリは `contexthub.module.contexthub.browserinfo` でなければなりません。
