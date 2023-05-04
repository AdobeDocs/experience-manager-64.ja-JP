---
title: 証明書失効リストの管理
seo-title: Managing certificate revocationlists
description: 証明書失効リストの管理方法を説明します。
seo-description: Learn how to manage certificate revocation lists.
uuid: d8c4b64c-a273-4f5d-8b71-f6ea455c0f0a
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_certificates_and_credentials
products: SG_EXPERIENCEMANAGER/6.4/FORMS
discoiquuid: 9744cc2d-5e6b-4341-9270-43d479bdca04
exl-id: 45741270-2d57-4d6d-92ef-65b6c1deb448
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 5%

---

# 証明書失効リストの管理{#managing-certificate-revocationlists}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

Trust Store の管理を使用して、証明書失効リスト (CRL) の読み込み、編集および削除を行うことができます。 Base64 および DER でエンコードされた証明書失効リストがサポートされています。

## CRL の読み込み {#import-a-crl}

1. 管理コンソールで、設定/Trust Store の管理/証明書失効リストをクリックし、「読み込み」をクリックします。
1. 「エイリアス」ボックスに、CRL の識別子を入力します。
1. 「参照」をクリックして CRL を探し、「OK」をクリックします。

## CRL の書き出し {#export-a-crl}

1. 管理コンソールで、設定/Trust Store の管理/証明書失効リストをクリックします。
1. 書き出す CRL のエイリアス名をクリックし、「書き出し」をクリックします。
1. 指示に従って CRL を書き出します。 CRL は Base64 エンコーディングで書き出されます。
1. 「OK」をクリックします。

## CRL の削除 {#delete-a-crl}

1. 管理コンソールで、設定/Trust Store の管理/証明書失効リストをクリックします。
1. 削除する CRL のチェックボックスをオンにし、「削除」をクリックして、「OK」をクリックします。
