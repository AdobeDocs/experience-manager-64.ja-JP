---
title: シングルサインオンとタイムアウトハンドラー
seo-title: Single Sign On and timeout handlers
description: AEM Forms Workspace のセッションのタイムアウト値を設定する方法。
seo-description: How-to set the session timeout value for AEM Forms workspace.
uuid: 17583fd5-6453-41d3-bb63-a639983fbea9
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: forms-workspace
discoiquuid: 698990a2-dd3f-480f-9d15-d87563860297
exl-id: eb7afdd3-0901-4dfb-b23c-88c46b5a4fb5
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 51%

---

# シングルサインオンとタイムアウトハンドラー {#single-sign-on-and-timeout-handlers}

AEM Forms Workspace は SSO 対応です。ユーザーがForms Manager やPDFジェネレーターなどのAEM Formsアプリケーションにログインし、同じブラウザーセッションでAEM Forms Workspace にアクセスした場合、そのユーザーはAEM Forms Workspace にログインし、その逆も同様になります。

## AEM Forms Workspace でのサーバータイムアウトの処理 {#handling-server-timeout-in-nbsp-aem-forms-workspace}

ユーザーに対するセッションタイムアウトは、 管理コンソールで設定できます。

タイムアウトを設定するには、にログインします。 `https://[server]:[port]/adminui`に移動します。 **「設定」>「ユーザー管理」>「設定」>「高度なシステム属性を設定」**&#x200B;をクリックし、必要な設定を行います。

AEM Forms Workspace のタイムアウトは、次のように処理されます。

* ユーザーのセッション時間長は、ユーザーセッションを初期設定する `initialize` コールに応答して得られます。
* ポップアップダイアログが表示され、セッションが期限切れになる 15 秒前に、そのことがユーザーに通知されます。

このポップアップダイアログで、以下のようにします。

* 「OK」をクリックすると、ユーザーセッションが終了します。
* 「キャンセル」をクリックすると、ユーザーセッションが再初期設定されます。

>[!NOTE]
>
>何も実行されなかった場合、ユーザーは、セッションの有効期限が 3 秒前に、AEM Forms Workspace から自動的にログアウトされます。
