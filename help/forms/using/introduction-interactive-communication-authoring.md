---
title: インタラクティブ通信オーサリング UI の概要
seo-title: インタラクティブ通信を作成するための各種ユーザーインターフェイス要素の概要
description: インタラクティブ通信を作成するための各種ユーザーインターフェイス要素の概要
seo-description: インタラクティブ通信を作成するための各種ユーザーインターフェイス要素の概要
uuid: 4e301b9a-76a1-4beb-9d67-dbd0a3bdd2e4
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: interactive-communications
discoiquuid: 565bfb42-6099-49f4-83ba-b1f0c129aab7
translation-type: tm+mt
source-git-commit: de440f57091d814a0a7ff48e9a0383c5415a0a5b
workflow-type: tm+mt
source-wordcount: '1315'
ht-degree: 47%

---


# インタラクティブ通信オーサリング UI の概要 {#introduction-to-interactive-communication-authoring-ui}

インタラクティブ通信を作成するための各種ユーザーインターフェイス要素の概要

The user interface for authoring [Interactive Communication](/help/forms/using/interactive-communications-overview.md) is intuitive and provides the following for authoring print and web channel of the Interactive Communication:

* WYSIWYG ドラッグアンドドロップドキュメントエディター
* アセットの統合リポジトリ — サーバーにアップロードされ、サーバー上で作成されたアセットは、Interactive Communicationオーサリングインターフェイスのアセットブラウザーで使用できます。

[新しいインタラクティブ通信の作成または既存のインタラクティブ通信の編集](/help/forms/using/create-interactive-communication.md)を行う場合は、以下のユーザーインターフェイス要素を使用します。

