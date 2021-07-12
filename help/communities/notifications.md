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
role: Admin
exl-id: f6c6619e-b386-4d34-9d17-654d7c97aedd
source-git-commit: 3c050c33a384d586d74bd641f7622989dc1d6b22
workflow-type: tm+mt
source-wordcount: '537'
ht-degree: 48%

---

# コミュニティの通知 {#communities-notifications}

## 概要 {#overview}

AEM Communities には、サインインしているコミュニティメンバーにとって興味深いイベントを表示する通知セクションが用意されています。

通知は[アクティビティ](essentials-activities.md)や[購読](subscriptions.md)と同様に、以下に基づいて生成されます。

* コンテンツを投稿するメンバー
* 別のメンバーに従うことを選択したメンバー
* 特定のトピック、記事、およびコンテンツの他のスレッドをフォローすることを選択したメンバー

通知は以下の点でアクティビティや購読と異なります。

* 通知セクションへのリンクは、コミュニティサイトのヘッダーに常に存在します
   * アクティビティでは、コミュニティサイトの構造に[アクティビティストリーム機能](functions.md#activity-stream-function)を含める必要があります
   * サブスクリプションには[電子メール](email.md)の設定が必要
* 通知の実装は、拡張性とプラグ可能なチャネルを通じて行われます
   * アクティビティはWebでのみ使用できます
   * 購読はEメールを使用した場合のみ利用できます

Communities [FP1](deploy-communities.md#latestfeaturepack) 以降、使用可能な通知チャネルは以下のとおりです。

* `Notifications`リンクを使用してアクセスするWebチャネル
* Eメールチャネル（Eメールが正しく設定されている場合に使用可能）

今後のチャネルとしてモバイルおよびデスクトップがあります。

### 要件 {#requirements}

**電子メールの設定**

通知の電子メールチャネルを機能させるには、電子メールを設定する必要があります。

電子メールを設定する手順については、[電子メールの設定](analytics.md)を参照してください。

**フォローの有効化**

フォローを有効にするようにコンポーネントを設定する必要があります。以下を可能にする機能には、[blog](blog-feature.md)、[forum](forum.md)、[Q&amp;A](working-with-qna.md)、[calendar](calendar.md)、[filelibrary](file-library.md)、[comments](comments.md)があります。

以下の点に注意してください。

* コミュニティ[サイトテンプレート](sites.md)および[グループテンプレート](tools-groups.md)内で使用されるコンポーネントは、既にフォローを許可するように設定されている場合があります

* メンバープロファイルは、他のメンバーがフォローできるように既に設定されています

## フォローによる通知 {#notifications-from-following}

![chlimage_1-254](assets/chlimage_1-254.png)

「**フォロー**」ボタンを使用すると、エントリをアクティビティや購読、通知としてフォローできます。「**フォロー**」ボタンを選択するたびに、選択のオン/オフを切り替えることができます。 `Email Subscriptions`は、設定時にのみ表示されます。

フォロー方法が選択されると、ボタンのテキストが「**フォロー中**」に変わります。 便宜上、`Unfollow All`を選択してすべてのメソッドをオフに切り替えることができます。

「**フォロー**」ボタンが表示されます

* 別のメンバーのプロファイルを表示する場合
* フォーラム、Q&amp;A、ブログなどのメイン機能ページ
   * その一般的な機能のすべてのアクティビティに従う
* フォーラムトピック、Q&amp;A質問、ブログ記事などの特定のエントリ
   * その特定のエントリのすべてのアクティビティに従う

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

[ウィザードで作成されたコミュニティサイト](sites-console.md)に、バナーの上にあるサイトのヘッダーバーに`Notifications`機能へのリンクが含まれるようになりました。 メッセージとは異なり、通知はコミュニティサイトごとに作成され、メッセージはサイト作成プロセス中に有効にする必要があります。

公開済みサイトにアクセスする際に、`Notifications`リンクを選択すると、そのメンバーに関するすべての通知が表示されます。

![chlimage_1-258](assets/chlimage_1-258.png)

### 電子メール通知 {#email-notifications}

電子メールチャネルを有効にすると、メンバーは、Web 上のコンテンツへのリンクが記載されている電子メールを受信します。

![chlimage_1-259](assets/chlimage_1-259.png)
