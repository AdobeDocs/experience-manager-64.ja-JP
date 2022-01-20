---
title: Forms Portal | ユーザーデータの処理
seo-title: Forms Portal | Handling user data
description: AEM Forms ポータルには、AEM Sites ページにアダプティブフォーム、HTML5 フォームおよびその他のフォームアセットを一覧表示するために使用できるコンポーネントが用意されています。Formsポータルでドラフトフォームと送信済みフォームのデータを保存する方法を説明します。 設定済みのデータストアでログインしたユーザーと匿名ユーザーのドラフトおよび送信済みフォームデータにアクセスする方法と、必要に応じて削除する方法について詳しく説明します。
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
ht-degree: 63%

---

# Forms Portal | ユーザーデータの処理 {#forms-portal-handling-user-data}

AEM Forms ポータルには、AEM Sites ページにアダプティブフォーム、HTML5 フォームおよびその他のフォームアセットを一覧表示するために使用できるコンポーネントが用意されています。さらに、ログインしたユーザーのためにドラフトや送信済みのアダプティブフォームおよび HTML5 フォームを表示するように構成することもできます。フォームポータルについて詳しくは、 [ポータル上のフォーム発行の概要](/help/forms/using/introduction-publishing-forms.md).

ログインしたユーザーがアダプティブフォームをドラフトとして保存したり、送信したりすると、これらのアダプティブフォームが Forms Portal の「ドラフト」タブおよび「送信」タブに表示されます。ドラフトまたは送信済みフォームのデータは、AEM デプロイメント用に構成されたデータストアに格納されます。Forms Portal ページには、匿名ユーザーのドラフトおよび送信は表示されません。ただし、データは構成済みのデータストアに格納されます。詳しくは、「[ドラフトと送信に使用するストレージサービスの設定](/help/forms/using/configuring-draft-submission-storage.md)」を参照してください。

## ユーザーデータとデータストア {#user-data-and-data-stores}

Forms Portal は、次のシナリオではドラフトフォームと送信済みフォームのデータを格納します。

* アダプティブフォームで設定された送信アクションは次のとおりです。 **Forms Portal 送信アクション**.
* 次以外の送信アクション： **Forms Portal 送信アクション**、 **[!UICONTROL フォームポータルにデータを保存する]** オプションは **送信** アダプティブフォームコンテナのプロパティ。

ログインしたユーザーと匿名ユーザーのすべてのドラフトと送信済みフォームの場合、Forms Portal には次のデータが格納されます。

* フォーム名、フォームパス、ドラフトまたは送信 ID、添付ファイルのパス、ユーザーデータ ID などのフォームメタデータ
* データバイトとしてのフォーム添付ファイル
* データバイトとしてのフォームデータ

設定されたデータストアの永続性に応じて、ドラフトおよび送信済みフォームデータは次の場所に格納されます。

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>永続性タイプ</strong></p> </td> 
   <td><p><strong>データストア</strong></p> </td> 
   <td><p><strong>場所</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>デフォルト</p> </td> 
   <td><p>オーサーインスタンスおよび発行インスタンスの AEM リポジトリ</p> </td> 
   <td><p><code>/content/forms/fp/</code></p> </td> 
  </tr> 
  <tr> 
   <td><p>リモート</p> </td> 
   <td><p>オーサーインスタンスおよびリモート AEM インスタンスの AEM リポジトリ</p> </td> 
   <td><p><code>/content/forms/fp/</code></p> </td> 
  </tr> 
  <tr> 
   <td><p>データベース</p> </td> 
   <td><p>オーサーインスタンスおよびデータベーステーブルの AEM リポジトリ</p> </td> 
   <td>データベーステーブル <code>data</code>, <code>metadata</code>、および <code>additionalmetadata</code></td> 
  </tr> 
 </tbody> 
</table>

## ユーザーデータへのアクセスと削除 {#access-and-delete-user-data}

ログインしたユーザーおよび匿名ユーザーのドラフトと送信済みフォームデータには、設定したデータストアからアクセスし、必要に応じて削除できます。

### AEM インスタンス {#aem-instances}

ログインしたユーザーと匿名ユーザーのAEMインスタンス（作成者、発行またはリモート）のすべてのドラフトおよび送信済みフォームデータは、 `/content/forms/fp/` 該当するAEMリポジトリのノード。 ログインしたユーザーまたは匿名ユーザーが下書きを保存したりフォームを送信したりするたびに、 `draft ID` または `submission ID`, a `user data ID`、およびランダム `ID` 各添付ファイル（該当する場合）が生成され、それぞれのドラフトまたは送信に関連付けられます。

