---
title: シングルサインオンとタイムアウトハンドラー
seo-title: Single Sign On and timeout handlers
description: AEM Forms Workspace のセッションタイムアウト値の設定方法。
seo-description: How-to set the session timeout value for AEM Forms workspace.
uuid: 17583fd5-6453-41d3-bb63-a639983fbea9
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: forms-workspace
discoiquuid: 698990a2-dd3f-480f-9d15-d87563860297
exl-id: eb7afdd3-0901-4dfb-b23c-88c46b5a4fb5
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '225'
ht-degree: 56%

---

# シングルサインオンとタイムアウトハンドラー {#single-sign-on-and-timeout-handlers}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

AEM Forms workspace は SSO 有効です。 ユーザーが Forms Manager、PDF Generator ユーザーインターフェイスなどの AEM Forms アプリケーションにログインして同じブラウザーセッションの AEM Forms Workspace にアクセスした場合、ユーザーは AEM Forms Workspace にもログインしたことになります。その逆の場合も同じです。

## AEM Forms Workspace でのサーバータイムアウトの処理 {#handling-server-timeout-in-nbsp-aem-forms-workspace}

ユーザーのセッションタイムアウトは、管理コンソールで設定できます。

タイムアウトを設定するには、`https://[server]:[port]/adminui` にログインし、**設定／User Management／設定／詳細なシステム属性の設定**&#x200B;に移動して必要な設定を行います。

AEM Forms Workspace で、タイムアウトは次のように処理されます。

* ユーザーのセッション時間は、ユーザーセッションを初期設定する `initialize` コールに応答して得られます。
* ポップアップダイアログが表示され、セッションの有効期限が 15 秒前にセッションの有効期限が切れようとしていることがユーザーに通知されます。

このポップアップダイアログで、次の操作を実行します。

* 「 OK 」をクリックして、ユーザーセッションを終了します。
* 「キャンセル」をクリックして、ユーザーセッションを再初期化します。

>[!NOTE]
>
>何もしなかった場合は、セッション期限切れの 3 秒前に、ユーザーは AEM Forms Workspace から自動的にログアウトされます。
