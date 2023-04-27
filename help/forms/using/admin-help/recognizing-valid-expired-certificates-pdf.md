---
title: PDF ドキュメントでの有効な証明書と期限切れ証明書の認識
seo-title: Recognizing valid and expired certificates in PDF documents
description: 証明書ドキュメントで有効な証明書と期限切れの証明書を認識するPDFを説明します。
seo-description: Learn how to recognize valid and expired certificates in PDF documents.
uuid: ceeff57a-586f-4f7b-852f-2a637f003d7e
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_acrobat_reader_dc_extensions
products: SG_EXPERIENCEMANAGER/6.4/FORMS
discoiquuid: 4559218a-65ba-4577-ad26-7721e28971bc
exl-id: 6e2c109c-381f-455d-bd1d-b08c37c0bd67
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '198'
ht-degree: 8%

---

# PDF ドキュメントでの有効な証明書と期限切れ証明書の認識 {#recognizing-valid-and-expired-certificates-in-pdf-documents}

Reader拡張機能によって使用権限が適用されたPDFドキュメントがAdobe Readerで開かれると、ステータスバーが表示され、PDFドキュメントで有効になっている特定の使用権限が示されます。

PDFドキュメントの使用権限を指定した電子証明書の有効期限が切れ、PDFドキュメントがAdobe Readerで開くと、PDFドキュメントに使用権限があるが、それらの権限は無効であることをユーザーに通知するダイアログボックスが表示されます。 メッセージは、PDFドキュメントが変更または改ざんされたことを示しますが、必ずしもそうではありません。 Adobe Readerは、証明書の有効期限が切れたり、ドキュメントが変更されたりすると、このメッセージを表示します。 Adobe Reader 7.0.x 以降では、現在問題が発生しているケースを特定できません。

ダイアログボックスを閉じると、Adobe ReaderがPDFドキュメントを開きます。 Acrobat Reader DC拡張機能を使用して適用された使用権限は、期待どおりに使用できません。 PDFドキュメントがインタラクティブフォームの場合、フォームフィールドはロックされ、ユーザーはフォームデータを変更できません。
