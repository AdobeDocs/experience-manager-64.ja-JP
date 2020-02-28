---
title: コミュニティグループコンソール
seo-title: コミュニティグループコンソール
description: グループコンソールにより、コミュニティグループを作成できます
seo-description: グループコンソールにより、コミュニティグループを作成できます
uuid: 7dac2d1b-78fc-4b39-a2cb-100f1e220c23
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.4/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 1293c01a-7308-494a-ab48-bd9938205b81
pagetitle: Community Groups Console
translation-type: tm+mt
source-git-commit: 28948f1f8678512f8fc970a4289cb01cde86c5c2

---


# コミュニティグループコンソール {#community-groups-console}

The Groups console provides access to creating community groups when a community site&#39;s [template structure](sites-console.md#step1) includes the [groups function](functions.md#groups-function).

* グループは、他のグループ内にネストすることができます。This happens when the [structure of the new group](tools-groups.md) contains the groups function.
* 作成者環境に限り、サイト作成ウィザードに似たグループ作成ウィザードがあります。
* メンバーがパブリッシュ環境からグループを作成できるかどうかは、コミュニティサイト構造またはコミュニティグループ構造へのグループ機能の追加時に設定できます。

Of the three group templates included, only the `Reference Group` template includes a groups function in its structure.

コミュニティグループには、次のような側面があります。

* 作成：新しいグループは作成者に対して作成でき、オプションで公開時に作成できます
* 制御：グループは、開いているか、秘密にしている
* 入れ子：グループは、0個以上のグループを含むことができる

