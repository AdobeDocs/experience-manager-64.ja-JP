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
exl-id: 9b8c3d1c-a9b1-4dde-9044-46c8f2b22c22
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '704'
ht-degree: 58%

---

# clientlib の追加  {#add-clientlibs}

## ClientLibraryFolder(clientlibs)を追加します。 {#add-a-clientlibraryfolder-clientlibs}

`clientlibs` という名前の ClientLibraryFolder を作成し、ここに、サイトのページをレンダリングするために使用される JS および CSS を格納します。

このクライアントライブラリに指定する `categories` プロパティの値は、clientlib をコンテンツページから直接含めたり、その他の clientlib に埋め込んだりする場合に使用される識別子です。

1. **[!UICONTROL CRXDE Lite]**&#x200B;を使用して、`/etc/designs`を展開します。

1. `an-scf-sandbox`を右クリックし、`Create Node`を選択します。

   * 名前：`clientlibs`
   * 型：`cq:ClientLibraryFolder`

1. 「**[!UICONTROL OK]**」をクリックします。

![chlimage_1-220](assets/chlimage_1-220.png)

新しい **[!UICONTROL ノードの「]**&#x200B;プロパティ`clientlibs`」タブで、**`categories`** プロパティを入力します。

* 名前：**[!UICONTROL categories]**
* タイプ：**[!UICONTROL String]**
* 値：**[!UICONTROL apps.an-scf-sandbox]**
* 「**[!UICONTROL 追加]**」をクリックします。
* 「**[!UICONTROL すべて保存]**」をクリックします。

注意：categories 値の前に「apps.」を付けるのは、「所有アプリケーション」が /libs ではなく、/apps フォルダー内にあることを示すための規則です。重要：プレースホルダー`js.txt`と`css.txt`ファイルを追加します。 （公式にはcq:ClientLibraryFolderが存在しない場合は除きます）。


1. **`/etc/designs/an-scf-sandbox/clientlibs`**&#x200B;を右クリック
1. 「**[!UICONTROL ファイルを作成…」を選択します。]**
1. **[!UICONTROL 名前]**&#x200B;を入力：`css.txt`

1. 「**[!UICONTROL ファイルを作成…」を選択します。]**
1. **[!UICONTROL 名前]**&#x200B;を入力：`js.txt`

1. 「**[!UICONTROL すべて保存]**」をクリックします。

![chlimage_1-221](assets/chlimage_1-221.png)

css.txt および js.txt の最初の行によって、後述のファイルのリストが見つかる基本の場所が特定されます。

css.txt の内容を次のように設定します。：

```
#base=.
 style.css
```

次に、clientlibsの下にstyle.cssという名前のファイルを作成し、コンテンツを次のように設定します。

`body {`

`background-color: #b0c4de;`

`}`

## SCF clientlib の埋め込み {#embed-scf-clientlibs}

**[!UICONTROL ノードの「]**&#x200B;プロパティ`clientlibs`」タブで、複数値の String プロパティ **[!UICONTROL embed]** を入力します。これにより、SCFコンポーネント](client-customize.md#clientlibs-for-scf)に必要な[クライアント側ライブラリ(clientlibs)が埋め込まれます。 このチュートリアルでは、コミュニティコンポーネントに必要なクライアントライブラリの多くを追加します。

ページごとにダウンロードされる clientlib の利点とサイズ／スピードに関する考慮事項があるので、このアプローチが実稼動サイトでの使用に適している場合もあれば、そうでない場合もある点に&#x200B;**注意してください**。

1 つのページで 1 つの機能のみを使用する場合は、&lt;% ui:includeClientLib categories=cq.social.hbs.forum&quot; %> など、その機能の完全な clientlib をページに直接含めることができます。

ここでは、それらをすべて挿入するので、オーサー clientlib である、より基本的な SCF clientlib が適しています。

* 名前：**`embed`**
* 型：**`String`**

