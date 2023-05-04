---
title: コミュニティサイトコンソール
seo-title: Communities Sites Console
description: コミュニティサイトコンソールへのアクセス方法
seo-description: How to access the Communities Sites console
uuid: 85017055-b8af-4eeb-a8ab-1cbbba0f5a6a
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.4/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 5ac2fcef-05b8-46f7-9a15-997cdd79a3db
role: Admin
exl-id: f1408709-5402-4f55-bd37-9943fe828af0
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '3263'
ht-degree: 4%

---

# コミュニティサイトコンソール {#communities-sites-console}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

コミュニティサイトコンソールでは、次の項目にアクセスできます。

* サイトの作成
* サイト編集
* サイト管理
* [ネストされたグループの作成と編集](groups.md) （サブコミュニティ）

詳しくは、 [AEM Communitiesの概要](getting-started.md) オーサー環境でコミュニティサイトをどれだけすばやく作成できるか、およびオーサー環境とパブリッシュ環境からコミュニティグループを作成する方法を体験できます。

>[!NOTE]
>
>作成用のメインのコミュニティメニュー [コミュニティサイト](sites-console.md), [コミュニティサイトテンプレート](sites.md), [コミュニティグループテンプレート](tools-groups.md) および [コミュニティ機能](functions.md) は、オーサー環境でのみ使用されます。

## 前提条件 {#prerequisites}

コミュニティサイトを作成する前に、次の手順を実行します。 *必須* 移動先：

