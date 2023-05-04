---
title: コミュニティの通知
seo-title: Communities Notifications
description: AEM Communitiesには、サインインしたコミュニティメンバーに関心のあるイベントを表示する通知が用意されています
seo-description: AEM Communities has notifications that display events of interest to the signed-in community member
uuid: d6ef12f1-7367-49a5-b891-56800a38b2ab
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.4/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 47201e2d-338d-40e0-af82-c681a552807b
role: Admin
exl-id: f6c6619e-b386-4d34-9d17-654d7c97aedd
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '557'
ht-degree: 4%

---

# コミュニティの通知 {#communities-notifications}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

## 概要 {#overview}

AEM Communitiesには、サインインしているコミュニティメンバーに関心のあるイベントを表示する通知セクションが用意されています。

通知は、 [アクティビティ](essentials-activities.md) および [購読](subscriptions.md) 結果として

* コンテンツを投稿するメンバー
* 別のメンバーに従うことを選択したメンバー
* 特定のトピック、記事、およびコンテンツの他のスレッドに従うことを選択したメンバー

通知とアクティビティおよびサブスクリプションの違いは、

* 通知セクションへのリンクは、コミュニティサイトのヘッダーに常に存在します
   * アクティビティには [アクティビティストリーム機能](functions.md#activity-stream-function) コミュニティサイトの構造に含まれる
   * 購読にはが必要です [電子メールの設定](email.md)
* 通知の実装は、拡張性とプラグ可能なチャネルを通じて行われます
   * アクティビティは Web でのみ使用できます
   * 購読は E メールでのみ利用できます

コミュニティの時点 [FP1](deploy-communities.md#latestfeaturepack)を使用する場合、使用可能な通知チャネルは次のとおりです。

* Web チャネル ( `Notifications` リンク
* E メールチャネル（E メールが正しく設定されている場合に使用可能）

将来のチャネルはモバイルとデスクトップです。

### 要件 {#requirements}

**電子メールを設定**

通知の電子メールチャネルを機能させるには、電子メールを設定する必要があります。

電子メールの設定手順については、 [電子メールの設定](analytics.md).

**フォローを有効にする**

以下を有効にするには、コンポーネントを設定する必要があります。 次の機能を使用できます。 [ブログ](blog-feature.md), [フォーラム](forum.md), [Q&amp;A](working-with-qna.md), [カレンダー](calendar.md), [filelibrary](file-library.md)、および [コメント](comments.md).

注意：

* コミュニティ内で使用されるコンポーネント [サイトテンプレート](sites.md) および [グループテンプレート](tools-groups.md) は、既に次を許可するように設定されている可能性があります

* メンバープロファイルは、他のメンバーがフォローできるように既に設定されています

## フォローからの通知 {#notifications-from-following}

![chlimage_1-254](assets/chlimage_1-254.png)

この **フォロー** ボタンを使用すると、エントリをアクティビティ、購読、通知としてフォローできます。 毎回 **フォロー** ボタンが選択されている場合、選択のオン/オフを切り替えることができます。 この `Email Subscriptions` 選択が存在するのは、設定時のみです。

次のいずれかの方法を選択した場合、ボタンのテキストは **フォロー中**. 便宜上、 `Unfollow All` をクリックして、すべてのメソッドをオフにします。

この **フォロー** ボタンが表示されます

* 別のメンバーのプロファイルを表示する場合
* フォーラム、Q&amp;A、ブログなどのメイン機能ページ
   * その一般的な機能のすべてのアクティビティに従う
* フォーラムトピック、Q&amp;A 質問、ブログ記事などの特定のエントリ
   * その特定のエントリのすべてのアクティビティに従う

## 通知設定の管理 {#managing-notification-settings}

「通知」ページから「通知設定」リンクを選択すると、各メンバーは通知の受信方法を管理できます。

Web チャネルは常に有効です。

![chlimage_1-255](assets/chlimage_1-255.png)

適切な [電子メールの設定](email.md)では、Web チャネルの場合と同じ設定を提供します。

E メールチャネルは、デフォルトではオフになっています。

![chlimage_1-256](assets/chlimage_1-256.png)

メンバーがオンにしても、設定中の電子メールに依存します。

![chlimage_1-257](assets/chlimage_1-257.png)

## 通知の表示 {#viewing-notifications}

### Web 通知 {#web-notifications}

A [ウィザードが作成したコミュニティサイト](sites-console.md) に、 `Notifications` 機能を使用します。 メッセージとは異なり、通知はすべてのコミュニティサイトに対して作成されますが、メッセージはサイト作成プロセス中に有効にする必要があります。

公開されたサイトにアクセスする際に、 `Notifications` リンクは、メンバーのすべての通知を表示します。

![chlimage_1-258](assets/chlimage_1-258.png)

### メール通知 {#email-notifications}

E メールチャネルが有効になると、メンバーは Web 上のコンテンツへのリンクを含む E メールを受け取ります。

![chlimage_1-259](assets/chlimage_1-259.png)
