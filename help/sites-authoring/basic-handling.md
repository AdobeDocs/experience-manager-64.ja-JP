---
title: 基本操作
seo-title: Basic Handling
description: AEM内での移動とその基本的な使用方法に慣れる
seo-description: Get comfortable with navigating AEM and its basic usage
uuid: 12958209-6a49-41ad-8a8e-b112503d26b1
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: introduction
content-type: reference
discoiquuid: 616d42c8-2316-4c56-b89f-660903270620
exl-id: 9abef452-b435-4419-895c-083cae6cd7d2
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '2789'
ht-degree: 48%

---

# 基本操作  {#basic-handling}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

>[!NOTE]
>
>* このページでは、AEMオーサー環境を使用する際の基本操作の概要を説明します。 これは **Sites** コンソールを基礎として使用します。
>
>* 一部の機能はすべてのコンソールで使用できるわけではなく、一部のコンソールで追加機能を使用できる場合があります。 個々のコンソールとその関連機能に関する具体的な情報については、他のページで詳しく説明します。
>* AEM 全体で（特に、[コンソールを使用する](/help/sites-authoring/keyboard-shortcuts.md)場合と[ページを編集する](/help/sites-authoring/page-authoring-keyboard-shortcuts.md)場合に）、キーボードショートカットを利用できます。
>


## はじめに {#getting-started}

### タッチ対応 UI {#a-touch-enabled-ui}

AEMユーザーインターフェイスでタッチ操作が有効になりました。 タッチ対応インターフェイスを使用すると、タップ、長押し、スワイプなどのタッチジェスチャーを使用して、ソフトウェアを操作できます。これは、従来のデスクトップインターフェイスが、クリック、ダブルクリック、右クリック、マウスオーバーなどのマウス操作で動作するのとは対照的です。 ジェスチャーのみが必要なので、タッチ操作対応 UI はモバイルタブレットデバイスで完全に動作し、デスクトップでも完全な機能を備えています。

### 最初の手順 {#first-steps}

