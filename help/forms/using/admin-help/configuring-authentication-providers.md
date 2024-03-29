---
title: 認証プロバイダーの設定
seo-title: Configuring authentication providers
description: 認証プロバイダーの追加、編集、削除、認証設定の変更、ユーザーのジャストインタイムプロビジョニングについての説明を参照してください。
seo-description: Add, edit, or delete authentication providers, change authentication settings, and read about just-in-time provisioning of users.
uuid: 90e7690b-1ce0-4604-b58f-6dca4f2372cf
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_managing_domains
products: SG_EXPERIENCEMANAGER/6.4/FORMS
discoiquuid: 31dd8db3-ddac-429e-82f8-8c5dc4ffc186
exl-id: 1b5ead0a-cf33-4422-bdca-2bd6aebbc98d
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '1612'
ht-degree: 39%

---

# 認証プロバイダーの設定 {#configuring-authentication-providers}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

ハイブリッドドメインには少なくとも 1 つの認証プロバイダーが必要で、エンタープライズドメインには少なくとも 1 つの認証プロバイダーまたはディレクトリプロバイダーが必要です。

SPNEGO を使用して SSO を有効にする場合は、SPNEGO が有効になっている Kerberos 認証プロバイダを追加し、バックアップとして LDAP プロバイダを追加します。 この設定は、SPNEGO が機能しない場合に、ユーザー ID とパスワードを使用したユーザー認証を有効にします。 ( [SPNEGO を使用した SSO の有効化](/help/forms/using/admin-help/enabling-single-sign-on-aem.md#enable-sso-using-spnego).)

## 認証プロバイダーの追加 {#add-an-authentication-provider}

1. 管理コンソールで、設定／User Management／ドメインの管理をクリックします。
1. リストで既存のドメインをクリックします。 新しいドメインに認証を追加する場合は、 [エンタープライズドメインの追加](/help/forms/using/admin-help/adding-domains.md#add-an-enterprise-domain) または [ハイブリッドドメインの追加](/help/forms/using/admin-help/adding-domains.md#add-a-hybrid-domain).
1. 「認証を追加」をクリックし、「認証プロバイダー」リストで、組織が使用している認証メカニズムに応じてプロバイダーを選択します。
1. ページで必要な追加情報を入力します。 ( [認証設定](configuring-authentication-providers.md#authentication-settings).)
1. （オプション）「テスト」をクリックして設定をテストします。
1. 「 OK 」をクリックし、もう一度「 OK 」をクリックします。

## 既存の認証プロバイダーの編集 {#edit-an-existing-authentication-provider}

1. 管理コンソールで、設定／User Management／ドメインの管理をクリックします。
1. リストで適切なドメインをクリックします。
1. 表示されるページで、リストから適切な認証プロバイダーを選択し、必要に応じて変更します。 ( [認証設定](configuring-authentication-providers.md#authentication-settings).)
1. 「OK」をクリックします。

## 認証プロバイダーの削除 {#delete-an-authentication-provider}

1. 管理コンソールで、設定／User Management／ドメインの管理をクリックします。
1. リストで適切なドメインをクリックします。
1. 削除する認証プロバイダーのチェックボックスを選択し、「削除」をクリックします。
1. 表示される確認ページで「 OK 」をクリックし、もう一度「 OK 」をクリックします。

## 認証設定 {#authentication-settings}

選択したドメインの種類と認証の種類に応じて、次の設定を使用できます。

### LDAP 設定 {#ldap-settings}

エンタープライズドメインまたはハイブリッドドメインの認証を設定し、LDAP 認証を選択する場合は、ディレクトリ設定で指定した LDAP サーバーを使用するか、別の LDAP サーバーを選択して認証に使用できます。 別のサーバーを選択する場合、ユーザーは両方の LDAP サーバーに存在する必要があります。

ディレクトリ設定で指定した LDAP サーバーを使用するには、認証プロバイダーとして「 LDAP 」を選択し、「 OK 」をクリックします。

別の LDAP サーバーを使用して認証を実行するには、認証プロバイダーとして「LDAP」を選択し、「カスタム LDAP 認証」チェックボックスをオンにします。 次の設定が表示されます。

**サーバー：**（必須）ディレクトリサーバーの完全修飾ドメイン名（FQDN）。例えば、example.com ネットワーク上の x というコンピューターの場合、FQDN は x.example.com となります。FQDN サーバー名の代わりに IP アドレスを使用することもできます。

**ポート：**（必須）ディレクトリサーバーが使用するポート。通常は 389 で、Secure Sockets Layer（SSL）プロトコルを使用してネットワーク経由で認証情報を送信する場合は 636 です。

**SSL：**（必須）ネットワーク経由でデータを送信するときにディレクトリサーバーで SSL を使用するかどうかを指定します。デフォルトは No です。 「はい」に設定した場合、対応する LDAP サーバー証明書は、アプリケーションサーバーの Java™ランタイム環境 (JRE) によって信頼される必要があります。

**連結**（必須）ディレクトリへのアクセス方法を指定します。

**匿名：**&#x200B;ユーザー名またはパスワードは不要です。

**ユーザー：**&#x200B;認証が必要です。「名前」ボックスに、ディレクトリにアクセスできるユーザーレコードの名前を指定します。ユーザーアカウントの完全な識別名（DN）を入力することをお勧めします。例えば、cn=Jane Doe, ou=user, dc=can, dc=com などです。「パスワード」ボックスに、関連するパスワードを指定します。 これらの設定は、「連結」オプションとして「ユーザー」を選択した場合に必要です。

**ベース DN の取得：**（非必須）ベース DN を取得し、ドロップダウンリストに表示します。この設定は、複数のベース DN がある場合に 1 つの値を選択する必要があるときに便利です。

**ベース DN：**（必須）LDAP 階層からユーザーとグループを同期するための開始点として使用されます。サービスに対して同期する必要のあるすべてのユーザーとグループを含む階層の最下位レベルで BaseDN を指定することをお勧めします。 この設定にユーザーの DN を含めないでください。 特定のユーザーを同期するには、検索フィルター設定を使用します。

**ページに次の値を入力：**（非必須）選択すると、ユーザー設定ページとグループの設定ページの属性に、対応するデフォルトの LDAP 値が入力されます。

**検索フィルター：**（必須）ユーザーに関連付けられているレコードを検索するために使用する検索フィルター。「検索フィルターの構文」を参照してください。

### Kerberos 設定 {#kerberos-settings}

エンタープライズドメインまたはハイブリッドドメインの認証を構成し、Kerberos 認証を選択する場合は、次の設定を使用できます。

**DNS IP：** AEM Forms を実行しているサーバーの DNS IP アドレス。Windows の場合、この IP アドレスは、コマンドラインで ipconfig /all を実行して確認できます。

**KDC ホスト：**&#x200B;認証に使用する Active Directory サーバーの完全修飾ホスト名または IP アドレス。

**サービスユーザー：** Active Directory 2003 を使用している場合、この値は `HTTP/<server name>` の形式でサービスプリンシパル用に作成されたマッピングになります。Active Directory 2008 を使用している場合、この値はサービスプリンシパルのログイン ID になります。例えば、サービスプリンシパル名が um spnego、ユーザー ID が spnegodemo、マッピングが HTTP/example.yourcompany.com であるとします。この場合、Active Directory 2003 では、「サービスユーザー」を HTTP/example.yourcompany.com に設定します。Active Directory 2008 では、「サービスユーザー」を spnegodemo に設定します。（SPNEGO を使用した SSO の有効化を参照。）

**サービス領域：** Active Directory のドメイン名。

**サービスパスワード：**&#x200B;サービスユーザーのパスワード

**SPNEGO を有効にする：**&#x200B;シングルサインオン（SSO）で SPNEGO を使用できるようにします。（SPNEGO を使用した SSO の有効化を参照）。

### SAML 設定 {#saml-settings}

エンタープライズドメインまたはハイブリッドドメインの認証を設定し、SAML 認証を選択する場合は、次の設定を使用できます。 追加の SAML 設定について詳しくは、 [SAML サービスプロバイダーの設定](/help/forms/using/admin-help/configure-saml-service-provider-settings.md#configure-saml-service-provider-settings).

**読み込む SAML ID プロバイダーメタデータファイルを選択してください：**「参照」をクリックして、IDP から生成された SAML ID プロバイダーメタデータファイルを選択し、「読み込み」をクリックします。IDP の詳細が表示されます。

**タイトル：** EntityID で示される URL のエイリアス。タイトルは、エンタープライズユーザーとローカルユーザーのログインページにも表示されます。

**ID プロバイダーは、クライアントの基本認証をサポートします。** クライアント基本認証は、IDP が SAML アーティファクト解決プロファイルを使用する場合に使用されます。このプロファイルでは、User Management は、IDP で実行されている Web サービスに接続して、実際の SAML アサーションを取得します。 IDP は認証を必要とする場合があります。 IDP で認証が必要な場合は、このオプションを選択し、表示されるボックスでユーザー名とパスワードを指定します。

**カスタムプロパティ：**&#x200B;追加のプロパティを指定できます。追加のプロパティは、名前と値のペアを新しい行で区切って指定します。

アーティファクトバインディングを使用する場合は、次のカスタムプロパティが必要です。

* 次のカスタムプロパティを追加して、AEM forms サービスプロバイダーを表すユーザー名を指定します。このユーザー名は、IDP Artifact Resolution サービスへの認証に使用されます。
   `saml.idp.resolve.username=<username>`

* 次のカスタムプロパティを追加して、`saml.idp.resolve.username` で指定したユーザーのパスワードを指定します。
   `saml.idp.resolve.password=<password>`

* 次のカスタムプロパティを追加して、サービスプロバイダーが SSL でアーティファクト解決サービスに接続を確立中に証明書検証を無視できるようにします。
   `saml.idp.resolve.ignorecert=true`

### カスタム設定 {#custom-settings}

エンタープライズドメインまたはハイブリッドドメインの認証を設定し、カスタム認証を選択する場合は、カスタム認証プロバイダーの名前を選択します。

## ユーザーのジャストインタイムプロビジョニング {#just-in-time-provisioning-of-users}

認証プロバイダーを介してユーザーが正常に認証された後、ジャストインタイムプロビジョニングによって、User Management データベースにユーザーが自動的に作成されます。 また、関連する役割とグループも新しいユーザーに動的に割り当てられます。 エンタープライズドメインおよびハイブリッドドメインに対して、ジャストインタイムプロビジョニングを有効にできます。

以下の手順では、AEM forms での従来の認証の動作方法を説明します。

1. ユーザーがAEM forms にログインしようとすると、User Management は、使用可能なすべての認証プロバイダーに対して資格情報を順次渡します。 （ログイン資格情報には、ユーザー名とパスワードの組み合わせ、Kerberos チケット、PKCS7 署名などが含まれます）。
1. 認証プロバイダーが資格情報を検証します。
1. 次に、認証プロバイダーは、ユーザーが User Management データベースに存在するかどうかを確認します。 次のステータスが考えられます。

   **存在する** ユーザーが登録されており、ロックされていない場合、User Management は認証成功を返します。これに対して、ユーザーが登録されていないか、ロックされている場合、User Management は認証失敗を返します。

   **存在しない** User Management は認証失敗を返します。

   **無効** User Management は認証失敗を返します。

1. 認証プロバイダーから返された結果が評価されます。 認証プロバイダーが認証成功を返した場合、ユーザーはログインできます。 それ以外の場合は、User Management は次の認証プロバイダー（手順 2～3）と確認します。
1. ユーザーの資格情報を検証する使用可能な認証プロバイダーがない場合は、認証失敗が返されます。

ジャストインタイムプロビジョニングが有効になっている場合、いずれかの認証プロバイダーが資格情報を検証すると、User Management で新しいユーザーが動的に作成されます。 （上記の手順 3 の後）。

ジャストインタイムプロビジョニングを使用しない場合、ユーザーが正常に認証され、User Management データベースに見つからないと、認証は失敗します。 ジャストインタイムプロビジョニングにより、認証手順に手順が追加され、ユーザーを作成し、役割とグループをユーザーに割り当てることができます。

### ドメインのジャストインタイムプロビジョニングを有効にする {#enable-just-in-time-provisioning-for-a-domain}

1. IdentityCreator および AssignmentProvider インターフェイスを実装するサービスコンテナを作成します。 ( [AEM forms によるプログラミング](https://www.adobe.com/go/learn_aemforms_programming_63_jp).)
1. サービスコンテナを forms サーバーにデプロイします。
1. 管理コンソールで、設定／User Management／ドメインの管理をクリックします。

   既存のドメインを選択するか、「新規エンタープライズドメイン」をクリックします。

1. ドメインを作成するには、「新規エンタープライズドメイン」または「新規ハイブリッドドメイン」をクリックします。 既存のドメインを編集するには、ドメインの名前をクリックします。
1. 「ジャストインタイムプロビジョニングを有効にする」を選択します。

   ***注意&#x200B;**：「ジャストインタイムプロビジョニングを有効にする」チェックボックスが見つからない場合は、ホーム／設定／User Management／設定／システム属性の詳細設定をクリックし、「再読み込み」をクリックします。*

1. 認証プロバイダーを追加します。 認証プロバイダーを追加する際に、新しい認証画面で、登録されている ID 作成者と割り当てプロバイダーを選択します。 ( [認証プロバイダーの設定](configuring-authentication-providers.md#configuring-authentication-providers).)
1. ドメインを保存します。
