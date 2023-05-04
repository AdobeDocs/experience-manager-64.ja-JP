---
title: Social タグクラウドの使用
seo-title: Using Social Tag Cloud
description: Social タグクラウドコンポーネントをページに追加する
seo-description: Adding a Social Tag Cloud component to a page
uuid: 8c400030-976c-457a-bb5f-e473909647a9
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.4/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 23a5a65e-774d-4789-9659-09e8be0c2bcd
exl-id: 3f55a02c-2733-4f69-8112-7c6c4c98938c
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '594'
ht-degree: 7%

---

# Social タグクラウドの使用 {#using-social-tag-cloud}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

## はじめに {#introduction}

この `Social Tag Cloud` コンポーネントは、コンテンツの投稿時にコミュニティメンバーが適用したタグをハイライトします。 これは、トレンドトピックを識別し、サイト訪問者がタグ付きコンテンツをすばやく見つけられるようにする手段です。

現在のトレンドを識別する別の方法として、 [アクティビティのトレンド](trends.md).

このページでは、 `Social Tag Cloud` コンポーネントダイアログの設定およびユーザーエクスペリエンスについて説明します。

開発者向けの詳細は、 [タグの基本事項](tag.md).

タグの作成および管理や、タグが適用されるコンテンツについては、[タグの管理](../../help/sites-administering/tags.md)を参照してください。

## Social タグクラウドの追加 {#adding-a-social-tag-cloud}

を追加するには、以下を実行します。 `Social Tag Cloud` コンポーネントをオーサリングモードでページに追加する場合は、コンポーネントブラウザーを使用して `Communities / Social Tag Cloud` をクリックし、ページ上のタグクラウドが表示される場所にドラッグします。

必要な情報については、 [コミュニティコンポーネントの基本](basics.md).

次の場合に [必要なクライアント側ライブラリ](tag.md#essentials-for-client-side) が含まれる場合、この方法で `Social Tag Cloud` コンポーネントが表示されます。

![chlimage_1-303](assets/chlimage_1-303.png)

## Social タグクラウドの設定 {#configuring-social-tag-cloud}

配置された `Social Tag Cloud` アクセスして選択するコンポーネント `Configure` 編集ダイアログを開くアイコン。

![chlimage_1-304](assets/chlimage_1-304.png)

以下 **[!UICONTROL Social タグクラウド]** タブで、表示するタグを指定し、タグがアクティブなリンクの場合は検索結果のページの場所を指定します。

![chlimage_1-305](assets/chlimage_1-305.png)

* **[!UICONTROL 表示する Social タグ]**
表示する UGC タグを指定します。 プルダウンオプションは次のとおりです。

   * `From page and child pages`
   * `All tags`

   デフォルトはです。 `From page and child pages`(「page」は **ページ** を設定します。

* **[!UICONTROL ページ]**
( そうでない場合は必須 
`All tags)` ページの UGC へのパス。 空白の場合、初期設定は現在のページです。

* **[!UICONTROL タグにリンクがありません]**
オンにすると、タグはプレーンテキストとしてタグクラウドに表示されます。 オフにすると、タグは、そのタグが適用されるすべてのコンテンツを検索するアクティブなリンクとして表示されます。 デフォルトはオフで、に必要な **[!UICONTROL 検索結果のパス]** を設定します。

* **[!UICONTROL 検索結果のパス]**
ページのパス。 
`Search Result` コンポーネントが配置され、 **ページ** 設定。

## Social タグクラウドの表示を変更 {#change-display-of-social-tag-cloud}

表示を編集するには **Social タグクラウド**&#x200B;を入力して、 [デザインモード](../../help/sites-authoring/default-components-designmode.md) そして、配置された `Social Tag Cloud` 追加のタブを含むダイアログを開くコンポーネント。

の使用 **[!UICONTROL Social タグクラウド（デザイン）]** タブで、タグの表示方法を指定します。 タグは、単純なタグ、デフォルト名前空間の単一の単語、階層的な分類のいずれかになります。

![chlimage_1-306](assets/chlimage_1-306.png)

* **[!UICONTROL 完全なタイトルパスを表示]**
オンにすると、適用された各タグの親タグと名前空間のタイトルが表示されます。

   次に例を示します。

   * チェック済み: `Geometrixx Media: Gadgets / Cars`
   * 未チェック: `Cars`

   単純なタグには違いはありません。

   初期設定はオフです。

* **[!UICONTROL リーフタグのみを表示]**
オンにすると、他のタグを含まない、適用されたタグのみが表示されます。

   例えば、タグ ID が

   `Geometrixx Media: Gadgets / Cars`

   次の 3 つのタグを適用できます。 `Geometrixx Media (the namespace)`, `Gadgets`、および `Cars`

   * チェック済み：のみ `Cars` 適用される場合は、表示されます
   * オフ： `Geometrixx Media` および `Gadgets`同様に `Cars` 適用される場合は、表示されます

   単純なタグはリーフタグです。

   初期設定はオフです。

* **[!UICONTROL リンクテンプレート]**
コンポーネント編集ダイアログでリンクを有効にした場合、タグクラウドにリンクを表示するために使用される、デフォルト以外のテンプレートです。

* **[!UICONTROL すべてのタグに同じサイズ]**
オンにすると、タグクラウド内のすべての単語に同じスタイルが設定されます。 オフにすると、単語のスタイルは使用方法に応じて異なります。 初期設定はオフです。

## 追加情報 {#additional-information}

詳しくは、 [タグの基本事項](tag.md) 開発者向けのページ

詳しくは、 [ユーザー生成コンテンツのタグ付け](tag-ugc.md) (UGC) を参照してください。
