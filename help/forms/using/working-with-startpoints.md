---
title: スタートポイントの使用
seo-title: スタートポイントの使用
description: Workbench で定義されたモバイルデバイスからAEM Forms プロセスを操作する手順。
seo-description: Workbench で定義されたモバイルデバイスからAEM Forms プロセスを操作する手順。
uuid: 9c51ce52-e7ba-43d3-a85c-67067f680ccb
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: forms-app
discoiquuid: 265eee8a-364e-4edf-b2a0-f42617169944
translation-type: tm+mt
source-git-commit: f13d358a6508da5813186ed61f959f7a84e6c19f
workflow-type: tm+mt
source-wordcount: '262'
ht-degree: 78%

---


# スタートポイントの使用  {#working-with-startpoints}

スタートポイントは Workbench で作成されたプロセスを呼び出します。これはフォームの送信時にプロセスを呼び出すフォームに関連付けられています。プロセスについて理解するには、「[Geometrixx Finance リファレンスサイトのチュートリアル](/help/forms/using/finance-reference-site-walkthrough.md)」を参照してください。

>[!NOTE]
>
>この概念について参照すると、スタートポイント、スタートプロセス、フォームという用語が区別なく使用される場合があります。

AEM Formsアプリからプロセスを開始するには、プロセス内にタイプ&#x200B;**Workspace**&#x200B;のスタートポイントが必要です。 また、スタートポイントに対して「**[!UICONTROL Mobile Workspace でスタートポイントを表示する]**」オプションをオンにする必要もあります。

![mws_startpoint_select_option](assets/mws_startpoint_select_option.png)

**Workbench で定義されたプロセスを開始するには**

1. AEM Forms アプリケーションで使用可能なスタートポイントを表示するには、[ホーム画面](/help/forms/using/home-screen.md)に移動してください。
1. **[!UICONTROL ホーム]**&#x200B;画面には、デフォルトで&#x200B;**[!UICONTROL すべてのForms]**&#x200B;リストが表示されます。

   スタートポイントはフォームに関連付けられています。リスト内でスタートポイントに関連付けられたフォームをタップして開きます。

   スタートポイントに関連付けられているフォームが開きます。

1. **[!UICONTROL スタートポイント]**&#x200B;フォームに、詳細情報を入力します。

   「[添付ファイル](/help/forms/using/add-attachments.md)」ボタンを使用して、このタスクに注釈を追加できます。

1. フォームに入力したら、「**送信**」ボタンをタップします。

アプリケーションがオフラインの場合、フォームとそのデータは Outbox フォルダーに保存されます。

アプリケーションがオンラインの場合、タスクは AEM Forms Server と同期され、プロセスで指定されたユーザーに割り当てられます。

タスクリスト内のタスクを実行するには、「[タスクを開く](/help/forms/using/open-task.md)」を参照してください。
