---
title: インストール時の admin パスワードの設定
seo-title: Configure the Admin Password on Installation
description: AEMのインストール時に管理者パスワードを変更する方法を説明します。
seo-description: Learn how to change the Admin Password on AEM Installation.
uuid: 06da9890-ed63-4fb6-88d5-fd0e16bc4ceb
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: Security
content-type: reference
discoiquuid: 00806e6e-3578-4caa-bafa-064f200a871f
exl-id: 6dd289ee-13fd-46be-82cd-aa69852397c9
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '342'
ht-degree: 24%

---

# インストール時の admin パスワードの設定{#configure-the-admin-password-on-installation}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

## 概要 {#overview}

バージョン 6.3 以降では、AEMを使用すると、新しいインスタンスをインストールする際にコマンドラインを使用して管理者パスワードを設定できます。

以前のバージョンのAEMでは、管理者アカウントのパスワードと他の様々なコンソールのパスワードをインストール後に変更する必要がありました。

この機能により、AEMインスタンスのインストール中にリポジトリとサーブレットエンジンの新しい管理者パスワードを設定できる機能が追加され、後で手動で設定する必要がなくなります。

>[!CAUTION]
>
>この機能では、Felix コンソールは対象外で、パスワードを手動で変更する必要があります。 詳しくは、 [セキュリティチェックリストセクション](/help/sites-administering/security-checklist.md#change-default-passwords-for-the-aem-and-osgi-console-admin-accounts).

## 使用方法 {#how-do-i-use-it}

この機能は、ファイルシステムエクスプローラーから JAR をダブルクリックするのではなく、コマンドラインを使用してAEMをインストールする場合に自動的にトリガーされます。

コマンドラインからAEMインスタンスを実行するための一般的な構文は次のとおりです。

```shell
java -jar aem6.3.jar
```

コマンドラインからインスタンスを実行すると、インストールプロセス中に admin パスワードを変更するオプションが表示されます。

![chlimage_1-116](assets/chlimage_1-116.png)

>[!NOTE]
>
>管理者パスワードの変更を求めるプロンプトは、新しいAEMインスタンスのインストール時にのみ表示されます。

## -nointeractive フラグの使用 {#using-the-nointeractive-flag}

プロパティファイルからパスワードを指定することもできます。 これは、 `-nointeractive` ～と組み合わされた旗 `-Dadmin.password.file` システムプロパティ。

次に例を示します。

```shell
java -Dadmin.password.file =/path/to/passwordfile.properties -jar aem6.3.jar -nointeractive
```

`passwordfile.properties` ファイル内のパスワードの書式は次のようにする必要があります。

```xml
admin.password = 12345678
```

>[!NOTE]
>
>`-Dadmin.password.file` システムプロパティを使用せずに `-nointeractive` パラメーターだけを使用した場合は、AEM ではデフォルトの管理者パスワードが使用され、変更を求めるメッセージは表示されません（基本的に以前のバージョンの動作と同じになります）。インストールスクリプトのコマンドラインでこの非インタラクティブモードを使用して、インストールを自動化できます。
