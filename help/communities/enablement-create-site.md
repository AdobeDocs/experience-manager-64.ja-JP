---
title: イネーブルメントのための新しいコミュニティサイトの作成
seo-title: Author a New Community Site for Enablement
description: イネーブルメント用のコミュニティサイトを作成します。
seo-description: Create a community site for enablement
uuid: 6822cc99-e272-4661-bddf-aa0800b88c41
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.4/COMMUNITIES
topic-tags: introduction
content-type: reference
discoiquuid: aff8b79f-dd4e-486e-9d59-5d09dfe34f27
exl-id: 5b16c775-3bd0-4a55-ba9e-f326224e8bae
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '1731'
ht-degree: 4%

---

# イネーブルメントのための新しいコミュニティサイトの作成 {#author-a-new-community-site-for-enablement}

## コミュニティサイトを作成 {#create-community-site}

[コミュニティサイトの作成](sites-console.md) は、コミュニティサイトの作成手順をガイドするウィザードを使用します。 を `Next`手順または `Back`を前の手順に戻してから、最後の手順でサイトをコミットします。

新しいコミュニティサイトの作成を開始するには：

の使用 [オーサーインスタンス](http://localhost:4502/)

* 管理者権限でログイン
* に移動します。 **[!UICONTROL コミュニティ/サイト]**

* 選択 **[!UICONTROL 作成]**

### 手順 1:サイトテンプレート {#step-site-template}

![enablementsitetemplate](assets/enablementsitetemplate.png)

の **サイトテンプレート** 手順を説明し、タイトル、説明、URL の名前を入力し、コミュニティサイトテンプレートを選択します。次に例を示します。

* **コミュニティサイトのタイトル**: `Enablement Tutorial`

* **コミュニティサイトの説明**: `A site for enabling the community to learn.`

* **コミュニティサイトのルート**:（デフォルトのルートの場合は空白のままにします） `/content/sites`)

* **クラウド設定**:（クラウド設定が指定されていない場合は空白にします）指定したクラウド設定へのパスを指定します。
* **コミュニティサイトの基本言語**:（単一言語の場合は、手を付けないでください）。英語 ) プルダウンメニューを使用して 1 つを選択します *以上* 使用可能な言語 ( ドイツ語、イタリア語、フランス語、日本語、スペイン語、ポルトガル語（ブラジル）、中国語（繁体字）、中国語（簡体字）)) のベース言語。 追加された言語ごとに 1 つのコミュニティサイトが作成され、 [多言語サイトのコンテンツの翻訳](../../help/sites-administering/translation.md). 各サイトのルートページには、選択した言語の 1 つの言語コード（英語の場合は「en」、フランス語の場合は「fr」など）で名前が付けられた子ページが含まれます。

* **[!UICONTROL コミュニティサイト名]**: `enable`

   * 初期 URL がコミュニティサイト名の下に表示されます
   * 有効な URL に、ベース言語コード+ &quot;.html&quot;を追加します。

      *例：*, http://localhost:4502/content/sites/ `enable/en.html`

* **[!UICONTROL 参照サイトテンプレート]**:引っ張って選ぶ `Reference Structured Learning Site Template`

選択 **[!UICONTROL 次へ]**

### 手順 2:デザイン {#step-design}

デザインの手順は、テーマとブランディングバナーを選択するための 2 つの節で示します。

#### コミュニティサイトのテーマ {#community-site-theme}

テンプレートに適用するスタイルを選択します。 選択すると、テーマにチェックマークが付きます。

![enablementsitetheme](assets/enablementsitetheme.png)

#### コミュニティサイトのブランディング {#community-site-branding}

（オプション）サイトのページ全体に表示するバナー画像をアップロードします。 バナーは、ブラウザーの左端、コミュニティサイトのヘッダーとメニュー（ナビゲーションリンク）の間に固定されます。 バナーの高さは 120 ピクセルに切り抜かれます。 バナーのサイズは、ブラウザーの幅と 120 ピクセルの高さに合わせて変更されません。

![chlimage_1-284](assets/chlimage_1-284.png) ![chlimage_1](assets/chlimage_1.jpeg)

「**[!UICONTROL 次へ]**」を選択します。

### 手順 3:設定 {#step-settings}

設定ステップで、選択する前に `Next`には、ユーザー管理、タグ付け、役割、モデレート、分析、翻訳およびイネーブルメントに関する設定にアクセスできる 7 つの節があることに注意してください。

#### ユーザー管理 {#user-management}

