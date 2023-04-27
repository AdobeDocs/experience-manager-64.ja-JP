---
title: フォームポータル | ユーザーデータの処理
seo-title: Forms Portal | Handling user data
description: AEM Formsポータルは、AEM Sitesページ上のアダプティブフォーム、HTML5 フォーム、その他のFormsアセットのリストを表示するために使用できるコンポーネントを提供します。 Formsポータルでドラフトフォームと送信済みフォームのデータを保存する方法を説明します。 設定済みのデータストアでログインしたユーザーと匿名ユーザーのドラフトおよび送信済みフォームデータにアクセスする方法と、必要に応じて削除する方法について詳しく説明します。
seo-description: AEM Forms portal provides components that you can use to list adaptive forms, HTML5 forms, and other Forms assets on AEM Sites page. Learn how Forms portal stores data for draft and submitted forms. Dig deeper on how to access draft and submitted forms data for logged-in and anonymous users in the configured data stores, and if required, delete it.
uuid: 2ac2b2a9-b603-489a-86b8-a78b697f130d
contentOwner: vishgupt
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.4/FORMS
discoiquuid: 48f841b7-0e7f-4216-9ee8-fb6e843acaf0
role: Admin
exl-id: 05dbb6ee-09fd-44ee-bb8b-a3f3ebb32f5a
source-git-commit: 3c050c33a384d586d74bd641f7622989dc1d6b22
workflow-type: tm+mt
source-wordcount: '915'
ht-degree: 52%

---

# フォームポータル | ユーザーデータの処理 {#forms-portal-handling-user-data}

AEM Formsポータルは、AEM Sitesページ上のアダプティブフォーム、HTML5 フォーム、その他のFormsアセットのリストを表示するために使用できるコンポーネントを提供します。 さらに、ログインしたユーザーのためにドラフトや送信済みのアダプティブフォームおよび HTML5 フォームを表示するように構成することもできます。Forms Portal について詳しくは、「[ポータルでのフォーム発行の概要](/help/forms/using/introduction-publishing-forms.md)」を参照してください。

ログインしているユーザーがアダプティブフォームをドラフトとして保存したり送信したりすると、それらはフォームポータルの「ドラフト」タブと「送信」タブに表示されます。 ドラフトまたは送信済みのフォームのデータは、AEMのデプロイメント用に設定されたデータストアに保存されます。 匿名ユーザーのドラフトと送信は、フォームポータルページに表示されません。ただし、データは設定済みのデータストアに保存されます。 詳細情報に関しては、[ドラフトと送信に使用するストレージサービスの設定](/help/forms/using/configuring-draft-submission-storage.md)を参照してください。

## ユーザーデータとデータストア {#user-data-and-data-stores}

Forms portal では、次のシナリオでドラフトフォームと送信済みフォームのデータを保存します。

* アダプティブフォームに設定された送信アクションが **Forms Portal 送信アクション**&#x200B;である。
* **Forms Portal 送信アクション**&#x200B;以外の送信アクションでは、「**[!UICONTROL Forms Portal にデータを格納]**」オプションが、アダプティブフォームコンテナの&#x200B;**送信** プロパティで有効になっている。

ログインしたユーザーと匿名ユーザーのドラフトおよび送信済みフォームごとに、フォームポータルには次のデータが保存されます。

* フォーム名、フォームパス、ドラフト ID または送信 ID、添付ファイルパス、ユーザーデータ ID などのフォームメタデータ
* データバイトとしてのフォームの添付ファイル
* データバイトとしてのフォームデータ

設定されたデータストアの永続性に応じて、ドラフトと送信済みのフォームのデータは、次の場所に保存されます。

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>永続性タイプ</strong></p> </td> 
   <td><p><strong>データストア</strong></p> </td> 
   <td><p><strong>場所</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>デフォルト</p> </td> 
   <td><p>オーサーインスタンスとパブリッシュインスタンスのAEMリポジトリ</p> </td> 
   <td><p><code>/content/forms/fp/</code></p> </td> 
  </tr> 
  <tr> 
   <td><p>リモート</p> </td> 
   <td><p>オーサーインスタンスとリモートAEMインスタンスのAEMリポジトリ</p> </td> 
   <td><p><code>/content/forms/fp/</code></p> </td> 
  </tr> 
  <tr> 
   <td><p>データベース</p> </td> 
   <td><p>オーサーインスタンスおよびデータベーステーブルのAEMリポジトリ</p> </td> 
   <td>データベーステーブル <code>data</code>、<code>metadata</code> および <code>additionalmetadata</code></td> 
  </tr> 
 </tbody> 
</table>

## ユーザーデータへのアクセスと削除 {#access-and-delete-user-data}

設定済みのデータストアで、ログインしたユーザーと匿名ユーザーのドラフトおよび送信済みのフォームデータにアクセスし、必要に応じて削除することができます。

### AEMインスタンス {#aem-instances}

