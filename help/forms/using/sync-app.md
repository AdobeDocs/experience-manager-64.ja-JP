---
title: アプリケーションの同期
seo-title: Synchronizing the app
description: モバイルデバイス上のAEM FormsアプリをAEM Formsサーバーと同期します。
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
ht-degree: 23%

---

# アプリケーションの同期 {#synchronizing-the-app}

## アプリケーションの同期 {#synchronizing-the-app-1}

アプリケーション内のフォームが、AEM Formsサーバーからダウンロードされます。 フォームは、「タスク」タブと「Forms」タブにダウンロードされます。 フォームから作成されたドラフトは「ドラフト」タブにダウンロードされ、タスクから作成されたドラフトは「タスク」タブにダウンロードされます。 OSGi サーバー上のスタンドアロンフォームの場合、フォームとドラフトは、それぞれ「Forms」タブと「ドラフト」タブにダウンロードされます。

フォームを完了して送信すると、アプリがオンラインの場合、フォームはすぐにAEM Formsサーバーにアップロードされます。 アプリケーションが同期されると、フォームはサーバーから取得されます。 ただし、アプリケーションがオンラインの場合、ドラフトはただちにサーバーと同期されます。

AEM Formsサーバーがオンラインの場合、デフォルトでは、15 分ごとにアプリが同期されます。 ただし、同期頻度を変更するオプションがあります。 または、いつでも手動でアプリを同期できます。

**アプリを手動で同期するには**

ホーム画面の右下にある「同期」ボタン ![sync-app](assets/sync-app.png) をタップしてください。

**同期頻度を変更するには**

1. 設定画面に移動するには、ホーム画面の左上隅にあるメニューボタンをタップし、 **設定**.
1. 設定画面で、「一般」タブをタップします。

   ![一般設定ウィンドウの「同期の頻度」設定](assets/gen-settings-1.png)

1. 「同期の頻度」オプションで、「同期の頻度」の右にある値をタップします。
1. ドロップダウンリストで、新しい同期頻度を選択します。

### 技術仕様 {#technical-specifications}

* オフラインアプリデータをAEM Formsサーバーに送信する主なロジックは、 runtime/offline/util/offline.jsに含まれます。
* .js で、processOfflineSubmittedSavedTasks(...) 関数への呼び出しによって、保存済み／送信済みタスクをサーバーに送信します。同期処理でのエラーや競合も処理されます。タスクの送信に失敗すると、アプリケーションのタスクは失敗としてマークされます。さらに、タスクは Outbox に残ります。
* syncSubmittedTask() 関数と syncSavedTask() 関数は、個々のタスクに対して操作を実行します。
* ユーザーがサーバーとのオフライン状態の同期またはバックグラウンドスレッドによる自動同期を選択した後、タスクリストコンポーネントによって processOfflineSubmittedSavedTasks() 関数の呼び出しが開始されます。
