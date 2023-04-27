---
title: グループテンプレート
seo-title: Group Templates
description: グループテンプレートコンソールへのアクセス方法
seo-description: How to access the Group Templates console
uuid: a3c6dfe6-f973-4dcf-9c66-ea52cbe56630
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.4/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 9a862756-58e8-47c0-a4b4-5d4aaac021e4
role: Admin
exl-id: ac399a66-0f3b-4f95-969e-a4109c260d1d
source-git-commit: 3c050c33a384d586d74bd641f7622989dc1d6b22
workflow-type: tm+mt
source-wordcount: '533'
ht-degree: 2%

---

# グループテンプレート {#group-templates}

グループテンプレートコンソールは、 [サイトテンプレート](sites.md) コンソール。 どちらも、コミュニティサイトを形成する一連の事前に配線されたページと機能のブループリントです。 異なる点は、サイトテンプレートがメインコミュニティ用であり、グループテンプレートがコミュニティグループ用であり、メインコミュニティ内にネストされたサブコミュニティ用である点です。

コミュニティグループは、 [グループ機能](functions.md#groups-function) （テンプレート内で最初に使用することも、唯一の機能として使用することもできません）。

コミュニティの時点 [機能パック 1](deploy-communities.md#latestfeaturepack)の場合は、グループテンプレート内にグループ機能を含めることで、グループをネストできます。

新しいコミュニティグループを作成するためのアクションが実行された時点で、グループのテンプレート（構造）が選択されます。 選択できる項目は、サイトまたはグループテンプレートに追加したときにグループ機能がどのように設定されたかによって異なります。

>[!NOTE]
>
>作成用のコンソール [コミュニティサイト](sites-console.md), [コミュニティサイトテンプレート](sites.md), [コミュニティグループテンプレート](tools-groups.md) および [コミュニティ機能](functions.md) は、オーサー環境でのみ使用されます。

## グループテンプレートコンソール {#group-templates-console}

オーサー環境で、グループテンプレートコンソールに移動するには

* グローバルナビゲーションから： **[!UICONTROL ツール/コミュニティ/グループテンプレート]**

このコンソールには、 [コミュニティサイト](sites-console.md) を作成し、新しいグループテンプレートを作成できます。

![groupstemplate](assets/groupstemplate.png)

## グループテンプレートを作成 {#create-goup-template}

新しいグループテンプレートの作成を開始するには、 **[!UICONTROL 作成]**

これにより、次の 3 つのサブパネルを含むサイトエディターパネルが表示されます。

### 基本情報 {#basic-info}

![chlimage_1-96](assets/chlimage_1-96.png)

基本情報パネルで、名前と説明、およびテンプレートの有効/無効を設定します。

* **[!UICONTROL 新しいグループテンプレート名]**
テンプレート名 ID

* **[!UICONTROL 説明]**
テンプレートの説明

* **[!UICONTROL 無効/有効]**
テンプレートを参照可能にするかどうかを制御する切り替えスイッチ

### サムネール {#thumbnail}

![chlimage_1-97](assets/chlimage_1-97.png)

（オプション）コミュニティサイトの作成者に対して、名前と説明に加えてサムネールを表示するには、画像をアップロードアイコンを選択します。

### 構造 {#structure}

>[!CAUTION]
>
>AEM 6.1 Communities FP4 以前を操作する場合は、グループテンプレートにグループ機能を追加しないでください。
>
>ネストされたグループ機能は、コミュニティで利用できます。 [FP1](communities.md#latestfeaturepack).
>
>グループ機能をテンプレートの最初の関数または唯一の関数として追加することは、まだできません。

![grptemplateeditor](assets/grptemplateeditor.png)

コミュニティ機能を追加するには、サイトメニューのリンクが表示される順に、右側から左にドラッグします。 スタイルは、サイトの作成時にテンプレートに適用されます。

例えば、フォーラムが必要な場合は、フォーラム機能をライブラリからドラッグし、テンプレートビルダーの下にドロップします。 これにより、フォーラム設定ダイアログが開きます。 詳しくは、 [関数コンソール](functions.md) を参照してください。

このテンプレートに基づくサブコミュニティサイト（グループ）に必要な他のコミュニティ機能を引き続きドラッグ&amp;ドロップします。

![drag 関数](assets/dragfunctions.png)

必要なすべての関数をテンプレートビルダー領域にドロップし、設定したら、「 」を選択します。 **[!UICONTROL 保存]** 右上隅に

## グループテンプレートを編集 {#edit-group-template}

メインでコミュニティグループを表示する場合 [グループテンプレートコンソール](#group-templates-console)の場合は、編集用に既存のグループテンプレートを選択できます。

グループテンプレートを編集しても、テンプレートから既に作成されているコミュニティサイトには影響しません。 直接 [コミュニティサイトを編集](sites-console.md#modify-structure)の構造が代わりに使用されます。

このプロセスは、 [グループテンプレートの作成](#create-goup-template).
