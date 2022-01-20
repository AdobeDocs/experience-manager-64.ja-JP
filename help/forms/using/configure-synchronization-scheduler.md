---
title: 同期スケジューラの設定
seo-title: Configuring the synchronization scheduler
description: アセットを移行し同期する方法や、同期スケジューラーの設定、およびフォルダーを使用してアセットを整理する方法を学びます。
seo-description: Learn how to migrate and sync assets, configure sync scheduler, and use folders to arrange assets.
uuid: a6445b45-9c1c-4483-a32e-453648c488c5
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: Configuration
discoiquuid: 2c8cea3c-8d8b-41d4-8ef9-a0ada8f86be6
role: Admin
exl-id: 7f1c4bac-accf-43e4-9439-89c5420d50f2
source-git-commit: 3c050c33a384d586d74bd641f7622989dc1d6b22
workflow-type: tm+mt
source-wordcount: '286'
ht-degree: 77%

---

# 同期スケジューラの設定 {#configuring-the-synchronization-scheduler}

デフォルトでは、同期スケジューラーは 3 分毎に実行して、LiveCycle Workbench 11 を経由してリポジトリ内で変更および更新されたすべてのアセットを同期します。同期プロセスが完了すると、フォームおよびリソースを含むアプリケーションを AEM Forms ユーザーインターフェイスで表示することができます。

## 同期スケジューラーの間隔の変更 {#change-interval-of-the-synchronization-scheduler}

次の手順を実行して、同期スケジューラーの間隔を変更します。

1. AEM Configuration Manager にログインします。Configuration Manager の URL は次のとおりです。 `https://[Server]:[Port]/lc/system/console/configMgr`

1. **FormsManagerConfiguration** バンドルを探して開きます。 

1. 「**同期スケジューラー頻度**」オプションに対して新しい値を指定します。

   頻度の単位は分です。例えば、スケジューラーを 60 分毎に実行するように設定するには、60 と指定します。

## アセットの同期 {#synchronizing-assets}

「**リポジトリからアセットを同期**」オプションを使用すると、アセットを手動で同期できます。次の手順を実行して、アセットを手動で同期します。

1. AEM Forms にログインします。デフォルトの URL は `https://[Server]:[Port]/lc/aem/forms/` です。

   ![AEM Forms ユーザーインターフェイス](assets/aem_forms_ui.png)

   **図：** *AEM Formsユーザーインターフェイス*

1. 次をクリック： ![aem6forms_sync](assets/aem6forms_sync.png) アイコンをクリックします。 最後に設定したパスにアセットが存在しない場合は、下の図に示すダイアログボックスが表示されます。「**開始**」をクリックして同期を開始します。

   ![同期ダイアログボックス](assets/migrate-and-syncronize.png)

   **図：** *同期ダイアログボックス*

## 同期エラーのトラブルシューティング {#troubleshooting-synchronization-error}

ワークフローデザイナー（LiveCycle Workbench）で新しいアプリケーションを作成できます。

新しく作成したアプリケーションと/content/dam/formsanddocuments のフォルダーの名前が同じ場合は、エラー「*このアプリケーションと同じ名前のアセットがルートレベルで既に存在します。*」がログに記録されます。

競合を解決するには、アプリケーションの名前を変更し、アセットを手動で同期します。

![アセット同期の競合ダイアログボックス](assets/sync-conflict.png)

**図：** *アセット同期の競合ダイアログボックス*