* 1 つ以上のパブリッシュインスタンスが実行中であることを確認します。
* を有効にします。 [トンネルサービス](deploy-communities.md#tunnel-service-on-author) メンバーとメンバーグループを管理する
* 次を識別： [主発行者](deploy-communities.md#primary-publisher)
* [レプリケーションの設定](deploy-communities.md#replication-agents-on-author) プライマリパブリッシャーポートがデフォルト (4503) でない場合

サイトで多くの機能をサポートできるように準備するためのベストプラクティスは、次の手順に従うことです。

* のインストール [最新の機能パック](deploy-communities.md#latestfeaturepack)
* 有効にする [Adobe Analytics](analytics.md) AEM Communities
* 設定 [電子メール](email.md)
* 特定 [コミュニティ管理者](users.md#creating-community-members)
* [OAuth ハンドラーを有効にする](social-login.md#adobe-granite-oauth-authentication-handler) ソーシャルログイン用

## コミュニティサイトコンソールへのアクセス {#accessing-communities-sites-console}

オーサー環境でコミュニティサイトコンソールにアクセスするには、次の手順を実行します。

* グローバルナビゲーションから： **[!UICONTROL コミュニティ/サイト]**

コミュニティサイトコンソールには、既存のコミュニティサイトが表示されます。 このコンソールから、コミュニティサイトを作成、編集、管理および削除できます。

新しいコミュニティサイトを作成するには、 **作成** アイコン

既存のコミュニティサイトにアクセスするには、ネストされたグループのオーサリング、変更、公開、書き出し、追加を目的として、サイトのフォルダーアイコンを選択します。

例えば、次の画像は、2 つのコミュニティサイト用のフォルダーを表示するメインのコミュニティサイトコンソールを示しています。 [有効](getting-started-enablement.md) および [エンゲージ](getting-started.md):

![chlimage_1-448](assets/chlimage_1-448.png)

## サイト作成 {#site-creation}

サイト作成コンソールでは、選択した [コミュニティサイトテンプレート](sites.md) および設定。

作成されるすべてのサイトにはログイン機能が含まれています。サイトの訪問者は、コンテンツの投稿、メッセージの送信、グループへの参加をおこなう前にログインする必要があるからです。 その他の機能には、ユーザープロファイル、メッセージング、通知、サイトメニュー、検索、テーマ設定、ブランディングが含まれます。

プロセスは、 `Create` コミュニティサイトコンソールの上部にあるボタン。

作成プロセスは、設定する一連の機能（サブパネルとして表示）を含むパネルとして表示される一連の手順です。 を **次へ** 手順または **戻る** を前の手順に戻してから、最後の手順でサイトをコミットします。

### 手順 1:サイトテンプレート {#step-site-template}

![newsitetemplate](assets/newsitetemplate.png)

[ サイトテンプレート ] パネルで、[ タイトル ]、[ 説明 ]、[ サイトルート ]、[ ベース言語 ]、[ 名前 ]、[ サイトテンプレート ] を指定します。

* **[!UICONTROL コミュニティサイトのタイトル]**:サイトの表示タイトル。

   タイトルは、公開されたサイトおよびサイトの管理 UI に表示されます。

* **[!UICONTROL コミュニティサイトの説明]**:サイトの説明。

   公開されたサイトに説明は表示されません。

* **[!UICONTROL コミュニティサイトのルート]**:サイトへのルートパス。

   デフォルトのルートはです。 `/content/sites`を参照してください。ただし、ルートは Web サイト内の任意の場所に移動できます。

* **[!UICONTROL コミュニティサイトの基本言語]**:（単一言語の場合は、手を付けないでください）。英語 ) プルダウンメニューを使用して 1 つを選択します *以上* 使用可能な言語 ( ドイツ語、イタリア語、フランス語、日本語、スペイン語、ポルトガル語（ブラジル）、中国語（繁体字）、中国語（簡体字）)) のベース言語。 追加された言語ごとに 1 つのコミュニティサイトが作成され、 [多言語サイトのコンテンツの翻訳](../../help/sites-administering/translation.md). 各サイトのルートページには、選択した言語の 1 つの言語コード（英語の場合は「en」、フランス語の場合は「fr」など）で名前が付けられた子ページが含まれます。

* **[!UICONTROL コミュニティサイト名]**:URL に表示されるサイトのルートページの名前

   * サイトの作成後に名前が簡単に変更されないので、名前を再確認します。
   * ベース URL ( `https://*server:port/site root/site name*)` が `Community Site Name`
   * 有効な URL に、ベース言語コード+ &quot;.html&quot;を追加します。

      *例：*, `http://localhost:4502/content/sites/mysight/en.html`

* **[!UICONTROL コミュニティサイトテンプレート]** メニュー：プルダウンメニューを使用して、使用可能な [コミュニティサイトテンプレート](tools.md).

選択 **[!UICONTROL 次へ]**

### 手順 2:デザイン {#step-design}

デザインパネルには、テーマとブランディングバナーを選択するための 2 つのサブパネルが含まれています。

#### コミュニティサイトのテーマ {#community-site-theme}

![sitetheme-1](assets/sitetheme-1.png)

フレームワークでは `Twitter Bootstrap` レスポンシブで柔軟なデザインをサイトに取り込む。 プリロードされた多数のBootstrapテーマの 1 つを選択して、選択したコミュニティサイトテンプレートのスタイルを設定したり、Bootstrapテーマをアップロードしたりできます。

選択すると、テーマの上に不透明な青いチェックマークが表示されます。

コミュニティサイトが公開されると、次の操作が可能になります。 [プロパティの編集](#modifying-site-properties) 別のテーマを選択します。

#### コミュニティサイトのブランディング {#community-site-branding}

![chlimage_1-449](assets/chlimage_1-449.png)

コミュニティサイトのブランディングは、各ページの上部にヘッダーとして表示される画像です。

画像のサイズは、ブラウザーでのページの予想される表示幅と高さ 120 ピクセルに合わせて調整する必要があります。

画像を作成または選択する場合は、次の点に注意してください。

* 画像の高さは、画像の上端から 120 ピクセルの範囲で切り抜かれます
* 画像はブラウザーウィンドウの左端に固定されます
* 画像のサイズは変更されず、画像の幅が次のようになる。

   * ブラウザーの幅より小さい場合、画像は水平方向に繰り返されます
   * ブラウザーの幅より大きい場合、画像は切り抜かれたように見えます

「**[!UICONTROL 次へ]**」を選択します。

### 手順 3:設定 {#step-settings}

設定パネルには、サイトを作成する前の手順に進む前に設定する必要のあるサブパネルの表示機能がいくつか含まれています。

* [ユーザー管理](#user-management)
* [タグ付け](#tagging)
* [役割](#roles)
* [モデレート](#moderation)
* [分析](#analytics)
* [翻訳](#translation)
* [有効化](#enablement)

>[!NOTE]
>
>**トンネルサービスの有効化**
>
>「設定」サブパネルの一部では、UGC のモデレート、グループの管理、パブリッシュ環境でのイネーブルメントリソースの連絡先など、信頼できるメンバーの割り当てが可能です。
>
>この規則は、パブリッシュ側で使用されます。 [ユーザーとユーザーグループ](users.md) （メンバーとメンバーグループ）をオーサー環境で複製しないようにする必要があります。
>
>したがって、オーサー環境でコミュニティサイトを作成し、信頼されたメンバーを様々な役割に割り当てる場合は、パブリッシュ環境からメンバーデータを取得する必要があります。
>
>これを行うには、 ` [AEM Communities Publish Tunnel Service](deploy-communities.md#tunnel-service-on-author)`オーサー環境用。

#### ユーザー管理 {#user-management}

![createsitesettings-1](assets/createsitesettings-1.png)

>[!NOTE]
>
>を推奨します。 [イネーブルメントコミュニティサイト](overview.md#enablement-community) 非公開にする（詳しくは、アカウント担当者にお問い合わせください）。
>
>コミュニティサイトは、匿名のサイト訪問者がアクセスを拒否されたり、自己登録やソーシャルログインを使用しなかったりすると、非公開になります。

* **[!UICONTROL ユーザー登録を許可]**

   オンにすると、サイト訪問者は自己登録によってコミュニティメンバーになる場合があります。

   オフにした場合、コミュニティサイトは *制限* サイト訪問者は、コミュニティサイトのメンバーグループに割り当てられ、リクエストを行うか、電子メールで招待状を送信する必要があります。 オフにした場合、匿名アクセスは許可されません。

   次の場合はオフにします。 *プライベート* コミュニティサイト。 初期設定はオンです。

* **[!UICONTROL 匿名アクセスを許可]**

   オンにすると、コミュニティサイトは *open* およびすべてのサイト訪問者がサイトにアクセスできます。

   オフにすると、サインインしたメンバーのみがサイトにアクセスできます。

   次の場合はオフにします。 *プライベート* コミュニティサイト。 初期設定はオンです。

* **[!UICONTROL メッセージを許可]**

   オンにすると、メンバーは互いにメッセージを送信し、コミュニティサイト内のグループにメッセージを送信できます。

   オフにした場合、コミュニティのメッセージは設定されません。

   初期設定はオフです。

* **[!UICONTROL ソーシャルログインを許可 : Facebook]**

   オンにすると、サイト訪問者はFacebookアカウントの資格情報を使用してログインできます。 選択した [Facebookクラウド設定](social-login.md#create-a-facebook-connect-cloud-service) コミュニティサイトを作成した後、コミュニティサイトのメンバーグループにユーザーを追加するように設定する必要があります。

   オフにした場合、Facebookログインは表示されません。

   チェックを外したままにすると、 *プライベート* コミュニティサイト。 初期設定はオフです。

* **[!UICONTROL ソーシャルログインを許可 : Twitter]**

   オンにすると、サイト訪問者はTwitterアカウントの資格情報を使用してログインできます。 選択した [Twitterクラウド設定](social-login.md#create-a-twitter-connect-cloud-service) コミュニティサイトを作成した後、コミュニティサイトのメンバーグループにユーザーを追加するように設定する必要があります。

   オフにした場合、Twitterログインは表示されません。

   チェックを外したままにすると、 *プライベート* コミュニティサイト。 初期設定はオフです。

>[!NOTE]
>
>**[!UICONTROL ソーシャルログインの許可]**
>
>サンプルのFacebook設定とTwitter設定が存在し、選択可能な場合がありますが、 [実稼動環境](../../help/sites-administering/production-ready.md)の場合は、カスタムのFacebookおよびTwitterアプリケーションを作成する必要があります。 詳しくは、 [facebookとTwitterを使用したソーシャルログイン](social-login.md).

#### タグ付け {#tagging}

![chlimage_1-450](assets/chlimage_1-450.png)

コミュニティコンテンツに適用できるタグを制御するには、 [タグ付けコンソール](../../help/sites-administering/tags.md#tagging-console).

また、コミュニティサイトのタグ名前空間を選択すると、カタログとリソースを定義する際に表示される選択が制限されます。 詳しくは、 [イネーブルメントリソースのタグ付け](tag-resources.md) 重要な情報を参照してください。

* テキスト検索ボックス：サイトで使用できるタグを識別するために入力を開始

#### 役割 {#roles}

![chlimage_1-451](assets/chlimage_1-451.png)

この [コミュニティメンバーの役割](users.md) はこれらの設定で割り当てられます。

先行入力検索を使用すると、コミュニティメンバーを簡単に検索できます。

* **[!UICONTROL コミュニティマネージャー]**

   入力を開始して、コミュニティメンバーとメンバーグループを管理する 1 つ以上のコミュニティメンバーまたはメンバーグループを選択します。

* **[!UICONTROL コミュニティのモデレーター]**

   入力を開始して、ユーザー生成コンテンツのモデレーターとして信頼される 1 つ以上のコミュニティメンバーまたはメンバーグループを選択します。

* **[!UICONTROL コミュニティ権限を持つメンバー]**

   入力を開始して、1 つ以上のコミュニティメンバーまたはメンバーグループを選択し、新しいコンテンツを作成するには、 `Allow Privileged Member` が [コミュニティ機能](functions.md).

#### モデレート {#moderation}

![chlimage_1-452](assets/chlimage_1-452.png)

ユーザー生成コンテンツ (UGC) をモデレートする際のグローバル設定は、次の設定で制御します。 個々のコンポーネントには、モデレートを制御するための追加の設定があります。

* **[!UICONTROL コンテンツを事前にモデレート]**

   オンにすると、投稿されたコミュニティコンテンツは、モデレーターが承認するまで表示されません。 初期設定はオフです。 詳しくは、 [コミュニティコンテンツのモデレート](moderate-ugc.md#premoderation).

* **[!UICONTROL コンテンツが非表示になるまでのフラグ設定しきい値]**

   0 より大きい場合は、トピックまたは投稿に何回フラグが設定された後に、その投稿が公開ビューで非表示になるかを指定する必要があります。 -1 に設定した場合、フラグ付きのトピックまたは投稿が公開表示から非表示になることはありません。 デフォルトは 5 です。

#### 分析 {#analytics}

![chlimage_1-453](assets/chlimage_1-453.png)

* **[!UICONTROL Analytics を有効にする]**

   Adobe Analyticsが [設定済み](analytics.md) コミュニティ機能の場合

   初期設定はオフです。 オンにすると、次の追加の選択メニューが表示されます。

![chlimage_1-454](assets/chlimage_1-454.png)

* **[!UICONTROL クラウド設定フレームワークの参照]**

   プルダウンメニューから、このコミュニティサイト用に設定された Analytics クラウドサービスフレームワークを選択します。

   `Communities`は、次のフレームワークの例です： [コミュニティ機能用の Analytics 設定](analytics.md#aem-analytics-framework-configuration) ドキュメント。

#### 翻訳 {#translation}

![chlimage_1-455](assets/chlimage_1-455.png)

* **[!UICONTROL 機械翻訳を許可]**
オン（デフォルトはオフ）にすると、サイト内の UGC に対して機械翻訳が有効になります。 この変更は、サイトが多言語サイトとして設定されている場合でも、ページコンテンツなどの他のコンテンツには影響しません。 詳しくは、 [ユーザー生成コンテンツの翻訳](translate-ugc.md) を参照してください。 詳しくは、 [多言語サイトのコンテンツの翻訳](../../help/sites-administering/translation.md) を参照してください。

![chlimage_1-456](assets/chlimage_1-456.png)

* **[!UICONTROL 選択した言語の機械翻訳を有効にする]**

   機械翻訳が有効な言語は、 [翻訳統合の設定](translate-ugc.md#translation-integration-configuration). これらのデフォルト設定は、デフォルトを削除するか、プルダウンメニューから他の言語を選択することで、このサイトに対して上書きできます。

* **[!UICONTROL 変換プロバイダーを選択]**

   デフォルトでは、サービスプロバイダーは、 `microsoft`デモのみ。 翻訳サービスプロバイダーがライセンスされていない場合、 **機械翻訳を許可** をオフにする必要があります。

* **[!UICONTROL グローバル共有ストアを選択]**

   複数の言語コピーがある Web サイトの場合、グローバル共有ストアは会話のスレッドを 1 つ提供し、各言語コピーから表示できます。 これは、言語コピーとして含まれる言語の 1 つを選択することで実現されます。 デフォルトはです。 *グローバル共有ストアがありません*.

* **[!UICONTROL 変換プロバイダー設定を選択]**

   を選択します。 [翻訳統合フレームワーク](../../help/sites-administering/tc-tic.md) ライセンスされた翻訳プロバイダー用に作成されました。

* **コミュニティサイトの翻訳オプションを選択**

   * **[!UICONTROL ページ全体を翻訳]**

      選択すると、ページ上のすべての UGC がページのベース言語に翻訳されます。

      デフォルトはです。 *未選択*.

   * **[!UICONTROL 選択項目のみ翻訳]**

      選択すると、各投稿の横に翻訳オプションが表示され、個々の投稿をページのベース言語に翻訳できます。

      デフォルトはです。 *選択済み*.

* **保持オプションを選択**

   * **[!UICONTROL ユーザーのリクエストにより投稿を翻訳し、その後保持する]**

      選択した場合、リクエストがおこなわれるまでコンテンツは翻訳されません。 翻訳が完了すると、翻訳はリポジトリに保存されます。

      デフォルトはです。 *未選択*.

   * **[!UICONTROL 翻訳を保持しない]**

      選択した場合、翻訳はリポジトリに保存されません。

      選択しなかった場合、翻訳は保持されます。

      デフォルトはです。 *未選択*.

* **[!UICONTROL スマートレンダリング]**
次のいずれかを選択

   * `Always show contributions in the original language`（デフォルト）
   * `Always show contributions in user preferred language`
   * `Show contributions in user preferred language for only logged-in users`

#### 有効化 {#enablement}

![chlimage_1-457](assets/chlimage_1-457.png)

この `ENABLEMENT`設定は、選択したコミュニティサイトテンプレートに [割り当て機能](functions.md#assignments-function)：イネーブルメント機能がライセンスを受け、 [設定済み](enablement.md). 割り当て機能を含む参照サイトテンプレートは次のとおりです。 `Reference Structured Learning Site Template.`

* **[!UICONTROL 実施可能マネージャー]**

   （必須） `Community Enablementmanagers` このイネーブルメントコミュニティを管理するために、グループを選択できます。 イネーブルメントマネージャーは、メンバーをリソースに割り当てます。 関連トピック [ユーザーとユーザーグループの管理](users.md).

* **[!UICONTROL Marketing Cloud 組織 ID]**

   （オプション） [ビデオハートビート分析](analytics.md#video-heartbeat-analytics) ライセンス。

「**[!UICONTROL 次へ]**」を選択します。

### 手順 4:コミュニティサイトを作成 {#step-create-communities-site}

調整が必要な場合は、 **戻る** ボタンを使用して作成します。

1 回 **作成** を選択して開始すると、サイトの作成プロセスは中断できません。

サイトが作成されたら、次の手順を実行します。

* URL（ノード名）の変更はサポートされていません
* 今後コミュニティサイトテンプレートを変更しても、作成したコミュニティサイトには影響しません。
* コミュニティサイトテンプレートを無効にしても、作成したコミュニティサイトには影響しません
* 次の項目を編集できます。 [構造](#modify-structure) コミュニティサイトのプロパティを変更することによって

![chlimage_1-458](assets/chlimage_1-458.png)

処理が完了すると、新しいサイトのフォルダーがコミュニティサイトコンソールに表示されます。このコンソールから、作成者がページの内容を追加したり、管理者がサイトのプロパティを変更したりできます。

![chlimage_1-459](assets/chlimage_1-459.png)

コミュニティサイトを変更するには、プロジェクトフォルダを選択して開きます。

![siteactions-2](assets/siteactions-2.png)

サイト上にマウスカーソルを置いたとき、またはサイトカードにマウスを合わせたときに、 [オーサーモードでのサイトの編集](#authoring-site-content), [変更用にサイトのプロパティを開く](#modifying-site-properties), [サイトのパブリッシュ](#publishing-the-site), [サイトのエクスポート](#exporting-the-site)、および [サイトの削除](#deleting-the-site).

## サイトコンテンツのオーサリング {#authoring-site-content}

![chlimage_1-460](assets/chlimage_1-460.png)

サイトのコンテンツは、他のAEM Web サイトと同じツールを使用してオーサリングできます。 オーサリング用にサイトを開くには、 `Open Site` サイトにマウスポインターを置くと表示されるアイコン。 サイトが新しいタブで開き、コミュニティサイトコンソールにアクセスできるようになります。

![chlimage_1-461](assets/chlimage_1-461.png)

>[!NOTE]
>
>AEMに詳しくない場合は、 [基本操作](../../help/sites-authoring/basic-handling.md) および [ページのオーサリングのクイックガイド](../../help/sites-authoring/qg-page-authoring.md).

## サイトのプロパティを変更する {#modifying-site-properties}

![chlimage_1-462](assets/chlimage_1-462.png)

サイト作成プロセス中に指定された既存のサイトのプロパティは、 `Edit Site`サイトにマウスポインターを置くと表示されるアイコン。

`Details of the following properties match the descriptions provided in the` [サイトの作成](#site-creation) 」セクションに入力します。

![chlimage_1-463](assets/chlimage_1-463.png)

### 基本を変更 {#modify-basic}

基本パネルでは

* コミュニティサイトのタイトル
* コミュニティサイトの説明

コミュニティサイト名は変更できません。

別のコミュニティサイトテンプレートを選択しても、テンプレートとサイト間の接続が残らないので、既存のコミュニティサイトには影響しません。

代わりに、 [構造](#modify-structure) コミュニティサイトの変更が可能です。

### 構造を修正 {#modify-structure}

構造パネルでは、選択したコミュニティサイトテンプレートから最初に作成された構造を変更できます。 パネルから、次の操作を実行できます。

* 追加の [コミュニティ機能](functions.md) サイト構造内に
* サイト構造内のコミュニティ機能のインスタンスで、次の操作を実行します。

   * **`gear icon`**

      表示タイトルと URL 名&amp;ast を含む設定を編集します。

      同様に [権限を持つメンバーグループ](users.md#privilegedmembersgroups)

   * **`trashcan icon`**

      サイト構造から関数を削除（削除）

   * **`grid icon`**

      サイトのトップレベルナビゲーションバーに表示される関数の順序を変更する

>[!NOTE]
>
>上部の関数を除く、サイト構造内のすべての関数の順序を変更できます。 したがって、コミュニティサイトのホームページを変更することはできません。

>[!CAUTION]
>
>表示タイトルは副作用なしに変更できますが、コミュニティサイトに属するコミュニティ機能の URL 名を編集することはお勧めしません。
>
>例えば、URL の名前を変更しても既存の UGC は移動されず、UGC が「失われる」結果になります。

>[!CAUTION]
>
>グループ機能は、 *not* は *最初でも唯一でも* 関数を使用して、サイト構造内で使用できます。
>
>その他の関数 ( [ページ関数](functions.md#page-function)、を含め、最初にリストする必要があります。

#### 例：コミュニティサイト構造へのカタログ機能の追加 {#example-adding-a-catalog-function-to-a-community-site-structure}

![chlimage_1-464](assets/chlimage_1-464.png)

### デザインを修正 {#modify-design}

デザインパネルを使用すると、新しいテーマを適用できます。

* [コミュニティサイトテーマ](#community-site-theme)
* [コミュニティサイトブランディング](#community-site-branding)
   * パネルの下部までスクロールして、ブランド画像を変更します。

### 設定を変更 {#modify-settings}

設定パネルを使用すると、コミュニティサイト作成の手順 3 のサブパネルにあるほとんどの設定にアクセスできます。

* [ユーザー管理](#user-management)
* [タグ](#tagging)
* [モデレート](#moderation)
* [メンバーの役割](#roles)
* [Analytics](#analytics)
* [翻訳](#translation)

### サムネールを変更 {#modify-thumbnail}

サムネールパネルを使用すると、コミュニティサイトコンソールでサイトを表す画像をアップロードできます。

### イネーブルメントの変更 {#modify-enablement}

イネーブルメントパネルを使用すると、コミュニティサイトの作成時に提供された設定にアクセスできます。

詳しくは、 [有効化](#enablement) 説明。

## サイトのパブリッシュ {#publishing-the-site}

コミュニティサイトを新しく作成または変更した後、 `Publish Site` アイコンをクリックします。

![chlimage_1-465](assets/chlimage_1-465.png)

サイトが正常に公開された後に、というメッセージが表示されます。

![chlimage_1-466](assets/chlimage_1-466.png)

### ネストされたグループを使用した公開 {#publishing-with-nested-groups}

コミュニティサイトを公開した後、 [グループコンソール](groups.md).

## サイトのエクスポート {#exporting-the-site}

![chlimage_1-467](assets/chlimage_1-467.png)

書き出しアイコンを選択し、サイトの上にマウスポインターを置くと、コミュニティサイトのパッケージが作成され、そのパッケージが [パッケージマネージャー](../../help/sites-administering/package-manager.md) とダウンロードされました。\
UGC はサイトパッケージに含まれていません。

## サイトの削除 {#deleting-the-site}

![deleteicon-1](assets/deleteicon-1.png)

コミュニティサイトを削除するには、コミュニティサイトコンソールでサイトにマウスを合わせたときに表示される「サイトを削除」アイコンを選択します。 この操作により、UGC、ユーザーグループ、アセット、データベースレコードなど、サイトに関連するすべての項目が削除されます。

## コミュニティユーザーグループを作成しました {#created-community-user-groups}

新しいコミュニティサイトが公開されると、様々な管理者ロールとメンバーロールに対して適切な権限が設定された新しいメンバーグループ（ユーザーグループはパブリッシュ環境で作成されます）が作成されます。

メンバーグループ用に作成された名前には、 *site-name* ～のサイトを考えると [手順 1](#step13asitetemplate) （URL に表示される名前）および一意の ID。コミュニティサイトや、異なるコミュニティサイトのルートに同じサイト名を持つグループとの競合を避けるために使用されます。

例えば、「Getting Started Tutorial」というタイトルのサイトに対して名前が「engage」の場合、モデレーターのユーザーグループは次のようになります。

* タイトル：コミュニティエンゲージモデレーター
* 名前：コミュニティ —*engage-uid* — モデレーター

サイトの作成時にモデレーターまたはグループ管理者として役割を割り当てられたメンバーは、適切なグループに割り当てられ、メンバーグループに割り当てられます。 これらのグループとメンバーの割り当ては、新しいサイトが公開されると、公開時に作成されます。

詳しくは、 [ユーザーとユーザーグループの管理](users.md).

>[!NOTE]
>
>If [ソーシャルログインを許可：Facebook](#user-management) を有効にした場合、ユーザーグループが
>
>* コミュニティ —*&lt;site-name>*-*&lt;uid>*-members
>
が作成され、適用される [Facebook cloud service](social-login.md#createafacebookcloudservice) は、このグループにユーザーを追加するように設定する必要があります。

## 認証エラー用の設定 {#configure-for-authentication-error}

デフォルトでは、ユーザーが誤った資格情報を入力してログインに失敗した場合、コミュニティサイトはサンプルのログインページにリダイレクトされます。 このサンプルログインは、 [本番サーバ](../../help/sites-administering/production-ready.md).

正しくリダイレクトするには、サイトを設定して公開にプッシュした後、次の手順を実行して、認証失敗をコミュニティサイトにリダイレクトする必要があります。

* 各AEMパブリッシュインスタンスで
* 最初に管理者権限でサインイン
* 次にアクセス： [Web コンソール](../../help/sites-deploying/configuring-osgi.md)
   * 例： [http://localhost:4503/system/console/configMgr](http://localhost:4503/system/console/configMgr)

* 場所 `Adobe Granite Login Selector Authentication Handler`
* を選択します。 `pencil`アイコンをクリックして設定を開き、編集します。
* を入力します。 **[!UICONTROL ログインページのマッピング]** 次のように指定します。

   `/content/sites/<site-name>/path/to/login/page:/content/sites/<site-name>`

   例：

   `/content/sites/engage/en/signin:/content/sites/engage/en`

* 「**[!UICONTROL 保存]**」を選択します

![chlimage_1-468](assets/chlimage_1-468.png)

### 認証リダイレクトをテスト {#test-authentication-redirection}

コミュニティサイトのログインページマッピングを使用して設定されたのと同じAEMパブリッシュインスタンス上で、次の操作を実行します。

* コミュニティサイトのホームページを参照します。
   * 例： [http://localhost:4503/content/sites/engage/en.html](http://localhost:4503/content/sites/engage/en.html)

* ログアウトを選択
* ログインを選択
* ユーザー名「x」、パスワード「x」など、明らかに正しくない資格情報を入力します
* ログインページには「無効なログイン」エラーが表示されます

![chlimage_1-469](assets/chlimage_1-469.png)

## メインサイトコンソールからコミュニティサイトにアクセスする {#accessing-community-sites-from-main-sites-console}

グローバルナビゲーションサイトコンソールから、コミュニティサイトは `Community Sites` フォルダー。

この方法でコミュニティサイトにアクセスできますが、管理タスクの場合は、コミュニティサイトコンソールからコミュニティサイトにアクセスする必要があります。

![chlimage_1-470](assets/chlimage_1-470.png)
