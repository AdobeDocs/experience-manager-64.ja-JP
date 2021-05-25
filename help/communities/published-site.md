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
exl-id: 8f716a59-1116-4855-baeb-3997de71b55f
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '1144'
ht-degree: 40%

---

# 公開したサイトを使ってみる {#experience-the-published-site}

## パブリッシュサーバー上の新しいサイトの参照 {#browse-to-new-site-on-publish}

新しく作成したコミュニティサイトが公開されたので、次はこのサイト作成時に表示された URL を参照します。ただし、このとき参照するのはパブリッシュサーバー上の URL です。次に例を示します。

* 作成者URL = http://localhost:4502/content/sites/engage/en.html
* パブリッシュURL = http://localhost:4503/content/sites/engage/en.html

どのメンバーがオーサーインスタンスにサインインし、どのメンバーがパブリッシュインスタンスにサインインしているかを混乱なく把握するために、インスタンスごとに異なるブラウザーを使用することを推奨します。

公開済みサイトに初めてアクセスするときは、通常、そのサイト訪問者はまだサインインしておらず、匿名です。

## http://localhost:4503/content/sites/engage/en.html  {#http-localhost-content-sites-engage-en-html}

![chlimage_1-311](assets/chlimage_1-311.png)

## 匿名のサイト訪問者 {#anonymous-site-visitor}

匿名のサイト訪問者のUIには、次の情報が表示されます。

* サイトのタイトル。 入門チュートリアル
* プロファイルリンクなし
* メッセージのリンクなし
* 通知リンクなし
* 検索フィールド
* ログインリンク
* ブランドバナー
* リファレンスサイトテンプレートに含まれるコンポーネントのメニューリンク

様々なリンクを選択すると、読み取り専用モードになります。

## JCR {#prevent-anonymous-access-on-jcr}での匿名アクセスを防ぐ

既知の制限により、jcrコンテンツとjsonを通じてコミュニティサイトのコンテンツを匿名訪問者に公開しますが、サイトのコンテンツに対して&#x200B;**匿名アクセスを許可**&#x200B;は無効になっています。 ただし、この動作は、Slingの制限を回避策として使用して制御できます。

コミュニティサイトのコンテンツを、匿名ユーザーがjcrコンテンツやjsonを介してアクセスするのを防ぐには、次の手順に従います。

1. AEMオーサーインスタンスで、 https://&lt;host>:&lt;port>/editor.html/content/site/&lt;sitename>.htmlに移動します。

   >[!NOTE]
   >
   >ローカライズされたサイトに移動しないでください。

1. **[!UICONTROL ページのプロパティ]**&#x200B;に移動します。

   ![site-authentication](assets/site-authentication.png)

1. 「**[!UICONTROL 詳細]**」タブに移動します。

   ![page-properties](assets/page-properties.png)

1. **[!UICONTROL 認証要件]**&#x200B;を有効にします。
1. ログインページのパスを追加します。 （例：`/content/......./GetStarted`）。
1. ページを公開します。

## 信頼されているコミュニティメンバー {#trusted-community-member}

