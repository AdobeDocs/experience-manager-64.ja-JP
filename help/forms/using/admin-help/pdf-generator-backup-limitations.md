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
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '55'
ht-degree: 14%

---

# PDF Generator バックアップの制限事項 {#pdf-generator-backup-limitations}

ファイルの変換にPDFジェネレーターが使用する一時ディレクトリはバックアップできません。 PDFジェネレーターは、設定された間隔で一時ディレクトリの内容を確認およびクリアするので、サービスが正しく復元されても、データが失われる可能性があります。
