---
title: Forms User Management | ユーザーデータの処理
seo-title: Forms user management | Handling user data
description: User Management は、AEM Forms にアクセスするために AEM Forms ユーザーを作成、管理および認証することができる AEM Forms JEE コンポーネントです。ユーザーデータとデータストアの詳細を掘り下げます。 ユーザーデータにアクセスして削除する方法を説明します。
seo-description: User management is an AEM Forms JEE component that allows creating, managing, and authorizing AEM Forms users to access AEM Forms. Dig deeper on user data and data stores. Learn how to access and delete user data.
uuid: 2b76b69f-6f3a-4f1a-a2a4-d39f5e529f75
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.4/FORMS
discoiquuid: a88fc933-f1af-4798-b72f-10e7b0d2fd11
role: Admin
exl-id: 5005d57c-2585-46d1-9785-939e249a0128
source-git-commit: 3c050c33a384d586d74bd641f7622989dc1d6b22
workflow-type: tm+mt
source-wordcount: '915'
ht-degree: 78%

---

# Forms User Management | ユーザーデータの処理 {#forms-user-management-handling-user-data}

User Management は、AEM Forms にアクセスするために AEM Forms ユーザーを作成、管理および認証することができる AEM Forms JEE コンポーネントです。User Management は、ユーザー情報を取得するためのディレクトリとしてドメインを使用します。次の種類のドメインがサポートされます。

**ローカルドメイン**：この種類のドメインは、サードパーティーのストレージシステムに接続されません。代わりに、ユーザーおよびグループがローカルに作成され、User Management データベースに格納されます。パスワードはローカルに保存され、認証はローカルデータベースを使用して実行されます。

**ハイブリッドドメイン**：この種類のドメインは、サードパーティーのストレージシステムには接続されません。代わりに、ユーザーおよびグループがローカルに作成され、User Management データベースに格納されます。ローカルドメインと異なり、ハイブリッドドメインは、外部認証プロバイダー（LDAP、Kerberos、SAML またはカスタム）を使用します。

**エンタープライズドメイン**：LDAP ディレクトリなどのサードパーティーのストレージシステムに格納されているユーザーおよびグループで構成されます。User Management では、サードパーティのストレージシステムに対する書き込みは行われません。代わりに、User Management によってユーザーおよびグループの情報が User Management データベースと同期されます。エンタープライズドメインでは、外部認証プロバイダー（LDAP、Kerberos、SAML またはカスタム）も使用します。

<!-- Fix broken links For more information about how user management works and configured, see AEM Forms JEE administration help. -->

## ユーザーデータとデータストア {#user-data-and-data-stores}

User Management は、My Sql、Oracle、MS SQL Server、IBM DB2 などのデータベースにユーザーデータを格納します。さらに、AEMのオーサーで、少なくとも 1 回Formsアプリケーションにログインしたすべてのユーザー `https://[*server*]:[*host*]/lc`を指定した場合、ユーザーはAEMリポジトリに作成されます。 したがって、User Management のデータは、次のデータストアに格納されます。

* データベース
* AEM リポジトリ
* LDAP ディレクトリなどのサードパーティーストレージ

>[!NOTE]
>
>サードパーティーストレージに格納されたデータについては、この文書で説明していません。このようなストレージでユーザーデータを管理する場合は、サードパーティーのベンダーに直接問い合わせてください。

### データベース {#database}

User Management では、次のデータベーステーブルにユーザーデータが格納されます。

