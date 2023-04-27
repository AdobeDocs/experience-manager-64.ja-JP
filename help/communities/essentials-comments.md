---
title: コメントの基本事項
seo-title: Comments Essentials
description: コメントコンポーネントの概要
seo-description: Comments component overview
uuid: 58b7bb58-f598-4bcb-93ae-b7795cab51cd
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.4/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 18f54a1c-52aa-414d-b494-1f19b5c10345
exl-id: 3d5396b5-10e5-49bc-aa11-5a3df93d70c3
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '352'
ht-degree: 5%

---

# コメントの基本事項 {#comments-essentials}

このページでは、コメントシステム（コメントコンポーネント）の操作に関する基本事項と、メンバーがコメントや返信を投稿したときに生成されるユーザー生成コンテンツ (UGC) を管理するためのオプションを提供します。

コメントコンポーネントは、個々の投稿がコメントコンポーネント（単数）で表されるようにコメントシステムを確立します。 ページに含まれるコメントシステムです。 コメントシステムは、呼び出されると個々のコメントを作成します。

## クライアント側の基本事項 {#essentials-for-client-side}

<table> 
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td> 
   <td> social/commons/components/hbs/comments</td> 
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>包含可能な</strong></a></td> 
   <td>はい — でプロパティを編集できます <i>デザイン </i>mode</td> 
  </tr>
  <tr>
   <td> <a href="client-customize.md#clientlibs-for-scf"><strong>Clientlibs</strong></a></td> 
   <td>cq.ckeditor<br /> cq.social.hbs.comments<br /> cq.social.hbs.voting</td> 
  </tr>
  <tr>
   <td> <strong>テンプレート</strong></td> 
   <td> /libs/social/commons/components/hbs/comments/comments.hbs<br /> </td> 
  </tr>
  <tr>
   <td> <strong>CSS</strong></td> 
   <td> /libs/social/commons/components/hbs/comments/clientlibs/commentsystem.css</td> 
  </tr>
  <tr>
   <td><strong> properties</strong></td> 
   <td> 詳しくは、 <a href="comments.md">コメントの使用</a></td> 
  </tr>
 </tbody>
</table>

[クライアント側のカスタマイズ](client-customize.md)

### 1 ページにつき 1 つのインスタンス {#one-instance-per-page}

ページネーションおよびキャッシュやリンクに URL を使用する場合、コメントシステムごとに一意の URL を指定する必要があります。 したがって、1 ページにつき 1 つのコメントシステムのインスタンスのみを使用できます。

その他の機能には、既にコメントシステムが含まれています。 以下が該当します。

* [ブログ](blog-developer-basics.md)
* [Calendar](calendar-basics-for-developers.md)
* [ファイルライブラリ](essentials-file-library.md)
* [フォーラム](essentials-forum.md)
* [Q&amp;A](qna-essentials.md)
* [レビュー](reviews-basics.md)

### フラグ設定理由リスト {#flag-reason-list}

フラグ設定の理由リストは、アプリに flagreasonlist.hbs を追加して、内の内容を上書きすることでカスタマイズできます

* /libs/social/commons/components/hbs/comments/comment/flagreasonlist.hbs

これは、コメントシステムを拡張するすべてのコンポーネントに適用されます。

## サーバー側の基本事項 {#essentials-for-server-side}

* [コメント API](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/commons/comments/api/package-summary.html)

* [コメントエンドポイント](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/commons/comments/endpoints/package-summary.html)

* [サーバー側のカスタマイズ](server-customize.md)

### 投稿されたコメント (UGC) へのアクセス {#accessing-posted-comments-ugc}

UGC は、モデレートの標準的な方法の 1 つを使用してモデレートする必要があります。\
詳しくは、 [ユーザー生成コンテンツのモデレート](moderate-ugc.md).

AEM 6.1 Communities 以降では、 [共通店](working-with-srp.md) UGC の場合は、選択したストレージオプション（ASRP、MSRP、JSRP など）に関係なく、プログラムで UGC にアクセスできます。

**リポジトリ内の UGC の場所と形式は、警告なしで変更される場合があります**.

以下を参照してください。

* [ストレージリソースプロバイダの概要](srp.md)  — 概要とリポジトリ使用の概要
* [SRP と UGC の基本事項](srp-and-ugc.md) - SRP ユーティリティメソッドと例
* [SRP を使用した UGC へのアクセス](accessing-ugc-with-srp.md)  — コーディングガイドライン
* [SocialUtils リファクタリング](socialutils.md)  — 廃止されたユーティリティメソッドを現在の SRP ユーティリティメソッドにマッピングする