ログインしたユーザーおよび匿名ユーザーの AEM インスタンス（作成者、発行またはリモート）のすべてのドラフトと送信済みフォームのデータは、該当する AEM リポジトリの `/content/forms/fp/` ノードに格納されます。ログインしたユーザーまたは匿名ユーザーがドラフトを保存するかフォームを送信するたびに、`draft ID` または `submission ID`、`user data ID`、および各添付ファイルのランダム `ID`（該当する場合）が生成され、ドラフトまたは送信に関連付けられます。

#### ユーザーデータにアクセス {#access-user-data}

ログインしているユーザーが下書きを保存したり、フォームを送信したりすると、そのユーザー ID を使用して子ノードが作成されます。 例えば、ユーザー ID が `srose` である Sarah Rose のドラフトデータと送信データが AEM リポジトリの `/content/forms/fp/srose/` ノードに格納されるとします。このユーザー ID ノード内では、データが階層構造で整理されます。

以下の表は、`srose` を使用して作成されたすべてのドラフトのデータが、どのように AEM リポジトリに格納されるのかを説明しています。

>[!NOTE]
>
>`drafts` と同一の構造が `srose` に送信されたフォーム用に `/content/forms/fp/srose/submit/` ノード下にレプリケートされます。
>
>`anonymous` ユーザーによるすべてのドラフトと送信済みフォームは、`/content/forms/fp/anonymous/` ノードに格納されます。このノードでは、匿名ユーザーのすべてのドラフトと送信済みフォームが、`draft` ノードと `submit` ノードによって整理されます。

| ノード | 説明 |
|---|---|
| `/content/forms/fp/srose/drafts` | ユーザーが作成したすべてのドラフトが含まれるコンテナノードデータ |
| `/content/forms/fp/srose/drafts/attachments/` | ドラフト ID に基づいてユーザーのすべての添付ファイルがまとめられる |
| `/content/forms/fp/srose/drafts/attachments/<ID>` | 選択した ID の添付ファイルがバイナリ形式で含まれる |
| `/content/forms/fp/srose/drafts/metadata/` | ドラフト ID にもとづいてユーザーのフォームメタデータがまとめられる |
| `/content/forms/fp/srose/drafts/metadata/<draft ID>` | 選択したドラフト ID のフォームメタデータが含まれる |
| `/content/forms/fp/srose/drafts/data/` | ユーザーデータ ID に基づいてユーザーのフォームデータがまとめられる |
| `/content/forms/fp/srose/drafts/data/<user data ID>` | 選択したユーザーデータ ID のフォームデータをバイナリ形式で格納します |

#### ユーザーデータの削除 {#delete-user-data}

AEM システムで、ログインしたユーザーのドラフトおよび送信済みフォームに含まれるユーザーデータを完全に削除するには、特定ユーザーの `user ID` ノードを作成者ノードから削除する必要があります。該当するすべての AEM インスタンスから手動でデータを削除する必要があります。

すべての匿名ユーザーのドラフトデータと送信データは、共通の `drafts` ノードと `submit` ノード内に格納されます。これらのノードは、`/content/forms/fp/anonymous` にあります。特定の匿名ユーザーのデータを検索する方法は、何らかの識別情報がわかっている場合を除きます。この場合、AEMリポジトリ内の匿名ユーザーを識別する情報を検索し、該当するすべてのAEMインスタンスからそのノードを手動で削除して、AEMシステムからデータを削除できます。 ただし、すべての匿名ユーザーのデータを削除する場合は、`anonymous` ノードを削除することで、すべての匿名ユーザーのドラフトデータと送信データを削除できます。

### データベース {#database}

データをデータベースに格納するようにAEMが設定されている場合、フォームポータルのドラフトと送信データは、次のデータベーステーブルに、ログインしたユーザーと匿名ユーザーの両方に格納されます。

* data
* メタデータ
* additionalmetadata

#### ユーザーデータにアクセス {#access-user-data-1}

データベーステーブル内のログイン済みユーザーと匿名ユーザーのドラフトと送信データにアクセスするには、次のデータベースコマンドを実行します。 クエリで、`logged-in user` を、アクセスするデータのユーザー ID または匿名ユーザーの `anonymous` と置き換えます。

```sql
select * from metadata, data, additionalmetadatatable where metadata.owner = 'logged-in user' and metadata.id = additionalmetadatatable.id and metadata.userdataID = data.id
```

#### ユーザーデータの削除 {#delete-user-data-1}

ログインしたユーザーのドラフトと送信データをデータベーステーブルから削除するには、次のデータベースコマンドを実行します。 クエリで、`logged-in user` を、削除するデータのユーザー ID または匿名ユーザーの `anonymous` と置き換えます。匿名ユーザーのデータをデータベースから削除するには、識別可能な情報を使用してデータを検索し、その情報が含まれるデータベーステーブルからデータを削除する必要があります。

```sql
DELETE FROM metadata, data, additionalmetadatatable USING metadata INNER JOIN data ON metadata.userdataID = data.id INNER JOIN additionalmetadatatable ON metadata.id = additionalmetadatatable.id WHERE metadata.owner = 'logged-in user'
```
