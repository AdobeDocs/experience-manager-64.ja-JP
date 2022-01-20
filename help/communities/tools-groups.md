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
ht-degree: 58%

---

# グループテンプレート {#group-templates}

グループテンプレートコンソールは、[サイトテンプレート](sites.md)コンソールによく似ています。どちらも、コミュニティサイトを形成する一連の事前に配線されたページと機能のブループリントです。 異なる点は、サイトテンプレートがメインコミュニティ用であり、グループテンプレートがコミュニティグループ用であり、メインコミュニティ内にネストされたサブコミュニティ用である点です。

コミュニティグループは、 [グループ機能](functions.md#groups-function) （テンプレート内で最初に使用することも、唯一の機能として使用することもできません）。

Communities [機能パック 1](deploy-communities.md#latestfeaturepack) 以降、グループテンプレート内にグループ機能を含めることにより、グループをネストできるようになりました。

新しいコミュニティグループを作成するアクションが実行されるとすぐに、グループのテンプレート（構造）が選択されます。選択できる項目は、サイトまたはグループテンプレートに追加したときにグループ機能がどのように設定されたかによって異なります。

>[!NOTE]
>
>作成用のコンソール [コミュニティサイト](sites-console.md), [コミュニティサイトテンプレート](sites.md), [コミュニティグループテンプレート](tools-groups.md) および [コミュニティ機能](functions.md) は、オーサー環境でのみ使用されます。

## グループテンプレートコンソール {#group-templates-console}

オーサー環境でグループテンプレートコンソールに移動するには、

* グローバルナビゲーションから： **[!UICONTROL ツール/コミュニティ/グループテンプレート]**

このコンソールには、 [コミュニティサイト](sites-console.md) を作成し、新しいグループテンプレートを作成できます。

![groupstemplate](assets/groupstemplate.png)

## グループテンプレートの作成 {#create-goup-template}

新しいグループテンプレートの作成を開始するには、「**[!UICONTROL 作成]**」を選択します。

するとサイトエディターパネルに移動します。パネルには以下の 3 つのサブパネルがあります。

### 基本情報 {#basic-info}

![chlimage_1-96](assets/chlimage_1-96.png)

基本情報パネルでは、名前、説明およびテンプレートを有効にするか無効にするかを設定します。

* **[!UICONTROL 新しいグループテンプレート名]**
テンプレート名 ID

* **[!UICONTROL 説明]**
テンプレートの説明

* **[!UICONTROL 無効/有効]**
テンプレートを参照可能にするかどうかを制御する切り替えスイッチ

### サムネール {#thumbnail}

![chlimage_1-97](assets/chlimage_1-97.png)

（オプション）コミュニティサイトの作成者に対し、名前と説明に加えてサムネイルを表示するには、画像をアップロードアイコンを選択します。

### 構造 {#structure}

>[!CAUTION]
>
>AEM 6.1 Communities FP4 以前のバージョンを使用している場合は、グループテンプレートにグループ機能を追加しないでください。
>
>ネストされたグループの機能を使用できるのは、Communities [FP1](communities.md#latestfeaturepack) 以降です。
>
>テンプレート内の 1 番目の機能または唯一の機能としてグループ機能を追加することはまだできません。

![grptemplateeditor](assets/grptemplateeditor.png)

コミュニティ機能を追加するには、右側から左側にドラッグします。サイトメニューのリンクは追加した順番で表示されます。スタイルは、サイトの作成時にテンプレートに適用されます。

例えば、フォーラムが必要な場合は、フォーラム機能をライブラリからテンプレートビルダーにドラッグ＆ドロップします。これにより、フォーラム設定ダイアログが開きます。 詳しくは、 [関数コンソール](functions.md) を参照してください。

このテンプレートをベースとするサブコミュニティサイト（グループ）に必要な、その他のコミュニティ機能を続けてドラッグ＆ドロップします。

![drag 関数](assets/dragfunctions.png)

必要なすべての関数をテンプレートビルダー領域にドロップし、設定したら、「 」を選択します。 **[!UICONTROL 保存]** 右上隅に

## グループテンプレートを編集 {#edit-group-template}

メインの[グループテンプレートコンソール](#group-templates-console)でコミュニティグループを表示しているときに、既存のサイトテンプレートを選択して編集できます。

グループテンプレートを編集しても、そのテンプレートを基に作成された既存のコミュニティサイトに影響が及ぶことはありません。その代わりに、直接[コミュニティサイトの構造を編集](sites-console.md#modify-structure)することができます。

このプロセスでは、[グループテンプレートの作成](#create-goup-template)と同じパネルを使用します。
