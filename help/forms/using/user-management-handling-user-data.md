---
title: Forms User Management | ユーザーデータの処理
seo-title: Forms user management | Handling user data
description: ユーザー管理は、AEM Forms JEE コンポーネントで、AEM Formsユーザーを作成、管理および承認して、AEM Formsにアクセスすることを許可します。 ユーザーデータとデータストアの詳細を掘り下げます。 ユーザーデータにアクセスして削除する方法を説明します。
seo-description: User management is an AEM Forms JEE component that allows creating, managing, and authorizing AEM Forms users to access AEM Forms. Dig deeper on user data and data stores. Learn how to access and delete user data.
uuid: 2b76b69f-6f3a-4f1a-a2a4-d39f5e529f75
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.4/FORMS
discoiquuid: a88fc933-f1af-4798-b72f-10e7b0d2fd11
role: Admin
exl-id: 5005d57c-2585-46d1-9785-939e249a0128
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '951'
ht-degree: 36%

---

# Forms User Management | ユーザーデータの処理 {#forms-user-management-handling-user-data}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

ユーザー管理は、AEM Forms JEE コンポーネントで、AEM Formsユーザーを作成、管理および承認して、AEM Formsにアクセスすることを許可します。 User Management は、ユーザー情報を取得するために、ドメインをディレクトリとして使用します。 次のドメインタイプがサポートされています。

**ローカルドメイン**:このタイプのドメインは、サードパーティのストレージシステムには接続されません。 代わりに、ユーザーとグループがローカルに作成され、User Management データベースに格納されます。 パスワードはローカルに保存され、認証はローカルデータベースを使用しておこなわれます。

**ハイブリッドドメイン**:このタイプのドメインは、サードパーティのストレージシステムには接続されません。 代わりに、ユーザーとグループがローカルに作成され、User Management データベースに格納されます。 ローカルドメインとは異なり、ハイブリッドドメインは、外部認証プロバイダーを使用します。外部認証プロバイダーは、LDAP、Kerberos、SAML、またはカスタム認証プロバイダーです。

**エンタープライズドメイン**:LDAP ディレクトリなど、サードパーティのストレージシステムに存在するユーザーとグループで構成されます。 User Management は、サードパーティのストレージシステムに書き込みを行いません。 代わりに、User Management はユーザーおよびグループの情報を User Management データベースと同期します。 エンタープライズドメインは、外部認証プロバイダも使用します。外部認証プロバイダは、LDAP、Kerberos、SAML、またはカスタム認証プロバイダです。

<!-- Fix broken links For more information about how user management works and configured, see AEM Forms JEE administration help. -->

## ユーザーデータとデータストア {#user-data-and-data-stores}

ユーザー管理では、My Sql、Oracle、MS SQL Server、IBM DB2 などのデータベースにユーザーデータを格納します。 また、`https://[*server*]:[*host*]/lc` から AEM オーサーの Forms アプリケーションに一度でもログインすると、AEM リポジトリにユーザーデータが作成されます。したがって、ユーザー管理は次のデータストアに保存されます。

* データベース
* AEMリポジトリ
* LDAP ディレクトリなどのサードパーティストレージ

>[!NOTE]
>
>サードパーティのストレージに保存されたデータは、このドキュメントの範囲外です。 サードパーティベンダーに直接問い合わせて、そのようなストレージ内のユーザーデータを管理します。

### データベース {#database}

ユーザー管理では、次のデータベーステーブルにユーザーデータを格納します。

<table> 
 <tbody> 
  <tr> 
   <td>データベーステーブル</td> 
   <td>説明</td> 
  </tr> 
  <tr> 
   <td><code>EdcPrincipalEntity</code></td> 
   <td><p>プリンシパルエンティティに関する情報を格納します。 プリンシパルは、ユーザー、グループ、または役割です。</p> <p> </p> </td> 
  </tr> 
  <tr> 
   <td><code>EdcPrincipalUserEntity</code></td> 
   <td>ユーザーの個人を特定できる情報 (PII) を格納します。 ローカルドメイン、エンタープライズドメイン、ハイブリッドドメインの各ユーザーのエントリが含まれます。</td> 
  </tr> 
  <tr> 
   <td><p><code>EdcPrincipalLocalAccountEntity</code></p> <p><code class="code">EdcPrincipalLocalAccount
       </code>（Oracle データベースおよび MS SQL データベース）</p> </td> 
   <td>ローカルユーザーのデータのみを格納します。</td> 
  </tr> 
  <tr> 
   <td><p><code>EdcPrincipalEmailAliasEntity</code></p> <p><code class="code">EdcPrincipalEmailAliasEn 
       </code>（Oracle データベースおよび MS SQL データベース）</p> </td> 
   <td>ローカルドメイン、エンタープライズドメイン、ハイブリッドドメインのすべてのユーザーのエントリが含まれます。 ユーザーの電子メール ID が含まれます。</td> 
  </tr> 
  <tr> 
   <td><p><code>EdcPrincipalGrpCtmntEntity</code></p> <p><code>EdcPrincipalGrpCtmntEnti</code> （Oracle データベースおよび MS SQL データベース）</p> </td> 
   <td>ユーザーとグループのマッピングを格納します。</td> 
  </tr> 
  <tr> 
   <td><code>EdcPrincipalRoleEntity</code></td> 
   <td>ユーザーとグループの両方について、ロールとプリンシパルのマッピングを格納します。</td> 
  </tr> 
  <tr> 
   <td><code>EdcPriResPrmEntity</code></td> 
   <td>ユーザーとグループの両方について、プリンシパルと権限のマッピングを格納します。</td> 
  </tr> 
  <tr> 
   <td><p><code>EdcPrincipalMappingEntity</code></p> <p><code>EdcPrincipalMappingEntit</code> （Oracle データベースおよび MS SQL データベース）</p> </td> 
   <td>プリンシパルに対応する古い属性値と新しい属性値を格納します。<br /> </td> 
  </tr> 
 </tbody> 
