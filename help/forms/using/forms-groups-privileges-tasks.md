---
title: OSGi 上の AEM Forms のグループと権限
seo-title: AEM Forms on OSGi Groups and Privileges
description: ユーザーをグループに割り当てて、OSGi 上でAEM Formsを管理する
seo-description: Assign users to the groups to manage AEM Forms on OSGi
uuid: 9ebb3a4e-4c0e-4105-921f-58077fc45281
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.4/FORMS
content-type: reference
topic-tags: Configuration
discoiquuid: 71412f5d-ff34-415f-baf8-d300756b93a9
role: Admin
exl-id: a79e863e-c316-422e-a565-b0ffdeffcc00
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '290'
ht-degree: 29%

---

# OSGi 上の AEM Forms のグループと権限 {#aem-forms-on-osgi-groups-and-privileges}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

ユーザーをグループに割り当てて、OSGi 上でAEM Formsを管理する

以下が可能です。 [グループを作成](/help/sites-administering/user-group-ac-admin.md#group-administration) およびポリシーを割り当てます。 [ユーザー](/help/sites-administering/user-group-ac-admin.md#user-administration) をAEMのグループに追加します。 これらのポリシーは、グループに属するユーザーの権限を制御します。

インストール後 [AEM Formsアドオンパッケージ](/help/forms/using/installing-configuring-aem-forms-osgi.md)この記事に記載されているグループ（ forms-user や forms-power-user など）は、自動的に割り当てに使用できます。 次の表に、ユーザーが OSGi 上の AEM Forms でグループの割り当てに基づいて実行できるタスクを示します。

<table> 
 <tbody>
  <tr>
   <td>グループ</td> 
   <td>タスク</td> 
  </tr>
  <tr>
   <td>forms-user <sup>[1]</sup></td> 
   <td>
    <ul> 
     <li>アダプティブフォームの作成、プレビュー、公開、送信</li> 
     <li>インタラクティブ通信とドキュメントフラグメントを作成、プレビュー、公開する</li> 
     <li>アセットのAEMインスタンスへのアップロード</li> 
     <li>テーマを作成</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>forms-power-users</td> 
   <td>
    <ul> 
     <li>アダプティブフォームの作成、プレビュー、公開、送信</li> 
     <li>インタラクティブ通信とドキュメントフラグメントを作成、プレビュー、公開する</li> 
     <li>コードエディターを使用してアダプティブフォームのスクリプトを作成する</li> 
     <li>スクリプトを含むアセットのアップロード</li> 
     <li>テーマを作成</li> 
     <li>XDP を含むパッケージのインポート</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>forms-submission-reviewers</td> 
   <td>
    <ul> 
     <li>送信をレビュー</li> 
     <li>送信を承認または却下</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>template-authors <sup>[2]</sup></td> 
   <td>
    <ul> 
     <li>アダプティブフォームやインタラクティブ通信テンプレートを作成およびプレビューする</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td><p>fdm-authors</p> </td> 
   <td>
    <ul> 
     <li>フォームデータモデルを作成および変更</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>cm-user-agent</td> 
   <td>
    <ul> 
     <li>エージェント UI を使用して Correspondence Management レターまたはインタラクティブ通信にアクセス</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td><p>workflow-editors</p> </td> 
   <td>
    <ul> 
     <li>インボックスアプリケーションの作成</li> 
     <li>ワークフローモデルを作成</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>workflow-user</td> 
   <td>
    <ul> 
     <li>AEMインボックスアプリケーションの使用</li> 
     <li>ワークフローインスタンスを管理</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>fd-administrators</td> 
   <td>
    <ul> 
     <li>PDF Generator を設定</li> 
     <li>監視フォルダーを設定</li> 
     <li>ワークフローアプリケーションを管理する</li> 
    </ul> </td> 
  </tr>
 </tbody>
</table>

1. forms-user グループ権限を持つユーザーは、アダプティブフォームのスクリプトを作成できません。
1. template-authors グループ権限を持つユーザーは、テンプレートのスクリプトを書くことができません。
