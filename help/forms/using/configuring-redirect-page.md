---
title: リダイレクトページの設定
seo-title: Configuring redirect page
description: アダプティブフォームに入力すると、フォームの作成時にフォーム作成者が設定できる Web ページにユーザーがリダイレクトされます。
seo-description: After filling an adaptive form, users can be redirected to a webpage that form authors can configure while creating the form.
uuid: 5a5f912a-9696-4bc1-af3f-ead78f767e02
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: author
discoiquuid: c51817aa-193a-4d4f-bd83-06518ddfb395
feature: Adaptive Forms
exl-id: bbe10952-d6a7-4adc-bab9-388c1ee8e56a
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '238'
ht-degree: 83%

---

# リダイレクトページの設定 {#configuring-redirect-page}

フォーム作成者は、フォーム送信後にユーザーがリダイレクトされるページを各フォームに設定することができます。

1. 編集モードで、コンポーネントを選択し、![フィールドレベル](assets/field-level.png)／**アダプティブフォームコンテナ**&#x200B;をクリックしてから、 ![cmppr](assets/cmppr.png) をクリックします。

1. サイドバーで、「**送信**」をクリックします。

1. 送信セクションの「ありがとうございました」ページで、リダイレクトページの URL を指定します。
1. オプションとして、「送信アクション」で、「REST エンドポイントへの送信」の送信アクションについて、リダイレクトページに渡されるパラメーターを設定することができます。

![リダイレクトページ設定](assets/thank-you-setting-1.png)
**図：** *リダイレクトページの設定*

フォーム作成者は、次のパラメーターを使用して「ありがとうございました」ページに渡すことができます。 使用可能なすべての送信アクションに対して、`status` と `owner` のパラメーターが渡されます。これら 2 つのパラメーターの他に、追加のパラメーターが次の送信アクションに渡されます。

* **コンテンツを格納アクション**（非推奨）：送信されたデータが格納されるリポジトリのノードのパス `contentPath` が渡されます。

* **PDF の保存アクション**（非推奨）：送信されたデータと、リポジトリで PDF ファイルを保存しているノードのパス `contentPath` が渡されます。

* **フォームワークフローへの送信**：フォームワークフローから返される出力パラメーターが渡されます。

* **REST エンドポイントへの送信**：フィールド内にパラメーターマッピングのため追加されたパラメータが渡されます。`status` および `owner` パラメーターは、この送信アクションでは渡されません。詳しくは、[送信アクション「REST エンドポイントへの送信」の設定](/help/forms/using/configuring-submit-actions.md)を参照してください。 