* [サイドバー](#sidebar)
* [ページツールバー](#page-toolbar)

* [コンポーネントのツールバー](#component-toolbar)
* コンテンツ領域

![インタラクティブ通信オーサリングユーザーインターフェイス](assets/form-editor.png)

**A.** Sidebar **B.** Page toolbar **C.** C. Content領域

## サイドバー {#sidebar}

![サイドバー](assets/sidebar-comps.png)

[クリックして拡大](assets/sidebar-comps-1.png)

**A.** チャネルブラウザ **B.** コンテンツブラウザC. **コンテンツブラウザ** C.プロパティD.アセットブラウザD.アセットブラウザE.コンポーネントF **************** ブラウザDataData Data Sources G.ブラウザG.コンテンツブラウザG.マスター

サイドバーには、以下のブラウザーが用意されています。

* **チャネルブラウザー**

   チャネルブラウザーにより、インタラクティブ通信の印刷チャネルと Web チャネルを切り替えることができます。チャネルブラウザーで選択したチャネルに基づいて、コンテンツブラウザーやコンポーネントブラウザーなどのブラウザーに対応するオプションが表示されます。

* **コンテンツブラウザー**

   コンテンツブラウザでは、選択したチャネルのドキュメントのオブジェクト階層を確認できます。 作成者は、ドキュメントオブジェクトツリーで目的の要素をタップして、特定のコンポーネントに移動することができます。作成者は、Web チャネルでオブジェクトを検索したり、ドキュメントオブジェクトツリーでオブジェクトの配置を変更したりすることができます。

* **プロパティブラウザー**

   コンポーネントのプロパティを編集できます。 表示されるプロパティは、コンポーネントによって異なります。例えば、ドキュメントコンテナのプロパティを表示するには：

   コンポーネントを選択し、 ![フィールドレベル](assets/field-level.png) / **ドキュメントコンテナ**&#x200B;をタップし、 ![](assets/cmppr.png)cmpprをタップします。

* **アセットブラウザー**

   レイアウトフラグメント、画像、ドキュメント、ページ、ビデオなど、様々なタイプのコンテンツを分類します。 作成者は、アセットをインタラクティブコミュニケーションにドラッグ&amp;ドロップできます。

* **コンポーネントブラウザー**

   ドキュメントの印刷チャネルやWebサーバーを作成するために使用できるコンポーネントが含まれます。 コンポーネントをインタラクティブ通信にドラッグして要素を追加し、必要に応じて追加した要素を設定できます。 以下の表に、印刷チャネルと Web チャネルについてコンポーネントブラウザーに表示されるコンポーネントを示します。

| **コンポーネント** | **印刷チャネル** | **Web チャネル** | **機能** |
|---|---|---|---|
| グラフ | ✓ | ✓ | インタラクティブ通信で使用できるグラフを追加して、フォームデータモデルのコレクションアイテムから取得された 2 次元のデータを視覚的に表現します。 |
| ドキュメントフラグメント | ✓ | ✓ | 再利用可能なコンポーネント、テキスト、リスト、または条件をインタラクティブコミュニケーションに追加できます。 インタラクティブ通信に追加する再利用可能なコンポーネントは、フォームデータモデルベースのコンポーネントでも、フォームデータモデルなしのコンポーネントでもかまいません。 |
| 画像 | ✓ | ✓ | 画像を挿入できるようにします。。 |
| パネル | - | ✓ | パネルコンポーネントは、他のコンポーネントをグループ化するためのプレースホルダーです。パネルコンポーネントにより、インタラクティブ通信内でのコンポーネントグループの配置方法が制御されます。パネルコンポーネントを使用して、エンドユーザーが繰り返し使用できるコンポーネントグループ（学歴を入力するための複数のエントリなど）を作成することもできます。また、複数のタブを持つ対話型通信のタブにそれぞれパネルを使用することをお勧めします。 |
| テーブル | &amp;ast; | ✓ | 行と列のデータを整理するためのテーブルを追加することができます。 |
| ターゲット領域 | &amp;ast;&amp;ast; | ✓ | Web チャネル固有のコンポーネントを整理するためのターゲット領域を、その Web チャネルに挿入します。 |
| テキスト | - | ✓ | インタラクティブ通信の Web チャネルにテキストを追加します。追加されたテキストでフォームデータオブジェクトを使用すると、動的なコンテンツを作成することができます。 |

&amp;ast; 表を追加するには、印刷チャネルのレイアウトフラグメントを使用します。

&amp;ast;&amp;ast; 印刷チャネルでは、ターゲット領域はXDP/印刷テンプレートにあらかじめ定義されています。 インタラクティブ通信オーサリング UI を使用して新しいターゲット領域を追加することはできません。

* **データソースブラウザー**

   データソースブラウザには、対話型通信の作成時に選択したフォームデータモデルで使用可能なデータソースが表示されます。

### コンポーネントを操作する場合のキーポイント {#key-points-for-working-with-components}

インタラクティブ通信のコンポーネントを操作する場合のキーポイントを以下に示します。

* 各コンポーネントには、そのコンポーネントの外観と機能をコントロールするプロパティが関連付けられています。To configure the properties of a component, tap the component and tap ![cmppr](assets/cmppr.png) to open the component properties in the Properties browser.
* コンポーネントは要素名で識別されます。When you tap ![cmppr](assets/cmppr.png), you can change the name of the component by changing the Element Name field value in the properties browser. 要素名フィールドに使用できるのは、英字、数字、ハイフン（-）、およびアンダースコア（_）のみです。その他の特殊文字は使用できません。また、要素名は英字で始まる必要があります。
* インタラクティブ通信にタイトルが表示されている限り、プロパティブラウザーを開かずに、エディター内でインラインのインタラクティブ通信コンポーネントのTitleプロパティを変更できます。 この作業を行うには：

   1. 「タイトル」プロパティが設定されていて、「タイトルを非表示」プロパティが無効になっているコンポーネントをタップして選択します。
   1. タイトルを編集可能にするには、 ![aem_6_3_edit](assets/aem_6_3_edit.png) をタップします。
   1. タイトルを変更し、Return キーをタップするかコンポーネント以外の場所をタップして、変更内容を保存します。変更を破棄するには、Escキーをタップします。

## コンポーネントのツールバー {#component-toolbar}

![](do-not-localize/toolbar.png)

コンポーネントを選択すると、そのコンポーネントを操作するためのツールバーが表示されます。切り取り、貼りつけ、移動、およびコンポーネントのプロパティを指定するオプションを使用することができます。次のオプションがあります。

A. **設定**：「**設定**」をタップすると、サイドバーにコンポーネントの各種プロパティが表示されます。

B. **Edit Rules**: When you tap Edit Rules, Rule Editor appears in which you can edit and create rules for the selected component. ルールエディタでは、他のフォームオブジェクト（コンポーネント）を選択したり、これらのフォームオブジェクトのルールを編集/作成したりすることもできます。

C. **Copy**: You can use the copy option to copy a component and paste it in other places in the Interactive Communication.

D. **Cut**: You can use the cut option to move a component from one place to another in the Interactive Communication.

E. **Delete**: Lets you delete the component from the Interactive Communication.

F. **Insert Component**: Lets you insert a component above the selected component.

G. **Paste**: Lets you paste the component you cut or copied using the options described above.

H. **Group**: Lets you select multiple components if you want to cut, copy, or paste more than one component together.

I. **親**：コンポーネントの親を選択します。

J. **More**: Provides more options to work with the selected component.

* SOM 式を表示（パネルのみ）
* パネル内のオブジェクトをグループ化（パネルのみ）
* フラグメントを編集（フラグメントのみ）
* パネルをフラグメントとして保存（パネルのみ）
* 子パネルを追加（パネルのみ）
* パネルツールバーを追加（パネルのみ）
* 置換（パネル以外）

## ページツールバー {#page-toolbar}

上部のページツールバーには、対話型通信をプレビューし、そのプロパティを変更するためのオプションが用意されています。 インタラクティブコミュニケーションの作成時にプレビューを設定し、それに応じて変更を加えることができます。 ページのツールバーには、以下の項目が表示されます。

* Toggle Side Panel ![toggle-side-panel](assets/toggle-side-panel.png): Lets you show or hide Sidebar.
* Page information ![pageinformationad](assets/pageinformationad.png): Lets you view page properties.
* Emulator ![ruler](assets/ruler.png): Lets you emulate the look of your Interactive Communication for different display sizes such as tablets and phones.
* 編集： 次のような他のモードを選択できます。 編集、スタイル、開発者、デザインを参照してください。

   * 編集： 対話型通信とそのコンポーネントのプロパティを編集できます。 例えば、コンポーネントの追加、画像の削除、必須フィールドの指定などを行うことができます。
   * スタイル：このモードでは、インタラクティブ通信のコンポーネントの外観を調整することができます。例えば、スタイルモードでパネルを選択して、パネルの背景色を指定することができます。
   * 開発者： 開発者は次のことができます。

      * 対話型通信の構成要素を見つけ出します。
      * エラーが発生したタイミングと場所を特定し、問題を修正する。
   * ターゲット: サイドバーに表示されていないカスタムコンポーネントまたはあらかじめ用意されているコンポーネントを有効または無効にできます。


* プレビュー: Interactive Communicationを公開したときの外観をプレビューできます。

