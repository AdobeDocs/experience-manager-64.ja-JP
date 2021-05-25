---
title: 新しいコミュニティサイトの作成
seo-title: 新しいコミュニティサイトの作成
description: 新しい AEM Communities サイトを作成する方法
seo-description: 新しい AEM Communities サイトを作成する方法
uuid: b8557416-cae4-489e-ab3b-e94d56686b7a
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.4/COMMUNITIES
topic-tags: introduction
content-type: reference
discoiquuid: bf182bb7-e305-45be-aadb-d71efd70f8cb
exl-id: 5d58f9c5-3210-48ef-94a3-805a1a57e3af
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '1649'
ht-degree: 51%

---

# 新しいコミュニティサイトの作成 {#author-a-new-community-site}

## 新しいコミュニティサイトの作成 {#create-a-new-community-site}

オーサーインスタンスを使用して新しいコミュニティサイトを作成します。

* 管理者権限でログイン
* グローバルナビゲーションから：**[!UICONTROL ナビゲーション/コミュニティ/サイト]**

コミュニティサイトコンソールでは、コミュニティサイトを作成する手順を案内するウィザードが提供されます。最後の手順でサイトをコミットする前に、`Next`手順または`Back`前の手順に進むことができます。

新しいコミュニティサイトの作成を開始するには：

* 「`Create`」ボタンを選択します。

![createcommunitysite](assets/createcommunitysite.png)

### Step 1 : Site Template {#step-site-template}

![createsitetemplate63](assets/createsitetemplate63.png)

[「サイトテンプレート」の手順](sites-console.md#step2013asitetemplate)では、URL のタイトル、説明、名前を入力し、コミュニティサイトテンプレートを選択します。次に例を示します。

* **[!UICONTROL コミュニティサイトのタイトル]**: `Getting Started Tutorial`

* **[!UICONTROL コミュニティサイトの説明]**: `A site for engaging with the community.`

* **[!UICONTROL コミュニティサイトのルート]**:(デフォルトのルートの場合は空白のままにし `/content/sites`ます)。

* **[!UICONTROL クラウド設定]**：（クラウド設定が指定されていない場合は空欄のままにする）指定されたクラウド設定へのパスを入力します。
* **[!UICONTROL コミュニティサイトのベース言語]**:（単一の言語に対しては手を加えないでください）。英語)プルダウンメニューを使用し *て、使用可能な言語(ドイツ語、イタリア語、フランス語、日本語、スペイン語、ポルトガル語（ブラジル）、中国語(繁体* 語)、中国語（簡体字）)から1つ以上を選択します。追加された言語ごとに1つのコミュニティサイトが作成され、[多言語サイトのコンテンツの翻訳](../../help/sites-administering/translation.md)で説明されているベストプラクティスに従って、同じサイトフォルダー内に存在します。 各サイトのルートページには、選択したいずれかの言語の言語コード（例えば、英語では「en」、フランス語では「fr」）で名付けられた子ページが含まれます。

* **[!UICONTROL コミュニティサイト名]**：engage

   * サイトの作成後に名前が容易に変更されないので、名前を再確認します。
   * コミュニティサイト名の下に初期URLが表示されます。
   * 有効なURLに、ベース言語コード+ &quot;.html&quot;を追加する
   * *例：* http://localhost:4502/content/sites/  `engage/en.html`

* **[!UICONTROL テンプレート]**:～を選ぶ  `Reference Site`

「**[!UICONTROL 次へ]**」を選択します。

### 手順 2：デザイン {#step-design}

「デザイン」の手順では、テーマとブランディングバナーを選択する 2 つのセクションが表示されます。

#### コミュニティサイトテーマ {#community-site-theme}

目的のスタイルを選択し、テンプレートに適用します。選択すると、テーマにチェックマークが付きます。

![sitetheme](assets/sitetheme.png)

#### コミュニティサイトブランディング {#community-site-branding}

（オプション）サイトページ全体に表示するバナー画像をアップロードします。 バナーはブラウザーの左端およびコミュニティサイトヘッダーとメニュー（ナビゲーションリンク）の間に固定されます。バナーの高さは 120 ピクセルに切り詰められます。バナーがブラウザーの幅や 120 ピクセルの高さに合わせてリサイズされることはありません。

![chlimage_1-353](assets/chlimage_1-353.png) ![chlimage_1-354](assets/chlimage_1-354.png)