<table> 
 <tbody> 
  <tr> 
   <td>データベーステーブル</td> 
   <td>説明</td> 
  </tr> 
  <tr> 
   <td><code>EdcPrincipalEntity</code></td> 
   <td><p>プリンシパルエンティティに関する情報を格納します。プリンシパルは、ユーザー、グループ、またはロールのいずれかになります。</p> <p> </p> </td> 
  </tr> 
  <tr> 
   <td><code>EdcPrincipalUserEntity</code></td> 
   <td>ユーザーの個人が特定できる情報（PII）を格納します。ローカル、エンタープライズおよびハイブリッドの各ドメインに含まれるすべてのユーザーのエントリが含まれます。</td> 
  </tr> 
  <tr> 
   <td><p><code>EdcPrincipalLocalAccountEntity</code></p> <p><code class="code">EdcPrincipalLocalAccount
       </code>(Oracleおよび MS SQL データベース )</p> </td> 
   <td>ローカルユーザーデータのみを格納します。</td> 
  </tr> 
  <tr> 
   <td><p><code>EdcPrincipalEmailAliasEntity</code></p> <p><code class="code">EdcPrincipalEmailAliasEn 
       </code>(Oracleおよび MS SQL データベース )</p> </td> 
   <td>ローカル、エンタープライズおよびハイブリッドの各ドメインに含まれるすべてのユーザーのエントリが含まれます。これにはユーザーの電子メール ID が含まれます。</td> 
  </tr> 
  <tr> 
   <td><p><code>EdcPrincipalGrpCtmntEntity</code></p> <p><code>EdcPrincipalGrpCtmntEnti</code> (Oracleおよび MS SQL データベース )</p> </td> 
   <td>ユーザーとグループ間のマッピングを格納します。</td> 
  </tr> 
  <tr> 
   <td><code>EdcPrincipalRoleEntity</code></td> 
   <td>ユーザーとグループ両方についてロールとプリンシパル間のマッピングを格納します。</td> 
  </tr> 
  <tr> 
   <td><code>EdcPriResPrmEntity</code></td> 
   <td>ユーザーとグループ両方についてプリンシパルとアクセス許可間のマッピングを格納します。</td> 
  </tr> 
  <tr> 
   <td><p><code>EdcPrincipalMappingEntity</code></p> <p><code>EdcPrincipalMappingEntit</code> (Oracleおよび MS SQL データベース )</p> </td> 
   <td>プリンシパルに対応する古い属性値と新しい属性値を格納します。<br /> </td> 
  </tr> 
 </tbody> 
</table>

### AEM リポジトリ {#aem-repository}

