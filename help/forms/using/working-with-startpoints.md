---
title: スタートポイントの使用
seo-title: Working with Startpoints
description: Workbench で定義されたモバイルデバイスからAEM Formsプロセスを操作する手順です。
seo-description: Steps to work with a AEM Forms process from your Mobile device defined in Workbench.
uuid: 9c51ce52-e7ba-43d3-a85c-67067f680ccb
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: forms-app
discoiquuid: 265eee8a-364e-4edf-b2a0-f42617169944
exl-id: ef9352c7-c164-4cbf-8f18-5b97aa5f56be
source-git-commit: 977ada5fefe476c7cd2fe1470eb024a517a681d2
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 54%

---

# スタートポイントの使用 {#working-with-startpoints}

スタートポイントは Workbench で作成されたプロセスを呼び出します。これはフォームの送信時にプロセスを呼び出すフォームに関連付けられています。詳しくは、 [Geometrixxファイナンスリファレンスサイトのチュートリアル](/help/forms/using/finance-reference-site-walkthrough.md) プロセスを理解するために。

>[!NOTE]
>
>この概念について参照すると、スタートポイント、スタートプロセス、フォームという用語が区別なく使用される場合があります。

AEM Forms アプリケーションからプロセスを開始するには、プロセスで&#x200B;**ワークスペース**&#x200B;タイプのスタートポイントが必要です。また、 **[!UICONTROL Mobile Workspace に表示]** オプションを使用します。

![mws_startpoint_select_option](assets/mws_startpoint_select_option.png)

**Workbench で定義されたプロセスを開始するには**

1. AEM Formsアプリで使用可能な Startpoint を表示するには、に移動します。 [ホーム画面](/help/forms/using/home-screen.md).
1. デフォルトでは、**[!UICONTROL ホーム]**&#x200B;画面に「**[!UICONTROL すべてのフォーム]**」リストが表示されます。

   スタートポイントはフォームに関連付けられています。リストでスタートポイントに関連付けられているフォームをタップして開きます。

   スタートポイントに関連付けられているフォームが開きます。

1. **[!UICONTROL スタートポイント]**&#x200B;フォームに、詳細情報を入力します。

   「[添付ファイル](/help/forms/using/add-attachments.md)」ボタンを使用して、このタスクに注釈を追加できます。

1. フォームを入力したら、「**送信**」ボタンをタップします。

アプリがオフラインの場合、フォームとそのデータは Outbox フォルダーに保存されます。

アプリがオンラインの場合、タスクはAEM Formsサーバーと同期され、プロセスで指定されたユーザーに割り当てられます。

タスクリスト内のタスクを操作するには、 [タスクを開く](/help/forms/using/open-task.md).
