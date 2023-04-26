---
title: オーサリング環境とツール
seo-title: Authoring Environment and Tools
description: AEM のオーサリング環境は、コンテンツを編成および編集するための様々なメカニズムを提供しています
seo-description: The authoring environment of AEM provides various mechanisms for organizing and editing your content
uuid: 2fe17bbf-f431-49bc-9d27-7a95f1f76252
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 4f6a525d-d291-426f-be22-d2ef92c57156
exl-id: 5bb5f984-f741-4185-acb0-ffcf7e116875
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '2124'
ht-degree: 49%

---

# オーサリング環境とツール{#authoring-the-environment-and-tools}

AEM のオーサリング環境は、コンテンツを編成および編集するための様々なメカニズムを提供しています. 提供されるツールには、様々なコンソールおよびページエディターからアクセスします。

## サイトの管理 {#managing-your-site}

この **サイト** コンソールを使用すると、ヘッダーバー、ツールバー、アクションアイコン（選択したリソースに適用）、パンくずリストおよび選択時にセカンダリレール（タイムラインや参照など）を使用して、Web サイトの移動や管理をおこなうことができます。

例えば、カード表示の場合は、次のようになります。

![chlimage_1-290](assets/chlimage_1-290.png)

## ページコンテンツの編集 {#editing-page-content}

ページエディターでページを編集できます。 次に例を示します。

`http://localhost:4502/editor.html/content/we-retail/us/en/equipment.html`

![screen_shot_2018-03-22at141536](assets/screen_shot_2018-03-22at141536.png)

>[!NOTE]
>
>初めてページを開いて編集する際に、一連のスライドで機能に関するツアーが表示されます。
>
>必要がない場合は、このツアーをスキップすることができます。このツアーは、**ページ情報**&#x200B;メニューからいつでも表示できます。

## ヘルプへのアクセス {#accessing-help}

ページの編集中、**ヘルプ**&#x200B;には次の場所からアクセスできます。

