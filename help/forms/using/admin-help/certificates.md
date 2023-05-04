---
title: 証明書の管理
seo-title: Managing certificates
description: 証明書の読み込みと書き出し、信頼設定の編集方法を説明します。
seo-description: Learn how to import and export a certificate and edit its trust settings.
uuid: 46b1dbe5-517c-4294-bb52-cc6700a768e8
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_certificates_and_credentials
products: SG_EXPERIENCEMANAGER/6.4/FORMS
discoiquuid: 9fd531c0-5206-4be0-a450-13e0dc806068
exl-id: b8d4f35b-dc9c-4e0a-b855-f49275d4ac1f
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '677'
ht-degree: 52%

---

# 証明書の管理 {#managing-certificates}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

Trust Store の管理を使用すると、電子署名と証明書認証の検証のために、サーバーで信頼する証明書の読み込み、編集、削除を行うことができます。 任意の数の証明書を読み込み、書き出すことができます。 証明書が読み込まれたら、信頼設定と Trust Store の種類を編集できます。 Trust Store の種類を組み合わせる際は、次のオプションを考慮してください。

* **Trust for Certificate Authentication with CA：** CRL の検証では、「ID で信頼」も選択します。
* **Trust for Certificate Authentication with ICA：**「ID で信頼」だけを選択します。ICA は証明書認証では信頼しないでください。証明書認証用の ICA を信頼すると、ICA はパス構築用の CA になります。 ICA が証明書認証と ID の両方に対して信頼されている場合、ICA が CA になるので、CA ベンダー証明書は無視されます。
* **Trust for OCSP Server with HTTPs：** OCSP 応答側サーバーが HTTPS の場所に存在する場合は、「SSL 接続で信頼」も選択する必要があります。OCSP 応答側で CRL の検証を必要とする場合は、必ず「ID で信頼」も選択します。
* **Adobe Root：**「SSL Connections」または「OCSP Server」の Trust Store の種類は選択しないでください。Adobeルートは、SSL 接続と OCSP サーバーに対して信頼されていません。 Adobeは OCSP および SSL 証明書を発行しません。 Adobeルートはエイリアス name=&quot;ADOBEROOT&quot;で暗黙的に信頼されています。

X509v3 証明書のみがサポートされます。 この証明書の種類は、バイナリの DER エンコードファイル（.cer ファイル）または同じ DER エンコード済み証明書の Base64 エンコード済みバージョン (Privacy Enhanced Mail(PEM) 形式の X509 証明書を含む ) を含むテキストファイルで指定できます。

署名の検証を完了するために必要な証明書は、同じストア（HSM またはデータベース）に存在する必要があります。

また、Trust Manager API を使用して証明書の読み込みと削除を行うこともできます。 詳しくは、「Trust Manager API を使用した証明書の読み込み」および「Trust Manager API を使用した証明書の削除」を参照してください。 [AEM forms によるプログラミング](https://www.adobe.com/go/learn_aemforms_programming_63_jp).

## 証明書の読み込み {#import-a-certificate}

1. 管理コンソールで、**[!UICONTROL 設定／Trust Store の管理／証明書]**&#x200B;をクリックします。
1. 「インポート」をクリックし、「Trust Store の種類」で次のいずれかのオプションを選択します。

   * **SSL 接続で信頼：** SSL 経由で外部システムに接続するために AEM Forms で証明書を使用できることを指定します。
   * **署名の認証で信頼：**&#x200B;作成者のデジタル署名の認証のために、ドキュメントの署名処理で証明書を信頼することを指定します。
   * **署名で信頼：**&#x200B;作成者以外のデジタル署名について、ドキュメントの署名処理で証明書を信頼することを指定します。
   * **証明書認証で信頼：**&#x200B;証明書またはスマートカードによるユーザー認証を行うために、AEM Forms で証明書を使用することを指定します。
   * **OCSP サーバーで信頼：**&#x200B;外部の OCSP レスポンダーに接続するために AEM Forms で証明書を使用できることを指定します。
   * **ID で信頼：**&#x200B;上記の種類以外の情報を信頼するために証明書を使用できることを指定します。

   >[!NOTE]
   >
   >Trust Store は、証明書の認証、Adobe、署名、および ID に対して、署名ルート証明書を暗黙的に信頼します。

1. 「エイリアス」ボックスに、証明書の識別子を入力します。
1. 「**[!UICONTROL 参照]**」をクリックして証明書を探し、「**[!UICONTROL OK]**」をクリックします。

## 証明書のエクスポート {#export-a-certificate}

1. 管理コンソールで、**[!UICONTROL 設定／Trust Store の管理／証明書]**&#x200B;をクリックします。
1. エクスポートする証明書のエイリアス名をクリックします。**[!UICONTROL 証明書の詳細]**&#x200B;ページが表示されます。
1. 「**[!UICONTROL エクスポート]**」をクリックし、指示に従って証明書をエクスポートして、「**[!UICONTROL OK]**」をクリックします。

## 証明書の信頼設定と Trust Store の種類の編集 {#edit-a-certificate-s-trust-settings-and-trust-store-type}

1. 管理コンソールで、**[!UICONTROL 設定／Trust Store の管理／証明書]**&#x200B;をクリックします。
1. 編集する証明書のエイリアス名をクリックします。
1. 「**[!UICONTROL 証明書を更新]**」をクリックします。
1. 証明書のエイリアス名を変更するには、「エイリアス」ボックスに新しい名前を入力します。
1. 証明書の Trust Store の種類を更新するには、適切な Trust Store の種類を選択します。
1. ポリシーに関する制限を更新するには、「証明書のポリシー」ボックスにポリシー情報を入力し、「**[!UICONTROL OK]**」をクリックします。

## 証明書の削除 {#delete-a-certificate}

1. 管理コンソールで、**[!UICONTROL 設定／Trust Store の管理／証明書]**&#x200B;をクリックします。
1. 削除する証明書のチェックボックスを選択して「**[!UICONTROL 削除]**」をクリックし、「**[!UICONTROL OK]**」をクリックします。
