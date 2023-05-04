---
title: 評価の基本事項
seo-title: Rating Essentials
description: 評価コンポーネントの概要
seo-description: Rating component overview
uuid: 48ef61ad-be7a-4a6b-a284-23e5bb4f1671
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.4/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 7dc3ef57-05c3-45d4-ace3-bb3ba6ea768b
exl-id: f722051c-9512-4420-b12e-cb20aa6759f7
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '315'
ht-degree: 5%

---

# 評価の基本事項 {#rating-essentials}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

評価コンポーネント、 [集計](tally.md) サブクラスを使用すると、サインインしたコミュニティメンバーが Web サイト上の機能を評価できます。

同じページに投票コンポーネントの複数のインスタンスを配置することができます。各インスタンスは、一意の `tally name` プロパティ。

匿名での評価の投稿はサポートされていません。 サイト訪問者が評価に参加するには、登録してサインインする必要があります。 サインインした訪問者（メンバー）は、いつでも評価を変更できます。

## クライアント側の基本事項 {#essentials-for-client-side}

<table> 
 <tbody> 
  <tr> 
   <td> <strong>resourceType</strong></td> 
   <td> social/tally/components/hbs/rating</td> 
  </tr> 
  <tr> 
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>包含可能な</strong></a></td> 
   <td>はい — でプロパティを編集できます <i>デザイン </i>mode</td> 
  </tr> 
  <tr> 
   <td> <a href="client-customize.md#clientlibs-for-scf"><strong>clientlibs</strong></a></td> 
   <td> cq.social.hbs.rating</td> 
  </tr> 
  <tr> 
   <td> <strong>テンプレート</strong></td> 
   <td><p> /libs/social/tally/components/hbs/rating/rating.hbs<br /> /libs/social/tally/components/hbs/rating/display.hbs<br /> /libs/social/tally/components/hbs/rating/histogram.hbs</p> </td> 
  </tr> 
  <tr> 
   <td><strong>CSS</strong></td> 
   <td> /libs/social/tally/components/hbs/rating/clientlibs/ratingcomponent.css</td> 
  </tr> 
  <tr> 
   <td><strong>properties</strong></td> 
   <td><p>詳しくは、 <a href="rating.md">評価の使用</a></p> </td> 
  </tr> 
 </tbody> 
</table>

* [クライアント側のカスタマイズ](client-customize.md)

## サーバー側の基本事項 {#essentials-for-server-side}

* [集計 API](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/tally/client/api/package-summary.html)

* [集計エンドポイント](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/tally/client/endpoints/package-summary.html)

* [サーバー側のカスタマイズ](server-customize.md)

### 投稿された評価 (UGC) へのアクセス {#accessing-posted-ratings-ugc}

UGC は、モデレートの標準的な方法の 1 つを使用してモデレートする必要があります。\
詳しくは、 [ユーザー生成コンテンツのモデレート](moderate-ugc.md).

AEM 6.1 Communities 以降では、 [共通店](working-with-srp.md) UGC の場合は、選択したストレージオプション（ASRP、MSRP、JSRP など）に関係なく、プログラムで UGC にアクセスできます。

**リポジトリ内の UGC の場所と形式は、警告なしで変更される場合があります**.

以下を参照してください。

* [ストレージリソースプロバイダの概要](srp.md)  — 概要とリポジトリ使用の概要
* [SRP と UGC の基本事項](srp-and-ugc.md) - SRP ユーティリティメソッドと例
* [SRP を使用した UGC へのアクセス](accessing-ugc-with-srp.md)  — コーディングガイドライン
* [SocialUtils リファクタリング](socialutils.md)  — 非推奨のユーティリティメソッドを現在の SRP ユーティリティメソッドにマッピングします
