---
title: 公開したサイトを使ってみる
seo-title: Experience the Published Site
description: イネーブルメント用に公開済みサイトを参照します。
seo-description: Browse to a published site for enablement
uuid: 1bfefa8a-fd9c-4ca8-b2ff-add79776c8ae
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.4/COMMUNITIES
topic-tags: introduction
content-type: reference
discoiquuid: 26715b94-e2ea-4da7-a0e2-3e5a367ac1cd
exl-id: bdf91013-2136-464a-a637-a3047144ec98
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '1262'
ht-degree: 5%

---

# 公開したサイトを使ってみる {#experience-the-published-site}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).


**[⇐ イネーブルメントリソースの作成と割り当て](resource.md)**

## 公開で新しいサイトを参照 {#browse-to-new-site-on-publish}

新しく作成したコミュニティサイトとそのイネーブルメントリソースおよび学習パスが公開されたので、イネーブルメントチュートリアルサイトを体験することができます。

まず、サイトの作成時に表示された URL を参照します。ただし、パブリッシュサーバー上に表示されます ( 例：

* author URL = [http://localhost:4502/content/sites/enable/en.html](http://localhost:4502/content/sites/enable/en.html)
* パブリッシュ URL = [http://localhost:4503/content/sites/enable/en.html](http://localhost:4503/content/sites/enable/en.html)

この [デフォルトのホームページが設定されました](enablement-create-site.md#changethedefaulthomepage)を選択し、 [http://localhost:4503/](http://localhost:4503/) はサイトを起動する必要があります。

公開されたサイトに初めてアクセスした場合、通常、サイト訪問者はまだサインインしておらず、匿名になります。

**http://localhost:4503/content/sites/enable/en.html**

![chlimage_1-433](assets/chlimage_1-433.png)

## 匿名のサイト訪問者 {#anonymous-site-visitor}

匿名のサイト訪問者には、このプライベートイネーブルメントコミュニティサイトのログインページがすぐに表示されます。 facebookまたはTwitterに自己登録したり、ログインしたりするオプションはありません。

このホームページには、次の 4 つのメニュー項目が表示されます。 `Assignments, Ski Catalog, What's New` および `Discussions`にログインしない限り、到達できないものはありません。

>[!NOTE]
>
>サイト訪問者に自己登録を許可することなく、イネーブルメントサイトへの匿名アクセスを許可できます。\
>イネーブルメントリソースが `show in catalog` および `allow anonymous access`を使用すると、匿名のサイト訪問者がカタログ内のリソースを表示できるようになります。

### JCR での匿名アクセスの防止 {#prevent-anonymous-access-on-jcr}

ただし、既知の制限により、コミュニティサイトコンテンツは jcr コンテンツと json を通じて匿名の訪問者に公開されます。 **[!UICONTROL 匿名アクセスを許可]** はサイトのコンテンツに対して無効です。 ただし、この動作は、Sling の制限を回避策として使用して制御できます。

jcr コンテンツと json を介した匿名ユーザーによるアクセスからコミュニティサイトのコンテンツを保護するには、次の手順に従います。

1. AEM オーサーインスタンスで、 https://に移動します。&lt;host>:&lt;port>/editor.html/content/site/&lt;sitename>.html

   >[!NOTE]
   >
   >ローカライズされたサイトに移動しないでください。

1. に移動します。 **[!UICONTROL ページプロパティ]**.

   ![page-properties-1](assets/page-properties-1.png)

1. 「**[!UICONTROL 詳細]**」タブに移動します。
1. 有効にする **[!UICONTROL 認証要件]**.

   ![site-authentication-1](assets/site-authentication-1.png)

1. ログインページのパスを追加します。 例：`/content/......./GetStarted`
1. ページを公開します。

## 登録済みメンバー {#enrolled-member}

このエクスペリエンスはユーザーに依存しています `Riley Taylor` および `Sidney Croft` 中 [作成済み](enablement-setup.md#publishcreateenablementmembers) および [割り当て済み](resource.md#settings) から *Ski Lessons* のメンバーシップを通じて学ぶ道 *コミュニティスキークラス* グループ化します。

ログイン方法

* `Username: riley`
* `Password: password`

ユーザープロファイルが自己登録によって作成されなかった場合は、メンバーが初めてログインしたときに、そのユーザーのプロファイルページが表示され、必要に応じて確認および変更できます。

次にメンバーがサインインすると、最初のメニュー項目で識別されるホームページが表示されます。

![chlimage_1-434](assets/chlimage_1-434.png)

### 割り当て {#assignments}

割り当てページでは、メンバーに割り当てられたすべての学習パスとイネーブルメントリソースが表示されます。

各割り当ては、以下に関する基本情報を提供します。

* 割り当てのタイプ
* 新しい割り当てかどうか
* 名前
* 割り当てのタイプに関連する詳細
* 割り当ての連絡先、エキスパート、作成者（指定されている場合）

割り当ての種類は、カードの左上隅にアイコンで示されます。 道路のイメージは、含まれるイネーブルメントリソースの数を含む学習パス用です。

![chlimage_1-435](assets/chlimage_1-435.png)

選択 *Ski Lessons* は、学習パスで参照されている 2 つのイネーブルメントリソースを表示します。

![chlimage_1-436](assets/chlimage_1-436.png)

選択 *スキーレッスン 1* イネーブルメントリソースの詳細ページが開きます。

メンバーは詳細ページから学習できます。 [評価](rating.md) レッスンと追加 [コメント](comments.md). メンバーのアクティビティは、サイトの新着情報セクションに反映されます。

イネーブルメントリソースとのインタラクションは、オーサー環境でアクセス可能な「レポート」セクションに記載されます。

![chlimage_1-437](assets/chlimage_1-437.png)

### Ski Catalog {#ski-catalog}

Ski Catalog ページは、 `Tutorial` 名前空間。 2 人は *Ski Lesson* リソースは `Skiing` タグを使用し、 `All` または `Tutorial: Sports / Skiing` が選択されている場合、何も表示されません。

メンバーにイネーブルメントリソースが直接または学習パスを通じて割り当てられていない場合は、カタログ内のイネーブルメントリソースを操作し、コメントや評価を通じてフィードバックを提供できます。

![chlimage_1-438](assets/chlimage_1-438.png)

### ディスカッショ {#discussions}

イネーブルメントリソース ([有効化時](enablement-create-site.md#step33asettings))、コミュニティサイトテンプレートの基になる `Enablement Tutorial` が作成されました： [フォーラム機能](functions.md#forum-function) ( タイトルは `Discussions)`.

を選択します。 `Discussions`トピックをリンクおよび投稿します。

Sidney Croft(sidney / password) としてログアウトし、ログインして質問に返信し、トピックをフォローします。

インラインモデレートに加えて、ソーシャルメディアでトピックを共有したり、トピックを電子メールで送信したりするオプションがあります。

![chlimage_1-439](assets/chlimage_1-439.png)

### 新機能 {#what-s-new}

この `What's New` メニュー項目は、 [アクティビティストリーム機能](functions.md#activity-stream-function) このコミュニティサイトの構造内で使用できます。

Sidney としてサインインしたまま、 `What's New` リンクをクリックしてアクティビティを表示します。

![chlimage_1-440](assets/chlimage_1-440.png)

## 信頼できるコミュニティメンバー {#trusted-community-member}

この操作は、次を前提としています。 ` [Quinn Harper](enablement-setup.md#publishcreateenablementmembers)` は次の役割を割り当てられました： [モデレーター](enablement-create-site.md#moderation) および [リソース連絡先](resource.md#settings).

ログイン方法

* `Username: quinn`
* `Password: password`

サインインすると、新しいメニュー項目が表示されます。 `Administration`（メンバーにモデレーターの役割が与えられたために表示されます）

![chlimage_1-441](assets/chlimage_1-441.png)

ホームページは、最初のメニュー項目である「割り当て」で識別されます。 Quinn はモデレーターおよびイネーブルメントリソースの連絡先で、イネーブルメントリソースまたは学習パスに登録されていなかったので、表示するものはありません。

### 管理 {#administration}

そこにあるのは、2 人の学習者が行動を起こしていることだ。 `Riley Taylor` および `Sidney Croft. By s`選択 `Administration`モデレートコンソールにアクセスするためのリンクをクインすると、 [一括モデレートコンソール](moderation.md) モデレートする

サイドパネルアイコンを選択すると、コミュニティコンテンツの検索に使用するフィルターが開きます。

コメントカードの上にマウスポインターを置くと、モデレートアクションが表示されます。

![chlimage_1-442](assets/chlimage_1-442.png)

## 作成者に関するレポート {#reports-on-author}

学習者とイネーブルメントリソースのレポートにアクセスする方法は 2 つあります。

作成者が、 **コミュニティ [リソースコンソール](resources.md)**（イネーブルメントリソースを管理する場所）。コミュニティサイトを選択すると、

* すべてのイネーブルメントリソースと学習パス
* 1 つの特定のイネーブルメントリソースまたは学習パス

次に移動： **コミュニティ [レポートコンソール](reports.md)**&#x200B;を使用し、

* イネーブルメントリソースと学習パスへの割り当て
* 特定の期間におけるコミュニティサイトへの投稿
* 特定の期間におけるコミュニティサイトの表示回数（サイト訪問回数）

* 投稿と閲覧は、すべてのコンテンツに対して、または特定のコンテンツに対して、次のように設定できます。

   * フォーラム
   * フォーラムトピック
   * Q&amp;A
   * Q&amp;A 質問
   * ブログ
   * ブログ記事
   * Calendar
   * カレンダー イベント

### リソースコンソール {#resources-console}

少しのアクティビティと、パブリッシュ時にリソースとやり取りを行うので、オーサー環境でのレポートの表示は、見る価値があります。

* 作成者
* 管理者権限でログイン
* メインメニューからに移動します。 **[!UICONTROL コミュニティ/リソース]**
* を選択します。 `Enablement Tutorial` サイト
* を選択します。 `Report`すべてのリソースの概要を表示するアイコン
* リソースを選択し、 `Report`そのリソースに関するレポートのアイコン

Adobe Analyticsからのデータを表示するには時間がかかる可能性が高く、1 ～ 12 時間かかる場合があります。 ただし、基本的な SCORM レポートは既に使用可能です。

#### Ski Lessons リソースレポート {#ski-lessons-resource-report}

![chlimage_1-443](assets/chlimage_1-443.png)

#### Ski Lessons ユーザーレポート {#ski-lessons-user-report}

* 選択 **[!UICONTROL コミュニティ/リソース]**

* カードを開く `Enablement Tutorial`
* カードを開く `Ski Lessons`
* `select Report, User Report`

![chlimage_1-444](assets/chlimage_1-444.png)

### レポートコンソール {#reports-console}

レポートコンソールを使用すると、

* **割り当て** すべてのイネーブルメントコミュニティサイト用
* **件数** 任意のコミュニティサイト
* **投稿** 任意のコミュニティサイト

割り当てに関するレポートの場合：

* 作成者
* 管理者権限でログイン
* に移動します。 **[!UICONTROL コミュニティ/レポート/割り当てレポート]**
* を選択します。 **[!UICONTROL サイト]** プルダウンメニューから ( `Enablement Tutorial`)

* 選択 **[!UICONTROL グループ]** ( `Community Ski Class`)

* を選択します。 **[!UICONTROL 割り当て]** ( `Ski Lessons`)

* 選択 **[!UICONTROL 生成]**

![chlimage_1-445](assets/chlimage_1-445.png)

ビューに関するレポートの場合：

* 作成者
* 管理者権限でログイン
* に移動します。 **[!UICONTROL コミュニティ/レポート/表示レポート]**
* を選択します。 **[!UICONTROL サイト]** プルダウンメニューから ( `Enablement Tutorial`)

* 選択 **[!UICONTROL コンテンツタイプ]** ( `all`)

* を選択します。 **[!UICONTROL 日付範囲]** ( `Last 7 days`)

* 選択 **[!UICONTROL 生成]**

![chlimage_1-446](assets/chlimage_1-446.png)

**[⇐ イネーブルメントリソースの作成と割り当て](resource.md)**
