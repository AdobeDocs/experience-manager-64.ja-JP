---
title: Social タグクラウドの使用
seo-title: Using Social Tag Cloud
description: Social タグクラウドコンポーネントをページに追加
seo-description: Adding a Social Tag Cloud component to a page
uuid: 8c400030-976c-457a-bb5f-e473909647a9
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.4/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 23a5a65e-774d-4789-9659-09e8be0c2bcd
exl-id: 3f55a02c-2733-4f69-8112-7c6c4c98938c
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '558'
ht-degree: 42%

---

# Social タグクラウドの使用 {#using-social-tag-cloud}

## はじめに {#introduction}

この `Social Tag Cloud` コンポーネントは、コンテンツの投稿時にコミュニティメンバーが適用したタグをハイライトします。 これは、トレンドトピックを識別し、サイト訪問者がタグ付きコンテンツをすばやく見つけられるようにする手段です。

現在のトレンドを識別するもう 1 つの手段については、「[アクティビティのトレンド](trends.md)」を参照してください。

このページでは、 `Social Tag Cloud` コンポーネントダイアログの設定およびユーザーエクスペリエンスについて説明します。

開発者向けの詳細な情報は、[タグの重要事項](tag.md)を参照してください。

タグの作成および管理や、タグが適用されるコンテンツについては、[タグの管理](../../help/sites-administering/tags.md)を参照してください。

## Social タグクラウドの追加 {#adding-a-social-tag-cloud}

を追加するには、以下を実行します。 `Social Tag Cloud` コンポーネントをオーサリングモードでページに追加する場合は、コンポーネントブラウザーを使用して `Communities / Social Tag Cloud` をクリックし、ページ上のタグクラウドが表示される場所にドラッグします。

必要な情報については、 [コミュニティコンポーネントの基本](basics.md).

次の場合に [必要なクライアント側ライブラリ](tag.md#essentials-for-client-side) が含まれる場合、この方法で `Social Tag Cloud` コンポーネントが表示されます。

![chlimage_1-303](assets/chlimage_1-303.png)

## Social タグクラウドの設定 {#configuring-social-tag-cloud}

配置された `Social Tag Cloud` アクセスして選択するコンポーネント `Configure` 編集ダイアログを開くアイコン。

![chlimage_1-304](assets/chlimage_1-304.png)

「**[!UICONTROL Social タグクラウド]**」タブでは、どのタグを表示するかと、タグがアクティブリンクである場合に、検索結果を表示するページの場所を指定します。

![chlimage_1-305](assets/chlimage_1-305.png)

* **[!UICONTROL 表示する Social タグ]**&#x200B;表示する UGC タグを指定します。プルダウンオプションは次のとおりです。

   * `From page and child pages`
   * `All tags`

   デフォルトはです。 `From page and child pages`(「page」は **ページ** を設定します。

* **[!UICONTROL ページ]**
( そうでない場合は必須 
`All tags)` ページの UGC へのパス。 空白の場合、初期設定は現在のページです。

* **[!UICONTROL タグにリンクがありません]**&#x200B;オンにすると、タグはタグクラウドにプレーンテキストとして表示されます。オフにすると、タグは、そのタグが適用されるすべてのコンテンツを検索するアクティブなリンクとして表示されます。 デフォルトはオフで、に必要な **[!UICONTROL 検索結果のパス]** を設定します。

* **[!UICONTROL 検索結果のパス]**
ページのパス。 
`Search Result` コンポーネントが配置され、 **ページ** 設定。

## Social タグクラウドの表示を変更する {#change-display-of-social-tag-cloud}

表示を編集するには **Social タグクラウド**&#x200B;を入力して、 [デザインモード](../../help/sites-authoring/default-components-designmode.md) そして、配置された `Social Tag Cloud` 追加のタブを含むダイアログを開くコンポーネント。

の使用 **[!UICONTROL Social タグクラウド（デザイン）]** タブで、タグの表示方法を指定します。 タグは、単純なタグ、デフォルト名前空間の単一の単語、階層的な分類のいずれかになります。

![chlimage_1-306](assets/chlimage_1-306.png)

* **[!UICONTROL タイトルの完全なパスを表示]**&#x200B;オンにすると、適用されたタグごとに、親タグと名前空間のタイトルが表示されます。

   次は例です。

   * チェック済み: `Geometrixx Media: Gadgets / Cars`
   * 未チェック: `Cars`

   シンプルなタグの場合は、表示に違いは現れません。

   初期設定はオフです。

* **[!UICONTROL リーフタグのみを表示]**&#x200B;オンにした場合は、適用されるタグのみが表示され、その他のタグは含まれません。

   例えば、タグ ID が

   `Geometrixx Media: Gadgets / Cars`

   次の 3 つのタグを適用できます。 `Geometrixx Media (the namespace)`, `Gadgets`、および `Cars`

   * チェック済み：のみ `Cars` 適用される場合は、表示されます
   * オフ： `Geometrixx Media` および `Gadgets`同様に `Cars` 適用される場合は、表示されます

   シンプルなタグはリーフタグです。

   初期設定はオフです。

* **[!UICONTROL リンクテンプレート]**&#x200B;コンポーネントの編集ダイアログでリンクが有効にされているときに、タグクラウド内にリンクを表示するために使用されるデフォルト以外のテンプレートを指定します。

* **[!UICONTROL すべてのタグに同じサイズ]**&#x200B;オンにすると、タグクラウド内のすべての単語が同じスタイルに設定されます。オフにすると、単語のスタイルは使用方法に応じて異なります。 初期設定はオフです。

## 追加情報 {#additional-information}

詳しくは、 [タグの基本事項](tag.md) 開発者向けのページ

詳しくは、 [ユーザー生成コンテンツのタグ付け](tag-ugc.md) (UGC) を参照してください。
