---
title: AEM Communities リリースノート
seo-title: AEM Communities
description: Adobe Experience Manager 6.4 Communities 固有のリリースノート。
seo-description: Release notes specific to Adobe Experience Manager 6.4 Communities.
uuid: 2de9f511-2a61-4003-9b2c-d6728bc9d57a
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.4
topic-tags: release-notes
content-type: reference
discoiquuid: 55a0b70e-5212-408b-8560-6e758bd8bb10
exl-id: 3a341e72-01c5-4c63-8942-6320e5b08440
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '317'
ht-degree: 76%

---

# AEM Communities リリースノート {#aem-communities-release-notes}

この節では、AEM Communities の 6.3 リリース以降の改善点について説明します。新機能について詳しくは、 [AEM 6.4 Communities の新機能](/help/communities/whats-new-aem-communities.md).

最新リリースを入手するには、このドキュメントの [Communities のデプロイ](/help/communities/deploy-communities.md#latest-releases)の節を参照してください。

## 主な改善点 {#main-improvements}

コミュニティサイト：

* コミュニティ管理者は、次の操作を実行できます。

   * コミュニティサイトを完全に削除
   * コンテキスト対応のコミュニティサイト設定フォルダーを選択

コミュニティグループ：

* コミュニティ管理者は、次の操作を実行できます。

   * コミュニティグループを完全に削除
   * 複数の言語でのコミュニティグループの作成
   * コミュニティグループ内に実施可能カタログおよび割り当てを追加

* イネーブルメントマネージャーは以下をおこなえるようになりました。

   * コミュニティグループ内にリソースと学習パスを作成して割り当て

ファイルライブラリ：

* コミュニティメンバーはファイルライブラリへのいくつかの機能強化（ソート順序、タグ付けなど）を利用できるようになりました。

通知:

* モデレートプロセスを経た投稿が承認されたときに、コミュニティメンバーが通知を受け取るようになりました。

モデレート：

* 自動スパム検出フィルター
* コミュニティモデレーターが使用できるモデレートフィルターが追加されました（回答済み／未回答の質問など）。
* コミュニティモデレーターはモデレートを定義済みのフィルター（承認保留中のすべての投稿など）にブックマークまたはリンクできます。

AEM 6.4 における基盤の変更と完全に互換性があります。

注意：これらの機能はすべてAEM 6.3 でも利用できます。AEM Communitiesのリリースノートで [6.3](https://helpx.adobe.com/jp/experience-manager/6-3/release-notes.html).

## 既知の問題 {#known-issues}

* **モデレート**：一括モデレート UI から 1 回の削除操作で親投稿を削除できない（CQ-4236797）
* **コンソール** - 「ユーザー名またはパスワードを忘れた場合」リンクが、対応するパスワード取得フォームの代わりにログインページにリダイレクトされています (CQ-4237682)

## 高度な機能 {#select-features}

エキスパートスコアリング（*Adobe Sensei を利用*）を使用すると、ゲーミフィケーションを有効にすることができます。これは、コミュニティでの有益な行動を奨励し、それに報いる効果的な手段です。また、レコメンデーションやマーケティングの目的で、エキスパートを識別するために使用することもできます。

## デモ {#demonstrations}

これらの機能はすべて、GitHub.com で公開されている [AEM のデモマシン](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki)を使用して AEM Communities のデモシナリオで試すことができます。また、新しい We.Retail のリファレンス実装内でも試すことができます。
