---
title: コミュニティグループの基本事項
seo-title: Community Group Essentials
description: コミュニティサイトの動的な作成
seo-description: Creating community sites dynamically
uuid: 168e7aeb-6e9a-468d-8ac4-274007cea252
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.4/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 4f85cd3c-5158-4f23-abe2-7e375fd0c8d4
exl-id: 357a130a-af60-4e86-9161-5dc7056aa052
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '418'
ht-degree: 4%

---

# コミュニティグループの基本事項 {#community-group-essentials}

コミュニティグループ機能を使用すると、パブリッシュ環境およびオーサー環境から許可されたユーザーがコミュニティサイト内でサブコミュニティを動的に作成できます。

コミュニティの時点 [機能パック 1](deploy-communities.md#latestfeaturepack)の場合、グループを他のグループ内にネストすることが可能です

## クライアント側の基本事項 {#essentials-for-client-side}

### コミュニティグループメンバーリスト {#community-groups-member-list}

<table> 
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td> 
   <td>social/group/components/hbs/communitygroupmemberlist</td> 
  </tr>
  <tr>
   <td> <a href="clientlibs.md"><strong>clientllibs</strong></a></td> 
   <td>cq.social.hbs.communitygroups</td> 
  </tr>
  <tr>
   <td> <strong>テンプレート</strong></td> 
   <td> /libs/social/group/components/hbs/communitygroupmemberlist/communitygroupmemberlist.hbs<br /> </td> 
  </tr>
  <tr>
   <td> <strong>css</strong></td> 
   <td> /libs/social/group/components/hbs/communitygroupmemberlist/clientlibs/memberList.css</td> 
  </tr>
  <tr>
   <td><strong>properties</strong></td> 
   <td>詳しくは、 <a href="creating-groups.md">コミュニティグループ</a></td> 
  </tr>
 </tbody>
</table>

### コミュニティグループ {#community-groups}

<table> 
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td> 
   <td>social/group/components/hbs/communitygroups</td> 
  </tr>
  <tr>
   <td> <a href="clientlibs.md"><strong>clientllibs</strong></a></td> 
   <td>cq.social.hbs.communitygroups</td> 
  </tr>
  <tr>
   <td> <strong>テンプレート</strong></td> 
   <td> /libs/social/group/components/hbs/communitygroups/communitygroups.hbs<br /> </td> 
  </tr>
  <tr>
   <td> <strong>css</strong></td> 
   <td> /libs/social/group/components/hbs/communitygroupmemberlist/clientlibs/communitygroups.css</td> 
  </tr>
 </tbody>
</table>

* [クライアント側のカスタマイズ](client-customize.md)

## サーバー側の基本事項 {#essentials-for-server-side}

* [コミュニティグループ API](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/group/client/api/package-summary.html)

* [コミュニティグループエンドポイント](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/group/client/endpoints/package-summary.html)

* [サーバー側のカスタマイズ](server-customize.md)

### グループ機能 {#groups-function}

を含むコミュニティサイト構造 [グループ機能](functions.md#groups-function) は、 `community groups` パブリッシュ環境およびオーサー環境から。 作成したコミュニティグループには、 `community groups member list` グループのメンバーをリストするコンポーネント。

1 つ以上 [コミュニティグループテンプレート](tools-groups.md)（コミュニティグループページのデザインを提供）は、機能を [コミュニティサイトテンプレート](sites.md) またはコミュニティグループテンプレート内にネストされている

複数のコミュニティグループテンプレートを組み込むと、コミュニティサイト用に新しいコミュニティグループを作成する際に、承認済みユーザーに提示するデザインを選択できます (「 [コミュニティグループ](creating-groups.md) 作成者向け

### ネストされたグループ {#nested-groups}

コミュニティの時点 [FP1](deploy-communities.md#latestfeaturepack)を使用すると、グループ機能をグループテンプレート内に組み込むことができ、ネストされたグループ（サブコミュニティ）に対して使用できます。

コミュニティサイトまたはグループテンプレートにグループ機能が含まれている場合は、次の操作が可能です。

* オーサー環境にサブコミュニティを作成する
* 許可するように設定されている場合は、パブリッシュ環境でグループを作成します。

オーサー環境でグループを作成する場合は、まずコミュニティサイトを公開し、次にグループを公開する必要があります。 コミュニティサイトを公開すると、ACL が設定されているサブコミュニティのメンバーグループを作成せずに、グループのページが公開されます。 したがって、制限付き（シークレット）グループは、グループが明示的に公開されるまで表示される場合があります。

## リンクと関連情報 {#links-and-related-information}

* [ユーザーとユーザーグループの管理](users.md)
* [コミュニティグループコンソール](groups.md)
* [グループ機能](functions.md#groups-function)
* [グループテンプレート](tools-groups.md)
