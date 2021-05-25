---
title: サイトテンプレート
seo-title: サイトテンプレート
description: サイトテンプレートコンソールにアクセスする方法
seo-description: サイトテンプレートコンソールにアクセスする方法
uuid: d2f7556e-7e43-424e-82f1-41790aeb2d98
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.4/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 202d7dba-2b34-431d-b10f-87775632807f
role: Administrator
exl-id: 5049c5df-c874-4c34-a96b-7944cd0353d5
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '463'
ht-degree: 63%

---

# サイトテンプレート  {#site-templates}

サイトテンプレートコンソールは、コミュニティグループに関心のある機能に焦点を当てた[グループテンプレート](tools-groups.md)コンソールと非常に似ています。

>[!NOTE]
>
>[コミュニティサイト](sites-console.md)、[コミュニティサイトテンプレート](sites.md)、[コミュニティグループテンプレート](tools-groups.md)、[コミュニティ機能](functions.md)の作成用のコンソールは、オーサー環境でのみ使用できます。

## Site Templates Console {#site-templates-console}

オーサー環境でコミュニティサイトコンソールに移動するには、

* グローバルナビゲーションから：**[!UICONTROL ツール/コミュニティ/サイトテンプレート]**

このコンソールでは、[コミュニティサイト](sites-console.md)を作成できるテンプレートが表示されます。また、新しいサイトテンプレートを作成できます。

![chlimage_1-18](assets/chlimage_1-18.png)

## Create Site Template {#create-site-template}

新しいサイトテンプレートの作成を開始するには、「`Create`」を選択します。

するとサイトエディターパネルに移動します。パネルには以下の 3 つのサブパネルがあります。

### 基本情報{#basic-info}

![chlimage_1-19](assets/chlimage_1-19.png)

基本情報パネルでは、名前、説明およびテンプレートを有効にするか無効にするかを設定します。

* **[!UICONTROL コミュニティサイトテ]**
ンプレート名テンプレート名id

* **[!UICONTROL コミュニティサイトテンプ]**
レートの説明テンプレートの説明

* **[!UICONTROL 無効/有]**
効テンプレートを参照可能にするかどうかを制御する切り替えスイッチ

### サムネール {#thumbnail}

![chlimage_1-20](assets/chlimage_1-20.png)

（オプション）コミュニティサイトの作成者に対し、名前と説明に加えてサムネイルを表示するには、画像をアップロードアイコンを選択します。

### 構造 {#structure}

![chlimage_1-21](assets/chlimage_1-21.png)

コミュニティ機能を追加するには、右側から左側にドラッグします。サイトメニューのリンクは追加した順番で表示されます。スタイルは、サイトの作成時にテンプレートに適用されます。

例えば、ホームページが必要な場合は、ページ機能をライブラリからテンプレートビルダーにドラッグ＆ドロップします。これにより、ページ設定ダイアログが開きます。 設定ダイアログについて詳しくは、[関数コンソール](functions.md)を参照してください。

このテンプレートをベースとするコミュニティサイトに必要な、他のコミュニティ機能を続けてドラッグ＆ドロップします。

ページ機能では空のページが作成されます。グループ機能を使用すると、コミュニティサイト内にグループサイト（サブコミュニティ）を作成できます。

>[!CAUTION]
>
>グループ関数は、**&#x200B;を&#x200B;*の最初の関数にし、サイト構造内で唯一の*&#x200B;関数にしないでください。
>
>他の機能（[ページ機能](functions.md#page-function)など）を含め、その機能を 1 番目にリストする必要があります。

![chlimage_1-22](assets/chlimage_1-22.png)

### グループ機能のためのグループテンプレート {#group-templates-for-groups-function}

サイトテンプレートにグループ機能を含める場合、パブリッシュ環境で新しいグループを作成するときに、グループテンプレート選択の仕様が設定により許可されている必要があります。

>[!CAUTION]
>
>Groups関数は、**&#x200B;を&#x200B;*の最初の関数でも、サイト構造内で唯一の*&#x200B;関数でもなければなりません。

![chlimage_1-23](assets/chlimage_1-23.png)

2 つ以上のグループテンプレートを選択することにより、グループ管理者が実際にコミュニティで新しいグループを作成するときに、テンプレートを選択できるようになります。

![chlimage_1-24](assets/chlimage_1-24.png)

## サイトテンプレートを編集 {#edit-site-template}

メインの[サイトテンプレートコンソール](#site-templates-console)でサイトテンプレートを表示しているときに、既存のサイトテンプレートを選択して編集できます。

このプロセスでは、[サイトテンプレートの作成](#create-site-template)と同じパネルを使用します。
