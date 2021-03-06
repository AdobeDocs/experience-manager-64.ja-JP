---
title: タスクの割り当て手順におけるカスタムの電子メールテンプレートの使用
seo-title: Use custom email templates in an Assign Task step
description: 'Forms ワークフローの電子メール通知のカスタム電子メールテンプレート '
seo-description: Custom email templates for forms workflow email notifications
uuid: bc2af94d-d4ad-417e-b3d2-bcfffc1b306d
topic-tags: publish
discoiquuid: c447fc39-c0f3-4932-ac6c-465d1fb83f8c
exl-id: 5af73823-2c32-41b3-9ab8-a7ad9fd9532f
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '531'
ht-degree: 94%

---

# タスクの割り当て手順におけるカスタムの電子メールテンプレートの使用 {#use-custom-email-templates-in-an-assign-task-step}

Forms ワークフローの電子メール通知のカスタム電子メールテンプレート

ユーザーまたはグループにタスクを作成して割り当てるには、タスクの割り当て手順を使用します。ユーザーまたはグループにタスクが割り当てられると、電子メール通知が指定されたユーザーまたは指定されたグループのメンバーに送信されます。一般的な電子メール通知には、割り当てられたタスクのリンクと、タスクに関連する情報が含まれています。次の画像は、サンプルの電子メール通知を示します。

![初期設定済みテンプレートを使用した電子メール通知](do-not-localize/default-email-template.png)

電子メール通知では、外観をカスタマイズしてカスタムメタデータを使用することができます。AEM Forms には電子メール通知用の初期設定済みテンプレートが用意されています。初期設定済みテンプレートをカスタマイズするか、新しいテンプレートをゼロから作成することができます。

電子メール通知テンプレートは、[HTML 形式の電子メール](https://en.wikipedia.org/wiki/HTML_email)をベースにしています。これらの電子メールは、様々な電子メールクライアントや画面サイズに対応します。さらに、電子メールのスタイルはテンプレート内で定義されます。

次の画像は、カスタマイズされた電子メール通知を表示します。

![カスタムテンプレートを使用した電子メール通知](do-not-localize/customized-email.png)

## 既存テンプレートのカスタマイズ {#customize-the-existing-template}

AEM Forms には電子メール通知用の初期設定済みテンプレートが用意されています。テンプレートには、タイトルの説明、期限、優先度、ワークフロー名、割り当てられたタスクのリンクが含まれています。テンプレートをカスタマイズして外観を変更することができます。次の手順を実行してテンプレートをカスタマイズします。

1. 管理者アカウントで CRXDE にログインします。

1. /libs/fd/dashboard/templates/email に移動します。

1. htmlEmailTemplate.txt ファイルを開きます。これにはデフォルトのテンプレートが含まれています。

1. htmlEmailTemplate.txt ファイルのコンテンツをカスタムのコンテンツと置き換えます。

   電子メール通知のテンプレートは、[HTML 形式の電子メール](https://en.wikipedia.org/wiki/HTML_email)です。既存の html コードをカスタムのコードで置き換えることで、テンプレートの外観を変更することができます。

1.  ファイルを保存します。これでカスタマイズされたテンプレートが使用できるようになります。

## 電子メールテンプレートの作成 {#create-an-email-template}

AEM Forms には電子メール通知用の初期設定済みテンプレートが用意されています。テンプレートには、タイトルの説明、期限、優先度、ワークフロー名、割り当てられたタスクのリンクが含まれています。また、タスクの割り当て手順にカスタムの電子メールテンプレート（独自のテンプレート）を追加できます。次の手順を実行して、カスタムの電子メールテンプレートを追加します。

1. 管理者アカウントで CRXDE にログインします。

1. /libs/fd/dashboard/templates/email に移動します。

1. .txt ファイルを作成します。例えば、EmailOnTaskAssign.txt のようにします。

1. カスタムの HTML コードをファイルに追加します。

   電子メール通知のテンプレートは、[HTML 形式の電子メール](https://en.wikipedia.org/wiki/HTML_email)です。カスタムの HTML コードをファイルに追加して、新しいテンプレートを作成します。

1.  ファイルを保存します。テンプレートは、タスクの割り当て手順で使用することができます。

## タスクの割り当て手順における電子メールテンプレートの使用 {#use-an-email-template-in-an-assign-task-step}

タスクの割り当て手順では、初期状態でデフォルトテンプレート htmlEmailTemplate.txt を使用するように設定されています。カスタムのテンプレートを使用するように選択できます。テンプレートの場所を変更するには：

1. を開きます。 **[!UICONTROL タスクを割り当て]** 手順

1. に移動します。 **[!UICONTROL 担当者/HTMLメールテンプレート]**.

1. 新規作成された HTML 電子メールテンプレートを選択します。

1. 「**[!UICONTROL OK]**」をクリックします。テンプレートが変更されました。

電子メール通知では、[メタデータ](/help/forms/using/use-metadata-in-email-notifications.md)も使用します。例えば、期限、優先度、ワークフロー名などです。また、使用するテンプレートを設定することもできます [カスタムメタデータ](/help/forms/using/use-metadata-in-email-notifications.md#using-custom-metadata-in-an-email-notification).
