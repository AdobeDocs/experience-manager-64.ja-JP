---
title: 初期サンドボックスコンテンツ
seo-title: 初期サンドボックスコンテンツ
description: コンテンツを作成
seo-description: コンテンツを作成
uuid: 9810fe47-8d1a-4238-9b9c-0cc47c63d97a
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.4/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: e8f28cd5-7950-4aab-bf62-3d4ed3d33cbd
exl-id: 171fd95d-51f6-468b-84ed-4a757dba868e
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '469'
ht-degree: 60%

---

# 初期サンドボックスコンテンツ  {#initial-sandbox-content}

ここでは、次のページを作成します。これらのすべてのページで[ページテンプレート](initial-app.md#createthepagetemplate)を使用します。

* SCF Sandbox Site。メインページの英語バージョンにリダイレクトします。

   * SCFサンドボックス — サイトの英語バージョンのメインページ

      * SCF Play — 再生するメインページの子

このチュートリアルでは[言語コピー](../../help/sites-administering/tc-prep.md)については詳しく説明しませんが、HTML ヘッダーによるユーザーの優先言語の検出をルートページに実装し、その言語の適切なメインページにリダイレクトできるように設計されています。通常は、ページのノード名に2文字の国コードを使用します（例：英語の場合は「en」、フランス語の場合は「fr」）。

## 最初のページの作成 {#create-first-pages}

[ページテンプレート](initial-app.md#createthepagetemplate)を作成したので、ここでは、/content ディレクトリで Web サイトのルートページを設定できます。

1. 標準 UI では現在、サイトを作成するためのブループリントが提供されます。このチュートリアルでは簡単なサイトを作成するので、クラシックUIが便利です。

   クラシック UI に切り替えるには、グローバルナビゲーションを選択し、「プロジェクト」アイコンの右側にマウスカーソルを合わせます。表示される&#x200B;*クラシックUIに切り替え*&#x200B;アイコンを選択します。

   ![chlimage_1-36](assets/chlimage_1-36.png)

   クラシック UI に切り替える機能は、[管理者が有効にする](../../help/sites-administering/enable-classic-ui.md)必要があります。

1. [クラシックUIのようこそページ](http://localhost:4502/welcome.html)から、「**[!UICONTROL Webサイト]**」を選択します。

   ![chlimage_1-37](assets/chlimage_1-37.png)

   または、[/siteadmin](http://localhost:4502/siteadmin) を参照して、Web サイトのクラシック UI に直接アクセスします。

1. エクスプローラーウィンドウで、「**[!UICONTROL Webサイト]**」を選択し、ツールバーで&#x200B;**[!UICONTROL 新規/新しいページ]**&#x200B;を選択します。

   **[!UICONTROL ページを作成]**&#x200B;ダイアログで、次のように入力します。

   * タイトル: `SCF Sandbox Site`
   * 名前：`an-scf-sandbox`
   * 「**[!UICONTROL An SCF Sandbox Play Template]**」を選択します。
   * 「**[!UICONTROL 作成]**」をクリックします。

   ![chlimage_1-38](assets/chlimage_1-38.png)

1. エクスプローラーウィンドウで、作成したページ`/Websites/SCF Sandbox Site`を選択し、**[!UICONTROL 新規/新しいページ]**&#x200B;をクリックします。

   * タイトル: `SCF Sandbox`
   * 名前：`en`
   * 「**An SCF Sandbox Play Template**」を選択します。
   * 「**作成**」をクリックします。

1. エクスプローラーウィンドウで、作成したページ`/Websites/SCF Sandbox Site/SCF Sandbox`を選択し、**[!UICONTROL 新規/新しいページ]**&#x200B;をクリックします。

   * タイトル: `SCF Play`
   * 名前：`play`
   * 「**[!UICONTROL An SCF Sandbox Play Template]**」を選択します。
   * 「**[!UICONTROL 作成]**」をクリックします。

1. Web サイトコンソールに Web サイトが次のように表示されます。エクスプローラペインで選択したアイテムの子ページが、管理可能な右側のペインに表示されます。

   ![chlimage_1-39](assets/chlimage_1-39.png)

   次に、Web サイトツールとテンプレートを使用して作成されたページのリポジトリビューを示します。

   ![chlimage_1-40](assets/chlimage_1-40.png)

## デザインパスの追加 {#add-the-design-path}

` [/etc/designs/an-scf-sandbox](setup-website.md#setupthedesigntreeetcdesigns)`がツールコンソールのdesignsセクションを使用して作成された場合、「

* `cq:template="/libs/wcm/core/templates/designpage"`

が定義されました。このプロパティによって、`currentDesign.getPath()` () を使用してスクリプト内のデザインアセットを参照するオプション機能が提供されます。例：

* &lt;% String favIcon = currentDesign.getPath() + &quot;/favicon.ico&quot;; %>


   * 名前：`cq:designPath`
   * 型：`String`
   * 値：`/etc/designs/an-scf-sandbox`

* 緑の`[+] Add`をクリックします。

リポジトリは次のようになります。

![chlimage_1-41](assets/chlimage_1-41.png)

* 「**[!UICONTROL すべて保存]**」をクリックします。

[ Trouble saving? Re-login! ]

>[!NOTE]
>
>cq:designPath の使用はオプションで、[clientlib の使用](develop-app.md#includeclientlibsintemplate)とは関係ありません。SCF コンポーネントでは [clientlib](client-customize.md#clientlibs-for-scf) を使用して JS および CSS が管理されるので、clientlib の使用は基本的に必須です。
