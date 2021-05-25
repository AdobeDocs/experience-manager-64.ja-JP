---
title: Forms Portal | ユーザーデータの処理
seo-title: Forms Portal | ユーザーデータの処理
description: AEM Forms ポータルには、AEM Sites ページにアダプティブフォーム、HTML5 フォームおよびその他のフォームアセットを一覧表示するために使用できるコンポーネントが用意されています。Formsポータルがドラフトフォームおよび送信済みフォームのデータを保存する方法を説明します。 設定済みのデータストアでログインしたユーザーと匿名ユーザーのドラフトおよび送信済みフォームデータにアクセスする方法を詳しく調べ、必要に応じて削除します。
seo-description: AEM Forms ポータルには、AEM Sites ページにアダプティブフォーム、HTML5 フォームおよびその他のフォームアセットを一覧表示するために使用できるコンポーネントが用意されています。Formsポータルがドラフトフォームおよび送信済みフォームのデータを保存する方法を説明します。 設定済みのデータストアでログインしたユーザーと匿名ユーザーのドラフトおよび送信済みフォームデータにアクセスする方法を詳しく調べ、必要に応じて削除します。
uuid: 2ac2b2a9-b603-489a-86b8-a78b697f130d
contentOwner: vishgupt
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.4/FORMS
discoiquuid: 48f841b7-0e7f-4216-9ee8-fb6e843acaf0
role: Administrator
exl-id: 05dbb6ee-09fd-44ee-bb8b-a3f3ebb32f5a
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '980'
ht-degree: 62%

---

# Forms Portal | ユーザーデータの処理 {#forms-portal-handling-user-data}

AEM Forms ポータルには、AEM Sites ページにアダプティブフォーム、HTML5 フォームおよびその他のフォームアセットを一覧表示するために使用できるコンポーネントが用意されています。さらに、ログインしたユーザーのためにドラフトや送信済みのアダプティブフォームおよび HTML5 フォームを表示するように構成することもできます。フォームポータルについて詳しくは、「[ポータル上のフォーム発行の概要](/help/forms/using/introduction-publishing-forms.md)」を参照してください。

ログインしたユーザーがアダプティブフォームをドラフトとして保存したり、送信したりすると、これらのアダプティブフォームが Forms Portal の「ドラフト」タブおよび「送信」タブに表示されます。ドラフトまたは送信済みフォームのデータは、AEM デプロイメント用に構成されたデータストアに格納されます。Forms Portal ページには、匿名ユーザーのドラフトおよび送信は表示されません。ただし、データは構成済みのデータストアに格納されます。詳しくは、「[ドラフトと送信に使用するストレージサービスの設定](/help/forms/using/configuring-draft-submission-storage.md)」を参照してください。

## ユーザーデータとデータストア {#user-data-and-data-stores}

Forms Portal は、次のシナリオではドラフトフォームと送信済みフォームのデータを格納します。

* アダプティブフォームで設定されている送信アクションは、**Forms Portal送信アクション**&#x200B;です。
* **Formsポータル送信アクション**&#x200B;以外の送信アクションの場合、**[!UICONTROL 「フォームポータルにデータを保存]** 」オプションは、アダプティブフォームコンテナの&#x200B;**送信**&#x200B;プロパティで有効になります。

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
   <td>データベーステーブル<code>data</code>、<code>metadata</code>、 <code>additionalmetadata</code></td> 
  </tr> 
 </tbody> 
</table>

## ユーザーデータへのアクセスと削除 {#access-and-delete-user-data}

ログインしたユーザーおよび匿名ユーザーのドラフトと送信済みフォームデータには、設定したデータストアからアクセスし、必要に応じて削除できます。

### AEM インスタンス  {#aem-instances}

ログインしたユーザーと匿名ユーザーのAEMインスタンス（オーサー、パブリッシュまたはリモート）内のすべてのドラフトおよび送信済みフォームデータは、該当するAEMリポジトリの`/content/forms/fp/`ノードに保存されます。 ログインユーザーまたは匿名ユーザーがドラフトを保存したりフォームを送信したりするたびに、（該当する場合は）添付ファイルごとに`draft ID`または`submission ID`、`user data ID`、ランダムな`ID`が生成されます。

#### ユーザーデータへのアクセス {#access-user-data}