* の [**ページ情報**](/help/sites-authoring/editing-page-properties.md#page-properties) セレクター；これにより、（エディターに初めてアクセスしたときに表示される）紹介用のスライドが表示されます。
* の [設定](/help/sites-authoring/editing-content.md#edit-configure-copy-cut-delete-paste) 特定のコンポーネント用のダイアログ ( ? アイコン（ダイアログツールバー内）コンテキスト依存のヘルプが表示されます。

それ以外の[ヘルプ関連リソースは、コンソールから表示できます](/help/sites-authoring/basic-handling.md#accessing-help)。

## コンポーネントブラウザー {#components-browser}

コンポーネントブラウザーには、現在のページで使用可能なすべてのコンポーネントが表示されます。 これらは適切な場所にドラッグし、編集してコンテンツを追加できます。

コンポーネントブラウザーはサイドパネル内のタブです（[アセットブラウザー](/help/sites-authoring/author-environment-tools.md#assets-browser)と[コンテンツツリー](/help/sites-authoring/author-environment-tools.md#content-tree)も同じ場所にあります）。サイドパネルを開く（または閉じる）には、ツールバーの左上にある次のアイコンを使用します。

![](do-not-localize/screen_shot_2018-03-22at141659.png)

サイドパネルを開く際、パネルは左側からスライドして開きます ( **コンポーネント** タブ（必要に応じて）をクリックします。 開いたら、ページで使用可能なすべてのコンポーネントを閲覧できます。

実際の外観や処理は、使用しているデバイスの種類によって異なります。

>[!NOTE]
>
>モバイルデバイスは、幅が 1,024 px 未満の場合に検出されます。 これは、小さなデスクトップウィンドウの場合にも該当します。

* **モバイルデバイス ( 例：iPad)**

   コンポーネントブラウザーは、編集中のページを完全にカバーします。

   ページにコンポーネントを追加する場合は、必要なコンポーネントをタッチ&amp;ホールドして右側に移動すると、コンポーネントブラウザーが閉じてページが再度表示され、コンポーネントの配置先になります。

   ![screen_shot_2018-03-22at141752](assets/screen_shot_2018-03-22at141752.png)

* **デスクトップデバイス**

   ウィンドウの左側にコンポーネントブラウザーが開きます。

   ページにコンポーネントを追加するには、必要なコンポーネントをクリックし、必要な場所にドラッグします。

   ![screen_shot_2018-03-22at141808](assets/screen_shot_2018-03-22at141808.png)

   コンポーネントは、

   * コンポーネント名
   * コンポーネントグループ（グレー）
   * アイコンまたは省略形

      * 標準コンポーネントのアイコンはモノクロです。
      * 略語は常にコンポーネント名の最初の 2 文字です。

   コンポーネントブラウザーの上部のツールバーでは、次の操作を実行できます。

   * コンポーネントを名前でフィルターします。
   * ドロップダウンから選択して特定のグループのみを表示します。

   コンポーネントについて詳しくは、コンポーネントブラウザー内のコンポーネントの横にある情報アイコンをクリックまたはタップしてください（使用可能な場合）。

   ![screen_shot_2018-03-22at141929](assets/screen_shot_2018-03-22at141929.png)

   使用可能なコンポーネントについて詳しくは、[コンポーネントコンソール](/help/sites-authoring/default-components-console.md)を参照してください。

## アセットブラウザー {#assets-browser}

アセットブラウザーには、現在のページ上で直接使用できるすべてのアセットが表示されます。

アセットブラウザーはサイドパネル内のタブで、 [コンポーネント参照](/help/sites-authoring/author-environment-tools.md#components-browser)r および [コンテンツツリー](/help/sites-authoring/author-environment-tools.md#content-tree). サイドパネルを開く（または閉じる）には、ツールバーの左上にある次のアイコンを使用します。

![](do-not-localize/screen_shot_2018-03-22at141659-1.png)

サイドパネルを開く際、パネルは（左側から）スライドして開きます。必要に応じて「**Assets**」タブを選択します。

![](do-not-localize/screen_shot_2018-03-22at142035.png)

アセットブラウザーが開いている場合は、ページで使用可能なすべてのアセットを参照できます。 必要に応じて、無限スクロールを使用してリストを展開します。

![chlimage_1-291](assets/chlimage_1-291.png)

ページにアセットを追加するには、を選択し、必要な場所にドラッグします。 次のことが考えられます。

* 適切なタイプの既存のコンポーネント。

   * 例えば、画像タイプのアセットを画像コンポーネントにドラッグできます。

* 適切なタイプの新しいコンポーネントを作成するための段落システム内の[プレースホルダー](/help/sites-authoring/editing-content.md#component-placeholder)。

   * 例えば、画像タイプのアセットを段落システムにドラッグして、画像コンポーネントを作成できます。

>[!NOTE]
>
>これは、特定のアセットおよびコンポーネントタイプで使用できます。 詳しくは、 [アセットブラウザーを使用したコンポーネントの挿入](/help/sites-authoring/editing-content.md#inserting-a-component-using-the-assets-browser) を参照してください。

アセットブラウザーの上部のツールバーで、次の方法でアセットをフィルタリングできます。

* 名前
* パス
* アセットタイプ（画像、原稿、ドキュメント、ビデオ、ページ、段落、製品など）
* 向き（縦、横、正方形）やスタイル（カラー、モノクロ、グレースケール）などのアセットの特性

   * 特定のアセットタイプに対してのみ使用可能

実際の外観や処理は、使用しているデバイスの種類によって異なります。

>[!NOTE]
>
>モバイルデバイスは、幅が 1,024 px 未満の場合に検出されます。つまり、画面の小さいデスクトップも検出されます。

* **iPadなどのモバイルデバイス**

   アセットブラウザーは、編集中のページの上に完全に表示されます。

   ページにアセットを追加するには、必要なアセットをタッチ&amp;ホールドし、右側に移動します。アセットブラウザーが閉じてページが再度表示され、必要なコンポーネントにアセットを追加できます。

   ![screen_shot_2018-03-22at142223](assets/screen_shot_2018-03-22at142223.png)

* **デスクトップデバイス**

   アセットブラウザーがウィンドウの左側に開きます。

   ページにアセットを追加するには、目的のアセットをクリックし、必要なコンポーネントまたは場所にドラッグします。

   ![screen_shot_2018-03-22at142337](assets/screen_shot_2018-03-22at142337.png)

アセットをすぐに変更する必要がある場合は、アセット名の横にある編集アイコンをクリックすると、アセットブラウザーから直接[アセットエディター](/help/assets/managing-assets-touch-ui.md)を開始できます。

![](do-not-localize/screen_shot_2018-03-22at142448.png)

## コンテンツツリー {#content-tree}

この **コンテンツツリー** では、ページ上のすべてのコンポーネントの概要を階層で表示し、ページの構成を一目で確認できます。

コンテンツツリーはサイドパネル内のタブです（コンポーネントとアセットブラウザーも同じ場所にあります）。 サイドパネルを開く（または閉じる）には、ツールバーの左上にある次のアイコンを使用します。

![](do-not-localize/screen_shot_2018-03-22at142042.png)

サイドパネルを開く際、パネルは（左側から）スライドして開きます。必要に応じて「**コンテンツツリー**」タブを選択します。開くと、ページやテンプレートのツリービュー表示が表示され、コンテンツが階層的にどのように構造化されているかを理解しやすくなります。 さらに、複雑なページでは、ページのコンポーネント間をジャンプしやすくなります。

![screen_shot_2018-03-22at142526](assets/screen_shot_2018-03-22at142526.png)

ページは同じタイプの多くのコンポーネントで簡単に構成できるので、コンポーネントツリーには、コンポーネントタイプの名前（黒）の後に説明テキスト（グレー）が表示されます。 説明テキストは、タイトルやテキストなど、コンポーネントの共通のプロパティから取得されます。

コンポーネントタイプはユーザーの言語で表示されるのに対して、コンポーネントの説明テキストはページの言語で表示されます。

コンポーネントの横にある山形をクリックすると、そのレベルが折りたたまれたり展開されたりします。

![screen_shot_2018-03-22at142559](assets/screen_shot_2018-03-22at142559.png)

コンポーネントをクリックすると、ページエディターでそのコンポーネントがハイライト表示されます。

![screen_shot_2018-03-22at142647](assets/screen_shot_2018-03-22at142647.png)

ツリー内でクリックしたコンポーネントが編集可能な場合は、レンチアイコンが名前の右に表示されます。 このアイコンをクリックすると、コンポーネントの編集ダイアログが直接開始されます。

![](do-not-localize/screen_shot_2018-03-22at142725.png)

>[!NOTE]
>
>ページをモバイルデバイス（ブラウザーの幅が 1,024 px より小さい場合）で編集している場合、コンテンツツリーは表示されません。

## フラグメント - 関連コンテンツブラウザー {#fragments-associated-content-browser}

ページにコンテンツフラグメントが含まれている場合、[関連コンテンツのブラウザー](/help/sites-authoring/content-fragments.md#using-associated-content)にもアクセスできます。

## 参照 {#references}

**参照** 選択したページへの接続を表示します。

* ブループリント
* ローンチ
* ライブコピー
* 言語コピー
* 参照コンポーネントの使用
* 製品ページへの参照（コマース／製品コンソールから）

必要なコンソールを開いたら、必要なリソースに移動し、次を使用して「**参照**」を開きます。

![screen_shot_2018-03-22at153653](assets/screen_shot_2018-03-22at153653.png)

[必要なリソースを選択](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources)し、そのリソースに関連する参照タイプのリストを表示します。

![screen_shot_2018-03-22at153731](assets/screen_shot_2018-03-22at153731.png)

詳細は、適切な参照タイプを選択してください。 特定の状況では、特定の参照を選択すると、次のような追加のアクションを使用できます。

* 参照コンポーネントのインスタンス（例：参照元/参照先ページへ移動）
* [製品ページへの参照](/help/sites-administering/generic.md#showing-product-references)（コマース／製品コンソールから使用可能）
* [ローンチ](/help/sites-authoring/launches.md)
* [ライブコピー](/help/sites-administering/msm.md)（選択したリソースに基づくすべてのライブコピーのパスを表示）
* [ブループリント](/help/sites-administering/msm-best-practices.md)
* [言語コピー](/help/sites-administering/tc-manage.md#creating-translation-projects-using-the-references-panel)

例えば、壊れている参照は、参照コンポーネントで修正できます。

![chlimage_1-292](assets/chlimage_1-292.png)

## イベント - タイムライン {#events-timeline}

該当するリソース（例：**Sites** コンソールからのページ、**Assets** コンソールからのアセット）では、[タイムラインを使用して、選択した項目に対する最近のアクティビティを表示できます](/help/sites-authoring/basic-handling.md#timeline)。

必要なコンソールを開いたら、必要なリソースに移動し、次を使用して「**タイムライン**」を開きます。

![screen_shot_2018-03-22at153952](assets/screen_shot_2018-03-22at153952.png)

[必要なリソースを選択](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources)し、「**すべて表示**」または「**アクティビティ**」を選択すると、選択したリソースに対する最近のアクションが一覧表示されます。

![screen_shot_2018-03-22at154130](assets/screen_shot_2018-03-22at154130.png)

## ページ情報 {#page-information}

ページ情報（イコライザーアイコン）をクリックするとメニューが開き、最後の編集および最後の公開に関する詳細も表示されます。ページ（およびそのサイト）の特性に応じて、使用できるオプションの数は異なります。

![screen_shot_2018-03-22at154210](assets/screen_shot_2018-03-22at154210.png)

* [プロパティを開く](/help/sites-authoring/editing-page-properties.md)
* [ページをロールアウト](/help/sites-administering/msm.md#msm-from-the-ui)
* [ワークフローを開始](/help/sites-authoring/workflows-applying.md#starting-a-workflow-from-the-page-editor)
* [ページをロック](/help/sites-authoring/editing-content.md#locking-a-page)
* [ページを発行](/help/sites-authoring/publishing-pages.md#publishing-pages)
* [ページを非公開](/help/sites-authoring/publishing-pages.md#unpublishing-pages)
* [公開済みとして表示](/help/sites-authoring/editing-content.md#view-as-published)
* [管理画面で表示](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources)
* [ヘルプ](/help/sites-authoring/basic-handling.md#accessing-help)

例えば、必要に応じて、 **ページ情報** には次のオプションもあります。

* [ローンチを昇格](/help/sites-authoring/launches-promoting.md) （ページがローンチの場合）
* [テンプレートを編集](/help/sites-authoring/templates.md) ページが [編集可能なテンプレート](/help/sites-authoring/templates.md#editable-and-static-templates)

* [クラシック UI で開く](/help/sites-authoring/select-ui.md#switching-to-classic-ui-when-editing-a-page)（このオプションが[管理者によって有効にされている](/help/sites-administering/enable-classic-ui-editor.md)場合）

該当する場合、**ページ情報**&#x200B;から分析や推奨を確認することもできます。

## ページモード {#page-modes}

ページの編集時には様々なモードがあり、異なるアクションを行うことができます。

* [編集](/help/sites-authoring/editing-content.md)  — ページコンテンツの編集時に使用するモード。
* [レイアウト](/help/sites-authoring/responsive-layout.md) - デバイスに応じたレスポンシブレイアウトを作成および編集できます（ページがレイアウトコンテナに基づいている場合）

* [基礎モード](/help/sites-authoring/scaffolding.md) - 同じ構造を共有しながらコンテンツが異なるページを大量に作成する場合に役立ちます。
* [開発者](/help/sites-developing/developer-mode.md) - 様々なアクションを実行できます（権限が必要です）。このアクションには、ページやそのコンポーネントの技術的な詳細の検査が含まれます。

* [デザイン](/help/sites-authoring/default-components-designmode.md)  — ページで使用するコンポーネントを有効または無効にしたり、コンポーネントのデザインを設定したりできます ( ページが [静的テンプレート](/help/sites-authoring/templates.md#editable-and-static-templates)) をクリックします。

* [ターゲット設定](/help/sites-authoring/content-targeting-touch.md)  — すべてのチャネルでターゲティングと測定をおこない、コンテンツの関連性を高めます。
* [Activity Map](/help/sites-authoring/pa-using.md) - ページの分析データを表示します。

* [タイムワープ](/help/sites-authoring/working-with-page-versions.md#timewarp) ：特定の時点のページの状態を表示できます。
* [ライブコピーステータス](/help/sites-authoring/editing-content.md#live-copy-status)  — ライブコピーのステータスと継承される（または継承されない）コンポーネントの概要をすばやく確認できます。
* [プレビュー](/help/sites-authoring/editing-content.md#previewing-pages) - パブリッシュ環境とまったく同じ形式でページを表示する、またはコンテンツ内のリンクを使用して移動するために使用します。

* [注釈](/help/sites-authoring/annotations.md) - ページで注釈の追加または表示を行う場合に使用するモード。

これらのモードには右上のアイコンを使用してアクセスできます。実際のアイコンは、現在利用中のモードに合わせて変化します。

![chlimage_1-293](assets/chlimage_1-293.png)

>[!NOTE]
>
>* ページの特性によっては、一部のモードを使用できない場合があります。
>* 一部のモードにアクセスするには、適切な権限または特権が必要です。
>* モバイルデバイスでは、スペースが制限されているので、開発者モードを使用できません。
>* [キーボードショートカット](/help/sites-authoring/page-authoring-keyboard-shortcuts.md)（`Ctrl-Shift-M`）で、**プレビュー**&#x200B;と、現在選択されているモード（**編集モード**、**レイアウトモード**&#x200B;など）を切り替えることができます。
>


## パスの選択 {#path-selection}

オーサリング時に、別のリソースを選択する必要が生じる場合がよくあります（別のページまたはリソースへのリンクを定義する場合、画像を選択する場合など）。パスを簡単に選択するには、次の手順に従います。 [パスフィールド](/help/sites-authoring/author-environment-tools.md#path-fields) オファーのオートコンプリートと [パスブラウザー](/help/sites-authoring/author-environment-tools.md#path-browser) では、より堅牢な選択が可能です。

### パスフィールド {#path-fields}

ここで例として使用する例は、画像コンポーネントです。 コンポーネントの使用と編集について詳しくは、 [ページオーサリング用コンポーネント](/help/sites-authoring/default-components.md).

パスフィールドにオートコンプリート機能とルックアヘッド機能が追加され、リソースを見つけやすくなりました。 パスフィールドに入力を開始すると、入力した内容と一致するパスがAEMに表示されます。

![screen_shot_2018-03-22at154403](assets/screen_shot_2018-03-22at154403.png)

パスフィールドで「**選択ダイアログを開く**」ボタンをクリックすると、「[パスブラウザー](/help/sites-authoring/author-environment-tools.md#path-browser)」ダイアログが開き、より詳細な選択オプションが表示されます。

![](do-not-localize/screen_shot_2018-03-22at154427.png)

### パスブラウザー {#path-browser}

パスブラウザーは、サイトコンソールの[列表示](/help/sites-authoring/basic-handling.md#column-view)のように整理されており、リソースをより詳細に選択できます。

![screen_shot_2018-03-22at154521](assets/screen_shot_2018-03-22at154521.png)

リソースを選択すると、 **選択** ボタンがアクティブになります。 クリックまたはタップして選択を確定するか、 **キャンセル** を中止します。

コンテキストで複数のリソースを選択できる場合、リソースを選択すると「選択」ボタンがアクティブ化され、選択したリソースの数がウィンドウの右上に表示されます。すべての選択を解除するには、数字の横にある X をクリックします。

![chlimage_1-294](assets/chlimage_1-294.png)

パンくずリストを使用すると、リソース階層内をすばやくジャンプできます。

![chlimage_1-295](assets/chlimage_1-295.png)

ダイアログの上部にある検索フィールドは、いつでも使用できます。

![chlimage_1-296](assets/chlimage_1-296.png)

検索をクリアするには、検索フィールドの X をクリックします。

検索を絞り込むには、フィルターオプションを表示して、特定のパスに基づいて結果をフィルターできます。

![chlimage_1-297](assets/chlimage_1-297.png)

## キーボードショートカット {#keyboard-shortcuts}

様々な[キーボードショートカット](/help/sites-authoring/page-authoring-keyboard-shortcuts.md)を利用できます。