ログインするとすぐに、[ナビゲーションパネル](/help/sites-authoring/basic-handling.md#global-navigation)が表示されます。これについては、後の節で詳しく説明します。

![screen_shot_2018-03-23at102603](assets/screen_shot_2018-03-23at102603.png)

いずれかのオプションをクリックすると、それぞれのコンソールが開きます。 AEM の基本的な使用方法を適切に理解できるように、このドキュメントでは **Sites** コンソールに基づいて説明します。

「**Sites**」をクリックまたはタップして開始します。

### 製品ナビゲーション {#product-navigation}

ユーザーが最初にコンソールにアクセスするたびに、製品ナビゲーションチュートリアルが開始されます。 AEMの基本操作の概要を確認するには、少し時間を割いてクリックまたはタップします。

![chlimage_1-357](assets/chlimage_1-357.png)

クリックまたはタップ **分かった！** をクリックして、概要の次のページに進みます。 クリックまたはタップ **閉じる** または、概要ダイアログの外側をクリックまたはタップして閉じます。

オプションをオンにしない限り、概要は、次回コンソールにアクセスすると再び開始します **次回から表示しない**.

## グローバルナビゲーション {#global-navigation}

グローバルナビゲーションパネルを使用してコンソール間を移動できます。これは、画面の左上にある Adobe Experience Manager リンクをクリックまたはタップすると、全画面表示のドロップダウンとしてトリガーされます。

「**閉じる**」をクリックまたはタップすると、グローバルナビゲーションパネルが閉じて、前の場所に戻ることができます。

![screen_shot_2018-03-23at102631](assets/screen_shot_2018-03-23at102631.png)

>[!NOTE]
>
>最初にログインしたとき、 **ナビゲーション** パネル。

グローバルナビゲーションには、2 つのパネルがあり、画面の左余白にアイコンで表示されます。

* **ナビゲーション** - コンパスと、
* **ツール**  — ハンマーで表される

これらのパネルで使用できるオプションを以下に示します。

1. ナビゲーションパネル：

   ![screen_shot_2018-03-23at102603-1](assets/screen_shot_2018-03-23at102603-1.png)

   ナビゲーションでは、次のコンソールを使用できます。

<table> 
 <tbody>
  <tr>
   <td><strong>コンソール</strong></td> 
   <td><strong>目的</strong></td> 
  </tr>
  <tr>
   <td>Assets<br /> </td> 
   <td>これらのコンソールでは、画像、ビデオ、ドキュメント、オーディオファイルなどの<a href="/help/assets/assets.md">デジタルアセット</a>を読み込んで、それらを管理できます。これにより、これらのアセットは、同じ AEM インスタンス上で実行されているすべての web サイトで使用できます。 </td> 
  </tr>
  <tr>
   <td>Communities</td> 
   <td>このコンソールでは、 <a href="/help/communities/sites-console.md">コミュニティサイト</a> 対象 <a href="/help/communities/overview.md#engagement-community">エンゲージメント</a> および <a href="/help/communities/overview.md#enablement-community">実施可能</a>.</td> 
  </tr>
  <tr>
   <td>Commerce</td> 
   <td>これにより、 <a href="/help/sites-administering/ecommerce.md">コマース</a> サイト。</td> 
  </tr>
  <tr>
   <td>エクスペリエンスフラグメント </td> 
   <td>An <a href="/help/sites-authoring/experience-fragments.md">エクスペリエンスフラグメント</a> は、複数のチャネルをまたいで再利用でき、バリエーションがあるスタンドアロンエクスペリエンスで、エクスペリエンスやエクスペリエンスの一部を繰り返しコピー&amp;ペーストする手間を省きます。</td> 
  </tr>
  <tr>
   <td>Forms</td> 
   <td>このコンソールでは、 <a href="/help/forms/using/introduction-aem-forms.md">フォームとドキュメント</a>&gt;.</td> 
  </tr>
  <tr>
   <td>パーソナライズ機能</td> 
   <td>このコンソールには、 <a href="/help/sites-authoring/personalization.md">ターゲットコンテンツをオーサリングし、パーソナライズされたエクスペリエンスを提示するためのツールのフレームワーク</a>.</td> 
  </tr>
  <tr>
   <td>プロジェクト</td> 
   <td>この <a href="/help/sites-authoring/touch-ui-managing-projects.md">プロジェクトコンソールを使用して、プロジェクトに直接アクセスできます</a>. プロジェクトは仮想ダッシュボードです。これを使用してチームを結成し、チームに対してリソース、ワークフロー、タスクを提供できるので、チームメンバーは共通の目標に向かって作業できます。. <br /> </td> 
  </tr>
  <tr>
   <td>Sites</td> 
   <td>サイトコンソールでは、次の操作を実行できます。 <a href="/help/sites-authoring/author-environment-tools.md">Web サイトの作成、表示、管理</a> をAEMインスタンスで実行している。 これらのコンソールを通じて、Web サイトページの作成、編集、コピー、移動および削除、ワークフローの開始、ページの公開をおこなうことができます。<br /> </td> 
  </tr>
 </tbody>
</table>

1. ツールパネルの各オプションには、様々なサブメニューが含まれています。 この [ツールコンソール](/help/sites-administering/tools-consoles.md) ここでは、Web サイト、デジタルアセット、およびコンテンツリポジトリのその他の要素の管理に役立つ、数多くの専用ツールおよびコンソールにアクセスできます。

   ![screen_shot_2018-03-23at103406](assets/screen_shot_2018-03-23at103406.png)

## ヘッダー {#the-header}

ヘッダーは常に画面の上部に表示されます。 ヘッダーのほとんどのオプションは、システム内のどこにいても同じですが、コンテキストに固有のオプションもあります。

![screen_shot_2018-03-23at102631-1](assets/screen_shot_2018-03-23at102631-1.png)

* [グローバルナビゲーション](#global-navigation)

   コンソール間を移動するには、**Adobe Experience Manager** リンクを選択します。

   ![screen_shot_2018-03-23at103615](assets/screen_shot_2018-03-23at103615.png)

* [検索](/help/sites-authoring/search.md)

   ![](do-not-localize/screen_shot_2018-03-23at103542.png)

   [ショートカットキー](/help/sites-authoring/keyboard-shortcuts.md) `/`（スラッシュ）を使用して、任意のコンソールから検索を呼び出すこともできます。

* [ヘルプ](#accessing-help)

   ![](do-not-localize/screen_shot_2018-03-23at103547.png)

* [Marketing Cloud解](https://www.adobe.com/jp/marketing-cloud.html)

   ![](do-not-localize/screen_shot_2018-03-23at103552.png)

* [通知](/help/sites-authoring/inbox.md)

   ![](do-not-localize/screen_shot_2018-03-23at103558.png)

   このアイコンには、現在割り当てられている未完了の通知の数を示すバッジが付きます。

   >[!NOTE]
   >
   >標準のAEMは、管理者ユーザーグループに割り当てられた管理タスクで事前に読み込まれます。 詳しくは、 [インボックス — 標準の管理タスク](/help/sites-authoring/inbox.md#out-of-the-box-administrative-tasks) 」を参照してください。

* [ユーザープロパティ](/help/sites-authoring/user-properties.md)

   ![](do-not-localize/screen_shot_2018-03-23at103603.png)

* [レールセレクター](/help/sites-authoring/basic-handling.md#rail-selector)

   ![](do-not-localize/screen_shot_2018-03-23at103943.png)

   現在のコンソールに応じて表示されるオプションです。例えば、**Sites** ではコンテンツのみ（デフォルト）、タイムライン、参照を選択したり、サイドパネルをフィルタリングしたりすることができます。

   ![screen_shot_2018-03-23at104029](assets/screen_shot_2018-03-23at104029.png)

* パンくずリスト

   ![chlimage_1-358](assets/chlimage_1-358.png)

   パネルの中央に位置し、常に現在選択している項目の説明を表示するパンくずリストを使用すると、特定のコンソール内を移動できます。Sites コンソールでは、web サイトのレベル間を移動できます。

   パンくずのテキストをクリックするだけで、現在選択されている項目の階層のレベルをリストするドロップダウンが表示されます。 エントリをクリックすると、その場所にジャンプします。

   ![chlimage_1-359](assets/chlimage_1-359.png)

* Analytics の期間選択

   ![screen_shot_2018-03-23at104126](assets/screen_shot_2018-03-23at104126.png)

   これは、リスト表示でのみ使用できます。詳しくは、[リスト表示](#list-view)を参照してください。

* 「**作成**」ボタン

   ![screen_shot_2018-03-23at104301](assets/screen_shot_2018-03-23at104301.png)

   クリックすると、コンソール／コンテキストに適したオプションが表示されます。

* [表示](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources)

   ![](do-not-localize/screen_shot_2018-03-23at104310.png)

   列表示、カード表示、リスト表示、表示設定を切り替えることができます。

   ![screen_shot_2018-03-23at104504](assets/screen_shot_2018-03-23at104504.png)

## ヘルプへのアクセス {#accessing-help}

様々なヘルプリソースを使用できます。

* **コンソールツールバー**

   場所に応じて、 **ヘルプ** アイコンをクリックすると、次の適切なリソースが開きます。

   ![screen_shot_2018-03-20at121326](assets/screen_shot_2018-03-20at121326.png)

* **ナビゲーション**

   初めてシステムを操作する際に、[AEM の操作を紹介するスライドが表示されます](/help/sites-authoring/basic-handling.md#product-navigation)。

* **ページエディター**

   ページを初めて編集するときに、一連のスライドでページエディターが開きます。

   ![chlimage_1-360](assets/chlimage_1-360.png)

   コンソールに最初にアクセスしたときの[製品ナビゲーションの概要](/help/sites-authoring/basic-handling.md#product-navigation)と同様に、この概要をナビゲートします。

   このスライドをもう一度表示するには、 [**ページ情報** メニューの「**ヘルプ**](/help/sites-authoring/author-environment-tools.md#accessing-help)」を選択します。

* **ツールコンソール**

   次の **ツール** コンソールで、外部の **リソース**:

   * **ドキュメント**
Web Experience Management のドキュメントを表示します。

   * **開発者向けリソース**
開発者向けリソースおよびダウンロード
   >[!NOTE]
   >
   >コンソールでは、ホットキー `?`（疑問符）を使用して、いつでもショートカットキーの概要を確認できます。
   >
   >すべてのキーボードショートカットの概要については、次のドキュメントを参照してください。
   >
   >* [ページ編集のキーボードショートカット](/help/sites-authoring/page-authoring-keyboard-shortcuts.md)
   >* [コンソールのキーボードショートカット](/help/sites-authoring/keyboard-shortcuts.md)


## アクションツールバー {#actions-toolbar}

リソース（ページやアセットなど）を選択するたびに、様々なアクションがアイコンで示され、ツールバーに説明テキストが表示されます。 これらのアクションは、次によって決定されます。

* 現在のコンソール。
* 現在のコンテキスト。
* 自分が [選択モード](#viewing-and-selecting-resources).

ツールバーで使用できるアクションは、選択した特定の項目に対して取ることのできるアクションを反映して変化します。

[リソースを選択する](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources)方法は、表示によって異なります。

一部のウィンドウではスペースが制限されるので、使用可能なスペースよりもツールバーのほうが長くなることがよくあります。この場合は、追加のオプションが表示されます。省略記号（三点リーダーまたは「**...**」）をクリックまたはタップすると、その他のすべてのアクションを含むドロップダウンセレクターが開きます。例えば、**Sites** コンソールでページを選択すると、次のように表示されます。

![screen_shot_2018-03-23at104827](assets/screen_shot_2018-03-23at104827.png)

>[!NOTE]
>
>使用可能な個々のアイコンは、該当するコンソール、機能、シナリオに関連して記載されています。

## クイックアクション {#quick-actions}

In [カード表示](#quick-actions) 特定のアクションは、クイックアクションアイコンとして使用することも、ツールバー上で使用することもできます。 クイックアクションのアイコンは、一度に 1 つのアイテムに対してのみ使用でき、事前に選択する必要はありません。

クイックアクションは、リソースカードにマウスオーバー（デスクトップデバイス）したときに表示されます。 使用できるクイックアクションは、コンソールとコンテキストに応じて異なります。 例えば、**Sites** コンソールのページのクイックアクションを次に示します。

![screen_shot_2018-03-23at104953](assets/screen_shot_2018-03-23at104953.png)

## リソースの表示と選択 {#viewing-and-selecting-resources}

概念上、表示、ナビゲーションおよび選択はすべての表示で同じ操作ですが、使用している表示によって処理がわずかに異なります。

使用可能な任意の表示方法で、リソースを表示、ナビゲーションおよび（追加のアクションを行うために）選択できます。表示を選択するには、右上のアイコンを使用します。

* [列表示](#column-view)
* [カード表示](#card-view)

* [リスト表示](#list-view)

>[!NOTE]
>
>デフォルトでは、AEM Assetsは、UI のアセットの元のレンディションをどのビューにもサムネールとして表示しません。 管理者は、オーバーレイを使用して、オリジナルのレンディションをサムネールとしてAEM Assetsに表示するように設定できます。

### リソースの選択 {#selecting-resources}

特定のリソースの選択方法は、表示とデバイスの組み合わせによって異なります。

<table> 
 <tbody>
  <tr>
   <td> </td> 
   <td>選択</td> 
   <td>選択解除</td> 
  </tr>
  <tr>
   <td>列表示<br /> </td> 
   <td>
    <ul> 
     <li>デスクトップ：<br />サムネールをクリックする</li> 
     <li>モバイルデバイス：<br />サムネールをタップする</li> 
    </ul> </td> 
   <td>
    <ul> 
     <li>デスクトップ：<br />サムネールをクリックする</li> 
     <li>モバイルデバイス：<br />サムネールをタップする</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>カード表示<br /> </td> 
   <td>
    <ul> 
     <li>デスクトップ：<br />マウスオーバーし、チェックマークのクイックアクションを使用する</li> 
     <li>モバイルデバイス：<br />カードをタップ＆ホールドする</li> 
    </ul> </td> 
   <td>
    <ul> 
     <li>デスクトップ：<br />カードをクリックする</li> 
     <li>モバイルデバイス：<br />カードをタップする</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>リスト表示</td> 
   <td>
    <ul> 
     <li>デスクトップ：<br />サムネールをクリックする</li> 
     <li>モバイルデバイス：<br />サムネールをタップする</li> 
    </ul> </td> 
   <td>
    <ul> 
     <li>デスクトップ：<br />サムネールをクリックする</li> 
     <li>モバイルデバイス：<br />サムネールをタップする</li> 
    </ul> </td> 
  </tr>
 </tbody>
</table>

#### すべて選択解除 {#deselecting-all}

どのような場合でも、項目を選択すると、選択された項目の数がツールバーの右上に表示されます。

カウントの横にある「 X 」をクリックまたはタップすると、すべての項目の選択を解除して、選択モードを終了できます。

![screen_shot_2018-03-23at105432](assets/screen_shot_2018-03-23at105432.png)

デスクトップデバイスを使用している場合、すべての表示で、キーボードの Esc キーを押すことですべての項目を選択解除できます。

#### 選択の例 {#selecting-example}

1. 例えば、カード表示では次のようになります。

   ![screen_shot_2018-03-23at105508](assets/screen_shot_2018-03-23at105508.png)

1. リソースを選択すると、上部のヘッダーの上に[アクションツールバー](#actions-toolbar)が重なって表示され、選択したリソースで現在適用可能なアクションにアクセスできます。

   選択モードを終了するには、 **X** を右上にドラッグします。

### 列表示 {#column-view}

![screen_shot_2018-03-23at105607](assets/screen_shot_2018-03-23at105607.png)

列表示では、一連のカスケード列を通じて、コンテンツツリーを視覚的にナビゲーションできます。 この表示では、Web サイトのツリー構造を視覚化してトラバースできます。

一番左の列でリソースを選択すると、右の列に子リソースが表示されます。 右側の列でリソースを選択すると、右側の別の列に子リソースが表示されます。

* リソース名またはリソース名の右にある山形記号をタップまたはクリックすると、ツリー内を上下に移動できます。

   * リソース名と山形は、タップまたはクリックするとハイライト表示されます。

   ![chlimage_1-361](assets/chlimage_1-361.png)

   * クリック/タップされたリソースの子が、クリック/タップされたリソースの右側の列に表示されます。
   * 子を持たないリソース名をタップまたはクリックすると、その詳細が最後の列に表示されます。


* サムネールをタップまたはクリックすると、リソースが選択されます。

   * 選択すると、チェックマークがサムネールにオーバーレイ表示され、リソース名もハイライト表示されます。
   * 選択されたリソースの詳細が最後の列に表示されます。

   ![chlimage_1-362](assets/chlimage_1-362.png)

   列表示でページを選択すると、選択したページは最後の列に、次の詳細と共に表示されます。

   * ページタイトル
   * ページ名（ページの URL の一部）
   * ページの基になるテンプレート
   * 最終変更日
   * ページを最後に変更したユーザー
   * ページの言語
   * 公開ステータス


### カード表示 {#card-view}

![screen_shot_2018-03-23at105508-1](assets/screen_shot_2018-03-23at105508-1.png)

* カード表示では、現在のレベルの各項目の情報カードが表示されます。 次のような情報が提供されます。

   * ページの内容を視覚的に表現したもの。
   * ページのタイトル。
   * 重要な日付（最終編集日、最終公開日など）。
   * ページがロックされているかどうか、非表示になっているかどうか、またはライブコピーの一部であるかどうか。
   * 必要に応じて、ワークフローの一部としてアクションを実行する必要がある場合。

      * 必要なアクションを示すマーカーは、 [インボックス](/help/sites-authoring/inbox.md).

* [クイックアクション](#quick-actions) は、選択や編集などの一般的なアクションなど、このビューでも使用できます。

   ![screen_shot_2018-03-23at104953-1](assets/screen_shot_2018-03-23at104953-1.png)

* カードを（クイックアクションを回避するために慎重に）タップまたはクリックしてツリーの下位に移動したり、[ヘッダーのパンくずリスト](/help/sites-authoring/basic-handling.md#the-header)を使用して再度上位に移動したりできます。

### リスト表示 {#list-view}

![screen_shot_2018-03-23at105824](assets/screen_shot_2018-03-23at105824.png)

* リスト表示では、現在のレベルの各リソースの情報が表示されます。
* リソース名をタップまたはクリックしてツリーの下に移動したり、[ヘッダーのパンくずリスト](/help/sites-authoring/basic-handling.md#the-header)を使用して上に戻ったりできます。

* リストですべての項目を簡単に選択するには、リストの左上にあるチェックボックスを使用します。

   ![screen_shot_2018-03-23at105857](assets/screen_shot_2018-03-23at105857.png)

   * リスト内のすべての項目が選択されている場合、このチェックボックスはオンになって表示されます。

      * すべての選択を解除するには、このチェックボックスをクリックまたはタップします。
   * 一部の項目のみが選択されている場合は、マイナス記号が表示されます。

      * すべてを選択するには、チェックボックスをクリックまたはタップします。
      * すべての選択を解除するには、チェックボックスを再度クリックまたはタップします。


* 表示ボタンの下にある「**表示設定**」オプションを使用して、表示する列を選択します。 次の列を表示できます。

   * **名前**  — ページ名。ページの URL の一部であり、言語に関係なく変更されないので、多言語オーサリング環境で役立つ場合があります。
   * **変更済み**  — 最終変更日と最終変更者
   * **公開済み**  — 公開ステータス
   * **テンプレート** - ページがベースにしているテンプレート
   * **ページ分析**
   * **実訪問者数**
   * **ページ滞在時間**

   ![screen_shot_2018-03-23at105952](assets/screen_shot_2018-03-23at105952.png)

   デフォルトでは、ページの URL の一部を構成する「**名前**」列が表示されます。場合によっては、作成者が異なる言語のページにアクセスする必要があり、ページの名前（通常は変更なし）を確認することが、作成者がページの言語を知らない場合に非常に役立ちます。

* リストの各項目の右端にある縦の点線マークを使用して項目の順序を変更します。

>[!NOTE]
>
>順序を変更できるのは、`jcr:primaryType` 値が `sling:OrderedFolder` である順序付きフォルダーの内部のみです。

![screen_shot_2018-03-23at110113](assets/screen_shot_2018-03-23at110113.png)

縦の選択バーをクリックまたはタップして、項目をリストの新しい位置にドラッグします。

![screen_shot_2018-03-23at110145](assets/screen_shot_2018-03-23at110145.png)

* 「設定を表示」ダイアログを使用して、適切な列を表示することで、Analytics データを表示できます。

   ヘッダーの右側にあるフィルターオプションを使用して、過去 30 日、90 日または 365 日の Analytics データをフィルタリングできます。

   ![screen_shot_2018-03-23at110230](assets/screen_shot_2018-03-23at110230.png)

## パネルセレクター {#rail-selector}

**レールセレクター**&#x200B;は、ウィンドウの左上にあり、現在のコンソールに応じてオプションを表示します。

![screen_shot_2018-03-21at095653](assets/screen_shot_2018-03-21at095653.png)

例えば、Sites では、コンテンツのみ（デフォルト）、コンテンツツリー、タイムライン、参照を選択したり、サイドパネルをフィルタリングしたりすることができます。

コンテンツのみが選択されている場合は、パネルアイコンのみが表示されます。他のオプションが選択されている場合は、パネルアイコンの隣にオプション名が表示されます。

>[!NOTE]
>
>[キーボードショートカット](/help/sites-authoring/keyboard-shortcuts.md)を使用してパネル表示オプションをすばやく切り替えることができます。

### コンテンツツリー {#content-tree}

コンテンツツリーを使用すると、サイドパネル内のサイト階層をすばやく移動して、現在のフォルダー内のページに関する多くの情報を表示できます。

コンテンツツリーサイドパネルをリスト表示やカード表示と組み合わせると、プロジェクトの階層構造を簡単に確認でき、コンテンツツリーサイドパネルを使用してコンテンツ構造全体を簡単に移動でき、詳細なページ情報をリスト表示で表示できます。

![screen_shot_2018-03-21at100858](assets/screen_shot_2018-03-21at100858.png)

>[!NOTE]
>
>階層ビューのエントリを選択すると、矢印キーを使用して階層をすばやく移動できます。
>
>詳しくは、 [キーボードショートカット](/help/sites-authoring/keyboard-shortcuts.md) を参照してください。

### タイムライン {#timeline}

タイムラインを使用して、選択したリソースで発生したイベントを表示または開始できます。 「タイムライン」列を開くには、レールセレクターを使用します。

「タイムライン」列では、次の操作を実行できます。

* 選択した項目に関連する様々なイベントを表示します。

   * ドロップダウンリストからイベントタイプを選択できます。

      * [コメント](#TimelineAddingandViewingComments)
      * 注釈
      * アクティビティ
      * [ローンチ](/help/sites-authoring/launches.md)
      * [バージョン](/help/sites-authoring/working-with-page-versions.md)
      * [ワークフロー](/help/sites-authoring/workflows-applying.md)

         * 履歴情報が保存されないので、[一時的なワークフロー](/help/sites-developing/workflows.md#transient-workflows)は除きます
      * すべて表示


* 選択した項目に関する[コメントを追加または表示](#TimelineAddingandViewingComments)します。イベントのリストの下部に「**コメント**」ボックスが表示されます。コメントを入力して Enter キーを押すと、コメントが登録されます。コメントは「**コメント**」または「**すべて表示**」を選択すると表示されます。

* 特定のコンソールには追加機能が用意されています。例えば、Sites コンソールでは次のアクションを実行できます。

   * [バージョンを保存](/help/sites-authoring/working-with-page-versions.md)します。
   * [ワークフローを開始](/help/sites-authoring/workflows-applying.md)します。

これらのオプションには、「**コメント**」フィールドの横にある山形記号からアクセスできます。

![screen_shot_2018-03-23at110958](assets/screen_shot_2018-03-23at110958.png)

### 参照 {#references}

**参照** 選択したリソースへの接続が表示されます。 例えば、**Sites** コンソールでは、ページの[参照](/help/sites-authoring/author-environment-tools.md#references)には次が表示されます。

* [ローンチ](/help/sites-authoring/launches.md#launches-in-references-sites-console)
* [ライブコピー](/help/sites-administering/msm-livecopy-overview.md)
* [言語コピー](/help/sites-administering/tc-prep.md#seeing-the-status-of-language-roots)
* コンテンツ参照（例：参照コンポーネントが借りたコンテンツや貸したコンテンツ）

![screen_shot_2018-03-23at111122](assets/screen_shot_2018-03-23at111122.png)

### フィルター {#filter}

これを使用すると、適切な場所フィルターが既に設定された状態で[検索](/help/sites-authoring/search.md)と同じようなパネルが開き、表示するコンテンツをさらにフィルタリングできます。

![screen_shot_2018-03-23at111509](assets/screen_shot_2018-03-23at111509.png)
