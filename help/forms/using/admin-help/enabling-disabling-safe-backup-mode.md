---
title: セーフバックアップモードの有効化と無効化
seo-title: Enabling and disabling safe backup mode
description: バックアップ設定ページでは、AEM forms をセーフバックアップモードで操作して、データベースとグローバルドキュメントストレージ (GDS) ディレクトリを確実にバックアップできます。 セーフバックアップモードを有効または無効にする方法を説明します。
seo-description: On the Backup Settings page, you can operate AEM forms in safe backup mode so that you can reliably back up your database and Global Document Storage (GDS) (GDS) directory. Learn how to enable and disable safe backup mode.
uuid: 2fdeaeaf-e969-40a4-8aee-1f2b627d3942
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.4/FORMS
discoiquuid: 9fda71e4-78a1-4581-9d02-bf06a75c3bcb
exl-id: 309a8cef-e84d-485b-9a7c-786a93e83c85
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 8%

---

# セーフバックアップモードの有効化と無効化 {#enabling-and-disabling-safe-backup-mode}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

バックアップ設定ページでは、AEM forms をセーフバックアップモードで操作して、データベースとグローバルドキュメントストレージ (GDS) ディレクトリを確実にバックアップできます。

AEM forms はセーフバックアップモードのときは、GDS ディレクトリからファイルをアクティブに削除しない点を除き、正常に動作します。

>[!NOTE]
>
>このオプションを設定しても、システムはバックアップされません。システムのバックアップを準備します。

## セーフバックアップモードを有効にする {#enable-safe-backup-mode}

1. 管理コンソールで、設定/コアシステム設定/バックアップ設定をクリックします。
1. [ バックアップ設定 ] ページで、[ セーフバックアップモードで動作 ] を選択し、[OK] をクリックします。

>[!NOTE]
>
>システムが既にセーフバックアップモードで実行されている場合、[OK] をクリックしても新しい予約は作成されません。

## セーフバックアップモードを無効にする {#disable-safe-backup-mode}

1. 管理コンソールで、設定/コアシステム設定/バックアップ設定をクリックします。
1. [ バックアップ設定 ] ページで、[ セーフバックアップモードで動作する ] の選択を解除し、[OK] をクリックします。
