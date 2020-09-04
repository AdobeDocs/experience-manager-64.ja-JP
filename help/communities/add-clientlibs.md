---
title: clientlib の追加
seo-title: clientlib の追加
description: ClientLibraryFolder の追加
seo-description: ClientLibraryFolder の追加
uuid: cdc1d258-2011-4517-9206-dd2b5d1f7e0d
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.4/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: c84040b0-7850-4960-b676-ffa0a74c8cb2
translation-type: tm+mt
source-git-commit: 805e4411930749ff4b6b05ea4a8b87b4f96d72fd
workflow-type: tm+mt
source-wordcount: '704'
ht-degree: 58%

---


# clientlib の追加 {#add-clientlibs}

## Add a ClientLibraryFolder (clientlibs) {#add-a-clientlibraryfolder-clientlibs}

`clientlibs` という名前の ClientLibraryFolder を作成し、ここに、サイトのページをレンダリングするために使用される JS および CSS を格納します。

このクライアントライブラリに指定する `categories` プロパティの値は、clientlib をコンテンツページから直接含めたり、その他の clientlib に埋め込んだりする場合に使用される識別子です。

1. **[!UICONTROL CRXDE Liteを使用する場合]**、展開します `/etc/designs`

1. を右クリックし、「 `an-scf-sandbox` `Create Node`

   * 名前：`clientlibs`
   * 型：`cq:ClientLibraryFolder`

1. 「**[!UICONTROL OK]**」をクリックします。

![chlimage_1-220](assets/chlimage_1-220.png)

新しい **[!UICONTROL ノードの「]**&#x200B;プロパティ`clientlibs`」タブで、**`categories`** プロパティを入力します。

* 名前：**[!UICONTROL categories]**
* タイプ：**[!UICONTROL String]**
* 値：**[!UICONTROL apps.an-scf-sandbox]**
* Click **[!UICONTROL Add]**
* Click **[!UICONTROL Save All]**

注意：categories 値の前に「apps.」を付けるのは、「所有アプリケーション」が /libs ではなく、/apps フォルダー内にあることを示すための規則です。重要：プ追加レースホルダー `js.txt` と `css.txt` ファイル （正式には、cq:ClientLibraryFolderが存在しない場合は除きます）。


1. 右クリックして **`/etc/designs/an-scf-sandbox/clientlibs`**
1. Select **[!UICONTROL Create File...]**
1. Enter **[!UICONTROL Name]**: `css.txt`

1. Select **[!UICONTROL Create File...]**
1. Enter **[!UICONTROL Name]**: `js.txt`

1. Click **[!UICONTROL Save All]**

![chlimage_1-221](assets/chlimage_1-221.png)

css.txt および js.txt の最初の行によって、後述のファイルのリストが見つかる基本の場所が特定されます。

css.txt の内容を次のように設定します。：

```
#base=.
 style.css
```

次に、clientlibsにstyle.cssという名前のファイルを作成し、内容を次のように設定します。

`body {`

`background-color: #b0c4de;`

`}`

## SCF clientlib の埋め込み {#embed-scf-clientlibs}

**[!UICONTROL ノードの「]**&#x200B;プロパティ`clientlibs`」タブで、複数値の String プロパティ **[!UICONTROL embed]** を入力します。This will embed the necessary [client-side libraries (clientlibs) for SCF components](client-customize.md#clientlibs-for-scf). このチュートリアルでは、Communitiesコンポーネントに必要なclientlibの多くを追加します。

ページごとにダウンロードされる clientlib の利点とサイズ／スピードに関する考慮事項があるので、このアプローチが実稼動サイトでの使用に適している場合もあれば、そうでない場合もある点に&#x200B;**注意してください**。

1 つのページで 1 つの機能のみを使用する場合は、&lt;% ui:includeClientLib categories=cq.social.hbs.forum&quot; %> など、その機能の完全な clientlib をページに直接含めることができます。

ここでは、それらをすべて挿入するので、オーサー clientlib である、より基本的な SCF clientlib が適しています。

* 名前：**`embed`**
* 型：**`String`**

* クリック **`Multi`**
* 値：**`cq.social.scf`**

   *&lt;enter>を指定すると、ダイアログが表示されます*

   *各エントリの&#x200B;**[後に+]**をクリックして、次のclientlibカテゴリを追加します。*

   * **`cq.ckeditor`**
   * **`cq.social.author.hbs.comments`**
   * **`cq.social.author.hbs.forum`**
   * **`cq.social.author.hbs.rating`**
   * **`cq.social.author.hbs.reviews`**
   * **`cq.social.author.hbs.voting`**
   * 「**[!UICONTROL OK]**」をクリックします。

