---
title: ソーシャルタグクラウドの使用
seo-title: Social タグクラウドの使用
description: Social タグクラウドコンポーネントをページに追加
seo-description: Social タグクラウドコンポーネントをページに追加
uuid: 8c400030-976c-457a-bb5f-e473909647a9
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.4/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 23a5a65e-774d-4789-9659-09e8be0c2bcd
translation-type: tm+mt
source-git-commit: 5e30bf76fd3304ed268c45cc8862a9c51c5d30f1
workflow-type: tm+mt
source-wordcount: '571'
ht-degree: 39%

---


# Social タグクラウドの使用 {#using-social-tag-cloud}

## 概要 {#introduction}

The `Social Tag Cloud` component highlights tags applied by community members when posting content. これは、トレンドトピックを識別し、サイト訪問者がタグ付けされたコンテンツをすばやく見つけられるようにする手段です。

現在のトレンドを識別するもう 1 つの手段については、「[アクティビティのトレンド](trends.md)」を参照してください。

This page documents the `Social Tag Cloud` component dialog settings and describes the user experience.

開発者向けの詳細な情報は、[タグの重要事項](tag.md)を参照してください。

See [Administering Tags](../../help/sites-administering/tags.md) for information about creating and managing tags, as well as to which content tags have been applied.

## Social タグクラウドの追加 {#adding-a-social-tag-cloud}

作成者モードでページに `Social Tag Cloud` コンポーネントを追加するには、コンポーネントブラウザーを使用してタグクラウドを表示するページを探し `Communities / Social Tag Cloud` 、ドラッグして配置します。

For necessary information, visit [Communities Components Basics](basics.md).

[必要なクライアント側ライブラリが含まれる場合](tag.md#essentials-for-client-side) 、次のようにコンポー `Social Tag Cloud` ネントが表示されます。

![chlimage_1-303](assets/chlimage_1-303.png)

## Social タグクラウドの設定 {#configuring-social-tag-cloud}

Select the placed `Social Tag Cloud` component to access and select the `Configure` icon which opens the edit dialog.

![chlimage_1-304](assets/chlimage_1-304.png)

「**[!UICONTROL Social タグクラウド]**」タブでは、どのタグを表示するかと、タグがアクティブリンクである場合に、検索結果を表示するページの場所を指定します。

![chlimage_1-305](assets/chlimage_1-305.png)

* **[!UICONTROL 表示する Social タグ]**&#x200B;表示する UGC タグを指定します。プルダウンオプションは、

   * `From page and child pages`
   * `All tags`

   デフォルト値は `From page and child pages`です。ここで、「page」は下の **「** Page」設定を指します。

* **[!UICONTROL ページ]**( 
`All tags)` ページのUGCへのパス。 デフォルトは、空白の場合に現在のページになります。

* **[!UICONTROL タグにリンクがありません]**&#x200B;オンにすると、タグはタグクラウドにプレーンテキストとして表示されます。選択しない場合、タグはアクティブリンクとして表示され、タグが適用されるすべてのコンテンツが検索されます。 Default is unchecked and requires the **[!UICONTROL Search Result Path]** to be set.

* **[!UICONTROL Search Result Path]**: 
`Search Result` コンポーネントが配置され、 **ページ** 設定で指定されたUGCパスを含むUGCを参照するように設定されている。

## Social タグクラウドの表示を変更する {#change-display-of-social-tag-cloud}

To edit the display of the **Social Tag Cloud**, enter [Design Mode](../../help/sites-authoring/default-components-designmode.md) and double click on the placed `Social Tag Cloud` component to open a dialog with an additional tab.

Using the **[!UICONTROL Social Tag Cloud (Design)]** tab, specify how tags are displayed. タグは、単純なタグ、デフォルトの名前空間内の単一の単語、または階層的な分類のいずれかです。

![chlimage_1-306](assets/chlimage_1-306.png)

* **[!UICONTROL タイトルの完全なパスを表示]**&#x200B;オンにすると、適用されたタグごとに、親タグと名前空間のタイトルが表示されます。

   次に例を示します。

   * チェック: `Geometrixx Media: Gadgets / Cars`
   * 未チェック: `Cars`

   シンプルなタグの場合は、表示に違いは現れません。

   初期設定はオフです。

* **[!UICONTROL リーフタグのみを表示]**&#x200B;オンにした場合は、適用されるタグのみが表示され、その他のタグは含まれません。

   例えば、

   `Geometrixx Media: Gadgets / Cars`

   適用できるタグは3つあります。 `Geometrixx Media (the namespace)`、 `Gadgets`および `Cars`

   * Checked: only `Cars` will display, if applied
   * Unchecked: `Geometrixx Media` and `Gadgets`as well as `Cars` will display, if applied

   シンプルなタグはリーフタグです。

   初期設定はオフです。

* **[!UICONTROL リンクテンプレート]**&#x200B;コンポーネントの編集ダイアログでリンクが有効にされているときに、タグクラウド内にリンクを表示するために使用されるデフォルト以外のテンプレートを指定します。

* **[!UICONTROL すべてのタグに同じサイズ]**&#x200B;オンにすると、タグクラウド内のすべての単語が同じスタイルに設定されます。選択しない場合、単語のスタイルは使用方法に応じて異なります。 初期設定はオフです。

## 追加情報 {#additional-information}

More information may be found on the [Tag Essentials](tag.md) page for developers.

See [Tagging User Generated Content](tag-ugc.md) (UGC) for information about creating and managing tags.