を推奨します。 [実施可能コミュニティ](overview.md#enablement-community) プライベートにして。

コミュニティサイトは、匿名のサイト訪問者がアクセスを拒否されたり、自己登録やソーシャルログインを使用しなかったりすると、非公開になります。

ほとんどのチェックボックスがオフになっていることを確認します。 [ユーザー管理](sites-console.md#user-management):

* サイト訪問者の自己登録を許可しない
* 匿名のサイト訪問者に対し、サイトの閲覧を許可しない
* コミュニティメンバー間でのメッセージングを許可するかどうか（オプション）
* facebookでのログインを許可しない
* twitterでのログインを許可しない

![chlimage_1-285](assets/chlimage_1-285.png)

#### タグ付け {#tagging}

コミュニティコンテンツに適用できるタグを制御するには、以前に [タグ付けコンソール](../../help/sites-administering/tags.md#tagging-console) ( [チュートリアル名前空間](enablement-setup.md#create-tutorial-tags)) をクリックします。

また、コミュニティサイトでタグ名前空間を選択すると、カタログとイネーブルメントリソースの定義時に表示される選択肢が制限されます。 詳しくは、 [イネーブルメントリソースのタグ付け](tag-resources.md) 重要な情報を参照してください。

名前空間を検索するには、先頭入力検索を使用すると簡単です。 例：

* &#39;tut&#39;と入力します
* 選択 `Tutorial`

![chlimage_1-286](assets/chlimage_1-286.png)

### 役割 {#roles}

[コミュニティメンバーの役割](users.md) は、「役割」セクションの設定を通じて割り当てられます。

コミュニティメンバー（またはメンバーのグループ）がコミュニティマネージャーとしてサイトを体験するには、先行入力検索を使用して、ドロップダウンのオプションからメンバーまたはグループ名を選択します。

例：

* 「q」と入力します。
* 選択 [クインハーパー](enablement-setup.md#publishcreateenablementmembers)

>[!NOTE]
>
>[トンネルサービス](deploy-communities.md#tunnel-service-on-author) パブリッシュ環境にのみ存在するメンバーとグループを選択できます。

![community_roles](assets/community_roles.png)

#### モデレート {#moderation}

のデフォルトのグローバル設定を受け入れる [モデレート](sites-console.md#moderation) ユーザー生成コンテンツ (UGC)。

![chlimage_1-287](assets/chlimage_1-287.png)

#### 分析 {#analytics}

プルダウンメニューから、このコミュニティサイト用に設定された Analytics クラウドサービスフレームワークを選択します。

スクリーンショットに表示される選択範囲。 `Communities`は、 [設定ドキュメント。](analytics.md#aem-analytics-framework-configuration)

![chlimage_1-288](assets/chlimage_1-288.png)

#### 翻訳 {#translation}

この [翻訳設定](sites-console.md#translation) UGC を翻訳できるかどうか、および翻訳できる場合はどの言語に翻訳するかを指定します。

* チェック **[!UICONTROL 機械翻訳を許可]**
* デフォルト設定を使用

![chlimage_1-289](assets/chlimage_1-289.png)

#### 有効化 {#enablement}

イネーブルメントコミュニティの場合は、1 つ以上のコミュニティイネーブルメントマネージャーを特定する必要があります。

* **[!UICONTROL 実施可能マネージャー]**
（必須） 
`Community Enablement Managers` このコミュニティサイトを管理するために、グループを選択できます。

   * 「s」と入力します。
   * 選択 `Sirius Nilson`

* **[!UICONTROL Marketing Cloud組織 ID]**
（オプション） Adobe Analyticsアカウントの ID で、 [ビデオハートビート分析](analytics.md#video-heartbeat-analytics) （イネーブルメントレポート内）

![chlimage_1-290](assets/chlimage_1-290.png)

「**[!UICONTROL 次へ]**」を選択します。

### 手順 4:コミュニティサイトを作成 {#step-create-community-site}

「**[!UICONTROL 作成]**」を選択します。

![chlimage_1-291](assets/chlimage_1-291.png)

処理が完了すると、新しいサイトのフォルダーがコミュニティ — サイトコンソールに表示されます。

![enablementsitecreated](assets/enablementsitecreated.png)

### 新しいコミュニティサイトを公開 {#publish-the-new-community-site}

作成したサイトは、コミュニティ — サイトコンソール、および新しいサイトを作成できる同じコンソールから管理する必要があります。

コミュニティサイトのフォルダーを選択した後、サイトアイコンの上にマウスポインターを置くと、次の 4 つのアクションアイコンが表示されます。

![siteactionicons](assets/siteactionicons.png)

省略記号アイコン（その他のアクションアイコン）を選択すると、「サイトを書き出し」および「サイトを削除」オプションが表示されます。

![siteactionsnew](assets/siteactionsnew.png)

左から右に、次のように表示されます。

* **サイトを開く**
鉛筆アイコンを選択してコミュニティサイトをオーサリング編集モードで開き、ページコンポーネントを追加または設定します。

* **サイトを編集**
プロパティアイコンを選択してコミュニティサイトを開き、タイトルやテーマの変更などのプロパティを変更します。

* **サイトを公開**
コミュニティサイトを公開する場合は、世界アイコンを選択します（デフォルトでは localhost:4503 に公開）。

* **サイトを書き出し**
書き出しアイコンを選択して、コミュニティサイトのパッケージを作成し、そのパッケージを次の場所に保存します。 [パッケージマネージャー](../../help/sites-administering/package-manager.md) とダウンロードされました。

   UGC はサイトパッケージに含まれていません。

* **サイトを削除**
コミュニティサイトを削除するには、コミュニティサイトコンソールでサイトにマウスを合わせたときに表示される「サイトを削除」アイコンを選択します。 この操作により、UGC、ユーザーグループ、アセット、データベースレコードなど、サイトに関連するすべての項目が削除されます。

![enablesiteactions](assets/enablesiteactions.png)

#### 公開を選択 {#select-publish}

世界のアイコンを選択して、コミュニティサイトを公開します。

![chlimage_1-292](assets/chlimage_1-292.png)

サイトが公開されたことを示すメッセージが表示されます。

![chlimage_1-293](assets/chlimage_1-293.png)

## コミュニティユーザーとユーザーグループ {#community-users-user-groups}

### 新しいコミュニティユーザーグループに通知 {#notice-new-community-user-groups}

新しいコミュニティサイトと共に、様々な管理機能に対して適切な権限が設定された新しいユーザーグループが作成されます。 詳しくは、 [コミュニティサイトのユーザーグループ](users.md#usergroupsforcommunitysites).

この新しいコミュニティサイトでは、手順 1 でサイト名「enable」を指定すると、パブリッシュ環境に存在する新しいユーザーグループが [コミュニティメンバーとグループコンソール](members.md#groups-console):

![chlimage_1-294](assets/chlimage_1-294.png)

### メンバーをコミュニティ有効化メンバーグループに割り当て {#assign-members-to-community-enable-members-group}

オーサー環境では、トンネルサービスを有効にして、 [初期設定時に作成されたユーザー](enablement-setup.md#publishcreateenablementmembers) 新しく作成したコミュニティサイトのコミュニティメンバーグループに追加します。

コミュニティグループコンソールを使用して、メンバーを個別に追加したり、グループのメンバーシップを通じて追加したりできます。

この例では、グループ `Community Ski Class` はグループのメンバーとして追加されます `Community Enable Members` 同様に、メンバー `Quinn Harper`.

* に移動します。 **[!UICONTROL コミュニティ/グループ]** コンソール
* 選択 **[!UICONTROL コミュニティを有効にするメンバー]** グループ
* 入力 `ski` に **[!UICONTROL メンバーをグループに追加]** 検索ボックス
* 選択 **[!UICONTROL コミュニティスキークラス]** （学習者のグループ）
* 入力 `quinn` 検索ボックスに
* 選択 **[!UICONTROL クインハーパー]** （イネーブルメントリソースの連絡先）

* 選択 **[!UICONTROL 保存]**

![chlimage_1-295](assets/chlimage_1-295.png)

## 公開時の設定 {#configurations-on-publish}

### http://localhost:4503/content/sites/enable/en.html {#http-localhost-content-sites-enable-en-html}

![chlimage_1-296](assets/chlimage_1-296.png)

### 認証エラー用の設定 {#configure-for-authentication-error}

サイトが設定され、パブリッシュにプッシュされると、 [ログインマッピングの設定](sites-console.md#configure-for-authentication-error) ( `Adobe Granite Login Selector Authentication Handler`) をパブリッシュインスタンスでクリックします。 ログイン資格情報が正しく入力されていない場合、認証エラーによってコミュニティサイトのログインページが再度表示され、エラーメッセージが表示されるという利点があります。

を追加します。 `Login Page Mapping` as

* /content/sites/enable/en/signin:/content/sites/enable/en

### （オプション）デフォルトのホームページの変更 {#optional-change-the-default-home-page}

公開サイトをデモ用に使用する場合は、デフォルトのホームページを新しいサイトに変更すると便利です。

そのためには、 [CRX|DE](http://localhost:4503/crx/de) を編集するには Lite を使用します。 [リソースマッピング](../../help/sites-deploying/resource-mapping.md) パブリッシュに関するテーブル。

使い始めるには

1. 公開時に、CRXDE にアクセスし、管理者権限でログインします。

   * 例えば、 [http://localhost:4503/crx/de](http://localhost:4503/crx/de) にログインし、 `admin/admin`

1. プロジェクトブラウザで、を展開します。 `/etc/map`
1. を選択します。 `http` ノード

   * 選択 **[!UICONTROL ノードを作成]**

      * **名前** localhost.4503

         ( 実行 *not* use `:`)

      * **タイプ** [sling:Mapping](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html)

1. 新しく作成された `localhost.4503` 選択されたノード

   * プロパティの追加

      * **名前** sling:match
      * **タイプ** 文字列
      * **値** localhost.4503/\$

         （「$」文字で終わる必要があります）
   * プロパティの追加

      * **名前** sling:internalRedirect
      * **タイプ** 文字列
      * **値** /content/sites/enable/en.html


1. 選択 **[!UICONTROL すべて保存]**
1. （オプション）閲覧履歴を削除します
1. http://localhost:4503/を参照します。

   * http://localhost:4503/content/sites/enable/en.htmlに到着します。

>[!NOTE]
>
>無効にするには、 `sling:match` プロパティ値に「x」を付ける — `xlocalhost.4503/$`  — および **[!UICONTROL すべて保存]**.

![chlimage_1-297](assets/chlimage_1-297.png)

#### トラブルシューティング：マップ保存エラー {#troubleshooting-error-saving-map}

変更を保存できない場合は、ノード名がであることを確認してください。 `localhost.4503`（ドット区切り記号を使用し、使用しない） `localhost:4503` 「コロン」区切り文字を使用する場合は、 `localhost`は有効な名前空間のプレフィックスではありません。

![chlimage_1-298](assets/chlimage_1-298.png)

#### トラブルシューティング：リダイレクトに失敗 {#troubleshooting-fail-to-redirect}

&#39;**$**&#39; （正規表現の末尾） `sling:match`文字列が非常に重要なので、正確に `http://localhost:4503/` がマッピングされている場合、リダイレクト値の前に、URL の server:port の後に存在する可能性があるすべてのパスが追加されます。 したがって、AEMがログインページにリダイレクトしようとすると、失敗します。

## コミュニティサイトの変更 {#modifying-the-community-site}

サイトが最初に作成された後、作成者は [サイトを開くアイコン](sites-console.md#authoring-site-content) 標準のAEMオーサリングアクティビティを実行する場合。

また、管理者は [サイトを編集アイコン](sites-console.md#modifying-site-properties) をクリックして、サイトのプロパティ（タイトルなど）を変更します。

変更後は、次の操作をおこなってください。 **保存** および re **公開** サイト。

>[!NOTE]
>
>AEMに詳しくない場合は、 [基本操作](../../help/sites-authoring/basic-handling.md) および [ページのオーサリングのクイックガイド](../../help/sites-authoring/qg-page-authoring.md).

### カタログを追加 {#add-a-catalog}

このコミュニティサイト用に選択したコミュニティサイトテンプレートには、カタログ機能を含める必要があります。

そうでない場合は、カタログ機能を簡単に追加できます。 これにより、イネーブルメントリソースや学習パスに割り当てられていないコミュニティの他のメンバーが、カタログからイネーブルメントリソースを選択できるようになります。

サイト構造にカタログ機能が既に含まれている場合は、そのタイトルを変更できます。

サイトの構造を変更するには、 **[!UICONTROL コミュニティ、サイト]** コンソールで、 `enable` フォルダを選択し、 **サイトを編集** アイコンをクリックして、 `Enablement Tutorial`.

カタログを追加または既存のカタログを変更するには、[ 構造 ] パネルを選択します。

* **タイトル**: `Ski Catalog`

* **URL**: `catalog`

* **すべての名前空間を選択**:デフォルトのままにします。
* 選択 **[!UICONTROL 保存]**

![chlimage_1-299](assets/chlimage_1-299.png)

[ 位置 ] アイコンを使用して、[ 割り当て ] の後の 2 番目の位置にカタログ機能を移動します。

![chlimage_1-300](assets/chlimage_1-300.png)

選択 **[!UICONTROL 保存]** をクリックして、コミュニティサイトへの変更を保存します。

次に、再度&#x200B;**公開** サイト。
