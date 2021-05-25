---
title: 公開したサイトを使ってみる
seo-title: 公開したサイトを使ってみる
description: イネーブルメントのために、公開したサイトを参照する
seo-description: イネーブルメントのために、公開したサイトを参照する
uuid: 1bfefa8a-fd9c-4ca8-b2ff-add79776c8ae
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.4/COMMUNITIES
topic-tags: introduction
content-type: reference
discoiquuid: 26715b94-e2ea-4da7-a0e2-3e5a367ac1cd
exl-id: bdf91013-2136-464a-a637-a3047144ec98
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '1237'
ht-degree: 46%

---

# 公開したサイトを使ってみる {#experience-the-published-site}


**[⇐ イネーブルメントリソースの作成と割り当て](resource.md)**

## パブリッシュサーバー上の新しいサイトの参照 {#browse-to-new-site-on-publish}

新しく作成したコミュニティサイトとそのイネーブルメントリソースおよび学習パスを公開したら、イネーブルメントチュートリアルサイトを実際に使ってみることができます。

まず、サイト作成時に表示された URL を参照します。ただし、このとき参照するのはパブリッシュサーバー上の URL です。次に例を示します。

* 作成者URL = [http://localhost:4502/content/sites/enable/en.html](http://localhost:4502/content/sites/enable/en.html)
* パブリッシュURL = [http://localhost:4503/content/sites/enable/en.html](http://localhost:4503/content/sites/enable/en.html)

[デフォルトホームページを設定](enablement-create-site.md#changethedefaulthomepage)した場合は、[http://localhost:4503/](http://localhost:4503/) を参照するだけでサイトが開きます。

公開済みサイトに初めてアクセスするときは、通常、そのサイト訪問者はまだサインインしておらず、匿名です。

**http://localhost:4503/content/sites/enable/en.html**

![chlimage_1-433](assets/chlimage_1-433.png)

## 匿名のサイト訪問者 {#anonymous-site-visitor}

匿名のサイト訪問者には、この非公開のイネーブルメントコミュニティサイトのログインページがすぐに表示されます。facebookやTwitterに自己登録やログインのオプションはないことに注意してください。

このホームページには、次の4つのメニュー項目が表示されます。`Assignments, Ski Catalog, What's New`と`Discussions`の両方に割り当てられますが、サインインしない限り、何も実行できません。

>[!NOTE]
>
>サイト訪問者に自己登録を許可することなく、イネーブルメントサイトへの匿名アクセスを許可できます。\
>イネーブルメントリソースが`show in catalog`および`allow anonymous access`に設定されている場合、匿名のサイト訪問者がカタログ内のリソースを表示できます。

### JCR {#prevent-anonymous-access-on-jcr}での匿名アクセスを防ぐ

既知の制限により、jcrコンテンツとjsonを通じてコミュニティサイトのコンテンツを匿名訪問者に公開しますが、サイトのコンテンツに対して&#x200B;**[!UICONTROL 匿名アクセスを許可]**&#x200B;は無効になっています。 ただし、この動作は、Slingの制限を回避策として使用して制御できます。

コミュニティサイトのコンテンツを、匿名ユーザーがjcrコンテンツやjsonを介してアクセスするのを防ぐには、次の手順に従います。

1. AEMオーサーインスタンスで、 https://&lt;host>:&lt;port>/editor.html/content/site/&lt;sitename>.htmlに移動します。

   >[!NOTE]
   >
   >ローカライズされたサイトに移動しないでください。

1. **[!UICONTROL ページのプロパティ]**&#x200B;に移動します。

   ![page-properties-1](assets/page-properties-1.png)

1. 「**[!UICONTROL 詳細]**」タブに移動します。
1. **[!UICONTROL 認証要件]**&#x200B;を有効にします。

   ![site-authentication-1](assets/site-authentication-1.png)

1. ログインページのパスを追加します。 （例：`/content/......./GetStarted`）。
1. ページを公開します。

## 登録済みメンバー {#enrolled-member}

このエクスペリエンスは、ユーザー`Riley Taylor`と`Sidney Croft`が[作成](enablement-setup.md#publishcreateenablementmembers)で、[が&#x200B;*Ski Lessons*&#x200B;の学習パスに&#x200B;*Community Ski Class*&#x200B;グループのメンバーシップを通じて割り当てられている](resource.md#settings)に依存します。

でログイン

* `Username: riley`
* `Password: password`

ユーザープロファイルが自己登録によって作成されなかった場合は、メンバーが初めてサインインしたときにプロファイルページが表示され、必要に応じてプロファイルを確認および変更することができます。

次にメンバーがサインインしたときは、1 番目のメニュー項目のページがホームページとして表示されます。

![chlimage_1-434](assets/chlimage_1-434.png)

### 割り当て {#assignments}

割り当てページでは、各メンバーに割り当てられたすべての学習パスとイネーブルメントリソースが表示されます。

それぞれの割り当てについて、次の基本情報が表示されます。

* 割り当てのタイプ
* 新しい割り当てかどうか
* 名前
* 割り当てのタイプに関連する詳細
* 割り当ての連絡先、エキスパートおよび作成者（指定されている場合）

カード左上隅のアイコンは、割り当ての種類を示しています。道路のイメージは、含まれるイネーブルメントリソースの数を含む学習パス用です。

![chlimage_1-435](assets/chlimage_1-435.png)

「Ski Lessons」を選択すると、その学習パスで参照される 2 つのイネーブルメントリソースが表示されます。**

![chlimage_1-436](assets/chlimage_1-436.png)

「Ski Lesson 1」を選択すると、イネーブルメントリソースの詳細ページが表示されます。**

詳細ページから、メンバーは学習し、[rate](rating.md)レッスンを学習し、[comments](comments.md)を追加できます。 メンバーのアクティビティは、サイトの新機能セクションに反映されます。

イネーブルメントリソースとのインタラクションは、オーサー環境からアクセスできるレポートセクションに表示されます。

![chlimage_1-437](assets/chlimage_1-437.png)

### Ski Catalog {#ski-catalog}

Ski Catalog のページは、`Tutorial` 名前空間のタグが付けられたイネーブルメントリソースのカタログです。2つの&#x200B;*Ski Lesson*&#x200B;リソースには`Skiing`タグが付けられ、`All`または`Tutorial: Sports / Skiing`以外のタグが選択されている場合は、何も表示されません。

メンバーにイネーブルメントリソースが（直接または学習パスを通じて）割り当てられていないときも、カタログ内にあるイネーブルメントリソースを使用したり、コメントや評価を付けてフィードバックを与えることができます。

![chlimage_1-438](assets/chlimage_1-438.png)

### Discussions {#discussions}

`Enablement Tutorial`の作成元のコミュニティサイトテンプレートには、イネーブルメントリソース（[有効](enablement-create-site.md#step33asettings)）の評価とコメント付けに加えて、[フォーラム機能](functions.md#forum-function)（タイトルは`Discussions)`）が含まれます。

「`Discussions`」のリンクを選択し、トピックを投稿します。

Sidney Croft（sidney／password）としてログインおよびログインし、質問に回答してトピックをフォローします。

インラインでのモデレートに加え、トピックをソーシャルメディアで共有したり電子メールで送信するオプションがあります。

![chlimage_1-439](assets/chlimage_1-439.png)

### 新機能 {#what-s-new}

`What's New`メニュー項目は、このコミュニティサイトの構造で[アクティビティストリーム機能](functions.md#activity-stream-function)に与えられるタイトルです。

Sidneyとしてサインインしたままで、`What's New`リンクを選択してアクティビティを表示します。

![chlimage_1-440](assets/chlimage_1-440.png)

## 信頼されているコミュニティメンバー {#trusted-community-member}

このエクスペリエンスでは、` [Quinn Harper](enablement-setup.md#publishcreateenablementmembers)`に[モデレーター](enablement-create-site.md#moderation)と[リソースの連絡先](resource.md#settings)の役割が割り当てられていると想定します。

でログイン

* `Username: quinn`
* `Password: password`

サインインすると、新しいメニュー項目`Administration`が表示されます。これは、メンバーにモデレーターの役割が与えられたためです。

![chlimage_1-441](assets/chlimage_1-441.png)

ホームページは、1 番目のメニュー項目として定義されている割り当てページです。Quinnはモデレーターとイネーブルメントリソースの連絡先で、イネーブルメントリソースや学習パスに登録されていなかったので、表示するものはありません。

### 管理 {#administration}

2人の学習者（`Riley Taylor`と`Sidney Croft. By s`）がモデレートコンソールにアクセスするための`Administration`リンクを選択している場合、Quinnは[一括モデレートコンソール](moderation.md)を使用して投稿をモデレートできます。

サイドパネルのアイコンを選択すると、コミュニティコンテンツの検索に使用するフィルターの展開／折りたたみが切り替わります。

コメントカードにカーソルを合わせると、モデレートアクションが表示されます。

![chlimage_1-442](assets/chlimage_1-442.png)

## オーサー環境でのレポート {#reports-on-author}

学習者とイネーブルメントリソースに関するレポートにアクセスには、2 つの方法があります。

オーサー環境で、**コミュニティ/[リソースコンソール](resources.md)**&#x200B;に移動します。このコンソールでイネーブルメントリソースを管理し、コミュニティサイトを選択すると、次のレポートを生成できます。

* すべてのイネーブルメントリソースと学習パス
* 特定のイネーブルメントリソースまたは学習パス

**コミュニティ、[レポートコンソール](reports.md)**&#x200B;に移動し、

* イネーブルメントリソースと学習パスの割り当て
* 特定の期間のコミュニティサイトへの投稿
* 特定の期間におけるコミュニティサイトの表示（サイト訪問）

* 投稿と表示は、すべてのコンテンツまたは特定のコンテンツに対して行うことができます。

   * フォーラム
   * フォーラムトピック
   * Q&amp;A
   * Q&amp;A 質問
   * ブログ
   * ブログ記事
   * Calendar
   * カレンダーイベント

### リソースコンソール {#resources-console}

パブリッシュ環境でリソースに対しておこなわれるアクティビティやインタラクションが少ない場合は、オーサー環境でレポートを表示すると有益です。

* 作成者
* 管理者権限でログイン
* メインメニューから&#x200B;**[!UICONTROL コミュニティ/リソース]**&#x200B;に移動します。
* `Enablement Tutorial`サイトを選択します。
* すべてのリソースの概要を表示するには、`Report`アイコンを選択します。
* リソースを選択し、そのリソースに関するレポート用の`Report`アイコンを選択します。

Adobe Analytics のデータを表示するには時期尚早のようです。データが表示されるには 1 時間から 12 時間かかります。ただし、基本的なSCORMレポートは既に使用可能です。

#### Ski Lessons のリソースレポート {#ski-lessons-resource-report}

![chlimage_1-443](assets/chlimage_1-443.png)

#### Ski Lessons のユーザーレポート {#ski-lessons-user-report}

* **[!UICONTROL コミュニティ/リソース]**&#x200B;を選択します。

* カード`Enablement Tutorial`を開く
* カード`Ski Lessons`を開く
* `select Report, User Report`

![chlimage_1-444](assets/chlimage_1-444.png)

### レポートコンソール {#reports-console}

レポートコンソールでは、以下のものに関するレポートを生成できます。

* イネーブルメントコミュニティサイトの&#x200B;**割り当て**
* コミュニティサイトの&#x200B;**表示**
* コミュニティサイトの&#x200B;**投稿**

割り当てに関するレポートの場合：

* 作成者
* 管理者権限でログイン
* **[!UICONTROL コミュニティ/レポート/割り当てレポート]**&#x200B;に移動します。
* プルダウンメニューから「**[!UICONTROL サイト]**」を選択します（「`Enablement Tutorial`」を選択します）。

* **[!UICONTROL グループ]**&#x200B;を選択します（`Community Ski Class`を選択）。

* **[!UICONTROL 割り当て]**&#x200B;を選択します（`Ski Lessons`を選択）。

* 「**[!UICONTROL 生成]**」を選択します。

![chlimage_1-445](assets/chlimage_1-445.png)

ビューに関するレポートの場合：

* 作成者
* 管理者権限でログイン
* **[!UICONTROL コミュニティ/レポート/表示レポート]**&#x200B;に移動します。
* プルダウンメニューから「**[!UICONTROL サイト]**」を選択します（「`Enablement Tutorial`」を選択します）。

* 「**[!UICONTROL コンテンツタイプ]**」を選択します（「`all`」を選択）。

* **[!UICONTROL 日付範囲]**&#x200B;を選択します（`Last 7 days`を選択）。

* 「**[!UICONTROL 生成]**」を選択します。

![chlimage_1-446](assets/chlimage_1-446.png)

**[⇐ イネーブルメントリソースの作成と割り当て](resource.md)**
