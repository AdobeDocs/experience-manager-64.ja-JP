---
title: カレンダーの基本事項
seo-title: Calendar Essentials
description: カレンダー機能の概要
seo-description: Calendar feature overview
uuid: 14ff7a83-b2a7-4f7e-8ee7-88f336329a1a
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.4/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 88932a3c-ba7f-47ba-9e0b-206755c2d42e
exl-id: cdf5e5d3-a78c-4f32-ad40-665876392a97
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '252'
ht-degree: 7%

---

# カレンダーの基本事項 {#calendar-essentials}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

このページでは、カレンダー機能の使用に関する重要な情報を提供します。

## クライアント側の基本事項 {#essentials-for-client-side}

<table> 
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td> 
   <td>social/calendar/components/hbs/calendar</td> 
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>包含可能な</strong></a></td> 
   <td>いいえ</td> 
  </tr>
  <tr>
   <td> <a href="client-customize.md#clientlibs-for-scf"><strong>clientllibs</strong></a></td> 
   <td>cq.social.hbs.calendar</td> 
  </tr>
  <tr>
   <td> <strong>テンプレート</strong></td> 
   <td>/libs/social/calendar/components/hbs/calendar/calendar.hbs</td> 
   <td> </td> 
  </tr>
  <tr>
   <td> <strong>css</strong></td> 
   <td>/libs/social/calendar/components/hbs/calendar/clientlibs/css/calendar.css<br /> /libs/social/calendar/components/hbs/calendar/clientlibs/css/jqueryui.css</td> 
  </tr>
  <tr>
   <td><strong> properties</strong></td> 
   <td>参照 <a href="calendar.md">カレンダーの使用</a></td> 
  </tr>
 </tbody>
</table>

* [クライアント側のカスタマイズ](client-customize.md)

## サーバー側の基本事項 {#essentials-for-server-side}

* [カレンダー API](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/calendar/client/api/package-summary.html)

* [カレンダーエンドポイント](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/calendar/client/endpoints/package-summary.html)

* [サーバー側のカスタマイズ](server-customize.md)

### カレンダー機能 {#calendar-function}

を含むコミュニティサイト構造 [カレンダー関数](functions.md#calendar-function) が設定されます。 `alendar`コンポーネント。 カレンダー関数は、 [権限を持つメンバーユーザーグループ](users.md#privileged-members-group).

### カレンダー投稿 (UGC) へのアクセス {#accessing-calendar-posts-ugc}

AEM 6.1 Communities 以降では、 [共通店](working-with-srp.md) UGC の場合は、選択したストレージオプション（ASRP、MSRP、JSRP など）に関係なく、プログラムで UGC にアクセスできます。

**リポジトリ内の UGC の場所と形式は、警告なしで変更される場合があります**.

以下を参照してください。

* [ストレージリソースプロバイダの概要](srp.md)  — 概要とリポジトリ使用の概要
* [SRP と UGC の基本事項](srp-and-ugc.md) - SRP ユーティリティメソッドと例
* [SRP を使用した UGC へのアクセス](accessing-ugc-with-srp.md)  — コーディングガイドライン
* [SocialUtils リファクタリング](socialutils.md)  — 非推奨のユーティリティメソッドを現在の SRP ユーティリティメソッドにマッピングします
