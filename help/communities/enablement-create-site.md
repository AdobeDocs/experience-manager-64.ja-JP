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
translation-type: tm+mt
source-git-commit: 3d2b91565e14e85e9e701663c8d0ded03e5b430c
workflow-type: tm+mt
source-wordcount: '1744'
ht-degree: 52%

---


# イネーブルメントのための新しいコミュニティサイトの作成 {#author-a-new-community-site-for-enablement}

## コミュニティサイトを作成 {#create-community-site}

[コミュニティサイトの作成](sites-console.md) ：コミュニティサイトの作成手順を案内するウィザードを使用します。 It is possible to move forward to the `Next`step or `Back`to the previous step before committing the site in the final step.

新しいコミュニティサイトの作成を開始するには：

[オーサーインスタンス](http://localhost:4502/)を使用します。

* 管理者権限でサインインする
* Navigate to **[!UICONTROL Communities > Sites]**

* 「**[!UICONTROL 作成]**」を選択します。

### Step 1 : Site Template {#step-site-template}

![enablementsitetemplate](assets/enablementsitetemplate.png)

「**サイトテンプレート**」の手順では、URL のタイトル、説明、名前を入力し、コミュニティサイトテンプレートを選択します。次に例を示します。

* **コミュニティサイトのタイトル**: `Enablement Tutorial`

* **コミュニティサイトの説明**: `A site for enabling the community to learn.`

* **コミュニティサイトルート**: (デフォルトのルートの場合は空白のまま `/content/sites`)

* **クラウド設定**：（クラウド設定が指定されていない場合は空欄のままにする）指定されたクラウド設定へのパスを入力します。
* **コミュニティサイトの基本言語**: （単一言語の場合は手を付けないでください）。 英語)プルダウンメニューを使用して *、ドイツ語、イタリア語、フランス語、日本語、スペイン語、ポルトガル語（ブラジル）、中国語（繁体字）、中国語（簡体字）の各言語から* 1つまたは複数のベース言語を選択します。 One community site will be created for each language added, and will exist within the same site folder following the best practice described in [Translating Content for Multilingual Sites](../../help/sites-administering/translation.md). 各サイトのルートページには、選択したいずれかの言語の言語コード（例えば、英語では「en」、フランス語では「fr」）で名付けられた子ページが含まれます。

* **[!UICONTROL コミュニティサイト名]**: `enable`

   * 初期 URL は、コミュニティサイト名の下に表示されます。
   * 有効な URL に、ベース言語コード + 「.html」を追加します。

      *例えば*、http://localhost:4502/content/sites/ `enable/en.html`

* **[!UICONTROL リファレンスサイトテンプレート]**: 下に降りて～を選ぶ `Reference Structured Learning Site Template`

「**[!UICONTROL 次へ]**」を選択します。

### 手順 2：デザイン {#step-design}

「デザイン」の手順では、テーマとブランディングバナーを選択する 2 つのセクションが表示されます。

#### コミュニティサイトテーマ {#community-site-theme}

目的のスタイルを選択し、テンプレートに適用します。選択すると、テーマはチェックマーク付きでオーバーレイされます。

![enablementsitetheme](assets/enablementsitetheme.png)

#### コミュニティサイトブランディング {#community-site-branding}

（オプション）サイトページに表示するバナー画像をアップロードします。バナーはブラウザーの左端およびコミュニティサイトヘッダーとメニュー（ナビゲーションリンク）の間に固定されます。バナーの高さは 120 ピクセルに切り詰められます。バナーがブラウザーの幅や 120 ピクセルの高さに合わせてリサイズされることはありません。

![chlimage_1-284](assets/chlimage_1-284.png) ![chlimage_1](assets/chlimage_1.jpeg)

「**[!UICONTROL 次へ]**」を選択します。

### 手順 3：設定 {#step-settings}

On the Settings step, before selecting `Next`, notice there are seven sections providing access to configurations involving user management, tagging, roles, moderation, analytics, translation, and enablement.

#### ユーザー管理 {#user-management}

