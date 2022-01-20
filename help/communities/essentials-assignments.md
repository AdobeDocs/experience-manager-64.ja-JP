---
title: 割り当ての基本事項
seo-title: Assignments Essentials
description: イネーブルメントコミュニティの割り当て機能の概要
seo-description: Assignments feature overview for enablement communities
uuid: 8310decf-174d-4e93-8c92-4a9583077b7a
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.4/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 796781e6-5cab-4ea1-b484-0945bc8febbf
exl-id: 310d9086-36b6-42ea-835f-c77d75e880cb
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '213'
ht-degree: 62%

---

# 割り当ての基本事項 {#assignments-essentials}

このページでは、[イネーブルメントコミュニティ](overview.md#enablement-community)サイトの割り当て機能の操作に関する基本情報をまとめています。

割り当て機能を使用すると、イネーブルメントコミュニティのメンバーに実施可能リソースおよびイネーブルメント学習パスを割り当てることができます。

## クライアント側の基本事項 {#essentials-for-client-side}

<table> 
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td> 
   <td>social/enablement/components/hbs/myassigned</td> 
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>インクルード可能</strong></a></td> 
   <td>不可</td> 
  </tr>
  <tr>
   <td> <a href="clientlibs.md"><strong>clientllibs</strong></a></td> 
   <td>cq.social.enablement.hbs.breadcrumbs<br /> cq.social.enablement.hbs.myassigned<br /> cq.social.enablement.hbs.resource<br /> cq.social.enablement.hbs.learningpath</td> 
  </tr>
  <tr>
   <td> <strong>テンプレート</strong></td> 
   <td> /libs/social/enablement/components/hbs/myassigned/myassigned.hbs</td> 
  </tr>
  <tr>
   <td> <strong>css</strong></td> 
   <td> /libs/social/enablement/components/hbs/myassigned/clientlibs/myassigned.css</td> 
  </tr>
  <tr>
   <td><strong> properties</strong></td> 
   <td>詳しくは、 <a href="assignments.md">割り当て機能</a></td> 
  </tr>
 </tbody>
</table>

### 完了ステータスと成功ステータス {#completion-and-success-status}

完了ステータスと成功ステータスは、割り当てのレポートおよびステータスバナーで使用されます。

完了ステータス：

* 割り当てなし
* 開始されていません（新規）
* 処理中
* 完了

成功ステータス：

* 不明
* パス
* 失敗

完了ステータスと成功ステータスの組み合わせとして有効なものは以下に限られます。

| **完了** | **成功** |
|---|---|
| 開始されていません | 不明 |
| 処理中 | 不明 |
| 完了 | パス |
| 完了 | 失敗 |

## サーバー側の基本事項 {#essentials-for-server-side}

### 割り当て機能 {#assignments-function}

を含むコミュニティサイト構造 [割り当て機能](functions.md#assignments-function)（設定済みを含む） ` [assignments](assignments.md)` コンポーネント。

### リファレンス API {#reference-apis}

* [イネーブルメント API](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/enablement/reporting/model/api/package-summary.html)

* [レポート API](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/reporting/dv/api/package-summary.html)

* [レポート分析 API](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/reporting/analytics/api/package-summary.html)
