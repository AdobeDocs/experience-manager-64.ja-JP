---
title: PDF Generator バックアップの制限事項
seo-title: PDF Generator backup limitations
description: Generator のバックアップの制限について説明します。
seo-description: Learn about PDF Generator backup limitations.
uuid: 9537ffde-4396-46d1-81ea-edcd25923ffb
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.4/FORMS
discoiquuid: 23386353-b2bf-49f1-947a-dd7587bba175
noindex: true
exl-id: d2ba9881-02b6-470b-b110-7d4609e6ab24
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '91'
ht-degree: 17%

---

# PDF Generator バックアップの制限事項 {#pdf-generator-backup-limitations}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

ファイルの変換にPDFジェネレーターが使用する一時ディレクトリはバックアップできません。 PDFジェネレーターは、設定された間隔で一時ディレクトリの内容を確認およびクリアするので、サービスが正しく復元されても、データが失われる可能性があります。
