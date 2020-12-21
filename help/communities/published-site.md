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

## http://localhost:4503/content/sites/engage/en.html  {#http-localhost-content-sites-engage-en-html}

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

## JCR {#prevent-anonymous-access-on-jcr}での匿名アクセスの禁止

既知の制限により、jcrコンテンツとjsonを介してコミュニティサイトのコンテンツが匿名訪問者に公開されますが、**allow anonymous access**&#x200B;はサイトのコンテンツに対して無効になっています。 ただし、この動作は、回避策として「Sling制限」を使用して制御できます。

jcrコンテンツとjsonを介した匿名ユーザーによるアクセスからコミュニティサイトのコンテンツを保護するには、次の手順に従います。

1. AEM作成者インスタンスで、https://&lt;ホスト>:&lt;ポート>/editor.html/content/site/&lt;サイト名>.htmlに移動します。

   >[!NOTE]
   >
   >ローカライズされたサイトには移動しないでください。

1. **[!UICONTROL ページプロパティ]**&#x200B;に移動します。

   ![サイト認証](assets/site-authentication.png)

1. 「**[!UICONTROL 詳細]**」タブに移動します。

   ![page-properties](assets/page-properties.png)

1. **[!UICONTROL 認証要件]**&#x200B;を有効にします。
1. ログ追加インページのパス。 例： `/content/......./GetStarted`
1. ページを公開します。

## 信頼されているコミュニティメンバー {#trusted-community-member}

