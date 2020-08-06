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
translation-type: tm+mt
source-git-commit: 3d2b91565e14e85e9e701663c8d0ded03e5b430c
workflow-type: tm+mt
source-wordcount: '1649'
ht-degree: 51%

---


# 新しいコミュニティサイトの作成 {#author-a-new-community-site}

## 新しいコミュニティサイトの作成 {#create-a-new-community-site}

オーサーインスタンスを使用して新しいコミュニティサイトを作成します。

* 管理者権限でサインインする
* From global navigation: **[!UICONTROL Navigation > Communities > Sites]**

コミュニティサイトコンソールでは、コミュニティサイトを作成する手順を案内するウィザードが提供されます。It is possible to move forward to the `Next`step or `Back`to the previous step before committing the site in the final step.

新しいコミュニティサイトの作成を開始するには：

* ボタンを選択し `Create` ます

![createcommunitysite](assets/createcommunitysite.png)

### Step 1 : Site Template {#step-site-template}

![createsitetemplate63](assets/createsitetemplate63.png)

[「サイトテンプレート」の手順](sites-console.md#step2013asitetemplate)では、URL のタイトル、説明、名前を入力し、コミュニティサイトテンプレートを選択します。次に例を示します。

* **[!UICONTROL コミュニティサイトのタイトル]**: `Getting Started Tutorial`

* **[!UICONTROL コミュニティサイトの説明]**: `A site for engaging with the community.`

* **[!UICONTROL コミュニティサイトルート]**: (デフォルトのルートの場合は空白のまま `/content/sites`)

* **[!UICONTROL クラウド設定]**：（クラウド設定が指定されていない場合は空欄のままにする）指定されたクラウド設定へのパスを入力します。
* **[!UICONTROL コミュニティサイトの基本言語]**: （単一言語の場合は手を付けないでください）。 英語)プルダウンメニューを使用して *、ドイツ語、イタリア語、フランス語、日本語、スペイン語、ポルトガル語（ブラジル）、中国語（繁体字）、中国語（簡体字）の各言語から* 1つまたは複数のベース言語を選択します。 One community site will be created for each language added, and will exist within the same site folder following the best practice described in [Translating Content for Multilingual Sites](../../help/sites-administering/translation.md). 各サイトのルートページには、選択したいずれかの言語の言語コード（例えば、英語では「en」、フランス語では「fr」）で名付けられた子ページが含まれます。

* **[!UICONTROL コミュニティサイト名]**：engage

   * サイトの作成後に名前が容易に変更されないので、重複チェックを行います。
   * コミュニティサイト名の下に最初のURLが表示されます
   * 有効なURLの場合は、ベース言語コード+ &quot;.html&quot;を追加します。
   * *例えば*、http://localhost:4502/content/sites/ `engage/en.html`

* **[!UICONTROL テンプレート]**: 下に降りて～を選ぶ `Reference Site`

「**[!UICONTROL 次へ]**」を選択します。

### 手順 2：デザイン {#step-design}

「デザイン」の手順では、テーマとブランディングバナーを選択する 2 つのセクションが表示されます。

#### コミュニティサイトテーマ {#community-site-theme}

目的のスタイルを選択し、テンプレートに適用します。選択すると、テーマはチェックマーク付きでオーバーレイされます。

![sitetheme](assets/sitetheme.png)

#### コミュニティサイトブランディング {#community-site-branding}

（オプション）サイトページ全体に表示するバナー画像をアップロードします。 バナーはブラウザーの左端およびコミュニティサイトヘッダーとメニュー（ナビゲーションリンク）の間に固定されます。バナーの高さは 120 ピクセルに切り詰められます。バナーがブラウザーの幅や 120 ピクセルの高さに合わせてリサイズされることはありません。

![chlimage_1-353](assets/chlimage_1-353.png) ![chlimage_1-354](assets/chlimage_1-354.png)

