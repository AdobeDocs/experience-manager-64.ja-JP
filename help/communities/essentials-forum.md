---
title: フォーラムの基本事項
seo-title: フォーラムの基本事項
description: フォーラムの概要
seo-description: フォーラムの概要
uuid: 68849582-8742-40be-9e7e-0b574ae38815
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.4/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 059c5bbe-07eb-4873-8157-2196df887b27
exl-id: 6562a440-887e-4a48-a14e-64dc36c70793
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '257'
ht-degree: 56%

---

# フォーラムの基本事項 {#forum-essentials}

このページでは、フォーラム機能の操作に関する基本情報をまとめています。

## クライアント側の基本事項  {#essentials-for-client-side}

<table> 
 <tbody>
  <tr>
   <td> <strong>resourceTypes</strong></td> 
   <td>social/forum/components/hbs/forum<br /> social/forum/components/hbs/topic<br /> social/forum/components/hbs/post</td> 
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>インクルード可能</strong></a></td> 
   <td>不可</td> 
  </tr>
  <tr>
   <td> <a href="clientlibs.md"><strong>clientllibs</strong></a></td> 
   <td>cq.ckeditor<br /> cq.social.hbs.voting<br /> cq.social.hbs.forum</td> 
  </tr>
  <tr>
   <td> <strong>テンプレート</strong></td> 
   <td> /libs/social/forum/components/hbs/forum/forum.hbs<br /> /libs/social/forum/components/hbs/post/post.hbs<br /> /libs/social/forum/components/hbs/topic/topic.hbs<br /> /libs/social/forum/components/hbs/topic/list-item.hbs<br /> </td> 
  </tr>
  <tr>
   <td> <strong>css</strong></td> 
   <td> /libs/social/forum/components/hbs/forum/clientlibs/forum.css</td> 
  </tr>
  <tr>
   <td><strong> properties</strong></td> 
   <td><a href="forum.md">フォーラム機能</a>を参照</td> 
  </tr>
 </tbody>
</table>

* [クライアント側のカスタマイズ](client-customize.md)

## サーバー側の基本事項 {#essentials-for-server-side}

* [フォーラム API](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/forum/client/api/package-summary.html)

* [フォーラムエンドポイント](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/forum/client/endpoints/package-summary.html)

* [サーバー側のカスタマイズ](server-customize.md)

### フォーラム機能 {#forum-function}

[フォーラム機能](functions.md#forum-function)を含むコミュニティサイト構造には、設定済みの`forum`コンポーネントのほか、モデレート、タグ付け、翻訳に影響する設定が含まれます。

### フォーラム投稿(UGC)へのアクセス{#accessing-forum-posts-ugc}

UGC は、標準モデレート方法のいずれかを使用してモデレートする必要があります。\
[ユーザー生成コンテンツのモデレート](moderate-ugc.md)を参照してください。

AEM 6.1 Communities 以降では、UGC の[共通ストア](working-with-srp.md)を使用する際に、選択されたストレージオプション（ASRP、MSRP、JSRP など）に関係なく、プログラムによって UGC にアクセスする必要があります。

**リポジトリ内の UGC の場所と形式は予告なく変更されることがあります**。

次のページを参照してください。

* [ストレージリソースプロバイダーの概要](srp.md) - 序論とリポジトリの使用方法の概要
* [SRPとUGCの基本事項](srp-and-ugc.md) - SRPユーティリティメソッドと例
* [SRPによるUGCへのアクセス](accessing-ugc-with-srp.md)  — コーディングのガイドライン
* [SocialUtils のリファクタリング](socialutils.md) - 廃止されたユーティリティメソッドと現在の SRP ユーティリティメソッドの対応関係
