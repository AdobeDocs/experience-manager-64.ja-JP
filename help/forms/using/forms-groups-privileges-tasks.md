---
title: OSGi 上の AEM Forms のグループと権限
seo-title: AEM Forms on OSGi Groups and Privileges
description: ユーザーをグループに割り当てることによる OSGi 上の AEM Forms の管理
seo-description: Assign users to the groups to manage AEM Forms on OSGi
uuid: 9ebb3a4e-4c0e-4105-921f-58077fc45281
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.4/FORMS
content-type: reference
topic-tags: Configuration
discoiquuid: 71412f5d-ff34-415f-baf8-d300756b93a9
role: Admin
exl-id: a79e863e-c316-422e-a565-b0ffdeffcc00
source-git-commit: 3c050c33a384d586d74bd641f7622989dc1d6b22
workflow-type: tm+mt
source-wordcount: '254'
ht-degree: 99%

---

# OSGi 上の AEM Forms のグループと権限 {#aem-forms-on-osgi-groups-and-privileges}

ユーザーをグループに割り当てることによる OSGi 上の AEM Forms の管理

AEM では、[グループを作成](/help/sites-administering/user-group-ac-admin.md#group-administration)してそのグループにポリシーと[ユーザー](/help/sites-administering/user-group-ac-admin.md#user-administration)を割り当てることができます。これらのポリシーは、グループに含まれるユーザーの権限を制御します。

[AEM Forms アドオンパッケージ](/help/forms/using/installing-configuring-aem-forms-osgi.md)をインストールすると、この記事に記載されている forms-user や forms-power-user などのグループは、自動的に割り当て可能になります。次の表に、ユーザーが OSGi 上の AEM Forms でグループの割り当てに基づいて実行できるタスクを示します。

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
     <li>アダプティブフォームを作成、プレビュー、パブリッシュ、送信する</li> 
     <li>インタラクティブ通信とドキュメントフラグメントを作成、プレビュー、パブリッシュする</li> 
     <li>AEM インスタンスにアセットをアップロードする</li> 
     <li>テーマを作成する</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>forms-power-users</td> 
   <td>
    <ul> 
     <li>アダプティブフォームを作成、プレビュー、パブリッシュ、送信する</li> 
     <li>インタラクティブ通信とドキュメントフラグメントを作成、プレビュー、パブリッシュする</li> 
     <li>コードエディターを使用してアダプティブフォームのスクリプトを作成する</li> 
     <li>スクリプトを含むアセットをアップロードする</li> 
     <li>テーマを作成する</li> 
     <li>XDP を含むパッケージを読み込む</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>forms-submission-reviewers</td> 
   <td>
    <ul> 
     <li>送信されたフォームをレビューする</li> 
     <li>送信されたフォームを承認または拒否する</li> 
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
   <td><p>FDM 作成者</p> </td> 
   <td>
    <ul> 
     <li>フォームデータモデルを作成および変更する</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>cm-user-agent</td> 
   <td>
    <ul> 
     <li>エージェント UI を使用して Correspondence Management レターまたはインタラクティブ通信にアクセスする</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td><p>ワークフロー編集者</p> </td> 
   <td>
    <ul> 
     <li>インボックスアプリケーションを作成する</li> 
     <li>ワークフローモデルを作成する</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>workflow-user</td> 
   <td>
    <ul> 
     <li>AEM インボックスアプリケーションを使用する</li> 
     <li>ワークフローインスタンスを管理する</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>FD 管理者</td> 
   <td>
    <ul> 
     <li>PDF Generator を設定する</li> 
     <li>監視フォルダーを設定する</li> 
     <li>ワークフローアプリケーションを管理する</li> 
    </ul> </td> 
  </tr>
 </tbody>
</table>

1. forms-user グループ権限を持つユーザーは、アダプティブフォームのスクリプトを書くことができません。
1. template-authors グループ権限を持つユーザーは、テンプレートのスクリプトを書くことができません。