ログインしたユーザーがドラフトを保存またはフォームを送信すると、そのユーザー ID を使用して子ノードが作成されます。例えば、ユーザーIDが`srose`であるSarah Roseのドラフトと送信データは、AEMリポジトリの`/content/forms/fp/srose/`ノードに保存されます。 このユーザー ID ノード内では、データが階層構造で整理されます。

次の表は、`srose`によるすべてのドラフトのデータがAEMリポジトリに保存される方法を示しています。

>[!NOTE]
>
>`drafts`のような正確な構造が、`/content/forms/fp/srose/submit/`ノードの下の`srose`の送信済みフォームに複製されます。
>
>`anonymous`ユーザーによるすべてのドラフトと送信は`/content/forms/fp/anonymous/`ノードに格納されます。このノードは、`draft`ノードと`submit`ノードの下に、匿名ユーザーのドラフトと送信をすべて整理します。

| ノード | 説明 |
|---|---|
| `/content/forms/fp/srose/drafts` | ユーザーが作成したすべてのドラフトデータが含まれる |
| `/content/forms/fp/srose/drafts/attachments/` | ドラフト ID に基づいてユーザーのすべての添付ファイルがまとめられる |
| `/content/forms/fp/srose/drafts/attachments/<ID>` | 選択した ID の添付ファイルがバイナリ形式で含まれる |
| `/content/forms/fp/srose/drafts/metadata/` | ドラフトIDに基づいてユーザーのフォームメタデータを整理する |
| `/content/forms/fp/srose/drafts/metadata/<draft ID>` | 選択したドラフト ID のフォームメタデータが含まれる |
| `/content/forms/fp/srose/drafts/data/` | ユーザーデータ ID に基づいてユーザーのフォームデータがまとめられる |
| `/content/forms/fp/srose/drafts/data/<user data ID>` | 選択したユーザーデータ ID のフォームデータがバイナリ形式で含まれる |

#### ユーザーデータの削除 {#delete-user-data}

AEM システムで、ログインしたユーザーのドラフトおよび送信済みフォームに含まれるユーザーデータを完全に削除するには、特定ユーザーの `user ID` ノードを作成者ノードから削除する必要があります。該当するすべてのAEMインスタンスから、手動でデータを削除する必要があります。

すべての匿名ユーザーのドラフトと送信データは、`/content/forms/fp/anonymous`の下の共通の`drafts`ノードと`submit`ノードに保存されます。 匿名ユーザーのデータは、識別情報がない限り検索することはできません。このような場合、AEM リポジトリで匿名ユーザーを特定する情報を検索し、その情報が含まれているノードをすべての AEM インスタンスから手動で削除します。これにより、AEM システムからデータを削除できます。ただし、すべての匿名ユーザーのデータを削除する場合は、`anonymous`ノードを削除して、すべての匿名ユーザーのドラフトおよび送信データを削除できます。

### データベース {#database}

AEM がデータベースにデータを格納するように構成されている場合、Forms Portal のドラフトと送信データは、ログインしたユーザーまたは匿名ユーザーを問わず、次のデータベーステーブルに格納されます。

* data
* メタデータ
* additionalmetadata

#### ユーザーデータへのアクセス  {#access-user-data-1}

ログインしたユーザーおよび匿名ユーザーのドラフトおよび送信データにデータベーステーブルからアクセスするには、次のデータベースコマンドを実行します。クエリで、 `logged-in user`を、アクセスするデータのユーザーIDに置き換えるか、匿名ユーザーの場合は`anonymous`に置き換えます。

```sql
select * from metadata, data, additionalmetadatatable where metadata.owner = 'logged-in user' and metadata.id = additionalmetadatatable.id and metadata.userdataID = data.id
```

#### ユーザーデータの削除 {#delete-user-data-1}

ログインしたユーザーのドラフトおよび送信データをデータベーステーブルから削除するには、次のデータベースコマンドを実行します。クエリで、 `logged-in user`を削除するデータのユーザーIDに置き換えるか、匿名ユーザーの場合は`anonymous`に置き換えます。 匿名ユーザーのデータをデータベースから削除するには、識別可能な情報を使用してデータを検索し、その情報が含まれるデータベーステーブルからデータを削除する必要があります。

```sql
DELETE FROM metadata, data, additionalmetadatatable USING metadata INNER JOIN data ON metadata.userdataID = data.id INNER JOIN additionalmetadatatable ON metadata.id = additionalmetadatatable.id WHERE metadata.owner = 'logged-in user'
```
