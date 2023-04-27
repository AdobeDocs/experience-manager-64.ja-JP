---
title: 秘密鍵証明書の使用に関する情報の確認
seo-title: Review credential use information
description: 秘密鍵証明書の使用情報を確認する方法を説明します。
seo-description: Learn how to review credential use information.
uuid: 02af75f9-c235-470d-a98b-a2102aa31381
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_acrobat_reader_dc_extensions
products: SG_EXPERIENCEMANAGER/6.4/FORMS
discoiquuid: cdf61cff-768b-49f7-9926-400bc96b0708
exl-id: abd62cca-edf0-4b44-94c3-7af3116b0c54
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 5%

---

# 秘密鍵証明書の使用に関する情報の確認 {#review-credential-use-information}

秘密鍵証明書には、Acrobat Reader DC Extensions エンドユーザー Web アプリケーションを通じてアクセスできる、使用目的を説明する情報が含まれています。 この情報を使用して、インストールされる秘密鍵証明書の種類（評価または実稼動）と有効期限を判断できます。

1. Web ブラウザーを開き、次の URL を入力します。

   http://localhost:*[ポート]*/ReaderExtensions ( *[ポート]* は、アプリケーションサーバーのポート番号です )

1. デフォルトのユーザー名とパスワードを使用してログインします。

   ユーザー名：administrator

   パスワード：password

   >[!NOTE]
   >
   >デフォルトのユーザー名とパスワードを使用してログインするには、管理者またはスーパーユーザーの権限が必要です。 他のユーザーがAcrobat Reader DC拡張機能にアクセスできるようにするには、ユーザー管理でユーザーアカウントを作成し、そのユーザーにAcrobat Reader DC拡張機能 Web アプリケーションの役割を付与します。

1. 「秘密鍵証明書を選択」リストから秘密鍵証明書のエイリアスを選択し、「有効期限」と「使用目的の通知」に記載されている情報を確認します。

>[!NOTE]
>
>秘密鍵証明書の有効期限は、管理コンソールの設定/Trust Store の管理/ローカル秘密鍵証明書ページの「有効期限」でも確認できます。
