---
title: アプリケーションの同期
seo-title: Synchronizing the app
description: モバイルデバイス上の AEM Forms アプリケーションを AEM Forms サーバーと同期します。
seo-description: Synchronize the AEM Forms app on your mobile device with the AEM Forms server.
uuid: 7e1526e1-13bd-498a-a265-cd4f2d05ccdd
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: forms-app
discoiquuid: dae1ce32-702e-4cf0-b3c6-976551208d09
exl-id: b5681fe5-69ba-4fc0-95e3-6ffdcdd95382
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '369'
ht-degree: 96%

---

# アプリケーションの同期 {#synchronizing-the-app}

## アプリケーションの同期 {#synchronizing-the-app-1}

アプリケーション内のフォームが AEM Forms サーバーからダウンロードされます。フォームは、「タスク」タブと「フォーム」タブにダウンロードされます。フォームから作成されたドラフトは「ドラフト」タブにダウンロードされ、タスクから作成されたドラフトは「タスク」タブにダウンロードされます。OSGi サーバー上のスタンドアロンフォームの場合、フォームとドラフトは、「フォーム」タブと「ドラフト」タブにそれぞれダウンロードされます。

アプリケーションがオンラインの場合、フォームを完了し送信すると、そのフォームはすぐに AEM Forms サーバーにアップロードされます。アプリケーションが同期されると、そのフォームはサーバーから取得されます。ただし、アプリケーションがオンラインの場合、ドラフトはただちにサーバーと同期されます。

AEM Forms サーバーがオンラインのときは、デフォルトでは、15 分間隔でアプリケーションが同期されます。ただし、この同期頻度を変更するオプションがあります。あるいは、任意の時点でアプリケーションを手動で同期することもできます。

**アプリケーションを手動で同期するには**

「同期」ボタンをタップします。 ![sync-app](assets/sync-app.png) ホーム画面の右下隅に

**同期頻度を変更するには**

1. 設定画面に移行するには、ホーム画面の左上角にあるメニューボタンをタップしてから、「**設定**」をタップします。
1. 設定画面で、「一般」タブをタップします。

   ![一般設定ウィンドウの「同期の頻度」設定](assets/gen-settings-1.png)

1. 「同期の頻度」オプションで、「同期の頻度」の右側の値をタップします。
1. ドロップダウンリストで、新しい同期頻度を選択します。

### 技術仕様 {#technical-specifications}

* AEM Forms サーバーへのオフラインアプリケーションデータの送信のメインロジックは runtime/offline/util/offline.js に含まれます。
* .js で、processOfflineSubmittedSavedTasks(...) 関数への呼び出しによって、保存済み／送信済みタスクをサーバーに送信します。 同期処理でのエラーや競合も処理されます。 タスクの送信に失敗すると、アプリケーションのタスクは失敗としてマークされます。 さらに、タスクは Outbox に残ります。
* syncSubmittedTask() および syncSavedTask() 関数は、個別のタスクに操作を実行します。
* ユーザーがサーバーへのオフライン状態の同期またはバックグラウンドスレッドによる自動同期を選択した後、タスクリストコンポーネントによって、processOfflineSubmittedSavedTasks() 関数への呼び出しが開始されます。
