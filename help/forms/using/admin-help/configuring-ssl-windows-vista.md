---
title: Windows Vista での SSL の設定
seo-title: Configuring SSL on Windows Vista
description: Windows Vista で SSL を設定する方法を説明します。
seo-description: Learn how to configure SSL on Windows Vista.
uuid: 20bfcefb-ec84-4c55-bceb-6af106d883d7
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_ssl
products: SG_EXPERIENCEMANAGER/6.4/FORMS
discoiquuid: 667645a0-53d0-4f9b-a0ba-cc7e366a23a1
exl-id: 8eee2ed2-8263-47f2-b928-214fd9ab5f6e
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 20%

---

# Windows Vista での SSL の設定 {#configuring-ssl-on-windows-vista}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

Windows Vista™で SSL を設定するには、認証用に RSA キーを持つ SSL 証明書が必要です。 Java keytool を使用して証明書を作成できます。

>[!NOTE]
>
>Windows Vista は、DSA キーでは機能しません。

証明書とキーストアの作成に必要なすべての情報を含む 1 つのコマンドを使用して、keytool を実行できます。

**SSL 証明書の作成**

1. コマンドプロンプトで、に移動します。 *[JAVA ホーム]*/bin と次のコマンドを入力して、証明書とキーストアを作成します。

   `keytool -genkey -keyalg RSA -dname "CN=`*ホスト名* `, OU=`*グループ名* `, O=`*会社名* `,L=`*市区町村******名前* `, S=`*都道府県* `, C=`*国コード* `" -alias`*&quot;LC Cert&quot;* `-keypass` `*key*`*_**パスワード* `-keystore`*keystorename* `.keystore`

   >[!NOTE]
   >
   >置換 *[JAVA_HOME] を JDK がインストールされているディレクトリに置き換え、斜体のテキストを環境に対応する値に置き換えます。*

1. パスワードに `changeit` と入力します。Java インストールではこれがデフォルトのパスワードですが、システム管理者によって変更されている場合があります。
