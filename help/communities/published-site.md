---
title: 公開したサイトを使ってみる
seo-title: 公開したサイトを使ってみる
description: 公開したサイトの参照
seo-description: 公開したサイトの参照
uuid: f510224c-d991-4528-864d-44672138740c
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.4/COMMUNITIES
topic-tags: introduction
content-type: reference
discoiquuid: 4dc54701-68b9-49dd-a212-b0b53330c1c0
translation-type: tm+mt
source-git-commit: 63001012f0d865c2548703ea387c780679128ee7
workflow-type: tm+mt
source-wordcount: '1144'
ht-degree: 40%

---


# 公開したサイトを使ってみる {#experience-the-published-site}

## パブリッシュサーバー上の新しいサイトの参照 {#browse-to-new-site-on-publish}

新しく作成したコミュニティサイトが公開されたので、次はこのサイト作成時に表示された URL を参照します。ただし、このとき参照するのはパブリッシュサーバー上の URL です。次に例を示します。

* 作成者URL = http://localhost:4502/content/sites/engage/en.html
* 発行URL = http://localhost:4503/content/sites/engage/en.html

どのメンバーがオーサーインスタンスにサインインし、どのメンバーがパブリッシュインスタンスにサインインしているかを混乱なく把握するために、インスタンスごとに異なるブラウザーを使用することを推奨します。

公開済みサイトに初めてアクセスするときは、通常、そのサイト訪問者はまだサインインしておらず、匿名です。

## http://localhost:4503/content/sites/engage/en.html {#http-localhost-content-sites-engage-en-html}

![chlimage_1-311](assets/chlimage_1-311.png)

## 匿名のサイト訪問者 {#anonymous-site-visitor}

匿名サイト訪問者のUIには、次の項目が表示されます。

* サイトのタイトル。 はじめにのチュートリアル
* プロファイルリンクなし
* メッセージのリンクなし
* 通知リンクなし
* サーチ場
* ログインリンク
* ブランドバナー
* リファレンスサイトテンプレートに含まれるコンポーネントのメニューリンク

様々なリンクを選択すると、それらは読み取り専用モードになっています。

## JCRでの匿名アクセスの禁止 {#prevent-anonymous-access-on-jcr}

既知の制限により、jcrコンテンツとjsonを介してコミュニティサイトのコンテンツが匿名訪問者に公開されますが、匿名アクセス **を許可** (allow anonymous access)はサイトのコンテンツに対して無効になります。 ただし、この動作は、回避策として「Sling制限」を使用して制御できます。

jcrコンテンツとjsonを介した匿名ユーザーによるアクセスからコミュニティサイトのコンテンツを保護するには、次の手順に従います。

1. AEM作成者インスタンスで、https://&lt;ホスト>:&lt;ポート>/editor.html/content/site/&lt;サイト名>.htmlに移動します。

   >[!NOTE]
   >
   >ローカライズされたサイトに移動しないでください。

1. 「 **[!UICONTROL ページプロパティ]**」に移動。

   ![サイト認証](assets/site-authentication.png)

1. 「**[!UICONTROL 詳細]**」タブに移動します。

   ![page-properties](assets/page-properties.png)

1. Enable **[!UICONTROL Authentication Requirement]**.
1. ログ追加インページのパス。 例： `/content/......./GetStarted`
1. ページを公開します。

## 信頼されているコミュニティメンバー {#trusted-community-member}