「**[!UICONTROL 次へ]**」を選択します。

### 手順 3：設定 {#step-settings}

On the Settings step, before selecting `Next`, notice there are seven sections providing access to configurations involving user management, tagging, moderation, group management, analytics, translation and enablement.

Visit the [Getting Started with AEM Communities for Enablement](getting-started-enablement.md) tutorial to experience working with the enablement features.

#### ユーザー管理 {#user-management}

「[ユーザー管理](sites-console.md#user-management)」タブのチェックボックスをすべてオンにします。

* サイト訪問者が自己登録できるようにするには
* サイト訪問者がサインインせずにサイトを表示できるようにするには
* 他のコミュニティメンバーからのメッセージの送受信を許可するには
* プロファイルの登録と作成を行う代わりにFacebookでのログインを許可するには
* プロファイルの登録と作成を行う代わりに、Twitterでのログインを許可するには

>[!NOTE]
>
>実稼動環境では、カスタムの Facebook アプリケーションおよび Twitter アプリケーションを作成する必要があります。[Facebook と Twitter を使用したソーシャルログイン](social-login.md)を参照してください。

![createsitesettings](assets/createsitesettings.png)

#### タグ付け {#tagging}

The tags which may be applied to community content are controlled by selecting AEM namespaces previously defined through the [Tagging Console](../../help/sites-administering/tags.md#tagging-console) (such as the [Tutorial namespace](setup.md#create-tutorial-tags)).

名前空間は先行入力検索で簡単に検索できます。例：

* &#39;tut&#39;と入力します。
*  `Tutorial`

![chlimage_1-355](assets/chlimage_1-355.png)

#### 役割 {#roles}

[コミュニティメンバーの役割](users.md) は、[役割]セクションの設定を通じて割り当てられます。

コミュニティメンバー（またはメンバーのグループ）がコミュニティマネージャーとしてサイトを体験できるようにするには、先頭入力検索を使用し、ドロップダウンのオプションからメンバーまたはグループ名を選択します。

例：

* 「q」と入力します。
* Select [Quinn Harper](enablement-setup.md#publishcreateenablementmembers)

>[!NOTE]
>
>[トンネルサービス](https://helpx.adobe.com/experience-manager/6-3/communities/using/deploy-communities.html#tunnel-service-on-author) ：パブリッシュ環境にのみ存在するメンバーとグループを選択できます。

![community_roles-1](assets/community_roles-1.png)

#### モデレート {#moderation}

ユーザー生成コンテンツ（UGC）を[モデレート](sites-console.md#moderation)する場合は、デフォルトのグローバル設定を受け入れます。

![chlimage_1-356](assets/chlimage_1-356.png)

#### Analytics {#analytics}

Adobe Analytics のライセンスを持っていて、Analytics のクラウドサービスおよびフレームワークが設定されている場合は、Analytics を有効にしてフレームワークを選択できます。

[コミュニティ機能のための Analytics の設定](analytics.md)を参照してください。

![chlimage_1-357](assets/chlimage_1-357.png)

#### TRANSLATION {#translation}

[翻訳設定](sites-console.md#translation)では、サイトの基本言語に加えて、UGC の翻訳を許可するかどうかと、どの言語に翻訳するかを指定します。

* Check **[!UICONTROL Allow Machine Translation]**
* デフォルトの機械翻訳サービスで、翻訳用にデフォルトの言語を選択したままにする
* デフォルトの翻訳プロバイダーとconfigのままにする
* 言語コピーがないので、グローバルストアは不要です
* Select **[!UICONTROL Translate entire page]**
* デフォルトの永続性オプションをそのまま使用

![chlimage_1-358](assets/chlimage_1-358.png)

#### イネーブルメント {#enablement}

エンゲージメントコミュニティを作成する場合は空白のままにします。

[イネーブルメントコミュニティ](overview.md#enablement-community)をすばやく作成する方法のチュートリアルについて詳しくは、[イネーブルメントのための AEM Communities 使用の手引き](getting-started-enablement.md)を参照してください。

「**[!UICONTROL 次へ]**」を選択します。

### 手順 4：コミュニティサイトの作成 {#step-create-communities-site}

「**[!UICONTROL 作成]**」を選択します。

![chlimage_1-359](assets/chlimage_1-359.png)

プロセスが完了すると、新しいサイトのフォルダーがコミュニティサイトコンソールに表示されます。

![communitiesconsole](assets/communitiessitesconsole.png)

## 新しいコミュニティサイトの公開 {#publish-the-new-community-site}

作成したサイトは、コミュニティ - サイトコンソールで管理する必要があります。このコンソールは、新しいサイトを作成するコンソールと同じものです。

コミュニティサイトのフォルダーを選択して開いた後、サイトアイコンにマウスカーソルを合わせると 4 つのアクションアイコンが表示されます。

![siteactionicons-1](assets/siteactionicons-1.png)

4つ目の楕円アイコン（その他のアクション）を選択すると、「サイトを書き出し」オプションと「サイトを削除」オプションが表示されます。

![siteactionsnew-1](assets/siteactionsnew-1.png)

各アイコンの機能は次のとおりです（左から右の順に説明）。

* **サイトを開く**&#x200B;鉛筆アイコンを選択して、作成者編集モードでコミュニティサイトを開き、ページコンポーネントを追加/設定します。

* **サイトの編集**&#x200B;プロパティアイコンを選択して、プロパティの変更（タイトルやテーマの変更など）を行うためにコミュニティサイトを開きます。

* **サイトの公開**&#x200B;コミュニティサイトを公開するには、世界のアイコンを選択します（例えば、公開サーバーがローカルマシンで実行されている場合は、デフォルトでlocalhost:4503に移動します）。

* **サイトの書き出し**&#x200B;書き出しアイコンを選択して、コミュニティサイトのパッケージを作成し、そのパッケージを [package managerに保存し](../../help/sites-administering/package-manager.md) 、ダウンロードします。

   UGC はサイトパッケージに含まれていません。

* **サイトを削除**

   select the delete icon to delete the community site from within **[!UICONTROL Communities > Sites console]**. サイトを削除すると、UGC やユーザーグループ、アセット、データベースレコードなど、そのサイトに関連付けられているアイテムがすべて削除されます。

![siteactions-1](assets/siteactions-1.png)

>[!NOTE]
>
>パブリッシュインスタンスにデフォルトポートの 4503 を使用していない場合は、デフォルトのレプリケーションエージェントを編集し、ポート番号を正しい値に設定します。
>
>オーサーインスタンスで、メインメニューから
>
>1. Navigate to **[!UICONTROL Tools > Operations > Replication]** menu
>1. Select **[!UICONTROL Agents on author]**
>1. Select **[!UICONTROL Default Agent (publish)]**
>1. Next to **[!UICONTROL Settings]** select **[!UICONTROL Edit]**
>1. エージェント設定のポップアップダイアログで、「トランスポート」タブを選択します
>1. URIで、ポート番号4503を目的のポート番号に変更します。

>
>
例えば、ポート6103を使用するには： `http://localhost:6103/bin/receive?sling:authRequestLogin=1`
>
>1. 「**[!UICONTROL OK]**」を選択します。
>1. （オプション）レプリケーションキュー `Clear` を選択す `Force Retry` るか、リセットします


### サイトの公開 {#select-publish}

公開サーバーが実行中であることを確認したら、地球のアイコンを選択して、コミュニティサイトを公開します。

![chlimage_1-360](assets/chlimage_1-360.png)

コミュニティサイトが正常に公開されると、次のような短いメッセージが表示されます。

![chlimage_1-361](assets/chlimage_1-361.png)

### 新しいコミュニティユーザーグループの確認 {#notice-new-community-user-groups}

新しいコミュニティサイトとともに、新しいユーザーグループが作成されます。各グループには、様々な管理機能に応じて適切な権限が設定されています。For details, visit [User Groups for Community Sites](users.md#usergroupsforcommunitysites).

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

Once a site has been configured and pushed to publish, [configure login mapping](sites-console.md#configure-for-authentication-error) ( `Adobe Granite Login Selector Authentication Handler`) on the publish instance. 利点は、ログイン資格情報が正しく入力されないと、認証エラーによってコミュニティサイトのログインページが再表示され、エラーメッセージが表示されることです。

追加～ `Login Page Mapping` の

* /content/sites/engage/en/signin:/content/sites/engage/en

## オプションの手順 {#optional-steps}

### デフォルトのホームページの変更 {#change-the-default-home-page}

公開サイトをデモ目的で操作するときは、デフォルトのホームページを新しいサイトに変更すると便利です。

これをおこなうには、[CRXDE](http://localhost:4503/crx/de) Lite を使用して、パブリッシュ側で[リソースマッピング](../../help/sites-deploying/resource-mapping.md)テーブルを編集します。

開始するには：

1. 公開時に、管理者権限でサインイン
1. Browse to [http://localhost:4503/crx/de](http://localhost:4503/crx/de)
1. In the project browser, expand `/etc/map`
1. Select the `http` node

   * Select **[!UICONTROL Create Node]**

      * **名前** localhost.4503

         (do *not* use `:`)

      * **Type** sling [:Mapping](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html)

1. With newly created `localhost.4503` node selected

   * 追加特性

      * **名前**：sling:match
      * **タイプ**：String
      * **値**：localhost.4503/\$

         （「$」文字で終わる必要があります）
   * 追加特性

      * **名前**：sling:internalRedirect
      * **タイプ**：String
      * **値**：/content/sites/engage/en.html


1. 「**[!UICONTROL すべて保存]**」を選択します。
1. （オプション）閲覧履歴の削除
1. http://localhost:4503/を参照します。

   * http://localhost:4503/content/sites/engage/en.htmlにアクセス

>[!NOTE]
>
>To disable, simply prepend the `sling:match` property value with an &#39;x&#39; - `xlocalhost.4503/$` - and **[!UICONTROL Save All]**.

![chlimage_1-364](assets/chlimage_1-364.png)

#### トラブルシューティング：マップ保存エラー {#troubleshooting-error-saving-map}

変更を保存できない場合は、ノード名が `localhost.4503`（区切り文字が「ドット」）となっているかを確認してください。`localhost:4503` は有効な名前空間のプレフィックスではないので、`localhost`（区切り文字が「コロン」）という表記は正しくありません。

![chlimage_1-365](assets/chlimage_1-365.png)

#### トラブルシューティング：リダイレクト失敗 {#troubleshooting-fail-to-redirect}

The &#39;**$**&#39; at the end of the regular expression `sling:match`string is crucial, so that only exactly `http://localhost:4503/` is mapped, else the redirect value is prepended to any path that might exist after the server:port in the URL. したがって、AEMがログインページにリダイレクトしようとすると、失敗します。

### サイトの変更 {#modify-the-site}

サイトを最初に作成した後、作成者は[サイトを開くアイコン](sites-console.md#authoring-site-content)を使用して、標準的な AEM のオーサリングアクティビティを実行できます。

また、管理者は[サイトを編集アイコン](sites-console.md#modifying-site-properties)を使用して、タイトルなどのサイトプロパティを変更できます。

After any modification, remember to **save** and **re-publish** the site.

>[!NOTE]
>
>AEM に馴染みがない場合は、[基本操作](../../help/sites-authoring/basic-handling.md)に関するドキュメントおよび[ページのオーサリングのクイックガイド](../../help/sites-authoring/qg-page-authoring.md)を参照してください。