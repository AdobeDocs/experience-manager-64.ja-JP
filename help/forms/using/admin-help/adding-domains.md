---
title: ドメインの追加
seo-title: Adding domains
description: ドメインの管理設定を使用してエンタープライズドメイン、ローカルドメインまたはハイブリッドドメインを追加する方法と、ドメイン名および ID に関する一般的な考慮事項について説明します。
seo-description: Learn how to add an enterprise, local, or hybrid domain using Domain Management settings and general considerations for domain names and IDs.
uuid: 3ae1e5d4-ea5b-4e0b-be97-3957c3702d5f
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_managing_domains
products: SG_EXPERIENCEMANAGER/6.4/FORMS
discoiquuid: d4004ffe-c981-487d-b803-dc4492ae5998
exl-id: f2bafa0c-072c-4599-92bc-4eaafece5b4f
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '958'
ht-degree: 9%

---

# ドメインの追加 {#adding-domains}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

## エンタープライズドメインの追加 {#add-an-enterprise-domain}

1. 管理コンソールで、設定／User Management／ドメインの管理をクリックします。
1. 「新規エンタープライズドメイン」をクリックします。
1. 「 ID 」ボックスにドメインの一意の ID を入力し、「名前」ボックスにドメインのわかりやすい名前を入力します。 ( [ドメイン名と ID に関する重要な考慮事項](adding-domains.md#important-considerations-for-domain-names-and-ids).)
1. アカウントのロックを有効にするかどうかを指定します。 ( [アカウントロックの設定](/help/forms/using/admin-help/configure-account-locking-settings.md#configure-account-locking-settings).) デフォルトでは、「アカウントロックを有効にする」が選択されています。
1. 「認証を追加」をクリックし、「認証プロバイダー」リストで、組織が使用している認証メカニズムに応じてプロバイダーを選択します。 値には、LDAP、Kerberos、SAML、またはカスタム認証プロバイダーを指定できます。

   LDAP を選択した場合は、ディレクトリ設定で指定した LDAP サーバーを使用するか、別の LDAP サーバーを選択して認証に使用できます。 別のサーバーを選択する場合、ユーザーは両方の LDAP サーバーに存在する必要があります。

1. ページで必要な追加情報を入力します。 ( [認証設定](/help/forms/using/admin-help/configuring-authentication-providers.md#authentication-settings).)
1. ディレクトリまたはカスタムの SPI(Service Provider Interface) を追加します。 ( [ディレクトリまたはカスタム SPI の追加](/help/forms/using/admin-help/configuring-directories.md#adding-directories-or-custom-spis).)
1. 「完了」をクリックし、「OK」をクリックします。

エンタープライズドメインを作成した後、User Management で使用する前に、手動でトリガーを同期するか、ディレクトリを作成して同期を実行します。 その後、ディレクトリ同期スケジュールを設定し、必要に応じて手動で同期を実行できます。 ( [ディレクトリの同期](/help/forms/using/admin-help/synchronizing-directories.md#synchronizing-directories).)

## ローカルドメインを追加 {#add-a-local-domain}

1. 管理コンソールで、設定／User Management／ドメインの管理をクリックします。
1. 「新規ローカルドメイン」をクリックします。
1. 「 ID 」ボックスにドメインの一意の ID を入力し、「名前」ボックスにドメインのわかりやすい名前を入力します。 ( [ドメイン名と ID に関する重要な考慮事項](adding-domains.md#important-considerations-for-domain-names-and-ids).)
1. アカウントのロックを有効にするかどうかを指定し、[OK] をクリックします。 ( [アカウントロックの設定](/help/forms/using/admin-help/configure-account-locking-settings.md#configure-account-locking-settings).) デフォルトでは、「アカウントロックを有効にする」が選択されています。

## ハイブリッドドメインの追加 {#add-a-hybrid-domain}

1. 管理コンソールで、設定／User Management／ドメインの管理をクリックします。
1. 「新しいハイブリッドドメイン」をクリックします。
1. 「 ID 」ボックスにドメインの一意の ID を入力し、「名前」ボックスにドメインのわかりやすい名前を入力します。 ( [ドメイン名と ID に関する重要な考慮事項](adding-domains.md#important-considerations-for-domain-names-and-ids).)
1. 「認証を追加」をクリックし、「認証プロバイダー」リストで、組織が使用している認証メカニズムに応じてプロバイダーを選択します。 値には、LDAP、Kerberos、SAML、またはカスタム認証プロバイダーを指定できます。
1. ページで必要な追加情報を入力します。 ( [認証設定](/help/forms/using/admin-help/configuring-authentication-providers.md#authentication-settings).)
1. 「 OK 」をクリックし、もう一度「 OK 」をクリックします。

## ドメイン名と ID に関する重要な考慮事項 {#important-considerations-for-domain-names-and-ids}

ドメイン名と ID を選択する際は、次の点に注意してください。

### 一般的な考慮事項 {#general-considerations}

* DB2 以外のデータベースプロバイダーを使用している場合、ドメイン ID には最大 50 バイトを含めることができます。 1 バイトの ASCII 文字を使用する場合、上限は 50 文字です。 ドメイン識別子にマルチバイト文字が含まれる場合、この制限は小さくなります。 例えば、識別子に 3 バイト文字が含まれるドメインを作成した場合、上限は 16 文字です。 また、4 バイト文字を含むドメインは作成できません。 この制限を超えるドメイン ID を作成した場合、AEM forms は不安定な状態になります。 この不安定な状態から回復するには、（このページ）[拡張文字またはマルチバイト文字を含むドメインの削除](adding-domains.md#remove-a-domain-that-contains-extended-or-multi-byte-characters)を参照してください。
* AEM forms 内で作成できるエンタープライズドメインおよびローカルドメインの数は、各ドメイン ID の長さによって異なります。 エンタープライズドメインまたはハイブリッドドメインを追加すると、User Management によってAEM forms 設定ファイル (config.xml) の AuthProviders ノードの configInstance 文字列が更新されます。 configInstance 文字列には、承認プロバイダーに関連付けられているすべてのドメインの絶対パスのコロン区切りリストが含まれます。 この文字列のサイズ制限は 8192 文字です。 この上限に達すると、追加のドメインを作成できなくなります。

### DB2 を使用する際の考慮事項 {#considerations-when-using-db2}

AEM forms データベースに DB2 を使用する場合、ドメイン ID の許可される最大長は、使用する文字の種類によって異なります。

* 1 バイト (ASCII) で 100 文字（例えば、英語、フランス語、ドイツ語の言語で使用されている文字）
* 全角 50 文字（例えば、中国語、日本語、韓国語で使用される文字）
* 4 バイト文字で 25 文字（例えば、繁体字中国語で使用される文字）

### MySQL を使用する際の考慮事項 {#considerations-when-using-mysql}

MySQL をAEM forms データベースとして使用する場合、次の制限が適用されます。

* ドメイン ID とドメイン名には 1 バイト (ASCII) 文字のみを使用します。 拡張 ASCII 文字を使用すると、AEM forms は不安定な状態になり、ドメインを削除しようとすると例外がスローされる場合があります。 この不安定な状態から回復するには、（このページ）[拡張文字またはマルチバイト文字を含むドメインの削除](adding-domains.md#remove-a-domain-that-contains-extended-or-multi-byte-characters)を参照してください。
* 大文字と小文字が異なる同じ名前の 2 つのドメインを作成することはできません。 例えば、という名前のドメインを作成しようとした場合 *Adobe* ( という名前のドメインが *adobe* は既に存在するので、エラーが発生します。
* User Management では、拡張文字の使用だけで異なる 2 つのドメイン名を区別することはできません。 例えば、 *abcde* また、「 *âbcdè * 」という名前のドメインも、同じと見なされます。

### 拡張文字またはマルチバイト文字を含むドメインを削除する {#remove-a-domain-that-contains-extended-or-multi-byte-characters}

1. 設定ファイルを書き出します。詳しくは、 [設定ファイルの読み込みと書き出し](/help/forms/using/admin-help/importing-exporting-configuration-file.md#importing-and-exporting-the-configuration-file).
1. 設定ファイルを開き、「ドメイン」ノードの下で、name 属性が拡張文字またはマルチバイト文字で作成されたドメインの名前と一致するノードを探します。 そのドメインに関連するノード全体を削除します。
1. データベースで、 edcprincipaldomainentity テーブルのドメインを検索します。

   * edcprincipaldomainentity から `*` を選択します。
   * 拡張文字またはマルチバイト文字を含むドメイン名を検索し、そのステータスを「廃止」に設定します。

1. 更新した設定ファイルを読み込みます。詳しくは、 [設定ファイルの読み込みと書き出し](/help/forms/using/admin-help/importing-exporting-configuration-file.md#importing-and-exporting-the-configuration-file).
