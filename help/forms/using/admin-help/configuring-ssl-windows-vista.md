---
title: Windows Vista での SSL の設定
seo-title: Windows Vista での SSL の設定
description: Windows Vista での SSL の設定方法について説明します。
seo-description: Windows Vista での SSL の設定方法について説明します。
uuid: 20bfcefb-ec84-4c55-bceb-6af106d883d7
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_ssl
products: SG_EXPERIENCEMANAGER/6.4/FORMS
discoiquuid: 667645a0-53d0-4f9b-a0ba-cc7e366a23a1
translation-type: tm+mt
source-git-commit: d04e08e105bba2e6c92d93bcb58839f1b5307bd8
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 63%

---


# Windows Vista での SSL の設定 {#configuring-ssl-on-windows-vista}

Windows Vista™ で SSL を設定するには、認証時に RSA 鍵が設定された SSL 秘密鍵証明書が必要になります。Java keytool を使用して、証明書を作成できます。

>[!NOTE]
>
>Windows Vista は DSA 鍵には対応していません。

証明書およびキーストアの作成に必要なすべての情報を指定した 1 つのコマンドを使用することにより、keytool を実行できます。

**SSL 証明書の作成**

1. コマンドプロンプトで、*[JAVA HOME]*/binに移動し、次のコマンドを入力して証明書とキーストアを作成します。

   `keytool -genkey -keyalg RSA -dname "CN=`*ホスト* `, OU=`*NameGroup* `, O=`*NameCompany* `,L=`*NameCity City*****Name** StateCountry Code `, S=`** `, C=`*&quot;LC cert&quot;* `" -alias`** `-keypass` `*key*`** `-keystore`**_*Passwordstorestoname* `.keystore`

   >[!NOTE]
   >
   >*[JAVA_HOME]は、JDKがインストールされているディレクトリに置き換え、斜体のテキストは、環境に対応する値に置き換えます。*

1. パスワードとして`changeit`と入力します。 Java インストールではこれがデフォルトのパスワードですが、システム管理者によって変更されている場合があります。

