---
title: 集計の基本事項
seo-title: Tally Essentials
description: 集計クラスの概要
seo-description: Tally class overview
uuid: c369c6a1-9ced-4b5c-af43-8c03236eaa52
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.4/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 9941ba90-3d40-4c90-bca8-5db49603cbfa
exl-id: f04ec253-08b8-4ee2-9873-4a51549daeba
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '305'
ht-degree: 56%

---

# 集計の基本事項 {#tally-essentials}

集計は、メンバーが特定の製品やサービスをどのように評価するかに関するフィードバックを収集する標準的な方法を提供する抽象クラスです。 匿名フィードバックはサポートされていません。 サイト訪問者が参加するには、登録してサインインし、フィードバックを変更するにはサインインする必要があります。 サインインする必要があるので、モデレートが容易になり、複数の投稿を防ぐことでフィードバックの価値が高まります。

抽象集計クラスを拡張することによってカスタム集計コンポーネントを作成できます。

[「いいね!」の設定](essentials-liking.md)は、肯定的な意見を単純な形式で表す集計実装です。

[投票](essentials-voting.md)は、肯定的な意見または否定的な意見を単純な形式で表す集計実装です。

[評価](rating-basics.md)は、肯定的な意見から否定的な意見まで幅広い意見を星制度で表す集計実装です。

AEM 6.1 以降、 *投票* コンポーネントは使用できなくなりました。

[レビュー](reviews-basics.md) は、 [コメント](essentials-comments.md) および [評価](rating-basics.md).

## クライアント側の基本事項 {#essentials-for-client-side}

* [クライアント側のカスタマイズ](client-customize.md)

## サーバー側の基本事項 {#essentials-for-server-side}

* [集計 API](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/tally/client/api/package-summary.html)

* [集計エンドポイント](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/tally/client/endpoints/package-summary.html)

* [サーバー側のカスタマイズ](server-customize.md)

### 投稿された集計（UGC）へのアクセス {#accessing-posted-tallies-ugc}

UGC は、標準モデレート方法のいずれかを使用してモデレートする必要があります。\
[ユーザー生成コンテンツのモデレート](moderate-ugc.md)を参照してください。

AEM 6.1 Communities 以降では、UGC の[共通ストア](working-with-srp.md)を使用する際に、選択されたストレージオプション（ASRP、MSRP、JSRP など）に関係なく、プログラムによって UGC にアクセスする必要があります。

**リポジトリ内の UGC の場所と形式は予告なく変更されることがあります**。

次のページを参照してください。

* [ストレージリソースプロバイダーの概要](srp.md) - 序論とリポジトリの使用方法の概要
* [SRP と UGC の基本事項](srp-and-ugc.md) - SRP ユーティリティメソッドと例
* [SRP を使用した UGC へのアクセス](accessing-ugc-with-srp.md)  — コーディングガイドライン
* [SocialUtils のリファクタリング](socialutils.md) - 廃止されたユーティリティメソッドと現在の SRP ユーティリティメソッドの対応関係
