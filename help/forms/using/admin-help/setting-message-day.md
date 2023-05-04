---
title: 今日のお知らせの設定
seo-title: Setting the message of the day
description: 今日のメッセージを使用すると、Workspace ユーザーインターフェイスのようこそページに表示するメッセージを設定できます。
seo-description: The message of the day let you set a message to be displayed on the Welcome page in the Workspace user interface.
uuid: 9c664438-6fc0-498e-bb3f-4c6bcb9414a7
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_workspace
products: SG_EXPERIENCEMANAGER/6.4/FORMS
discoiquuid: c2b3a412-70c2-4257-bfb4-1430bb1f8891
exl-id: 7ddd5a4d-2b46-4408-b241-81e16cfead3c
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 26%

---

# 今日のお知らせの設定 {#setting-the-message-of-the-day}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

Workspace ユーザーインターフェイスのようこそページに表示するメッセージを設定できます。

必要に応じて、AdobeFlash® Player でサポートされているHTMLタグを使用して、テキストの外観を書式設定できます。

* &lt;a> アンカータグ
* &lt;b> 太字タグ
* &lt;br> タグを解除
* &lt;font> フォントタグ
* &lt;img> 画像タグ
* &lt;i> 斜体タグ
* &lt;li> リスト項目タグ
* &lt;p> 段落タグ
* &lt;span> スパンタグ
* &lt;textformat> テキスト形式タグ
* &lt;u> タグに下線を引く

サポートされているタグについて詳しくは、[Flex Language Reference](https://flex.apache.org/) の TextField クラスの `htmlText` ロパティの定義を参照してください。

## 今日のメッセージを設定 {#set-the-message-of-the-day}

1. 管理コンソールで、サービス/Workspace/今日のメッセージをクリックします。
1. 「今日のメッセージ」ボックスに、ようこそ画面に表示するテキストを入力します。
1. 「保存」をクリックします。

>[!NOTE]
>
>AEM Forms のリリースでは Flex Workspace は廃止されています。
