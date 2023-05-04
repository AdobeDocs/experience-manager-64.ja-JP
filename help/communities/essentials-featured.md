---
title: おすすめコンテンツの基本事項
seo-title: Featured Content Essentials
description: フィーチャコンテンツの操作
seo-description: Working with feature content
uuid: b376828a-1431-4d16-ad6b-b23a3ea62a75
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.4/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 781625f1-39a0-4e34-948c-d4eab35dd5c1
exl-id: 4805db0f-18d2-4bbc-a4d6-eaafa7a4c152
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '142'
ht-degree: 14%

---

# おすすめコンテンツの基本事項 {#featured-content-essentials}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

このページでは、おすすめコンテンツを扱う際に必要な情報を紹介します。

フォーラムの上部に投稿を固定するのとは異なり、この機能を使用すると、コミュニティサイト内の任意の場所でコンテンツをハイライト表示できます。

## クライアント側の基本事項 {#essentials-for-client-side}

<table> 
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td> 
   <td>social/commons/components/hbs/featuredcontent</td> 
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>包含可能な</strong></a></td> 
   <td>いいえ</td> 
  </tr>
  <tr>
   <td> <a href="clientlibs.md"><strong>clientllibs</strong></a></td> 
   <td> <i>default</i></td> 
  </tr>
  <tr>
   <td> <strong>テンプレート</strong></td> 
   <td> /libs/social/commons/components/hbs/featuredcontent/featuredcontent.hbs<br /> /libs/social/commons/components/hbs/featuredtopic/featuredtopic.hbs</td> 
  </tr>
  <tr>
   <td> <strong>css</strong></td> 
   <td> /libs/social/commons/components/hbs/featuredcontent/clientlibs/featuredcontent.css</td> 
  </tr>
  <tr>
   <td><strong> properties</strong></td> 
   <td>詳しくは、 <a href="featured.md">おすすめコンテンツ</a></td> 
  </tr>
 </tbody>
</table>

* [クライアント側のカスタマイズ](client-customize.md)

### ファイルライブラリ機能 {#file-library-function}

を含むコミュニティサイト構造 [おすすめコンテンツ機能](functions.md#featured-content-function)（設定済みを含む） `featured content` コンポーネント。
