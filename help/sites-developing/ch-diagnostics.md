---
title: ContextHub の診断
seo-title: ContextHub の診断
description: ContextHub には、ContextHub フレームワークの概要を確認できる診断ページがあります
seo-description: ContextHub には、ContextHub フレームワークの概要を確認できる診断ページがあります
uuid: 94ef0696-3977-4781-ad32-9f4f117eb096
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: personalization
content-type: reference
discoiquuid: 6aa88583-5d34-4f77-a932-d47d84785eca
translation-type: tm+mt
source-git-commit: 39b6af8ee815e8f6fa6e0b4a0a6dc80f29165243
workflow-type: tm+mt
source-wordcount: '491'
ht-degree: 72%

---


# ContextHub の診断 {#contexthub-diagnostics}

ContextHub には、ContextHub フレームワークの概要を確認できる診断ページがあります。このページを開くには、AEM オーサーインスタンスの `contexthub.diagnostics.html` ページに移動します。例：

`http://<host>:<port>/conf/<tenant>/settings/cloudsettings/default/contexthub.diagnostics.html`

ContextHub の診断ページには、作成されたストアおよび UI モジュール、読み込まれているクライアントライブラリフォルダー、役立つページへのリンクに関する情報が表示されます。

>[!NOTE]
>
>診断情報が返されるようにするために、デバッグモードを有効にする必要があります。そうしないと、診断ページが空白になります。デバッグモードを有効にする方法について詳しくは、[このドキュメント](/help/sites-administering/contexthub-config.md#debugging-contexthub)を参照してください。

>[!NOTE]
>
>ContextHub設定が従来のパスの下にまだ存在する場合、診断ページの場所は`http://<host>:<port>/libs/settings/cloudsettings/legacy/contexthub.diagnostics.html`です。

## ストア {#stores}

ストアセクションには、設定されているすべての ContextHub ストアが一覧表示されます。リストの各項目は、次の情報で構成されます。

* **タイトル：**&#x200B;ストアのベースとなっている[ストアタイプ](/help/sites-developing/ch-samplestores.md)。
* **パス：**&#x200B;設定を保持しているリポジトリノードへのパス。
* **リソースタイプ：**&#x200B;ストアタイプが定義されているリポジトリノードのパス。
* **クライアントライブラリ：**&#x200B;読み込まれ、ストアタイプを実装するクライアントライブラリのカテゴリ。

## モジュール  {#modules}

モジュールセクションには、設定されているすべての ContextHub UI モジュールが一覧表示されます。リストの各項目は、次の情報で構成されます。

* **タイトル**：UI モジュールのベースとなっている [UI モジュールタイプ](/help/sites-developing/ch-samplemodules.md)。
* **パス：**&#x200B;設定を保持しているリポジトリノードへのパス。
* **リソースタイプ：** UI モジュールタイプが定義されているリポジトリノードのパス。
* **クライアントライブラリ：**&#x200B;読み込まれ、UI モジュールタイプを実装するクライアントライブラリのカテゴリ。

## Clientlibs  {#clientlibs}

Clientlibs セクションには、ContextHub によって読み込まれたすべてのクライアントライブラリフォルダーが一覧表示されます。クライアントライブラリは、次のように分類されます。

* **kernel.js：** ContextHub フレームワーク、セグメントエンジン、ストアタイプを実装するクライアントライブラリ。
* **ui.js：** ContextHub UI および UI モジュールタイプを実装するクライアントライブラリ。
* **style.css：**&#x200B;クライアントライブラリから読み込まれる CSS ファイル。

## URL  {#urls}

URL セクションには、次の ContextHub 機能へのリンクが含まれます。

* **設定エディター**：ストア、UI モードおよび UI モジュールを設定できる [ContextHub 設定ページ](/help/sites-administering/contexthub-config.md)を開きます。

* **ContextHubモジュールの設定：/etc/cloudsettings/default/contexthub.config.kernel.jsファイルを** 開きます。このファイルには、ContextHubストア設定のJavaScriptオブジェクト表現が含まれています。
* **ContextHub UIの設定：/etc/cloudsettings/default/contexthub.config.ui.jsファイルを** 開きます。このファイルには、ContextHub UIモード設定のJavascriptオブジェクト表現が含まれています。
* **kernel.js:/etc/cloudsettings/default/contexthub.kernel.jsファイルを** 開きます。このファイルには、ContextHubフレームワーク、セグメントエンジン、ストアタイプを実装するクライアントライブラリのソースコードが含まれています。
* **ui.js:/etc/cloudsettings/default/contexthub.ui.jsファイルを** 開きます。このファイルには、ContextHub UIとUIモジュールタイプを実装するクライアントライブラリのソースコードが含まれています。
* **style.css:/etc/cloudsettings/default/contexthub.styles.cssファイルを** 開きます。このファイルには、ContextHub UIおよびUIモジュールのCSSスタイルが含まれています。
