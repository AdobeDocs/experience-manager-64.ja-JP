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


# Social タグクラウドの使用  {#using-social-tag-cloud}

## 概要 {#introduction}

`Social Tag Cloud`コンポーネントは、コンテンツを投稿する際にコミュニティメンバーが適用したタグをハイライトします。 これは、トレンドトピックを識別し、サイト訪問者がタグ付けされたコンテンツをすばやく見つけられるようにする手段です。

現在のトレンドを識別するもう 1 つの手段については、「[アクティビティのトレンド](trends.md)」を参照してください。

このページでは、`Social Tag Cloud`コンポーネントダイアログの設定をドキュメントし、ユーザーエクスペリエンスを説明します。

開発者向けの詳細な情報は、[タグの重要事項](tag.md)を参照してください。

タグの作成と管理、および適用されたコンテンツタグについては、[タグ](../../help/sites-administering/tags.md)の管理を参照してください。

## Social タグクラウドの追加 {#adding-a-social-tag-cloud}

作成者モードで`Social Tag Cloud`コンポーネントをページに追加するには、コンポーネントブラウザーを使用して`Communities / Social Tag Cloud`を探し、タグクラウドが表示されるページにドラッグして配置します。

必要な情報については、[Communities Components Basics](basics.md)を参照してください。

[必要なクライアント側ライブラリ](tag.md#essentials-for-client-side)が含まれる場合、`Social Tag Cloud`コンポーネントは次のように表示されます。

![chlimage_1-303](assets/chlimage_1-303.png)

## Social タグクラウドの設定 {#configuring-social-tag-cloud}

アクセスする配置済みの`Social Tag Cloud`コンポーネントを選択し、編集ダイアログを開く`Configure`アイコンを選択します。

![chlimage_1-304](assets/chlimage_1-304.png)

「**[!UICONTROL Social タグクラウド]**」タブでは、どのタグを表示するかと、タグがアクティブリンクである場合に、検索結果を表示するページの場所を指定します。

![chlimage_1-305](assets/chlimage_1-305.png)

* **[!UICONTROL 表示する Social タグ]**&#x200B;表示する UGC タグを指定します。プルダウンオプションは、

   * `From page and child pages`
   * `All tags`

   デフォルトは`From page and child pages`です。&quot;page&quot;は、下の&#x200B;**Page**&#x200B;設定を参照します。

* **[!UICONTROL ページ]**
( 
`All tags)` ページのUGCへのパス。デフォルトは、空白の場合に現在のページになります。

* **[!UICONTROL タグにリンクがありません]**&#x200B;オンにすると、タグはタグクラウドにプレーンテキストとして表示されます。選択しない場合、タグはアクティブリンクとして表示され、タグが適用されるすべてのコンテンツが検索されます。 デフォルトはオフで、**[!UICONTROL Search Result Path]**&#x200B;の設定が必要です。

* **[!UICONTROL 検索結果]**
のパス 
`Search Result` コンポーネントが配置され、 **** Pagesettingで指定されたUGCパスを含むUGCを参照するように設定されている。

## Social タグクラウドの表示を変更する {#change-display-of-social-tag-cloud}

**Social Tag Cloud**&#x200B;の表示を編集するには、[デザインモード](../../help/sites-authoring/default-components-designmode.md)に入り、配置された`Social Tag Cloud`コンポーネントを重複がクリックして、追加のタブを含むダイアログを開きます。

「**[!UICONTROL Socialタグクラウド（デザイン）]**」タブを使用して、タグの表示方法を指定します。 タグは、単純なタグ、デフォルトの名前空間内の単一の単語、または階層的な分類のいずれかです。

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

   適用できるタグは3つあります。`Geometrixx Media (the namespace)`、`Gadgets`、`Cars`

   * チェック済み：`Cars`のみが表示されます（適用される場合）
   * オフ：`Geometrixx Media`と`Gadgets`、`Cars`が適用される場合は表示されます

   シンプルなタグはリーフタグです。

   初期設定はオフです。

* **[!UICONTROL リンクテンプレート]**&#x200B;コンポーネントの編集ダイアログでリンクが有効にされているときに、タグクラウド内にリンクを表示するために使用されるデフォルト以外のテンプレートを指定します。

* **[!UICONTROL すべてのタグに同じサイズ]**&#x200B;オンにすると、タグクラウド内のすべての単語が同じスタイルに設定されます。選択しない場合、単語のスタイルは使用方法に応じて異なります。 初期設定はオフです。

## 追加情報 {#additional-information}

詳しくは、開発者向けの[Tag Essentials](tag.md)ページを参照してください。

タグの作成と管理については、[ユーザー生成コンテンツのタグ付け](tag-ugc.md)(UGC)を参照してください。
