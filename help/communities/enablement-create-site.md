---
title: イネーブルメントのための新しいコミュニティサイトの作成
seo-title: イネーブルメントのための新しいコミュニティサイトの作成
description: イネーブルメントのためのコミュニティサイトの作成
seo-description: イネーブルメントのためのコミュニティサイトの作成
uuid: 6822cc99-e272-4661-bddf-aa0800b88c41
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.4/COMMUNITIES
topic-tags: introduction
content-type: reference
discoiquuid: aff8b79f-dd4e-486e-9d59-5d09dfe34f27
exl-id: 5b16c775-3bd0-4a55-ba9e-f326224e8bae
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '1744'
ht-degree: 52%

---

# イネーブルメントのための新しいコミュニティサイトの作成 {#author-a-new-community-site-for-enablement}

## コミュニティサイトを作成 {#create-community-site}

[コミュニティサ](sites-console.md) イトの作成では、コミュニティサイトの作成手順を案内するウィザードを使用します。最後の手順でサイトをコミットする前に、`Next`手順または`Back`前の手順に進むことができます。

新しいコミュニティサイトの作成を開始するには：

[オーサーインスタンス](http://localhost:4502/)を使用します。

* 管理者権限でログイン
* **[!UICONTROL コミュニティ/サイト]**&#x200B;に移動します。

* 「**[!UICONTROL 作成]**」を選択します。

### Step 1 : Site Template {#step-site-template}

![enablementsitetemplate](assets/enablementsitetemplate.png)

「**サイトテンプレート**」の手順では、URL のタイトル、説明、名前を入力し、コミュニティサイトテンプレートを選択します。次に例を示します。

* **コミュニティサイトのタイトル**: `Enablement Tutorial`

* **コミュニティサイトの説明**: `A site for enabling the community to learn.`

* **コミュニティサイトのルート**:(デフォルトのルートの場合は空白のままにし `/content/sites`ます)。

* **クラウド設定**：（クラウド設定が指定されていない場合は空欄のままにする）指定されたクラウド設定へのパスを入力します。
* **コミュニティサイトのベース言語**:（単一の言語に対しては手を加えないでください）。英語)プルダウンメニューを使用し *て、使用可能な言語(ドイツ語、イタリア語、フランス語、日本語、スペイン語、ポルトガル語（ブラジル）、中国語(繁体* 語)、中国語（簡体字）)から1つ以上を選択します。追加された言語ごとに1つのコミュニティサイトが作成され、[多言語サイトのコンテンツの翻訳](../../help/sites-administering/translation.md)で説明されているベストプラクティスに従って、同じサイトフォルダー内に存在します。 各サイトのルートページには、選択したいずれかの言語の言語コード（例えば、英語では「en」、フランス語では「fr」）で名付けられた子ページが含まれます。

* **[!UICONTROL コミュニティサイト名]**: `enable`

   * 初期 URL は、コミュニティサイト名の下に表示されます。
   * 有効な URL に、ベース言語コード + 「.html」を追加します。

      *例：* http://localhost:4502/content/sites/  `enable/en.html`

* **[!UICONTROL 参照サイトテンプレート]**:～を選ぶ  `Reference Structured Learning Site Template`

「**[!UICONTROL 次へ]**」を選択します。

### 手順 2：デザイン {#step-design}

「デザイン」の手順では、テーマとブランディングバナーを選択する 2 つのセクションが表示されます。

#### コミュニティサイトテーマ {#community-site-theme}

目的のスタイルを選択し、テンプレートに適用します。選択すると、テーマにチェックマークが付きます。

![enablementsitetheme](assets/enablementsitetheme.png)

#### コミュニティサイトブランディング {#community-site-branding}

（オプション）サイトページに表示するバナー画像をアップロードします。バナーはブラウザーの左端およびコミュニティサイトヘッダーとメニュー（ナビゲーションリンク）の間に固定されます。バナーの高さは 120 ピクセルに切り詰められます。バナーがブラウザーの幅や 120 ピクセルの高さに合わせてリサイズされることはありません。

![chlimage_1-284](assets/chlimage_1-284.png) ![chlimage_1](assets/chlimage_1.jpeg)

「**[!UICONTROL 次へ]**」を選択します。

### 手順 3：設定 {#step-settings}

設定の手順で`Next`を選択する前に、ユーザー管理、タグ付け、役割、モデレート、分析、翻訳およびイネーブルメントに関する設定にアクセスできる7つのセクションがあることに注意してください。

#### ユーザー管理 {#user-management}

