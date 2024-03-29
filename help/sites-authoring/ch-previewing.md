---
title: ContextHub データを使用したページのプレビュー
seo-title: Previewing Pages Using ContextHub Data
description: ContextHub ツールバーは、ContextHub ストアからのデータを表示し、ストアデータを変更することができ、コンテンツのプレビューに立ちます。
seo-description: The ContextHub toolbar displays data from ContextHub stores and enables you to change store data and  is useful for previewing content
uuid: 0150555a-0a92-4692-a706-bbe59fd34d6a
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.4/SITES
content-type: reference
topic-tags: personalization
discoiquuid: f281ef8c-0831-470c-acb7-189f20452a50
exl-id: 24f94dd5-62a4-4ac3-9a1b-a8e189da9958
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '401'
ht-degree: 43%

---

# ContextHub データを使用したページのプレビュー{#previewing-pages-using-contexthub-data}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

この [ContextHub](/help/sites-developing/contexthub.md) ツールバーは、ContextHub ストアのデータを表示し、ストアデータを変更できます。 ContextHub ツールバーは、ContextHub ストア内のデータによって決定されるコンテンツをプレビューする場合に役立ちます。

ツールバーは、1 つ以上の UI モジュールを含む一連の UI モードで構成されます。

* UI モードは、ツールバーの左側に表示されるアイコンです。 アイコンをクリックまたはタップすると、その中に含まれている UI モジュールがツールバーに表示されます。
* UI モジュールは、1 つ以上の ContextHub ストアのデータを表示します。 また、一部の UI モジュールでは、ストアデータを操作することもできます。

ContextHub によって、いくつかの UI モードと UI モジュールがインストールされます。管理者が [設定済みの ContextHub](/help/sites-administering/contexthub-config.md) を使用して、異なるものを表示できます。

![screen_shot_2018-03-23at093446](assets/screen_shot_2018-03-23at093446.png)

## ContextHub ツールバーの表示 {#revealing-the-contexthub-toolbar}

ContextHub ツールバーは、プレビューモードで使用できます。 このツールバーは、オーサーインスタンス上で、管理者が有効にしている場合にのみ使用できます。

![screen_shot_2018-03-23at093730](assets/screen_shot_2018-03-23at093730.png)

1. 編集用にページを開いた状態で、ツールバーの「プレビュー」をクリックまたはタップします。

   ![chlimage_1-219](assets/chlimage_1-219.png)

1. ツールバーを表示するには、ContextHub アイコンをクリックまたはタップします。

   ![](do-not-localize/screen_shot_2018-03-23at093621.png)

## UI モジュールの機能 {#ui-module-features}

各 UI モジュールは異なる機能セットを提供しますが、次のタイプの機能が一般的です。 UI モジュールは拡張可能なので、開発者は必要に応じて他の機能を実装できます。

### ツールバーの内容 {#toolbar-content}

UI モジュールは、1 つ以上の ContextHub ストアのデータをツールバーに表示できます。UI モジュールは、アイコンとタイトルで識別されます。

![screen_shot_2018-03-23at093936](assets/screen_shot_2018-03-23at093936.png)

### ポップアップコンテンツ {#popup-content}

一部の UI モジュールは、クリックまたはタップされるとポップアップオーバーレイを表示します。 一般的に、ポップアップには、ツールバーに表示されている以外の追加情報が含まれています。

![screen_shot_2018-03-23at094003](assets/screen_shot_2018-03-23at094003.png)

### ポップアップフォーム {#popup-forms}

モジュールのポップアップオーバーレイには、ContextHub ストア内のデータを変更できるフォーム要素を含めることができます。 ページのコンテンツがストアデータによって決まる場合は、フォームを使用して、ページコンテンツの変更を観察できます。

### 全画面表示モード {#fullscreen-mode}

ポップアップオーバーレイには、クリックまたはタップするとポップアップコンテンツを拡張してブラウザーウィンドウまたは画面全体に表示するアイコンを含めることができます。

![](do-not-localize/chlimage_1-18.png)
