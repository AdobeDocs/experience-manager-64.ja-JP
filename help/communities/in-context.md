---
title: コンテキスト内モデレート
seo-title: In-Context Moderation
description: モデレーターの操作を実行する方法
seo-description: How to perform moderator actions
uuid: 282a8bea-2822-4e5c-b9f4-4d9a5380d895
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.4/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: ee104f6f-123b-4a6e-9031-849fc1318cc5
role: Admin
exl-id: a7678273-81f6-4089-ac73-2458d940e374
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '825'
ht-degree: 3%

---

# コンテキスト内モデレート {#in-context-moderation}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

AEM Communitiesの場合、管理者や信頼できるコミュニティメンバーは、コミュニティコンテンツが投稿された公開済みページで直接モデレートを実行できます。

を使用する場合 [モデレートコンソール](moderation.md)コンテンツに対して表示される情報には、コンテキスト内でモデレートする際に使用できる追加のモデレートアクションにアクセスできるように、公開済みページへのリンクが含まれます。

## モデレートアクション {#moderation-actions}

モデレートの概要で [モデレートアクション](moderate-ugc.md#moderation-actions).

## モデレート UI {#moderation-ui}

パブリッシュインスタンスのモデレーターに表示される UI は、ユーザー生成コンテンツ (UGC) の投稿と管理を行うためのダイアログ内に含まれています。 UI の要素は、サイト訪問者のステータス ( 訪問者が

1. コンテンツを投稿したメンバー
1. 信頼できるメンバーモデレーター
1. 管理者
1. サインインしていますが、管理者、モデレーター、コンテンツの作成者ではありません
1. サインインしていません

## 例 {#example}

の使用 [Geometrixxエンゲージ](http://localhost:4503/content/sites/engage/en.html) 次の場合に作成されたサイト [AEM Communitiesの概要](getting-started.md)を使用すると、次に示すように、パブリッシュ環境で様々なモデレートアクティビティを体験できるフォーラムに、スレッドをすばやく設定できます。

Aaron McDonald(aaron.mcdonald@mailinator.com) は、サイトの作成時に community-engage-moderators グループに追加することで、信頼できるコミュニティメンバーとして識別されました。

Rebekah Larsen(rebekah.larsen@trashymail.com) は、 [メンバーコンソール](members.md).

コミュニティユーザーグループの詳細については、 [ユーザーとユーザーグループの管理](users.md).

### フォーラム投稿の作成 {#create-the-forum-posts}

* Rebekah Larsen(rebekah.larsen@trashymail.com) としてログインします。

   * フォーラムを選択
   * 新しい投稿を選択
   * 件名を入力

      ハミングバードフィーダーでネクターを変更するタイミング

   * 本文を入力

      毎年ハチドリの餌を吊り上げる時はあまり成功していませんでした 1 日か 2 日来るみたいですね。 1 週間に 1 回変えるのはそんなに長いの？ 早く変更する必要がありますか？
   * 投稿を選択
   * ログアウトを選択

* Aaron McDonald(aaron.mcdonald@mailinator.com) としてログインします。

   * フォーラムを選択
   * Hummingbird のトピックで、「詳細を表示」を選択します。
   * 返信を投稿のコメントを入力

      私は週に 1 回私のを変更し、5 月から 10 月までそれらを得る。

   * 返信を選択
   * ログアウトを選択

* Andrew Schaeffer(andrew.schaeffer@trashymail.com) としてログインします。

   * フォーラムを選択
   * Hummingbird のトピックで、「詳細を表示」を選択します。
   * 返信を投稿のコメントを入力

      私は蜜と飼料を販売しています — https://my.viral.url/にアクセスしてください

   * 返信を選択
   * ログアウトを選択

### 匿名のサイト訪問者 (#5) {#anonymous-site-visitor}

以下は、サインインしていないサイト訪問者が閲覧したフォーラムのビューです (5)。

匿名のサイト訪問者はフォーラムのみを表示できますが、コンテンツを投稿したり、モデレート操作を実行したりすることはできません。

![chlimage_1](assets/chlimage_1.png)

### 新規メンバー (#4) {#new-member}

オーサー環境で、管理者としてログインし、Boyd Larsen(boyd.larsen@dodgit.com) を community-engage-members グループの新しいメンバーとして追加します。その際、 [メンバーコンソール](members.md)、次にログアウトします。

公開時に、Boyd Larsen としてログインし、を選択してスレッドにアクセスします。 `Forum`、 `Read more` 蜂雀の巣箱のために

注意

* Boyd はフォーラムに参加していません
* Boyd は何も削除できません
* Boyd はサインインし、返信またはフラグコンテンツを実行できます

Boyd が「フラグ」を選択し、Andrew が投稿したコンテンツにフラグを設定します。

ログアウト

![chlimage_1-1](assets/chlimage_1-1.png)

### 管理者 (#3) {#administrator}

管理者 (admin) としてログインし、「フォーラム」を選択してスレッドにアクセスし、投稿の「詳細を表示」を選択します。

注意

* 管理者は、フラグ設定、削除、編集、拒否、切り取り、閉じる、ピン、機能を実行できます
* 管理者は「管理」を選択してモデレートコンソールにアクセスできます

![communityadmin-forum](assets/communityadmin-forum.png)

管理メニュー項目を選択して、 [モデレートコンソール](moderation.md) パブリッシュ環境から。

管理者の場合、GeometrixxEngage コミュニティサイトからのコンテンツだけでなく、モデレート可能なコンテンツもすべて表示されます。

検索フィルターは、開く/閉じるを切り替えるサイドパネルです。

ログアウト.

![moderationconsole-publish](assets/moderationconsole-publish.png)

### コミュニティモデレーター (#2) {#community-moderator}

コミュニティモデレーターの Aaron McDonald(aaron.mcdonal@mailinator.com) としてログインし、「フォーラム」を選択してスレッドにアクセスし、Hummingbird の投稿の「詳細を表示」を選択します。

注意

* Aaron は、自分の投稿の返信、削除、編集または拒否を実行できます
* Aaron では、他のコンテンツにフラグを設定/許可、返信、削除、編集、拒否することもできます
* Aaron は、フォーラムトピックを切り取って、そのトピックをモデレート対象の別のフォーラムに移動できます
* Aaron は「管理」を選択してモデレートコンソールにアクセスできます

![chlimage_1-2](assets/chlimage_1-2.png)

管理メニュー項目を選択して、 [モデレートコンソール](moderation.md) パブリッシュ環境から。

コミュニティモデレーターの場合、GeometrixxEngage コミュニティサイトからのモデレート可能なコンテンツのみが表示されます。

コミュニティモデレーターには、管理者と同じオプション（画像は検索サイドバーを閉じた状態です）がありますが、他のAEMコンソールにはアクセスできません。

ログアウト.

![moderatoraccess](assets/moderatoraccess.png)

### コンテンツ作成者 (#1) {#content-author}

スレッドを開始したコミュニティメンバーである Rebekah Larsen(rebekah.larsen@mailinator.com) としてログインし、「フォーラム」を選択してスレッドにアクセスし、Hummingbird の投稿の「続きを読む」を選択します。

注意

* Rebekah は自分の投稿を削除または編集できます
* Rebekah は他のコンテンツに返信またはフラグを設定することもできます
* Rebekah はモデレートコンソールにアクセスできません

![chlimage_1-3](assets/chlimage_1-3.png)
