---
title: コンポーネントのサイドローディング
seo-title: Component Sideloading
description: コミュニティコンポーネントのサイドロードは、Web ページが単純な単一ページアプリとして設計され、サイト訪問者が選択した内容に応じて表示内容を動的に変更する場合に役立ちます
seo-description: Communities component sideloading is useful when a web page is designed as a simple, single page app that dynamically alters what is displayed depending on what is selected by the site visitor
uuid: 8c9a5fde-26a3-4610-bc14-f8b665059015
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.4/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: a9cb5294-e5ab-445b-b7c2-ffeecda91c50
exl-id: 12fdc503-29b6-4970-a883-c22162f7a9eb
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '441'
ht-degree: 2%

---

# コンポーネントのサイドローディング {#component-sideloading}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

## 概要 {#overview}

コミュニティコンポーネントのサイドロードは、Web ページが単純な単一ページアプリとして設計され、サイト訪問者が選択した内容に応じて表示内容を動的に変更する場合に役立ちます。

これは、コミュニティコンポーネントがページテンプレートに存在せず、代わりにサイト訪問者の選択に従って動的に追加される場合に実行されます。

ソーシャルコンポーネントフレームワーク (SCF) は軽量な存在なので、最初のページ読み込み時に存在する SCF コンポーネントのみが登録されます。 ページの読み込み後に動的に追加された SCF コンポーネントを登録するには、SCF を呼び出してコンポーネントを「サイドロード」する必要があります。

Communities コンポーネントをサイドロードするように設計されているページでは、ページ全体をキャッシュできます。

SCF コンポーネントを動的に追加する手順は次のとおりです。

1. [DOM にコンポーネントを追加します。](#dynamically-add-component-to-dom)

1. [コンポーネントをサイドロード](#sideload-by-invoking-scf) 次の 2 つの方法のいずれかを使用します。

* [動的な追加](#dynamic-inclusion)
   * 動的に追加されたすべてのコンポーネントをブーストラップ
* [動的な読み込み](#dynamic-loading)
   * 特定のコンポーネントをオンデマンドで追加

>[!NOTE]
>
>サイドローディング [存在しないリソース](scf.md#add-or-include-a-communities-component) はサポートされていません。

## DOM にコンポーネントを動的に追加 {#dynamically-add-component-to-dom}

コンポーネントが動的に含まれるか動的に読み込まれるかに関わらず、まず DOM に追加する必要があります。

SCF コンポーネントを追加する際に最も一般的なタグは DIV タグですが、他のタグも使用できます。 SCF はページが最初に読み込まれたときにのみ DOM を調べるので、SCF が明示的に呼び出されるまで、DOM へのこの追加は無視されます。

どのタグを使用する場合でも、少なくとも、その要素は、次の 2 つの属性を含めることで、通常の SCF ルート要素パターンに準拠している必要があります。

* **data-component-id**
追加されたコンポーネントへの有効なパス

* **data-scf-component**
コンポーネントの resourceType

次に、追加されたコメントコンポーネントの例を示します。

```xml
<div
    class="scf-commentsystem scf translation-commentsystem" 
    data-component-id="<%= currentPage.getPath()%>/jcr:content/content-left/comments"
    data-scf-component="social/commons/components/hbs/comments"
>
</div>
```

## SCF の呼び出しによるサイドロード {#sideload-by-invoking-scf}

### 動的な組み込み {#dynamic-inclusion}

動的インクルージョンは、ブーストラップリクエストを使用するので、SCF が DOM を調べて、ページ上のすべての SCF コンポーネントをブートスラップします。

ページの読み込み後に SCF コンポーネントを初期化するには、次のような JQuery イベントを発生させます。

$(document).トリガー(SCF.events.BOOTSTRAP_REQUEST);

### 動的読み込み {#dynamic-loading}

動的な読み込みは、SCF コンポーネントの読み込みを制御します。

DOM 内のすべての SCF コンポーネントをブートストラップする代わりに、次の JavaScript メソッドを使用して、読み込む特定の SCF コンポーネントを指定することができます。

SCF.addComponent(document.getElementById(*someId*));

ここで、 *someId* が **data-component-id** 属性。