[イネーブルメントコミュニティ](overview.md#enablement-community)はプライベートにすることをお勧めします。

コミュニティサイトを非公開にするとは、匿名のサイト訪問者に対してアクセスを拒否し、自己登録やソーシャルログインを使用禁止にすることです。

[User Management](sites-console.md#user-management)のほとんどのチェックボックスがオフになっていることを確認します。

* サイト訪問者の自己登録を許可しない
* 匿名のサイト訪問者に対し、サイトの閲覧を許可しない
* コミュニティメンバー間でのメッセージングを許可するかどうか（オプション）
* facebookでのログインを許可しない
* twitterでのログインを許可しない

![chlimage_1-285](assets/chlimage_1-285.png)

#### タグ付け {#tagging}

コミュニティコンテンツに適用できるタグを制御するには、[タグ付けコンソール](../../help/sites-administering/tags.md#tagging-console)で以前に定義したAEM名前空間（[Tutorial namespace](enablement-setup.md#create-tutorial-tags)など）を選択します。

また、コミュニティサイトに対してタグ名前空間を選択すると、カタログとイネーブルメントリソースを定義するときに表示される選択肢が制限されます。重要な情報については、[イネーブルメントリソースのタグ付け](tag-resources.md)を参照してください。

名前空間は先行入力検索で簡単に検索できます。例：

* &#39;tut&#39;と入力します
*  `Tutorial`

![chlimage_1-286](assets/chlimage_1-286.png)

### 役割 {#roles}

[コミュニティメ](users.md) ンバーの役割は、役割セクションの設定を使用して割り当てられます。

コミュニティメンバー（またはメンバーのグループ）がコミュニティマネージャーとしてサイトを体験するには、先頭入力検索を使用して、ドロップダウンのオプションからメンバーまたはグループ名を選択します。

例：

* 「q」と入力します。
* [Quinn Harper](enablement-setup.md#publishcreateenablementmembers)を選択します。

>[!NOTE]
>
>[トンネル](deploy-communities.md#tunnel-service-on-author) サービスを使用すると、パブリッシュ環境にのみ存在するメンバーとグループを選択できます。

![community_roles](assets/community_roles.png)

#### モデレート {#moderation}

ユーザー生成コンテンツ（UGC）を[モデレート](sites-console.md#moderation)する場合は、デフォルトのグローバル設定を受け入れます。

![chlimage_1-287](assets/chlimage_1-287.png)

#### ANALYTICS {#analytics}

プルダウンメニューから、このコミュニティサイト用に設定した Analytics クラウドサービスフレームワークを選択します。

スクリーンショットに表示されている選択肢「`Communities`」は、[設定ドキュメント](analytics.md#aem-analytics-framework-configuration)のフレームワークの例です。

![chlimage_1-288](assets/chlimage_1-288.png)

#### 翻訳 {#translation}

[翻訳設定](sites-console.md#translation)では、UGC の翻訳を許可するかどうかと、どの言語に翻訳するかを指定します。

* 「**[!UICONTROL 機械翻訳を許可]**」をオンにします。
* デフォルト設定を使用する

![chlimage_1-289](assets/chlimage_1-289.png)

#### イネーブルメント {#enablement}

1 つのイネーブルメントコミュニティに対し、1 人以上のコミュニティ実施可能マネージャーを指定する必要があります。

* **[!UICONTROL イネーブルメントマネージャー]**
（必須） 
`Community Enablement Managers` グループを選択して、このコミュニティサイトを管理できます。

   * 型&quot;s&quot;
   *  `Sirius Nilson`

* **[!UICONTROL Marketing Cloud組織ID]**
（オプション）Adobe AnalyticsアカウントのIDです。有効化レポートにビデオハートビー [ト分析を含め](analytics.md#video-heartbeat-analytics) る際に必要になります。

![chlimage_1-290](assets/chlimage_1-290.png)

「**[!UICONTROL 次へ]**」を選択します。

### 手順 4：コミュニティサイトの作成 {#step-create-community-site}

「**[!UICONTROL 作成]**」を選択します。

![chlimage_1-291](assets/chlimage_1-291.png)

プロセスが完了すると、新しいサイトのフォルダーがコミュニティサイトコンソールに表示されます。

![enablementsitecreated](assets/enablementsitecreated.png)

### 新しいコミュニティサイトの公開 {#publish-the-new-community-site}

作成したサイトは、コミュニティ - サイトコンソールで管理する必要があります。このコンソールは、新しいサイトを作成するコンソールと同じものです。

コミュニティサイトのフォルダーを選択した後、サイトアイコンにマウスカーソルを合わせると、4 つのアクションアイコンが表示されます。

![siteactionicons](assets/siteactionicons.png)

省略記号アイコン（その他のアクションアイコン）を選択すると、「サイトを書き出し」および「サイトを削除」オプションが表示されます。

![siteactionsnew](assets/siteactionsnew.png)

各アイコンの機能は次のとおりです（左から右の順に説明）。

* **サイトを**
開く鉛筆アイコンを選択して、コミュニティサイトをオーサー編集モードで開き、ページコンポーネントを追加または設定します。

* **サイトを編**
集プロパティアイコンを選択して、コミュニティサイトを開き、タイトルやテーマなどのプロパティを変更します。

* **サイトを公**
開コミュニティサイトを公開する世界のアイコンを選択します（デフォルトではlocalhost:4503に）。

* **サイトを書き**
出し書き出しアイコンを選択して、コミュニティサイトのパッケージを作成し、パッケージマネージャーに保存してダウ [ンロー](../../help/sites-administering/package-manager.md) ドします。

   UGC はサイトパッケージに含まれていません。

* **サイトを削除**&#x200B;コミュニティサイトを削除するには、サイトを削除アイコンを選択します。このアイコンは、コミュニティサイトコンソール内でサイトにマウスポインターを置くと表示されます。サイトを削除すると、UGC やユーザーグループ、アセット、データベースレコードなど、そのサイトに関連付けられているアイテムがすべて削除されます。

![enablesiteactions](assets/enablesiteactions.png)

#### サイトの公開 {#select-publish}

地球のアイコンを選択して、コミュニティサイトを公開します。

![chlimage_1-292](assets/chlimage_1-292.png)

サイトが公開されると、次のようなメッセージが表示されます。

![chlimage_1-293](assets/chlimage_1-293.png)

## コミュニティのユーザーとユーザーグループ {#community-users-user-groups}

### 新しいコミュニティユーザーグループの確認 {#notice-new-community-user-groups}

新しいコミュニティサイトとともに、新しいユーザーグループが作成されます。各グループには、様々な管理機能に応じて適切な権限が設定されています。詳しくは、[コミュニティサイトのユーザーグループ](users.md#usergroupsforcommunitysites)を参照してください。

この新しいコミュニティサイトでは、手順1でサイト名「enable」を指定すると、パブリッシュ環境に存在する新しいユーザーグループが[コミュニティメンバーとグループコンソール](members.md#groups-console)から表示されます。

![chlimage_1-294](assets/chlimage_1-294.png)

### 「Community Enable Members」グループへのメンバー割り当て{#assign-members-to-community-enable-members-group}

オーサー環境で、トンネルサービスを有効にすると、初期セットアップ](enablement-setup.md#publishcreateenablementmembers)中に作成された[ユーザーを、新しく作成したコミュニティサイトのコミュニティメンバーグループに割り当てることができます。

コミュニティグループコンソールでは、メンバーを個別に追加したり、グループのメンバーシップを使用して追加したりできます。

この例では、グループ`Community Ski Class`がグループ`Community Enable Members`のメンバーとして追加され、メンバー`Quinn Harper`も追加されます。

* **[!UICONTROL コミュニティ/グループ]**&#x200B;コンソールに移動します。
* **[!UICONTROL Community Enable Members]**&#x200B;グループを選択します。
* 「**[!UICONTROL グループにメンバーを追加]**」検索ボックスに`ski`と入力します。
* 「**[!UICONTROL Community Ski Class]**」（学習者のグループ）を選択します。
* 検索ボックスに`quinn`と入力します。
* **[!UICONTROL Quinn Harper]**（イネーブルメントリソースの連絡先）を選択します。

* 「**[!UICONTROL 保存]**」を選択します。

![chlimage_1-295](assets/chlimage_1-295.png)

## パブリッシュ側の設定 {#configurations-on-publish}

### http://localhost:4503/content/sites/enable/en.html {#http-localhost-content-sites-enable-en-html}

![chlimage_1-296](assets/chlimage_1-296.png)

### 認証エラーの設定 {#configure-for-authentication-error}

サイトが設定され、パブリッシュにプッシュされたら、パブリッシュインスタンス上で[ログインマッピング](sites-console.md#configure-for-authentication-error)(`Adobe Granite Login Selector Authentication Handler`)を設定します。 ログイン資格情報が正しく入力されない場合、認証エラーによってコミュニティサイトのログインページが再表示され、エラーメッセージが表示されるという利点があります。

`Login Page Mapping`を

* /content/sites/enable/en/signin:/content/sites/enable/en

### （オプション）デフォルトのホームページの変更  {#optional-change-the-default-home-page}

公開サイトをデモ目的で操作するときは、デフォルトのホームページを新しいサイトに変更すると便利です。

これをおこなうには、[CRX|DE](http://localhost:4503/crx/de) Lite を使用して、パブリッシュ側で[リソースマッピング](../../help/sites-deploying/resource-mapping.md)テーブルを編集します。

開始するには、次のようにします。

1. 公開時に、CRXDEにアクセスし、管理者権限でログインします。

   * 例えば、[http://localhost:4503/crx/de](http://localhost:4503/crx/de)を参照し、`admin/admin`を使用してログインします。

1. プロジェクトブラウザで、`/etc/map`を展開します。
1. `http`ノードを選択します。

   * 「**[!UICONTROL ノードを作成]**」を選択します。

      * **** Namelocalhost.4503

         （*使用*&#x200B;しないでください`:`）

      * **** [型：マッピング](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html)

1. 新しく作成された`localhost.4503`ノードを選択した状態

   * プロパティの追加

      * **名前**：sling:match
      * **タイプ**：String
      * **値**：localhost.4503/\$

         （「$」文字で終わる必要があります）
   * プロパティの追加

      * **名前**：sling:internalRedirect
      * **タイプ**：String
      * **値**：/content/sites/enable/en.html


1. 「**[!UICONTROL すべて保存]**」を選択します。
1. （オプション）閲覧履歴の削除
1. http://localhost:4503/を参照します。

   * http://localhost:4503/content/sites/enable/en.htmlにアクセスします。

>[!NOTE]
>
>無効にするには、`sling:match`プロパティの値の前に「x」を付け、`xlocalhost.4503/$`と&#x200B;**[!UICONTROL すべて保存]**&#x200B;を付けます。

![chlimage_1-297](assets/chlimage_1-297.png)

#### トラブルシューティング：マップ保存エラー {#troubleshooting-error-saving-map}

変更を保存できない場合は、ノード名が `localhost.4503`（区切り文字が「ドット」）となっているかを確認してください。`localhost:4503` は有効な名前空間のプレフィックスではないので、`localhost`（区切り文字が「コロン」）という表記は正しくありません。

![chlimage_1-298](assets/chlimage_1-298.png)

#### トラブルシューティング：リダイレクト失敗 {#troubleshooting-fail-to-redirect}

正規表現`sling:match`文字列の末尾にある「**$**」は重要なので、正確に`http://localhost:4503/`のみがマッピングされます。そうでない場合、URLのserver:portの後に存在するパスの前にリダイレクト値が付加されます。 したがって、AEMがログインページにリダイレクトしようとすると、失敗します。

## コミュニティサイトの変更 {#modifying-the-community-site}

サイトを最初に作成した後、作成者は[サイトを開くアイコン](sites-console.md#authoring-site-content)を使用して、標準的な AEM のオーサリングアクティビティを実行できます。

また、管理者は[サイトを編集アイコン](sites-console.md#modifying-site-properties)を使用して、タイトルなどのサイトプロパティを変更できます。

変更後は、必ず&#x200B;**保存**&#x200B;して再&#x200B;**公開**&#x200B;してください。

>[!NOTE]
>
>AEM に馴染みがない場合は、[基本操作](../../help/sites-authoring/basic-handling.md)に関するドキュメントおよび[ページのオーサリングのクイックガイド](../../help/sites-authoring/qg-page-authoring.md)を参照してください。

### カタログの追加 {#add-a-catalog}

このコミュニティサイトに選択されたコミュニティサイトテンプレートには、カタログ機能が含まれています。

含まれていない場合は、カタログ機能を簡単に追加できます。これにより、イネーブルメントリソースや学習パスに割り当てられていないコミュニティの他のメンバーが、カタログからイネーブルメントリソースを選択できるようになります。

サイト構造にカタログ機能が既に含まれている場合、タイトルが変わることがあります。

サイトの構造を変更するには、**[!UICONTROL コミュニティ/サイト]**&#x200B;コンソールに移動し、`enable`フォルダーを開いて、**サイトを編集**&#x200B;アイコンを選択し、`Enablement Tutorial`のプロパティにアクセスします。

構造パネルを選択し、カタログを追加するか、既存のカタログを変更します。

* **タイトル**: `Ski Catalog`

* **URL**: `catalog`

* **すべての名前空間を選択**：デフォルトのままにします。
* 「**[!UICONTROL 保存]**」を選択します。

![chlimage_1-299](assets/chlimage_1-299.png)

位置アイコンを使用し、カタログ機能を Assignments の後の 2 番目の位置に移動します。

![chlimage_1-300](assets/chlimage_1-300.png)

右上隅の「**[!UICONTROL 保存]**」を選択してコミュニティサイトに対する変更を保存します。

その後、サイトを再び&#x200B;**公開**&#x200B;します。