この経験では、[Aaron McDonald](tutorials.md#demo-users)が[コミュニティマネージャーおよびモデレーター](create-site.md#roles)の役割を割り当てられたと想定しています。 そうでない場合は、作成者環境に戻って[サイト設定](sites-console.md#modifying-site-properties)を変更し、コミュニティマネージャーとモデレーターの両方としてAaron McDonaldを選択します。

右上隅の「`Log in`」を選択し、ユーザー名「aaron.mcdonald@mailinator.com」とパスワード「password」で署名します。 TwitterまたはFacebookの資格情報を使用してサインインする機能に注目してください。

![chlimage_1-312](assets/chlimage_1-312.png)

サインインすると、今までになかった「`Administration`」というメニューアイテムが表示されます。これは、サインインしたメンバーにモデレーターの役割が付与されているからです。さらに、様々なリンクを選択する方が興味深い結果が得られます。

![chlimage_1-313](assets/chlimage_1-313.png)

カレンダーページがホームページになっていますが、これは、選択した参照サイトテンプレートの最初に含まれているのがカレンダー機能で、その後にアクティビティストリーム機能、フォーラム機能などが続いているからです。この構造体は、[サイトテンプレート](sites.md#edit-site-template)コンソールから、または作成者環境でサイトのプロパティを変更する場合に表示されます。

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

グループは、オーサー環境で作成し、オーサー環境のコミュニティサイト（[コミュニティグループコンソール](groups.md)）内で管理することもできます。[作成者](nested-groups.md)でのグループ作成の経験は、このチュートリアルで次に説明します。

![chlimage_1-316](assets/chlimage_1-316.png)

参照グループの作成：

1. 「**[!UICONTROL 新しいグループ]**」を選択します
1. **[!UICONTROL 「設定」タブ]**
   * Group Name: `Sports`
   * 説明: `A parent group for various sporting groups`
   * グループ URL 名: `sports`
   * `Open Group`を選択（コミュニティのメンバーが参加できるようにする）
1. **[!UICONTROL 「テンプレート」タブ]**
   * `Reference Group`を選択します（ネストされたグループを許可するため、構造にグループ関数を含む）
1. 「**[!UICONTROL グループを作成]**」を選択します

![chlimage_1-317](assets/chlimage_1-317.png)

新しいグループが作成されたら、その中に（ネストされる）2 つのグループを作成するために&#x200B;**新しい Sports グループを選択**&#x200B;します。サイト構造はグループ機能では始まらないので、スポーツグループを開いた後、「グループ」リンクを選択する必要があります。

![chlimage_1-318](assets/chlimage_1-318.png)

`Blog`で始まる2番目のリンクセットは、現在選択されているグループ`Sports`グループに属しています。 「スポーツ」`Groups`リンクを選択すると、スポーツグループ内に2つのグループをネストできます。

例として、`ew groups.`に

* `Baseball`という名前の1つ
   * `Open Group`（必須メンバーシップ）に設定したままにします
   * 「テンプレート」タブで、`Conversational Group`を選択します。
* `Gymnastics`という名前の1つ
   * 設定を`Member Only Group`に変更（制限付きメンバーシップ）
   * 「テンプレート」タブで、`Conversational Group`を選択します。

**注意**：

* 両方のグループが表示される前に、ページの更新が必要になる場合があります
* このテンプレートにはグループ機能が含まれていない**ので、グループをこれ以上ネストすることはできません。
* 作成者の場合、[グループコンソール](groups.md)は3つ目の選択肢として`Public Group` （オプションのメンバーシップ）を提供します

両方のグループが作成されたら、野球グループと開いているグループを選択し、そのリンクを確認します。`Discussions` `What's New` `Members`
グループのリンクはメインサイトのリンクの下に表示され、結果は次のように表示されます。

![chlimage_1-319](assets/chlimage_1-319.png)

作成者 — 管理者権限で、[Communities Groupsコンソール](members.md)に移動し、`Community Engage Gymnastics <uid> Members`グループにWeston McCallを追加します。

引き続きパブリッシュ環境で、Aaron McDonald としてログアウトし、次のように匿名のサイト訪問者として Sports グループ内のグループを表示します。

* ホームページから
* `Groups`リンクを選択
* `Sports`リンクを選択
* 「スポーツ」`Groups`リンクを選択

Baseball グループのみが表示されます。

Weston McCall（weston.mccall@dodgit.com／password）としてログインし、同じ場所に移動します。Westonは、開いている`Baseball`グループと`enter or Leave`プライベート`Gymnastics`グループのどちらかを`Join`できることに注意してください。

![chlimage_1-320](assets/chlimage_1-320.png)

## Web ページリンク {#web-page-link}

Web ページリンクを選択すると、サイトに含まれる基本的な Web ページが表示されます。標準のAEMオーサリングツールを使用して、作成者環境のこのページにコンテンツを追加できます。

例えば、**author**&#x200B;インスタンスに移動し、[Communitiesのサイトコンソール](sites-console.md)で`engage`フォルダーを開き、**サイトを開く**&#x200B;アイコンを選択して、作成者編集モードにします。 次に、プレビューモードを選択して`Web Page`リンクを選択し、編集モードを選択してタイトルとテキストのコンポーネントを追加します。 最後に、ページのみまたはサイト全体を再公開します。

![chlimage_1-321](assets/chlimage_1-321.png)

## 管理リンク {#administration-link}

コミュニティメンバーがモデレート権限を持つ場合は、管理リンクが表示され、リンクを選択すると、投稿されたコミュニティコンテンツが表示され、作成者環境の[モデレートコンソール](moderation.md)と同様の方法で[モデレート](moderate-ugc.md)できます。

ブラウザーの戻るボタンを使用して、公開したサイトに戻ります。ほとんどのコンソールは、公開環境のグローバルナビゲーションからはアクセスできません。

![chlimage_1-322](assets/chlimage_1-322.png)

## 自己登録 {#self-registration}

ログアウトした後に、新しいユーザー登録を作成できます。

*  `Log In`
*  `Sign up for a new account`

![chlimage_1-323](assets/chlimage_1-323.png) ![chlimage_1-324](assets/chlimage_1-324.png)

デフォルトでは、電子メールアドレスがログイン ID になります。選択しない場合、訪問者は独自のログインID（ユーザー名）を入力できます。 ユーザー名は、発行環境で一意である必要があります。

ユーザーの名前、電子メール、パスワードを指定した後、`Sign Up`を選択すると、ユーザーが作成され、ユーザーの署名が有効になります。

サインインすると、最初に表示されるページは`Profile`ページで、これをパーソナライズできます。

![chlimage_1-325](assets/chlimage_1-325.png)

メンバーが自分のログイン ID を忘れた場合は、電子メールアドレスを使用して回復することができます。

![chlimage_1-326](assets/chlimage_1-326.png)
