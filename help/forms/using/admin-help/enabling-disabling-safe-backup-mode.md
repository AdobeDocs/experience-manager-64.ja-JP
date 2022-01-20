---
title: セーフバックアップモードの有効化と無効化
seo-title: Enabling and disabling safe backup mode
description: バックアップ設定ページでは、AEM Forms をセーフバックアップモードで操作できるので、データベースとグローバルドキュメントストレージ（GDS）ディレクトリを確実にバックアップできます。セーフバックアップモードを有効化および無効化する方法について説明します。
seo-description: On the Backup Settings page, you can operate AEM forms in safe backup mode so that you can reliably back up your database and Global Document Storage (GDS) (GDS) directory. Learn how to enable and disable safe backup mode.
uuid: 2fdeaeaf-e969-40a4-8aee-1f2b627d3942
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.4/FORMS
discoiquuid: 9fda71e4-78a1-4581-9d02-bf06a75c3bcb
exl-id: 309a8cef-e84d-485b-9a7c-786a93e83c85
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 100%

---

# セーフバックアップモードの有効化と無効化 {#enabling-and-disabling-safe-backup-mode}

バックアップ設定ページでは、AEM Forms をセーフバックアップモードで操作できるので、データベースとグローバルドキュメントストレージ（GDS）ディレクトリを確実にバックアップできます。

セーフバックアップモードになっている場合でも、AEM Forms は正常に稼働します。ただし、ファイルは GDS ディレクトリから削除されません。

>[!NOTE]
>
>このオプションを設定しても、システムのバックアップは実行されません。このオプションでは、バックアップを行うようにシステムが準備されます。

## セーフバックアップモードの有効化 {#enable-safe-backup-mode}

1. 管理コンソールで、設定／コアシステム設定／バックアップ設定をクリックします。
1. バックアップ設定ページで、「セーフバックアップモードで稼動する」を選択して「OK」をクリックします。

>[!NOTE]
>
>システムが既にセーフバックアップモードで稼動している場合は、「OK」をクリックしても新しい予約は作成されません。

## セーフバックアップモードの無効化 {#disable-safe-backup-mode}

1. 管理コンソールで、設定／コアシステム設定／バックアップ設定をクリックします。
1. バックアップ設定ページで、「セーフバックアップモードで稼動する」の選択を解除して「OK」をクリックします。
