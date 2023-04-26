---
title: SSL 対応の LDAP サーバーを対象とした User Management の設定
seo-title: Configure User Management for an SSL-enabled LDAP server
description: SSL 対応の LDAP サーバーを対象として User Management を設定し、同期を有効にして LDAPS 経由で正しく動作させる方法について説明します。
seo-description: Learn how  to configure User Management for an SSL-enabled LDAP server to enable synchronization to work properly over LDAPS.
uuid: 4b3f8ac7-fa38-4adf-a851-82d55fe431fe
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.4/FORMS
discoiquuid: e6e7e2fa-579d-4b36-8598-6ced469a94b1
exl-id: 9ed22c75-bce7-4d26-a4cd-a58e41e5068e
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 30%

---

# SSL 対応の LDAP サーバーを対象とした User Management の設定 {#configure-user-management-for-an-ssl-enabled-ldap-server}

同期が LDAPS 経由で正しく機能するには、認証局 (CA) が発行した LDAP 証明書がアプリケーションサーバーの Java ランタイム環境 (JRE) に存在する必要があります。 証明書をアプリケーションサーバーの JRE cacerts ファイルに読み込みます。通常、このファイルは *[JAVA_HOME]*/jre/lib/security/cacerts ディレクトリにあります。

1. ディレクトリサーバーで SSL を有効にします。 詳しくは、ディレクトリのベンダーが提供するドキュメントを参照してください。
1. ディレクトリサーバーからクライアント証明書を書き出します。
1. keytool プログラムを使用して、クライアント証明書ファイルをAEM forms アプリケーションサーバーのデフォルトの Java 仮想マシン (JVM™) 証明書ストアに読み込みます。 このタスクの手順は、JVM とクライアントのインストールパスによって異なります。 例えば、BEA WebLogic Server と JDK 1.5 を使用する場合は、コマンドプロンプトで次のテキストを入力します。

   `keytool -import -alias`*alias* `-file certificatename -keystore C:\bea\jdk15_04\jre\lib\security\cacerts`

1. プロンプトが表示されたら、パスワードを入力します（Java では、デフォルトのパスワードは `changeit` です）。証明書が正常に読み込まれたことを示すメッセージが表示されます。
1. プロンプトが表示されたら、`Yes` と入力して証明書を信頼します。
1. User Management で SSL を有効にし、ディレクトリ設定を構成する際に、SSL オプションで「はい」を選択し、それに応じてポート設定を変更します。 デフォルトのポート番号は 636 です。

>[!NOTE]
>
>SSL の使用に問題が発生した場合は、LDAP ブラウザを使用して、SSL の使用時に LDAP システムにアクセスできるかどうかを確認します。 LDAP ブラウザーがアクセスできない場合は、証明書またはアプリケーションサーバーが正しく設定されていません。 LDAP ブラウザが正しく動作し、まだ問題が発生している場合は、User Management が正しく設定されていません。
