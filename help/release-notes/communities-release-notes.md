---
title: AEM Communities リリースノート
seo-title: AEM Communities
description: Adobe Experience Manager 6.4 Communities 固有のリリースノート
seo-description: Release notes specific to Adobe Experience Manager 6.4 Communities.
uuid: 2de9f511-2a61-4003-9b2c-d6728bc9d57a
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.4
topic-tags: release-notes
content-type: reference
discoiquuid: 55a0b70e-5212-408b-8560-6e758bd8bb10
exl-id: 3a341e72-01c5-4c63-8942-6320e5b08440
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '353'
ht-degree: 12%

---

# AEM Communities リリースノート {#aem-communities-release-notes}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

この節では、6.3 リリース以降のAEM Communitiesの改善点について説明します。 新機能について詳しくは、 [AEM 6.4 Communities の新機能](/help/communities/whats-new-aem-communities.md).

最新リリースを入手するには、このドキュメントの [Communities のデプロイ](/help/communities/deploy-communities.md#latest-releases)の節を参照してください。

## 主な改善点 {#main-improvements}

コミュニティサイト:

* コミュニティ管理者は、次の操作を実行できます。

   * コミュニティサイトを完全に削除
   * コミュニティサイトのコンテキスト対応構成フォルダを選択

コミュニティグループ:

* コミュニティ管理者は、次の操作を実行できます。

   * コミュニティグループを完全に削除
   * 複数の言語でのコミュニティグループの作成
   * コミュニティグループ内にイネーブルメントカタログと割り当てを追加する

* イネーブルメントマネージャが

   * コミュニティグループ内でリソースと学習パスを作成し、割り当てます

ファイルライブラリ:

* コミュニティメンバーに、並べ替え順、タグ付けなど、ファイルライブラリに対する複数の機能強化が加えられました。

通知:

* モデレートプロセスを経た投稿の承認時にコミュニティメンバーに通知が届くようになりました

モデレート:

* 自動スパム検出フィルター
* コミュニティモデレーターには、追加のモデレートフィルターがあります（回答済み/未回答の質問など）
* コミュニティモデレーターは、モデレートを定義済みフィルターにブックマークおよびリンクできます（例：承認待ちのすべての投稿）

AEM 6.4 の基本的な変更との全体的な互換性。

注意：これらの機能はすべてAEM 6.3 でも利用できます。AEM Communitiesのリリースノートで [6.3](https://helpx.adobe.com/jp/experience-manager/6-3/release-notes.html).

## 既知の問題 {#known-issues}

* **モデレート**  — 一括モデレート UI から単一の削除操作として親投稿を削除できない (CQ-4236797)
* **コンソール** - 「ユーザー名またはパスワードを忘れた場合」リンクが、対応するパスワード取得フォームの代わりにログインページにリダイレクトされています (CQ-4237682)

## フィーチャを選択 {#select-features}

エキスパートスコアリング (*Powered by Sensei*) — ゲーミフィケーションを有効にするために使用されます。ゲーミフィケーションは、コミュニティの価値ある行動を奨励し、報奨を与える効果的な方法です。 また、レコメンデーションやマーケティングの目的で、エキスパートを識別するために使用することもできます。

## デモ {#demonstrations}

これらの機能はすべて、 [AEM Demo Machine](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki) AEM Communitiesデモシナリオを使用する場合や、新しい We.Retail 参照実装内で使用する場合に、GitHub.com で一般公開されます。