>[!NOTE]
>
>[コミュニティグループコンソールが追加される](https://helpx.adobe.com/in/experience-manager/6-3/communities/using/version-history.html#FeaturePack1FP1)前にパブリッシュ環境で作成されたコミュニティグループは、コミュニティグループコンソールに一覧表示されないため、コンソールを使用して変更することはできません。

>[!NOTE]
>
>This Groups console, only accessible from the Communities Sites console, is not to be confused with the member [Groups console](members.md) for managing member groups.
>
>メンバーグループは、パブリッシュ環境に登録されたユーザーグループであり、[トンネルサービス](deploy-communities.md#tunnel-service-on-author)を使用してオーサー環境からアクセスします。

## グループ作成 {#group-creation}

グループコンソールにアクセスするには：

* 作成者の場合、管理者権限でサインイン
* From global navigation: **[!UICONTROL Communities > Sites]**
* 既存のコミュニティサイトフォルダを選択して開きます
* フォルダ内のコミュニティサイトのインスタンスを選択します

   * コミュニティサイトの構造には、グループ機能が含まれている必要があります
   * These screen shots are from the Getting Started tutorial after [creating groups on publish](published-site.md)

![chlimage_1-133](assets/chlimage_1-133.png)

**[!UICONTROL グループフォルダー]**&#x200B;を選択して、開きます。

開いたら、オーサーまたはパブリッシュで作成されたすべての既存のグループが表示されます。

このグループコンソールから、新しいグループを作成できます。

![chlimage_1-134](assets/chlimage_1-134.png)

* Select **[!UICONTROL Create Group]** button

### 手順 1：コミュニティグループテンプレート {#step-community-group-template}

![多言語群](assets/multilingualgroup.png)

* **[!UICONTROL コミュニティグループのタイトル]**:グループの表示タイトル。

   タイトルは、グループのパブリッシュされたサイトに表示されます。

* **[!UICONTROL コミュニティグループの説明]**:グループの説明。
* **[!UICONTROL コミュニティグループルート]**:グループのルートパス。

   デフォルトのルートは親サイトですが、ルートは Web サイト内の任意の場所に移動できます。変更することはお勧めしません。

* **[!UICONTROL 追加のコミュニティグループ言語]** メニュー：プルダウンメニューを使用して、利用可能なコミュニティグループ言語を選択します。 このメニューには、親コミュニティサイトを作成できる言語がすべて表示されます。この中から言語を選択することで、1 回の手順で複数のロケールにグループを作成できます。指定した複数の言語で、それぞれのコミュニティサイトのグループコンソールに同じグループが作成されます。

* **[!UICONTROL コミュニティグループ名]**:URLに表示されるグループのルートページの名前

   * グループの作成後に簡単に変更できないので、名前を再確認します。
   * ベースURLは、 `Community Group Name`
   * 有効なURLの場合は、「.html」を追加します。

      *例えば*、 `http://localhost:4502/content/sites/mysight/en/mygroup.html`

* **[!UICONTROL コミュニティグループテンプレート]** メニュー：プルダウンメニューを使用して、利用可能なコミュニティグル [ープテンプレートを選択しま](tools.md)す。

### 手順 2：デザイン {#step-design}

#### コミュニティグループのテーマ {#community-group-theme}

![communitygrouptheme](assets/communitygrouptheme.png)

このフレームワークでは、レスポンシブで柔軟なサイトデザインを実現できるよう、[Twitter Bootstrap](https://twitterbootstrap.org/) を使用しています。プリロードされた多数のブートストラップテーマの1つを選択して、選択したコミュニティグループテンプレートのスタイルを設定したり、ブートストラップテーマをアップロードしたりできます。

選択すると、テーマの上に不透明な青色のチェックマークのオーバーレイが表示されます。

親サイトのテーマとは異なるテーマを選択することもできます。

コミュニティサイトがパブリッシュされた後、[プロパティを編集](#modifying-group-properties)して、別のテーマを選択できます。

#### コミュニティグループブランディング {#community-group-branding}

![chlimage_1-135](assets/chlimage_1-135.png)

コミュニティサイトブランディングとは、各ページ上部にヘッダーとして表示される画像のことです。他のサイトページとは異なるグループ用のバナーを表示することができます。

画像の幅は、予想されるブラウザー内でのページの表示に合わせます。画像の高さは 120 ピクセルにします。

画像を選択するときは、次の点に注意してください。

* 画像の高さは、画像の上端から120ピクセルに切り抜かれます。
* 画像はブラウザーウィンドウの左端に固定されます
* 画像の幅が…のようなサイズ変更は行われません。

   * ブラウザーの幅より小さい場合、画像は水平方向に繰り返されます
   * ブラウザーの幅よりも大きい場合、画像は切り抜かれたように見えます

### 手順 3：設定 {#step-settings}

#### モデレート {#moderation}

![chlimage_1-136](assets/chlimage_1-136.png)

デフォルトで、親コミュニティサイトのモデレーターリストが継承されます。

グループに固有のモデレーターを追加できます。

* （公開環境から）メンバーを検索し、モデレーターとして追加します

#### メンバーシップ {#membership}

メンバーシップ設定によって、コミュニティグループをセキュリティ保護する 3 つの方法のうち 1 つを選択できます。

![chlimage_1-137](assets/chlimage_1-137.png)

* オプションのメンバーシップ

   選択した場合、コミュニティグループはパブリックグループです。 サイトメンバーは、明示的にグループに参加せずに、グループに参加して投稿することができます。 デフォルトで選択されています。
* 必要なメンバーシップ

   選択した場合、コミュニティグループは開かれたグループです。 コミュニティサイトのメンバーは、グループのコンテンツを表示できますが、コンテンツを投稿するには、グループに参加する必要があります。 Members join by selecting the `Join` button in the publish environment. 初期設定では選択されていません。

* 制限されたメンバーシップ

   選択した場合、コミュニティグループは秘密グループです。 コミュニティメンバーは明示的に招待する必要があります。 招待されたメンバーは検索ボックスに入力されます。 Members may be added later using the [Members and Groups consoles](members.md) the author environment. 初期設定では選択されていません。

#### サムネイル {#thumbnail}

![chlimage_1-138](assets/chlimage_1-138.png)

サムネイルは、オーサーおよびパブリッシュのグループに対して表示される画像です。

グループ画像の最適なサイズは、サポートされている画像形式（JPG や PNG など）の 170 x 90 ピクセルです。

画像を追加しない場合は、デフォルトの画像が表示されます。

![chlimage_1-139](assets/chlimage_1-139.png)

### 手順 4：グループの作成 {#step-create-group}

![chlimage_1-140](assets/chlimage_1-140.png)

If any adjustments are needed, use the **Back** button to make them.

Once **Create** is selected and started, the process of creating the group cannot be interrupted.

処理が完了すると、新しいサブコミュニティサイト（グループ）のカードがCommunitiesのサイトグループコンソールに表示されます。ここから作成者がページコンテンツを追加したり、管理者がサイトのプロパティを変更したりできます。

![createcommunitygroup-1](assets/createcommunitygroup-1.png)

>[!NOTE]
>
>それぞれのコミュニティサイトのコミュニティグループコンソールに、[手順 1：コミュニティグループテンプレート](groups.md#step1communitygrouptemplate)の「追加の使用可能なコミュニティグループの言語」で指定したすべての言語でグループが作成されます。

## グループコンテンツのオーサリング {#authoring-group-content}

![chlimage_1-141](assets/chlimage_1-141.png)

グループのページコンテンツは、他の AEM ページと同じツールでオーサリングできます。グループをオーサリング用に開くには、グループカードの上にカーソルを置くと表示される「サイトを開く」アイコンを選択します。

## グループのプロパティの変更 {#modifying-group-properties}

既存のサブコミュニティサイトのプロパティは、コミュニティグループの作成プロセスで指定し、グループカードの上にカーソルを置くと表示される「サイトを編集」アイコンを選択して変更できます。

![chlimage_1-142](assets/chlimage_1-142.png)

以下のプロパティの詳細は、[グループ作成](#group-creation)で説明した内容と同じです。ネストされたグループは、パブリッシュ環境でも作成者環境でも、変更できます。

![chlimage_1-143](assets/chlimage_1-143.png)

### 基本事項の変更 {#modify-basic}

基本パネルでは、次のものを変更できます。

* コミュニティグループのタイトル
* コミュニティグループの説明

コミュニティグループ名は変更できません。

別のコミュニティグループテンプレートを選択しても、テンプレートとサイトの間に関係は残っていないので、既存のコミュニティグループサイトに影響が及ぶことはありません。

その一方で、サブコミュニティの[構造](#modify-structure)は変更できます。

### 構造の変更 {#modify-structure}

構造パネルでは、オーサー環境またはパブリッシュ環境でサブコミュニティを作成するときに選択したコミュニティグループテンプレートから最初に作成した構造を変更できます。パネルから、

* Drag-and-drop additional [community functions](functions.md) into the site structure
* サイト構造内のコミュニティ関数のインスタンスで、次の操作を行います。

   * **`gear icon`**

      Edit settings, including the display title and URL name as well as [privileged members groups](users.md#privilegedmembersgroups)

   * **`trashcan icon`**

      サイト構造から関数を削除（削除）

   * **`grid icon`**

      サイトのトップレベルナビゲーションバーに表示される関数の順序を変更する

>[!CAUTION]
>
>表示タイトルは副作用なく変更できますが、コミュニティサイトに属するコミュニティ機能のURL名を編集することはお勧めしません。
>
>例えば、URL の名前を変更しても、既存の UGC は移動されません。そのため、UGC が「失われる」ことになります。

>[!CAUTION]
>
>The groups function must *not* be the *first nor the only* function in the site structure.
>
>他の機能（[ページ機能](functions.md#page-function)など）を含め、その機能を 1 番目にリストする必要があります。

#### 例：サブコミュニティ（グループ）構造へのカレンダー機能の追加 {#example-adding-a-calendar-function-to-a-sub-community-group-structure}

![chlimage_1-144](assets/chlimage_1-144.png)

### デザインの変更 {#modify-design}

デザインパネルでは、次のものを変更できます。

* [コミュニティグループのテーマ](#community-group-theme)
* [コミュニティグループブランディング](#community-group-branding)

   * パネルの下部までスクロールして、ブランド画像を変更します

### 設定の変更 {#modify-settings}

設定パネルでは、コミュニティの[モデレーター](#moderation)を追加できます。

### メンバーシップの変更 {#modify-membership}

[メンバーシップ](#membership)パネルは情報提供のみを目的としています。設定されたグループメンバーシップのタイプは、オプション、必須、制限のいずれであっても変更できません。

### サムネイルの変更 {#modify-thumbnail}

[サムネイル](#thumbnail)パネルでは、コミュニティグループを表す画像をアップロードできます。この画像は、パブリッシュ環境でサイト訪問者に表示され、オーサー環境のコミュニティサイトのグループコンソールにも表示されます。

## グループの公開 {#publishing-the-group}

![chlimage_1-145](assets/chlimage_1-145.png)

After a community group has been newly created or modified, it is possible to publish (activate) the group by selecting the `Publish Site` icon.

グループが正常に公開されると、メッセージが表示されます。

![chlimage_1-146](assets/chlimage_1-146.png)

>[!CAUTION]
>
>親コミュニティサイトおよび親グループが既に公開されている必要があります。
>
>コミュニティサイトおよびネストされたグループは、階層の上から下の順に公開される必要があります。

## グループの削除 {#deleting-the-group}

![deleteicon](assets/deleteicon.png)

コミュニティグループコンソール内のグループを削除するには、グループを削除アイコンを選択します。このアイコンは、グループにマウスポインターを置くと表示されます。

グループを削除すると、グループに関連付けられているアイテムはすべて削除されます。例えば、グループのコンテンツはすべて永久に削除され、ユーザーメンバーシップはシステムから削除されます。
