---
title: 公開したサイトを使ってみる
seo-title: Experience the Published Site
description: 公開したサイトの参照
seo-description: Browse to a published site
uuid: f510224c-d991-4528-864d-44672138740c
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.4/COMMUNITIES
topic-tags: introduction
content-type: reference
discoiquuid: 4dc54701-68b9-49dd-a212-b0b53330c1c0
exl-id: 8f716a59-1116-4855-baeb-3997de71b55f
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '1135'
ht-degree: 40%

---

# 公開したサイトを使ってみる {#experience-the-published-site}

## パブリッシュサーバー上の新しいサイトの参照 {#browse-to-new-site-on-publish}

新しく作成したコミュニティサイトが公開されたので、次はこのサイト作成時に表示された URL を参照します。ただし、このとき参照するのはパブリッシュサーバー上の URL です。次に例を示します。

* 作成者 URL = http://localhost:4502/content/sites/engage/en.html
* 公開 URL = http://localhost:4503/content/sites/engage/en.html

どのメンバーがオーサーインスタンスにサインインし、どのメンバーがパブリッシュインスタンスにサインインしているかを混乱なく把握するために、インスタンスごとに異なるブラウザーを使用することを推奨します。

公開済みサイトに初めてアクセスするときは、通常、そのサイト訪問者はまだサインインしておらず、匿名です。

## http://localhost:4503/content/sites/engage/en.html {#http-localhost-content-sites-engage-en-html}

![chlimage_1-311](assets/chlimage_1-311.png)

## 匿名のサイト訪問者 {#anonymous-site-visitor}

匿名のサイト訪問者の UI には、次の情報が表示されます。

* サイトのタイトル。 はじめにのチュートリアル
* プロファイルリンクなし
* メッセージリンクがありません
* 通知リンクがありません
* 検索フィールド
* ログインリンク
* ブランドバナー
* 参照サイトテンプレートに含まれるコンポーネントのメニューリンク

様々なリンクを選択すると、読み取り専用モードになります。

## JCR での匿名アクセスの防止 {#prevent-anonymous-access-on-jcr}

ただし、既知の制限により、コミュニティサイトコンテンツは jcr コンテンツと json を通じて匿名の訪問者に公開されます。 **匿名アクセスを許可** はサイトのコンテンツに対して無効です。 ただし、この動作は、Sling の制限を回避策として使用して制御できます。

jcr コンテンツと json を介した匿名ユーザーによるアクセスからコミュニティサイトのコンテンツを保護するには、次の手順に従います。

1. AEM オーサーインスタンスで、 https://に移動します。&lt;host>:&lt;port>/editor.html/content/site/&lt;sitename>.html

   >[!NOTE]
   >
   >ローカライズされたサイトに移動しないでください。

1. に移動します。 **[!UICONTROL ページプロパティ]**.

   ![site-authentication](assets/site-authentication.png)

1. 「**[!UICONTROL 詳細]**」タブに移動します。

   ![page-properties](assets/page-properties.png)

1. 有効にする **[!UICONTROL 認証要件]**.
1. ログインページのパスを追加します。 （例：`/content/......./GetStarted`）。
1. ページを公開します。

## 信頼されているコミュニティメンバー {#trusted-community-member}