この経験は、[Aaron McDonald](tutorials.md#demo-users)に[コミュニティマネージャーおよびモデレーター](create-site.md#roles)の役割が割り当てられたことを前提としています。 そうでない場合は、オーサー環境に戻って[サイト設定を変更](sites-console.md#modifying-site-properties)し、コミュニティマネージャーとモデレーターの両方としてAaron McDonaldを選択します。

右上隅で、「`Log in`」を選択し、ユーザー名「aaron.mcdonald@mailinator.com」とパスワード「password」で署名します。 twitterまたはFacebookの資格情報を使用してログインする機能に注意してください。

![chlimage_1-312](assets/chlimage_1-312.png)

サインインすると、今までになかった「`Administration`」というメニューアイテムが表示されます。これは、サインインしたメンバーにモデレーターの役割が付与されているからです。現在は、様々なリンクを選択する方が興味深いです。

![chlimage_1-313](assets/chlimage_1-313.png)

カレンダーページがホームページになっていますが、これは、選択した参照サイトテンプレートの最初に含まれているのがカレンダー機能で、その後にアクティビティストリーム機能、フォーラム機能などが続いているからです。この構造は、[サイトテンプレート](sites.md#edit-site-template)コンソールから、またはオーサー環境でサイトのプロパティを変更する際に表示されます。

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

グループは、オーサー環境で作成し、オーサー環境のコミュニティサイト（[コミュニティグループコンソール](groups.md)）内で管理することもできます。オーサー](nested-groups.md)上での[グループの作成は、このチュートリアルで次に行います。

![chlimage_1-316](assets/chlimage_1-316.png)

参照グループの作成：

1. **[!UICONTROL 新しいグループ]**&#x200B;を選択します。
1. **[!UICONTROL 「設定」タブ]**
   * Group Name: `Sports`
   * 説明: `A parent group for various sporting groups`
   * グループ URL 名: `sports`
   * `Open Group`を選択します（コミュニティメンバーの参加を許可）。
1. **[!UICONTROL 「テンプレート」タブ]**
   * `Reference Group`を選択します（ネストされたグループを許可するために、構造にグループ機能を含めます）
1. 「**[!UICONTROL グループを作成]**」を選択します。

![chlimage_1-317](assets/chlimage_1-317.png)

新しいグループが作成されたら、その中に（ネストされる）2 つのグループを作成するために&#x200B;**新しい Sports グループを選択**&#x200B;します。サイト構造はグループ機能で始まることができないので、Sportsグループを開いた後、「グループ」リンクを選択する必要があります。

![chlimage_1-318](assets/chlimage_1-318.png)

`Blog`から始まる2番目のリンクセットは、現在選択されているグループ`Sports`グループに属しています。 「Sports」の`Groups`リンクを選択すると、Sportsグループ内に2つのグループをネストできます。

例えば、`ew groups.`に2つ追加します。

* `Baseball`という名前の1つ
   * `Open Group`（必須のメンバーシップ）のままにします。
   * 「テンプレート」タブで、「`Conversational Group`」を選択します。
* `Gymnastics`という名前の1つ
   * 設定を`Member Only Group`（制限付きメンバーシップ）に変更します。
   * 「テンプレート」タブで、「`Conversational Group`」を選択します。

**注意**：

* 両方のグループを表示する前に、ページの更新が必要な場合があります
* このテンプレートにはグループ機能が含まれていないので、グループのこれ以上のネストはできません
* オーサー環境では、[グループコンソール](groups.md)に3つ目の選択肢(`Public Group`（オプションのメンバーシップ）が用意されています。

両方のグループが作成されたら、 Baseballグループと開いているグループを選択し、リンクに注目します。`Discussions` `What's New` `Members`
グループのリンクはメインサイトのリンクの下に表示され、結果は次のように表示されます。

![chlimage_1-319](assets/chlimage_1-319.png)

オーサー環境で、管理権限を持つ[コミュニティグループコンソール](members.md)に移動し、`Community Engage Gymnastics <uid> Members`グループにWeston McCallを追加します。

引き続きパブリッシュ環境で、Aaron McDonald としてログアウトし、次のように匿名のサイト訪問者として Sports グループ内のグループを表示します。

* ホームページから
* `Groups`リンクを選択
* `Sports`リンクを選択
* 「スポーツ」`Groups`リンクを選択します。

Baseball グループのみが表示されます。

Weston McCall（weston.mccall@dodgit.com／password）としてログインし、同じ場所に移動します。Westonは、開いている`Baseball`グループと`enter or Leave`プライベートの`Gymnastics`グループの`Join`を実行できます。

![chlimage_1-320](assets/chlimage_1-320.png)

## Web ページリンク {#web-page-link}

Web ページリンクを選択すると、サイトに含まれる基本的な Web ページが表示されます。標準のAEMオーサリングツールを使用して、オーサー環境でこのページにコンテンツを追加できます。

例えば、**author**&#x200B;インスタンスに移動し、[コミュニティサイトコンソール](sites-console.md)で`engage`フォルダーを開き、**サイトを開く**&#x200B;アイコンを選択してオーサー編集モードに入ります。 次に、プレビューモードを選択して`Web Page`リンクを選択し、編集モードを選択してタイトルとテキストコンポーネントを追加します。 最後に、ページのみまたはサイト全体を再公開します。

![chlimage_1-321](assets/chlimage_1-321.png)

## 管理リンク {#administration-link}

コミュニティメンバーがモデレート権限を持っている場合は、「管理」リンクが表示され、投稿されたコミュニティコンテンツが表示され、オーサー環境の[モデレートコンソール](moderation.md)と同様の方法で[モデレート](moderate-ugc.md)できます。

ブラウザーの戻るボタンを使用して、公開したサイトに戻ります。ほとんどのコンソールは、パブリッシュ環境のグローバルナビゲーションからはアクセスできません。

![chlimage_1-322](assets/chlimage_1-322.png)

## 自己登録 {#self-registration}

ログアウトした後に、新しいユーザー登録を作成できます。

*  `Log In`
*  `Sign up for a new account`

![chlimage_1-323](assets/chlimage_1-323.png) ![chlimage_1-324](assets/chlimage_1-324.png)

デフォルトでは、電子メールアドレスがログイン ID になります。オフにすると、訪問者は独自のログインID（ユーザー名）を入力できます。 ユーザー名は、パブリッシュ環境で一意である必要があります。

ユーザーの名前、電子メール、パスワードを指定した後、`Sign Up`を選択すると、ユーザーが作成され、署名できるようになります。

サインインすると、最初に表示されるページは`Profile`ページで、ページをパーソナライズできます。

![chlimage_1-325](assets/chlimage_1-325.png)

メンバーが自分のログイン ID を忘れた場合は、電子メールアドレスを使用して回復することができます。

![chlimage_1-326](assets/chlimage_1-326.png)
