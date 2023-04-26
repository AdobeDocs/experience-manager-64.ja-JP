---
title: 「いいね!」の設定の基本事項
seo-title: Liking Essentials
description: 「いいね！」設定コンポーネントの概要
seo-description: Liking component overview
uuid: 89f16859-c901-4090-8e16-363b95c508de
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.4/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: f176c42b-b16b-42c9-af22-4b6421de5a90
pagetitle: Liking Essentials
exl-id: 509d1fb4-a88d-4438-a618-ba063adb6fb9
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '290'
ht-degree: 2%

---

# 「いいね!」の設定の基本事項 {#liking-essentials}

「いいね！」設定コンポーネント、 [集計](tally.md) サブクラスは、メンバーがハートアイコンを選択するだけで、コンテンツの特定の部分に関する肯定的な意見を表すのに役立つツールです。

「いいね！」設定コンポーネントの複数のインスタンスを同じページに配置することができます。各インスタンスは、一意の `tally name` プロパティ。

「いいね！」の匿名投稿はサポートされていません。 サイト訪問者が「いいね！」に参加するには、登録してサインインする必要があります。 サインインした訪問者（メンバー）は、いつでも、「いいね！」のオンとオフを切り替えることができます。

## クライアント側の基本事項 {#essentials-for-client-side}

<table> 
 <tbody> 
  <tr> 
   <td> <strong>resourceType</strong></td> 
   <td>social/tally/components/hbs/liking</td> 
  </tr> 
  <tr> 
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>包含可能な</strong></a></td> 
   <td>はい — でプロパティを編集できます <i>デザイン </i>mode</td> 
  </tr> 
  <tr> 
   <td> <a href="client-customize.md#clientlibs-for-scf"><strong>clientlibs</strong></a></td> 
   <td> cq.social.hbs.liking</td> 
  </tr> 
  <tr> 
   <td> <strong>テンプレート</strong></td> 
   <td><p> /libs/social/tally/components/hbs/liking/liking.hbs<br /> /libs/social/tally/components/hbs/liking/activity-icon.hbs<br /> /libs/social/tally/components/hbs/liking/activity-title.hbs</p> </td> 
  </tr> 
  <tr> 
   <td><strong>CSS</strong></td> 
   <td> /libs/social/tally/components/hbs/liking/clientlibs/likingcomponent.css</td> 
  </tr> 
  <tr> 
   <td><strong>properties</strong></td> 
   <td><p>詳しくは、 <a href="liking.md">「いいね！」の使用</a></p> </td> 
  </tr> 
 </tbody> 
</table>

* [クライアント側のカスタマイズ](client-customize.md)

## サーバー側の基本事項 {#essentials-for-server-side}

* [集計 API](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/tally/client/api/package-summary.html)

* [集計エンドポイント](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/tally/client/endpoints/package-summary.html)

* [サーバー側のカスタマイズ](server-customize.md)

### 投稿された投票 (UGC) へのアクセス {#accessing-posted-voting-ugc}

UGC は、モデレートの標準的な方法の 1 つを使用してモデレートする必要があります。\
詳しくは、 [ユーザー生成コンテンツのモデレート](moderate-ugc.md).

AEM 6.1 Communities 以降では、 [共通店](working-with-srp.md) UGC の場合は、選択したストレージオプション（ASRP、MSRP、JSRP など）に関係なく、プログラムで UGC にアクセスできます。

**リポジトリ内の UGC の場所と形式は、警告なしで変更される場合があります**.

以下を参照してください。

* [ストレージリソースプロバイダの概要](srp.md)  — 概要とリポジトリ使用の概要
* [SRP と UGC の基本事項](srp-and-ugc.md) - SRP ユーティリティメソッドと例
* [SRP を使用した UGC へのアクセス](accessing-ugc-with-srp.md)  — コーディングガイドライン
* [SocialUtils リファクタリング](socialutils.md)  — 非推奨のユーティリティメソッドを現在の SRP ユーティリティメソッドにマッピングします
