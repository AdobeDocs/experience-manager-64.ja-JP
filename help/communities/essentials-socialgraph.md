---
title: ソーシャルグラフの基本事項
seo-title: Social Graph Essentials
description: フォローコンポーネントとフォローコンポーネントの概要
seo-description: follow component and following component overview
uuid: 8ea33760-62b1-4de2-b07f-bc2417ade156
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.4/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: f8d85d72-0215-4680-a334-e37a530fba58
exl-id: 55aa015e-e0e4-411e-8e28-75006ae3090b
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '305'
ht-degree: 8%

---

# ソーシャルグラフの基本事項 {#social-graph-essentials}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

コミュニティメンバーがフォローする機能 [アクティビティ](essentials-activities.md) それに続くものは、次の 2 つの構成要素を通じて確立されます。

この `follow`コンポーネントは別のリソースに関連付ける必要があります。この関連付けは、 [コミュニティサイト](overview.md#communitiessites).

この `following`コンポーネントは、現在のメンバーをフォローしているメンバー、または現在のメンバーをフォローしているメンバーをリストします。 このメンバー間の関係のソーシャルグラフは、コミュニティサイト用に確立されたユーザープロファイルに含まれます。

## クライアント側の基本事項 {#essentials-for-client-side}

### フォロー {#following}

<table> 
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td> 
   <td>social/socialgraph/components/hbs/relationships</td> 
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>包含可能な</strong></a></td> 
   <td>いいえ</td> 
  </tr>
  <tr>
   <td> <a href="clientlibs.md"><strong>clientllibs</strong></a></td> 
   <td>cq.social.hbs.socialgraph</td> 
  </tr>
  <tr>
   <td> <strong>テンプレート</strong></td> 
   <td> /libs/social/socialgraph/components/hbs/relationships/relationships.hbs</td> 
  </tr>
  <tr>
   <td> <strong>css</strong></td> 
   <td> /libs/social/socialgraph/components/hbs/relationships/clientlibs/relationships.css</td> 
  </tr>
  <tr>
   <td><strong> properties</strong></td> 
   <td>詳しくは、 <a href="socialgraph.md">ソーシャルグラフの使用</a></td> 
  </tr>
  <tr>
   <td><strong> <br /> プロパティ（オプション）</strong></td> 
   <td>
    <ul> 
     <li>名前： <strong><code>outgoing</code></strong></li> 
     <li>型：ブール値</li> 
     <li>値：<br /> 
      <ul> 
       <li><i>true </i>- <code>following</code> コンポーネントは、現在サインインしているメンバーを一覧表示します <code>follows</code></li> 
       <li><i>false </i>- <code>following</code> コンポーネントは次のメンバーをリストします： <code>follow </code>現在サインインしているメンバー</li> 
      </ul> </li> 
    </ul> <p>デフォルトはです。 <i>true</i> を返します。 現在、オーサーモードで編集ダイアログを使用してこのプロパティを設定することはできません。 プロパティを <code>following </code>ノードを使用 <a href="../../help/sites-developing/developing-with-crxde-lite.md">CRXDE|Lite</a>.</p> </td> 
  </tr>
 </tbody>
</table>

### フォロー {#follow}

| **resourceType** | social/socialgraph/components/hbs/following |
|---|---|
| [**包含可能な**](scf.md#add-or-include-a-communities-component) | いいえ |
| **テンプレート** | /libs/social/socialgraph/components/hbs/following/following.hbs |
| **css** | /libs/social/socialgraph/components/hbs/following/clientlibs/following.css |

* [クライアント側のカスタマイズ](client-customize.md)

## サーバー側の基本事項 {#essentials-for-server-side}

* [ソーシャルグラフ API](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/graph/client/api/package-frame.html)

* [ソーシャルグラフエンドポイント](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/graph/client/endpoint/package-frame.html)

* [サーバー側のカスタマイズ](server-customize.md)
