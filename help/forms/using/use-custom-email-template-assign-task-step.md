---
title: タスクの割り当て手順におけるカスタムのメールテンプレートの使用
seo-title: Use custom email templates in an Assign Task step
description: フォームワークフローの電子メール通知用のカスタム電子メールテンプレート
seo-description: Custom email templates for forms workflow email notifications
uuid: bc2af94d-d4ad-417e-b3d2-bcfffc1b306d
topic-tags: publish
discoiquuid: c447fc39-c0f3-4932-ac6c-465d1fb83f8c
exl-id: 5af73823-2c32-41b3-9ab8-a7ad9fd9532f
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '531'
ht-degree: 39%

---

# タスクの割り当て手順におけるカスタムのメールテンプレートの使用 {#use-custom-email-templates-in-an-assign-task-step}

フォームワークフローの電子メール通知用のカスタム電子メールテンプレート

タスクの割り当て手順を使用して、タスクを作成し、ユーザーまたはグループに割り当てることができます。 タスクがユーザーまたはグループに割り当てられると、定義されたユーザーまたは定義されたグループの各メンバーに電子メール通知が送信されます。 一般的な電子メール通知には、割り当てられたタスクのリンクと、タスクに関連する情報が含まれます。 以下の画像は、サンプルの電子メール通知を示しています。

![デフォルトのテンプレートを使用したメール通知](do-not-localize/default-email-template.png)

外観をカスタマイズし、電子メール通知でカスタムメタデータを使用することができます。 AEM Formsは、電子メール通知用の標準のテンプレートを提供します。 標準のテンプレートをカスタマイズすることも、新しいテンプレートを一から作成することもできます。

電子メール通知テンプレートは、 [HTMLE メール](https://en.wikipedia.org/wiki/HTML_email). これらの E メールは、様々な E メールクライアントや画面サイズに適応します。 さらに、E メールのスタイル設定は、テンプレート内で定義されます。

次の画像は、カスタマイズされたメール通知です。

![カスタムテンプレートを使用したメール通知](do-not-localize/customized-email.png)

## 既存のテンプレートのカスタマイズ {#customize-the-existing-template}

デフォルトでは、AEM Formsには電子メール通知用のテンプレートが用意されています。 このテンプレートには、割り当てられたタスクのタイトルの説明、期限、優先度、ワークフロー名、リンクが表示されます。 テンプレートをカスタマイズして外観を変更できます。 テンプレートをカスタマイズするには、次の手順を実行します。

1. 管理者アカウントで CRXDE にログインします。

1. /libs/fd/dashboard/templates/email に移動します。

1. htmlEmailTemplate.txt ファイルを開きます。これにはデフォルトのテンプレートが含まれています。

1. htmlEmailTemplate.txt ファイルのコンテンツをカスタムコンテンツと置き換えます。

   メール通知テンプレートは、[HTML 形式のメール](https://en.wikipedia.org/wiki/HTML_email)です。既存の HTML コードをカスタムコードで置き換えることで、テンプレートの外観を変更することができます。

1. ファイルを保存します。これでカスタマイズされたテンプレートが使用できるようになります。

## E メールテンプレートの作成 {#create-an-email-template}

デフォルトでは、AEM Formsには電子メール通知用のテンプレートが用意されています。 このテンプレートには、割り当てられたタスクのタイトルの説明、期限、優先度、ワークフロー名、リンクが表示されます。 また、タスクの割り当て手順用に、カスタム電子メールテンプレート（独自のテンプレート）を追加することもできます。 次の手順を実行して、カスタム電子メールテンプレートを追加します。

1. 管理者アカウントで CRXDE にログインします。

1. /libs/fd/dashboard/templates/email に移動します。

1. .txt ファイルを作成します。例えば、EmailOnTaskAssign.txt などです。

1. カスタムの HTML コードをファイルに追加します。

   メール通知テンプレートは、[HTML 形式のメール](https://en.wikipedia.org/wiki/HTML_email)です。カスタムの HTML コードをファイルに追加して、新しいテンプレートを作成します。

1. ファイルを保存します。テンプレートが、タスクの割り当て手順で使用できるようになりました。

## タスクの割り当て手順での電子メールテンプレートの使用 {#use-an-email-template-in-an-assign-task-step}

タスクの割り当て手順は、デフォルトのテンプレートである htmlEmailTemplate.txt を使用するようにデフォルトで設定されています。 カスタムテンプレートを使用するように選択できます。 テンプレートを変更するには：

1. を開きます。 **[!UICONTROL タスクを割り当て]** 手順

1. に移動します。 **[!UICONTROL 担当者/HTMLメールテンプレート]**.

1. 新しく作成された HTML メールテンプレートを選択します。

1. 「**[!UICONTROL OK]**」をクリックします。テンプレートが変更されました。

電子メール通知では、 [メタデータ](/help/forms/using/use-metadata-in-email-notifications.md). 例えば、期限、優先度、ワークフロー名などです。 [カスタムメタデータ](/help/forms/using/use-metadata-in-email-notifications.md#using-custom-metadata-in-an-email-notification)を使用するために、テンプレートを設定することもできます。
