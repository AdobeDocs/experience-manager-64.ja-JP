---
title: 一般設定の更新
seo-title: Updating general settings
description: ホーム画面などの AEM Forms アプリケーションの設定を更新し、Startpoints や添付ファイルのオプションを取得する
seo-description: Update AEM Forms app settings such as the Home screen and fetch Startpoints and attachments options
uuid: 234cd2da-2b47-4d60-82ed-68363d782632
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: forms-app
discoiquuid: a3aac07e-7d67-4a4f-b941-ff25a981092f
exl-id: 5ca6212f-d3c7-4239-beba-9a0bdac4b1ec
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '385'
ht-degree: 78%

---

# 一般設定の更新 {#updating-general-settings}

AEM Forms アプリの一般設定によって、添付ファイルの取得、オフラインモード、ランディング画面、デフォルトのカテゴリー、自動保存の頻度などの設定を行うことができます。

## アプリケーションの一般設定を更新する {#working-with-the-form}

アプリケーションを AEM Forms サーバーと同期すると、すべてのフォームと定義済みタスクがモバイルデバイス上にダウンロードされます。

標準搭載のAEM Formsアプリソリューションでは、アプリを同期する際に、各フォームに関連付けられた添付ファイルをダウンロードしません。

「一般」タブで、ダウンロードの添付ファイルや、オフラインモード、ランディング画面、自動保存、および同期設定変更します。この [ホーム画面](/help/forms/using/home-screen.md) 」と入力します。

**設定画面で、「一般」タブに移動します。**

1. 設定画面に移動するには、ホーム画面の左上角にあるメニューボタンをタップしてから、「**設定**」をタップします。
1. 設定画面で、「一般」タブをタップします。

   ![AEM Forms アプリケーションの一般設定](assets/gen-settings-2.png)

   >[!NOTE]
   >
   >このオプションは、モバイルデバイスごとに表示が異なる場合があります。

### 一般設定 {#general-settings}

アプリの設定では、次の項目を変更することができます。

* **タスク添付ファイルを取得**： 各タスクがアプリケーションにダウンロードされたときに、関連の添付ファイルをダウンロードするかどうかを指定します。

* **オフラインモード**： AEM Forms アプリケーションのオフラインサービスを有効または無効にします。詳細については、「[オフラインモードの使用](/help/forms/using/work-offline-mode.md)」を参照してください。

* **ランディング画面**： アプリケーションの開始場所（[ホーム画面](/help/forms/using/home-screen.md)）を設定します。

    選択可能なオプション：

   * Forms
   * タスク
   * お気に入り

* **デフォルトカテゴリ**： ホーム画面に表示するフォームのカテゴリを選択できます。「すべて」を選択すると、すべてのフォームがホーム画面に表示されます。カテゴリは、アプリケーションにロードされるフォームに基づいて自動入力されます。Formsは、AEM Formsサーバーで指定されたフォーム設定に基づいて、アプリで使用できます。

* **自動保存頻度**:頻度を設定するには、以下を実行します。 [モバイルアプリがフォームデータを保存](/help/forms/using/autosave-data-app.md) ローカルで使用できます。

* **同期頻度**:頻度を設定するには、以下を実行します。 [モバイルアプリが同期されました](/help/forms/using/sync-app.md) AEM Formsサーバーをオンラインモードで使用します。

**ローカルデータの消去**：デバイス上からデータベースを消去します。この中には、すべてのユーザやファイルストレージ用の設定とローカルデータが含まれます。 

>[!NOTE]
>
>キャッシュを消去すると、直後にアプリからログアウトされます。
>
>ただし、キャッシュ消去の操作を確認するプロンプトが表示されます。