少なくとも 1 回以上でFormsアプリケーションにアクセスしたユーザーのユーザー管理データ ( `https://[*server*]:[*host*]/lc` はAEMリポジトリにも格納されます。

## ユーザーデータへのアクセスと削除 {#access-and-delete-user-data}

User Management データベースおよび AEM リポジトリにあるユーザーの User Management データにアクセスしてデータを書き出すことができます。また、必要に応じてデータを永続的に削除できます。

### データベース {#database-1}

User Management データベースのユーザーデータを書き出すまたは削除するには、データベースクライアントを使用してデータベースに接続し、ユーザーの PII に基づいてプリンシパル ID を検索します。例えば、ログイン ID を使用してユーザーのプリンシパル ID を取得するには、次の `select` コマンドをデータベースで実行します。

内 `select` コマンド、 `<user_login_id>` を使用します。

```sql
select refprincipalid from EdcPrincipalUserEntity where uidstring = <user_login_id>
```

プリンシパル ID が分かったら、ユーザーデータを書き出したり、削除したりすることができます。

#### ユーザーデータの書き出し {#export-user-data}

次のデータベースコマンドを実行して、プリンシパル ID の User Management データをデータベーステーブルから書き出します。内 `select` コマンド、置換 `<principal_id>` を、書き出すデータを持つユーザーのプリンシパル ID に置き換えます。

>[!NOTE]
>
>次のコマンドでは、My SQL および IBM DB2 データベースのデータベーステーブル名を使用しています。これらのコマンドを Oracle および MS SQL データベースで実行するときは、コマンドの次のテーブル名を置き換えます。
>
>* 置換 `EdcPrincipalLocalAccountEntity` と `EdcPrincipalLocalAccount`
>
>* 置換 `EdcPrincipalEmailAliasEntity` と `EdcPrincipalEmailAliasEn`
>
>* 置換 `EdcPrincipalMappingEntity` と `EdcPrincipalMappingEntit`
>
>* 置換 `EdcPrincipalGrpCtmntEntity` と `EdcPrincipalGrpCtmntEnti`

>


```sql
Select * from EdcPrincipalLocalAccountEntity where refuserprincipalid in (Select id from EdcPrincipalUserEntity where refprincipalid in (Select id from EDCPRINCIPALENTITY where id='<principal_id>'));

Select * from EdcPrincipalEmailAliasEntity where refprincipalid in (Select id from EdcPrincipalEntity where id='<principal_id>');

Select * from EdcPrincipalRoleEntity where refprincipalid in (Select id from EdcPrincipalEntity where id='<principal_id>');

Select * from EdcPriResPrmEntity where refprinid in (Select id from EdcPrincipalEntity where id='<principal_id>');

Select * from EdcPrincipalUserEntity where refprincipalid in (Select id from EdcPrincipalEntity where id='<principal_id>');

Select * from EdcPrincipalMappingEntity where refprincipalid in (Select id from EdcPrincipalEntity where id='<principal_id>');

Select * from EdcPrincipalGrpCtmntEntity where refchildprincipalid in (Select id from EdcPrincipalEntity where id='<principal_id>');

Select * from EdcPrincipalEntity where id='<principal_id>';
```

#### ユーザーデータの削除 {#delete-user-data}

特定のプリンシパル ID の User Management データをデータベーステーブルから削除するには、次の手順を実行します。

1. 「[ユーザーデータの削除](/help/forms/using/user-management-handling-user-data.md#delete-aem)」の説明に従って AEM リポジトリからユーザーデータを削除します（該当する場合）。
1. AEM Forms サーバーをシャットダウンします。
1. 次のデータベースコマンドを実行して、目的のプリンシパル ID の User Management データをデータベーステーブルから削除します。内 `Delete` コマンド、置換 `<principal_id>` を、削除するデータのユーザーのプリンシパル ID に置き換えます。

   ```sql
   Delete from EdcPrincipalLocalAccountEntity where refuserprincipalid in (Select id from EdcPrincipalUserEntity where refprincipalid in (select id from EdcPrincipalEntity where id='<principal_id>'));
   
   Delete from EdcPrincipalEmailAliasEntity where refprincipalid in (Select id from EdcPrincipalEntity where id='<principal_id>');
   
   Delete from EdcPrincipalRoleEntity where refprincipalid in (Select id from EdcPrincipalEntity where id='<principal_id>');
   
   Delete from EdcPriResPrmEntity where refprinid in (Select id from EdcPrincipalEntity where id='<principal_id>');
   
   Delete from EdcPrincipalUserEntity where refprincipalid in (Select id from EdcPrincipalEntity where id='<principal_id>');
   
   Delete from EdcPrincipalMappingEntity where refprincipalid in (Select id from EdcPrincipalEntity where id='<principal_id>');
   
   Delete from EdcPrincipalGrpCtmntEntity where refchildprincipalid in (Select id from EdcPrincipalEntity where id='<principal_id>');
   
   Delete from EdcPrincipalEntity where id='<principal_id>';
   ```

1. AEM Forms サーバーを開始します。

### AEM リポジトリ {#aem-repository-1}

Forms JEE ユーザーは、AEM Forms オーサーインスタンスに少なくとも一度アクセスしている場合、AEM リポジトリにデータが格納されています。AEM リポジトリのユーザーデータにアクセスして削除することができます。

#### ユーザーデータへのアクセス {#access-user-data}

AEMリポジトリで作成されたユーザーを表示するには、次の場所にログインします。 `https://[*server*]:[*port*]/lc/useradmin` AEM管理者の資格情報を使用して URL の `*server*` と `*port*` は、AEM オーサーインスタンスのサーバーとポートであることに注意してください。ここでは、ユーザー名でユーザーを検索できます。ユーザーをダブルクリックすると、ユーザーのプロパティ、権限、グループなどの情報が表示されます。ユーザーの `Path` プロパティは、AEM リポジトリで作成されたユーザーノードへのパスを指定します。

#### ユーザーデータの削除 {#delete-aem}

ユーザを削除するには：

1. に移動します。 `https://[*server*]:[*port*]/lc/useradmin` AEM管理者の資格情報を使用して
1. ユーザーを検索してユーザー名をダブルクリックし、ユーザープロパティを開きます。を `Path` プロパティ。
1. AEM CRX DELite( ) に移動します。 `https://[*server*]:[*port*]/lc/crx/de/index.jsp` ユーザーパスに移動または検索します。
1. パスを削除し、 **[!UICONTROL すべて保存]** をクリックして、AEMリポジトリからユーザーを永久に削除します。
