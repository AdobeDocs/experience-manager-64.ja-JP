---
title: ローカル秘密鍵証明書の管理
seo-title: Managing local credentials
description: ローカル秘密鍵証明書の管理方法を説明します。
seo-description: Learn how to manage local credentials.
uuid: 3c4358e0-aaff-4e94-a6b2-04b463fca260
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_certificates_and_credentials
products: SG_EXPERIENCEMANAGER/6.4/FORMS
discoiquuid: 598a9a03-3773-4620-8867-1f754d8ca031
exl-id: f8c6f4e3-4c2d-4843-8f29-6d3297e57c89
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '537'
ht-degree: 21%

---

# ローカル秘密鍵証明書の管理 {#managing-local-credentials}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

ローカル秘密鍵証明書は、Trust Store 管理でホストされる秘密鍵資格情報です。 A *ローカル秘密鍵証明書* は、ユーザーの DES 秘密鍵証明書が保存される場所を示します。 Trust Store の管理では、既存の PFX ファイルなどを使用してローカル秘密鍵証明書の読み込みと管理を行い、ローカル秘密鍵証明書の読み込み、編集、削除を行うことができます。

AEM forms は、標準の PKCS12 形式（.pfx および.p12 ファイル）の最大 4096 ビットの RSA および DSA 秘密鍵証明書をサポートします。

任意の数の資格情報を読み込み、書き出しできます。 同じエイリアスを使用して期限切れの秘密鍵証明書を置き換える場合は、秘密鍵証明書を削除し、同じエイリアスで新しい秘密鍵証明書を読み込みます。

Acrobat Reader DC拡張機能に関する情報と手順については、 [Acrobat Reader DC Extensions で使用するための資格情報の設定](/help/forms/using/admin-help/configuring-credentials-acrobat-reader-dc.md#configuring-credentials-for-use-with-acrobat-reader-dc-extensions).

## 秘密鍵証明書の読み込み {#import-a-credential}

1. 管理コンソールで、設定／Trust Store の管理／ローカル秘密鍵証明書をクリックします。
1. 「読み込み」をクリックします。「Trust Store の種類」で、次のいずれかのオプションを選択します。

   * **ドキュメント署名証明書：**&#x200B;ドキュメントの電子署名の発行に使用する秘密鍵証明書です。
   * **Acrobat Reader DC Extensions 証明書：** Acrobat Reader DC Extensions に固有の電子証明書です。これにより、生成された PDF ドキュメントで Adobe Reader の使用権限をアクティブにすることができます。
   * **デフォルト：** Acrobat Reader DC Extensions で使用するデフォルトの証明書であることを示します。

   秘密鍵証明書の取得について詳しくは、 [AEM forms のインストールの準備](https://www.adobe.com/go/learn_aemforms_prepareInstallsingle_63_jp).

1. 「エイリアス」ボックスに、秘密鍵証明書の識別子を入力します。 この識別子は、Acrobat Reader DC Extensions と Signature サービスで、秘密鍵証明書の表示名として使用されます。 このエイリアスは、AEM forms SDK を使用してプログラムで秘密鍵証明書にアクセスする場合にも使用されます。

   >[!NOTE]
   >
   >エイリアス名は、表示用に自動的に大文字に変換されます。 エイリアス名をプロセスで参照する際、大文字と小文字は区別されません。

1. 「参照」をクリックして秘密鍵証明書を探し、秘密鍵証明書のパスワードを入力して、「OK」をクリックします。

   「ファイル形式が正しくないか、パスワードが正しくないため、秘密鍵証明書を読み込めませんでした」というエラーメッセージが表示される場合は、パスワードが有効であることを確認します。

## 秘密鍵証明書の書き出し {#export-a-credential}

秘密鍵証明書は、PKCS#12 形式で P12 ファイルとして書き出されます。

1. 管理コンソールで、設定／Trust Store の管理／ローカル秘密鍵証明書をクリックします。
1. 書き出す秘密鍵証明書のエイリアス名をクリックし、「書き出し」をクリックします。
1. 「パスワード」ボックスに、パスワードを入力します。 このパスワードは新規で、書き出した秘密鍵証明書の暗号化に使用されます。
1. 「書き出し」をクリックし、指示に従って秘密鍵証明書を書き出し、「OK」をクリックします。

## 秘密鍵証明書のエイリアスまたは Trust Store の種類の編集 {#edit-a-credential-s-alias-or-trust-store-type}

秘密鍵証明書が読み込まれたら、そのエイリアス名と Trust Store の種類を編集できます。

1. 管理コンソールで、設定／Trust Store の管理／ローカル秘密鍵証明書をクリックします。
1. 編集する秘密鍵証明書のエイリアス名をクリックします。
1. 「秘密鍵証明書を更新」をクリックします。
1. 必要に応じてエイリアス名と Trust Store の種類を編集し、「OK」をクリックします。

## 秘密鍵証明書の削除 {#delete-a-credential}

1. 管理コンソールで、設定／Trust Store の管理／ローカル秘密鍵証明書をクリックします。
1. 削除する秘密鍵証明書のチェックボックスを選択します。
1. 「削除」をクリックし、「OK」をクリックします。
