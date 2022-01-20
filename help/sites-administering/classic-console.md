---
title: クラシック UI のタグ付けコンソール
seo-title: Classic UI Tagging Console
description: クラシック UI のタグ付けコンソールについて説明します。
seo-description: Learn about the Classic UI Tagging Console.
uuid: c3080c82-0b34-4922-a263-1674a9522649
contentOwner: Chiradeep Majumdar
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: content
content-type: reference
discoiquuid: a7f31bc8-c583-439f-b2af-1dcc58f9c481
exl-id: 0c989965-c6cc-4ec7-a90f-6c52e8362485
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '879'
ht-degree: 64%

---

# クラシック UI のタグ付けコンソール{#classic-ui-tagging-console}

この節では、クラシック UI のタグ付けコンソールについて説明します。

タッチ操作向け UI のタグ付けコンソールは[こちら](/help/sites-administering/tags.md#tagging-console)です。

クラシック UI のタグ付けコンソールにアクセスするには：

* オーサー環境で
* 管理者権限でサインインします。
*  コンソールに移動します。

   例： [http://localhost:4502/tagging](http://localhost:4502/tagging)

![managing_tags_usingthetagasadministrationconsole-1](assets/managing_tags_usingthetagasministrationconsole-1.png)

## タグおよび名前空間の作成 {#creating-tags-and-namespaces}

1. 開始するレベルに応じて、「**新規**」を使用してタグまたは名前空間を作成できます。

   「**タグ**」を選択すると、名前空間を作成できます。

   ![creating_tags_andnamespaces-1](assets/creating_tags_andnamespaces-1.png)

   名前空間（例えば「**Demo**」）を選択すると、その名前空間内にタグを作成できます。

   ![creating_tags_andnamespacesinnewnamespace](assets/creating_tags_andnamespacesinnewnamespace.png)

1. どちらの場合も、次のように入力します。

   * **タイトル**
(
*必須*) タグの表示タイトル。 どの文字も入力できますが、

      次の特殊文字は使用しないことをお勧めします。

      * `colon (:)`  — 名前空間区切り文字
      * `forward slash (/)`  — サブタグ区切り文字

      これらの文字は入力しても表示されません。

   * **名前**

      (*必須*) タグのノード名。

   * **説明**

      (*オプション*) タグの説明。

   * 「**作成**」を選択します


## タグの編集 {#editing-tags}

1. 右側のウィンドウで、編集するタグを選択します。
1. 「**編集**」をクリックします。
1. 「**タイトル**」および「**説明**」を変更できます。
1. 「**保存**」をクリックしてダイアログを閉じます。

## タグの削除 {#deleting-tags}

1. 右側のウィンドウで、削除するタグを選択します。
1. 「**削除**」をクリックします。
1. 「**はい**」をクリックしてダイアログを閉じます。

   これでタグはリストから削除されます。

## タグのアクティベートおよびアクティベート解除 {#activating-and-deactivating-tags}

1. 右側のウィンドウで、アクティベート（公開）またはアクティベート解除（非公開に）する名前空間またはタグを選択します。
1. 必要に応じて、「**アクティベート**」または「**アクティベートの解除**」をクリックします。

## リスト - タグが参照されている場所の表示 {#list-showing-where-tags-are-referenced}

「**リスト**」を選択すると、新しいウィンドウが開き、ハイライト表示されたタグを使用しているすべてのページのパスが表示されます。

![list_showing_wheretagsarereferenced](assets/list_showing_wheretagsarereferenced.png)

## タグの移動 {#moving-tags}

タグの管理者および開発者が分類の整理やタグ ID の名前の変更ができるように、タグを新しい場所に移動することができます。

1. **Tagging** コンソールを開きます。
1. タグを選択して、最上部のツールバー（またはコンテキストメニュー）で「**Move...**」をクリックします。
1. **Move Tag** ダイアログで次の項目を指定します。

   * **to**：移動先のノード。
   * **Rename to**：新しいノード名。

1. 「**Move**」をクリックします。

**Move Tag** ダイアログは次のようになります。

![move_tag](assets/move_tag.png)

>[!NOTE]
>
>作成者は、タグを移動したり、タグ ID の名前を変更したりしないでください。作成者は、必要に応じて [タグのタイトルを変更する](#editing-tags).

## タグの統合 {#merging-tags}

タグの統合は、分類が重複する場合に使用できます。タグ A がタグ B にマージされると、タグ A が付けられたすべてのページにタグ B が付けられ、作成者はタグ A を使用できなくなります。

タグを別のタグにマージするには：

1. **Tagging** コンソールを開きます。
1. タグを選択して、最上部のツールバー（またはコンテキストメニュー）で「**Merge...**」をクリックします。
1. **Merge Tag** ダイアログで次の項目を定義します。

   * **into**：マージ先のノード。

1. 「**Merge**」をクリックします。

この **タグを結合** ダイアログは次のように表示されます。

![mergetag](assets/mergetag.png)

## タグの使用回数のカウント {#counting-usage-of-tags}

タグの使用回数を確認するには：

1. **Tagging** コンソールを開きます。
1. 最上部のツールバーで「**数の使用法**」をクリックします。「数」列に結果が表示されます。

## 他の言語でのタグの管理 {#managing-tags-in-different-languages}

オプション `title`タグのプロパティは、複数の言語に翻訳できます。 タグ `titles` は、その後、ユーザーの言語またはページの言語に従って表示できます。

### 複数言語でのタグタイトルの定義 {#defining-tag-titles-in-multiple-languages}

以下の手順は、 `title`タグの **動物** 英語、ドイツ語、フランス語に

1. 次に移動： **タグ付け** コンソール。
1. タグの編集 **動物** 下 **タグ** > **フォトグラフィー**.
1. 次の言語での翻訳を追加します。

   * **英語**：Animals
   * **ドイツ語**：Tiere
   * **フランス語**：Animaux

1. 変更内容を保存します。

ダイアログは次のようになります。

![edit_tag](assets/edit_tag.png)

Tagging コンソールではユーザーの言語設定が使用されます。したがって Animal タグは、ユーザープロパティで言語をフランス語に設定しているユーザーには「Animaux」と表示されます。

ダイアログに新しい言語を追加する方法については、[開発者のためのタグ付け](/help/sites-developing/building.md#adding-a-new-language-to-the-edit-tag-dialog)の&#x200B;**タグを編集ダイアログへの新しい言語の追加**&#x200B;を参照してください。

### 指定した言語でページのプロパティにタグタイトルを表示 {#displaying-tag-titles-in-page-properties-in-a-specified-language}

デフォルトでは、タグは `titles`ページのプロパティは、ページの言語で表示されます。 ページプロパティのタグダイアログには、タグを表示できる言語フィールドがあります `titles`別の言語で 次の手順で、タグを表示する方法を説明します `titles`フランス語：

1. 前の節を参照して、 **動物** 下 **タグ** > **フォトグラフィー**.
1. **Geometrixx** サイトの英語ブランチで、**Products** ページのページプロパティを開きます。
1. を開きます。 **タグ/キーワード** ダイアログで（「タグ/キーワード」表示領域の右にあるプルダウンメニューを選択して）、 **フランス語** 言語を、右下隅のプルダウンメニューから選択します。
1. 左右の矢印を使用してスクロールし、 **フォトグラフィー** タブ

   を選択します。 **動物** (**アニモー**) タグをクリックし、ダイアログの外側を選択して閉じ、ページのプロパティにタグを追加します。

   ![french_tag](assets/french_tag.png)

デフォルトでは、ページのプロパティダイアログにタグが表示されます `titles`ページ言語に従って。

通常は、ページ言語が有効な場合、タグの言語はページ言語から取得されます。[tag ウィジェット](/help/sites-developing/building.md#tagging-on-the-client-side)が他のケース（フォームやダイアログなど）で使用されている場合、タグの言語はコンテキストによって変わります。

>[!NOTE]
>
>標準ページコンポーネント内のタグクラウドとメタキーワードは、ローカライズされたタグを使用します `titles`ページ言語に基づく（可能な場合）
