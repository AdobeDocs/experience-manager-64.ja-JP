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
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '245'
ht-degree: 26%

---

# コンポーネントおよび機能の基本事項 {#component-function-and-feature-essentials}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

AEM Communitiesの機能を使用するには、サイト訪問者がメンバーになり、 [コミュニティサイト](overview.md#communitiessites) コンテンツを投稿できるようになります。 このように [コミュニティサイトテンプレート](sites.md)（コミュニティサイトの場所） [作成済み](sites-console.md)は、ログイン機能に加え、ユーザープロファイル、メッセージング、検索、モデレート、翻訳を含むように設計されています。

コミュニティサイトは、 [コミュニティグループ機能](functions.md#groups-function) 選択したコミュニティサイトテンプレートに含まれています。

コミュニティのコンポーネント、機能、機能に関する重要な情報へのリンクを次に示します。

## 基本コンポーネント {#base-components}

* [コメント](essentials-comments.md)
* [レビュー](reviews-basics.md)
* [集計](tally.md)

   * [「いいね!」の設定](essentials-liking.md)
   * [レーティング](rating-basics.md)
   * [投票](essentials-voting.md)
   * *投票（利用不可）*

## 関数を持つコンポーネント {#components-with-functions}

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
* [質問と答え](qna-essentials.md) `(QnA)`

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

## Javadocs {#javadocs}

この [オンライン javadoc](../../help/sites-developing/reference-materials.md) AEM 6.3 リリースで使用可能な API を反映しています。\
コミュニティ API は、 `com.adobe.cq.social.*` パッケージ。

各 [機能パック](deploy-communities.md#latestfeaturepack)の場合、javadoc jar が使用可能になります。 詳しくは、 [コミュニティでの Maven の使用](maven.md#javadocs).

## 追加情報 {#additional-information}

* [ソーシャルコンポーネントフレームワーク (SCF)](scf.md)

   * [クライアント側のカスタマイズ](client-customize.md)
   * [サーバー側のカスタマイズ](server-customize.md)
   * [ストレージリソースプロバイダーの概要](srp.md)

* [コーディングのガイドライン](code-guide.md)
* [チュートリアル](tutorials.md)
* [トラブルシューティング](troubleshooting.md)
