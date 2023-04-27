---
title: 証明書と秘密鍵証明書の管理の基本事項
seo-title: Basics of managing certificates and credentials
description: 証明書と資格情報の管理の基本について説明します。
seo-description: Learn about the basics of managing certificates and credentials.
uuid: f421e206-e7b5-416c-b9fb-974094f10a66
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_certificates_and_credentials
products: SG_EXPERIENCEMANAGER/6.4/FORMS
discoiquuid: 986d16fc-4c81-4785-b1f3-fe8bd7ff669e
exl-id: 4817d150-9bfe-4cb9-8f06-6ff4eaaa6f55
source-git-commit: e608249c3f95f44fdc14b100910fa11ffff5ee32
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 21%

---

# 証明書と秘密鍵証明書の管理の基本事項 {#basics-of-managing-certificates-and-credentials}

A *資格情報* には、ドキュメントの署名や識別に必要な秘密鍵情報が含まれます。 A *証明書* は、信頼用に設定する公開鍵情報です。 AEM forms では、いくつかの目的で証明書と秘密鍵証明書を使用します。

* Acrobat Reader DC Extensions では、秘密鍵証明書を使用して、PDF ドキュメントで Adobe Reader の使用権限を有効にします。( [Acrobat Reader DC Extensions で使用するための資格情報の設定](/help/forms/using/admin-help/configuring-credentials-acrobat-reader-dc.md#configuring-credentials-for-use-with-acrobat-reader-dc-extensions).)
* Acrobatで使用するRights Management情報を、信頼できる発行者からのみ表示するように設定できます。 ( [Rights Managementの表示設定](/help/forms/using/admin-help/configuring-client-server-options.md#configure-document-security-display-settings).) 証明書に共通名 (CN) が存在する必要があります。
* Signature サービスは証明書と資格情報にアクセスします。 Signature サービスについて詳しくは、 [サービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63).

**ペアキーの生成**

AEM forms では、Trust Store を使用して、証明書、秘密鍵証明書および証明書失効リスト (CRL) を保存および管理します。 また、独立したハードウェアセキュリティモジュール (HSM) デバイスを使用して、秘密鍵を保存することもできます。

AEM forms には、キーペアを生成するオプションはありません。 ただし、Java keytool などのツールを使用して生成し、AEM forms Trust Store に読み込むことができます。 Java keytool について詳しくは、次を参照してください。

[https://docs.oracle.com/javase/tutorial/security/toolsign/step3.html](https://docs.oracle.com/javase/tutorial/security/toolsign/step3.html)

[https://docs.oracle.com/cd/E19798-01/821-1841/gjrgy/index.html](https://docs.oracle.com/cd/E19798-01/821-1841/gjrgy/index.html)

[https://helpcenter.gsx.com/hc/en-us/articles/115015960428-How-to-Generate-a-Self-Signed-Certificate-and-Private-Key-using-OpenSSL](https://helpcenter.gsx.com/hc/en-us/articles/115015960428-How-to-Generate-a-Self-Signed-Certificate-and-Private-Key-using-OpenSSL)

次の署名タイプがサポートされ、AEM forms で読み込むことができます。

* XML 署名
* XMLTimeStampToken
* RFC 3161 TimeStampToken
* PKCS#7
* PKCS#1
* DSA 署名

**キーの紛失または破損の処理**

鍵が失われた、または鍵が侵害されたと思われる場合は、次の操作を行ってください。

1. 認証局に通知して、認証失効リストに問題が発生したキーを追加し、キーを失効させます。
1. 認証機関から新しいキーと証明書を取得します。
1. 問題が発生したキーを使用して署名したドキュメントに、新しいキーを使用して再び署名します。