It is recommended that [enablement communities](overview.md#enablement-community) be private.

コミュニティサイトを非公開にするとは、匿名のサイト訪問者に対してアクセスを拒否し、自己登録やソーシャルログインを使用禁止にすることです。

Ensure most checkboxes are unchecked for [User Management](sites-console.md#user-management):

* サイト訪問者が自己登録することを許可しない
* 匿名サイト訪問者がサイトに表示することを許可しない
* コミュニティメンバー間でのメッセージングを許可するかどうか（オプション）
* Facebookでのログインを許可しない
* Twitterでのログインを許可しない

![chlimage_1-285](assets/chlimage_1-285.png)

#### タグ付け {#tagging}

The tags which may be applied to community content are controlled by selecting AEM namespaces previously defined through the [Tagging Console](../../help/sites-administering/tags.md#tagging-console) (such as the [Tutorial namespace](enablement-setup.md#create-tutorial-tags)).

また、コミュニティサイトに対してタグ名前空間を選択すると、カタログとイネーブルメントリソースを定義するときに表示される選択肢が制限されます。See [Tagging Enablement Resources](tag-resources.md) for important information.

名前空間は先行入力検索で簡単に検索できます。例：

* &#39;tut&#39;と入力します。
*  `Tutorial`

![chlimage_1-286](assets/chlimage_1-286.png)

### 役割 {#roles}

[コミュニティメンバーの役割](users.md) は、[役割]セクションの設定を通じて割り当てられます。

コミュニティメンバー（またはメンバーのグループ）がコミュニティマネージャーとしてサイトを体験できるようにするには、先頭入力検索を使用し、ドロップダウンのオプションからメンバーまたはグループ名を選択します。

例：

* 「q」と入力します。
* Select [Quinn Harper](enablement-setup.md#publishcreateenablementmembers)

>[!NOTE]
>
>[トンネルサービス](deploy-communities.md#tunnel-service-on-author) ：パブリッシュ環境にのみ存在するメンバーとグループを選択できます。

![community_roles](assets/community_roles.png)

#### モデレート {#moderation}

ユーザー生成コンテンツ（UGC）を[モデレート](sites-console.md#moderation)する場合は、デフォルトのグローバル設定を受け入れます。

![chlimage_1-287](assets/chlimage_1-287.png)

#### Analytics {#analytics}

プルダウンメニューから、このコミュニティサイト用に設定した Analytics クラウドサービスフレームワークを選択します。

スクリーンショットに表示されている選択肢「`Communities`」は、[設定ドキュメント](analytics.md#aem-analytics-framework-configuration)のフレームワークの例です。

![chlimage_1-288](assets/chlimage_1-288.png)

#### TRANSLATION {#translation}

[翻訳設定](sites-console.md#translation)では、UGC の翻訳を許可するかどうかと、どの言語に翻訳するかを指定します。

* Check **[!UICONTROL Allow Machine Translation]**
* デフォルト設定を使用する

![chlimage_1-289](assets/chlimage_1-289.png)

#### イネーブルメント {#enablement}

1 つのイネーブルメントコミュニティに対し、1 人以上のコミュニティ実施可能マネージャーを指定する必要があります。

* **[!UICONTROL 有効化マネージャ]**（必須） 
`Community Enablement Managers` グループを選択して、このコミュニティサイトを管理できます。

   * 「s」と入力します。
   *  `Sirius Nilson`

* **[!UICONTROL Marketing Cloud組織ID]**（オプション）Adobe AnalyticsアカウントのID。有効化レポートに [Video Heartbeat Analytics](analytics.md#video-heartbeat-analytics) を含める場合に必要です。

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

* **サイトを開く**&#x200B;鉛筆アイコンを選択して、作成者編集モードでコミュニティサイトを開き、ページコンポーネントを追加/設定します。

* **サイトの編集**&#x200B;プロパティアイコンを選択して、プロパティの変更（タイトルやテーマの変更など）を行うためにコミュニティサイトを開きます。

* **サイトを公開**&#x200B;コミュニティサイトを公開する（デフォルトでlocalhost:4503に）には、世界共通アイコンを選択します。

* **サイトの書き出し**&#x200B;書き出しアイコンを選択して、コミュニティサイトのパッケージを作成し、そのパッケージを [package managerに保存し](../../help/sites-administering/package-manager.md) 、ダウンロードします。

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

新しいコミュニティサイトとともに、新しいユーザーグループが作成されます。各グループには、様々な管理機能に応じて適切な権限が設定されています。For details, visit [User Groups for Community Sites](users.md#usergroupsforcommunitysites).

For this new community site, given the site name &quot;enable&quot; in Step 1, the new user groups that exist in the publish environment may be seen from the [Communities Members &amp; Groups console](members.md#groups-console):

![chlimage_1-294](assets/chlimage_1-294.png)

### 「Community Enable Members」グループへのメンバー割り当て{#assign-members-to-community-enable-members-group}

On author, with the tunnel service enabled, it is possible to assign the [users created during Initial Setup](enablement-setup.md#publishcreateenablementmembers) to the Community Members group for the newly created community site.

コミュニティグループコンソールでは、メンバーを個別に追加したり、グループのメンバーシップを使用して追加したりできます。

In this example, the group `Community Ski Class` is added as a member of the group `Community Enable Members` as well as member `Quinn Harper`.

* Navigate to **[!UICONTROL Communities > Groups]** console
* Select **[!UICONTROL Community Enable Members]** group
* Enter `ski` into the **[!UICONTROL Add Members To Group]** search box
* Select **[!UICONTROL Community Ski Class]** (group of learners)
* Enter `quinn` into the search box
* Select **[!UICONTROL Quinn Harper]** (enablement resource contact)

* Select **[!UICONTROL Save]**

![chlimage_1-295](assets/chlimage_1-295.png)

## パブリッシュ側の設定 {#configurations-on-publish}

### http://localhost:4503/content/sites/enable/en.html {#http-localhost-content-sites-enable-en-html}

![chlimage_1-296](assets/chlimage_1-296.png)

### 認証エラーの設定 {#configure-for-authentication-error}

Once a site has been configured and pushed to publish, [configure login mapping](sites-console.md#configure-for-authentication-error) ( `Adobe Granite Login Selector Authentication Handler`) on the publish instance. 利点は、ログイン資格情報が正しく入力されないと、認証エラーによってコミュニティサイトのログインページが再表示され、エラーメッセージが表示されることです。

追加～ `Login Page Mapping` の

* /content/sites/enable/en/signin:/content/sites/enable/en

### （オプション）デフォルトのホームページの変更 {#optional-change-the-default-home-page}

公開サイトをデモ目的で操作するときは、デフォルトのホームページを新しいサイトに変更すると便利です。

これをおこなうには、[CRX|DE](http://localhost:4503/crx/de) Lite を使用して、パブリッシュ側で[リソースマッピング](../../help/sites-deploying/resource-mapping.md)テーブルを編集します。

開始するには、次のようにします。

1. 公開時に、CRXDEにアクセスし、管理者権限でログインします

   * For example, browse to [http://localhost:4503/crx/de](http://localhost:4503/crx/de) and login with `admin/admin`

1. In the project browser, expand `/etc/map`
1. Select the `http` node

   * Select **[!UICONTROL Create Node]**

      * **名前** localhost.4503

         (Do *not* use `:`)

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
      * **値**：/content/sites/enable/en.html


1. 「**[!UICONTROL すべて保存]**」を選択します。
1. （オプション）閲覧履歴の削除
1. http://localhost:4503/を参照します。

   * http://localhost:4503/content/sites/enable/en.htmlにアクセス

>[!NOTE]
>
>To disable, simply prepend the `sling:match` property value with an &#39;x&#39; - `xlocalhost.4503/$` - and **[!UICONTROL Save All]**.

![chlimage_1-297](assets/chlimage_1-297.png)

#### トラブルシューティング：マップ保存エラー {#troubleshooting-error-saving-map}

変更を保存できない場合は、ノード名が `localhost.4503`（区切り文字が「ドット」）となっているかを確認してください。`localhost:4503` は有効な名前空間のプレフィックスではないので、`localhost`（区切り文字が「コロン」）という表記は正しくありません。

![chlimage_1-298](assets/chlimage_1-298.png)

#### トラブルシューティング：リダイレクト失敗 {#troubleshooting-fail-to-redirect}

The &#39;**$**&#39; at the end of the regular expression `sling:match`string is crucial, so that only exactly `http://localhost:4503/` is mapped, else the redirect value is prepended to any path that might exist after the server:port in the URL. したがって、AEMがログインページにリダイレクトしようとすると、失敗します。

## コミュニティサイトの変更 {#modifying-the-community-site}

サイトを最初に作成した後、作成者は[サイトを開くアイコン](sites-console.md#authoring-site-content)を使用して、標準的な AEM のオーサリングアクティビティを実行できます。

また、管理者は[サイトを編集アイコン](sites-console.md#modifying-site-properties)を使用して、タイトルなどのサイトプロパティを変更できます。

変更後は、必ず&#x200B;**保存**&#x200B;して再&#x200B;**公開**&#x200B;してください。

>[!NOTE]
>
>AEM に馴染みがない場合は、[基本操作](../../help/sites-authoring/basic-handling.md)に関するドキュメントおよび[ページのオーサリングのクイックガイド](../../help/sites-authoring/qg-page-authoring.md)を参照してください。

### カタログの追加 {#add-a-catalog}

このコミュニティサイトに選択されたコミュニティサイトテンプレートには、カタログ機能が含まれています。

含まれていない場合は、カタログ機能を簡単に追加できます。これにより、有効化リソースや学習パスに割り当てられていないコミュニティの他のメンバーが、カタログから有効化リソースを選択できるようになります。

サイト構造にカタログ機能が既に含まれている場合、タイトルが変わることがあります。

To modify the site&#39;s structure, navigate to the **[!UICONTROL Communities, Sites]** console, open the `enable` folder, and select the **Edit Site** icon to access the properties of `Enablement Tutorial`.

構造パネルを選択し、カタログを追加するか、既存のカタログを変更します。

* **タイトル**: `Ski Catalog`

* **URL**: `catalog`

* **すべての名前空間を選択**：デフォルトのままにします。
* Select **[!UICONTROL Save]**

![chlimage_1-299](assets/chlimage_1-299.png)

位置アイコンを使用し、カタログ機能を Assignments の後の 2 番目の位置に移動します。

![chlimage_1-300](assets/chlimage_1-300.png)

右上隅の「**[!UICONTROL 保存]**」を選択してコミュニティサイトに対する変更を保存します。

その後、サイトを再び&#x200B;**公開**&#x200B;します。