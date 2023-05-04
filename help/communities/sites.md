---
title: サイトテンプレート
seo-title: Site Templates
description: サイトテンプレートコンソールへのアクセス方法
seo-description: How to access the Site Templates console
uuid: d2f7556e-7e43-424e-82f1-41790aeb2d98
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.4/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 202d7dba-2b34-431d-b10f-87775632807f
role: Admin
exl-id: 5049c5df-c874-4c34-a96b-7944cd0353d5
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '490'
ht-degree: 5%

---

# サイトテンプレート {#site-templates}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

サイトテンプレートコンソールは、 [グループテンプレート](tools-groups.md) コミュニティグループに関心のある機能に焦点を当てたコンソール。

>[!NOTE]
>
>作成用のコンソール [コミュニティサイト](sites-console.md), [コミュニティサイトテンプレート](sites.md), [コミュニティグループテンプレート](tools-groups.md) および [コミュニティ機能](functions.md) は、オーサー環境でのみ使用されます。

## サイトテンプレートコンソール {#site-templates-console}

オーサー環境でコミュニティサイトコンソールにアクセスするには、次の手順を実行します。

* グローバルナビゲーションから： **[!UICONTROL ツール/コミュニティ/サイトテンプレート]**

このコンソールには、 [コミュニティサイト](sites-console.md) を作成して、新しいサイトテンプレートを作成できます。

![chlimage_1-18](assets/chlimage_1-18.png)

## サイトテンプレートを作成 {#create-site-template}

新しいサイトテンプレートの作成を開始するには、「 `Create`.

これにより、次の 3 つのサブパネルを含むサイトエディターパネルが表示されます。

### 基本情報 {#basic-info}

![chlimage_1-19](assets/chlimage_1-19.png)

基本情報パネルで、名前と説明、およびテンプレートの有効/無効を設定します。

* **[!UICONTROL コミュニティサイトテンプレート名]**
テンプレート名 ID

* **[!UICONTROL コミュニティサイトテンプレートの説明]**
テンプレートの説明

* **[!UICONTROL 無効/有効]**
テンプレートを参照可能にするかどうかを制御する切り替えスイッチ

### サムネール {#thumbnail}

![chlimage_1-20](assets/chlimage_1-20.png)

（オプション）コミュニティサイトの作成者に対して、名前と説明に加えてサムネールを表示するには、画像をアップロードアイコンを選択します。

### 構造 {#structure}

![chlimage_1-21](assets/chlimage_1-21.png)

コミュニティ機能を追加するには、サイトメニューのリンクが表示される順に、右側から左にドラッグします。 スタイルは、サイトの作成時にテンプレートに適用されます。

例えば、ホームページが必要な場合は、ライブラリからページ機能をドラッグし、テンプレートビルダーの下にドロップします。 これにより、ページ設定ダイアログが開きます。 詳しくは、 [関数コンソール](functions.md) を参照してください。

このテンプレートに基づいて、コミュニティサイトに必要な他のコミュニティ機能を引き続きドラッグ&amp;ドロップします。

ページ関数は、空のページを提供します。 グループ機能を使用すると、コミュニティサイト内にグループサイト（サブコミュニティ）を作成できます。

>[!CAUTION]
>
>グループ機能は、 *not* は *最初でも唯一でも* 関数を使用して、サイト構造内で使用できます。
>
>その他の関数 ( [ページ関数](functions.md#page-function)、を含め、最初にリストする必要があります。

![chlimage_1-22](assets/chlimage_1-22.png)

### グループ機能のグループテンプレート {#group-templates-for-groups-function}

サイトテンプレートにグループ機能を含める場合、設定では、パブリッシュ環境で新しいグループを作成する際に使用できるグループテンプレートの選択肢を指定する必要があります。

>[!CAUTION]
>
>Groups 関数を使用する必要があります。 *not* は *最初でも唯一でも* 関数を使用して、サイト構造内で使用できます。

![chlimage_1-23](assets/chlimage_1-23.png)

2 つ以上のコミュニティグループテンプレートを選択すると、コミュニティで新しいグループを実際に作成する際に、グループ管理者に選択肢が提供されます。

![chlimage_1-24](assets/chlimage_1-24.png)

## サイトテンプレートを編集 {#edit-site-template}

メインでサイトテンプレートを表示する場合 [サイトテンプレートコンソール](#site-templates-console)の場合は、編集用に既存のサイトテンプレートを選択できます。

このプロセスは、 [サイトテンプレートの作成](#create-site-template).