This experience assumes [Aaron McDonald](tutorials.md#demo-users) was assigned the roles of [community manager and moderator](create-site.md#roles). If not, return to the author environment to [modify the site settings](sites-console.md#modifying-site-properties) and select Aaron McDonald as both community manager and moderator.

In the upper right corner, select `Log in`, and sign with username &quot;aaron.mcdonald@mailinator.com&quot; and password &quot;password&quot;. TwitterまたはFacebookの資格情報を使用してサインインする機能に注目してください。

![chlimage_1-312](assets/chlimage_1-312.png)

サインインすると、今までになかった「`Administration`」というメニューアイテムが表示されます。これは、サインインしたメンバーにモデレーターの役割が付与されているからです。さらに、様々なリンクを選択する方が興味深い結果が得られます。

![chlimage_1-313](assets/chlimage_1-313.png)

カレンダーページがホームページになっていますが、これは、選択した参照サイトテンプレートの最初に含まれているのがカレンダー機能で、その後にアクティビティストリーム機能、フォーラム機能などが続いているからです。This structure is visible from the [Site Template](sites.md#edit-site-template) console or when modifying site properties in the author environment:

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

グループは、オーサー環境で作成し、オーサー環境のコミュニティサイト（[コミュニティグループコンソール](groups.md)）内で管理することもできます。The experience of [creating groups on author](nested-groups.md) is next in this tutorial.

![chlimage_1-316](assets/chlimage_1-316.png)

参照グループの作成：

1. Select **[!UICONTROL New Group]**
1. **[!UICONTROL 「設定」タブ]**
   * Group Name: `Sports`
   * 説明: `A parent group for various sporting groups`
   * グループ URL 名: `sports`
   * select `Open Group` (allow any community member to participate by joining)
1. **[!UICONTROL 「テンプレート」タブ]**
   * Select `Reference Group` (contains a groups function in its structure to allow nested groups)
1. Select **[!UICONTROL Create Group]**

![chlimage_1-317](assets/chlimage_1-317.png)

新しいグループが作成されたら、その中に（ネストされる）2 つのグループを作成するために&#x200B;**新しい Sports グループを選択**&#x200B;します。サイト構造はグループ機能では始まらないので、スポーツグループを開いた後、「グループ」リンクを選択する必要があります。

![chlimage_1-318](assets/chlimage_1-318.png)

The second set of links, beginning with `Blog`, belong to the currently selected group, the `Sports`group. By selecting the Sports&#39; `Groups` link, it is possible to nest two groups within the Sports group.

As an example, add two n `ew groups.`

* One named `Baseball`
   * Leave it set as an `Open Group` (required membership)
   * 「テンプレート」タブで、 `Conversational Group`
* One named `Gymnastics`
   * 設定を `Member Only Group` （制限付きメンバーシップ）に変更します
   * 「テンプレート」タブで、 `Conversational Group`

**注意**：

* 両方のグループが表示される前に、ページの更新が必要になる場合があります
* このテンプレートにはグループ機能が含まれていない**ので、グループをこれ以上ネストすることはできません。
* On author, the [Groups console](groups.md) provides a third choice - a `Public Group` (optional membership)

両方のグループが作成されたら、野球グループと開いているグループを選択し、そのリンクを確認します。 `Discussions` `What's New` `Members`
グループのリンクはメインサイトのリンクの下に表示され、結果は次のように表示されます。

![chlimage_1-319](assets/chlimage_1-319.png)

On author - with administrative privileges, navigate to the [Communities Groups console](members.md) and add Weston McCall to the `Community Engage Gymnastics <uid> Members` group.

引き続きパブリッシュ環境で、Aaron McDonald としてログアウトし、次のように匿名のサイト訪問者として Sports グループ内のグループを表示します。

* ホームページから
* Select `Groups`link
* Select `Sports`link
* Select the Sports&#39; `Groups`link

Baseball グループのみが表示されます。

Weston McCall（weston.mccall@dodgit.com／password）としてログインし、同じ場所に移動します。Westonは、オープン・ `Join` グループとプライベート・ `Baseball` グループのどちらか `enter or Leave``Gymnastics`を実行できることに注意してください。

![chlimage_1-320](assets/chlimage_1-320.png)

## Web ページリンク {#web-page-link}

Web ページリンクを選択すると、サイトに含まれる基本的な Web ページが表示されます。標準のAEMオーサリングツールを使用して、作成者環境のこのページにコンテンツを追加できます。

For example, go to **author** instance, open the `engage` folder in the [Communities Sites console](sites-console.md), select the **Open Site** icon to enter author edit mode. Then select preview mode to select the `Web Page`link, then select edit mode to add Title and Text components. 最後に、ページのみまたはサイト全体を再公開します。

![chlimage_1-321](assets/chlimage_1-321.png)

## 管理リンク {#administration-link}

When the community member has moderation privileges, then the Administration link will be visible and selecting it will display the community content posted and allow it to be [moderated](moderate-ugc.md) in a manner similar to the [moderation console](moderation.md) in the author environment.

ブラウザーの戻るボタンを使用して、公開したサイトに戻ります。ほとんどのコンソールは、公開環境のグローバルナビゲーションからはアクセスできません。

![chlimage_1-322](assets/chlimage_1-322.png)

## 自己登録 {#self-registration}

ログアウトした後に、新しいユーザー登録を作成できます。

*  `Log In`
*  `Sign up for a new account`

![chlimage_1-323](assets/chlimage_1-323.png) ![chlimage_1-324](assets/chlimage_1-324.png)

デフォルトでは、電子メールアドレスがログイン ID になります。選択しない場合、訪問者は独自のログインID（ユーザー名）を入力できます。 ユーザー名は、発行環境で一意である必要があります。

After specifying the user&#39;s name, email, and password, selecting `Sign Up`will create the user and enable them to sign.

Once signed in, the first page presented is their `Profile`page, which they can personalize.

![chlimage_1-325](assets/chlimage_1-325.png)

メンバーが自分のログイン ID を忘れた場合は、電子メールアドレスを使用して回復することができます。

![chlimage_1-326](assets/chlimage_1-326.png)