この操作は、次を前提としています。 [Aaron McDonald](tutorials.md#demo-users) は次の役割を割り当てられました： [コミュニティマネージャーとモデレーター](create-site.md#roles). そうでない場合は、オーサー環境に戻ります。 [サイト設定の変更](sites-console.md#modifying-site-properties) コミュニティマネージャーとモデレーターの両方として Aaron McDonald を選択します。

右上隅で、「 `Log in`をクリックし、ユーザー名「aaron.mcdonald@mailinator.com」とパスワード「password」を使用して署名します。 twitterまたはFacebookの資格情報を使用してログインする機能に注目してください。

![chlimage_1-312](assets/chlimage_1-312.png)

サインインすると、今までになかった「`Administration`」というメニューアイテムが表示されます。これは、サインインしたメンバーにモデレーターの役割が付与されているからです。現在は、様々なリンクを選択する方が興味深いです。

![chlimage_1-313](assets/chlimage_1-313.png)

カレンダーページがホームページになっていますが、これは、選択した参照サイトテンプレートの最初に含まれているのがカレンダー機能で、その後にアクティビティストリーム機能、フォーラム機能などが続いているからです。この構造は、 [サイトテンプレート](sites.md#edit-site-template) コンソールまたはオーサー環境でサイトプロパティを変更する場合：

![chlimage_1-314](assets/chlimage_1-314.png)

>[!NOTE]
>
>コミュニティコンポーネントと機能について詳しくは、以下を参照してください。
>
>* [コミュニティコンポーネント](author-communities.md)（作成者向け）
>* [コンポーネントおよび機能の基本事項](essentials.md)（開発者向け）

>


## フォーラムリンク {#forum-link}

フォーラムリンクを選択すると、基本的なフォーラム機能が表示されます。

メンバーは、新しいトピックを投稿したり、トピックをフォローしたりできます。

サイト訪問者は、様々な方法で投稿を表示したり、並べ替えたりできます。

![chlimage_1-315](assets/chlimage_1-315.png)

## グループリンク {#groups-link}

Aaron はグループ管理者なので、グループリンクを選択すると、新しいグループを作成するための画面が表示されます。ここで、グループテンプレートや画像を選択したり、グループをオープンにするかシークレットにするかを設定したり、メンバーを招待したりできます。

パブリッシュ環境でグループを作成する例を次に示します。

グループは、オーサー環境で作成し、オーサー環境のコミュニティサイト（[コミュニティグループコンソール](groups.md)）内で管理することもできます。の経験 [オーサー環境でのグループの作成](nested-groups.md) は、このチュートリアルの次の段階です。

![chlimage_1-316](assets/chlimage_1-316.png)

参照グループの作成：

1. 選択 **[!UICONTROL 新しいグループ]**
1. **[!UICONTROL 「設定」タブ]**
   * Group Name: `Sports`
   * 説明: `A parent group for various sporting groups`
   * グループ URL 名: `sports`
   * 選択 `Open Group` （コミュニティメンバーが参加することを許可）
1. **[!UICONTROL 「テンプレート」タブ]**
   * 選択 `Reference Group` （構造内にグループ機能を含み、ネストされたグループを許可します）
1. 選択 **[!UICONTROL グループを作成]**

![chlimage_1-317](assets/chlimage_1-317.png)

新しいグループが作成されたら、その中に（ネストされる）2 つのグループを作成するために&#x200B;**新しい Sports グループを選択**&#x200B;します。サイト構造は、グループ機能で始めることができないので、Sports グループを開いた後、「グループ」リンクを選択する必要があります。

![chlimage_1-318](assets/chlimage_1-318.png)

2 番目のリンクセット ( `Blog`( 現在選択されているグループに属し、 `Sports`グループ化します。 「スポーツ」 `Groups` リンクを使用すると、Sports グループ内に 2 つのグループをネストできます。

例えば、 n を 2 つ追加します。 `ew groups.`

* 次の名前の 1 つ： `Baseball`
   * 設定を `Open Group` （必須メンバーシップ）
   * 「テンプレート」タブで、「 `Conversational Group`
* 次の名前の 1 つ： `Gymnastics`
   * 設定をに変更します。 `Member Only Group` （メンバーシップの制限）
   * 「テンプレート」タブで、「 `Conversational Group`

**注意**：

* 両方のグループが表示される前に、ページの更新が必要になる場合があります
* このテンプレートにはグループ機能が含まれていないので、これ以上グループをネストすることはできません
* 作成者の場合、 [グループコンソール](groups.md) は 3 つ目の選択肢を提供します。 `Public Group` （オプションのメンバーシップ）

両方のグループを作成したら、Baseball グループ（開いているグループ）を選択し、リンクに注目します。 `Discussions` `What's New` `Members`
グループのリンクはメインサイトのリンクの下に表示され、結果として次のように表示されます。

![chlimage_1-319](assets/chlimage_1-319.png)

オーサー環境で、管理者権限を持つユーザーが [コミュニティグループコンソール](members.md) をクリックし、Weston McCall を `Community Engage Gymnastics <uid> Members` グループ化します。

引き続きパブリッシュ環境で、Aaron McDonald としてログアウトし、次のように匿名のサイト訪問者として Sports グループ内のグループを表示します。

* ホームページから
* 選択 `Groups`リンク
* 選択 `Sports`リンク
* スポーツを選択&#39; `Groups`リンク

Baseball グループのみが表示されます。

Weston McCall（weston.mccall@dodgit.com／password）としてログインし、同じ場所に移動します。Weston が `Join` 開場 `Baseball` グループ化し、次のいずれかを選択します。 `enter or Leave` 私人 `Gymnastics`グループ化します。

![chlimage_1-320](assets/chlimage_1-320.png)

## Web ページリンク {#web-page-link}

Web ページリンクを選択すると、サイトに含まれる基本的な Web ページが表示されます。標準のAEMオーサリングツールを使用して、オーサー環境でこのページにコンテンツを追加できます。

例えば、次に移動します。 **作成者** インスタンス、 `engage` フォルダーを [コミュニティサイトコンソール](sites-console.md)を選択し、 **サイトを開く** アイコンをクリックしてオーサリング編集モードに入ります。 次に、プレビューモードを選択して、 `Web Page`リンクをクリックし、「編集モード」を選択して、タイトルコンポーネントとテキストコンポーネントを追加します。 最後に、ページのみ、またはサイト全体を再公開します。

![chlimage_1-321](assets/chlimage_1-321.png)

## 管理リンク {#administration-link}

コミュニティメンバーがモデレート権限を持っている場合は、「管理」リンクが表示され、このリンクを選択すると、投稿されたコミュニティコンテンツが表示され、投稿されたコミュニティコンテンツを使用できるようになります [モデレート済み](moderate-ugc.md) ～に似た方法で [モデレートコンソール](moderation.md) （オーサー環境で）

ブラウザーの戻るボタンを使用して、公開したサイトに戻ります。ほとんどのコンソールは、パブリッシュ環境のグローバルナビゲーションからはアクセスできません。

![chlimage_1-322](assets/chlimage_1-322.png)

## 自己登録 {#self-registration}

ログアウトした後に、新しいユーザー登録を作成できます。

*  `Log In`
*  `Sign up for a new account`

![chlimage_1-323](assets/chlimage_1-323.png) ![chlimage_1-324](assets/chlimage_1-324.png)

デフォルトでは、電子メールアドレスがログイン ID になります。オフにすると、訪問者は独自のログイン ID（ユーザー名）を入力できます。 ユーザー名は、パブリッシュ環境で一意である必要があります。

ユーザーの名前、電子メールおよびパスワードを指定した後、「 」を選択します。 `Sign Up`ユーザーを作成し、署名を有効にします。

サインインすると、最初に表示されるページが `Profile`ページに貼り付けることができます。

![chlimage_1-325](assets/chlimage_1-325.png)

メンバーが自分のログイン ID を忘れた場合は、電子メールアドレスを使用して回復することができます。

![chlimage_1-326](assets/chlimage_1-326.png)
