---
title: コミュニティの通知
seo-title: コミュニティの通知
description: AEM Communities には、サインインしているコミュニティメンバーにとって興味深いイベントを表示する通知が用意されています
seo-description: AEM Communities には、サインインしているコミュニティメンバーにとって興味深いイベントを表示する通知が用意されています
uuid: d6ef12f1-7367-49a5-b891-56800a38b2ab
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.4/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 47201e2d-338d-40e0-af82-c681a552807b
translation-type: tm+mt
source-git-commit: 5ddbcb2addff2d6e3a3e9d7e100a6d9ba89fdd60
workflow-type: tm+mt
source-wordcount: '537'
ht-degree: 48%

---


# コミュニティの通知 {#communities-notifications}

## 概要 {#overview}

AEM Communities には、サインインしているコミュニティメンバーにとって興味深いイベントを表示する通知セクションが用意されています。

通知は[アクティビティ](essentials-activities.md)や[購読](subscriptions.md)と同様に、以下に基づいて生成されます。

* コンテンツを投稿するメンバ
* 別のメンバーに従うことを選択したメンバー
* 特定のトピック、記事、およびコンテンツの他のスレッドをフォローすることを選択したメンバー

通知は以下の点でアクティビティや購読と異なります。

* 通知セクションへのリンクは、コミュニティサイトのヘッダーに常に存在します
   * Activities require the [activity stream function](functions.md#activity-stream-function) to be included in the community site&#39;s structure
   * Subscriptions require [configuration of email](email.md)
* 通知の実装は、拡張性とプラグ可能なチャネルを通じて行われます。
   * アクティビティはWeb上でのみ使用できます
   * 購読は電子メールでのみ使用できます

Communities [FP1](deploy-communities.md#latestfeaturepack) 以降、使用可能な通知チャネルは以下のとおりです。

* The web channel, accessed using the `Notifications` link
* 電子メールチャネル。電子メールが正しく設定されている場合に使用できます

今後のチャネルとしてモバイルおよびデスクトップがあります。

### 要件 {#requirements}

**電子メールの設定**

通知の電子メールチャネルを機能させるには、電子メールを設定する必要があります。

電子メールを設定する手順については、[電子メールの設定](analytics.md)を参照してください。

**フォローの有効化**

フォローを有効にするようにコンポーネントを設定する必要があります。Features that allow following are [blog](blog-feature.md), [forum](forum.md), [QnA](working-with-qna.md), [calendar](calendar.md), [filelibrary](file-library.md), and [comments](comments.md).

以下の点に注意してください。

* Components used within community [site templates](sites.md) and [group templates](tools-groups.md) may already be configured to allow following

* メンバプロファイルは、他のメンバが従うように既に構成されています

## フォローによる通知 {#notifications-from-following}

![chlimage_1-254](assets/chlimage_1-254.png)

「**フォロー**」ボタンを使用すると、エントリをアクティビティや購読、通知としてフォローできます。Each time the **Follow** button is selected, it is possible to toggle on or off a selection. The `Email Subscriptions` selection is only present when configured.

フォロー方法が選択されると、ボタンのテキストが「**フォロー中**」に変わります。 For convenience, it is possible to select `Unfollow All` to toggle off all methods.

The **Follow** button will appear

* 別のメンバーのプロファイルを表示する場合
* フォーラム、QnA、ブログなどのメイン機能ページ
   * その一般的な機能のすべてのアクティビティに従う
* フォーラムトピック、QnA質問、ブログ記事など、特定のエントリ
   * 特定のエントリのすべてのアクティビティに従う

## 通知設定の管理 {#managing-notification-settings}

通知ページから通知設定リンクを選択すると、各メンバーは通知の受信方法を管理することができます。

Web チャネルは常に有効になっています。

![chlimage_1-255](assets/chlimage_1-255.png)

電子メールチャネルでは、Web チャネルの場合と同様の設定が用意されていますが、別途適切な[電子メールの設定](email.md)が必要です。

電子メールチャネルは、デフォルトでオフになっています。

![chlimage_1-256](assets/chlimage_1-256.png)

これはメンバーがオンにすることもできますが、それでも電子メールの設定によって決まります。

![chlimage_1-257](assets/chlimage_1-257.png)

## 通知の表示 {#viewing-notifications}

### Web 通知 {#web-notifications}

A [wizard created community site](sites-console.md) now includes a link to the `Notifications` feature in the site&#39;s header bar above the banner. メッセージとは異なり、通知はすべてのコミュニティサイトに対して作成されますが、メッセージはサイト作成プロセス中に有効にする必要があります。

When visiting the published site, selecting the `Notifications` link will display all notifications for the member.

![chlimage_1-258](assets/chlimage_1-258.png)

### 電子メール通知 {#email-notifications}

電子メールチャネルを有効にすると、メンバーは、Web 上のコンテンツへのリンクが記載されている電子メールを受信します。

![chlimage_1-259](assets/chlimage_1-259.png)

