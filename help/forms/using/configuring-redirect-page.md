---
title: リダイレクトページの設定
seo-title: リダイレクトページの設定
description: アダプティブフォーム入力後、フォーム作成時にフォーム作成者が設定可能な Web ページへ、ユーザーをリダイレクトさせることができます。
seo-description: アダプティブフォーム入力後、フォーム作成時にフォーム作成者が設定可能な Web ページへ、ユーザーをリダイレクトさせることができます。
uuid: 5a5f912a-9696-4bc1-af3f-ead78f767e02
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: author
discoiquuid: c51817aa-193a-4d4f-bd83-06518ddfb395
translation-type: tm+mt
source-git-commit: 8cbfa421443e62c0483756e9d5812bc987a9f91d

---


# リダイレクトページの設定 {#configuring-redirect-page}

フォーム作成者は、フォーム送信後にユーザーがリダイレクトされるページを各フォームに設定することができます。

1. In the edit mode, select a component, then click ![field-level](assets/field-level.png) > **Adaptive Form Container**, and then click ![cmppr](assets/cmppr.png).

1. サイドバーで、「**送信**」をクリックします。

1. 送信セクションの「ありがとうございました」ページで、リダイレクトページの URL を指定します。
1. オプションとして、「送信アクション」で、「REST エンドポイントへの送信」の送信アクションについて、リダイレクトページに渡されるパラメーターを設定することができます。

![](assets/thank-you-setting-1.png) リダイレクトページの設定&#x200B;****&#x200B;図：リダイレクト *ページの設定*

フォーム作成者は、「ありがとうございます」ページに渡される次のパラメーターを使用することができます。For all the available submit actions, `status` and `owner` parameters are passed. これら 2 つのパラメーターの他に、追加のパラメーターが次の送信アクションに渡されます。

* **コンテンツ保存アクション** （非推奨）:送信 `contentPath`されたデータが保存されるリポジトリ内のノードのパス。

* **PDFの保存アクション** （非推奨）:送信さ `contentPath`れたデータのパスと、リポジトリにPDFファイルを格納しているノードのパスが渡されます。

* **フォームワークフローへの送信**：フォームワークフローから返される出力パラメーターが渡されます。

* **REST エンドポイントへの送信**：フィールド内にパラメーターマッピングのため追加されたパラメータが渡されます。`status` および `owner` パラメーターは、この送信アクションでは渡されません。詳しくは、[送信アクション「REST エンドポイントへの送信」の設定](/help/forms/using/configuring-submit-actions.md)を参照してください。 

