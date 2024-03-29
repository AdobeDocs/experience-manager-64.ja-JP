---
title: 共有キューの設定
seo-title: Configuring Shared Queues
description: 共有キューを使用すると、ユーザーキューを効果的に設定および管理できます。 共有キューを設定する方法を説明します。
seo-description: Shared Queues allow you to configure and manage user queues effectively. Learn how to configure shared queues.
uuid: 69ab611d-334b-40a5-bd2d-533d4cb25eda
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms_workflow
products: SG_EXPERIENCEMANAGER/6.4/FORMS
discoiquuid: fc403a60-b635-4334-9bf8-2f3d2036b2f3
exl-id: 40890db3-240c-4021-967a-b6b3eb1d4b7c
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '688'
ht-degree: 7%

---

# 共有キューの設定{#configuring-shared-queues}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

共有キューを使用すると、ユーザーキューを効果的に設定および管理できます。 ユーザーキューは、ユーザーに割り当てられたすべてのタスクです。 [タスクリスト](https://help.adobe.com/ja_JP/livecycle/11.0/WorkspaceHelp/WS92d06802c76abadb-2b6ab502126beb6ba2f-7ffc.2.html) を参照してください。 組織のニーズに応じて、ユーザーキューを割り当て、割り当て解除、再割り当てできます。 共有キューは次の 2 つの方法で管理できます。

**ユーザーへのアクセスを管理**

このオプションを使用して、選択したユーザーキューへのアクセスを管理できます。

**ユーザーによるアクセスの管理**

このオプションを使用して、選択したユーザーに割り当てられた共有キューを管理できます。

## 選択したユーザーキューへのアクセスの管理 {#managing-access-to-a-selected-user-queue}

「ユーザーへのアクセスを管理」機能を使用すると、選択したユーザーキューへのアクセスを管理できます。 選択したユーザーキューへのアクセスを組織内の他のユーザーに許可または取り消すことができます。 例えば、Kara Bowman は不在です。 「ユーザーへのアクセスを管理」機能を使用して、ユーザーのキューを田中明および John Jacobs と共有して完了できます。 後で、Kara Bowman がオフィスに戻ると、Kara Bowman と John Jacobs のキューへのアクセスを取り消すことができます。

共有が完了すると、これらのタスクは、Workspace を使用して、キューへのアクセス権を持つユーザーが完了できます。

>[!NOTE]
>
>AEM Forms のリリースでは Flex Workspace は廃止されています。

### 選択したユーザーキューへのアクセスの設定 {#configuring-access-to-a-selected-user-queue}

1. 管理者アカウントを使用して管理コンソールにログインします。
1. 選択 **サービス** > **フォームワークフロー** > **共有キュー**.

1. 「ユーザーへのアクセスを管理」タブで、共有するキューのユーザーを探して選択します。 右下のウィンドウには、選択したユーザーキューにアクセスできるユーザーのリストが表示されます。
1. 左下のウィンドウで、ユーザーを探して選択します。 「共有」をクリックします。
1. 「保存」をクリックして完了します。

### 選択したユーザーキューへのアクセスの取り消し {#revoking-access-to-a-selected-user-queue}

1. 管理者アカウントを使用して管理コンソールにログインします。
1. 選択 **サービス** > **フォームワークフロー** > **共有キュー**.

1. 「ユーザーへのアクセスを管理」タブで、管理するキューのユーザーを探して選択します。
1. 右下のウィンドウには、選択したユーザーキューへのアクセス権を持つユーザーのリストが表示されます。 ユーザーを選択し、「失効」をクリックします。
1. 「保存」をクリックして完了します。

## ユーザーに割り当てられたキューの管理 {#managing-queues-assigned-to-a-user}

「ユーザーによるアクセスを管理」機能を使用すると、選択したユーザーに割り当てられたキューを管理できます。 選択したユーザーに対して、ユーザーキューへのアクセスを個別に許可または取り消すことができます。 例えば、Akira Tanaka と John Jacobs のユーザーキューを Kara Bowman に割り当てるとします。 「ユーザーによるアクセスを管理」機能を使用して、Kara Bowman を検索し、Akira Tanaka および John Jacobs に割り当てられたタスクへのアクセス権を付与できます。 後で、Kara Bowman によるこれらのユーザーキューへのアクセスを取り消すことができます。

割り当てられたタスクは、ユーザーが Workspace を使用して完了できます。

>[!NOTE]
>
>AEM Forms のリリースでは Flex Workspace は廃止されています。

### 選択したユーザーキューへのアクセスの許可 {#granting-access-to-a-selected-user-queue}

1. 管理者アカウントを使用して管理コンソールにログインします。
1. 選択 **サービス** > **フォームワークフロー** > **共有キュー**.

1. 「ユーザーへのアクセスを管理」タブで、共有するキューのユーザーを探して選択します。 右下のウィンドウには、選択したユーザーキューにアクセスできるユーザーのリストが表示されます。
1. 左下のウィンドウで、選択したユーザーと共有するユーザーキューを探して選択します。 「共有」をクリックします。
1. 「保存」をクリックして完了します。

### 選択したユーザーキューへのアクセスの取り消し {#revoking_access_to_a_selected_user_queue-1}

1. 管理者アカウントを使用して管理コンソールにログインします。
1. 選択 **サービス** > **フォームワークフロー** > **共有キュー**.

1. 「ユーザーによるアクセスの管理」タブで、管理するキューのユーザーを探して選択します。
1. 右下のウィンドウには、選択したユーザーに割り当てられたユーザーキューのリストが表示されます。 ユーザーキューを選択し、「失効」をクリックします。
1. 「保存」をクリックして完了します。
