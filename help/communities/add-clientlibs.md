---
title: clientlib の追加
seo-title: Add Clientlibs
description: ClientLibraryFolder の追加
seo-description: Add a ClientLibraryFolder
uuid: cdc1d258-2011-4517-9206-dd2b5d1f7e0d
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.4/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: c84040b0-7850-4960-b676-ffa0a74c8cb2
exl-id: 9b8c3d1c-a9b1-4dde-9044-46c8f2b22c22
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '699'
ht-degree: 59%

---

# clientlib の追加 {#add-clientlibs}

## ClientLibraryFolder（clientlibs）の追加 {#add-a-clientlibraryfolder-clientlibs}

`clientlibs` という名前の ClientLibraryFolder を作成し、ここに、サイトのページをレンダリングするために使用される JS および CSS を格納します。

このクライアントライブラリに指定する `categories` プロパティの値は、clientlib をコンテンツページから直接含めたり、その他の clientlib に埋め込んだりする場合に使用される識別子です。

1. 使用 **[!UICONTROL CRXDE Lite]**、展開 `/etc/designs`

1. 右クリック `an-scf-sandbox` を選択し、 `Create Node`

   * 名前：`clientlibs`
   * 型：`cq:ClientLibraryFolder`

1. 「**[!UICONTROL OK]**」をクリックします。

![chlimage_1-220](assets/chlimage_1-220.png)

新しい **[!UICONTROL ノードの「]**&#x200B;プロパティ`clientlibs`」タブで、**`categories`** プロパティを入力します。

* 名前：**[!UICONTROL categories]**
* タイプ：**[!UICONTROL String]**
* 値：**[!UICONTROL apps.an-scf-sandbox]**
* クリック **[!UICONTROL 追加]**
* クリック **[!UICONTROL すべて保存]**

注意：categories 値の前に「apps.」を付けるのは、「所有アプリケーション」が /libs ではなく、/apps フォルダー内にあることを示すための規則です。重要：プレースホルダーを追加 `js.txt` および `css.txt` ファイル。 （正式には cq:ClientLibraryFolder ではありません。）


1. 右クリック **`/etc/designs/an-scf-sandbox/clientlibs`**
1. 選択 **[!UICONTROL ファイルを作成…]**
1. 入力 **[!UICONTROL 名前]**: `css.txt`

1. 選択 **[!UICONTROL ファイルを作成…]**
1. 入力 **[!UICONTROL 名前]**: `js.txt`

1. クリック **[!UICONTROL すべて保存]**

![chlimage_1-221](assets/chlimage_1-221.png)

css.txt および js.txt の最初の行によって、後述のファイルのリストが見つかる基本の場所が特定されます。

css.txt の内容を次のように設定します。：

```
#base=.
 style.css
```

次に、clientlibs の下に style.css という名前のファイルを作成し、コンテンツを次のように設定します。

`body {`

`background-color: #b0c4de;`

`}`

## SCF clientlib の埋め込み {#embed-scf-clientlibs}

**[!UICONTROL ノードの「]**&#x200B;プロパティ`clientlibs`」タブで、複数値の String プロパティ **[!UICONTROL embed]** を入力します。これにより、必要な [SCF コンポーネントのクライアント側ライブラリ (clientlibs)](client-customize.md#clientlibs-for-scf). このチュートリアルでは、コミュニティコンポーネントに必要な clientlib の多くを追加します。

ページごとにダウンロードされる clientlib の利点とサイズ／スピードに関する考慮事項があるので、このアプローチが実稼動サイトでの使用に適している場合もあれば、そうでない場合もある点に&#x200B;**注意してください**。

1 つのページで 1 つの機能のみを使用する場合は、&lt;% ui:includeClientLib categories=cq.social.hbs.forum&quot; %> など、その機能の完全な clientlib をページに直接含めることができます。

ここでは、それらをすべて挿入するので、オーサー clientlib である、より基本的な SCF clientlib が適しています。

* 名前：**`embed`**
* 型：**`String`**