「**[!UICONTROL 次へ]**」を選択します。

### 手順 3：設定 {#step-settings}

設定の手順で`Next`を選択する前に、ユーザー管理、タグ付け、モデレート、グループ管理、分析、翻訳およびイネーブルメントに関する設定にアクセスできる7つのセクションがあることに注意してください。

イネーブルメント機能の使用を体験するには、 [AEM Communities for Enablement](getting-started-enablement.md)の手引きを参照してください。

#### ユーザー管理 {#user-management}

「[ユーザー管理](sites-console.md#user-management)」タブのチェックボックスをすべてオンにします。

* サイト訪問者の自己登録を許可するには
* サイト訪問者がサインインせずにサイトを表示できるようにするには
* メンバーが他のコミュニティメンバーからメッセージを送受信できるようにするには
* プロファイルの登録と作成の代わりにFacebookでのログインを許可するには
* プロファイルの登録と作成の代わりにTwitterでのログインを許可するには

>[!NOTE]
>
>実稼動環境では、カスタムの Facebook アプリケーションおよび Twitter アプリケーションを作成する必要があります。[Facebook と Twitter を使用したソーシャルログイン](social-login.md)を参照してください。

![createsitesettings](assets/createsitesettings.png)

#### タグ付け {#tagging}

コミュニティコンテンツに適用できるタグを制御するには、[タグ付けコンソール](../../help/sites-administering/tags.md#tagging-console)で以前に定義したAEM名前空間（[Tutorial namespace](setup.md#create-tutorial-tags)など）を選択します。

名前空間は先行入力検索で簡単に検索できます。例：

* &#39;tut&#39;と入力します
*  `Tutorial`

![chlimage_1-355](assets/chlimage_1-355.png)

#### 役割 {#roles}

[コミュニティメ](users.md) ンバーの役割は、役割セクションの設定を使用して割り当てられます。

コミュニティメンバー（またはメンバーのグループ）がコミュニティマネージャーとしてサイトを体験するには、先頭入力検索を使用して、ドロップダウンのオプションからメンバーまたはグループ名を選択します。

例：

* 「q」と入力します。
* [Quinn Harper](enablement-setup.md#publishcreateenablementmembers)を選択します。

>[!NOTE]
>
>[トンネル](https://helpx.adobe.com/experience-manager/6-3/communities/using/deploy-communities.html#tunnel-service-on-author) サービスを使用すると、パブリッシュ環境にのみ存在するメンバーとグループを選択できます。

![community_roles-1](assets/community_roles-1.png)

#### モデレート {#moderation}

ユーザー生成コンテンツ（UGC）を[モデレート](sites-console.md#moderation)する場合は、デフォルトのグローバル設定を受け入れます。

![chlimage_1-356](assets/chlimage_1-356.png)

#### ANALYTICS {#analytics}

Adobe Analytics のライセンスを持っていて、Analytics のクラウドサービスおよびフレームワークが設定されている場合は、Analytics を有効にしてフレームワークを選択できます。

[コミュニティ機能のための Analytics の設定](analytics.md)を参照してください。

![chlimage_1-357](assets/chlimage_1-357.png)

#### 翻訳 {#translation}

[翻訳設定](sites-console.md#translation)では、サイトの基本言語に加えて、UGC の翻訳を許可するかどうかと、どの言語に翻訳するかを指定します。

* 「**[!UICONTROL 機械翻訳を許可]**」をオンにします。
* デフォルトの機械翻訳サービスで翻訳用に選択されたデフォルトの言語をそのままにします
* デフォルトの翻訳プロバイダーと設定をそのまま使用
* 言語コピーがないので、グローバルストアは不要です
* **[!UICONTROL ページ全体を翻訳]**&#x200B;を選択します。
* デフォルトの永続性オプションを維持

![chlimage_1-358](assets/chlimage_1-358.png)

#### イネーブルメント {#enablement}

エンゲージメントコミュニティを作成する場合は空白のままにします。

[イネーブルメントコミュニティ](overview.md#enablement-community)をすばやく作成する方法のチュートリアルについて詳しくは、[イネーブルメントのための AEM Communities 使用の手引き](getting-started-enablement.md)を参照してください。

「**[!UICONTROL 次へ]**」を選択します。

### 手順 4：コミュニティサイトの作成 {#step-create-communities-site}

「**[!UICONTROL 作成]**」を選択します。

![chlimage_1-359](assets/chlimage_1-359.png)

プロセスが完了すると、新しいサイトのフォルダーがコミュニティサイトコンソールに表示されます。

![communitiessitesconsole](assets/communitiessitesconsole.png)

## 新しいコミュニティサイトの公開 {#publish-the-new-community-site}

作成したサイトは、コミュニティ - サイトコンソールで管理する必要があります。このコンソールは、新しいサイトを作成するコンソールと同じものです。

コミュニティサイトのフォルダーを選択して開いた後、サイトアイコンにマウスカーソルを合わせると 4 つのアクションアイコンが表示されます。

![siteactionicons-1](assets/siteactionicons-1.png)

4つ目の省略記号アイコン（その他のアクション）を選択すると、「サイトを書き出し」および「サイトを削除」オプションが表示されます。

![siteactionsnew-1](assets/siteactionsnew-1.png)

各アイコンの機能は次のとおりです（左から右の順に説明）。

* **サイトを**
開く鉛筆アイコンを選択して、コミュニティサイトをオーサー編集モードで開き、ページコンポーネントを追加または設定します。

* **サイトを編**
集プロパティアイコンを選択して、コミュニティサイトを開き、タイトルやテーマなどのプロパティを変更します。

* **サイトを公**
開世界中のアイコンを選択してコミュニティサイトを公開します（例えば、公開サーバーがローカルマシンで実行されている場合は、デフォルトでlocalhost:4503に公開されます）。

* **サイトを書き**
出し書き出しアイコンを選択して、コミュニティサイトのパッケージを作成し、パッケージマネージャーに保存してダウ [ンロー](../../help/sites-administering/package-manager.md) ドします。

   UGC はサイトパッケージに含まれていません。

* **サイトを削除**

   **[!UICONTROL コミュニティ/サイトコンソール]**&#x200B;からコミュニティサイトを削除するには、削除アイコンを選択します。 サイトを削除すると、UGC やユーザーグループ、アセット、データベースレコードなど、そのサイトに関連付けられているアイテムがすべて削除されます。

![siteactions-1](assets/siteactions-1.png)

>[!NOTE]
>
>パブリッシュインスタンスにデフォルトポートの 4503 を使用していない場合は、デフォルトのレプリケーションエージェントを編集し、ポート番号を正しい値に設定します。
>
>オーサーインスタンスで、メインメニューから
>
>1. **[!UICONTROL ツール/運営/レプリケーション]**&#x200B;メニューに移動します。
>1. **[!UICONTROL 作成者のエージェント]**&#x200B;を選択します。
>1. 「**[!UICONTROL デフォルトエージェント(publish)]**」を選択します。
>1. **[!UICONTROL 設定]**&#x200B;の横にある「**[!UICONTROL 編集]**」を選択します。
>1. エージェント設定のポップアップダイアログで、「トランスポート」タブを選択します。
>1. URIで、ポート番号4503を目的のポート番号に変更します。

>
>
例えば、ポート6103を使用するには、次のようにします。`http://localhost:6103/bin/receive?sling:authRequestLogin=1`
>
>1. 「**[!UICONTROL OK]**」を選択します。
>1. （オプション） `Clear`または`Force Retry`を選択して、レプリケーションキューをリセットします。


### サイトの公開 {#select-publish}

公開サーバーが実行中であることを確認したら、地球のアイコンを選択して、コミュニティサイトを公開します。

![chlimage_1-360](assets/chlimage_1-360.png)

コミュニティサイトが正常に公開されると、次のような短いメッセージが表示されます。

![chlimage_1-361](assets/chlimage_1-361.png)

### 新しいコミュニティユーザーグループの確認 {#notice-new-community-user-groups}

新しいコミュニティサイトとともに、新しいユーザーグループが作成されます。各グループには、様々な管理機能に応じて適切な権限が設定されています。詳しくは、[コミュニティサイトのユーザーグループ](users.md#usergroupsforcommunitysites)を参照してください。

この新しいコミュニティサイトでは、手順 1 で「engage」というサイト名を指定したので、[グループコンソール](members.md)（グローバルナビゲーション：コミュニティ／グループ）で以下に示す 4 つの新しいユーザーグループを確認できます。

* コミュニティ Engage コミュニティマネージャー
* コミュニティ Engage グループ管理者
* コミュニティ Engage メンバー
* コミュニティ Engage モデレーター
* コミュニティ Engage の権限を持つメンバー
* コミュニティ Engage サイトコンテンツマネージャー

[Aaron McDonald](tutorials.md#demo-users) が次のグループのメンバーになっていることに注目してください。

* コミュニティ Engage コミュニティマネージャー
* コミュニティ Engage モデレーター
* コミュニティ Engage メンバー（モデレーターグループのメンバーとして間接的に）

![chlimage_1-362](assets/chlimage_1-362.png)

#### http://localhost:4503/content/sites/engage/en.html {#http-localhost-content-sites-engage-en-html}

![chlimage_1-363](assets/chlimage_1-363.png)

## 認証エラーの設定 {#configure-for-authentication-error}

サイトが設定され、パブリッシュにプッシュされたら、パブリッシュインスタンス上で[ログインマッピング](sites-console.md#configure-for-authentication-error)(`Adobe Granite Login Selector Authentication Handler`)を設定します。 ログイン資格情報が正しく入力されない場合、認証エラーによってコミュニティサイトのログインページが再表示され、エラーメッセージが表示されるという利点があります。

`Login Page Mapping`を

* /content/sites/engage/en/signin:/content/sites/engage/en

## オプションの手順 {#optional-steps}

### デフォルトのホームページの変更 {#change-the-default-home-page}

公開サイトをデモ目的で操作するときは、デフォルトのホームページを新しいサイトに変更すると便利です。

これをおこなうには、[CRXDE](http://localhost:4503/crx/de) Lite を使用して、パブリッシュ側で[リソースマッピング](../../help/sites-deploying/resource-mapping.md)テーブルを編集します。

作業を開始するには：

1. 公開時に、管理者権限でログインします。
1. [http://localhost:4503/crx/de](http://localhost:4503/crx/de)を参照します。
1. プロジェクトブラウザで、`/etc/map`を展開します。
1. `http`ノードを選択します。

   * 「**[!UICONTROL ノードを作成]**」を選択します。

      * **** Namelocalhost.4503

         （*not*&#x200B;は`:`を使用しないでください）。

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
      * **値**：/content/sites/engage/en.html


1. 「**[!UICONTROL すべて保存]**」を選択します。
1. （オプション）閲覧履歴の削除
1. http://localhost:4503/を参照します。

   * http://localhost:4503/content/sites/engage/en.htmlにアクセスします。

>[!NOTE]
>
>無効にするには、`sling:match`プロパティの値の前に「x」を付け、`xlocalhost.4503/$`と&#x200B;**[!UICONTROL すべて保存]**&#x200B;を付けます。

![chlimage_1-364](assets/chlimage_1-364.png)

#### トラブルシューティング：マップ保存エラー {#troubleshooting-error-saving-map}

変更を保存できない場合は、ノード名が `localhost.4503`（区切り文字が「ドット」）となっているかを確認してください。`localhost:4503` は有効な名前空間のプレフィックスではないので、`localhost`（区切り文字が「コロン」）という表記は正しくありません。

![chlimage_1-365](assets/chlimage_1-365.png)

#### トラブルシューティング：リダイレクト失敗 {#troubleshooting-fail-to-redirect}

正規表現`sling:match`文字列の末尾にある「**$**」は重要なので、正確に`http://localhost:4503/`のみがマッピングされます。そうでない場合、URLのserver:portの後に存在するパスの前にリダイレクト値が付加されます。 したがって、AEMがログインページにリダイレクトしようとすると、失敗します。

### サイトの変更 {#modify-the-site}

サイトを最初に作成した後、作成者は[サイトを開くアイコン](sites-console.md#authoring-site-content)を使用して、標準的な AEM のオーサリングアクティビティを実行できます。

また、管理者は[サイトを編集アイコン](sites-console.md#modifying-site-properties)を使用して、タイトルなどのサイトプロパティを変更できます。

変更後は、必ず&#x200B;**保存**&#x200B;して&#x200B;**再公開**&#x200B;してください。

>[!NOTE]
>
>AEM に馴染みがない場合は、[基本操作](../../help/sites-authoring/basic-handling.md)に関するドキュメントおよび[ページのオーサリングのクイックガイド](../../help/sites-authoring/qg-page-authoring.md)を参照してください。