* クリック **`Multi`**
* 値：**`cq.social.scf`**

   *&lt;enter> ダイアログが表示されます*

   *各エントリ&#x200B;**[の後に「+]**」をクリックして、次のクライアントライブラリカテゴリを追加します。*

   * **`cq.ckeditor`**
   * **`cq.social.author.hbs.comments`**
   * **`cq.social.author.hbs.forum`**
   * **`cq.social.author.hbs.rating`**
   * **`cq.social.author.hbs.reviews`**
   * **`cq.social.author.hbs.voting`**
   * 「**[!UICONTROL OK]**」をクリックします。

* 「**[!UICONTROL すべて保存]**」をクリックします。

![chlimage_1-222](assets/chlimage_1-222.png)

`/etc/designs/an-scf-sandbox/clientlibs`は次のようにリポジトリに表示されます。

![chlimage_1-223](assets/chlimage_1-223.png)

## playpage テンプレートに clientlibs を含める {#include-clientlibs-in-playpage-template}

`apps.an-scf-sandbox` ClientLibraryFolderカテゴリをページに含めないと、SCFコンポーネントは機能しなくなり、スタイルも設定されません。必要なJavaScriptやスタイルは使用できなくなります。

例えば、clientlibs を挿入しなかった場合、SCF コメントコンポーネントは、スタイルが設定されていない状態で表示されます。

![chlimage_1-224](assets/chlimage_1-224.png)

apps.an-scf-sandbox clientlibs を含めると、SCF コメントコンポーネントは、スタイルが設定された状態で表示されます。

![chlimage_1-225](assets/chlimage_1-225.png)

includeステートメントは、`<html>`スクリプトの`<head>`セクションに属しています。 デフォルトの&#x200B;**`foundation head.jsp`**&#x200B;には、オーバーレイ可能なスクリプトが含まれています。**`headlibs.jsp`**.

**headlibs.jsp をコピーし、clientlibs を含めます。**

1. **[!UICONTROL CRXDE Lite]**&#x200B;を使用して、**`/libs/foundation/components/page/headlibs.jsp`**&#x200B;を選択します。
1. 右クリックし、「**[!UICONTROL コピー]**」を選択します（またはツールバーの「コピー」を選択します）。
1.  **`/apps/an-scf-sandbox/components/playpage`**
1. 右クリックし、「**[!UICONTROL 貼り付け]**」を選択します（またはツールバーの「貼り付け」を選択します）。
1. **`headlibs.jsp`**&#x200B;をダブルクリックして開きます。
1. ファイルの末尾に次の行を追加します。

   **`<ui:includeClientLib categories="apps.an-scf-sandbox"/>`**

1. 「**[!UICONTROL すべて保存]**」をクリックします。


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


* **[!UICONTROL CRXDE Lite]**&#x200B;で、[パッケージアイコン](http://localhost:4502/crx/packmgr/)をクリックします。
* 「**[!UICONTROL パッケージを作成]**」をクリックします。

   * パッケージ名: `an-scf-sandbox-minimal-pkg`
   * バージョン: `0.1`
   * グループ：&lt;デフォルトのまま>
   * 「**[!UICONTROL OK]**」をクリックします。

* 「**[!UICONTROL 編集]**」をクリックします。

   * 「**[!UICONTROL フィルター]**」タブを選択します。

      * 「**[!UICONTROL フィルターを追加]**」をクリックします。
      * ルートパス：&lt;`/apps/an-scf-sandbox`を参照します。
      * 「**[!UICONTROL 完了]**」をクリックします。
      * 「**[!UICONTROL フィルターを追加]**」をクリックします。
      * ルートパス：&lt;`/etc/designs/an-scf-sandbox`を参照します。
      * 「**[!UICONTROL 完了]**」をクリックします。
      * 「**[!UICONTROL フィルターを追加]**」をクリックします。
      * ルートパス：&lt;`/content/an-scf-sandbox`を参照します。
      * 「**[!UICONTROL 完了]**」をクリックします。
   * 「**[!UICONTROL 保存]**」をクリックします。


* 「**[!UICONTROL ビルド]**」をクリックします。

これで、**[!UICONTROL ダウンロード]**&#x200B;を選択してディスクに保存し、**[!UICONTROL パッケージ]**&#x200B;を別の場所にアップロードし、**[!UICONTROL 詳細>レプリケート]**&#x200B;を選択してサンドボックスの領域を拡張できます。