#### ユーザーデータへのアクセス {#access-user-data}

ログインしたユーザーがドラフトを保存またはフォームを送信すると、そのユーザー ID を使用して子ノードが作成されます。例えば、Sarah Rose のドラフトと送信データのユーザー ID が `srose` が `/content/forms/fp/srose/` AEMリポジトリのノード。 このユーザー ID ノード内では、データが階層構造で整理されます。

次の表で、すべてのドラフトのデータを `srose` はAEMリポジトリに保存されます。

>[!NOTE]
>
>のような正確な構造 `drafts` は次の送信済みフォームに対してレプリケートされます： `srose` の下に `/content/forms/fp/srose/submit/` ノード。
>
>すべてのドラフトと送信者 `anonymous` ユーザーは、 `/content/forms/fp/anonymous/` ノード。匿名ユーザーのすべてのドラフトと送信を、 `draft` および `submit` ノード。

| ノード | 説明 |
|---|---|
| `/content/forms/fp/srose/drafts` | ユーザーが作成したすべてのドラフトデータが含まれる |
| `/content/forms/fp/srose/drafts/attachments/` | ドラフト ID に基づいてユーザーのすべての添付ファイルがまとめられる |
| `/content/forms/fp/srose/drafts/attachments/<ID>` | 選択した ID の添付ファイルがバイナリ形式で含まれる |
| `/content/forms/fp/srose/drafts/metadata/` | 下書き ID に基づいてユーザーのフォームメタデータを整理 |
| `/content/forms/fp/srose/drafts/metadata/<draft ID>` | 選択したドラフト ID のフォームメタデータが含まれる |
| `/content/forms/fp/srose/drafts/data/` | ユーザーデータ ID に基づいてユーザーのフォームデータがまとめられる |
| `/content/forms/fp/srose/drafts/data/<user data ID>` | 選択したユーザーデータ ID のフォームデータがバイナリ形式で含まれる |

#### ユーザーデータの削除 {#delete-user-data}

AEM システムで、ログインしたユーザーのドラフトおよび送信済みフォームに含まれるユーザーデータを完全に削除するには、特定ユーザーの `user ID` ノードを作成者ノードから削除する必要があります。該当するすべてのAEMインスタンスから手動でデータを削除する必要があります。

すべての匿名ユーザーのドラフトと送信データは、共通の `drafts` および `submit` の下のノード `/content/forms/fp/anonymous`. 匿名ユーザーのデータは、識別情報がない限り検索することはできません。このような場合、AEM リポジトリで匿名ユーザーを特定する情報を検索し、その情報が含まれているノードをすべての AEM インスタンスから手動で削除します。これにより、AEM システムからデータを削除できます。ただし、匿名ユーザー全員のデータを削除する場合は、 `anonymous` すべての匿名ユーザーのドラフトと送信データを削除するノード。

### データベース {#database}

AEM がデータベースにデータを格納するように構成されている場合、Forms Portal のドラフトと送信データは、ログインしたユーザーまたは匿名ユーザーを問わず、次のデータベーステーブルに格納されます。

* data
* メタデータ
* additionalmetadata

#### ユーザーデータへのアクセス {#access-user-data-1}

ログインしたユーザーおよび匿名ユーザーのドラフトおよび送信データにデータベーステーブルからアクセスするには、次のデータベースコマンドを実行します。クエリで、 `logged-in user` を、アクセスするデータのユーザー ID または `anonymous` 匿名ユーザー向け

```sql
select * from metadata, data, additionalmetadatatable where metadata.owner = 'logged-in user' and metadata.id = additionalmetadatatable.id and metadata.userdataID = data.id
```

#### ユーザーデータの削除 {#delete-user-data-1}

ログインしたユーザーのドラフトおよび送信データをデータベーステーブルから削除するには、次のデータベースコマンドを実行します。クエリで、 `logged-in user` を、削除するまたはを使用するデータのユーザー ID に置き換えます。 `anonymous` 匿名ユーザー向け 匿名ユーザーのデータをデータベースから削除するには、識別可能な情報を使用してデータを検索し、その情報が含まれるデータベーステーブルからデータを削除する必要があります。

```sql
DELETE FROM metadata, data, additionalmetadatatable USING metadata INNER JOIN data ON metadata.userdataID = data.id INNER JOIN additionalmetadatatable ON metadata.id = additionalmetadatatable.id WHERE metadata.owner = 'logged-in user'
```