* Click **[!UICONTROL Save All]**

![chlimage_1-222](assets/chlimage_1-222.png)

This is how `/etc/designs/an-scf-sandbox/clientlibs` should now appear in the repository:

![chlimage_1-223](assets/chlimage_1-223.png)

## playpage テンプレートに clientlibs を含める {#include-clientlibs-in-playpage-template}

Without including the `apps.an-scf-sandbox` ClientLibraryFolder category on the page, the SCF components will not be functional nor styled as the necessary Javascript(s) and style(s) will not be available.

例えば、clientlibs を挿入しなかった場合、SCF コメントコンポーネントは、スタイルが設定されていない状態で表示されます。

![chlimage_1-224](assets/chlimage_1-224.png)

apps.an-scf-sandbox clientlibs を含めると、SCF コメントコンポーネントは、スタイルが設定された状態で表示されます。

![chlimage_1-225](assets/chlimage_1-225.png)

The include statement belongs in the `<head>` section of the `<html>` script. The default **`foundation head.jsp`** includes a script that can be overlaid: **`headlibs.jsp`**.

**headlibs.jsp をコピーし、clientlibs を含めます。**

1. Using **[!UICONTROL CRXDE Lite]**, select **`/libs/foundation/components/page/headlibs.jsp`**
1. Right click and select **[!UICONTROL Copy]** (or select Copy from the tool bar)
1.  **`/apps/an-scf-sandbox/components/playpage`**
1. Right click and select **[!UICONTROL Paste]** (or select Paste from the tool bar)
1. Double click on **`headlibs.jsp`** to open it
1. ファイルの末尾に次の行を追加します。

   **`<ui:includeClientLib categories="apps.an-scf-sandbox"/>`**

1. Click **[!UICONTROL Save All]**


```xml
<%@ page session="false" %><%
%><%@include file="/libs/foundation/global.jsp" %><%
%><ui:includeClientLib categories="cq.foundation-main"/><%
%>
<cq:include script="/libs/cq/cloudserviceconfigs/components/servicelibs/servicelibs.jsp"/>
<% currentDesign.writeCssIncludes(pageContext); %>
<ui:includeClientLib categories="apps.an-scf-sandbox"/>
```

Web サイトをブラウザーに読み込み、背景が青の網掛けでないかどうかを確認します。

[http://localhost:4502/content/an-scf-sandbox/en/play.html](http://localhost:4502/content/an-scf-sandbox/en/play.html)

![chlimage_1-226](assets/chlimage_1-226.png)

## これまでの作業内容の保存 {#saving-your-work-so-far}

この時点で、必要最低限のサンドボックスが作成されているので、パッケージとして保存します。保存しておくと、操作中にリポジトリが破損してもう一度やり直したい場合に、サーバーの電源をオフにし、フォルダー crx-quickstart/ の名前変更または削除をおこなった後、サーバーの電源をオンにし、ここで保存したパッケージをアップロードしてインストールすることができます。つまり、これらの最も基本的な手順を繰り返さなくて済みます。

すぐに操作してみたい場合は、[サンプルページの作成](create-sample-page.md)チュートリアルにこのパッケージがあります。

パッケージを作成するには：


* **[!UICONTROL CRXDE Liteから]**、 [パッケージアイコンをクリックします](http://localhost:4502/crx/packmgr/)
* Click **[!UICONTROL Create Package]**

   * パッケージ名: `an-scf-sandbox-minimal-pkg`
   * バージョン: `0.1`
   * グループ：&lt;デフォルトのまま>
   * 「**[!UICONTROL OK]**」をクリックします。

* 「**[!UICONTROL 編集]**」をクリックします。

   * Select **[!UICONTROL Filters]** tab

      * Click **[!UICONTROL Add filter]**
      * Root Path: &lt;browse to `/apps/an-scf-sandbox`>
      * Click **[!UICONTROL Done]**
      * Click **[!UICONTROL Add filter]**
      * Root Path: &lt;browse to `/etc/designs/an-scf-sandbox`>
      * Click **[!UICONTROL Done]**
      * Click **[!UICONTROL Add filter]**
      * Root Path: &lt;browse to `/content/an-scf-sandbox`>
      * Click **[!UICONTROL Done]**
   * 「**[!UICONTROL 保存]**」をクリックします。


* Click **[!UICONTROL Build]**

Now you can select **[!UICONTROL Download]** to save it to disk and **[!UICONTROL Upload Package]** elsewhere, as well as select **[!UICONTROL More > Replicate]** in order to push the sandbox to a localhost publish instance to expand the realm of your sandbox.
