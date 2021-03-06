---
title: コンポーネントおよび機能の基本事項
seo-title: Component, Function and Feature Essentials
description: コミュニティサイト、テンプレート、グループの機能
seo-description: How community sites, templates, and groups function
uuid: 6edfca2d-fe5b-4261-b033-51dc2f9dbfd7
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.4/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 2d308756-79d1-4d69-b51c-d4b6e692a137
exl-id: bde29d3a-8bc8-4c30-b764-a2fa1ac34069
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '209'
ht-degree: 70%

---

# コンポーネントおよび機能の基本事項 {#component-function-and-feature-essentials}

サイト訪問者が AEM Communities の機能を使用し、コンテンツを投稿するには、事前にメンバー登録し、[コミュニティサイト](overview.md#communitiessites)にログインする必要があります。このように [コミュニティサイトテンプレート](sites.md)（コミュニティサイトの場所） [作成済み](sites-console.md)は、ログイン機能に加え、ユーザープロファイル、メッセージング、検索、モデレート、翻訳を含むように設計されています。

コミュニティサイトは、 [コミュニティグループ機能](functions.md#groups-function) 選択したコミュニティサイトテンプレートに含まれています。

次のリンクをクリックすると、コミュニティのコンポーネントおよび機能に関する基本情報にアクセスできます。

## 基本コンポーネント {#base-components}

* [コメント](essentials-comments.md)
* [レビュー](reviews-basics.md)
* [集計](tally.md)

   * [「いいね!」の設定](essentials-liking.md)
   * [レーティング](rating-basics.md)
   * [投票](essentials-voting.md)
   * *投票（利用不可）*

## 機能のあるコンポーネント {#components-with-functions}

* [アクティビティストリーム](essentials-activities.md)
* [割り当て](essentials-assignments.md)
* [ブログ](blog-developer-basics.md) ( `Journal`)

* [Calendar](calendar-basics-for-developers.md)
* [カタログ](catalog-developer-essentials.md)
* [おすすめコンテンツ](essentials-featured.md)
* [ファイルライブラリ](essentials-file-library.md)
* [フォーラム](essentials-forum.md)
* [グループ](essentials-groups.md)
* [アイディエーション](ideation.md)
* [リーダーボード](leaderboard.md)
* [質問と回答](qna-essentials.md) `(QnA)`

## 機能 {#features}

* [クライアントライブラリ](clientlibs.md)
* [コミュニティサイト](sites-for-developers.md)
* [コンポーネントの OSGi イベント](events.md)
* [コンポーネントのサイドローディング](sideloading.md)
* [メッセージ](essentials-messaging.md)
* [リッチテキストエディター](rte.md)
* [スコアとバッジ](configure-scoring.md)
* [検索](search-implementation.md)
* [ソーシャルグラフ](essentials-socialgraph.md)
* [ストレージリソースプロバイダ](srp-and-ugc.md) `(SRP)`

* [タグ付け](tag.md)

## Javadoc {#javadocs}

[オンライン javadoc](../../help/sites-developing/reference-materials.md) には、AEM 6.3 リリースで使用できる API が反映されています。\
コミュニティ API は、 `com.adobe.cq.social.*` パッケージ。

各[機能パック](deploy-communities.md#latestfeaturepack)に対し、javadoc jar が提供されます。詳しくは、[Communities 用 Maven の使用](maven.md#javadocs)を参照してください。

## 追加情報 {#additional-information}

* [ソーシャルコンポーネントフレームワーク（SCF）](scf.md)

   * [クライアント側のカスタマイズ](client-customize.md)
   * [サーバー側のカスタマイズ](server-customize.md)
   * [ストレージリソースプロバイダーの概要](srp.md)

* [コーディングのガイドライン](code-guide.md)
* [チュートリアル](tutorials.md)
* [トラブルシューティング](troubleshooting.md)
