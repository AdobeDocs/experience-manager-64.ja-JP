---
title: PDFG ネットワークプリンターの設定（Windows のみ）
seo-title: Setting up a PDFG Network Printer (Windows only)
description: PDFG ネットワークプリンターの設定方法を説明します（ Windows のみ）
seo-description: Learn how to set up a PDFG Network Printer ( Windows only )
uuid: 13b8481e-5ef0-4a07-9602-7bc4d9e05dd4
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.4/FORMS
discoiquuid: 7620e5e4-022e-49b2-8cfe-d5eec8ab99d7
feature: PDF Generator
exl-id: 0b7642c3-d616-44e8-a5d9-3cdd362fedb5
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '644'
ht-degree: 14%

---

# PDFG ネットワークプリンターの設定（Windows のみ） {#setting-up-a-pdfg-network-printer-windows-only}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

PDFG ネットワークプリンターを使用すると、印刷をサポートする任意のPDFからアプリケーションドキュメントを生成できます。 PDFG ネットワークプリンターをインストールすると、*PDF Generator* という名前の新しいプリンターが Windows コントロールパネルの「プリンター」セクションに表示されます。同じ名前のプリンタが既に存在する場合は、別の名前を指定するように求められます。

任意のアプリケーションからこのプリンターに印刷すると、ドキュメントが（PostScript 形式で）PDFジェネレーターに送信され、PostScript ファイルがPDFに変換されます。 PDFジェネレーターの設定に応じて、PDFドキュメントが電子メールメッセージへの添付ファイルとしてユーザーに送信されるか、PDFドキュメントが指定のAEM forms サービスまたはプロセスに転送されるか、両方のアクションが実行されます。

PDFG ネットワークプリンターを設定するには、次の手順を実行する必要があります。

1. 電子メールを設定します。 ( [PDFG ネットワークプリンターの電子メール設定の指定](setting-pdfg-network-printer-windows.md#configure-email-settings-for-pdfg-network-printer).)
1. 管理コンソールで、PDFG ネットワークプリンターの設定を指定します。 ( [PDFG ネットワークプリンターの設定](setting-pdfg-network-printer-windows.md#configure-the-pdfg-network-printer-settings).)
1. ユーザーがAEM forms データベース内の有効な電子メールアドレスを使用して設定され、各ユーザーに PDFGUserPermission を割り当てていることを確認します。 <!-- Fix broken link See Setting up and organizing users -->
1. 32 ビット JRE6 がユーザーのコンピュータにインストールされていることを確認します。
1. ユーザーのコンピュータにプリンタをインストールします。 ( [ユーザーのコンピューターに PDFG ネットワークプリンターをインストールする](setting-pdfg-network-printer-windows.md#install-pdfg-network-printer-on-a-user-s-computer).)

## PDFG ネットワークプリンターの電子メール設定の指定 {#configure-email-settings-for-pdfg-network-printer}

1. 管理コンソールで、サービス／アプリケーションおよびサービス／サービスの管理をクリックします。
1. 「サービスの管理」ページで、provider.email_sendmail_service をクリックし、SMTP 設定を指定して、「保存」をクリックします。

## PDFG ネットワークプリンターの設定 {#configure-the-pdfg-network-printer-settings}

1. 管理コンソールで、サービス/Network Generator/PDFG Network Printer をクリックします。
1. 「 Adobe PDF設定」リストと「セキュリティ設定」リストで、生成される設定に適用するオプションをPDFします。 これらの設定の詳細については、 [Adobe PDF設定](/help/forms/using/admin-help/configuring-pdf-settings.md#configuring-adobe-pdf-settings) および [セキュリティ設定の指定](/help/forms/using/admin-help/configuring-security-settings.md#configuring-security-settings).
1. 変換後のPDFを再度ユーザーに送信するには、「変換後のPDFファイルを電子メールでユーザーに返す」オプションを選択し、次の情報を指定します。

   * ユーザーにPDFを送信する際に使用する電子メールアドレス
   * 電子メールメッセージの件名
   * 電子メールメッセージのヘッダー、本文およびフッター。 電子メールメッセージで、 &lt;receivername> は、ドキュメントを印刷したユーザーのフルネームに置き換えられます。

1. 変換後のPDFをAEM forms サービスまたはプロセスに送信するには、「Forward The Converted The ConvertedPDFTo The Specified AEM forms Service Or Process」オプションを選択し、以下の情報を指定します。

   * 呼び出すサービスの名前
   * 呼び出すサービスの操作の名前
   * サービスまたはプロセスの component.xml ファイルで指定された、入力パラメーターの名前。 PDFドキュメントは、その入力パラメーターの値として使用されます。

1. 「保存」をクリックします。

元のデフォルトの電子メールテキストに戻す場合は、[ 電子メールの内容を復元する ] をクリックします。

## ユーザーのコンピューターに PDFG ネットワークプリンターをインストールする {#install-pdfg-network-printer-on-a-user-s-computer}

「PDFG 管理者」または「PDFG ユーザー」の役割を持つユーザーは、PDFG ネットワークプリンターをインストールできます。 コンピューターに 32 ビット JDK がインストールされている必要があります。

1. （PDFG 管理者）管理コンソールで、サービス/ネットワークジェネレーター/PDFGPDFプリンターをクリックします。

   （PDFG ユーザーの場合）`http(s)://[host]:[port]/pdfgui` にアクセスし、「PDFG ネットワークプリンターのインストール」にあるリンクをクリックします。

1. 「PDFG ネットワークプリンターのインストール」で、リンクをクリックします。 ユーザーアカウント情報の入力を求められたら、手順 1 で使用したユーザー名とパスワードを指定してログインします。 プリンタが正常にインストールされたことを示すメッセージが表示されます。

   ***注意&#x200B;**：ユーザーのパスワードを変更する場合、ユーザーは PDFG ネットワークプリンターをコンピューターに再インストールする必要があります。管理コンソールからパスワードを更新することはできません。*

1. 「OK」をクリックします。