* クリック **`Multi`**
* 値：**`cq.social.scf`**

   *&lt;enter> ダイアログがポップアップ表示されます*

   *クリック&#x200B;**[+]**各エントリの後に、次の clientlib カテゴリを追加します。*

   * **`cq.ckeditor`**
   * **`cq.social.author.hbs.comments`**
   * **`cq.social.author.hbs.forum`**
   * **`cq.social.author.hbs.rating`**
   * **`cq.social.author.hbs.reviews`**
   * **`cq.social.author.hbs.voting`**
   * 「**[!UICONTROL OK]**」をクリックします。

* クリック **[!UICONTROL すべて保存]**

![chlimage_1-222](assets/chlimage_1-222.png)

このように `/etc/designs/an-scf-sandbox/clientlibs` がリポジトリに表示されます。

![chlimage_1-223](assets/chlimage_1-223.png)

## playpage テンプレートに clientlibs を含める {#include-clientlibs-in-playpage-template}

を含めずに、 `apps.an-scf-sandbox` 必要な JavaScript とスタイルが使用できないので、ページの ClientLibraryFolder カテゴリ、SCF コンポーネントは機能しないか、スタイル設定されません。

例えば、clientlibs を挿入しなかった場合、SCF コメントコンポーネントは、スタイルが設定されていない状態で表示されます。

![chlimage_1-224](assets/chlimage_1-224.png)

apps.an-scf-sandbox clientlibs を含めると、SCF コメントコンポーネントは、スタイルが設定された状態で表示されます。

![chlimage_1-225](assets/chlimage_1-225.png)

include ステートメントは、 `<head>` セクション `<html>` スクリプト デフォルト **`foundation head.jsp`** には、オーバーレイ可能なスクリプトが含まれます。 **`headlibs.jsp`**.

**headlibs.jsp をコピーし、clientlibs を含めます。**

1. 使用 **[!UICONTROL CRXDE Lite]**&#x200B;を選択します。 **`/libs/foundation/components/page/headlibs.jsp`**
1. 右クリックして「 」を選択します。 **[!UICONTROL コピー]** （または、ツールバーから「コピー」を選択します）。
1.  **`/apps/an-scf-sandbox/components/playpage`**
1. 右クリックして「 」を選択します。 **[!UICONTROL 貼り付け]** （または、ツールバーから「貼り付け」を選択します）。
1. ダブルクリック **`headlibs.jsp`** 開ける
1. ファイルの末尾に次の行を追加します。

   **`<ui:includeClientLib categories="apps.an-scf-sandbox"/>`**

1. クリック **[!UICONTROL すべて保存]**


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


* 送信者 **[!UICONTROL CRXDE Lite]**、 [パッケージアイコン](http://localhost:4502/crx/packmgr/)
* クリック **[!UICONTROL パッケージを作成]**

   * パッケージ名: `an-scf-sandbox-minimal-pkg`
   * バージョン: `0.1`
   * グループ：&lt;デフォルトのまま>
   * 「**[!UICONTROL OK]**」をクリックします。

* 「**[!UICONTROL 編集]**」をクリックします。

   * 選択 **[!UICONTROL フィルター]** タブ

      * クリック **[!UICONTROL フィルターを追加]**
      * ルートパス： &lt;browse to=&quot;&quot; span=&quot;&quot; id=&quot;0&quot; translate=&quot;no&quot; />>`/apps/an-scf-sandbox`
      * クリック **[!UICONTROL 完了]**
      * クリック **[!UICONTROL フィルターを追加]**
      * ルートパス： &lt;browse to=&quot;&quot; span=&quot;&quot; id=&quot;0&quot; translate=&quot;no&quot; />>`/etc/designs/an-scf-sandbox`
      * クリック **[!UICONTROL 完了]**
      * クリック **[!UICONTROL フィルターを追加]**
      * ルートパス： &lt;browse to=&quot;&quot; span=&quot;&quot; id=&quot;0&quot; translate=&quot;no&quot; />>`/content/an-scf-sandbox`
      * クリック **[!UICONTROL 完了]**
   * 「**[!UICONTROL 保存]**」をクリックします。


* クリック **[!UICONTROL ビルド]**

これで、 **[!UICONTROL ダウンロード]** ディスクに保存し **[!UICONTROL パッケージをアップロード]** 他の場所では、選択 **[!UICONTROL 詳細 > レプリケート]** サンドボックスを localhost パブリッシュインスタンスにプッシュしてサンドボックスの領域を拡張するために使用します。