</table>

### AEMリポジトリ {#aem-repository}

`https://[*server*]:[*host*]/lc` から Forms アプリケーションに一度でもログインすると、User Management データも AEM リポジトリに格納されます。

## ユーザーデータへのアクセスと削除 {#access-and-delete-user-data}

User Management データベースおよびAEMリポジトリのユーザーのユーザー管理データにアクセスして書き出すことができ、必要に応じて永久に削除できます。

### データベース {#database-1}

ユーザー管理データベースからユーザーデータを書き出しまたは削除するには、データベースクライアントを使用してデータベースに接続し、ユーザーの PII に基づいてプリンシパル ID を見つける必要があります。 例えば、ログイン ID を使用してユーザーのプリンシパル ID を取得するには、次の `select` コマンドをデータベースで実行します。

`select` コマンドで、`<user_login_id>` をプリンシパル ID を取得したいユーザーのログイン ID に置き換えます。

```sql
select refprincipalid from EdcPrincipalUserEntity where uidstring = <user_login_id>
```

プリンシパル ID がわかったら、ユーザーデータを書き出したり、削除したりできます。

#### ユーザーデータの書き出し {#export-user-data}

次のデータベースコマンドを実行して、プリンシパル ID のユーザー管理データをデータベーステーブルから書き出します。 `select` コマンドで、`<principal_id>` を書き出すデータのユーザーに割り当てられたプリンシパル ID に置き換えます。

>[!NOTE]
>
>次のコマンドでは、My SQL および IBM DB2 データベースのデータベーステーブル名を使用しています。oracleおよび MS SQL データベースでこれらのコマンドを実行する場合は、コマンドで次のテーブル名を置き換えます。
>
>* `EdcPrincipalLocalAccountEntity` を `EdcPrincipalLocalAccount` に置き換えます。
>
>* `EdcPrincipalEmailAliasEntity` を `EdcPrincipalEmailAliasEn` に置き換えます。
>
>* `EdcPrincipalMappingEntity` を `EdcPrincipalMappingEntit` に置き換えます。
>
>* `EdcPrincipalGrpCtmntEntity` を `EdcPrincipalGrpCtmntEnti` に置き換えます。
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

プリンシパル ID のユーザー管理データをデータベーステーブルから削除するには、次の手順を実行します。

1. 必要に応じて、AEMリポジトリからユーザーデータを削除します。詳しくは、 [ユーザーデータを削除](/help/forms/using/user-management-handling-user-data.md#delete-aem).
1. AEM Formsサーバーをシャットダウンします。
1. 次のデータベースコマンドを実行して、目的のプリンシパル ID の User Management データをデータベーステーブルから削除します。`Delete` コマンドで、`<principal_id>` を、削除するデータのユーザーに割り当てられたプリンシパル ID に置き換えます。

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

1. AEM Forms サーバーを起動します。

### AEMリポジトリ {#aem-repository-1}

Forms JEE ユーザーが少なくとも 1 つのAEM Formsオーサーインスタンスにアクセスした場合、AEMリポジトリにデータが格納されます。 ユーザーデータにアクセスして、AEMリポジトリから削除できます。

#### ユーザーデータにアクセス {#access-user-data}

AEM リポジトリで作成されたユーザーを表示するには、AEM 管理者の資格情報を使用して `https://[*server*]:[*port*]/lc/useradmin` にログインします。URL の `*server*` と `*port*` は、AEM オーサーインスタンスのサーバーとポートであることに注意してください。ここでは、ユーザー名を使用してユーザーを検索できます。 ユーザーをダブルクリックして、そのユーザーのプロパティ、権限、グループなどの情報を表示します。 ユーザーの `Path` プロパティは、AEM リポジトリで作成されたユーザーノードへのパスを指定します。

#### ユーザーデータの削除 {#delete-aem}

ユーザーを削除するには：

1. AEM 管理者の資格情報を使用して、`https://[*server*]:[*port*]/lc/useradmin` に移動します。
1. ユーザーを検索してユーザー名をダブルクリックし、ユーザープロパティを開きます。`Path` プロパティをコピーします。
1. `https://[*server*]:[*port*]/lc/crx/de/index.jsp` にある AEM CRX DELite にアクセスし、ユーザーパスに移動するか、ユーザーパスを検索します。
1. パスを削除して「**[!UICONTROL すべて保存]**」をクリックし、AEM リポジトリからこのユーザーを永続的に削除します。
